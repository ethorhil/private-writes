## 2.1 Header

- **PID:** P15 — Immature Privacy-Preserving Compliance
- **Clusters:** `Compliance & selective disclosure`
- **Patterns bound:** `L1 Overlay – Stealth  OTR`; `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Permissioned Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`

## 2.2 Problem statement

**Definition**  
Immature privacy-preserving compliance describes the fact that “compliance-compatible privacy” designs (e.g., screened access, credential gating, audit hooks) remain early-stage and inconsistent across mechanisms, and the compliance hooks themselves often introduce new linkability channels or reduce anonymity sets. Interoperability across compliance approaches is limited, pushing fragmentation and jurisdiction-specific silos.

Expanded: many current approaches either (a) meet compliance needs by sharply reducing privacy (stable identifiers, repeated checks, broad disclosures) or (b) preserve privacy but fail to provide credible compliance hooks. The result is a brittle ecosystem where compliance features can become the dominant privacy failure mode.

What this is not: this PID is about the **maturity and interoperability** of compliance-compatible privacy designs. It is not primarily the absence of selective-disclosure standards (see P14), and it is not narrowly the “identity proofs become stable pseudonyms” mechanism (see P16), though both are closely related dependencies.

**Why it matters**  
Compliance requirements are a gating constraint for institutional adoption and can materially shape what private transfer and private DeFi systems can support in practice. If compliance hooks routinely destroy unlinkability or force ecosystem fragmentation, privacy systems either remain niche or become “privacy in name only,” with high operational and regulatory risk.

**Affected workloads**  
Transfers (baseline): screened pools, eligibility gating, audit hooks, interaction with regulated counterparties, and integration with compliance workflows without requiring full-history disclosure.  
DeFi stress-test manifestation (when relevant): higher-scrutiny workflows (lending/leverage, long-lived positions) that need ongoing visibility/eligibility without turning repeated disclosures into linkage channels.

## 2.3 Failure modes & success

**Failure modes / symptoms**
- Compliance hooks become new linkage channels (repeat checks, credential reuse, persistent “eligible user” identifiers).
- Permissioning/screening shrinks anonymity sets into small, predictable pools, making deanonymization structurally easier.
- Lack of interoperability across compliance approaches leads to fragmented markets, jurisdiction-specific silos, and broken composability.
- Compliance-driven operational processes create de facto privileged visibility roles that can become privacy backdoors.

Dependencies / prerequisites (non-prescriptive)
- Selective disclosure primitives and standards (dependency on P14).
- Identity/credential integration patterns that preserve unlinkability across repeated interactions (dependency on P16).
- Clear threat models that treat compliance interfaces as part of the privacy surface (not as an external add-on).

Tradeoffs / failure modes of fixes
- Stronger compliance enforcement often pressures toward stronger identity binding and repeated attestations, increasing linkability risk.
- Avoiding linkability can reduce policy expressiveness or increase operational complexity (e.g., revocation/rotation without repeated linkable checks).
- Interoperability goals can conflict with jurisdictional variance and venue-specific policy requirements.

**What success looks like (measurable)**
- At least **2 mechanism families** demonstrate compliance hooks (eligibility + scoped disclosures) that do not create stable pseudonyms across repeated use, measured by low cross-transaction linkability from compliance artifacts (e.g., **≤ 10% precision at ≥ 20% recall** for linking based only on compliance-interface outputs under realistic usage).
- Compliance-compatible designs do not reduce effective anonymity sets below a minimum viable threshold for intended usage (measured as candidate set size distribution under realistic volumes).
- A common, mechanism-agnostic compliance interface (claims + verification expectations) is usable by integrators without bespoke per-system integrations, reducing fragmentation pressure.
- Clear documentation exists for “failure modes of fixes” (how compliance hooks can silently become linkage channels) and these are tested in evaluation harnesses.

## 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 5
- Tractability (1–3y): 3
- Crowdedness: Medium
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

## 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| `L1 Overlay – Stealth  OTR` | Overlay privacy is narrow; compliance needs may require disclosure interfaces that risk re-linking stealth receipts to long-lived identity. Lack of mature compliance hooks encourages either over-disclosure or non-adoption. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Overlay – Stealth  OTR.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/15 Immature Privacy-Preserving Compliance.md` |
| `L1 Shielded Pools` | Screened/permissioned variants can sharply reduce anonymity sets and create repeat-check linkability; compliance hooks must avoid becoming stable identifiers while remaining operationally credible. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Shielded Pools.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| `Burn-and-Mint Privacy` | Compliance requirements for cross-context burns/mints can introduce provenance or eligibility signals that re-link flows if immature; inconsistent approaches across deployments increase fragmentation. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Burn-and-Mint Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/15 Immature Privacy-Preserving Compliance.md` |
| `Permissioned Privacy` | This pattern is defined by compliance drivers; immaturity shows up as inconsistent credential/policy integration, stable pseudonym risk from repeated checks, and weak interoperability between permissioned domains. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Permissioned Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |
| `Private Rollups (Full DA)` | Private rollups face pressure to offer credible compliance hooks for complex workflows; immature hooks can leak strategy/identity across multi-write lifecycles and push fragmentation across venues/jurisdictions. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Rollups (Full DA).md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` |
| `Private Plasma` | Operator/exit constraints can interact with compliance enforcement (e.g., repeated checks near exits), creating linkability under stress; immature compliance processes can become operational backdoors. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Plasma.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |
| `Private Validium` | Consortium/operator-heavy environments can implement compliance controls, but immaturity risks (inconsistent policies, privileged visibility, linkable attestations) are amplified; interoperability is often weakest across deployments. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Validium.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |

## 2.6 Intervention modes (non-prescriptive)

- Research  
  - Model how compliance hooks (eligibility checks, disclosures, revocation) create linkability channels; define measurable leakage budgets.
  - Study policy variability (jurisdiction/venue) as a driver of fragmentation and linkage risk.

- Engineering  
  - Build evaluation harnesses for “compliance interface leakage” (ability to link transactions based only on compliance artifacts).
  - Develop integrator-friendly compliance interfaces and documentation patterns that reduce bespoke implementations.

- Standards / coordination  
  - Coordinate on minimal, mechanism-agnostic compliance interface expectations (separate from any specific policy choices).
  - Align how compliance approaches interoperate to reduce silos.

- Grants / convening  
  - Fund multi-stakeholder workshops (privacy + compliance + integrators) and independent reviews of compliance-interface privacy risks.

## 2.7 Evidence & uncertainty

**Key references**
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/15 Immature Privacy-Preserving Compliance.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix A — Pattern Definition Cards.md`

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Uncertainty / notes |
|---|---|---|
| P15-C1 | Major jurisdictions are extending "travel rule"-style requirements to crypto-asset transfers, requiring originator/beneficiary information to accompany transfers under defined conditions. | Jurisdictional scope and thresholds vary; applicability depends on whether entities qualify as obliged parties (e.g., VASPs). |
| P15-C2 | Compliance requirements often mandate persistent identity-related data flows (originator/beneficiary information), creating direct pressure against end-to-end transactional privacy if implemented naively. | Some models may support privacy-preserving data sharing via regulated intermediaries; operational details matter. |
| P15-C3 | International AML/CFT standards are evolving to increase payment transparency and encourage use of tools to protect against fraud/error, indicating a moving compliance target for privacy-preserving systems. | Interpretation and implementation timelines differ; "tools" are not necessarily privacy-preserving tools. |
| P15-C4 | Research proposals are explicitly exploring privacy-preserving compliance layers (e.g., "proof of innocence" / privacy-pool-style screening) that aim to preserve user privacy while enabling some forms of misuse mitigation. | Approaches are early-stage and may not satisfy all regulatory expectations; definitions of "innocence" differ by policy. |
| P15-C5 | Even "privacy-preserving compliance" mechanisms can introduce new linkage surfaces (e.g., proof artifacts, membership/blacklist checks, or repeated attestations), which must be assessed as part of the privacy model. | Evidence is mostly conceptual/prototypical; real-world deployments and adversary models are under-studied. |
| P15-C6 | Overall, privacy-preserving compliance remains immature: requirements are heterogeneous and fast-evolving, and technical mechanisms (standards + assurance) are still developing, creating uncertainty for builders. | This is a synthesis claim; maturity varies by jurisdiction and by the type of compliance objective (KYC, sanctions, reporting). |


**Key uncertainties (Sprint 1)**
- What compliance interface “minimum set” is required across target venues without forcing over-disclosure.
- How much fragmentation is driven by policy variance vs technical immaturity.

**What would change the score**
- If multiple real-world deployments demonstrate compliance hooks that preserve unlinkability across repeated use, Tractability could increase.
- If policy/venue requirements converge on a stable minimal interface (reducing fragmentation), Impact remains high but the feasible path becomes clearer.
- If compliance requirements tighten for DeFi-like workloads (ongoing monitoring), Impact may increase and "failure modes of fixes" become more severe.