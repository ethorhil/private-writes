
## 6.1 Problem Catalog Overview

Phase A complements the pattern-level comparison (Section 5) with a **cross-pattern problem catalog**: a list of structural issues that show up repeatedly across multiple mechanisms, regardless of which pattern is used.

[[Appendix C — Global Problem Catalog & Radar]] identifies **19 problems**, each assigned to one or more thematic categories.

These problems are **explicitly cross-pattern**: they show up in different forms across L1 overlays, shielded pools, private rollups, Plasma, Validium, and permissioned systems, rather than being tied to a single mechanism family.

---

## 6.2 Problem Clusters

Section 10.3 groups the catalog into a set of **structural clusters**, each describing a recurring theme that cuts across multiple patterns and projects.

### 6.2.1 Privacy Leakage & Anonymity

This cluster covers how privacy can degrade **beyond the cryptography of the core protocol**:

- [[01 Transaction Graph Leakage]] (1)
- [[02 Fragmented Anonymity Sets]] (2)
- [[11 Private Execution Leakage in DeFi Primitives]] (11)
- [[13 Cross-Domain Privacy Leakage in Bridging]] (13)
- [[16 Identity Binding Without Linkability]] (16)
- [[19 Network-Layer Metadata Leakage]] (19)

Even when sender, receiver, and amount are cryptographically shielded, **timing, routing, liquidity fragmentation, and network behavior** can reintroduce linkability. The catalog treats this as a structural issue: solving privacy at the state layer alone is insufficient.

### 6.2.2 Data Availability, Scalability & Exits

This cluster focuses on **data placement and safety under failure**:
- [[03 High L1 Costs for Private Verification and Data Availability]] (3)
- [[04 Limited Throughput for Privacy-Preserving Rollups]] (4)
- [[05 Lack of User-Resilient Exits]] (5)
- [[06 Trust-Heavy DA Committees and Operators]] (6)

Private systems face a persistent tension between **L1 costs, throughput, and safety**:
- L1-native designs are costly and throughput-constrained.
- Off-chain DA improves throughput but introduces exit fragility and DA trust assumptions.

The catalog identifies this as one of the central structural trade-offs in the private-transfer landscape.

### 6.2.3 Governance & Operational Risk

Here section 10.3 groups issues around **control over upgrades, operations, and incentives**:
- [[07 Upgrade and Governance Risks for Private Circuits]] (7)
- [[17 Monitoring, Observability, and Debugging Blindness]] (17)
- [[18 Incentive Fragility in Privacy Infrastructure]] (18)

Because much of the system logic is opaque, **circuit upgrades, operator behavior, and infra incentives** carry outsized systemic risk. Lack of safe observability makes these risks harder to detect and manage.

### 6.2.4 UX & Developer Experience

This cluster addresses the **human-facing and builder-facing friction**:
- [[08 Multi-Key Management Complexity]] (8)
- [[09 Private Fee Payment and Relayer Friction]] (9)
- [[10 Poor Developer Tooling for Private Logic]] (10)
- Monitoring and debugging challenges (17, also in governance)

Many patterns impose **non-standard mental models and responsibilities** on users (multiple keys, note management, exit actions) and on developers (limited tooling, opaque debugging). These UX/DevEx frictions are treated as first-class structural problems, not just “polish issues”.

### 6.2.5 Compliance & Selective Disclosure

This cluster captures the gap between **privacy and real-world regulatory requirements**:
- [[14 Missing Selective-Disclosure Standards]] (14)
- [[15 Immature Privacy-Preserving Compliance]] (15)
- [[16 Identity Binding Without Linkability]] (16)

Across patterns, there is no widely adopted way to express **proofs-of-innocence, audit trails, or role-based disclosure policies**. Permissioned privacy deployments partially address this for specific use cases, but the catalog treats the broader absence of shared standards as a cross-ecosystem problem.

### 6.2.6 Composability & Interoperability

Finally, section 10.3 identifies a cluster around **composing private systems with each other and with public DeFi**:

- [[02 Fragmented Anonymity Sets]] (2)
- [[12 Lack of Private-to-Private Composability]] (12)
- [[13 Cross-Domain Privacy Leakage in Bridging]] (13)

Even when individual systems provide strong local privacy, **composing them often reintroduces leakage**—for example, when bridging between chains, interacting with public AMMs, or chaining private applications. The catalog treats this as a structural friction in moving from isolated private silos to a coherent private DeFi stack.

---

## 6.3 Impact–Tractability–Crowdedness Radar

To complement the qualitative catalog, section 10.3 introduces an **Impact–Tractability–Crowdedness “problem radar”** that positions each problem in a three-dimensional descriptive space.

```text
[Figure 3: Global Problem Radar — Impact × Tractability × Crowdedness]
````

### 6.3.1 Dimensions of the Radar

Each problem is scored along:

- **Impact (1–5)**  
    _Question:_ _If this problem were meaningfully mitigated, how much would it change the private-transfer ecosystem?_
    
- **Tractability (1–5)**  
    _Question:_ _Is meaningful progress on this problem feasible over roughly a 1–3 year horizon, given realistic resources and ecosystem constraints?_
    
- **Crowdedness**  
    Categorical indicator of how much existing work is focused on the problem: **Many teams / Medium / Sparse / Unclear**.
    

The radar arranges problems so that readers can **visually compare structural issues**, not just list them.

### 6.3.2 Descriptive Role in Phase A

In **Phase A**, the radar is explicitly:

- **Descriptive, not prescriptive.**  
    It summarizes how the current research and builder ecosystem is distributed across structural problems, without deciding which problems “should” be worked on first.
- **Cross-pattern.**  
    It focuses on issues that cut across multiple patterns (e.g., DA and exit risk, metadata leakage) rather than pattern-specific bugs or implementation details. 
- **An input to later discussion, not a prioritization.**  
    It provides a **structured snapshot** that Phase B and other tracks can use when asking questions like “which structural problems matter most for us?” or “where is the ecosystem already crowded?”. Those questions are **explicitly out-of-scope** for Phase A and are revisited only as Phase B inputs (Section 9).

As with the comparison table in section 10.2, the radar should be read as a **frozen, time-bounded view** of the ecosystem at the moment of analysis, not as a permanent classification.