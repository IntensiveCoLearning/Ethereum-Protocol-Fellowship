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

### 2025.02.21

#### [SGweek7-dev](https://epf.wiki/#/eps/week7-dev)

今天看 week 7 **Execution client architecture** 的內容，是關於 **Reth**（一個用 Rust 開發的以太坊客戶端）的最新進展、2024 年的發展路線圖，以及未來的可能發展方向。

#### **為什麼要開發 Reth？**
1. **客戶端多樣性**：以太坊需要獨立的客戶端來確保 Staking 的去中心化與安全性。
2. **人才培養**：吸引新開發者參與，以提高 Ethereum 核心協議的可維護性與開發者數量。
3. **擴展能力**：為高 Gas 消耗的 L2 世界設計高效能客戶端。
4. **代碼可擴展性**：以可維護、模組化的方式設計，而非不規則的分叉或 Rebasing。

#### **2024 年目標**
1. **成為 L1 Ethereum 的可靠替代客戶端**
2. **成為最快的 L2 EVM 客戶端**
3. **打造最先進的 EVM 基礎設施開發框架**

#### **目前的進展**
- **開源文化與貢獻**
- **性能測試**
  - 歷史同步速率達 **2-4K mg/s**
  - Tip 狀態同步達 **100-200 mg/s**
- **已完成的里程碑**
  - 與 Ethereum Foundation 進行 Fuzzing 測試
  - L1 Cancun 升級測試完成
  - L2 OP Stack 支持（OP Reth）
  - **完整的 JSON-RPC 支持**（兼容 Geth 和 Parity）
  - **快照同步**：[Merkle.io](https://snapshots.merkle.io)
  - **文檔與開發者支持**：[Reth Docs](https://paradigmxyz.github.io/reth/)

#### **Reth 何時能用於生產環境？**
- **1.0 版本計劃於 2024 年 5 月發布**
- **審計與安全測試**
  - Sigma Prime（Lighthouse 團隊）進行 Reth 審計
  - Revm Fuzzing 測試（Guido Vranken，ETH Bug Bounty 排行第一）

#### **未來開發路線圖**

Reth 的開發將沿三條主線進行：

##### **1. 核心開發：以太坊 L1 的穩健性**
- **Cancun 升級已發布**
- **Electra 升級計劃**
  - **EOF（EVM Object Format）**
  - **Verkle Tries**
  - **Account Abstraction**
- **參與核心開發進程，提供精確的寫作與基準測試**

##### **2. 性能優化：最大化 Gas 處理能力**
- **並行 EVM**：不同場景下的並行執行（歷史同步、實時同步、Builder、Sequencer）
- **JIT/AOT EVM**：使用原生代碼執行，減少解釋器開銷
- **優化狀態提交**：並行計算 state root + 新算法
- **優化數據庫**：考慮替換 MDBX，探索 MonadDB 或基於 Perfect Hash Table 的索引設計
- **系統性優化**：回歸測試與 CI，壓榨最大性能

##### **3. Reth Kernel：構建最先進的 EVM 基礎設施**
- **Node Builder API**：模組化組件，避免 Fork Geth，直接使用 `reth::cli::*`
- **Rust 節點基礎設施**：
  - **Rethhouse**：Reth + Lighthouse（CL+EL）合併為單一二進制文件
  - **Reth + Helios**：輕量客戶端 CL+EL 整合
  - **OP Reth + Helios + Magi**：同時支持 L1、L2
- **應用案例**
  - 測試網 Rollup + 自定義 EIP？

#### **Reth 2.0 – 面向 Rollup 的節點架構**
##### **多 Rollup & 雲端架構**
- **讓 Rollup 節點變得像 BigQuery / Amazon Aurora**
- **多 Rollup 支持**
  - **可同時運行多條 Rollup**（如 `reth node --chains=mainnet,op-mainnet,base-mainnet,zora`）
  - **減少 DevOps 成本，提升可擴展性**
- **多租戶架構**
  - **基於 Actor 模型**
  - **計算與存儲分離，適合雲端部署**
  - **為 Rollup 提供真正的彈性伸縮能力**

### 2025.02.22

#### [SGweek7-research](https://epf.wiki/#/eps/week7-research)

今天看 week 7 介紹了 **Verkle Trees**

#### **1. 動機**
- **有狀態應用的挑戰**
  - 需要下載完整狀態才能驗證區塊，導致同步時間長
  - 目前 Ethereum 全節點需要約 1TiB+300GiB 磁碟空間
  - MPT（Merkle Patricia Tree）數據結構複雜，不利於 zk-friendly 設計
- **轉向無狀態設計**
  - 減少新節點同步狀態的需求
  - 降低硬體需求，使 EL（Execution Layer）客戶端更容易實作
  - 可能允許提升 gas 限制
  - 促進區塊鏈角色的專業化（如分離驗證者與執行者）
- **引入 Execution Witness**
  - 包含執行區塊所需的狀態
  - 包含小型加密證明確保狀態正確性
  - 狀態包括合約程式碼

#### **2. 密碼學**
##### **目前 Ethereum 的狀態樹**
- **Merkle Patricia Tree（MPT）**
- **使用 Keccak 哈希函數**

##### **Verkle Tree 使用的密碼學**
- **向量承諾（Vector Commitments）**
- **內積證明（Inner Product Argument）**
- **多重證明（Multiproof）**
- **EC 群選擇**
  - **Bandersnatch 橢圓曲線**（Banderwagon，移除 cofactor）
  - **標量場（Fr）= 253 bits**，**基數場（Fp）= 255 bits**
  - **無配對運算（No pairings）→ 更高效**
- **與 zk 友好**
  - **Fp 是 BLS12-381 的標量場 Fr**
  - **橢圓曲線計算可作為原生操作執行**

### 2025.02.23

#### [SGweek7-research](https://epf.wiki/#/eps/week7-research)

延續昨天的內容

#### **3. 資料結構**
- **從 Merkle Patricia Tree（MPT）轉換到 Verkle Tree**
  - Verkle Tree = **向量承諾（Vector Commitment）+ Merkle Tree**
- **EIP-6800 提案**
  - **leaf 節點存儲 256 個 32-byte 數值**
  - **帳戶標頭（Account Header）與額外存儲槽**
  - **合約程式碼存儲**
    - **程式碼以 32-byte 塊（Code Chunks）存儲**
    - **Chunk[0] 表示當前塊是否延續前一 PUSHX 指令**
    - **Chunk[1:32] 為對應的程式碼部分**
- **計算樹鍵（Tree Keys）**
  - **不再使用 Keccak**
  - **改用 EC-based 哈希函數（Pedersen hash）**
  - **範例**
    ```plaintext
    TreeKey(address, treeIndex, subIndex) = Commit(2+256*64, address[0:16], address[16:32], treeIndex[0:16], treeIndex[16:32])[0:31] ++ subIndex
    ```
  - **帳戶資訊**
    - 0 = 版本（Version）
    - 1 = 餘額（Balance）
    - 2 = Nonce
    - 3 = CodeHash
    - 4 = CodeSize
  - **存儲槽與程式碼索引**
    - **主存儲計算方式**
      ```plaintext
      pos = MAIN_STORAGE_OFFSET + storage_key
      TreeKey(address, pos / VERKLE_NODE_WIDTH, pos % VERKLE_NODE_WIDTH)
      ```
    - **程式碼塊索引**
      ```plaintext
      chunk_id = CODE_OFFSET + chunk_id
      TreeKey(address, chunk_id / VERKLE_NODE_WIDTH, chunk_id % VERKLE_NODE_WIDTH)
      ```

#### **4. Gas 計算（Gas Accounting, EIP-4762）**
- **狀態大小不再是主要關心點，gas 需考慮 Execution Witness**
- **增加 witness 大小的操作**
  - **讀取狀態**
  - **寫入狀態**
  - **執行合約程式碼**
- **主要 Gas 成本**
  | 操作 | 成本 |
  |------|------|
  | 訪問新樹分支 | 1900 |
  | 訪問 leaf 節點的值 | 200 |
  | 寫入觸發更新 | 3000 |
  | 變更 leaf 節點的值 | 500 |
  | 寫入原本為空的 leaf 節點 | 6200 |

- **這些成本在每筆交易內僅收取一次**
- **重複訪問已存儲的 key，僅收取「暖存取」成本（100 gas）**

### 2025.02.24

#### [SGweek7-research](https://epf.wiki/#/eps/week7-research)

#### **5. 狀態轉換**
- **需要將所有狀態從 MPT 遷移至 VKT**
- **當前提案：Overlay Tree 方法**
  - **分叉點 hfork**
    - **凍結 MPT 狀態**
    - **新寫入進入 Verkle Tree**
    - **每個區塊將 N 個葉子轉換到 Verkle Tree**
  - **數據訪問**
    1. **優先從 Verkle Tree 讀取**
    2. **若 Verkle Tree 無對應值，則回溯至 MPT**
  - **隨時間刪除 MPT 節點**
    - **N = 1K → 6 個月**
    - **N = 5K → 1 個月**
    - **N = 10K → 15 天**

- **挑戰**
  - **重算樹鍵（Tree Keys）需要 pre-images**
  - **許多 EL 客戶端未存儲 Keccak pre-images**
  - **如何確保節點在轉換開始前獲得此資訊？**
  - 參考 HackMD 提案：[vkt-preimage-generation-and-distribution](https://hackmd.io/@jsign/vkt-preimage-generation-and-distribution)

#### **6. Verkle 同步**
- **在區塊 n 進行 Verkle Sync**
- **區塊 n+1 進一步回填（Backfill）數據**
- **逐步遷移到純 Verkle Tree**

### 2025.02.25

#### [SGweek8-dev](https://epf.wiki/#/eps/week8-dev)

今天看 week 8 **Teku 共識層**

#### 1. 簡介
Teku 是 Consensys 開發的以太坊共識層 (CL) 客戶端，專注於機構級質押者，主要特點包括：
- **使用 Java 編寫**
- **強調測試** (單元測試、整合測試、系統測試)
- **詳盡的指標監控** (Prometheus/Grafana)
- **頻繁發布**
- **清晰的日誌**
- **開源、文件完善**
- **內部運行 Teku 進行測試**


#### 2. Teku 架構與 API 設計
Teku 的架構包含多個模組，其中 API 扮演關鍵角色。

##### **2.1 API 設計**
- **Beacon API**：用於與 Beacon 節點交互。
- **Keymanager API**：管理驗證者密鑰。
- **Builder API**：與 Execution Layer (EL) 溝通。
- **安全性設計**：預設僅允許本地主機訪問。
- **TypeDefinition 框架**：提供宣告式接口，SSZ (Simple Serialize) 物件作為型別定義基礎。

##### **2.2 API 示例**
- **PostAttestation** (提交簽名認證到 Beacon 節點)
- **GetBlockRoot** (獲取區塊根)

```java
EndpointMetadata.post("/eth/v1/beacon/pool/attestations")
   .operationId("submitPoolAttestations")
   .summary("提交認證對象到節點")
   .requestBodyType(DeserializableTypeDefinition.listOf(...))
   .response(SC_OK, "認證已接收並廣播")
   .build();
```


#### 3. EIP 原型開發
**EIP (Ethereum Improvement Proposal) 原型開發** 旨在將研究轉化為實際開發。

##### **3.1 例子 - EIP-7251 (增強最大有效餘額)**
- 目標：降低初始罰款，解決 2048 ETH 驗證者可能導致的 4 ETH 吹哨人獎勵問題。
- 調整 **BeaconState** 和相關數據結構。
- 使用 **_features** 目錄跟蹤變更。
- 透過 “丟石頭” 方法發掘潛在問題。

##### **3.2 影響與測試**
- **測試發現問題**：透過“煩人的測試”來找出遺漏點。
- **罕見的 branch 開發**：Teku 通常使用 trunk 開發方式，但 EIP-7251 需要特例處理。


#### 4. 性能優化範例

##### **4.1 Slashing Protection 文件鎖同步優化**
- 之前使用 synchronized:
```java
public synchronized SafeFuture<Boolean> maySignBlock(
final BLSPublicKey validator, final Bytes32 genesisValidatorsRoot, final UInt64 slot)
```
- 新方法透過 **行級鎖定 (row-level locking)** 移除 synchronized。
- 透過 `--validator-is-local-slashing-protection-synchronized-enabled` 開關控制。

### 2025.02.26

#### [SGweek8-research](https://epf.wiki/#/eps/week8-research)

今天看 week 8 關於以太坊的**協議（protocol）**

#### **1. 簡介**
- 2020 年加入以太坊基金會 RIG
- 主要研究方向：
  - **PoS 共識**
  - **EIP-1559 / 費用市場機制**
  - **MEV / 提案者-建設者分離（PBS）**
  - **機制設計**

#### **2. 以協議視角看待以太坊**
##### **2.1 以太坊協議的核心目標**
- 以太坊的運行由**分佈式社群**決定，採取「**粗略共識**」治理模式
- 主要目標：提供**去中心化區塊空間**，讓用戶獲得**最大福利**，並**最小化租金費用**
- **驗證者（Validators）** 負責運行協議

##### **2.2 協議與驗證者的關係**
- 核心挑戰：如何讓驗證者行為符合協議的目標？
- 主要機制：
  - **協議內省（Protocol Introspection）**：透過鏈上狀態獲取環境信號
  - **協議代理（Protocol Agency）**：根據信號調整獎勵與懲罰

#### **3. 區塊生產服務**
- **驗證者** 充當區塊生產者，負責交易排序與打包
- **區塊資源供應受限**，確保低驗證成本
- **動態定價機制**：
  - **EIP-1559**：區塊目標 15M Gas，上限 30M Gas
  - **Gas > 目標值 ⇒ 基礎費（Reserve Price）增加**
  - **EIP-4844**：引入「**數據可用性 Gas（DA Gas）**」供 Rollups 使用（與執行 Gas 分離）

##### **3.1 區塊構建的權限分配**
- **現行模式**：
  - 驗證者可直接構建區塊
- **提案者-建設者分離（PBS）模式**：
  - 驗證者可將區塊構建權**委派給建設者**
  - 透過 MEV-Boost 競標來確保最優區塊選擇

#### **4. 共識服務**
##### **4.1 驗證者的角色**
- **確保鏈的最終性（Casper FFG）**
- **提議區塊（包含共識數據）**
- **選擇區塊鏈頭部（LMD-GHOST）**

##### **4.2 為何要質押（Staking）？**
- **提供可信承諾**：「如果 X 事件發生，Y 億美元將被沒收」
- **質押池（LSP）與 Liquid Staking**
  - 資本希望流動，出現 Lido 等 LSP
  - 協議**無法感知**委託（Delegation）狀況
  - **Rocket Pool** 允許個人質押，並由其他委託者補足剩餘 ETH

#### **5. 包含列表（Inclusion Lists）與審查抵抗**
##### **5.1 什麼是 Inclusion List？**
- **讓最去中心化的以太坊驗證者影響區塊內容**
- 主要提案：
  - **EIP-7547**：引入包含列表
  - **ROP-9**：多重機制抵抗審查
  - **COMIS**（Committee-based Inclusion Sets）：透過委員會強制包含交易

#### **6. 以太坊發行（Issuance）與 Staking 經濟**
- **高發行量 ⇒ 更多人質押 ⇒ 質押池集中化**
- **最新提案**：
  - **Electra Proposal**：調整發行率
  - **Endgame Staking Economics**：設定 ETH 質押範圍
- **「彩虹質押」（Rainbow Staking）**：提升個人質押者的可持續性

### 2025.02.27

#### [SGweek9-dev](https://epf.wiki/#/eps/week9-dev)

今天看 week 9 關於以太坊的**測試**

#### 1. **測試挑戰**
- 需要測試超過 20 種客戶端組合，避免回歸錯誤。
- 不同客戶端的溝通和除錯困難。
- 可靠的測試方式尚不明確，傳統測試側重於單一客戶端。
- 所有未來升級都會繼承這些挑戰。

#### 2. **開發網絡（Devnets）**
- 為以太坊基層的測試鏡像，包含 EL/CL/驗證者。
- 可部署分叉和變更，而不影響主網。
- 提供完全可控的驗證者集，可設計極端測試場景。

#### 3. **當前測試內容**
- Pectra（即將到來的硬分叉）。
- Verkle（未來硬分叉）。
- ILs 和 EIP-7441（Whisk）。
- 以太坊客戶端優化，如 EthereumJS Snap sync 測試、Blob/驗證者限制測試。

#### 4. **本地測試**
- 早期需要完整測試網絡，速度慢。
- 現在使用 **Kurtosis** 來快速迭代測試：
  - 本地可配置（3s slot time、快速分叉、MEV 測試）。
  - 可擴展，支援 Kubernetes/Docker。

#### 5. **MEV 測試**
- 在本地測試最大可提取價值（MEV）。

#### 6. **原型測試**
- **允許所有內容覆寫**，可快速測試協議變更。
- 測試新的客戶端或工具，連接到現有網絡即可驗證效果。

#### 7. **影子分叉（Shadowforks）**
- 可跨所有客戶端測試升級相容性，並模擬真實交易 payload。
- 影子分叉步驟：
  1. 取主網 Genesis 文件，添加分叉時間戳。
  2. 設立新的 Beacon Chain，與 EL 連接。
  3. 在分叉時間點，所有 EL 和 CL 進入新鏈。
  4. 新鏈基於主鏈繼續運行。

#### 8. **推薦工具**
- **Kurtosis**（本地測試環境）。
- **Assertoor**（驗證網絡的各種測試場景）。
- **Forky**（分叉可視化工具）。
- **Tracoor**（區塊追蹤工具）。
- **Dora**（輕量級 Beacon Chain 瀏覽器）。
- **Xatu**（以太坊 P2P 數據收集與可視化）。

### 2025.02.28

#### [SGweek10-dev](https://epf.wiki/#/eps/week10-dev)

今天看 week 10 學習 precompile

#### 1. 什麼是 Precompile？
Precompile（預編譯合約）是以太坊虛擬機（EVM）內部的特殊合約，它們執行特定的加密或數學運算，並且在 EVM 內部以原生方式實現，而不是用 Solidity 或 Vyper 編寫的智能合約。這些合約主要用於提高計算效率，降低 Gas 成本。

#### 2. 為何需要 Precompile？
如果在 Solidity 中純粹用 EVM 指令實現某些運算（例如 Keccak-256 哈希、橢圓曲線簽名驗證），計算成本非常高。因此，以太坊提供了一組內建 Precompile 來加速這類操作，使其比傳統的智能合約實現更高效。

#### 3. 主要 Precompile 合約（地址 0x01 - 0x0A）
以太坊目前定義了一些標準的 Precompile，地址範圍為 `0x01` 至 `0x0A`，每個 Precompile 都有特定功能。

| 地址  | Precompile 名稱 | 功能 |
|--------|----------------|----------------|
| 0x01   | `ecrecover`    | 用於橢圓曲線數字簽名恢復（ECDSA） |
| 0x02   | `sha256`       | 計算 SHA-256 雜湊 |
| 0x03   | `ripemd160`    | 計算 RIPEMD-160 雜湊 |
| 0x04   | `identity`     | 簡單的身份函數，直接返回輸入數據 |
| 0x05   | `modexp`       | 進行模指數運算（Modular Exponentiation） |
| 0x06   | `bn256Add`     | BN256 曲線上的點加運算 |
| 0x07   | `bn256ScalarMul` | BN256 曲線上的標量乘運算 |
| 0x08   | `bn256Pairing` | BN256 雙線性配對檢查 |
| 0x09   | `blake2f`      | Blake2 雜湊函數 |
| 0x0A   | `curve25519`   | Curve25519 橢圓曲線運算（EIP-2537） |

#### 4. Precompile 的 Gas 計算
Precompile 的 Gas 費用通常根據輸入數據長度和計算複雜度來確定。例如：
- `ecrecover` 固定消耗 3000 Gas。
- `sha256` 根據數據長度收費，每 32 字節收取 12 Gas。
- `modexp` 依據底數、指數和模數長度計算 Gas 費用，根據 EIP-198 進行優化。

#### 5. Precompile 的擴展與 EIP
除了以太坊主網內建的 Precompile，不同的 EIP 提議新增 Precompile 來提升計算能力，例如：
- **EIP-196 / EIP-197**: 引入 BN256 橢圓曲線的點加、標量乘與配對檢查。
- **EIP-198**: 優化模指數運算，提高 RSA 驗證效率。
- **EIP-2537**: 添加 BLS12-381 曲線，用於 ZK-SNARKs。

#### 6. 應用場景
Precompile 主要應用於以下領域：
- **數字簽名驗證**：`ecrecover` 被廣泛用於驗證交易簽名。
- **跨鏈橋與 ZK-SNARKs**：BN256、BLS12-381 相關 Precompile 用於零知識證明計算。
- **高效加密哈希**：`sha256`、`ripemd160`、`blake2f` 提供高效的加密哈希運算。

#### 7. 結論
Precompile 提供了高效的數學與加密運算，降低 Gas 成本，使智能合約能夠執行複雜運算而不會消耗過多資源。未來，隨著 Layer 2 方案和 zk-SNARKs 的發展，新的 Precompile 可能會繼續加入以提升以太坊的計算能力。

### 2025.03.01

#### [SGweek10-research](https://epf.wiki/#/eps/week10-research)

今天看 week 10 學習 Gasper 共識機制與改進方案

#### 1. Gasper 共識機制回顧
Gasper 是 LMD-GHOST 和 Casper-FFG 的結合，作為以太坊共識機制的一部分。
- **LMD-GHOST (Latest Message Driven - Greediest Heaviest Observed SubTree)**：
  - 依照最新的訊息進行權重計算，選擇最重的子樹作為主鏈。
- **Casper-FFG (Friendly Finality Gadget)**：
  - 用於提供最終性 (finality)，透過投票機制確保區塊不會被重組 (reorg)。


#### 2. LMD-GHOST 的問題
- **簡單的 ex-ante reorg** (先驗重組攻擊)
  - 惡意節點可以隱藏區塊和部分驗證人投票，導致誠實節點不知情地在舊鏈上繼續挖掘。
  - 當惡意節點釋出隱藏的區塊與投票時，誠實節點會轉而支持這條鏈，導致原本的誠實鏈被重組。
- **提案者增益 (Proposer Boost)**
  - 新區塊在提出時獲得額外 40% 權重，以減少重組攻擊風險。
  - 但若攻擊者控制多個連續提案者，仍能成功發動攻擊。


#### 3. Casper-FFG 與最終性
- 以太坊目前的共識機制透過 Casper-FFG 在 32 個 slot 內進行一次完整投票，確保區塊的最終性。
- **問題**：
  - 當網路同步性變差時，誠實節點可能會受到惡意節點操控，導致最終性確認受到影響。


#### 4. 改進方案
##### (1) **RLMD-GHOST (Recent LMD-GHOST)**
- **主要改進**：
  - **View-Merge**：
    - 讓所有誠實驗證人在下一輪投票前“凍結”當前視圖，防止惡意節點突然釋出隱藏投票。
  - **移除 Committees**：
    - 讓所有誠實驗證人每個 slot 都能投票，確保誠實鏈不會被重組。
  - **投票過期機制 (Vote Expiry)**：
    - 限制歷史投票的影響，確保投票權重隨時間降低，以防止長期攻擊。

##### (2) **SSF 協議 (Single Slot Finality Protocol)**
- **目標**：
  - 在單個 slot 內提供區塊的快速確認 (fast confirmation)。
- **機制**：
  - 若某個區塊獲得 2/3 驗證人投票，則所有誠實節點都會視其為最終確認的區塊。
  - 減少最終性確認所需的時間，提高交易安全性。

##### (3) **ePBS (Enshrined Proposer-Builder Separation)**
- **目標**：
  - 減少區塊提案者 (proposer) 和構建者 (builder) 之間的影響，提高 MEV 抑制能力。
- **挑戰**：
  - ePBS 可能會增加惡意節點發動 ex-ante reorg 攻擊的可能性。
  - 需要搭配 PTC (Payload Timeliness Committee) 機制，確保區塊 payload 及時發佈。

##### (4) **PeerDAS (Data Availability Sampling)**
- **目標**：
  - 減少全節點 (full nodes) 需要下載的數據量，透過抽樣驗證區塊數據的可用性。
- **機制**：
  - 透過抽樣檢查 50% 以上的數據是否可用，以確保整個區塊數據的可用性。
  - 在 fork-choice 規則中加入數據可用性檢查，以防止無法獲取完整數據的區塊成為主鏈的一部分。


#### 5. 以太坊未來發展方向
- **SSF 協議**：
  - 確保快速交易確認，降低交易延遲。
  - 提高 L2 (Layer 2) 互通性，加速跨鏈資產轉移。
- **ePBS (強化 MEV 控制)**：
  - 減少 MEV (最大可提取價值) 濫用，確保區塊提案機制的公平性。
- **PeerDAS (去中心化數據可用性)**：
  - 允許輕量級節點參與共識，提高整體系統安全性。

<!-- Content_END -->
