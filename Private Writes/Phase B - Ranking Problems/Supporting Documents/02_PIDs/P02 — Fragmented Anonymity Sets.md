# P02 — Fragmented Anonymity Sets

## 2.1 Problem

Anonymity sets in privacy systems (mixers, shielded pools, private rollups) are often fragmented across assets, protocols, chains, and user segments. Instead of one large anonymity set, users interact in many small pools, each with limited participation. This reduces effective privacy and can create "two-tier" outcomes where only the largest pools provide meaningful cover traffic.

## 2.2 Why it matters

* **DeFi requires specific assets and interactions.** Users can't always choose the highest-volume privacy pool if it doesn't support the asset or protocol they need.
* **Fragmentation weakens privacy guarantees.** Small anonymity sets make timing, amount, and motif inference easier.
* **Adoption feedback loops.** If privacy is weak in small pools, users avoid them, making them even smaller.

## 2.3 Who/what it affects

* **End users** who need privacy in specific assets or DeFi contexts.
* **Protocol designers** who must choose between many small pools or fewer larger ones.
* **Ecosystem builders** trying to create interoperable privacy layers across chains and apps.

## 2.4 System / pattern context

* Common across L1 privacy pools, private rollups, app-specific privacy systems, and cross-chain privacy tools.
* Especially relevant when privacy is optional rather than default (users self-select into pools).

## 2.5 Failure modes / complications

* **Long-tail pools.** Many pools exist, but most have low volume and weak privacy.
* **Asset fragmentation.** Each token, denomination, or pair can create a separate anonymity set.
* **Cross-chain splits.** Deployments on multiple chains divide users further.
* **Repeated workflows.** Users who repeat the same actions across pools may leak linkage.
* **Market-induced segmentation.** Fees, liquidity, and UX differences push different user types into different pools.

## 2.6 Current attempts / partial solutions (neutral)

* Unified pools or shared anonymity sets across assets.
* Cross-asset mixing or aggregation layers.
* Incentives to concentrate liquidity and activity in fewer pools.

## 2.7 Evidence & uncertainty

### Sprint 2 key claims (ClaimID → evidence map)

| ClaimID | Claim (verbatim)                                                                                                                                                                                            | Uncertainty / notes                                                                                                                  |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| P02-C1  | Anonymity can be quantified with information-theoretic metrics (e.g., entropy of the sender distribution), and effective anonymity decreases as probability mass concentrates on a smaller subset of users. | Metric choice matters (entropy vs k-anonymity vs other); mapping to real adversaries can be non-trivial.                             |
| P02-C2  | In Zcash, empirical analysis found that heuristics and user behavior can materially reduce practical anonymity, so nominal pool size can overstate effective anonymity.                                     | Period-dependent; does not imply inevitability for all shielded designs.                                                             |
| P02-C3  | Mixer anonymity sets are instance/pool specific (e.g., by denomination), so splitting activity across many pools reduces anonymity available to any single user.                                            | Most directly supported for Tornado Cash denomination pools; other systems may pool differently.                                     |
| P02-C4  | Shocks that reduce deposit flow can shrink anonymity sets and reduce privacy for remaining users (Tornado Cash sanctions as a case study).                                                                  | Causal pathways can mix "volume drop" with "user-type selection"; generalization to other shocks/pools is uncertain.                 |
| P02-C5  | A cross-chain Tornado Cash study reported comparable leakage across multiple chains, suggesting fragmentation across chains does not eliminate behavior-driven linkage risks.                               | Source is withdrawn by authors (reference issues); treat cross-chain quantitative results as provisional until corrected/replicated. |
| P02-C6  | DeFi liquidity and activity can be fragmented across pools (e.g., fee-tier pools), which can segment users and activity flows that privacy layers might otherwise rely on for cover.                        | This supports "fragmentation exists"; direct mapping from liquidity fragmentation → anonymity fragmentation remains under-studied.   |
| P02-C7  | Fragmentation can create "two-tier" anonymity outcomes: high-volume pools yield meaningfully better cover than the long tail of low-volume pools.                                                           | Evidence is strongest for mixers/denomination pools; more empirical work needed on private rollups and app-specific privacy pools.   |

### Key references

* Phase A problem file: `Private Transfers/03_Problems/02 Fragmented Anonymity Sets.md`
* Appendix C pointer: `Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
* Related Phase A report sections: `Private Transfers/05_Reports/DeFi Privacy Report.md` (anonymity fragmentation)

### Evidence gaps

* Empirical measurement of anonymity set fragmentation across DeFi use cases and chains.
* Cross-protocol comparability of "effective anonymity set" metrics (entropy, k-anonymity, etc.) in deployed systems.

### Open questions

* What interventions most effectively concentrate activity without harming usability or decentralization?
* How should privacy systems handle "rare asset" cases where fragmentation is unavoidable?

