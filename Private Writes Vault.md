
This vault is a working research log on **privacy-preserving on-chain writes**: ways to change state (move value, open/modify positions, coordinate/govern) without defaulting to full public traceability.

- Published vault: https://publish.obsidian.md/private-writes
- GitHub (issues / contributions): https://github.com/ethorhil/private-writes

## Start here

If you have 10 minutes:
- How the work is organized: [[Phases of the Private Writes Track]]
- Phase A (Transfers) overview + takeaways: [[1 Summary]]
- Phase A (DeFi) overview + what it changes: [[Overview – DeFi (Private Writes)]]

If you’re trying to *navigate* instead of reading linearly:
- Transfers Phase A index: [[Phase A – Private Transfers Landscape]]
- DeFi Phase A index: [[Overview – DeFi (Private Writes)]] → [[Synthesis for PhaseB]]

## What we’re investigating

We are mapping the design space of “private writes” and the constraints that keep reappearing across systems:

- Practical privacy (not just cryptography): transaction-graph leakage, timing, metadata, bridging, and network-layer exposure.
- Mechanism families (“patterns”) and their trade-offs across **cost**, **throughput**, **trust**, **UX**, **programmability**, and **selective disclosure/compliance**.
- Which problems are *structural* (show up across many patterns) vs. local to a specific design.

Were conducting our research in three Phases:
- Phase A: Ecosystem Mapping And research (completed for transfers and defi)
- Phase B: Determine PSE focus (starting now)
- Phase C: Ecosystem engagement and execition
## High-level results so far

Phase A outputs are intentionally **descriptive** (a factual baseline), not a strategy recommendation.

Private Transfers (Phase A):
- A **7-pattern taxonomy** (overlays, shielded pools, burn-and-mint, private rollups, plasma, validium).
- A **19-item cross-pattern problem catalog** (“problem radar”). Recurring themes include: metadata leakage beyond the proof, fragmented anonymity sets, DA/proving-cost ceilings, exit/liveness fragility, limited private-to-private composability, and missing selective-disclosure standards.
- A shared metric frame and comparative evaluation across those patterns.

![[Appendix B — Comparison Table & Score Justifications#<**2. Master Comparison Table**>]]


Private DeFi (Phase A vertical):
- Uses DeFi as a **worst-case workload** to stress-test the transfers backbone above.
- Key implication: privacy has to hold at the **workflow / position lifecycle** level (not “per transaction”).
- Hard points: unavoidable public/provable global surfaces, liquidation/keeper design, anonymity-set fragmentation coupled to liquidity, and liveness/exits becoming directly financial.

## Where to dig deeper

For the core Phase A materials:
- Compare approaches: [[5 Comparative Evaluation]] + metric notes like [[Privacy]] and [[Trust Assumptions]]
- Browse the problem radar: [[6 Cross-Pattern Problems]] and [[Appendix C — Global Problem Catalog & Radar]]
- Pattern reference cards: [[Appendix A — Pattern Definition Cards]]
- Real deployments and project notes: [[7 Ecosystem and Deployment Landscape]]

For DeFi-specific mapping:
- DeFi pain points lens: [[4 Open Problems – DeFi]]
- Canonical mapping into the transfers problem catalog: [[5 Problem Matrix Transfers & DeFi]]
- Phase B handoff: [[Synthesis for PhaseB]]
