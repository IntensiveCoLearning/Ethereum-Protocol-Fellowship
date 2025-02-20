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

### 2025.02.15

#### [SGweek5](https://epf.wiki/#/eps/week5)

### 關於以太坊的發展

### 1. 以太坊發展階段概覽
- 以太坊的技術升級主要分為六個階段，目標是提升可擴展性、安全性和可用性。

#### 1.1 Merge
- 以太坊從 PoW 轉向 PoS。
- 提高能源效率，減少碳足跡。
- 增強網絡安全性，降低 51% 攻擊風險。

#### 1.2 Surge
- 主要目標是提升 L2 Rollup 的數據可用性。
- **關鍵技術**：EIP-4844（Blobspace）
  - 允許節點處理較大數據區塊（Blob），提高擴展能力。
  - 未來支持資料可用性抽樣（DAS）。

#### 1.3 Scourge
- 目標是減少 MEV 對網絡的負面影響。
- **關鍵技術**：
  - **提案者與建設者分離（PBS）**：防止 MEV 對驗證者的影響。
  - **MEV Boost**：目前通過第三方中介處理。
  - **Enshrined PBS**：計劃內建到協議中。
  - **Inclusion lists**：確保交易不會被過度審查。

#### 1.4 Verge
- 簡化驗證者驗證區塊的過程。
- **關鍵技術**：
  - **Verkle 樹** 取代 Merkle 樹，使驗證更高效。
  - **Stateless Clients**（無狀態客戶端）：減少節點存儲需求。

#### 1.5 Purge
- 目標是減少以太坊的歷史和狀態數據存儲。
- **關鍵技術**：
  - **EIP-4444**：自動修剪一年以上的歷史數據。
  - **狀態過期**：計劃刪除舊狀態，減少節點存儲負擔。

#### 1.6 Splurge
- 各種優化與新技術。
- **EVM 改進**（EVM Object Format，EOF）。
- **帳戶抽象（Account Abstraction）**：
  - EIP-3074 允許 EOA（Externally Owned Account）授權智能合約。
  - ERC-4337 支持標準化智能錢包功能。

---

### 2. 以太坊技術詳解

#### 2.1 信標鏈（Beacon Chain）
- PoS 機制的核心。
- **同步委員會（Sync Committee）**：
  - 每 256 個 epoch（約 27 小時）輪換一次。
  - 僅需驗證 512 個簽名，而非約 100 萬個，提高效率。
  - 參考 a16z 的 Helios 輕客戶端。

#### 2.2 單 Slot 最終性（Single Slot Finality, SSF）
- 從當前的 12.6 分鐘縮短至 12 秒。
- 主要挑戰：需要處理大量簽名。
- 解決方案：
  - **減少驗證者數量**（如 MaxEB 機制）。
  - **改進簽名聚合技術**。

#### 2.3 量子抗性技術
- 目前以 KZG 承諾方案進行數據可用性抽樣（Data Availability Sampling, DAS）。
- 計劃用 **STARKs 或 Lattice-based 方案** 替代 KZG，以增強抗量子攻擊能力。

#### 2.4 Rollup 方案
- 以太坊採用 **Rollup-centric roadmap** 來提升可擴展性。
- **Optimistic Rollup**
  - 假設所有交易都是正確的。
  - 依賴 **欺詐證明（Fraud Proof）** 來檢測惡意行為。
- **Zero-Knowledge Rollup（ZK Rollup）**
  - 使用 **有效性證明（Validity Proof）** 保證交易正確性。
  - 短證明可由 L1 驗證，提高安全性。

#### 2.5 提案者與建設者分離（PBS）
- 目前由 **MEV Boost** 完成，未來將內建到協議中。
- **Execution Tickets**（執行票）機制：
  - 允許驗證者預先競標出塊權。
  - 減少 MEV 對區塊提案者的影響。

#### 2.6 Verkle 樹
- **與 Merkle 樹的不同點**
  - Verkle 樹使用 **多項式承諾（Polynomial Commitment）**，而非哈希函數。
  - 驗證時只需較少數據，減少同步時間。
  - 可支持 **無狀態驗證者（Stateless Validators）**。

#### 2.7 EVM 改進
- **EVM Object Format（EOF）**
  - 重新設計 EVM 執行方式，提升升級靈活性。
- **帳戶抽象（Account Abstraction）**
  - 透過 EIP-3074 和 ERC-4337，提升智能合約錢包的可用性。

---

### 3. 未來技術研究方向

#### 3.1 深層加密（Deep Crypto）
- **完全同態加密（Fully Homomorphic Encryption, FHE）**
  - 支持加密狀態下的計算，提升隱私性。
- **可驗證延遲函數（Verifiable Delay Functions, VDF）**
  - 確保隨機性無法被提前計算，提高安全性。

#### 3.2 加密 Mempool
- 交易不公開，減少 MEV 對用戶的不利影響。
- 防止搶跑交易（Front-running）。

#### 3.3 Multi-dimensional EIP-1559
- 當前的 **EIP-1559** 只針對 gas 費，未來計劃擴展到其他資源（如存儲、狀態讀取等）。

### 2025.02.16

今天看其他人整理的筆記作為複習。

### 2025.02.17

#### [SGweek6-dev](https://epf.wiki/#/eps/week6-dev)

今天看 week 6 **Ethereum Consensus Layer Pyspec**（可執行的共識規範）的內容。 

#### **1. Pyspec 是什麼？**
- Ethereum 核心共識規範
- 可執行且可驗證
- 測試向量生成器：提供 CL 客戶端測試其行為是否符合規範

Pyspec 定義了運行在 CL 客戶端的共識協議，並能產生測試向量，讓 CL 客戶端測試自己的共識規則。

#### **2. Pyspec 的結構**
[Pyspec 的 code](https://github.com/ethereum/consensus-specs)

- **目錄結構（如何閱讀 Pyspec）**：
```
/specs/
 ├── _features/  # WIP（待開發）功能
 │   ├── eip6110
 │   ├── ...
 ├── altair/
 ├── bellatrix/
 ├── capella/
 ├── deneb/
 ├── phase0/
```
這些文件涵蓋 Ethereum 各個階段的升級，這些 Markdown 文件會透過 SpecBuilder 轉換為 Python 文件，形成可執行的 Pyspec 程式碼。

#### **3. Pyspec 的核心概念**
##### **(1) SSZ 容器（SSZ Containers）**
Pyspec 使用 **SSZ（Simple Serialize）** 來表示共識對象的數據結構，在 Ethereum 共識層中，SSZ **哈希樹根（hash tree root）** 用於生成對象的唯一摘要。

##### **(2) 狀態轉換函數（State Transition Function）**
Pyspec 使用純函數來處理狀態轉換：
```python
post_state = state_transition(pre_state, block)
```
這意味著 **輸入相同，輸出就一定相同**，便於測試和驗證。

#### **4. 總結**
- Pyspec 是 Ethereum 共識層的核心規範，可用來執行、驗證及測試。
- 安裝後可用 Python 執行測試案例，確保狀態轉換符合規範。
- 開發者可參與 Pyspec 貢獻，甚至尋找漏洞來參與 Bug Bounty。

### 2025.02.18

#### [SGweek6-dev](https://epf.wiki/#/eps/week6-dev)

今天看 week 6 **Ethereum Execution Layer
Specification**的內容。

#### **1. 簡介**
**EELS（Ethereum Execution Layer Specification）**
- 以 Python 方式實作 Ethereum Execution Layer，作為 Yellow Paper 的後繼版本。
- 由 Consensys 的 Quilt 團隊於 2021 年 5 月創建，後由 Ethereum Foundation 維護。
- 目標是讓 Ethereum 內部運作更容易被程式設計師理解，並提供可測試的規範。

#### **2. Yellow Paper（以太坊黃皮書）**
**歷史背景**
- 2014 年由 Gavin Wood 創建，採用 CC-BY-SA 4.0 授權。
- 是 Ethereum 的技術規範，但對程式設計師而言難以理解。

**內容涵蓋**
- 區塊鏈架構
- 分叉選擇（Fork Choice）
- 狀態（State）
- 交易（Transaction）
- 區塊（Block）
- 其他技術（Gas、合約、EVM、RLP、MPT、預編譯合約、EVM 指令等）

**Yellow Paper 的問題**
- **不易讀**：大多數程式設計師難以理解。
- **無法測試**：規範以人類語言描述，無法直接用來測試。
- **與 EIP 不匹配**：許多核心 EIP 並未使用 Yellow Paper 的數學記法。

**Yellow Paper 的優勢**
- **簡潔**
- **形式化**
- **與演算法無關**

#### **3. EELS（Ethereum Execution Layer Specification）**
**為何需要 EELS？**
- Yellow Paper 難以理解，EELS 提供更友善的 Python 版本。
- Yellow Paper 只提供過去的狀態，EELS 提供當前 Ethereum Execution Layer 的完整規範。
- 讓 Ethereum 的規範同時可以用來進行自動化測試。

**EELS 的架構**
- **Forks**
- **區塊鏈（Blockchain）**
- **分叉選擇（Fork Choice）**（EELS 假設僅接收 canonical chain）
- **狀態（State）**
- **交易（Transaction）**
- **區塊（Block）**

**EELS 的問題**
- **需要 Python 知識**
- **包含具體演算法選擇**（不像 Yellow Paper 一樣抽象）
- **較冗長**
- **對學術界不夠友好**

**EELS 的優勢**
- **對程式設計師更友善**（用 Python 撰寫，EIP 也開始使用 Python 風格的偽代碼）
- **可維護性強**（任何會寫 Python 的人都可以閱讀和維護）
- **可測試性強**（可以同步鏈，通過 ethereum/tests 測試）

#### **4. EELS 的創新**
**1. 變更比較（Diffs）**
- 追蹤 Ethereum 版本變更，並用程式碼來描述更新內容。

**2. 模糊測試（Fuzzing）**
- 產生隨機輸入並與其他 Ethereum 客戶端比較輸出，確保正確性。

### 2025.02.19

#### [SGweek6-research](https://epf.wiki/#/eps/week6-research)

今天看 week 6 **Sharding and Data
Availability Sampling**的內容。

#### 1. 區塊鏈擴展性三難困境（Scalability Trilemma）
- 設計區塊鏈時，通常需要在 **擴展性（Scalability）、安全性（Security）、去中心化（Decentralization）** 之間權衡。
- 目前的區塊鏈架構包括：
  - **執行層（Execution）**
  - **結算層（Settlement）**
  - **數據可用性層（Data Availability）**
  - **共識層（Consensus）**

#### 2. 數據可用性問題（Data Availability Problem）
- **定義**：確保數據已發布且不可被任何節點（即使是超級多數節點）隱藏或丟棄。
- 目前傳統解法：
  - **所有全節點（Full Node）下載所有數據**
  - 缺點：影響可擴展性，數據量過大
- 可擴展的數據可用性解法需要減少下載的數據量（如常數或對數級的工作量）

#### 3. 數據可用性取樣（Data Availability Sampling, DAS）
- **核心概念**：節點只隨機取樣部分數據來檢查區塊是否可用。
- **問題**：
  - 假設客戶端取樣 10% 的數據，若區塊生產者隱藏了一筆交易，則只有 10% 的機率能檢測到問題，這仍然太低。
  - 需要更高效的驗證方式。

#### 4. 糾刪碼（Erasure Coding）
- **方法**：使用 Reed-Solomon 編碼進行數據擴展，生成額外的冗餘數據。
- **優勢**：即使 50% 的原始數據遺失，仍可透過剩餘數據重建完整內容。
- **驗證方式**：
  - 採用 KZG 承諾（KZG Commitments）
  - 確保數據在同一多項式上（避免惡意篡改）

#### 5. Danksharding 方案
- **機制**：
  - 透過分離「提議者（Proposer）」與「建構者（Builder）」角色，優化區塊生成。
  - 採用 KZG 2D 方案，透過行列驗證確保數據可用性。
  - 75% 可用性以下的區塊會自動失敗。
  - 若有遺失數據，驗證者會重建缺失部分，確保數據完整。

#### 6. 以太坊提案 EIP-4844（Proto-Danksharding）
- **目標**：透過數據 Blob 來提升數據可用性並降低成本。
- **特色**：
  - Blob 與執行層分離，定價獨立。
  - Blob 不是狀態計算的一部分，只會短期存儲。
  - 未來可透過網絡升級（如引入糾刪碼）進一步提升擴展性。

#### 7. 研究未來展望
- **短期**：EIP-4844 將作為 Proto-Danksharding 的基礎，提供過渡解決方案。
- **中期**：引入糾刪碼，增強 DAS 的效率。
- **長期**：全面實施 Danksharding，最終實現高效、低成本的數據可用性方案。

### 2025.02.20

昨天參加了 ETHTaipei的活動，當中介紹了以 EIP-7702 為主將在 Pectra 升級啟用的 EIP，EIP-7702 實現了 AA 錢包，在 EOA 的 code 欄位存了一個 pointer 指向 SCA，能同時擁有 EOA 和 SCA 的優點，分別是 **EOA 能發起交易**、**SCA 能執行 smart contract**。

<!-- Content_END -->
