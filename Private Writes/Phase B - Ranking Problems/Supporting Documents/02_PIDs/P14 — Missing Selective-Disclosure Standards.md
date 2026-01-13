## 2.1 Header

- **PID:** P14 — Missing Selective-Disclosure Standards
- **Clusters:** `Compliance & selective disclosure`
- **Patterns bound:** `L1 Overlay – Stealth  OTR`; `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Permissioned Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`

## 2.2 Problem statement

**Definition**  
Missing selective-disclosure standards refers to the absence of widely adopted, interoperable primitives and formats for privacy-preserving auditability (e.g., proofs-of-innocence, scoped attribute disclosures, structured audit trails). In practice, each system invents bespoke disclosure mechanisms, often forcing all-or-nothing disclosures (such as overly broad viewing access) that raise integration costs and create accidental deanonymization risk.

Expanded: without shared standards, integrators (wallets, exchanges, custodians, institutions) face high and repeated costs to support disclosures across systems. Users and operators also face “disclose too much or disclose nothing” traps, where compliance needs are met only by leaking far more information than intended.

What this is not: this PID is about missing **standards/primitives** for selective disclosure. It is not about choosing jurisdictional compliance policy, and it is not the broader “compliance-compatible privacy is immature/inconsistent” ecosystem maturity problem (see P15).

**Why it matters**  
Selective disclosure is a gating interface for real-world adoption (institutions, regulated venues, dispute resolution, and operational audit). Without standards, disclosure becomes fragmented, expensive, and error-prone—either preventing adoption entirely or creating new privacy failures via over-disclosure and inconsistent semantics.

**Affected workloads**  
Transfers (baseline): “prove I received funds,” scoped transaction history disclosure, attestations of innocence/eligibility without revealing full history, audit trail production for specific counterparties.  
DeFi stress-test manifestation (when relevant): richer disclosures (positions, PnL/risk posture), liquidation legitimacy and dispute resolution disclosures, and role-based disclosure policies that vary by venue/jurisdiction.

## 2.3 Failure modes & success

**Failure modes / symptoms**
- Bespoke disclosure mechanisms per system; no interoperability across patterns or deployments.
- All-or-nothing sharing (e.g., overly broad view access) substitutes for scoped, minimal disclosures.
- Integration friction: each integrator must build custom pipelines per system, slowing adoption and raising operational risk.
- Accidental deanonymization: disclosures leak stable identifiers, excessive history, or cross-context linkages.

Dependencies / prerequisites (non-prescriptive)
- Coordination across stakeholders (privacy system teams, integrators, auditors/compliance stakeholders) to converge on shared claim types and proof formats.
- Clear separation between “baseline privacy properties” and “disclosure interface” so disclosure does not become an implicit backdoor.

Tradeoffs / failure modes of fixes
- Over-standardization can ossify early/immature disclosure semantics; under-standardization can preserve fragmentation.
- If disclosure primitives are not least-privilege by design, “standards” can encode over-disclosure and permanently reduce privacy.

**What success looks like (measurable)**
- A minimal selective-disclosure spec exists with conformance tests and public test vectors for core disclosure claims (innocence/eligibility/audit-scope).
- At least **3 independent implementations** (across different pattern families) pass conformance tests for the same disclosure claims.
- At least **2 integrator classes** (e.g., wallet + custodian, or exchange + auditor tooling) integrate the standard once and can support multiple privacy systems without bespoke disclosure logic per system.
- Disclosures can be scoped (least-privilege) and do not require persistent identifiers across transactions by default; “all-or-nothing view” is no longer the baseline.

## 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 5
- Tractability (1–3y): 4
- Crowdedness: Sparse
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

## 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| `L1 Overlay – Stealth  OTR` | Overlay-style privacy often relies on viewing/derivation disclosures; without standards, recipients/auditors face bespoke and potentially over-broad disclosures, increasing accidental linkage risk. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Overlay – Stealth  OTR.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/14 Missing Selective-Disclosure Standards.md` |
| `L1 Shielded Pools` | Shielded pools vary widely in disclosure capability; missing standards pushes “share too much view access” patterns and increases integrator complexity and deanonymization risk. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Shielded Pools.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |
| `Burn-and-Mint Privacy` | Cross-context burn/mint flows create audit needs (e.g., legitimacy/provenance claims) that are currently bespoke; missing standards increases both compliance friction and linkage risk through custom disclosures. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Burn-and-Mint Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| `Permissioned Privacy` | This pattern is explicitly driven by structured disclosure; lack of shared standards forces siloed compliance interfaces and reduces interoperability between permissioned environments and broader ecosystems. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Permissioned Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/14 Missing Selective-Disclosure Standards.md` |
| `Private Rollups (Full DA)` | Private rollups aiming for protocol-level selective disclosure need interoperable claim formats; without standards, audits and disclosures become bespoke per rollup and increase key/viewing complexity. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Rollups (Full DA).md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` |
| `Private Plasma` | Plasma-like systems often require operational/audit surfaces; missing disclosure standards increases bespoke tooling and risks “observability backdoors” via ad hoc disclosures. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Plasma.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |
| `Private Validium` | Validium deployments frequently feature stronger disclosure needs (auditor/committee visibility); without standards, disclosure becomes institution-specific and can hard-code linkability through repeated, non-standard attestations. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Validium.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |

## 2.6 Intervention modes (non-prescriptive)

- Research  
  - Define minimal disclosure claim sets and adversary models for “least-privilege” disclosures.
  - Study how disclosure primitives interact with long-lived workflows (DeFi positions) without creating stable identifiers.

- Engineering  
  - Build conformance tooling (test vectors, reference parsers/verifiers) for selective disclosure formats and claim definitions.
  - Improve integrator-facing APIs and documentation patterns that reduce “all-or-nothing view access” defaults.

- Standards / coordination  
  - Convene ecosystem actors around a minimal interoperability spec (claims, formats, test vectors, conformance).
  - Align disclosure semantics across patterns to avoid ecosystem fragmentation.

- Grants / convening  
  - Fund multi-implementation interop efforts and independent privacy reviews of disclosure interfaces.

## 2.7 Evidence & uncertainty

**Key references**
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/14 Missing Selective-Disclosure Standards.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix A — Pattern Definition Cards.md`

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Uncertainty / notes |
|---|---|---|
| P14-C1 | Selective disclosure can be standardized at the token layer; SD-JWT specifies how a holder can disclose only a subset of claim values from an issuer-signed JWT. | SD-JWT addresses JWT/JOSE ecosystems; it does not by itself unify selective disclosure across non-JWT credential formats. |
| P14-C2 | The W3C Verifiable Credentials Data Model v2.0 defines an extensible data model for expressing and exchanging verifiable credentials and presentations in a three-party ecosystem (issuer, holder, verifier). | Interoperability depends on adopting compatible securing mechanisms and profiles; the data model alone does not ensure end-to-end interop. |
| P14-C3 | VC Data Model v2.0 positions itself as a Recommendation and notes that ecosystem compatibility requires conformance plus at least one securing mechanism, implying multiple permissible security stacks and potential fragmentation. | Inference: multiple securing mechanisms can fragment interoperability unless ecosystems converge on profiles/test suites. |
| P14-C4 | BBS signatures support proving knowledge of a signature while selectively disclosing any subset of signed messages, enabling cryptographic selective disclosure and unlinkable presentations. | BBS is still evolving in standards track; implementations and cryptosuite details vary. |
| P14-C5 | Standards are converging: SD-JWT includes an appendix on SD-JWT-based verifiable credentials and references the VC Data Model v2.0, demonstrating active integration work between token and credential standards. | Integration guidance does not guarantee interoperable implementations across ecosystems (profiles may diverge). |
| P14-C6 | Selective-disclosure primitives can be embedded into VC security suites (e.g., W3C Data Integrity BBS cryptosuites) to support selective disclosure and privacy-preserving proof presentations. | Adoption is uneven; verifier support and conformance testing remain limiting factors. |
| P14-C7 | Despite progress, privacy systems still often rely on coarse-grained disclosure mechanisms (e.g., broad viewing permissions) or bespoke standards, keeping selective-disclosure interoperability a live gap. | General claim; scope varies widely across ecosystems and protocol families (ZKPs, VCs, account abstraction, etc.). |


**Key uncertainties (Sprint 1)**
- Which disclosure claim set is genuinely “table-stakes” across venues without forcing over-disclosure.
- How to handle revocation/rotation and jurisdictional variance without embedding linkability into the standard.

**What would change the score**
- If a cross-pattern disclosure spec with conformance tests is adopted by multiple independent teams/integrators, Tractability increases and Crowdedness may move from Sparse.
- If regulatory/venue requirements shift toward richer position-level disclosures (especially for DeFi), Impact may increase and success criteria may tighten.