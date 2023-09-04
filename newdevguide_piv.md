# 👩🏼‍💻 A New Developer’s Bullet-Point Guide to Blockchains and Cryptocurrencies (Part 2.1.1/4) // Ethereum // EVM

This guide is written in 4 parts (with in between bonus parts that emerged out of interest, importance, and perceived helpfulness in understanding fundamentals).
The bare minimum basics (what is blockchain)
Transaction examples (show me the money — tech version) // Bitcoin
2.1 Transaction examples… // Ethereum
2.1.1 Transaction examples… // Ethereum // EVM
More quick blockchain concepts
A comparison chart (cheatsheet of 5 top blockchains)

This is the fourth or technically Part 2.1.1 out of what is a four-part series.

If you’ve read the first three parts, you should now have a strong grasp of blockchain first principles and how the Bitcoin and Ethereum blockchains execute a normal transaction.

This is a beginner blockchain developer’s guide to the EVM. Keep in mind Ethereum is a complex Layer 1 and there are many nuances to its architecture, infrastructure, and the ways in which users and developers can interact with it. For more advanced technicals feel free to browse through a few resources I’ve included at the end as further starting points.

The way these articles has been written builds upon previous articles in knowledge acquisition. If you find yourself unfamiliar with the terminology or concepts please refer back to earlier articles in this series or check the w w w. These articles also assume a certain level of working knowledge in computer programming / science. Stylistically this is a compact article balancing low-level details in a bullet-style way designed to pack as much detail as comprehensively as possible to get you comfortable with relevant critical concepts.

Now that we’ve run through the execution and consensus layers of Ethereum, what happens after the transactions are recorded onto the blockchain? How does the blockchain execute said programs or smart contracts?

Part 2.1.1 - Transaction examples (show me the money - tech version ) // Ethereum // EVM

https://ethereum.org/static/9628ab90bfd02f64cf873446cbdc6c70/302a4/gas.png

What is the EVM (Ethereum Virtual Machine)?
At the end of an epoch in ETH2, the state transition function performs bookkeeping to figure out what happened on the consensus layer during this period of time and prepares for the next epoch. Core Ethereum operates the EVM (Ethereum Virtual Machine) which can be thought of as a distributed algorithmically-deterministic state machine - or a lightweight operating system which is a sandboxed runtime environment designed to run Ethereum’s smart contracts. The EVM updates its state according to transactions from confirmed blocks and its state may be considered updated when a block is accepted.

The EVM consists of three main components: (1) working memory (non-persistent / volatile / linear random-access) (2) its stack which tracks the instructions it executes and (3) a program counter which continuously calculates gas fees (transactions in the EVM have costs and every transaction starts at 21000 gas). Worthy to note on gas costs - when execution instructions reduce state size refunds are possible though it cannot exceed half the gas used for the current contract call, and is only refunded once contract execution ends. The EVM stack has a max height of 1024 x 256-bit width items with only the most recent 16 items able to be accessed / manipulated at once. The stack works under LIFO (Last In First Out) and PostFix Notation arithmetic principles. The EVM operates on low-level machine bytecodes called opcodes (operation codes) which are human readable with hexadecimal value counterparts. Opcodes are 1 byte each so there can only be a maximum of 256 (16²) opcodes with 1 byte equal to 2 hexadecimal characters. There are 140 unique opcodes (for a full list of current opcodes - see here). Each opcode has a base cost and some costs are dynamic on a per word (256 bit) basis based on computational complexity. The EVM is Turing complete meaning it is able to compute almost anything given enough resources. For further information on interpreting EVM opcode values and instructions see here.

What is a smart contract, technically?
As you may recall from our previous article - at a primitive level a smart contract is simply a transaction emitted to the blockchain without a specified recipient. The null in the “to” field will get filled with a blockchain contract address once the transaction has been confirmed and can be referenced for future interactions. A contract address is similar to an Ethereum wallet address and is computed internally by the EVM through RLP (Recursive Length Prefix) encoding and Keccak-256 - hashing the address of its sender and how many transactions the sender has sent (a nonce). The EVM uses the opcode CREATE to generate this. As a side note, an Ethereum address is a 42-character hexadecimal address derived from the last 20 bytes of the paired account public key with 0x appended (which indicates it is a hexadecimal value). Externally Owned Addresses (EOAs) have corresponding private keys to their public keys whereas contract accounts are controlled by their hosted code in addition to cryptographic signatures.

https://medium.com/swlh/getting-deep-into-evm-how-ethereum-works-backstage-ab6ad9c0d0bf

How does the EVM execute a smart contract?
Ethereum smart contract functions are written in Solidity, Vyper, or another Ethereum-compatible programming language. In EVM execution high-level code is compiled into Yul - a lower level programming language - which is then optimised and turned into Assembly - then converted into opcodes with the bytecode split into bytes and stored in a binary format. When smart contracts are compiled creation bytecode, runtime bytecode, and contract ABI are generated.

Creation bytecode is one-time executable constructor logic and functions added as input data during deployment such as writing initial variables to storage and is responsible for returning immutable runtime bytecode.

Runtime bytecode is copied to persistent on-chain storage using the CODECOPY opcode and will run each time a smart contract is triggered by an external call or contract message call.

Contract ABI (Application Binary Interface) consists of human-readable codes that define a scheme for interacting with the binary contract by encoding and decoding native bytecode execution results. For Solidity contract ABI technical specifications see this.

Ethereum executes normal transactions by noting the recipient of the transaction receiving the specified ether value with the rest that was sent deposited toward block rewards. In the case of smart contract transactions the EVM will interpret the associated contract code. Smart contracts can only be triggered to execute its logic by an EOA-initiated transaction directed at it, or other smart contracts through contract calls (in response to an original EOA transaction). Whilst operating, the EVM uses memory which is stored temporarily at the contract address and discarded once execution ends. This memory is in the form of an array of 2^256 slot spaces (slots) each with 32 byte words and acts as a read/write database with the first four 32-byte slots reserved for scratch space, a free memory pointer, and a zero slot. Information can be written to contract storage (the storage trie) which supports word arrays, is costly, and stored indefinitely as part of Ethereum’s system state. The EVM code itself is stored in virtual Read-Only Memory and initialised to main memory at zero’ed settings whenever invoked.

With all this contract and balance information - where does Ethereum data live generally?
Each block references in its header the modified Merkle Patricia (Practical algorithm to retrieve information coded in alphanumeric) Tries stored as 256-bit hashes.

stateRoot: the EVM world state trie is permanent data and includes information such as the key and value pair for every Ethereum account. The key is a 160-bit Ethereum account address and the value is the RLP encoding of the nonce, balance, storageRoot, and codeHash of the account (storageRoot and codeHash are only applicable to smart contracts). This represents the entire state of the blockchain at a snapshot in time. storageRoot is the storage trie where contract data / code / runtime bytecode lives. Each Ethereum account has its own storage trie which is stored in the global state trie.

transactionRoot: the transaction trie is where confirmed transactions are recorded. Each Ethereum block has its own transaction trie.

receiptsRoot: Ethereum transactions generate receipts which record the outcome of a successful transaction such as the state of the transaction, cumulative gas used, and the set of logs created during execution.

Only the root node hashes of the transaction trie, state trie, and receipts trie are stored directly in the blockchain. For more information regarding Ethereum’s modified Merkle Patricia Trie architecture see here. For the technical specifications of a block check this out.

https://derao.medium.com/ethereum-under-the-hood-part-7-blocks-c8a5f57cc356

It seems that smart contracts are isolated since the EVM is a contained runtime environment. So how does Ethereum work with off-chain data?
Back to our example, Alice’s smart contract is relatively complex and includes the help of oracles to capture data for the contract’s multiple completion conditions. Oracles may be considered a type of middleware containing components that can query for off-chain information. These components periodically provide updates to the smart contract's data through call message transactions which are associated as separate transactions (or interactions) with the contract and incur fees. Oracles help retrieve real world information via an immediate-read, publish-subscribe, or request-response method. For further information about oracles in general - see here.

Alice has selected Chainlink as her oracle service. Chainlink is a decentralised network of independent node operators and pertinent to our example - with NFT floor price feeds powered by Coinbase Cloud. Node operators are incentivised through ERC677 LINK token-rewards and its own consensus mechanism. A separate Chainlink client smart contract is deployed for which Chainlink provides a unique Job ID for each client smart contract and assigns a pre-determined node to fulfil the request. The Chainlink Oracle smart contract communicates with its network by publishing EVM events broadcasting client requests - or jobs. A request-event-response mechanism is used by nodes to listen for broadcasted events requesting off-chain data which the node sends back to the smart contract via a contract call.

Alice’s custom client contract logic indicates that as long as the strike price has not yet been hit her contract would stay alive. Chainlink network keepers use checkUpkeep during each Ethereum block to determine the passage of time since the last increment and if a job needs servicing. When checkUpkeep returns true the Chainlink Automation Network calls performUpkeep to perform its job. This cycle repeats until the Upkeep is cancelled or runs out of funding. In order to ensure that her contract maintains sufficient funds Alice has deposited a significant amount (Chainlink recommends 3-5x the minimum balance and requires an additional 150k for gas). The client contract is responsible for providing funds to cover gas costs incurred by the Oracle contract in returning the response via the callback function specified in the request. For more information regarding Chainlink Upkeep refer to the Chainlink automation guide here and specifically for costs here.

Hm. What happens if a smart contract runs out of gas?
If at any point the gas supply is reduced to zero an "Out of Gas" (OOG) exception will occur and execution halts. The transaction is included in the block but the only changes applied to the EVM will be the increment to the sender’s nonce and depletion of ether balance sent to block rewards. (Just for fun, read about EIP-150’s esoteric rule that for network security purposes at least 1/64th of the sender’s remaining gas will be saved).

OK. What happens to Alice and Hannah and their NFT?
For Alice and Hannah, it may take some time before their smart contract is completely executed whilst in the world of Ethereum transactions and blocks continue to get built and confirmed and their contract’s Chainlink keepers are at work.

At the Ethereum block height of an arbitrary number :) Alice and Hannah’s target Bored Ape NFT drops to the strike price of 85 ETH on OpenSea. With diligence and luck Alice has maintained her funds well covering the Ethereum smart contract and oracle network fees and her 85 ETH has been kept safely in Ethereum escrow. Her keeper feeds this information back to the EVM triggering Alice’s smart contract logic which purchases the NFT. Alice and Hannah are now up one Bored Ape and down 85 ETH in addition to all fees.

Remember that Ethereum is a live project that is continually undergoing organised upgrades and reviewing community proposals. For an overview of Ethereum’s progress, start here. To get involved, check this out. For more resources on the Ethereum blockchain check out the end of my first article on Ethereum here. Check out GETH client’s EVM code here. For more information on Solidity compilers check this out. And in case you require a decompiler here’s one.
