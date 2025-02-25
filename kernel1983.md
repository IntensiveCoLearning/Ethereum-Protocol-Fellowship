---
timezone: America/New_York
---

# 0xKJ

1. 自我介绍
    - Dr KJ，密码学和共识算法博士，Useful PoW 和 Minus Theory 发现者。
    - 近期向以太坊提出扩容方案 https://ethresear.ch/t/l1-improvement-based-on-minus-theory/21494
    - 由于仅仅熟悉 PoW 以太坊机制，对于 PoS 并不是太理解。所以来补课，并且试图搞清楚以太坊 L1 扩容的可能性和技术细节。

2. 你认为你会完成本次残酷学习吗？
    - 不一定！

## Notes

<!-- Content_START -->

### 2025.02.06

今天是首次参加残酷共学，由于基本上我已经手撸过一个完整的POW区块链了，对以太坊的虚拟机和MPT也有过动手经验，所以这次会主要把注意力放在之前不太熟悉的POS知识上，也希望能结合到代码层面，弥补对 https://github.com/ethereum/go-ethereum 和 https://github.com/prysmaticlabs/prysm 的认知。

今天主要熟悉 The Protocol 部分, 值得一看的主要是 https://epf.wiki/#/wiki/protocol/architecture ，在转向POS之后，仅仅运行geth已经不够，还要结合 prysm 运行 Beacon Node。
第一张图中User APIs可以理解为ETH RPC，以前我实现过 https://github.com/EcoPoW/BitPoW/blob/master/eth_rpc.py

Beacon APIs 和 validator 连接，结合这两天看的油管视频，prysm应该是可以运行成 Beacon Node 或者 validator 模式的，所以这里的 validator 应该是用来验证 POS 谁有权出块的验证，而不是对整个区块链或者 EVM 执行结果的验证。

Engine API 是 geth 和 prysm 之间通信的API，暂时还不知道具体工作内容。但是可以知道，如果 POS 算法得知当前节点现在有出块权，prism 应该第一时间主动通知 geth 切换到出块模式。

代码可以看到 https://github.com/prysmaticlabs/prysm/tree/develop/cmd 有 beacon-chain 和 validator 模式，以及其它模式。每个都会有对应的`main.go`代码。在运行 `func main` 之后进入 `func startNode`，`node.New` 和 `beacon.Start` 之后应该就跳转到https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/node/node.go 去了。

今天就先研究到这里。

### 2025.02.07

从 https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/node/node.go 中的 `beacon.Start` 跳转到
https://github.com/prysmaticlabs/prysm/blob/develop/runtime/service_registry.go#L42 `StartAll`, 这里顺便学习一下 Go 语言的 `go` 关键字用来启动 coroutine。软件工程里的很多东西还真的得有调试环境和 log 才能更容易的学习到。这里光靠读代码已经跟丢了，所以这就是我们未来实现工程需要避免的地方，写普通人能读的代码！尤其是区块链开源。

https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/node/node.go#L203 我们在 `func New` 里找到了 `func registerServices`

休息一下……我们遇到了分叉路口，需要好好思考一下接下来读哪些代码？

直接从名字猜吧：
 * P2P Service 顾名思义，P2P广播网络
 * [Backfill Service](https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/sync/backfill/service.go) 进代码看了一下，好像和slot有关系，也和同步有关系
 * POW Chain Service 向前兼容
 * [Attestation Pool Service](https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/operations/attestations/service.go) 见证，可能和 PoS 有关系
 * Blockchain Service 名字起的太泛泛了
 * Initial Sync Service 首次同步之后要做些什么？
 * Sync Service 很明显
 * [Slashing Pool Service](https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/operations/slashings/service_new.go) 和 POS 质押有关系
 * [Slasher Service](https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/slasher/service.go#L84) 和质押有关系
 * builder service 猜测这里的 builder 就是区块链新 block 的 builder 的意思
 * RPC Service 很好懂
 * HTTP Service 很好懂，可以看看有什么API在里面
 * Validator Monitoring Service 很好懂
 * Pruner Service 历史数据库删除？

经过一下午的研究，我大致确认 Slasher Service 才是我要研究的代码，应该是 PoS 逻辑最主要的部分。
Attestation Pool Service 似乎和区块分叉的选择有关系。
Slashing Pool Service 则是 Slasher Service 的依赖模块。

### 2025.02.08

继续阅读代码，由于没有本地搭建编译和调试环境，所以以阅读为主，不求甚解。

https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/slasher/service.go#L88 首先是这个 `func (s *Service) run()` 阅读这里的逻辑。这里在做并行系统的人，需要有一种代码感受，因为做 beacon 是一个分布式系统，所以 slash 的逻辑需要在很多 beacon nodes 上一起执行，并且得到相同结果。

带着问题去看以上的代码，尝试把关于POS的一些基本问题定位到具体代码逻辑：什么时候质押（比如32个ETH）会被罚没呢？这会反向让我们跳出代码来思考问题本身。

感受到了知识的缺乏以后，开始在网上搜索，找到了 prysm 自己的官方 doc https://docs.prylabs.network/docs/install/install-with-script 在这方面学习更多对 POS 的基本概念。

阅读之后有了更多基本概念，如果你仅仅需要 staking，做 validator 就可以了。这里我又有了新问题，以太坊 staking 的合约地址和内容是什么？这已经离开了节点层面的知识了。

另外，做 validator 不仅是 staking，也是需要 propose 新区块的。 Execution + Beacon 更是一个全节点，validator 是连接到 Beacon 的。那么作为 propose 或者 builder 的机制也非常值得研究，这看起来是一个 geth 和 prysm 需要通信和合作才能完成的工作。

在这个文档里，我们还发现了能回答上面问题的页面 https://docs.prylabs.network/docs/concepts/slashing 什么条件下，质押会被 slash。

### 2025.02.09

简单查看了一下 ETH 的 staking 合约 https://etherscan.io/address/0x00000000219ab540356cBB839Cbe05303d7705Fa#code 并不复杂。

兴趣驱使，发现了用 Nim 语言编写的以太坊，感觉比 rust 更有前途，另外还有个语言 Zig 也挺有意思。
  * https://github.com/status-im/nimbus-eth1
  * https://github.com/status-im/nimbus-eth2

接下来的计划，还是搞清楚 prysm 和 geth 之间的通信接口，该看一看 geth 的代码了。

首先回到wiki的architecture，beacon 和 execution 中间有个 Engine API，找了一些资料 https://hackmd.io/@danielrachi/engine_api 。
我的理解是，如果共识选中了 validator ，新的区块是在 beacon 中创建的，前面我们提到过 builder service。
如果交易计算出来的状态就对不上，beacon 作恶广播了不合法的区块，那么非常容易被验证出来并丢弃区块。PoS 共识主要保护的是区块的选择，一个 validator 不能投两票，这些会被 slash 掉质押。

### 2025.02.10

目前基本上理清了 geth 和 prysm 的结构，对于开发者使用也很友好。如果仅仅需要一个本地全节点而不参与共识，运行 geth 节点即可。如果需要质押，运行 prysm 成为 validator。如果需要参与安全，则需要同时运行 geth 和 prysm 并成为 beacon 节点，prysm 是连接 geth 的 execute api 的。

回到我之前在以太坊 research 论坛上的提案 https://ethresear.ch/t/l1-improvement-based-on-minus-theory/21494 ，我们认为 Minus Theory 应用在 POS 以太坊上是完全可能的。但是需要硬分叉，将交易共识和执行解耦。

最大的挑战在于，以太坊的区块 header 中需要三棵树的默克尔根，由于减法理论需要先共识交易输入，再执行 EVM 更新全局状态，所以这一大改就迫使我们需要把全局状态和回执树的默克尔树根设置为0。这应该是一个不可能完成的任务。如果小V有志于改进以太坊 L1，亲自推动也会遇到很大的阻力，毕竟如果 L1 达到上万 TPS，将会直接影响 L2 的利益。

如果有幸实现了，那么在 geth 和 prysm 之外我们需要增加一个新的节点，需要把 geth 切分成两个节点，一个用于存储所有历史交易，另一个用于执行和保存全局状态。Prysm 应该链接到交易节点，当 beacon 选到 validator 的时候，从交易节点选择 tx 构建交易树根。同时 Prysm 也需要链接到执行节点，访问全局状态，这些信息中可以看到质押情况。由于在减法理论中，执行是延迟的，所以这部分工程实现上还是相当有挑战的，甚至有必要重新设计质押的机制。

所以，在这次学习之后，我们还是要重点发展我们的 Python VM 执行器 https://zentra.gitbook.io ，它可以和以太 L1 以及 L2s 工作，甚至可以和所有的 L1s 配合。我们应该可以在比较短期实现可以向全世界 demo 的成果。或许能反向推动以太 L1 的发展。


### 2025.02.11

今天不知道学啥了, 关注了一下 dajuguan 的 RANDAO 的 python 实现，感兴趣的可以玩玩https://github.com/dajuguan/lab/blob/main/eth/randao.py
N年前研究 POW 的同时，我也瞎写过 POS https://github.com/kernel1983/simple_pos/blob/master/pos.py

顺便也看到了 megaETH 在 MPT 方向的探索，我在推特上提了一句我们当年直接扔掉 MPT 树的工作 https://foresightnews.pro/article/detail/45335 在这里分享一下。

摸鱼为主。

### 2025.02.12

今天随机阅读了其它同学的学习笔记，一些提到 Verkle 树能解决状态爆炸问题。应该有一些计算机基础的人，都会否定这个想法。

首先，有一些语言上的艺术，在误导大家学习：压缩是什么？一般无损压缩需要能够解压还原。如果我有1G数据，我通过一些方法可以验证数据，比如默克尔树，那么我生成的是证明，默克尔根并没有起到压缩的作用，因为它无法解压成原始数据。所以说 Verkle 树能把不断增加的全局状态压缩到一个很小的数据，仅仅用于验证。

EVM 在执行中必须访问全局状态，如果是默克尔根或者 Verkle 树，则根本无法用于运行 EVM。我们还是需要全局状态，保存不断变大的全局状态，去支持 EVM 的运行。

我在研究区块链分片的时候，一开始就非常轻松的完成了对于交易的分片。对于全局状态的分片，一直没有很好的方案。但是在去年，我们意识到，全局状态爆炸，本来就是需要被抑制的，不断增长的全局状态会影响节点运行的去中心化（除非有完美的分片方案，但是这非常不切实际）。抑制全局状态，意味着我们无需全局状态的分片，这两者达到了空前的统一。

同时，我们也认识到，区块链中必须要有稀缺性资源，我们可以认为的定义 coin 的总量，故意制造稀缺，但是更需要定义这些 coin 与什么资源相关。在比特币中，coin 用于支付交易手续费。这里有一个悖论，成功的区块链代币将不断上涨，不断上涨的代币将抑制链上繁荣，区块链不再繁荣则会导致区块链的失败。我们称为 BTC 悖论（这不是说 BTC 会失败，而是采用 BTC 类似代币模型，用代币支付链手续费的其它区块链，会受到这一悖论魔咒的困扰，包括 ETH）。这个悖论简单说，区块链的繁荣将导致失败。

改进方法：在我们 Zentra 中，会利用全局状态的稀缺性，设计代币。这样的设计将鼓励链上繁荣，币价上涨不会抑制链上活跃度。

### 2025.02.13

学习BLS的过程中，重新理解一下pairing https://epf.wiki/#/wiki/Cryptography/bls?id=how-bls-works 看看经典的 pairing 可以设计什么有意思的方案。

### 2025.02.14

发现 https://github.com/ethereum/execution-specs/tree/master/src/ethereum 里面有一些宝库，有完整的所有 fork 的 python 实现，并且这个是权威的。
这个应该就是 py-evm 的各个版本快照。找时间运行一下，看看需不需要魔改。

### 2025.02.15

尝试配置环境运行 execution-specs/src，从 frontier 开始读取交易构建 state。有一些进展。

    import ethereum.frontier.trie

    print(ethereum.frontier.trie.EMPTY_TRIE_ROOT.hex())

    print(ethereum.frontier.trie.root(ethereum.frontier.trie.Trie(default={}, secured=True)).hex())

    t = ethereum.frontier.trie.Trie(default={}, secured=True)
    ethereum.frontier.trie.trie_set(t, b'1', b'2')
    print(ethereum.frontier.trie.root(t).hex())

### 2025.02.16

https://etherscan.io/block/3 研究叔块的 reward 机制 https://medium.com/@javierggil/ethereum-reward-explained-8f927a1263c6
这对于手工更新全局状态中的以太坊余额很有用。

    import ethereum_types.numeric
    import ethereum.genesis
    import ethereum.frontier.fork
    import ethereum.frontier.trie
    import ethereum.frontier.state
    
    
    description: ethereum.genesis.GenesisFork[
        ethereum.frontier.fork_types.Address,
        ethereum.frontier.fork_types.Account,
        ethereum.frontier.state.State,
        ethereum.frontier.trie.Trie,
        ethereum.frontier.fork_types.Bloom,
        ethereum.frontier.blocks.Header,
        ethereum.frontier.blocks.Block
    ] = ethereum.genesis.GenesisFork(
        Address=ethereum.frontier.fork_types.Address,
        Account=ethereum.frontier.fork_types.Account,
        Trie=ethereum.frontier.trie.Trie,
        Bloom=ethereum.frontier.fork_types.Bloom,
        Header=ethereum.frontier.blocks.Header,
        Block=ethereum.frontier.blocks.Block,
        set_account=ethereum.frontier.state.set_account,
        set_storage=ethereum.frontier.state.set_storage,
        state_root=ethereum.frontier.state.state_root,
        root=ethereum.frontier.trie.root,
        hex_to_address=ethereum.frontier.utils.hexadecimal.hex_to_address,
    )
    
    MAINNET_GENESIS_CONFIGURATION = ethereum.genesis.get_genesis_configuration("mainnet.json")
    
    chain = ethereum.frontier.fork.BlockChain([], ethereum.frontier.state.State(), ethereum_types.numeric.U64(1))
    ethereum.genesis.add_genesis_block(description, chain, MAINNET_GENESIS_CONFIGURATION)

创建一个空的区块链，并且从 mainnet.json 导入初始的预挖信息。接下来我应该可以通过 RPC API 读取数据，送到 EVM 构建新的区块。

### 2025.02.17

已经从以前我的公链项目中提取了 ETH RPC 的代码，开始与 execution-specs 对接。目前已经能 `brownie console` 并且实现 `a[0].balance()` 余额查询。
准备再探索一下，看看有没有其它技术难点，没问题的话，希望招募共学的朋友一起完成。（因为3.2之前还要去Denver一趟）

### 2025.02.18

在群里招募一起做 py 版本的 hardhat，响应人数为零。
自己做了一些零星的工作，开源 https://github.com/kernel1983/brownievm ，但是一个人做不值得立项，纯粹解决完一些有意思的问题就可以收手了。
也在考虑我们即将开始的招聘工作中，用这个项目来作为面试题目。

### 2025.02.19

今天休息一天，简单计划一下 brownievm。回头把任务再 breakdown 大家一起做。

 * 实现 transfer balance 功能
 * 实现 deploy contract 功能

### 2025.02.20

今天招募到一位感兴趣的朋友，开了一个小时会，讲解了 https://github.com/kernel1983/brownievm 的思路和进度。
能不能成功做出一些代码贡献并提交PR，就看缘分了。

实际上一个开源项目的成功不仅仅是依靠开发者，学习和传播也是重要部分，测试和使用也是一种支持。也包括撰写文档，发布新闻，以及建立联系。
现代开源除了开发者本身的爱好以外，也会是一种GTM策略。
对于区块链来说，开源是一种必须手段，但是我们更要学习除了写代码以外的其它技能。
如果没有组织协调的能力，一味写代码，开源是很难获得成功的。

### 2025.02.21

尝试了一下 bruce 的方法，用 unittest 读 go-ethereum 的代码。我们做区块链开发的时候，应该不仅限于这种方法，搭测试网应该是家常便饭。

花了时间写了一个提交 https://github.com/kernel1983/brownievm/commit/456204622f8b41da7372870960bcdef36a8acce2 参考 anvil 把10个测试账号导了进去。

### 2025.02.22

今天摸鱼提交 https://github.com/kernel1983/brownievm/commit/d59670db5b2226737d0cfd48aff657057b585b50

### 2025.02.24

和共享开源代码的朋友保持沟通。
接下来去 Denver 进入高压工作状态，学习任务基本进入摸鱼状态。
尽可能每日打开。

扑热点看了一下 safe 的合约 https://github.com/safe-global/safe-smart-account/blob/main/contracts/Safe.sol 
想不明白这么重要的合约不应该是可读性第一位的嘛，搞那么多继承，我是不敢用。

    contract Safe is
        Singleton,
        NativeCurrencyPaymentFallback,
        ModuleManager,
        GuardManager,
        OwnerManager,
        SignatureDecoder,
        SecuredTokenTransfer,
        ISignatureValidatorConstants,
        FallbackManager,
        StorageAccessible,
        ISafe

### 2025.02.25

继续发表感想，Safe 合约中居然有 `execTransaction` 这种功能，它应该老老实实的做一个管钱的多签工具，而不是往里面加功能。

目前看来，对于多签管理资产，应该寻找更加精简的单文件合约，功能要更少，更简单易读。

<!-- Content_END -->
