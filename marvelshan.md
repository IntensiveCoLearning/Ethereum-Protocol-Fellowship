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

<!-- Content_END -->
