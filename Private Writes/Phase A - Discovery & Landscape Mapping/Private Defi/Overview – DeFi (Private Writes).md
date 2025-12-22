
This is the **DeFi vertical inside the Private Writes mapping**, using DeFi as a **worst‑case workload** (stateful, multi‑step, time‑sensitive) to stress‑test the **Transfers Phase A backbone** (patterns + the **19 cross‑pattern problems**).

The **actual outputs** are:
- a concrete **scope/definition of “private DeFi write”**,
- a **mapping of DeFi stressors onto the 19‑problem catalog**, and
- a synthesis explaining what Phase B must account for if it wants to support DeFi‑driven workflows.

---

## Start here (recommended reading order)

If you only read 3 things:
1) **What is “private DeFi” in this project?**  
   → [[1 Definitions, Scope & Boundaries]]

2) **How DeFi maps onto the [[Appendix C — Global Problem Catalog & Radar|19 cross‑pattern problems]]  we found in private transfers**  
   → [[4 Open Problems – DeFi]] is the fast DeFi “pain points” lens 
   → [[5 Problem Matrix Transfers & DeFi]] is the canonical mapping of those pain points into the problem catalog 
3) **What DeFi implies for Transfers Phase B priorities (handoff artifact)**  
   → [[Synthesis for PhaseB]]

Then, as needed:
- **Pattern notes (substrates + DeFi-specific extensions)** → [[2 Mechanisms & Patterns in DeFi]]
- **Private Defi Deployment shapes** → [[3 Ecosystem Snapshot – DeFi]]
- **Orientation note (why DeFi reuses Transfers framing)** → [[DeFi – What I Took From Transfers]]

---

## Main conclusions

### A) DeFi forces “privacy success” to be defined at the **workflow / lifecycle** level
In transfers, you can sometimes reason about privacy “per send.”  In DeFi, a user’s behavior is naturally a **position lifecycle** (deposit → borrow → swap → adjust → repay/close), which is easy to reconstruct via timing, infrastructure, and repeated touchpoints even if each write is “private.”

**Where it’s captured:**
- Phase B priority framing → [[Synthesis for PhaseB]]
- Problem mapping evidence → [[5 Problem Matrix Transfers & DeFi]]

---

### B) “Minimum public/provable global state” is a *structural* leakage channel in private DeFi
Even with hidden users/amounts, DeFi often **must** expose or prove consistency of **global surfaces** (AMM reserves/invariant‑relevant state, aggregate debt/utilization, oracle references). Those surfaces can move in market‑visible jumps, especially for whales and liquidations.

**Where it’s captured:**
- Scope definition + required public state note → [[1 Definitions, Scope & Boundaries]]
- Open problems bullets → [[4 Open Problems – DeFi]]
- Phase B priority hook (P11, P03) → [[Synthesis for PhaseB]]

---

### C) Liquidations / keepers are the hardest “private DeFi” problem to make safe
Naive “hide everything” breaks solvency monitoring; naive “show enough to liquidate” concentrates power in privileged actors and can reintroduce MEV / targeted liquidations.

**Where it’s captured:**
- Open problems bullets → [[4 Open Problems – DeFi]]
- Pattern notes (privacy-compatible keepers) → [[2 Mechanisms & Patterns in DeFi]]

---

### D) Anonymity sets fragment *naturally* in DeFi — and that couples to liquidity quality
DeFi shards activity by **asset, market, venue, and strategy type**. That fragments anonymity sets and also degrades market quality (slippage, liquidation quality), creating a “privacy ↔ liquidity” coupling that transfers don’t face as directly.

**Where it’s captured:**
- Phase B priority hook (P02) → [[Synthesis for PhaseB]]
- Problem matrix (P02) → [[5 Problem Matrix Transfers & DeFi]]

---

### E) Stress-mode liveness and exits become directly financial (not just “L2 risk”)
If a private system can’t provide **throughput + exits + DA availability** during volatility/liquidation waves, users can’t self‑rescue positions in time. That turns infra failure into time‑bounded losses.

**Where it’s captured:**
- Phase B priority hook (P04–P06) → [[Synthesis for PhaseB]]
- Open problems bullets → [[4 Open Problems – DeFi]]

---

### F) Compliance / selective disclosure is a dependency, but it can silently destroy unlinkability
Private DeFi needs “table‑stakes” interfaces for eligibility proofs and selective disclosure—without turning repeated proofs/view-key usage into stable pseudonyms.

**Where it’s captured:**
- Phase B priority hook (P14–P16, P08) → [[Synthesis for PhaseB]]
- Problem matrix (P14–P16) → [[5 Problem Matrix Transfers & DeFi]]

---