---
timezone: Asia/Dubai
---

# lllapland

1. 自我介绍
   大家好我是 lllapland，爱好和饭碗都是写代码，智能合约萌新。

2. 你认为你会完成本次残酷学习吗？
   根据以往经验不会完成，但是我会尽力完成。我自控力比较差，一般被push的时候效果最好（逃）。

## Notes


<!-- Content_START -->

### 2025.02.06

https://epf.wiki/#/eps/week1

#### Prehistory and Philosophy

- Free Software movement
  - **UNIX** (1960s): Modular design, key to Ethereum's architecture; Bell Labs' open collaboration mirrors Ethereum's core development.  
  - **Free Software Movement**: Led by Richard Stallman, emphasizing software freedom and open source principles
  - **FOSS (Free & Open Source Software)**: Software that respects users' freedom and community
  - **GNU**: Foundation for open-source software, influencing Ethereum's development principles. GNU stands for "GNU's Not Unix"
- Cryptography
  | **Characteristic** | **Symmetric Encryption** | **Asymmetric Encryption** |
  |-------------------|-------------------------|--------------------------|
  | **Key Usage** | same key for encryption & decryption | public/private key pair |
  | **Security** | less secure if key is exposed | more secure; only private key must be kept secret |
  | **Speed** | faster (simpler computation) | slower (complex mathematical operations) |
  | **Key Distribution** | requires secure key exchange | public key can be shared openly |
  | **Common Algorithms** | AES, DES, RC4 | RSA, ECC, Diffie-Hellman |
  | **Use Cases** | encrypting files, database security | digital signatures, 🌟 **blockchain**, secure communication (TLS, PGP) |


#### Implementations and Development
- **Clients**: Implementations of the Execution Layer (EL) or Consensus Layer (CL).
  - EL clients: Geth, Nethermind, Besu
  - CL clients: Prysm, Lighthouse, Teku
- **Nodes**: Computers running both an EL and CL client, actively participating in the Ethereum network.


---
### 2025.02.07

https://epf.wiki/#/eps/week2

#### Execution Layer

##### Block Validation
```typescript
stf(parentBlock: Block, curBlock: Block, state: State): [State, Error]
```
- `stf` -> state transition function
- verify header
  - merkle roots
  - gas limit
  - timestamp
  - etc.
- verify and process a block
##### Block Building

```typescript
build(env: Environment, pool: TransactionPool, state: State): [Block, State, Error]
```
- construct a new block from environment, transaction pool, and current state


### 2025.02.09
https://epf.wiki/#/eps/week2



#### Execution Layer

##### Uncle Blocks
- valid blocks that were mined but not included in the canonical chain ( usually due to network delays or simultaneous block production by multiple miners)
  - Why exist?
    - for miners to include uncle blocks in new blocks and receive **additional rewards**
    - to improve security and reduce centralization by compensating **valid but orphaned blocks**


##### Modern Ethereum Execution Clients

| **Client**     | **Language** | **Why Chosen?**                                      |
|---------------|-------------|------------------------------------------------------|
| **Geth**      | Go          | easy concurrency, large developer community, mature ecosystem |
| **Erigon**    | Go          | optimized storage, improved sync speed 💡         |
| **Nethermind** | C#         | suitable for .NET ecosystem, enterprise-friendly   |
| **Besu**      | Java        | hyperledger compatibility, enterprise-level support |
| **Reth**      | Rust        | high performance, memory safety                     |


##### Consensus Layer vs. Execution Layer

| **Comparison**      | **Execution Layer (EL)**            | **Consensus Layer (CL)**       |
|---------------------|----------------------------------|----------------------------------|
| **Main Function**   | processes transactions, executes smart contracts | validates blocks, runs **PoS** consensus |
| **Core Components** | EVM, Transaction Pool, State Database | Beacon Chain, Validators, Slot/Epoch Mechanism |
| **Runs PoS?**       | ❌ No | ✅ Yes |
| **Consensus Role**  | executes transactions but does not determine consensus | runs **PoS** rules, decides block validity |
| **Client Examples** | Geth, Erigon, Nethermind | Prysm, Lighthouse, Teku, Nimbus |
| **Stored Data**     | account balances, smart contracts, transaction history | validator registry, voting data, finality information |

##### Why Did Ethereum Split CL and EL?

Before **The Merge**, Ethereum used a **PoW (Proof of Work) + Execution Layer** model, where a single client handled both **consensus (mining) and transaction execution**, leading to several issues:

- High computational cost (electricity).  
- Slow blockchain synchronization (the continuously growing state increased sync time).  
- Inefficient consensus mechanism (PoW was difficult to optimize).  

After **The Merge**, Ethereum split into **Execution Layer (EL) + Consensus Layer (CL)**, offering key advantages:  
- Execution Clients focus on **transaction execution and performance optimization**
- Consensus Clients handle **PoS rules**, improving **security and decentralization**
- EL and CL can be upgraded **independently**, enhancing **flexibility** 🌟

##### How Do CL and EL Communicate?

via the **Engine API**, 

1. **CL** requests **EL** to provide a new block
2. **EL** executes the block and returns the execution result
3. **CL** decides whether to accept the new block through validator voting.  

##### EVM
![EVM](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*a4cYYJZLlObtCGMIDiQeKQ.png)

- arithmetic (add, mod, etc.)
- bitwise 
- environment (block context, etc.)
- system (call, create, storage, return, etc.)
- control flow (branch, jump, etc.)
- stack (push, pop, etc.)
- memory (load, store, etc.)

##### p2p
- Execution layer operates** on devp2p (ethereum's p2p protocol).
  - **devp2p** allows nodes to support different **sub-protocols**:
    - **eth/68, eth/69** – for transaction and state synchronization.
    - **snap** – for fast state synchronization.
      - optimizations:
          1. **quickly syncing new nodes** by fetching **flat state data** instead of reconstructing the Merkle Patricia Trie.  
          2. uses **batch requests** (`GetAccountRange`, `GetStorageRanges`) to efficiently retrieve account and contract storage data.  
          3. **reduces disk I/O** by eliminating deep MPT traversals, improving sync speed. 
      - outcome:
        - enables nodes to complete state synchronization in **3-6 hours instead of days**.      
    - **les** – for light clients.
  - features  
    - efficiently communicate and synchronize data.
    - support different types of clients (full nodes, light clients, etc.) 💡
- **Responsibility**
  1. historical data
    - `GetBlockHeader`
    - `GetBlockBodies`
    - `GetReceipts`
    - etc.
  2. pending transactions
    - `Transactions`
    - `NewPooledTransactionHashes`
      - notifies peers of new pending transactions by sharing only their transaction hashes, reducing bandwidth usage
    - `GetPooledTransactions`
    - etc.
  3. state

    


### 2025.02.10
https://epf.wiki/#/eps/week3
  
- how to make digital scarcity?
  - solution: don't have a single trusted operator
- how to remove single trusted operator?
  - solution: consensus via "state machine replication"
- BFT: byzantine fault tolerance
  - 2PC: two-phase commit protocol
      1. **prepare phase** (each participant submit a binary vote for **commit** or **abort**)
      2. **commit phase** (if all participants vote commit, then execute the command)

  - PBFT: practical byzantine fault tolerance
    - utilizes **message signatures** and **multiple rounds of voting** to reach consensus.


| **Feature**            | **PBFT (Practical Byzantine Fault Tolerance)** | **2PC (Two-Phase Commit)** |
|------------------------|-----------------------------------------------|----------------------------|
| **Objective**         | tolerates malicious nodes | ensures **all** databases either commit or rollback a transaction consistently |
| **Fault Tolerance Model** | **Byzantine Fault Tolerance (BFT)**, capable of handling malicious nodes | **Crash Fault Tolerance (CFT)**, only handles node crashes but cannot tolerate malicious behavior |
| **Applicable Scenarios** 🌟 | **blockchain** (Hyperledger, Tendermint, HotStuff, etc.) | **distributed databases & transaction management** (MySQL, PostgreSQL, distributed storage) |
| **Voting Mechanism**   | **voting + signature authentication**, consensus is reached if more than **2/3 agree** | **unanimous agreement required**, if **any** participant votes `"abort"`, the transaction is rolled back |
| **Communication Complexity** | **O(n²)** -> multiple rounds of message exchanges, where each node broadcasts messages to all other nodes 🌟| **O(n)** |



### 2025.02.11
https://epf.wiki/#/eps/week3

- PoS
  - in-protocol signal allow for **penalties**, not just rewards (compared to PoW)
    - scenarios:
      - double signing
      - going offline
      - equivocation -> voting for multiple **competing blocks** at the same height [💡](https://youtu.be/5gfNUVmX3Es?si=z7ba-EZ48kbH4I5V)
    - how?
      - **slashing**: cutting validator's stake for malicious behavior (up to 32 ETH)
      - **inactivity leak**: gradual stake reduction for being offline to maintain network liveness
    - benefits:
      - reduce attack surface
      - less resource intensive
-  Bribe attacks -> attackers influence validator behavior through **economic incentives**
     - examples:
       - paying validators to vote for specific blocks
       - bribing validators to stay offline
     - mitigations:
       - slashing penalties make bribe acceptance **more costly than potential gains**
       - withdrawal delays increase the cost of malicious behavior 
- GHOST vs. Casper
  - ethereum 2.0's consensus mechanism uses a modified version of **GHOST** combined with **Casper FFG** (Finality Gadget)

| Mechanism | Purpose | Consensus Type | Key Features |
|-----------|---------|---------------|--------------|
| **GHOST** | **fork-choice rule** to determine the canonical chain | **PoW & PoS** | • usually considers the **entire tree of blocks** (special case: LMD-GHOST looks at validators' **latest messages**)<br>• chooses the **heaviest** subtree<br>• prevents short-chain attacks |
| **Casper FFG** | **finality gadget** for PoS consensus | **PoS** | • checkpoint-based finalization<br>• uses validator voting<br>• provides economic finality through slashing |



### 2025.02.12
https://epf.wiki/#/eps/week3

- Attestation: statement or proof of a certain fact
  - Ethereum's PoS consensus [tutorial](https://youtu.be/5gfNUVmX3Es?si=_fkMJ6mn3LQGAE4V&t=83)
    - epoch -> **a time unit** used to **organize validator duties** and **finalize** blocks efficiently
      - **1 epoch = 32 slots** (Each slot is **12 seconds**)
      - **1 slot** = opportunity to **propose a block**
    - How to?
      1. **a validator is selected** to propose a block in **each slot**
      2. **other validators attest** using **BLS signatures** (aggregating hundreds of signatures into a single signature)
         - validators are assigned to different **committees**
         - each committee is responsible for validating **specific shards**
      3. **attestations are aggregated** and included in the next block
      4. **epoch ends after 32 slots** (~6.4 min)
      5. **If 2/3 validators agree, finalization occurs**
  - EAS: Ethereum Attestation Service 🔥 [tutorial](https://youtu.be/DMGj5GNll0k?si=LFfMfwQp7LqfNyCV&t=967)
    - [usage cases / ideas](https://docs.attest.org/docs/category/example-use-cases)
      - identity
      - statements
      - etc.


### 2025.02.13
https://epf.wiki/#/eps/week4

#### Execution Layer Testing
- EVM Testing
  - key characteristics
    - pre-state
      - accounts with balances etc.
    - environment
      - timestamp etc.
    - transaction(s)
      - origin
      - destination
      - ether value
      - gas limit
      - etc.
    - post-state
      - accounts with balances etc.
  - State Testing <> Fuzzy Differential State Testing

| Feature                          | State Testing                                      | Fuzzy Differential State Testing                   |
|----------------------------------|---------------------------------------------------|--------------------------------------------------|
| **Testing Goal**                 | verify **a single client**’s state transitions       | compare **multiple clients** to detect state inconsistencies |
| **Input Generation**             | predefined, deterministic transactions or state changes | fuzzing (**randomly generated** or **mutated** transactions) |
| **Execution**                    | single client                          |  multiple clients (e.g., **Geth, Nethermind, Besu**) |
| **Types of Issues Detected**     | - EVM computation errors <br>- state update errors <br>- smart contract execution issues | - client implementation differences <br>- **potential consensus forks** |
| **Use Cases**                    | - ensuring a client follows Ethereum protocol <br>- regression testing in CI/CD <br>- validating EIP implementations | - identifying network-wide inconsistencies <br>- preventing **hard forks due to state mismatches** |
| **Complexity**                   | controlled, predictable inputs                   | higher complexity due to unexpected fuzzing cases |
  -  Blockchain Negative Testing
     1. transaction-level negative testing
          - **case**: construct a transaction with an excessively **large nonce** and check if the client correctly rejects it

      2. smart contract negative testing
           - **case**: attempt to trigger an integer overflow

      3. network-level negative testing
           - **case**: simulate a **DDoS attack** by sending a large number of junk transactions or requests to nodes
      4. consensus mechanism negative testing
           - **case**: construct two transactions with the same `nonce` but different `to` addresses and check if the PoS/PoW mechanism correctly handles the conflict  
           - **test objective**: ensure that the client does not cause **a consensus divergence** due to **mismatched transaction states**  
      5. data storage negative testing
           - **case**: provide a tampered block header (with an incorrect merkle root)
           - **test objective**: ensure that the node correctly rejects a manipulated block

  - ethereum tests
  - ethereum/execution-spec-tests (EEST) [doc](https://ethereum.github.io/execution-spec-tests/verkle@v0.0.6/)
#### Consensus Layer Testing
  - ethereum/consensus-specs
  
### 2025.02.16
https://epf.wiki/#/eps/week4

#### Cross-Layer (interop) Testing 
(Execution + Consensus) (E2E testing)
  - **Hive 💡**  
    - ✅ **Suitable for**  
      - ethereum PoS EL-CL interaction testing
      - fork upgrade compatibility  
      - cross-client interoperability –> verifies **different EL-CL client pairings** work together  
      - stability under network issues –> simulates delays, packet loss, and failures.  

    - ❌ **Not suitable for**  
      - fuzz testing –> runs structured tests, not random input-based bug detection. 
      - standalone EVM execution –> focuses on EL-CL, not individual transaction processing   
      - isolated EL or CL testing –> designed for their integration, not single-layer testing  
  - Devnets <> Shadow-Forks <> Testnets

| **Category**       | **Purpose**                  | **Characteristics**          | **Use Cases**                                |
|--------------------|-----------------------------|------------------------------|---------------------------------------------|
| **Devnets** | **local** or **private** testing environment | customizable, fully controlled | internal team **development**, rapid iteration |
| **Shadow Forks**   | simulate the mainnet environment | real blockchain data, non-disruptive | **mainnet upgrade simulation**, MEV analysis |
| **Testnets**       | public testing environment  | open access, free test tokens | DApp **deployment**, wallet & DeFi compatibility |



#### Security
- Execution layer security

| category | risk | impact | mitigation | attack example |
|----------|------|--------|------------|---------------|
| Valid invalidation | mistakenly rejecting valid transactions | consensus forks, transaction failures | consensus testing, transaction replay tests, proper evm rule adaptation | clients misinterpreting evm updates, causing certain transactions to be rejected |
| Invalid validation | mistakenly accepting invalid transactions | network pollution, fund loss | **formal verification**, state rollback, strict evm rule enforcement | ❗️ **integer overflow** in smart contracts allowing unauthorized withdrawals |
| DoS during execution | **excessive resource consumption** during transaction execution | transaction delays, node crashes, network congestion | 💡 gas fee optimization, contract execution limits, monitoring and detection | ❗️ **recursive contract calls** (e.g., gas griefing) to consume block resources |

- Consensus layer security
  - faulty clients and finalization
    - if **< 1/3 of nodes** fail, the network can reach **finality**.  
    - if **> 1/2 of nodes** fail, the network may **lose consensus** and enter an **uncertain state**.  
    - if **> 2/3 of nodes** are attacked or controlled, ethereum could **finalize the wrong chain**, causing major risks.  

| Faulty node percentage | Impact |
|------------------------|--------|
| **< 33%** | may cause **missed slots**, but **finalization is not affected** |
| **33%+** | **delayed finality**, block confirmation takes longer, but the chain continues |
| **50%+** | may disrupt forkchoice, leading to network uncertainty and a **non-finalized state**, where users cannot be sure if their transactions are permanently recorded. |
| **66%+** | may **finalize an incorrect chain** 💀, causing severe consequences |



### 2025.02.17
https://epf.wiki/#/eps/week5

#### Ethereum Roadmap Phases  
- **The Merge** - PoS
  - transition from **Proof of Work (PoW)** to **Proof of Stake (PoS)**  
- **The Surge** 
  - scalability improvements with **rollups** and **sharding**.  
- **The Scourge** - less MEV downsides 
  - addressing censorship resistance and decentralization issues 
- **The Verge** - easier verification
  - introduction of **Verkle Trees** to optimize data storage 
- **The Purge** - simpler protocol  
  - pruning old state data to reduce node storage requirements 
- **The Splurge** 
  - miscellaneous upgrades and optimizations.  
  
<!-- Content_END -->

