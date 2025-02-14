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

# {吃汤圆}

1. 自我介绍   一个普普通通又好吃的汤圆，技术栈：Python/Matlab/C，具备电力系统仿真和量化交易系统开发经验。  对web3感兴趣探索ing
2. 你认为你会完成本次残酷学习吗？ 一定会的

## Notes

<!-- Content_START -->

### 2025.02.06

今天阅读了
1.The Protocol：
1.1Prehistory of Ethereum
我一直很看好以太坊，而不是很看好比特币，我为什么这么坚持的原因就可以从这一段历史里面读出来。
其实以太坊的出现来源于两种精神：开源运动和密码朋克运动。
开源运动的代表有GNU/Linux 操作系统和它后面一整个庞大的社区
密码朋克运动代表有David Chaum 在 1985 年发表的 “无需识别的安全：使老大哥过时的交易系统”
这两种思想共同孕育出了Ethereum。
接下来说说为什么不看好比特币，我这里的不看好只是指发展的潜力，作为区块链的开创者比特币的价值必然不低，可是我并不看好他。因为它只是密码朋克运动的发展，但是却没有充分的结合开源运动的精神。从比特币发行到现在虽然价格一直在涨，感觉很热闹，但是基础基本上完全没变，有人说这就够了，这说明比特币已经足够成功了无需再变，以太坊那些所谓区块链2.0无非是画蛇添足的跳梁小丑。但是我认为这大错特错，是比特币无需改，还是比特币改不动了，在这里要打上一个问号？而且我认为只有能结合时代不断发展改变自身的技术，才能真正为人类做出实打实的贡献。虽然以太坊一跌再跌，我也一点不心疼，因为这就是创新的代价。比特币的价值就算在高也只能当成古董，但是以太坊的价值才是新世界的卡密。

### 2025.02.07
以太坊的设计哲学就是一层一层叠上去：

最底层的就是核心的理念想法：简洁性，通用性，模块化，非歧视性，敏捷性
而在这之上是更具体的想法：
三明治模型：综合了简洁性，通用性，模块化的思想。其实就是把以太坊架构的“底层”和“接口”都做得简单易懂，把复杂性藏到中间。
gas fee：非歧视性的延伸。不会限制你的自由，不会直接禁止你，但是如果你干的事情占用了更多资源，那就多交点gas fee。公平公正非歧视！

### 2025.02.08
执行层负责处理交易和执行智能合约，确保交易的合法性和状态的更新。
共识层负责验证区块、维护网络的安全性和一致性，确保所有节点对区块链的状态达成共识。
### 2025.02.09
今天看以太坊Execution Layer看麻了，这么多数学公式，这么多代码，你是要我命吗？！

EIP-1559
作用：引入了动态基础费用（Base Fee），这个费用会根据网络的拥堵情况自动调整。
例子：如果网络很忙（很多交易等待处理），基础费用会增加，鼓励用户减少交易或支付更高的费用来优先处理。
EIP-4844
作用：引入了Blob交易，这是一种新的交易类型，用于处理大量的数据（比如智能合约的存储）。
例子：Blob交易有自己的Gas价格机制，当网络对Blob数据的需求增加时，Blob Gas价格会上升。
就看了这些，明天接着
### 2025.02.10
Development:
Core development:
核心开发包括制定规则、编写程序、进行测试，确保以太坊网络正常运行。
分别是EF Testing、EF DevOps、EF Ipsilon、EF JavaScript来负责

### 2025.02.11
1. 合并（The Merge）
目标：从挖矿（工作量证明）转向质押（权益证明），让网络更环保、更安全。
已完成：
启动了信标链，为合并做准备。
成功完成了合并，停止了挖矿，转向了质押。
允许质押者提取他们的以太币。
未来研究：
单槽最终性（SSF）：让交易更快确认（从12分钟缩短到12秒），提升用户体验。
量子安全签名：研究新的加密技术，防止未来可能出现的量子计算机攻击。
2. 激增（The Surge）
目标：通过“卷叠”（rollups）和“数据分片”（data sharding）提升以太坊的交易处理能力。
已完成：
实现了“Proto-danksharding”，降低了交易成本。
未来研究：
Danksharding：进一步扩展rollups，让以太坊能处理更多交易。
数据可用性采样（DAS）：一种高效验证数据完整性的方法，减轻节点的负担。
3. 净化（The Scourge）
目标：减少审查（censorship）风险，优化矿工提取价值（MEV）的分配，防止中心化。
已完成：
MEV-Boost：将MEV部分分配给质押者。
未来研究：
ePBS（增强型区块提议者和构建者分离）：防止交易被审查，保护小质押者的利益。
MEV-Burn（MEV燃烧）：将MEV的一部分销毁，让所有以太币持有者受益。
ET（执行票证）：通过市场机制选择区块构建者，防止中心化。
IL（包含列表）：确保某些交易必须被包含，防止区块构建者随意审查。
### 2025.02.12
1以太坊客户端测试的重要性
确保网络稳定性和安全性，保障客户端间一致性
2测试内容
执行和共识规范的遵循：测试验证所有客户端是否一致地解释和执行交易，确保符合执行和共识规范。
预防网络分叉：严格的测试作为一种主动的漏洞检测工具，防止因客户端不一致而引发的网络分叉（对规范区块链状态的分歧）。
测试资源和工具
3通用测试套件
pytest：Python测试框架。
Ethereum Tests：适用于所有实现的通用测试。
Hive：以太坊端到端测试工具。
4执行层测试
Execution Spec Tests：针对执行客户端的测试用例。
FuzzyVM：EVM的差异模糊测试工具。
retesteth：测试生成工具。
EVM lab utilities：包括Go evmlab（受EVMLAB启发的EVM实验室）以及执行API的集合。
5共识层测试
Consensus Spec Tests：共识规范测试。

### 2025.02.13
### 2025.02.14
### 2025.02.15
### 2025.02.16
<!-- Content_END -->
