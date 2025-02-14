---
timezone: Asia/Shanghai
---

# {evan wu}

1. 自我介绍
大家好，我叫evan wu，从事web3开发有2年时间，希望和大家一起交流学习
2. 你认为你会完成本次残酷学习吗？
必须的
3. 你的 Telegram

## Notes

<!-- Content_START -->

### 2025.02.06
学习了以太坊的协议层架构，分为共识层(CL)和执行层(EL) 
其中：
CL：负责区块排序，提供共识证明，形成一个公共的账本
EL：负责和用户进行交易，以及交易的执行和交易状态的生产，是真正链上程序本地执行的地方

在具体实现中，CL和EL有各自独立的客户端，api以及p2p网络，CL和EL之间通过Engine api来进行交互，共同完成交易上链的过程

CL常见的客户端实现有：Prysm, Teku, Nimbus, Lighthouse, Lodestar
EL常见的客户端实现有：Besu，Erigon, Go-Ethereum(geth), Nethermind

### 2024.02.07
学习了以太坊账户模型的分类
以太坊账户模型可以分为EOA账户和Contract账户
EOA账户模型包含nonce和balance两个字段，balance用于记录账户余额，nonce从0开始递增，每发送一笔交易加1，这是为了防止交易重放
Contrac账户模型包含nonce、bance、storageRoot和codeHash四个字段，其中balance用于记录账户余额，nonce从1开始，通过该合约每部署一个新合约nonce值加1，storageRoot用于存放状态数据的roothash，而codeHash用于存放合约代码的hash值

对于EOA账户和Contract账户地址的生成：
EOA：hash(公钥）
Contract地址有create和create2两种生成方式
create：senderAddress + nonce
create2:keccak256(deployer_address ++ salt ++ keccak256(init_code))


### 2024.02.08

### 2024.02.09
学习了以太坊的合约升级方法，一般合约升级有两种通用的做法
Data separation
即逻辑合约和数据合约进行分离，然后有一个代理合约调用逻辑合约，升级的时候只要将逻辑合约升级，同时更新代理合约中的地址即可。
Delegatecall-base proxies
detegatecall即委托调用，即当前合约委托其他合约调用自己，delegatecall请求访问的数据是当前合约的数据
该方法升级的思路是让数据合约使用delegatecall来委托调用逻辑合约，当逻辑合约升级后，只要在数据合约中调用升级之后的逻辑合约即可


### 2024.02.10
今天学了了以太坊EVM的相关内容
EVM是以太坊协议的核心内容之一，是合约的执行环境
EVM是一个基于栈的执行环境，其数据存储的地方包括Stack、memory和storage三部分，并且定义了一些op code用于相关的数据操作
其中stack是一个基于栈的数据结构，大小为256bit * 1024，栈上的数据只能在当前合约使用
memory是内存基本的数据存储结构，可以按照节点字节进行寻址，每次可以读取256位，但是写入只能是8bit或者256bit
storage是持久化的数据存储，gas费用最贵

### 2024.02.11

<!-- Content_END -->
