## 2.1 Header

- **PID:** P16 — Identity Binding Without Linkability
- **Clusters:** `Compliance & selective disclosure`; `Privacy leakage & anonymity`
- **Patterns bound:** `L1 Overlay – Stealth  OTR`; `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Permissioned Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`

## 2.2 Problem statement

**Definition**  
Identity binding without linkability is the challenge of enforcing identity-, membership-, or eligibility-based access (or producing repeated eligibility proofs) without turning those proofs and credentials into stable correlators (“pseudonyms”) that allow observers to link a user’s actions across contexts, apps, and domains.

Expanded: even if each eligibility proof is “zero-knowledge,” reusing the same credential across apps/chains—or producing repeated proofs with consistent metadata—can enable cross-context correlation. Revocation, rotation, and multi-jurisdiction attribute policies add pressure toward repeated, linkable checks.

What this is not: this PID is specifically about **identity/credential binding artifacts becoming linkability channels**. It is not general behavioral fingerprinting via on-chain interaction patterns (see P01) and it is not primarily network-layer metadata correlation (see P19), though both can compound identity-based linkability.

**Why it matters**  
Many compliance and institutional workflows require some form of identity or eligibility. If identity binding collapses privacy by making users linkable across transactions and venues, privacy claims fail precisely for the user segments most likely to require these controls. In DeFi-like workloads with repeated interactions, stable identity correlators can reveal strategy, risk posture, and organizational behavior over time.

**Affected workloads**  
Transfers (baseline): permissioned pools, credential-gated access, repeated eligibility checks for receiving/sending, revocation/rotation events that may force re-checks.  
DeFi stress-test manifestation (when relevant): repeated eligibility proofs across an end-to-end position lifecycle (open/adjust/close), cross-venue activity, and organizational identity requirements that must not reveal strategies via correlatable proofs.

## 2.3 Failure modes & success

**Failure modes / symptoms**
- Eligibility proofs act as stable pseudonyms across transfers (linking a user’s actions despite otherwise-private state).
- Credential reuse across apps/chains enables cross-context correlation even if each app is locally private.
- Revocation/rotation and policy variability force repeated checks that become linkability signals.
- Identity-binding requirements push systems into small, stable membership sets that are easy to correlate over time (compounding with low-volume regimes).

Dependencies / prerequisites (non-prescriptive)
- Selective disclosure primitives that support least-privilege claims (dependency on P14).
- Compliance integration patterns that do not require stable identifiers or repeated, linkable attestations (dependency on P15).

Tradeoffs / failure modes of fixes
- Stronger revocation and richer attributes can increase the number and cadence of checks, raising linkability pressure.
- Designing for unlinkability can increase operational complexity (credential rotation, recovery, multi-venue interoperability).
- If systems “solve” this by enforcing stable identities for convenience, privacy is structurally reduced and may become incompatible with the original goals.

**What success looks like (measurable)**
- Repeatable eligibility/membership proofs can be produced over time **without enabling linkage** beyond a defined leakage budget (e.g., observers using only credential/proof artifacts achieve **≤ 10% precision at ≥ 20% recall** in linking a user’s actions across venues under realistic usage).
- Credential rotation and revocation can occur without forcing users into public boundary hops that expose linkage (measured by whether rotation events themselves create stable correlators).
- Multi-policy (multi-jurisdiction / multi-venue) attribute requirements can be satisfied without increasing the frequency of linkable checks above a defined threshold.
- Evaluation harnesses explicitly test “stable pseudonym emergence” from credential reuse and repeated proofs under DeFi-like repeated workflows.

## 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 4
- Tractability (1–3y): 4
- Crowdedness: Medium
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

## 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| `L1 Overlay – Stealth  OTR` | If overlays are used in credential-gated contexts, identity-binding artifacts can trivially re-link stealth-derived receipts to a stable identity; disclosure must remain scoped and non-correlating. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Overlay – Stealth  OTR.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/16 Identity Binding Without Linkability.md` |
| `L1 Shielded Pools` | Permissioned shielded pools and screened access risk turning eligibility proofs into stable pseudonyms; preventing cross-transaction correlation from repeated proofs is binding for “permissioned shielded” deployments. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Shielded Pools.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| `Burn-and-Mint Privacy` | Cross-context mint eligibility checks can become stable correlators; identity binding must not allow linking burns/mints across contexts via repeated eligibility proofs. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Burn-and-Mint Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/16 Identity Binding Without Linkability.md` |
| `Permissioned Privacy` | This pattern explicitly requires identity/credential gating; preventing credential reuse from becoming a stable pseudonym across apps/venues is a primary constraint. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Permissioned Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |
| `Private Rollups (Full DA)` | Rollups that support repeated workflows (DeFi lifecycles) amplify pseudonym risk: repeated eligibility proofs can link many writes over time unless explicitly designed to avoid correlation. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Rollups (Full DA).md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` |
| `Private Plasma` | Stress-mode exits and operational constraints can force repeated identity/eligibility interactions (e.g., disputes, support), increasing pseudonym risk; identity binding must not become an operational backdoor. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Plasma.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^3cb481` |
| `Private Validium` | Consortium environments with credential systems are common; repeated attestations and operator-mediated checks can create stable correlators across venues unless unlinkability is treated as a first-class constraint. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Validium.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15` |

## 2.6 Intervention modes (non-prescriptive)

- Research  
  - Develop models and measurement approaches for “pseudonym emergence” from repeated eligibility proofs, including DeFi-like repeated workflows.
  - Study revocation/rotation and multi-policy attribute requirements as primary drivers of linkability.

- Engineering  
  - Build evaluation harnesses and test suites that measure linkage arising solely from credential/proof artifacts.
  - Improve key/credential lifecycle UX patterns (rotation, recovery) to reduce operational pressure toward stable identities.

- Standards / coordination  
  - Align on minimal interfaces for eligibility proofs and revocation/rotation semantics that are compatible with unlinkability goals.
  - Coordinate across venues/integrators to avoid bespoke eligibility implementations that hard-code correlators.

- Grants / convening  
  - Fund cross-team interop pilots and independent reviews focused on identity-binding linkability, especially in repeated DeFi-like workflows.

## 2.7 Evidence & uncertainty

**Key references**
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/16 Identity Binding Without Linkability.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c4ed15`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^3cb481`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix A — Pattern Definition Cards.md`

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Uncertainty / notes |
|---|---|---|
| P16-C1 | Identity systems can reduce cross-domain linkability by issuing pairwise pseudonymous identifiers (distinct per relying party/sector); OpenID Connect specifies a pairwise subject identifier algorithm whose values are non-reversible by parties other than the issuer. | Pairwise IDs mitigate RP-to-RP correlation but do not prevent the issuer from correlating users across RPs. |
| P16-C2 | Ephemeral or session-bound identifiers further reduce correlation by changing the subject identifier across visits while remaining constant within a session (as specified in an OpenID Connect draft). | Draft maturity; ecosystem adoption and compatibility with existing deployments are uncertain. |
| P16-C3 | Anonymous credential systems (CL) are designed so repeated credential presentations can be unlinkable, enabling identity/eligibility binding without revealing a stable identifier to verifiers. | Anonymous revocation and abuse-prevention mechanisms can reintroduce correlation if not designed carefully. |
| P16-C4 | Idemix explicitly targets unlinkable pseudonyms and allows proving credential possession across organizations without revealing more than the required statement. | Real-world deployments need careful issuance, revocation, and anti-sharing controls; operational metadata remains a risk. |
| P16-C5 | Token/credential approaches like U-Prove are designed to support privacy-enhancing attribute disclosure, illustrating long-standing interest but also fragmented ecosystems of non-interoperable schemes. | U-Prove differs from anonymous-credential schemes in properties (e.g., unlinkability may be weaker/optional depending on usage). |
| P16-C6 | Modern selective-disclosure signature schemes such as BBS enable zero-knowledge proofs with selective disclosure of signed attributes, supporting non-linkable identity binding in credential-based systems. | Standardization and verifier support are still evolving; different suites (BBS vs SD-JWT) are not directly interoperable. |
| P16-C7 | Binding identities to on-chain actions without linkability remains hard in practice because operational needs (revocation, abuse prevention, compliance) tend to reintroduce stable identifiers or repeated checks. | Synthesis claim; feasibility depends strongly on threat model, regulator expectations, and whether identity binding is mandatory or optional. |


**Key uncertainties (Sprint 1)**
- What revocation/rotation requirements are “non-negotiable” for target venues, and how frequently checks must occur.
- Whether practical deployments can keep eligibility proofs unlinkable under repeated workflows without forcing heavy operational burden.

**What would change the score**
- If widely adopted identity/credential approaches demonstrate unlinkable repeat proofs with workable revocation/rotation (in repeated workflows), Tractability may increase (and Medium crowdedness may rise).
- If venues/regulators require stable identifiers by default for broad participation, Impact of "unlinkable identity binding" solutions may decrease (or the problem shifts toward explicit scope limitations).