
## 5.1 Metrics and Scoring Methodology

The comparative evaluation in Phase A is based on a **maturity‑weighted, rubric‑normalized scoring framework** (see 10.2).

### 5.1.1 Maturity-Weighted Pattern Scores

Each pattern’s score is derived from the real projects that instantiate it, weighted by their **deployment maturity**. Concretely, we define pattern scores as:

> A maturity-weighted average of project-level scores within the pattern,  
> where each project is weighted by how battle-tested its deployment is.

Maturity weights follow a 1–4 scale:
- **1** – Prototype / conceptual / devnet
- **2** – Public testnet / early pilot
- **3** – Mainnet with moderate usage
- **4** – Battle-tested, multi‑year mainnet deployment

This ensures that **long‑running, widely used systems** have more influence on the pattern’s profile than proofs‑of‑concept or early pilots.

We also set a clear interpretation rule:

> **Pattern scores describe the current, maturity‑weighted shape of the pattern as deployed today.**  
> They are neither theoretical upper bounds nor minimum baselines.

### 5.1.2 Metric Rubric (1–5 Scale)

All metrics use a **1–5 rubric**, normalized across patterns:
- Higher is always **better** on each column.
- Thresholds are **shared across patterns**, not tuned per pattern.

The core metrics are:

1. **Privacy**  
    – Strength of transactional privacy at the state level (sender/receiver/amount shielding, linkability, metadata exposure).
2. **L1 Gas / Transfer**  
    – Typical on-chain cost per transfer, including proof verification and calldata.
3. **TPS Potential**  
    – Realistic throughput potential, considering cryptographic overhead and DA constraints, not just raw block limits.
4. **Programmability / Flexibility**  
    – Range and expressiveness of private logic: from simple payment flows to rich private smart-contract ecosystems.
5. **UX Complexity**  
    – Operational burden on users: keys, notes, relayers, exits, onboarding.  
    – Higher scores correspond to **simpler, more robust UX** in practice.
6. **Readiness**  
    – Deployment maturity and ecosystem robustness: mainnet status, stability, integrations, tooling.
7. **Selective Disclosure**  
    – Quality and richness of mechanisms for revealing information selectively to auditors, regulators, or counterparties.
8. **Trust Assumptions**  
    – Strength of security guarantees against data withholding, censorship, and operator misbehavior:  
    from fully trust-minimized (L1-equivalent) to DA-committee- or operator-heavy patterns.
    

Each pattern’s values on these metrics are fixed and are **not re-scored** in this report.

---

## 5.2 Master Comparison Table

We define a **canonical master table** that scores the seven patterns across all metrics using the methodology above. That table is the quantitative backbone for Phase A and is referenced here.

The full, high-resolution version of this table (including decimal pre-scores and short justifications per cell) appears in:

[[Appendix B — Comparison Table & Score Justifications]]

---

## 5.3 Key Trade-Offs and Observations

The scores and justifications reveal several **recurring trade‑off curves** across the seven patterns.

### 5.3.1 Privacy vs L1 Cost

Patterns that deliver **stronger on-chain privacy** generally incur **higher L1 costs**:

- **L1 Shielded Pools, Burn-and-Mint, Private Rollups, Private Plasma, and Private Validium** cluster toward **strong privacy**, but pay for this with **expensive proofs, higher calldata, or DA infrastructure costs**.
- **L1 Overlays** trade off some privacy strength (e.g., amounts and senders remain public) for **much lower incremental gas and simpler integration**.

This is a core structural tension: **strong privacy at the state level tends to be gas- and bandwidth-intensive**, especially on L1.

### 5.3.2 Throughput vs DA Model vs Trust

Throughput potential tracks **where data lives and who holds it**:

- **L1-native systems** (Overlays, Shielded Pools, Burn-and-Mint) are bounded by Ethereum’s base throughput; they cannot scale beyond L1 without moving data off-chain.    
- **Private Rollups (Full DA)** improve **TPS per unit cost** via batching and proof aggregation, while keeping full data on L1 and preserving strong trust minimization.
- **Private Plasma** and **Private Validium** can reach the **highest throughput scores** by pushing most data off-chain—but this introduces **exit fragility and DA-committee trust** respectively.

As a result, the table shows a clear pattern:

> To move along the **throughput frontier**, systems generally pay in **either L1 cost** (Rollups) or **trust and exit safety** (Plasma, Validium).

### 5.3.3 Programmability vs Simplicity

We distinguish between patterns built for **simple payment-like flows** and those designed for **rich, private smart-contract logic**:

- **L1 Overlays, Burn-and-Mint, and many Plasma variants** score lower on programmability: they are optimized for transfers and basic workflows rather than complex private DeFi.
- **Private Rollups and Private Validium** score higher, reflecting deployments that support private exchanges, AMMs, or general-purpose private VMs.

However, programmability comes with **higher complexity** for both implementers and users (more elaborate circuits, tooling, and UX responsibilities).

### 5.3.4 UX Friction and Operational Risk

Patterns with stronger privacy and more complex DA models tend to have lower UX scores:
- **Shielded Pools, Rollups, Plasma, and Validium** often require **multi-key management**, **note handling**, **use of relayers**, or **exit‑related user responsibilities**.
    
- **Permissioned Privacy** and some **Validium deployments** can provide smoother UX once onboarding is complete, since day-to-day transfers may resemble standard token transfers, albeit within a gated environment.
    

The table and justifications emphasize that **UX complexity is tightly coupled to DA and exit semantics**—especially in Plasma and Validium, where users must understand safety assumptions around data withholding and exits.

### 5.3.5 Readiness and Ecosystem Maturity

Readiness scores reflect **where the ecosystem is today**, not where it might go:

- **L1 Overlays, L1 Shielded Pools, and many Permissioned Privacy deployments** enjoy relatively higher readiness: they have **live mainnets, real users, and production integrations**.
- **Burn-and-Mint** designs and **Private Plasma** are generally earlier-stage, with fewer mature deployments.
- **Private Validium** benefits from **StarkEx-style systems and early application chains**, raising its readiness relative to its novelty as a privacy pattern.

This underscores that **pattern attractiveness in theory** may differ from **pattern maturity in practice** at the time of Phase A.

### 5.3.6 Selective Disclosure and Compliance Integration

Selective disclosure scores vary significantly by pattern family and deployment style:

- Some **Shielded Pools** offer little or no SD, while others introduce **viewing keys or association-set proofs** to support proofs-of-innocence.
- **Permissioned Privacy** systems and certain **Validium deployments** are often designed around **compliance and auditability**, giving them relatively strong SD scores.
- **Overlays and simple Burn-and-Mint systems** can support ad-hoc SD but rarely provide rich policy frameworks out of the box.

Across patterns, we highlight a structural gap: **mature, standardized SD and compliance tooling is still rare**, even where privacy and readiness are high.