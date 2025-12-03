
## **2.1 Purpose of the Private Transfers Track**

The **Private Transfers** track investigates how users can move value privately on Ethereum and adjacent systems. Private transfers are a foundational building block for user protection, commercial use cases, institutional adoption, and compliant on-chain finance.

Yet, unlike public transfers—where designs converge on a shared set of primitives—the privacy landscape is diverse, fragmented, and driven by different assumptions about data availability, trust, programmability, and identity. This diversity makes it difficult for protocol teams, builders, and researchers to speak a common language about “how private transfers work” and where the main structural bottlenecks lie.

Phase A responds to this need by producing a **clear, normalized overview** of:
- the major mechanism families that support private value movement,
- how they differ in guarantees and costs,
- where they share common failure modes, and
- how the ecosystem is distributed across these mechanism types.

The goal is not to decide which pattern is “best,” but to map the field in a way that enables future decision-making.

---

## **2.2 What This Report Covers (Phase A Boundaries)**

Phase A is deliberately **descriptive**.  
It aims to:

- Define the **seven canonical private-transfer patterns** used throughout the ecosystem.
- Explain the **taxonomy** that distinguishes them.
- Compare patterns using a **frozen, maturity-weighted scoring framework**.
- Describe the **cross-pattern problems** that affect multiple approaches.
- Introduce the **ecosystem landscape** and where current projects fit.
- Provide a **common vocabulary** for teams thinking about private transfers.

Phase A does **not**:
- Recommend which patterns PSE or anyone else should invest in.
- Rank patterns by strategic importance.
- Introduce new metrics or modify existing scores.
- Speculate on future technical breakthroughs.
- Perform any prioritization.

Any instruction or interpretation requiring those actions is out of scope and must be handled in **Phase B**.

---

## **2.3 How to Read This Report**

This report is structured so that readers can enter at different levels of depth:
- **Section 3** introduces the taxonomy — the conceptual backbone of Phase A.
- **Section 4** provides short, comparable pattern snapshots.
- **Section 5** explains the comparison methodology and presents the master table.
- **Section 6** summarizes structural problems that recur across patterns.
- **Section 7** presents two diagrams
    - `[DIAGRAM PLACEHOLDER: Taxonomy Map (WS4 – Concept A)]`
    - `[DIAGRAM PLACEHOLDER: Ecosystem Landscape Map (WS4 – Concept B)]`
- **Section 8** clarifies related mechanisms that are _not_ patterns.
- **Section 9** lists Phase B questions, without answering them.
- **Section 10** introduces the appendices containing full pattern cards, score justifications, and the problem catalog.

Readers seeking a top-level narrative should focus on **Sections 1, 3, 5, and 6**.  
Readers needing technical grounding or references to specific systems will find details in the **appendices**.