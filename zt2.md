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

# zt2

1. 自我介绍: 一名 WEB3 研究员
2. 你认为你会完成本次残酷学习吗？能
3. TG 联系方式：@hi_ztz

## Notes

<!-- Content_START -->

### 2025.02.06

### Ethereum Protocol 101


#### 以太坊


The World Computer 由三部分组成：


- Ethereum Virtual Machine (EVM): 以太坊核心，本质上是一个图灵完备的状态机，通过在节点的 EVM 执行能力为全球节点提供一个抽象的计算平台。
- Ethereum Blockchain: 提供数据存储读写能力
- Ethereum Network: 由实际的算力与主机组成，涉及各类网络协议

#### 以太坊节点


以太坊节点负责执行真实的交易与区块上链，通常由具备一定算力的主机硬件构成。节点执行两类客户端：


- 共识客户端
- 执行客户端

#### Proof of Stake


以太坊的核心共识，2015 年的工作量证明（PoW）支持到2022 年，22 年后完全转为 PoS，大大提高了以太坊的交易执行速度。

PoS 涉及验证者角色，每个验证者至少需要质押 32 ETH。

PoS 通过经济假设来提高作恶成本，来取代原先的中心化信任机制，利用经济模型奖励与惩罚验证者，保护去中心化的信任关系不被破坏。

#### De-Fi


基于以太坊可执行合约 Dapp 建立的以太坊经济体系，是一种去中心化的金融生态系统。

### 2025.02.07

#### Ethereum Virtual Machine （EVM）


EVM 本质上是一个 VM，通过抽象计算层抹除硬件平台和底层细节差异，所有加入以太坊网络的节点都是一个个的 EVM，每个 EVM 上运行 Solidity 语言，实现图灵完备的计算。

EVM 围绕账本实现了完全的状态机，允许基于全球节点的去中心化账本记账的状态变化，相比之下 BTC 也具备一定的计算能力，只不过由于 BTC 的限制，其支持的计算能力图灵不完备，极其受限。
> 比特币的脚本系统被特意设置为图灵不完备是出于安全性、可预测性和效率性的考虑。


相比之下，Ethereum 的 EVM 被设计为图灵完备计算系统，是与比特币相比最大的不同，比特币更偏向于“价值存储和转账”，以太坊则是一个通用的计算平台，但也因此以太坊上的合约有安全漏洞风险，而比特币则没有。

![image](https://res.craft.do/user/full/ca875b0a-92a3-940e-21e3-a9ace35d9a4b/doc/DCE1FE68-D5B8-46CE-8ADD-E4C88CAA5C60/38B5EDA7-166A-4EFE-966F-D9A30594429D_2/ly9OCgp75qdLTdV4KZyyozs9zVppKb5N2Sh6sQxgTaoz/Image.png)

以太坊的状态经有 Solidity 计算后，表现为所有以太坊账户的变化。

由于区块链和账本的存在，导致了以太坊作为一个计算平台具有以下特点：


- 去中心化：以太坊的计算能力本质上由一个个的记账节点组成，每个记账节点运行单独独立的 EVM，并将记账结果放置于区块链中，依据以太坊共识实现计算结果的固定。
- 计算结果不可篡改性：由共识系统保护的计算结果一经上链，结果就存在在所有以太坊网络节点中，节点遵循的共识系统将保护其无法撤回无法修改。
- 数据所有权性：每个计算结果都体现在作为数据所有者：账户的身上，发生的影响也在账户身上，由程序化的代码保证其结果的所有权。

### 2025.02.08

#### 以太坊的设计哲学

以太坊设计遵循以下设计哲学：
1. 简洁性：确保以太坊的设计应尽可能简洁，宁愿付出额外的计算成本和代价也要保持现有架构尽可能简单，以确保普通的程序员也可以参与以太坊开发，从而防止以太坊被技术精英和群体把控，巩固以太坊作为全民开放协议的愿景。
2. 通用性：以太坊将扩展能力从本身抽离出来，形成通用计算平台，底层和底座不再为某个具体功能提供复杂的实现，只保证底层能力对上的通用性，至于具体的功能实现交给上层业务系统（EVM）和智能合约完成。
3. 模块化：以太坊协议的各个组成部分被尽可能设计为可分离的模块。在开发过程中，保证对模块内部的变动不会影响模块之间的调用关系。
4. 不歧视：以太坊不歧视任何合约结算，只要有足够的 gas 费，以太坊可以执行任何计算。
5. 敏捷性：如果有某个破坏性变动或大变更，会对以太坊带来巨大好处，开发团队也愿意为此付出代价。

#### 默克尔树

默克尔树是一种用于组织和加密海量数据集的数据结构。

作用：用于在不传递整体数据集的基础上，验证某个数据是否存在于数据集中。

使用场景：用于验证某笔交易 hash 存在

![image](https://github.com/user-attachments/assets/0c3d5ea3-d1ea-40bd-b8a7-63f17fe84513)

原理：
默克尔树通过不停反复对子数据的hash进行二次合并hash，最终得到一个单独hash，这条hash链就像树一样，由底向上不停被hash函数计算，只要任何一个数据发生改变，就会传导到默克尔树根导致最终的根hash发生变化（普通hash函数也是为了解决这个问题设计的）。
证明某段数据是否存在于数据集中主要依靠默克尔证明：
首先需要准备：
1. 待验证数据的hash
2. 目标数据集的默克尔树根hash
3. 验证路径，即待验证数据位于目标数据集的位置，从而构建一条默克尔树路径（proof路径）

验证过程：
1. 验证者将准备验证数据集和目标大数据集的默克尔树结构与hash
2. 验证者计算待验证数据集的hash，并本地使用目标大数据集的默克尔树hash一同重新构建默克尔树
3. 如果本地重建的默克尔树根hash与实际默克尔树根hash一致，则说明数据集存在于大数据集中

默克尔证明的本质就是链式hash计算，所以需要准备待验证hash和后续的hash链。

![image](https://github.com/user-attachments/assets/e15dec3e-5cc7-42ea-b028-a8da9f09ea60)

### 2025.02.09

#### EOA

以太坊执行层（EL）指的是以太坊协议中负责执行交易和存储世界状态的部分。而以太坊 EOA 全称为 Externally-Owned Accounts，代表了可进行交易交互的被外部私钥管理的以太坊账户。一个 EOA 的私钥是 256 bits 的数字，通常表示方法为十六进制字符串，而更常见的是作为 12 个常见 seed phrase 出现，如：

```
“heart forest bird damp abandon soap bird holiday poverty expire grant keep”
```

而 EOA 的地址则是私钥对应的公钥后 20 字节生成的，如：

```
0x5e16Fa36555B428823d3Ed32aa7CbB07a92F301B
```

一个 EOA 通常包含两部分：
- nonce：表示从账户创建以来产生的交易数
- balance：表示账户当前余额

![image](https://github.com/user-attachments/assets/96ff2d33-9f73-4498-8f09-abdd860f6997)

### 2025.02.10

#### 以太坊账户

以太坊账户分两种：

- 合约账户（CA）：CAs 完全存在于以太坊内部。它们不受加密密钥控制，而是由智能合约代码中的逻辑所控制。
- 外部拥有账户（EOA）：外部账户（EOAs）由以太坊虚拟机（EVM）外部的人（或事物）控制（例如用户）。

在技术层面上，CA 和 EOA 都具有相同的 3 个属性：

- 一个地址
- ETH 余额
- nonce：随机数（用于唯一标识每个账户每笔交易的计数器）

CA 具有两个附加属性：

- 代码
- 存储

### 2025.02.11

#### 执行层（Execution Layer）


##### 执行层的定义


以太坊执行层是最初由黄皮书引入的，实现了以太坊作为全球计算机的状态转换（State Transition Function 或 STF），通俗来说，它具备两个核心角色：


- 决定某个区块是否能够上链
- 决定该区块上链后，整个以太坊全球计算机的状态如何发生变化

为了支持核心角色，它也要负责一些具体的工作如：


- 验证区块链数据并进行本地副本保存
- 实现稳定的客户端通信协议
- 维护交易池
- 满足共识层的要求

##### 执行层具体架构


经过合并升级，以太坊网络中的执行层功能已发生结构性调整。此前，该层级肩负着区块链共识管理、区块序列验证及链重组处理等核心职责。而当前架构下，这些核心功能已全面移交至共识层运作，执行层因此实现了职能精简化转型。在现有体系中，执行层可被抽象理解为专门执行状态转换功能的核心模块。

![image](https://res.craft.do/user/full/ca875b0a-92a3-940e-21e3-a9ace35d9a4b/doc/EFD8C5C2-91E3-4D88-9218-08555760530E/9EB98687-5A5F-4D89-886E-B8984A0377BB_2/DscRQ5xcQAo0c0IyjH3jnNeZ2QMyGiB7En0mywTiQHAz/Image.png)

从这张图中可以看到，执行层通过左下角的协议实现与其他执行层完成通信，在通信建立后接受其他执行层客户端发来的交易与区块，并同步维护本地状态（State）同时将新交易通过引擎 API 向共识层传递，接收共识层处理结果后交给 EVM 虚拟机执行具体交易逻辑，并完成状态转换后同步到本地状态（State）中，交给网络层协议完成状态对其他客户端的同步，最终利用 JSON-RPC 接口向 WEB3 钱包提供服务。


- Engine API：共识层与执行层之间唯一的沟通桥梁。

关键概念：`execution_engine`

###### execution_engine


`execution_engine` 负责执行层与共识层之间的沟通，同时承担了大量的复杂工作，简要描述如下：


1. 共识层获得区块后，对区块进行一系列高层级验证，该类验证比较轻量级，如验证父哈希的准确性、时间戳的准确性等等
2. 共识层简单验证通过后，将具体区块细节传递给执行层，执行层进行精确验证，如区块头精确性验证、交易状态验证等
3. 执行层完成核心验证后，最终交给执行引擎进行交易，并实现状态转换，通知共识层状态转换结果。

（注意，区块中的单个交易执行失败，整个区块都会被打回重来）

### 2025.02.12

#### Bridge

无论是智能合约还是以太坊，其根本是建立在一个个的节点（node）之上，依靠节点上 EVM 虚拟机的计算能力实现上层业务逻辑的构造。

其缺陷在于，无论智能合约逻辑有如何复杂，但它永远只能够在以太坊钩织的数据里漫游而无法接触到以太坊网络以外的数据，因为 EVM 限制其获取以太坊网络以外的数据，如互联网数据。

脱离了外部世界的以太坊合约是不完整的，而“桥”则是一个构建起外部世界与以太坊世界数据流通的通道。

运行了 bridge 的服务，可以通过主动向以太坊链上的合约 push 外部世界的数据，从而完成外部数据上链的工作，这样，以太坊网络中，就存在了外部世界的数据，这通常维护在某个智能合约中。

![image](https://github.com/user-attachments/assets/2075b70e-4bb8-40b8-a0c3-7ee7ae4ba66f)

同样，如果某个服务能够将两个链的数据进行互通，则也可以视作一种桥：Blockchain Bridges

![image](https://github.com/user-attachments/assets/2ed7c94c-3782-4d36-b15b-17a3b0f538d3)

这里就引入了另一个概念，预言机（Oracle）：区块链预言机是位于以太坊与外部世界之间的实体，负责在两者之间传递信息。

预言机一般包括：

- Oracle 智能合约部分：存在于以太坊中的代码，处理请求并协调内部与外部客户端之间的交互。
- Oracle 外部接口（节点）：与以太坊进行通信的计算机和服务器。节点是能够进行极其快速且低成本计算的中心化实体。它们还连接到外部数据源，并可以将这些数据发布到链上。

![image](https://github.com/user-attachments/assets/ea77b6ba-dfc6-4fa8-8d3b-4cc25fcfd002)

预言机解决方案：[Chainlink](https://chain.link/):

<img width="1520" alt="image" src="https://github.com/user-attachments/assets/6f4638af-6577-4535-9105-fe0720d51776" />

<!-- Content_END -->
