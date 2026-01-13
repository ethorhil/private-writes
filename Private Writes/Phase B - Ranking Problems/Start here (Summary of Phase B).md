
## Summary

This memo is the summary of Phase B (“Private Writes”). It describes the main problems of privacy‑preserving on‑chain activity, groups them into a small set of recurring themes, and shows how the priority list changes under different ways of ranking problems (for example: impact‑first vs “feasible in 1–3 years” vs “DeFi‑focus”). It links to the supporting evidence: one‑page problem briefs and a scored register with rationale fields and citations. It also links to a short backlog of “uncertainty‑reduction experiments” proposed for the next phase. This memo does not recommend a single architecture or technical stack; it is meant to help readers decide what to investigate, measure, or coordinate on next.

## What Phase B produced

Phase B output is best understood as three linked artifacts:

1) [[Problems & Ranking Overview (Key Findings)]]: short write-ups of recurring problems of privacy-preserving on-chain activity. Grouped into recurring themes and ranked by 2) below. Contains concrete lists themes, Top 10s under different lenses, and the highlighted experiment IDs.

2) A scored register: a spreadsheet-style register that records per-problem scores and the rationale/evidence used for those scores. The point of the register is not a single “true ranking,” but to make tradeoffs legible and to support multiple ranking views. See [spreadsheet](https://docs.google.com/spreadsheets/d/1d_3HSmVSDhDjW5YqhdwZSc9SffQuvtWeheBHv5TKCf4/edit?gid=0#gid=0).

3) A Phase C experiment backlog: a shortlist of uncertainty-reduction experiments (benchmarks, threat models, standards drafts, and prototypes) intended to reduce the biggest unknowns without committing to one architecture. See [[Whats Next (Phase C)]].

## How to interpret Phase B’s priorities

The register and its ranked views are a structured way to answer: “What seems to block real-world privacy-preserving activity most often, and what is plausibly addressable next?” They are not a forecast of what will happen, and they are not a verdict on any one technical approach.

## Three decision-relevant conclusions

### 1) Privacy is most fragile at boundaries, not in the cryptography

In practice, privacy fails when a user crosses a boundary: entering or exiting a private system, bridging across domains, paying fees, routing transactions, or repeating a recognizable workflow. Even strong cryptography cannot compensate for stable identifiers, repeated patterns, or metadata leakage.

Implication: prioritize work that reduces boundary leakage and makes “end-to-end workflow privacy” testable. This is why benchmarks and measurement are important (so different systems can be compared on the same leakage questions), not only on new proving performance.

### 2) Liveness and exits are privacy problems, not just engineering details

When systems are congested or adversarially pressured, the ability to exit safely (and to do so without relying on trusted operators) becomes a first-order constraint. In DeFi-like workflows, being unable to exit can turn into time-bounded financial loss; even outside DeFi, constrained exit paths can force users into public “escape hatches” that destroy privacy.

Implication: evaluate privacy systems under stress-mode assumptions (censorship, DA withholding, congestion, sequencer/operator failure), not only under happy-path throughput numbers. This is one reason we emphasize threat models and stress simulators: they make exit guarantees comparable and explicit.

### 3) Standardization and “boring plumbing” are leverage points

A large fraction of real-world friction comes from missing standards and missing interfaces: selective disclosure formats, wallet/relayer UX conventions, monitoring without privacy backdoors, and consistent metrics for anonymity and leakage. These are not glamorous, but they reduce fragmentation, improve composability, and allow multiple implementations to share an ecosystem.

Implication: treat standards drafts, conformance (TODO: dont know conformance, change word) suites, and shared metrics as core deliverables. Even partial standardization can unlock cross-project interoperability and reduce ecosystem-level fragmentation effects.

## Choosing a prioritization lens

Depending on high level direction one can intentionally choose a lens rather than defaulting to whatever “Top 10” one saw first.

If you are building a near-term product or deployment, you will care about feasibility and operational risk: what can be delivered within real constraints, and what fails in production conditions (key management, fee payment, operator trust, monitoring).

If you are funding ecosystem infrastructure, you should overweight under-served, high-leverage problems that create positive spillovers: shared standards, shared benchmarks, and composability enablers. These reduce duplication and make future work cheaper.

If you are an ecosystem steward (trying to improve the whole environment), you should overweight fragmentation dynamics: anything that increases shared anonymity sets, reduces cross-domain leakage, and improves safe interoperability tends to compound.

For a compact summary of how the Top 10 shifts under several baseline lenses, see the “Rankings depend on the prioritization lens” section in [[Problems & Ranking Overview (Key Findings)]].

## What could change the conclusions

Several factors could shift the effective priority order over time:

- If L1/L2 cost structures change materially, some cost and throughput constraints may become less binding, while boundary leakage and fragmentation remain.
- If one or two systems reach dominant adoption, ecosystem fragmentation effects may weaken—but the stakes of their governance and exit guarantees increase.
- If regulatory and compliance expectations shift quickly, selective disclosure and privacy-preserving compliance could become a gating requirement for broad deployment.
- If wallet and RPC defaults shift (e.g., better metadata protection becomes common), some network-layer risks may compress, but application-layer motif leakage can remain.

This memo should therefore be read as a “current best map of constraints,” designed to be updated as the Phase C experiments resolve unknowns.
