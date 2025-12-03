
## 9.1 Problem Selection Questions

Phase A identifies **structural problems** and positions them on an **Impact–Tractability–Crowdedness radar**, but it does **not** decide which problems to tackle first. The following questions are intentionally left open for **Phase B** and related planning:

- **Which structural problems should be prioritized?**  
    – From the catalog in section 10.3 (privacy leakage, DA & exits, governance, UX/DevEx, compliance, composability), which problems are most important to address first, given the organization’s mandate?
- **How should the radar dimensions inform prioritization?**  
    – How should **Impact**, **Tractability (1–3 years)**, and **Crowdedness** be combined or weighted when choosing problems?
- **Where are there “high‑impact, under-served” problems?**  
    – Which problems appear high‑impact and reasonably tractable but relatively **sparsely worked on** today?
- **What level of ambition is appropriate?**  
    – Should Phase B focus on “shaving off rough edges” (UX/tooling, standardization) or on more ambitious shifts (new DA models, new composability layers)?
- **What is the right mix of research vs. engineering problems?**  
    – For each structural issue, what balance of **fundamental research**, **protocol design**, and **pragmatic engineering** is realistic in the near term?

These questions use the Phase A artefacts (section 10.3 problem catalog and radar) as inputs, but the **selection and ranking** of problems is explicitly deferred to Phase B.

---
## 9.2 Pattern Fit Questions

Phase A describes **how patterns behave**, but it does **not** decide which patterns align best with any specific organization or mandate. We explicitly list pattern‑fit questions as out‑of‑scope:

- **Which patterns align best with organizational capabilities and risk tolerance?**  
    – Given existing skills, infra, and constraints, which patterns are realistic to support, extend, or experiment with?
- **Which patterns are most relevant for targeted user segments?**  
    – For example, which patterns matter most for:
    - retail users needing simple safety and deniability,
    - DeFi users and builders,
    - institutions and RWAs,
    - public-goods and donation flows?
        
- **Where are there “natural adjacencies” to existing work?**  
    – How do the seven patterns intersect with ongoing work in **identity**, **ordering privacy**, **L2 infrastructure**, or other PSE tracks?

- **What prototypes or experiments would be most informative?**  
    – Which combinations of pattern + problem (e.g., “rollup UX under exit stress,” “Validium SD standards,” “overlay + ordering privacy”) would yield the most insight per unit effort?

- **What is the appropriate diversity of patterns in a portfolio of experiments?**  
    – Should Phase B concentrate on one or two patterns in depth, or deliberately keep a small portfolio across multiple patterns?
    
These questions turn the **Phase A pattern landscape and comparison table** into inputs for strategic decision-making, without answering them inside this report.

---

## 9.3 Coordination With Adjacent Work

Finally, several out-of-scope questions concern **how private transfers should coordinate with adjacent domains** that Phase A deliberately treats as “related mechanisms not scored.”

Key coordination questions include:
- **How should private transfers integrate with identity and credential systems?**  
    – What role should zk‑credentials, anonymous credentials, and attribute proofs play in Permissioned Privacy deployments and compliance-aware flows?

- **How should private transfers interact with ordering/privacy and mempool work?**  
    – Given that transaction submission and ordering privacy are handled in a separate track, how should **L1 overlays, shielded pools, rollups, Plasma, and Validium** plug into encrypted mempools or orderflow protection mechanisms?
    
- **How should general private compute (FHE, iO, private VMs) be combined with transfer patterns?**  
    – When (if ever) should private transfers be re‑expressed on top of fully general private compute stacks, and how would that affect classification and metrics?
    
- **How should cross-domain and bridging mechanisms be coordinated?**  
    – What role should **shielded bridges, private channels, and cross-domain privacy mechanisms** play in mitigating the cross-domain leakage and fragmented anonymity problems identified in WS3?
    
- **What ongoing benchmarks and observability tools are needed?**  
    – What kinds of **benchmarks, monitoring, and UX studies** would make future iterations of the comparison table and problem radar more empirically grounded?
    

These questions explicitly **bridge** the Phase A artifacts (taxonomy, comparison table, problem radar, related mechanisms) with **future coordination and strategy work**, without prescribing any particular answers.

---

In summary, **Section 9 collects the questions that Phase A intentionally leaves open**:

- **Which problems to focus on.**
- **Which patterns to emphasize.**
- **How to coordinate with identity, private reads, general private compute, and cross-domain mechanisms.**