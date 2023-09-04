# 👩🏼‍💻 A New Developer’s Bullet-Point Guide to Blockchains and Cryptocurrencies (Part 1/4) // Basics

Diving into the world of blockchain can be intimidating! Everything feels raw and like thieves and scammers are lurking around every corner. And admittedly both may be true! It took me months of doing deep-dives and first-hand experiments to get remotely comfortable just buying my first coins. I pored over a myriad of resources that gave me bites of information here and there but failed to find one authoritative, easy-to-understand, and comprehensive place to go to. So I thought this article might be helpful.

A quick-start guide that’s hopefully straightforward and clear and just dense enough to lead you to the rabbit hole.

The guide is written in 4 parts:
The bare minimum basics (what is blockchain)
Transaction examples (show me the money — tech version)
2.1. Transaction examples… // Ethereum
2.1.1. Transaction examples… // Ethereum // EVM
More quick blockchain concepts
A comparison chart (cheatsheet of 5 top blockchains)

This guide is by no means itself authoritative and has been drawn from various sources across the web and my own understanding along the journey. Big shoutout and thanks to all the brilliant and generous bloggers and developers out there who have indirectly contributed to this piece (pivotal resources I used have been included at the bottom of the comparison chart which is TBC).

If you have any suggestions on how to make this guide better please feel free to reach out to me. Until then, have fun, good luck, and see you on the blockchain!

And without further ado…

Part 1 — The Bare Minimum Basics

From the beginning — what is blockchain?

Blockchain is a decentralised trust-based network of computers that each run on / collaborate through consensus algorithms prescribed by the blockchain to do work and earn rewards. Each blockchain has its own consensus mechanism and work usually comprises of recording and facilitating transactions in addition to solving a system labour-intensive computation problem. All blockchain transactions are public information. Computers, or nodes, that partake in a blockchain network are incentivised to run the network accurately and quickly through fees they receive paid by users who request work to be done (i.e. initiate a transaction on the blockchain) and/or the reward of coins by the blockchain itself. These nodes are called miners and such coins are distributed by the blockchain algorithm when the node (or a pool which is a collection of nodes) has completed the work. Only one mining node or mining pool will win the rewards by being the first to complete the work. Like with consensus mechanisms and types of work, rewards also vary by blockchain. Nodes are discouraged from manipulating blockchain data by natural defence mechanisms that are part of the consensus algorithm.

Blockchains are called blockchains because of the way data is structured. Nodes lay transaction records into the form of blocks with blocks appended to a single running chain of transactions. Forks of an original blockchain can occur and nodes must then decide which chain will be selected as the main one.

What does decentralised mean? Decentralised means that the network or ecosystem is not owned or operated by any one single organisation or person, etc. but rather each node operates independently on its own, in collaboration — through communication, trust, and principle(s) — with other nodes. In the case of blockchain such principles are essentially consensus algorithms and cryptocurrencies.

What do we mean by “work”? The kind of work done on the blockchain can range from recording transactions as a simple accounting system such as with Bitcoin to more complex scenarios carried out via smart contracts as on Ethereum. Different blockchains are best used for different types of transactions. Work will also include any other requirements set by the consensus algorithm (typically solving computation problems that require large amounts of energy and effort expenditure).

What is a consensus algorithm? Consensus algorithms establish the principles for node participants about how they can operate on a particular blockchain network. These algorithms use cryptography to promote the security of the network whilst using rewards to promote its efficiency. Each blockchain can have its own consensus algorithm but there are two principles that apply to all blockchains and are inherent in the nature of blockchain by design (1) the transparency and (2) immutability of information stored on the blockchain. Further information about a blockchain’s operating principles or consensus protocols can be found within its whitepaper and yellowpaper.

Consensus protocol defences promote the security of a decentralised system by making it practically impossible for bad actors to manipulate data. Consensus algorithm defences typically use a combination of a Sybil resistance mechanism and a chain selection mechanism (this duo combination is called a “Nakamoto Consensus”) to protect themselves against a Sybil attack.

A Sybil attack occurs when the network is attacked by a bad actor seeking to gain disproportionate influence through the creation of multiple identities. Typically at least 51% of the network must accept a new block to confirm the block and the longer the chain (the more nodes which have accepted the transactions) the more confirmed the transactions are. This 51% rule means that any modification to established blocks or data on the network would require at least 51% control of the network. The system labour-intensive computation problems presented in the algorithm means that in order for an attacker to gain 51% control it would need to have enough computing power to rewrite previous blocks and overtake good actors that are continuing to process new transactions. In terms of chain selection, the Bitcoin consensus protocol selects the longest or “heaviest” chain as the main one whilst Ethereum uses the GHOST (Greedy Heaviest Observed Subtree) protocol to decide.

Proof of Work (PoW) Consensus Mechanism A common type of consensus algorithm for selecting the winner of a blockchain’s rewards is based on proof of work. PoW involves solving a computation puzzle that takes energy and effort (i.e. computing power) and whichever node solves it and also completes the block accurately first earns the rewards which the blockchain automatically distributes. The blockchain maintains block difficulty consistent across the network for fairness and sets a target number of blocks it seeks to process during a specific time period (the algorithm adjusts block difficulty level to enforce this target). This helps facilitate steady mining-side traffic.

Proof of Stake (PoS) Consensus Mechanism Another common consensus mechanism is proof of stake. PoS requires considerably less computational power and functions using validators that are chosen algorithmically to complete a new block whilst other validators attest that blocks look correct. Validators are required to “stake” — or put up a certain amount of a blockchain’s existing coins as collateral — in order to participate in the selection. Once a proposed block completed by a selected validator receives the required number of attestations the block is included and the validator earns the reward for doing the work. Validators lose their stakes if they attest to malicious blocks.

What is a cryptocurrency or coin? A cryptocurrency / coin is the reward earned by miner nodes or validators when a certain amount of work (typically a block) has been done by being the first or selected to complete the block accurately.

What are transaction fees? Transaction fees are the fees that users pay in order to have work done or transactions processed and recorded on the blockchain. Transaction fees are typically based on transaction data volume and the congestion of the network usually with those with higher fees being prioritised by miners. Block fees are distributed to the winner of each block.

What is a fork? A fork of a blockchain occurs when a new instance of the blockchain incorporates development changes to its core protocol. A soft fork of the blockchain means there remains a single blockchain and the changes are backwards compatible with pre-fork blocks and the protocol. A hard fork means that the new chain is no longer compatible with pre-fork blocks or the original protocol resulting in two chains and thus new coins. Hard forks are permanent.

And that’s about it for Part 1! Move forward to Part 2 Transaction examples — let’s get technical.
