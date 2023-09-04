# 👩🏼‍💻 A New Developer’s Bullet-Point Guide to Blockchains and Cryptocurrencies (Part 2.1/4) // Ethereum

This guide is written in 4 parts (with in between bonus parts that emerged out of interest, importance, and perceived helpfulness in understanding these fundamentals).
The bare minimum basics (what is blockchain)
Transaction examples (show me the money — tech version) // Bitcoin
2.1. Transaction examples… // Ethereum
2.1.1 Transaction examples… // Ethereum // EVM
More quick blockchain concepts
A comparison chart (cheatsheet of 5 top blockchains)

This is the third or technically Part 2.1 out of what was originally a four-part series.

If you’ve read the first two parts, you should now have a strong grasp of blockchain first principles and how the Bitcoin blockchain processes a typical transaction.

Moving on let’s take a look at how things work on the Ethereum blockchain by tracing a transaction or interaction end-to-end. This will show how the protocol functions, help form a concept of what types of interactions Ethereum can handle, and touch on a few social governance components that interplay across the network.

As always you are encouraged to participate in the network itself to gain first-hand knowledge and experience of how things work - all while securing the network.

Part 2.1 - Transaction examples (show me the money - tech version) // Ethereum

Ethereum is the second largest blockchain network by market capitalisation (price per unit multiplied by total amount in circulation). It is known as the programmable blockchain because of its ability to process participant-written codes.

The EVM (Ethereum Virtual Machine) is able to process smart contracts, which are pieces of code on the blockchain that are programmed to execute transactions and interactions thereof based on pre-defined variables and conditions. In Part 2.51 - The EVM we will explore how the EVM loops through. First up though we look at how Ethereum’s execution layer processes these transactions and secures its network.

Below is an Ethereum smart contract in action - a technical example.

Ethereum (ETH)

Alice is writing a multi-sig (i.e. multi-signature, requiring more than one signature) smart contract for her friend Hannah and herself. Her smart contract requirements stipulate that when she and Hannah both agree to buy Bored Ape Yacht Club NFT #10000 at 85 ETH their wallet will buy the specified asset from the OpenSea marketplace at this strike price. Using Hardhat - an Ethereum IDE (Integrated Development Environment) - Alice programs a smart contract that has this desired preset condition and related instructions. In order to incentivise that her transactions are prioritised for inclusion in the blockchain Alice has also set a tip or priority fee to be sent to the validator (more on this below).

At a primitive level smart contracts are transactions emitted from a blockchain address without a specified recipient. The null in the “to” field will get filled with a blockchain contract address once the transaction has been confirmed and can be referenced for future interactions. Smart contracts are passive, without the ability to automatically execute, so require the help of bots either/both on- and off-chain to access information as necessary. In this instance Alice is using Chainlink - a well-known decentralised oracle (i.e. data feed) network.

Alice tests out her contract and has built a graphical interface to give external users a user-friendly way to interact with it. Satisfied with her contract’s functionality and security Alice deploys it onto Ethereum Mainnet (the execution layer) via Vercel which has hosting services (otherwise she could also deploy separately and host her own website). She now votes yes through the site and signs this transaction after connecting to the multi-sig wallet. Hannah visits the site and agrees to the proposal - voting yes and signing the transaction in favour of the purchase at the agreed-upon strike price.

Local nodes pick up the smart contract transaction and following interactions broadcasting them to the wider network. These transactions are continuously transmitted until they are included in a proposed block. Alice’s smart contract is picked up by MEV (Maximal Extractable Value - previously known as Miner-Extractable Value) searcher Alex. Alice’s transaction is added to the middle of Alex’s pool of unconfirmed transactions (a memory pool - or mempool, also called transaction pool or queue) where it is validated whilst waiting to be included in a pending block. This node’s pool will continuously seek to synchronise itself with the rest of the live nodes on the network. Validations at this stage include funds availability for completing the transaction, nonce value for correct transaction ordering, gas price analysis, signatures, etc. Alex’s block building configuration optimises transaction inclusions based on validator tips offered and the DeFi (Decentralised Finance) arbitrage opportunities Alex is seeking to play out and profit from. Alice has sent a sizeable tip for her transactions so they have been accordingly prioritised. Typical reasons transactions at this point may be dropped are a speedup or cancel or if they do not meet / fulfil a particular node’s selection criteria.

https://www.quicknode.com/guides/ethereum-development/transactions/how-to-access-ethereum-mempool/

The Ethereum network uses Proof of Stake (PoS) with optional proposer-builder separation as its consensus mechanism. The network uses transaction fees denominated natively in Ether (ETH) to run and builds variable-sized blocks targeting 15m gas per block (maxing out at 2x the target so 30m gas). Block base fees fluctuate according to the prior block and are adjusted proportionally (increasing at a max of 12.5%) to incentivise equilibrium of the target gas per block. Searcher nodes perform verifications and submit bids for these exec blocks to be proposed by validators. Transaction fees or base (gas) fees on Ethereum are burned and searchers earn revenue through MEV which results from block building tactics based on the ordering of transactions within a single block and related DeFi arbitrage opportunities particular to individual searchers. (MEV is a special topic that will be covered in a separate article). Searchers pay a proposing fee (a percentage of their revenue) in a sealed-price bid to the proposing validator that will select the highest bid - the most profitable execution payload.

In addition to block-building themselves or receiving direct bids from searchers, proposers also have the option to query a block marketplace supplied by private relayers. Relayers are trusted aggregators of submitted blocks and verify block validity (including fees, attributes, and gas) sharing the most profitable block header with the validator. Validators may connect to multiple relayers. In this case where the searcher and proposer are two separate entities, in order to prevent the proposer from capturing MEV, the chosen proposer cannot see block content but rather only the execution payload header which they will need to sign using their public key. Once signed the header is transferred to the escrow which ensures data availability and sends the payload to the relayer. For a dashboard on block-building activity check this out. For information regarding validator keys - see here.

Alex’s algorithm builds a block and proposes it through an API (Application Programming Interface) to a popular relay aggregator MEV-Boost. Other private relayers include Eden, Manifold, BloxRoute and BlockNative.

https://ethresear.ch/t/mev-boost-merge-ready-flashbots-architecture/11177

Ethereum’s consensus layer or ETH2.0 (previously known as the Beacon Chain) is split into slots which occur every 12 seconds with every 32 slots called an epoch. Ethereum uses Casper Proof of Stake or “finality gadget” where finality occurs when more than two thirds of validators vote correctly on the chain head during an epoch, at which it becomes justified. If two consecutive epochs are justified finality occurs.

Validators are chosen at pseudorandom using process_randao and validators not proposing are attesting to blocks (there is always 1 proposer and multiple attesters). A minimum of 16,384 validators are required in order to initiate Ethereum. They are incentivised to behave through staking requirements. A minimum of 32 ETH is required (e.g. deposited into a deposit contract) in order to participate as a validator, of which is burned by the network in the circumstance of poor behaviour or performance which may include but is not limited to failure to vote or malicious actions such as proposing multiple blocks in a single slot (equivocating) or submitting contradictory attestations. Validators may also be slashed for poor behaviour and ejected from the network. Penalty severity is correlated to the severity of the offence. Validators are rewarded for their work with the potential to earn up to 2 ETH per block (a rate which decreases over time by about 90% to a minimum of 0.22ETH staking reward per block). Rewards minus penalties are transferred to validator balances every epoch.

ETH2.0 selects Suraj’s validating node as the proposer. Suraj signs the proposal for Alex’s block to take the slot since it earns all participators the highest amount of rewards. It is accepted by the attesters.

In addition to proposing the new block, the responsibilities of the proposer include adding proof that a validator should be slashed and new attestations from attesters. The role of attester validators is to agree with other validators on the correct selection and related checkpoints (the most recent justified block and the first block in the current epoch - known as source and target checkpoints). For details on attestation votes - see here. For technical specifications of the attestations - see here. For more information on the validator voting workflow in detail - see here.

For extended details on validator rewards and punishments, see here and here for explanations and here for core code and complementary commentary. For FAQ on validation go here. For help calculating network validator rewards, use this. For more information on how to participate in securing the network, see here for block building and here for validating. For details on Ethereum Layer 1 attacks and defences - see here.

Next up Part 2.1.1 - the EVM.

Remember that Ethereum is live project that is continually undergoing organised upgrades and reviewing community proposals. The Merge which brought together the execution layer and the consensus layer occurred on September 15 2022. For a roadmap of post-merge upgrades - see here. For technical specifications on the execution layer - here. For specifications on the consensus layer - here. For the original yellowpaper on core Ethereum architecture - here.
