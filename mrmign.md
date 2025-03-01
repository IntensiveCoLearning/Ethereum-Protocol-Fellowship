---
timezone: Asia/Shanghai
---

# mrmign

1. Web2->Web3新人，之前学习过Sui和Move，但是理解不够深。想要深入理解区块链生态还是要从以太坊开始。
2. 你认为你会完成本次残酷学习吗？ Yes, Just do It!

## Notes

<!-- Content_START -->

### 2025.02.06
### Learning general concepts:
Learn [Inevitable Ethereum - World Computer](https://inevitableeth.com/home/ethereum/world-computer)
- Btc came up the promise: fair payments, for anyone, at any time, forever
- The World Computer is made of up 3 parts:
	- Ethereum Virtual Machine (EVM)
		- a Turing-complete distributed state machine
	- Ethereum Blockchain
		- A [block](https://inevitableeth.com/home/ethereum/blockchain/block) is made up of 3 key components:
			- A record of the [transactions](https://inevitableeth.com/home/ethereum/blockchain/transaction) executed at the time the block was created
			- A [signature](https://inevitableeth.com/home/concepts/digital-signatures), unique to each specific block
			- A reference to the previous block's signature
	- Ethereum Network
		- is made up of a group of people and institutions who decide to run an Ethereum node
		- A single node runs two pieces of software:
			- a consensus client
			- an execution client (responsible for operating the EVM)
		- PoS(2022) <- PoW(2015)
			- Stake 32ETH to become a validator

### 2025.02.07
- Ethereum Accounts
	- the information("state") that the blockchain keeps track of is make up of accounts.
	- Two types of accounts:
		- Externally owned account(EOA), represents the user
		- Contract, a computer program that lives on-chain
- Gas
	- Gas is the "unit" of resource consumption within Ethereum
- Ethereum fundamental principles:
	- Simplicity
	- Universality
	- Modularity
	- Non-discrimination
	- Agility
- [The vision for the Ethereum roadmap](https://twitter.com/VitalikButerin/status/1741190491578810445)
	- **The Merge**: upgrades relating to the switch from proof-of-work to proof-of-stake
	- **The Surge**: upgrades related to scalability by rollups and data sharding
	- **The Scourge**: upgrades related to censorship resistance, decentralization and protocol risks from MEV
	- **The Verge**: upgrades related to verifying blocks more easily
	- **The Purge**: upgrades related to reducing the computational costs of running nodes and simplifying the protocol
	- **The Splurge**: other upgrades that don't fit well into the previous categories.

### 2025.02.08
- ### Week2 Pre-reading
- ### Nodes and clients
	- Node Types
		- Full node
			- Full nodes do a block-by-block validation of the blockchain, including downloading and verifying the block body and state data for each block
		- Archive node
			- Archive nodes are full nodes that verify every block from genesis and never delete any of the downloaded data.
		- Light node
			- Light nodes only download block headers. Any other information the light node requires gets requested from a full node.
	- Synchronization modes
		- Execution layer sync modes
			- Full sync
			- Fast sync
			- Snap sync
			- Light sync
		- Consensus layer sync modes
			- **Optimistic sync**, a post-merge synchronization strategy designed to be opt-in and backwards compatible, allowing execution nodes to sync via established methods
			- **Checkpoint sync**(weak subjectivity sync), It's based on assumptions of [weak subjectivity](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/weak-subjectivity/) which enables syncing the Beacon Chain from a recent weak subjectivity checkpoint instead of genesis


### 2025.02.09
### Execution Layer(Eth1)
- **核心功能**：
	- **交易处理**：
		- 执行层负责验证和执行用户发起的交易（例如转账 ETH、调用智能合约）。
		- 每笔交易需要支付 **Gas 费用**（以 ETH 计价），用于补偿网络的计算资源消耗。
	- **智能合约执行**：
		- 智能合约的代码在 **以太坊虚拟机（EVM）** 中运行，执行层通过 EVM 确保合约按预定逻辑执行。
		- EVM 是以太坊的“全球计算机”，所有节点运行相同的代码以保证一致性。
	- **状态管理**：
		- 执行层维护以太坊的全局状态（State），包括：
			- 账户余额（ETH）。
			- 智能合约的存储数据。
			- 账户的 nonce（防止重放攻击）。
	- **Gas 机制**：
		- 每笔交易需要指定 Gas Limit 和 Gas Price，Gas 用于限制计算资源的使用。
		- 如果 Gas 不足，交易会失败并回滚，但已消耗的 Gas 不会退回。
- **核心组件：**
	- **以太坊虚拟机（EVM）**：
		- EVM 是执行智能合约的沙盒环境，完全隔离且确定性（相同输入必得相同输出）。
		- 支持 EVM 兼容的智能合约编程语言（如 Solidity、Vyper）。
	- **账户系统**：
		- **外部账户（EOA）**：由私钥控制的用户账户，可发起交易。
		- **合约账户（CA）**：由代码控制的账户，存储智能合约的代码和状态。
	- **交易结构**：
		- 每笔交易包含以下关键字段：
			- `from`：发送者地址。
			- `to`：接收者地址（如果是合约创建，则为空）。
			- `value`：转账的 ETH 数量。
			- `data`：调用合约时的输入数据。
			- `gasLimit`：交易允许消耗的最大 Gas。
			- `gasPrice`：用户愿意支付的 Gas 单价。
	- **状态树（Merkle Patricia Trie）**：
		- 以太坊使用状态树存储所有账户和合约的状态，通过哈希保证数据的不可篡改性。
	- **执行客户端**：
		- 执行层的软件实现（如 **Geth**、**Nethermind**、**Besu**），负责处理交易、运行 EVM、维护状态等。

### 2025.02.10
- wiki的知识点感觉有点零散，读《Absolute Essentials of Ethereum》梳理下整体脉络。
- **Ch2. Execution Layer**
	- Ethereum address are 42-character hexadecimal identifiers derived from the last 20 bytes of the public key with 0x prefix.
		- more intuitive and user-friendly account experience called **Account Abstraction**
	- EOA
		- address + associated account state
		- contains two fields:
			- **Nonce**, is an increasing number showing how many transactions an account has made and how many contracts it has created. It is used to determine the order of transactions in the same slot.
			- **Balance**, how much ETH is holding.
	- Contract Accounts
		- are smart contracts that have been deployed on Ethereum and are controlled by their own internal code.
		- Ethereum address + associated account state
		- contain a state of four fields:
			- **Nounce**, incremeting number showing how many contracts the contract account has created ??
			- **Balance**, how much ETH the contract account is holding
			- **Code**, is the smart contract code contained in the account
			- **Storage**, maps the contents of the contract account. When a transaction involving a contract account is processed, the changes are recorded permanantly in the contract's Storage.
	- Transactions (two types)
		- Message Call
			- Value, ETH
			- Input Data
				- EOA-EOA, arbitrary Data, perhaps to send a message or tag a transaction. *Usually is left empty*
				- EOA-contract, contract-contract, includes the contract's Code  to be invoked and any proposed changes to Storage.
		- Contract Creation
			- request a new contract account to be added to the Ethereum world state.
			- sent to an empty address since there's no recipient
			- once initialised, are a combination of the sender's address and the last Nonce from the sender's account
	-

### 2025.02.11
- 《Absolute Essentials of Ethereum》Ch2 **Execution Layer**
	- **Ether & Transaction Fees**
		- Gwei is used to denominate transaction fees.
		- **gas cost** and **gas fees**. In Ethereum, computational cycles are calculated in a unit call gas. A gas unit is not a currency unit. Gas cost relates only to how many computational cycles are needed.
		- *Every computational instruction(an Opcode) in a transaction has an associated gas cost.*
		- The Gas Limit included in a transaction is the maximum amount of gas that a user is willing to pay for.
		- Gas fees have two forms.
			- **base fee**, refers to the algorithmically dynamic cost of gwei in the Ethereum network
			- **priority fee**, get transaction accepted faster
		- Transaction fees = gas cost * (base fee + priority fee)
		- The above is pre-2021 situtaion(London Upgrade/EIP-1559)
		- The base fee is burnt and removed from circulation.
		- The priority fee is paied to the users called validators.
	- **Transaction Structure**
        | Field | comment |
        |---|---|
        | From | sending address |
        | To | receiving address |
        | Digital Signature | a signature produced using the private key of the sender |
        | Nonce | show how many transactions an account has made |
        | Value | the ETH to be transfered |
        | Input Data | Input data(message call) ; Initialise(contract creation) |
        | Gas Limit | limit on gas |
        | Max Priority Fee | maximum priority fee you will pay |
        | Max Fee | maximum overall fee you will pay |
    - **Ethereum Virtual Machine(EVM)**
		- the most important field is the **Input Data**, because it contains the function we want to call and the arguments we want to pass.
		- it follows Application Binary Interface(ABI) format.
		- functions are identified in the ABI specification by the reference MethodID.
		- `transfer(address to, uint256 value)`
			- MethodID: `0xa9059cbb`
			- ByteCode: `0xa9059cbb00000000000000000000009f11260cb6427c20a019780d99d3a2d7ffe9a25300000000000000000000000000000000000000000000000000002c8650c0`
		- The EVM interprets and executes the Input Data field using the following:
			- **Virtual Read-Only Memory(ROM)**: Reads the code of an involved contract account
			- a temporary state for processing the transactions:
				- **Program Counter**: The program counter tracks what instructions from the contract code need to be processed next
				- **The Stack**: The EVM uses a stack-based model for executing code
				- **EVM Memory**: Temporary memory used within the machine state to track changes
				- **Gas counter**: Tracks the gas used. Reverts if no more gas is available and undoes the proposed state changes.
			- **Storage**: changes are recorded permanently to reflect the new world state that emerges from the temporary machine state.
	- **ERC-20**
		- The ERC-20 token standard creates fungible tokens.
	- **ERC-721**
		- ERC-721 is designed to create Non-Fungible Tokens(NFT). *ERC-721 tokens are unique.*
		- usually an NFT smart contract builds a collection of items that are a similar type, but with unique differences.
	- **Decentralised Application(dApps)**
		- In an Ethereum context, a dApp refers to the smart contract plus the non-blockchain technologies it combines with to aid the user experience.

### 2025.02.12
- The Concensus Layer(CL) -1 
	- Proof of Staking(PoS) or Staking
		- 2015~2022 PoW
		- The Merge: transitioned to staking from mining in September 2022
	- Validators
		- superphiz.eth is a well-known staker
		- 32ETH deposited to the *deposit contract*( a list of participating validators)
		- The first task , the head of the blockchain, is decided using a **Latest Message Driven Greedy Heaviest-Observe Sub-Tree(LMD GHOST)** vote.
		- The second task, to finalise blocks, is decided using a **Casper the Friendly Finality Gadget(Casper-FFG)** vote.
			- justification
			- finalisation
		- Validators work within a timeframe split up into slots and epochs.
			- **LMD GHOST** vote happens in a slot
			- **Gasper-FFG** vote happens across epochs
		- A slot = 12 seconds
		- An epoch = 32 slots ≈ 6.4 minutes
		- Slots and LMD GHOST
			- In every slot , a block proposer is randomly selected as the leader. Only one validator is assigned as the block proposer for a slot.
			- Block proposers are chosen in advance using a pseudo-random algorithm called **RANDAO**.
			- The block proposer's job:
				- look back at the last slot and find the previous block with the most attestations, the "heaviest" block
				  logseq.order-list-type:: number
				- construct a new Beacon block with contextual information, such as entering and exiting validators, penalties for misbehaving validators, that transitions Ethereum to a new Beacon state.
				  logseq.order-list-type:: number
				- in their execution layer, transition the world state by gathering transactions from the mempool, execution them in the EVM, and producing the execution payload, in the form of an execution block
				  logseq.order-list-type:: number
				- sign the block and then present it to the validators to attest to. Don't present it to the entire validator set.
				  logseq.order-list-type:: number
				- The other validators are involved in attestation.
		-
### 2025.02.13
- The Concencus Layer(CL) -2
	- Epochs and Casper-FFG
		- two Checkpoints
			- the first is the *target*, refers to the checkpoint at the start of the current epoch
			- the second is the *source*, refers to the checkpoint in the epoch prior.
			- 2/3 supermajority votes
	- Aggregation
		- To improve the efficiency of attestations, validators use the **Boneh-Lynn-Shacham (BLS)**  digital signature scheme. it is similar to **ECDSA**.
	- Rewards and Penalties
		- Rewards:
			- Block proposal: priority fees and MEV
			- Attestations: Attesting to the block, to the checkpoints
			- Sync committee: participation in a sync committee
			- Slashing reward: Reporting malicious behaviour
		- Penalties:
			- Missed Proposal: No penalty
			- Missed Attestations: Failure to attest
			- Missed Committee: Failure to participate in sync committee
	- Beacon Block
		- Merkle Patricia Tree
	- Staking Pools
		- combine smaller amounts of ETH to create shared validators.
		- Centralised staking pool, (Binance)
		- Decentralised pool, smart contract protocols (Lido, Rocket Pool)
			- deposit ETH and receive **Liquid Staking Derivative(LSD)** in return
	- Maximum Extractable Value(MEV)
		- refers to the extracting of value by manipulating how transactions are ordered within a block.
		- a complex ecosystem of MEV specialists:
			- Searchers, are users who watch the mempool for transactions
			- block builders, use the mempool to build an execution payload, but they also include the oportimised MEV transactions form searchers.
			- relayers, passes the block builder blocks to proposers, who select the most profitable one of them.
		- Proposer-Builder-Separation(PBS) will be enshrined into the protocol, but for now it is a semi-formal distinction.
	- Blockchain Forks
		- Temporary chain split
		- Soft fork
		- Hard fork
		- Contentious Hard Fork
		- Malicious hard fork
### 2025.02.14
- Accounts over UTXOs
	- UTXO: an unspent transaction output is a distinctive element in a subset of digital currency models. A UTXO represents a certain amount of cryptocurrency that has been authorized by a sender and is available to be spent by a recipient.
	- Benefits of Accounts
		- Space Saving.
		- Great fungibility
		- Simplicity
	- Weakness
		- in order to prevent replay attacks, every transaction must have a nonce.
		- account keeps track of the nonces used and only accept a transaction if its nonce is 1 after the last nonce used.
- Merkle Patricia Trie(MPT)
	- A Merkle-Patricia trie is deterministic and cryptographically verifiable
### 2025.02.15
- DHT(Distributed Hash Table)
	- A DHT is used in protocols like [bittorrent](https://www.bittorrent.org/beps/bep_0005.html) and IPFS which store a wide range of content and users try to *find* the content they are interested in.
	- DHT is used in Ethereum networking to find different peers, not blocks.
	- the discovery protocol in the networking layer of Ethereum uses discv5, a [kademlia based DHT](https://github.com/ethereum/devp2p/blob/master/discv5/discv5.md) to store [ENR records](https://github.com/ethereum/devp2p/blob/master/enr.md).
		- ENR records contain routing information to establish connections between peer.
	- Blocks in Ethereum network are distributed using *gossip protocol* of the p2p stack
### 2025.02.16
- Execution Layer
	- Downloader
	- Transaction Pools
		- **Legacy Pools**: these pools employ price-sorted heaps or priority queues to organize transactions based on their price.
			- transactions are arranged using two heaps:
				- one prioritizes the effective tip for the upcoming block
				- the other focuses on the gas fee cap
			- the larger of these two heaps is selected for the eviction of transactions
		- **Blob Pools**: maintain a priority heap for transaction eviction but incorporate distinct mechanisms for operation.
			- A key feature of blob pools is the use of logarithmic functions in their eviction queues.
	- Storage
		- Blockchain and state data processed by execution client need to be stored in the disk.
		- ancient database: historical data
		- trie structure database: current state and small number of recent states
		- clients keep various databases for different data categories, and can implement different backend handle this data, e.g. leveldb, pebble, mdbx.
### 2025.02.17
- [The Ethereum Virtual Machine (EVM)](https://epf.wiki/#/wiki/EL/evm?id=the-ethereum-virtual-machine-evm)
	- It performs the crucial computations needed to finalise transactions, permanently storing the results on the blockchain.
	- Ethereum can be viewed as a `transaction-based state machine`
	- In Ethereum, the world state is essentially a mapping of 20-byte addresses to account states.
	- TODO [][Ethereum data structures](https://epf.wiki/#/wiki/EL/data-structures) for details on how the world state is implemented.
	- [Virtual machine paradigm](https://epf.wiki/#/wiki/EL/evm?id=virtual-machine-paradigm) go on...

### 2025.02.18
- [Virtual machine paradigm](https://epf.wiki/#/wiki/EL/evm?id=virtual-machine-paradigm)
	- EVM has a word size of 32 bytes.
	- EVM bytecodes: is a representation of a program as a sequence of bytes. Each byte is either:
		- an instruction known as `opcode`
		- input to an opcode known as `operand`
	- EVM bytecode is commonly expressed in [**hexadecimal**](https://en.wikipedia.org/wiki/Hexadecimal) notation
	- `EVM assembly`, human readable
	- The **EVM stack** has a maximum size of 1024 items.
	- EVM memory is a byte array of 2^256 (or [practically infinite](https://www.talkcrypto.org/blog/2019/04/08/all-you-need-to-know-about-2256/)) bytes
### 2025.02.19
- Block Building
	- Importantly, a validator isn't limited to broadcasting a block solely from its own EL
- Nodes broadcast transactions through a peer-to-peer network using the gossip protocol
- Each slot has a designated block proposer, selected through a psuedo-random process by the consensus layer.

  ```go
  func build(env environment, pool txpool.Pool, state state.StateDB) (types.Block, state.StateDB, error) { //1
      var (
          gasUsed = 0
          txs []types.Transactions
      ) //2
  
    for ; gasUsed < 30_000_000 || !pool.Empty(); { //3
        transaction := pool.Pop() //4
        res, gas, err := vm.Run(env, transaction, state) //5
        if err != nil { // 6
            // transaction invalid
            continue
        }
        gasUsed += gas // 7
        transactions = append(transactions, transaction)
    }
    return core.Finalize(env, transactions, state) //8
  }
  ```
### 2025.02.20
- Data Structures in Execution Layer
	- the Ethereum data are stored in trie like structures, mainly `Merkle Patricia Tree` MPT
	- Patricia Tries is a tree data structure where all the data is store in the leaf nodes, and each non-leaf nodes is a character of a unique string identifying the data
	- three types of nodes within the MPT:
		- **Branch Nodes**: consists of a 17-element array, includes one node value and 16 branches.
		- **Extension Nodes**: function as optimized nodes within the MPT
		- **Leaf Nodes**: key-value pair. key is the node's hash, value is the MPT node's content.
	- Ethereum state is stored in four different modified merkle patricia tries (MMPTs):
		- Transaction Trie
		- Receipt Trie
		- World State Trie
		- Account State Trie
	- Verkle Trees
 ### 2025.02.21
  - Transaction
	- A **transaction** is a cryptographically-signed instruction issued by **an external account**, broadcasted to the entire network using [JSON-RPC](https://epf.wiki/#/wiki/EL/JSON-RPC).
	- Fields:
		- **nonce**: An integer value equal to the number of transactions sent by the sender.
			- **Prevent replay attack**
			- **Determine contract account address**
			- **Replace a transaction**
		- **gasPrice**
		- **gasLimit**
		- **to**: 20-byte address of the recipient.
		  | Value of `to` | Transaction Mode | Description |
		  |---|---|---|
		  | *Empty* | Contract creation | The transaction creates a new contract account. |
		  | External Account | Value transfer | The transaction transfers Ether to an external account. |
		  | Contract Account | Contract execution | The transaction invokes the existing smart contract code. |
		- **value**: An integer value equal to the number of Wei to be transferred to this transaction's recipient.
		- **data or init**
		- **signature**
   
### 2025.02.22
- JSON-RPC
  ```json
  {
    "id": 1,
    "jsonrpc": "2.0",
    "method": "<prefix_methodName>",
    "params": [...]
  }
  ```
- Namespaces
  | **Namespace** | **Description** | **Sensitive** |
  |---|---|---|
  | eth | The eth API allows you to interact with Ethereum. | Maybe |
  | web3 | The web3 API provides utility functions for the web3 client. | No |
  | net | The net API provides access to network information of the node. | No |
  | txpool | The txpool API allows you to inspect the transaction pool. | No |
  | debug | The debug API provides several methods to inspect the Ethereum state, including Geth-style traces. | No |
  | trace | The trace API provides several methods to inspect the Ethereum state, including Parity-style traces. | No |
  | admin | The admin API allows you to configure your node. | Yes |
  | rpc | The rpc API provides information about the RPC server and its modules | No |
	- Eth is probably. the most used namespace providing basic access to Ethereum network. 
	  The full list can be found in the [Ethereum JSON-RPC specification](https://ethereum.github.io/execution-apis/api-documentation/).  

### 2025.02.23
- [Recursive-Length Prefix (RLP) Serialization](https://epf.wiki/#/wiki/EL/RLP?id=recursive-length-prefix-rlp-serialization)
	- [Data Serialization in Ethereum](https://epf.wiki/#/wiki/EL/RLP?id=data-serialization-in-ethereum)
	- Ethereum actually utilizes 2 formats: RLP and Simple Serialize (SSZ) which is more modern standard used by consensus layer.
	- RLP
### 2025.02.24
- [Consensus Layer Overview](https://epf.wiki/#/wiki/CL/overview?id=consensus-layer-overview)
	- ensure that tens of thousands of independent nodes around the world stay reasonably synchronized.
	- a reliable distributed system:
		- Each node keeps a ledger with the state of every account, and all these ledgers must match exactly.
		- There can be no differences;
		- the nodes must agree and do so quickly
	- Ethereum's consensus protocol:
		- **LMD GHOST**
		- **Casper FFG**
		- the combination known as **Gasper**
### 2025.02.25
- #efp.wiki
	- [Consensus Layer Overview](https://epf.wiki/#/wiki/CL/overview?id=consensus-layer-overview)
		- In Ethereum's PoS, the proposer(leader) is pseudo-randomly selected from active validator set.
		- In Ethereum's execution chain, block size is limited by the block gas limit.
		- [Beacon block](https://epf.wiki/#/wiki/CL/beacon-api?id=beaconblockbody) sizes are limited by hard-coded constants.
		- [Beacon Chain Introduction](https://epf.wiki/#/wiki/CL/overview?id=beacon-chain-introduction)
			- **Staking ETH**
			- **Proposing Blocks**
			- **Attesting Blocks**
			- **Participating in Consensus**
### 2025.02.26
- Components of the Consensus Layer
	- Beacon Node
	- Validator
### 2025.02.27
- **When the consensus client is not the block producer:**
	- Receives a block via the block gossip protocol.
	- Pre-validates the block.
	- Sends transactions in the block to the execution layer as an execution payload.
	- Execution layer executes transactions and validates the block state.
	- Execution layer sends validation data back to the consensus layer.
	- Consensus layer adds the block to its blockchain and attests to it, broadcasting the attestation over the network.
- **When the consensus client is the block producer:**
	- Receives notice of being the next block producer.
	- Calls the create block method in the execution client.
	- Execution layer accesses the transaction mempool.
	- Execution client bundles transactions into a block, executes them, and generates a block hash.
	- Consensus client adds transactions and block hash to the beacon block.
	- Consensus client broadcasts the block over the block gossip protocol.
	- Other clients validate the block and attest to it.
	- Once attested by sufficient validators, the block is added to the head of the chain, justified, and finalized.
 ### 2025.02.28
 前面学过的知识点还是散的，没有完整的串起来，今天开始先跟着[Building A simplified blockchain implementation in Golang](https://github.com/Jeiwan/blockchain_go) 走一遍，顺便回忆下前面学习过的概念，理论结合实际。纯理论的东西太枯燥了。
### 2025.03.01
今天继续跟着跟着[Building A simplified blockchain implementation in Golang](https://github.com/Jeiwan/blockchain_go) 构建区块链。
<!-- Content_END -->
