---
timezone: Asia/Shanghai
---

---

# Louis Tsai

1. 自我介绍
Hi, my name is Louis. I'm  a security researcher focusing on the Ethereum ecosystem. 
1. 你认为你会完成本次残酷学习吗？
Yes.

## Notes

<!-- Content_START -->
### 2025.02.06
I finished the protocol wiki week0 and week1.
And this blog post from Vitalik: https://vitalik.eth.limo/general/2017/09/14/prehistory.html
The wiki is awesome, it provide very useful resource to me.

### 2025.02.07
Today I learn the protocol overview and the protocol introduction in protocol wiki. I already know the protocol architecture contains the execution and consensus layer but do not know much about the details. I read the breakdown and gain more insight about Ethereum core!

### 2025.02.08
Read the week2 recording on the study group wiki and read the content regarding the execution layer. Complete the EL Specs part!

### 2025.02.09
Today, start learning some fundamentals for Pectra's next upgrade, which will include the EOF updates. The changes are documented in EIP-7692. This upgrade significantly impacts the execution layer, so it includes a large number of EIPs!

### 2025.02.10
Watching the video for introducing the EOF and some examples in the update: https://www.youtube.com/watch?v=WKVgCoNp39g.

### 2025.02.13
Watch this video to learn stack validation algorithm in EOF upgrade: https://www.youtube.com/watch?v=80szRrNW0MM It is hard to learn purely from EIP, but the video demonstration is clear.

### 2025.02.14
Start reviewing the EEST codebase and try to find an issue I could contribute to, and dive deeper into the EOF implementation.

### 2025.02.15
I reviewed this PR: https://github.com/ethereum/execution-spec-tests/issues/770, and the EEST contribution guideline.

### 2025.02.16
I reviewed the recent discussion of Fusaka upgrade, and found some people are against the EOF upgrade, since we still need to maintain the legacy client code but add much complexity to the current design. In my opinion, the EOF is necessary, it is not only limited to solve the "stack too deep" issue, but allows more moduler future integration and more possibility.

### 2025.02.17
I start my contribution to the EEST projects, but I encounter some problem during installation. And I review the documentation and try to solve the issue but failed. I join the office hour hosted by EPF to ask for answer.

### 2025.02.18
I review the EIP-3540, and start integrate the EIP into my EVM decompilation project. I encounter some issue when dealing with the layout. But there is some problem in Java language.

### 2025.02.21
Integrating EOF into Mothra, extracting header information from the bytecode and display in the decompilation header.

### 2025.02.22
Start analyzing the EIP-7702 in the Pectra upgrade, and participate in the Ethereum audit contest. I start with the virtual machine section and try to find issues.
<!-- Content_END -->
