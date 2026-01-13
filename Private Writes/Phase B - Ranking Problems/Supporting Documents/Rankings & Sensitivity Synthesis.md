
This file summarizes which PIDs rise to the top under multiple baseline ranking lenses and what changes under baseline sensitivity weight profiles. The source of these rankings is [this register](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=0#gid=0) 

## 1) How to read these rankings

- These are baseline-only lenses mechanically derived. Read them as “what rises under this lens,” not as a single authoritative ordering.
- A PID can move up/down depending on which baseline constraints you privilege (impact-maximizing vs moveability vs under-served space vs DeFi stress relevance).
- EF-fit is a separate overlay about comparative advantage

## 2) Baseline ranking profiles (Top 10)

### 2.1 Impact-first
[Source](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=193659070#gid=193659070)

| Rank | PID ID | PID title |
| --- | --- | --- |
| 1 | P14 | P14 — Missing Selective-Disclosure Standards |
| 2 | P05 | P05 — Lack of User-Resilient Exits |
| 3 | P11 | P11 — Private Execution Leakage in DeFi Primitives |
| 4 | P01 | P01 — Transaction Graph Leakage |
| 5 | P15 | P15 — Immature Privacy-Preserving Compliance |
| 6 | P08 | P08 — Multi-Key Management Complexity |
| 7 | P10 | P10 — Poor Developer Tooling for Private Logic |
| 8 | P06 | P06 — Trust-Heavy DA Committees and Operators |
| 9 | P09 | P09 — Private Fee Payment and Relayer Friction |
| 10 | P16 | P16 — Identity Binding Without Linkability |

What stands out (why these rise under this lens):
- The Top 5 are all Impact_Score=5: `P14 — Missing Selective-Disclosure Standards`, `P05 — Lack of User-Resilient Exits`, `P11 — Private Execution Leakage in DeFi Primitives`, `P01 — Transaction Graph Leakage`, `P15 — Immature Privacy-Preserving Compliance`. When impact is primary, standards/compliance and safety/leakage items dominate the top tier.
- `P14 — Missing Selective-Disclosure Standards` ranks #1 because it is the only Impact=5 item with Tractability_Score=4; the register treats it as both high-impact and relatively movable, but with very high coordination burden (CoordinationRisk_Score=5).
- `P05 — Lack of User-Resilient Exits` and `P11 — Private Execution Leakage in DeFi Primitives` are both tagged DeFiStressTestRelevance=Critical, so they remain salient under DeFi stress-test filtering as well as impact-maximizing views.
- The lower half of the Top 10 is largely Tractability_Score=4 “execution-friction / operationalization” PIDs: `P08 — Multi-Key Management Complexity`, `P10 — Poor Developer Tooling for Private Logic`, `P06 — Trust-Heavy DA Committees and Operators`, `P09 — Private Fee Payment and Relayer Friction`, `P16 — Identity Binding Without Linkability`. These outrank some Impact=4/Tractability=3 items via the view’s tie-breakers.
- Cluster coverage in the Top 10 is broad: compliance/selective disclosure (P14/P15/P16), exits + DA/operator trust (P05/P06), leakage/anonymity (P01/P11), and UX/DevEx/relayer friction (P08/P09/P10).

Register fields used for the notes above: `Impact_Score`, `Tractability_Score`, `CoordinationRisk_Score`, `DeFiStressTestRelevance`, `Cluster_Labels`, plus the corresponding rationale fields (`Impact_Rationale`, `Tractability_Rationale`, `CoordinationRisk_Rationale`).

### 2.2 Impact × tractability

[Source](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=1509686785#gid=1509686785)

| Rank | PID ID | PID title |
| --- | --- | --- |
| 1 | P14 | P14 — Missing Selective-Disclosure Standards |
| 2 | P06 | P06 — Trust-Heavy DA Committees and Operators |
| 3 | P08 | P08 — Multi-Key Management Complexity |
| 4 | P09 | P09 — Private Fee Payment and Relayer Friction |
| 5 | P10 | P10 — Poor Developer Tooling for Private Logic |
| 6 | P16 | P16 — Identity Binding Without Linkability |
| 7 | P01 | P01 — Transaction Graph Leakage |
| 8 | P05 | P05 — Lack of User-Resilient Exits |
| 9 | P11 | P11 — Private Execution Leakage in DeFi Primitives |
| 10 | P15 | P15 — Immature Privacy-Preserving Compliance |

What stands out (why these rise under this lens):
- `P14 — Missing Selective-Disclosure Standards` stays #1 because it is uniquely Impact=5 and Tractability=4 (Composite=20).
- Tractability=4 / Impact=4 items `P06 — Trust-Heavy DA Committees and Operators`, `P08 — Multi-Key Management Complexity`, `P09 — Private Fee Payment and Relayer Friction`, `P10 — Poor Developer Tooling for Private Logic`, `P16 — Identity Binding Without Linkability` (Composite=16) move ahead of Impact=5 / Tractability=3 items `P01 — Transaction Graph Leakage`, `P05 — Lack of User-Resilient Exits`, `P11 — Private Execution Leakage in DeFi Primitives`, `P15 — Immature Privacy-Preserving Compliance` (Composite=15). This lens privileges “moveability” more than incremental impact within the top tier.
- The Top 10 membership is identical to Impact-first; the main difference is ordering. For memo framing: the “candidate set” is stable, but prioritization changes if you optimize for near-term tractable movement.
- This view disproportionately surfaces operational and integration frictions (DA/operator trust, relaying/fees, tooling, key management, identity binding) because those have high baseline tractability scores in the register.
- High-impact but more coordination-heavy items do not disappear, but can move down when they do not also score highly on tractability.

Register fields used for the notes above: `Impact_Score`, `Tractability_Score`, `Impact_Rationale`, `Tractability_Rationale`, `CoordinationRisk_Score`/`CoordinationRisk_Rationale`, and `Cluster_Labels`.

### 2.3 Under-served high-impact (Tier 1)

[Source](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=1714298775#gid=1714298775) 
Note: the Tier 1 filter yields only 4 eligible PIDs (so this is a shortlist, not a full Top 10).

| Rank | PID ID | PID title |
| --- | --- | --- |
| 1 | P14 | P14 — Missing Selective-Disclosure Standards |
| 2 | P05 | P05 — Lack of User-Resilient Exits |
| 3 | P02 | P02 — Fragmented Anonymity Sets |
| 4 | P12 | P12 — Lack of Private-to-Private Composability |

What stands out (why these rise under this lens):
- This is a strict “filter-first” view: Impact_Score≥4, Tractability_Score≥3, and Crowdedness_Score=Sparse. The output is intentionally small.
- The shortlist is: `P14 — Missing Selective-Disclosure Standards`, `P05 — Lack of User-Resilient Exits`, `P02 — Fragmented Anonymity Sets`, `P12 — Lack of Private-to-Private Composability`.
- Compared to impact-maximizing views, the inclusion of P02 and P12 is driven largely by the under-served proxy (Sparse crowdedness), not by the highest raw Impact×Tractability composites.
- Interpreting this lens depends heavily on the register’s crowdedness tagging and rationale; it primarily answers “which high-impact areas appear less crowded,” not “which problems are easiest.”

Register fields used for the notes above: `Impact_Score`, `Tractability_Score`, `Crowdedness_Score`, `Crowdedness_Rationale`, plus `Impact_Rationale`/`Tractability_Rationale` for short justification hooks.

### 2.4 Under-served high-impact (Tier 2)

Source CSV: `Phase B/Sprints/4/_outputs/ranking_under_served_high_impact_tier2.csv`

| Rank | PID ID | PID title |
| --- | --- | --- |
| 1 | P14 | P14 — Missing Selective-Disclosure Standards |
| 2 | P06 | P06 — Trust-Heavy DA Committees and Operators |
| 3 | P08 | P08 — Multi-Key Management Complexity |
| 4 | P10 | P10 — Poor Developer Tooling for Private Logic |
| 5 | P16 | P16 — Identity Binding Without Linkability |
| 6 | P05 | P05 — Lack of User-Resilient Exits |
| 7 | P15 | P15 — Immature Privacy-Preserving Compliance |
| 8 | P02 | P02 — Fragmented Anonymity Sets |
| 9 | P04 | P04 — Limited Throughput for Privacy-Preserving Rollups |
| 10 | P12 | P12 — Lack of Private-to-Private Composability |

What stands out (why these rise under this lens):
- Tier 2 relaxes the under-served proxy from Crowdedness={Sparse} to Crowdedness={Sparse, Medium}, producing a fuller Top 10 while still excluding Crowded items.
- Crowded items that are otherwise top-ranked in impact-maximizing views—`P01 — Transaction Graph Leakage`, `P09 — Private Fee Payment and Relayer Friction`, `P11 — Private Execution Leakage in DeFi Primitives`—drop out here purely because of the crowdedness filter, not because they score low on impact or tractability.
- Under this lens, “under-served” swaps in `P02 — Fragmented Anonymity Sets`, `P04 — Limited Throughput for Privacy-Preserving Rollups`, `P12 — Lack of Private-to-Private Composability`, shifting the shortlist toward composability/fragmentation and throughput constraints.
- `P14 — Missing Selective-Disclosure Standards` still anchors #1 under the filter because it combines Impact=5, Tractability=4, and Crowdedness=Sparse.
- Near-miss to note for downstream synthesis: P19 appears at Rank 11 in the Tier 2 CSV export (just outside the Top 10 under this filter).

Register fields used for the notes above: `Crowdedness_Score`/`Crowdedness_Rationale` (filter driver), plus `Impact_Score`, `Tractability_Score`, `Impact_Rationale`, `Tractability_Rationale`, and `Cluster_Labels`.

### 2.5 DeFi-weighted critical

[Source](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=1243835841#gid=1243835841)

| Rank | PID ID | PID title |
| --- | --- | --- |
| 1 | P06 | P06 — Trust-Heavy DA Committees and Operators |
| 2 | P09 | P09 — Private Fee Payment and Relayer Friction |
| 3 | P01 | P01 — Transaction Graph Leakage |
| 4 | P05 | P05 — Lack of User-Resilient Exits |
| 5 | P11 | P11 — Private Execution Leakage in DeFi Primitives |
| 6 | P03 | P03 — High L1 Costs for Private Verification and Data Availability |
| 7 | P04 | P04 — Limited Throughput for Privacy-Preserving Rollups |
| 8 | P07 | P07 — Upgrade and Governance Risks for Private Circuits |
| 9 | P12 | P12 — Lack of Private-to-Private Composability |
| 10 | P17 | P17 — Monitoring, Observability, and Debugging Blindness |

What stands out (why these rise under this lens):
- This is a filter-first view: only PIDs tagged DeFiStressTestRelevance=Critical are included, then ranked by baseline Impact×Tractability. Treat it as “under DeFi stress-test assumptions,” not a general baseline priority list.
- The top two are `P06 — Trust-Heavy DA Committees and Operators`, `P09 — Private Fee Payment and Relayer Friction` because both are Critical and score Impact=4, Tractability=4 (Composite=16), elevating operational viability constraints ahead of some higher-impact-but-less-tractable items.
- High-impact leakage and safety items remain near the top when they are also tagged Critical: `P01 — Transaction Graph Leakage`, `P05 — Lack of User-Resilient Exits`, `P11 — Private Execution Leakage in DeFi Primitives`.
- This lens pulls in additional “system viability under stress” constraints that are Critical-tagged even if their baseline Impact_Score is lower, including `P07 — Upgrade and Governance Risks for Private Circuits`, `P17 — Monitoring, Observability, and Debugging Blindness` (both Tractability_Score=4) and `P03 — High L1 Costs for Private Verification and Data Availability`, `P04 — Limited Throughput for Privacy-Preserving Rollups` (DA/cost/throughput constraints).
- Several non-Critical but otherwise high-ranking items—`P14 — Missing Selective-Disclosure Standards`, `P15 — Immature Privacy-Preserving Compliance`, `P16 — Identity Binding Without Linkability`, `P08 — Multi-Key Management Complexity`, `P10 — Poor Developer Tooling for Private Logic`—are absent by construction; their absence is driven by the DeFiStressTestRelevance filter, not by low baseline scores.

Register fields used for the notes above: `DeFiStressTestRelevance` (filter driver), `Impact_Score`, `Tractability_Score`, `Impact_Rationale`, `Tractability_Rationale`, and `Cluster_Labels`.

## 3) Overlap and divergence across baseline profiles

Consistently top-present across the baseline lenses above:
- `P05 — Lack of User-Resilient Exits` appears in the Top set of all five baseline profiles shown here (including the strict under-served Tier 1 shortlist).
- Across the four “full” Top 10 profiles (Impact-first, Impact×tractability, Under-served Tier 2, DeFi-weighted critical), `P06 — Trust-Heavy DA Committees and Operators` is also consistently present.

Where the baseline lenses diverge most (what assumption drives the changes):
- **Under-served filter effect (Crowdedness):** Under-served Tier 2 swaps in `P02 — Fragmented Anonymity Sets`, `P04 — Limited Throughput for Privacy-Preserving Rollups`, `P12 — Lack of Private-to-Private Composability` and drops `P01 — Transaction Graph Leakage`, `P09 — Private Fee Payment and Relayer Friction`, `P11 — Private Execution Leakage in DeFi Primitives` relative to the impact-maximizing Top 10 set. Driver: `Crowdedness_Score` (excluding `Crowded`).
- **DeFi stress-test filter effect (Critical-only):** DeFi-weighted critical swaps in `P03 — High L1 Costs for Private Verification and Data Availability`, `P04 — Limited Throughput for Privacy-Preserving Rollups`, `P07 — Upgrade and Governance Risks for Private Circuits`, `P12 — Lack of Private-to-Private Composability`, `P17 — Monitoring, Observability, and Debugging Blindness` and drops `P08 — Multi-Key Management Complexity`, `P10 — Poor Developer Tooling for Private Logic`, `P14 — Missing Selective-Disclosure Standards`, `P15 — Immature Privacy-Preserving Compliance`, `P16 — Identity Binding Without Linkability` relative to the impact-maximizing Top 10 set. Driver: `DeFiStressTestRelevance == Critical`.
- **Ordering vs membership:** Impact-first vs Impact×tractability have the same Top 10 membership; the difference is rank ordering driven by whether you privilege Impact_Score first or the Impact×Tractability composite.

Profile-sensitive PIDs (examples):
- `P14 — Missing Selective-Disclosure Standards` is top-ranked in impact-maximizing and under-served views, but disappears in the DeFi-weighted critical view because it is tagged `Relevant` rather than `Critical` for DeFi stress relevance.
- `P02 — Fragmented Anonymity Sets` and `P12 — Lack of Private-to-Private Composability` are most visible in the under-served lenses (Sparse/Medium crowdedness). They are not absent elsewhere because of low impact, but because other lenses do not treat crowdedness as a constraint.
- `P03 — High L1 Costs for Private Verification and Data Availability`, `P07 — Upgrade and Governance Risks for Private Circuits`, and `P17 — Monitoring, Observability, and Debugging Blindness` show up most strongly when the DeFi stress-test constraint is imposed (Critical-only), indicating they are treated as stress-mode viability bottlenecks rather than general top-impact items.

## 4) Sensitivity pivots (baseline-only; weight profiles)

Main “switches” tested (and what they change in the Top 10):
- **Impact-heavy vs Balanced:** membership is stable; ordering shifts toward Impact_Score=5 items (relative deprioritization of tractability-first items).
- **Tractability-heavy:** introduces `P07 — Upgrade and Governance Risks for Private Circuits` and `P17 — Monitoring, Observability, and Debugging Blindness` and can push out `P01 — Transaction Graph Leakage` and `P15 — Immature Privacy-Preserving Compliance` (reflecting higher weight on Tractability_Score).
- **Coordination-heavy:** penalizes high CoordinationRisk strongly (via CoordinationEase), which removes `P14 — Missing Selective-Disclosure Standards` and `P15 — Immature Privacy-Preserving Compliance` from the Top 10 in that profile and pulls in `P04 — Limited Throughput for Privacy-Preserving Rollups`.
- **Fast-wins:** a moderated tractability emphasis; elevates tractability=4 items to the top while retaining many impact=5 items.
- **Under-served (Balanced weights + Crowdedness filter):** excludes Crowded items—`P01 — Transaction Graph Leakage`, `P09 — Private Fee Payment and Relayer Friction`, `P11 — Private Execution Leakage in DeFi Primitives`—and replaces them with Medium/Sparse items, isolating the effect of “avoid crowded areas” as a separate assumption.

Stability summary from `sensitivity_profiles_top10.csv` (Top 10 presence across the 5 weight-only profiles):
- Robust (appear in Top 10 in all 5 weight-only profiles): `P05 — Lack of User-Resilient Exits`, `P06 — Trust-Heavy DA Committees and Operators`, `P08 — Multi-Key Management Complexity`, `P09 — Private Fee Payment and Relayer Friction`, `P10 — Poor Developer Tooling for Private Logic`, `P11 — Private Execution Leakage in DeFi Primitives`.
- Near-robust (appear in 4/5 weight-only profiles): `P14 — Missing Selective-Disclosure Standards`, `P16 — Identity Binding Without Linkability`.
- Weight-sensitive (appear in 3/5 weight-only profiles): `P01 — Transaction Graph Leakage`, `P07 — Upgrade and Governance Risks for Private Circuits`, `P17 — Monitoring, Observability, and Debugging Blindness`.
- Highly weight-sensitive (appear in ≤2/5 weight-only profiles): `P04 — Limited Throughput for Privacy-Preserving Rollups`, `P15 — Immature Privacy-Preserving Compliance`.

Most sensitive PIDs (rank / inclusion changes that drive the above categories):
- `P04 — Limited Throughput for Privacy-Preserving Rollups`: appears in the Top 10 only when coordination-weight is high and/or when the under-served crowdedness filter is applied.
- `P15 — Immature Privacy-Preserving Compliance`: present when impact dominates (and in the under-served filtered view), but drops out when tractability or coordination ease dominate (high-impact / high-coordination-burden behavior under pivots).
- `P01 — Transaction Graph Leakage`: present in impact-heavy/balanced/coordination-heavy profiles, but drops out in tractability-heavy and fast-wins, and is also excluded by the under-served crowdedness filter (Crowdedness_Score=Crowded).
- `P14 — Missing Selective-Disclosure Standards`: stable #1 in most profiles, but drops out entirely in the coordination-heavy profile due to high coordination-risk weighting (CoordinationRisk_Score=5 → low CoordinationEase).
- `P11 — Private Execution Leakage in DeFi Primitives`: robust across weight-only profiles, but excluded by the under-served filter because it is tagged Crowded, illustrating that the “avoid crowded areas” assumption can change the Top 10 set even when weights do not.

## 5) EF-fit note

EF-fit ranking outputs exist as a separate lens and should be treated as an overlay for “who can act effectively,” not “what matters most.” Do not merge these into the baseline Top 10s above (Worker 6 will synthesize EF-fit separately).