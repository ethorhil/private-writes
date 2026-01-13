# P04 — Limited Throughput for Privacy-Preserving Rollups

## 2.1 Problem

Privacy-preserving rollups (and similar L2 systems) often have limited throughput compared to transparent rollups. They may require expensive proof generation, larger data payloads (commitments, encrypted state), and more complex state transitions. Even when L1 verification is efficient, bottlenecks in proving, batching, data availability, and sequencer operation can cap TPS.

## 2.2 Why it matters

* **DeFi is latency- and throughput-sensitive.** Congestion or slow finality can cause liquidation cascades, slippage, and MEV exposure.
* **Private rollups must compete with public L2s.** If private systems are slower or more expensive, they won't be adopted.
* **Stress events reveal bottlenecks.** When markets are volatile, throughput constraints become systemic risk.

## 2.3 Who/what it affects

* **Users** needing private transfers or private DeFi interactions.
* **Protocol builders** deploying private rollups or app-specific privacy L2s.
* **Ecosystem** if private systems can't scale to meaningful activity levels.

## 2.4 System / pattern context

* Applies to zk-rollups with privacy extensions, private execution environments, and validity-based L2s.
* Interacts with Ethereum DA constraints and L2 operator/sequencer designs.

## 2.5 Failure modes / complications

* **Proof generation bottleneck.** Proving large circuits can cap batch frequency.
* **DA bottleneck.** Private systems may need more on-chain data per state update.
* **Sequencer centralization.** Limited operator capacity or downtime reduces throughput.
* **Composability constraints.** Private state may require additional synchronization steps.
* **Stress events.** High-volume bursts (liquidations/arbitrage) can overwhelm private rollup capacity.

## 2.6 Current attempts / partial solutions (neutral)

* Proof recursion and aggregation.
* Off-chain DA or specialized DA layers.
* Parallel proving, hardware acceleration.
* Hybrid architectures (selective privacy).

## 2.7 Evidence & uncertainty

### Sprint 2 key claims (ClaimID → evidence map)

| ClaimID | Claim (verbatim)                                                                                                                                                                                         | Uncertainty / notes                                                                                                                                     |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| P04-C1  | ZK-rollups execute transactions off-chain and prove correctness via validity proofs posted to Ethereum, so throughput depends on batching strategy and proof generation cadence.                         | The source establishes the architecture; it does not directly quantify private-rollup prover bottlenecks (which are implementation/circuit dependent).  |
| P04-C2  | Optimistic rollups execute transactions off-chain but post transaction data to Ethereum as calldata or blobs, so DA bandwidth/cost is an explicit throughput constraint for L2s.                         | DA constraint magnitude depends on calldata vs blob usage, compression, and per-block limits.                                                           |
| P04-C3  | Calldata costs were high enough to motivate protocol-level changes (EIP-2028) and EIP-4844 explicitly targets scaling data availability for rollups via blob-carrying transactions.                      | Establishes DA as a bottleneck; does not isolate the incremental overhead from "privacy payloads" vs normal rollup data.                                |
| P04-C4  | EIP-4844 parameterizes blob throughput with a target and max blob gas per block, implying rollup throughput remains bounded by DA capacity even under blob transactions.                                 | Future protocol upgrades may raise/lower these limits; throughput is also affected by rollup-internal batching.                                         |
| P04-C5  | Withdrawal UX differs by rollup type: ZK-rollup exits execute once the validity proof is verified, while optimistic rollup exits can be delayed to allow challenges.                                     | Exact delays and mechanisms are rollup-specific; the claim is about the general architecture patterns described in docs.                                |
| P04-C6  | ZK-based privacy systems depend on heavy cryptography; protocol-level gas repricing discussions explicitly cite privacy/scaling systems as beneficiaries, indicating cryptographic overhead is material. | This supports "cryptographic overhead matters" but not a direct private-rollup TPS bound; proving cost is mostly off-chain and implementation-specific. |

### Key references

* Phase A problem file: `Private Transfers/03_Problems/04 Limited Throughput for Privacy-Preserving Rollups.md`
* Appendix C pointer: `Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
* Related Phase A report sections: `Private Transfers/05_Reports/DeFi Privacy Report.md` (rollup constraints)

### Evidence gaps

* Head-to-head throughput benchmarks: public rollups vs privacy-preserving rollups under comparable DA regimes.
* Empirical data on prover bottlenecks for privacy workloads (circuit sizes, recursion strategies, hardware).

### Open questions

* How much throughput is lost to privacy payload overhead relative to "plain" zk-rollups?
* What DA regime (calldata vs blob vs external DA) is required for private rollups to support DeFi stress events?

