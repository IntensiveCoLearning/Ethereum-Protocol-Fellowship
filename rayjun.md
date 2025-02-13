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


<!-- Content_END -->
