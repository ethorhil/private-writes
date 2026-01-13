# P05 — Lack of User-Resilient Exits

## 2.1 Problem

Many privacy-preserving L2 systems and off-chain architectures lack user-resilient exits. If operators, DA committees, or sequencers fail or censor users, users may not be able to withdraw funds or exit safely without relying on trusted parties. In stress events, the inability to exit quickly can cascade into broader financial risk.

## 2.2 Why it matters

* **Funds safety and trust.** Users need credible guarantees that they can recover funds even if operators fail.
* **Systemic risk in DeFi.** If private L2 users can't exit during volatility, liquidations and insolvency can spread.
* **Regulatory and operational fragility.** Centralized exit dependencies create coercion points.

## 2.3 Who/what it affects

* **Users** holding assets in privacy-preserving rollups or validiums.
* **Protocols** that rely on private L2 infrastructure.
* **Ecosystem** trust in privacy systems as "safe" financial rails.

## 2.4 System / pattern context

* Especially relevant for:

  * Validiums / off-chain DA architectures
  * Plasma-style exit games
  * L2s with centralized sequencers or weak censorship resistance

## 2.5 Failure modes / complications

* **Data withholding.** Without state data, users can't generate exit proofs.
* **Committee failure or collusion.** DA committees can block exits.
* **Mass exit events.** Exits may be too slow or costly under stress.
* **User burden.** Some designs require users to monitor chains or store data to exit safely.

## 2.6 Current attempts / partial solutions (neutral)

* Escape hatches and forced inclusion mechanisms.
* On-chain DA rollups instead of validiums.
* Watchtower services and delegated monitoring.

## 2.7 Evidence & uncertainty

### Sprint 2 key claims (ClaimID → evidence map)

| ClaimID | Claim (verbatim)                                                                                                                                                                                   | Uncertainty / notes                                                                                                     |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| P05-C1  | In validium, transaction data is kept off-chain; if data availability managers withhold data, users cannot compute the Merkle proof needed to withdraw and funds can be frozen.                    | General validium limitation; some deployments may add additional fallback mechanisms, but the trust assumption remains. |
| P05-C2  | Validium explicitly relies on a set of data availability managers (a committee) to provide data and attest availability for batches.                                                               | Committee composition and operational guarantees vary by implementation.                                                |
| P05-C3  | Plasma architectures rely on fraud proofs and exit games anchored to L1, which require the ability to challenge and exit; safety depends on monitoring and access to relevant data.                | Plasma has many variants; user burden and exit complexity vary; mass-exit dynamics are context dependent.               |
| P05-C4  | ZK-rollup withdrawals can execute without a challenge delay once the L1 contract verifies the validity proof.                                                                                      | Exact exit path is rollup-specific; the claim reflects the general property described in documentation.                 |
| P05-C5  | Optimistic rollup withdrawals are subject to a delay to allow challenges (fraud proofs), affecting how quickly users can exit.                                                                     | Delay duration varies by rollup; some systems offer liquidity/fast-exit mechanisms with additional trust assumptions.   |
| P05-C6  | Some validium designs include anti-censorship mechanisms allowing users to submit withdrawals directly without operator cooperation, but withdrawals still require access to off-chain state data. | "Anti-censorship" does not solve data withholding; user-resilient exit still depends on DA assumptions.                 |
| P05-C7  | Designs that require users to monitor chains or store data to exit impose significant operational burden and create failure modes for less sophisticated users.                                    | Operational-burden magnitude is not well quantified; burden can sometimes be offloaded to third parties (adding trust). |

### Key references

* Phase A problem file: `Private Transfers/03_Problems/05 Lack of User-Resilient Exits.md`
* Appendix C pointer: `Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
* Related Phase A report sections: `Private Transfers/05_Reports/DeFi Privacy Report.md` (exit risks)

### Evidence gaps

* Empirical evidence on how quickly users can exit private L2 systems under stress (fees, delays, congestion).
* Comparative analysis of exit guarantees across validium / rollup / plasma patterns.

### Open questions

* What minimum exit guarantees are required for DeFi-grade safety in privacy systems?
* How can "user burden" be reduced without introducing new trusted intermediaries?

