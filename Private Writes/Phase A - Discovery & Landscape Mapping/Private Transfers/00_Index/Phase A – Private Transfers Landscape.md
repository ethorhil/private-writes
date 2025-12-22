  
Phase A maps the current ecosystem of private-transfer mechanisms, builds a simple taxonomy, and compares the main patterns (overlays, shielded pools, burn‑and‑mint, private rollups, etc.) across shared metrics like privacy strength, L1 cost, throughput, UX, and trust assumptions. The output is a shared factual baseline plus a “problem radar” of recurring structural challenges.

## Start Here / Reading Paths

- **New to Private Transfers?**  
    Read [[1 Summary]] → [[4 Pattern Overview]] for a narrative overview and short pattern snapshots.
    
- **Interested in specific privacy problems?**  
    Go to [[6 Cross-Pattern Problems]] and then the detailed problem list in the **Problems** section below. For more structure, use [[Appendix C — Global Problem Catalog & Radar]].
    
- **Looking for ecosystem projects?**  
    Start at [[7 Ecosystem and Deployment Landscape]] and follow links into project notes in the `05_Projects/` folder.
    
- **Want to compare approaches?**  
    See [[5 Comparative Evaluation]] for the main comparison, then dive into [[Appendix B — Comparison Table & Score Justifications]] for detailed scores and explanations.
    
- **Need full pattern reference cards?**  
    Use [[Appendix A — Pattern Definition Cards]] for complete pattern write-ups.
    

For a high-level overview of all phases of the work, see [[Phases of the Private Writes Track]].

---

## Index

- [[1 Summary]] (start here)
- [[2 Background and Scope]]
- [[3 Taxonomy]]
- [[4 Pattern Overview]]
- [[5 Comparative Evaluation]]
- [[6 Cross-Pattern Problems]]
- [[7 Ecosystem and Deployment Landscape]]
- [[8 Scope Boundaries, Related Mechanisms, and Limitations]]
- [[9 Out-of-Scope for Phase A & Inputs to Phase B]]
- [[10 Appendices Overview]]

---

## Patterns

Canonical pattern **definitions** live in [[Appendix A — Pattern Definition Cards]], which contains the authoritative pattern cards for all seven patterns used in this report.

For deeper context, deployment notes, and extended discussion, use the pattern note files:

- [[L1 Overlay – Stealth  OTR]]
- [[L1 Shielded Pools]]
- [[Burn-and-Mint Privacy]]
- [[Permissioned Privacy]]
- [[Private Rollups (Full DA)]]
- [[Private Plasma]]
- [[Private Validium]]

---

## Problems

Detailed problem catalog underlying the “cross-pattern problems” discussion:

- [[01 Transaction Graph Leakage]]
- [[02 Fragmented Anonymity Sets]]
- [[03 High L1 Costs for Private Verification and Data Availability]]
- [[04 Limited Throughput for Privacy-Preserving Rollups]]
- [[05 Lack of User-Resilient Exits]]
- [[06 Trust-Heavy DA Committees and Operators]]
- [[07 Upgrade and Governance Risks for Private Circuits]]
- [[08 Multi-Key Management Complexity]]    
- [[09 Private Fee Payment and Relayer Friction]]
- [[10 Poor Developer Tooling for Private Logic]]
- [[11 Private Execution Leakage in DeFi Primitives]]
- [[12 Lack of Private-to-Private Composability]]
- [[13 Cross-Domain Privacy Leakage in Bridging]]
- [[14 Missing Selective-Disclosure Standards]]
- [[15 Immature Privacy-Preserving Compliance]]
- [[16 Identity Binding Without Linkability]]
- [[17 Monitoring, Observability, and Debugging Blindness]]
- [[18 Incentive Fragility in Privacy Infrastructure]]
- [[19 Network-Layer Metadata Leakage]]

For a structured view and radar-style prioritization, see [[Appendix C — Global Problem Catalog & Radar]].

---

## Metrics

Metric dimensions used in the comparison tables and narrative:

- [[Privacy]]
- [[L1 Gas per Transfer]]
- [[TPS Potential]]
- [[Programmability & Flexibility]]
- [[UX Complexity]]
- [[Readiness]]
- [[Selective Disclosure]]
- [[Trust Assumptions]]

These are the reference points for scores and trade-offs in [[5 Comparative Evaluation]] and [[Appendix B — Comparison Table & Score Justifications]].

---

## Projects

Use these materials to understand concrete deployments and ecosystem coverage:

- [[7 Ecosystem and Deployment Landscape]] – visual overview of key projects and how they map to the seven patterns.
- Follow links from the visual maps into individual project notes in the `05_Projects/` folder for deeper dives.

---

## Appendices (06_Appendices/)

Supporting reference layers that extend the main report
- [[Appendix A — Pattern Definition Cards]] – full pattern cards for all seven patterns.
- [[Appendix B — Comparison Table & Score Justifications]] – detailed comparison table, methodology, and score justifications.
- [[Appendix C — Global Problem Catalog & Radar]] – structured problem catalog and radar built from the problems above.