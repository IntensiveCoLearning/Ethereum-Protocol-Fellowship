# Jeason Zhang

1. 自我介绍：大家好，我是 Jeason Zhang，以太坊爱好者，全栈工程师，独立开发者，很开心参加今年的 EPF 残酷共学。
2. 你认为你会完成本次残酷学习吗？会的！

## Notes

<!-- Content_START -->

### 2025.02.06

今天是残酷共学的第一天，参加了 chloe 主持的第一周周会，会后看了一下[ epf wiki ](https://epf.wiki/#/eps/week1)中的内容，并用 deepseek - R1 总结了一下内容如下：

#### **EPF WIKI WEEK1**

#### **I. 核心学习目标**

**主题**：以太坊协议基础与研发生态全景
**目标**：理解以太坊设计哲学、技术架构、开发流程及社区协作模式。

------

#### **II. 核心学习模块**

##### **1. 历史与哲学基础**

- **UNIX哲学**
  - **核心理念**：模块化、简洁性、协作开发
  - 推荐资源
    - [UNIX纪录片](https://www.youtube.com/watch?v=tc4ROCJYbm0)（贝尔实验室文化）
    - [UNIX历史解析](https://www.theregister.com/2024/02/16/what_is_unix/)
- **自由软件运动**
  - **关键人物**：Richard Stallman（GNU项目）
  - **核心原则**：用户自由（运行、研究、修改、分发）
  - 必读材料
    - [自由软件定义](https://www.gnu.org/philosophy/free-sw.html)
    - 《大教堂与集市》（[在线版](http://www.catb.org/~esr/writings/cathedral-bazaar/)）
- **密码朋克与加密无政府主义**
  - **核心思想**：去中心化、隐私保护、密码学驱动自治
  - 经典文献
    - [密码朋克宣言](https://activism.net/cypherpunk/manifesto.html)
    - [加密无政府主义宣言](https://activism.net/cypherpunk/crypto-anarchy.html)
    - [网络空间独立宣言](https://www.eff.org/cyberspace-independence)

------

##### **2. 以太坊协议设计**

- **设计原则**
  - **五大核心**：简洁性、通用性、模块化、非歧视性、敏捷性
  - 技术文档
    - [以太坊黄皮书](https://ethereum.github.io/yellowpaper/)（数学化协议定义）
    - [执行层规范](https://github.com/ethereum/execution-specs)（Python实现）
- **网络架构**
  - 分层结构
    - **执行层（EL）**：处理交易与智能合约（EVM）
    - **共识层（CL）**：PoS机制与区块确认
  - **节点类型**：全节点、轻节点、归档节点
  - 扩展阅读
    - [节点架构文档](https://ethereum.org/developers/docs/nodes-and-clients/)
    - [路线图解析](https://ethereum.org/roadmap)

------

##### **3. 实现与开发**

- 客户端多样性
  - **执行层客户端**：Geth、Nethermind、Besu
  - **共识层客户端**：Lighthouse、Prysm、Teku
  - **开发语言**：Go、Rust、Java、C#等
  - 资源
    - [客户端列表](https://ethereum.org/developers/docs/nodes-and-clients/#execution-clients)
    - [EPF项目案例](https://github.com/eth-protocol-fellows/cohort-four)

------

##### **4. 测试与安全**

- **测试工具链**
  - 核心仓库
    - [通用测试集](https://github.com/ethereum/tests)
    - [Retesteth工具](https://github.com/ethereum/retesteth)（状态转换测试）
    - [Hive测试框架](https://github.com/ethereum/hive)（多客户端仿真）
  - **测试类型**：单元测试、模糊测试、影子分叉
- **安全实践**
  - **漏洞赏金计划**：通过[HackerOne](https://hackerone.com/ethereum)提交
  - **代码审计**：形式化验证（如[KEVM](https://github.com/kframework/evm-semantics)）

------

##### **5. 社区协作机制**

- **协调流程**
  - 核心会议
    - **ACD会议**（All Core Devs）：双周例会
    - **PM仓库**（[ethereum/pm](https://github.com/ethereum/pm)）记录议程
  - **提案流程**：EIP（[EIPs仓库](https://github.com/ethereum/EIPs)）
- **讨论平台**：
  - [EthResearch论坛](https://ethresear.ch/)（技术研究）
  - [Ethereum Magicians](https://ethereum-magicians.org/)（提案讨论）
  - **R&D Discord**（需邀请）

------

#### **III. 学习路径建议**

##### **1. 入门阶段**

- **视频学习**：
  - [Mario Havel讲座](https://streameth.org/ethereum-protocol-101)（以太坊协议基础）
  - [Richard Stallman演讲](https://www.youtube.com/watch?v=Ag1AKIl_2GM)（自由软件理念）
- **基础阅读**：
  - [以太坊30分钟入门](https://ethereum.org/learn/)
  - [绝对以太坊精要](https://www.amazon.com/Absolute-Essentials-Ethereum-Matt-Garnett/dp/1119893410)（新书推荐）

------

##### **2. 技术深化**

- **实践任务**：
  - **运行测试网节点**：使用Geth + Lighthouse组合
  - **参与测试**：通过[Hive](https://github.com/ethereum/hive)提交客户端兼容性报告
- **代码研读**：
  - 分析[执行层规范](https://github.com/ethereum/execution-specs)中的状态转换逻辑
  - 研究[EIP-1559](https://eips.ethereum.org/EIPS/eip-1559)实现代码

------

##### **3. 社区参与**

- **跟踪开发动态**：
  - 订阅[ACD会议纪要](https://github.com/ethereum/pm)
  - 加入[EPF Discord](https://discord.gg/eth-protocol-fellows)参与讨论
- **贡献方式**：
  - 提交EIP改进提案
  - 参与[ETHGlobal黑客松](https://ethglobal.com/)

------

#### **IV. 扩展资源**

- **书籍推荐**：
  - 《The Infinite Machine》（以太坊早期史）
  - 《Mastering Ethereum》（技术细节解析，需注意版本）
- **高级学习**：
  - [Devcon演讲存档](https://archive.devcon.org/)（技术深度内容）
  - [形式化验证案例](https://github.com/ethereum/aleth)（Aleth项目）

------

#### **V. 学习评估**

- 自测工具
  - [以太坊基础知识测验](https://ethereum.org/quizzes)
  - 编写简单智能合约并通过[执行层测试](https://github.com/ethereum/execution-spec-tests)验证

### 2024.02.07

#### **EPF WIKI WEEK2**

#### **I. 核心学习目标**

**主题**: 以太坊执行层（Execution Layer）深度解析
**目标**: 掌握执行层节点架构、状态转换机制、EVM运行原理及网络通信协议。

------

#### **II. 课程大纲重点**

##### **1. 执行层节点架构**

- **区块验证（Block Validation）**：
  - 处理状态转换（State Transition），将交易结果记录到**状态树（Merkle Patricia Trie）**
  - 维护动态机制更新：EIP-1559基础费用、EIP-4844 Blob Gas、信标链提款等
  - 提供**快速同步机制**（Snap Sync）帮助新节点快速接入网络
- **区块构建（Block Building）**：
  - 基于P2P交易池（Tx Pool）构建新区块
  - 交易广播与验证的双向流程

##### **2. 状态转换函数**

- 区块头验证：
  - 校验**默克尔根**（交易根、状态根、收据根）
  - 验证Gas限制与时间戳合法性
- 区块验证代码实践：
  - 分析[go-ethereum代码库](https://github.com/ethereum/go-ethereum)中`core/state_processor.go`的`Process()`函数

##### **3. EVM运行机制**

- 栈式虚拟机原理：
  - 操作码分类解析：
    - 堆栈操作码（如`PUSH`, `POP`）
    - 内存操作码（如`MLOAD`, `MSTORE`）
    - 系统级操作（如`CALL`, `DELEGATECALL`）
- 实战工具推荐：
  - [evm.codes](https://www.evm.codes/)：交互式EVM操作码解析工具
  - [ethervm.io](https://ethervm.io/)：EVM指令集速查表

##### **4. P2P网络协议**

- 三大核心功能：
  - 历史区块数据传输
  - 未确认交易（Pending Transactions）广播
  - 状态数据同步
- Snap Sync技术：
  - **阶段一**：下载快照数据块（Snapshot Tiles）
  - **阶段二**：状态修复（State Healing）

##### **5. JSON-RPC接口**

- 设计目标：
  - 统一所有客户端的API标准，实现工具链无缝集成
  - 目前接近实现但仍有细微差异
- 关键RPC方法：
  - `eth_getBlockByNumber`
  - `eth_sendRawTransaction`
  - `eth_call`

------

#### **III. 核心学习资源**

##### **必读材料**：

- [执行层规范](https://github.com/ethereum/execution-specs)（Python实现）
- [ETH2术语更新说明](https://blog.ethereum.org/2022/01/24/the-great-eth2-renaming)
- [合并对应用层的影响](https://blog.ethereum.org/2021/11/29/how-the-merge-impacts-app-layer)

##### **进阶工具**：

- [Engine API可视化指南](https://hackmd.io/@danielrachi/engine_api)（Daniel Ramirez）
- [Lightclient开发环境配置](https://github.com/lightclient/dotfiles)

##### **代码研究**：

- 核心代码库：
  - [go-ethereum](https://github.com/ethereum/go-ethereum)
  - [devp2p协议](https://github.com/ethereum/devp2p)
- 执行层API规范：
  - [execution-apis](https://github.com/ethereum/execution-apis)

------

#### **IV. 学习实践建议**

1. **代码调试**：在本地运行Geth节点，观察`state_processor.go`的区块处理流程
2. **网络模拟**：使用[devp2p工具包](https://github.com/ethereum/devp2p)模拟P2P交易广播
3. **RPC实验**：通过Postman调用JSON-RPC接口获取链上数据

### 2025.02.09

#### **EPF WIKI WEEK3**

#### **I. 核心学习目标**

**主题**: 以太坊共识层（Consensus Layer）技术解析
**目标**: 掌握权益证明（PoS）机制、Gasper协议架构及信标链安全模型。

------

#### **II. 课程大纲重点**

##### **1. 共识机制基础**

- 拜占庭容错（BFT）：
  - 区块链通过分布式网络实现数字稀缺性，需解决节点作恶问题
  - 比特币通过工作量证明（PoW）首次实现BFT
- PoS机制创新：
  - 以太坊转向权益证明，使用内生经济信号（质押ETH）实现女巫攻击防护
  - 通过**罚没（Slashing）**机制惩罚拜占庭行为

##### **2. Gasper协议架构**

- 混合共识机制：
  - **LMD-GHOST分叉选择规则**：基于最新消息（Latest Message Driven）确定主链
  - **Casper FFG**：负责最终性确认（Finality），确保链活性（Liveness）
- 关键特性：
  - 每32个区块（Epoch）进行最终性确认
  - 支持动态验证者集合调整

##### **3. 信标链安全模型**

- 密码经济学保障：
  - 验证者需质押32 ETH，作恶将面临罚没
  - 罚没条件：双重签名、违反分叉规则等
- 抗攻击能力：
  - 1/3质押量攻击可导致链暂停
  - 2/3质押量攻击可导致链重组

------

#### **III. 核心学习资源**

##### **必读材料**：

- [Gasper协议白皮书](https://arxiv.org/pdf/2003.03052.pdf)
- [LMD-GHOST优化解析](https://medium.com/@aditya.asgaonkar/bitwise-lmd-ghost-an-efficient-cbc-casper-fork-choice-rule-6db924e57d1f)
- [Eth2规范注释版](https://eth2book.info/)（技术细节宝典）

##### **深度分析**：

- [Slashing场景详解](https://dankradfeist.de/ethereum/2022/03/24/run-the-majority-client-at-your-own-peril.html)（Dankrad Feist）
- [信标链设计反思](https://www.youtube.com/watch?v=10Ym34y3Eoo)（Justin Drake演讲）

------

#### **IV. 实践建议**

1. **客户端运行**：

   - 组合运行执行层（如Geth）与共识层客户端（如Lighthouse）
   - 观察日志中的`attestation`（见证）与`proposal`（区块提议）流程

2. **时隙分析**：

   - 研究

     时隙解剖视频

     ，理解12秒时隙内的操作序列：

     - 区块提议 → 见证打包 → 最终性投票

3. **安全实验**：

   - 在测试网模拟双重签名场景，观察罚没机制触发过程

------

#### **V. 关键概念对照表**

| 英文术语       | 中文解释   |
| -------------- | ---------- |
| Finality       | 最终性     |
| Justification  | 合理性证明 |
| Checkpoint     | 检查点     |
| Attestation    | 见证       |
| Sync Committee | 同步委员会 |

### 2025.02.10

#### **EPF WIKI WEEK4**

#### **I. 核心学习目标**

**主题**: 以太坊测试框架与安全实践
**目标**: 掌握以太坊核心测试工具链、安全漏洞发现方法及网络升级测试流程。

------

#### **II. 课程大纲重点**

##### **1. 核心测试工具链**

- **执行层测试套件**：
  - **[ethereum/tests](https://github.com/ethereum/tests)**: 标准状态转换测试集
  - **[execution-spec-tests](https://github.com/ethereum/execution-spec-tests)**: 执行层规范验证测试
  - **[retesteth](https://github.com/ethereum/retesteth)**: 动态测试生成与执行工具
- **网络仿真工具**：
  - **[Hive](https://github.com/ethereum/hive)**: 多客户端测试框架，支持创建定制化测试网
  - **[Kurtosis](https://github.com/kurtosis-tech/kurtosis)**: 分布式测试环境编排平台
- **模糊测试工具**：
  - **[FuzzyVM](https://github.com/MariusVanDerWijden/FuzzyVM)**: EVM字节码模糊测试器
  - **[tx-fuzz](https://github.com/MariusVanDerWijden/tx-fuzz)**: 交易生成与异常检测工具

##### **2. 安全测试实践**

- 合并测试经验：
  - 通过影子分叉（Shadow Fork）模拟主网环境
  - 使用**[eth_tools](https://github.com/marioevz/eth_tools)**监控网络异常
- 漏洞挖掘案例：
  - 共识层分叉规则漏洞（如LMD-GHOST边缘场景）
  - 客户端同步协议缺陷（如LibP2P消息处理）

##### **3. 测试方法论**

- 分层测试策略：
  - **单元测试**：验证单个功能模块
  - **集成测试**：多客户端交互验证
  - **压力测试**：高负载场景模拟（如Dencun升级的blob处理）
- 自动化流水线：
  - 持续集成（CI）触发测试套件
  - 测试结果可视化与回归分析

------

#### **III. 关键学习资源**

##### **必读材料**：

- [以太坊测试文档](https://ethereum-tests.readthedocs.io/)：测试类型与执行指南
- [执行层规范测试说明](https://ethereum.github.io/execution-spec-tests/)：测试用例设计原则

##### **深度实践**：

- **[RPC测试生成器](https://github.com/lightclient/rpctestgen)**：自动化生成JSON-RPC接口测试
- **[Dencun测试教程](https://www.youtube.com/watch?v=88tZticGbTo)**：分片blob处理测试案例

##### **经典案例研究**：

- [The Merge测试回顾](https://archive.devcon.org/archive/watch/6/quest-for-the-best-tests-a-retrospective-on-testingthemerge/)（Devcon6演讲）
- [Layer1共识漏洞挖掘](https://archive.devcon.org/archive/watch/6/killing-eth-finding-consensus-issues-on-layer-1/)（Marius Van Der Wijden）

------

#### **IV. 实践建议**

1. 本地测试环境搭建：

   ```bash
   # 使用Hive创建多客户端测试网
   hive --client=geth,lighthouse --sim=eth2/merge
   ```

2. 模糊测试执行：

   ```bash
   # 运行FuzzyVM检测EVM异常
   go run ./cmd/fuzzy --test=evm_opcodes
   ```

3. 自定义测试开发：

   - 在`ethereum/tests`中新增状态转换测试用例
   - 通过`retesteth`验证客户端兼容性

------

#### **V. 测试类型对照表**

| 测试类型     | 工具示例   | 检测目标           |
| ------------ | ---------- | ------------------ |
| 状态转换测试 | retesteth  | 区块处理逻辑正确性 |
| 网络协议测试 | Hive       | P2P消息兼容性      |
| 模糊测试     | FuzzyVM    | EVM执行边界条件    |
| RPC接口测试  | rpctestgen | JSON-RPC规范符合性 |

------

通过本课程的系统学习，开发者将掌握以太坊核心测试框架的运作机制，具备参与网络升级测试和安全审计的能力。建议从[标准测试集](https://github.com/ethereum/tests)入手，逐步深入定制化测试开发。

### 2025.02.11

##### **EPF WIKI WEEK5**

#### **I. 核心学习目标**

**主题**: 以太坊研究生态与路线图演进
**目标**: 掌握以太坊六大发展阶段（Merge/Surge/Scourge/Verge/Purge/Splurge）的技术规划及当前研究热点。

------

#### **II. 以太坊路线图解析**

##### **1. 六大发展阶段**

| 阶段        | 核心目标         | 关键技术                                                     |
| ----------- | ---------------- | ------------------------------------------------------------ |
| **Merge**   | PoS共识完善      | 单槽最终性（SSF）、秘密领导者选举（SLE）、提款机制优化       |
| **Surge**   | 扩容与数据可用性 | EIP-4844（Blob交易）、数据可用性采样（DAS）、ZK Rollup互操作性 |
| **Scourge** | MEV治理与抗审查  | ePBS（Enshrined PBS）、MEV销毁、质押上限机制                 |
| **Verge**   | 状态验证效率提升 | Verkle树、SNARK化（信标链状态转换、EVM验证）                 |
| **Purge**   | 协议简化         | EIP-4444（历史数据修剪）、状态过期机制                       |
| **Splurge** | 用户体验优化     | 账户抽象（ERC-4337）、EIP-1559最终形态、深度密码学整合       |

------

#### **III. 当前研究热点**

##### **1. 密码学前沿**

- **KZG多项式承诺**：用于Blob数据验证（[KZG仪式](https://scroll.io/blog/kzg)）
- **Verkle树结构**：替代Merkle Patricia Trie，提升状态证明效率（[Vitalik解析](https://vitalik.eth.limo/general/2021/06/18/verkle.html)）

##### **2. 扩容技术**

- **数据可用性采样（DAS）**：通过随机抽样验证数据可用性
- **跨Rollup互操作**：标准化跨链消息协议

##### **3. 抗MEV机制**

- **包含列表（Inclusion Lists）**：防止交易审查
- **MEV-Burn**：通过协议内拍卖销毁MEV收益

------

#### **IV. 关键升级进展**

##### **1. 近期里程碑**

- **Dencun升级**：EIP-4844实施，降低Layer2成本
- **Pectra升级**：Verkle树预编译合约部署

##### **2. 开发者工具**

- **Helios轻客户端**：Rust实现的快速同步客户端（[构建指南](https://a16zcrypto.com/posts/article/building-helios-ethereum-light-client/)）
- **EVM对象格式（EOF）**：优化合约代码存储结构

------

#### **V. 学习资源推荐**

##### **必读材料**

- [以太坊终极形态](https://vitalik.eth.limo/general/2021/12/06/endgame.html)（Vitalik长文）
- [Blob空间经济学](https://domothy.com/blobspace/)（Domothy分析）
- [以太坊数据结构演进](https://arxiv.org/pdf/2108.05513.pdf)（学术论文）

##### **实践指南**

- [EthRoadmap.com](https://ethroadmap.com/)：交互式路线图可视化
- [执行票据提案](https://ethresear.ch/t/execution-tickets/17944)：参与协议改进讨论

------

#### **VI. 技术术语对照**

| 英文术语                   | 中文解释                |
| -------------------------- | ----------------------- |
| Single Slot Finality       | 单槽最终性              |
| Data Availability Sampling | 数据可用性采样          |
| Enshrined PBS              | 协议内提议者-构建者分离 |
| Verkle Proofs              | Verkle树证明            |
| MEV Burn                   | MEV销毁机制             |

------

通过本课程的系统学习，开发者可全面把握以太坊技术演进的宏观框架，深入参与核心协议研究。建议结合[Ethresear.ch论坛](https://ethresear.ch/)跟踪最新提案，通过节点工作坊实践客户端运维。

### 2025.02.12

##### **EPF WIKI Node Workshop**

#### **I. 核心学习目标**

**主题**: 以太坊客户端实践操作
**目标**: 掌握执行层（EL）与共识层（CL）客户端的部署、配置及运维技能。

------

#### **II. 环境准备**

##### **1. 系统要求**

- **推荐系统**: Debian 12（支持Ubuntu/macOS，建议使用虚拟机统一环境）

- **硬件配置**: 测试网节点无需高性能硬件（2核CPU/4GB RAM/50GB存储）

- 基础工具安装:

  ```bash
  sudo apt update && sudo apt install -y curl git gpg docker.io build-essential
  ```

##### **2. 前置知识**

- **客户端架构**: 复习[节点架构文档](https://ethereum.org/en/developers/docs/nodes-and-clients/node-architecture/)
- **Linux基础**: 掌握[基础命令行操作](https://ubuntu.com/tutorials/command-line-for-beginners)

------

#### **III. 客户端部署流程**

##### **1. 客户端选择与获取**

- **推荐组合**: Geth（EL） + Lighthouse（CL）

- 二进制验证（以Geth为例）:

  ```bash
  # 下载签名文件
  curl -O https://geth.ethereum.org/geth-linux-amd64-1.13.0-6c74b4e6.sig
  # 验证签名
  gpg --verify geth-linux-amd64-1.13.0-6c74b4e6.sig
  ```

##### **2. Docker快速部署**

```bash
# 启动Geth测试网节点
docker run -d -p 8545:8545 -v /data/geth:/root/.ethereum \
  ethereum/client-go --goerli --http --http.addr 0.0.0.0

# 启动Lighthouse共识客户端
docker run -d -p 9000:9000 -p 9001:9001 -v /data/lighthouse:/root/.lighthouse \
  sigp/lighthouse lighthouse beacon --network holesky
```

##### **3. 测试网配置**

- Holesky测试网:

  ```bash
  geth --holesky --syncmode snap --http
  lighthouse beacon --network holesky
  ```

- Ephemery自定义创世块:

  ```bash
  geth init --datadir ./ephemery ephemery-genesis.json
  ```

------

#### **IV. 节点运维实践**

##### **1. RPC接口使用**

- 基础访问:

  ```bash
  curl -X POST -H "Content-Type: application/json" \
    --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' \
    http://localhost:8545
  ```

- 控制台交互:

  ```bash
  geth attach http://localhost:8545
  > eth.syncing
  ```

##### **2. 验证者管理**

- 质押存款:

  ```bash
  lighthouse account validator deposit \
    --network holesky \
    --keystore ./validator_keys \
    --deposit-value 32
  ```

##### **3. 系统服务配置**

- systemd服务文件示例（Geth）:

  ```ini
  [Unit]
  Description=Geth Execution Client
  After=network.target
  
  [Service]
  ExecStart=/usr/bin/geth --http --syncmode snap --cache 2048
  Restart=always
  User=geth
  
  [Install]
  WantedBy=multi-user.target
  ```

------

#### **V. 进阶实践建议**

##### **1. 节点监控**

- Prometheus+Grafana方案:

  ```bash
  # 安装Prometheus
  docker run -d -p 9090:9090 -v /prometheus-data:/prometheus prom/prometheus
  # 配置Grafana仪表盘（参考Coincashew指南）
  ```

##### **2. 网络诊断**

- P2P网络分析:

  ```bash
  # 使用devp2p工具检查节点连接
  devp2p discv5 nodes -bootnodes enr://...
  ```

##### **3. 客户端切换实验**

- 执行层切换

  （Geth → Erigon）:

  ```bash
  erigon --chain holesky --datadir ./erigon-data --http
  ```

- 共识层切换

  （Lighthouse → Nimbus）:

  ```bash
  nimbus_beacon_node --network=holesky --web3-url=http://localhost:8545
  ```

------

#### **VI. 关键资源推荐**

- **节点维护指南**: [EthStaker Holesky指南](https://github.com/eth-educators/ethstaker-guides)
- **验证者监控**: [Grafana仪表板配置](https://www.coincashew.com/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet/part-i-installation/monitoring-your-validator-with-grafana-and-prometheus)
- **故障排查**: [合并后节点FAQ](https://notes.ethereum.org/@launchpad/node-faq-merge)

------

通过本工作坊的系统实践，开发者将具备独立部署和维护以太坊全节点的能力，为参与网络验证或协议开发奠定基础。建议从测试网开始，逐步过渡到主网节点运维。

### 2025.02.13

##### **EPF WIKI WEEK6: Consensus and Execution spec**

#### **I. 核心学习目标**

**主题**: 共识层与执行层技术规范深度解析
**目标**: 掌握规范实现原理，参与协议改进提案（EIP）开发。

------

#### **II. 课程大纲重点**

##### **1. 共识层规范（CL Specs）**

- Gasper协议实现：
  - 结合LMD-GHOST分叉选择规则与Casper FFG最终性机制
  - 状态转换逻辑：见证打包、检查点证明、验证者奖惩
- Python参考实现：
  - [共识层规范代码库](https://github.com/ethereum/consensus-specs)
  - 测试框架：通过`pytest`验证区块生成与状态转换
- 关键测试场景：
  - 分叉场景模拟（7节点网络测试）
  - 罚没条件触发验证（双重签名检测）

##### **2. 执行层规范（EELS）**

- EVM对象格式（EOF）：
  - 分离代码与数据段，优化合约存储结构
  - 支持版本化合约部署（向后兼容）
- 操作码扩展实践：
  - 在[execution-specs](https://github.com/ethereum/execution-specs)中添加自定义操作码
  - 生成一致性测试向量（JSON测试用例）
- 黄皮书对照：
  - 状态转换函数的数学形式化验证
  - Gas计算模型与预编译合约实现

------

#### **III. 关键学习资源**

##### **必读材料**：

- [EELS规范解析](https://blog.ethereum.org/2023/08/29/eel-spec)：执行层演进逻辑
- [Vitalik注释版规范](https://github.com/ethereum/annotated-spec)：协议设计思想解读

##### **实践指南**：

- 共识层开发：

  ```python
  # 测试分叉场景
  def test_multiple_forks():
      genesis_state = initialize_beacon_state()
      fork1_blocks = generate_alt_chain(genesis_state, length=3)
      fork2_blocks = generate_alt_chain(genesis_state, length=5)
      assert get_head(fork1_blocks) != get_head(fork2_blocks)
  ```

- 执行层扩展：

  - 修改`src/ethereum/[frontier|homestead]/vm/opcodes.py`
  - 在`tests/[frontier|homestead]/test_opcodes.py`添加测试

------

#### **IV. 技术术语对照**

| 英文术语             | 中文解释               |
| -------------------- | ---------------------- |
| LMD-GHOST            | 最新消息驱动的最重子树 |
| Casper FFG           | 友好最终性小工具       |
| EOF                  | EVM对象格式            |
| Precompiled Contract | 预编译合约             |

------

#### **V. 实践建议**

1. **共识层实验**：
   - 修改`beacon-chain.md`中的`process_attestation`逻辑
   - 运行`make test`验证状态转换正确性
2. **执行层扩展**：
   - 添加`OP_CALLDATA`操作码实现数据直接访问
   - 生成并提交EIP草案至[EIPs仓库](https://github.com/ethereum/EIPs)

------

通过本课程的系统学习，开发者将具备直接参与以太坊核心协议开发的能力。建议结合[Eth2 Book](https://eth2book.info)深化共识层知识，通过[黄皮书教程](https://ethereum.org/en/developers/tutorials/yellow-paper-evm/)理解EVM底层原理。

### 2025.02.15

#### **EPF WIKI WEEK6: Study Group Week 6 | Sharding and DAS**

#### **I. 核心学习目标**

**主题**: 分片技术与数据可用性采样（DAS）
**目标**: 理解Danksharding架构与数据可用性保障机制，掌握扩容路线图核心技术。

------

#### **II. 课程大纲重点**

##### **1. 扩容演进史**

- **原始分片方案**：64个分片链并行处理交易
- **Danksharding优化**：
  - 统一结算层与数据可用性层
  - 通过EIP-4844（Proto-Danksharding）过渡
  - 引入Blob交易类型降低Layer2成本

##### **2. 数据可用性采样（DAS）**

- **核心组件**：
  - **KZG多项式承诺**：通过[KZG仪式](https://scroll.io/blog/kzg)实现高效数据验证
  - **2D Reed-Solomon编码**：将数据扩展为二维矩阵，确保部分数据丢失时可恢复
  - **随机抽样验证**：轻节点通过随机抽样（约30次）确保数据可用性（99.9%置信度）
- **抗审查机制**：
  - **包含列表（Inclusion Lists）**：强制区块包含特定交易
  - **数据可用性委员会（DAC）**：临时过渡方案，最终由协议内机制取代

##### **3. Danksharding架构**

- **角色分离**：
  - **区块提议者**：负责排序交易
  - **构建者**：生成包含Blob的区块
  - **证明者**：验证数据可用性
- **经济模型**：
  - Blob存储费用动态调整（类似EIP-1559）
  - MEV-Burn机制销毁部分MEV收益

------

#### **III. 关键学习资源**

##### **基础理论**：

- [数据可用性问题解析](https://www.youtube.com/watch?v=OJT_fR7wexw)（技术讲座）
- [Danksharding设计提案](https://hackmd.io/@vbuterin/das)（Vitalik Buterin）

##### **深度分析**：

- [DAS设计选择](https://www.youtube.com/watch?v=Al7Jns8bCO4)（Dankrad Feist演讲）
- [欺诈证明与数据可用性证明](https://arxiv.org/abs/1809.09044)（学术论文）

##### **实践工具**：

- [Danksharding测试网工具链](https://github.com/ethereum/danksharding)
- [数据可用性模拟器](https://github.com/ethereum/das-simulator)

------

#### **IV. 技术术语对照**

| 英文术语                    | 中文解释                 |
| --------------------------- | ------------------------ |
| Data Availability Sampling  | 数据可用性采样           |
| KZG Commitment              | KZG多项式承诺            |
| Reed-Solomon Erasure Coding | 里德-所罗门纠删码        |
| Proto-Danksharding          | 原始Danksharding过渡方案 |
| Blob Transaction            | Blob交易类型             |

------

##### **V. 实践建议**

1. **DAS模拟实验**：

   ```python
   # 使用das-simulator进行数据可用性验证
   from das import DataAvailability
   blob = DataAvailability.generate_blob()
   samples = blob.sample_random_indices(30)
   assert blob.verify_samples(samples)
   ```

2. **KZG仪式参与**：

   - 通过[KZG仪式客户端](https://github.com/ethereum/kzg-ceremony)贡献随机数
   - 验证多项式承诺生成过程

3. **扩容影响分析**：

   - 测算Blob交易对Gas费的影响
   - 评估Layer2在Danksharding下的TPS提升

------

通过本课程的系统学习，研究者将深入理解以太坊未来扩容方向，掌握数据可用性核心技术。建议结合[Devcon研讨会资料](https://www.youtube.com/watch?v=8L2C6RDMV9Q)跟进最新进展，参与[Ethresear.ch论坛](https://ethresear.ch/)讨论协议改进提案。

### 2025.02.16

#### **EPF WIKI Week 7 | Execution client architecture**

#### **I. 核心学习目标**

**主题**: 执行层客户端架构与Reth设计解析
**目标**: 掌握现代执行层客户端设计理念，深入理解Reth代码架构。

------

#### **II. 课程大纲重点**

##### **1. Reth客户端概述**

- **开发语言**：Rust（兼顾性能与安全性）
- 核心优势：
  - 模块化设计，支持插件扩展
  - 基于Actor模型的异步任务处理
  - 状态树存储优化（替代传统Merkle Patricia Trie）

##### **2. 架构设计亮点**

- 分层架构：
  - **网络层**：基于LibP2P实现高效节点通信
  - **同步引擎**：支持快照同步与增量同步混合模式
  - **执行环境**：隔离的EVM运行时（WASM兼容）
- 创新特性：
  - 基于RocksDB的列式存储优化
  - 交易池优先级队列与抗DoS机制
  - 轻客户端模式下的状态证明生成

##### **3. 代码结构解析**

- 核心模块：

  - `reth-db`：数据库抽象层（支持多后端存储）
  - `reth-network`：P2P网络协议实现
  - `reth-executor`：EVM执行引擎（兼容EOF规范）

- 示例分析：

  ```rust
  // 区块处理流程
  async fn process_block(block: Block) -> Result<(), Error> {
      let state = State::new();
      execute_transactions(block.transactions, &state).await?;
      persist_state(state).await?;
      Ok(())
  }
  ```

##### **4. 性能优化策略**

- **并行处理**：交易执行与状态更新解耦
- **缓存机制**：热数据内存缓存（LRU策略）
- **批处理写入**：减少数据库I/O操作

------

#### **III. 关键学习资源**

##### **必读材料**：

- [Reth官方文档](https://paradigmxyz.github.io/reth/)：架构设计与API参考
- [Erigon设计理念](https://github.com/ledgerwatch/erigon)：Geth分叉项目的创新实践

##### **深度解析**：

- [Reth技术解析](https://www.youtube.com/watch?v=pxhq7YrySRM)（Dragan演讲）
- [Rust异步编程模型](https://tokio.rs/)：理解Actor模型实现基础

------

#### **IV. 实践建议**

1. **环境搭建**：

   ```bash
   # 克隆Reth代码库
   git clone https://github.com/paradigmxyz/reth
   # 编译调试版本
   cargo build --features "jemalloc,backend-mdbx"
   ```

2. **调试实践**：

   ```bash
   # 启用交易池调试日志
   RUST_LOG=debug reth --debug.txpool
   # 观察区块同步过程
   RUST_LOG=info reth --sync-mode snap
   ```

3. **自定义模块开发**：

   - 实现`reth-consensus`模块的自定义分叉规则
   - 扩展`reth-rpc`添加新的JSON-RPC方法

------

##### **V. 技术术语对照**

| 英文术语         | 中文解释   |
| ---------------- | ---------- |
| Actor Model      | 参与者模型 |
| Columnar Storage | 列式存储   |
| State Trie       | 状态树     |
| Snapshot Sync    | 快照同步   |

------

通过本课程的系统学习，开发者将掌握现代以太坊客户端的架构设计精髓，具备参与Reth等新一代客户端开发的能力。建议结合[Erigon代码库](https://github.com/ledgerwatch/erigon)对比学习传统与创新设计差异，通过[Tokio文档](https://tokio.rs/)深化异步编程理解。

<!-- Content_END -->
