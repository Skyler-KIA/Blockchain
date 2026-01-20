# Introduction

This section focuses on a shared starting point: the original challenge was not merely “creating digital money,” but resolving the paradox of synchronization and double spending in open networks without centralized authority. The historical context of b-money and Bitcoin shows that the problem can be broken down into three layers:

## I. The Three-Layer Structure of the Problem

1. Core technical challenge: network synchronization  
In distributed networks, nodes may receive transactions in different orders, making it impossible to agree on “which transaction happened first.” b-money’s Protocol 1 relies on a “synchronous and unjammable broadcast channel,” a premise that the real Internet cannot satisfy, so ledger ordering and state consistency cannot be reliably established.

2. Core financial challenge: double spending  
Digital currency is copyable. Without a unified transaction order and ledger consensus, recipients cannot confirm whether the same funds have been spent elsewhere. Traditional approaches rely on mints or banks to keep a global ledger, introducing trust costs and single points of failure. A decentralized solution must enable the entire network to agree on a single transaction order to eliminate double spending.

3. Core coordination challenge: the Byzantine Generals Problem  
In networks with potentially malicious nodes, how can honest nodes agree on the ledger state? b-money’s Protocol 2 lets a subset of “servers” maintain the ledger and post deposits to constrain misbehavior, but it still faces consensus divergence and centralization risks.

## II. Bitcoin’s Practical Resolution

Bitcoin’s core goal is to achieve “peer-to-peer electronic cash” and “double-spend prevention” without trusted third parties. The whitepaper proposes a distributed timestamp server built from a peer-to-peer network and a longest-chain history validated by proof of work, establishing a consistent transaction order in open networks.[bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)

Bitcoin fills three key gaps in b-money:
1. Consistent ordering in asynchronous networks  
Transactions propagate on a best-effort basis, nodes package them into blocks, and PoW competition determines the accepted order, forming a unified view of transaction sequence in an asynchronous network.[bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)
2. Publicly verifiable history  
Chained timestamps and the longest-chain rule build a public, auditable transaction history. Recipients can rely on the network-accepted order to rule out double spending, replacing centralized bookkeeping with majority hash-power consensus.[bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)
3. Majority decision under cost constraints  
System security depends on the verifiable assumption that the majority of hash power is honest; rewriting history would require sustained dominance over network hash power, making attacks economically unsustainable.[bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)

## III. New Costs Introduced by Practicality

From the idealized goals of b-money (value anchored to computation costs, universal consensus, built-in contract arbitration), Bitcoin solved synchronization and double spending but introduced new structural issues:

1. Energy consumption and environmental externalities  
PoW serves as the foundation for ordering and Sybil resistance, driving a hash-power arms race and higher energy use. The U.S. EIA, citing CBECI estimates, indicates the 2024 median annualized electricity use of the Bitcoin network is around 170 TWh, with a wide uncertainty range.[eia.gov](https://www.eia.gov/todayinenergy/detail.php?id=61364)

2. Hash-power concentration and “decentralization” drift  
Economies of scale and ASIC advantages push hash power toward large mining pools. Data shows a small set of pools such as Foundry USA and AntPool hold significant shares over extended periods, sustaining pool-level centralization risk.[hashrateindex.com](https://hashrateindex.com/hashrate/pools)

3. Abandoning cost-anchored value and high volatility  
b-money sought stability by anchoring value to computation cost, while Bitcoin adopts a fixed supply cap and halving issuance, compressing supply elasticity and making price more sensitive to demand swings.[controlled_supply](https://en.bitcoin.it/wiki/Controlled_supply) [ishares](https://www.ishares.com/us/insights/what-is-the-bitcoin-halving)

4. Limited programmability and contract capability  
To keep verification costs bounded, Bitcoin Script is intentionally non-Turing-complete and disallows loops, limiting on-chain expressiveness relative to b-money’s envisioned arbitration and contract execution.[Script](https://en.bitcoin.it/wiki/Script)

5. The privacy paradox: transparent, traceable ledger  
Bitcoin’s public broadcast and global validation prevent double spending but make history fully auditable. Many sources describe Bitcoin as pseudonymous rather than anonymous; once addresses are linked to real identities, transaction histories become traceable.[river](https://river.com/learn/bitcoin-privacy-and-anonymity/)

## IV. The Subsequent Roadmap

These trade-offs shaped divergent blockchain paths. Consensus innovation, scaling, architectural shifts, and privacy enhancement are responses to the efficiency, privacy, and functionality costs introduced by Bitcoin’s solution to b-money’s synchronization and double-spend problems.

### 1. Consensus innovation: lower energy and faster finality
The main direction shifts from hash-power competition to stake and voting.
<details>
<summary>Representative paths and examples</summary>

- PoS: stake replaces hash-power competition, cutting energy use and improving finality (Ethereum The Merge).[ethereum.org](https://ethereum.org/roadmap/merge/)  
- DPoS: delegate voting with a small set of block producers for efficiency (EOSIO).[EOSIO Technical White Paper](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md)  
- BFT variants: voting-based confirmation for fast finality (Tendermint/CometBFT in the Cosmos ecosystem).[tendermint.pdf](https://tendermint.com/static/docs/tendermint.pdf)  
- DAG BFT: parallel proposals, low-latency consensus (Sui Mysticeti).[Sui Consensus](https://docs.sui.io/concepts/sui-architecture/consensus)  
- PoH+PoS/BFT: PoH as a time source, Tower BFT voting for consensus (Solana).[Tower BFT](https://docs.solanalabs.com/implemented-proposals/tower-bft)
</details>

### 2. Scaling mainline: Layer 2 rollups
<details>
<summary>Path and mechanism</summary>

Rollups move execution off-chain while posting data back to the main chain, using L1 security as the settlement base. Optimistic rollups assume validity by default and correct via fraud proofs; ZK-rollups use validity proofs to verify correctness at submission time.[ethereum.org](https://ethereum.org/developers/docs/scaling/optimistic-rollups/)
</details>

### 3. Data availability and sharding evolution: Danksharding / EIP-4844
<details>
<summary>Route and goal</summary>

Ethereum shifts to a rollup-centric roadmap. Proto-Danksharding (EIP-4844) introduces blob data so rollups can publish data more cheaply, and the data is pruned after a fixed period, reducing long-term storage burdens. The route targets scaling toward >100,000 TPS.[ethereum.org](https://ethereum.org/roadmap/danksharding/) [ethereum.org](https://ethereum.org/developers/docs/scaling/)
</details>

### 4. Architectural paradigm shift: monolith to modular
<details>
<summary>Key decomposition</summary>

Modular blockchains separate consensus, execution, and data availability into distinct layers, forming a division of labor across DA layers, execution layers, and shared security to reduce main-chain bloat and improve composability.
</details>

### 5. Interoperability and privacy enhancement
<details>
<summary>Goals and approaches</summary>

Cross-chain protocols and privacy techniques reclaim b-money’s goal of “anonymous cooperation”: cross-chain improves asset mobility, while zero-knowledge proofs and ring signatures strengthen privacy protection and compliance capabilities.
</details>
