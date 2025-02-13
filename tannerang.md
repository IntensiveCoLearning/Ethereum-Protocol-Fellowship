---
timezone: Asia/Shanghai
---

---

# Tanner

1. 自我介绍
Hi, I'm Tanner. I'm excited to dive deeper into the Ethereum protocol and can't wait to learn more at this event!
1. 你认为你会完成本次残酷学习吗？
As much as I can.

## Notes

<!-- Content_START -->
### 2025.02.06

完成 week0 和部分 week1 內容
瀏覽 epf.wiki 一些內容，有很多典故是第一次聽，對於歷史有更宏寬的了解
同時也去底下連結做了些有關乙太坊的題目順便複習
https://ethereum.org/quizzes

### 2025.02.08

瀏覽 Execution Layer 的 EL Spec，順便複習 EIP-1559 在做什麼。

EIP-1559
- 引入動態 baseFee 的機制來做到費用可預測性和優化尖峰時期使用體驗
- 改變了原有 gas 費用結構，一是引入 baseFee 且其值會根據當前區塊的需求而浮動，二是用 priorityFee 作為激勵礦工優先處理交易的小費
- 當一區塊 gas 的使用程度超過 50%，baseFee 將上升，反之則下降，最大漲跌為 12.5%，其中，若新的區塊持續保持最大使用量，將在 200 block 達到 baseFee = 1 Ether
- baseFee 將被 burn 掉，而不是支付給驗證者，燃燒可以減少總供應量，藉此降低通膨壓力

### 2025.02.10

看 Week2 影片部分內容
瀏覽 EL Spec 的 Transaction Execution
其中，當 MessageType 是創建合約：
- 新建立的合約地址會是 `address = keccak256(rlp.encode([sender_address, sender_nonce]))[12:]`
- 新合約 Nonce 等於 1，Balance 等於 pre-existingValue + msg.value​​ `σ∗[newAccount]≡(Nonce=1,Balance=preexistingValue+Tvalue​​,Storage=TRIE(∅)​,CodeHash=KEC(())​))`

### 2025.02.11

把 Week2 影片看完，筆記明日補上

### 2025.02.12

在 CL 的 verifyHeader 中的 `errInvalidUncleHash`:
- `Uncle Block` 是指兩個重複且高度一樣的 block，它只在 PoW 下存在，原因是當兩個礦工幾乎同時挖出新區塊且節點之間尚未溝通，但只有一個可被加入 Canonical chain，另一個則是 Uncle Block
- Uncle Block 雖然不是主鏈的一部分，但仍然會獲得部分獎勵，藉 Uncle 機制可以用來減少 PoW 中心化挖礦的優勢
- Uncle Chain 不等於 Orphaned Chain，當發生較長的分叉，較短的那條鏈就會成為 Orphaned Chain，在上面的區塊不會得到任何獎勵，且會被網絡拋棄，交易需要重新打包到主鏈中
- 由於 PoS 的驗證者是預先選定的，不像 PoW 存在多個礦工同時競爭的情況，所以 `UncleHash` 在 PoS 之下沒有意義，在 CL 會直接將 `UncleHash` 判斷為 `EmptyUncleHash`，否則回傳 `errInvalidUncleHash`
- `header.Difficulty` 在 PoS 後也是 0



<!-- Content_END -->
