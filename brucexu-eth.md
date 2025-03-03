---
timezone: Pacific/Auckland
---

# Bruce Xu

1. 自我介绍：大家好，我是 Bruce Xu，以太坊爱好者，LXDAO 和 ETHPanda 联合发起人，很开心参加今年的 EPF 残酷共学。
2. 你认为你会完成本次残酷学习吗？会的！

## Notes

<!-- Content_START -->

# 2025.02.06

今天先把 https://epf.wiki/#/ 大概得过一下，看看整体结构和一些相关的信息，列一些 TODO 记录自己感兴趣的话题和内容，进行下一步的学习。

填写了 survey：<https://forms.gle/G5V95qyGV8uMjKGcA>

今年的 EPFsg 是 2 周 intense 的之前课程回顾，然后 6 周新的在线课程，覆盖几个部分。

TODO 这两周可以快速复习 https://epf.wiki/#/eps/SG2024 24 年的课程和笔记。


## [Prehistory of Ethereum](https://epf.wiki/#/wiki/protocol/prehistory)

以太坊的愿景来自于互联网早期的开放精神、Unix、GNU/Linux、Cypherpunks、比特币等等，构建一个无边界、自我主权的数字经济生态。

"National borders are just speed bumps on the information superhighway."
— Timothy May, Cypherpunk.

互联网的兴起，打破了国家的便捷，促进了不可想象的人类互动。

密码学和开源软件作为根基，促进了互联网新人，助推了电子商务和网上银行业务的增长。

Free software 的 free 是 freedom 而不是 price。但是 FOSS 是非常有价值和贡献的。

90 年代开始，密码朋克就有很多次对于实现 digital currency 的尝试，例如 Digicash、E-Gold、B-Money、Bitgold、Bitcoin。而 Bitcoin 上面开发应用程序的几次尝试都失败了，所以有了 Ethereum 的诞生。

分享：<https://x.com/brucexu_eth/status/1887257222436298803>

## [Protocol Architecture Overview](https://epf.wiki/#/wiki/protocol/architecture)

执行层处理实际交易和用户交互，共识层提供证明的共识机制。

## [Protocol Design Philosophy](https://epf.wiki/#/wiki/protocol/design-rationale)

- 简单
- 普遍：图灵完备的虚拟机
- 模块化
- 中立不歧视
- 敏捷

原则：

- 尽量简单
- Freedom：使用时，不会受到限制或者歧视。
- Generalization
- 没有任何特性：可以通过智能合约自己设计

实际上我感觉以太坊协议还是太复杂了，避免不了软件工程的屎山的归途。按照架构的演进，模块化肯定是必然，分层的设计需要非常清晰和能看到全局的资深研究员。

TODO 绘制以太坊的分层架构图。

UTXO vs Account：这是个比较大的话题，不过智能合约的实现，账号确实是比较好的选择。

Merkle-Patricia Trie 是以太坊的存储数据结构，高效检索的能力构成了以太坊状态的各项数据。

TODO 获取一下以太坊的 state tree 真实数据看看

MPT 正在被考虑弃用，准备使用 Verkle tree，实现更高效的数据结构。

TODO 简单了解 MPT 之后，重点研究 Verkle tree

目前的节点状态数据包括 1-2TB，其实挺麻烦的，启动节点等还是比较麻烦的。

# 2025.02.07

## [Protocol Design Philosophy](https://epf.wiki/#/wiki/protocol/design-rationale)

Recursive Length Prefix (RLP) 创建新序列化方案的理由在于其他方案的概率性质。RLP 通过简单而确定的序列化解决了这一问题，并保证了绝对的字节级一致性。这是一个序列化数据的算法？

Simple serialize (SSZ) 序列化是将数据结构转换为可以传输并在以后重建的格式的过程。SSZ 是以太坊 2.0 信标链中使用的一种序列化格式。根据 Vitalik 的评论，SSZ 试图解决的一个主要问题是 RLP 不允许 Merkle 化，这将意味着排除了任何简洁轻客户端证明的可能性。因此，无法实现无状态性——而无状态性仍然是当前以太坊研发的关键目标。

Casper Friendly Finality Gadget (FFG) 用于实现 finality，finality 表示的是一个 block 和里面的数据，再也无法被修改或者 remove。通过在 proposal 机制之上，通过选择代表 canonical transaction ledger 的唯一链来最终确定区块。

Byzantine Fault Tolerance (BFT) 拜占庭将军容错是一个分布式计算系统的特性。应对的挑战是在一个去中心化的环境，如何在某些节点故障或者存在恶意行为下达成一致。比如 PoS 就是针对这个问题实现的算法，来确保在去中心化环境下实现一致。

Latest Message Driven Greediest Heaviest Observed Sub-Tree (LMD-GHOST) 是一个分支选择的规则。有点类似 PoW 使用的分叉选择，其中完成最多工作的被选为 canonical chain。

Gasper 是一个完全的 PoS protocl，结合了 casper FFG 和 LMD-GHOST 来推动 Eth2 的共识层机制。

Using a DHT DHT（分布式哈希表）的主要优势在于，它的查找操作在网络中仅产生对数级别的通信开销。因此，它非常适用于在 P2P 网络中查找（查询）内容。但一个直接的问题是：在以太坊中，我们为什么需要查找内容？毕竟，大多数节点都关注相同的内容——即最新的区块。由于共识槽（consensus slot）在每个时刻只会产生一个区块，并且该区块通过gossip 协议进行传播，因此链的最新状态（tip of the chain）始终是一致的。在 BitTorrent 和 IPFS 这样的协议中，DHT 用于存储各种内容，并帮助用户查找他们感兴趣的内容。而在以太坊的网络层，DHT 并不是用于查找区块，而是用于发现不同的对等节点（peers）。

discv5 是一个 Ethereum 使用的 discovery protocol，使用 kademlia based DHT 来存储 ENR records. ENR 记录包括路由信息来建立 P2P 链接。

# 2025.02.08

## [Protocol history and evolution](https://epf.wiki/#/wiki/protocol/history)

几个比较重要的以太坊升级：

- Frontier 是 Ethereum Protocol 的发起，在 2015 7 月 30 日上线，创世区块 <https://etherscan.io/block/0>
- Homestead 在 2016 年 3 月 14 日上线。是一个更加成熟稳定的平台，包括 EIP-2、EIP-7、EIP-8 等升级
- The Merge 在 2022 年 9 月 15 日上线，将共识层机制切换为 PoS。然后 PoS 共识层分开放在了一个新的 Beacon Chain Layer，有自己的 p2p 网络和逻辑。Beacon Chain 从 2020 年 12 月 1 号就开始运行和测试，没有发现什么问题。

# 2025.02.09

开始学习去年 EPFsg 的资料：https://epf.wiki/#/eps/week0

## Week0

[Merkle Tress](https://ethereum.org/en/developers/docs/data-structures-and-encoding/patricia-merkle-trie/)

所有以太坊目前的数据包括 all accounts、balances 和 smart contracts（？合约是怎么用 Merkle Tree 存储的）使用了 Merkle Tree 进行编码。主要好处是一个 root value 可以用于验证数据。

以太坊数据结构是 modified Merkle-Patricia Trie，使用了 PATRICIA 来实现高效数据读取。“Patricia”部分主要是为了减少节点高度、节省存储空间，将重复前缀合并到同一个路径上。

Merkle Tree 是不包含数据的，而是对数据进行 hash 然后链接起来成为一棵树，然后通过提交从叶子节点到根节点的一条 hash 路径来生成或者验证一个数据是否存在或者被篡改。

在以太坊中，用 MPT 来保存“世界状态（全局账户的余额、合约存储等）”。每次状态更新都会导致相应的 MPT 变化，从而生成一个新的根哈希（state root）。

trie 是一种类型的 tree，包括 prefix tree 等，带有一些特殊逻辑的 tree。

# 2025.02.10

对于 radix tree 而言，通过 root hash 的存储查询，是会通过 key-value 的方式，将序列化节点数据存储到了某个地方，这样可以查出来整个树。拿到的节点数据反序列化，例如 Ethereum 的 RLP，然后可以拿到根节点对应的完整结构，包括子节点、前缀信息等。然后继续递归调用查询子节点数据，直到目标的叶子节点。感觉如果树的层级太深会比较麻烦，所以尽量扁平，然后每个树叶子节点也不要太多。

```
   def update(node_hash, path, value):
        curnode = db.get(node_hash) if node_hash else [ NULL ] * 17
        newnode = curnode.copy()
        if path == '':
            newnode[-1] = value
        else:
            newindex = update(curnode[path[0]], path[1:], value)
            newnode[path[0]] = newindex
        db.put(hash(newnode), newnode)
        return hash(newnode)
```

更新 radix 树的操作，就是递归调用遍历 `[i_0, i_1 ... i_n, value]` 这个结构，然后对最后的一个 value 进行更新，同时返回将整个链路的 hash index 更新。

MPT

Radix tries 不够高效，比如 Ethereum EOA 64 characters 长度的地址，每次 lookup 或者 delete 都需要 64 steps。所以 Patricia Trie 引用了下面的办法来解决问题：

A node in a Merkle Patricia trie is one of the following:

- NULL (represented as the empty string)
- branch A 17-item node [ v0 ... v15, vt ]
- leaf A 2-item node [ encodedPath, value ]
- extension A 2-item node [ encodedPath, key ]

由于地址比较长，所以中间或者某段结构，可能并不需要挨个字符进行下降，所以通过 encodedPath 进行存储路径快速下降。

Tries in Ethereum

State Trie

There is one global state trie, and it is updated every time a client processes a block. 路径是 keccak256(ethereumAddress) 然后值是 rlp(ethereumAccount)。具体一点 account 是 `[nonce,balance,storageRoot,codeHash]` 这四个 item。

Storage Trie

Storage trie is where all contract data lives. There is a separate storage trie for each account.

Transactions Trie

路径是 rlp(transactionIndex)。There is a separate transactions trie for every block, again storing (key, value) pairs.

Receipts Trie

Every block has its own Receipts trie. A path here is: rlp(transactionIndex).

TODO 提取一下上面这些 Trie 的原始数据结构，进行解码看看。

# 2025.02.11

## https://medium.com/coinmonks/ethereum-data-transaction-trie-simplified-795483ff3929

![image](https://github.com/user-attachments/assets/1cf70c09-1a4a-48d7-b2c8-52e751b38c89)

Light clients are nodes that do not contain entire blockchain data. Instead, they download only the chain of block headers. They cannot take part in block validation however they can access the blockchain in a similar way as the full node does.

![image](https://github.com/user-attachments/assets/2ccae255-5dfd-4268-a2a3-4de3e51c7898)

轻客户端通过读取对应 block 的 txs 然后自己计算 hashes 来对比 root hash 是不是一样的。通过 merkle tree 来实现的话，然后并不需要全部的 tx 就可以，只需要选择几个就可以了。

![image](https://github.com/user-attachments/assets/3c001a97-fe90-47f5-a39c-b6070cea17dd)

选择要验证的 tx 的相关 hash 即可，因为上层的 hash 节点都是计算生成的。

TODO 跑一下代码 https://github.com/dajuguan/lab/blob/main/eth/randao.py

# 2025.02.12

## https://epf.wiki/#/eps/week1

![image](https://github.com/user-attachments/assets/3635c3a4-c051-4557-a8cb-0621a5b84467)

The Merge 的过程，其实是构建了一个平行的 Beacon Chain 一直在运行和检测，之后把 execution layer 接过来。

As hinted above, the main high level components of Ethereum are execution and consensus layer. These are 2 networks which are connected and dependent on each other. Execution layer provides the execution engine, handles user transaction and all state (address, contract data) while consensus implements the proof-of-stake mechanism ensuring security and fault tolerance.

The traditional development cycle for new features or changes is Idea - Research - Development - Testing - Adoption. However, problems might arise at any moment of this cycle resulting in iterating again from the beginning.

The coordination mainly happens via regular calls which are scheduled in the PM repo.

The ideas and proposed changes from the community are coordinated using EIP process. Additionally, there are a few discussion forums. The biggest one discussing core upgrades is https://ethresear.ch. Another forum which is connected to the EIP process and serves for discussion about specific proposals is Ethereum Magicians. Lots of important discussion is also happening on the R&D Discord server (ping us in EPFsg discord to get an invite) and in client team groups. There are also offsites or workshops where many core developers meet in person to speed up the process face to face.

通过 https://github.com/ethereum/pm 学习到的社区协调和管理经验：

1. 通过创建 issues + tag 来放议题、会议链接等信息，例如 https://github.com/ethereum/pm/issues/1253 包括全部的会议，不仅仅是 ACDE ACDC
2. 提供了一个 Google Calendar 来快速添加，但是目前不知道是自动还是人工维护的
3. 欢迎大家通过评论的方式，添加议题等
4. 写清楚了议题如何添加、谁能参加、谁主持等
5. ECH 提供了字幕稿，然后下面有个大表单，可以看到每次会议的录屏、notes、讨论等等

对 LXDAO 的启发：

- 可以考虑将会议集中在这里管理，避免在论坛占用大家的注意力
- 提供会议的速记和内容稿，作为社区周报的内容，而非比较制式的，重点在于引导大家讨论

TODO https://notes.ethereum.org/@mikeneuder/rcr2vmsvftv

# 2025.02.13

## https://epf.wiki/#/eps/week2

### https://github.com/ethereum/consensus-specs/blob/dev/specs/deneb/beacon-chain.md#modified-process_execution_payload

```
class ExecutionPayload(Container):
    # Execution block header fields
    parent_hash: Hash32 # 上一个区块的 hash，连起来
    fee_recipient: ExecutionAddress  # 'beneficiary' in the yellow paper 执行层中，是区块提交者的地址
    state_root: Bytes32
    receipts_root: Bytes32
    logs_bloom: ByteVector[BYTES_PER_LOGS_BLOOM] # 用于日志过滤的 bloom 过滤器，用于快速查找日志
    prev_randao: Bytes32  # 'difficulty' in the yellow paper
    block_number: uint64  # 'number' in the yellow paper
    gas_limit: uint64
    gas_used: uint64
    timestamp: uint64
    extra_data: ByteList[MAX_EXTRA_DATA_BYTES]
    base_fee_per_gas: uint256
    # Extra payload fields
    block_hash: Hash32  # Hash of execution block
    transactions: List[Transaction, MAX_TRANSACTIONS_PER_PAYLOAD]
    withdrawals: List[Withdrawal, MAX_WITHDRAWALS_PER_PAYLOAD] # 目前区块的提款列表
    blob_gas_used: uint64  # [New in Deneb:EIP4844]
    excess_blob_gas: uint64  # [New in Deneb:EIP4844]
```

需要进行能力扩展和数据增加，就是通过类似 EIP4844 这样的标准，创建新的标准，然后客户端来实现读取和保存记录。

真实的信息和数据：

![image](https://github.com/user-attachments/assets/185dcd23-b49a-4980-8c9a-f6f66d365543)

![image](https://github.com/user-attachments/assets/51da5284-ff7a-44af-8b53-b286f9e35555)

![image](https://github.com/user-attachments/assets/7861ddc2-dc22-4da3-84aa-406d639f2eda)

logs_bloom 的工作原理：

- logs_bloom 是一个固定大小的位数组，通常为256字节，即2048位。
- 当一个新的日志被添加到区块中时，计算该日志的哈希值，并使用多个哈希函数（如3个）生成多个哈希值。
- 将这些哈希值映射到logs_bloom的位数组中，将对应的位设置为1。
- 查询某个日志是否存在于某个区块的时候，只需要计算日志的 hash，然后快速检查 logs_bloom 的对应的位置是否全部为 1，如果是，那么日志可能在当前区块。可能会存在误报
- 通过这个，可以快速过滤不包含特定日志的区块，提高检索效率，比如查询 event 发生在哪些区块，从而仅仅加载和处理相关区块

TODO Hackerscan 可以加入查看原始区块信息的功能，没有找到 logs_bloom 的原始数据

TODO Contract Internal Transactions 是什么？跟 Block 的 transactions 区别是什么？

TODO 明天把整个区块的所有信息和内容过一下 https://etherscan.io/block/21833528 https://eth.blockscout.com/block/21833528?tab=index

TODO randao
TODO withdrawals 提款工作原理？

# 2025.02.14

## https://epf.wiki/#/eps/week2

LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.

一个原始的 block 数据（deneb）：

```
{
  "slot": "8631513",
  "proposer_index": "1124880",
  "parent_root": "0x5a585679198d1bae7f337f987496d22c9f0db95fb1bcd4d8069a74be0e76a5ae",
  "state_root": "0x855b6335a3b955443fb14111738881680817a2de050a1e2534904ce2ddd8e5e0",
  "body": {
    "randao_reveal": "0x8c290463d6e68154d171deeca3a4d8d8fa276c72e9c34094f8b6bf89e551e99d63162e362a936b628af4840d69b10c24191e892d0a282bb5358a5669f44e42b627ebeb63fd6467c7aad62636a348b5f4edfb8ce01650e4d079339d9dc5700f05",
    "eth1_data": {
      "deposit_root": "0x636ab1747c976fe08cf337b437ccbb5f543e0d0c6b5d70097c3ab7737c1748d5",
      "deposit_count": "1342638",
      "block_hash": "0x429813f0390a9e104740e8a24ebb83ac03929dff4a9702385f2bf24391ba754b"
    },
    "graffiti": "0x526f636b617761795820496e6672610000000000000000000000000000000000",
    "proposer_slashings": [],
    "attester_slashings": [],
    "attestations": [
      {
        "aggregation_bits": "0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff7f",
        "data": {
          "slot": "8631512",
          "index": "19",
          "beacon_block_root": "0x5a585679198d1bae7f337f987496d22c9f0db95fb1bcd4d8069a74be0e76a5ae",
          "source": {
            "epoch": "269733",
            "root": "0x508880ef7fe7cac1a601bcb00868cc41a523497b34d85fb71dc338f891eb049b"
          },
          "target": {
            "epoch": "269734",
            "root": "0x89926ca6add36803c7239a78f78af0fb91df932f8af2ac34d4cf89998ea3ec68"
          }
        },
        "signature": "0x903146f136e4df8200be0229eb96bc9a2409d04763df61ebba51f54cfbd9eca2c88274cb94828c2705bff1454c50322e03372883c2dd47ee329cd17a3653f44314fa8693c73fa2097f622e7f2e163f7b7cb688aebad93e14c273d406743ec7ad"
      },
      {
        "aggregation_bits": "0xffffffffffbfffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff7f",
        "data": {
          "slot": "8631512",
          "index": "27",
          "beacon_block_root": "0x5a585679198d1bae7f337f987496d22c9f0db95fb1bcd4d8069a74be0e76a5ae",
          "source": {
            "epoch": "269733",
            "root": "0x508880ef7fe7cac1a601bcb00868cc41a523497b34d85fb71dc338f891eb049b"
          },
          "target": {
            "epoch": "269734",
            "root": "0x89926ca6add36803c7239a78f78af0fb91df932f8af2ac34d4cf89998ea3ec68"
          }
        },
        "signature": "0x99d3c97b5036025d1b30ac32efd469a815269e2575a7525b1cc8323db85556aef7af7464d965ab9b6ee1804005436a0b05faf870cb213dff04552ddffcfe355987d35201e58dce3897c0de27a19016321fba9ac346452755ae9340f60cea895d"
      }
    ],
    "deposits": [],
    "voluntary_exits": [],
    "sync_aggregate": {
      "sync_committee_bits": "0xfffffffffffffffeffffffffffffffffffbffffffffffffffffffdfffffffbffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "sync_committee_signature": "0xae953c135ac95f1cd669a8caf9e89770483bdf3dbf138b2dfdd76198e9baac00ab4d807b518ebfa9e665a8a78dab9c210ff7a073b85fef1e75ccd49f0747c73fe850f9e87c63985f9bf5d795c28474c4ea67716e194a320382c6d9e560aebc9e"
    },
    "execution_payload": {
      "parent_hash": "0x5cb0f2822e542e2c6fbc0099aa8f996509c178bfaa634e04b728add8da42c65d",
      "fee_recipient": "0x95222290dd7278aa3ddd389cc1e1d165cc4bafe5",
      "state_root": "0xca4e0ab986d29ee5bddd8b4b9d9481e90d7bbd1ce7ee9e0d077c89ba03cdcf32",
      "receipts_root": "0x09fdee17a2dafb2328798f9e47b44e50a5a8e5d9951929afa51f70fc222846c2",
      "logs_bloom": "0xbffdca4be5945bfbba8a8ed5eadb7ff2dcefce7f6cb67b94cf81ad38dc9a943b76e541efe10b2768ded9de385ffdd9596b79a4ecffbafd407ffca3453cff2d9ebf7f57ffe3069abb7eebf66eddc460ecd9ef7ded9c67de1b1ccb7ce9e9f9cf7e3fdcdc2fbe974ae2be4cd35271d47b5bda4459fde93d3f0bead5c558997b18386ef38ff77e234f6eb7cda7d47bee4ab6b273b8f9ffb37d5be6ffb7dac9ffbd36ffc6eb33ffaa7f832f264dc5f9966fed1fc7c0fdf6fb719e7fb39b6e38dddfe3defbde6a7668fb7f2166e79fb8df91adbd73545fbf3ae59caeedf7df6937fc5039fafaff21fd720fd9f5d6a3e85798e0d7abde86f3a6afff6383fb0beefcdc0f",
      "prev_randao": "0xb48f684132ba484557c07ea6964d6b3841607a44a540a24dd31cbbccb14f06a5",
      "block_number": "19431837",
      "gas_limit": "30000000",
      "gas_used": "28138718",
      "timestamp": "1710402179",
      "extra_data": "0x6265617665726275696c642e6f7267",
      "base_fee_per_gas": "44330915133",
      "block_hash": "0x4cf7d9108fc01b50023ab7cab9b372a96068fddcadec551630393b65acb1f34c",
      "transactions": [
        "0x02f904b40183222e6b80850a5254153d8303adab946b75d8af000000e20b7a7ddf000ba900b4009a808509bafeda9db83a7f381ce270557c1f68cfb577b856766310bf8b47fd9ce8d11a5b113a7a922aea89288d8c91777beecc68df4a17151df102bbfc4140e8c3d5e806f90407f8bc94e485e2f1bab389c08721b291f6b59780fec83fd7f8a5a0ddf68a16e33fcf794c93d34148c2e2c4391f4f3f27ff7a52703ddbcdb5c569f0a0b39e9ba92c3c47c76d4f70e3bc9c3270ab78d2592718d377c8f5433a34d3470aa09edbdabec2e16ca41f1efb3c19f5f3d18c604847272628636ea866af352b901ca09bb3e24e1534bce24e9896f3377327d742d6c1d430477b7ebc070c2eb64e3147a0000000000000000000000000000000000000000000000000000000000000000bf859941ce270557c1f68cfb577b856766310bf8b47fd9cf842a0b39e9ba92c3c47c76d4f70e3bc9c3270ab78d2592718d377c8f5433a34d3470aa094fe3377ad59f5716da176e7699b06460ce5b4208f8313f3d26113b1cf3d3170f8dd947054b0f980a7eb5b3a6b3446f3c947d80162775cf8c6a00000000000000000000000000000000000000000000000000000000000000007a00000000000000000000000000000000000000000000000000000000000000009a0000000000000000000000000000000000000000000000000000000000000000aa0000000000000000000000000000000000000000000000000000000000000000ca00000000000000000000000000000000000000000000000000000000000000008a00000000000000000000000000000000000000000000000000000000000000006f85994c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2f842a0051234925bf172ac8e2ccbd292c65330169d67445a0966551f13a5df19bb9321a012231cd4c753cb5530a43a74c45106c24765e6f81dc8927d4f4be7e53315d5a8f8bc94a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48f8a5a0d2764b6d304d6875dc1632274f53a7d27047ae66fe20f57cce9fb878c86ccdeaa010d6a54a4754c8869d6886b5f5d7fbfa5b4522237ea5c60d11bc4e7a1ff9390ba07050c9e0f4ca769c69bd3a8ef740bc37934f8e2c036e5a723fd8ee048ed3f8c3a00000000000000000000000000000000000000000000000000000000000000001a0154bb98efc83b034ad81fbf23cc88c9737739df170c146ea18e8113dac893665d69443506849d7c04f9138d1a2050bbf3a0c054402ddc0f8dd947a922aea89288d8c91777beecc68df4a17151df1f8c6a00000000000000000000000000000000000000000000000000000000000000008a00000000000000000000000000000000000000000000000000000000000000006a00000000000000000000000000000000000000000000000000000000000000007a00000000000000000000000000000000000000000000000000000000000000009a0000000000000000000000000000000000000000000000000000000000000000aa0000000000000000000000000000000000000000000000000000000000000000c80a0bc7a0020d84346ad4ffdce908fbf7291f7f7f251a6381bd43583f02606a05471a04acbaeb9886f864bc654123665b91e527623fd2a9225e1371e061ecf5fa4dbf8",
        "0x02f9017501829a308502540be400850f8839d18083061a80947a250d5630b4cf539739df2c5dacb4c659f2488d80b9010438ed17390000000000000000000000000000000000000003221ceed0394f7b8ef2b12118000000000000000000000000000000000000000000000000213a0fe9640f2a2d00000000000000000000000000000000000000000000000000000000000000a00000000000000000000000001d283807630ffb876a5d78b8e0788e491449f2410000000000000000000000000000000000000000000000000000018e3bee84e100000000000000000000000000000000000000000000000000000000000000020000000000000000000000001ce270557c1f68cfb577b856766310bf8b47fd9c000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2c001a036e76fbcbc86dd2d6fe3d37e65ca3e83aec7259a850b28686fece7105c1d2a24a06c4b4d44d359c9360b8ebf2554eacae621824441f00d99275be3bfd01f554239",
        "0x02f87201830bbc2a80850a5254153d827d0094388c818ca8b9251b393131c08a736a67ccb19297880185a6d6be627f3280c080a038cbd7a4589d49f061b88da94c6d16e085faed4ea61f60a744d781bea95862a3a061eb4b1dc235a3fdb04c589150326d7e49089439428c22ced7bc7ddb559edd37"
      ],
      "withdrawals": [
        {
          "index": "38350022",
          "validator_index": "171011",
          "address": "0x8626354048f90faafc212c07ec7f3613406b1b32",
          "amount": "18545672"
        },
        {
          "index": "38350023",
          "validator_index": "171012",
          "address": "0x8626354048f90faafc212c07ec7f3613406b1b32",
          "amount": "18561699"
        }
      ],
      "blob_gas_used": "131072",
      "excess_blob_gas": "0"
    },
    "bls_to_execution_changes": [],
    "blob_kzg_commitments": [
      "0x97d62d4572935295f909f243714201d9221215bfcc91af6546d28d2e52040577a77957256c530ca25974f6a814511b1a"
    ]
  }
}
```

# 2025.02.17

开始跟随官方的 EPFsg 高强度学习 https://epf.wiki/#/eps/intro，其实就是复习，但是要确保一天能完成一个主题。

今天我把 Execution Layer W2 的收尾完成掉。

## https://epf.wiki/#/eps/week2

看了下视频，其实整个执行层的运行还是比较简单的，无非就是去将 env、tx、state 等进行执行和验证，确保 gas 没有超出，然后出块等。然后修改到 stateDB 上面，相当于一个状态函数转移。

在 txpool.Pop() 的时候，先按照 paying gas to the builder 进行排序，然后取出来最大收益的 tx。

EL 会判断如果 tx 是 invalid 就不会发到 CL 了，只是负责打包等。加密 mempool 有待解决。

打算把 go-ethereum 的代码跑起来，直接 debug 看源代码，暂时卡住了，对 Go 语言不熟悉。

# 2025.02.18

因为后面的一些实现逻辑等想直接看 go-ethereum 代码了，所以花了一些时间研究如何使用 dlv 来 debug go。结果发现 VSCode 默认就支持针对 Unit Test 的 debug，在可以执行的方法上面会有 debug test 按钮，下断点，点一下就可以进入 debug 模式。实在是太高级太简单了。

![image](https://github.com/user-attachments/assets/54ce4bcd-d4cd-480c-b6f3-18c73e7fbdcf)


然后通过 AI 工具帮忙找到对应的功能，直接就可以开始下断点 debug 看看具体的实现逻辑：

![image](https://github.com/user-attachments/assets/11a14590-3a2c-4f2d-acc2-967d8268f536)

# 2025.02.19

## https://epf.wiki/#/eps/week2

EL 主要就是 Block 验证和 Block 构建，验证包括 state 转移、evm 执行、EIP 等新的 gas 逻辑等、构建 block，因此需要一个基于 p2p 的 tx pool。

状态转移函数在 [state_processor.go](https://github.com/ethereum/go-ethereum/blob/master/core/state_processor.go#L57) 的 Process 方法里面，主要用途验证 merkle roots、gas limit、timestamp 等。Debug 一下测试用例，一些观察如下：

// Process returns the receipts and logs accumulated during the process and
// returns the amount of gas that was used in the process. If any of the
// transactions failed to execute due to insufficient gas it will return an error.


![image](https://github.com/user-attachments/assets/8af10a0e-2572-452a-94be-2a55e5871ea9)

这个就是 GO 里面对于 hash 的存储方式，一般是 32 bytes，或者是以一个拼接 16 进制字符串 `|\xbex\x8e\x04\xd1M\xeeD}\x83Cj\xc4s\x1d\xa6\bt\xe6\v?\x85\xcf\xcbI\x8b\xb0\xe4\xdd\xf33` 这样。

![image](https://github.com/user-attachments/assets/f832d6e2-4495-46b1-ad8e-65bb910f9ac3)

The DAO 事件反复拉出来被讨论，早已从一个简单的问题上升到了社会学和哲学层面，Ethereum 也分叉成了 ETH 和 ETC，其实实际上背后的代码就是这么朴实无华的一堆硬编码：遍历这些黑客钱包，把他们的余额转移到 refund 合约地址。🤣

var tracingStateDB = vm.StateDB(statedb) TODO 有空研究下 StateDB 的底层存储模式是什么，似乎是 LevelDB。

会先构建一个 EVM Context 来继续执行，包括一些基本配置参数：

```
vm.BlockContext{
		CanTransfer: CanTransfer,
		Transfer:    Transfer,
		GetHash:     GetHashFn(header, chain),
		Coinbase:    beneficiary,
		BlockNumber: new(big.Int).Set(header.Number),
		Time:        header.Time,
		Difficulty:  new(big.Int).Set(header.Difficulty),
		BaseFee:     baseFee,
		BlobBaseFee: blobBaseFee,
		GasLimit:    header.GasLimit,
		Random:      random,
	}
```

然后创建一个 evm 进行执行：`evm := vm.NewEVM(context, tracingStateDB, p.config, cfg)`。

![image](https://github.com/user-attachments/assets/16219e97-b87d-402f-b209-e927f5559f71)

预编译合约的实现就是在 evm 进行加载，根据相应的参数，找到对应的合约编译到 EVM 里面。具体内容在 contracts.go 文件。

```
var PrecompiledContractsPrague = PrecompiledContracts{
	common.BytesToAddress([]byte{0x01}): &ecrecover{},
	common.BytesToAddress([]byte{0x02}): &sha256hash{},
	common.BytesToAddress([]byte{0x03}): &ripemd160hash{},
	common.BytesToAddress([]byte{0x04}): &dataCopy{},
	common.BytesToAddress([]byte{0x05}): &bigModExp{eip2565: true},
	common.BytesToAddress([]byte{0x06}): &bn256AddIstanbul{},
	common.BytesToAddress([]byte{0x07}): &bn256ScalarMulIstanbul{},
	common.BytesToAddress([]byte{0x08}): &bn256PairingIstanbul{},
	common.BytesToAddress([]byte{0x09}): &blake2F{},
	common.BytesToAddress([]byte{0x0a}): &kzgPointEvaluation{},
	common.BytesToAddress([]byte{0x0b}): &bls12381G1Add{},
	common.BytesToAddress([]byte{0x0c}): &bls12381G1MultiExp{},
	common.BytesToAddress([]byte{0x0d}): &bls12381G2Add{},
	common.BytesToAddress([]byte{0x0e}): &bls12381G2MultiExp{},
	common.BytesToAddress([]byte{0x0f}): &bls12381Pairing{},
	common.BytesToAddress([]byte{0x10}): &bls12381MapG1{},
	common.BytesToAddress([]byte{0x11}): &bls12381MapG2{},
}
```

每次升级进行添加，必须要保持向前兼容，分配一个固定的位置方便合约调用。实现的接口是：

```
type PrecompiledContract interface {
	RequiredGas(input []byte) uint64  // RequiredPrice calculates the contract gas use
	Run(input []byte) ([]byte, error) // Run runs the precompiled contract
}
```

比如 ecrecover 的实现就是：

```
// ecrecover implemented as a native contract.
type ecrecover struct{}

func (c *ecrecover) RequiredGas(input []byte) uint64 {
	return params.EcrecoverGas
}

func (c *ecrecover) Run(input []byte) ([]byte, error) {
	const ecRecoverInputLength = 128

	input = common.RightPadBytes(input, ecRecoverInputLength)
	// "input" is (hash, v, r, s), each 32 bytes
	// but for ecrecover we want (r, s, v)

	r := new(big.Int).SetBytes(input[64:96])
	s := new(big.Int).SetBytes(input[96:128])
	v := input[63] - 27

	// tighter sig s values input homestead only apply to tx sigs
	if !allZero(input[32:63]) || !crypto.ValidateSignatureValues(v, r, s, false) {
		return nil, nil
	}
	// We must make sure not to modify the 'input', so placing the 'v' along with
	// the signature needs to be done on a new allocation
	sig := make([]byte, 65)
	copy(sig, input[64:128])
	sig[64] = v
	// v needs to be at the end for libsecp256k1
	pubKey, err := crypto.Ecrecover(input[:32], sig)
	// make sure the public key is a valid one
	if err != nil {
		return nil, nil
	}

	// the first byte of pubkey is bitcoin heritage
	return common.LeftPadBytes(crypto.Keccak256(pubKey[1:])[12:], 32), nil
}
```

所以这里的实现还挺重要的，不能有问题，以后也不能随便改。由于直接在客户端上执行，gas 消耗比较低，性能比较高，但是不能加入太多，太多的话会导致客户端代码和复杂度增加。

TODO debug 到 	evm := vm.NewEVM(context, tracingStateDB, p.config, cfg) 了，明天继续 debug 完。



---

EVM 主要是一个 stack machine。The Ethereum VM is a stack-based, big-endian VM with a word size of 256-bits and is used to run the smart contracts on the Ethereum blockchain.
Smart contracts are just like regular accounts, except they run EVM bytecode when receiving a transaction, allowing them to perform calculations and further transactions.
Transactions can carry a payload of 0 or more bytes of data, which is used to specify the type of interaction with a contract and any additional information.

TODO EVM 是如何将 EVM bytecode 一步步执行的？Debug 一个简单的




p2p 主要是三件工作，t包括历史数据、pending txs、状态同步，同时可以通过 snap 文件的方式快速的同步状态。


fork 了一个学习注解版本的 go-ethereum 仓库 https://github.com/brucexu-eth/go-ethereum/commit/16ab6c3351a9cd5f612633409e7828876e1a37b0 方便大家使用，使用 cursor 生成自己想要的 unit test 进行 debug，很方便。

# 2025.02.20

继续 debug EL 的代码。

```
// IsVerkle returns whether time is either equal to the Verkle fork time or greater.
func (c *ChainConfig) IsVerkle(num *big.Int, time uint64) bool {
	return c.IsLondon(num) && isTimestampForked(c.VerkleTime, time)
}
```

使用检测时间的方式使升级生效，所以客户端都是提前更新和部署的，定好区块时间上线。这里面估计有一些协调工作。

Go debug 的时候，如果要执行某个方法，需要在 debug console 里面使用 `call value.String()` 这样的方式，添加 call。

```
evm := &EVM{
	Context:     blockCtx,
	StateDB:     statedb,
	Config:      config,
	chainConfig: chainConfig,
	chainRules:  chainConfig.Rules(blockCtx.BlockNumber, blockCtx.Random != nil, blockCtx.Time),
	jumpDests:   make(map[common.Hash]bitvec),
}
```

这个 jumpDests 还挺有意思的，是 EVM 里面用于优化 JUMP/JUMPI 指令执行的缓存，先把合约代码里面有效的跳转目标位置进行记录，方便进行跳转。bitvec 位向量用于标记代码哪些位置是有效的跳转目标，但是具体的运算逻辑还不是很清楚。

![image](https://github.com/user-attachments/assets/8786f08d-d9ec-4992-8afd-49015b6ccf42)

会提前将 transaction 转换成 message，然后 apply 到 evm 上面，然后就到了具体的执行逻辑，TODO 明天继续看

![Cursor 2025-02-20 19 30 28](https://github.com/user-attachments/assets/d01269a7-5d92-42bd-9a10-c9156fefbf27)


# 2025.02.21

今天搭建一下 node 玩玩 https://epf.wiki/#/eps/nodes_workshop

去年跑过，我的笔记和命令 https://github.com/IntensiveCoLearning/ethereum-protocol/blob/main/brucexu.md#52

下载最新版的，然后执行：

```
# Generate jwtsecret
openssl rand -hex 32 > ./jwt

./geth --holesky --datadir ./geth-data --syncmode snap --http --http.port 8545 --authrpc.jwtsecret ./jwt --authrpc.port 8551

./lighthouse bn --network holesky --execution-endpoint http://localhost:8551 --datadir ./lh-data --execution-jwt ./jwt --http --checkpoint-sync-url https://holesky.beaconstate.ethstaker.cc/
```

然后等待同步就可以了。

![image](https://github.com/user-attachments/assets/1df5ea9c-345c-4982-b46c-46d86878f7f0)


# 2025.02.23

继续 debug processor logic 里面的 evm 和后续 tx 的逻辑：

```
func (st *stateTransition) execute() (*ExecutionResult, error) {
	// First check this message satisfies all consensus rules before
	// applying the message. The rules include these clauses
	//
	// 1. the nonce of the message caller is correct
	// 2. caller has enough balance to cover transaction fee(gaslimit * gasprice)
	// 3. the amount of gas required is available in the block
	// 4. the purchased gas is enough to cover intrinsic usage
	// 5. there is no overflow when calculating intrinsic gas
	// 6. caller has enough balance to cover asset transfer for **topmost** call

```

测试用例有点问题，需要修改参数继续下去，目前会报错显示 gas 不足。

# 2025.02.24

执行层的 JSON-RPC 规范文档 https://ethereum.github.io/execution-apis/api-documentation/

## https://hackmd.io/@danielrachi/engine_api

两个客户端先通过 engine_exchangeCapabilities and engine_forkchoiceUpdatedV2 握手建立通信。

不停地 call API 进行探测是否同步完成了 blocks。

构建一个 Block 的流程：

![image](https://github.com/user-attachments/assets/5469d351-2efc-4483-8697-f4e128760b2b)

先是 Validator 被选中出块，然后构建 execution_payload 然后被 CL 读取，将执行结果放在 BeaconBlock 上面，然后计算 state_root 发送 Block 出去。

# 2025.02.25

## https://gisli.hamstur.is/2020/08/understanding-ethereum-by-studying-the-source-code/

### Account model

core/state/state_object.go

```
// Account is the Ethereum consensus representation of accounts.
// These objects are stored in the main account trie.
type Account struct {
	Nonce    uint64
	Balance  *big.Int
	Root     common.Hash // merkle root of the storage trie
	CodeHash []byte
}
```

### p2p network

The Ethereum Node Records (ENR) is an open format for peer-to-peer connectivity information. 

```
p2p/enr/enr.go

// Record represents a node record. The zero value is an empty record.
type Record struct {
	seq       uint64 // sequence number
	signature []byte // the signature
	raw       []byte // RLP encoded record
	pairs     []pair // sorted list of all key/value pairs
}

p2p/enode/node.go

// ID is a unique identifier for each node.
type ID [32]byte

// Node represents a host on the network.
type Node struct {
	r  enr.Record
	id ID
}

// Load retrieves an entry from the underlying record.
func (n *Node) Load(k enr.Entry) error {
	return n.r.Load(k)
}

// IP returns the IP address of the node. This prefers IPv4 addresses.
func (n *Node) IP() net.IP {
	var (
		ip4 enr.IPv4
		ip6 enr.IPv6
	)
	if n.Load(&ip4) == nil {
		return net.IP(ip4)
	}
	if n.Load(&ip6) == nil {
		return net.IP(ip6)
	}
	return nil
}
```

### Networks and their genesis

```
params/config.go

	// MainnetChainConfig is the chain parameters to run a node on the main network.
	MainnetChainConfig = &ChainConfig{
		ChainID:             big.NewInt(1),
		HomesteadBlock:      big.NewInt(1150000),
		DAOForkBlock:        big.NewInt(1920000),
		DAOForkSupport:      true,
		EIP150Block:         big.NewInt(2463000),
		EIP150Hash:          common.HexToHash("0x2086799aeebeae135c246c65021c82b4e15a2c451340993aacfd2751886514f0"),
		EIP155Block:         big.NewInt(2675000),
		EIP158Block:         big.NewInt(2675000),
		ByzantiumBlock:      big.NewInt(4370000),
		ConstantinopleBlock: big.NewInt(7280000),
		PetersburgBlock:     big.NewInt(7280000),
		IstanbulBlock:       big.NewInt(9069000),
		MuirGlacierBlock:    big.NewInt(9200000),
		Ethash:              new(EthashConfig),
	}
```

一些 blockchain 的启动参数。

```
core/genesis.go

// GenesisAlloc specifies the initial state that is part of the genesis block.
type GenesisAlloc map[common.Address]GenesisAccount

// DefaultGenesisBlock returns the Ethereum main net genesis block.
func DefaultGenesisBlock() *Genesis {
	return &Genesis{
		Config:     params.MainnetChainConfig,
		Nonce:      66,
		ExtraData:  hexutil.MustDecode("0x11bbe8db4e347b4e8c937c1c8370e4b5ed33adb3db69cbdb7a38e1e50b1b82fa"),
		GasLimit:   5000,
		Difficulty: big.NewInt(17179869184),
		Alloc:      decodePrealloc(mainnetAllocData),
	}
}

func decodePrealloc(data string) GenesisAlloc {
	var p []struct{ Addr, Balance *big.Int }
	if err := rlp.NewStream(strings.NewReader(data), 0).Decode(&p); err != nil {
		panic(err)
	}
	ga := make(GenesisAlloc, len(p))
	for _, account := range p {
		ga[common.BigToAddress(account.Addr)] = GenesisAccount{Balance: account.Balance}
	}
	return ga
}
```


**RLP**（**Recursive Length Prefix**）是以太坊中用于**序列化**（或编码）任意嵌套的、基于字节序列的结构的一种编码方式。它的设计初衷是为了在以太坊的各类数据（如账户信息、交易、区块头、默克尔树节点等）之间进行高效和一致的编码与传输。下面对 RLP 的要点进行简要说明：

1. **用途与定位**  
   - **通用编码方案**：以太坊需要一种通用的编码方式，能够对各种结构化数据进行打包并在网络上传输。RLP 就是以太坊底层所使用的编码规范，可以应用于简单的字符串、数字、列表，以及嵌套列表（比如多层数组）的编码中。
   - **与 JSON、Protobuf 等的区别**：相比于 JSON 或者 Protocol Buffers（Protobuf），RLP 更加轻量、格式更紧凑，且易于在智能合约、区块链节点之间做快速处理。此外，RLP 只关心原始字节，不关心实际的字段含义或数据类型（例如字符串或数字），这使得它非常灵活。

2. **编码规则**  
   RLP 通过“前缀 + 数据”的方式来表示一个元素（或列表）。  
   - **单个字节**：如果一个字符串（或数字在字节层面的表示）本身只包含一个字节，且数值小于 0x80，那么编码后就是它自己，不需要前缀。  
   - **字符串/字节序列**：对于长度在 0～55 字节之间的非单字节数据，RLP 使用 0x80 + 数据长度作为前缀。若字符串长度超过 55 字节，则采用 0xB7 之后再紧跟表示长度的字节数，之后再跟原始数据。  
   - **列表**：列表同理。长度在 0～55 字节之间时使用 0xC0 + 列表编码后字节长度作为前缀。如果列表整体长度超过 55 字节，就使用 0xF7 之后再紧跟表示长度的字节数，然后再跟列表的原始内容。

3. **示例**  
   - 如果要编码一个空字符串 `""`：  
     - 空字符串表示长度为 0，于是编码结果是 `0x80`。  
   - 如果要编码单个字节 `0x05`（也就是整数 5 的字节形式），因为它小于 0x80，所以直接就是 `0x05`。  
   - 如果要编码字符串 `"cat"`（ASCII：0x63 0x61 0x74），其长度为 3，因此前缀会是 `0x80 + 3 = 0x83`，后面跟上 “cat” 的字节，所以编码结果为 `0x83 63 61 74`。  
   - 如果是包含多个元素的列表（比如 `[ "cat", "dog" ]`），则先分别对 `"cat"` 和 `"dog"` 做 RLP 编码，再将两者拼起来，再对拼起来的结果前面加上表示“列表长度”的前缀。

4. **在以太坊中的应用场景**  
   - **交易数据**：以太坊交易会用 RLP 对地址、金额、nonce 等字段进行打包。  
   - **区块数据**：区块头及区块中其他结构（如交易列表、叔块列表等）的编码、解码都使用 RLP。  
   - **存储及默克尔树节点**：在以太坊的 Patricia Trie（Merkle Patricia Trie）里，节点也是以 RLP 形式存储或进行网络传输。

5. **优势**  
   - **紧凑性**：RLP 的编码相对简单并且紧凑，尽可能减少冗余信息，提高存储及网络传输效率。  
   - **实现简单**：RLP 的编码解码逻辑并不依赖具体的数据结构定义，是一套通用的字节级别编码规则，因此很容易在不同编程语言里实现。  
   - **灵活性**：不对字段意义做过多限制，专注于把任意的（嵌套）字节序列结构给“打包”好。

6. **局限性**  
   - **缺乏数据类型语义**：例如，对一串字节，你并不知道它到底是字符串还是数字，需要结合上层逻辑解释。  
   - **调试不如 JSON、Protobuf 直观**：用工具查看 RLP 编码的二进制数据会相对抽象，阅读不如 JSON 或其他更高级别编码来得友好，需要一些解码器工具。

---

综上，**RLP** 就是在以太坊中非常核心的**底层数据编码协议**。它以简洁的前缀规则对各类数据进行序列化，为以太坊在网络与存储中的高效数据传输和存储提供了基础。

# 2025.02.26

### Connecting via bootnodes

```
// MainnetBootnodes are the enode URLs of the P2P bootstrap nodes running on
// the main Ethereum network.
var MainnetBootnodes = []string{
	// Ethereum Foundation Go Bootnodes
	"enode://d860a01f9722d78051619d1e2351aba3f43f943f6f00718d1b9baa4101932a1f5011f16bb2b1bb35db20d6fe28fa0bf09636d26a87d31de9ec6203eeedb1f666@18.138.108.67:30303", // bootnode-aws-ap-southeast-1-001
	"enode://22a8232c3abc76a16ae9d6c3b164f98775fe226f0917b0ca871128a74a8e9630b458460865bab457221f1d448dd9791d24c4e5d88786180ac185df813a68d4de@3.209.45.79:30303",   // bootnode-aws-us-east-1-001
	"enode://2b252ab6a1d0f971d9722cb839a42cb81db019ba44c08754628ab4a823487071b5695317c8ccd085219c3a03af063495b2f1da8d18218da2d6a82981b45e6ffc@65.108.70.101:30303", // bootnode-hetzner-hel
	"enode://4aeb4ab6c14b23e2c4cfdce879c04b0748a20d8e9b59e25ded2a08143e265c6c25936e74cbc8e641e3312ca288673d91f2f93f8e277de3cfa444ecdaaf982052@157.90.35.166:30303", // bootnode-hetzner-fsn
}
```

节点启动的时候，会去找相关的启动节点。作用？获取一些必要启动信息？会不会有中心化的问题或者被 DDoS 的问题。暂时不知道具体是做什么的。

### Discovering peers

The discovery protocol relies on a Kademlia-like DHT that stores information about Ethereum nodes.

TODO Kademlia-like DHT 是什么？

```
// RequestENR sends ENRRequest to the given node and waits for a response.
func (t *UDPv4) RequestENR(n *enode.Node) (*enode.Node, error) {
	addr, _ := n.UDPEndpoint()
	t.ensureBond(n.ID(), addr)

	req := &v4wire.ENRRequest{
		Expiration: uint64(time.Now().Add(expiration).Unix()),
	}
	packet, hash, err := v4wire.Encode(t.priv, req)
	if err != nil {
		return nil, err
	}

	// Add a matcher for the reply to the pending reply queue. Responses are matched if
	// they reference the request we're about to send.
	rm := t.pending(n.ID(), addr.Addr(), v4wire.ENRResponsePacket, func(r v4wire.Packet) (matched bool, requestDone bool) {
		matched = bytes.Equal(r.(*v4wire.ENRResponse).ReplyTok, hash)
		return matched, matched
	})
	// Send the packet and wait for the reply.
	t.write(addr, n.ID(), req.Name(), packet)
	if err := <-rm.errc; err != nil {
		return nil, err
	}
	// Verify the response record.
	respN, err := enode.New(enode.ValidSchemes, &rm.reply.(*v4wire.ENRResponse).Record)
	if err != nil {
		return nil, err
	}
	if respN.ID() != n.ID() {
		return nil, errors.New("invalid ID in response record")
	}
	if respN.Seq() < n.Seq() {
		return n, nil // response record is older
	}
	if err := netutil.CheckRelayAddr(addr.Addr(), respN.IPAddr()); err != nil {
		return nil, fmt.Errorf("invalid IP in response record: %v", err)
	}
	return respN, nil
}
```

# 2025.02.27

### Propagating blocks

node 起来之后就需要同步全部的 block，通过使用 total difficulty 来判断 peers 中最长的 chain。

这一部分通过 PoW 的已经过时了。

### State transition

验证交易这里，通过 EIP155 标准实现签名，并且进行验证。使用了 Ecrecover 的加密算法，主要是先验证签名的有效性，然后再根据签名恢复出来公钥和钱包地址，通过判断钱包地址是否是签名的地址来确认当前状态有效。EIP-155 是预防交易在不同链上重放。

签名的核心字段：交易的哈希值由 AccountNonce、Price、GasLimit 等字段以及 chainId 计算得出。

签名恢复过程：通过 V、R 和 S 恢复公钥，进而计算出发送者地址。

错误处理：如果 chainId 不匹配或签名无效，会返回相应的错误。

# 2025.02.28

### Executing code in the EVM

TODO EVM 官方技术资料文档 https://ethereum.org/en/developers/docs/evm/

以太坊智能合约是一种底层的 stack-based bytecode 语言，包括一堆 bytes，每个 byte 表示一个操作。

TODO，写一个 byte 对以太坊 EVM 进行调用和计算。

操作作用于下面三种类型的存储：

- The stack，就是运行过程中的堆栈
- Memory 运行内存，byte array
- contract long-term storage，长期存储内容

执行的时候没有指定 tx recipient，就会创建一个新合约，代码存储在 contract account state 里面。第一次运行的时候，会调用 contract constructor 然后创建初始 state 并且返回 final contract bytecode，所以 constructors 在 deploy 之后，就不保存了。

合约之间通过 sending messages 来进行相互调用。

通过 gas 消耗来避免 DDoS 攻击。gas price 是 originator 愿意支付的每个 gas 的价格，gas limit 是 upper bound originator 愿意为这个 tx 支付的，避免全部花完了。实际上需要的 gas 是由智能合约执行的具体 opcode 来决定的，是固定的。类比汽车就是我从 A 到 B 走 100KM 需要固定消耗 15L 的汽油，这个 15L 的汽油就是 15L 的汽油，因为必须要走 100KM 的路。然后汽油价格是每个加油站不一样的，你可以选择便宜的汽油型号或者加油站，也可以选择贵的。那么实际的支出就是 15L x 汽油价格，你可以限制最多花费的价格，比如 100 刀这样最多只能到 100 刀。假如此时 1L 油价 10 刀，那么 100 刀的 Limit 只能跑 10L 对应的距离，也就是无法达到 100KM 的距离，此时在 EVM 里面就会因为 gas 不足，终止这项工作，因为走不到终点。但是由于确实存在运算，或者在路上跑了一段时间，gas 也确实消耗掉了，所以已经消耗的 gas 就不退还了。

需要付出成本，也是阻止滥用的一种方案。

```
core/vm/contract.go

// UseGas attempts the use gas and subtracts it and returns true on success
func (c *Contract) UseGas(gas uint64) (ok bool) {
	if c.Gas < gas {
		return false
	}
	c.Gas -= gas
	return true
}
```

### Transacting

Ethereum uses the ECDSA signature scheme for the secp256k1 elliptic curve. 

Ethereum使用secp256k1椭圆曲线的ECDSA签名方案。加密模块为crypto.Sign提供两种实现，一种依赖用纯Go编写的椭圆曲线密码库，另一种依赖用C编写并通过cgo调用的libsecp256k1。ECDSA签名以一对整数(r,s)的形式返回，每个值的范围为[1,2^256-1]，其中r是随机点R=k*G的x坐标，s=k^-1*(h+r*privKey)是签名者知道消息h=hash(msg)和私钥privKey的证明。对于已签名的交易，节点会按上述方式将其中继到点对点网络。

最关键的是 ECDSA signature scheme allows the public key to be recovered from the signed message together with the signature，通过对比 signature 还原出来的 public key 来验证当前用户是否真正有 private key。

---

对 EVM 感兴趣，后面的时间深入研究下 https://ethereum.org/en/developers/docs/evm/

debug 下代码：https://github.com/ethereumjs/ethereumjs-monorepo/tree/master/packages/evm

# 2025.03.01

## https://ethereum.org/en/developers/docs/evm/

![image](https://github.com/user-attachments/assets/5033f9d6-3b68-44d1-9665-76dcfad20383)

- PC 是什么？怎么运行的

Instead of a distributed ledger, Ethereum is a distributed state machine(opens in a new tab). Ethereum's state is a large data structure which holds not only all accounts and balances, but a machine state, which can change from block to block according to a pre-defined set of rules, and which can execute arbitrary machine code.

State 通过 MPT 存储的庞大数据结构，通过 Hash 将所有账户连接起来并且有一个 root hash。

有两种 txs：1. message calls 2. create contract

合约的创建就是把 smart contract bytecode 进行编码，然后创建了一个 account 将其进行存储。之后有其他的 account 调用 message call 就是执行这个上面的 bytecode。

EVM 的 stack machine 深度是 1024 items，每一个 item 是 256-bit word，这样比较容易适配 256-bit cryptography，例如 Keccak-256 hashes 或者 secp256k1 signatures。

TODO EVM 这边，还需要把 https://ethereumjs.readthedocs.io/en/latest/introduction.html 和对应源代码跑一下，这样就算彻底搞懂了。


<!-- Content_END -->
