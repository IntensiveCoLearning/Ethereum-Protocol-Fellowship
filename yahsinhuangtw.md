---
timezone: Asia/Taipei
---

# Yahsin Huang

1. 自我介绍：大家好，我是 Yahsin。第一次參加以太坊協議殘酷共學，相當開心。期待對以太坊底層協議有更深刻的理解。
2. 你認為你會完成這次的殘酷學習嗎？希望！

## Notes

<!-- Content_START -->

### 2025.02.06

今天聽了約 20 分鐘 Chloe 主持的殘酷共學星期四的 weekly call，發現班長好認真，居然去年整整跟了一次特訓，還寫了很多精美的筆記。感覺花好多時間和力氣去做這個事。聽到她對 light client 主題有興趣，還有對另一個主題也有興趣，但當時因為在路上，網路不是很穩，剛好沒有聽到她說另一個她也有興趣的主題是哪一個。可能再找機會請教。晚上看了幾段 epf wiki 網站 week 1 pre-reading 的段落，其中提到一個很久以前的影片，可能是 1982 年拍攝製作的訪談類型節目，影片標題是 AT&T Archives: The UNIX Operating System。大概看了前十分鐘，訪談內容有提到 modularity 模組化的概念，裡面的老師們都講得很好，影片值得觀看。

<img width="684" alt="Screenshot 2025-02-06 at 9 39 37 PM" src="https://github.com/user-attachments/assets/e01e1ce5-9aeb-430b-b9a9-8d02b7c3ce8c" />

### 2025.02.07

今天先看了老師怎麼介紹第一週的內容，看了前二十分鐘。Ethereum Protocol 101 talk by Mario Havel on StreamEth
想到自由軟體 « Logiciel libre » [free software]  同時參考 https://www.gnu.org/philosophy/free-sw.html 提及的 “free” as in “free speech” 這邊的意思是自由，不是免費。文件提到可借用法語和西語的 libre 自由。We sometimes call it “libre software,” borrowing the French or Spanish word for “free” as in freedom, to show we do not mean the software is gratis.

另外參考維基百科 https://en.wikipedia.org/wiki/Gratis_versus_libre 的介紹 "The adjective free in English is commonly used in one of two meanings: "at no monetary cost" (gratis) or "with little or no restriction" (libre)."

自由軟體 https://fr.wikipedia.org/wiki/Logiciel_libre 

同時參考法語介紹 Qu'est-ce que le logiciel libre ? 
https://www.gnu.org/philosophy/free-sw.fr.html#TransNote1
Notes de traduction
a. Free veut dire « libre », mais aussi « gratuit ».


### 2025.02.08

今日的學習主要是觀看 v 老師三十分鐘深入淺出以太坊 2022 年這場演講「Ethereum in 30 minutes by Vitalik Buterin | Devcon Bogotá」，也就是 Week 1 推薦的延伸學習內容 https://epf.wiki/#/eps/week1?id=implementations-and-development 看了前二十分鐘。

https://youtu.be/UihMqcj-cqc?si=MqL3ac9Xg30LPJmE

<img width="666" alt="Screenshot 2025-02-08 at 11 36 48 PM" src="https://github.com/user-attachments/assets/2c9dbd0f-ae2a-400d-b334-1ff23da9d45a" />


### 2025.02.10
今日下午殘酷學習時間，看完了後半段的 v 老師 2022 年深入淺出認識以太坊系列演講。老師三十分鐘以太坊言講主題每年都會講一次，這場有幾張簡報更新。接近尾聲的地方有提到美國電腦科學家 Ralph C. Merkle 老師。根據 v 老師的演講說法，這位七十歲電腦科學家近期可能有在忙人體冷凍技術 cryonics 的東西。

<img width="665" alt="Screenshot 2025-02-10 at 6 07 39 PM" src="https://github.com/user-attachments/assets/d0a772a2-c45b-4c18-96b7-dd099159ad8e" />

<img width="642" alt="Screenshot 2025-02-10 at 6 15 23 PM" src="https://github.com/user-attachments/assets/e5673106-519c-45cd-b85f-474cc5c6b4e0" />

這裡要強調的重點是，merkle tree 在以太坊驗證資料上持續扮演重要角色。以太坊技術底層中到處都有使用到 merkle tree，主要用途是在以太坊的驗證資料方面。你要驗證有龐大的 40 gb 的 state 資料的某一塊小小的資料時，你不需要全部 40 gb 都撈出來驗證，只要一小塊 tree 的某些節點資料拿出來就可以驗證。

### 2025.02.12

今日晚上殘酷學習時間，拜讀了 Nic Lin 林老師今天發表的新文章「Ethereum Pectra 硬分叉介紹」https://medium.com/taipei-ethereum-meetup/ethereum-pectra-eips-introduction-1f90f4ea25d5  

<img width="749" alt="Screenshot 2025-02-12 at 9 12 55 PM" src="https://github.com/user-attachments/assets/888b2f3c-3dfc-4114-bd1f-c0e2fdab1206" />

中間段落提到，EIP-7251: Increase the MAX_EFFECTIVE_BALANCE 這段，提及 EIP-7251 之後，質押下限（MIN_ACTIVATION_BALANCE）仍然是 32 ETH，但上限（MAX_EFFECTIVE_BALANCE）大幅調高為 2048 ETH。這裡意思是之後就可以質押 32~2048 ETH 這麼大一個範圍。

<img width="713" alt="Screenshot 2025-02-12 at 9 12 16 PM" src="https://github.com/user-attachments/assets/a230bed3-ce10-44b8-8c71-37e1b5e6e618" />

還有一段提到 EIP-7702 這個改進，最關鍵的改動是，之後 EOA 可以搖身一變成合約。老師文中舉例，如果你填一個 Safe 合約地址，那你的 EOA 就會變身成為 Safe 合約。

### 2025.02.13
晚上殘酷學習時間，聽完整整一個半小時的 matt 老師報告（Study Group Week 2 | Execution Layer）https://epf.wiki/#/eps/week2 
覺得老師好厲害，可以這樣邊打字邊解釋說明很多細節。同時也感覺到整個系統的複雜性。

<img width="937" alt="Screenshot 2025-02-13 at 10 42 55 PM" src="https://github.com/user-attachments/assets/9b5a7902-1cf2-437b-ab47-44dea1d7906a" />

### 2025.02.14

今晚的殘酷學習時間聽了 Alex Stokes 老師怎麼介紹「狀態機複製 State machine replication」概念。https://en.wikipedia.org/wiki/State_machine_replication 

很多年前，曾經和 Alex 老師有一面之緣，簡單打過招呼，可能是在 2019 年澳洲雪梨的那次。記得當時他沒有留鬍子，看起來很年輕，有種獨特的優雅氣質。現在好像全然變一個人的樣子，似乎個人風格有變化，覺得有點奇妙。

<img width="866" alt="Screenshot 2025-02-14 at 7 30 46 PM" src="https://github.com/user-attachments/assets/95226fbb-fa03-4c17-9379-ad2a249aca9a" />

以下這邊開始就是我邊聽邊打字出來的內容，一方面練習英文聽力，一方面期望進一步強化 狀態機複製 State machine replication 的概念理解。

Ethereum Consensus Layer | Alex Stokes | Week 3
https://www.youtube.com/live/FqKjWYt6yWk?si=w0jmYFctZtqgVG7G

https://epf.wiki/#/eps/week3

One topic being discussed by the lecturer, Alex Stokes, was the concept of consensus via “state machine replication.” The following are his words introducing this concept in about 2 minutes (lecture video time 20:13–21:39).

This concept is called “state machine replication.” The “replication” here refers to the fact that we have multiple nodes in the system; they essentially all duplicate the same work. This is like an input log to get the same output. In particular, this is what we mean by consensus: every node in the system should eventually agree on the outputs.

You write your program or protocol as a deterministic function of the inputs. Imagine then that if you have an honest node, they’re going to run the same function on the same inputs, and they have to get the same output, right? This is assuming there are no bugs or anything in the protocol. For the same set of inputs, you get the same output.

This is useful to get rid of our single trusted operator because as the number of nodes increases, this becomes harder to attack. Rather than exploring a bug on one node and taking down the whole system, you now have to attack, say, two or three, or maybe all of them. And there’s this notion of a majority in the system. This is really what we mean when we say consensus: at any point in time, there should be some majority of nodes that all have the same view, the same output, or the same state.

When they do this, then, even if some of the nodes are faulty, you still have a majority of them saying, "This is the state of the world." So, the idea is that it becomes much harder now to attack our system as we have more nodes who are doing the same thing.

### 2025.02.15

星期六的早上殘酷學習時間，繼續看了一段 Alex Stokes 老師 Week 3 針對 Consensus Layer 的介紹，其中一些內容讓我想到 Tim Roughgarden 老師也講過類似的主題，只是 Tim Roughgarden 老師講得更深入且用詞更精確。像是 Tim Roughgarden Lectures 頻道其中一個系列影片「Foundations of Blockchains (Lecture 1.4: State Machine Replication)」 https://youtu.be/EaPBj_EUBPI?si=XHUeohYZ4IgxbV14 就有詳細介紹 State Machine Replication。

### 2025.02.16

週日晚上殘酷學習時間，主要觀看第四週的報告老師 Mario Vega 談 Testing 的主題「Testing & Security Overview | Mario Vega | Week 4」https://www.youtube.com/live/PQVW5dJ8J0c?si=Ee0MeIE6hnvN5hDB 

https://epf.wiki/#/eps/week4

<img width="882" alt="Screenshot 2025-02-16 at 10 46 54 PM" src="https://github.com/user-attachments/assets/4b2fae98-00c4-4912-ac20-df9ffb1fe562" />

談了與 EVM 相關的議題，例如 EVM testing - Tests Filling 以及 EVM testing - Fuzzing Differential State Testing 等等議題，看影片聽老師介紹一段，光是 EVM testing 就花了很長一段時間討論，感覺實際作業相當複雜。

<img width="879" alt="Screenshot 2025-02-16 at 10 57 28 PM" src="https://github.com/user-attachments/assets/79c54b40-31e9-4293-a14f-c2db1b5a0eb0" />

### 2025.02.18

週二晚上殘酷學習時間來關心第五週的主題 https://epf.wiki/#/eps/week5 Ethereum Research and Roadmap | Domothy | Week 5 

https://www.youtube.com/live/UClaoL12W00?si=BnPEXWymzFRuuAs2 

<img width="867" alt="Screenshot 2025-02-18 at 11 33 18 PM" src="https://github.com/user-attachments/assets/cbc1aa15-6c39-4adf-afbe-aafc7a47511b" />

<img width="865" alt="Screenshot 2025-02-18 at 11 34 57 PM" src="https://github.com/user-attachments/assets/39576d99-6d85-4435-8d9c-7a94660f93bc" />

<img width="208" alt="Screenshot 2025-02-18 at 11 38 44 PM" src="https://github.com/user-attachments/assets/137c5733-fa34-4dc0-8d94-c4115e5a2d98" />

老師的大橘貓登場五秒鐘

<img width="864" alt="Screenshot 2025-02-18 at 11 40 03 PM" src="https://github.com/user-attachments/assets/d6060e0a-b868-4d0d-9e1d-3fd3ca968e2a" />

Rollups from 10,000 feet

<img width="871" alt="Screenshot 2025-02-18 at 11 48 13 PM" src="https://github.com/user-attachments/assets/355b553e-10f7-4aaf-9e84-b9764a3dc753" />

### 2025.02.19

今日的殘酷學習 帕斯卡 Blaise Pascal 機率論，同時也關心 a16z crypto research 近期在忙些什麼。

https://a16zcrypto.com/posts/article/crypto-readings-resources/

<!-- Content_END -->
