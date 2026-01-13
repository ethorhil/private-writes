
## Cluster: `Privacy leakage & anonymity`

This cluster covers how privacy degrades in practice beyond the core cryptography: graph-level inference, anonymity-set weakness, and metadata leakage that allow observers to link actions to the same entity or workflow. It includes both on-chain and off-chain correlators (transaction motifs, routing metadata) as well as cross-domain boundary effects when users move between domains. Several PIDs in this cluster are “system property” issues: they arise from user behavior, infrastructure, and market structure, not just protocol correctness. Under DeFi-shaped workflows, richer motifs and shared-state dependencies tend to amplify these leakages and tighten real-world success thresholds.

### PIDs in cluster

#### P01 — Transaction Graph Leakage

What it is: Practical linkability persists even when payloads/state are cryptographically shielded: amounts, timing, interaction motifs, relayer behavior, and cross-domain touchpoints can allow observers to reconstruct partial transaction graphs and cluster activity.

Why it matters: If observers can reliably connect actions to the same entity, the privacy claim degrades quickly—especially in DeFi-shaped workflows where repeated motifs and composability create strong graph signals.

Evidence pointers: [P01 — Transaction Graph Leakage](<Human Readable/Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage.md>) (§2.1 Problem; §2.2 Why it matters; §2.4 System / pattern context).

#### P02 — Fragmented Anonymity Sets

What it is: Anonymity sets fragment across pools, assets, chains, and venues, producing small “effective” anonymity sets for many users and making behavior easier to fingerprint.

Why it matters: Fragmentation pushes privacy toward a two-tier outcome (a few large sets vs many weak sets) and is amplified for DeFi users who need specific assets/markets and cannot always select the single largest set.

Evidence pointers: [P02 — Fragmented Anonymity Sets](<Human Readable/Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>) (§2.1 Problem; §2.2 Why it matters; §2.4 System / pattern context).

#### P08 — Multi-Key Management Complexity

What it is: Private systems often require multiple keys and private state management (spend/view keys, delegation, recovery), creating user confusion, custody pressure, and accidental disclosure risk.

Why it matters: Key management failures can cause irreversible loss or privacy compromise, and UX coping strategies (delegation, reuse patterns) can become stable correlators that silently degrade unlinkability.

Evidence pointers: [P08 — Multi-Key Management Complexity](<Human Readable/Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>) (§1.1 Problem overview (tl;dr); §1.3 Why it matters (impact)).

#### P11 — Private Execution Leakage in DeFi Primitives

What it is: Even with private execution, DeFi primitives can leak through shared-state signals (prices, interest rates, liquidation events) and market dynamics, so “local” shielding does not guarantee workflow privacy.

Why it matters: This determines whether privacy substrates can support meaningful DeFi workloads; leakage can enable strategy inference and MEV-like harms even when transactions are individually private.

Evidence pointers: [P11 — Private Execution Leakage in DeFi Primitives](<Human Readable/Supporting Documents/02_PIDs/P11 — Private Execution Leakage in DeFi Primitives.md>) (§1.1 Problem overview (tl;dr); §1.3 Why it matters (impact)).

#### P13 — Cross-Domain Privacy Leakage in Bridging

What it is: Cross-domain moves (bridging, wrap/unwrap, private↔public boundaries) create timing/amount/wrapper fingerprints that allow observers to link activity across domains, collapsing end-to-end privacy.

Why it matters: Real users and DeFi workflows frequently cross domains; boundary leakage can be the dominant deanonymization vector even when each domain is locally private.

Evidence pointers: [P13 — Cross-Domain Privacy Leakage in Bridging](<Human Readable/Supporting Documents/02_PIDs/P13 — Cross-Domain Privacy Leakage in Bridging.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P16 — Identity Binding Without Linkability

What it is: Binding identity/eligibility attributes to actions without creating linkability is difficult: repeated checks, revocation/rotation, and policy enforcement can introduce stable correlators (“pseudonyms”).

Why it matters: Institutional and regulated workflows require eligibility controls; if identity binding becomes linkable, privacy collapses for the very user segments most likely to demand these controls.

Evidence pointers: [P16 — Identity Binding Without Linkability](<Human Readable/Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P19 — Network-Layer Metadata Leakage

What it is: Network-layer metadata (RPC endpoint choice, timing, routing, client fingerprints) can correlate users with private actions, defeating privacy “outside the cryptographic layer.”

Why it matters: If network metadata is linkable, privacy guarantees can fail systematically, particularly for urgent/time-sensitive workflows and when users rely on common infrastructure providers.

Evidence pointers: [P19 — Network-Layer Metadata Leakage](<Human Readable/Supporting Documents/02_PIDs/P19 — Network-Layer Metadata Leakage.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

### What gates progress across patterns

- Practical unlinkability depends on controlling non-payload observables (amount/timing/motifs, relayer behavior, boundary touchpoints); without that, `L1 Overlay – Stealth  OTR` and `Burn-and-Mint Privacy` remain linkable in practice (P01; see binding matrix and longform).
- Network-layer metadata and RPC/relay routing can recreate linkability outside the on-chain payload, gating overlay-style and burn-and-mint workflows even when cryptography is sound (P19).
- Large shared anonymity sets are a precondition for meaningful privacy; fragmentation across pools/assets/domains creates small effective sets and uneven guarantees, gating `L1 Shielded Pools` and `Burn-and-Mint Privacy` (P02).
- Key-management and delegation patterns can become stable correlators (who holds view keys, recovery and delegation workflows), gating adoption and raising silent linkability risk for overlays and pools (P08).
- DeFi-shaped workflows introduce rich, repeated motifs and shared-state signals; “local” transaction privacy does not imply workflow privacy, tightening success thresholds for private DeFi (P11; and graph linkage via P01).
- Cross-domain boundary events (bridge in/out, wrap/unwrap, domain transitions) are high-leakage points; they gate end-to-end privacy for cross-domain patterns and for private rollups’ boundary workflows (P13).
- Identity/eligibility requirements can force repeated checks or stable identifiers; this gates regulated/privacy-with-controls workflows and creates a persistent tradeoff between enforceability and unlinkability (P16).
- Cross-cutting tradeoff: strengthening privacy typically increases operational burdens (routing hygiene, key handling, workflow constraints), and those burdens feed back into privacy via user behavior and infrastructure reliance (P08, P19).

## Cluster: `Data availability, scalability & exits`

This cluster focuses on data placement and capacity constraints that determine whether privacy systems can be safe and usable at scale, especially under failure or stress. It includes L1 cost floors for private verification and data publication, throughput limits for privacy-preserving rollups, and the availability of credible user-resilient exits. The cluster also captures the central tradeoff between moving data off-chain (to reduce costs/increase throughput) and the resulting trust and availability dependencies on operators/committees. For DeFi-grade safety, these constraints tend to surface in “stress mode” (congestion, volatility), when exit and inclusion capacity become adoption-critical.

### PIDs in cluster

#### P03 — High L1 Costs for Private Verification and Data Availability

What it is: Verifying privacy proofs and providing the necessary data availability on L1 can impose high cost floors, which constrains throughput and prices many users/workflows out of privacy-preserving systems.

Why it matters: High costs directly reduce adoption and composability, and they create pressure toward “shortcuts” that often increase trust assumptions or weaken safety guarantees.

Evidence pointers: [P03 — High L1 Costs for Private Verification and Data Availability](<Human Readable/Supporting Documents/02_PIDs/P03 — High L1 Costs for Private Verification and Data Availability.md>) (§2.1 Problem; §2.2 Why it matters).

#### P04 — Limited Throughput for Privacy-Preserving Rollups

What it is: Privacy-preserving rollups often face throughput and latency limits driven by heavy proving workloads, batching constraints, data availability overhead, and sequencer operation limits.

Why it matters: Throughput constraints are especially punitive for DeFi-grade workloads (latency/volume sensitive) and become systemic during stress events, affecting safety and user experience.

Evidence pointers: [P04 — Limited Throughput for Privacy-Preserving Rollups](<Human Readable/Supporting Documents/02_PIDs/P04 — Limited Throughput for Privacy-Preserving Rollups.md>) (§2.1 Problem; §2.2 Why it matters).

#### P05 — Lack of User-Resilient Exits

What it is: Users may lack credible, practical exit paths when operators fail, censor, or go offline; even when exits exist “on paper,” user burden, timing, and cost can make them non-resilient in practice.

Why it matters: Exit fragility undermines funds safety and trust, and under DeFi stress it can propagate risk (e.g., inability to unwind positions or respond to volatility) beyond the private system itself.

Evidence pointers: [P05 — Lack of User-Resilient Exits](<Human Readable/Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>) (§2.1 Problem; §2.2 Why it matters).

#### P06 — Trust-Heavy DA Committees and Operators

What it is: Many scalability/privacy approaches rely on trusted DA committees or privileged operators; those roles become safety dependencies (for verification/exits) and can also form confidentiality and censorship/coercion choke points.

Why it matters: When DA or operator trust is central, both safety and privacy become contingent on governance and real-world pressure resistance—especially in plasma/validium-like designs and permissioned instantiations.

Evidence pointers: [P06 — Trust-Heavy DA Committees and Operators](<Human Readable/Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>) (§2.1 Problem; §2.2 Why it matters).

### What gates progress across patterns

- L1 cost floors for proof verification and data publication constrain throughput and set minimum fees; they gate `L1 Shielded Pools` and `Private Rollups (Full DA)` viability at adoption-grade usage (P03; see binding longform).
- Pressure to reduce L1 costs/DA load can shift trust assumptions to off-chain roles; this is a core tradeoff between cost/throughput and trust/coercion resistance (P03 ↔ P06).
- Throughput limits in privacy-preserving rollups (proving + DA + sequencing) can become systemic UX and safety constraints under congestion/stress, gating `Private Rollups (Full DA)` as a DeFi-capable substrate (P04).
- User-resilient exits require not just formal correctness but realistic user ability (or safe delegation) to respond under stress; exit designs that are sound in theory can be non-resilient in practice (P05).
- Off-chain DA availability is a prerequisite for verification and exits; committees/operators become safety dependencies and privacy boundaries, especially for plasma/validium-like designs (P06).
- Mass-exit feasibility ties DA and L1 capacity to safety: if many users need to exit simultaneously, DA and fee constraints can make exits impractical, tightening requirements for systems that depend on them (P05, P03).
- DeFi stress mode tightens requirements: volatility concentrates demand for throughput and exits, making DA and L1 inclusion capacity first-class constraints rather than tail risks (P04, P05, P03).
- Cross-cutting tradeoff: moving data off-chain can improve performance but increases coordination and operational risk; assumptions must be explicit to avoid silently weakening safety guarantees (P06).

## Cluster: `Governance & operational risk`

This cluster groups problems around control over upgrades, operations, observability, and incentives—areas where failures can silently undermine safety or privacy even if cryptography is sound. It includes operator/committee trust dependencies, governance and upgrade risks for privacy-critical circuits, monitoring/observability limits, and incentive fragility in required infrastructure roles. The shared gating issue is that many privacy systems introduce privileged or always-on roles and opaque logic, which concentrates risk and makes failures harder to diagnose and recover from. Progress is constrained by the ability to manage these operational surfaces without creating coercion points or forcing users into non-resilient assumptions.

### PIDs in cluster

#### P05 — Lack of User-Resilient Exits

What it is: Users may lack credible, practical exit paths when operators fail, censor, or go offline; even when exits exist “on paper,” user burden, timing, and cost can make them non-resilient in practice.

Why it matters: Exit fragility undermines funds safety and trust, and under DeFi stress it can propagate risk (e.g., inability to unwind positions or respond to volatility) beyond the private system itself.

Evidence pointers: [P05 — Lack of User-Resilient Exits](<Human Readable/Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits.md>) (§2.1 Problem; §2.2 Why it matters).

#### P06 — Trust-Heavy DA Committees and Operators

What it is: Many scalability/privacy approaches rely on trusted DA committees or privileged operators; those roles become safety dependencies (for verification/exits) and can also form confidentiality and censorship/coercion choke points.

Why it matters: When DA or operator trust is central, both safety and privacy become contingent on governance and real-world pressure resistance—especially in plasma/validium-like designs and permissioned instantiations.

Evidence pointers: [P06 — Trust-Heavy DA Committees and Operators](<Human Readable/Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators.md>) (§2.1 Problem; §2.2 Why it matters).

#### P07 — Upgrade and Governance Risks for Private Circuits

What it is: Upgrading private circuits/provers and related protocol logic introduces governance and operational risk: changes can break correctness or privacy, are hard to audit quickly, and concentrate power in upgrade controllers.

Why it matters: Opaque or captured upgrades can cause catastrophic regressions and fragment ecosystems; credible, trust-preserving upgrade processes are therefore a gating dependency for privacy infrastructure.

Evidence pointers: [P07 — Upgrade and Governance Risks for Private Circuits](<Human Readable/Supporting Documents/02_PIDs/P07 — Upgrade and Governance Risks for Private Circuits.md>) (§1.1 Problem overview (tl;dr); §1.3 Why it matters (impact); (see also §1.2 Stakeholders & pain)).

#### P17 — Monitoring, Observability, and Debugging Blindness

What it is: Privacy-preserving systems are intrinsically harder to monitor and debug: reduced visibility impairs incident detection, root-cause analysis, and user support for both operators and developers.

Why it matters: Operational blindness increases failure risk and can motivate “workarounds” (privileged dashboards, key-sharing) that undermine privacy boundaries and centralize trust.

Evidence pointers: [P17 — Monitoring, Observability, and Debugging Blindness](<Human Readable/Supporting Documents/02_PIDs/P17 — Monitoring, Observability, and Debugging Blindness.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P18 — Incentive Fragility in Privacy Infrastructure

What it is: Privacy infrastructure depends on auxiliary roles (relayers, provers, committees, watchers) whose incentives may be fragile; if underprovided or centralized, liveness and reliability degrade.

Why it matters: Unreliable or concentrated infrastructure creates censorship and correlation choke points and compounds trust assumptions, especially under fee spikes or dispute/stress conditions.

Evidence pointers: [P18 — Incentive Fragility in Privacy Infrastructure](<Human Readable/Supporting Documents/02_PIDs/P18 — Incentive Fragility in Privacy Infrastructure.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

### What gates progress across patterns

- Privileged operator/committee roles create capture and coercion surfaces; safety and confidentiality become contingent on real-world pressure resistance, gating permissioned, plasma, and validium-like instantiations (P06, P18).
- Upgrades to privacy-critical circuits and protocol logic are high-stakes; governance agility conflicts with auditability and credible non-regression, gating `Permissioned Privacy` and `Private Validium` (P07; see binding longform).
- User-resilient exits are the backstop when operations fail; without credible, practical exits, “trust-minimized” posture erodes under stress (P05).
- Incentive fragility in auxiliary infrastructure (relayers, watchers, DA providers) can create persistent chokepoints and correlation surfaces, gating overlays and off-chain DA patterns especially during fee spikes or disputes (P18).
- Monitoring/observability limits increase operational risk and can drive privileged monitoring or key-sharing; this creates a tradeoff between accountability and preserving privacy boundaries (P17).
- Governance/ops often require multi-party coordination (integrators, wallets, DA providers); failure to coordinate upgrades or incident response can fragment deployments and reduce verifiability (P07, P18).
- Cross-cutting tradeoff: stronger decentralization can increase operational complexity (harder monitoring, more actors), while centralized operations simplify response but raise capture and privacy-boundary risks (P06, P17, P18).
- Stress events are governance tests: downtime, censorship, or urgent fixes under volatility can force exceptional procedures, exposing brittle governance and incentive arrangements (P05, P07, P18).

## Cluster: `UX & developer experience`

This cluster captures the user-facing and builder-facing friction that determines whether privacy systems can be adopted and safely integrated. It includes multi-key/private-state management burdens, private fee payment and relayer friction, developer tooling gaps, observability/debugging blindness, and network-layer metadata leakage. These issues are often “second-order” but become first-order in practice because they drive user coping strategies (custody, shared infrastructure) that can reintroduce privacy leakage and centralization risk. As a result, progress across multiple patterns is gated by usability and tooling constraints as much as by protocol primitives.

### PIDs in cluster

#### P08 — Multi-Key Management Complexity

What it is: Private systems often require multiple keys and private state management (spend/view keys, delegation, recovery), creating user confusion, custody pressure, and accidental disclosure risk.

Why it matters: Key management failures can cause irreversible loss or privacy compromise, and UX coping strategies (delegation, reuse patterns) can become stable correlators that silently degrade unlinkability.

Evidence pointers: [P08 — Multi-Key Management Complexity](<Human Readable/Supporting Documents/02_PIDs/P08 — Multi-Key Management Complexity.md>) (§1.1 Problem overview (tl;dr); §1.3 Why it matters (impact)).

#### P09 — Private Fee Payment and Relayer Friction

What it is: Private transactions still require fee payment; paying from public addresses or relying on relayers can reintroduce linkability and adds friction, trust dependencies, and censorship/availability risks.

Why it matters: If fee payment is not private and reliable, private workflows become either linkable or unusable, and relayer/RPC infrastructure can become an operational choke point.

Evidence pointers: [P09 — Private Fee Payment and Relayer Friction](<Human Readable/Supporting Documents/02_PIDs/P09 — Private Fee Payment and Relayer Friction.md>) (§1.1 Problem overview (tl;dr); §1.3 Why it matters (impact)).

#### P10 — Poor Developer Tooling for Private Logic

What it is: Developer tooling for private logic (circuits/private contracts/provers) is fragmented and immature: debugging, testing, auditing, and iteration are harder than for conventional smart contracts.

Why it matters: Tooling gaps raise cost and error rates; bugs can compromise privacy or soundness, slowing ecosystem progress across multiple patterns and increasing operational risk.

Evidence pointers: [P10 — Poor Developer Tooling for Private Logic](<Human Readable/Supporting Documents/02_PIDs/P10 — Poor Developer Tooling for Private Logic.md>) (§1.1 Problem overview (tl;dr); §1.3 Why it matters (impact)).

#### P17 — Monitoring, Observability, and Debugging Blindness

What it is: Privacy-preserving systems are intrinsically harder to monitor and debug: reduced visibility impairs incident detection, root-cause analysis, and user support for both operators and developers.

Why it matters: Operational blindness increases failure risk and can motivate “workarounds” (privileged dashboards, key-sharing) that undermine privacy boundaries and centralize trust.

Evidence pointers: [P17 — Monitoring, Observability, and Debugging Blindness](<Human Readable/Supporting Documents/02_PIDs/P17 — Monitoring, Observability, and Debugging Blindness.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P19 — Network-Layer Metadata Leakage

What it is: Network-layer metadata (RPC endpoint choice, timing, routing, client fingerprints) can correlate users with private actions, defeating privacy “outside the cryptographic layer.”

Why it matters: If network metadata is linkable, privacy guarantees can fail systematically, particularly for urgent/time-sensitive workflows and when users rely on common infrastructure providers.

Evidence pointers: [P19 — Network-Layer Metadata Leakage](<Human Readable/Supporting Documents/02_PIDs/P19 — Network-Layer Metadata Leakage.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

### What gates progress across patterns

- Multi-key and private state lifecycle complexity creates user burden and accidental disclosure risk, gating overlay and shielded pool usability and increasing silent linkability via coping strategies (P08).
- Private fee payment and relayer dependencies can recreate linkability (public fee funding) and add censorship/availability risk and UX friction; this gates overlays, pools, and burn-and-mint workflows (P09; see binding longform).
- Network-layer submission metadata can defeat privacy even when payloads are private; it gates overlay-style and burn-and-mint workflows and is amplified by reliance on shared RPC/relay infrastructure (P19).
- Developer tooling gaps slow iteration and increase errors in private logic; this gates progress across patterns by raising the cost of safely building and maintaining privacy-preserving applications (P10).
- Observability/debugging blindness makes privacy systems harder to operate safely; remediation often trades off privacy boundaries vs operational transparency, affecting confidence in deployments (P17).
- UX constraints can force centralization (custodial wallets, hosted RPCs, privileged support flows) to manage complexity; this increases correlated risk and can reintroduce leakage surfaces (P08, P09, P17, P19).
- Builder-facing fragmentation (toolchains and interfaces) increases integration costs and inconsistent UX, which can compound anonymity-set fragmentation and slow ecosystem convergence (P10; cross-cluster linkage to P02).
- Cross-cutting tradeoff: usability improvements often introduce new infrastructure dependencies (relayers, wallets, monitoring) that must be accounted for as new trust and metadata surfaces (P09, P17, P19).

## Cluster: `Compliance & selective disclosure`

This cluster covers the gap between privacy systems and real-world regulatory/institutional requirements: being able to selectively disclose relevant facts, support compliance workflows, and bind identity/eligibility attributes without creating linkability. It includes missing selective-disclosure standards, immature privacy-preserving compliance mechanisms, and identity binding without linkability. In the pattern binding matrix these are highlighted most strongly for `Permissioned Privacy`, but the same constraints tend to recur whenever other patterns engage regulated venues or institutional users. The central tradeoff is between enforceability (eligibility, reporting) and maintaining unlinkability across repeated, real-world workflows.

### PIDs in cluster

#### P14 — Missing Selective-Disclosure Standards

What it is: Selective disclosure lacks broadly adopted standards and profiles (what to prove/reveal, how to represent claims, and how to interoperate), pushing ecosystems toward bespoke disclosure implementations.

Why it matters: Without standards, disclosure often becomes over-disclosure or inconsistent, increasing integration cost and accidental deanonymization risk—especially when disclosure is required repeatedly.

Evidence pointers: [P14 — Missing Selective-Disclosure Standards](<Human Readable/Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P15 — Immature Privacy-Preserving Compliance

What it is: Privacy-preserving compliance mechanisms are immature and inconsistent; available approaches often require tradeoffs that either weaken privacy or fail to satisfy operational/regulatory requirements.

Why it matters: Compliance requirements can become the dominant adoption blocker; immature compliance hooks can drive fragmentation into silos and can introduce stable identifiers or monitoring surfaces that degrade privacy.

Evidence pointers: [P15 — Immature Privacy-Preserving Compliance](<Human Readable/Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P16 — Identity Binding Without Linkability

What it is: Binding identity/eligibility attributes to actions without creating linkability is difficult: repeated checks, revocation/rotation, and policy enforcement can introduce stable correlators (“pseudonyms”).

Why it matters: Institutional and regulated workflows require eligibility controls; if identity binding becomes linkable, privacy collapses for the very user segments most likely to demand these controls.

Evidence pointers: [P16 — Identity Binding Without Linkability](<Human Readable/Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

### What gates progress across patterns

- Without shared selective-disclosure standards and profiles, integrators tend to resort to bespoke disclosure flows; this raises integration costs and increases over-disclosure and accidental linkability risk (P14; gates `Permissioned Privacy` in the binding matrix).
- Privacy-preserving compliance mechanisms are immature and vary by jurisdiction/venue; uncertainty around required controls can block adoption or drive fragmentation into siloed deployments (P15).
- Identity/eligibility binding often requires repeated checks and revocation/rotation; if these introduce stable identifiers, privacy collapses for regulated workflows, creating a persistent tradeoff between enforceability and unlinkability (P16).
- Even when proofs are “zero-knowledge,” operational metadata and policy enforcement can reintroduce correlation; compliance designs must manage both proof semantics and workflow-level linkability (P14–P16).
- Selective disclosure often occurs at boundaries (exchanges, bridges, institutional venues); repeated boundary disclosures can become link points if not carefully scoped, intersecting with cross-domain leakage (P14, P16; cross-cluster with P13).
- Cross-pattern applicability: the pattern binding matrix surfaces these PIDs as top constraints for `Permissioned Privacy`, but similar constraints tend to surface whenever other patterns engage regulated venues or institutional users (P14–P16).
- Tradeoff axis: minimizing disclosure vs meeting policy needs can shift risk between non-adoption (under-disclosure) and systematic linkability (over-disclosure), and the balance is context-specific (P14, P15).

### Expert deep-dive entry points

- Canonical cluster mapping: [sprint4_problem_register_extended.csv](<../../4/sprint4_problem_register_extended.csv>) (column `Cluster_Labels`) using locked labels from [Locked strings lockfile.md](<../../2/Locked strings lockfile.md>).
- Cross-pattern gating context: [Pattern PID binding matrix.md](<../../4/Pattern PID binding matrix.md>) and [pattern_pid_binding_longform.csv](<../../4/_outputs/pattern_pid_binding_longform.csv>) (filter `PID_ID` in {P14, P15, P16} and/or `Pattern_Name` in {Permissioned Privacy}).
- PID one-pagers (cluster members): [P14 — Missing Selective-Disclosure Standards](<Human Readable/Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards.md>); [P15 — Immature Privacy-Preserving Compliance](<Human Readable/Supporting Documents/02_PIDs/P15 — Immature Privacy-Preserving Compliance.md>); [P16 — Identity Binding Without Linkability](<Human Readable/Supporting Documents/02_PIDs/P16 — Identity Binding Without Linkability.md>).

## Cluster: `Composability & interoperability`

This cluster addresses the difficulty of composing private systems with each other and with public DeFi, across assets and domains, without collapsing privacy. It includes fragmentation of anonymity sets across venues, lack of private-to-private composability (forcing de-shielding or trusted mediation), and cross-domain privacy leakage in bridging. The shared gating issue is that real user workflows are multi-protocol and cross-domain, so boundaries and interface mismatches become dominant leakage and usability drivers. Progress is constrained by both technical interoperability and ecosystem coordination dynamics that determine whether privacy guarantees can survive end-to-end workflows.

### PIDs in cluster

#### P02 — Fragmented Anonymity Sets

What it is: Anonymity sets fragment across pools, assets, chains, and venues, producing small “effective” anonymity sets for many users and making behavior easier to fingerprint.

Why it matters: Fragmentation pushes privacy toward a two-tier outcome (a few large sets vs many weak sets) and is amplified for DeFi users who need specific assets/markets and cannot always select the single largest set.

Evidence pointers: [P02 — Fragmented Anonymity Sets](<Human Readable/Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets.md>) (§2.1 Problem; §2.2 Why it matters; §2.4 System / pattern context).

#### P12 — Lack of Private-to-Private Composability

What it is: Private systems often cannot compose privately with other private contracts/systems; heterogeneous interfaces and proof/encryption formats prevent atomic private-to-private workflows without declassification or trusted mediation.

Why it matters: Composability is a core driver of on-chain utility; when private-to-private composition fails, multi-step workflows collapse into silos or require “break glass” steps that defeat end-to-end privacy.

Evidence pointers: [P12 — Lack of Private-to-Private Composability](<Human Readable/Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

#### P13 — Cross-Domain Privacy Leakage in Bridging

What it is: Cross-domain moves (bridging, wrap/unwrap, private↔public boundaries) create timing/amount/wrapper fingerprints that allow observers to link activity across domains, collapsing end-to-end privacy.

Why it matters: Real users and DeFi workflows frequently cross domains; boundary leakage can be the dominant deanonymization vector even when each domain is locally private.

Evidence pointers: [P13 — Cross-Domain Privacy Leakage in Bridging](<Human Readable/Supporting Documents/02_PIDs/P13 — Cross-Domain Privacy Leakage in Bridging.md>) (§2.2 Problem statement (Definition; Why it matters); §2.5 Binding constraints by pattern).

### What gates progress across patterns

- Fragmented anonymity sets across pools/assets/domains reduce effective privacy and can make matching attacks easier at boundaries, gating shielded pools and burn-and-mint deployments (P02; see binding longform).
- Without private-to-private composability, workflows must declassify data, exit/de-shield, or rely on trusted intermediaries; this collapses privacy for multi-step workflows and gates pools, rollups, and plasma-like designs (P12).
- Cross-domain bridging creates timing/amount/wrapper fingerprints that link flows; it is a primary gate for burn-and-mint privacy and a meaningful boundary risk for private rollups’ end-to-end privacy (P13).
- Heterogeneous interfaces and proof/encryption formats increase interoperability friction; this increases user/builder burden and entrenches silos, reinforcing fragmentation (P12 ↔ P02).
- Boundary events (bridge in/out, exit workflows) are repeated link points; low-volume regimes and urgent actions (especially in stress conditions) tighten unlinkability thresholds (P13; cross-cluster linkage to P05 and P11).
- Composability pressures often create coordination surfaces (shared primitives, interface convergence); progress can stall on ecosystem alignment even when local mechanisms exist (P12, P02).
- Tradeoff axis: broader interoperability expands the leakage surface (more touchpoints and boundary conditions) unless correlation risks are managed as first-class constraints (P13, P02).
