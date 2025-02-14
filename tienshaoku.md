---
timezone: Asia/Taipei
---

# Shao-Ku Tien

1. 自我介绍：大家好，我是 Shao。第一次參加以太坊協議殘酷共學，名字很酷，希望可以更瞭解以太坊的底層東西。
2. 你認為你會完成這次的殘酷學習嗎？YES!

## Notes

<!-- Content_START -->

### 2025.02.06

#### Asymmetric encryption

- In 1976, Merkle's Puzzles inspired Whitfield Diffie and Martin Hellman to publish their historic paper _"New directions in cryptography"_ that introduced Diffie–Hellman key exchange algorithm
- Pretty Good Privacy (PGP) protocol is one of the earliest example of asymmetric encryption without a third party

#### BitTorrent

- breaks a file into multiple pieces, letting each node take a piece and request the rest from each other, instead of always having to ask the server
- this also benefits from the upload download asymmetry of residential internet connection, fully utilising the limited uploading speed of residential internet connection, compared to not using it at all (always download from servers)

#### Bitcoin

- by specifying how many leading bits == 0 to adjust the difficulty of PoW, and it's dead easy to verify: look at the leading bits
- hashing function really is the core of blockchains

### 2025.02.07

#### History

> _"National borders are just speed bumps on the information superhighway."_
> — Timothy May

- In the 1950s through 60s, early software was often primitive and required modification and software source code was no secret; in fact sharing source code was the norm
- In 1990, David Chaum introduced DigiCash providing the first glimpse of an anonymous digital economy. However, it relied on existing financial infrastructure and was largely centralized. Ultimately, DigiCash filed for bankruptcy in 1998
- In 1998, Wei Dai proposed B-money powered by a cryptographic function to create money. In 2005, Nick Szabo designed BitGold but was never implemented
- A solution to the open problem of **how to achieving consensus without a leader** was introduced by Bitcoin in 2008

#### Architecture Overview

- The protocol consists of 2 main parts - execution and consensus layer. The execution layer (EL) handles the actual transactions and user interactions, it's where the global computer executes its programs. The consensus layer (CL) provides the proof-of-stake consensus mechanism - a cryptoeconomic security making sure all nodes follow the same tip and drives the canonical chain of execution layer
- In practice, these layers are implemented in its own clients connected via API. Each have their own p2p network handling different kind of data

```
user ---(User API)>>> execution engine ---(Engine API)>>> beacon node ---(Beacon API)>>> other nodes
```

#### Protocol Design Philosophy

- Simplicity
- Universality
- Modularity: Modularity derives itself from the idea of encapsulated complexity, which occurs when a system consists of sub-systems -- which are internally complex and are available to the outside by means of high level interfaces
- Non-discriminant
- Agility

#### Principles

- Managing complexity
  - One of the challenges of this goal, however, is that complexity is difficult to define, and sometimes, you have to trade off between two choices that introduce different kinds of complexity and have different cost
  - Sandwich model complexity v.s. Encapsulated complexity

#### Blockchain-level protocol

- explorations of serialisation: Recursive Length Prefix (RLP) & Simple Serialise (SSZ)
- account based, instead of UTXO

###### Pros and Cons of Account

- Space saving: every transaction need only make one reference and one signature and produces one output
- Fungibility: UTXOs are not perfectly fungible, as a UTXO can be tainted by being used in a transaction with a tainted UTXO, and there are some heuristics that can be used to track the history of a coin. Accounts are perfectly fungible, as any coin can be replaced by any other coin
- Simplicity: UTXOs require a more complex transaction validation algorithm, and the UTXO model is less flexible and less powerful than the account model. For example, it is impossible to implement a decentralized exchange in the UTXO model because the UTXO model does not allow for the existence of a "sell" order that is not tied to a specific UTXO. UTXO lacks the flexibility needed for general order matching without tying the trades to specific UTXOs upfront
- Con: to prevent replay attacks, every transaction must have a nonce. This means that even no-longer-used accounts can never be pruned from the account state, but there're simple solutions to this

##### Merkle Patricia Trie (MPT) and Verkle Tree

- Ethereum's data structure is a 'modified Merkle-Patricia Trie', designed for efficient data retrieval of items that comprise the Ethereum state
- A Merkle-Patricia trie is deterministic and cryptographically verifiable. Theoretically, this structure provides the 'holy grail' of O(log n) efficiency for inserts, lookups and deletes
- A Merkle Tree with `n` leaves has O(log2 n)-sized proofs. However, in large trees, sending proofs can dominate bandwidth consumption. Verkle tree with branching factor (amount of branches) `k` achieve O(kn) construction time and O(logk n) membership proof size. This means that the branching factor `k` offers a trade-off between computational power and bandwidth. For example, larger `k`, i.e. more branches, reduces bandwidth but increase the computation needed to handle the tree
- One of the pressing problems of Ethereum is the current state size, estimated at around 1-2TB

###### Hunt for Finality

- Finality refers to the guarantee that a block cannot be altered or removed from the blockchain **without burning at least 33% of the total staked ETH**. The underlying consensus protocol to achieve this is called Casper Friendly Finality Gadget (FFG)
- Casper FFG: follows a Byzantine Fault Tolerance (BFT) tradition with modifications to achieve PoS. Simply put, each validator votes on the checkpoint, and after two rounds of voting, the checkpoint is finalized. All finalized checkpoints become part of the blockchain history. While Casper **guarantees finality** through attestations to the latest block addition to the canonical chain, it requires a **fork-choice rule** where validators attest to blocks to signal support for those blocks
- Latest Message Driven Greediest Heaviest Observed Sub-Tree (LMD-GHOST) is the fork-choice rule similar in some ways to the fork choice rule used in Proof-of-work network, where the fork with the most work done is selected as the canonical chain

### 2025.02.08

#### Protocol History

##### The Merge

- On Sep 15th, 2022, EIP-3675: Upgrade consensus to Proof-of-Stake, was live
- New proof-of-stake consensus has been implemented in its own layer with a separate p2p network and logic, also know as Beacon Chain. The Beacon Chain has been running and achieving consensus since December 1st, 2020. After a prolonged period of consistent performance without any failures, it was deemed ready to become Ethereum's consensus provider. The Merge gets its name from the union of the two networks

### 2025.02.09

### 2025.02.10

### 2025.02.11

### 2025.02.12

#### Execution Layer Spec

- The Execution Layer focuses exclusively on executing the state transition function (STF). This role addresses two primary questions:
  - Is it possible to append the block to the end of the blockchain?
  - How does the state change as a result?
- Rather than being stored in a specific location, the system's state is dynamically derived through the application of the state collapse function
  - The state is not explicitly preserved as a simple flat snapshot at every block. Instead, state information is dynamically reconstructed using MPT structures
  - The execution layer uses a trie (tree-like structure) to store state data efficiently and verify its integrity. Rather than accessing a static state object, the system looks up components dynamically
  - Storing every single state for every block would be computationally infeasible. The MPT structure allows nodes to efficiently derive and prove state without keeping redundant snapshots
- The state transition function includes the following steps:
  1. Retrieve the Header: Obtain the header of the most recent block added to the chain, referred to as the parent block
  2. Excess Blob Gas Validation
  3. Header Validation: Compare and validate the current block's header against that of the parent block. Performing header checks early allows the State Transition Function (STF) to potentially return an "Invalid Payload" message to the Consensus Layer (CL) without proceeding to the computationally intensive stage of block/transaction execution
  - Minimum Gas Limit: A minimum gas limit of 5,000 ensures a basic level of transaction processing capacity
  - Economic Model Compliance: e.g. EIP-1559
  4. Ommers Field Check: Verify that the ommers field in the current block is empty. Note: "ommers" is the gender-neutral term that replaces the previously used term "uncles."
  5. Block Execution: Execute the transactions within the block, which yields the following outputs:
  - Gas Used
  - Trie Roots: The roots of the tries for all transactions and receipts contained in the block
  - Logs Bloom: A bloom filter (a data structure for efficient filtering) of logs from all transactions within the block
  - State: The state after executing all transactions
  6. Header Parameters Verification
  7. Block Addition
  8. Pruning Old Blocks: Remove blocks that are older than the most recent 255 blocks from the blockchain
  9. Error Handling: If any validation checks fail, raise an "Invalid Block" error. Otherwise, return None

<!-- Content_END -->
