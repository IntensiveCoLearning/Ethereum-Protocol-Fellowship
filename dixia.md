---
timezone: Asia/Bangkok
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Pacific/Honolulu # 夏威夷-阿留申标准时间 (UTC-10)
---

# dixia

1. 自我介绍: 一名 Crypto 研究员
2. 你认为你会完成本次残酷学习吗？Try my best
3. TG 联系方式：@imkurt

## Notes

<!-- Content_START -->

### 2025.02.06

Node and EL. But is this a physical scope separation? Need to learn more. 

EOA controlled by key pair. Contract controlled by code.

Every smart contract's persistent storage is just an array of 32 bytes. The root is a MPT hash. Does balance take up space of storage? Nope

Messages are just tx from contract without signature but then how do other contracts know the message is from the initial contract?
And how does EVM verify the message (virtual tx)?

https://cs251.stanford.edu/lectures/lecture7.pdf [0]

### 2025.02.07

Block Data Structure: world state root has MPT hash of all accounts on Ethereum.

It takes 16tb to run an archive node rn.

EVM still uses stack (max: 1024) to execute code but with JUMP instruction code.

Burn ether preventing off-chain fee refund agreement to proposers (I did not think before). A proposer could create/encourage fake txs to farm more ether reward if eth not burned and refund gas fee off-chain. The fee they paid would be less than eth reward to block proposer which is the case given there is ether inflation for block proposers. But why would proposers be incentivized to do this? They could just collect reward from block building without the trouble of creating fake txs unless the block reward is proportional to the txs they included?

In bitcoin's world, miners have fixed cost for mining the block but they do get fee reward as well. So this could apply to Bitcoin as well.

### 2025.02.08

#### Why would proposers engage in off-chain fee refund agreement

It is not due to the block reward as it is not proportional to the txs they included. But for the following reasons:

1. Proposers could fake transactions to create an impression/illusion of higher activity on the chain. Given if they could get the gas fee back, the cost of artificially creating txs is very low (transaction fee + effort to inflate txs). But that would require you control majority of the validator nodes or can reliably predict the next block proposer. The former could be the case actually right now? Given there are 2-3 block builders building most of the blocks (builder == proposer?)

2. To bid up the gas fee so other users have to pay more to get their txs included. This could require the same condition as above. As you intentionally pay a higher gas fee but can recover most of it back. It would be in the interest of proposers to do so. This would apply to Bitcoin as well. If majority of mining pools have an agreement. Could very well be the case for other chains.

#### 
Gas fee before EIP-1559 feels like a spam preventing mechanism rather than a fee market which prices different resources.

Encrypted mempool: total gas case has to be unencrypted. Cosmos has encrypted mempool. General idea no one have seen a complete solution available yet.

### 2025.02.10

An epoch has 32 slots.

A validator will be randomly selected to be a proposer for a slot. So the validator is the proposer.

1 slot has 3 phases and a block:

propagation (broadcast)
attestation aggregation (fork for a block (not sure if this is only rely to fork rule or other rules))
aggre propagration: broadcast the voted block

finality

first justifiy a block which mean 2/3 has pass the checkpoint ( what is checkpoint cmp to block? ) for it
then the last justified block is the finalized block.

12s for a slot is based on the block time of PoW ETH

why have a slot instead of a block?

#### MEV

proposer can reorder txs in a slot. so I guess other validators has no way to verify the order of txs in a block when they attest to it. I guess this is why validators only follow the fork-choice rule

given the deadline for attesetion is 4 seconds, so that give you some idea on how much bot could MEV using the time advantage.

#### spam txs

actually once is a validator is chosen to be a proposer, it can know therefore it could time the opportunity to spam txs.

https://www.paradigm.xyz/2023/04/mev-boost-ethereum-consensus
https://epf.wiki/#/eps/week3



### 2025.02.11

a commmitte is of 128 validators.
a validator run a beacon node 

still not sure why a committe concept is needed after watch all these video

PoW consensus use economic (hash power) to reach consensus which looks a lot simpler. Through it does give entity who has most computing power an advantage so it is more close to "real" economy where PoS could at certain time depeg from real economy power. As long as stakeholder/token holder has a little real world economy power(pay for server and bandwdith). (eth will have price but it is less impact by commodity price such as electricity) it is easier to develop as independent set of stakerholders on its own economy compare to Bitcoin i.e. if someone is very good at investing/trading, he or she could acquire ether at lower price. But you alway need to pay for a market price for electricity. PoW resets the game each time but does make bitcoin's opeartion more close to "real world".

### 2025.02.12

fork choice rule == LMD GHOST 

"Node and EL. But is this a physical scope separation? Need to learn more."

EL execute EVM and validate evm related logic and generate a block. It also maintain mempool for sharing the txs which has not been included in the block. EL also handle RPC requests. So CL node and EL software are separated. 

"The challenge a consensus protocol seeks to solve is that of building a reliable distributed system on top of unreliable infrastructure." 

"the nodes must agree, and they must come to agreement swiftly."

"So, if I have 1 ETH and I simultaneously tell the network that I am sending that 1 ETH to Alice and also to Bob, we expect that eventually the network will agree that either I sent it to Alice or I sent it to Bob. It would be a failure if both Alice and Bob received my Ether, or if neither received it."

https://eth2book.info/capella/part2/consensus/preliminaries/

#### fork choice rule == Gasper

when consensus prevent are issue:

network delay (probably most common cases)
code error/conflict
bad actors

mostly preventing forks

liveness vs. safety. PBFT is always safe (so not fork?)

goal is select most likely linear chain

first rule of fork rule is the block and ancestor of the block are valid

todo:

keep reading https://eth2book.info/capella/part2/consensus/preliminaries/#fork-choice-rules

Execution layer validate cryptographic perspective of safety and together with consensus layer it make sure the validation rule (cryptographic rule ) are follow (safty) and working (liveness)?

### 2025.02.13

read more about fork choice rules particular about casper & LMD GHOST

### 2025.02.15

一个节点排序交易。共识机制排序区块。

checkpoint is used for mark a block's finality.


"system...are politically decentralised (for permissionlessness and censorship resistance), architecturally decentralised (for resilience, with no single point of failure), but logically centralised (so that they give consistent results)."

GHOST is a fork choice rule which was meant to replace the bitcoin's longest chain rule consensus(2013).

So LMD ghost decide the head block and casper decide the finality of the block.

TODO

kept reading https://eth2book.info/capella/part2/consensus/lmd_ghost/#finding-the-head-block and consider read the GHOST paper

### 2025.02.17

GHOST: "the block are off the main chain can still contribute to the chain weight"

Why it is better than longest chain rule? 

If there is a fork, likely there are latency but a subtree that has more leafs mean the the head of tree has been built on (meaning they all agree on that head block)by more validators/miner, there the chance to build a linear chain from there is higher.  When they are two competing leafs, just chose the one with heavier weight. And this information is discarded by longest chain rule which also allow secret mining. interestingly, this idea is originally meant for bitcoin but has never been adopted( the argument is fork does not happen frequently for 10 mins block time). the GHOST paper made a statement that without changing the longest chain rule, it will not be sufficient to just increase the block size or block time.

todo:

https://eth2book.info/capella/part2/consensus/lmd_ghost/#confirmation-rule

keep read page 10 (ghost)

### 2025.02.19

confirmation rule:

In ETH2, consensus layer has more information of a block's consensus perspective than PoW version. Namely beside the view of a proposer, you can get the head block's vote from other validators( derived from fork rule)

The exact rule is basically the vote of one sub root recevive since that subtree root has been proposed.

incentive design for fork rule:

* proposer has incentive to build on best head given there is higher chance to get the block included. if their block is reorged, they will not received rewards.
* validators have incentive to head vote (attestion is included next slot (block) so it can get the more reward.(22% for total reward)

discourage double building:

reason that proposer will multiple building is the cost of building a block is almost 0.
next proposer can submit a proof that previous proposer is double building. given it is all signed so it can be verified. And proposer will get reward to prove that.

same for attesetion

LMD GHOST is speced in 2018.it's original idea started as early as 2015.

TODO:

https://eth2book.info/capella/part2/consensus/casper_ffg/

rewriting notes

keep read page 10 (ghost)



<!-- Content_END -->