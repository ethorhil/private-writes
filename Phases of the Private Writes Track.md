This track studies **privacy-preserving on-chain writes**: transfers, DeFi position workflows, and (later) governance. The work is structured into phases that move from mapping the space to ranking constraints and then reducing uncertainty with concrete experiments.

For orientation, start at [[Private Writes Vault]].

## What the phases do

- **Phase A**: map the landscape and identify recurring constraints (patterns + problem catalog).
- **Phase B**: synthesize and rank the recurring problems under multiple prioritization lenses; produce a Phase C experiment backlog.
- **Phase C**: run uncertainty-reduction experiments (benchmarks, measurement, threat models, standards drafts, minimal prototypes) and use the results to guide any deeper build/integration work.

DeFi is treated as a **stress-test vertical** that exposes weaknesses not visible in simple transfer privacy (composability, liquidations, stress-mode liveness).

## Phase A — Landscape & problem discovery

Goal:
- Establish a shared taxonomy, evaluation frame, and vocabulary.
- Identify cross-pattern failure modes that persist across designs.

Key outputs:
- Pattern taxonomy and definition cards.
- Comparative evaluation across privacy, cost, throughput, UX, trust.
- A cross-pattern “problem radar” (P01–P19) of recurring issues.
- Ecosystem and deployment snapshot.

Fast orientation:
- [[Private Writes Vault]] → [[1 Summary]] → [[6 Cross-Pattern Problems]]

Transfers:
- [[Phase A – Private Transfers Landscape]] → [[3 Taxonomy]] → [[5 Comparative Evaluation]] → [[Appendix A — Pattern Definition Cards]]

DeFi (stress test vertical):
- [[Overview – DeFi (Private Writes)]] → [[4 Open Problems – DeFi]] → [[5 Problem Matrix Transfers & DeFi]] → [[Synthesis for PhaseB]]

## Phase B — Ranking problems (decision support)

Phase A produced a descriptive map. Phase B turns that map into **decision support**: a set of one-page problem briefs, an evidence-backed scoring register, and multiple “Top problems” views that reflect different prioritization lenses (impact-first vs near-term feasibility vs under-served vs DeFi-critical).

Goal:
- Make the main obstacles to privacy-preserving on-chain activity legible, comparable, and easy to debate.
- Be explicit about assumptions and tradeoffs (impact, tractability, crowdedness, coordination risk, DeFi stress relevance).
- Produce a portfolio of Phase C experiments that reduce the biggest unknowns without committing to a single architecture.

Key outputs (entry points):
- [[Start here (Summary of Phase B)]] (how to read Phase B, and the main conclusions)
- [[Problems & Ranking Overview (Key Findings)]] (six recurring themes + Top 10 lists under different lenses)
- One-page problem briefs (P01–P19), linked from the Key Findings page
- Supporting syntheses: [[Clusters Synthesis]], [[Rankings & Sensitivity Synthesis]], [[DeFi delta mapping]]
- Proposed next steps: [[Whats Next (Phase C)]] (experiment portfolio + links to the backlog)

## Phase C — Uncertainty reduction & validation

Phase C is framed as a portfolio of experiments (not a single “bet the stack” build). The core output types are:

- Benchmarks (comparability across systems)
- Measurement studies (real-world constraints like fragmentation and effective anonymity)
- Threat models (explicit trust / failure-mode envelopes)
- Minimal standards + conformance suites (coordination and interoperability)

The current Phase C starting point is [[Whats Next (Phase C)]].