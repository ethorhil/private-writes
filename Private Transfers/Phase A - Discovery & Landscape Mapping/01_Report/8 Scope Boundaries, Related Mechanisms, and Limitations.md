
## 8.1 Related Mechanisms Not Scored

Phase A explicitly **focuses on seven transfer‑centric patterns** that define how private balances are represented and how data availability and correctness are enforced. Several closely related mechanism families are **acknowledged but not scored as patterns**, because they operate at different layers or provide general private compute rather than a dedicated private‑transfer state model.

### General Private Compute / Private VMs

Systems based on **FHE, iO, or similar private VM paradigms** enable arbitrary private computation. Private transfers are just one possible application on these platforms. In Phase A they are treated as **general‑purpose private compute infrastructure**, not as transfer patterns.

Many of the seven patterns—especially **Private Rollups**, **Private Validium**, and **Private Plasma**—could be instantiated on top of such VMs, but the underlying transfer semantics still match one of those patterns.

### TEE- and MPC-Based Private Execution

Systems that execute private logic inside **trusted hardware enclaves (TEEs)** or **MPC committees** follow the same broad “off‑chain private execution with on‑chain attestation” paradigm as zk-based systems, but introduce different trust anchors (hardware vendors, committee composition). Mechanistically they often resemble **Rollup-, Validium-, or Plasma-like semantics** with alternate execution security models.

For Phase A, they are treated as **execution-model variants**, not separate private‑transfer patterns.

### Transaction Submission & Ordering Privacy

Mechanisms like **encrypted mempools, threshold-encrypted transaction pools, and orderflow protection** hide how transactions are routed and ordered, not how balances are represented in state. Any of the seven patterns can underlie them.

These designs are part of a distinct **Privacy of Reads track** and are therefore **not scored as private‑transfer patterns** in Phase A.

### Identity & Credential Systems

**zk-credential systems, anonymous credentials, and zk-based identity primitives** provide ways to prove attributes or membership without revealing full identity. In practice, they often feed into **Permissioned Privacy** flows or compliance-oriented deployments by supplying the attestations that gate access to private transfer systems.

However, the identity layer itself does **not define how balances are stored or moved**, so it is treated as an **orthogonal track** rather than a transfer pattern.

### Cross-Domain & Channel-Based Privacy

Mechanisms such as **shielded bridges, privacy-preserving interoperability protocols, state/payment channels with shielded balances, and dark-pool–style off-chain markets** focus on how assets move across domains or how parties coordinate off-chain while settling on-chain.

These systems typically **wrap or compose existing private‑transfer patterns** rather than defining new ways for balances to sit at rest. In Phase A they are treated as **transport and coordination layers** that sit on top of, or alongside, the seven scored patterns.


---

## Primitive Catalog

Phase A **scores transfer-centric patterns**, not the underlying cryptographic or infrastructure primitives. Each entry briefly states what the primitive is and which pattern families or deployments it typically supports.

#### Anonymous Signaling Primitives

- **Group membership & signaling primitives (e.g., Semaphore)** – Schemes where users register a secret into a shared membership structure (often a Merkle tree of identity commitments) and later prove membership and emit a “signal” using zk proofs and **nullifiers** to prevent double-use. They support **anonymous signaling deployments** (votes, attestations, anonymous posts) and can act as a backend for mixers or L1 shielded-pool–style systems that want unlinkable “one-time actions” rather than persistent accounts.

- **Merkle-tree membership + nullifier-based one-time actions** – The combination of (a) a commitment tree encoding a set of members and (b) nullifier-based spend or signal semantics that enforce “use-once” without revealing which member acted. This pattern of membership and nullifier logic appears inside multiple anonymous signaling and mixer-style deployments, including those that plug into L1 Shielded Pools or overlays.

#### Private Compute Primitives

- **FHE / iO / private-VM paradigms**  – General-purpose compute stacks (e.g., FHE-based VMs, iO/obfuscation-based VMs, zk-VMs) that allow arbitrary private computation where private transfers are just one application. In Phase A, they are treated as **general private-compute infrastructure** on top of which multiple transfer patterns (especially **Private Rollups**, **Private Validium**, and **Private Plasma**) can be instantiated without changing the underlying transfer semantics.

- **Trusted hardware enclaves (TEEs)** – Execution environments (e.g., SGX-style enclaves) that run private code with hardware-backed attestation guarantees. They support **off-chain private execution with on-chain attestation** for rollup-, Validium-, or Plasma-like deployments, changing the trust anchors (hardware vendors, operators) but not the high-level transfer pattern.

- **MPC committees** – Multi-party computation setups where a committee jointly executes private logic and produces an attested result. As with TEEs, these are used to instantiate **off-chain private execution** variants of rollups, Validium, or Plasma-like systems, and can also underpin private or threshold-signing services for overlays and bridges.

- **zk proof systems (e.g., zkSNARKs) as verification backends** – General zero-knowledge proof systems used to verify private statements on-chain (e.g., “this transfer is valid”, “this credential has attribute X”, “this user is a member of the group”). They are the common verification layer for many transfer patterns and identity systems, but are treated here as shared primitives that various patterns and deployments plug into.

---

## 8.2 Known Limitations and Analysis Gaps

Phase A is deliberately framed as a **first-pass landscape study**, we document several limitations and gaps that should inform how the results are interpreted.

### Heterogeneous Projects Within Each Pattern

Many pattern families—especially **L1 Shielded Pools** and **Private Rollups**—contain **architecturally diverse projects** (different assets, proof systems, DA strategies, UX paradigms). Maturity-weighted scoring mitigates but does not eliminate this variance:

- Pattern scores represent a **weighted average of heterogeneous deployments**, not a single canonical implementation.

### Metric Coupling and Overlap

Section 10.2 highlights several cases where metrics are **not fully independent**:
- **Programmability ↔ Selective Disclosure coupling** in Shielded Pools and Permissioned Privacy, where SD logic is embedded in programmable compliance layers.
- **UX ↔ DA model coupling** in Rollups, Plasma, and Validium, where user experience is dominated by DA and exit assumptions.

These couplings mean some columns in the comparison table are **partially correlated** by construction, even though the rubric treats them as separate dimensions.

### Limited Empirical UX and Gas Data

For some patterns—especially **Burn-and-Mint** and **Plasma/Validium variants**—there is **limited empirical data**:
- Few large-scale user studies or long-lived production deployments for complex UX flows.
- Gas measurements sometimes rely on **benchmarks or documentation**, not extensive in‑the‑wild transaction sets.

As a result, UX and gas scores for these patterns are **less constrained by real-world evidence** than for more mature categories like overlays or established shielded pools.

### Data Availability and Roadmap Uncertainty

DA assumptions are a dominant factor in many metrics, especially for **Rollups, Plasma, and Validium**. At the same time, roadmaps for key systems (e.g., **new rollup generations, evolving DA layers, or fully encrypted variants**) may significantly alter pattern characteristics over time.

Phase A scores should therefore be read as a **time‑bounded snapshot**, not as predictions about future performance or security.

### Gas Data and Tooling Gaps

Not all projects provide the same level of **transparent gas data, API access, or tooling documentation**, which constrains the precision of some metrics. Section 10.2 explicitly flags:

- **Incomplete gas datasets** for certain systems.
- **Weak debugging and dev tooling** across much of the private-stack ecosystem.

These are treated as analysis gaps rather than reasons to exclude patterns.

---

## 8.3 Implications for Interpretation

Given the boundaries and limitations above, readers should interpret the Phase A results with the following guardrails in mind:

1. **Descriptive, Not Normative**
    - Pattern scores, diagrams, and problem radars are **descriptive artifacts**: they summarize how the ecosystem looks today under a specific, maturity-weighted rubric.
    - They are **not recommendations**, rankings, or guidance; any such use belongs in **Phase B**, not Phase A.
2. **Pattern-Level Results Are Coarse-Grained**
    - Each pattern aggregates **multiple heterogeneous deployments**; internal variance can be high.
    - Use the table and pattern snapshots for **directional comparisons** (e.g., “this family tends to be more DA-trust-heavy than that one”), not as precise predictions for any single project.
3. **Metrics Are Interdependent in Practice**
    - UX, trust assumptions, DA model, and programmability often **move together**; improvements or regressions in one dimension may affect others.
    - Interpret differences in scores against that backdrop, especially for off-chain DA designs.
4. **Evolving Ecosystem Baseline**
    - Emerging systems (e.g., new rollup generations, private VMs, DA innovations) may change pattern characteristics or even blur boundaries over time.
    - Phase A should be seen as a **frozen baseline** that later work can update or refine, not as a once‑and‑for‑all taxonomy.
5. **Inputs to Phase B, Not Substitutes for It**
    - The comparison table, problem radar, and ecosystem maps are designed to feed into Phase B questions—such as **which problems to prioritize** or **which patterns best match organizational strengths**—but they **do not answer those questions**.
    - Section 9 makes those Phase B questions explicit while keeping them clearly out of scope for Phase A.

Under these interpretive guardrails, the reader can use the Phase A report as a **shared factual baseline**: a consistent, auditable landscape of private-transfer mechanisms, their trade-offs, and their structural problems—ready to be combined with strategic and organizational considerations in later phases.