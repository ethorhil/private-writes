
Phase A mapped the landscape (design patterns, maturity, and recurring problems) without recommending what to build. Phase B turns that descriptive map into **decision support**: it clarifies the main obstacles, provides evidence-backed scoring under multiple prioritization lenses, and produces a short list of uncertainty‑reduction experiments for the next phase. Importantly, Phase B is **non‑prescriptive**: it does not recommend a single technical stack or architecture.

## Key findings 

### 1) The problem space is well described by six recurring themes

We can group the 19 problem briefs from our problem space mapping exercise into six recurring themes (a problem can sit in more than one theme). For each theme, open the problem briefs listed below.

| Cluster label                            | PIDs                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Privacy leakage & anonymity`            | [P01 — Transaction Graph Leakage](<Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage.md>)<br>[P02 — Fragmented Anonymity Sets](<Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>)<br>[P08 — Multi-Key Management Complexity](<Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>)<br>[P11 — Private Execution Leakage in DeFi Primitives](<Supporting Documents/02_PIDs/P11 — Private Execution Leakage in DeFi Primitives.md>)<br>[P13 — Cross-Domain Privacy Leakage in Bridging](<Supporting Documents/02_PIDs/P13 — Cross-Domain Privacy Leakage in Bridging.md>)<br>[P16 — Identity Binding Without Linkability](<Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>)<br>[P19 — Network-Layer Metadata Leakage](<Supporting Documents/02_PIDs/P19 — Network-Layer Metadata Leakage.md>) |
| `Data availability, scalability & exits` | [P03 — High L1 Costs for Private Verification and Data Availability](<Supporting Documents/02_PIDs/P03 — High L1 Costs for Private Verification and Data Availability.md>)<br>[P04 — Limited Throughput for Privacy-Preserving Rollups](<Supporting Documents/02_PIDs/P04 — Limited Throughput for Privacy-Preserving Rollups.md>)<br>[P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)<br>[P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)                                                                                                                                                                                                                                                                                 |
| `Governance & operational risk`          | [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)<br>[P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)<br>[P07 — Upgrade and Governance Risks for Private Circuits](<Supporting Documents/02_PIDs/P07 — Upgrade and Governance Risks for Private Circuits.md>)<br>[P17 — Monitoring, Observability, and Debugging Blindness](<Supporting Documents/02_PIDs/P17 — Monitoring, Observability, and Debugging Blindness.md>)<br>[P18 — Incentive Fragility in Privacy Infrastructure](<Supporting Documents/02_PIDs/P18 — Incentive Fragility in Privacy Infrastructure.md>)                                                                                                                                                     |
| `UX & developer experience`              | [P08 — Multi-Key Management Complexity](<Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>)<br>[P09 — Private Fee Payment and Relayer Friction](<Supporting Documents/02_PIDs/P09 — Private Fee Payment and Relayer Friction.md>)<br>[P10 — Poor Developer Tooling for Private Logic](<Supporting Documents/02_PIDs/P10 — Poor Developer Tooling for Private Logic.md>)<br>[P17 — Monitoring, Observability, and Debugging Blindness](<Supporting Documents/02_PIDs/P17 — Monitoring, Observability, and Debugging Blindness.md>)<br>[P19 — Network-Layer Metadata Leakage](<Supporting Documents/02_PIDs/P19 — Network-Layer Metadata Leakage.md>)                                                                                                                                                                                             |
| `Compliance & selective disclosure`      | [P14 — Missing Selective-Disclosure Standards](<Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>)<br>[P15 — Immature Privacy-Preserving Compliance](<Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>)<br>[P16 — Identity Binding Without Linkability](<Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>)                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `Composability & interoperability`       | [P02 — Fragmented Anonymity Sets](<Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>)<br>[P12 — Lack of Private-to-Private Composability](<Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability.md>)<br>[P13 — Cross-Domain Privacy Leakage in Bridging](<Supporting Documents/02_PIDs/P13 — Cross-Domain Privacy Leakage in Bridging.md>)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

Full theme write‑ups, with evidence pointers and membership, are in [[Clusters Synthesis|Clusters Synthesis]].


### 2) Problem rankings

The [master problem register](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=0#gid=0) provides per‑problem scores and rationales (impact, near‑term feasibility, how crowded the space is, coordination risk, and several “organizational fit” fields). Different summary views combine these fields differently.

A) If you prioritize the biggest blockers regardless of ease (impact‑first), the Top 10 is:
- [P14 — Missing Selective-Disclosure Standards](<Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>)
- [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)
- [P11 — Private Execution Leakage in DeFi Primitives](<Supporting Documents/02_PIDs/P11 — Private Execution Leakage in DeFi Primitives.md>)
- [P01 — Transaction Graph Leakage](<Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage.md>)
- [P15 — Immature Privacy-Preserving Compliance](<Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>)
- [P08 — Multi-Key Management Complexity](<Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>)
- [P10 — Poor Developer Tooling for Private Logic](<Supporting Documents/02_PIDs/P10 — Poor Developer Tooling for Private Logic.md>)
- [P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)
- [P09 — Private Fee Payment and Relayer Friction](<Supporting Documents/02_PIDs/P09 — Private Fee Payment and Relayer Friction.md>)
- [P16 — Identity Binding Without Linkability](<Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>)

B) If you prioritize problems that look both important and plausibly solvable in the next 1–3 years (impact × feasibility), the memo's Top 10 is:
- [P14 — Missing Selective-Disclosure Standards](<Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>)
- [P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)
- [P08 — Multi-Key Management Complexity](<Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>)
- [P09 — Private Fee Payment and Relayer Friction](<Supporting Documents/02_PIDs/P09 — Private Fee Payment and Relayer Friction.md>)
- [P10 — Poor Developer Tooling for Private Logic](<Supporting Documents/02_PIDs/P10 — Poor Developer Tooling for Private Logic.md>)
- [P16 — Identity Binding Without Linkability](<Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>)
- [P01 — Transaction Graph Leakage](<Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage.md>)
- [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)
- [P11 — Private Execution Leakage in DeFi Primitives](<Supporting Documents/02_PIDs/P11 — Private Execution Leakage in DeFi Primitives.md>)
- [P15 — Immature Privacy-Preserving Compliance](<Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>)

C) If you prioritize high‑impact problems that appear under‑served (i.e., not already crowded with mature solutions):

Tier 1 shortlist (very strict under‑served filter):
- [P14 — Missing Selective-Disclosure Standards](<Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>)
- [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)
- [P02 — Fragmented Anonymity Sets](<Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>)
- [P12 — Lack of Private-to-Private Composability](<Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability.md>)

Tier 2 (still under‑served, broader filter; Top 10):
- [P14 — Missing Selective-Disclosure Standards](<Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>)
- [P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)
- [P08 — Multi-Key Management Complexity](<Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>)
- [P10 — Poor Developer Tooling for Private Logic](<Supporting Documents/02_PIDs/P10 — Poor Developer Tooling for Private Logic.md>)
- [P16 — Identity Binding Without Linkability](<Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>)
- [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)
- [P15 — Immature Privacy-Preserving Compliance](<Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>)
- [P02 — Fragmented Anonymity Sets](<Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>)
- [P04 — Limited Throughput for Privacy-Preserving Rollups](<Supporting Documents/02_PIDs/P04 — Limited Throughput for Privacy-Preserving Rollups.md>)
- [P12 — Lack of Private-to-Private Composability](<Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability.md>)

D) If you only consider problems tagged as "critical" for DeFi  the Top 10 is:
- [P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)
- [P09 — Private Fee Payment and Relayer Friction](<Supporting Documents/02_PIDs/P09 — Private Fee Payment and Relayer Friction.md>)
- [P01 — Transaction Graph Leakage](<Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage.md>)
- [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>)
- [P11 — Private Execution Leakage in DeFi Primitives](<Supporting Documents/02_PIDs/P11 — Private Execution Leakage in DeFi Primitives.md>)
- [P03 — High L1 Costs for Private Verification and Data Availability](<Supporting Documents/02_PIDs/P03 — High L1 Costs for Private Verification and Data Availability.md>)
- [P04 — Limited Throughput for Privacy-Preserving Rollups](<Supporting Documents/02_PIDs/P04 — Limited Throughput for Privacy-Preserving Rollups.md>)
- [P07 — Upgrade and Governance Risks for Private Circuits](<Supporting Documents/02_PIDs/P07 — Upgrade and Governance Risks for Private Circuits.md>)
- [P12 — Lack of Private-to-Private Composability](<Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability.md>)
- [P17 — Monitoring, Observability, and Debugging Blindness](<Supporting Documents/02_PIDs/P17 — Monitoring, Observability, and Debugging Blindness.md>)

Across many lenses, two problems show up consistently in the highest‑priority set: [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>) and [P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>). 

The sensitivity analysis explaining what changes (and why) is in [[Supporting Documents/Rankings & Sensitivity Synthesis|Rankings & Sensitivity Synthesis]].

### 3) Some constraints recur across themes

These constraints show up repeatedly across different technical approaches and use-cases. 

- End-to-end unlinkability has to hold at the workflow level (not only "the payload is encrypted"): repeated patterns, boundary touchpoints, and funding/fee behavior can re-create linkability. Related problem briefs: [P01 — Transaction Graph Leakage](<Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage.md>), [P13 — Cross-Domain Privacy Leakage in Bridging](<Supporting Documents/02_PIDs/P13 — Cross-Domain Privacy Leakage in Bridging.md>)
- Network and submission metadata (routing, timing, RPC endpoints, scanning traffic) can deanonymize users even when on-chain data is hidden. Related problem brief: [P19 — Network-Layer Metadata Leakage](<Supporting Documents/02_PIDs/P19 — Network-Layer Metadata Leakage.md>)
- Strong anonymity usually requires aggregation at ecosystem scale; fragmented liquidity/venues/domains shrink the *effective* anonymity set. Related problem brief: [P02 — Fragmented Anonymity Sets](<Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>)
- Multi-step workflows need "private-to-private" composability; missing composability forces public detours or trusted mediation that breaks end-to-end privacy. Related problem briefs: [P12 — Lack of Private-to-Private Composability](<Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability.md>), [P13 — Cross-Domain Privacy Leakage in Bridging](<Supporting Documents/02_PIDs/P13 — Cross-Domain Privacy Leakage in Bridging.md>)
- Under stress (congestion, volatility), throughput and exits become safety-critical. Trust assumptions around data availability (DA) and operators also become binding. Related problem briefs: [P04 — Limited Throughput for Privacy-Preserving Rollups](<Supporting Documents/02_PIDs/P04 — Limited Throughput for Privacy-Preserving Rollups.md>), [P05 — Lack of User-Resilient Exits](<Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>), [P06 — Trust-Heavy DA Committees and Operators](<Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>)
- Selective disclosure / compliance / identity controls must avoid stable long-lived correlators (repeated proofs, key sprawl, revocation flows). Related problem briefs: [P14 — Missing Selective-Disclosure Standards](<Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>), [P15 — Immature Privacy-Preserving Compliance](<Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>), [P16 — Identity Binding Without Linkability](<Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>), [P08 — Multi-Key Management Complexity](<Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>)
- Governance and upgrade processes for privacy-critical circuits/policies can invalidate guarantees if they are opaque or capture-prone. Related problem brief: [P07 — Upgrade and Governance Risks for Private Circuits](<Supporting Documents/02_PIDs/P07 — Upgrade and Governance Risks for Private Circuits.md>)
- Monitoring and debugging needs can conflict with privacy; "observability backdoors" are a recurring risk in complex systems. Related problem brief: [P17 — Monitoring, Observability, and Debugging Blindness](<Supporting Documents/02_PIDs/P17 — Monitoring, Observability, and Debugging Blindness.md>)

### 4) DeFi  workflows change what “privacy” needs to mean

This project treats “private transfers” as the baseline, and then uses DeFi-like workflows as a stress test. The key idea is that privacy requirements change when users execute multi-step financial workflows rather than a single transfer.

In the DeFi stress test framing:

- Privacy is evaluated across repeated, multi-write workflows (position/workflow privacy), so repeated motifs and infrastructure reuse become major correlation channels.
- Privacy often breaks at boundaries (apps, bridges, shield/unshield operations). That makes private-to-private composability and boundary privacy gating constraints.
- Shared-state leakage becomes central: many DeFi functions require public or provable global signals (prices, utilization, liquidations), leaving residual leakage even with private execution.
- Cost-per-write and throughput constraints tighten: DeFi writes can be heavier and more frequent than transfers, and stress bursts amplify proof/DA overhead.
- Stress-mode liveness and exits become direct safety requirements: inability to exit or close positions quickly under volatility can create time-bounded financial loss.
- Selective disclosure and eligibility checks become lifecycle constraints; repeated proof patterns and key management can become stable identifiers if not designed carefully.
- Operability (monitoring, audit, upgrades) becomes a safety constraint and must be handled without creating privacy bypasses.

Detailed mapping and checklist lives in [[DeFi delta mapping]].