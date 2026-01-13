### 2.1 Header

- **PID:** P12 — Lack of Private-to-Private Composability
- **Clusters:** `Composability & interoperability`
- **Patterns bound:** `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`; `Permissioned Privacy`

### 2.2 Problem statement

**Definition**  
Private systems often cannot perform private contract calls or asset flows across applications/domains without declassifying data, exiting/de-shielding, or relying on trusted intermediaries. Incompatible note formats, encryption schemes, and proof interfaces prevent atomic “private-to-private” composition and force users to bridge between privacy silos.

**What this is NOT (boundary)**  
This is not the cross-domain bridging linkability problem itself (P13), though boundary hops can be a consequence of poor composability. It is also not primarily “fragmented anonymity sets” (P02), though fragmentation is reinforced when composability forces many small, incompatible silos.

**Why it matters**  
Composability is a core driver of on-chain utility. If private apps cannot compose privately, users are forced into public detours at exactly the most revealing moments in multi-step workflows, causing privacy collapse and significant UX friction. In DeFi, inability to compose across protocols is a major functional regression (many workflows are natively multi-protocol and atomic).

**Affected workloads**  
Transfers: multi-app private workflows (e.g., move from one private domain/app to another) that currently require de-shielding, trusted intermediaries, or non-atomic sequences.  
DeFi stress-test: atomic multi-protocol actions (borrow → swap → LP; refinance; roll positions) that break if private-to-private calls are unavailable.

### 2.3 Failure modes & success

**Failure modes / symptoms**
- **Declassification at boundaries:** users must unshield or reveal metadata to move between apps/protocols, causing privacy collapse.
- **Non-atomic workflows:** without private-to-private calls, users must perform multi-step actions non-atomically, increasing both risk and leakage.
- **Interop dead-ends:** incompatible note/proof formats prevent private assets from moving across private domains even when “conceptually similar.”
- **Silo bridging:** users repeatedly hop between privacy silos, amplifying boundary leakage risks (ties to P13).

**What success looks like (measurable)**
- Users can complete defined cross-app workflows privately without requiring de-shielding or trusted intermediaries, and without losing atomicity where it matters.
- Interoperability surfaces exist such that private assets/state can move across applications with bounded, explicit disclosure (no “accidental declassification”).
- For DeFi-shaped workflows, a minimal private composability surface is defined and demonstrably supports representative multi-step actions.

**Known tradeoffs / failure modes of fixes**
- Increasing composability can expand the cross-app interface surface, increasing the risk of leakage through richer interaction patterns unless explicitly constrained.
- Standardization can enable interoperability, but may also couple ecosystems to shared formats/interfaces whose bugs or design flaws propagate widely.

### 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 4
- Tractability (1–3y): 3
- Crowdedness: Sparse
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

### 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| L1 Shielded Pools | Cross-app private calls often require unshielding or trusted intermediaries; lack of shared interfaces/note formats limits atomic private composition. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` (P12 section); `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^e74e59` |
| Burn-and-Mint Privacy | Stateless transfer-focused designs are not naturally suited to multi-step cross-app workflows; composability constraints show up as “not suitable for multi-step workflows.” | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix A — Pattern Definition Cards.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| Private Rollups (Full DA) | Without cross-app private call surfaces, users must exit/de-shield between apps; DeFi workflows require an explicit private composability surface to avoid public boundary hops. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` (P12 ask); `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| Private Plasma | Limited programmability and heterogeneous designs make private-to-private composition harder; users risk being trapped in silos without interoperable interfaces. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix A — Pattern Definition Cards.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| Private Validium | Incompatible note formats/encryption/proof interfaces prevent atomic private transfers between private domains; composability gaps push users into boundary hops. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` (P12 section) |
| Permissioned Privacy | Even if composition is easier within a controlled environment, cross-app private interoperability still requires compatible disclosure/policy interfaces; otherwise, users route through trusted intermediaries. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` (P12/P13 gating framing) |

### 2.6 Intervention modes (non-prescriptive)

Categories only — not implementations.

- Research  
  - Identify the minimal primitives/interfaces required for private-to-private composition without privacy collapse; map the irreducible disclosure required for cross-app calls.
- Engineering  
  - Develop reference test workloads for cross-app private workflows and measure where declassification happens (and why).
- Standards / coordination  
  - Coordinate on interoperability targets (note/proof interface expectations; disclosure semantics) so private systems can compose without bespoke bridges.
- Grants / convening  
  - Fund cross-ecosystem interoperability work and measurement frameworks that evaluate composability without turning interfaces into leakage backdoors.

**Dependencies / prerequisites (non-exhaustive)**
- Agreement on a minimal composability surface for private apps (especially for DeFi multi-protocol actions).
- Interoperable interfaces/formats for private assets/state movement across domains.

### 2.7 Evidence & uncertainty

**Key references**
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/12 Lack of Private-to-Private Composability.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^e74e59`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` (P12 section)
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` (P12 ask)

**Sprint 2 key claims (ClaimID → evidence map)**

| ClaimID | Claim (one sentence) | Uncertainty / notes |
|---|---|---|
| P12-C1 | Privacy systems often rely on protocol-specific note/address/key structures, so "private assets" are not automatically portable across privacy domains (even within a single ecosystem across upgrades). | Interop is possible with explicit bridges/migrations, but that is not the same as native private-to-private composability. |
| P12-C2 | Unified address/viewing-key formats are introduced to bundle multiple receiver types and ease migration across shielded pools, highlighting underlying fragmentation and compatibility requirements. | Unified formats improve UX, but do not guarantee application-level atomic composability. |
| P12-C3 | Cross-chain / cross-domain interoperability requires multi-stakeholder standardization; emerging standards like ERC-7683 aim to unify intent messages and settlement interfaces across bridging/trading systems. | ERC-7683 addresses a broad interop class; privacy-specific composability adds additional constraints beyond the standard. |
| P12-C4 | Current cross-L2 interoperability often depends on intermediaries (bridge operators/relayers/solvers and off-chain infrastructure), underscoring the coordination and trust challenges of interoperable multi-domain workflows. | This is about public cross-L2 interop; private-to-private adds further trust/metadata-leakage considerations. |
| P12-C5 | Achieving synchronous, atomic cross-domain calls ("Lego-like" composability) is treated as an ideal in multi-rollup designs, implying that today's multi-domain workflows are often asynchronous and non-atomic. | Applicability to privacy domains depends on whether synchronous call surfaces can preserve privacy without declassification. |

**Key uncertainties**
- Whether meaningful cross-app composability can be achieved without requiring disclosure surfaces that substantially degrade privacy in practice.
- How much coordination and standardization is realistically achievable in a 1–3 year horizon (interoperability is inherently multi-stakeholder).

**What would change the score**
- Evidence of interoperable private-to-private composition that supports representative cross-app workflows without declassification and with measurable privacy guarantees.
- Evidence that coordination/standardization barriers dominate (or that the required disclosure surfaces are too leaky), implying lower tractability than the Phase A baseline suggests.