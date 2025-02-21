---
timezone: Asia/Shanghai
---

# Zaki

1. 自我介绍
    - Hi我是Zaki，這是第1次參加共學，大家一起努力！
2. 你认为你会完成本次残酷学习吗？
    - Let's go!!!!

## Notes

<!-- Content_START -->

### 2025.02.06

“Heroes are heroes because they are heroic in behavior, not because they won or lost.”
— Nicholas Taleb

## Prehistory

- 在 prehistory 的第一張及介紹了 Ethereum 的的起源和願景 並且從 1969 年冷戰時的 ARPANET 開始介紹，從此之後網路迅速的擴張，到目前已經是幾十億人在使用了。

- 接著是 UNIX 的起源了，不得不說到的事兩位偉大的人物，Ken Thompson 和 Dennis Ritchie，Dennis Ritchie 也可稱它為 dmr，他也早一步在 2011 年時離開了，這兩位為了未來的資訊世界發展可說是最重要並且沒有之一呀，後續 Thompson 也前往了 google 並發明了 go 語言，後續就不多說了([wiki](https://zh.wikipedia.org/zh-tw/%E8%82%AF%C2%B7%E6%B1%A4%E6%99%AE%E9%80%8A))。在 UNIX 中，帶入了像是分層系統，shell 等等的功能與概念，讓未來的資訊系統世界打好良好的網路基礎設施概念，以下簡單的解釋這些概念。

### **Unix 的階層式檔案系統（Hierarchical File System）**

Unix 採用 **階層式檔案系統（Hierarchical File System, HFS）**，這是一種樹狀結構的目錄系統，所有的檔案和目錄都從 **根目錄（`/`）** 開始，逐層向下展開。

📂 **主要概念**：

1. **根目錄 `/`**：Unix 檔案系統的最頂層，一切皆從 `/` 開始。
2. **標準目錄**：
   - `/bin`（Binary）：基本可執行程式，如 `ls`、`cp`、`mkdir`。
   - `/home`：使用者的家目錄（如 `/home/user`）。
   - `/etc`：系統設定檔，如 `/etc/passwd`（使用者帳號資訊）。
   - `/var`：動態資料，如 `/var/log`（系統日誌）。
   - `/tmp`：暫存檔案（開機後可能被刪除）。
3. **絕對路徑 & 相對路徑**：
   - **絕對路徑**：從根目錄 `/` 開始，例如 `/home/user/file.txt`。
   - **相對路徑**：相對於當前目錄，例如 `./file.txt`。
4. **檔案與目錄權限**：
   - 使用 ls -l 可查看權限（`rwxr-xr-x` 代表擁有者可讀寫執行，其他人只能讀取和執行）。

---

### **Shell 作為命令列介面（Shell as a Command-Line Interface）**

**Shell** 是 Unix/Linux 的命令列介面（CLI），用來與作業系統互動。常見的 shell 包括：

- **Bash（Bourne Again Shell）**：預設於大多數 Linux 發行版。
- **Zsh（Z Shell）**：功能更強大，許多 macOS 使用者選擇使用。
- **Fish（Friendly Interactive Shell）**：強調易用性與自動補全。

📌 **常見的 Shell 操作**：

- `pwd`：顯示當前路徑。
- `ls`：列出目錄內容（`ls -l` 顯示詳細資訊）。
- `cd /path/to/dir`：切換目錄。
- `cp source destination`：複製檔案或目錄。
- `mv old_name new_name`：移動或重新命名檔案。
- rm file / `rm -r dir`：刪除檔案或目錄（⚠️ 小心使用）。

---

### **單一用途的 Unix 工具（Single-Purpose Utilities）與組合使用**

Unix 遵循 **「一個程式只做一件事，並且做得好」** 的設計哲學，許多工具都是單一用途，但可以透過 **管線（`|`）** 和 **重導向（`>`、`>>`、`<`）** 組合來完成更複雜的任務。

📌 **常見 Unix 工具**：
| 指令 | 功能 |
|------|------|
| cat file | 顯示檔案內容 |
| grep "keyword" file | 搜尋檔案中的關鍵字 |
| sort file | 對檔案內容排序 |
| uniq file | 移除重複行 |
| wc -l file | 計算行數 |
| head -n 10 file | 顯示前 10 行 |
| tail -n 10 file | 顯示最後 10 行 |
| cut -d',' -f2 file.csv | 擷取 CSV 第二欄 |
| awk '{print $1}' file | 取出第一欄 |
| sed 's/old/new/g' file | 文字取代 |
| find /path -name "*.txt" | 在指定路徑尋找檔案 |
| xargs | 接收輸入並執行指令 |

---

- 在那個充滿阿諛我詐的戰爭時代中，資訊網路是一大通訊的利器，但是在戰爭中就有敵對的一方，讓對方知道了了傳輸資料是一件危險的事情，這時加密與解密就是相當重要的技術了，這時我們相當熟悉的電影模仿遊戲中的主角圖靈 Alan Turing 在其中也扮演了相當重要的角色，在此之後密碼學也迎來快速的發展。
  - 1974 年，Ralph Merkle 提出了 Merkle’s Puzzles，這是一種讓雙方在沒有共同秘密的情況下交換訊息並建立共享密鑰的方法。
  - 1976 年，Whitfield Diffie 和 Martin Hellman 受 Merkle 的研究啟發，發表了 **「New Directions in Cryptography」**（密碼學新方向）論文，並提出了 Diffie–Hellman 密鑰交換算法，這標誌著「無需信任的加密技術」的誕生。
  - 1977 年，Ron Rivest、Adi Shamir 和 Leonard Adleman 發明了 RSA 加密系統，這是第一個可行的公鑰密碼學實作，並在論文《A Method for Obtaining Digital Signatures and Public-Key Cryptosystems》中發表。
  - 1977 年，數學家 Martin Gardner 在《Scientific American》雜誌上介紹了 RSA-129 加密挑戰，並懸賞 $100 獎勵破解者。
  - 1994 年，一組科學家與志願者成功破解 RSA-129，並將獎金捐給自由軟體基金會，證明了「加密的完美安全性只是一種幻覺」，因為密碼技術需不斷進化來應對新威脅（如量子計算機）。
  - 現代 RSA 加密（1024 至 4096 位元）成為網路安全的基礎，保護金融交易，促進電子商務與網路銀行的發展。
- 在過去 code 是相當自由的存在，會刊登在報紙上讓每個人都能有反饋，想當初小時候都會拿報紙上的數讀在解，現在的小孩應該都沒有這種回憶了。在過去 IBM 可說是壟斷了計算機這塊的市場，在 1969 年美國的反壟斷訴訟打開了軟體必須綁定硬體的鎖鏈，接著的開源大戰也開打，從 Unix 的收費到微軟大大 Bill Gates 停止共用 BASIC source code，GNU 也因此從 Richard Stallman 的手上催生了，接著的網路世界也慢慢到我們熟知的 Linus Torvalds 開發的 kernel 奠定了未來軟體開發的藍圖。
- 講回在 WW2 結束時，各國對於密碼學的控制，美國也將此列入管制，不外乎於當時的國家安全局 NAS，當時 MIT 所發表的 RSA 一度被列為機密，後續也因為此，被公共強烈的批評，政府試圖削弱密碼學的行為被視為監控公民通信的手段，但是密碼學的研究仍在持續發展。後續在許多的密碼學家的推動下，cyberpunks 也快速地被推動著，這場運動 最終推動了去中心化數位貨幣的誕生，為後來的區塊鏈與比特幣奠定了理論基礎。
- 資訊世界快速的發展下，在 1990 年時 David Chaum 推出 DigiCash，嘗試建立匿名數位支付系統，提供隱私保護。然而，由於過於依賴傳統金融機構，最終於 1998 年破產，未能普及， Wei Dai 的 B-money 和 Nick Szabo 的 BitGold 都試圖解決數位貨幣的去中心化問題，但當時技術條件尚未成熟，未能廣泛應用，這些理念影響了 2008 年比特幣（Bitcoin）的誕生，中本聰（Satoshi Nakamoto）在白皮書中提出了區塊鏈技術，成功實現了真正的去中心化數位貨幣。
- 2008 年，中本聰（Satoshi Nakamoto）提出了比特幣，去中心化的電子現金系統，並且不依賴任何中心化的發行機構或資產作為支持，比特幣使用區塊鏈技術來確保交易的安全性和順序，並且可以在沒有銀行或中介機構的情況下進行交易，不僅是一種數字貨幣，還是一個社會經濟實驗，利用了「POW」機制，允許在無需中央控制的情況下達成交易順序的共識，但其網路也顯示出某些局限性，尤其是在應用開發方面，許多嘗試在比特幣區塊鏈上構建的應用由於網路擴展性差，變得非常複雜且不易擴展。
- 2012 年，Vitalik Buterin 和 Mihai Alisie 創辦了 Bitcoin Magazine，Vitalik 很快發現比特幣的局限性，並提出了一個可以支持各種金融應用的平臺構想，在 Gavin Wood 的協助下，乙太坊（Ethereum）的設計得到了正式確立，並開始著手建設一個去中心化的世界電腦，這個平台不僅支持數字貨幣交易，還能運行智能合約和去中心化應用（DApps），2015 年 7 月 30 日，乙太坊正式啟動，成為一個致力於建立自我主權經濟的平臺，也利用數字貨幣建立更為開放和自由的經濟體系，到目前為止市值已超過 $400 billion 美元，為非常重要的區塊鏈平台之一。



### 2025.02.07

## Architecture

以太坊的協議架構經過多年的演進，目前分為兩個主要部分：**執行層（Execution Layer, EL）**和**共識層（Consensus Layer, CL）**。這兩個層次分別負責不同的功能，並通過定義好的 API 進行互動。以下是對其架構和流程的詳細說明。

---

#### 1. **執行層（Execution Layer, EL）**
   - **功能**：負責處理實際的交易和用戶互動，執行智能合約，並維護區塊鏈的狀態（State）。
   - **核心元件**：
     - **EVM（以太坊虛擬機）**：執行智能合約的環境。
     - **交易池（TXs/newpool）**：存儲待處理的交易。
     - **State（狀態數據）**：區塊鏈的當前狀態。
     - **JSON-RPC**：提供與外部應用程序（如 Web3）的接口。
   - **p2p 網路**：使用 **devp2p** 協議與其他 EL 節點通信，傳輸交易和區塊數據。

#### 2. **共識層（Consensus Layer, CL）**
   - **功能**：提供權益證明（Proof-of-Stake, PoS）共識機制，確保所有節點遵循同一條鏈，並驅動執行層的規範鏈（Canonical Chain）。
   - **核心元件**：
     - **RANDAO**：隨機數生成機制，用於選擇驗證者。
     - **LMD-GHOST**：分叉選擇算法，決定哪條鏈是有效的。
     - **Beacon APIs**：與信標鏈（Beacon Chain）相關的接口。
     - **Validators（驗證者）**：負責驗證區塊和交易的節點。
   - **p2p 網路**：使用 **libp2p** 協議與其他 CL 節點通信，傳輸共識相關數據（如見證 Attestation）。


![image](https://github.com/user-attachments/assets/73d6c77d-069b-4f1f-a053-d87a84860668)

---

### **Eth 1.0 與 Eth 2.0 的共識機制比較**

#### 1. **Eth 1.0（PoW 機制）**
   - **共識機制**：工作量證明（Proof-of-Work, PoW）和分叉選擇規則（Fork Choice Rule）。
   - **流程**：
     1. 節點收到新區塊後，驗證 PoW 的有效性。
     2. 比較新鏈的累積工作量（Work），選擇工作量最高的鏈。
     3. 執行並驗證區塊中的交易，確保交易有效。
   - **特點**：PoW、分叉選擇和交易驗證是綁定在一起的（如 Geth 客戶端）。


![image](https://github.com/user-attachments/assets/1255ae31-c972-42a0-8ef4-4952fd0db185)

#### 2. **Eth 2.0（PoS 機制）**
   - **共識機制**：權益證明（Proof-of-Stake, PoS）和分叉選擇規則。
   - **流程**：
     1. 節點收到新區塊後，驗證 PoS 的有效性。
     2. 根據驗證者的見證（Attestation）數量決定區塊的權重，選擇權重最高的鏈。
     3. 執行並驗證區塊中的交易，確保交易有效。
   - **特點**：PoS 和分叉選擇由 CL 處理，交易驗證由 EL 處理。


![image](https://github.com/user-attachments/assets/8231039a-8770-44aa-b416-2671db6926d6)

---

### **CL 與 EL 的互動流程**

1. **區塊提案與驗證**：
   - 當 CL 收到新區塊時，會將區塊中的 EL 相關內容（如交易）通過 **Engine API** 發送給 EL。
   - EL 驗證交易的有效性，並將結果返回給 CL。
   - 如果交易有效且符合 CL 的分叉選擇規則，CL 會通知 EL 更新狀態。

2. **狀態更新**：
   - CL 決定哪條鏈是最長鏈後，會通知 EL 套用該區塊中的交易，並計算最新的狀態（State）。
   - EL 更新狀態後，將結果返回給 CL。

3. **區塊生成**：
   - 如果 CL 節點是驗證者並需要提案區塊，它會請求 EL 生成 EL 區塊（包含 EVM 交易）。
   - CL 自己生成 CL 區塊（包含驗證者的見證 Attestation）。
  
   
![image](https://github.com/user-attachments/assets/39745d7a-4f42-4eb4-8ecd-a83a252c67ae)

---

### **CL 與 EL 的獨立性**

- **開發者互動**：
  - 開發者通過 **web3.eth** 與 EL 互動（如查詢交易、狀態）。
  - 通過 **web3.beacon** 與 CL 互動（如查詢共識相關數據）。
- **p2p 網路**：
  - EL 使用 **devp2p** 網路（Eth 1.0 的 p2p 協議）。
  - CL 使用 **libp2p** 網路（Eth 2.0 的 p2p 協議）。
![image](https://github.com/user-attachments/assets/0ef94e96-7ab4-407a-8308-cc5f19433806)

![image](https://github.com/user-attachments/assets/e8b9b431-c674-436d-932e-32a30c915014)

在合併前，以太坊的執行層和共識層是獨立運行的，所有交易和區塊驗證都由執行層完成，並依賴 PoW 共識機制。

自 2020 年 12 月起，共識層（信標鏈）開始運行，採用 PoS 共識，並協調驗證者（Validator）。

合併後，以太坊正式轉向 PoS，執行層負責交易處理，共識層負責驗證區塊，兩者需協同運作。
![image](https://github.com/user-attachments/assets/6e7352fe-74bc-41d5-bcb9-ad9cf61f4164)

參考：

[Eth 2.0 的共識層和執行層分工及 The Merge 影響](https://medium.com/taipei-ethereum-meetup/eth-2-0-cl-el-separation-and-impact-of-the-merge-dbeb6828c907)

[如何跑起以太坊執行層與共識層客戶端](https://medium.com/swf-lab/%E5%A6%82%E4%BD%95%E8%B7%91%E8%B5%B7%E4%BB%A5%E5%A4%AA%E5%9D%8A%E5%9F%B7%E8%A1%8C%E5%B1%A4%E8%88%87%E5%85%B1%E8%AD%98%E5%B1%A4%E5%AE%A2%E6%88%B6%E7%AB%AF-54d0b472e7ac)

### 2025.02.08

在 Ethereum 協議設計中，有兩個特別的設計原則值得關注：**Modularity** 和 **Non-discriminant**。

#### **1. Modularity**
Modularity 使得 Ethereum 協議能夠靈活適應未來的技術變革。這種設計哲學意味著 Ethereum 的核心協議應當是高度模組化的，使開發者能夠在不影響整個應用堆疊的情況下進行局部修改。

- **靈活升級**：Ethereum 持續進行研究與工程改進，模組化架構允許開發者針對特定部分進行優化，而不會影響整體系統運作。例如 Proto-Danksharding 的引入，為 Layer 2 擴展提供了靈活的構建模組。
- **獨立性與可重用性**：許多 Ethereum 內部的技術創新，如 Dagger、Patricia Trees 和 SSZ，都被設計為獨立的庫，即使 Ethereum 本身不使用其中的某些功能，它們仍然可以被其他協議採用。
- **封裝複雜性**：Ethereum 的架構由多個子系統組成，每個子系統內部可能相當複雜，但對外提供的是高級接口，讓開發者能夠輕鬆組裝和調試不同的組件，提高開發效率與系統穩定性。

#### **2. Non-discriminant**
Ethereum 的設計哲學源自 FOSS（自由與開源軟體）和 Cypherpunk 運動，強調開放與去中心化，在協議本身對於應用場景的中立性：

- **無審查**：Ethereum 不會主動限制特定類型的應用，任何人都可以在協議之上部署智能合約，只要它們遵循協議規則。
- **關注協議本身的穩定性**：Ethereum 內部的調控機制僅針對協議的安全性與穩定性，而不會基於價值判斷來限制某些應用。例如，理論上，你可以在 Ethereum 上運行一個無限迴圈的腳本，只要你願意支付計算步驟所需的交易費用，並且不超過協議允許的 Gas 限制。
- **去中心化精神**：這種設計確保 Ethereum 平台保持對所有開發者的開放性，不會因特定應用場景或使用者需求而施加額外限制，確保區塊鏈的去中心化本質。

參考：

[模組化區塊鏈是什麼？](https://www.blocktempo.com/what-is-modular-blockchain/)

### 2025.02.09

## UTXO 
全名是Unspent Transaction Output（未花費的交易輸出）。

從較為標準的定義上而言，UTXO（未使用的交易輸出）是比特幣的核心概念之一，UTXO 是一種記錄交易輸出狀態的方式，它跟蹤了每個未使用的交易輸出，以確定哪些比特幣屬於哪個地址。

類比簡單理解，每個 UTXO 就像一張鈔票，它有特定的面值（比特幣數量）並附加了一個鎖，只能被一個私鑰打開。當你要發送比特幣時，你需要選擇一些鈔票，將它們合併成一個新的鈔票，並用收件人的鎖重新鎖上。

UTXO 核心設計思路是：它記錄交易事件，而不記錄最終狀態。要計算某個用戶有多少比特幣，就要對其錢包裡所有的 UTXO 求和，得到結果就是他的持幣數量。

## Nonce

“Nonce”一詞可能看起來充滿技術性且很覆雜，但其本質很簡單。它是一個獨特的數字，源自短語“僅使用一次的號碼”，在區塊鏈和密碼學中髮揮著重要作用。

## [Merkle Patricia Tree](https://hackmd.io/@pohanlu/Merkle_Patricia_Tree)

Ethereum 使用 **修改版的 Merkle-Patricia Trie** 來存儲狀態數據，這是一種結合 **PATRICIA Trie** 和 **Merkle Tree** 特性的數據結構，能夠高效地查找和驗證數據。  

這種 Trie 結構是確定性且可加密驗證的： 
- 狀態的根哈希（state root）是根據所有狀態數據計算出的，兩個相同的狀態必然會有相同的根哈希。  
- 透過 Merkle Proof，可以輕鬆驗證某個值是否存在於該狀態中。  
- 任何改變狀態的操作都會導致根哈希的變化，確保數據的安全性與唯一性。  
- 這種結構理論上能提供 **O(log(n))** 的插入、查找和刪除效率。  


### 1. **帳戶模型 vs UTXO 模型**  
   - 了解這兩種模型的區別，可以幫助我們理解為何比特幣和以太坊在交易處理和隱私性上有所不同。  
   - UTXO 模型提供更好的隱私性和並行處理能力，但帳戶模型更適合智能合約和去中心化應用（DApps）。  
   - 這些概念對於開發智能合約、錢包、交易機制以及 Layer 2 方案（如 Rollups）都很重要。  

### 2. **Merkle Patricia Trie (MPT) 與 Verkle Trees**  
   - 以太坊的狀態存儲依賴 MPT，而未來可能會改用 Verkle 樹，以減少節點存儲需求並提高可擴展性。  
   - MPT 的設計允許高效驗證區塊狀態，這對於輕客戶端（light clients）和 Layer 2 解決方案尤為重要。  
   - Verkle Trees 的研究代表了以太坊向「無狀態客戶端」（stateless clients）邁進的重要一步，這將有助於降低節點運行成本，進一步去中心化網絡。  

### 3. **序列化格式：RLP vs SSZ**  
   - RLP 是以太坊 1.0 使用的序列化格式，但它不支援 Merkle 化，影響了輕客戶端的可行性。  
   - SSZ（Ethereum 2.0 使用）允許更高效的 Merkle 化，使輕客戶端能夠驗證數據而不需要下載整個區塊鏈。  
   - 這些序列化格式影響智能合約的數據存儲方式，以及如何高效同步網絡狀態。  

### 4. **以太坊共識機制與最終性（Finality）**  
   - 以太坊 2.0 採用 **Casper FFG** 和 **LMD-GHOST** 來實現最終性，這與傳統 PoW 區塊鏈（如比特幣）有很大不同。  
   - 了解最終性機制，可以幫助我們理解如何避免長時間的區塊鏈回溯（reorg），以及如何確保交易不可逆。  
   - Gasper（結合 Casper FFG + LMD-GHOST）是以太坊目前使用的完整 PoS 共識協議，這與 DeFi、Staking 獎勵和安全性息息相關。  

### 5. **DHT（分散式哈希表）在以太坊網絡中的作用**  
   - 以太坊使用 DHT（類似於 BitTorrent 和 IPFS）來尋找節點，而非查找區塊。  
   - 這有助於提升 P2P 網絡的效率，並確保以太坊節點能夠快速發現其他節點進行同步。  
   - 了解 DHT 可以幫助我們優化節點發現機制，改善以太坊網絡連接和同步速度。  


參考:

[科普 | 一文讀懂UTXO概念與操作](https://news.cnyes.com/news/id/5534920)

[科普 | 想了解 BRC-20，先學比特幣的 「UTXO 模型」是什麼？](https://www.blocktempo.com/to-understand-brc-20-first-learn-the-utxo-model-adopted-by-bitcoin/)

[什麽是區塊鏈中的交易Nonce？](https://www.gate.io/zh-tw/learn/articles/what-is-a-transaction-nonce-in-blockchain/808)

[連Ethereum都在用！用一個例子徹底理解DHT](https://medium.com/taipei-ethereum-meetup/%E9%80%A3ethereum%E9%83%BD%E5%9C%A8%E7%94%A8-%E7%94%A8%E4%B8%80%E5%80%8B%E4%BE%8B%E5%AD%90%E5%BE%B9%E5%BA%95%E7%90%86%E8%A7%A3dht-f772ea2c6dcf)

[Data Partitioning - Distributed Hash Table and Consistent Hashing](https://ithelp.ithome.com.tw/articles/10226170)

[eth 1.x 與無狀態節點介紹](https://medium.com/cryptocow/eth1-x-stateless-clients-deddc3f935bb)

[Cryptography](https://ithelp.ithome.com.tw/articles/10287338)

[Casper FFG 與 Casper CBC 的瑜亮情結](https://medium.com/taipei-ethereum-meetup/history-and-state-of-ethereums-casper-research-85e8fba26002)


## Protocol history and evolution

### **Frontier - 以太坊的誕生**  

**發布時間：** 2015 年 7 月 30 日 3:26:13 AM UTC（以太坊創世區塊的時間戳）  

Frontier 是以太坊協議的首次正式發布，主要目標是讓開發者開始學習、實驗，並構建去中心化應用（DApps）和工具。  

#### **Frontier 的關鍵特性**  
- **初始 Gas 限制**：  
  - Frontier 啟動時，Gas 限制被硬性設定為 **5000**，這是為了讓礦工和用戶能夠順利運行以太坊節點並安裝客戶端。  
  - 在 **Frontier Thawing Fork**（解凍分叉）後，Gas 限制提升至 **3,141,592（約 3 百萬）**，確保網絡能夠處理更大的交易量。  

- **Canary Contracts（金絲雀合約）**：  
  - 這些合約只會返回 **0 或 1**，作為一種特殊的網絡監控機制。  
  - 如果多個 Canary Contracts 同時回傳 **1**，則表示區塊鏈需要升級，客戶端會自動停止挖礦並提醒用戶更新軟體，避免網絡長時間停滯。  

Frontier 版本主要是讓以太坊開發者熟悉這個新興平台，並為後續的升級做準備。  

---

### **Homestead - 以太坊邁向成熟**  

**發布時間：** 2016 年 3 月 14 日  

Homestead 是以太坊的 **第一個正式穩定版本**，標誌著以太坊從測試階段轉向更穩定、成熟的網絡。這次升級引入了幾個重要的改進，包括安全性強化、Gas 費用調整，以及合約創建邏輯的修正。  

### **Homestead 主要改進**  

#### **EIP-2：合約創建與交易簽名的優化**  
- **提高合約創建的 Gas 費用**：  
  - 透過交易創建合約的 Gas 費用從 **21,000 提高到 53,000**，目的是減少濫用交易來部署合約，鼓勵開發者使用 **CREATE** 操作碼來創建合約。  

- **無效的高 s 值簽名（Invalid high s-value signatures）**：  
  - 簽名中的 `s` 值若超過 `secp256k1n/2`，則交易將視為無效。  
  - 這個改變解決了 **交易可塑性（Transaction Malleability）** 問題，確保交易哈希值不會被輕易修改，提高交易追蹤的可靠性。  

- **合約創建失敗時不再留下空合約**：  
  - 若合約創建時 Gas 不足，將直接導致合約創建失敗，而不是留下一個 **空合約**，避免無效合約佔用區塊鏈狀態存儲。  

- **調整難度調整算法（Difficulty Adjustment Algorithm）**：  
  - Frontier 版本的難度調整機制存在一些問題，Homestead 修改了算法，使區塊時間更加穩定，減少難度變化過大導致的區塊時間波動。  

#### **EIP-7：新增 DELEGATECALL 操作碼**  
- `DELEGATECALL` 操作碼（0xf4）與 `CALLCODE` 類似，但它允許合約傳遞 **原始交易的發送者（msg.sender）和價值（msg.value）**。  
- 這使得 **代理合約模式（Proxy Pattern）** 變得更加靈活，開發者可以使用代理合約來轉發交易，而不影響原始發送者的身份。  

#### **EIP-8：提高網絡升級的兼容性**  
- Homestead 允許以太坊客戶端接受未來協議升級，即使數據包格式有所變化，也不會導致節點之間的連線失敗。  
- 這種「**Forward Compatibility**」機制確保網絡升級時，不會因為不同版本的客戶端不兼容而導致分裂。  

Homestead 讓以太坊從 **測試性質的 Frontier** 進入了更穩定的發展階段，為之後的智能合約應用和 DeFi 領域打下了基礎。  

### **Metropolis —— 智能合約的優化與隱私改進**  
**分為 Byzantium 和 Constantinople 兩個階段，分別於 2017 年和 2019 年發布。**  

Metropolis 旨在提高以太坊的智能合約功能、隱私性和可用性，並為 PoS 轉換做準備。  

#### **Byzantium —— 2017 年 10 月**  
- **EIP-649（降低區塊獎勵 & 延緩難度炸彈）**  
  - 區塊獎勵從 5 ETH 降至 **3 ETH**，減少通脹壓力。  
  - 延緩「難度炸彈」，避免區塊時間過快增加。  

- **EIP-658（交易狀態變更）**  
  - 引入 `status` 字段，讓交易成功與否更清晰。  

- **EIP-197 / EIP-198 / EIP-206（新密碼學指令）**  
  - 增加 zk-SNARK 支持，為以太坊上的隱私交易鋪平道路。  

#### **Constantinople —— 2019 年 2 月**  
- **EIP-145（位移操作提升效率）**  
  - 提升智能合約執行效率，降低 gas 費用。  
- **EIP-1052（智能合約驗證）**  
  - 允許合約透過 `EXTCODEHASH` 來獲取另一個合約的哈希，提高合約間交互效率。  
- **EIP-1234（進一步降低區塊獎勵 & 再次延緩難度炸彈）**  
  - 區塊獎勵從 **3 ETH 降至 2 ETH**，延緩難度炸彈。  

### **Serenity —— 以太坊 2.0**  
Serenity 是以太坊的最終形態，包含 **PoS（權益證明）、分片技術（Sharding）** 和 **更強大的虛擬機（eWASM）**。  

- **Beacon Chain（信標鏈）**：2020 年 12 月 1 日上線，作為以太坊 PoS 的骨幹。  
- **分片技術（Sharding）**：以太坊將區塊鏈拆分為多個 **分片鏈**，提升交易處理能力。  
- **eWASM**（取代 EVM）：允許以 WebAssembly 編寫智能合約，提高執行效能和靈活性。  



### **The Merge - 以太坊正式轉向 PoS**  

**發生時間：** 2022 年 9 月 15 日  

The Merge 是以太坊歷史上 **最重要的升級之一**，標誌著以太坊從 **工作量證明（Proof-of-Work, PoW）** 完全轉向 **權益證明（Proof-of-Stake, PoS）**。這次升級不僅大幅降低能源消耗，還為未來的擴展性和升級鋪平了道路。  

### **The Merge 的主要變化**  

- **棄用 PoW，改用 PoS**：  
  - **PoW Mining完全停止**，取而代之的是 **驗證者（Validators）** 負責區塊驗證。  
  - 這使得以太坊的 **能源消耗降低超過 99%**，成為更環保的區塊鏈。  

- **兩層架構：執行層（Execution Layer）+ 共識層（Consensus Layer）**：  
  - 以太坊將 **交易執行層（原本的以太坊鏈）** 與 **共識層（Beacon Chain）** 進行合併。  
  - **Beacon Chain** 早在 **2020 年 12 月 1 日** 就開始運行，並經過長時間測試，確保 PoS 共識機制的穩定性。  

- **提升安全性與去中心化**：  
  - PoS 驗證者需要 **抵押（Stake）ETH** 才能參與共識，若有惡意行為將面臨**資金懲罰（Slashing）**，這讓網絡更加安全。  
  - PoS 降低了礦池壟斷風險，讓更多個人驗證者能夠參與，提升去中心化程度。  


參考:

[以太坊歷史超迅速補充包（一）：寧靜之前](https://medium.com/swf-lab/%E4%BB%A5%E5%A4%AA%E5%9D%8A%E6%AD%B7%E5%8F%B2%E8%B6%85%E8%BF%85%E9%80%9F%E8%A3%9C%E5%85%85%E5%8C%85-%E4%B8%80-%E5%AF%A7%E9%9D%9C%E4%B9%8B%E5%89%8D-24f24753f9b6)

[簡述以太坊歷史的關鍵節點，坎昆升級前應該怎樣布局](https://m.cnyes.com/news/print/5231561?exp=a)

[以太坊的下個十年：坎昆升級](https://www.markreadfintech.com/p/bb3)

[「以太坊」坎昆升級 Proto-Danksharding](https://matters.town/a/71wfdgqk7vpa)

### 2025.02.10

![image](https://github.com/user-attachments/assets/5aa7acbf-ba25-4944-82e3-ae17f1e865cd)

1. **區塊驗證機制**
   - 只有有效的區塊才能加入區塊鏈，無效的區塊會被拒絕。
   
2. **區塊鏈的存儲策略**
   - 只保留最近 255 個區塊，以減少存儲開銷，這可能與 Ethereum EELS 的歷史區塊管理策略有關。

3. **狀態轉換**
   - 每當新的區塊被接受，狀態 (`State'`) 也會同步更新，包括存儲 Trie 和快照。
  
EELS 則是構建在執行層上的規範，可以用於運行測試，驗證新的 EIPs。當以太坊網路發生升級（分叉）時，EELS 的目標是給出一個整體的、清晰的以太坊狀態現況。這就像是在每個新的分叉版本上拍下一張完整的照片，讓開發者不必費力去閱讀覆雜的黃皮書，然後還要再額外針對各種應用，去提出改進提案（EIPs）。

![image](https://github.com/user-attachments/assets/42733caf-cb95-4103-a598-21a5f020a8e0)

1. **Account State**：每個帳戶包含 `nonce`、`balance`、`storageRoot` 和 `codeHash`，對應普通帳戶與合約帳戶。  
2. **World State**：由所有帳戶的狀態組成，透過地址映射到帳戶資訊。  
3. **State Transition Function**：處理區塊內交易，更新 `World State`。  
4. **Merkle Patricia Trie**：將狀態存入 Trie 資料結構，以 `storageRoot` 標識存儲內容，並最終生成 `World State Root`。  

![image](https://github.com/user-attachments/assets/be8a1c99-23f7-41c0-8dae-a2baf8ed039e)

**EIP-1559** 的 **Base Fee 調整機制**，即以太坊在倫敦升級後的交易費用模型。

### 1. **Gas 目標與 Base Fee 調整**
   - 每個區塊都有一個 **Gas Target（目標 gas）**，是 **Gas Limit** 的一半。
   - **Base Fee** 根據區塊使用的 gas 來調整：
     - 若 `Gas Used > Gas Target`，則 **Base Fee 增加**（最多 +12.5%）。
     - 若 `Gas Used < Gas Target`，則 **Base Fee 減少**（最多 -12.5%）。
   - **目標**：使長期內 `Gas Used` 接近 `Gas Target`，保持區塊大小穩定。

### 2. **多個區塊的影響**
   - 當交易需求高時，**Base Fee 會隨區塊增長上升**，以抑制需求。
   - 當需求下降時，**Base Fee 逐漸降低**，鼓勵更多交易。

### 3. **交易費用總計**
   - **總費用 = Gas Used × (Base Fee + Priority Fee)**
   - **Priority Fee**（優先費）是給礦工的小費，影響交易優先順序。

小總結：
**EIP-1559 設計原則**
- 當 區塊使用量 > 目標值 → Base Fee 上升。
- 當 區塊使用量 < 目標值 → Base Fee 下降。
- Base Fee 最多變動 12.5%（防止波動過大）。
- 新 Base Fee 可用於估算下一區塊交易費用。

參考：

[以太坊整合Python！公布ETH執行層最新規範 (EELS)](https://www.blocktempo.com/ethereum-execution-layer-specification/)
[ETH 將進入通縮時代？從五大 EIP 了解「倫敦升級」的變革性](https://blockcast.it/2021/06/24/everything-you-need-to-know-about-ethereum-london-hard-fork/)


### 2025.02.11

![image](https://github.com/user-attachments/assets/ba2ff0d7-5834-4ac0-ad24-56cd87ee22bf)

### 1. 執行層的角色與架構
執行層的主要職責包括：
- 執行交易（Transaction Execution）
- 驗證區塊鏈數據並存儲本地副本
- 透過 Gossip 協議與其他執行層客戶端通訊
- 維護交易池（Transaction Pool）
- 滿足共識層（Consensus Layer）需求，以驅動整體運作

執行層架構的核心組件：
- **執行引擎（Execution Engine）：** 負責驅動執行層，並受共識層驅動。
- **DevP2P（Networking Layer）：** 透過引導節點（Boot Nodes）初始化，以進入以太坊網絡。
- **Engine API：** 例如 `fork choice updated` 方法，可透過訂閱特定同步模式來從其他節點下載區塊。

---

### 2. 以太坊虛擬機（EVM）
- EVM 為以太坊提供虛擬化的 CPU，確保不同硬體架構（如 x86、ARM、RISC-V）下的執行結果一致。
- EVM 的作用類似於 JVM（Java 虛擬機），讓所有以太坊客戶端能夠對計算結果達成共識。
- **三明治複雜性模型（Sandwich Complexity Model）：**
  - 外層應保持簡單，所有複雜性集中於中間層。
  - 以太坊的最外層是 EVM 代碼，高層為 Solidity，透過編譯器轉譯為 EVM 字節碼。

---

### 3. 以太坊的狀態（State）
- **以太坊是狀態機（State Machine）：** 透過交易在不同狀態間轉換。
- 與比特幣不同，以太坊維護**全域狀態**（Global State），而比特幣只維護 UTXO（未花費交易輸出）。
- **狀態的組成部分：**
  - 以太坊地址、餘額
  - 智能合約的代碼與數據
  - 當前網絡狀態（State & Network State）

---

### 4. 交易（Transactions）
- 交易會觸發**狀態轉換（State Transition）**，透過 EVM 進行處理。
- 交易在 EVM 內部執行後，如果合法，就會改變以太坊的全域狀態。

---

### 5. DevP2P（點對點網絡通信）
- **作用：** 執行層客戶端透過 DevP2P 傳播交易與區塊。
- 交易先存入**記憶池（Mempool）**，再透過 P2P 傳遞給其他客戶端。
- 每個接收交易的節點都會驗證交易的有效性，並再次廣播至網絡。

---

### 6. JSON-RPC API（執行層對外接口）
- **用途：**
  - 透過 JSON-RPC API 與執行層互動，例如查詢以太坊狀態或發送交易。
  - 錢包（如 MetaMask）或 DApp 透過 JSON-RPC API 與以太坊網絡通訊。
- **交易流程：**
  1. 使用錢包簽署交易
  2. 交易經執行層驗證
  3. 廣播交易至整個網絡

---

### 7. Engine API（共識層與執行層的接口）
- **作用：** 連接共識層與執行層，提供兩類主要端點：
  - **New Payload（V1/V2/V3）：** 負責區塊驗證與插入
  - **Fork Choice Updated（V1/V2/V3）：** 負責狀態同步與區塊建構

---

### 8. 同步（Sync）
- **以太坊的交易處理依賴於全球狀態，而非單一節點的本地狀態。**
- 執行層透過**LMD-GHOST 算法**決定最佳分叉選擇，並透過 Engine API 傳遞至執行層。
- **同步方式：**
  1. 下載遠端節點的區塊
  2. 驗證區塊，並在 EVM 中執行

---

### 9. 執行層架構組件
- **Engine（執行引擎）：** 負責執行 Engine API，並連接至共識層。
- **認證機制：** Engine API 透過 JSON-RPC（HTTP）提供服務，並透過 JWT（JSON Web Token）驗證請求來源。
- **安全性：**
  - Engine API **僅供共識層訪問**，不對外開放。
  - JWT 只用於驗證來源，**不加密**傳輸流量。

---

### 10. 負責交易驗證的例行程序（Routines）
- **Payload 驗證**
  - 透過區塊頭（Block Header）與執行環境規則驗證區塊內容。
- **合併後（The Merge）的變化**
  - 以前，執行層負責共識、排序區塊、處理區塊重組。
  - 現在，這些任務交由**共識層**，執行層主要負責**狀態轉換（State Transition）。**

---

### 11. 共識層與執行層的交互
- **共識層如何與執行層互動？**
  - 共識層在**Deneb 信標鏈規範**（Beacon Chain Specs）中定義**執行負載（Execution Payload）**。
  - 負載透過 `execution_engine` 函數傳遞到執行層。
  - **驗證流程：**
    1. **高級檢查**（如父區塊哈希、時間戳驗證）。
    2. **基礎檢查**（輕量級驗證）。
    3. **傳輸至執行層進行區塊驗證**。
    4. **通知負載函數（notify payload）**：將執行負載傳遞給執行引擎。
    5. **執行引擎執行狀態轉換，並返回成功或失敗結果**。
  
---

### 12. 狀態轉換函數（State Transition Function, STF）
- **區塊級狀態轉換函數（Block Level STF）**
  - 是執行層的核心功能，負責區塊驗證與插入。
  - 雖然在 Geth 具體實作，但不同客戶端的 STF 概念相同。
  - 在 EELS Python 規範客戶端中，STF 才明確被提及，其他客戶端則將 STF 功能拆分至不同架構組件中。

參考：

[以太坊的節點](https://ithelp.ithome.com.tw/m/articles/10289488)

### 2025.02.12

#### Besu
- **私密交易**：僅限於部署或調用智能合約，無法進行 Ether 轉帳。
- **私密智能合約**：只有指定的參與方節點可以讀取和寫入合約內容。
- **應用場景**：適用於聯盟鏈中，特定企業之間的隱私保護需求，例如投票系統。

- 基本知識
	- **Ethereum 智能合約**：智能合約是可編程的區塊鏈協議，用於執行合約條款。
	- **Ballot 智能合約**：一個投票合約範例，包含投票權分配、投票、查看結果等功能。
	- **Besu 私密智能合約**：與一般智能合約的區別在於，只有參與方節點可以操作合約。

- Besu 私密交易參數設定
	- **PrivateFrom**：發起方的公鑰。
	- **PrivateFor**：參與方的公鑰列表。
	- **Payload**：智能合約的操作數據，編碼為 16 進位字串。
	- **GasLimit**：交易所需的 Gas 上限。
	- **Nonce**：交易序號，確保交易唯一性。

- 發佈私密智能合約
	- **步驟**：
	  1. **定義候選人名單**：例如 `["Alice", "Bob", "Kevin"]`。
	  2. **型態轉換**：將候選人名單轉換為智能合約所需的 `[32]byte` 格式。
	  3. **參數打包**：使用 ABI 打包合約的建構函數參數。
	  4. **產生 Payload**：將合約的 Bytecode 與打包後的參數結合。
	  5. **產生 Private Raw Transaction**：使用 `NewContractCreation` 創建交易。
	  6. **發佈合約**：透過 `eea_sendRawTransaction` 發佈合約，並取得合約地址。

- 寫入私密智能合約
	- **賦予投票權**：
	  - 使用 `giveRightToVote` 函數，賦予特定帳戶投票權。
	  - 打包參數並產生 Payload，發送私密交易。
	- **投票**：
	  - 使用 `vote` 函數，進行投票。
	  - 打包參數並產生 Payload，發送私密交易。

- 讀取私密智能合約
	- **查看投票結果**：
	  - 使用 `winnerName` 函數，查看當前最高票的候選人。
	  - 透過 `priv_call` RPC 方法讀取合約數據。
---
#### Reth

1. **Reth 使用 MDBX 作為主要的資料庫**
   - MDBX（Lightning Memory-Mapped Database Extended）是一個高效能、低開銷的鍵值存儲系統，專門設計來處理高並發讀寫操作。  
   - Reth 透過一層 **抽象（abstraction）**，讓底層存儲層具有靈活性，未來若要更換 MDBX，變更的成本可以降到最低。  

2. **Codecs（編碼/解碼）**
   - Reth 透過 **Compact Trait** 來進行數據壓縮，比如：  
     - 壓縮 **無符號整數（unsigned integers）** 的前導 0  
     - 優化存儲 **區塊頭（headers）、訪問列表（access-lists）** 等數據  

3. **DB Abstractions（資料庫抽象層）**
   - **Database Trait**  
     - 提供 **唯讀** 或 **讀寫** 交易的基本 API，讓 Reth 操作底層數據時不需要直接依賴 MDBX，而是透過這一層抽象來與資料庫交互。  

   - **Cursor（游標）**  
     - 用於 **遍歷資料庫**，提高查詢和計算效率。  
     - **特點**：
       - 適用於 **Merkle Root 計算**，因為連續存取數據比隨機讀取快得多。  
       - 在寫入大量數據時，**先排序再寫入** 會大幅提升性能，游標可以幫助我們更有效地管理這個過程。  

**Reth執行擴展（ExEx）：**

Reth引入了執行擴展（Execution Extensions，簡稱ExEx），這是一個框架，用於構建高性能和複雜的鏈下基礎設施作為執行後掛鉤。可用於實現Rollup、索引器、MEV機器人等，與現有方法相比，代碼量減少了10倍以上。這使得開發人員能夠以標準化的方式構建可重用的ExEx，類似於Cosmos SDK模組或Substrate Pallets的工作方式。

參考：

[如何透過 Private Transaction 操作 Hyperledger Besu 私密智能合約](https://medium.com/bsos-taiwan/how-to-use-besu-private-smart-contract-51e33c5b6d62)

[Paradigm：介紹 Reth 執行擴充（ExEx），建構高效能的鏈下基礎設施](https://web3caff.com/zh_tc/archives/103079)

### 2025.02.13

### 2025.02.14

### 交易（Transaction）筆記  

#### 定義  
交易是由外部帳戶發出的加密簽名指令，透過 JSON-RPC 廣播至整個網絡。  

#### 交易包含的欄位  

1. **Nonce（交易計數）**  
   - 這是一個整數值，等於發送者已發送的交易數量。  
   - 作用：  
     - **防止重放攻擊**：由於每筆交易的 Nonce 是唯一的，EVM 會拒絕已存在的交易，防止惡意重播交易。  
     - **決定智能合約地址**：在創建合約時，Nonce 與發送者地址一起決定合約帳戶的地址。  
     - **替換交易**：如果交易因為低 Gas 價格而卡住，可發送相同 Nonce 但更高 Gas 價格的新交易來取代舊交易。但是否成功取決於礦工與網絡條件。  

2. **Gas Price（燃料價格）**  
   - 這是一個整數值，表示每單位 Gas 需要支付的 Wei 數量。  
   - 1 ETH = \(10^{18}\) Wei。  
   - Gas Price 決定了交易的優先級，越高的 Gas Price 越可能被礦工優先打包進區塊。  

3. **Gas Limit（燃料上限）**  
   - 這是一個整數值，代表此交易執行時允許消耗的最大 Gas 數量。  
   - 如果執行時 Gas 消耗超過 Gas Limit，交易會失敗。  

4. **To（接收者地址）**  
   - 這是一個 20 字節的地址，表示此交易的接收者。  
   - `to` 欄位也決定了交易的模式或目的，例如發送 ETH 或部署智能合約。

#### **TestRPC（本地私有區塊鏈）**
✅ **優點**：
- 無需同步區塊鏈，啟動快，幾乎無磁碟需求。  
- 測試Ether無限制，可自行挖礦獲取獎勵。  
- 只有你一個用戶，環境可控。  
- 沒有其他合約影響測試結果。  

❌ **缺點**：
- 缺少真實區塊鏈的交易競爭與排序機制。  
- 挖礦預測性強，無法測試公開網路的不確定性。  
- 需自行部署所有依賴的智能合約與庫。  
- 不能重現公共合約及其地址來測試特定場景。  

---

#### **以太坊客戶端運行（Geth & Parity）**
**完整節點運行條件**：
- **最低需求**：2核CPU、80GB SSD、4GB RAM（HDD需8GB）、8+ MBit/sec網速。  
- **推薦配置**：4核以上CPU、16GB RAM、500GB SSD、25+ MBit/sec網速。  

🔹 **Geth（Go-Ethereum）**：
- 以Go語言編寫，官方支持度高。  
- **安裝方式**：GitHub獲取原始碼 ➝ `make geth` 編譯 ➝ `geth version` 檢查。  
- **快速同步模式**（`--fast`）可減少區塊驗證時間。  

🔹 **Parity**：
- 以Rust語言開發，運行效率高。  
- **安裝方式**：GitHub獲取原始碼 ➝ `cargo build` 編譯 ➝ `parity --version` 檢查。  
- **快速同步**（舊版`--warp`，1.6+ 版本自動啟用）。  

---

#### **以太坊區塊鏈同步與JSON-RPC**
- **完整同步**：下載並驗證所有區塊與交易，較慢但數據完整。  
- **快速同步**：僅同步最新區塊，提升速度但省略歷史驗證。  
- **JSON-RPC API**：
  - 用於與以太坊網絡交互的標準接口（HTTP 8545）。  
  - 限制本地訪問，提高安全性，可用於智能合約調用與交易管理。
 
參考:

[蜜蜂書第三章](https://cypherpunks-core.github.io/ethereumbook_zh/)

### 2025.02.15

### **RLP（Recursive-Length Prefix）序列化**  

**Recursive-Length Prefix（RLP）** 是執行層（Execution Layer）中的核心序列化協議，用於對數據進行編碼與解析。其設計目的是將數據序列化，以生成所有客戶端軟體均可讀取的結構。RLP 序列化適用於從交易數據到整個區塊鏈狀態的各種場景。本文探討 RLP 的內部運作機制、編碼/解碼規則、可用工具，以及它在 Ethereum 中的功能。

---

### **Ethereum 中的數據序列化**  

數據序列化是指將數據結構或對象轉換為字節流，以便存儲、傳輸或稍後重建。在像 Ethereum 這樣的分散式系統中，序列化對於在網路節點間可靠、高效地傳遞數據至關重要。不同程式語言編寫的客戶端都需要以相同的方式處理數據，並且客戶端向其他節點傳輸數據或導出數據時，都必須遵循標準格式。  

雖然常見的序列化格式包括 **JSON、XML、Protobuf**，但 Ethereum 採用了自己的協議，因為它在編碼**嵌套字節數組（Nested Arrays of Bytes）**方面更簡單高效。  

Ethereum 事實上使用了兩種主要的數據序列化格式：  
1. **RLP（Recursive-Length Prefix）** —— 用於執行層（Execution Layer）。  
2. **SSZ（Simple Serialize）** —— 一種較新的標準，主要用於共識層（Consensus Layer）。  

![image](https://github.com/user-attachments/assets/f13cbf77-0300-4b7a-87ee-5a6ea45e0bcb)


[5分鐘深入了解以太坊編碼原理
2019-07-22](https://blockbar.io/ethereum/%E4%BB%A5%E5%A4%AA%E5%9D%8A%E7%B7%A8%E7%A2%BC%E5%8E%9F%E7%90%86-ethereum-coding-principle/)

### 2025.02.16



## **1. 以太坊虛擬機（EVM）簡介**  
EVM 是以太坊世界計算機（Ethereum World Computer）的核心，負責執行交易，並將最終結果永久儲存到區塊鏈上。  

## **2. 以太坊作為狀態機（State Machine）**  
EVM 處理交易時，會改變以太坊的整體狀態，因此可以將以太坊視為一種狀態機。  
- **狀態機（State Machine）**：用於描述系統如何從一種狀態轉變到另一種狀態的抽象模型。  
- **例子**：販賣機根據投幣及按鍵輸入來改變狀態，最終吐出商品。  

## **3. 虛擬機（Virtual Machine）的概念**  
- 軟體需要轉換成機器語言（ISA, 指令集架構）才能執行，且不同硬體架構（如 Intel vs. Apple Silicon）有不同 ISA。  
- 現代軟體還需要依賴作業系統來管理記憶體等資源。  
- EVM 透過「虛擬機」這一層抽象，確保智能合約能在不同環境中一致執行。  

---

# **EVM 的結構與組成**  

## **1. 基本架構**  
- **字組（Word Size）**：EVM 的字組大小為 **32 bytes（256 bits）**。  
- **EVM Bytecode**（位元碼）：EVM 程式由一串「位元組（byte）」組成，每個位元組代表：  
  - **操作碼（Opcode）**：具體指令，如 `ADD`（加法）。  
  - **操作數（Operand）**：提供給操作碼的輸入數據。  

## **2. 堆疊（Stack）**  
- **運作方式**：採用 **LIFO（後進先出）** 原則。  
- **基本操作**：
  - `PUSH`：將數據壓入堆疊頂部。  
  - `POP`：移除堆疊頂部數據。  
- **錯誤處理**：若試圖從空堆疊 `POP`，會觸發 **堆疊下溢（Stack Underflow）錯誤**。  

## **3. 程式計數器（Program Counter, PC）**  
- 負責追蹤**下一條**將要執行的指令在位元碼中的偏移量（offset）。  
- 例如：
  ```
  Bytecode    Assembly   長度（bytes）   偏移量（hex）
  60 06      PUSH1 06       2         00
  60 07      PUSH1 07       2         02
  01         ADD            1         04
  ```
  - `PC` 最初為 `00`，執行 `PUSH1 06`，然後移動到 `02`，依此類推。  

## **4. 燃料（Gas）機制**  
- **目的**：
  - 防止無窮迴圈、DDoS 攻擊，保護以太坊網路資源。  
  - **計算資源 = 以太幣（ETH）支付 Gas 費用**。  
- **工作原理**：
  - EVM 指令執行時需要消耗 Gas。  
  - 若 Gas 不足，則交易失敗，EVM 停止執行。  
- **EVM 的圖靈完備性**：由於 Gas 限制了計算步驟，EVM 被視為**準圖靈完備（Quasi-Turing Complete）**。  

## **5. 記憶體（Memory）**  
- **特點**：
  - EVM 記憶體為一個長度 **2^256**（幾乎無限大）的字節陣列。  
  - 初始時所有記憶體位置皆為 `0`。  
- **操作指令**：
  - `MSTORE`：從堆疊取值，寫入記憶體。  
  - `MLOAD`：從記憶體讀取數據，壓入堆疊。  
- **動態擴展機制**：
  - 記憶體是以**頁（page）**為單位擴展，每頁 **32 bytes**。  
  - 擴展記憶體需支付額外 Gas。  

## **6. 儲存（Storage）**  
- **特點**：
  - 儲存區是**持久化存儲**，與智能合約地址關聯，交易結束後仍然存在。  
  - 初始值皆為 `0`，只能透過**合約內部代碼**存取。  
- **操作指令**：
  - `SSTORE`：從堆疊取值，寫入智能合約儲存區。  
  - `SLOAD`：從儲存區讀取數據，壓入堆疊。  

---

# **EVM 的未來升級（EVM Upgrades）**  

## **1. EVM 變更的挑戰**  
- 以太坊網路持續升級，但 **EVM 變更較為保守**，因為：
  - **重大變更可能破壞現有智能合約**，增加開發維護成本。  
  - 需要保持多個 EVM 版本，帶來額外的系統負擔。  

## **2. 近期的 EVM 升級**  
以下是一些 EIP（Ethereum Improvement Proposal，以太坊改進提案）：  
- **EIP-1153**：新增暫存存儲（Transient Storage）。  
- **EIP-4788**：引入信標鏈狀態的存取功能。  
- **EIP-5000**：優化運行時指令。  
- **EIP-5656**：增加新的 `MCOPY` 指令，提高記憶體拷貝效率。  
- **EIP-6780**：**弱化 `SELFDESTRUCT` 指令**，防止合約惡意銷毀，卻仍維持向後兼容性。  

## **3. EVM 重大改變：EOF 格式**  
- **EOF（EVM Object Format）**是一項重要的未來升級，目標是：
  - 統一 EVM 內部的位元碼格式，提升處理效率。  
  - 簡化 EVM 的解析與執行，提高安全性與擴展性。  
  - 涵蓋多項 EIP，已經討論和優化了相當長的時間。  

### 2025.02.17

區塊構建是以太坊區塊鏈正常運作的關鍵，涉及驗證者 (Validator) 如何獲取區塊，並將其提議到網絡。以太坊網絡由執行層 (EL) 和共識層 (CL) 的客戶端組成，兩者協同工作以在每個 slot 內產生新的區塊。

當驗證者被選中提議區塊時，它會尋找 CL 提供的區塊。驗證者可以使用自身 EL 構建的區塊，也可以使用外部建構者 (Builder) 構建的區塊。

---

## 區塊的建構流程 (Payload Building Routine)

### **(1) 接收 CL 指令**
當共識層決定應由某個驗證者建構區塊時，會透過 Engine API 的 `forkchoiceUpdated` 端點通知 EL，啟動建構區塊的流程。

- 交易透過 P2P 網絡在節點之間傳播，節點會接收並驗證這些交易。
- 驗證標準：交易的 nonce 是否符合帳戶的下一個有效 nonce，且帳戶餘額是否足夠支付交易費用。
- EL 需要持續監聽交易池 (Transaction Pool)，以確保區塊填充最有價值的交易。

### **(2) 區塊構建步驟**
1. **初始化區塊環境 (Environment Setup)**  
   - 包含時間戳 (Timestamp)、區塊號 (Block Number)、前一個區塊 (Parent Block)、基本費用 (Base Fee) 以及提款資訊 (Withdrawals)。
   - 這些資訊來自 CL，決定了區塊的基本結構。

2. **選取交易 (Transaction Selection)**
   - 交易池中的交易按照手續費排序，優先選擇價值最高的交易，以構建最有利可圖的區塊。
   - EL 會遍歷交易池中的交易，直到 gas 限制 (30M gas) 被達到。

3. **執行交易 (Executing Transactions)**
   - 透過 EVM 來執行每筆交易，應用到狀態 (State)。
   - 若交易執行失敗（如超出 gas 限制或合約調用錯誤），則該交易會被跳過，並繼續處理下一筆交易。

4. **記錄交易及 gas 消耗**
   - 若交易執行成功，則將其加入交易列表，並累積所消耗的 gas。

5. **計算 Merkle 根並組裝完整區塊**
   - 最後，使用交易列表計算 **交易根 (Transaction Root)**、**收據根 (Receipts Root)** 和 **提款根 (Withdrawals Root)**，組裝完整的區塊頭 (Block Header)。

---

## 以太坊 Geth 客戶端內部區塊建構過程
以下範例基於 Geth（Go Ethereum）代碼，解析 EL 內部如何處理區塊構建。

### **(1) 啟動區塊建構**
當驗證者被選中建構區塊時，會透過 **Engine API** 呼叫 `engine_forkchoiceUpdatedV2`，讓 EL 啟動區塊建構過程：
🔗 [Geth 代碼 - engine_forkchoiceUpdatedV2](https://github.com/ethereum/go-ethereum/blob/0a2f33946b95989e8ce36e72a88138adceab6a23/eth/catalyst/api.go#L398)

核心邏輯位於 Geth 的 **miner 模組**，負責：
- 透過 `buildPayload` 初始化一個空區塊，確保不會錯過 slot。
- 啟動 **Go 協程** 填充區塊的交易資訊：
  🔗 [Geth 代碼 - buildPayload](https://github.com/ethereum/go-ethereum/blob/0a2f33946b95989e8ce36e72a88138adceab6a23/miner/payload_building.go#L180)

### **(2) 獲取可封裝區塊 (Sealing Block)**
- 在 `buildPayload` 方法中，透過 `getSealingBlock` 獲取可封裝的區塊，確保該區塊 **不會是空的**。
  🔗 [Geth 代碼 - getSealingBlock](https://github.com/ethereum/go-ethereum/blob/master/miner/worker.go#L1222)

- `getSealingBlock` 透過 `getWorkCh` 通道發送請求，而 `getWorkCh` 在 `mainLoop` 函數內部監聽並處理請求：
  🔗 [Geth 代碼 - mainLoop](https://github.com/ethereum/go-ethereum/blob/master/miner/worker.go#L537)

### **(3) 填充交易**
- `generateWork` 方法負責將交易填充到區塊中：
  🔗 [Geth 代碼 - generateWork](https://github.com/ethereum/go-ethereum/blob/0a2f33946b95989e8ce36e72a88138adceab6a23/miner/worker.go#L1094)

- `fillTransactions` 方法從交易池中取出交易，依據手續費排序後加入區塊：
  🔗 [Geth 代碼 - fillTransactions](https://github.com/ethereum/go-ethereum/blob/master/miner/worker.go#L1024)

- 交易依序提交到 `commitTransactions`：
  🔗 [Geth 代碼 - commitTransactions](https://github.com/ethereum/go-ethereum/blob/master/miner/worker.go#L1072)
  - 確保 gas 限制內可容納交易
  - 根據 EIP-4844 規範，每個區塊可包含的 blob 交易數量有限：
    🔗 [EIP-4844](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-4844.md)

### **(4) 執行交易**
- `commitTransactions` 內部調用 `applyTransaction`：
  🔗 [Geth 代碼 - applyTransaction](https://github.com/ethereum/go-ethereum/blob/master/miner/worker.go#L760)

- `applyTransaction` 調用 `core.ApplyTransaction`，將交易應用到本地狀態：
  🔗 [Geth 代碼 - ApplyTransaction](https://github.com/ethereum/go-ethereum/blob/master/core/state_processor.go#L161)

- 若交易執行失敗（例如 gas 不足或合約調用失敗），則不會對狀態產生影響，該交易不會包含在區塊內。

### **(5) 交易執行完畢，封裝至區塊**
當所有交易執行完畢後：
1. **EL 透過 Engine API `getPayload` 將交易填充進區塊。**
2. **CL 接收此區塊並打包進信標區塊 (Beacon Block)，最終向網絡廣播。**


### 2025.02.18

JSON-RPC 是一種基於 OpenRPC 的遠端程序呼叫 (RPC) 協議，使用 JSON 編碼。它允許在遠端伺服器上執行函式並返回結果，屬於 **Execution API** 規範的一部分。JSON-RPC 主要用於讓使用者透過客戶端與 Ethereum 區塊鏈互動，也包括 **共識層 (CL)** 與 **執行層 (EL)** 透過 **Engine API** 進行通信。  

### API 規範  
JSON-RPC 方法透過 **命名空間 (namespace)** 來分類，並遵循統一的請求格式：  
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "<prefix_methodName>",
  "params": [...]
}
```
- **id**：請求的唯一識別碼  
- **jsonrpc**：JSON-RPC 協議的版本 (2.0)  
- **method**：要調用的方法名稱 (帶有命名空間前綴)  
- **params**：方法的參數，若無則為空陣列  

### Namespaces
每個方法名稱由 **命名空間前綴** 和 **方法名稱** 組成，例如 `eth_getBlockByNumber` (eth 為命名空間)。Ethereum 客戶端必須至少支援與網路互動的基本 RPC 方法，此外，每個客戶端還可能提供額外的專屬方法，例如 Geth 和 Reth 各自的命名空間與方法集。因此，使用時應參考特定客戶端的官方文件。

### **編碼方式**  
JSON-RPC 方法的參數遵循 **十六進位 (hex) 編碼** 規範：  
- 數值 (Quantities) 以 `"0x"` 前綴的十六進位格式表示。例如：  
  - **數字 65** 表示為 `"0x41"`  
  - **數字 0** 表示為 `"0x0"`  
  - **無效示例**：`"0x"` (沒有數字) 或 `"ff"` (缺少 `"0x"` 前綴)  
- **未格式化資料** (如哈希值、帳戶地址、位元組陣列) 也需使用 `"0x"` 前綴。例如：  
  - `0x400` (十進位 1014)  
  - **無效示例**：`0x0400` (不允許前導零)  

---

### **傳輸協議 (Transport Agnostic)**  
JSON-RPC 不依賴特定的傳輸方式，可透過 **HTTP、WebSockets (WSS) 或 IPC** 進行通信：  
- **HTTP**：單向請求-回應模式，回應發送後即關閉連線。  
- **WebSockets (WSS)**：雙向持續連線，可用於事件驅動 (訂閱) 通訊。  
- **IPC (進程間通信)**：用於同機器上的進程間通信，速度最快，但無法用於遠端連線 (如本地 JS 控制台)。  

---

### **使用工具**  
#### 1. **透過 curl 發送 JSON-RPC 請求**  
使用 `curl` 查詢最新區塊號：  
```sh
curl <node-endpoint> \
-X POST \
-H "Content-Type: application/json" \
-d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```
此請求的 `params` 為空，因為 `eth_blockNumber` 預設回傳 `"latest"`。  

#### 2. **透過 axios (JavaScript/TypeScript)**  
查詢地址餘額：  
```js
import axios from 'axios';

const node = '<node-endpoint>';
const address = '<address>';

const response = await axios.post(node, {
  jsonrpc: '2.0',
  method: 'eth_getBalance',
  params: [address, 'latest'],
  id: 1,
  headers: {
    'Content-Type': 'application/json',
  },
});
```
JSON-RPC 方法透過 **POST 請求**，參數放在請求主體 (body) 內。  

#### 3. **使用 web3 庫 (web3py / ethers.js)**  
使用 `web3py` (Python)：  
```python
from web3 import Web3

# 設定 HTTPProvider
w3 = Web3(Web3.HTTPProvider('http://localhost:8545'))

# 查詢餘額
w3.eth.get_balance('0xaddress')
```
使用 `ethers.js` (JavaScript/TypeScript)：  
```js
import { ethers } from "ethers";

const provider = new ethers.providers.JsonRpcProvider('http://localhost:8545');

await provider.getBlockNumber();
```
**web3 庫 (web3py、web3.js、ethers.js)** 封裝了 JSON-RPC 方法，使與 Ethereum 執行層的交互更方便，建議根據使用的編程語言選擇適合的庫。

### **執行層的 P2P 通訊協議**  
Ethereum **執行層 (EL)** 使用 **devp2p** 作為其與網路中節點的通信協議，包含多種子協議與功能，例如：  
- **eth**：主要的 Ethereum P2P 協議  
- **snap**：用於快速同步狀態的協議  
- **les**：輕客戶端 (Light Ethereum Subprotocol)  
- **pip**、**wit**：其他輔助協議  

由於 **libp2p** (共識層 CL 使用的 P2P 協議) 在 Ethereum 創建時尚未準備就緒，因此 Ethereum 自行開發了 **devp2p** 作為專屬的 P2P 協議棧。

### 2025.02.19

### **Consensus Layer**  
共識協議的主要目標是**在不可靠的基礎設施上建立可靠的分佈式系統**。這一領域的研究可追溯到 1970 年代，但 Ethereum 需要達成的規模遠比傳統共識系統更具挑戰性。  

Ethereum 共識層 (Consensus Layer, CL) 的目標是確保**全球數萬個獨立節點保持同步**，並且每個節點的賬本狀態完全一致。這意味著，無論網路連線多麼不穩定、節點設備多麼普通，甚至有惡意節點存在，整個系統仍然要能夠達成共識。

---

### **拜占庭容錯 (BFT) 與拜占庭將軍問題**  
**拜占庭容錯 (Byzantine Fault Tolerance, BFT)** 是分佈式系統的一項關鍵屬性，使其即使在某些節點故障或惡意行為的情況下仍能正常運行。這對於區塊鏈這樣的**去中心化系統**至關重要，因為在這類系統中，無法假定所有節點都是誠實的。  

Ethereum 的共識機制採用 BFT 來確保所有誠實節點能夠達成一致，即使存在不可靠或惡意的節點。

---

### **Ethereum 的共識機制**  
Ethereum 的共識機制將 **LMD GHOST** 和 **Casper FFG** 兩種共識協議結合，形成 **Gasper**。  

- **LMD GHOST** (Latest Message Driven Greedy Heaviest Observed Subtree)  
  - 用於決定哪條鏈應該被視為**最重鏈**。  
  - 幫助節點選擇最合適的區塊作為鏈的延續。  

- **Casper FFG** (Friendly Finality Gadget)  
  - 負責最終確保區塊不可逆，防止鏈的分叉。  
  - 透過**投票與罰沒 (slashing)** 來約束驗證者行為。  

這兩者的結合使 Ethereum 在 PoS (Proof-of-Stake) 之下能夠維持**安全性、去中心化與效率**。

---

### **區塊鏈與區塊**  
Ethereum 的區塊鏈由**區塊 (block)** 組成，每個區塊包含一組交易：  
- **執行層 (EL) 區塊**：存放用戶交易 (Execution Payload)。  
- **信標鏈 (Beacon Chain) 區塊**：存放驗證者的**見證 (attestations)** 和其他共識相關數據。  

區塊是由節點的 **提議者 (proposer)** 建立，並由**驗證者 (validators)** 進行投票和確認。

Ethereum 採用 **PoS**，因此區塊提議者是**隨機從驗證者池中選擇**，而非透過工作量競賽 (如 PoW 中的挖礦競爭)。

---

### **Ethereum 過渡到 Proof-of-Stake (PoS)**  
Ethereum 在 2022 年 9 月 15 日進行 **The Merge (合併)**，正式從 **PoW 過渡到 PoS**。  

- **合併 (The Merge)** 透過 **Paris 硬分叉** 完成。  
- 轉換標準：基於 **終端總難度 (Terminal Total Difficulty, TTD)**，而非區塊高度。  
- PoS 取代 PoW，**驗證者 (Validators) 取代礦工**，成為共識層的主要參與者。  

這次轉變大幅減少能源消耗，使 Ethereum 更具可持續性。

---

### **信標鏈 (Beacon Chain) 與驗證者 (Validators)**  
信標鏈負責 PoS 共識，並協調驗證者的行為。  

驗證者需執行以下角色：  
- **質押 ETH**：每位驗證者需**質押 32 ETH** 以參與共識。  
- **提議區塊**：隨機選出的驗證者負責創建區塊。  
- **見證區塊 (Attestations)**：驗證其他區塊的有效性，確保共識達成。  
- **參與共識**：在每個**時段 (epoch)** 內投票，以幫助確定區塊鏈的最終狀態。  

Ethereum PoS 的 **時間結構**：
- **槽 (Slot)**：每 **12 秒** 為一個 slot，對應一次出塊機會。  
- **時段 (Epoch)**：每 **32 個 slot** 為一個 epoch (~6.4 分鐘)。  

---

#### **Attestations**
- **區塊提議者（Proposer）** 是被隨機選中的驗證者，負責提議新區塊。  
- **驗證者（Validators）** 主要負責對區塊進行投票（即**證明**），這些投票決定信標鏈（Beacon Chain）的最新狀態。  
- **證明（Attestation）** 是驗證者的投票，權重由其質押的 ETH 多少決定，並會廣播至信標鏈。  
- 驗證者可舉報作惡者（如雙重投票或提交多個區塊），並獲得獎勵。  

#### **Committees**
- 每個區塊槽（Slot）至少有 128 名 Committees 組成委員會，提高安全性。  
- 通過**RANDAO 隨機數** 選擇提議者，每個槽的提議者都是隨機決定的。  
- 如果驗證者數量超過 8,192，就會有多個委員會同時運行。  

#### **EIP-4844 與 Blobs**
- **EIP-4844（proto-danksharding）** 引入了**數據可用性層**，支持臨時存儲數據（**blobs**），降低 Layer 2 交易成本，提高以太坊擴展性。  
- 每個區塊可包含 3~6 個 blob sidecars，節點存儲需求預計增加 52~104GB。  

#### **檢查點與最終性（Finality）**
- 每個 Epoch 生成一個**檢查點（Checkpoint）**，若 2/3 以上驗證者投票支持，則其被**確認（Justified）**。  
- 若下一個 Epoch 也確認新的檢查點，則前一個檢查點**最終確定（Finalized）**，即不可逆轉。  
- 交易通常需 **14~16 分鐘** 才能最終確定。  

#### **質押獎勵與懲罰**
- **獎勵**：正確投票、及時提交證明、提議區塊、舉報作惡者可獲得獎勵。  
- **懲罰**：離線、錯誤投票、或雙重投票等惡意行為會被**削減（Slashing）**，最嚴重可損失全部 32 ETH 並強制退出。  
- **特殊機制**：若網絡長時間無法達成最終性，將觸發**非活躍泄漏（Inactivity Leak）**，逐步消耗不活躍驗證者的余額，直到剩下的活躍者可恢覆最終性。  

#### **驗證者生命周期**
- **需質押 32 ETH 激活**，若余額降至 16 ETH 將被移除。  
- **自願退出** 需等待 **9 天（2048 epochs）**，退出後 **27 小時** 才能提款。  
- **被削減的驗證者** 需 **36 天** 才能提現，且會失去部分質押金。  

#### **整體影響**
- **所有驗證者** 都會投票確認同一個檢查點（FFG 規則）。  
- **同一槽的驗證者** 投票決定最新區塊（LMD GHOST 規則）。  
- 以太坊信標鏈自 2020 年 12 月 1 日上線時，驗證者約 **21,063 名**，截至 2024 年 5 月 **已超 1,000,000 名**，證明了 PoS 的可擴展性。

補充：

[EIP-4844：大幅提升以太坊擴容能力，降低 L2 手續費的改進方案](https://kordan.medium.com/eip-4844-%E5%A4%A7%E5%B9%85%E6%8F%90%E5%8D%87%E4%BB%A5%E5%A4%AA%E5%9D%8A%E6%93%B4%E5%AE%B9%E8%83%BD%E5%8A%9B-%E9%99%8D%E4%BD%8E-l2-%E6%89%8B%E7%BA%8C%E8%B2%BB%E7%9A%84%E6%94%B9%E9%80%B2%E6%96%B9%E6%A1%88-7daa941e8ee2)


### 2025.02.20

以太坊的共識層（CL）架構涉及兩種共識協議：**LMD GHOST**（提供活性）和 **Casper FFG**（提供最終性），合稱為 **Gasper**。  

### **分叉選擇機制**
因為網路延遲、節點不同步或惡意行為，區塊鏈可能出現分叉。分叉選擇規則（Fork Choice Rule）決定哪條鏈成為最終的主鏈：  
- **工作量證明（PoW）**：最重鏈規則（Heaviest Chain Rule），即總算力最高的鏈獲勝。  
- **Casper FFG（PoS）**：選擇包含最高高度已證明（Justified）檢查點的鏈。  
- **LMD GHOST（PoS）**：選擇「當前累積投票最多的區塊」作為主鏈。  

節點根據這些規則選擇主鏈，並可能發生**重組（Reorg）**，即拋棄舊鏈的一部分並轉向更優的鏈。

### **安全性與活性**
- **安全性（Safety）**：確保區塊鏈一致，不會出現雙花或相衝突的最終區塊。  
- **活性（Liveness）**：確保系統能持續新增區塊，不會卡住。  
- **以太坊優先考慮活性**：在網路分區的情況下，即使無法最終確定區塊，鏈仍然會繼續前進。

### **共識層元件**
- **Beacon 節點**：協調 PoS 共識，與執行層（EL）和其他 Beacon 節點通訊。  
- **驗證者（Validator）**：需質押 32 ETH 來參與共識，負責提議和驗證區塊。  

### **執行層（EL）與共識層（CL）的協作**
- CL 負責選擇區塊，並透過 **Engine API** 與 EL 溝通，請求交易資料和執行交易。  
- EL 執行交易並回傳狀態，CL 會驗證狀態並確認區塊。  
- CL 和 EL 需同步執行，確保最終一致性。  

### **狀態轉換**
以太坊的狀態透過函數 **state_transition(S, B)** 更新，其中：
- **每 Slot 轉換**（固定間隔更新狀態）  
- **每區塊轉換**（當新區塊到來時更新狀態）  
- **每 Epoch 轉換**（針對 PoS 驗證者輪換）  

狀態轉換是確保所有節點達成共識的關鍵。以太坊透過 Gasper 結合 LMD GHOST 和 Casper FFG，在確保鏈條持續運行的同時，也確保了最終性。

### 2025.02.21

#### **網路協議**
- **共識客戶端** 使用 **libp2p** 作為點對點協議，**discv5** 進行節點發現，**libp2p-noise** 進行加密，**SSZ** 進行資料編碼，並可選擇使用 **Snappy** 進行壓縮。  
- **Ethereum Node Records (ENR)** 用於節點發現。  
- **libp2p-noise** 使用 XX（transmit-transmit）模式進行金鑰交換。  
- **SSZ**（Simple Serialize）是共識層的主要序列化機制，可高效進行 Merkle 化。  

#### **共識層與 Beacon Chain**
- **以太坊最初使用工作量證明 (PoW)，後來轉向權益證明 (PoS)**，共識機制結合 **Casper 和 GHOST**，並在 **Gasper** 論文中發布。  
- **Pyspec** 是共識層的可執行 Python 規範，供客戶端開發者參考。  
- **Beacon Chain** 是以太坊 PoS 系統的核心，負責管理驗證者註冊、存款與退出機制，主要負載來自「驗證投票」（Attestations）。  

#### **共識客戶端**
- **共識客戶端（CL）負責 PoS 協議運行**，但不執行交易或狀態轉換，這部分由執行客戶端（EL）負責。  
- **主要共識客戶端**：  
  - **Lighthouse（Rust）**：安全性與效能導向  
  - **Lodestar（TypeScript）**：適用於瀏覽器與快速原型開發  
  - **Prysm（Go）**：專注於易用性與可靠性  
  - **Nimbus（Nim）**：適合低資源設備  
  - **Teku（Java）**：企業級應用  
  - **Grandine（Rust）**：高效能與輕量化  
  - **Caplin（Go）**：與 Erigon 執行客戶端整合  
  - **LambdaClass（Elixir）**：仍在開發階段  

#### **弱主觀性與同步機制**
- **「客觀性」與「主觀性」**  
  - PoW 時代：區塊鏈歷史可透過創世區塊回溯驗證，屬於**弱客觀性**。  
  - PoS 時代：共識層與執行層分離，**創世區塊同步變得不安全**，引入**弱主觀性**。  

- **同步機制變化**
  1. **同步方向改變**：共識層節點需從弱主觀性檢查點回溯到創世區塊。  
  2. **同步目標帶有信任需求**：由於歷史可被改變，節點需透過**可信來源**獲取同步檢查點（不透過隨機 P2P 連接）。  
  3. **同步時間限制**：若節點長時間不同步，可能會受到歷史篡改攻擊，因此需**樂觀導入區塊**（optimistic importing）。  

- **完整同步流程**
  1. **獲取弱主觀性檢查點**（透過可信來源）。  
  2. **回溯同步至創世區塊**。  
  3. **更新執行層的目標區塊頭**。  
  4. **樂觀導入新區塊**（不驗證執行層狀態）。  
  5. **執行層同步完成後，再標記共識層區塊為已驗證**。  

補充:

[全節點與輕節點：以太坊節點面面觀 <10> 文組也該知道的區塊鏈技術知識](https://medium.com/pelith/ethereum-nodes-d3e07745d189)

[Libp2p简介](https://woxinfei666.medium.com/libp2p%E7%AE%80%E4%BB%8B-42c6d1fae469)

[點對點網路組建：從 Kademlia 到 Discv5](https://www.chaindaily.cc/posts/1dd47a7905a813bf5cf5a06ae98ed6fb)

[一文讀懂以太坊Beam Chain的願景和技術架構](https://www.gate.io/zh-tw/post/status/7695610)

[如何跑起以太坊執行層與共識層客戶端](https://medium.com/swf-lab/%E5%A6%82%E4%BD%95%E8%B7%91%E8%B5%B7%E4%BB%A5%E5%A4%AA%E5%9D%8A%E5%9F%B7%E8%A1%8C%E5%B1%A4%E8%88%87%E5%85%B1%E8%AD%98%E5%B1%A4%E5%AE%A2%E6%88%B6%E7%AB%AF-54d0b472e7ac)

### 2025.02.22


<!-- Content_END -->
