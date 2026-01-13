This vault is a working research log on **privacy-preserving on-chain writes**: ways to change state (move value, open/modify positions, coordinate/govern) without defaulting to full public traceability.

- Published vault: https://publish.obsidian.md/private-writes
- GitHub (issues / contributions): https://github.com/ethorhil/private-writes

## Start here

If you have 10 minutes:
- How the work is organized: [[Phases of the Private Writes Track]]
- Phase B (current priorities + what to do next): [[Start here (Summary of Phase B)]] → [[Problems & Ranking Overview (Key Findings)]]
- Phase A (Transfers) overview + takeaways: [[1 Summary]]
- Phase A (DeFi stress test) overview + what it changes: [[Overview – DeFi (Private Writes)]]

If you’re trying to *navigate* instead of reading linearly:
- Transfers Phase A index: [[Phase A – Private Transfers Landscape]]
- DeFi Phase A index: [[Overview – DeFi (Private Writes)]] → [[Synthesis for PhaseB]]
- Phase B index (ranking + experiments): [[Start here (Summary of Phase B)]] → [[Problems & Ranking Overview (Key Findings)]] → [[Whats Next (Phase C)]]

## What we’re investigating

We are mapping the design space of “private writes” and the constraints that keep reappearing across systems:

- Practical privacy (not just cryptography): transaction-graph leakage, timing, metadata, bridging, and network-layer exposure.
- Mechanism families (“patterns”) and their trade-offs across **cost**, **throughput**, **trust**, **UX**, **programmability**, and **selective disclosure / compliance**.
- Which problems are *structural* (show up across many patterns) vs. local to a specific design.

This research is structured in three phases:
- Phase A: landscape mapping and problem discovery (completed for transfers + DeFi stress test).
- Phase B: ranking problems and producing decision support (completed; produces a scored register, one-page problem briefs, and a Phase C experiment backlog).
- Phase C: uncertainty-reduction experiments and ecosystem engagement (next; benchmarks, threat models, standards drafts, and minimal prototypes).

## High-level results so far

Phase A outputs are intentionally **descriptive** (a factual baseline), not a strategy recommendation.

Private Transfers (Phase A):
- A **7-pattern taxonomy** (overlays, shielded pools, burn-and-mint, permissioned privacy, private rollups, plasma, validium).
- A **19-item cross-pattern problem catalog** (“problem radar”). Recurring themes include: metadata leakage beyond the proof, fragmented anonymity sets, DA/proving-cost ceilings, exit/liveness fragility, limited private-to-private composability, and missing selective-disclosure standards.
- A comparative evaluation across those patterns (see [[5 Comparative Evaluation|here]] for justification of scores).

Private DeFi (Phase A vertical):
- Uses DeFi as a **worst-case workload** to stress-test the transfers backbone above.
- Key implication: privacy has to hold at the **workflow / position lifecycle** level (not “per transaction”).
- Hard points: unavoidable public/provable global surfaces, liquidation/keeper design, anonymity-set fragmentation coupled to liquidity, and liveness/exits becoming directly financial.

Phase B (Ranking Problems):
- Produces **19 one-page problem briefs** (P01–P19) and groups them into **six recurring themes** (see [[Problems & Ranking Overview (Key Findings)]] and [[Clusters Synthesis]]).
- Builds an evidence-backed **problem register** (scores + rationales) and shows how “Top problems” change under different prioritization lenses (impact-first, impact × feasibility, under-served, DeFi-critical).
- Ends with a **Phase C experiment backlog**: a portfolio of benchmarks, measurement studies, threat models, and minimal standards drafts (see [[Whats Next (Phase C)]]).

## Where to dig deeper

Phase B materials (recommended if you want “what seems to matter most”):
- Start with: [[Start here (Summary of Phase B)]]
- Key findings + ranked views: [[Problems & Ranking Overview (Key Findings)]]
- Sensitivity / what changes under different lenses: [[Rankings & Sensitivity Synthesis]]
- DeFi-specific checklist of what changes under workflows: [[DeFi delta mapping]]
- Proposed next steps: [[Whats Next (Phase C)]]

Phase A materials (recommended if you want the full map and primary sources):
- Compare approaches: [[5 Comparative Evaluation]]
- Browse the problem radar: [[6 Cross-Pattern Problems]] and [[Appendix C — Global Problem Catalog & Radar]]
- Pattern reference cards: [[Appendix A — Pattern Definition Cards]]
- Real deployments and project notes: [[7 Ecosystem and Deployment Landscape]]

DeFi-specific mapping (Phase A):
- DeFi pain points lens: [[4 Open Problems – DeFi]]
- Canonical mapping into the transfers problem catalog: [[5 Problem Matrix Transfers & DeFi]]
- Phase A → Phase B handoff: [[Synthesis for PhaseB]]