---
timezone: Asia/Shanghai
---

# {Devbards}

1. 自我介绍
  - Full Stack Engineer, starting to learn crypto and security-related topics to become a better developer.
2. 你认为你会完成本次残酷学习吗？
  - Sure!
3. TG 联系方式：@Devbards

## Notes

<!-- Content_START -->

### 2025.02.06

I had finished week 0 and week 1 study materials.
Like what Mario said, the first five weeks are about the introduction of Enthereum.
That is, I would be able to write some code after that.

-- one take away daily --
The Merkle Tree calculates the hash value by combining each node with its neighboring node to generate the parent node value.
This means that checking the final node value can be used to verify the entire tree.
Any change to a node will result in a different hash value, making it impossible to pass verification.
It is a fundamental mechanism in cryptocurrencies.

### 2025.02.07

Week 2 is about how Ethereum’s execution layer works. The Execution Layer (EL) processes transactions and keeps the network running smoothly. Every transaction goes through a validation process, gets executed, and then updates Ethereum’s state. There’s a lot happening under the hood, such as adjusting gas fees (EIP-1559) and handling staking withdrawals.

Ethereum nodes don’t just verify transactions—they also build new blocks by collecting transactions from the network. This requires a transaction pool to keep track of pending transactions before they’re added to a block. I wonder whether that causes latency or not.

The State Transition Function is responsible for processing blocks and updating Ethereum’s state. The Ethereum Virtual Machine (EVM) runs smart contract code using a stack-based system, meaning operations are processed one after another.

The P2) network plays a crucial role in how Ethereum nodes share data, whether it’s historical records, pending transactions, or state syncing (like with snap sync). To make everything accessible, Ethereum provides a JSON-RPC interface, allowing developers to interact with the blockchain using standard API calls. However, would this become a critical issue if the network were hacked?

### 2025.02.08
Week 3 covered consensus mechanisms, but to be honest, I didn’t fully grasp everything. So I’m reading it together with Week 4 to get a better understanding. However, there are still some parts that require further clarification. I plan to review everything again after going through Week 5.

### 2025.02.09
Week 5's content is much more complex than I expected. It seems like I need to fully understand and integrate the concepts from the first four weeks before I can make sense of it… So, I’ve decided to spend more time reviewing the previous weeks.

### 2025.02.10
I realized that my fundamental knowledge of cryptocurrencies is too limited, and jumping straight into BFT feels like taking on a boss fight way beyond my level—everything just seems vague and confusing. So, I’ve decided to borrow some introductory books on cryptocurrencies to build a stronger foundation. Additionally, I noticed that writing notes in English might not be as helpful for the Chinese-speaking community. Therefore, once I have a more complete understanding, the recording style would change somehow.

### 2025.02.11
From the reading on the history of cryptocurrencies, blockchain techniques, and consensus mechanisms:

Bitcoin uses a reward mechanism to incentivize miners to become nodes in its P2P network. However, this raises the question—once the total supply of Bitcoin reaches its limit and no more Bitcoin can be "mined," how will the network continue to operate? The alternative mechanism I found is that transaction fees will sustain network operations, which in turn creates the necessity for higher fees. This has led to the development of off-chain solutions like the Lightning Network.

Ethereum, on the other hand, is gradually replacing PoW with a PoS mechanism, where participants stake ETH to take part in consensus and earn rewards. To enhance security, the slashing mechanism punishes malicious actors. Unlike Bitcoin, Ethereum does not have a fixed supply limit, but by implementing Base Fee burning, it introduces a deflationary aspect to ETH.

Understanding these concepts gives me a deeper appreciation of the motivations behind founding this study group—it’s truly fascinating!

### 2025.02.12
Today was abit late for updating. Will update it late~

### 2025.02.13
Pass

### 2025.02.14
After the weekly meeting, it might be a time to adjust the way recording. Would start in next week.

### 2025.02.15
Still preparing for next week, the record would be update after then.

### 2025.02.16

-- EPF week 1 --
### 2025.02.17

Materials in Day 1
[Mastering Ethereum](https://cypherpunks-core.github.io/ethereumbook/)
[Ethereum Virtual Machine (Ethereum 101)](https://veridelisi.substack.com/p/understanding-ethereum-virtual-machine-evm])
[Discord Live Talk](https://discord.com/channels/1205546645496795137/1205546645937463356)

### 2025.02.18
The topic today is about Validator machanism.
It still in progress now.

### 2025.02.19

Pass

### 2025.02.20
 Exercution Layer today.

### 2025.02.21
 Network Layer has been updated since the previous study materail published.

### 2025.02.22

### 2025.02.23

-- EPF week 2 --
### 2025.02.24

<!-- Content_END -->
