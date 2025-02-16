---
timezone: Asia/Shanghai
---

# cooper

1. 自我介绍：大家好，我是 cooper， 区块链技术爱好者，Rust/Go开发工程师。很高兴参加 epf 残酷共学，希望通过这次学习，更详细的了解以太坊底层协议。
2. 你认为你会完成本次残酷学习吗？会的。

## Notes

<!-- Content_START -->

### 2025.02.06
> 周四

笔记内容

### 2025.02.07
> 周五

看了一下 https://epf.wiki/#/ 的目录。我希望在这次共学中重点学习的知识有以下几个，在wiki中没有包含的内容，我会从其他途径中尽量补充。

1）MPT 树的使用。如状态树、交易树。
2）当前以太坊的整体架构。
3）共识层、执行层机制。
4）EVM相关内容。

#### 相关事项
填写了 survey：<https://forms.gle/G5V95qyGV8uMjKGcA>

#### 学习内容总结
1）阅读了 [Prehistory of Ethereum](https://epf.wiki/#/wiki/protocol/prehistory) ，了解了以太坊的诞生背景。

2) 协议架构学习。
当前的协议架构是多年发展的结果。该协议由 2 个主要部分组成 - 执行层和共识层。执行层 （EL） 处理实际交易和用户交互，是全球计算机执行其程序的地方。共识层 （CL） 提供权益证明共识机制 - 一种加密经济安全，确保所有节点都遵循相同的提示并驱动执行层的规范链。

EL和CL的在各自的节点间，都维护着自己的P2P网络。EL和CL通过API进行交互。
![全局架构抽象图](https://epf.wiki/wiki/protocol/img/clients-overview.png)

![基础功能模块图](https://epf.wiki/wiki/protocol/img/protocol-overview.png)

3) 设计理念

- Simplicity
- Universality
- Modularity
- Non-discrimination
- Agility

4) 新的数据结构
文章提到，Merkle-Patricia trie被认为是可以弃用的。新的替代数据结构为：[Verkle tree](https://verkle.info/).

TODO: 值得仔细研究下。

> 以太坊的紧迫问题之一是当前的状态大小。估计约为 1-2TB（在撰写本文时）

5) Recursive Length Prefix (RLP)

RLP在我开发GDWeb3项目时已有详细了解。RLP是用于序列化以太坊交易和状态的编码格式。同时，大量的key-value数据存储时都使用了RLP规范进行数据的序列化。

GDWeb3项目中，集成了libethc的实现。代码参考：https://github.com/qingfengzxr/gdscript-web3/blob/main/modules/web3/ethprotocol/rlp.h

6）Simple serialize (SSZ)

SSZ 是以太坊 2.0 信标链中使用的一种序列化格式。设计为不是自描述的序列化方案，而是依赖于必须事先知道的架构。与 RLP 相比，SSZ 有很多优势，例如对象的高效重新哈希和快速索引，而 RLP 缺乏这些优势，因此复杂性很高。

SSZ 试图解决的主要问题之一是 RLP 不允许 Merkleization，这意味着取消任何简洁的轻量级客户端证明的可能性。因此，没有留下实现无状态的余地——而无状态仍然是当前以太坊研发的关键目标。

7）最终确定性

在以太坊基于权益证明的共识机制中，最终确定性是指保证在未销毁至少 33% 的 ETH 总质押量的情况下，无法更改或从区块链中删除区块。实现这一目标的底层共识协议称为 Casper Friendly Finality Gadget （FFG）。

Gasper 是完整的权益证明协议，是以太坊实现的理想化抽象。它结合了 Casper FFG 和 LMD-GHOST 来驱动 Eth2 的共识机制。

8）DHT

DHT 在以太坊网络中用于查找不同的对等节点，而不是区块。

以太坊网络层中的发现协议使用基于 kademlia 的 DHT discv5 来存储 ENR 记录。ENR 记录包含路由信息（互联网层的），用于在对等体之间建立连接。加入网络的对等节点使用引导节点在 DHT 中中继其node_id的查找查询。在此过程中，他们发现了其他对等体的 ENR 记录，这有助于他们填充路由表。通常，对等体还会随机查找 node_id来枚举网络，即找到所有对等体。

> 又接触到了新的知识点：ENR记录、kademlia based DHT、gossipsub。

以太坊网络中的区块使用 p2p 堆栈的 gossip 协议进行分发。通过底层 DHT 发现 Peer 节点后，Peer 节点使用覆盖网络 （gossipsub） 在整个网络中传播区块。覆盖网络使用路由信息创建自己的路由表，以建立连接和覆盖特定信息（订阅的主题、扇出等）这个覆盖网络确实是一个非结构化网络。

**以太坊的P2P实现协议为devp2p, 与 libp2p 的关系:**

libp2p项目与 devp2p 大约同时启动，旨在成为一组模块，用于通过模块化组件组装对等网络。关于 devp2p 和 libp2p 之间关系的问题经常出现。

很难比较这两个项目，因为它们的范围不同，并且在设计时考虑了不同的目标。devp2p 是一个集成系统定义，希望能够很好地满足以太坊的需求（尽管它也可能适合其他应用程序），而 libp2p 是一个编程库部分的集合，并不服务于任何特定的应用程序。

也就是说，这两个项目在精神上非常相似，并且 devp2p 在成熟过程中正在慢慢采用 libp2p 的部分功能。

**ENR记录(Ethereum Node Record):**

ENR 记录是节点在以太坊网络中进行通信的唯一标识。每个节点都有一个唯一的 ENR 记录，包含节点的网络地址、公钥、节点 ID 等信息。

以太坊节点记录最初是在EIP-778中提出的。



### 2025.02.08
> 周六

#### 学习内容总结

执行层

1) State transition function (状态过度功能 STF)

从 EELS（Ethereum Execution Client Specifications） 角度来看，执行层专注于执行状态转换函数 (STF)。
* 是否可以将块附加到区块链的末端？
* 状态如何转变？

黄皮书中的定义的块状态过渡函数：
![STF](https://epf.wiki/images/el-specs/stf_eels.png)

此外，至关重要的是要理解，不要将其与python规范中定义的State类混淆。系统的状态不是通过状态崩溃函数的应用动态得出的，而不是存储在特定位置。这突出了区块链状态过渡的数学模型与软件规范中的实际实现细节之间的概念分离。

![State](https://epf.wiki/images/el-specs/state.png)

代码文档中的状态过渡功能的指定过程包括以下步骤：

1.检索区块头：获取添加到链条中的最新块的区块头，称为父块。

2.过量Blob Gas验证：从父区块头计算过多的blob gas，并确保其与当前区块头的参数excess_blob_gas匹配。

3.区块头验证：比较并验证当前块的标头与父块的标头。

4.Ommers Field Check：验证当前块中的Ommers字段是否为空。注意：“ Ommers”是替代先前使用的术语“叔叔”的性别中立术语。

5.执行区块：执行块内的交易，该交易产生以下输出：
* Gas Used: 通过执行块中的所有交易而消耗的总气体。
* Trie Roots: 块中包含的所有交易和收据的trie根。
* Logs Bloom: 块内所有交易的日志的布隆过滤器。
* State: 执行所有交易后的状态，如Python执行规格中指定的状态。

6.区块头参数验证：确认从执行块返回的参数存在于区块头中。这包括将状态根与块标头中的state_root字段进行比较。

7.Block Addition：如果所有检查都成功，请将块附加到区块链上。

8.修剪旧块：从区块链中删除早于最近的 255 个区块的区块。

9.错误处理：如果任何验证检查失败，请提出“无效块”错误。否则，请勿返回。

2) EIP-1559

EIP-1559 中为以太坊经济模型引入了一系列旨在提高网络效率和稳定性的机制。

[EIP-1559](https://eips.ethereum.org/EIPS/eip-1559)

此外， eip-4844 引入了一种新型的交易类型，BLOB交易，从而增强了EIP-1559的经济模型。

[EIP-4844](https://eips.ethereum.org/EIPS/eip-4844)

3) GAS 的分析和机制讲解

TODO: 这部分以后再说。暂时不感兴趣。

4) 区块执行过程

5) 执行交易
* stage1: checkpoint state
* stage2: Transaction Normalization and Substate initialization
* stage3: Main Execution
* stage4: Provisional State
* stage5: Pre-Final State
* stage6: Final State

6) 客户端架构

除了执行层执行交易的基本作用外，执行层客户端承担了几个关键职责。其中包括对区块链数据的验证并存储其本地副本，通过与其他执行层客户端的八卦协议来促进网络通信，维护事务池，并满足共识层的要求，以驱动其功能。这种多方面的操作可确保以太坊网络的鲁棒性和完整性。

客户端的体系结构围绕着各种特定标准建立，每个标准在整体功能中都起着独特的作用。执行引擎位于顶部，驱动执行层，而执行层又由共识层驱动。执行层在网络层DevP2P的顶部运行，该网络层是通过提供合法的启动节点来初始化的，该启动节点可为网络提供初始访问点。当我们调用一种引擎API方法之一（例如更新的叉选择更新）时，我们可以通过订阅诸如我们首选的同步模式之类的主题来下载同行的块。

下图说明了设计的简化表示，不包括几个组件：
![客户端架构](https://epf.wiki/images/el-architecture/architecture-overview.png)

**EVM**

以太坊以虚拟化中央处理单元（CPU）为中心。计算机在硬件级别上有自己的中央处理单元（CPU），该单元可能是X86，ARM，RISC-V或其他类型的许多类型。这些多样化的处理器体系结构具有独特的指令集，使它们能够执行算术，逻辑和数据操作等任务，从而使计算机可以用作通用计算机。因此，在执行用硬件级指令集编写的程序时，结果可能会因执行的特定硬件而有所不同。因此，在计算机科学中，我们通过创建虚拟机，例如JVM（Java Virtual Machine）来解决此问题。这些虚拟机构不管基本硬件如何，都可以确保一致的结果。 EVM是为以太坊程序设计的虚拟化执行引擎。无论其运行的硬件如何，它都确保了一致的结果，并在所有以太坊客户端就计算结果促进了共识。

此外，以太坊还将三明治复杂性模型作为设计理念的一部分。这意味着外层应简单，而所有复杂性应集中在中层。在这种情况下，EVM的代码可以看作是最外层的一层，而像固体之类的高级语言可以视为顶层。在两者之间，有一个复杂的编译器将固体代码转换为EVM字节码。

**State**

以太坊是一种通用计算系统，可作为状态机器运行，这意味着它可以根据收到的输入而在几个状态之间过渡。此外，以太坊与像比特币这样的其他区块链有显着不同，因为它保持了全局状态，而比特币仅保留全局的未支付交易输出（UTXOS）。 “状态”一词是指数据结构的全面收集（例如，Merkle-Patricia Tries）以及存储各种信息的数据库。这包括合同的地址，余额，代码和数据以及当前状态和网络状态。

**Transactions**

EVM通过称为状态过渡的过程产生数据并修改以太坊网络的状态。该状态转变是由交易触发的，这些交易是在EVM内处理的。如果事务被认为是合法的，则会导致以太坊网络的状态变化。

**DevP2P**

与其他执行层客户端通信的接口。最初存储在Mempool中的交易是所有传入交易的存储库，通过执行层客户端通过使用点对点通信将执行层客户端传播到网络中的其他执行层客户端。通过网络发送的每笔交易的收件人在将其广播到网络之前确认其有效性。

**JSON-RPC API**

当使用钱包或DAPP时，我们与执行层的通信是通过标准化的JSON-RPC API进行的。这使我们能够外部查询以太坊状态或将交易派遣到钱包签名，后来由执行层客户端验证并围绕网络进行了验证。

**Engine API**

这是共识层和执行层之间唯一的链接。引擎向共识层暴露了两大类端点：fork choice updated 和 new payload，它们分别以三个版本（V1-V3）暴露。这些方法封装了执行层提供的两个主要管道：
* New Payload (V1/V2/V3)：有效负载验证和插入管道。
* Fork Choice Updated (V1/V2/V3)：状态同步和区块构建管道。

**Sync**

为了在以太坊上准确处理交易，我们必须就网络的全局状态达成共识，而不仅仅依赖于本地视角。执行层客户端的全局状态同步是由共识层中LMD-GHOST算法管理的分叉选择规则触发的，然后通过引擎API的fork choice updated端点传递到执行层。同步过程可能包含两个步骤：从对等节点下载远程区块，并在EVM中验证它们。

### 2025.02.09
> 周日

#### 学习内容总结

**Payload building**

基本上一个完整的Payload就代表一个区块创建到执行的完整流程。

**Fork choice updated**
关于ETH POS机制中，如何选择最长有效链的规则。有一篇详细的论文讲解该规则。属于共识层的核心机制。

> Proof-of-stake LMD-GHOST fork choice rule & payload building routine instantiation.

**Transaction Pools**
ETH中的交易池有两个吗？我之前一直以为是一个交易池，是在交易类型上划分Legacy和Blob的不同交易类型，但是都在同一个tx pool中。

TODO: 需要结合代码才能确认。

### 2025.02.10
> 周一

#### 学习内容总结

**什么是EVM?**
> 当 EVM 处理交易时，它会改变以太坊的整体状态。从这个角度来看，以太坊可以被视为一个状态机。

以太坊整体上可以看作是一个基于交易的状态机。它接收交易作为输入并转换到新状态。以太坊的当前状态称为世界状态。

![状态转换示例](https://epf.wiki/images/evm/ethereum-state-machine.gif)

在以太坊中，世界状态本质上是 20 字节地址到账户状态的映射。

![以太坊世界状态](https://epf.wiki/images/evm/ethereum-world-state.jpg)

![三个重要的Trie](https://epf.wiki/images/tries.png)

每个账户状态由存储、代码、余额等数据等各种组件组成，并与特定地址相关联。

以太坊有两种账户：

外部账户：由关联私钥和空的 EVM 代码控制的账户。
合约账户：由关联的非空 EVM 代码控制的账户。作为此类账户一部分的 EVM 代码俗称智能合约。

下面这两个图对于虚拟机所带来的层级优化展示的很好：
![1](https://epf.wiki/images/evm/platform-dependent-execution.jpg)
![2](https://epf.wiki/images/evm/virtual-machine-paradigm.jpg)

这提供了两个关键好处：可移植性（字节码可以在不同平台上运行而无需重新编译）和抽象性（将硬件复杂性与软件分开）。因此，开发人员可以为单个虚拟机编写代码：

在计算机体系结构中，word是指 CPU 可以一次处理的固定大小的数据单元。EVM 的word size为 32 字节。

![alt text](https://epf.wiki/images/evm/evm-anatomy.jpg)

EVM 是以太坊状态机的状态转换函数。它根据 input （transactions） 和 current state 的 intent 值。它作为虚拟机实现，因此它可以在任何平台上运行，独立于底层硬件。

**EVM 字节码**
EVM 字节码是程序的字节序列（8 位）的表示。字节码中的每个字节都是：
* 称为 OpCode 的指令，or指令。
* input 传递给称为 operand 的操作码。

![EVM 字节码格式](https://epf.wiki/images/evm/opcode-binary.jpg)

为简洁起见，EVM 字节码通常用十六进制表示法表示：
![EVM 字节码十六进制](https://epf.wiki/images/evm/opcode-hex.jpg)


为了进一步增强理解能力，作码具有人类可读的助记词。这种简化的字节码称为 EVM 汇编，是 EVM 代码的最低人类可读形式：
![EVM 汇编](https://epf.wiki/images/evm/opcode-assembly.jpg)

从作数中识别作码非常简单。目前，只有 PUSH*作码具有作数（这可能会随 EOF 而改变）。PUSHX 定义作数长度（PUSH 后的 X 字节）。


### 2025.02.11
> 周二

笔记内容

### 2025.02.12
> 周三

#### 学习总结
参考：https://epf.wiki/#/wiki/EL/evm

细致的了解了EVM的执行流程，以及EVM的执行引擎。

### 2025.02.14
> 周五

参考：https://epf.wiki/#/wiki/EL/evm

结合geth的代码，粗略的看了一下evm的实现。

### 2025.02.15
> 周六

笔记内容

### 2025.02.16
> 周日

笔记内容


<!-- Content_END -->
