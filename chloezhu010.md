---
timezone: Europe/Berlin
---

# Chloe Zhu

1. 自我介绍
    - Chloe，[ETHPanda](https://x.com/EthPanda_org) Core team，prev [EIP Fun](https://x.com/EIPfun) project lead
    - 去年参加了第一期 EPF study group，对以太坊底层协议研发开始上瘾，去年10周 study group 的笔记也可以作为参考：https://hackmd.io/@chloezhux/epfsg_notes ， 目前我对 protocol network/ light client 比较关注和感兴趣
    - 底层协议的信息量巨大，前沿领域也在不断发展，需要一遍遍不断学习，so here I am~
    - 我的 [Twitter](https://x.com/Chloe_zhuX) 和 [Telegram](https://t.me/chloe_zhu)
2. 你认为你会完成本次残酷学习吗？
    - 一定！

## Notes

<!-- Content_START -->

### 2025.02.06

Quick review of Week 0
- What's a P2P network
    - Definition
        - A decentralized communication model where nodes in the network can communicate directly with each other witout a central server
        - Unlike traditional client/ server model, where a centralized authority manage all connection & data transfer, p2p network distribute workload and data among participants
    - Key features of p2p network
        - decentralized: no central server, nodes share data directly
        - scalable: network grows as more nodes join
        - fault tolerance: no single point of failure
        - resource sharing: peers can share computing power, storage, or bandwidth
    - Type of p2p network
        - unstructured p2p
            - nodes randomly connect (eg. Gnutella, Kazaa)
        - structured p2p
            - use algo to route data (eg. DHT in BitTorrent, Kademila)
        - hybrid p2p
            - mix of decentralized peers and some centralized componenets
- What type of p2p is Ethereum and Bitcoin
    - Bitcoin: mostly unstructured p2p with a gossip protocol for tx & block propagation
        - Network structure
            - bitcoin nodes randomly connect to other nodes
            - tx and blocks are relayed to neighbours, which propagate them further
            - nodes discover & main peer lists dynamically
        - Data progagtion
            - Uses flooding (gossip protocol) where each node forwards data to its connected peers
        - Peer discovery
            - use DNS seed nodes, hardcoded bootstrap nodes, and peer exchanges
    - Ethereum: structured p2p with Kademlia DHT
        - Network structure
            - used a modified Kademlia DHT to structure peer discovery & routing
            - nodes are identified by unique IDs and stored in tree-like structure for efficient lookup
            - allow for faster peer discovery & data retrieval compared to Bitcoin
        - Data propagation
            - also use gossip protocol
            - has additional subnetworks (devp2p, libp2p) for different types of data, eg. state sync, block propagation, tx relaying
        - Peer discovery
            - use a Kademlia DHT for peer lookup
            - nodes maintain a routing table that organizes peers based on proximity in the DHT
      
    |         | Bitcoin | Ethereum |
    | -------- | ------- | ------- |
    | network type  | unstructred p2p    | structured p2p (kademlia DHT)    |
    | node discovery | random peer selection, DNS seed     | kademlia DHT for structured peer lookup   |
    | data porpagation    | gossip-based (flooding)    | gossip-based + DHT routing   |
    | efficiency    | redundant message forwarding    | more efficient lookup   |


### 2025.02.07

<!-- Content_END -->
