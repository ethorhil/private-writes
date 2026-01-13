## 2.1 Header

- **PID:** P13 — Cross-Domain Privacy Leakage in Bridging
- **Clusters:** `Composability & interoperability`; `Privacy leakage & anonymity`
- **Patterns bound:** `L1 Overlay – Stealth  OTR`; `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Permissioned Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`

## 2.2 Problem statement

**Definition**  
Cross-domain privacy leakage occurs when moving assets between domains (L1↔L2, chain↔chain, public↔private) because bridge contracts, wrappers, and exit routines create public “boundary edges” and distinctive fingerprints that allow observers to link otherwise-private activity across domains.

Expanded: even if a domain is locally private, boundary events frequently reveal amounts, timing, and asset-specific identifiers that enable deposit↔withdrawal (or shield↔unshield) matching—especially under low volume or user time pressure (e.g., urgent exits, liquidation defense). Wrapper and intermediary representations can further reduce plausible deniability by creating unique “this must be that flow” signatures.

What this is not: this PID is specifically about **privacy loss at domain boundaries** (bridge/shield/unshield/exit). It is not the general within-domain interaction-graph motif problem (see P01), and it is not primarily about network-layer submission metadata (see P19).

**Why it matters**  
Cross-domain movement is often required for real use (moving between chains/rollups, accessing liquidity/venues, or shifting between “private” and “public” contexts). If privacy collapses at the boundary, users and counterparties can reconstruct sensitive linkages (identity, strategy, provenance), which can negate the value of privacy substrates and create secondary risks (market/front-running exposure, compliance exposure, reduced willingness to adopt private rails).

**Affected workloads**  
Transfers (baseline): deposit/withdraw, bridge in/out, wrapping/unwrapping, exit routines, and “round-trip” behaviors that create linkable public edges across domains.  
DeFi stress-test manifestation (when relevant): entry → DeFi action(s) → exit flows; boundary events for LP tokens or wrapped collateral; time-constrained boundary actions (e.g., during volatile markets) that tighten amount/timing correlations and increase linkage risk.

## 2.3 Failure modes & success

**Failure modes / symptoms**
- One-to-one or near-one-to-one matching between deposits and withdrawals using amount + timing windows (strongest under low volume or urgency).
- Distinctive wrapper assets or intermediary representations that create unique boundary fingerprints (e.g., “only one user could be doing this round trip”).
- Repeated “round trips” (in/out flows) that compound linkage signals over time, especially when chasing liquidity across domains.
- Boundary policies (rate limits, exit windows, operational constraints) that force distinctive user behaviors, further aiding linkage.

Dependencies / prerequisites (non-prescriptive)
- Adequate boundary-side volume and/or churn so boundary events do not become “unique” by default.
- Coordination with adjacent “related mechanisms not scored” where relevant (cross-domain transports; ordering/submission privacy; identity/credential layers) to avoid boundary leakage becoming the dominant leakage channel.

Tradeoffs / failure modes of fixes (what can go wrong)
- Reducing boundary linkability often pressures UX and latency (e.g., if users must avoid urgency or accept longer time windows to blend into others).
- Stronger boundary privacy constraints can fragment liquidity or make certain asset forms less usable (e.g., if wrappers become too restrictive or too standardized).
- “Compliance-friendly” boundary disclosures can accidentally reintroduce stable identifiers that worsen linkability if not carefully scoped (overlap risk with P14–P16).

**What success looks like (measurable)**
- A repeatable evaluation harness exists for cross-domain linking attacks (amount/timing/wrapper matching) and is used consistently across patterns.
- In representative boundary-volume conditions, the median deposit↔withdraw candidate set size (for a reasonable external observer) is **≥ 20** for common boundary workflows, and no common workflow collapses to a “unique match” by default.
- Under benchmarked boundary-linking classifiers that use timing/amount/asset identifiers, linking performance is near-baseline (e.g., **≤ 10% precision at ≥ 20% recall**) for typical user flows.
- Boundary workflows for DeFi-relevant assets (including wrapped collateral / LP-adjacent artifacts) do not create distinctive, repeated “round-trip” fingerprints that make strategies trivially correlatable.

## 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 4
- Tractability (1–3y): 2
- Crowdedness: Sparse
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

## 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| `L1 Overlay – Stealth  OTR` | Because amounts/senders remain public, any cross-domain move from/to overlay-managed funds can amplify amount/timing linkage; boundary privacy cannot assume hidden amounts and must control “public edge” uniqueness. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Overlay – Stealth  OTR.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/13 Cross-Domain Privacy Leakage in Bridging.md` |
| `L1 Shielded Pools` | Deposit/withdraw (and cross-chain bridging) remain public boundary edges; low-volume pools or urgent withdrawals strengthen matching attacks, so boundary privacy is a first-order constraint on “effective privacy.” | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Shielded Pools.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| `Burn-and-Mint Privacy` | The core burn→mint cross-context flow is inherently exposed to amount/timing matching; preventing “burn fingerprint → mint fingerprint” linkage is binding for cross-domain privacy claims. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Burn-and-Mint Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/13 Cross-Domain Privacy Leakage in Bridging.md` |
| `Permissioned Privacy` | Boundary interactions with public systems can leak identity through disclosure policy, access control, or operational procedures; cross-domain flows must avoid turning compliance-required artifacts into stable boundary identifiers. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Permissioned Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^e74e59` |
| `Private Rollups (Full DA)` | “Bridge in/out” and exit routines create boundary events whose timing/amount patterns can re-link otherwise-private rollup activity; boundary unlinkability is required for end-to-end privacy claims. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Rollups (Full DA).md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` |
| `Private Plasma` | Exit windows and user time pressure (especially under stress) can force distinctive boundary behaviors; boundary privacy must explicitly account for “urgent exit” linkage risk. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Plasma.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| `Private Validium` | Operator/DA-provider mediated exits and wrapper representations can create distinctive boundary fingerprints and centralized timing patterns; boundary privacy must treat operator-mediated flows as potential linkability channels. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Validium.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^3cb481` |

## 2.6 Intervention modes (non-prescriptive)

- Research  
  - Formalize cross-domain linkage threat models (amount/timing/wrapper matching) and define metrics for “boundary unlinkability.”
  - Study how “round-trip” behaviors amplify linkage, especially under DeFi stress (time-sensitive actions).

- Engineering  
  - Develop measurement/benchmark tooling and reproducible evaluation harnesses for boundary linkage risk (datasets, simulators, test vectors).
  - Improve developer/operator guidance for boundary workflows to reduce accidental uniqueness (without mandating any specific architecture).

- Standards / coordination  
  - Coordinate on common evaluation metrics and reporting formats for boundary privacy (so systems can be compared without re-scoring).
  - Align cross-domain transport interfaces (where in-scope) to reduce wrapper-driven fingerprinting.

- Grants / convening  
  - Fund independent red-teaming and measurement work focused on boundary-linkage attacks and realistic workload traces.

## 2.7 Evidence & uncertainty

**Key references**
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/13 Cross-Domain Privacy Leakage in Bridging.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^e74e59`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^3cb481`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/9 Out-of-Scope for Phase A & Inputs to Phase B.md`

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Uncertainty / notes |
|---|---|---|
| P13-C1 | Moving assets between privacy domains (e.g., L2↔L1 or chain↔chain) introduces observable boundary events that can create linkability between otherwise private contexts. | Boundary leakage depends on protocol design (e.g., amount randomization, delays) and user behavior. |
| P13-C2 | Cross-chain transaction matching heuristics can link deposits/withdrawals across chains at high rates, implying that bridge flows are often traceable and therefore privacy-leaky at domain boundaries. | Matching success depends on data availability, bridge design, and how many candidate transfers share similar timing/amounts. |
| P13-C3 | Empirical analyses show that anonymity in deployed private-transfer systems can be reduced by usage-pattern heuristics, shrinking effective anonymity sets. | Results are system- and epoch-dependent; heuristics may degrade as users adopt better privacy hygiene. |
| P13-C4 | In mixer-style systems, deposit/withdrawal clustering can deanonymize users by linking withdrawals to likely deposits using on-chain patterns. | Effect size varies by pool size, denomination structure, and adversary auxiliary data. |
| P13-C5 | Cross-chain usage (bridging + mixing) increases correlation surface; clustering across multiple chains can further reduce anonymity versus single-chain analysis. | Cross-chain clustering quality depends on consistent addresses, reuse patterns, and cross-chain timing synchrony. |
| P13-C6 | Wallet-level fingerprints (behavioral or structural features) can be used to attack mixer anonymity sets beyond simple amount/timing matching. | Attack performance depends on feature availability and whether wallets adopt countermeasures (e.g., batching, decoys). |
| P13-C7 | Linkability risk increases when anonymity sets are small or when users perform predictable exits (e.g., rapid withdrawal after deposit), making boundary leakage more acute under low-volume or stress conditions. | General trend is well supported, but exact thresholds are context-specific (fees, user mix, adversary view). |


**Key uncertainties (Sprint 1)**
- What boundary-volume regimes are “typical” for the intended user segments (low-volume makes linkage structurally easier).
- How much user urgency (time constraints) is unavoidable in common workflows (especially under DeFi stress).
- Whether wrapper/representation diversity is a must-have for usability (and therefore a persistent fingerprinting surface).

**What would change the score**
- If multiple independent systems demonstrate strong benchmark results on boundary unlinkability (reducing deposit↔withdraw matching) under realistic volumes, Tractability likely increases.
- If cross-domain "round-trip" usage becomes dominant (or regulators/venues force more boundary disclosures), Impact could increase (more harm) or the success threshold may tighten.
- If crowdedness materially increases (many teams converge on boundary privacy measurement + mitigations), Crowdedness would change from Sparse.