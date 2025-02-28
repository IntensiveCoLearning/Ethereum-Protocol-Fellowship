---
timezone: Asia/Shanghai
---


# ThalesLiu

1. 我是ThalesLiu, solidity练习生，以太坊支持者
2. 你认为你会完成本次残酷学习吗？ 应该可以


## Notes

<!-- Content_START -->

### 2025.02.06

目前协议由 2 个主要部分组成 - 执行层和共识层。执行层 （EL） 处理实际交易和用户交互，是全球计算机执行其程序的地方。共识层 （CL） 提供权益证明共识机制 - 一种加密经济安全，确保所有节点都遵循相同的提示并驱动执行层的规范链。 目前以太坊协议面向未来采用了模块化，模块化源于封装复杂性的理念。当系统由子系统组成时，就会出现封装复杂性 —— 这些子系统内部很复杂，可以通过高级接口提供给外部。现在，这在子系统的选择和更好的单个组件调试方面产生了很大的灵活性。

### 2025.02.07
了解了一下目前 ethereum 所使用的几种不同的执行层客户端。 这使得网络更加强大和多样化。理想目标是实现多样性，而没有任何客户端占主导地位，以减少任何单点故障。 主要包括以下五种
##### 执行客户端
| 客户端                                                       | 语言       | 操作系统              | 
| ------------------------------------------------------------ | ---------- | --------------------- | 
| [Geth](https://geth.ethereum.org/)                           | Go         | Linux、Windows、macOS | 
| [Nethermind](https://www.nethermind.io/)                     | C#、.NET   | Linux、Windows、macOS | 
| [Besu](https://besu.hyperledger.org/en/stable/)              | Java       | Linux、Windows、macOS | 
| [Erigon](https://github.com/ledgerwatch/erigon)              | Go         | Linux、Windows、macOS | 
| [Reth](https://reth.rs/)                                     | Rust       | Linux、Windows、macOS | 
| [EthereumJS](https://github.com/ethereumjs/ethereumjs-monorepo) | TypeScript | Linux、Windows、macOS | 

### 2025.02.08
以太坊权益证明的核心是一条称为“信标链”的系统链。信标链存储和管理验证者注册表。在权益证明的初始部署阶段，成为验证者的唯一机制是将 ETH 交易单向（Capella 后可提现）到以太坊工作量证明链上的存款合约。当信标链处理存款收据、达到激活余额并完成排队过程时，就会激活验证者。退出要么是自愿的，要么是作为对不当行为的惩罚而被迫进行的。信标链上的主要负载来源是 “证明”。证明同时是分片块的可用性投票（在以后的升级中）和信标块的权益证明投票（第 0 阶段）。

### 2025.02.09
EIP-4844，也称为 proto-danksharding，是 Deneb/Cancun 硬分叉的一部分。它为以太坊引入了数据可用性层，允许在区块链上临时存储任意数据。这种以这种方式存储的任意数据称为 blob，每个块可以有 3 ~ 6 个 blob sidecar（blob 的包装器）。EIP-4844 标志着以太坊迈向分片和可扩展性的第一步，使第 2 层解决方案 （L2） 能够使用此数据可用性层来降低 gas 费用并处理更多交易。

### 2025.02.10
如何在以太坊权益证明中执行交易
发起交易：用户通过钱包工具签署交易，设定燃料费（小费给验证者，基础费被销毁），并通过节点提交至以太坊网络。
验证交易：节点检查交易有效性（余额足够、签名正确），通过后存入本地待处理交易池（内存池），并广播给全网节点。部分高级用户会绕过广播，直接将交易发送给专业区块构建者以优化收益（如利用MEV策略）。
打包区块：当前时隙的随机选中的验证节点（提议者）将内存池交易打包为“执行负载”，生成状态变更数据，并封装到包含共识信息的“信标区块”中。
全网验证：其他节点收到新区块后，在本地重新执行交易以验证有效性。验证者确认区块合法后，将其加入自身数据库，并基于多数共识（分叉规则）认可其为链上新头区块。
最终确认：交易需在两个连续时段（检查点）间获得超过66%质押以太坊的共识验证，方可视为不可逆的“最终确定”状态。检查点机制确保网络周期性达成全局一致。

### 2025.02.11
权益证明相较于工作量证明有如下一些优点：
能效更高 – 无需在工作量证明计算中使用大量能源
门槛更低、硬件要求下降 – 无需购买高性能硬件以便获得创建新区块的机会
中心化风险降低 – 权益证明应该可以增加保护网络安全的节点

### 2025.02.12
• Phase0 – 未来升级的准备阶段，引入主要的信标链状态和权益证明（PoS）设计。大多数基础规范在这个硬分叉中建立。
• Altair – 继续为从工作量证明（PoW）迁移到权益证明（PoS）做准备。这个硬分叉引入了轻客户端协议和“同步委员会”，这是一个由 512 个验证器在每个“同步委员会周期”（约 1 天）中伪随机选择的特殊子集。这些验证器不断签署新的信标区块头，使得“外部”的轻客户端能够以显著简化的复杂度验证共识状态。
• Bellatrix – 这个硬分叉标志着正式转向权益证明，使用在早期硬分叉中引入的规范。它作为“合并”的“开启”开关。
• Capella – 这个硬分叉启用了验证器的提现，这在之前的版本中是禁用的。它通过允许验证器提取奖励，最终确定了以太坊 PoS 的完整经济模型。
• Deneb – 在撰写本文时最新的硬分叉（2025 年 1 月）。它将信标区块根添加到以太坊虚拟机（EVM），这是跨链证明以太坊共识的重要变化，并更改了一些与证明和激活/退出限制相关的值。
• Electra – 一个未来的硬分叉，将验证器的最大有效余额从 32 ETH 增加到 2048 ETH，允许整合许多冗余的验证器。此外，它引入了对存款和提现的重大更改，使其更快、更灵活。
• Fulu – 目前正在建设中。

### 2025.02.13
账户抽象是如何工作的
用户创建 UserOperations 对象。
Bundlers 将多个 UserOperations 组合成一个交易并发送到 EntryPoint 合约。 
EntryPoint 启动验证，该验证在 CA 上实现。然后，它通过调用在 CA 上实现的 `execute()` 函数来处理交易。
UserOperations 被执行，触发状态变化。
可选地，Aggregator 聚合签名验证，并由 Paymaster 处理交易费用。

### 2025.02.14
[EIP-7702](https://eips.ethereum.org/EIPS/eip-7702) 并不完全是帐户抽象，但它确实提供了执行抽象，即为外部拥有帐户 (EOA) 添加了额外功能。这使你的 EOA 能够执行如发送批量交易和委托给其他加密密钥方案 (如 passkeys) 等操作。它通过将与 EOA 关联的代码设置为协议级别的代理标识来实现这一点。可以在[此处](https://eips.ethereum.org/EIPS/eip-7702)找到完整的规范。EIP-7702 引入了一种新的交易类型，可在单笔交易期间临时授权 EOA 特定的合约代码，使其能够像智能合约帐户一样运作。这为用户提供了多个应用场景，包括批量交易、gas 赞助和权限降级。

### 2025.02.15
Maximal Extractable Value (MEV)，即最大可提取价值，指的是通过在区块生产中有策略地排序、包含或排除交易，超出标准区块奖励和 Gas 费用所能提取的最大价值。
在以太坊中，MEV 尤其在 DeFi 应用中受到关注，常见策略包括抢跑（front-running）、夹心攻击（sandwiching）和尾随（back-running）。
MEV 的影响
MEV 的提取可能导致：大型矿池或验证者的不公平优势；对 DeFi 用户的负面影响，如滑点增加或交易被审查。

### 2025.02.16
EVM 作为深度为 1024 个项目的堆栈机器执行。每个项目都是一个 256 位字，选择该字是为了便于与 256 位加密技术（例如 Keccak-256 哈希或 secp256k1 签名）一起使用。在执行过程中，EVM 维护一个瞬态内存（作为字寻址字节数组），该内存不会在交易之间持续存在。但是，合约确实包含一个 Merkle Patricia 存储树（作为字可寻址的字数组），与相关账户相关联，并且是全局状态的一部分。编译后的智能合约字节码作为多个 EVM作码执行，这些作码执行标准堆栈作，如 XOR、AND、ADD、SUB 等。EVM 还实现了许多特定于区块链的堆栈作，例如 ADDRESS、BALANCE、BLOCKHASH 等
### 2025.02.17
以太坊虚拟机有不同的区域可以存储数据，其中最突出的是存储、瞬态存储、内存和堆栈。每个账户都有一个称为 storage 的数据区域，该数据区域在函数调用和事务之间是持久的。Storage 是将 256 位字映射到 256 位字的键值存储。不可能从 Contract 中列举 storage，读取成本相对较高，初始化和修改 storage 的成本更高。由于这种成本，您应该将存储在持久存储中的内容减少到合约运行所需的数量。将派生计算、缓存和聚合等数据存储在合约外部。合约既不能读取也不能写入除其自身以外的任何存储。
与存储类似，还有另一个数据区域称为瞬态存储，其主要区别在于它在每个事务结束时重置。存储在此数据位置中的值仅在源自事务的第一次调用的函数调用中保留。当事务结束时，瞬态存储将被重置，并且存储在其中的值将对后续事务中的调用不可用。尽管如此，读取和写入临时存储的成本明显低于存储。
第三个数据区域称为 memory，合约为每次消息调用获取一个新清除的实例。内存是线性的，可以在字节级别寻址，但读取限制为 256 位的宽度，而写入可以是 8 位或 256 位宽。当访问（读取或写入）以前未触及的内存字（即字中的任何偏移量）时，内存会扩展一个字（256 位）。在扩建时，必须支付 gas 成本。内存增长得越大，成本就越高（它以二次方方式扩展）。
EVM 不是寄存器机，而是**堆栈机**，因此所有计算都在称为堆栈的数据区域上执行。它的最大大小为 1024 个元素，包含 256 位的字。对堆栈的访问仅限于顶端，方式如下：可以将最顶部的 16 个元素之一复制到堆栈顶部，或者将最顶部的元素与其下方的 16 个元素之一交换。所有其他作从堆栈中获取最上面的两个（或一个或多个，取决于作）元素，并将结果推送到堆栈上。当然，可以将堆栈元素移动到 storage 或 memory 以获得对堆栈的更深访问，但不首先删除堆栈的顶部，就不可能只访问堆栈中更深的任意元素。
### 2025.02.18
calldata 区域是作为智能合约交易的一部分发送到交易的数据。例如，在创建合约时，calldata 将是新合约的构造函数代码。外部函数的参数最初总是以 ABI 编码的形式存储在 calldata 中，然后才解码到其声明中指定的位置。如果声明为 memory，编译器将在函数开始时急切地将它们解码到内存中，而将它们标记为 calldata 意味着这将延迟完成，仅在访问时完成。值类型和存储指针直接解码到堆栈上。
returndata 是智能合约在调用后返回值的方式。通常，外部 Solidity 函数使用 return 关键字将值 ABI 编码到 returndata 区域。
代码是存储智能合约的 EVM 指令的区域。Code 是 EVM 在智能合约执行期间读取、解释和执行的字节。存储在代码中的指令数据作为合约账户状态字段的一部分是持久的。不可变变量和常量变量存储在代码区域中。对 immutable 的所有引用都将替换为分配给它们的值。对于常量，将执行类似的过程，这些常量的表达式内联在智能合约代码中引用它们的位置。
### 2025.02.19
支付的总 Gas 费分为两部分：基本费用和优先费用 （TIP）。基本费用由协议设定 - 您必须至少支付此金额才能使您的交易被视为有效。优先费是您添加到基本费用中的一个小费，以使您的交易对验证者有吸引力，以便他们选择将其包含在下一个区块中。仅支付基本费用的交易在技术上是有效的，但不太可能被包括在内，因为它没有激励验证者选择它而不是任何其他交易。“正确”的优先费用取决于您发送交易时的网络使用情况 - 如果需求很大，那么您可能必须将优先费用设置得更高，但是当需求较少时，您可以支付更少的费用。
gas 费用有助于保持以太坊网络的安全。通过对网络上执行的每次计算收取费用，我们可以防止不良行为者向网络发送垃圾邮件。为了避免代码中出现意外或恶意的无限循环或其他计算浪费，每个事务都需要设置其可以使用的代码执行计算步骤数的限制。基本计算单位是 “gas”。尽管交易包含限制，但交易中未使用的任何 gas 都会退还给用户（即返回最高费用 - （基本费用 + 小费））。
### 2025.02.20
使用智能合约执行人之间的协议并非易事，因为以太坊是确定性系统。 确定性系统(opens in a new tab)是指在给定初始状态和特定输入的情况下始终产生相同结果的系统，这意味着根据输入计算输出的过程不存在随机性或变化。预言机通常由链上运行的智能合约和一些链下组件构成。 链上合约接收其他智能合约的数据请求，并将这些请求传送给链下组件（称为预言机节点）。 这类预言机节点可以查询数据源—例如使用应用程序接口 (API)—并发送交易将请求的数据存储在智能合约的存储中。
### 2025.02.21
Bridges can usually be classified into one of the following buckets:
网桥通常可以分为以下类别之一：

Native bridges – These bridges are typically built to bootstrap liquidity on a particular blockchain, making it easier for users to move funds to the ecosystem. For example, the Arbitrum Bridge(opens in a new tab)
原生桥 – 这些桥通常用于引导特定区块链上的流动性，使用户更容易将资金转移到生态系统中。例如，Arbitrum 桥 is built to make it convenient for users to bridge from Ethereum Mainnet to Arbitrum. Other such bridges include Polygon PoS Bridge, Optimism Gateway(opens in a new tab)
旨在方便用户从 Ethereum 主网桥接到 Arbitrum。其他此类桥包括 Polygon PoS Bridge、Optimism Gateway, etc.  等。
Validator or oracle based bridges – These bridges rely on an external validator set or oracles to validate cross-chain transfers. Examples: Multichain and Across.
基于验证器或预言机的桥 –这些桥依赖于外部验证器集或预言机来验证跨链传输。示例：Multichain 和 Across。
Generalized message passing bridges – These bridges can transfer assets, along with messages and arbitrary data across chains. Examples: Axelar, LayerZero, and Nomad.
通用消息传递桥 –这些桥可以跨链传输资产、消息和任意数据。示例：Axelar、LayerZero 和 Nomad。
Liquidity networks – These bridges primarily focus on transferring assets from one chain to another via atomic swaps. Generally, they don’t support cross-chain message passing. Examples: Connext and Hop.
流动性网络 –这些桥主要专注于通过原子交换将资产从一条链转移到另一条链。通常，它们不支持跨链消息传递。示例：connext 和 hop。
### 2025.02.22
ERC-20 - A standard interface for fungible (interchangeable) tokens, like voting tokens, staking tokens or virtual currencies.
ERC-223 - A fungible tokens standard that makes tokens behave identical to ether and supports token transfers handling on the recipients side.
ERC-1363(opens in a new tab) - Defines a token interface for ERC-20 tokens that supports executing recipient code after transfer or transferFrom, or spender code after approve.
ERC-721 - A standard interface for non-fungible tokens, like a deed for artwork or a song.
ERC-2309(opens in a new tab) - A standardized event emitted when creating/transferring one, or many non-fungible tokens using consecutive token identifiers.
ERC-4400(opens in a new tab) - Interface extension for EIP-721 consumer role.
ERC-4907(opens in a new tab) - Add a time-limited role with restricted permissions to ERC-721 tokens.
ERC-777 - (NOT RECOMMENDED) A token standard improving over ERC-20.
ERC-1155 - A token standard which can contain both fungible and non-fungible assets.
ERC-4626 - A tokenized vault standard designed to optimize and unify the technical parameters of yield-bearing vaults.
### 2025.02.23
Optimistic rollup 是在以太坊上运行的链下扩容解决方案。每个Optimistic rollup都由部署在 Ethereum 网络上的一组智能合约管理。Optimistic rollup 处理以太坊主链上的交易，但将链下交易（批量）发布到链上 rollup 合约。与以太坊区块链一样，此交易记录是不可变的，并形成“Optimistic rollup CHAIN”。链上合约：乐观卷叠的运行由运行在以太坊上的智能合约控制。这包括存储 rollup 区块、监控 rollup 状态更新和跟踪用户存款的合约。从这个意义上说，以太坊是乐观卷叠的基础层或“第 1 层”。链下虚拟机 （VM）：尽管管理乐观卷叠协议的合约在以太坊上运行，但卷叠协议在独立于以太坊虚拟机的另一个虚拟机上执行计算和状态存储。链下 VM 是应用程序所在的位置，也是执行状态更改的地方;它充当乐观卷叠的上层或“第 2 层”。
### 2025.02.25
零知识卷叠 （ZK-rollups） 将交易捆绑（或“卷叠”）成批次，在链下执行。链下计算减少了必须发布到区块链的数据量。零知识卷叠作员提交表示批量中所有交易所需的更改摘要，而不是单独发送每个交易。他们还生成有效性证明来证明其更改的正确性。零知识卷叠的状态由部署在以太坊网络上的智能合约维护。要更新此状态，ZK-rollup 节点必须提交有效性证明进行验证。如前所述，有效性证明是一种加密保证，即 rollup 提出的状态更改实际上是执行给定批次交易的结果。这意味着零知识卷叠只需要提供有效性证明即可在以太坊上完成交易，而不是像乐观卷叠那样将所有交易数据发布到链上。将资金从 ZK-rollup 转移到以太坊时没有延迟，因为一旦 ZK-rollup 合约验证了有效性证明，就会执行退出交易。相反，从 Optimistic Rollup 中提取资金可能会有延迟，以允许任何人使用 欺诈证明。
### 2025.02.27
通道是简单的点对点协议，允许双方在他们之间进行许多交易，然后只将最终结果发布到区块链。该通道使用加密技术来证明它们生成的摘要数据确实是一组有效的中间事务的结果。“多重签名”智能合约可确保交易由正确的各方签署。使用通道，状态更改由相关方执行和验证，从而最大限度地减少以太坊执行层的计算。这减少了以太坊的拥塞，也提高了用户的交易处理速度。每个通道都由运行在以太坊上的多重签名智能合约管理。要打开通道，参与者将通道合约部署到链上并将资金存入其中。双方共同签署状态更新以初始化通道的状态，之后他们可以快速自由地在链下进行交易。要关闭通道，参与者需要在链上提交通道的最后约定状态。之后，智能合约根据每个参与者在通道最终状态下的余额分配锁定的资金。点对点通道对于某些预定义的参与者希望以高频率进行交易而不会产生可见开销的情况特别有用。区块链通道分为两类：支付通道和状态通道。
<!-- Content_END -->
