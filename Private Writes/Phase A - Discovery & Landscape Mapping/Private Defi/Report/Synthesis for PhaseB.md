## Overview

This note is a **handoff artifact from the DeFi vertical to “Transfers Phase B.”** It distills what DeFi (as a worst‑case, stateful, time‑sensitive workload) implies for Phase B priorities, success criteria, and evaluation questions.

**What it contains**

* **Section 1:** DeFi-driven **Phase B priorities** phrased as “what Phase B must decide / measure” if Transfers is meant to support DeFi workflows.
* **Section 2:** Concrete **cross-domain asks** to Transfers Phase B—what the Transfers substrate should explicitly support (or explicitly declare out-of-scope) to avoid private DeFi collapsing into public boundary hops and metadata leakage.

**How it connects to the rest of the vault**

* The detailed “why” and DeFi-specific manifestations of each PID live in the main mapping deliverable:
  → [[5 Problem Matrix Transfers & DeFi]] (DeFi column is filled; P01–P19 are the shared catalog)
* The recommended entry point and reading order for this whole DeFi pass:
  → [[Overview – DeFi (Private Writes)]]
* Background and definitions for what counts as a “private DeFi write” in this project:
  → [[1 Definitions, Scope & Boundaries]]
* DeFi mechanism/pattern notes that explain *how* different privacy substrates show up in DeFi:
  → [[2 Mechanisms & Patterns in DeFi]] and [[03_Pattern Observations – DeFi]]
* A shorter “pain points” list (useful when you need examples fast):
  → [[4 Open Problems – DeFi]]
* Orientation on why this work reuses Transfers’ Phase A framing (patterns + 19 problems):
  → [[DeFi – What I Took From Transfers]]

**Terminology / IDs**

* **PIDs (P01–P19)** refer to the **19 cross‑pattern problems** from Transfers Phase A, used here as the shared backbone across domains. For the full list and DeFi-specific elaboration, see [[5 Problem Matrix Transfers & DeFi]].

---

## 1) DeFi-Driven Phase B Priorities

* **Priority:** Define Phase B “privacy success” at the level of an **end-to-end position lifecycle**, not at the level of single transfers. Include the real-world touchpoints: relayers, paymasters, aggregators, and **network-layer submission metadata** (routing + timing).
  **PIDs:** P01, P09, P19
  **Why DeFi makes it urgent:** DeFi behavior is naturally **multi-write and time-correlated** (deposit → borrow → swap → adjust → repay/close). Even if each write is private in isolation, a lifecycle can often be reconstructed via repeated infrastructure choices, shared intermediaries, and timing patterns.
  **Phase B question:** Which lifecycle edges (funding, relayer/paymaster usage, routing, timing/submission metadata) must be hidden vs. can remain observable **without enabling practical graph reconstruction**?

* **Priority:** Treat **private-to-private composability** (across apps/protocol calls) and **boundary privacy** (in/out of the private domain) as **gating criteria** for “private DeFi stacks,” not optional add-ons.
  **PIDs:** P12, P13
  **Why DeFi makes it urgent:** Real DeFi workflows depend on **atomic multi-protocol actions** (borrow → swap → LP; refinance; roll debt; re-hedge). If privacy breaks at app boundaries or at bridge/shield boundaries, users are forced into public detours that reintroduce linkability exactly at the most revealing points.
  **Phase B question:** What is the minimum composability surface Transfers must enable so multi-step DeFi can remain private **without collapsing into public boundary hops**?

* **Priority:** Make **anonymity-set fragmentation and liquidity fragmentation** an explicit Phase B evaluation axis (by asset, venue, and L2), rather than assuming one “big” anonymity set will exist.
  **PIDs:** P02
  **Why DeFi makes it urgent:** DeFi naturally **shards users by market structure**: asset pair, venue, product type (LP vs borrower vs trader), and chain. This shrinks effective anonymity sets and can also degrade market quality (slippage, liquidation quality), creating a tight privacy ↔ liquidity coupling.
  **Phase B question:** How will Phase B measure “effective anonymity set” for DeFi-relevant assets/markets, and what minimums are required for **usable** private DeFi?

* **Priority:** Treat “minimum public/provable global state” and “cost per complex write” as first-class Phase B decisions. Quantify **residual leakage** and **DA/proof overhead** for core DeFi primitives (not just transfers).
  **PIDs:** P11, P03
  **Why DeFi makes it urgent:** Even if users/amounts are hidden, DeFi often requires global surfaces (e.g., reserves/utilization/oracle references) to be public or publicly provable; those surfaces can leak market-moving activity, especially in thin pools or around liquidations. DeFi operations are also structurally heavier than transfers, so proof/DA costs are paid repeatedly.
  **Phase B question:** Which public/provable signals are strictly necessary for safety/composability, and what leakage + cost budgets are acceptable for DeFi?

* **Priority:** Make **stress-mode liveness** (throughput + exits + DA trust) a first-class safety requirement if Transfers is expected to support leverage and liquidations downstream.
  **PIDs:** P04, P05, P06
  **Why DeFi makes it urgent:** During volatility and liquidation waves, load becomes bursty and adversarial. If users can’t close debt or exit quickly (because DA is withheld, throughput collapses, or operators censor), privacy-infra failure becomes **direct, time-bounded financial loss**.
  **Phase B question:** Under worst-case stress, what time-to-self-rescue and throughput targets are required, and what DA/operator trust assumptions are acceptable?

* **Priority:** Establish Phase B’s minimal **selective-disclosure and compliance interface** requirements, and explicitly address how repeated eligibility proofs avoid becoming stable pseudonyms.
  **PIDs:** P14, P15, P16, P08
  **Why DeFi makes it urgent:** Institutions (and some protocols) need controlled visibility (positions, solvency, dispute resolution) and eligibility checks. But view-key sprawl and repeated credential proofs can silently deanonymize long-lived positions and multi-step workflows.
  **Phase B question:** What “table-stakes” selective disclosure and eligibility interfaces are needed for DeFi participation **while preserving unlinkability across repeated actions**?

* **Priority:** Treat operability, auditability, and upgrade surfaces of private logic as DeFi safety constraints (not just DX concerns).
  **PIDs:** P17, P07, P10
  **Why DeFi makes it urgent:** DeFi places high-stakes financial logic inside private circuits/engines. Without privacy-preserving observability, constrained upgrades, and adequate audit/tooling capacity, correctness failures are harder to detect and can be catastrophic.
  **Phase B question:** What minimal observability/audit surfaces and upgrade constraints are required before private systems can safely host leverage and liquidations?

---

## 2) Cross-Domain “Asks” to Transfers Phase B

Use this list as a **checklist for Phase B scope**: either these are supported (with explicit guarantees), or Phase B should clearly state what is out-of-scope so downstream “private DeFi” claims don’t rely on assumptions Transfers won’t provide.

* **Ask:** Evaluate privacy at the level of **multi-write workflows / position lifecycles**, not just single transfers.
  **PIDs:** P01
  **What breaks without it (DeFi example):** A collateral → borrow → swap → repay lifecycle gets reconstructed as a “one user did a lifecycle” motif from timing-correlated footprints and repeated shared touchpoints.

* **Ask:** Support **private fee payment / relayer use** without making relayer choice, paymaster funding, or repeated top-ups into stable fingerprints.
  **PIDs:** P09, P01
  **What breaks without it (DeFi example):** Private swaps/LP actions that repeatedly use the same relayer/paymaster patterns become linkable, and can fail under urgency (repay/close windows) if the “private” path is fragile.

* **Ask:** Treat **network-layer metadata** (RPC/sequencer/relayer routing + timing) as part of the privacy threat model for DeFi-driven transfers.
  **PIDs:** P19
  **What breaks without it (DeFi example):** Time-critical actions near liquidation create distinctive timing signatures that correlate across writes via submission metadata even when onchain details are shielded.

* **Ask:** Provide (or clearly bound) a composability surface sufficient for **private-to-private, cross-app atomic actions**.
  **PIDs:** P12
  **What breaks without it (DeFi example):** Users can’t do borrow → swap → LP (or refinancing bundles) privately without breaking atomicity or detouring through public hops that add leakage.

* **Ask:** Account for **end-to-end boundary unlinkability** for shield/bridge in → DeFi action → unshield/bridge out workflows.
  **PIDs:** P13
  **What breaks without it (DeFi example):** Unique amount/timing patterns at entry/exit (especially for LP tokens or wrapped assets) correlate deposits with later withdrawals when volume is low or users are urgency-constrained.

* **Ask:** Assume anonymity sets will **shard by asset + venue (and across L2s)**; don’t evaluate as if one pooled anonymity set exists.
  **PIDs:** P02
  **What breaks without it (DeFi example):** A “private ETH/USDC pool” does not mix with “private stETH/ETH” or a lending market; whales/strategies become easier to fingerprint and liquidity quality degrades.

* **Ask:** Expose/consider how higher-layer apps can publish or prove the **minimum global state** DeFi needs (without revealing per-user details), and explicitly account for residual leakage + per-write cost.
  **PIDs:** P11, P03
  **What breaks without it (DeFi example):** Even with hidden users/amounts, reserve/utilization jumps and liquidation events leak coarse activity; if proofs/DA are too expensive per operation, DeFi writes become economically non-viable.

* **Ask:** Treat **stress-mode liveness** (throughput + exits + DA trust) as a requirement for DeFi safety actions.
  **PIDs:** P04, P05, P06
  **What breaks without it (DeFi example):** During liquidation storms, bottlenecked throughput or withheld encrypted state prevents users from exiting/closing debt before insolvency.

* **Ask:** Define what privacy-preserving **observability / dispute / debugging surfaces** are required to operate and audit private systems without creating “observability backdoors.”
  **PIDs:** P17, P07
  **What breaks without it (DeFi example):** Users/operators can’t diagnose failures or validate liquidations without oversharing position details, pushing teams toward dashboards/analytics that become privacy bypasses.

* **Ask:** Support selective disclosure and repeatable eligibility checks as an **interface (not an identity system)**—without turning credentials or view keys into stable pseudonyms across a lifecycle.
  **PIDs:** P14, P15, P16, P08
  **What breaks without it (DeFi example):** Institutions can’t participate without eligibility/disclosure hooks, but ad-hoc view keys and repeated proofs silently link many actions to the same entity over time.
