## Overview

This matrix is a **cross-domain read-through** of the **19 cross-pattern problems defined in [[Appendix C — Global Problem Catalog & Radar]] and summarized in [[6 Cross-Pattern Problems]]. For each of the 19 problems, we record (a) how the issue shows up in **private transfers** (baseline), and (b) how it shows up in **private DeFi**, including the **delta vs transfers** captured during the DeFi pass.

## At-a-glance matrix
The Problem and Cluster labels used here are the **structural problem clusters** defined in [[6 Cross-Pattern Problems]] . A single problem can appear in multiple clusters.

| ID  | Problem                                                      | Cluster(s)                                                     | Impact | Tractability | Crowdedness | Transfers (baseline)                                              | DeFi             |
| --- | ------------------------------------------------------------ | -------------------------------------------------------------- | ------ | ------------ | ----------- | ----------------------------------------------------------------- | ---------------- |
| 01  | Transaction Graph Leakage                                    | Privacy Leakage & Anonymity                                    | 5      | 3            | Crowded     | Timing/amount leakage around deposits, withdrawals, relayers      | Filled (see P01) |
| 02  | Fragmented Anonymity Sets                                    | Privacy Leakage & Anonymity; Composability & Interoperability  | 4      | 3            | Sparse      | Pool/asset/chain fragmentation shrinks effective anonymity sets   | Filled (see P02) |
| 03  | High L1 Costs for Private Verification and Data Availability | Data Availability, Scalability & Exits                         | 4      | 3            | Crowded     | Proof verification + calldata/DA costs impose high fee floors     | Filled (see P03) |
| 04  | Limited Throughput for Privacy-Preserving Rollups            | Data Availability, Scalability & Exits                         | 4      | 3            | Medium      | Proving + DA bottlenecks cap private rollup TPS                   | Filled (see P04) |
| 05  | Lack of User-Resilient Exits                                 | Data Availability, Scalability & Exits                         | 5      | 3            | Sparse      | DA failures can trap private state and block exits                | Filled (see P05) |
| 06  | Trust-Heavy DA Committees and Operators                      | Data Availability, Scalability & Exits                         | 4      | 4            | Medium      | Operators/committees can censor or withhold private state/data    | Filled (see P06) |
| 07  | Upgrade and Governance Risks for Private Circuits            | Governance & Operational Risk                                  | 3      | 4            | Sparse      | Circuit/prover upgrades are high-stakes and trust-centralizing    | Filled (see P07) |
| 08  | Multi-Key Management Complexity                              | UX & Developer Experience                                      | 4      | 4            | Medium      | Spend/view/audit keys + note/witness backup failure modes         | Filled (see P08) |
| 09  | Private Fee Payment and Relayer Friction                     | UX & Developer Experience                                      | 4      | 4            | Crowded     | Relayers + gas top-ups reintroduce linkability and UX friction    | Filled (see P09) |
| 10  | Poor Developer Tooling for Private Logic                     | UX & Developer Experience                                      | 4      | 4            | Medium      | Opaque circuits + fragmented DSLs slow building and auditing      | Filled (see P10) |
| 11  | Private Execution Leakage in DeFi Primitives                 | Privacy Leakage & Anonymity                                    | 5      | 3            | Crowded     | Mostly out-of-scope for transfer-only; arises with shared-state   | Filled (see P11) |
| 12  | Lack of Private-to-Private Composability                     | Composability & Interoperability                               | 4      | 3            | Sparse      | Cross-app private calls often require exits/de-shielding          | Filled (see P12) |
| 13  | Cross-Domain Privacy Leakage in Bridging                     | Privacy Leakage & Anonymity; Composability & Interoperability  | 4      | 2            | Sparse      | Bridge/exit routines expose timing+amount linkages across domains | Filled (see P13) |
| 14  | Missing Selective-Disclosure Standards                       | Compliance & Selective Disclosure                              | 5      | 4            | Sparse      | No standard proofs-of-innocence / auditability primitives         | Filled (see P14) |
| 15  | Immature Privacy-Preserving Compliance                       | Compliance & Selective Disclosure                              | 5      | 3            | Medium      | Compliance-compatible privacy is early-stage and inconsistent     | Filled (see P15) |
| 16  | Identity Binding Without Linkability                         | Privacy Leakage & Anonymity; Compliance & Selective Disclosure | 4      | 4            | Medium      | Identity/membership proofs can become stable correlators          | Filled (see P16) |
| 17  | Monitoring, Observability, and Debugging Blindness           | Governance & Operational Risk; UX & Developer Experience       | 3      | 4            | Sparse      | Hard to debug/operate without adding privacy-breaking telemetry   | Filled (see P17) |
| 18  | Incentive Fragility in Privacy Infrastructure                | Governance & Operational Risk                                  | 3      | 3            | Medium      | Relayer/prover/DA incentives are brittle; liveness is not assured | Filled (see P18) |
| 19  | Network-Layer Metadata Leakage                               | Privacy Leakage & Anonymity                                    | 4      | 3            | Medium      | RPC/mempool/timing/routing metadata correlates users              | Filled (see P19) |

---

## Per-problem sections

### P01 — Transaction Graph Leakage

**Cluster(s):** Privacy Leakage & Anonymity
**Radar (Phase A):** Impact 5 / Tractability 3 / Crowdedness Crowded

**Transfers**
**Transfers manifestation (2–5 bullets):**

* **Public entry/exit edges** (deposit/withdraw) create timing- and amount-correlated link signals, especially when withdrawals follow deposits quickly or use distinctive amounts.
* **Pool flow observability** (net inflows/outflows, churn, denomination usage) enables clustering even when individual transfers are shielded.
* **Fee payment + relayer/paymaster patterns** can create stable intermediaries (same relayer set, same sponsorship patterns) that reintroduce graph hubs and correlation.
* **Cross-domain moves** (bridge → shield → unshield) produce recognizable multi-step motifs that are easy to stitch into a user graph (overlaps with P13, but P01 is about the *graph motif*).

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* **Multi-step position workflows** (deposit collateral → borrow → swap → repay / adjust LP) leave timing-correlated footprints across contracts/relayers that can be stitched into a graph of “one user did a lifecycle.”
* **Fee/relayer routing** for private swaps or private LP joins can introduce stable intermediaries (same relayer set, same paymaster, same aggregator) that become graph hubs, re-introducing linkability.

**Delta vs Transfers (1–2 bullets):**

* DeFi actions are often **multi-write and stateful** (position lifecycle), creating more distinctive and repeated graph motifs than one-off transfers.
* Shared DeFi touchpoints (specific pools/markets, relayer/paymaster infrastructure) create **high-entropy “where did the user go?” edges** that aren’t present in pure shielded transfers.

**Severity (DeFi):** High
Private DeFi users typically must interact with shared protocol state and multi-step flows, creating many graph-level link signals even when payloads are private. **Boundary note:** P01 is about **onchain interaction graph motifs**; P19 is about **offchain submission / infra metadata correlation**.

**Phase B hook (1 sentence):**
Phase B should treat “end-to-end private position lifecycles” as the unit of analysis (not single writes) and ask which lifecycle edges must remain observable.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P02 — Fragmented Anonymity Sets

**Cluster(s):** Privacy Leakage & Anonymity; Composability & Interoperability
**Radar (Phase A):** Impact 4 / Tractability 3 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* **Anonymity sets shard by pool, asset, and denomination** (or note type), so users in one pool are not meaningfully mixed with users in another.
* **Multi-chain / multi-L2 deployments** further split users across domains; bridges do not automatically unify anonymity sets.
* **Two-tier privacy emerges:** “large, liquid pools” provide meaningfully better privacy than long-tail pools with thin activity, creating predictable user migration patterns.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* **Anonymity sets shard by asset + venue:** traders in a “private ETH/USDC pool” are not meaningfully mixed with users in a “private stETH/ETH pool” or “private lending market,” shrinking effective sets per action.
* **Product stratification:** LPs, borrowers, and leveraged traders form distinct behavioral clusters; even inside one private system, whales/institutions can stand out via interaction frequency or lifecycle patterns.
* **Cross-domain fragmentation:** private DeFi deployed across multiple L2s/app-chains creates parallel small anonymity sets, especially for non-bluechip assets.

**Delta vs Transfers (1–2 bullets):**

* Transfers can sometimes concentrate into a few high-volume shielded pools; DeFi naturally **splits by market** (pair, maturity, risk parameters), making fragmentation structurally worse.
* DeFi requires **liquidity** to be useful; fragmentation is simultaneously a privacy problem *and* a market-quality problem (slippage, liquidation quality).

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should explicitly evaluate whether private DeFi designs can *aggregate liquidity + anonymity* across assets/venues without forcing users into tiny per-market pools.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P03 — High L1 Costs for Private Verification and Data Availability

**Cluster(s):** Data Availability, Scalability & Exits
**Radar (Phase A):** Impact 4 / Tractability 3 / Crowdedness Crowded

**Transfers**
**Transfers manifestation (2–5 bullets):**

* **Proof verification + onchain commitments** (nullifiers, commitments, roots) create a high gas floor per private transfer, making small transfers uneconomic.
* **Calldata/DA requirements** (ciphertext payloads, commitments, roots) add recurring L1 cost that scales with throughput.
* **Fee volatility distorts behavior:** users delay/batch or route through relayers/L2s, which can create secondary leakage through timing and routing patterns.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* **Per-operation proofs are heavier than transfers:** validating an AMM swap or a collateral+debt update typically requires more arithmetic/constraints than a note transfer, increasing proof costs and/or calldata commitments per action.
* **Minimum public/provable surfaces still need posting:** even if positions are private, DeFi often must expose or prove consistency of global fields (e.g., AMM reserve/invariant state, aggregate debt/utilization, oracle references), which can add L1 data/verification overhead.
* **High-frequency writes** amplify costs because privacy overhead is paid repeatedly.

**Delta vs Transfers (1–2 bullets):**

* DeFi correctness requires **financial invariants and risk checks**, so “cost per private write” is structurally higher than for “send.”
* DeFi includes **time-sensitive safety actions**, so high L1 verification + DA posting costs (and fee spikes) can force economically bad outcomes (throughput/latency sensitivity is treated under P04).

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should model “cost per swap / borrow / liquidation” (not per transfer) and identify which DeFi rules can be proved cheaply vs must be simplified.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P04 — Limited Throughput for Privacy-Preserving Rollups

**Cluster(s):** Data Availability, Scalability & Exits
**Radar (Phase A):** Impact 4 / Tractability 3 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* **Proof generation and batching** (especially for larger circuits) can bottleneck throughput well below public rollups.
* **DA bandwidth** (posting commitments/ciphertexts) can become the limiting resource before compute does.
* **Congestion cascades into UX and centralization:** users rely more on relayers/operators to get included, concentrating submission paths.

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* **Stateful markets limit parallelism**; throughput can bottleneck on proving + sequencing for hot markets.
* **Market stress creates bursty load:** liquidation waves/mass deleveraging demand high throughput when private systems may be most constrained.
* **Rollup DA needs scale with DeFi frequency:** repeated small position adjustments can overwhelm DA.

**Delta vs Transfers (1–2 bullets):**

* Transfers are easier to batch; DeFi has **contention hotspots**.
* DeFi has **time-sensitive safety actions** that can’t be queued indefinitely.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should test private DeFi under “stress workloads” to see whether throughput limits become systemic risk.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P05 — Lack of User-Resilient Exits

**Cluster(s):** Data Availability, Scalability & Exits
**Radar (Phase A):** Impact 5 / Tractability 3 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* In **DA-light** designs (Validium/Plasma-like), if the DA provider withholds or censors data, users may be unable to **reconstruct private state** (notes/witnesses) needed to exit.
* Even when an escape hatch exists, **exit proofs depend on having the right data** (ciphertexts, witnesses, historic state) and can be operationally difficult for normal users.
* Some exit paths can force **partial declassification** (revealing notes/paths) or impose long delays, weakening privacy and usability.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* If a private rollup/validium halts or withholds data, users may be unable to **withdraw collateral or close debt** before insolvency.
* **Exit latency matters economically:** waiting out an **exit/escape delay (where applicable)** can be equivalent to forced liquidation.
* **LP exit under stress:** inability to exit can trap users during volatility.

**Delta vs Transfers (1–2 bullets):**

* DeFi positions have **liquidation and price-risk clocks**.
* **System-initiated writes** (liquidations/keepers) may continue (or be selectively censored) when users can’t act.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should treat “user-resilient exits under market stress” as a first-class DeFi safety requirement.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`

---

### P06 — Trust-Heavy DA Committees and Operators

**Cluster(s):** Data Availability, Scalability & Exits
**Radar (Phase A):** Impact 4 / Tractability 4 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Validium/Plasma-style systems rely on **operators or DA committees** for encrypted state availability; withholding can **freeze withdrawals** or strand users.
* DA power enables **selective censorship** (targeting specific exits or users) and can create coercion points even without breaking cryptography.
* Reliance on operator-provided data also creates **downtime UX failure modes** (wallet sync, witness availability) that disproportionately harm non-expert users.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* DA committees/operators can **withhold or delay state**, preventing exits or liquidation defense.
* **Censorship incentives are sharper in DeFi** (liquidation profit / adverse moves).
* Operator-served encrypted state becomes critical during stress.

**Delta vs Transfers (1–2 bullets):**

* Stronger adversarial incentives than transfers.
* More frequent state access for position monitoring increases exposure to operator reliability.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should model operator/committee attack incentives during liquidation events and ask what DA trust budget is tolerable.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P07 — Upgrade and Governance Risks for Private Circuits

**Cluster(s):** Governance & Operational Risk
**Radar (Phase A):** Impact 3 / Tractability 4 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* **Circuit/prover upgrades are high-stakes:** subtle bugs can break soundness (fund safety) or privacy, and are hard for users to independently verify.
* Upgrade control (admin keys, upgrade committees) can become a **centralization and trust point**, especially if upgrades can change validation rules or privacy parameters.
* Upgrades can also create **migration and fragmentation** problems (older note formats, multiple pools/versions), compounding P02.

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Upgrades via control points (upgrade keys / circuit maintainers / governance) can change **risk parameters, oracle references, or circuit logic** in ways hard to detect/verify quickly.
* Emergency upgrades during market events create centralized control points.
* Reduced ability for outsiders to re-execute/audit DeFi logic in real time.

**Delta vs Transfers (1–2 bullets):**

* Upgrading **financial risk logic** has higher stakes than “send.”
* Governance capture has stronger profit motives (liquidations).

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should ask what governance/upgrade constraints are required before private systems can safely host leverage and liquidations.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P08 — Multi-Key Management Complexity

**Cluster(s):** UX & Developer Experience
**Radar (Phase A):** Impact 4 / Tractability 4 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Users often must manage **multiple key roles** (spend/view/audit/recovery), creating failure modes: lost keys = lost funds; leaked view keys = lost privacy.
* Private systems require **note and witness management** (backups, rescans, device migration) that is fragile in today’s wallet UX.
* Optional disclosures (view keys for compliance, custodians, or dashboards) can become a **privacy bypass** if not scoped and rotated safely.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Multiple roles/keys (viewing/auditing keys) increase leakage/loss modes.
* Long-lived positions require durable key mgmt + **private-state persistence (notes/witnesses)**; recovery/resync and **exit actions** are non-trivial.
* Sharing view access with frontends/analytics can become a privacy bypass.

**Delta vs Transfers (1–2 bullets):**

* Persistent positions + monitoring increase key sprawl/disclosure events.

**Severity (DeFi):** Medium

**Phase B hook (1 sentence):**
Phase B should treat view-key sprawl as a concrete design constraint for private DeFi UX and institutional participation.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P09 — Private Fee Payment and Relayer Friction

**Cluster(s):** UX & Developer Experience
**Radar (Phase A):** Impact 4 / Tractability 4 / Crowdedness Crowded

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Paying fees from a public account **re-links private activity** to an address; fully private fee payment is non-trivial.
* **Relayers and gas abstraction** improve UX but introduce new trust and censorship surfaces, and relayer choice can become a fingerprint.
* **Top-up patterns** (funding relayer accounts, bridging gas) can create recognizable timing/amount correlations that undermine privacy.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Private swaps/LP actions often require relayers; relayer choice can become a fingerprint.
* Time-sensitive operations are brittle when dependent on relayer availability/latency/censorship.
* Fee payment flows can leak (recognizable top-up patterns).

**Delta vs Transfers (1–2 bullets):**

* Higher frequency/urgency makes relayer friction a risk surface (liquidation defense, LP exit).

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should evaluate private fee + relayer designs under DeFi urgency scenarios.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P10 — Poor Developer Tooling for Private Logic

**Cluster(s):** UX & Developer Experience
**Radar (Phase A):** Impact 4 / Tractability 4 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Even “simple” private transfers require **non-trivial circuits and cryptography**, and today’s debugging/auditing workflows lag far behind EVM tooling.
* Fragmented stacks (DSLs, proving systems, encryption/note formats) reduce reuse and slow iteration, making security review more expensive.
* Limited privacy-preserving testnets/observability makes it harder to catch **performance regressions and leakage** early.

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Complex circuits/constraint engineering for AMMs/lending/liquidations; missing tooling increases subtle bug risk.
* Audit scarcity and opaque debugging make validation hard (edge cases, rounding, oracle staleness).
* Fragmentation across DSLs/proving systems slows iteration vs public EVM workflows.

**Delta vs Transfers (1–2 bullets):**

* DeFi complexity/adversarial economics make tooling failures catastrophic.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should treat developer/auditor throughput as a constraint on which mechanisms are viable in a 1–3 year horizon.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P11 — Private Execution Leakage in DeFi Primitives

**Cluster(s):** Privacy Leakage & Anonymity
**Radar (Phase A):** Impact 5 / Tractability 3 / Crowdedness Crowded

**Transfers**
**Transfers manifestation (2–5 bullets):**

* For **transfer-only systems**, leakage is usually dominated by **entry/exit and pool flow signals** (P01) rather than shared-state price/risk mechanics.
* As soon as transfers are used inside **shared-state apps** (private swaps, private lending, “shielded” AMM layers), **economic surfaces** (price impact, utilization changes, liquidation-like events) can reveal private intent even if balances are encrypted.
* This problem marks a key boundary where “private transfers” start to inherit **DeFi-style leakage channels**.

**Severity (Transfers):** Low (transfer-only) / High (once DeFi primitives exist)

**DeFi**
**DeFi manifestation (2–5 bullets):**

* AMM reserve/invariant surfaces leak market-moving activity.
* Lending utilization/aggregate debt jumps leak activity.
* Liquidations are inherently revealing events.

**Delta vs Transfers (1–2 bullets):**

* DeFi writes touch shared pricing/risk state that often must remain public/provable.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should prioritize quantifying “minimum public/provable state” per primitive and residual leakage.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P12 — Lack of Private-to-Private Composability

**Cluster(s):** Composability & Interoperability
**Radar (Phase A):** Impact 4 / Tractability 3 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Private systems often cannot make **private contract calls across applications** without declassifying data, so cross-app workflows require **unshielding or trusted intermediaries**.
* Different systems use **incompatible note formats, encryption schemes, and proof interfaces**, preventing atomic transfers between private domains.
* Users end up “bridging between privacy silos,” increasing both friction and leakage (ties to P13).

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Atomic multi-protocol actions break across cross-app/protocol-call boundaries without declassification.
* Vault/aggregator patterns face friction downstream.
* Lack of composability pushes bridging between privacy silos.

**Delta vs Transfers (1–2 bullets):**

* DeFi composability is core value; inability is a major functional regression.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should treat cross-app private composability (swap↔lend↔liquidate) as gating.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P13 — Cross-Domain Privacy Leakage in Bridging

**Cluster(s):** Privacy Leakage & Anonymity; Composability & Interoperability
**Radar (Phase A):** Impact 4 / Tractability 2 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* **Bridge + exit routines** expose linkable public edges when moving assets between domains (L1↔L2, chain↔chain, public↔private).
* **Amount and timing matching** between deposits and withdrawals becomes especially strong when volume is low or when users are time-constrained.
* Wrappers and intermediary assets (escrows, “shielded” representations) can create **distinctive fingerprints** that reduce plausible deniability.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Entry/exit workflows can create unique amount/timing patterns correlating deposits↔withdrawals, especially with low volume or urgency (liquidation defense).
* DeFi-adjacent assets (LP tokens, wrapped collateral) are distinctive at boundaries.
* Cross-domain liquidity chasing becomes a behavioral signature.

**Delta vs Transfers (1–2 bullets):**

* DeFi has more “round trips,” creating stronger cross-domain linkage signals.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should evaluate end-to-end privacy across entry → DeFi action → exit flows.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`

---

### P14 — Missing Selective-Disclosure Standards

**Cluster(s):** Compliance & Selective Disclosure
**Radar (Phase A):** Impact 5 / Tractability 4 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* There is no widely adopted standard for **proofs-of-innocence, attribute-based disclosures, or auditability**; each system invents its own disclosure mechanism.
* Disclosure tools are often **all-or-nothing** (e.g., broad view-key sharing) rather than scoped, revocable, and minimal.
* Lack of standards increases integration cost (wallets, exchanges, custodians) and raises the risk of **accidental deanonymization**.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Selectively disclose positions/PnL/risk posture; today mostly bespoke view-key sharing.
* Disclosures for liquidation legitimacy/dispute resolution.
* Missing standards: proofs-of-innocence, audit trails, role-based disclosure policies; policy varies by jurisdiction/venue/counterparty.
* Bespoke disclosure models increase integration friction and accidental deanonymization.

**Delta vs Transfers (1–2 bullets):**

* DeFi requires richer disclosures than “I received funds.”

**Severity (DeFi):** Medium

**Phase B hook (1 sentence):**
Phase B should decide which selective-disclosure primitives are table-stakes and push standardization.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P15 — Immature Privacy-Preserving Compliance

**Cluster(s):** Compliance & Selective Disclosure
**Radar (Phase A):** Impact 5 / Tractability 3 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* “Compliance-compatible privacy” designs (screened pools, credential-gated access, audit hooks) are **early and inconsistent** across mechanisms.
* Compliance hooks can create **new linkability channels** (repeat checks, credential reuse) or shrink anonymity sets (permissioned pools).
* Lack of interoperability across compliance approaches pushes fragmentation and jurisdiction-specific silos.

**Severity (Transfers):** High

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Overlay private DeFi can appear mixer-like to observers/regulators.
* DeFi writes may need to consume external eligibility/attestation credentials; immature integration without collapsing privacy.
* Policy variability + repeated disclosures can become deanonymization channels.

**Delta vs Transfers (1–2 bullets):**

* DeFi (esp lending/leverage) sits in higher scrutiny zone; ongoing compliance visibility increases linkage risk.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should separate compliance-compatible requirements by primitive and identify minimal viable hooks that don’t destroy unlinkability.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`

---

### P16 — Identity Binding Without Linkability

**Cluster(s):** Privacy Leakage & Anonymity; Compliance & Selective Disclosure
**Radar (Phase A):** Impact 4 / Tractability 4 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Systems that require identity/membership (permissioned pools, credential gates) risk turning eligibility proofs into a **stable pseudonym** across transfers.
* Re-using the same credential across apps/chains makes **cross-context correlation** likely, even if each proof is “zero-knowledge.”
* Revocation, rotation, and multi-jurisdiction attribute policies are hard to implement without adding repeated, linkable checks.

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Repeatable credential/attestation proofs across a position lifecycle can act like a stable pseudonym across writes/venues over time.
* Institutional DeFi may need org-level identity while hiding strategy; binding identity across position management risks correlation.
* Policy variability increases linkability pressure (different attributes and re-check cadence).
* Adjacent risk: behavioral identity emerges (closer to P01/P17 than credential binding).

**Delta vs Transfers (1–2 bullets):**

* DeFi is repeated interaction; identity-binding events are more frequent/correlatable than one-off transfers.

**Severity (DeFi):** Medium

**Phase B hook (1 sentence):**
Phase B should ask how repeatable eligibility can be proven across DeFi lifecycles without becoming a stable pseudonym.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P17 — Monitoring, Observability, and Debugging Blindness

**Cluster(s):** Governance & Operational Risk; UX & Developer Experience
**Radar (Phase A):** Impact 3 / Tractability 4 / Crowdedness Sparse

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Privacy-preserving systems are **hard to observe and debug**: operators can’t easily detect anomalies (spam, sync failures, withheld data) without revealing private state.
* Users and support teams struggle to diagnose failures (missing note, failed withdraw) without **sharing sensitive information** (keys, view access, note history).
* Ad hoc monitoring dashboards can become **privacy backdoors**, concentrating visibility in a small set of services.

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Harder for users/auditors/operators to monitor solvency/risk; most apparent during stress/liquidations.
* Incident response hard without leaking positions.
* Users/support can’t validate failures/liquidations without sharing sensitive details.
* Observability backdoors via dashboards/analytics.

**Delta vs Transfers (1–2 bullets):**

* DeFi requires continuous monitoring; gaps translate to systemic financial risk.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should identify minimally necessary privacy-preserving telemetry to operate private AMMs/lending safely.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---

### P18 — Incentive Fragility in Privacy Infrastructure

**Cluster(s):** Governance & Operational Risk
**Radar (Phase A):** Impact 3 / Tractability 3 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Private transfers depend on **relayers, provers, and/or DA providers**; incentives are often immature or subsidized.
* When conditions worsen (fee spikes, adversarial load), infrastructure can degrade (slower inclusion, censorship, outages), directly impacting liveness and UX.
* Some incentive models can create **centralized chokepoints** (a small relayer set, privileged provers), compounding trust and privacy risk.

**Severity (Transfers):** Medium

**DeFi**
**DeFi manifestation (2–5 bullets):**

* Depends on provers/relayers/keepers; incentives can degrade when needed most (volatility/liquidations).
* Private liquidations are hard without privileged keepers; concentrating role creates fragility + new governance power under stress.
* Subsidized infra may be economically unstable at scale/adversarial load.

**Delta vs Transfers (1–2 bullets):**

* DeFi profit motives destabilize “neutral” infra roles; liveness failures become protocol risk (distinct from P06 trust assumptions).

**Severity (DeFi):** Medium

**Phase B hook (1 sentence):**
Phase B should evaluate which private DeFi components need always-on incentives vs best-effort service.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/03_Pattern Observations – DeFi.md`

---

### P19 — Network-Layer Metadata Leakage

**Cluster(s):** Privacy Leakage & Anonymity
**Radar (Phase A):** Impact 4 / Tractability 3 / Crowdedness Medium

**Transfers**
**Transfers manifestation (2–5 bullets):**

* Even with private onchain payloads, **RPC/mempool/sequencer metadata** (timing, ordering, endpoint choice) can correlate actions to a user or strategy.
* Network identifiers (IP/routing, client fingerprints) can link otherwise-unlinkable transfers across time and across pools.
* Reliance on relayers can reduce exposure but introduces another observer; without careful design, relayer routing becomes its own fingerprint.

**Severity (Transfers):** High

**DeFi**
P19 = network/infra metadata correlation; not MEV markets; not onchain graph linkage.

**DeFi manifestation (2–5 bullets):**

* Submission metadata (RPC endpoint, timing, routing, sequencer/relayer interaction) can correlate DeFi actions across time.
* Time-critical behavior near liquidation strengthens timing correlation.
* Keeper/liquidator bots may have identifiable network footprints.

**Delta vs Transfers (1–2 bullets):**

* DeFi actions are bursty/time-sensitive; more repeated network interactions per strategy.

**Severity (DeFi):** High

**Phase B hook (1 sentence):**
Phase B should treat network privacy as part of private DeFi threat model, not an optional add-on.

**Evidence pointers:**

* Transfers: [[Appendix C — Global Problem Catalog & Radar]]; [[6 Cross-Pattern Problems]]
* DeFi: `03_DeFi/01_Report/4 Open Problems – DeFi.md`
* DeFi: `03_DeFi/01_Report/3 Ecosystem Snapshot – DeFi.md`

---
