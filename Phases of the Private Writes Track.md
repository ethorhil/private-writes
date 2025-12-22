

This track studies **privacy-preserving on-chain writes**: transfers, DeFi position workflows, and (later) governance. The work is structured into phases that move from mapping the space to selecting and validating concrete designs.

For orientation, start at [[Private Writes Vault]].

## What the phases do

- **Phase A**: map the landscape and identify recurring constraints.
- **Phase B**: narrow to a small set of candidate designs and specify what to build.
- **Phase C**: prototype, validate, and integrate.

DeFi is treated as a **stress-test vertical** that exposes weaknesses not visible in simple transfer privacy (composability, liquidations, stress-mode liveness).

## Phase A — Landscape & problem discovery

Goal:
- Establish a shared taxonomy, evaluation frame, and vocabulary.
- Identify cross-pattern failure modes that persist across designs.

Key outputs:
- Pattern taxonomy and definition cards.
- Comparative evaluation across privacy, cost, throughput, UX, trust.
- A cross-pattern “problem radar” of recurring issues.
- Ecosystem and deployment snapshot.

Fast orientation:
- [[Private Writes Vault]] → [[1 Summary]] → [[6 Cross-Pattern Problems]]

Transfers:
- [[3 Taxonomy]] → [[5 Comparative Evaluation]] → [[Appendix A — Pattern Definition Cards]]

DeFi:
- [[Overview – DeFi (Private Writes)]] → [[4 Open Problems – DeFi]] → [[Synthesis for PhaseB]]


## Phase B — Narrowing & design selection

Goal:
- Convert the Phase A map into a **shortlist** of viable approaches.
- Make explicit choices on privacy targets, trust assumptions, and public vs. private surfaces.

Typical outputs:
- Candidate shortlist and assumptions.
- Threat / leakage model.
- Architecture sketches and workflow diagrams.
- Cost and performance model.
- Open questions and required experiments.

Primary Phase A inputs:
- [[6 Cross-Pattern Problems]]
- [[Appendix C — Global Problem Catalog & Radar]]
- [[Synthesis for PhaseB]]

## Phase C — Prototyping & validation

Goal:
- Validate privacy properties, failure modes, and integration paths.

Typical outputs:
- Reference implementations and benchmarks.
- Test suites and audit-ready threat models.
- Integration guides and operational lessons.