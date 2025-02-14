---
timezone: Asia/Shanghai
---


---

# realgu

1. 在金融行业做软件开发。去年看了许多v神文章，大为振奋，在3700大举买入以太，并持有至今 ：）推特账号 @0xrealgu 欢迎互关
2. 之前完成过链上叙事共学，这次应该也没问题，期待

## Notes

<!-- Content_START -->

### 2025.02.06

看完了week1 writeup，有许多不错的参考资料链接，有空慢慢看

### 2025.02.07
边看边记：
- execution layer and concensus layer are actually two different clients, each have its own p2p network
- 重点研究: trie, merkle trie/tree, patricia trie, merkle-patricia trie, verkle trie 把leetcode150里面trie的题做了

### 2025.02.09
- trie: also known as prefix tree, 做一道题就全明白了 [check this](https://leetcode.com/problems/implement-trie-prefix-tree?envType=study-plan-v2&envId=top-interview-150)
- Patricia trie: a trie in which each node that is the only child is merged with its parent. [check this](https://en.wikipedia.org/wiki/Radix_tree)
- Merkle tree: a tree of hashes. [check this](https://www.investopedia.com/terms/m/merkle-tree.asp) Bitcoin's software does not run the entire block of transaction data through the hash function all at once. Rather, each transaction is hashed, then a pair of transactions is concatenated and hashed together, and so on, until there is one hash for the entire block. If there is an odd number of transactions, one transaction is doubled, and its hash is concatenated with itself.
- why don't we just have a hash of all transactions concatenated? why do we run a lot more hashes by building a merkle tree? The Merkle tree is useful because it allows users to verify a specific transaction without downloading an entire blockchain—which can be hundreds of gigabytes in size. For example, say that you wanted to verify that transaction TD is included in the block in the diagram above. If you have the root hash (HABCDEFGH), you can query the network about HD. It might return HC, HAB, and HEFGH. The Merkle tree allows you to verify that everything is accounted for with three hashes: given HAB, HC, HEFGH, and the root HABCDEFGH, HD (the only missing hash) has to be present in the data. Additionally, the structure is helpful because the process is very fast. It seems as if hashing thousands of transactions would be time-consuming, but modern computers can do it in milliseconds. Because it is easy for computers to do, it makes sense to use the technique to verify large amounts of data, like the data contained in a blockchain. Merkle roots, trees, and block hashes are what create the unalterable chain of transactions and blocks.
- merkle-patricia trie [checkthis](https://ethereum.org/en/developers/docs/data-structures-and-encoding/patricia-merkle-trie/)

### 2025.02.10
- 1e = 1 billion gwei
- 一笔交易大概需要21000 gas unit，每个block 的 gas limit 目前大概 30m gas unit，base fee是 gwei / gas unit
- 晕了 EL Spec 很难读下去，暂时跳过吧

### 2025.02.11
State Trasition Function:
```
func stf(parent types.Block, block types.Block, state state.StateDB) (state.StateDB, error) { //1
    if err := core.VerifyHeaders(parent, block); err != nil { //2
            // header error detected
            return nil, err
  }
  for _, tx := range block.Transactions() { //3
      res, err := vm.Run(block.header(), tx, state)
      if err != nil {
              // transaction invalid, block is invalid
              return nil, err
      }
      state = res
  }
  return state, nil
}
```
问题: what exactly does a 'state' contains? what are the tries?

### 2025.02.12
Ethereum state is stored in four different modified merkle patricia tries (MMPTs):
- Transaction Trie
- Receipt Trie
- World State Trie
- Account State Trie

计算机组成课flashback：  

1 word = 32 bytes, 1 byte = 8 digits = 2 digits in hexadecimal  

The EVM stack has a maximum size of 1024 items. PUSH -> PUSH -> ADD  
Also there's a program counter and JUMP. But where is compare and jump insn like bne, bge, blt?  
And there's an available gas counter.  


EVM memory is a byte array of 2<sup>256</sup> (or practically infinite) bytes . All locations in memory are well-defined initially as zero.  
MSTORE takes two values from the stack: an address offset and a 32-byte value. It then writes the value to memory at the specified offset.  

In EVM, memory is dynamically allocated in multiples of 1 word “pages”. Gas is charged for the number of pages expanded.  
MSIZE: number of words/pages allocated  

Storage can only be accessed via the code of its associated account. External accounts don't have code and therefore cannot access their own storage.  

SSTORE takes two values from the stack: a storage slot and a 32-byte value. It then writes the value to storage of the account. So an account have associated storage



<!-- Content_END -->
