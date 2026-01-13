# P03 — High L1 Costs for Private Verification and Data Availability

## 2.1 Problem

Even when privacy systems use advanced cryptography (e.g., zk-proofs), they often still require expensive L1 verification and/or data availability publication. On Ethereum, proof verification, calldata, and on-chain commitments can impose high gas costs. These costs constrain throughput, raise user fees, and make privacy-preserving applications less accessible.

## 2.2 Why it matters

* **Cost floors for private transactions.** If private transfers cost significantly more than public ones, users will avoid them.
* **Limits DeFi composability.** Privacy systems that rely on L1 for verification or DA inherit L1 congestion and volatility.
* **Centralization pressure.** High costs push systems toward off-chain shortcuts (DA committees, centralized operators) that weaken trust assumptions.

## 2.3 Who/what it affects

* **End users** paying fees for private interactions.
* **Privacy protocol builders** deploying pools, rollups, or middleware.
* **L2s** that rely on Ethereum for verification and DA.

## 2.4 System / pattern context

* Applies to any privacy system that uses Ethereum L1 for:

  * verifying zk-proofs or fraud proofs
  * publishing transaction data or commitments for DA
* Especially relevant for private rollups and L1 privacy pools.

## 2.5 Failure modes / complications

* **High fixed verification costs.** Proof verification can be expensive even with precompiles.
* **Calldata bloat.** Private systems may need to publish more data (commitments, nullifiers, encrypted payloads).
* **Proving overhead.** Proof generation itself may constrain batching and raise operational costs.
* **Fee volatility.** L1 congestion spikes can make private systems unusable at peak times.

## 2.6 Current attempts / partial solutions (neutral)

* Calldata compression and off-chain DA layers.
* Proof aggregation and recursion to amortize verification.
* Specialized precompiles and gas repricing for cryptographic operations.
* Blob-style data availability improvements.

## 2.7 Evidence & uncertainty

### Sprint 2 key claims (ClaimID → evidence map)

| ClaimID | Claim (verbatim)                                                                                                                                                                                                               | Uncertainty / notes                                                                                                            |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| P03-C1  | EIP-196 and EIP-197 introduced alt_bn128 elliptic-curve precompiles specifically to enable zkSNARK verification within Ethereum's block gas limits.                                                                            | Establishes that "verification was too expensive" without precompiles; does not quantify current end-to-end application costs. |
| P03-C2  | EIP-1108 explicitly argues that the elliptic-curve precompiles were "overpriced" and that repricing would assist privacy and scaling solutions, indicating cryptographic verification costs are material on L1.                | Gas repricing reflects client-performance estimates and governance choices; "material" cost is application-dependent.          |
| P03-C3  | Ethereum calldata has significant per-byte costs; EIP-2028 reduced non-zero calldata cost from 68 gas/byte to 16 gas/byte, underscoring that on-chain DA publication is expensive enough to motivate protocol-level repricing. | Costs continue to evolve with upgrades; "expensive" is relative to throughput targets and application compression efficiency.  |
| P03-C4  | EIP-4844 introduces blob-carrying transactions as a stop-gap to scale Ethereum data availability for rollups, motivated by rollup fees remaining too expensive for many users.                                                 | EIP motivation is clear; fee impacts depend on rollup usage and blob market conditions.                                        |
| P03-C5  | EIP-4844 sets explicit throughput targets/limits for blob data per block (target ~0.375 MB per block; limit ~0.75 MB), demonstrating that DA bandwidth is treated as scarce even in the "stop-gap" design.                     | These parameters are protocol choices; future upgrades may change capacity materially.                                         |
| P03-C6  | Ethereum's roadmap frames scaling data availability (e.g., sharding / danksharding) as necessary for rollup scaling, implying DA constraints are a primary limiter for L2 cost/throughput.                                     | Roadmap documents can be aspirational; specific timelines and realized capacity can differ.                                    |
| P03-C7  | High L1 verification and DA costs create a fee/throughput floor for privacy-preserving applications that need on-chain verification and/or on-chain data publication.                                                          | This is an inference from protocol cost structures; magnitude varies with compression, batching, and upgrade regime.           |

### Key references

* Phase A problem file: `Private Transfers/03_Problems/03 High L1 Costs for Private Verification and Data Availability.md`
* Appendix C pointer: `Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
* Related Phase A report sections: `Private Transfers/05_Reports/DeFi Privacy Report.md` (cost constraints)

### Evidence gaps

* Updated cost breakdowns for private rollup transactions post-blob regime (verification vs DA vs overhead).
* Comparative costs across proof systems and batch sizes for privacy workloads.

### Open questions

* How much do blob-style DA improvements reduce the cost floor for privacy rollups versus public rollups?
* What is the practical lower bound on private transaction fees if L1 verification remains required?

