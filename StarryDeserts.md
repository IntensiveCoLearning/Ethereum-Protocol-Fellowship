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

<!-- Content_END -->
