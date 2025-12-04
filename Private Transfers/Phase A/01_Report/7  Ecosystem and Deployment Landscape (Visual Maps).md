
## 7.1 Taxonomy Diagram

The **taxonomy diagram** presents the seven private-transfer patterns in a **single visual frame**, organized along the same conceptual axes used throughout this report:

- **Primary axis:** how private state is represented and how data availability and correctness are enforced (L1-native vs separate state machine; full DA vs off-chain DA; trust model).
- **Cross-cutting attributes:** membership (open vs permissioned) and selective disclosure profiles, shown as visual annotations rather than separate pattern boxes.

At a glance, the diagram lets the reader:

- See all **seven patterns** at once.
- Understand how they relate in terms of **state model, DA model, and trust assumptions**.

The taxonomy diagram is intentionally **non-prescriptive**: it does not rank patterns or indicate which are “better”; it simply fixes a **shared map** of the design space used by all other sections (pattern cards, comparison table, problem radar).

![[Pasted image 20251203103357.png]]

---

## 7.2 Project Landscape Map

The **ecosystem landscape map** extends the taxonomy by placing **concrete projects and deployments** into the pattern boxes. Where the taxonomy diagram shows _categories_, the landscape map shows the **real systems populating those categories**.

For each pattern, the map can encode attributes such as:
- Example projects or deployments associated with that pattern.
- Rough deployment **status or maturity** (e.g., prototype, testnet, mainnet), aligned with the maturity concepts.

The goal is to give readers a **visual feel** for:

- Which patterns are **densely populated** by current work.
- Which patterns have **few or emerging deployments**.
- How different ecosystems (e.g., L1-native, rollups, Validium-style systems, permissioned stacks) line up against the taxonomy.

Again, the map is **descriptive**: it shows **where projects are**, not where they should go next or which ones are preferred. Coverage is representative rather than exhaustive; not all deployments can be shown on a single diagram.

| Pattern                        | Tier 1 — Prototype / Devnet                                                               | Tier 2 — Public Testnet / Early Pilot                                                                                                  | Tier 3 — Mainnet (Moderate Use)                                                                            | Tier 4 — Battle-tested Mainnet          |
| ------------------------------ | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| **L1 Overlay – Stealth / OTR** | —                                                                                         | —                                                                                                                                      | [[Umbra]]  · [[Fluidkey]]                                                                                  | —                                       |
| **L1 Shielded Pools**          | —                                                                                         | —                                                                                                                                      | [[Railgun]] ·<br>[[zkBob]] · [[Privacy Pools]] · [[Panther Protocol (zAssets)\|Panther]] · [[Semaphore]] · | [[Tornado Cash]]                        |
| **Burn-and-Mint Privacy**      | [[EIP-7503 – Private Transfers (ZK Proof-of-Burn, Burn-and-Mint)\|EIP-7503]] · [[Burnth]] | [[Intmax zERC20 (Burn‑and‑Mint Pattern)\|Intmax zERC20]]                                                                               | —                                                                                                          | —                                       |
| **Permissioned Privacy**       | —                                                                                         | [[Polygon ID  zk-KYC]] · [[Panther Protocol (zAssets)\|Panther]] · [[ZKSync Prividium]]                                                | [[ERC-1404 (Simple Restricted Token)\|ERC-1404]] · Consortium / custodial                                  | [[ERC-3643 (T‑REX Protocol)\|ERC-3643]] |
| **Private Rollups (Full DA)**  | —                                                                                         | [[ZKOPRU]] · [[Espresso Systems CAPE]] · [[Aztec Network v3\|New Aztec Network]] · [[Aztec Network v2 (Aztec Connect)\|Aztec Connect]] | [[Polygon Nightfall\|Nightfall ]]                                                                          | —                                       |
| **Private Plasma**             | [[PlasmaFold & zkPlasmaFold]]  · Other Plasma R&D                                     | INTMAX                                                                                                                                 | —                                                                                                          | —                                       |
| **Private Validium**           | —                                                                                         | [[ZKSync Prividium]] · [[Polygon Nightfall\|Nightfall (validium)]]                                                                     | —                                                                                                          | [[StarkEx (Validium Mode)]]             |


---

## 7.3 How to Interpret the Maps

Together, the taxonomy and landscape diagrams act as a **visual index** for the rest of the report:
- **Sections 3–4** explain the **taxonomy and pattern definitions** that underpin the layout of the maps.
- **Section 5** provides the **quantitative comparison** that describe how each pattern behaves along key metrics.
- **Section 6** introduces **cross-pattern problems** that cut across multiple boxes in the map.

Readers can use these maps as a **navigation aid**: to find which projects instantiate a given pattern, to see how crowded different areas of the design space are, and to orient more quickly when moving between the narrative, tables, and appendices.