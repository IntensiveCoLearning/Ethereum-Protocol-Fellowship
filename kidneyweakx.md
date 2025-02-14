---
timezone: Asia/Taipei
---

# {你的名字}

1. 自我介绍: Hello，大家好，區塊鏈開發者曾經做聯盟鏈底層的研究
2. 你认为你会完成本次残酷学习吗？ 會的

## Notes

<!-- Content_START -->

# 2025.02.06

Note: 今日任務把 https://epf.wiki/#/ 簡單掃一遍，列一下這次共學目標以及學習規劃

### [Ethereum Architecture](https://epf.wiki/#/wiki/protocol/architecture)

第一天先從以太坊目前的架構設計開始，在 the Merge 之後沒有關注的很緊，目前比較熟悉的部分在 EL，初期想研究一下，CL 和 EL 之間溝通的 Engine API 設計，想理解其中 fault tolerance 設計
![](https://epf.wiki/wiki/protocol/img/clients-overview.png)

在以太坊的設計理念上簡單、普遍、模組，非歧視、敏捷，

但目前看起來是真的頗複雜，我覺得 CL 和 EL 分開確實是一件不錯的設計，但我還尚未深入研究，想要知道對整體設計上有沒有類似理想原則設計的大局觀

以太坊的本體價值類似於 Linux 這樣的自由軟體，大型軟體的底層管理和政治上的平衡，個人覺得以太坊做得還不錯，在原則和教育上都有做到一定的水平

TODO: 明日計畫看一下 protocol 目前的樹設計 MPT 和 Verkle Tree 的優劣之類的

# 2025.02.07
看來 MPT 和 Verkle 的主要差異就在 witness 證明，這邊只有簡介到時候會再花時間研究

LMD GHOST + Casper FFG = Gasper (ETH2 目前的共識機制)

DHT 是我蠻感興趣的部分，很好奇ETH 底層的 p2p 效率和路由如何構建
以太目前設計和多數 DHT 不同的是，在 bittorrent 和 IPFS 這類產品都沒有一個明確的搜索目標，而在以太坊網路中最重要的就是最新區塊
用過私有鏈一陣子，整體 p2p 大概是透過 enode:// + ip 和地址來互相獲取資訊，接下來就是 Gossipsub 裡面在做的事了

整體把結構看了一下，ETH 和 ETH2 主要不同的點目前看來比較會 focus 在 Gasper 的實現，之後也可以深入研究下 Verkle 對於當前以太的好處

TODO: 明天假日可以來看下 week0 + 1 的影片，如正常按照順序會順便看 EL 的介紹

# 2025.02.08

Protocol History 簡介: Frontier (創世區塊) -> Homestead (EIP-2, 7, 8) -> The Merge

EL 的關鍵: State Transition Function
過程大概可以列為下列步驟
1. 獲取區塊頭 (Block Header)
2. 驗證 blob gas
3. 計算區塊頭
4. Ommers Field 驗證叔區塊
5. 區塊執行
6. 標頭驗證
7. 區塊添加
8. 刪除舊區塊
9. error handle

# 2025.02.09
gas 算式挺複雜的，看了一陣子
以太坊在 EIP-1559 後的 gas 計算功能，這有再用以太的應該都挺熟的，Base Fee 的經濟估算我明天會和 Blob 一起看

# 2025.02.10
今天看的東西不多，大概搞懂坎昆升級後 Blob 的計算公式，總感覺現在這機制弄的有點複雜和雜亂

# 2025.02.11
EL Client 今天看的相對比較熟，之前玩過 quorum 和 besu 設計挺像的

# 2025.02.12
EVM 這篇教學不錯，有圖解很詳細，不過我還要多看看下面的 ref

# 2025.02.13
開始看 ref 最近的心得都比較少...
<!-- Content_END -->