## A workplan structure that matches the uncertainty

Phase C should be structured as a portfolio of experiments, not as a single “bet the stack” build. A practical portfolio splits into four experiment types, each with a concrete output format:

1) Benchmarks (comparability)
Output: a canonical workload suite + a metric definition + a reference harness (even if crude).
Purpose: make “leakage,” “throughput under privacy,” and “cost-per-write” comparable across approaches.

2) Measurement studies (real-world constraints)
Output: a methodology + a dataset (or reproducible pipeline) + sensitivity analysis over assumptions.
Purpose: quantify fragmentation, effective anonymity, and where linkability emerges in realistic usage.

3) Threat models (making trust assumptions explicit)
Output: an adversary model + failure mode taxonomy + parameterized risk template.
Purpose: translate vague operator/committee trust questions into explicit, reviewable assumptions.

4) Minimal standards + conformance suites (coordination)
Output: a claim set or interface spec + test vectors + a conformance checklist.
Purpose: reduce ecosystem fragmentation and enable implementations to interoperate safely.

The Phase C backlog already tags each item with a type and links it to the motivating problem briefs. The backlog notes explain why a small subset of problem briefs appears repeatedly in the “high priority across lenses” group. 

## Experiment Backlog

Phase B ends by proposing a set of **uncertainty‑reduction experiments**—benchmarks, measurement studies, threat models, and minimal standards drafts—that can be executed without committing to a particular stack.

The backlog is in this spreadsheet [Phase C backlog](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=1620901530#gid=1620901530) 

The synthesis memo calls out eight high‑leverage experiment items:

- C-002 (Benchmark; linked to [[Supporting Documents/02_PIDs/P01 — Transaction Graph Leakage|P01 — Transaction Graph Leakage]]): Design a motif-leakage benchmark suite: define a small canonical workload set (synthetic traces + parameter ranges), specify output metrics (e.g., candidate set size distributions, linkage classifier precision/recall under defined adversary tiers), and ship a reference harness that can run against simulators or traces. Emphasize comparability and reproducibility over breadth.
- C-006 (Prototype/PoC; linked to [[Supporting Documents/02_PIDs/P05 — Lack of User-Resilient Exits|P05 — Lack of User-Resilient Exits]]): Build a parameterized stress-mode exit simulator: model exit latency/cost as a function of throughput, DA availability assumptions, proof cadence, and congestion. Use it to generate comparative 'exit envelopes' (best/typical/worst) for different pattern assumptions and to identify which parameters most affect user-resilient exits.
- C-011 (Benchmark; linked to [[Supporting Documents/02_PIDs/P11 — Private Execution Leakage in DeFi Primitives|P11 — Private Execution Leakage in DeFi Primitives]]): Create a shared-state leakage benchmark: define inference tasks (e.g., reconstructing position changes) given only public outputs, parameterize by liquidity/volume, and measure attacker performance (precision/recall or error) across a small set of DeFi primitives (AMM, lending, liquidation events).
- C-013 (Benchmark; linked to [[Supporting Documents/02_PIDs/P12 — Lack of Private-to-Private Composability|P12 — Lack of Private-to-Private Composability]]): Define a representative private composability workflow suite (e.g., deposit→borrow→swap→LP; adjust collateral; unwind under stress) and document where declassification occurs (public detours, boundary hops, shared-state leakage). Provide a harness spec for comparing how different approaches support (or break) these workflows.
- C-015 (Standards Draft; linked to [[Supporting Documents/02_PIDs/P14 — Missing Selective-Disclosure Standards|P14 — Missing Selective-Disclosure Standards]]): Draft a minimal selective-disclosure claim set and conformance suite: specify claims (and non-claims), encode them in a testable format with vectors, and document revocation/rotation semantics that avoid stable pseudonyms. Emphasize least-privilege and interoperability for integrators.
- C-007 (Threat Model; linked to [[Supporting Documents/02_PIDs/P06 — Trust-Heavy DA Committees and Operators|P06 — Trust-Heavy DA Committees and Operators]]): Develop a DA/committee threat model and quantification template: enumerate withholding/censorship/coercion scenarios, define measurable indicators (committee size/threshold/rotation, external auditing, recovery paths), and provide a simple quantitative 'risk envelope' model with sensitivity to adversary power and committee concentration.
- C-010 (Standards Draft; linked to [[Supporting Documents/02_PIDs/P09 — Private Fee Payment and Relayer Friction|P09 — Private Fee Payment and Relayer Friction]]): Draft a wallet-facing interface requirements note for private relaying/fee abstraction: specify required fields and behaviors that minimize metadata (avoid stable identifiers), expose censorship/availability signals, and support safe fallback. Keep it as a requirements/conformance document, not a protocol proposal.
- C-003 (Measurement Study; linked to [[Supporting Documents/02_PIDs/P02 — Fragmented Anonymity Sets|P02 — Fragmented Anonymity Sets]]): Define comparable 'effective anonymity set' metrics (entropy/candidate-set style) and run a measurement study that characterizes fragmentation drivers: asset type, venue, chain, and workflow class. Where direct measurement is infeasible, specify a reproducible sampling methodology and a synthetic calibration model to bound uncertainty.
