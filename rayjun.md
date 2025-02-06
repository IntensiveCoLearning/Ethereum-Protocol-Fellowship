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

<!-- Content_END -->
