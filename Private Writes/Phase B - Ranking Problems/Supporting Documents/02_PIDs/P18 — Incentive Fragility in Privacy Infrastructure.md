# P18 — Incentive Fragility in Privacy Infrastructure

## 2.1 Header

- **PID:** P18 — Incentive Fragility in Privacy Infrastructure
- **Clusters:** `Governance & operational risk`
- **Patterns bound:** `L1 Overlay – Stealth  OTR`; `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Permissioned Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`

## 2.2 Problem statement

### Definition

Privacy-preserving systems depend on auxiliary infrastructure roles (e.g., relayers, provers, operators, DA providers/committees, keepers in DeFi-like settings). When the incentive structures for these roles are immature, subsidized, or unstable, system liveness and reliability degrade—often at the times when dependable service is most needed (fee spikes, adversarial load, volatility). Incentive fragility can also concentrate power into a small set of providers, increasing censorship, trust, and privacy risks.

What this is not: this PID is not the same as “trust-heavy DA committees and operators” (P06), which is about DA trust assumptions and withholding risk; P18 is about whether required roles are sustainably provided and incentive-compatible over time, including under stress.

### Why it matters

If the required infrastructure is not reliably provided, privacy systems become operationally fragile: users experience outages, delayed inclusion, or coercive chokepoints, and may be forced into fallback behaviors that reduce privacy. Concentrated infrastructure providers also create governance and censorship leverage that can undermine both safety and privacy guarantees.

### Affected workloads

Transfers (baseline):
- Private transfers depend on relayers, provers, and/or DA providers; incentives are often immature or subsidized.
- Under adverse conditions (fee spikes, load), infrastructure can degrade (slower inclusion, censorship, outages), harming liveness and UX.
- Incentive designs can create centralized chokepoints (small relayer sets, privileged provers), compounding trust and privacy risk.

DeFi stress-test lens:
- DeFi introduces time-sensitive roles (keepers/liquidators) and stress dynamics (volatility) where incentive failures are most damaging.
- Private liquidations can concentrate privileged roles, increasing fragility and governance power under stress.
- DeFi profit motives can destabilize “neutral” infra roles; liveness failures become protocol risk (distinct from DA trust assumptions).

## 2.3 Failure modes & success

### Failure modes / symptoms

- “Best-effort” infra becomes unavailable during fee spikes or adversarial load; inclusion latency increases beyond what users can tolerate.
- A small number of relayers/provers/operators become de facto gatekeepers due to economics, creating censorship and privacy risks.
- Roles required for safety actions in DeFi-like contexts (e.g., liquidation/keeper workflows) require privileged access, creating fragility and governance leverage.
- Systems become dependent on ongoing subsidies, making long-run service guarantees unclear.

### What success looks like (measurable)

- For each pattern class, the set of required always-on roles is explicit, and there is measurable evidence of service robustness (availability and inclusion performance) across adverse conditions rather than only in steady-state.
- There is provider diversity for critical roles (no single provider is a hard dependency), and provider churn does not break liveness for users.
- The system does not require users to sacrifice privacy (e.g., by reusing identifiable infra paths) in order to obtain timely inclusion under stress.

## 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 3
- Tractability (1–3y): 3
- Crowdedness: Medium
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

## 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| L1 Overlay – Stealth  OTR | Operation often relies on scanning/notifier infrastructure; incentives must avoid central single-provider dependencies that can become chokepoints or correlated observers. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Overlay – Stealth  OTR.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/18 Incentive Fragility in Privacy Infrastructure.md` |
| L1 Shielded Pools | Relayers/provers/paymasters are often needed for usable UX; incentives must sustain liveness without forcing users into a small, fingerprintable relayer set. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Shielded Pools.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| Burn-and-Mint Privacy | Proving and submission infrastructure must remain available across time and load; incentive fragility can cause “stuck” redemption/settlement flows and centralization of proving services. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Burn-and-Mint Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/18 Incentive Fragility in Privacy Infrastructure.md` |
| Permissioned Privacy | Governed operators and privileged service roles may rely on institutional incentives; fragility or misalignment can translate into censorship, freezes, or degraded service, with limited user recourse. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Permissioned Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c14e56` |
| Private Rollups (Full DA) | Sequencer/prover roles are central to liveness and UX; incentives must support timely posting/inclusion under stress to prevent systemic degradation or coercive gatekeeping. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Rollups (Full DA).md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| Private Plasma | Safety relies on operators plus active monitoring and exit behavior; incentives for operators and watchdog-like roles affect whether users can realistically self-protect during disputes or mass-exit events. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Plasma.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c14e56` |
| Private Validium | DA committees/operators are required for availability; incentives must reliably fund data serving and resistance to stress-induced outages, or users face persistent liveness degradation. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Validium.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/18 Incentive Fragility in Privacy Infrastructure.md` |

## 2.6 Intervention modes (non-prescriptive)

- Research  
  Mechanism design and incentive analysis for relayer/prover/DA roles under adversarial load; characterization of “always-on” versus “best-effort” services in private systems; failure analysis under stress.

- Engineering  
  Instrumentation and benchmarks for liveness and service quality across adverse conditions; designs that degrade gracefully when optional infra is unavailable; operational playbooks for provider churn.

- Standards / coordination  
  Common role definitions and interfaces for privacy infrastructure (relayer/prover service expectations); shared measurement approaches for availability and censorship indicators that can be compared across projects.

- Grants / convening  
  Support neutral measurement and benchmarking efforts; convene cross-project discussions about sustainable infra provisioning and the privacy risks of concentrated service roles.

## 2.7 Evidence & uncertainty

### Key references

- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/18 Incentive Fragility in Privacy Infrastructure.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^c14e56`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md`

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Uncertainty / notes |
|---|---|---|
| P18-C1 | Privacy systems often rely on intermediating infrastructure (e.g., relayers) to submit transactions on behalf of users, which becomes a critical dependency and potential single-point fragility. | Specific mechanics differ by protocol; reliance can be reduced with wallet-level features but not eliminated. |
| P18-C2 | Relay/relayer operation has real ongoing costs and sustainability challenges; operator communities explicitly discuss incentivization and fairness as open problems. | Tor's relay model differs from blockchain relayers, but the sustainability dynamics are analogous. |
| P18-C3 | Some privacy infrastructures propose explicit cryptoeconomic reward sharing to incentivize mix nodes and sustain network capacity as usage grows. | Economic models are sensitive to assumptions (fee markets, adversarial nodes, reserve design). |
| P18-C4 | Incentive design is a recurring requirement in P2P infrastructures to achieve participation, reliability, and security; privacy networks inherit these incentive-mechanism problems. | Broad literature; mapping results directly onto privacy-mix networks requires care. |
| P18-C5 | Weak or misaligned incentives can drive centralization (fewer relays/mix nodes) or degraded privacy (smaller anonymity sets), undermining security assumptions that rely on diverse participation. | Evidence is partly inferential; empirical measurements differ by network and time. |
| P18-C6 | Overall, privacy infrastructure incentive fragility remains a key risk because the infrastructure is often external to L1 security, can be under-funded, and is exposed to non-technical pressures (e.g., legal risk). | Synthesis claim; severity depends on governance and whether infrastructure is permissioned/regulated. |


### Key uncertainties (Sprint 1)

- Which infrastructure roles are strictly required for safety/liveness versus optional for UX, and how that differs by pattern.
- Whether incentive structures can be made robust without concentrating power (chokepoints) that undermine privacy and governance assumptions.
- How “stress-mode” economics (fee spikes, volatility) change the incentive landscape for privacy infrastructure roles.

### What would change the score

- Evidence of durable, non-fragile provisioning for critical privacy infrastructure roles (measured performance under adverse conditions and provider diversity over time).
- Demonstrations that private DeFi-like safety actions (time-sensitive operations) can function without relying on a narrow set of privileged, centralized service providers.

---