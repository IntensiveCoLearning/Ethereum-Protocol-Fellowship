---
timezone: Asia/Shanghai
---

---

# henryleo

1. 自我介绍 hi，我是henryleo，生物信息工程师，开放科学/DeSci爱好者，同时也对代币经济学、隐私和区块链在社会治理中的作用很感兴趣。目前专注合成生物学工作。
2. 你认为你会完成本次残酷学习吗？ 我想我可以！

## Notes

<!-- Content_START -->

### 2025.02.06

#### 2025残酷共学、EPFsg 和 EPF
EPF全称是[Ethereum Protocol Fellowship](https://github.com/eth-protocol-fellows/cohort-five/blob/main/program-guide/program-details.md)，
是一个以学徒制的形式招募、筛选和培养以太坊核心开发者的活动。可想而知EPF是小规模且深入的活动，为了吸引更多开发者加入以太坊生态，
EPF Study Group（EPFsg）被提出，以相对浅显的形式介绍以太坊，从开发哲学到路线图均有涉及，更方便广大开发者、研究员，
甚至爱好者了解以太坊的核心组织架构、开发进展以及目前面临的技术问题。

残酷共学是ETHPanda主办，以中文社群为主，基于EPFsg的材料的共学获得，每日打卡但并不限制学习进度（无需许可的进展2333），旨在为中文社群更好地连接至EPFsg

### 2025.02.07

Encryption 加密 是将一个被称为Plaintext 明文的信息，对其进行一种操作，称为Cipher 密码。这样，你就会收到一个混乱的、不可读的信息作为输出，称为Ciphertext 密码文本。而将密码文本转会为可读的明文的过程称为Decryption 解密

#### Cipher 密码 
由两部分组成的：
- Encryption algorithm 加密算法 用于将明文转换为密文的基本逻辑或过程
- Key 密钥 为你的密码引入了一些独特的东西。如果没有密钥，任何使用相同算法的人都能解码你的信息，而你实际上不会有任何保密性
    - 是保护你的数据的独特部分，对称密钥必须保密以确保被保护数据的机密性。Key size 密钥大小，以bit为单位，是组成加密密钥的比特或数据的总数。可以把密钥大小看作是一个给定加密算法可能的密钥总数的上限。Key length 密钥长度在密码学中超级重要，因为它本质上定义了系统的最大潜在强度

#### Kerckhoff's principle 柯克霍夫原则
又名"the enemy knows the system" “敌人了解系统“， Shannon's maxim 香农箴言

该原则指出，一个Cryptosystem 密码系统，或一个用于Key generation 密钥生成和Encryption 加密及Decryption 解密操作的算法集合，构成了一个密码服务，应该保持安全，即使关于该系统的一切都被知道，除了密钥。这意味着，即使你的敌人知道你用来保护数据的确切加密算法，他们仍然无法从截获的密码文本中恢复明文。

#### Cryptography 密码学
定义了加密，但涵盖编码和隐藏信息不被第三方发现的做法的总体学科。与此相反，寻找隐藏信息或试图破译编码信息被称为Cryptanalysis 密码分析

- Frequency analysis 频率分析 是研究字母在密码文本中出现的频率的做法 最早记录是来自一个九世纪的阿拉伯数学家

##### 对称密码学
Symmetric-key algorithm 对称密钥算法，这类型的加密算法被称为symmetric 对称算法，因为它们使用相同的密钥来加密和解密信息。对称加密的最大缺陷是假设密钥可以传达给预期的接收者，而不会将其暴露给不需要的一方。换句话说，无论是单个数字、秘密词还是具有特定配置的机器，密钥都必须以受信任的设置从发送方传递到接收方。所有后续消息的安全性取决于维护密钥的安全传输。
- Substitution cipher 替换密码 是一种加密机制，用密码文本替换部分明文。Caesar cipher 凯撒密码 是一种替换加密技术，明文中的所有字母都在字母表上向后（或向前）按照一个固定数目进行偏移后被替换成密文，如：当偏移量是3的时候，所有的字母A将被替换成D，B变成E，以此类推。另一种例子，Vigenère cipher 此密码不是使用常量值来交换消息中的每个字母，而是根据秘密词（secret code word，也称为key 密钥）中字母的字母顺序来改变每个字符的偏移量。 如：密钥 abc 会将编码单词的第一个字母按字母顺序移动一个字母，将第二个字母移动 2 个字母，将第三个字母移动 3 个字母
- Block ciphers 区块密码，它将明文分成多个等长的模块（block），使用确定的算法和对称密钥对每个区块分别加密解密。
- Stream ciphers 流密码，加密和解密双方使用相同pseudo-random stream 伪随机加密数据流作为密钥，明文数据每次与密钥数据流顺次对应加密（Simple XOR cipher 简单异或密码），得到密文数据流。

**一些实例：**
- DES Data Encryption Standard 数据加密标准：使用128位区块密码
- AES Advanced Encryption Standard 高级加密标准：对称的区块密码
- RC4 Rivest Cipher 4：一种串流加密法，密钥长度可变。
- TLS 1.2 + AES GCM：是AES区块密码的一种特殊操作模式，基本上将其变成了流密码。

##### Asymmetric Cryptography 非对称密码学
又称Public-key cryptography 公开密钥加密。它需要两个密钥，一个是公开密钥，另一个是私有密钥；公钥用作加密，私钥则用作解密。使用公钥把明文加密后所得的密文，只能用相对应的私钥才能解密并得到原本的明文，最初用来加密的公钥不能用作解密。
- 第一步，A、B交换公钥
- 第二步，A使用B的公钥加密信息并发送
- 第三步，B接受接受加密的信息，通过B的私钥将加密信息解密为明文

> 公钥/私钥的物理隐喻是个人锁定邮箱。任何人都可以在其中存放一封信，但只有邮箱的所有者才能打开它并阅读其中包含的消息。

**对称与不对称密码系统的比较：**
- 不对称密码系统在不受信任的信道上传输比较安全
- 对称密码系统的算法速度更快，效率更高，可以加密大量的数据
- 有时可以联合使用，通过不对称密码系统传输对称密码系统的密钥，通过对称密码系统的密钥解锁数据

**非对称密码系统实例**
- RSA：最早的非对称密码系统 以发明人首字母命名 密钥的生成过程取决于选择两个独特的、随机的、通常是非常大的素数
- DSA Digital Signature Algorithm 数字签名算法：这个系统的安全性取决于选择一个随机种子值，并将其纳入签署过程。如果这个值被泄露了，或者可以推断出质数不是真正的随机数，那么攻击者就有可能恢复私钥
- DH Diffie-Hellman 一种流行的密钥交换算法
- ECC** **E**lliptic **c**urve **c**ryptography  椭圆曲线密码学， 传统的公钥系统是利用大素数的因式分解，ECC使用有限域上的椭圆曲线的代数结构来生成安全密钥。
    - 椭圆曲线是由一组符合等式的坐标组成的，类似于 $y^2=x^3+ax+b$。一个是**水平对称性**，这意味着在曲线的任何一点都可以沿X轴进行镜像，并且仍然构成相同的曲线。除此之外，任何**非垂直的直线**最多只能在三个地方与曲线相交。
    - **正是这最后一个特性使得椭圆曲线可以被用于加密**。基于椭圆曲线的加密系统的好处是，它们能够以较小的密钥规模实现与传统公钥系统类似的安全性
        - 举例来说，一个256位的椭圆曲线密钥，将与一个3072位的RSA密钥相当。这确实很有利，因为它减少了处理密钥时需要存储和传输的数据量

**Cryptography Applications 密码学应用**
- PKI Public Key Infrastructure system 公钥基础设施系统
- Web of Trust 信任之网
- Pretty Good Privacy （PGP） 优良保密协议

#### Hashing 哈希
又名Hash function 散列函数，是一种函数或操作，它接收任意数据输入并将其映射到一个固定大小的输出，称为Hash 散列或digest 摘要。

哈希不同于加密，哈希是单向的、不可逆的，但运算速度快，一旦有微小的变化哈希函数就会发生改变

**Hash collisions 哈希冲突**
- 即两个不同的输入映射到同一个输出，这是不应该存在的、需要修正的

**一些例子**
- MD5：它在512bit的block 区块上运行，并产生128bit的哈希值。是一个流行和广泛使用的散列函数，设计于20世纪90年代初，是一个加密散列函数
- SHA-1：它操作一个512bit的区块并生成160bit的哈希值 是一个广泛使用的加密散列函数，用于流行的协议，如TLS/SSL、PGP SSH和IPsec。也用于像Git这样的版本控制系统，它使用哈希值来识别修订版，并通过检测损坏或篡改来确保数据的完整性。
- MIC Message Integrity check 信息完整性检查：是有关信息的哈希值。你可以把它看成是信息的一个校验和，确保信息的内容在传输过程中没有被修改。

### 2025.02.08

#### 比特币网络

**比特币网络中交易记录的非对称加密**

每个账户有一个公钥(pk)和一个私钥(sk)，转账记录是一个明文的信息，其中唯一的交易编号，这个信息通过**签名函数**生成一个Digtal Signature电子签名（也许是一个哈希），并可以将其与信息和公钥以及另一个**验证函数**验证真伪。
![image](https://github.com/user-attachments/assets/8703d682-b7e0-4ab8-9ea1-63875dad6c47)


**Merkle tree**

Merkle Tree是一种数据结构，将已有的交易记录通过哈希散列函数反复求值合并为一个Merkle root（这也是一个Hash），并将其记录在比特币网络的Block Header区块标头中，以确保区块无法被篡改。具体的计算方法如下：
- 假设已有的交易记录有4笔，为L1~L4，通过散列函数计算其哈希（分别为H0_0、H0_1、H1_0、H1-1）
- 其次，按交易的先后顺序将其哈希两两拼接，再次计算哈希，如`H0_0+H0_1=>H0`、`H1_0+H1_1=>H1`，这样我们就把四笔交易的信息压缩为两个哈希
- 第三，将H0和H1拼接并计算哈希，得到一个Merkle root，完成压缩
- 最后，将Merkle root放入比特币网络的Block Header区块标头中
![image](https://github.com/user-attachments/assets/2367d849-1157-485d-bbce-acf0f76a9b6e)


**比特币网络解决账本的中心化问题的方法——工作量证明**

Proof of Work (PoW) 工作量证明是一种方法，其核心理念是**“信任最多工作量的结果”**，在区块链的世界里，这意味着矿工/参与者信任最长的那条区块链。
![image](https://github.com/user-attachments/assets/26cd4bc6-0890-41b0-b91e-92199ebe6dff)


要解释这一点首先要介绍工作量的来源，也是散列函数计算哈希导致的。首先先介绍比特币区块标头的数据结构：前一个区块的哈希值（Prev Hash，又称哈希指针）+随机数（Nonce）+在上文中我们描述的由Merkle tree压缩的当前区块的交易记录+时间戳。比特币的工作量来源于这个随机数，这是因为网络鼓励矿工去找到一个随机数使得整个区块标头经过散列函数（SHA256）计算后的哈希值**前若干位**为0，例如`0000000000000000000ec8769a995429b85e6301c97fa76de6fb9bc5162b27de` 

同时，比特币网络要求大约十分钟出一个块，这意味着随机数前导0的数量是动态的，当矿工算力变强，前导0的数量要求会更高，反之更少。

那么“信任最多工作量的结果”是什么意思呢？假设有恶意者试图使用假的交易记录蒙骗其他人，那他会构建一个假的Merkle tree和一个Nonce合并Prev Hash和时间戳发送给其他所有人，**且大家一定会接受！这是因为它满足要求**（前一个区块的哈希值正确、足够的前导0以及符合要求的时间戳）；但有其他矿工同时在工作，他们大概率不是同谋，所以他们有真的交易记录也会生成一个符合要求的区块标头，其他人也会接受，这时，所有人拥有两份不同且同样长度的区块链，这也就是所谓“冲突”。随着下一个十分钟，新的区块出来，为了实现攻击恶意者必须超过其他所有人计算出正确的随机值，一旦有人抢先，那么其他矿工将会受到一个不同与恶意者发布的且长度更长的区块链，届时攻击将失败。因此，恶意者必须在随后N个区块内保持领先，但根据研究，若恶意者不拥有超过网络50%总算力将无法实现攻击，这就是著名的“51攻击”。
![image](https://github.com/user-attachments/assets/d30fb872-da27-459d-8888-ece55216ff28)

但十分钟出一个区块的限制导致了交易手续费昂贵且效能不足，这也就是以太坊和其他公链谈及的“Scaling 扩容”问题

**挖矿奖励**

当矿工计算出正确的随机数时，比特币网络将会在交易记录的最上方加入一行记录——xxx创造N个BTC，再构造Merkle tree。当区块被确认（被大家认可），该矿工则拥有N个BTC的记录，这也是所谓的挖矿奖励。

比特币网络每构造21万个区块后奖励会减半，初始值为50，这保证了BTC总量在2100万颗左右。

**Refs**

- [What is the merkle tree in Bitcoin? | Keifer Kif](https://www.youtube.com/watch?v=V6gLY-1G4Mc)
- [Merkle tree | Wikipedia](https://en.wikipedia.org/wiki/Merkle_tree)
- [你有疑惑過比特幣（與其他加密貨幣）的運作原理嗎？| 3Blue1Brown](https://www.youtube.com/watch?v=bBC-nXj3Ng4)
- [比特币的区块 | 以太坊的指南针](https://ethbook.abyteahead.com/ch10/block.html)

### 2025.02.09

#### P2P、分布式网络和BitTorrent
##### P2P和分布式网络
P2P（peer to peer）区别于“服务器-客户端”模型，传统互联网需要一个中心机构储存、管理和分发数据，而P2P网络中的每一个计算机（被称为Node 节点）拥有数据的多个相同副本，这有助于防止数据操纵和控制行为的发生。

因此，P2P网络属于一种分布式网络，区块链也构筑在P2P网络的基础上。

##### BitTorrent 
BitTorrent 旨在解决依赖中心化服务器下载大文件导致的网络堵塞问题，通过将大文件切分成小块，每个用户理论上拥有一个小块，互相之间形成一个网络的全连接图，从而可以分享文件并减少网络负载。

另一个好处是对于家庭网络而言，上传带宽往往小于下载带宽，这称为“上传下载的不对称性”。因此当只有一位用户为另一位用户提供资源时速度是很慢的，这是由于上传带宽不足。而BitTorrent支持多个用户为一个用户提供资源，这使得上传带宽得以共享，在带宽资源有限的情况下提升了效能。

##### Refs
- [What is BitTorrent? | internet-class](https://www.youtube.com/watch?v=xH00ikD1oDo)
- [What is a Peer to Peer Network? Blockchain P2P Networks Explained | Lisk](https://www.youtube.com/watch?v=ie-qRQIQT4I)


### 2025.02.10

#### 为什么要有以太坊？

以太坊之所以创立是因为比特币网络的保守性，难以开发相对复杂的应用程序以支持现代金融和其他应用方式。

#### 以太坊是什么？

##### 以太坊的愿景
以太坊的愿景是“世界计算机”，我认为更好理解一点的说法是一个通用的计算平台，而不是可编程货币的平台，这在Vitalik的博客中“Gavin对以太坊的微妙愿景转变做出的贡献”有所提及。

以太坊坚持去中心化来实现无需许可、可信中立和抗审查，这并不意味着要求绝对的透明和排斥商业或其他组织，合约或者协议可以有不透明的部分，但规则和退出机制必须透明（个人理解）。要求和排斥是控制，以太坊不要控制，要**通过技术**构筑“无限花园”，这一点承接密码朋克的核心信念之一：“that the power of technology often creates new political realities.”。

###### Refs
- [A Prehistory of the Ethereum Protocol | vitalik.eth.limo](https://vitalik.eth.limo/general/2017/09/14/prehistory.html)
- [Inevitable Ethereum - World Computer](https://inevitableeth.com/home/ethereum/world-computer)
- [密码朋克 | 以太坊协议的史前史](https://epf.wiki/#/wiki/protocol/prehistory?id=cypherpunks-write-code)


### 2025.02.11

#### 以太坊的组成

以太坊通过三个Part 组件致力于实现通用计算平台：
- EVM Ethereum Virtual Machine 以太坊虚拟机
- Ethereum Blockchain 以太坊区块链
- Ethereum Network 以太坊网络

三个组件并非相互独立，而是嵌套的，EVM是一个安装在物理设备（节点）上的一个程序，其中包含以太坊区块链，而全世界的节点组成以太坊网络。

要理解以太坊这个平台不能以“服务器-客户端”的模型去理解，而是每一个节点都是一个完整的副本，即每个参与以太坊的物理世界的计算机都拥有一个可信的计算平台也就是EVM，在EVM中更新区块链。

##### Refs
- [协议架构概览 | epf.wiki](https://epf.wiki/#/wiki/protocol/architecture?id=protocol-architecture-overview)
- [节点架构](https://ethereum.org/zh/developers/docs/nodes-and-clients/node-architecture/)
- [Vitalik Buterin带你三十分钟了解以太坊 | Devcon Bogotá](https://www.youtube.com/watch?v=UihMqcj-cqc)

### 2025.02.12

#### 以太坊账户

以太坊有两种账户：
- Externally-owned account 外部所有的帐户 (EOA)
- Smart contract account 智能合约帐户

举个例子，我们在Metamask创建的账户、我们自己拥有私钥的账户就是EOA，而拥有的USDT就是智能合约账户，所以USDT有CA（Contract Address 合约地址）。

在以太坊中，EOA只能进行ETH和代币交易，假设我在我的EOA中转移USDT，实际上它并不保存在我的账户中，而是EOA和USDT的智能合约进行交互，在合约中更新了token ID

##### Refs
- [以太坊账户|EF](https://ethereum.org/zh/developers/docs/accounts/)


### 2025.02.14
#### Replay 重放攻击和Double-spending 双花攻击
重放攻击是跨链或者跨时间复制一笔交易，而双花攻击是一笔交易同一时间广播多次。

对于比特币网络，任何一个矿工都可以从一个区块读取某一笔交易的信息，假设没有时间戳，
一笔交易虽然被签名了，恶意的矿工虽然没有私钥，但它只需要将这个签名后的信息广播到新的区块就可以反复执行该笔交易，
因为签名是真的，验证函数会回传True。假设A想要攻击B，就会反复广播B的交易，这是双花攻击。

有了时间戳，这时A广播他获得的签名会发生什么？答案是会被矿工拒绝，**因为时间戳显示该区块已经被打包了**，不过这需要一些时间。因此最好的方案是等待交易确认多次后信任。

对于重放攻击，UTXO这种类似于纸币的性质天然就可以抵抗重放。

而以太坊通过Nonce防止重放攻击。以太坊中Nonce是一个账户的交易计数，
**执行层会优先执行同一个账户Nonce较小的交易（TX2会在TX1被接受或取消之后才会进行处理），
且同一Nonce的交易只会执行一次（优先费高的）**

先让我们忽略Gas fee的问题，假设发送者想做坏事，他有一个ETH，先发送一个ETH（`TX1`），
后又发送一个ETH（`TX2`），`TX2`会被拒绝，因为他账户余额不足；
他不服气，复制了一份`TX1`再广播一次（记为`TX1'`，假设此时TX1还没被接受），
但`TX1`或`TX1'`会直接被拒绝，因为只会接受一次Nonce等于1的交易。

这下他十分生气，决定做接收者并且再做坏事，当他母亲给他打生活费时，他复制了这笔交易企图获得更多，
但也被拒绝了，因为Nonce被使用过了，防御重放成功。

### 2025.02.15

#### 执行层
简而言之，执行层相当于比特币区块链去除PoW的部分，仅起到验证区块和更新区块的作用。

##### 验证区块
客户端需要：
- 上一个区块
- 当前区块
- StateDB 状态数据库：账户信息
一旦发生错误将会唤起错误，简单代码体现：
```python
def stf(parent_block: Block, current_block: Block, state: StateDB) -> StateDB:
	# something validations
	try:
		verify_headers(parent_block, current_block)
	except Error as error:
		return (state,  error) # the state no updated

	state, error = verify_transactions(current_block, state)
	if error:
		return (state, error) # the state no updated
	return state
```

###### 标头验证
```python
def verify_headers(parent_block: Block, current_block: Block) -> Optional[error]:
	# something validations
	# error = None or others
	if error:
		raise Error("...")
```
一个有意思的错误是gas超过上限，而gas上限是被硬编码的，这也制约了智能合约的复杂性。

###### 交易验证
```python
def verify_transactions(current_block: Block, state: StateDB) -> Tuple[state, Optional[error]]:
	origin_state = state.copy()
	updated_state = state.copy()
	good_tx = []

	for n, tx in enumerate(current_block):
		try:
			# some validations
		except Error as error:
			return origin_state, error
		else:
			good_tx.append(tx)
	updated_state = update_state(updated_state, good_tx)
	return (updated_state, None)
```
错了就返回原状态和错误原因，正确就更新。

###### 检验区块验证
这个东东负责告诉信标链当前区块是否验证成功
```python
def new_payload(exec_payload: ExecutionPaylaod) -> bool:
    _, error = stf(exec_payload.parent_block, exec_payload.current_block, exec_payload.state)

    if error:
        return False

    return True
```

##### 构建区块
构建区块需要：
- Environment 环境：包括一些信息，比如标头（时间戳、gas多少）、共识层的信息等
- TxPool 交易池：一个包含交易的列表，通过其价值降序排列。这个池也是根据广播中优先费最高的组成的。换句话说这些Gas信息没加密
- StateDB 状态数据库

```python
def build(env: Environment, pool: TxPool, state: StateDB) -> Tuple[Block, StateDB, error]:
    gas_used = 0  # 确定gas用量
    txs = []

	# Gas达到上限或池是非空
    while gas_used < env.gas_limit or not pool.empty():
        tx = pool.pop()
        updated_state, gas, err = vm.run(env, tx, state)
        if err is not None:
            # tx invalid
            continue
        gas_used += gas
        txs.append(tx)
        state = updated_state

	# 通过一个外包的函数回传，用于计算生产完整的块，比如一些数据压缩计算
    return finalize(env, txs, state)
```

### 2025.02.16

#### 共识层 
共识层旨在协调分布式系统的同步问题，即基于区块链的分布式系统旨在就单一交易历史达成一致，包括抵抗不可靠的节点和恶意节点。

#####  Consensus mechanism共识机制

工作量证明 PoW和权益证明 PoS是共识机制，共识机制是用来确保能够实现Consensus protocol 共识协议的。
以太坊实际上采用两种不同的共识协议，并把它们结合在一起。一种称为[LMD GHOST](https://epf.wiki/#/wiki/CL/gasper?lmd-ghost)，
另一种称为[Casper FFG](https://epf.wiki/#/wiki/CL/gasper?casper-ffg)。这种组合被称为[Gasper](https://epf.wiki/#/wiki/CL/gasper)。

###### 权益证明 PoS Proof-of-stake
区块链是一组不断延长的账本、不可串改的证明。每次延长时需要一个节点为此负责，在比特币网络中采用工作量证明——算力最强的矿工——作为负责人，
而以太坊是从质押者中随机挑选一位作为新区块的提议者。他负责将区块添加到链中，选择并排序其内容。

### 2025.02.17

#### 实现权益证明的方法——信标链
以太坊在巴黎升级中通过Beacon Chain 信标链替代原以太链的PoW机制，从原来的以太链上获得交易记录并验证。

信标链负责监督提出和证明新区块的验证者。验证者是根据一系列标准选出的，其中之一是他们质押的 ETH 数量，这也作为防止恶意行为的抵押品，也就是网络的安全经费。

验证者的工作：
- 质押 ETH：验证者必须质押至少 32 ETH 才能参与。
- 提议区块：随机选择一个验证者来提议新区块。他们必须构建有效的区块并将其广播到网络
- 参与委员会 Committees：验证者被分成多个委员会，负责区块提议和证明。每个委员会负责验证和证明区块，确保验证过程的去中心化和安全。
	- 证明区块：验证者证明其他人提出的区块的有效性。证明本质上是对区块有效性的投票，以确保达成共识。
	- 参与共识：验证者通过定期对区块链的状态进行投票来参与共识，帮助最终确定区块链的状态。

##### 选出区块提议者的随机机制
选拔过程通过加密随机性，通过[RANDAO](https://inevitableeth.com/home/ethereum/network/consensus/randao) 和 [VDF（可验证延迟函数）](https://inevitableeth.com/home/ethereum/upgrades/consensus-updates/vdf)机制实现

##### Slots 与 Epochs
12秒是一个Slot 时隙，一个时隙出一个区块，但也可以不出（没有交易）；32个时隙为一个Epoch 时期。时隙和时期的计数都是从0开始的。

##### 验证者与证明
某一个验证者被随机选为区块提议者（伪随机过程 RANDAO），这个选择的过程是以Epoch为单位的，一次选32个提议者，然后委员会的其他验证者验证该区块。验证者通过投票进行区块验证，并将投票记录放在信标链的区块标头上。验证者的投票权重与其质押量相关。

信标链的内容主要是验证者地址的registry 注册表、每个验证者的状态和证明。

质押者与其质押的ETH数量相关联，而每个验证者的最大余额为32 ETH。每质押32 ETH，即可激活一个验证者。验证者由验证者客户端运行，这些客户端通过信标节点来跟踪并读取信标链。一个验证者客户端能够管理多个验证者。

##### 委员会

当以太坊网络超过 $2^{13}=8192$ 个验证者时，每个时隙会有多个委员会，且每个委员会最少需要128个验证者，这样才安全。

当验证者小于 $2^{12}=4096$ 时，每个时隙有仅有一个委员会。

##### Blobs
[EIP-4844](https://eips.ethereum.org/EIPS/eip-4844)，又称proto-danksharding，是Deneb/Cancun硬分叉的一部分。它为以太坊引入了数据可用性层，使得在区块链上临时存储任意数据成为可能。这种数据结构被称为 `Blob`，每个区块可包含3至 6个 Blob sidecars（即Blob的封装）。这使得L2可以将交易打包送回L1验证，使得Gas费大减。

Blob这种临时数据存放4096个Epochs， 约18天。

储存要求：
$$
131,928 \space ssz \space bytes / blob * 4096 \space blobs \space retention \space period * 32 \space potential \space blocks/epoch * 3~6 \space blob \space sidecars / block = 52~104 \space GB
$$

### 2025.02.18

#### 拜占庭将军问题
Byzantine Generals Problem 拜占庭将军问题，描述的是一组分布式计算机如何通过交换信息保持协作的难题。

> 一组[拜占庭](https://zh.wikipedia.org/wiki/%E6%8B%9C%E5%8D%A0%E5%BA%AD%E5%B8%9D%E5%9C%8B "拜占庭帝国")将军分别各率领一支军队共同围困一座城市。为了简化问题，将各支军队的行动策略限定为进攻或撤离两种。因为部分军队进攻部分军队撤离可能会造成灾难性后果，因此各位将军必须通过投票来达成一致策略，即所有军队一起进攻或所有军队一起撤离。
> 
> 因为各位将军分处城市不同方向，他们只能通过信使互相联系。在投票过程中每位将军都将自己投票给进攻还是撤退的信息通过信使分别通知其他所有将军，这样一来每位将军根据自己的投票和其他所有将军送来的信息就可以知道共同的投票结果而决定行动策略。

这个问题的难点在于这些分布式电脑中可能有恶意用户，假设有9台电脑，4比4平票的时候，恶意电脑就选择反向投票，就会破坏系统。

注意：**这个问题的关键不在于答案是什么，而在于大家能不能有一致的答案。**

##### 拜占庭容错 Byzantine Fault Tolerance BFT
拜占庭容错是一个系统的特性，定义为：**在一个拜占庭将军问题中，有一个解法，满足即使若干个将军都是叛徒系统都不会发生问题**。

结论是：只要三分之二的节点同意一个答案，就能达成拜占庭容错。

推导过程略。

##### 比特币网络达成拜占庭容错
比特币网络通过其工作量证明实现拜占庭容错，即选择算力消耗最高的结果，实现共识机制。

##### Refs
- [拜占庭将军问题|维基百科](https://zh.wikipedia.org/wiki/%E6%8B%9C%E5%8D%A0%E5%BA%AD%E5%B0%86%E5%86%9B%E9%97%AE%E9%A2%98)
- [了解区块链的基本（第一部分）：拜占庭容错(Byzantine Fault Tolerance)|Loom Network](https://medium.com/loom-network-chinese/%E4%BA%86%E8%A7%A3%E5%8C%BA%E5%9D%97%E9%93%BE%E7%9A%84%E5%9F%BA%E6%9C%AC-%E7%AC%AC%E4%B8%80%E9%83%A8%E5%88%86-%E6%8B%9C%E5%8D%A0%E5%BA%AD%E5%AE%B9%E9%94%99-byzantine-fault-tolerance-8a1912c311ba)
- [第三周|EPS 2024](https://epf.wiki/#/eps/week3)

#### 以太坊的共识机制
工作量证明 PoW和权益证明 PoS是共识机制，共识机制是用来确保能够实现Consensus protocol 共识协议的。拜占庭将军问题是共识问题的一种描述形式，共识协议是实现拜占庭容错的途径。

> [!以上这些的概念容易混淆！]
> 共识机制 -实现-> 共识协议 -实现-> 拜占庭容错 -克服-> 拜占庭将军问题（分布式网络通信）



<!-- Content_END -->
