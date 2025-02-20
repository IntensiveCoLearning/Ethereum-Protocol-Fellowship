---
timezone: Asia/Shanghai
---

# Five

1. 自我介绍
大家好，我是来自 **safestake** 的一名开发人员，目前主要从事基于 **DKG（分布式密钥生成）** 的 **ETH Staking** 相关开发工作。我对协议层的基础知识有着浓厚的兴趣，希望通过更系统的学习，进一步提升自己的技术能力。
在工作中，我专注于构建安全、可靠的去中心化系统，致力于为以太坊生态系统的发展贡献自己的力量。未来，我希望能够深入理解协议层的设计原理，并将其应用到实际开发中。

1. 你认为你会完成本次残酷学习吗？
一定会的。

## Notes

<!-- Content_START -->

### 2025.02.19
生病了几天，开追进度。
记录一下关于惩罚机制,以太坊的PoS系统采用了一套全面的奖励和惩罚措施来激励验证者的行为并维护网络安全。本节涵盖这些激励措施的六个主要方面：
1. 证明者奖励：验证者通过与大多数其他验证者一致的证明（LMD GHOST和FFG投票）获得奖励。包含在最终块中的证明更有价值。
2. 证明者惩罚：验证者因未能证明或证明未完成的块而受到惩罚。这些惩罚措施确保验证者保持活跃，并与网络的共识保持一致。
3. 利益相关者的典型下行风险：利益相关者可以通过比较潜在收益和罚款来估计其下行风险。一个诚实的验证者在一年内赚了10%，如果表现不好，可能会损失7.5%。短期不活动会受到轻微的处罚，而长时间离线会受到更大的处罚。
4. Slashing和Whistleblower Rewards：Slashing对严重违反协议的验证者进行惩罚。处罚范围从超过0.5 ETH到整个股份。例如，一个验证者犯了一个可砍的进攻，失去了至少1/32的平衡，并被停用。额外的惩罚与同时削减的验证器数量成比例。举报人举报一个可削减的进攻收到奖励，这目前去块提议。
5. 提议者奖励：区块提议者因提出最终确定的区块而获得丰厚的奖励。一致执行验证器获得大约1/8的总奖励。此外，提议者还可以获得少量奖励，因为他们在自己的区块中加入了大量证据。
6. 不活动泄漏惩罚：不活动泄漏是一种严重的惩罚，旨在确保网络的终结性。如果终结延迟超过四个epoch，验证器将受到越来越多的惩罚，直到检查点终结。这种机制会耗尽不活跃验证者的余额，导致他们被迫退出，从而允许活跃验证者形成绝对多数以恢复最终性。在不活动泄漏期间，只有提议者和举报者获得奖励，而证明者奖励为零。

罪行,有四个条件可以削减验证器：
1. 双重提议：为分配的插槽提议一个以上的区块。
2. LMD GHOST Double Vote：证明同一个插槽的不同Beacon Chain头。
3. FFG环绕投票：投出一张FFG投票，该投票环绕或被同一验证者先前的FFG投票环绕。
4. FFG双重投票：在同一纪元内对不同的目标投两张FFG票。

### 2025.02.10
接下来重要研究 consensus layer 的内容，先从 EIP 官方对 POS 的解释开始。
通过阅读 https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/ 理解 ETH 的 POS 机制设计，由于都是相对较熟的内容，不做过多的笔记。
这里记录一个疑问：当 EIP7251 上线后，POS机制将做什么改变？


### 2025.02.08
今天直接开始从 week2 的内容开始学习。
通过观看视频中伪代码的演示，对 validator 在 execution layer 中如何校验 transactions 和如何产生一个 block 有了更清晰的认识。
明天计划通过阅读 geth 中这部分的源码，更深入的理解 execution layer 中对 transactions 的处理细节。


### 2025.02.07

 由于是 ethereum 开发老手，快速的过了 week1 的内容。
 粗略的过了一遍 test case repo，很好的学习仓库，先 mark ，慢慢学习。
 ```
 Here is a short list of repositories dedicated to testing:

https://github.com/ethereum/tests
https://github.com/ethereum/retesteth
https://github.com/ethereum/execution-spec-tests
https://github.com/ethereum/hive
https://github.com/kurtosis-tech/kurtosis
https://github.com/MariusVanDerWijden/FuzzyVM
https://github.com/lightclient/rpctestgen
 ```
 最后尝试去 [https://ethereum.org/quizzes](https://ethereum.org/quizzes) 做了个小测试，没满分，还是得谦虚。



<!-- Content_END -->
