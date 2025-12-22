
## Review summary

During the DeFi workstream review we explicitly asked: **“Does DeFi introduce any privacy problem that is *categorically new* (i.e., not already covered by P01–P19)?”**
We collected the DeFi-native candidates that initially looked “new” in this vault (notably in `03_Pattern Observations – DeFi.md` and `4 Open Problems – DeFi.md`) and attempted to map each one to the existing problem catalog, using the DeFi column in `02_Problem_Matrix_Transfers_DeFi_Governance.md` as the reference point.

**Result:** **No DeFi-only problems were added.**
Across the candidates reviewed, DeFi tends to **amplify** or **combine** existing problems (e.g., shared market state, liveness under liquidation stress, composability across protocols, and boundary/linkability at entry/exit) rather than introducing a distinct “20th category” of problem.

The **mapping log** below documents the main “seems DeFi-specific” candidates and the reasoning for why each is best treated as a **DeFi manifestation across one or more existing PIDs**, rather than a new standalone DeFi-only PID.

## Mapping log (DeFi-specific candidates that *do* map to P01–P19)

> These are **not** additional problems. They are recorded to show that a mapping attempt was made and succeeded.

### Candidate: Privacy-compatible keepers and liquidation flows (pattern-level item)

**What this refers to (DeFi framing):**

* Lending/perps positions become eligible for liquidation when collateralization crosses a threshold, often during fast-moving markets.
* In private systems, the challenge is to support **solvency monitoring + timely liquidation execution** without turning all positions into public targets or giving a privileged set of actors exclusive visibility.

**Source(s) in this vault:**

* `03_Pattern Observations – DeFi.md` (Section B: “Seems DeFi-specific / new”)
* `4 Open Problems – DeFi.md` (liquidations/keepers bullet)

**Mapped to existing problem IDs:**

* **P11 — Private Execution Leakage in DeFi Primitives** (liquidations are inherently revealing events; minimum public/provable state and “coarse activity” leaks)
* **P04 — Limited Throughput for Privacy-Preserving Rollups** (liquidation waves demand burst throughput under stress)
* **P05 — Lack of User-Resilient Exits** (time-bounded self-rescue/exit constraints when positions are at risk)
* **P18 — Incentive Fragility in Privacy Infrastructure** (keeper/liquidator roles concentrate power; incentives degrade under volatility)
* **P19 — Network-Layer Metadata Leakage** (keeper/liquidator bots and their submission paths can be correlated via RPC/relayer/sequencer metadata)

**Why this is *not* a new DeFi-only problem:**

* The candidate is not a single root constraint; it is a **bundle** of already-captured constraints that become tightly coupled in liquidation scenarios:

  * **Information leakage / minimum public surfaces** (P11): even if positions are private, liquidation-triggering events and any required public/provable aggregates leak activity.
  * **Liveness + capacity under stress** (P04/P05): liquidation timing pressure makes throughput limits and exit guarantees directly material to user outcomes.
  * **Role centralization + incentives** (P18): specialized actors (“keepers”) introduce concentrated power and failure modes that are incentive-driven, especially during volatility.
  * **Submission-path correlation** (P19): the network layer can re-link actors and actions even when on-chain state is private.
* Stating this as a separate PID would largely duplicate the above PIDs while narrowing the context to one DeFi mechanism (liquidations), so it is tracked more cleanly as a **DeFi example cluster spanning P11/P04/P05/P18/P19**.

---

### Candidate: Vault / aggregator entry/exit privacy (pattern-level item)

**What this refers to (DeFi framing):**

* Vaults/aggregators pool user funds, issue shares, and execute multi-step strategies across downstream DeFi primitives.
* Even when deposits/withdrawals/shares are private, **external strategy interactions** (and the operational tooling around them) can leak intent or re-link users.

**Source(s) in this vault:**

* `03_Pattern Observations – DeFi.md` (Section B: “Vault/aggregator entry/exit privacy”)

**Mapped to existing problem IDs:**

* **P01 — Transaction Graph Leakage** (multi-step deposit/withdraw/share lifecycle can be linked via timing, touchpoints, and repeated management actions)
* **P12 — Lack of Private-to-Private Composability** (vault strategies compose downstream primitives; private↔public boundaries break atomic privacy across calls)
* **P13 — Cross-Domain Privacy Leakage in Bridging** (vault workflows often touch boundary points: wrap/bridge/unshield; distinctive amounts/timing can stitch “round trips”)
* **P17 — Monitoring, Observability, and Debugging Blindness** (pressure for dashboards/analytics can create “observability backdoors” that reintroduce correlation)

**Why this is *not* a new DeFi-only problem:**

* The privacy risk is primarily **end-to-end linkability across a lifecycle** (P01): vault participation is rarely a single action; it is a sequence (deposit → strategy updates → withdrawals/claims) that can accumulate correlation signals.
* The “vault” context also stresses **composability and boundary leakage** rather than creating a new category:

  * When strategies touch other protocols or domains, privacy depends on private-to-private composability (P12) and boundary handling (P13).
  * Operational demands (accounting, PnL, user dashboards) create additional leakage pressure captured by P17.
* The remaining statement can be expressed as: **“vaults/aggregators amplify P01 + P12/P13 + P17”**; there is no residual core constraint that requires a new DeFi-only PID.

---

### Candidate: “Encrypted orderflow + MEV-aware delivery with public settlement” (adjacent infra item)

**What this refers to (DeFi framing):**

* Even if final settlement is public, systems like encrypted mempools, private relays, commit–reveal, or batch auctions aim to reduce **pre-trade leakage** (swaps, liquidations, perps) that enables front-running, targeted liquidations, or other MEV behaviors.
* In practice, many attacks happen **before** on-chain verification (at RPC/relayer/sequencer/builder layers).

**Source(s) in this vault:**

* `03_Pattern Observations – DeFi.md` (Section C: Adjacent primitives / infra)
* `4 Open Problems – DeFi.md` (orderflow/MEV bullet; RPC/relayer/sequencer leakage)

**Mapped to existing problem IDs:**

* **P19 — Network-Layer Metadata Leakage** (submission metadata correlation at RPC/relayer/sequencer/builder layers)
* **P09 — Private Fee Payment and Relayer Friction** (relayer dependence; availability/latency/censorship and fee-routing constraints affect DeFi workflows)

**Why this is *not* a new DeFi-only problem:**

* In this vault’s scope, encrypted orderflow / MEV-aware delivery is treated as **adjacent infrastructure** rather than a DeFi write pattern that warrants its own problem ID.
* The parts that matter for DeFi privacy in this review reduce to:

  * **How transactions leak via the network and intermediaries** (P19), and
  * **What frictions and dependencies are introduced by relayer-based delivery and fee payment** (P09).
* As a result, it is tracked as an infra-adjacent manifestation of P09/P19 rather than a DeFi-only PID.

---

### Candidate: “Minimum public/provable global state” (scope-level tension)

**What this refers to (DeFi framing):**

* Many DeFi primitives require some **shared market/risk state** to remain public or at least publicly verifiable (e.g., AMM reserves/invariants, lending utilization, oracle references, aggregate solvency constraints).
* Even when per-user positions are private, these required surfaces can leak **coarse activity** (e.g., “someone just moved the pool”) and can impose proof/DA cost overhead.

**Source(s) in this vault:**

* `1 Definitions, Scope & Boundaries.md` (minimum global state notes)
* `4 Open Problems – DeFi.md` (“Necessary global state still leaks coarse activity”)

**Mapped to existing problem IDs:**

* **P11 — Private Execution Leakage in DeFi Primitives** (market-moving activity leaks through required public/provable surfaces; liquidations and other discontinuities are revealing)
* **P03 — High L1 Costs for Private Verification and Data Availability** (proving consistency of required public/provable fields can increase verification + DA overhead)

**Why this is *not* a new DeFi-only problem:**

* This is already the **central DeFi manifestation** of P11: DeFi is unusually sensitive to what must remain public/provable because shared state is economically meaningful.
* Where the “minimum global state” choice increases proof/verification or DA costs, that aspect is already captured under P03.
* The candidate therefore does not create a new problem category; it specifies the DeFi-shaped instance of P11 (with cost implications tracked in P03).
