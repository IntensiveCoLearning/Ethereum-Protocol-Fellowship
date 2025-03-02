---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Pacific/Honolulu # 夏威夷-阿留申标准时间 (UTC-10)

timezone: America/Anchorage # 阿拉斯加标准时间 (UTC-9)

timezone: America/Los_Angeles # 太平洋标准时间 (UTC-8)

timezone: America/Denver # 山地标准时间 (UTC-7)

timezone: America/Chicago # 中部标准时间 (UTC-6)

timezone: America/New_York # 东部标准时间 (UTC-5)

timezone: America/Halifax # 大西洋标准时间 (UTC-4)

timezone: America/St_Johns # 纽芬兰标准时间 (UTC-3:30)

timezone: America/Sao_Paulo # 巴西利亚时间 (UTC-3)

timezone: Atlantic/Azores # 亚速尔群岛时间 (UTC-1)

timezone: Europe/London # 格林威治标准时间 (UTC+0)

timezone: Europe/Berlin # 中欧标准时间 (UTC+1)

timezone: Europe/Helsinki # 东欧标准时间 (UTC+2)

timezone: Europe/Moscow # 莫斯科标准时间 (UTC+3)

timezone: Asia/Dubai # 海湾标准时间 (UTC+4)

timezone: Asia/Kolkata # 印度标准时间 (UTC+5:30)

timezone: Asia/Dhaka # 孟加拉国标准时间 (UTC+6)

timezone: Asia/Bangkok # 中南半岛时间 (UTC+7)

timezone: Asia/Shanghai # 中国标准时间 (UTC+8)

timezone: Asia/Tokyo # 日本标准时间 (UTC+9)

timezone: Australia/Sydney # 澳大利亚东部标准时间 (UTC+10)

timezone: Pacific/Auckland # 新西兰标准时间 (UTC+12)

---

# Ray

1. 自我介绍
LXDAO builder，正在做 [PGNode](https://pgnode.xyz/)，正在持续深入研究以太坊
2. 你认为你会完成本次残酷学习吗？
会的

## Notes

<!-- Content_START -->

### 2025.02.06

填写了 Survey 2025：https://docs.google.com/forms/d/e/1FAIpQLSf4W3R5LZnUIqXpAw2MwJ4E4Q_YWf9tv-BlR5w8v9ED5LjBjw/viewform

整个 Wiki 在第一次残酷共学的时候已经看过了一遍，这次相当于重新复习一下。

#### 如何使用这份资料
这份资料对于想深入研究以太坊协议的人来说非常棒，可以完整系统的学习以太坊协议层的内容：

- 想深入了解以太坊协议的细节，仔细阅读 `Execution Layer` 和 `Consensus Layer` 两个章节，里面的内容比以太坊官方的文档更加深入
- 想了解以太坊简史及设计理念，阅读 `The Protocol` 章节，里面介绍了以太坊的设计理念和发展简史
- 想了解以太坊的开发模式，阅读 `Development` 和 `Testing and security` 等章节，其中 `Development` 中的 `Dev Resources` 中整理了参与以太坊协议开发需要储备的知识，非常贴心了
- 关于以太坊当前正在进行的前沿研究，阅读 `Research`
- Study Group 2024 中是之前的学习笔记，偏实践，也很值得阅读

#### 对以太坊协议发展的理解
很多人总把以太坊和 BTC 放在一起比较，但其中这两个项目本质上的发展路径是不一样的：
- BTC：诞生就是完全体，协议本身没有做迭代的计划，更多的是安全性的优化和抗量子方面的考量
- Ethereum：初始是一个半成品，一开始就有迭代计划，目前离完全体还有很长的路要走

所以在以太坊的发展过程中，会持续有新的话题产生。因为随着技术的迭代，之前的规划很多都会作废，需要有新的方案诞生，然后继续实现，然后出现新的问题，然后继续解决问题。这会成为以太坊发展过程中的常态。

相比与最初的版本，当前以太坊的协议已经很复杂了，协议复杂化的解决方案就是模块化，The Merge 升级之后，以太坊就已经分成了两个大的模块，后续可能会拆分成更多的模块。模块化的好处很明显，可以封装复杂性，不同模块之间通过 API 来通信，模块内部的实现可以自行迭代，不同模块之间互不影响。确定也很明显，模块增加，理解成本增加，以后可能很难找到一个人能真正完整理解以太坊。

模块化还会带来另外一个问题，以太坊节点的部署难度会增加，而且随着以太坊的发展，节点的种类会越来越多，那么节点的部署门槛可能就会增加，solo-staking 的比例就会不够，这可能会对以太坊的安全性有害，[PGNode](https://pgnode.xyz/)，正在尝试解决这个问题，降低节点的部署门槛。

以太坊的路害很长，还有很多事情可以做，持续 Building。

### 2025.02.07
以太坊之前的[黄皮书](https://ethereum.github.io/yellowpaper/paper.pdf)已经过期了，现在以太坊协议已经拆分成了两个规范，[执行层规范](https://github.com/ethereum/execution-specs)和[共识层规范](https://github.com/ethereum/consensus-specs)。

在拆分之前，以太坊客户端既负责交易的执行、传播，也负责网络共识的达成，在拆分之后，共识层剥离成为单独的共识层，原来的客户端也就成了纯粹的执行层。在拆分之后，执行层和共识层的所承载的功能大致如下：
- 执行层
    - 交易池
    - 状态存储
    - 区块和交易的执行（STF）
    - EVM
- 共识层
    - 共识模块（Gasper = Casper-FFG + LMD-GHOST）
    - 最新区块同步
    - Blob 数据存储
    - Validator 交互

关于执行层和共识层所需要知道的一些事情：
- 执行层和共识层都又自己的 p2p 网络，执行层的 p2p 网络主要用来传播和接收交易，共识层的 p2p 网络主要用来同步最新区块和 blob 数据
- 一个执行层客户端只能连接一个共识层，而共识层可以连接多个执行层和多个 Validator
- 与此同时 Beam Chain 项目也立项了，准备对共识层进行重构，并将大量应用 ZK 技术，没有在当前的共识层上设计是为了减轻技术负债的负担，可以面向未来重新出发，这也是模块化的好处，只要共识层和执行层之间的 API 不变，就可以在模块内部重新设计并开发，而且对于共识层来说，大多数数据是只需要存储一段时间，大多数数据过期之后可以不用存储，对数据兼容性的处理的负担也会比较小


经过这几年的发展，以太坊的客户端多样性得到了很大的提升，越来越多新的客户端被开发出来，Geth 不再是唯一的选择了，其中有个趋势是，使用 rust 开发的的客户端越来越多，其实这也好理解，因为这些客户端始终是运行在单机上的，客户端需要处理的数据和请求越来越多，使用 rust 会将机器的能力发挥的更好，rust 开发或许是一个趋势。


### 2025.02.08

执行层的核心是 EVM，如果把整个以太坊协议看作是**交易驱动的状态机（transaction-based state machine）**，那么 EVM 就是其中的 STF（State transition function），状态机有三个重要的组成部分：
- State
- Inputs
- State transtion function

State 就对应了**世界状态**，Inputs 就对应了**交易**，STF 对应 EVM，可以说这三个才是以太坊协议的核心，其他的组件都是为这三个核心服务的，保证交易能够在 EVM 上正常执行，然后交易带来的变更能够写入世界状态。区块链记录了所有交易执行的过程，这样任何一个节点的世界状态也都是一致的，也无法篡改，而共识层所做的事情就是为了新区块的产生是有序的，新区块的产生是更新世界状态的唯一途径。

但是由于整个以太坊网络是公开的，所以通过 gas 来限制恶意的攻击以及实现按照市场的方式让用户付出对应的成本来来使用以太坊，gas 机制的存在让用户提交的交易在以太坊上执行的次数是有限制的，因此 EVM 被认为是准图灵完备（quasi Turing complete）的。

在初始阶段，以太坊是执行层和共识层在同一个客户端中，完成在 The Merge 升级之后，以太坊分成了两个客户端，**执行层客户端**和**共识层客户端**，这样有好处也有坏处：

坏处：
- 失去了一个简单的共识规则，共识规则变得很复杂
- 失去了真正意义上的 permissionless

好处：
- 减少了能源的消耗
- 带来了更好的可塑性，比如 blob 交易的实现

在分开之后，以太坊构造区块的过程也是由共识层和执行层配合完成，如果 validator 被选中在 slot 中创建区块之后，就会向共识层客户端要求获取区块，共识层客户端就会调用执行层客户端的 fork choice updated API 来生成区块。

共识层在获取到新的区块信息之后，也会传递给执行层客户端，执行层客户端会验证区块头信息是否合法，确认没问题之后就会执行区块中的交易，然后将区块附加到区块链上。

### 2025.02.09

EVM 是为了屏蔽底层操作系统和硬件的差异而创建，这样应用层的代码就可以统一，只需要为 EVM 写一遍，类似Java 中的 JVM。

EVM 中有一些关键的组件：

- EVM bytecode：字节码是将程序表示为一系列的字节（byte），每个字节都表示如下的含义，为了简单，每个字节都是用 16 进制表示：
    - 一个指令（opcode），为了进一步增强理解，把操作码抽象层人类可读的形式，比如 PUSH1，这种简化的字节码称之为 EVM assembly（EVM 汇编）
    - 指令的输入，操作数（operand）
- EVM stack：EVM 的字节码的操作是在一个 stack 中进行的，stack 最大为 1024，如果超出这个范围，就会报 stack underflow error
- Program counter：表示指令的偏移量，表示下一个指令开始的位置
    - JUMP：改变程序计数器的值，从而实现控制流
    - JUMPDEST：标记一个有效的跳转目的地，当 JUMP 执行时，它所跳转的目标位置必须被 JUMPDEST 标记过，JUMPDEST 会标记每个循环的开始位置以及不同条件分支的入口
- Memory：是一个长度为 2^256 次方的字节数组，内存中的初始值都定义为 0，与 EVM 搭配使用
    - 字（Word）与字节（Byte）的区别
        - Byte 就是一个字节，等于 8 位
        - 计算机进行数据处理时，一次存取、加工和传送的数据长度，在不同的计算机系统中可能不同，常见的字长有8 位、16位、32位、64位，比如在 32 位的计算系统中，一个字就是 32 位，也就是 4 个字节
- Storage：EVM 执行的结果都需要写入到 stroage 中，storage 与以太坊地址相关联，并作为世界状态的一部分永久保存，storage 只能通过关联的代码才能访问，EOA 没有代码，因此无法访问自己的 storage

### 2025.02.10
- 无状态化：是以太坊后续发展过程中很重要的一环
    - 当前以太坊节点的运行过程中，每个全节点都需要存储完整的区块链状态信息，其中包含了所有账户的余额、智能合约的存储数据，随着以太坊网络的运行，这些数据在不断的膨胀，导致运行节点的成本持续增加，能运行节点的人也越来越少，这不利于以太坊后续的发展
    - 以太坊无状态化方案想改变这种全节点必须存储完整状态信息的模式，节点无需永久存储完整的区块链状态，而是在需要处理交易时，能够动态的从网络中获取执行交易所需要的状态数据
    - 无状态化的好处：
        - 可以降低节点的运行成本，让更多的开发者可以运行自己的节点
        - 提升网络的去中心化程度，运行节点的 solo-staker 越多，那么网络的去中心化程度就越高，网络就越安全
- Verkle 树：准备用来替代 MPT 树，可以实现很轻量级的验证，为以太坊的无状态化做准备
    - MPT 树的深度更深，生成证明时，需要的数据量非常大
    - Verkle 树更宽，生产证明时所需要的数据更少，当前 Verkle 树的设计中，每个节点有 256 个子节点
    - 对于有有 1000 个数据规模的树，MPT 大概需要 4MB 的证明数据，而 Verkle 树只需要 150 kb 的数据 
- 当前 执行层客户端对数据使用的序列化方式是 RLP，而当前共识层使用的序列化方式是 SSZ
    - RLP：主要为以太坊早期的工作量证明（PoW）阶段设计，侧重于简单性和通用性，能对任意嵌套的二进制数据进行编码，满足当时以太坊基本数据结构的序列化需求。
    - SSZ：（Simple Serialize，简单序列化）是为以太坊共识层设计的，其提供更高效、更安全且确定性更强的序列化方案。

### 2025.02.11
- 共识协议主要的挑战在于在一个不可靠的基础设施上构造一个可靠的分布式系统，这里的不可靠有几个方面：
    - 网络是公开的，可能会被各种攻击
    - 运行节点的基础设施参差不齐，并且有随时宕机的可能，大多数是消费级硬件
    - 网络可能会丢包
    - 节点的运营者可能会配置错误或者作出一些恶意的行为
- 共识协议的研究起源于 1970 年代， 以太坊的共识层的目标是让世界上几十万独立的节点保持有序的同步，每个节点所保存的状态都能达成一致，从而构成一个可靠的分布式系统。
- 拜占庭容错（BFT）和拜占庭将军问题，https://hackmd.io/@kira50/SknuPZMIC
   - BFT 时分布式系统的一个特性，即使某些组件发生故障或者恶意行为，该系统也可以正常运行
   - BFT 在去中心化网络中很重要，因为节点之间的没有信任关系
   - 具有 BFT 的系统可以容忍拜占庭故障
   - 在这类的分布式系统中，达成共识的唯一方式是至少要拥有 2/3 的诚实节点，所以对于以太坊来说，很怕某个质押供应商的占比超过 33%，比如 Lido
   - 常见的解决拜占庭将军问题的算法有：
        - PBFT（Practical Byzantine Fault Tolerance）：基于多数投票的三阶段协议（预准备、准备、提交），要求节点通信达成共识。
            - 应用：Hyperledger Fabric
        - FBA（Federated Byzantine Agreement）：节点自行选择信任的节点集合（法定人数），通过局部共识达成全局一致。
            - 应用：Stellar、Ripple（RPCA）
        - PoW（Proof of Work）：通过计算密集型难题竞争出块权，最长链为有效链，其实 PoW 本身不是共识协议，但是可以实现共识协议
            - 应用：比特币、The Merge 之前的以太坊
        - PoS（Proof of Stake）：根据持币比例选择验证者，降低能耗，PoS 同理，本身不是共识协议，但是可以实现共识协议
            - 应用：The Merge 之后的以太坊（Casper FFG）
         - DPoS（Delegated PoS）：持币者投票选举代表节点负责出块，提升效率
            - 应用：EOS、TRON
        - HoneyBadgerBFT：基于异步网络的拜占庭容错协议，通过阈值加密和随机化排序容忍网络延迟
        - Tendermint：结合PBFT与PoS，通过两轮投票达成共识，支持即时最终性。
            - 应用：Cosmos、Binance Chain
        - Algorand（Pure PoS + VRF）：使用可验证随机函数（VRF）随机选择验证者，避免中心化并提升效率
            - 应用：Algorand
        - DBFT（Delegated BFT）：改进PBFT，通过选举少数代表节点降低通信开销
            - 应用：NEO
        - RBFT（Redundant BFT）：在PBFT基础上引入冗余节点和动态主节点切换，提升鲁棒性
            - 应用：Hyperledger Indy
        - Hotstuff：相比于 PBFT 更适合大规模分布式系统，消息复杂度低并有着确定性的共识机制，在节点数据增加是，仍然能保持较好的性能
            - 应用：Celo 
- 在以太坊协议中，节点和验证者是共识系统的参与者，slot 和 epoch 控制共识时间，Block 和 Attestations 是共识系统中的核心要素，达成共识需要依赖这些数据

### 2025.02.12
- 以太坊从 PoW 转成 PoS 的核心原因：能耗高且扩展性有限
    - 以太坊当前的共识协议：LMD GHOST + Casper FFG = Gasper
    - PoW 和 PoS 本身不是共识协议，而是一线共识协议的机制，主要作用是用来抵抗 Sybil 攻击，让参与网络有一定的成本
    - PoW 和 PoS 都是通过分叉选择来选择链的方向：
        - PoW：依据完成的总计算量
        - PoS：依据特定链的总质押价值
- The Merge 在升级的时候使用的是 TTD 而不是区块高度， TTD 其实就是每个区块难度的累加，之所以不使用区块高度，是为了方式有人恶意加速或者减缓 The Merge 升级的进度 
- 以太坊的共识层称之为 Beacon Chain，它负责监督提出和证明新区块的验证者，确保网络的完整性和安全性。
    - Validator 的限制
        - 当前需要质押 32 个 ETH 才能成为 Validator
        - Block Proposer 的选择过程依赖 RANDAO 和 VDF 来保证随机性
        - Validator 会被分成多个委员会，负责区块提议和证明
        - 如果 Validator 作恶，那么他们的资金就会面临处罚
    - slot 和 epoch：每个 slot 12 秒，一个 epoch 为 32 个 slot，每个 slot 都需要指定一名 validator 来提议区块，而验证委员会者证明该区块的有效性
        - Block Proposer 由 RANDAO 选出，选择的过程中，会加权计算 Validator 的余额
        - Validator 可以同时成为 Block Proposer 和 Committees 成员，这种情况很少，概率为 1/32
    - Validator 和 Attestations：Blocker Proposer 时被伪随机（因为缺乏真正的随机院）选择来构建区块的验证者，大多数情况下，验证者时对区块进行投票的 asstester，这些投票记录在信标链中
    - Committees：委员会至少由 128 名验证者组成，在一个 epoch 中，每个 slot 都会分配至少一个 Committees，也就是说在一个 epoch 中，validator 只会存在一个 Committees 中，所以这里也就说明了为什么一个 Validator 在一个 slot 中 同时为 Block Proposer 和 Committees 成员的概率很小
        - Committees 中 Validator 的数量至少要有 128 个
        - 如果网络的 Validator 少于 8192 个，那么就会有一些 slot 的委员会人数不足，如果 Validator 的数量超过 8192 ，那么每个 slot 都至少有两个完整的委员会
        - 如果委员会的规则不足 128，整个网络的 validator 人数少于 4096 时，网络的安全性就会很低
    - Blob 中的数据实际存储在共识层，执行层只存储 blob 的 KZG commitments

### 2025.02.13
 - Checkpoints 和 Finality
    - 在每个 epoch 结束的时候，都会创建 Checkpoint，Checkpoint 为每个 epoch 中 第一个 slot 中的区块，如果没有这个区块，那么 Checkpoint 就是前一个最近的区块，每个 epoch 都需要指定一个 Checkpoint
    - Validator 的投票有两类：
        - 用于 LMD GHOST 的投票
            - 只有分配到对应 slot 中的 validator 需要投 LMD GHOST 的投票
        - 用于 Checkpoint 的 Casper FFG 投票
            - 所有的 Validator 都需要投这个票
            - 指定 source Checkpoint 和 target Checkpoint
            - 同一个委员会中的验证者作出相同的 LMD-GHOST 和 FFG 投票时，他们的签名可以合并
    - 如果要让一个 Checkpoint 转成 justified，就需要获得超过 2/3 的验证者投票，当前的这个 Checkpoint 转成 justified后，那么前一个 Checkpoint 就会变成 Finality
        - 一半来说，区块会在 epoch 的中间变成 Finality，这样也就意味着交易最终性达成需要2.5 个 epoch，大约 16分钟
    - Staking Rewards and Penalties
        - 处罚场景
            - penalties：节点离线会被罚钱，保持 42.5% 的时间在线收益会为正
            - inactivity leak：网络出现重大问题，节点不投票时会被罚，出现的概率很小
            - slashing：作恶时被罚
                - 重复提议区块
                - LMD GHOST 双重投票
                - FFG 环绕投票
                - FFG 双重投票 
        - 奖励场景
            - 持续投票和证明会获得奖励
            - 提议区块会获得奖励
            - 举报可 slashing 的行为也会获得奖励
    - Validator 生命周期如下
        - 存款
        - 进入排队队列
        - 激活 validator，就可以进行投票和提议区块
        - 被 slashed 退出，需要等待 36 天左右才能提款
        - 正常退出，27 小时左右就可以提款

### 2025.02.14
- 分叉选择机制：LMD GHOST + Casper FFG
    - Casper FFG 确定检查点，确保已经 Finality 的检查点永远不会撤销
    - LMD GHOST 会确定当前最新的区块应该基于哪个分支去构建，基于哪个分支的累加投票数量去决定
    - 所有正常运行的节点都会根据同一条链追溯到 Genesis 区块
    - 由于网络延迟等问题，节点可能会对最新的几个区块进行重组，几回到之前的某个区块，重新开始同步区块，而废弃已经构建了的几个区块
    - 在共识系统了，有两个概念很重要：Safety 和 Liveness
        - Safety：它保证一致性，意味着所有诚实节点应该始终就区块链的状态达成一致
        - Liveness：确保区块链可以持续产生新的区块
        - Safety 和 Liveness 对应 CAP 中的一致性和可用性，所以当区块链网络出现问题时，一致性就很难得到保证了，这样就保证了可用性和分区容忍性，但这样做的结果就是让链分叉
        - LMD GHOST 保证 Liveness，Casper FFG 通过定期确定 Checkpoint 来保证 Safety，保护区块链不被逆转
- 控制流程：
    - 但共识客户端不是 Block Proposer 时
        - 通过 Gossip 协议接收一个区块
        - 验证区块的有效性
        - 将区块中的交易发送到执行层
        - 执行层执行交易并验证区块状态
        - 执行层将验证数据发回共识层
        - 共识层将区块添加到区块链并对其进行证明，并通过网络广播该证明
    - 但共识客户端作为 Block Proposer
        - 收到成为下一个区块生产者的通知
        - 调用客户端中创建区块的创建方法
        - 执行层访问交易内存池
        - 执行层将交易打包层区块，并执行交易，生成区块 hash
        - 共识客户端就交易和区块 hash 驾到信标链区块
        - 共识客户端通过 gossip 协议广播这个区块
        - 其他客户端验证这个区块并为它提供投票证明
        - 一旦得到足够多的 Validator 的证明，改区块就会被添加到链的头部，得到证明和完成最终性（Finality）
- 网络层
    - libp2p 作为点对点协议
    - discv5 作为对等发现
    - libp2p-noise 用作加密
    - SSZ 作为序列化协议
    - Snappy 作为压缩协议

### 2025.02.15
- 以太坊路线图
    - 以太坊是一个无限游戏
    - 以太坊核心协议完全开放、免费，任何人都可以参与，只要有想法和能力
    - 路线图
        - The Merge：完成协议的升级，从 Pow 转成 PoS，SSF 等
        - The Surge：扩展以太坊，围绕 rollup 的升级，比如 EIP-4844 、peerDAS 等升级
        - The Scourge：抗审查、MEV 等问题的解决
        - The Verge：零知识证明的技术路径实施、让区块链的验证的更加轻量级，实现无状态化
        - The Purge：清理技术债务和通过清除历史数据降低加入网络的成本
        - The Splurge ：其他遗留问题的修复，比如账户、EVM、EIP-1559 等等
- 以太坊扩容
    - 在不可能三角的限制下，以太坊无法在保证安全性和去中心化特性的前提下实现很高的扩展性，所以需要寻找其他的扩容方案。
        - 以太坊当前的做法是通过模块化来实现扩展性
        - 以太坊网络本身将实现安全性和去中心化程度，扩展性留给 layer2 去实现，layer2  可以共享以太坊的安全性和高度去中心化
        - layer2 的相关解决方案有 State Channel、Plasma 和 Rollup，其中 Rollup 是当前最受欢迎的方案
        - 多个 Rollup 链自身完成交易的执行，而将交易执行的结果上传到 Rollup 链上
        - Rollup 的具体实现也有很多种，总体可以分成：
            - ZK Rollups：通过零知识证明来实现，交易的确认速度更快
            - Optimistic Rollups：通过 Fraud Proof 来保证安全性，交易确认的速度更慢
- MEV（Maximal Extractable Value，之前的术语是  Miner Extractable Value），是指通过对交易进行策略性地排序、包含和排除，从区块中提取出超出标准区块奖励和 gas 费用
    - 特别是在 Defi 应用中，通过对区块中的交易进行排序，可以通过抢先交易、三明治交易或者反向交易等策略实现套利机会
    - 这样会导致一些负面后果，比如大型矿池获得的不公平的优势、交易审查或者 Defi 用户的滑点增加
    - 在以太坊网络转成 PoS 之后， PBS 可以缓解 MEV 带来的问题，PBS 会让 MEV 在两个角色之间重新分配，从而可能改变每个角色相关的激励
    - 当前 PBS 典型的实现来自于 Flashbots 实现的 mev-boost

### 2025.02.16
- PBS（Proposer Builder Separation）
    - 在以太坊当前的系统中，验证者既创建区块，又广播区块。PBS 将这写任务分配给多个验证者
    - Block Builder负责创建区块、并且在每个 slot 中将区块提供给 Block Proposer，Block Proposer 选择一个区块，并向 Block Builder 支付费用。
    - PBS 对于以太坊实现去中心化非常重要，因为它可以最大限度降低成为验证者说需要的计算开销，降低了成为验证者的门槛，并激励了更多样话的参与者群体。
    - PBS 也是以太坊协议模块化实现的一部分
    - Block Builder 收集、验证并将交易组装成区块
    - Block Proposer 接受 Block Builder 提供的区块，并通过添加必要的元数据（比如区块头）来创建完整的区块，并验证区块的有效性
    - PBS 带来的好处：
        - 增加验证者的奖励
        - 提高网络的效率：让专门的区块构建者去完成区块构建，从而实现更搞笑的区块传播和处理
        - 降低中心化程度：通过角色分离，PBS 可以潜在减少目前 staking 供应商的影响力
    - 当前的 PBS 实现是在协议之外实现（side-car）的，比如 mev-boost在这种实现中需要依赖一个 relay 的组件，这个组件通常来说是中心化的，这些提升了以太坊的中心化风险，并且让以太坊更容易收到审查而且 PBS 让区块构建的过程变长，那么可以被攻击的地方就变得更多了，PBS 可能会导致区块丢失，即使使用 PBS，以太坊客户端也需要保留传统的区块构建流程，一旦外部流程出现问题，那么就需要切换到从传统的区块构建流程
    - 解决这些问题的办法
        - ePBS（Enshrined Proposer-Builder Separation）
            - 降低中心化风险，减少对第三方的依赖
            - 提升安全性和稳定性
            - PTC（Payload-Timeliness Committee）是一种在以太坊协议内实现 ePBS 的方案
            - TBHL（Two-Block HeadLock）：修改了 slot 结构，在单个 slot 时间范围内引入了双区块模式，有效的解决了区块的提议和构建的问题，解决了 ePBS 中的几个关键问题
        - Protocol-Enforced Proposer Commitments (PEPC)
            - 针对 PBS 和 mev-boost 的缺陷而提出的一种解决方案，是 PBS 的扩展，Block Proposer 会定义一组区块构建的 commitment，区块构建者会根据这套 commitment 去构建区块，这套协议需要在以太坊协议内实现
            - 可能会提高协议的复杂性以及提高计算开销
        - EIP-7547（包含列表）
            - 通过指定一种机制，让 Block Proposer 指定一组必须及时包含的交易，从而提高以太坊的看审查能力
    - Ethereum Based Preconfirmations
        - 交易的发起者可以通过提供额外的消费预约交易在未来的某个 slot 纳入区块，这就是预确认。这种实现方式需要依赖包含列表才能实现
    - 轻客户端：无需信任（比如某个中心化的 RPC 供应商）就可以访问网络，而不需要运行完整节点，当前存在的各类轻客户端如下：
        - Statless clients
        - LES ptorocol
        - Portal network

### 2025.2.17
- 以太坊建立在密码学之上
    - 以太坊使用的椭圆曲线算法和签名算法
        - ECC（椭圆曲线加密，实际使用的是 secp256k1 曲线）：以太坊的公私钥依赖这个加密算法生成
        - ECDSA（椭圆曲线数字签名算法）：基于 secp256k1 曲线，以太坊中交易的签名和验签
    - Boneh-Lynn-Shacham（BLS）签名算法
        - 验证者签名所使用的算法，用于给区块和证明签名
        - BLS 的签名可以聚合，可以实现数十万 validator 的大规模验证
        - 目前主要在共识层使用，执行层依然使用 ECDSA
    - Keccak256 是一种在以太坊中广泛使用的哈希函数，这个算法本质上就是 SHA3-256，由于 SHA3-256 定义的时间比较晚，所有依然沿用了 Keccak256 这个名称
    - KZG Polynomial Commitment Scheme（KZG 多项式承诺）
        - 已经成为了以太坊中一项关键技术，已经在以太坊中大量使用了 KZG 多项式承诺，是后续很多零知识相关应用的基础，可以在不泄漏实际信息的情况实现高效、安全的数据验证。比如以太坊中
            - Proto-Dansharding（EIP-4844），使用 KZG 多项式承诺来处理 blob 数据
            - Data Availability Sampling，允许验证者无需下载所有的数据就可以确认 blob 数据的正确性和可用性
    - Post-Quantum Cryptography（后量子密码学）
        - 量子计算对以太坊最直接的威胁是可以逆转 ECDSA，从而暴露出私钥，这会让所有的外部账户 EOA 都面临量子攻击，而且这些攻击可能会很隐蔽，如果钱包被盗，大家可能会认为是私钥被盗，而不是私钥被破解
        - 当前各类的抗量子密码学正在发展当中，也在规划对应的硬分叉方案来应对量子攻击

### 2025.02.18
- Ethereum Staking 的四种方式：https://ethereum.org/en/staking/#what-is-staking
    - Home Staking（Solo Staking）：最理想的 Staking 方式，但是门槛最高，难度最大，需要 32 ETH 的入门资金，还需要准备硬件
        - 风险点：
            - 私钥管理
            - 节点维护，down 机后怎么恢复
            - 在线时间管理，节点不能长时间下线
            - Slashing 风险，节点如果作出错误的行为，可能会被 slasking 大量资金
    - Staking as a service：借用别人的基础设施，自己控制私钥
    - Pooled Staking：最流行的 staking 方式，直接将钱转入一个 Pool，操作和资金的门槛低，还能保留资金的流动性
    - CEX Staking：完全失去资金的掌控权，把钱交给 CEX 打理
- 以上四种方式在参与到 Ethereum Staking 时，都需要满足以下的必要条件
    - 运行全节点（执行层 + 共识层）
    - 运行 Validator 并加载私钥
    - 完成存款，并且存款交易被共识层处理
- Staking 流程
    - 运行全节点，包括执行层和共识层客户端
    - 生成共识层账户（公私钥对），生成私钥之后，需要签署一个存款交易，其中会标记存款的金额和账户的公钥，并指定提款地址
        - 常见的用于生成共识层私钥的工具
            - staking-deposit-cli
            - wagyu-key-gen
    - Staker 向执行层的存款合约发送以太坊交易来进行存款（当前需要存款 32 ETH，Pertca 升级之后可以提升到 2048 个 ETH）
    - 存款完成之后，共识层会收到存款凭据，然后创建一个 Validator 账户，并存入存款的金额，账户由上面生成的公私钥控制
    - 运行 Validator 客户端，保持节点在线，那么用户的余额就会增加，如果作恶或者掉线，那么用户的余额就会减少
    - 如果 Staker 想退出，那么就使用 Validator 客户端签署并广播退出的消息，等待 Vaidator 退出之后，就会进入到允许提款的状态
    - Staker 可以提取自己的全部资金，结束 staking

### 2025.02.19
- Staking 的存款和取款
    - 取款和存款各有两种类型
        - 首次存款：创建 Validator
        - 充值存款：向已经存在的 Validator 账户存入资金
        - 部分提款：将超出 32 ETH 的部分转移到执行层
        - 完全提款：将验证者的全部余额转移到执行层
    - 存款
        - 存款合约地址：https://etherscan.io/address/0x00000000219ab540356cbb839cbe05303d7705fa
            - 存款合约接收四个参数：
                - pubkey：validator 的公钥
                - 提款凭证：以太坊执行层的地址，用来接收后续的提款
                - 签名：validator 私钥对 validator 公钥、提款凭证和存款金额的签名，用来证明私钥的所有权
                - 存款数据 root：是上面数据生成的 SSZ Merkleization，可以作为一种校验和
                - 如果对上面数据校验失败，那么就会导致存款交易失败
                - 在存款交易中，还有一个很大风险点，那就是存款合约不会对签名进行校验，在存款的时候，如果传入的签名是错误的，那么存款交易也会成功，但共识层会校验这个签名，会导致共识层无法计算这笔存款，而且存入的 ETH 也将永久丢失
        - 如果是首次存款，需要生成私钥，这块通常使用上面提到的 CLI 工具来完成，在生成私钥的时候可以先让电脑断网
        - 通常使用 Ethereum Launchpad 来完成存款操作
        - 以太坊质押的存款合约账户余额只会增加而不会减少，可以理解为，当 Staker 向存款合约中转入 32 ETH 时，这些 ETH 就已经销毁了
        - 如果 Validator 由于其他的原因导致有效余额低于 32 ETH，那就需要通过充值存款使有效余额增加到 32 ETH，每次存款最低一个 eth
    - 提款
        - 提款功能是在上海升级（Capella）之后才真实启用，在上海升级（Capella）之前，都只能存款而不同提取
        - 提款功能是自动进行的，不需要 staker 作任何操作，由共识层来完成
        - Validator 需要设置提款凭证，也就是执行层的以太坊地址，如果之前没有绑定，那么就需要把提款凭证从 BLS 提款凭证（0x00）升级到 ETH1 提款凭证（0x01）
            - 如果 Validator 已经退出，处在可提现状态，而且余额不为 0， 那么就会发起全额提款
            - 如果 Validator 的有效余额为 32 ETH，而实际余额高于 32 ETH，那么就会发起部分提款
            - 如果上面两个条件都满足，就会按照全额提款处理
            - 每个共识层区块中可以处理的提款次数是由限制的，当前是 16 次
            - 当前退款情况见：https://beaconcha.in/validators/withdrawals
        - 在进行全额提款之前，需要先退出 Validator
            - 以太坊中 Validator 的激活和退出都是受限制的，每个 epoch 中处理的数量有限，激活依靠 EIP-7514 这个 规范进行，当前每个 epoch 中可以激活的最大数量是 8
            - Validator 退出也是基于同样的机制，但是最大值有所不同，当前每个 epoch 可以退出的 validator 最大数量是 16

### 2025.02.20
- 共识层处理存款
    - 在执行层完成存款之后，这些存款信息需要传递到共识层，共识层需要根据这些信息来完成 Validator 的的创建和激活
    - 存款信息丛执行层转移到共识层的方式有两种：
        - Voting process：Block proposer 通过执行层的 RPC API 来获取存款信息，并构造 Eth1data， block_hash 是执行层的特定区块，deposit_root 和 deposit_count 通过调用该区块存款合约的 get_deposit_root() 的方式来设置，维护这个状态来证明这些存款的存在。Block Proposer 会对存款合约近期的状态进行投票，当这些投票是没有激励的。
           -  但当前这种将存款导入共识层的方式需要有很长时间的延迟。共识层在 2048 个 slot 之后才会处理该质押， Validator 通过投票就上面的 Eth1data 达成一致，Block proposer 才将当前质押数据包含在共识层区块中生效
           - 这种机制是从原来 PoW 机制下遗留下来的机制，因为 PoW 中会出现最新区块重组的情况，如果信标链中包含了后来被撤销的存款，就会出现存款的双重支付
           - 但是在 The Merge 升级之后，这种延迟就有点多余，因为现在执行层和共识层的状态总是一致的，所以在即将进行的 Pectra 升级中，通过 EIP-6110 升级，将 Eth1data 直接放到区块当中，直接在协议内对存款状态达成共识，这样存款状态在 2 个 epoch （大概 13 分钟）之后就能达成共识，完成状态确认，大大缩小了存款状态被确认的时间
        - Validator 导入存款证明：Validator 可以通过执行层客户端手动导入存款数据，维护本地的存款数据，这种方式虽然避免了投票延迟。但是存在数据同步不一致的情况
    - 存款信息验证完成之后，如果是首次存款，就可以激活 Validator，参与网络共识，如果是充值存款，达到 32 ETH 有效余额之后，就能最大化质押收益

<img width="288" alt="eth1data" src="https://github.com/user-attachments/assets/f4afc0af-76ba-436f-9dcf-f26bd4753087" />


### 2025.02.21
- Solidity 编写的智能合约会被编译成字节码，字节码会被 EVM 执行，其中字节码中有很多被预先定义的操作码，由这些操作码串联整个字节码的执行
- 一个操作码的长度为 1 个字节，最多可以定义 256 种操作码，当前大约定义了 140 个操作码，后续还有很大的扩展空间
- 在 EVM 中调用函数需要函数选择器加上具体的参数，总长为 36 字节，函数选择器占 4个字节，参数占 32 个字节，这也有另一个让我们熟知的名字 calldata
    - 函数签名是指函数名和参数列表组成，比如 store(uint256)，不包括返回值
    - 函数选择器是 Keccak256 哈希函数计算函数签名的哈希值的前 4 个字节，在合约调用时，通过这个 4 个字节来确定调用哪个函数，这里的函数选择器是有可能会重复的，在合约升级中需要注意这个问题
        - 在这里可以查到当前以太坊的函数签名库（https://www.4byte.directory/signatures/）
    - calldata 字节码可以由 abi.encodeWithSignature("stroe(uint256)", 10) 计算得到
    - 这个调用 abi.encodeWithSelector(bytes4(keccak256("store(uint256)"),  10) 等价于上面的调用，都可以用来生成 calldata
- EVM 是栈结构，calldata 会被拆分成对应的操作码入栈执行
    - 假如现在合约收到上面 store 函数的调用 calldata，这 36 字节的数据代表了想要调用的目标函数和对应的参数
    - 首先 calldata 的的函数选择器会先被加载
    - 在进入到合约之后，可以理解为合约中内置了一系列的 if 判断，依次去比对函数选择器对应合约中的哪个函数
    - 找到对应的函数之后，就找到函数对应的程序计数器，这个代表合约中函数的字节码位置
    - 然后通过 JUMP 操作码跳转到对应的函数开始执行

### 2025.02.22
- 合约内存是一个简单的字节数组，其中数据存储可以使用 32字节或者1 字节的数据块存储数据，但是每次只能固定读取 32 字节的数据块
    - MSTORE (x, y)：从内存位置 “x” 开始存储一个 32 字节（256 位）的 “y” 值
    - MLOAD (x)：从内存位置 “x” 开始将 32 字节（256 位）加载到调用栈上
    - MSTORE8 (x, y)：在内存位置 “x” 存储一个 1 字节（8 位）的值 “y”（32 字节栈值的最低有效字节）
    - 当我们正在写入一个以前没有写入过的内存区域，会产生内存扩展开销
        - 假设在位置 32  第一次写入一个字节，就会开始触发内存扩展，内存就会增加 32 字节，增加到 64 字节，内存中所有位置都被初始化为 0
        - 前 724 个字节，内存扩展是线性增长，之后就会开始二次方增长
    - 内存是一个字节数组，内存是连续的，这意味着可以从任何内存位置开始读取和写入数据，不限于 32 的倍数
    - 空闲内存指针指向空闲内存开始位置的指针。它确保只能合约可以跟踪到哪些内存位置已经写入，哪些未写入，防止sheet覆盖已经分配给另一个变量的某些内存
        - 空闲内存指针的位置 + 数据的字节大小 = 新空闲内存指针的位置
    - 在合约开始加载时，会首先执行 PUSH1 0x80，PUSH1 40，这两个操作就是用来初始化空闲内存指针，表明空闲内存指针位于内存中字节 0x40 的位置，值为 0x80，这个表示保留了4 个 32 字节位置，真正的数据存储从这 4 个 32字节之后开始，四个
        - 0x00 - 0x3f (64 bytes)：暂存空间，可用于语句之间，即内联汇编和哈希散列方法
        - 0x40 - 0x5f (32 bytes)：空闲内存指针，当前分配的内存大小，空闲内存的起始位置，初始化为 0x80
        - 0x60 - 0x7f (32 bytes)：zero slot，用作动态内存数组的初始值，永远不应写入
     - 合约内存的初始化发生在每次合约调用开始时，当合约被调用时，EVM 会为该调用上下文创建一个新的内存实例，并在调用开始时将其初始化为空，调用结束之后内存内容就会被销毁。

### 2025.02.23
- 合约存储是一个简单的键值映射，它将一个 32 字节的 key 映射到一个 32 字节的 value，最多可以有 2^256  -1 个 key
    - 存储中所有的值都被初始化0，但是 0 没有被明确存储，存储位置从 slot 0 开始，每个插槽存储的数据都是 32 字节
    - 因为2 ^256 时大约已知的、可观测的宇宙中的原子数量，没有一台计算机可以容纳这么多的数据
    - 合约存储用来存储合约中变量
        - 定长变量
        - 不定长变量
    - 对于定长变量来说，会根据变量在合约中的声明顺序来存储
        - 假设现在有3个 uint256 的变量，那么 slot 0 将存储 value1， slot1 将存储 value1， slot2 将存储 value2
        - 如果对于长度不是 256（32 字节）的变量，比如是 2 个 uint32 和一个 uint64 以及一个 uint128 的变量，那么存储方式就有所不同
    - slot packing
        - 会将多个长度不多于 32 字节的变量存储到一个 slot 中，比如上面的四个变量长度刚好为 256 位（32 字节），就刚好可以存储到一个 slot 中
        - uint8 是最小的 solidity 类型，因此 slot packing 时不能小于 1 字节
    - 存储操作码
        - SSTORE：从调用栈中接收一个 32 字节的 key 和一个 32 字节的 value，并将该 32 字节的value 存储在该 32 字节的 key 的位置
        - SLOAD：它从调用栈中接收一个 32 字节的 key，并将存储在该32 字节的 key 的 value 加载到调用栈
        - 那么这两个操作码如何从 slot 提取对应 slot packing 的变量的呢？
            - SSTORE
                - 先确定变量的偏移量，比如 value2 的偏移量是 0x04，从第四个字节开始
                - 然后以一个字节的偏移量 0x0100 为基数，通过 EXP 产生对应的二进制值 e1
                - 然后使用 e1 乘以 value2，就可以得到 value2 在 32 字节插槽的位置的值 v1
                - 然后使用 e1 乘以 0xffffffff 得到 value2 所在 4个字节的位掩码 b1
                - 然后对这个掩码进行按位非运算，就得到了除了 value2 所在4 个字节之外所有字节的位掩码 b2
                - 然后将 slot 0 中的数据和 b2 使用 AND 操作，就可以返回除了 value2 四个字节之外的所有数据 v2
                - 最后将 v1 和 v2 进行按位或操作，就得到了最终要存储的值
            - SLOAD
                - 先确定变量的偏移量，比如 value2 的偏移量是 0x04
                - 然后以一个字节的偏移量 0x0100 为基数，通过 EXP 产生对应的二进制值 e1
                - 然后将 slot 0 上的数据加载出来
                - 然后使用 DIV 将 slot 0 的除以 e1，这实际是将 value1 所使用的底部 4 字节修剪掉，得到 v1
                - 最后将 v1 与前 四个字节的位掩码做按位 and 操作，就得到了 value2

### 2025.02.24
- 以太坊的每个区块中有三棵树，这三棵树的结构都是 MPT（Merkle Patricia Trie）：
    - State Root：执行万区块中所有交易的以太坊中，所有账户状态的 merkle 树根 Keccak 哈希值
    - Transaction Root：交易生成的 Merkle 树根 Keccak 哈希值
    - Receipt Root：交易回执生成的 Merkle 树根 Keccak 哈希值
    - 在 Geth 的实现中， State 的存储会和三个结构有关系
        - StateAccount 是以太坊账户的共识表示
            - 代表一个以太坊账户，其中的 root 表示存储根
        - StateObject 是交易执行中正在被修改的以太坊账户状态
            - stateObject 中有一个 StateAccount 类型，是代码实现里的中间态，映射到一个以太坊账户
        - StateDB：StateDB 结构是用来存储 MPT 内的错有数据，用于检索合约和以太坊账户的查询接口
            - StateDB 中有一个 stateObjects 的字段，是地址到 stateObject 的映射集
    - 当一个新的地址产生状态时，就需要创建一个新的 StateAccount
        - StateDB 有一个 createObject 函数，可以创建一个新的 stateObject
        - createObject 调用 newObject，传入 stateDB、地址和一个空的 StateAccount，返回一个stateObject
        - stateObject 被成功创建并带着已经初始化完成的 StateAccount 返回
        - 在当前区块中被修改的状态会先存储到 dirtyStorage 中，然后被复制到 pendingStroage 中，在 MPT 被更新之后，StateAccount 的 root 也会被更新
        - StateDB 中的 GetState 函数会获得与该合约地址相关的 stateObject，如果 dirtyStorage 存在，那么就直接使用 dirtyStorage 中的值，如果不存在就返回 pending Storage 中值，最后再检查 oroginStorage 中值

### 2025.02.25
- EVM 在执行智能合约时，会为其创建一个上下文：
    - The Code：合约的字节码不可改变， 存储在链上，并使用合约地址进行引用。
    - The Stack：每个 EVM 合约执行时都会初始化一个空的栈，栈是一个 32 字节的元素列表，用于暂时存储智能合约指令的输入和输出，每个调用上下文创建一个栈，但调用上下文结束时，这个栈就会被销毁，栈的最大限制时 1024
    - The Memory：为每个EVM 合约执行而初始化的一个空的内存，EVM 内存时临时的，在调用上下文结束的时候被销毁。
    - The Storage：智能合约的持久化存储，格局合约地址和 slot  寻址，storage 时一个 32 字节的 key 和 32 字节的 value 的应用，最大长度是 2^256 -1，每个合约都有自己的存储，不能读取或者修改其他合约的存储。
    - The Calldata：交易传入的数据，calldata 区域是作为智能合约交易的一部分发送给交易的数据。如果是创建合约，calldata 就是新合约的构造器的代码。当一个合约执行 xCall 时，也会创建一个 拿不交易，然后在新的上下文中产生一个 calldata 区域，calldata 是不可变的。
    - The Return Data：合约调用返回的数据。The Return Data 是智能合约在调用后可以返回一个值的方式。
    - 合约中跨调用函数的方式：
        - DELEGATECALL：实际的逻辑是从另一个合约从复制粘贴一个函数到当前的合约中执行，所有状态的变更都产生在当前合约，这要求这两个合约的内存布局是一样的，否则会产读写错误的情况
            - gas：执行所需要消耗的 gas 费
            - address ：需要执行的账户
            - argsOffset：输入内存中数据(calldata) 的字节偏移量
            - argsSize：需要复制数据(calldata) 的字节大小
            - retOffset：输出内存中数据(return data) 的字节偏移量
            - retSize：需要复制数据(return data) 的字节大小
        - CALL：直接跨合约调用，状态的修改都发生在被调用的合约
        - CALL 和 DELEGATECALL 有完全相同的输入变量，CALL 会多一个 value 的调用，DELEGATECALL 不需要 value 值输入

### 2025.02.26
- 在以太坊中，可以通过事件日志来存储数据，这个也相对更便宜一些，事件日志可以用来触发合约中特定事件，节点不需要永久保留日志，可以通过删除日志来节省空间，合约也无法访问日志存储
    - 在以太坊区块中，除了有 State Root，还有 Transaction Root 和 Receipt Root，其中 TransactionRoot 对应的 Transaction Trie 中记录这这个区块中所有的交易
    - 但是在 Transaction Trie 中并不会记录任何交易结果的信息，所有的交易结果将会记录到 Receipt Trie 中，包括交易所消耗的 gas、Event logs、logs 对应的布隆过滤器等等
    - Event logs 通过合约中的 event 来生成，通过 emit 来触发，早期的合约会直接通过 event 来触发
    - 在 Event 中定义中，如果一个参数被标记为 indexed，然后这个字段会被放入 Log 的结构体的 Tpoics 字段中，以 Transfer(address,address,uint256) 为例，在 Tpoics 中会保存三个值，第一个是函数签名的哈希值，第二个和第三个是分别对应第一个 address 和第二个 address，tpoics 中最多有四个值，也就是最多在 event 中 index 三个参数
    - Solidity 中可以声明匿名 event，这样 tpoics 中就不用存储函数签名的哈希值，也就能 index 4 个参数了。
    - 日志中 Data 字段用来存储其他的非索引字段
    - 这些被索引的字段能够被快速查找主要是因为 Bloom Filter：https://llimllib.github.io/bloomfilter-tutorial/
        - 它可以判断一个元素绝对不在集合内或者可能在集合内

### 2025.02.27
- Verkle Tree = Vector commitment + Merkle Tree
- Verkle Tree 的目标：让以太坊节点不需要存储大量的状态数据，但同时又不丢失验证区块的能力
- 验证区块 = 重新执行区块中的所有交易 + 将状态变化持久化道状态树 + 重新计算状态树的树根
    - 在当前的以太坊客户端中，验证区块需要本地有整个状态数据库
    - Witness 可以做到要验证一个区块所有必要的数据都包含在这个区块本身
- Verkle Tree 是以太坊在无状态化这条路径上很关键的一步
    - 无状态客户端不需要为了验证区块而存储整个状态数据库
    - 无状态客户端使用状态数据的 witness（见证）来验证区块
    - 一个 Witness 是执行一组交易所需要依赖的状态数据的集合以及这组状态数据确实属于整个状态数据的加密证明
    - Witness 数据需要非常小，在一个 slot 时间内能广播到所有的 validator，当前的状态数据结构太大了，不满足这个条件，Verkle Tree 可以用来解决这个问题
    - Verkle Tree 相比于 MPT 结构的改进
        - 缩短叶子节点到根节点之间的距离， Verkle Tree 更扁平
        - 消除提供兄弟节点来验证根哈希的需要
        - 使用 polynimial commitment （Pedersen）而不是 hash-style vector commitment
        - Ploynimial commitment 具有固定大小，不会因为要证明的叶子节点的增加而增加
    - Verkle Tree 的 key 采用分层设计，前 31 字节为词干（Stem）最后一字节为后缀（Suffix），这种设计让相邻存储位置共享同一个词干，仅后缀不同，从而验证的时候只需要处理局部而不是全树

### 2025.02.28
- 为什么以太坊需要无状态
    - 带状态的应用程序一般都比较复杂
    - 状态总是会随着时间增长
    - 会给以太坊的核心功能带来挑战
        - 在验证区块之前需要先下载所有的状态数据（需要 TiB 级别的空间）
        - 处理状态对 ZK 不友好
    - 为以太坊构建一个无状态的世界
        - 理想情况下，一个新的节点加入网络时，不需要同步所有的状态，执行层客户端没有存储要求，并且降低对硬件的需求，这样也就能提高区块的 gas limit
        - 构建一个对 ZK 友好的 Layer1
            - 移除复杂的数据结构（MPT）
            - 移除对 ZK 不友好的 hash 算法（Keccak256）
        - 引入 witness 的概念
            - 其中包含了验证一个区块所需要的全部内容
            - 另外包含了一个很小的加密证明来证明 witness 是有效的
        - 但是要做的事情很多：
            - 需要引入新的加密技术栈
                - 当前 MPT 使用的是 Keccak256 哈希函数
                - 在 Verkle Tree 中则要引入很多新的加密技术
                    - EC Bandersnatch：专为零知识证明和高效密码学协议设计的椭圆曲线
                    - BLS12-381：聚合签名算法
                    - Vector Commitment and Vector Opening：从 Merkle Proof 转向向量承诺
            - 需要改变状态树的数据结构，从 MPT 转成 Verkle Tree
                - Verkle 树永远不会删除值
                - Verkle 的节点有两种类型：
                    - 扩展节点：表示相同词干但不同后缀的 256 个值
                        - 扩展节点的 commitment 计算 C =  Commit(1, stem, C1, C2), C1 和 C2 是另外两个 Commitment，单个 Commitment 存不了 256 个的值，C1 存储 0 到 127 的值，C2 存储 128 到 255 的值
                        - 扩展节点与 C1 和 C2 被称之为 extension-and suffix tree, 简称为 EaS
                        - C1 和 C2 是 分别对存储 Value 叶子节点 Commitment 的计算，其中，每个叶子节点都保留了一个用来标记是否被访问的标记，用来区分叶子节点没有写入数据（默认都初始化为0）还是写入的数据是 0
                    - 内部节点：最多有 256 个子节点，可以是其他内部节点或者扩展节点
                        - 内部节点 commitment 的计算 C = Commit(C0, C1, ....., C255)
                        - 如果产生路径冲突，内部节点可能分裂成扩展节点和新内部节点
            - 需要改变 gas 的计算方式
            - 需要将数据从 MPT 迁移到 Verkle Tree 

### 2025.03.01
 - 虽然以太坊想让协议保持简单，但是由于以太坊承载的东西越来越多，以太坊已经是一个很复杂的系统了，后续可能很少有人能真正完全理解以太坊
    - 在软件越来越复杂时，对软件进行模块化是必备的选项了，当前以太坊已经拆分成了共识层和执行层，随着以太坊无状态化的推进，以后可能会有更多类型的客户端出现
    - 在学习以太坊时，由于每一个细节都可能包含大量的信息，很容易掉进一个细节然后出不来，所以首先要对以太坊有一个整体的认识
        - 以太坊执行层是一个状态机，状态机的状态变化只能通过交易来实现，其中 EVM 就是这个状态机的 STF（状态转换函数）
        - 共识层是让以太坊网络达成共识的方式，共识层决定让哪个 validator 来出块，但是具体出块的的行为是由执行层来做
        - Engine API 是执行层和共识层沟通的方式，以太坊整体逻辑就是这样
    - 但以太坊完全运行在公开的网络中，会随时面临各种攻击，包括恶意交易和 validator 本身作恶，所以各种安全的措施都需要在客户端软件中实现：
        - 执行层 Gas：停机问题无解，所以让 gas 来衡量计算量，gas 耗尽则攻击停止
        - 共识层分叉算法和 Checkpoint 机制：让链上区块的增长总是沿着大多数 validator 支持的方向
    - 整体上来看，以太坊解决的问题很简单，但是在这个过程中，需要各种额外的机制的来保障上面的这些主要过程能顺利执行，有了这样整体的认识之后，如果对其中的某个点感兴趣，就可以深入研究，比如：
        - EVM + solidity + 智能合约安全
        - 节点之间的通信机制
        - 共识层共识机制，如何选择出块的 validator、如何解决拜占庭将军问题
        - 以太坊状态增长问题
        - 等等

### 2025.03.02
- 推荐一些常见的以太坊学习资料：
    - 以太坊官网：https://ethereum.org/en/
    - Ethereum Protocol Fellowship：https://epf.wiki/#/README
    - 共识层规范：https://github.com/ethereum/consensus-specs
    - 执行层规范：https://github.com/ethereum/execution-specs
    - eth2book：https://eth2book.info/
        - 对以太坊协议系统地讲解，但目前只更新到上海升级，虽然缺了不少内容，但是可以根据目录的提纲进行学习
    - 以太坊关键信息：https://etheralpha.org/
        - 对以太坊很多关键信息，包括客户端多样性等等各类以太坊关键信息披露
    - Vitalik blog：https://vitalik.eth.limo/
    - 以太坊研究论坛：https://ethresear.ch/
    - EIP 和 ERC 讨论的论坛：https://ethereum-magicians.org/
<!-- Content_END -->
