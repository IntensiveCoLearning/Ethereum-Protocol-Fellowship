---
timezone: Asia/Shanghai
---
# {Patrick}

1. 自我介绍
Hi, 我是国内一名理科研究生，会一些编程语言，平时科研主要也是写程序算东西，
自学过一些前端、后端、服务器运维等知识（每次用还得去查一堆代码的程度，不过有了AI之后好了许多）

对区块链技术很感兴趣，希望学习到硬核的知识。

3. 你认为你会完成本次残酷学习吗？ Yes.
4. TG 联系方式：@ppatrick007

## Notes

<!-- Content_START -->

### 2025.02.06

### 今日学习主题：Ethereum —— The World Computer
- **Ethereum 是世界计算机**
  - 以太坊（Ethereum）是一种去中心化计算平台，为全球提供可信、开放、可编程的计算环境。
  - 由 **Ethereum Virtual Machine (EVM)**、**Ethereum Blockchain** 和 **Ethereum Network** 三部分组成。

- **以太坊共识机制**
  - 早期采用 **Proof of Work (PoW)**，2022年成功切换至 **Proof of Stake (PoS)**。
  - 使用 32 ETH 即可成为验证者（Validator），同时有 **Slashing（惩罚机制）** 来保证网络安全性。

- **去信任化（Trustless Trust）**
  - 以太坊的核心目标是 **可信中立（Credible Neutrality）**。
  - 通过 PoS 及去中心化架构实现全球无须信任的协调机制。

- **DeFi 及以太坊生态**
  - 以太坊支持 **去中心化金融（DeFi）**，让用户能够拥有 **互联网原生的财产所有权**。
  - 未来可能拓展至 **NFT、游戏、投票、物流** 等多种应用场景。

- **以太坊的扩展性挑战**
  - 目前以太坊面临 **扩展性三难困境（Scalability Trilemma）**，在 **安全、去中心化、扩展性** 之间需要权衡。
  - **Rollups** 和 **Danksharding** 可能是未来解决方案，提高吞吐量的同时保持去中心化。

### 2025.02.07

### 主题：Ethereum 执行层（Execution Layer）

#### 主要内容
今天的学习主要根据去年EPFsg的week2内容，重点是 **Ethereum 执行层（Execution Layer, EL）**，它负责处理交易、执行智能合约并维护以太坊的状态。主要涉及以下方面：

#### 执行层概览
- 负责处理状态转换（State Transition）。
- 验证并执行每一笔交易，将其累积到状态树（State Trie）。
- 处理以太坊改进提案（EIP）相关的机制，如：
  - **EIP-1559**: 交易基础费用调整机制。
  - **EIP-4844**: 处理 Blob Gas 以提高扩展性。
  - **信标链提款（Beacon Chain Withdrawals）**。

#### 区块验证（Block Validation）
- 执行层需要验证每个区块：
  - **头部验证（Header Validation）**：
    - 校验 **Merkle Root**。
    - 确保 **Gas Limit** 在合理范围内。
    - 确保时间戳有效。
  - **区块处理（Block Processing）**：
    - 通过 `state_processor.go` 执行状态转换。

#### EVM 及其操作码
- 以太坊虚拟机（EVM）是基于 **堆栈（Stack Machine）** 的计算环境。
- 主要操作码类别：
  - **栈/内存操作（Stack & Memory Manipulation）**。
  - **环境获取（Env Getters）**。
  - **以太坊系统操作（Ethereum System Operations）**。

#### P2P 网络 & 同步机制
- 以太坊的 **P2P 网络** 负责：
  - **提供历史数据**。
  - **广播待处理交易**。
  - **管理状态同步**。
- **Snap Sync 机制**：
  - **第一阶段：下载 Snap Tiles**（快速获取区块状态）。
  - **第二阶段：Healing**（填补数据缺失）。

#### JSON-RPC 及 Engine API
- JSON-RPC 是 **与以太坊交互的主要接口**，目标是所有客户端提供一致 API。
- 主要 RPC 方法：
  - `eth_getBlockByNumber`
  - `eth_call`
  - `eth_sendTransaction`
  - `eth_subscribe`

### 2025.02.08

###  主题：Ethereum 共识层（Consensus Layer, CL）

####  主要内容
今天的学习重点是 **Ethereum 共识层（Consensus Layer, CL）**，它负责以太坊网络的安全性、数据一致性以及区块共识机制。主要涉及以下方面：

#### 共识层概述
- 区块链保证了 **数字稀缺性（Digital Scarcity）**，但需要 **安全性** 来确保其完整性。
- 分布式网络需要 **拜占庭容错（Byzantine Fault Tolerance, BFT）** 来应对恶意节点。
- **比特币（Bitcoin）** 通过 **工作量证明（Proof-of-Work, PoW）** 解决了 BFT 问题。
- **以太坊（Ethereum）** 通过 **权益证明（Proof-of-Stake, PoS）** 作为新共识机制。

#### PoS 机制
- PoS 由 **信标链（Beacon Chain）** 管理，并使用 **验证者（Validators）** 进行区块提议和投票。
- **从 PoW 转向 PoS 的关键变化：**
  - 由 **计算能力（哈希算力）** 转向 **代币抵押（Stake）** 作为 **反女巫攻击（Sybil Protection）** 机制。
  - 通过 **BFT 机制** 确保网络达成一致。
  - 参与 PoS 需要 **质押 32 ETH**，被选中的验证者负责出块和投票。

#### 拜占庭容错与 Slashing
- 以太坊 PoS 采用 **拜占庭容错（BFT Majority）** 来决定链的状态。
- 如果验证者行为异常或恶意，则会触发 **Slashing（削减惩罚）**：
  - **部分 Slash**：轻微违规，如错误投票，扣除部分质押。
  - **完全 Slash**：严重违规，如双重签名，导致全部 ETH 被销毁并被逐出网络。

#### Fork Choice Rule: LMD-GHOST
- 以太坊 PoS 使用 **LMD-GHOST（Latest Message Driven - Greedy Heaviest Observed Subtree）** 作为 **分叉选择规则（Fork Choice Rule）**：
  - **最新投票驱动**（Latest Message Driven）：最新投票更具权重。
  - **贪心最重子树**（Greedy Heaviest Observed Subtree）：选择投票最多的链作为主链。
  - **保证活跃性（Liveness）**：结合 **Casper FFG** 确保网络不会停滞。

#### 以太坊的加密经济安全性
- **Casper** 提供了更强的经济安全性：
  - 质押 ETH 提供了 **经济安全保证**，攻击者必须承担高额成本。
  - **双重签名 = 资金被 Slash**，确保验证者不会作恶。

### 2025.02.09

### 主题：开发和测试（Development and Testing）

#### 主要内容
今天的重点是以太坊的 **开发和测试**，包括如何进行节点的开发与测试、如何确保系统的稳定性和安全性等。

#### 开发概述
- **开发环境设置**：确保每个参与者的开发环境一致是关键，使用容器化（如 Docker）或虚拟机（VM）来模拟以太坊节点环境。
- **工具链**：常用的开发工具包括 **Go-Ethereum（Geth）** 和 **Besu** 等，以太坊的客户端实现；此外，**Hardhat** 和 **Truffle** 也常用于开发和测试智能合约。
- **智能合约开发**：了解如何在以太坊网络上部署和交互，重点是与 EVM 进行交互的能力。

#### 测试
- **自动化测试**：使用工具（如 **Ganache**、**Hardhat Network**）进行本地链测试，确保代码和智能合约的稳定性。
- **E2E 测试**：从区块链网络的端到端进行测试，模拟整个以太坊网络和应用的交互，以便测试其是否能正常运行。

#### 安全性
- **智能合约安全**：通过静态分析工具（如 **MythX**、**Slither**）来扫描合约中的漏洞。
- **攻击模型**：理解可能的攻击类型，如 **重入攻击（Reentrancy）**、**时间戳依赖性**、**整数溢出（Overflow）** 等，并采取相应的防护措施。

#### 测试实例
- **覆盖率测试**：测试合约的各个功能，确保所有可能的路径都被测试覆盖。
- **模拟真实场景**：使用 **测试网（Testnets）** 和 **正式网（Mainnet）** 的相同配置和行为来模拟真实场景，确保应用程序的稳定性。

### 2025.02.10

### 主题：以太坊研究现状与路线图（Ethereum Research and Roadmap）

#### 主要内容
今天的重点是 **以太坊当前的研究方向和未来发展路线图**，以及涉及 **节点工作坊（Node Workshop）** 相关的内容。

#### 以太坊合并（Merge）
- **Altair 升级**：引入 **轻客户端协议（Light Client Protocol）**，让资源受限的设备能够更轻松地访问以太坊网络。
- **合并（Merge）和提款（Withdrawals）**：主网从 PoW 迁移到 PoS，允许验证者提款。
- **单 Slot Finality（SSF）**：研究提高以太坊区块最终性（Finality）的方法，以减少重组风险。

#### 扩展性（Surge）
- **ZK Rollups & Optimistic Rollups**：两种 Layer 2 方案，提升以太坊吞吐量。
- **KZG 仪式（KZG Ceremony）**：为 **EIP-4844（Proto-Danksharding）** 提供可信设置，提高数据可用性。
- **数据可用性采样（Data Availability Sampling, DAS）**：用于保证 rollup 交易数据的可访问性。
- **跨 Rollup 互操作性（Cross-rollup Interop）**：确保不同 Rollup 之间可以安全交互。

#### 以太坊去中心化 & MEV 研究（Scourge）
- **最小可提取价值（MEV）**：研究如何降低矿工/验证者可提取的额外收益，以减少网络中心化风险。
- **ePBS（加密投票区块提案）**：改善区块提议机制，减少 MEV 操作带来的负面影响。
- **MEV Burn**：类似于 **EIP-1559** 机制，销毁部分 MEV 以减少市场操控。

#### 以太坊状态优化（Verge）
- **Verkle Trees**：提高以太坊存储效率，使状态存储更加轻量化。
- **SNARKify（零知识证明）**：使用 SNARK 进行状态过渡，提高隐私性和同步速度。
  - **信标链快速同步（Beacon Fast Sync）**。
  - **信标链状态转换（Beacon State Transition）**。
  - **Verkle 证明（Verkle Proofs）**。

#### 以太坊协议简化（Purge）
- **EIP-4444**：删除历史状态存储，减少全节点的存储需求，提高同步效率。
- **协议精简（Protocol Simplifications）**：降低协议复杂度，使以太坊更易维护和升级。

#### 以太坊未来创新（Splurge）
- **EIP-1559 终局（Endgame）**：优化交易费用市场，提高用户体验。
- **账户抽象（Account Abstraction, AA）**：减少对 EOA（Externally Owned Accounts）的依赖，使智能合约钱包成为主流。
- **深度加密（Deep Cryptography）**：研究更高效的加密方法，以提高隐私性和安全性。


### 2025.02.11

### 主题：共识层与执行层规范（Consensus and Execution Spec）

#### 主要内容
今天学习的重点是深入了解 **共识层（Consensus Layer）** 和 **执行层（Execution Layer）** 的规范。

#### 共识层规范（Consensus Specs）
- **Hsiao-Wei Wang 的讲座**：介绍了以太坊 **共识规范（Consensus Spec）**，包括其架构、工作原理以及如何在不同的客户端实现。
- **Pyspec**：通过 Python 编写的以太坊共识规范实现，适用于验证共识规则。ß

#### 执行层规范（Execution Layer Specs）
- **Sam Wilson 的讲座**：讨论了 **执行层规范（EELS）**，重点是执行引擎与智能合约执行过程的规范定义。
- 通过演示，Sam 展示了如何通过修改执行层规范来添加新的 **EVM 操作码（Opcode）**。

### 2025.02.12

今天总结了前几天的内容，重点回顾了共识层（Consensus Layer）和执行层（Execution Layer）的规范和基础知识。
没有接触到新的技术内容，主要是通过前几天的学习材料进行巩固和整理。通过对规范的理解和总结，我对以太坊协议的各个部分有了更加系统的认识。
在接下来的学习中，将继续深化对协议各层次的理解，并准备好进入更深入的技术分析阶段。

### 2025.02.13

今天继续学习了Upgrading Ethereum书中共识协议的相关内容，主要总结了以下几个部分：

## 1. 共识协议的基础
共识协议是建立可靠分布式系统的基础。其目标是让多个节点在不可靠的环境下达成一致，形成单一的交易历史。每个节点维护一个账本，确保所有账本内容一致，达成一致并迅速确认。

## 2. 区块链的基本概念
区块链的基本单位是“区块”，每个区块包含交易数据，并通过特定的规则链接到前一个区块，形成区块链。每个区块的选择和排序由“区块领导者”决定，区块领导者是通过特定的共识机制（如工作量证明、权益证明等）选举出来的。

## 3. 分叉与分叉选择规则
在真实的网络环境中，区块链可能出现“分叉”现象，即多个区块链分支并存。区块链协议通过分叉选择规则来确定最终被认可的链。这一规则确保所有正确的节点最终会达成一致，选择一个唯一的线性链。

## 4. 算法背景
讨论了“拜占庭将军问题”和实际解决方案，比如PBFT和Nakamoto共识。PBFT能够确保协议的“安全性”，但在异步网络中失去活跃性，而Nakamoto共识则允许分叉，注重“活跃性”而非“安全性”。

## 5. 工作量证明与权益证明
虽然工作量证明（PoW）和权益证明（PoS）都被称为共识协议，但实际上它们并不是独立的共识协议，而是支持共识协议的机制，确保系统具有抗Sybil攻击的能力。



<!-- Content_END -->
