# P06 — Trust-Heavy DA Committees and Operators

## 2.1 Problem

Many privacy-preserving scalability approaches rely on trusted data availability (DA) committees or centralized operators. Instead of publishing all transaction data on L1, validiums and similar designs outsource DA to a small set of parties. Even when proofs ensure correctness, these trusted actors can censor, withhold data, or become coercion points. This weakens trust assumptions and can undermine both security and privacy.

## 2.2 Why it matters

* **DA is a security dependency.** Without data, users can't verify or exit.
* **Centralization and coercion risk.** Small committees/operators are easier to pressure, bribe, or compromise.
* **Privacy risk.** Operators and DA providers may observe metadata (who transacts, when, and possibly with what patterns).

## 2.3 Who/what it affects

* **Users** whose funds and privacy depend on operator/committee behavior.
* **Rollup/validium builders** who must choose DA trade-offs.
* **Ecosystem** trust in "trust-minimized" privacy systems.

## 2.4 System / pattern context

* Validiums, volitions, and other off-chain DA patterns.
* Private rollups with centralized sequencers/operators.
* Any architecture where DA or ordering is outsourced.

## 2.5 Failure modes / complications

* **Data withholding.** DA committee can freeze funds by refusing to provide state data.
* **Censorship.** Operators can selectively include/exclude users.
* **Bribery/coercion.** Small committees can be targeted.
* **Opaque failures.** Users may not detect withholding until exit time.
* **Governance capture.** Committee membership may be politically or economically captured.

## 2.6 Current attempts / partial solutions (neutral)

* Larger committees, threshold signatures, and rotating membership.
* DA sampling and sharding-based approaches.
* Escape hatches, forced inclusion, and fallback publication mechanisms.

## 2.7 Evidence & uncertainty

### Sprint 2 key claims (ClaimID → evidence map)

| ClaimID | Claim (verbatim)                                                                                                                                                                               | Uncertainty / notes                                                                                                                                                 |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| P06-C1  | Validium moves transaction data off-chain and relies on data availability managers to store/provide the data needed for verification and withdrawals.                                          | This is the defining trade-off of validium; exact roles and implementation details vary.                                                                            |
| P06-C2  | Even with validity proofs, if DA managers withhold transaction/state data, users may be unable to compute Merkle proofs to withdraw and funds can be frozen.                                   | Some systems may add fallbacks, but the DA trust assumption remains a core risk.                                                                                    |
| P06-C3  | StarkEx documentation describes a committee-service-based approach to data availability, indicating real-world reliance on committee infrastructure in validium-like deployments.              | Documentation is implementation-specific; other validiums may implement DA differently.                                                                             |
| P06-C4  | ZK and optimistic rollup patterns are described as off-chain execution systems anchored to L1, and (in practice) often depend on operator/sequencer infrastructure for ordering and inclusion. | The "centralized sequencer common in practice" aspect is not uniformly specified in these docs; degree of centralization varies by rollup and can change over time. |
| P06-C5  | DA committees and operators concentrate power into small sets of actors, creating bribery/coercion/censorship surfaces compared to on-chain DA.                                                | Largely inferential from the committee model; empirical measurement of coercion/bribery incidence is limited.                                                       |
| P06-C6  | Validium is explicitly positioned as improving scalability by reducing on-chain data publication, but at the cost of stronger trust assumptions about DA providers.                            | Magnitude of scalability benefits varies; some trade-offs depend on application payload size and DA market conditions.                                              |
| P06-C7  | DA assumptions directly interact with exit safety: when data is off-chain (validium) or exit games are required (plasma), user safety depends on data access and timely challenges.            | Plasma has many variants; exit/monitoring burden differs across implementations.                                                                                    |

### Key references

* Phase A problem file: `Private Transfers/03_Problems/06 Trust-Heavy DA Committees and Operators.md`
* Appendix C pointer: `Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
* Related Phase A report sections: `Private Transfers/05_Reports/DeFi Privacy Report.md` (DA trust and operator risks)

### Evidence gaps

* Quantitative risk assessment: probability and impact of DA committee failure, coercion, or collusion.
* Empirical studies linking operator metadata visibility to privacy leakage (beyond general transaction-graph leakage).

### Open questions

* What minimum DA decentralization is needed for DeFi-grade safety in privacy systems?
* Can DA committee trust be reduced without reintroducing L1 cost floors that kill usability?

