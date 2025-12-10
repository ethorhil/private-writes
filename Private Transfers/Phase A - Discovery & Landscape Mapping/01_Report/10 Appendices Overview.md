## [[Appendix A — Pattern Definition Cards]]
Gathers the **full Pattern Definition Cards** for all seven private-transfer patterns:

1. L1 Overlay – Stealth / OTR
2. L1 Shielded Pools
3. Burn-and-Mint Privacy
4. Permissioned Privacy
5. Private Rollups (Full DA)
6. Private Plasma
7. Private Validium

Each card provides:

- A clear **one-sentence definition**
- A more detailed conceptual description of the mechanism
- Notes on **state model**, **DA model**, and **trust assumptions**
- Clarifications on **membership**, **visibility**, and **selective disclosure** as cross-cutting attributes
- Examples of representative deployments (where relevant)

**Who it is for**

- Readers who want deeper technical context than the brief pattern snapshots in **Section 4**
- Engineers and researchers who need a **precise classification reference** when mapping new or existing systems into the Phase A taxonomy
- Reviewers checking that later discussions (tables, radar, visuals) are consistent with the underlying pattern definitions

## [[Appendix B — Comparison Table & Score Justifications]]

**What it contains**

Appendix B contains the full **Private Transfers Comparison Table**, including:

- The **canonical master comparison table** with frozen scores for the seven patterns across:  
    _Privacy, L1 Gas / Transfer, TPS Potential, Programmability / Flexibility, UX Complexity, Readiness, Selective Disclosure, Trust Assumptions_
- The **maturity-weighted scoring methodology**, including the 1–4 maturity weights and the 1–5 rubric normalization rules
    
- A **score-justification appendix** for each pattern:
    - Decimal pre-score and rounded score
    - 1–2 sentence justification per metric
    - Source references and notes on data quality or uncertainty
- A short **inconsistencies & gaps report** describing metric coupling, heterogeneity inside patterns, gas data gaps, and roadmap uncertainty

**Who it is for**

- Readers who need **numerical detail** behind the high-level trade-off narrative in **Section 5**
- Quantitative reviewers verifying that scores are traceable and derived from documented deployments
- Anyone using Phase A as a baseline for **future re-scoring or benchmarking**, while keeping the Phase A scores themselves frozen

## [[Appendix C — Global Problem Catalog & Radar]]

**What it contains**

Appendix C hosts the detailed artifacts for **Global Problem Radar for Private Transfers**, including:

- The full **cross-pattern problem catalog** of 19 problems, with:
    - Problem title and description
    - Thematic categories (Privacy & Leak Vectors, Scalability & DA, Trust & Governance, UX & DevEx, Programmability & Expressiveness, Interoperability & Composability, Compliance & Selective Disclosure)
- The underlying **Impact, Tractability, and Crowdedness annotations** used to build the problem radar (where available)
- Any additional notes or examples illustrating how specific problems manifest across different patterns (e.g., DA issues in rollups vs Validium vs Plasma, composability issues in DeFi)

**Who it is for**

- Researchers and product leads exploring **which structural problems affect multiple patterns**
- Contributors who want to ensure that **new workstreams** map cleanly onto existing problem definitions instead of inventing overlapping terminology
---
