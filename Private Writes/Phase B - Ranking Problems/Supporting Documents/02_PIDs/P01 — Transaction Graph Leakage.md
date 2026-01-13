

## 2.1 Problem

Privacy on L1 and L2 is not just a cryptographic problem: even with perfect hiding of transaction contents, a system can leak information through transaction graphs, timing correlations, workflow motifs, fee payment patterns, relayer behavior, and cross-domain bridges. In DeFi, these "side-channel" observables can often be enough to infer user identities, strategies, or asset movements.

## 2.2 Why it matters

* **DeFi workloads are pattern-rich.** Liquidations, arbitrage, routing, vault rebalancing, and multi-step trades create recognizable motifs.
* **Leakage compounds with composability.** A "private" action often touches public liquidity pools, public bridges, and public governance, creating linkage points.
* **User trust and adoption.** If privacy tools are perceived as leaky, users either avoid them or misuse them in ways that further reduce anonymity sets.

## 2.3 Who/what it affects

* **End users** seeking private transfers or private DeFi interactions.
* **Protocols** trying to offer privacy-preserving UX in composable environments.
* **Builders** of privacy pools, private rollups, and account abstraction relayers.

## 2.4 System / pattern context

* Applies across L1 privacy pools, private rollups, and privacy middleware.
* Especially acute in DeFi environments where workflows are multi-step and publicly observable.

## 2.5 Failure modes / complications

* **Timing/amount correlation at boundaries.** Deposits/withdrawals and bridging events create obvious link points.
* **Motif clustering.** Repeated execution of similar multi-step workflows can be fingerprinted.
* **Relayer and fee payment leakage.** Paying gas in public assets or using a small set of relayers creates correlation hubs.
* **Cross-domain linkage.** Bridges and cross-chain relays create observable synchronization points.

## 2.6 Current attempts / partial solutions (neutral)

* Larger anonymity sets, delayed execution, batching, decoy activity.
* Relayer networks, paymasters, and private RPC.
* "Intent"-based designs that abstract away some user workflows.

## 2.7 Evidence & uncertainty

### Sprint 2 key claims (ClaimID → evidence map)

| ClaimID | Claim (verbatim)                                                                                                                                                                                      | Uncertainty / notes                                                                                                                                                  |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| P01-C1  | On transparent blockchains, transaction-graph analysis and heuristics can cluster addresses and infer likely common control/entities, undermining pseudonymity.                                       | Clustering accuracy depends on chain, heuristics, and availability of ground truth; results can be directionally strong without being universally precise.           |
| P01-C2  | Empirical studies of Zcash found that simple heuristics can link a substantial fraction of shielded activity, reducing practical anonymity relative to the nominal shielded pool.                     | Study-period and protocol-usage dependent; may not generalize to current Zcash usage or to other shielded designs.                                                   |
| P01-C3  | In mixer systems, user behavior (e.g., address reuse, transactional linkage) can re-connect deposits to withdrawals for a non-trivial subset of transactions.                                         | The arXiv source is withdrawn; treat quantitative linkage rates as provisional pending a corrected version and independent replication.                              |
| P01-C4  | Timing-based matching between deposits and withdrawals can further increase linkage beyond address-based heuristics in mixers.                                                                        | Withdrawn preprint; timing linkage depends on user delay distributions, adversary capabilities, and protocol-specific batching/relaying behavior.                    |
| P01-C5  | Mixers/privacy tools are often organized as separate pools/denominations/instances, and privacy depends on the size/composition of the relevant pool's activity; low activity makes inference easier. | Evidence is strongest for Tornado Cash-style denomination pools; generalization depends on pool design and user behavior.                                            |
| P01-C6  | Similar leakage mechanisms (workflow motifs, bridge events) can apply across L1 pools, L2s, and cross-chain contexts because they are driven by observable boundary events and user workflows.        | This is supported conceptually and via observed ecosystem behavior; there is limited standardized benchmarking for DeFi-specific motif leakage across architectures. |

### Key references

* Phase A problem file: `Private Transfers/03_Problems/01 Transaction Graph Leakage.md`
* Appendix C pointer: `Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
* Related Phase A report sections: `Private Transfers/05_Reports/DeFi Privacy Report.md` (side-channel leakage)

### Evidence gaps

* Quantitative mapping from DeFi workflow motifs → deanonymization risk.
* Benchmarks comparing leakage across privacy architectures (L1 pools vs private rollups vs middleware).

### Open questions

* What observables dominate in real-world deanonymization (timing, motif structure, fee patterns, relayer behavior)?
* How much decoy activity or batching is needed to meaningfully reduce motif leakage without destroying UX?

