---
timezone: Asia/Shanghai
---

# zhouCode

1. 自我介绍
    - zhou，高校网络安全专业教师，教授课程《系统安全》《网络内容安全》等
    - 近期学习以太坊协议，同时经过好友推荐发现 EPF study group，非常想加入共同学习一起进步！
    - 实践经验：轻度参与**D2PFuzz 模糊测试工具**的协议安全性验证（DevP2P协议族测试）
2. 你认为你会完成本次残酷学习吗？
    - 一定！

## Notes

<!-- Content_START -->

### 2025.02.06

#### 认识以太坊

- 主要内容：以太坊基本概念
- 关键词：以太坊协议、以太坊开发、以太坊测试、以太坊开发模式

#### 学习目标

- [x] 目标1：了解以太坊背景，起源和发展历程
- [x] 目标2：阅读相关条目及背景资料

#### 主要内容

##### 以太坊出现的必要条件

模块化、自由软件运动、非对称加密

##### 以太坊协议

灵感来自比特币，基本原则：简单、通用、模块化、无歧视、敏捷

以太坊协议还在不断完善和进步

主要分为2层：**执行层**(EL)、**共识层**(CL)

执行层提供执行动力，处理交易和状态

共识层包括权益证明机制，确保安全和纠错

##### 以太坊的实施和开发

执行层和共识层的实现称为**客户端**。运行此客户端并连接到网络的计算机称为**节点**。

因此，节点是一对积极参与网络的EL和CL客户端。

由于ETH只在形式上做规定，所以任何语言都可以实现

##### 以太坊测试

由于客户端有多个，所以安全测试也是必要的，有多种测试工具会被使用。

测试根据规范生成，并创建各类场景。有对单独客户端的测试，也有对多个客户端行程的网络的测试。

由此分出类型：状态转换测试(state transition testing)、模糊测试(fuzzing)、影子分叉(shadow forks)、RPC 测试(RPC tests)、客户端单元测试(client unit tests)和 CI/CD 等。

##### 合作模式

以太坊开发均为公开，不同团队负责不同部分

> 新功能或更改的传统开发周期是 `Idea - Research - Development - Testing - Adoption`

### 2025.02.07
#### study group 2024 week2 Pre-reading学习

- 主要内容：初步认识EVM，认识节点和客户端的概念，了解同步模式
- 关键词：EVM，节点，执行客户端，共识客户端，同步

#### 学习目标

- [x] 目标1：认识EVM
- [x] 目标2：认识节点和客户端
- [x] 目标3：认识同步模式

#### 主要内容

##### 内容1：以太坊虚拟机(Ethereum Virtual Machine)

![EVM 组成结构图](https://ethereum.org/_next/image/?url=%2Fcontent%2Ftranslations%2Fzh%2Fdevelopers%2Fdocs%2Fevm%2Fevm.png&w=1920&q=75)

##### 以太坊状态转换函数

EVM类似于函数，输入后会有确定输出。所以，以太坊——状态转换函数

```
Y(S, T)= S'
```

给定一个旧的有效状态 `（S）`> 和一组新的有效交易 `（T）`，以太坊状态转换函数 `Y（S，T）` 产生新的有效输出状态` S'`

###### 状态(State)

状态是一个巨大的数据结构，称为[修正的 Merkle Patricia Trie](https://ethereum.org/en/developers/docs/data-structures-and-encoding/patricia-merkle-trie/)，它保持所有[账户](https://ethereum.org/en/developers/docs/accounts/)通过哈希链接，并可简化为存储在区块链上的单个根哈希。

###### 交易(Transactions)

交易是来自帐户的密码学签名指令。

分为2种：**消息调用交易**，**合约创建交易**

合约创建交易会创建一个新的合约帐户，其中包含已编译的 [智能合约](https://ethereum.org/zh/developers/docs/smart-contracts/anatomy/) 字节码。 每当另一个帐户对该合约进行消息调用时，它都会执行其字节码。

##### EVM说明

EVM为一个堆栈机，栈深度为1024 item，每个item 是一个256位的word， 256方便使用256位的加密技术

运行过程中，EVM 维持一个瞬态内存（字可寻址字节数组），不会在交易间持久存在

合约中存在的是Merkle Patricia *storage* trie(MPT)，与账户关联，且是**全局状态的一部分**

已编译的智能合约字节码在执行时会调用多个 EVM 操作码（Opcode），这些操作码执行标准的栈操作，例如 XOR、AND、ADD、SUB 等。此外，EVM 还实现了一些特定于区块链的栈操作，例如 ADDRESS、BALANCE、BLOCKHASH 等。

![表明 EVM 操作需要 Gas 的图表](https://ethereum.org/_next/image/?url=%2Fcontent%2Fdevelopers%2Fdocs%2Fgas%2Fgas.png&w=1920&q=75)

##### EVM的实现

EVM 的所有实现都必须遵守以[太坊黄皮书](https://ethereum.github.io/yellowpaper/paper.pdf)中描述的规范。

以太坊虚拟机经过了几次修订，并且存在不同编程语言实现的以太坊虚拟机版本。

##### 内容2：节点和客户端

以太坊是一个**由计算机组成的分布式网络**，这些计算机运行**可验证区块**和**交易数据的软件**，称为**节点**。 该软件必须在你的计算机上运行，才能将其转化为以太坊节点。 **一个节点由两个独立的软件**（名为“客户端”）构成。

##### 节点和客户端

**节点**是指任何以太坊客户端软件的实例，它连接到其他也运行以太坊软件的计算机，形成一个网络。

**客户端**是以太坊的实现，它根据协议规则验证数据并保持网络安全。 

个节点需要运行两种客户端软件：共识客户端和执行客户端。

- 执行客户端（也称为执行引擎、EL 客户端或旧称“以太坊 1”客户端）侦听网络中广播的新交易，并在以太坊虚拟机中执行它们，并保存所有当前以太坊数据的最新状态和数据库。
- 共识客户端（也称为信标节点、CL 客户端或旧称“以太坊 2”客户端）实现权益证明共识算法，使网络能够根据来自执行客户端的经验证数据达成一致。 此外还有名为“验证者”的第三种软件，它们可被添加到共识客户端中，使节点能参与保护网络安全。

![关联执行和共识客户端](https://ethereum.org/_next/image/?url=%2Fcontent%2Fdevelopers%2Fdocs%2Fnodes-and-clients%2Feth1eth2client.png&w=1920&q=75)

关联执行与共识客户端的简化图

##### 客户端多样性

不同团队开发的各种编程语言中都有[执行客户端](https://ethereum.org/zh/developers/docs/nodes-and-clients/#execution-clients)和[共识客户端](https://ethereum.org/zh/developers/docs/nodes-and-clients/#consensus-clients)。

多种客户端实现减少了对于单一代码库的依赖，使网络更强大。

##### 跟踪网络中的节点

多种跟踪器提供以太坊网络中节点的实时概览。由于去中心化网络的性质，这些爬虫只能提供有限的网络视图，并且可能会报告不同的结果。

##### 节点类型

客户端可以运行三种类型的节点：**轻节点**、**全节点**和**归档节点**。

###### 轻节点（发展方向）

轻节点只下载区块头，而不会下载每个区块。这些区块头包含区块内容的摘要信息。

轻节点会向全节点请求其所需的任何其他信息。

轻节点可以让用户加入以太坊网络，无需运行全节点所需的功能强大的硬件或高带宽。 最终，轻节点也许能在手机和嵌入式设备中运行。 轻节点不参与共识（即它们不能成为矿工/验证者），但可以访问功能和安全保障和全节点相同的以太坊区块链。

以太坊目前还不支持大量轻节点，但轻节点支持是一个有望在不久的将来快速发展的领域。 特别是像 [Nimbus](https://nimbus.team/)、[Helios](https://github.com/a16z/helios) 以及 [LodeStar](https://lodestar.chainsafe.io/) 这样的客户端目前都非常关注轻节点。

###### 全节点

全节点对区块链进行逐块验证，包括下载和验证每个块的块体和状态数据。全节点只保留相对较新数据的本地副本（通常是最近的 128 个区块），允许删除比较旧的数据以节省磁盘空间。 旧数据可以在需要时重新生成。

特点：

- 存储全部区块链数据（会定期修剪，所以全节点并不存储包含创世块在内的所有状态数据）
- 参与区块验证，验证所有区块和状态。
- 全节点可以从本地储存中检索所有状态，或从“快照”中重新生成。
- 为网络提供服务，并应要求提供数据。

###### 归档节点

归档节点是从创世块开始验证每个区块的全节点，它们从不删除任何下载的数据。

特点：

- 存储全节点中保存的所有内容，并建立历史状态存档。 如果你想查询区块 #4,000,000 的帐户余额，或者想简单可靠地测试自己的一组交易而不使用跟踪挖掘它们，则需要归档节点。
- 这些数据以太字节为单位，这使得归档节点对普通用户的吸引力较低，但对于区块浏览器、钱包供应商和链分析等服务来说则很方便。

以归档以外的任何方式同步客户端将导致区块链数据被修剪。 这意味着，不存在包含所有历史状态的归档，但全节点能够在需要时构建它们。

##### 运行节点

对个人的优点：

以私密、自给自足的去信任方式使用以太坊。可以使用自己的客户端验证数据。*“不要信任，直接验证”*

![如何通过你的应用和节点访问以太坊](https://ethereum.org/_next/image/?url=%2Fcontent%2Fdevelopers%2Fdocs%2Fnodes-and-clients%2Fnodes.png&w=1920&q=75)

对网络的优点：

多样化的节点对于以太坊的健康、安全和运行弹性非常重要。

##### 运行节点的代替方法

可以使用第三方应用程序接口提供商。 有关使用这些服务的概述，请查看[节点即服务](https://ethereum.org/zh/developers/docs/nodes-and-clients/nodes-as-a-service/)。

##### 执行客户端

| 客户端                                                       | 语言       | 操作系统              | 网络                   | 同步策略         | 状态缓冲        |
| ------------------------------------------------------------ | ---------- | --------------------- | ---------------------- | ---------------- | --------------- |
| [Geth](https://geth.ethereum.org/)                           | Go         | Linux、Windows、macOS | 主网、Sepolia、Holesky | 快照、完全       | Archive、Pruned |
| [Nethermind](https://www.nethermind.io/)                     | C#、.NET   | Linux、Windows、macOS | 主网、Sepolia、Holesky | 快照、完全       | Archive、Pruned |
| [Besu](https://besu.hyperledger.org/en/stable/)              | Java       | Linux、Windows、macOS | 主网、Sepolia、Holesky | 快照、快速、完全 | Archive、Pruned |
| [Erigon](https://github.com/ledgerwatch/erigon)              | Go         | Linux、Windows、macOS | 主网、Sepolia、Holesky | 完全             | Archive、Pruned |
| [Reth](https://reth.rs/)                                     | Rust       | Linux、Windows、macOS | 主网、Sepolia、Holesky | 完全             | Archive、Pruned |
| [EthereumJS](https://github.com/ethereumjs/ethereumjs-monorepo) | TypeScript | Linux、Windows、macOS | Sepolia、Holesky       | 完全             | 修剪            |

##### 共识客户端

负责所有共识相关的逻辑，包括分叉选择算法、处理认证与管理[权益证明](https://ethereum.org/zh/developers/docs/consensus-mechanisms/pos/)奖励及惩罚。

| 客户端                                                       | 语言       | 操作系统              | 网络                                                 |
| ------------------------------------------------------------ | ---------- | --------------------- | ---------------------------------------------------- |
| [Lighthouse](https://lighthouse.sigmaprime.io/)              | Rust       | Linux、Windows、macOS | 信标链、Goerli、Pyrmont、Sepolia、Ropsten 等         |
| [Lodestar](https://lodestar.chainsafe.io/)                   | TypeScript | Linux、Windows、macOS | 信标链、Goerli、Sepolia、Ropsten 等                  |
| [Nimbus](https://nimbus.team/)                               | Nim        | Linux、Windows、macOS | 信标链、Goerli、Sepolia、Ropsten 等                  |
| [Prysm](https://docs.prylabs.network/docs/getting-started/)  | Go         | Linux、Windows、macOS | 信标链、Gnosis、Goerli、Pyrmont、Sepolia、Ropsten 等 |
| [Teku](https://consensys.net/knowledge-base/ethereum-2/teku/) | Java       | Linux、Windows、macOS | 信标链、Gnosis、Goerli、Sepolia、Ropsten 等          |
| [Grandine](https://docs.grandine.io/)                        | Rust语言   | Linux、Windows、macOS | 信标链、Goerli、Sepolia 等                           |

##### 同步模式

同步方法如下：从对等节点下载数据，用加密方法验证其完整性，并构建一个本地区块链数据库。

客户端在实现同步算法方面也各不相同。 有关实现的具体细节，请参考你所选客户端的官方文档。

##### 执行层的同步

分为完全同步，快速同步，快照同步，轻量同步

###### 完全同步

完全同步会下载所有区块（包括区块头和区块体），并通过执行自创世块以来的每个区块，以增量方式重新生成区块链的状态。

[存档节点](https://ethereum.org/zh/developers/docs/nodes-and-clients/#archive-node)会执行完全同步，以构建（并保留）每个区块中每笔事务所做的状态更改的完整历史记录。

###### 快速同步

与完全同步一样，快速同步会下载所有区块（包括区块头、交易和收据）。 不过，快速同步并不重新处理历史交易，而是依赖收据，直至到达最近的头部时，再切换到导入和处理区块，以提供一个完整的节点。（可以减少带快使用）

###### 快照同步

逐块验证链。不是从创世区块开始，而是从一个最近的已知为真实区块链一部分的受信任检查点开始。节点会定期保存检查点，同时删除早于某个时间的数据。 这些快照被用于在需要时重新生成状态数据，而不是永久储存它。

- 最快的同步策略，目前是以太坊主网的默认策略。
- 节省大量磁盘空间和网络带宽，同时不牺牲安全性。

###### 轻量同步

轻客户端模式下载所有区块头和区块数据，并对其中一些进行随机验证。 仅从可信的检查点同步链的头部。

- 仅获取最新状态，同时依赖于对开发者和共识机制的信任。
- 客户端在几分钟内便可以使用当前网络状态。

##### 共识层的同步

###### 乐观同步

是合并后同步策略，允许执行节点通过已确立的方法进行同步。执行引擎可以在不进行完全验证的情况下*乐观地*导入信标区块，找到最新区块头，然后使用上述方法开始同步链。 接着，在执行客户端更新之后，它将通知共识客户端信标链中交易的有效性。

**先导入，再确认**

###### 检查点同步

也叫弱主观性同步，从最近的弱主观性检查点而不是从创世块同步信标链。检查点同步可大幅加快初始同步速度，其信任假设与从创世块同步时类似。

在实践中，这意味着你的节点会连接到远程服务，以下载最近的最终确定状态并从该点继续验证数据。 提供数据的第三方会受到信任，因此要谨慎选择。
### 2025.02.08

#### Study Group 2024 week2 学习

#### 学习内容

观看thereum Execution Layer Overview | lightclient视频

#### 概念补充

##### gas

as 是衡量交易和智能合约执行时所消耗计算资源的单位，其消耗量决定了需支付的交易费用，同时通过限制资源消耗来防止网络滥用。

Gas 的使用量主要取决于交易或合约调用中执行的操作类型和复杂性，交易中操作越简单、状态变化越少、计算越轻量，gas 使用就越少；而操作越复杂、需要修改状态或执行大量计算时，则会消耗更多 gas。

##### Deneb Beacon Chain

以太坊共识层——即Beacon Chain，在经过“Deneb”升级后所呈现的新版形态。简单来说：

- **Beacon Chain 的作用**：Beacon Chain 是以太坊采用权益证明（PoS）共识机制的核心链，负责管理验证者、组织区块生产和确认，以及协调网络安全。
- **Deneb 升级**：Deneb 是以太坊后续升级计划中的一个阶段（常与Capella等升级配合），旨在改善Beacon Chain的性能和数据处理能力，提升网络效率，并为未来扩容（如Danksharding）做准备。

因此，“Deneb Beacon Chain”就是指在完成Deneb升级之后的Beacon Chain版本，它通过一系列技术改进，提高了共识效率、数据可用性和整体网络扩展性。

#### 视频主要内容

##### 1 执行层的区块验证

执行层现在更像是一个状态转换函数

```go
// 接收父区块、当前区块和当前状态（StateDB）作为参数。
// 首先调用 core.VerifyHeaders 验证区块头（确保区块头信息符合规定，如时间戳、难度、父区块哈希等）。
// 然后遍历区块中所有交易，对于每笔交易调用 vm.Run 在虚拟机中执行，更新状态。
// 如果在验证区块头或执行某笔交易时出错，则立即返回错误，说明该区块无效；如果所有操作都成功，则返回更新后的状态。
func stf(parent types.Block, block types.Block, state state.StateDB) (state.StateDB, error) {
    if err := core.VerifyHeaders(parent, block); err != nil {
        // header error detected
        return nil, err
    }
    for _,tx := range block.Transactions() {
        res, err := vm.Run(block.Header(), tx, state)
        if err != nil {
            // trasaction invalid, block is invalid
            return nil, err
        }
        state = res
    }
    return state, nil
}
// 这个函数调用了 stf函数来处理（执行）一个执行载荷（ExecutionPayload）。
// 如果执行过程中没有错误，说明载荷中的交易都合法，则返回 true；否则返回 false，表示载荷无效。
func newPayLoad(execPayload engine.ExecutionPayload) bool {
    if _, err := stf(..); err != nil {
        return false
    } 
    return true
}
```

- 合并后，执行层（Execution Layer）的职责简化，主要负责状态转换功能（State Transition Function）。
- 共识层（Consensus Layer）接管了区块排序、重组（reorgs）等任务，执行层仅需验证区块的有效性并生成新的状态。
- 执行层通过 `process_execution_payload` 函数与共识层交互，返回区块是否有效的布尔值。
- 验证区块头（Header）的合法性，包括父哈希、时间戳、Gas Limit（需符合1/1024调整规则）、Base Fee计算等。
- 执行层调用 `state_transition` 函数，逐笔执行交易并更新状态数据库（State DB）。
- 若交易执行失败（如Gas不足或无效Nonce），整个区块会被标记为无效。

##### 2 区块构建

```go
func build(env Environment, pool txpool.Pool, state state.StateDB) (types.Block, state.StateDB, error){
    var (
    	gasUsed = 0 // 定义一个变量 gasUsed，初始值为 0，用来累计已消耗的 Gas。
        txs []types.Transactions // 定义一个交易列表 txs，用于存放从交易池中挑选并执行成功的交易。
    )
    // 循环条件是“当已消耗的 gas 小于环境设置的 GasLimit 或者交易池非空时”（注意：这里的条件写成“||”，即只要有一个条件满足就继续循环）。
    for ; gasUsed < env.GasLimit || ! pool.Empty(); {
        tx := pool.Pop() // 在每次循环中，从交易池中弹出一笔交易（tx := pool.Pop()）。
        // 调用 vm.Run(env, tx, state) 在虚拟机中执行这笔交易。该函数返回三个值：
        // res：执行后的新状态；
        // gas：该笔交易实际消耗的 gas 数量；
        // err：执行过程中产生的错误（如果交易无效，则返回错误）。
        // 如果执行过程中出错（例如交易无效），则跳过这笔交易（continue），不把它加入区块中。
        res, gas, err := vm.Run(env, tx, state)
        if err != nil {
            // tx invalid
            continue
        }
        // 如果交易执行成功，则将该交易消耗的 gas 累加到 gasUsed 上。
        // 将这笔交易添加到交易列表 txs 中。
        // 更新状态 state 为这笔交易执行后的结果 res。
        gasUsed += gas
        txs = append(txs, tx)
        state = res
    }
    // 循环结束后，调用 core.Finalize(env, txs, state) 对交易列表和状态进行最终处理，生成一个完整的区块，并返回该区块、最终状态和可能的错误。
    return core.Finalize(env, txs, state)
}
```

- 交易池（Transaction Pool）按Gas价格排序交易，优先选择高Gas费的交易填充区块。
- 通过循环执行交易，累积Gas使用量，直到达到区块Gas上限（如30M）。
- 最终调用 `Finalize` 函数生成完整的区块，包含交易哈希、收据哈希等默克尔根。

##### 3 状态转换函数

代码见go-ethereum

- 状态转换函数的核心是逐笔执行交易，通过EVM（以太坊虚拟机）更新状态。
- EVM执行时需传入区块上下文（如Coinbase、时间戳）和交易上下文（如Gas Price）。
- 交易执行失败（如合约回滚）仅消耗Gas，不影响区块有效性，但无效交易会导致区块被拒绝。

##### 4 EVM工作原理与指令示例

- EVM是基于栈的虚拟机，指令包括算术运算（ADD）、存储操作（SSTORE）、环境指令（COINBASE）等。
- 示例：通过 `MSTORE` 将数据写入内存，`RETURN` 返回结果。
- 每个EVM调用帧（Call Frame）包含独立的栈、内存和Gas计数器。

##### 5 点对点（P2P）协议与数据同步

- DevP2P协议负责广播交易、同步区块头和状态数据（通过 `eth/68` 和 `snap` 协议）。
- 交易广播采用“平方根广播”策略，减少带宽消耗。
- Snap Sync分两阶段：连续状态下载（Contiguous Retrieval）和状态修复（Healing），依赖默克尔证明验证数据完整性。

### 2025.02.09

#### Study Group 2024 week3 学习

#### 学习内容

观看Ethereum Consensus Layer | Alex Stokes | Week 3视频

#### 视频主要内容

##### 1 区块链与数字稀缺性

- 区块链的核心价值是创造“数字稀缺性”，解决数字世界中无法复制的资源问题（如货币、数字资产）。
- 传统中心化系统的缺陷：依赖单一信任方，易受攻击或操纵。
- 分布式共识的目标：通过多节点协作实现去信任化，确保协议规则自动执行。

##### 2 拜占庭容错（BFT）与共识机制

- 拜占庭容错（BFT）是分布式系统的核心问题，需保证即使部分节点故障或作恶，系统仍能达成一致。
- 传统BFT协议（如PBFT）的局限性：节点数量受限，消息复杂度高。
- 比特币的PoW创新：通过工作量证明实现开放网络的共识，但存在能源浪费和激励机制单一的问题。

##### 3 以太坊的权益证明（PoS）机制

- **PoS的核心设计**：验证者需质押32 ETH参与共识，通过经济惩罚（Slashing）增强安全性。
- **Slot与Epoch**：
  - Slot：12秒为一个时间单元，每个Slot由随机选出的验证者提议区块。
  - Epoch：32个Slot（约6.4分钟），用于批量处理验证者奖惩、状态更新等。
- **随机性（RANDAO）**：通过链上随机数生成验证者分配，确保公平性。

##### 4 以太坊共识协议（Gasper）

- **Gasper协议**：结合FFG（Friendly Finality Gadget）和LMD GHOST算法，实现动态可用性与最终性。
- **最终性（Finality）**：需2/3验证者投票确认的区块不可逆转，防止分叉。
- **分片与动态委员会**：通过随机分片降低单个验证者的负载，提升网络吞吐量。

##### 5 未来改进方向

- **单槽最终性（SSF）**：缩短最终性确认时间至单个Slot（12秒），减少攻击窗口。
- **提议者-构建者分离（PBS）**：分离区块提议与构建角色，降低MEV（最大可提取价值）对去中心化的影响。
- **验证者优化**：探索更高质押门槛（如2048 ETH）以减少节点数量，提升效率。

### 2025.02.10

#### Study Group 2024 week3 学习

#### 概念补充

##### 共识机制

“共识机制”一词常常泛指“权益证明”、“工作量证明”或“权威证明”协议。 不过，这些协议只是共识机制的组成部分，用于防范女巫攻击（女巫攻击是指个人欺骗系统，使系统认为他们是多人以增加他们的影响力。）。 共识机制是由一整套想法、协议和激励构成的体系，使得一系列分布式节点能够就区块链状态达成一致。

##### 权益证明(PoS)

权益证明 (PoS) 是支撑以太坊[共识机制](https://ethereum.org/zh/developers/docs/consensus-mechanisms/)的基础。 以太坊于 2022 年启动了权益证明机制，这是因为和原先的[工作量证明](https://ethereum.org/zh/developers/docs/consensus-mechanisms/pow/)架构相比，以太坊更安全、能耗更低并且更利于实现新的扩容解决方案。

权益证明是一种证明验证者已经将有价值物品质押到网络上的方法。如果验证者有失信行为，这些物品可能会被销毁。 在以太坊的权益证明机制下，验证者明确地通过以太币将资产质押到以太坊上的智能合约中。 之后，验证者负责检查在网络上传播的新区块是否有效，偶尔自己也创建和传播新区块。 当他们试图欺骗网络（例如，在应该发送一个区块时提出多个区块，或者发送冲突的认证）时，他们质押的部分或全部以太币可能会被销毁。

权益证明体系保障加密经济的安全，因为攻击者若试图控制整条链，就必须销毁大量以太币。 奖励机制会奖励诚实的质押人，而惩罚机制则阻止质押人作出恶意行为。

###### 验证者

要想作为验证者参与，用户必须向存款合约中存入 32 以太币并运行三种独立的软件：执行客户端、共识客户端和验证者客户端。 存入以太币时，用户会进入一个激活队列，限制新验证者加入网络的速度。 激活后，验证者将从以太坊网络上的对等节点接收新区块。 区块中的交易会被重新执行，以检查提议的以太坊状态变更是否有效，并检查区块的签名。 然后验证者在整个网络上发送支持该区块的投票（称为认证）。

在工作量证明中，生成区块的时间是由挖矿难度决定的，而在权益证明中，节奏是固定的。 权益证明以太坊中的时间分为时隙（12 秒）和时段（32 个时隙）。 在每个时隙中随机选择一位验证者作为区块提议者。 该验证者负责创建新区块并发送给网络上的其他节点。 另外在每个时隙中，都会随机选择一个验证者委员会，通过他们的投票确定所提出区块的有效性。 将验证者集合划分为若干个委员会对于保持网络负荷易于管理非常重要。 委员会将验证者集合分成不同部分，以便每个活跃的验证者在每个时段都会出示证明，但并不在每个时隙都这样做。

##### 如何在以太坊权益证明中执行交易

1. **发起交易**：用户通过钱包工具签署交易，设定燃料费（小费给验证者，基础费被销毁），并通过节点提交至以太坊网络。
2. **验证交易**：节点检查交易有效性（余额足够、签名正确），通过后存入本地待处理交易池（内存池），并广播给全网节点。部分高级用户会绕过广播，直接将交易发送给专业区块构建者以优化收益（如利用MEV策略）。
3. **打包区块**：当前时隙的随机选中的验证节点（提议者）将内存池交易打包为“执行负载”，生成状态变更数据，并封装到包含共识信息的“信标区块”中。
4. **全网验证**：其他节点收到新区块后，在本地重新执行交易以验证有效性。验证者确认区块合法后，将其加入自身数据库，并基于多数共识（分叉规则）认可其为链上新头区块。
5. **最终确认**：交易需在两个连续时段（检查点）间获得超过66%质押以太坊的共识验证，方可视为不可逆的“最终确定”状态。检查点机制确保网络周期性达成全局一致。

##### 最终确定性

1. **最终确定性概念**：在分布式网络中，一旦交易被纳入区块，就被视为“最终确定”，即除非销毁大量以太币，否则无法篡改该区块。
2. **检查点机制**：以太坊将每个时段的第一个区块设为检查点。验证者针对认为有效的检查点对进行投票。如果某对检查点获得了超过质押以太币总数三分之二的票数，则这对检查点会被升级：较新的检查点成为“合理”的，而之前的检查点（作为上个时段的目标）则升级为“最终确定”。
3. **攻击成本**：为了回滚一个已经最终确定的区块，攻击者需要承担至少相当于质押以太币总数三分之一的损失，从而提高了攻击成本。
4. **怠惰惩罚机制**：由于最终确定需要三分之二多数投票，攻击者如果持有三分之一投票权，可能会阻止链的最终确定。为防范这种情况，当链连续超过四个时段未能最终确定时，怠惰惩罚机制便会触发，逐步削减与大多数投票相反的验证者的质押，促使大多数验证者重新获得三分之二的投票，从而最终实现链的最终确定。

##### 加密经济的安全性

1. **验证者的承诺**：
   - 验证者需要保持足够的硬件资源和网络连接，积极参与区块的验证和提议。
   - 作为回报，其质押的以太币会增加，从而获得奖励。
2. **风险与攻击面**：
   - 成为验证者虽然能获得奖励，但也为攻击者提供了通过验证者节点进行恶意行为或个人利益攻击网络的渠道。
3. **不参与与不诚实的后果**：
   - 如果验证者在需要参与时缺席，则会错过奖励；
   - 如果进行不诚实行为，其质押以太币可能会被销毁（即被罚没）。
4. **主要的不诚实行为**：
   - 在同一时隙中提出多个区块（模棱两可行为）；
   - 提交相互矛盾的认证。
5. **惩罚机制（相关性惩罚）**：
   - 惩罚的幅度取决于同时被罚验证者的数量：可能是轻微的（单个验证者损失约 1% 的质押），也可能是严重的（导致全部质押被销毁）。
   - 惩罚过程分阶段进行：
     - 第 1 天：立即惩罚（最多 1 个以太币）；
     - 第 18 天：实施相关性惩罚；
     - 第 36 天：将验证者逐出网络。
   - 即便验证者保持在线但未提交投票，也会每天受到轻微的惩罚。
6. **总体效果**：
   - 这些措施使得任何企图通过协同攻击来破坏网络的成本极高，从而保护了网络的安全性。

##### 分叉选择

当网络以最佳状态诚信运行时，链头始终只会有一个新区块并且所有验证者都会证明它。 然而，由于网络延迟或因为区块提议者提出多个区块（模棱两可），验证者可能看到不同的链头视图。 因此，共识客户端需要一种算法来确定支持哪一个区块。 权益证明以太坊中使用的算法称为 [LMD-GHOST(opens in a new tab)](https://arxiv.org/pdf/2003.03052.pdf)。它的工作原理是确定其历史记录中具有最大证明权重的分叉。

##### 权益证明和安全性

除了 51% 攻击，不良行为者也可能尝试其他形式的恶意活动，例如：

- 远程攻击（尽管确定性工具能抵消这种攻击向量）
- 近程“重组”（尽管提议者权重提升和认证期限可以缓解这种情况）
- 弹跳和平衡攻击（也能通过提议者权重提升来缓解，并且这些攻击无论如何都只在理想化的网络条件下得到证明）
- 雪崩攻击（通过只考虑最新信息的分叉选择算法规则来抵消）

总的来说，已经证实以太坊实施的权益证明在经济方面比工作量证明更安全。

##### 优点和缺点

| **优点**                                                     | **缺点**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 质押使个人更容易参与其中保障网络的安全，促进去中心化。 验证者节点可以在普通笔记本电脑上运行。 质押池让用户可以在没有 32 个以太币的情况下质押。 | 与工作量证明相比，权益证明仍处于起步阶段，并且经过的实践检验较少。 |
| 权益质押更加去中心化。 规模经济不像适用于工作量证明挖矿那样适用于权益证明。 | 实现权益证明比实现工作量证明更加复杂。                       |
| 权益证明的加密经济安全性高于工作量证明                       | 用户需要运行三种软件才能参与以太坊的权益证明。               |
| 需要发行较少的新以太币就可以激励网络参与者                   |                                                              |

以太坊原来使用的是工作量证明，但在 2022 年 9 月转换为使用权益证明。 权益证明相较于工作量证明有如下一些优点：

- 能效更高 – 无需在工作量证明计算中使用大量能源
- 门槛更低、硬件要求下降 – 无需购买高性能硬件以便获得创建新区块的机会
- 中心化风险降低 – 权益证明应该可以增加保护网络安全的节点
- 由于能源需求低，发行较少的以太币就可以激励大家参与
- 与工作量证明相比，对不当行为的经济处罚让 51% 攻击的代价变得更高。
- 如果 51% 攻击是为了攻破加密经济的防御，那么社区可以求助于诚实链的社交恢复。

### 2025.02.11

#### Study Group 2024 week4 学习

#### 以太坊测试与安全

##### 测试的核心

- **预状态（Pre-state）**：测试前的区块链状态（合约代码、存储、余额等）。
- **环境（Environment）**：区块参数（时间戳、燃料限制、基础费用、分叉激活时间）。
- **交易（Transactions）**：触发特定EVM操作的输入数据。
- **后状态（Post-state）**：测试后预期的区块链状态（存储变更、状态根等）。
- **测试生成（Test Filling）**：通过工具（如Go Ethereum的`evm`模块）将测试定义转换为可执行的测试夹具（Fixture）。

##### **测试工具与框架**

- **执行规范测试库（Ethereum Execution Spec Tests）**：
  - 使用Python编写，支持复杂参数化测试（如不同分叉规则）。
  - 依赖Go Ethereum生成测试夹具，未来计划通过[EELS](https://github.com/ethereum/execution-specs)实现独立验证。
- **Hive框架**：
  - 用于跨层端到端测试，模拟共识层与执行层的交互（如Engine API调用）。
  - 支持并行测试多客户端（如Geth、Nethermind）的兼容性。

##### **共识层测试**

- **共识规范测试（Consensus Spec Tests）**：
  - 将规范与测试代码合并，覆盖信标链状态转换、分片逻辑等。
  - 生成多种格式的测试夹具（如区块有效性、质押操作）。

##### **安全漏洞与披露**

- **潜在风险**：
  - 客户端错误验证有效/无效区块可能导致网络分叉。
  - 不同层（执行层/共识层）的客户端兼容性问题。
- **漏洞披露流程**：
  - 发现漏洞后通过[以太坊漏洞赏金计划](https://bounty.ethereum.org/)提交，最高可获得25万美元奖励。
  - 公开披露需在修复后进行（参考[历史案例库](https://github.com/ethereum/eth-sec)）。

### 2025.02.12

#### Study Group 2024 week5 学习

#### **合并（The Merge）**

- 以太坊从工作量证明（PoW）转向权益证明（PoS）的重要性，信标链（Beacon Chain）的启动与合并后的经济安全性提升。
- 最终性（Finality）概念的引入（12.6分钟完成区块最终确认）。
- 签名聚合（Signature Aggregation）和秘密领导者选举（Whisk协议）的研究进展。

#### **激增（The Surge）**

- **数据可用性采样（DAS）**: 通过多项式承诺（如KZG）实现高效数据验证，支持Rollup扩展。
- **EIP-4844（Proto-Danksharding）**: 引入“Blob”存储结构，降低Rollup数据成本，已上线主网。
- **Rollup分类**: 乐观Rollup与零知识Rollup的对比，强调数据可用性对挑战机制的重要性。

#### **The Scourge**

- **提议者-构建者分离（PBS）**: 减少验证者中心化风险，通过MEV-Boost临时方案过渡到协议内实现。
- **最大有效余额（Max EB）**: 从32 ETH提升至2048 ETH，优化验证者效率。
- **流动性质押（Liquid Staking）**: 探索降低罚没风险的新机制（如质押上限）。

#### **验证（The Verge）**

- **Verkle树**: 取代Merkle树，实现更高效的轻客户端验证和状态证明，支持无状态验证。
- **ZK化（ZK-SNARKs）**: 未来将共识层和执行层交易验证集成零知识证明，提升可扩展性。

#### **清洗（The Purge）**

- **历史过期（EIP-4444）**: 节点不再存储超过1年的历史数据，依赖Portal Network等去中心化存储方案。
- **状态简化**: 移除旧版协议支持（如RLP序列化），向SSZ过渡。

#### **挥霍（The Splurge）**

- **账户抽象（ERC-4337）**: 支持智能合约钱包，实现社交恢复、批量交易等高级功能。
- **EVM优化（EOF）**: 提升EVM兼容性，支持模块化升级。
- **加密创新**: 全同态加密（FHE）、一次性签名（One-Shot Signatures）等前沿研究。

#### 其他关键讨论

- **量子抗性**: 长期规划中替换BLS签名，采用抗量子算法（如STARKs）。
- **路线图复杂性**: 未来可能面临协议僵化（Ossification）风险，需平衡创新与稳定性。

### 2025.02.13

##### Study Group Week 5 | Using Ethereum clients

##### **客户端选择与安装**

- **客户端多样性**：建议根据开发语言偏好（如Java开发者可选Besu）或生态贡献需求选择客户端。
- **签名验证**：通过PGP验证客户端二进制文件的安全性。
- **编译客户端**：演示从源码编译Geth的过程。

##### **节点配置与运行**

- **数据目录与网络配置**：指定数据存储路径及网络参数（如`--datadir`和`--network`）
- **同步模式**：解释全同步（Full Sync）与快照同步（Snap Sync）的区别
- **JWT认证**：配置执行层与共识层通信的JWT密钥

### 2025.02.14

开始实践

#### 尝试建立私链

[ethpandaops/ethereum-package：一个 Kurtosis 包，用于部署私有、可移植和模块化的以太坊开发网 --- ethpandaops/ethereum-package: A Kurtosis package that deploys a private, portable, and modular Ethereum devnet](https://github.com/ethpandaops/ethereum-package)

#### Quickstart 快速入门

1. [Install Docker & start the Docker Daemon if you haven't done so already](https://docs.docker.com/get-docker/)

2. [Install the Kurtosis CLI, or upgrade it to the latest version if it's already installed](https://docs.kurtosis.com/install)

3. Run the package with default configurations from the command line:

   ```
   kurtosis run --enclave my-testnet github.com/ethpandaops/ethereum-package
   ```

#### Run with your own configuration

Kurtosis packages are parameterizable, meaning you can customize your network and its behavior to suit your needs by storing parameters in a file that you can pass in at runtime like so:

```
kurtosis run --enclave my-testnet github.com/ethpandaops/ethereum-package --args-file network_params.yaml
```

Where `network_params.yaml` contains the parameters for your network in your home directory.

#### Run on Kubernetes

Kurtosis packages work the same way over Docker or on Kubernetes. Please visit our [Kubernetes docs](https://docs.kurtosis.com/k8s) to learn how to spin up a private testnet on a Kubernetes cluster.

#### Considerations for Running on a Public Testnet with a Cloud Provider

When running on a public testnet using a cloud provider's Kubernetes cluster, there are a few important factors to consider:

1. State Growth: The growth of the state might be faster than anticipated. This could potentially lead to issues if the default parameters become insufficient over time. It's important to monitor state growth and adjust parameters as necessary.
2. Persistent Storage Speed: Most cloud providers provision their Kubernetes clusters with relatively slow persistent storage by default. This can cause performance issues, particularly with Execution Layer (EL) clients.
3. Network Syncing: The disk speed provided by cloud providers may not be sufficient to sync with networks that have high demands, such as the mainnet. This could lead to syncing issues and delays.

To mitigate these issues, you can use the `el_volume_size` and `cl_volume_size` flags to override the default settings locally. This allows you to allocate more storage to the EL and CL clients, which can help accommodate faster state growth and improve syncing performance. However, keep in mind that increasing the volume size may also increase your cloud provider costs. Always monitor your usage and adjust as necessary to balance performance and cost.

For optimal performance, we recommend using a cloud provider that allows you to provision Kubernetes clusters with fast persistent storage or self hosting your own Kubernetes cluster with fast persistent storage.

### 2025.02.15

##### ethpandaops/ethereum-package初步搭建成功

遇到的坑记录（Ubuntu系统24.04.1LTS）：

1. kurtosis run --enclave my-testnet github.com/ethpandaops/ethereum-package运行不了
   - 尝试登录docker（x），配置gpg（x），修改镜像源（多次尝试才成功）
2. 原因：docker国内直连网络问题严重，各种国内镜像时常过期，挂VPN也不一定有用，总结了一些（可能有用的）镜像源

```json
"https://<阿里云个人镜像>.mirror.aliyuncs.com", #https://cr.console.aliyun.com/cn-hongkong/instances/mirrors，当前仅支持阿里云用户使用具备公网访问能力的阿里云产品进行镜像加速
"https://mirrors.ustc.edu.cn/docker-ce",
"https://registry.docker-cn.com",
"http://hub-mirror.c.163.com",
"https://dockerpull.org",
"https://docker.1panel.dev",
"https://docker.foreverlink.love",
"https://docker.fxxk.dedyn.io",
"https://docker.xn--6oq72ry9d5zx.cn",
"https://docker.zhai.cm",
"https://docker.5z5f.com",
"https://a.ussh.net",
"https://docker.cloudlayer.icu",
"https://hub.littlediary.cn",
"https://hub.crdz.gq",
"https://docker.unsee.tech",
"https://docker.kejilion.pro",
"https://registry.dockermirror.com",
"https://hub.rat.dev",
"https://dhub.kubesre.xyz",
"https://docker.nastool.de",
"https://docker.udayun.com",
"https://docker.rainbond.cc",
"https://hub.geekery.cn",
"https://docker.1panelproxy.com",
"https://atomhub.openatom.cn",
"https://docker.m.daocloud.io",
"https://docker.1ms.run",
"https://docker.linkedbus.com",
"https://dytt.online",
"https://func.ink",
"https://lispy.org",
"https://docker.xiaogenban1993.com"
```

2. 仓库下的`network_params.yaml`为配置文件，可以自行配置

<!-- Content_END -->
