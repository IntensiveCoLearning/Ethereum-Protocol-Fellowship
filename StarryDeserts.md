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

# {StarryDeserts}

1. 自我介绍

   第三次参加残酷共学，全靠这个学以太坊生态的知识了，我初学就直接干move了，对以太坊生态的很多具体细节都不够了解，希望在这里能够学到很多新知识，同时也增长下见识。

2. 你认为你会完成本次残酷学习吗？

   完全没问题！

## Notes

<!-- Content_START -->

### 2025.02.06

#### Protocol Design Philosophy（one day）

------

##### **核心原则**

**简洁性 (Simplicity)**

- 以太坊协议最初以简化设计为目标，强调普通开发者应能理解并实现整个协议。随着发展，模块化设计（如**`Proto-Danksharding`**）帮助维持了简洁性，复杂功能被封装为独立模块（如Dagger、Patricia树）。

**通用性 (Universality)**

- 以太坊不预设特定功能，而是通过**EVM**提供图灵完备的虚拟机，允许开发者构建任意数学定义的智能合约。目标是成为无需信任的去中心化应用平台。

**模块化 (Modularity)**

- 协议设计强调组件解耦，使得单个模块的修改不影响整体系统。例如，存储结构（**`LevelDB`**）、序列化工具（**`SSZ`**）等作为独立库存在，便于复用和升级。

**非歧视性 (Non-discriminant)**

- 协议不限制特定用途，仅通过交易费用机制防止滥用（如无限循环脚本需持续付费）。体现了FOSS（自由开源）和密码朋克精神。

**敏捷性 (Agility)**

- 协议通过**EIP（以太坊改进提案）**开放演进，对高层组件（如EVM）的修改需谨慎，但发现优化机会时果断调整。

------

##### **设计原则**

**管理复杂性 (Managing Complexity)**

- **三明治模型**：核心层（共识）和用户接口保持简单，复杂性封装在中间层（编译器、序列化脚本等）。
- **复杂性优先级**：Layer 2 > 客户端实现 > 协议规范，确保核心层稳定。

**自由 (Freedom)**

- 用户使用协议不受限制，避免类似比特币的“OP_RETURN限制”等歧视性规则。通过**Pigovian税**（交易费）让资源消耗者承担成本。

**泛化 (Generalization)**

- 操作码设计追求底层化，例如将“事件日志”从交易中分离为独立`LOG`指令，而非硬编码到消息结构。

**无特性 (We Have No Features)**

- 拒绝内置高频用例（如比特币的锁定时间），鼓励通过合约实现子协议。例如，通过签名数据包模拟锁仓功能。

------

##### 关键思考点

- **模块化如何促进创新**：Proto-Danksharding为Layer 2扩展提供基础模块，验证了模块化设计的灵活性。
- **复杂性封装的意义**：将LevelDB接口与核心共识分离，降低开发者参与门槛，同时支持未来存储方案的替换。



### 2025.02.07

#### Protocol Design Philosophy（two day）

------

##### **账户模型 vs. UTXO**

- **UTXO缺点**：隐私虽高但结构复杂，难以支持智能合约（如去中心化交易所）。
- **账户优势**：
  1. **空间效率**：账户存储占用更低（30字节 vs. UTXO的300字节）。
  2. **同质化**：账户余额完全可互换，无UTXO的“污染”问题。
  3. **防重放攻击**：通过递增`nonce`实现，但需解决废弃账户存储问题（如引入区块号限时重置）。

------

##### **数据结构演进**

1. **Merkle Patricia Trie (MPT)**
   - 结合Merkle树和Patricia算法，实现O(log n)的插入/查询效率，状态根哈希保证数据不可篡改。
   - **问题**：状态膨胀（1-2TB）导致节点存储压力，推动**无状态性**研究。
2. **Verkle树**
   - 通过向量承诺（Vector Commitments）缩小证明体积，支持更高效的轻客户端验证。
   - 分支因子`k`权衡带宽与计算，目标取代MPT以支持未来扩容。

------

##### **序列化协议**

1. **RLP (Recursive Length Prefix)**
   - 仅编码结构（嵌套数组），无数据类型定义，确保确定性序列化。
   - 缺点：不支持高效默克尔化（Merkleization），影响无状态性。
2. **SSZ (Simple Serialize)**
   - 引入固定类型和默克尔化，提升哈希计算效率（O(1) vs. RLP的O(n)），成为Eth2核心序列化方案。

------

##### **共识与最终性**

- **Casper FFG**：通过两轮验证者投票实现最终性，惩罚33%质押ETH的恶意行为。
- **LMD-GHOST**：选择最重子链的分叉规则，结合Casper形成**Gasper**共识协议，平衡安全性与活性。

------

##### **网络层设计**

- **DHT (Kademlia)**：用于节点发现（ENR记录），提供去中心化的路由表维护。
- **Gossip协议**：区块传播通过无结构网络（如gossipsub）实现高鲁棒性，DHT仅用于引导而非数据传输。

------

##### 技术挑战与趋势

- **状态爆炸**：Verkle树与无状态客户端是解决存储压力的关键路径。
- **混合网络模型**：DHT（结构化）与Gossip（无结构）结合，平衡全局发现与高效传播。



### 2025.02.08

#### 以太坊协议的历史与演进

------

#### **Frontier阶段（2015.7.30）**

- **定位**：以太坊首个测试版协议，允许开发者实验和构建去中心化应用。
- **关键特性**：
  1. **初始Gas限制**：创世区块启动时硬编码Gas上限为5000，后通过**解冻分叉**提升至314万（3,141,592），为早期网络启动提供缓冲。
  2. **金丝雀合约（Canary Contracts）**：
     - 功能：通过返回`0`或`1`信号控制客户端行为，若检测到多个合约返回`1`，客户端停止挖矿并提示升级。
     - 目的：防止长期网络分裂，确保矿工及时响应协议升级。

------

#### **Homestead阶段（2016.3.14）**

- **意义**：标志以太坊从测试版转向成熟稳定平台。
- **核心升级（EIPs）**：
  1. **EIP-2**（多项改进）：
     - **合约创建Gas成本提升**：从21,000增至53,000，抑制通过交易创建合约的滥用行为。
     - **高s值签名失效**：防止交易哈希被篡改（如s值取`secp256k1n/2`以上时无效）。
     - **合约创建失败处理**：Gas不足时直接失败，避免生成空合约。
     - **难度调整算法优化**：动态调整出块时间，提升网络稳定性。
  2. **EIP-7**：新增`DELEGATECALL`操作码。
     - **作用**：允许子合约继承父合约的`msg.sender`和`msg.value`，支持代码库复用（如代理合约模式）。
     - **与CALLCODE区别**：不附加Gas津贴，Gas管理更可控。
  3. **EIP-8**：网络协议向前兼容性。
     - **原则**：遵循**Postel法则**（“对输出严格，对输入宽容”），客户端忽略未知协议版本/字段，确保未来升级平滑过渡。

------

#### **The Merge（2022.9.15）**

- **核心变革**：共识机制从PoW（工作量证明）转向PoS（权益证明）。
- **实现路径**：
  1. **分层架构**：
     - **执行层**：处理交易与智能合约（原PoW逻辑层）。
     - **共识层**：由**信标链（Beacon Chain）**提供PoS共识（独立P2P网络），自2020年12月运行验证。
  2. **EIP-3675**：正式弃用PoW，合并执行层与共识层。
- **影响**：
  - 能源消耗降低99.95%，终结矿机挖矿时代。
  - 为后续扩容（分片）和安全性升级（最终性机制）奠定基础。

------

#### 思考

**Homestead的奠基作用**：

- `DELEGATECALL`推动智能合约可组合性，成为DeFi和代理合约（如ERC-1967）的技术支柱。
- EIP-8的兼容性设计使以太坊网络具备长期演进能力。

**Merge的意义与挑战**：

- **去中心化增强**：PoS降低参与门槛，但需解决质押中心化风险。
- **技术复杂性**：分层架构要求执行层与共识层紧密协同，验证者客户端（如Prysm、Lighthouse）的稳定性成为关键。

**历史演进的模式**：

- 从**功能验证（Frontier）到稳定扩展（Homestead）**，再到**架构重构（Merge）**，体现以太坊“敏捷迭代，长期主义”的技术哲学。



### 2025.02.09

#### 以太坊执行层规范（第1天）

------

#### **状态转换函数（State Transition Function）**

- **核心作用**：回答两个关键问题——

  1. 当前区块能否被添加到区块链末尾？
  2. 添加后状态如何变化？

- **公式表示**：

  $$\sigma_{t+1} \equiv \Pi(\sigma_t, B)$$

  - $$\sigma_t$$：前一区块状态
  - $$B$$：当前区块
  - $$\Pi$$：区块级状态转换函数，处理交易并更新状态

- **实现步骤**：

  1. 获取父区块头（Parent Header）
  2. 验证"Excess Blob Gas"（EIP-4844引入的Blob交易相关参数）
  3. 检查区块头字段（时间戳、Gas限制等）
  4. 执行区块内交易，生成状态根、日志等
  5. 验证执行结果与区块头是否一致

------

#### **区块头验证（Block Header Validation）**

- **关键校验项**：
1. **Gas限制约束**：子区块Gas限制需在父区块的±1/1024范围内，防止突变：
     $$\begin{cases}
     H_{\text{gasLimit}} < P(H)_{\text{gasLimit}} + \left\lfloor \frac{P(H)_{\text{gasLimit}}}{1024} \right\rfloor & (57b) \\
     H_{\text{gasLimit}} > P(H)_{\text{gasLimit}} - \left\lfloor \frac{P(H)_{\text{gasLimit}}}{1024} \right\rfloor & (57c)
     \end{cases}$$
  
2. **时间戳顺序**：$$H_{\text{timestamp}} > P(H)_{\text{timestamp}}$$（57e）
  
3. **Nonce与难度归零**：$$H_{\text{difficulty}} = 0$$（57k），$$H_{\text{nonce}} = \texttt{0x0000000000000000}$$（57l）
  
4. **Blob Gas限制**：单区块Blob Gas上限为786,432（57p），且必须为217的整数倍（57q）

------

#### **数据结构与数学基础**

- **状态树（Merkle Patricia Trie）**：

  - 存储账户状态，通过TRIE函数生成状态根哈希。

  - 示例：账户存储根计算（公式7）：

    $$\text{TRIE}(LI^*(\sigma[a]_s)) \equiv \sigma[a]_s$$

    - $$LI((k,v)) \equiv (\text{KEC}(k), \text{RLP}(v))$$

- **自然数（$$\mathbb{N}$$）的应用**：

  - Gas相关参数（如$$H_{\text{gasUsed}}`、`H_{\text{gasLimit}}$$）使用自然数，确保计算精确性。



### 2025.02.10

#### 以太坊执行层规范（第2天）

##### **经济模型与Gas动态**

- **EIP-1559机制**：

  - **基础费用调整公式**：
    $$\nu = 
    \begin{cases}
    \left\lfloor \frac{P(H)_{\text{baseFeePerGas}} \times (\tau - P(H)_{\text{gasUsed}})}{\tau \times \xi} \right\rfloor & \text{if } P(H)_{\text{gasUsed}} < \tau \\
    \max\left(\left\lfloor \frac{P(H)_{\text{baseFeePerGas}} \times (P(H)_{\text{gasUsed}} - \tau)}{\tau \times \xi} \right\rfloor, 1\right) & \text{if } P(H)_{\text{gasUsed}} > \tau
    \end{cases}$$
    - $$\xi= 8$$（控制基础费用最大变化率）
  
- **模拟分析**：
  - 基础费用在目标附近呈线性变化（见下图）：
    <img src=".starrydeserts_image/gasused-basefee.png" alt="gasused-basefee" style="zoom: 67%;" />

------

##### **Blob Gas定价机制**

- **超额Blob Gas计算**：
  
  $$\text{CalcExcessBlobGas}(P(H)) = 
  \begin{cases}
  0 & \text{if } P(H)_{\text{blobGasUsed}} < \text{TargetBlobGasPerBlock} \\
  P(H)_{\text{blobGasUsed}} - \text{TargetBlobGasPerBlock} & \text{otherwise}
  \end{cases}$$
  
  - $$\text{TargetBlobGasPerBlock} = 393,216$$
  
- **Blob Gas价格公式**：
  $$\text{BlobGasPrice} = \text{fake\_exponential}\left(1, \frac{\text{excessBlobGas}}{3,338,477}\right)$$

  - 模拟显示持续超额时价格指数上升（见下图）：
    ![blob-gas-and-price](.starrydeserts_image/blob-gas-and-price.png)



### 2025.02.11

#### 以太坊执行层规范（第3天）

------

##### **交易执行与EVM机制**

- **执行阶段**：

  1. **检查点状态（$$\sigma_0$$）**：
     $$\sigma_0 \equiv \sigma \quad \text{except:} \quad 
     \begin{cases}
     \sigma_0[\text{Sender}]_{\text{balance}} = \sigma[\text{Sender}]_{\text{balance}} - \text{upfrontCost} \\
     \sigma_0[\text{Sender}]_{\text{nonce}} = \sigma[\text{Sender}]_{\text{nonce}} + 1
     \end{cases}$$

- **EVM状态机**：
  - **寄存器定义**：
    $$\mu \equiv (\mu_{\text{gasAvailable}}, \mu_{\text{programCounter}}, \mu_{\text{memoryContents}}, \mu_{\text{activeWordsInMemory}}, \mu_{\text{stackContents}})$$

------

##### **合约创建流程**

1. **地址生成**：
   $$\text{地址} = \text{KEC}(\text{RLP}([\text{Sender}_{\text{address}}, \text{Sender}_{\text{nonce}} - 1]))[-20:]$$

2. **账户初始化**：
   $$\sigma^*[\text{newAccount}] \equiv (\text{Nonce}=1, \text{Balance}=T_{\text{value}}, \text{Storage}=\text{TRIE}(\emptyset), \text{CodeHash}=\text{KEC}(()))$$

------

##### **Gas计算模型**

- **内存扩展成本**：
  $$\text{MemoryExpansionCost} = 3 \times \Delta_{\text{expansion}} + \left\lfloor \frac{\Delta_{\text{expansion}}^2}{512} \right\rfloor$$
  - $$\Delta_{\text{expansion}}$$：新增内存块数

------

##### **R代码：基础费用模拟**

```R
calculate_base_fee_per_gas <- function(
  parent_gas_limit, parent_gas_used, parent_base_fee_per_gas,
  max_change_denom = 8, elasticity_multiplier = 2
) {
  parent_gas_target <- parent_gas_limit %/% elasticity_multiplier
  if (parent_gas_used == parent_gas_target) {
    parent_base_fee_per_gas
  } else if (parent_gas_used > parent_gas_target) {
    gas_used_delta <- parent_gas_used - parent_gas_target
    base_fee_per_gas_delta <- max(
      (parent_base_fee_per_gas * gas_used_delta %/% parent_gas_target) %/% max_change_denom,
      1
    )
    parent_base_fee_per_gas + base_fee_per_gas_delta
  } else {
    gas_used_delta <- parent_gas_target - parent_gas_used
    base_fee_per_gas_delta <- (parent_base_fee_per_gas * gas_used_delta %/% parent_gas_target) %/% max_change_denom
    parent_base_fee_per_gas - base_fee_per_gas_delta
  }
}
```



### 2025.02.12

#### 以太坊执行层架构（第1天）

------

##### **客户端架构概览**

###### 核心职责

1. **区块链数据验证与存储**
   - 维护本地区块链副本
   - 通过默克尔树验证数据完整性
2. **网络通信**
   - 使用DevP2P协议进行点对点通信
   - 交易池（mempool）管理
3. **共识层协作**
   - 实现Engine API接口
   - 响应`forkChoiceUpdated`和`newPayload`调用

##### 分层架构

<img src=".starrydeserts_image/Layered-Architecture.png" alt="Layered-Architecture" style="zoom: 33%;" />

------

##### **EVM设计原理**

###### 虚拟机核心特征

- **硬件无关性**
  通过`EVM字节码`实现跨平台一致性，类似JVM设计理念
- **沙盒环境**
  每个交易在隔离环境中执行，保证状态变更原子性

###### 三明治复杂性模型

1. **外层（简单）**
   - Solidity/Yul等高级语言
   - JSON-RPC接口
2. **中间层（复杂）**
   - 编译器（Solidity→EVM字节码）
   - Gas计量系统
3. **内层（简单）**
   - EVM指令集（约140个操作码）

------

##### **状态管理机制**

###### 全局状态组成

| 组件     | 存储内容                | 数据结构        |
| -------- | ----------------------- | --------------- |
| 账户状态 | 余额/Nonce/合约代码哈希 | Merkle-Patricia |
| 合约存储 | 智能合约变量数据        | Merkle-Patricia |
| 交易收据 | 交易执行日志            | Bloom Filter    |

###### 状态转换公式
$$\sigma_{t+1} \equiv \Upsilon(\sigma_t, T)$$

- $$\sigma_t$$: 当前状态
- $$T$$: 交易集合
- $$\Upsilon$$: 状态转换函数

------

##### **交易生命周期**

###### 处理流程

1. **接收**
   通过JSON-RPC接口接收签名交易
2. **验证**
   - 签名有效性
   - Nonce连续性
   - Gas预算充足
3. **传播**
   通过DevP2P协议广播至全网节点
4. **打包**
   被矿工/验证者选入候选区块
5. **执行**
   在EVM中触发状态转换

###### Gas计算模型
$$\text{总Gas成本} = \text{固有成本} + \sum(\text{操作码Gas} \times \text{执行次数})$$

------

##### **网络层（DevP2P）**

###### 关键协议

| 协议   | 功能         | 传输内容      |
| ------ | ------------ | ------------- |
| eth/66 | 区块同步     | 区块头/体数据 |
| eth/67 | 交易传播     | 原始交易数据  |
| les/4  | 轻客户端支持 | 状态证明      |

###### 节点发现机制

1. 使用Kademlia DHT协议
2. 通过ENR记录存储节点元数据
3. 维护动态路由表（Bucket结构）



### 2025.02.13

#### 以太坊执行层架构学习笔记（第2天）

------

##### **引擎API（Engine API）**

###### 核心接口

```go
type EngineAPI interface {
    NewPayloadV1(payload ExecutionPayload) (PayloadStatusV1, error)
    ForkchoiceUpdatedV1(state ForkchoiceState, attr PayloadAttributes) (ForkchoiceUpdatedResult, error)
}
```

###### 工作流程

1. **共识层触发**
   - 接收`ForkchoiceUpdated`调用
   - 确定规范链头（head block）
2. **有效载荷验证**
   - 检查父块哈希一致性
   - 验证时间戳序列
3. **状态同步**
   - 执行区块内交易
   - 更新全局状态树

------

##### **同步机制**

###### 同步模式对比

| 模式     | 特点                     | 适用场景         |
| -------- | ------------------------ | ---------------- |
| 全量同步 | 从创世块开始验证所有交易 | 新节点初始化     |
| 快速同步 | 下载最新状态快照         | 追赶网络最新状态 |
| 轻同步   | 仅同步区块头+Merkle证明  | 移动设备/浏览器  |

###### 状态同步公式

$$\text{同步进度} = \frac{\text{已验证区块高度}}{\text{网络最新高度}} \times 100\%$$

------

##### **有效载荷验证流程**

###### 验证步骤

1. **区块头验证**

   $$H_{\text{gasLimit}} \in \left[P(H)_{\text{gasLimit}} \pm \left\lfloor \frac{P(H)_{\text{gasLimit}}}{1024} \right\rfloor\right]$$

2. **随机数验证**

   - $$H_{\text{difficulty}} = 0$$ (PoS区块)
   - $$H_{\text{nonce}} = 0x0000000000000000$$

3. **时间戳验证**

   

   $$H_{\text{timestamp}} > P(H)_{\text{timestamp}}$$

###### 客户端实现差异

| 检查项       | Geth实现位置              | Reth实现位置        |
| ------------ | ------------------------- | ------------------- |
| Gas限制验证  | `core/block_validator.go` | `crates/engine/src` |
| 基础费用计算 | `core/fee_history.go`     | `crates/revm/src`   |

------

##### **交易池管理**

###### 双池架构

<img src=".starrydeserts_image/Dual-pool_architecture.png" alt="Dual-pool_architecture" style="zoom: 33%;" />

###### 淘汰机制对比

| 池类型 | 排序依据                  | 淘汰策略           |
| ------ | ------------------------- | ------------------ |
| Legacy | 有效小费（Effective Tip） | 大顶堆淘汰低优先级 |
| Blob   | 对数时间衰减              | 滑动窗口淘汰       |

------

##### **共识引擎集成**

###### 多引擎支持

```go
type ConsensusEngine interface {
    VerifyHeaders(chain BlockChain, headers []*Header) (chan<- struct{}, <-chan error)
    Finalize(chain BlockChain, header *Header, state *state.StateDB, txs []*Transaction)
}
```

###### 验证流程示例

1. 分离PoW/PoS区块头
2. 预合并区块使用Ethash验证
3. 后合并区块通过Beacon链验证
4. 检查终态性（Finality）标记





### 2025.02.14

#### 以太坊区块构建与交易处理学习笔记

------

##### **区块构建概览**

###### 核心参与方

1. **共识层（CL）**
   - 负责验证者选举
   - 确定区块提案者
   - 通过Engine API触发执行层构建区块
2. **执行层（EL）**
   - 维护交易池（mempool）
   - 执行交易并生成有效载荷（Payload）
   - 实现状态转换函数

###### 构建流程触发

- **触发条件**：验证者通过`engine_forkchoiceUpdatedV2`接口接收构建指令

- **输入参数**：

  $$\text{PayloadAttributes} = \{ \text{timestamp}, \text{prev\_hash}, \text{base\_fee}, ... \}$$

------

##### **区块构建核心流程**

###### 初始化空区块

```go
func buildPayload(env *Environment) (*ExecutionPayload, error) {
    emptyBlock := createEmptyBlock(env)  // 创建基准空区块
    go asyncFillBlock(emptyBlock)        // 异步填充交易
    return emptyBlock, nil
}
```

- **目的**：确保在时间窗口内至少有空区块可提议
- **异步优化**：后台继续完善区块内容

###### 交易填充机制

<img src=".starrydeserts_image/Transaction-filling-mechanism.png" alt="Transaction-filling-mechanism" style="zoom: 33%;" />

- **排序规则**：优先选择gas费率高且nonce连续的交易

- **Gas配额管理**：

  $$\sum(\text{tx.gasLimit}) \leq 30,000,000 \quad (\text{当前主网Gas上限})$$

###### 交易执行与状态转换

```go
func applyTransaction(tx *Transaction, state *StateDB) error {
    evm := NewEVM(Context{Block: env}, state)
    result, err := evm.Run(tx)  // 执行交易
    if err != nil {
        return err  // 失败交易被丢弃
    }
    state.ApplyResult(result)   // 更新状态
    return nil
}
```

- **原子性保证**：单笔交易失败不影响区块整体有效性

- **状态树更新**：

  $$\sigma_{new} = \Upsilon(\sigma_{old}, tx)$$

------

##### **关键组件解析**

###### 交易池（TxPool）

- **数据结构**：
  - **Pending队列**：已验证待打包交易
  - **Queued队列**：nonce不连续交易
- **淘汰策略**：
  - **Legacy交易**：按gas价格大顶堆淘汰
  - **Blob交易**：按时间衰减窗口淘汰

###### EVM执行环境

| 环境变量          | 来源              | 示例值     |
| ----------------- | ----------------- | ---------- |
| `block.timestamp` | PayloadAttributes | 1700000000 |
| `block.number`    | 父区块高度+1      | 18923456   |
| `block.basefee`   | EIP-1559动态计算  | 15 Gwei    |

------

##### **错误处理机制**

###### 交易级别错误

- **类型**：
  - Gas不足（OutOfGas）
  - 无效操作码（InvalidOpcode）
  - 合约回滚（Revert）
- **处理方式**：
  - 丢弃无效交易
  - 继续尝试打包后续交易

区块级别错误

- **类型**：
  - GasLimit超标
  - 时间戳不连续
- **处理方式**：
  - 终止当前构建流程
  - 触发CL重新选择提案者

------

##### **性能优化策略**

1. **异步填充**：先返回空区块再完善内容
2. **交易预验证**：维护已验证交易池
3. **状态快照**：使用`StateDB`的快照功能快速回滚
4. **并行执行**：实验性支持多交易并行执行



### 2025.02.15

#### 以太坊执行层数据结构学习笔记

------

##### **核心数据结构概览**

###### 默克尔树（Merkle Tree）

- **结构特性**

  <img src=".starrydeserts_image/tries.png" alt="tries"  />

- **核心机制**：

  - 叶子节点存储数据哈希值
  - 非叶子节点存储子节点哈希的拼接哈希
  - 根哈希存储在区块头中

- **数据完整性验证**：

  - $$\text{篡改检测} \Rightarrow \Delta Data \rightarrow \Delta LeafHash \rightarrow \Delta RootHash$$

###### 前缀树（Patricia Tree）

- **优化特性**：
  - 共享前缀压缩（如`0x12A`和`0x12B`共享`0x12`路径）
  - 节点类型精简（分支/扩展/叶子）
- **存储效率**：
  - $$\text{传统Trie空间复杂度} O(n) \rightarrow \text{Patricia空间复杂度} O(k) \quad (k为键长)$$

###### 默克尔前缀树（MPT）

- **混合设计**：

  - 继承Merkle的完整性验证
  - 采用Patricia的存储优化

- **节点类型**：

  | 节点类型 | 结构描述                    | 示例场景       |
  | -------- | --------------------------- | -------------- |
  | 分支节点 | 17元素数组（16分支+值指针） | 路径分叉点     |
  | 扩展节点 | [压缩路径, 子节点哈希]      | 单一路径段压缩 |
  | 叶子节点 | [剩余路径, 值数据]          | 键值对存储终点 |

------

##### **以太坊中的MPT应用**

###### 四大核心Trie结构

| Trie类型     | 存储内容                     | 更新频率     | 根哈希位置                |
| ------------ | ---------------------------- | ------------ | ------------------------- |
| 交易Trie     | 区块内所有交易               | 区块不可变   | BlockHeader.txRoot        |
| 收据Trie     | 交易执行结果（日志/Gas消耗） | 区块不可变   | BlockHeader.receiptRoot   |
| 世界状态Trie | 所有账户的当前状态           | 区块可变     | BlockHeader.stateRoot     |
| 账户存储Trie | 智能合约的持久化变量         | 合约调用可变 | 账户对象的storageRoot字段 |

###### 交易Trie构建规则

- **键值编码**：
  - $$Key = RLP(交易索引) \quad Value = RLP(交易数据)$$

- **交易数据结构**：

  ```go
  type Transaction struct {
      Nonce    uint64
      GasLimit uint64
      To       common.Address
      Value    *big.Int
      Data     []byte
      V, R, S  *big.Int // 签名
  }
  ```

------

##### **RLP编码规范**

###### 编码规则

- **基本类型**：

  - 字符串：直接编码为字节序列
  - 整数：大端序无前缀零编码

- **嵌套结构**：

  - $$RLP([a, b, c]) = RLP(a) \oplus RLP(b) \oplus RLP(c)$$

- **长度标识**：

  | 数据长度 | 前缀字节         |
  | -------- | ---------------- |
  | 0-55字节 | 0x80 + len       |
  | >55字节  | 0xB7 + len字节数 |

###### 应用场景

- 交易/收据的序列化存储
- 状态树节点的键值编码
- 网络传输数据封装

------

##### **MPT节点哈希机制**

###### 哈希计算流程

1. **序列化节点**：使用RLP编码节点内容
2. **Keccak-256哈希**：
   - $$nodeHash = \text{Keccak256}(RLP(nodeContent))$$
3. **递归计算**：子节点哈希参与父节点哈希生成

###### 安全特性

- **雪崩效应**：单字节修改导致根哈希完全变化
- **防碰撞保证**：
  - $$P(\text{哈希碰撞}) \approx \frac{1}{2^{256}} \approx 10^{-77}$$

------

##### **MPT操作示例**

###### 数据插入流程

1. 从根节点开始匹配键路径
2. 遇到扩展节点时展开共享前缀
3. 在分支节点处分叉
4. 创建新叶子节点存储值
5. 自底向上更新路径上的所有节点哈希



### 2025.02.16

#### 以太坊交易与合约创建解析

------

##### **交易（Transaction）结构解析**

1. **核心字段**：

   - **Nonce**：
     - 用途：防止重放攻击、确定合约地址、替换卡顿交易。
     - 示例：首次交易 Nonce=0，递增保证唯一性。
   - **gasPrice**（单位：Wei）：
     - 决定交易优先级，矿工优先打包高 gasPrice 的交易。
   - **gasLimit**：
     - 交易执行的最大 Gas 消耗量，不足则执行中断。
   - **to**：
     - 为空：合约创建模式。
     - 外部账户地址：转账模式。
     - 合约地址：调用合约函数。
   - **value**（单位：Wei）：
     - 转账金额（若为合约创建，则为新合约初始余额）。
   - **data/init**：
     - 合约创建模式：`init` 字节码（部署时执行，返回 runtime 代码）。
     - 其他模式：调用合约的输入数据（如函数参数）。
   - **签名**（Signature）：
     - ECDSA 签名，验证交易合法性。

2. **交易模式**：

   | `to` 字段值  | 模式     | 描述               |
   | ------------ | -------- | ------------------ |
   | 空           | 合约创建 | 创建新合约账户     |
   | 外部账户地址 | 转账     | 向外部账户转移 ETH |
   | 合约账户地址 | 合约调用 | 执行合约代码       |

------

##### **合约创建流程示例**

1. **目标合约代码**：

   ```solidity
   // Runtime 代码（执行 6*7=42 并存储）
   [0c] PUSH1 06
   [0e] PUSH1 07
   [10] MUL
   [11] PUSH1 0
   [13] SSTORE
   ```

2. **Init 代码构造**：

   - **功能**：将 Runtime 代码复制到内存并返回。
   - **步骤**：
     1. 使用 `CODECOPY` 复制代码到内存。
     2. `RETURN` 返回内存中的 Runtime 代码。

   ```javascript
   // Init 字节码
   6008600c60003960086000f3 // 复制代码到内存并返回
   6006600702600055         // Runtime 代码（6*7）
   ```

3. **部署交易参数**：

   ```json
   [
     "0x",                    // Nonce=0（首次交易）
     "0x77359400",            // gasPrice=2 Gwei
     "0x13880",               // gasLimit=80000
     "0x",                    // to=空（合约创建模式）
     "0x05",                  // 向合约转账 5 Wei
     "0x6008600c60003960086000f36006600702600055" // init 代码
   ]
   ```

4. **工具使用（Foundry）**：

   - **Anvil**：启动本地测试节点。

     ```bash
     $ anvil  # 启动节点，生成测试账户
     ```

   - **Cast**：签名并发布交易。

     ```bash
     $ cast publish <RAW_TX>  # 发布交易
     $ cast code <CONTRACT_ADDRESS>  # 查询合约代码
     $ cast storage <CONTRACT_ADDRESS> 0x  # 查询存储槽0的值
     ```

------

##### **合约执行验证**

1. **调用合约交易**：

   ```json
   [
     "0x1",                   // Nonce=1（递增）
     "0x77359400",            // gasPrice=2 Gwei
     "0x13880",               // gasLimit=80000
     "0x5fbdb2315678afecb367f032d93f642f64180aa3", // 合约地址
     "0x",                    // value=0（不转账）
     "0x"                     // data=空（触发默认函数）
   ]
   ```

2. **验证结果**：

   ```bash
   $ cast storage 0x5fbdb... 0x
   # 输出 0x2a（即 42，6*7 的结果）
   ```

------

##### **总结**

1. **交易字段协作**：Nonce 防重放、gas 控制资源、to/data 决定行为。
2. **合约生命周期**：
   - Init 代码（一次性执行） → 返回 Runtime 代码（持久存储）。
   - 后续交易通过 `to` 指向合约地址调用代码。
3. **工具链**：Foundry（Anvil + Cast）简化本地测试与调试。



<!-- Content_END -->
