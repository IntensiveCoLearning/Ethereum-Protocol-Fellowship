---
timezone: Asia/Shanghai
---

---

# poyucheese

1. 自我介绍
   我是在DeFi領域學習的大學生
2. 你认为你会完成本次残酷学习吗？
   會
3. TG 联系方式：@cheeseyes

## Notes

<!-- Content_START -->

### 2025.02.06

#### [SGweek1](https://epf.wiki/#/eps/week1) and my background acknowledge of ethereum

##### history of ethereum

以太坊在2020年底啟用 Beacon Chain ，作為以太坊的共識層(Consensus Layer)並開始使用PoS。在2022年經過了一次 The Merge ，從 PoW 完全轉為 PoS 的共識機制，合併主網與 Beacon Chain ，在同一條鏈上執行和共識分層運行。

- Execution Layer 負責處理單一 block 內的交易、邏輯、Gas 等運算。
- Consensus Layer 負責 block 之間的排序，並確保最終性。

由於目前共識層需要執行層的數據支持，並且主網更新必須保持向後相容，兩層尚無法獨立運行，大量的鏈上交易拖慢速度，這也是目前致力於開發 Layer2 solution 的原因。

### 2025.02.07

#### [SGweek1](https://epf.wiki/#/eps/week1)

今天讀了 week 1 的內容，順便做了 [quiz](https://ethereum.org/zh/quizzes/) 測試自己對以太坊基礎架構的認識，發現我對一般節點和質押驗證者的區別還不夠了解，只要在客戶端運行並在線就能成為一般節點，不必質押 ETH 同時也不會獲得獎勵，而質押驗證者還負責參與共識和打包區塊，須質押 32 ETH 並且在線時間達 50% 以上才能在上線時得到交易費和質押獎勵，質押驗證者若違反共識機制 (**double proposal** or **double voting**)，會遭到罰沒 (Slashing) ，質押的 ETH 被沒收並被踢出驗證。

看到有關 ENS 域名的技術，但還不懂他的運作原理，明天繼續衝鋒。

### 2025.02.08

#### [SGweek2](https://epf.wiki/#/eps/week2)

今天看了 week 2 錄影的片段，介紹的是執行層和共識層的邏輯，這讓我想到曾經看到 PAXG 穩定幣，感興趣查到一種應用在分布式系統的共識算法 [**Paxos 算法**](https://www.youtube.com/watch?v=d7nAGI_NZPk) (不過兩者好像沒什麼關聯)，這種算法可以應用於分佈式資料庫來實現跨資料中心的一致性，但在區塊鏈方面，因為它是基於預先指定的節點投票，所以只能應用於私有區塊鏈，無法應用於公有區塊鏈。

### 2025.02.09

#### [SGweek2](https://epf.wiki/#/eps/week2)

繼續 week 2 的課程，感覺 EVM 的架構在執行和運算上有一些跟 CPU 類似的地方，但還是有本質上的不同，例如 EVM 是 stack-based 的，CPU 則是 register-based，為了確保正確的交易順序，傳統 EVM 與 CPU 不同，無法平行化，我有看到一些有關 Parallel EVM 的研究和技術，但這些研究看起來還有很多挑戰要克服，VM 的平行化感覺會是未來很值得深究的一個方向。

### 2025.02.10

#### [SGweek2](https://epf.wiki/#/eps/week2)

今天沒時間看新的東西，簡單複習消化 week 2 的內容，看其他人的筆記也能收穫很多不同觀點的看法。

### 2025.02.11

#### [SGweek3](https://epf.wiki/#/eps/week3)

今天看了 week 3 的內容，是關於以太坊的共識，包含爲什麼需要共識機制——因為要做到去中心化，此類共識機制如何解決拜占庭問題（確保惡意節點難以攻擊）：

- **PoW (Bitcoin)** 使創建區塊難度提升，攻擊成本大
- **PoW + GHOST (Ethereum1.0)** 以太坊的出塊時間比 bitcoin 短，所以容易出現分叉 (新創建的區塊來不及被廣播)，使用 GHOST 協議和獎勵接受沒成為最長鏈的叔塊，也保護礦工的權益
- **PoS + Casper FFG + LMD GHOST (Ethereum2.0)** 
    - **Casper FFG (Friendly Finality Gadget)**

        >採用投票機制，驗證者透過 質押 ETH 來表決哪個區塊應該成為最終區塊。惡意驗證者若投票錯誤，將面臨懲罰。
    - **LMD GHOST (Latest Message Driven Greediest Heaviest Observed Subtree)**

        >透過權重最大（最多驗證者投票的）的子樹來決定主鏈，確保惡意節點無法輕易影響共識。

### 2025.02.12

#### [SGweek4](https://epf.wiki/#/eps/week4)

week 4 是有關 Ethereum 測試的內容。

##### Execution Layer Testing

- 用於確保 Ethereum 執行客戶端的正確性，避免因實作差異導致的鏈分叉，需要 EVM testing 進行測試，為客戶端提供相同 pre-state (賬戶餘額、nonce、合約代碼和存儲)、環境、輸入 (交易) 、規則，預期得到相同的 post-state。
- Test Filling 可以跨客戶端執行，確保所有實作遵循相同的行為。

### 2025.02.13

#### [SGweek4](https://epf.wiki/#/eps/week4)

##### EVM 測試格式

- 狀態測試（State Testing）：
    - 透過比對狀態根（State Root）來驗證不同客戶端的結果是否一致。
    - 狀態根是一種加密計算結果，可確保狀態完整性。

- 模糊測試（Fuzzy Differential State Testing）：
    - 使用工具 FuzzyVM 在交易中加入隨機智能合約代碼，測試不同客戶端是否仍能保持相同的狀態根。

- 區塊鏈測試（Blockchain Testing）：
    - 測試不僅限於 EVM 執行，還包括 1559 費用機制等完整區塊驗證。

- 區塊鏈負測試（Blockchain Negative Testing）：
    - 插入無效區塊，檢查客戶端是否能正確拒絕此區塊並 revert 到先前的有效區塊。

### 2025.02.14

#### [SGweek4](https://epf.wiki/#/eps/week4)

##### Consensus Layer Testing

- 用於驗證 Ethereum 共識層的行為，確保所有 CL 客戶端遵循相同的規範，並在相同條件下得出一致的結果，防止因實作差異導致區塊鏈分叉或共識錯誤。
- 測試用例包含在規範內，適用於所有客戶端。
- 提供比 EVM 測試更多樣的格式，讓開發者能針對不同需求對各部分進行不同程度的測試。
- CL 測試涵蓋 Ethereum 2.0 的信標鏈，驗證區塊提議、驗證者行為等重要機制。核心測試內容包括：
    - **區塊處理（Block Processing）**：
        >測試信標鏈如何處理新的區塊，確保狀態轉換符合規範。

    - **狀態轉換（State Transition）**：
        >確保不同客戶端在相同條件下，最終產生相同的信標鏈狀態。

    - **驗證者（Validators）行為測試**：
        >測試驗證者的投票、獎勵和懲罰機制，確保一致性。

    - **同步協議（Sync Protocols）**：
        >測試客戶端如何下載並同步信標鏈數據。

    - **罰沒機制（Slashing Conditions）**：
        >驗證當驗證者違反規範時，客戶端是否能正確執行罰沒機制。

    - **最終性檢查（Finality Checks）**：
        >確保共識協議能夠正確確定哪些區塊已被最終化。
---
##### CL 測試的重要性

CL 在 Ethereum 2.0 中負責整個網絡的共識機制。若 CL 客戶端出現錯誤，可能會導致**區塊無法最終化**、**錯誤的區塊被最終化**、**驗證者錯誤行為**，導致資金損失或網絡不穩定。
因此，CL 測試確保 所有 CL 客戶端遵循相同的共識規則，保證以太坊網絡的安全性和穩定性。

<!-- Content_END -->
