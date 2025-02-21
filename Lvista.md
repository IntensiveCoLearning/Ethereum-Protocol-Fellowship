---
timezone: Asia/Shanghai
---

# Lvista

1. 自我介绍: 
    - 个人主页：[lvista.site](lvista.site)
    - 个人简介：学生，C，C++，C#，嵌入式，python
2. 你认为你会完成本次残酷学习吗？ 会的。

## Notes

<!-- Content_START -->

TODO: Read https://inevitableeth.com/home/ethereum/world-computer  
TODO: Figuring out the meaning of this [roadmap](https://x.com/VitalikButerin/status/1741190491578810445) or [here](https://ethereum.org/zh/roadmap/)

Links:

| Description  |  Links  |
|---|---|
| Great speech vido | https://archive.devcon.org/archive/ |

### 2025.02.06

今日任务：
- [x] 了解区块链->https://en.wikipedia.org/wiki/Blockchain
- [x] 了解以太坊（Ethereum）的基本要概念->https://epf.wiki/#/eps/week1

#### Block Chain
> See also: [what-is-a-blockchain](https://ethereum.org/zh/developers/docs/intro-to-ethereum/#what-is-a-blockchain)  

以太坊是基于区块链的一种[公有链](https://en.wikipedia.org/wiki/Blockchain#Private_blockchains).

从数据结构上来看，区块链通过首尾相接的“区块”来连接成“链”的，这种链的特点是，
由于每个节点包含前一个结点的信息（Hash Code），每个数据节点的变化会影响后面所有节点，
这样的特点使得数据的变化很容易被发现，从而保证了数据的强壮性。
> See this vido about Blockchain:https://youtu.be/_160oMzblY8

从数据管理方式上来看，区块链是一种分布式帐本，通俗讲就相当于将一个公共帐本拆开，将每一页分给每个帐户，每条交易记录都分布在每个人手上，
这就避免了[双重支出问题](# "甲方帐户扣除一次而在两个乙方帐户上增加")。
没错，就像peer-to-peer (P2P)一样，而Block chain正是由P2P进行管理的。

比如电子人民币就是典型的联盟链的应用。

下面这张表格很好的展示了以太坊的定位:
|          | 公有链                  | 联盟链              | 私有链           |   |   |   |   |   |   |
|----------|----------------------|------------------|---------------|---|---|---|---|---|---|
| **参与者**  | 不限                   | 联盟成员             | 链的所有者         |   |   |   |   |   |   |
| **共识机制** | PoW/PoS              | 分布式一致性算法         | solo/pbft等    |   |   |   |   |   |   |
| **验证者**  | 自愿提供算力或质押加密货币者       | 联盟成员协商确定         | 链的所有者         |   |   |   |   |   |   |
| **激励机制** | 需要                   | 可选               | 无             |   |   |   |   |   |   |
| **去中心化** |                      |                  |               |   |   |   |   |   |   |
| **程度**   | 较高                   | 偏低               | 极低            |   |   |   |   |   |   |
| **如初特点** | 解决双重支付               | 效率和成本优化          | 安全性高、效率高      |   |   |   |   |   |   |
| **吞吐量** | 7笔/秒至数千笔/秒(TPS)      | <10万笔/秒(TPS)     | 视配置决定         |   |   |   |   |   |   |
| **应用领域** | 区块链游戏、非同质化代币、去中心化金融等 | 供应链管理、金融服务、医疗保健等 | 大型组织或私人企业之业务等 |   |   |   |   |   |   |
| **代表项目** | 比特币、以太坊              | R3、 Hyperledger  |               |   |   |   |   |   |   |


#### The Prehistory and Philosophy of Ethereum 
> See also:
> - TODO[Inevitable Ethereum - World Computer](https://inevitableeth.com/home/ethereum/world-computer)
> - TODO[Ethereum in 30 minutes](https://www.youtube.com/watch?v=UihMqcj-cqc)
> - [Ethereum.org docs](https://ethereum.org/zh/what-is-ethereum/)
> - [Ethereum Develop Document](https://ethereum.org/zh/developers/docs/)

以太坊的理念源于类似Unix的免费和开源理念。开放的平台需要安全性，中立性和无信任性,
这成为了以太坊的核心课题。

以太坊的主要高级组成部分是执行层( Execution layer)和共识层(Consensus layer):
- 执行层: Execution layer provides the execution engine, handles user transaction and all state (address, contract data)
> 简而言之就是提供算力
- 共识层: implements the proof-of-stake mechanism ensuring security and [fault tolerance](https://inevitableeth.com/home/concepts/bft)
> 也就是保证数据的健壮，安全，可信

作为区块链的一种，以太坊的[共识机制](https://ethereum.org/zh/developers/docs/consensus-mechanisms/)是[权益证明](https://ethereum.org/zh/developers/docs/consensus-mechanisms/pos/)
> TODO: Lean about the consensus mechanisms

#### 小结
区块链是一种去中心化的公共数据库，相对的中心化数据库就是各种互联网企业。

以太坊是一种公共区块链技术，主要由执行层和共识层构成，
执行层提供执行或者算力，共识层保证以太坊数据的健壮。

### 2025.02.07

#### Implementations and Development
- client and node  
 An implementation of the execution layer (EL) or consensus layer (CL) is called a **client**. A computer running this client and connecting to the network is called a **node**. 

- client diversity  
Ethereum client can be implemented in different language, which make it [diverse](https://ethereum.org/zh/developers/docs/nodes-and-clients/client-diversity/).
[Here is the implementations list](https://ethereum.org/en/developers/docs/nodes-and-clients/#execution-clients).

#### Testing

You can find some test tools from [here](https://epf.wiki/#/eps/week1?id=testing)
#### Coordination

- [PM repo](https://github.com/ethereum/pm)shows the schedule for coordination.
- You can also discuss or propose features through https://ethresear.ch/ or [Ethereum Magicians](https://ethereum-magicians.org/)

#### Bitcoin
> I think [this video](https://youtu.be/eEQ41gD0iC4?si=w5LNr1Va2oM2R0aX) should been seen by everyone who try to develop Ethereum implementations after learning about the basic concept of Ethereum.

Bitcoin is a Cryptocurrency, the transaction of Bitcoin include the following 
factors:
- Signature: To verify the owner of a request, not anyone else, verify the validity of the request.
- Uniqueness: The transaction request is Uni , to avoid the [Dual spending issue] (# "Deducting once from Party A's account and adding to two Party B's accounts")
So the **Proof of Work** comes on stage. 

### 2025.02.08

#### Proof of work (PoW)
> See also: https://youtu.be/_160oMzblY8?si=ySD7m-WXH__b5vlv
and https://youtu.be/eEQ41gD0iC4?si=w5LNr1Va2oM2R0aX

A block of ledger is needed to be proofed for its validity, so making it less likely to be created is a good proof method. 

An block chain is just like this(play it in [here](https://andersbrownworth.com/blockchain/blockchain)):
![block_chain](https://files.catbox.moe/oyxjpg.png)

The hash code below is calculate(or called **Mine**, yes! it is the button below) based on the Data, Nonce, Block, Prev.

- **Data** is the essence
- **Nonce** is the specific num by mining, which makes Hash have multiple zeros starting with it, the more the zeros the greater the workload
- **Prev** is the previous block's Hash, which included into the Mining in current block.
- **Block** is just a num of block index

The "Hash with Zeros" and the Nonce are exactly the Proof of Work.
#### Why is PoW trustworthy

1. Because of the "Chain", once a certain block in the middle is changed, all subsequent blocks will be changed, Moreover, there are many copy of ledger, the forged ledger will be overwhelmed by the correct version.
2. Of cause, the latest block maybe untrustworthy, or perhaps the latest ledger you received was indeed forged by someone else, who mined out in the fastest time. But this won't last long, other miners will soon surpass it, and the ledger will return to its correct state.

#### Proof of stake

[TODO](#proof-of-stake-pos)

#### Gas

Gas is the fee of transaction

**Gas and ETH**  

The unit of gas is *wei*, and Gas prices are usually quoted in *gwei*.
$$
1 gwei =  10^{-9} ETH
$$
**Gas fees calculating**  
$$
Gas\;fees =  units\;of\;gas\;used * (base \;fee + priority\;fee)
$$
- *base fee* is a value set by the protocol, which is finally to be burned and out of currency circulation.
- *priority fee* is a value set by the user as a tip to the validator.

### 2025.02.09
An overview of Week2

> See also: https://ethereum.org/en/developers/docs/nodes-and-clients/

#### Node
> $\mathcal{def}$: A **node** is any instance of Ethereum client software that is connected to other computers also running Ethereum software, forming a network.

**Node type**:  
- light: only download block headers
- full: 
    - Stores full blockchain data (although this is periodically pruned so a full node does not store all state data back to genesis)
    - Participates in block validation, verifies all blocks and states.
    - All states can be either retrieved from local storage or regenerated from 'snapshots' by a full node.
    - Serves the network and provides data on request.
- archive: full nodes that verify every block from genesis and never delete any of the downloaded data.

#### An Overview of the Ethereum Execution Layer
> https://www.youtube.com/watch?v=7sxBjSfmROc

**The Ethereum system**
- The Ethereum System is divided into EL(execution layer Or compute layer) and CL(beacon chain)
- By`notify_new_payload(payload)`, CL do nothing! CL just sends the execution payloads(State updating query) to the EL.
![](https://files.catbox.moe/crd2ea.png)

---
**Ethereum compute layer: the EVM**
> The EVM is just the core of the EL, EL include the [other parts](# "Mempool, State Storage, interface client").
- Two types of accounts:
    - *EOA*: the people's accounts.
    - *contracts*: the "bot".

![](https://files.catbox.moe/dwcric.png)

**Data associated with an account**
![](https://files.catbox.moe/zw9qh7.png)

**Account state: persistent storage**

- Only valid in the *contract*.
- The all data mentioned above is stored as an array(`S[]`)
- These array collectively define the status of the account and are stored in the *Ethereum state tree* through a *Merkle tree* structure.
- *Ethereum state tree* only calc the non-zero cells.

![](https://files.catbox.moe/cq6xbq.png)

### 2025.02.10

**State transitions: Tx and messages**

- Simply, the Txs can be divided into four types, here is just an analog:
    - 人 to 人
    - 人 to bot
    - bot to 人
    - bot to bot
- In the final analysis, the Txs only happen btw owned(people) and owned(people).
contract is called by owned as well.

> If it's just a Txs btw bots, then it's meaningless, isn't it?

![](https://files.catbox.moe/znbpck.png)

**State transitions: Tx and messages**

- When Tx to a "0" address of target, a new account will be created.
- nonce: prevent replay attacks, every transaction must have a nonce
    > there are two types of nonce, the Account nonce and Proof of work nonce  
See more: https://ethereum.stackexchange.com/questions/27432/what-is-nonce-in-ethereum-how-does-it-prevent-double-spending


![](https://files.catbox.moe/8w0tc0.png)

**The Ethereum blockchain: abstractly**

- accts: Accounts, the world state is a snapshot of the status of all accounts in the world
- Tx: The Tx actions
- log massages: show some characters about what the contract has done or what 
happened about Tx.

![](https://files.catbox.moe/5fztyz.png)

### 2025.02.11

**An Example contract: NameSystem**

A name system on Eth: [uniswap -> addr]
> is a simplified ENS, like DNS

Need to support three operations:
- `Name.new`(OwnerAddr, Name): intent to register
- `Name.update`(Name, newVal, newOwner)
- `Name.lookup`(Name)

``` solidity
contract nameSys{
    struct nameEntry{
        address owner;
        bytes32 value;
    }
    mapping(bytes32=> nameEntry) data;

    function nameNew(bytes32 name){
        //registration fee is 100 Wei
        if(data[name]==0 && msg.value >=100){
            data[name].owner = msg.sender
            emit Register(msg.sender, name)
        }
    }

    function nameUpdate(bytes32 name, 
                        bytes32 newValue, 
                        address newOwner) {
        // check if message is from domain owner,
        // and update cost of 10 Wei is paid
        if (data[name].owner == msg.sender && msg.value >= 10) {
            data[name].value = newValue; // record new value
            data[name].owner = newOwner; // record new owner
        }
    }

    function nameLookup(bytes32 name) {
        return data[name];
    }
}

```
1. ⚠️ Here the `nameNew`func is unsafe, Anyone can use this function to peek into the database or steal certain names and resell them.
> The resolve is commit-reveal
> TODO
2. The `nameLookup` is used by contracts, humans do not need this.(use etherscan.io)

**EVM mechanics: execution environment**

- The EVM is **Ethereum’s execution engine**, ensuring that smart contracts run **securely, in a decentralized, and deterministic manner**, making it the backbone of DeFi, NFTs, and DApps.
- EVM is compiled to bytecode

| Function | Description |
|----------|------------|
| Running Smart Contracts | Interprets and executes Solidity, Vyper-based contracts |
| Decentralized Computing | Executes on all Ethereum nodes, ensuring consistency |
| Transaction Processing | Verifies transactions, updates balances and contract states |
| Maintaining Blockchain State | Manages contract storage, account data, and logs |
| Gas Fee Management | Prevents excessive computation, incentivizes validators |
| Security & Isolation | Runs contracts in a safe environment to prevent exploits |

**Gas**

- Every instruction costs gas.
- Different instruction costs different gas.(See https://www.evm.codes/)
    > eg. SLOAD, SSTORE VS MLOAD, MSTORE, the former operate on blockchain(like disk), and the latter operate for single Tx(like RAM)
- Tx fees (gas) prevents submitting Tx that runs for many steps.
- During high load: block proposer chooses Tx from mempool
that maximize its income.
- Reducing on chain storage is advocated
    ![](https://files.catbox.moe/pcntjb.png)

**Gas prices spike during congestion**

**Congestion** can result in an increase in gas prices, which can bring 
more income for those block proposer.

![](https://files.catbox.moe/k63zc7.png)

**EIP1559: How to figure out this congestion issue?**

> EIP1559, since8/2021, goal: 
> - users incentivized to bid their true utility for posting Tx,
> - block proposer incentivized to not create fake Tx, and
> - disincentivize off chain agreements.

Links:
|Title|Year|Authors|
|---|---|---|
|[Transaction Fee Mechanism Design](https://arxiv.org/abs/2106.01340)|2021|T. Roughgarden|
|[Empirical Analysis of EIP-1559: Transaction Fees, Waiting Time, and Consensus Security](https://arxiv.org/abs/2201.05574)|2023|Yulin Liu, et al.|

### 2025.02.12

#### Proof of stake (PoS)
> See also:
>    - [PoW](#proof-of-work-pow)
>    - [The Beacon Chain Ethereum 2.0 explainer you need to read first](https://ethos.dev/beacon-chain)

**Slots and Epochs: the heartbeat to Ethereum’s consensus**

- Each *slot* is 12 seconds and an *epoch* is 32 slots: 6.4 minutes.
- the index of each slot is start at 0
- Every slots, one block is added when the system is running optimally
- slots can be empty

![](https://ethos.dev/assets/images/posts/beacon-chain/Beacon-Chain-Slots-and-Epochs.png.webp)

**Validators and Attestations**

- A block proposer is a validator that has been **pseudorandomly** selected to build a block.
- Most of the time, validators are **attesters** that vote on blocks, just like
a committee, [with each person randomly sitting in power](# "随机坐庄").
- Validators is police each other and are rewarded for reporting other validators that make conflicting votes, or propose multiple blocks.
- An **attestation** is a validator’s vote, weighted by the validator’s balance. 
- The validators not only broadcasts new blocks, but also Attestation to indicate their recognition of the block.

> Beacon Chain is different from World State Chain!!!

### 2025.02.13

#### Stakers and Validators

1. Stakers（质押者）：
   Stakers like "capitalist", wich mean those who holding "money".
   - Everyone can become a staker.
   - If you have ETH over 32, such as 55, you can stake all, the part of 32 is to activate one validator,
     and the remain is to activate another one. Of course, you will get the all reward from the 32-voted one,
     and get the part from the another one.
   - If you have ETH less than 32, you can also stake into a pool to activate a validator and get the part
     reward.
2. Validators(验证者)：
   The only requirement to become a validator is the certain "money"(ETH)
   - You should become a staker before validator(Means that holding ETH in fact)

### 2025.02.14

#### Why is the committee set to 128 people
[Minimum Committee Size Explained](https://medium.com/@chihchengliang/minimum-committee-size-explained-67047111fa20)
> See also: https://ethos.dev/beacon-chain

This photo is one from the article above. 
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*hoRCxFzkTaHZuXdo1kfqyQ.png)
- A constant `TARGET_COMMITTEE_SIZE` of 128 is chosen as an approximate number of 111 because every constant in the specification is defined as a power of 2. 
- $\frac{1}{3}$：Supposing the rate of attackers😈 in all validators is $\frac{1}{3}$.
- $k = [\frac{2}{3}n]$: k means the num of attackers😈 when a new committee 
with $n$ validators is chosen. The $\frac{2}{3}$ here does not means the rate of honest validators😇 in all validators($1-\frac{2}{3}$). In PoS of ethereum,  it needs 2/3rd majority to attest and block on to the beacon chain.

> Why $\frac{2}{3}$
> https://www.fanwb.xyz/posts/casperffg/#%E4%B8%BA%E4%BB%80%E4%B9%88%E6%98%AF%E4%B8%89%E5%88%86%E4%B9%8B%E4%BA%8C
> https://eth2book.info/capella/part2/consensus/casper_ffg/#why-two-thirds

### 2025.02.15
### 2025.02.17

#### LMD GHOST

- GHOST: (Greedy Heaviest Observed Sub-Tree) is a fork selection algorithm that selects a subtree containing the most proof of work (PoW)
- LMD-GHOST: LMD-GHOST is a variant of GHOST and is suitable for Proof of Stake (PoS) system.
![图片](https://github.com/user-attachments/assets/277b6148-ed36-49cf-aa28-be1b000fd77b)
Let's see what happened to the blocks in this diagram:
- Defining the three block to Alice, Bob, Eve(who proposed the block)
- For Alice, it received three attests, but two is from committee A, and one is from committee B
- For Bob, it received only two attests from committee B
- For Eve, it received three attests, all of them came from the committee.

Do you think which blocks will be chose by LMD GHOST? The answer is Alice and Eve, 
and the Eve is built based on the Alice.  
At slot1, none of them were selected as head, at slot2, Alice was set as head, 
at slot3, Eve was set as head based on Alice.

Let's see what happened to the validator in this diagram:
- One in committee A is offline.
- One in committee B is vote the Alice for some reason like network delay.
- As such case above, the Alice and Bob received a abnormal attests.

Eventually, Eve was reached a consensus.

#### Beacon Chain Checkpoints

![](https://ethos.dev/assets/images/posts/beacon-chain/Beacon-Chain-Checkpoints.jpg.webp)
- A checkpoint is a block in the first slot of an epoch.  
- If there is no such block, then the checkpoint is the preceding most recent block.  
- There is always one checkpoint block per epoch. A block can be the checkpoint for multiple epochs.
- Epoch boundary blocks (EBB) = checkpoints

### 2025.02.18

#### FFG vote

**What is FFG vote?**  
At the end of each epoch, the start of each epoch, the validator votes on the checkpoint block and tries to finalize the block.
FFG vote consists of two parts:
- *source*: The latest justified checkpoint that has been voted before.
- *target*: The checkpoint block of the current epoch.

If enough validators vote for a *target* as the new justified checkpoint, and the next epoch votes to confirm it, it will be finalized.

**When dose FFG vote happen?**  
At the end of each epoch (after 32 slots), the start of each epoch, the validator start to submit their FFG vote.
> Be cautious that FFG and block proposal and confirmation are two different processes, this will be mentioned again in the next section of Finality

### 2025.02.20

**How long does FFG vote last?**  
Because one FFG attestation only can be submitted at one slot from one committee, 
it will last until receiving ⅔ of attestations, means 22 slots(which was mentioned below). 

> $\mathcal{def}$ **Supermajority**: A vote that is made by ⅔ of the total balance of all active validators, is deemed a supermajority.  

**Finality**

> $\mathcal{def}$ **Justified**: At the start of a epoch(slot 1), all validators is gave a justify query to justify the checkpoint of prior epoch, once ⅔ of attestations reached, this checkpoint is justified.  Typically, a checkpoint is justified in ⅔ ~ 1 epoch.  

> $\mathcal{def}$ **Finality**: If a checkpoint B is justified and the checkpoint in the immediate next epoch becomes justified, then B becomes finalized.  Typically, a checkpoint is finalized in 1⅔ ~ 2 epochs, 10.7 ~ 12.8 minutes.  

Note that the time is measured from when the FFG vote is recorded (slot 1 of the next epoch). If a Tx is written in the middle of an epoch (slot 16), the total time required is 0.5 + 1 + ⅔ epochs until finalized.

In this diagram below, checkpoint at slot 32 is justified before slot 64. Info of FFG voting at 32 is saved at slot 32, and these info is proved at slot 96, which mean being finalized.

> ⚠ If checkpoint at slot 32 haven't been justified in epoch 1, FFG will restart from slot 64.

> 💡 The issue about the justification of a block can sometimes finalize a block two or more epochs ago.

![](https://ethos.dev/assets/images/posts/beacon-chain/Beacon-Chain-Justification-and-Finalization.png.webp)

**Proposers and bribery(贿赂)**  
TODO  
Proposers are only assigned to slots once the epoch starts, 
But how to avoid a bribery of proposers?[secret leader election](https://ethresear.ch/t/low-overhead-secret-single-leader-election/5994)

### 2025.02.21
# Staking 奖励和惩罚

1. attester rewards：

   - validators通过参与attest(LMD GHOST and FFG votes)获得rewards
   - 如果成功达成一个Finalized block，你将获得更多

2. attester penalties：

   - attesting未执行（无作为）
   - attesting给一个未被finalized的block（错误行为）

3. typical downside risk for stakers

   站在一个Staker的角度来看，我们关注的是收益损失的回报比

   - penalty是reward的¾（比如，好人😇全勤一年获得10%的reward，那么坏人😈会被penaltied 7.5%）

4. slashings and whistleblower rewards

   slashings就是举报的意思

   - $\mathcal{def}$: The protocol also imposes an ==additional penalty== based on how many others have been slashed near the same time.
     $$
     Additional\_penalty = validator\_balance\times 3\times fraction\_of\_validators\_slashed
     $$

5. proposer rewards

   proposer能得到更多的奖励

   - validator在Tx中提出slash，proposer将该Tx推送到block中，就能获得reward

     > 😕Currently, all of the whistleblower’s reward actually goes to the proposer.

6. inactivity leak penalty

   这与#3所说的不一样，这个惩罚机制主要是针对集体事件的

   - 当一个block在4个epoch后依然没被finalized，就可判定为1/3以上的validator不活跃😈，就会触发inactivity leak penalty
   - 惩罚力度成2次指数（quadratic）递增，目的是为了让坏人😈尽快下线，让剩下的人😇达成2/3多数。

# Slashable Offences

有四种情况能被指控：

1. **double proposal**：一个slot提出一个以上block

2. **LMD GHOST double vote**：在同一个slot，同时attest给两个head block

   > 验证者如何同时看到两个不同的 Beacon Chain 头？
   >
   > 1. 网络延迟或分区; 2. 恶意行为; 3. 客户端 Bug

3. **surround vote**: 
   See also: https://github.com/protolambda/eth2-surround?tab=readme-ov-file

   - $\mathcal{def}$: 
     ```
     s: source
     t: target
     
     a surrounds b if: s_a < s_b < t_b < t_a
     
     s < t is a pre, so the condition can also be:
     
     s_a < s_b and t_b < t_a
     ```

4. **FFG double vote**: 
   在一个Epoch(或slot)同时提出两个不一样的FFG vote对。比如：

   - 同target不同source

   ![](https://ethos.dev/assets/images/posts/beacon-chain/Casper-FFG-Double-Vote-Example-1.png)

   - 同source不同target
     ![](https://ethos.dev/assets/images/posts/beacon-chain/Casper-FFG-Double-Vote-Example-2.png)

> ✅同一个attestation出现在不同aggrevates(聚合)
>
> - 同一个attestation可能会被不同的[aggrevators](https://eth2book.info/capella/part2/building_blocks/aggregator/)收集，但本质上是同一个attestation，所以并不会被判定为double vote
### 2025.02.22
