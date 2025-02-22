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


### 2025.02.15

# 以太坊 2.0 自定义数据类型

以太坊 2.0 协议中定义了一些自定义数据类型，用于提高代码的可读性和类型提示。虽然这些类型在整个协议中频繁出现，但它们是构建其他结构的基础。

## 数据类型

### Slot（时隙）
- **描述**：表示一个时间段或时隙。每个时隙会选择一个验证者提议区块。

### Epoch（纪元）
- **描述**：由多个时隙组成，用来划分协议中的一段时间。每个纪元结束时，验证者的余额会被更新，委员会会重新组织。

### CommitteeIndex（委员会索引）
- **描述**：每个时隙中会有多个委员会，而每个委员会会被赋予一个索引来标识。

### ValidatorIndex（验证者索引）
- **描述**：每个验证者都会有一个唯一的索引，作为他们在验证者注册表中的标识。

### Gwei
- **描述**：表示以太坊中某个金额，单位为 Gwei，1 Gwei = 10⁹ Wei。

### Root（根哈希）
- **描述**：Merkle 根，用于加密数据的摘要，是一种简洁且防篡改的数据表示方式。

### Hash32
- **描述**：一个 256 位的加密哈希，用于表示以太坊 1 的区块哈希。

### BLSPubkey（BLS 公钥）
- **描述**：BLS12-381 公钥，代表一个验证者的公钥。

### BLSSignature（BLS 签名）
- **描述**：BLS 签名，用于验证协议消息的真实性。

### ParticipationFlags（参与标志）
- **描述**：用于跟踪验证者的参与状态，帮助提高处理效率，减少纪元边界时的处理负担。

### Transaction（交易）
- **描述**：表示以太坊的交易，包含在 Beacon 链区块中的执行层交易。

### ExecutionAddress（执行地址）
- **描述**：表示交易执行层中的地址，用于标识交易的费用接收地址。

### WithdrawalIndex（提取索引）
- **描述**：表示从共识层到执行层的提取交易的索引。

### 2025.02.16

# Beacon Chain 配置和初始化

尽管 Beacon 链的创世事件已经过去，但初始化功能仍然对启动测试网络等场景非常有用。在此，我们讲解的是关于 Beacon 链创世的参数配置。

## 创世设置

### 参数配置

| 名称 | 值 |
|------|----|
| **MIN_GENESIS_ACTIVE_VALIDATOR_COUNT** | uint64(2**14) (= 16,384) |
| **MIN_GENESIS_TIME** | uint64(1606824000) (2020年12月1日，12:00 UTC) |
| **GENESIS_FORK_VERSION** | Version('0x00000000') |
| **GENESIS_DELAY** | uint64(604800) (7天) |

### MIN_GENESIS_ACTIVE_VALIDATOR_COUNT
- **描述**：在 Beacon 链能够开始生产区块之前，必须至少有这么多验证者的质押数。这个数量是为了确保一定的安全性，以防止少数验证者控制网络。
- **默认值**：16,384（即 2¹⁴）

### MIN_GENESIS_TIME
- **描述**：Beacon 链可以启动的最早时间。这是为了避免 "门卫攻击"（gatekeeper attack），即少数验证者控制初期区块，防止其他验证者进入网络。
- **默认值**：2020年12月1日 12:00 UTC

### GENESIS_FORK_VERSION
- **描述**：创世事件时的分叉版本。这个版本号仅在计算加密域（用于存储消息和 BLS 凭证更改）时使用。
- **默认值**：Version('0x00000000')

### GENESIS_DELAY
- **描述**：Beacon 链创世事件前的延迟时间，允许节点和节点运营商有足够的时间做好准备。
- **默认值**：604800 秒（7天）

## 各个分叉版本

| 名称 | 值 |
|------|----|
| **ALTAIR_FORK_VERSION** | Version('0x01000000') |
| **ALTAIR_FORK_EPOCH** | Epoch(74240) (2021年10月27日 10:56:23 UTC) |
| **BELLATRIX_FORK_VERSION** | Version('0x02000000') |
| **BELLATRIX_FORK_EPOCH** | Epoch(144896) (2022年9月6日 11:34:47 UTC) |
| **CAPELLA_FORK_VERSION** | Version('0x03000000') |
| **CAPELLA_FORK_EPOCH** | Epoch(194048) (2023年4月12日 10:27:35 UTC) |

## 时间参数

| 名称 | 值 | 单位 | 时长 |
|------|----|------|------|
| **SECONDS_PER_SLOT** | uint64(12) | 秒 | 12秒 |
| **SECONDS_PER_ETH1_BLOCK** | uint64(14) | 秒 | 14秒 |
| **MIN_VALIDATOR_WITHDRAWABILITY_DELAY** | uint64(2**8) (= 256) | 纪元 | ~27小时 |
| **SHARD_COMMITTEE_PERIOD** | uint64(2**8) (= 256) | 纪元 | ~27小时 |
| **ETH1_FOLLOW_DISTANCE** | uint64(2**11) (= 2,048) | Eth1区块 | ~8小时 |

### SECONDS_PER_SLOT
- **描述**：每个时隙的时长。最初是6秒，现在是12秒。网络延迟是决定时隙长度的主要因素。
- **当前值**：12秒

### SECONDS_PER_ETH1_BLOCK
- **描述**：假设的 Eth1 区块时间，用于与 `ETH1_FOLLOW_DISTANCE` 一起计算 Eth1 链上的区块。
- **当前值**：14秒

### MIN_VALIDATOR_WITHDRAWABILITY_DELAY
- **描述**：当验证者退出协议时，仍需等待此延迟期才能完全提取其质押和奖励。
- **当前值**：256个纪元（约27小时）

### SHARD_COMMITTEE_PERIOD
- **描述**：每个分片委员会的周期，也就是每多少个纪元会重新安排委员会成员。
- **当前值**：256个纪元（约27小时）

### ETH1_FOLLOW_DISTANCE
- **描述**：Beacon 链如何同步 Eth1 链的区块。该值定义了 Beacon 链对 Eth1 链的跟随距离。
- **当前值**：2048个 Eth1 区块（约8小时）

### 2025.02.17

## 以太坊 2.0 预设参数（Preset）

以太坊 2.0 规范中定义了一些预设参数（Preset），用于配置不同的网络环境。目前主要有 **Mainnet（主网）** 和 **Minimal（测试用）** 两种预设。主网配置在 Beacon 链上运行，而 Minimal 预设则用于测试。其他配置也是可能的，例如 Teku 客户端使用 Swift 配置进行验收测试。

这些参数大多是 **2 的幂次**，这是计算机科学中的常见做法，便于优化计算，并减少对参数取值的争论（bike-shedding）。

---

## 1. 主要配置参数

### **最大委员会数（MAX_COMMITTEES_PER_SLOT）**
- 在 Beacon 链中，验证者会被组织成委员会，每个时隙最多可以有 64 个委员会。
- 每个委员会的成员对区块进行 **投票（Attestation）**，最终整个网络会基于投票结果选择最优的链。

### **目标委员会大小（TARGET_COMMITTEE_SIZE）**
- 设定了每个委员会的目标最小人数，以确保委员会具备足够的去中心化和安全性。
- 如果网络中的验证者数量过少，系统会 **减少每个时隙的委员会数** 来维持合理的委员会规模。
- 只有当验证者总数低于 `SLOTS_PER_EPOCH * TARGET_COMMITTEE_SIZE = 4096` 时，委员会规模才会小于目标值。

### **单个委员会的最大验证者数（MAX_VALIDATORS_PER_COMMITTEE）**
- 主要用于 **限制数据结构的大小**，并不影响正常运行。
- 若达到此上限，意味着网络已有超过 **400 万个活跃验证者**，质押总量将超过 **128M ETH**，远超目前的以太坊供应量。

### **验证者随机打乱轮数（SHUFFLE_ROUND_COUNT）**
- 以太坊 2.0 采用 **Swap-or-Not Shuffle** 算法对验证者进行随机分组，以确保委员会不会被攻击者轻易控制。
- 该算法的洗牌轮数为 **90**，能够保证在 **330 万个验证者** 的情况下仍然提供足够的随机性。

---

## 2. 平衡调整参数（Hysteresis）

以太坊 2.0 采用 **迟滞（Hysteresis）** 机制来调整验证者的有效余额（Effective Balance），以防止频繁的余额变化影响网络稳定性。

- **若余额下降 0.25 ETH 以下**，有效余额会 **减少 1 ETH**。
- **若余额上升 1.25 ETH 以上**，有效余额会 **增加 1 ETH**。
- 这些计算在 **每个纪元（Epoch）结束时** 进行。

这种机制的引入是为了避免验证者因短暂余额下降而长期损失奖励，提升参与者的收益稳定性。

---

## 3. Gwei 相关参数

### **最小存款金额（MIN_DEPOSIT_AMOUNT）**
- 设定了验证者最小存款金额，防止恶意用户提交微额存款。
- **当前值：1 Gwei（10⁹ Wei）**。

### **最大有效余额（MAX_EFFECTIVE_BALANCE）**
- 设定了验证者的最大有效余额，即 **32 ETH**。
- 任何超过 32 ETH 的余额 **不会增加额外的奖励**，但仍然可以作为存款以抵御罚没（Slashing）。

### **有效余额增量（EFFECTIVE_BALANCE_INCREMENT）**
- 有效余额按 1 Gwei 递增，计算时以 1 Gwei 为最小单位。

---

## 4. 以太坊 2.0 质押规则

以太坊 2.0 允许验证者 **补充存款（Top-up）**，以防止因惩罚或交易费用消耗导致余额降至 32 ETH 以下。不过，这一机制曾被用于 **前置交易攻击（Front-running Attack）**，攻击者可以篡改提款地址，截获质押奖励。

为了提高安全性，验证者的提款地址变更机制已做了调整，以防止这种攻击。

### 2025.02.18

## 以太坊 2.0 配置与规范学习

### 配置参数

#### GENESIS 设置

- **MIN_GENESIS_ACTIVE_VALIDATOR_COUNT**：这是启动 beacon 链所需的最小验证者数量，在启动时需要至少 16,384 个验证者存款才能开始出块。
- **MIN_GENESIS_TIME**：这是 beacon 链可以开始的最早时间，设置为 2020 年 12 月 1 日 12:00 UTC。此参数旨在防止某个恶意节点操控启动时间。
- **GENESIS_FORK_VERSION**：指定启动时使用的 fork 版本，默认为 `0x00000000`。
- **GENESIS_DELAY**：启动时的延迟，默认为 7 天，允许节点和开发者有足够时间准备。

#### 时间参数

- **SECONDS_PER_SLOT**：每个槽的时间长度，默认为 12 秒。该值受网络延迟的限制，较短的槽时间有助于提升链的处理能力，但也会增加同步问题。
- **SECONDS_PER_ETH1_BLOCK**：以太坊 1.0 的区块间隔，设定为 14 秒，用于与 ETH1 区块的同步。
- **MIN_VALIDATOR_WITHDRAWABILITY_DELAY**：验证者的提取延迟时间，设定为 256 个 epoch，大约 27 小时。

---

### Preset 设置

以太坊 2.0 中有两组预设配置：`mainnet` 和 `minimal`，分别用于生产环境和测试环境。`mainnet` 配置用于 beacon 链的实际运行，而 `minimal` 配置则用于轻量级的测试。

#### 关键参数

- **MAX_COMMITTEES_PER_SLOT**：每个槽最多可以有 64 个committee，每个个committee的验证者参与投票。
- **TARGET_COMMITTEE_SIZE**：委员会的目标大小为 128 个验证者，以确保足够的安全性。
- **MAX_VALIDATORS_PER_COMMITTEE**：每个委员会最多可以有 2048 个验证者，这决定了委员会数据结构的大小。
- **SHUFFLE_ROUND_COUNT**：决定委员会洗牌的轮数，默认为 90，确保验证者被随机分配到各个委员会。

#### Hysteresis 参数

- **HYSTERESIS_QUOTIENT**：控制有效余额变化的参数，防止因为小的余额波动导致奖励的频繁变化。
- **HYSTERESIS_DOWNWARD_MULTIPLIER**：当余额下降时，减少有效余额的乘数。
- **HYSTERESIS_UPWARD_MULTIPLIER**：当余额上升时，增加有效余额的乘数。

---

### 注释函数学习

今天继续学习了以太坊 2.0 规范中的一些重要函数，如整数平方根函数（`integer_squareroot`）

```python
def integer_squareroot(n: uint64) -> uint64:
    """
    返回最大的整数``x``，使得``x**2 <= n``。
    """
    x = n
    y = (x + 1) // 2
    while y < x:
        x = y
        y = (x + n // x) // 2
    return x
```

### 2025.02.20

## Beacon State Mutators 学习

今天的学习内容涉及 Beacon State 中关于验证者余额的增加和减少操作，以及验证者退出机制的相关函数。下面是详细的内容：

### increase_balance 函数

```python
def increase_balance(state: BeaconState, index: ValidatorIndex, delta: Gwei) -> None:
    """
    增加验证者在索引 ``index`` 处的余额 by ``delta``。
    """
    state.balances[index] += delta
```

### 2025.02.22

## 初始化状态（Initialise State）学习

今天学习了关于以太坊 beacon 链的状态初始化过程。主要包括通过以太坊 1.0 的块数据初始化 beacon 链的状态，并处理相关的存款和激活。下面是具体的学习内容。

### 引言

在以太坊 beacon 链的创世事件触发之前，以及每个以太坊的工作量证明块（Proof of Work Block），通过调用 `initialize_beacon_state_from_eth1()` 函数来初始化一个候选状态 `candidate_state`，该函数的参数如下：

- **eth1_block_hash**：以太坊工作量证明块的哈希值。
- **eth1_timestamp**：与 `eth1_block_hash` 对应的 Unix 时间戳。
- **deposits**：所有存款的序列，按照时间顺序排列，直到并包括 `eth1_block_hash` 对应的区块。

在以太坊工作量证明块的情况下，必须保证这些块至少经过 `SECONDS_PER_ETH1_BLOCK * ETH1_FOLLOW_DISTANCE` 秒后才会被考虑。这意味着，`eth1_timestamp + SECONDS_PER_ETH1_BLOCK * ETH1_FOLLOW_DISTANCE <= current_unix_time`。因此，如果 `GENESIS_DELAY < SECONDS_PER_ETH1_BLOCK * ETH1_FOLLOW_DISTANCE`，创世事件的时间可能会在时间/状态首次可用之前发生，应该配置合适的值以避免这种情况。

### 初始化状态（Initialisation）

初始化过程也称为创世事件。此函数仅用于纯 Capella 测试网和测试中初始化状态。

#### `initialize_beacon_state_from_eth1` 函数

```python
def initialize_beacon_state_from_eth1(eth1_block_hash: Hash32,
                                      eth1_timestamp: uint64,
                                      deposits: Sequence[Deposit],
                                      execution_payload_header: ExecutionPayloadHeader=ExecutionPayloadHeader()
                                      ) -> BeaconState:
    fork = Fork(
        previous_version=CAPELLA_FORK_VERSION,  # [Modified in Capella] for testing only
        current_version=CAPELLA_FORK_VERSION,  # [Modified in Capella]
        epoch=GENESIS_EPOCH,
    )
    state = BeaconState(
        genesis_time=eth1_timestamp + GENESIS_DELAY,
        fork=fork,
        eth1_data=Eth1Data(block_hash=eth1_block_hash, deposit_count=uint64(len(deposits))),
        latest_block_header=BeaconBlockHeader(body_root=hash_tree_root(BeaconBlockBody())),
        randao_mixes=[eth1_block_hash] * EPOCHS_PER_HISTORICAL_VECTOR,  # Seed RANDAO with Eth1 entropy
    )

    # Process deposits
    leaves = list(map(lambda deposit: deposit.data, deposits))
    for index, deposit in enumerate(deposits):
        deposit_data_list = List[DepositData, 2**DEPOSIT_CONTRACT_TREE_DEPTH](*leaves[:index + 1])
        state.eth1_data.deposit_root = hash_tree_root(deposit_data_list)
        process_deposit(state, deposit)

    # Process activations
    for index, validator in enumerate(state.validators):
        balance = state.balances[index]
        validator.effective_balance = min(balance - balance % EFFECTIVE_BALANCE_INCREMENT, MAX_EFFECTIVE_BALANCE)
        if validator.effective_balance == MAX_EFFECTIVE_BALANCE:
            validator.activation_eligibility_epoch = GENESIS_EPOCH
            validator.activation_epoch = GENESIS_EPOCH

    # Set genesis validators root for domain separation and chain versioning
    state.genesis_validators_root = hash_tree_root(state.validators)

    # Fill in sync committees
    # Note: A duplicate committee is assigned for the current and next committee at genesis
    state.current_sync_committee = get_next_sync_committee(state)
    state.next_sync_committee = get_next_sync_committee(state)

    # Initialize the execution payload header
    state.latest_execution_payload_header = execution_payload_header

    return state
```




<!-- Content_END -->
