# P19 — Network-Layer Metadata Leakage

## 2.1 Header

- **PID:** P19 — Network-Layer Metadata Leakage
- **Clusters:** `Privacy leakage & anonymity`; `UX & developer experience`
- **Patterns bound:** `L1 Overlay – Stealth  OTR`; `L1 Shielded Pools`; `Burn-and-Mint Privacy`; `Permissioned Privacy`; `Private Rollups (Full DA)`; `Private Plasma`; `Private Validium`

## 2.2 Problem statement

### Definition

Even when on-chain payloads are private, users can be correlated and deanonymized via network- and submission-layer metadata: RPC endpoint choice, timing and ordering characteristics, sequencer/relayer routing, client fingerprints, and other routing and interaction signals. These correlations can link actions across time and across pools/venues, leaking identity or strategy “outside the cryptographic layer.”

What this is not: this PID is about off-chain submission and network metadata correlation, not on-chain interaction graph motifs (P01), not cross-domain bridge/exit linkage (P13), and not private execution leakage via shared-state market behavior (P11).

### Why it matters

If network metadata is linkable, privacy guarantees can fail in practice even if cryptographic shielding is correct. In addition, the mitigations people use for UX (stable endpoints, preferred relayers, automation for time-sensitive actions) can create stronger and more repeated identifiers, making privacy degradation systematic rather than incidental.

### Affected workloads

Transfers (baseline):
- RPC/mempool/sequencer metadata (timing, ordering, endpoint choice) can correlate actions to a user.
- Network identifiers (IP/routing, client fingerprints) can link otherwise-unlinkable transfers across time and across pools.
- Relayers can reduce some exposure but also introduce another observer; relayer routing can become its own fingerprint.

DeFi stress-test lens:
- DeFi actions are bursty and time-sensitive (especially near liquidation), strengthening timing-based correlation.
- Strategies often require repeated submissions (position management), creating repeated network interactions per strategy.
- Keeper/liquidator automation can have identifiable network footprints.

## 2.3 Failure modes & success

### Failure modes / symptoms

- A user’s private actions become linkable because they repeatedly use the same endpoint(s), relay path(s), or exhibit distinctive timing patterns.
- Attempts to improve UX (automation, preferred routes, time-critical submissions) amplify correlation risk, especially during stress windows.
- A small number of infra providers observe and can potentially correlate traffic, even if on-chain data is shielded.

### What success looks like (measurable)

- Users can submit private actions without a stable network identifier being necessary for liveness (endpoint diversity or privacy-bounded submission paths are feasible by default).
- Correlation risk from submission metadata is explicitly modeled and measurably reduced (e.g., demonstrable reduction in linkability of repeated actions under realistic adversary models).
- Reliance on relayers/sequencers does not force a single, fingerprintable routing behavior for most users.

## 2.4 Baseline scoring snapshot

Reference values from the Problem Register; no recomputation.

- Impact: 4
- Tractability (1–3y): 3
- Crowdedness: Medium
- Coordination risk: TBD (Sprint 4 scoring)
- DeFi stress-test relevance: TBD (Sprint 4 scoring)
- Horizon tag: TBD (Sprint 4 scoring)

## 2.5 Binding constraints by pattern

| Pattern | Constraint description | Evidence pointer |
|---|---|---|
| L1 Overlay – Stealth  OTR | Overlay privacy can be undermined if transaction submission patterns or scanning/notification flows are linkable at the network layer; endpoint and timing metadata can re-link stealth usage to identities. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Overlay – Stealth  OTR.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/19 Network-Layer Metadata Leakage.md` |
| L1 Shielded Pools | Shielded payloads do not prevent network-level correlation; relayers may help but can become correlated observers if routing choices are stable or distinctive. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/L1 Shielded Pools.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md` |
| Burn-and-Mint Privacy | Burn/mint flows can be correlated through timing and routing, even if the on-chain linkage is cryptographically hidden; submission metadata can reintroduce the very link the pattern aims to break. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Burn-and-Mint Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/19 Network-Layer Metadata Leakage.md` |
| Permissioned Privacy | Permissioned environments often use identifiable endpoints and controlled infrastructure; network metadata can leak participation and repeated activity patterns even when on-ledger visibility is restricted. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Permissioned Privacy.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/19 Network-Layer Metadata Leakage.md` |
| Private Rollups (Full DA) | Users interact with sequencers/RPC providers; submission timing and routing can correlate repeated actions, especially for time-sensitive operations in DeFi-like workloads. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Rollups (Full DA).md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md` |
| Private Plasma | Operator-mediated systems can produce strong network-level identifiers (operator endpoints, watcher behavior); repeated interactions can link users or strategies even if state is private. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Plasma.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/19 Network-Layer Metadata Leakage.md` |
| Private Validium | DA committees/operators and their access paths can become stable routing fingerprints; network metadata can leak user correlation despite private execution. | `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/02_Patterns/Private Validium.md`; `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/19 Network-Layer Metadata Leakage.md` |

## 2.6 Intervention modes (non-prescriptive)

- Research  
  Threat modeling and measurement for submission-layer adversaries; analysis of how time sensitivity and repeated workflows affect metadata linkability; evaluation methodologies for correlation risk.

- Engineering  
  Client and infra approaches that reduce stable submission identifiers and avoid single-path routing dependencies; designs that avoid turning relayers/sequencers into unavoidable correlated observers.

- Standards / coordination  
  Shared interfaces and expectations for “private submission” surfaces across patterns; common terminology and metrics so projects can compare mitigations without conflating on-chain privacy with network privacy.

- Grants / convening  
  Support neutral evaluation and benchmarking of metadata leakage risks; convene cross-project work on submission-layer privacy as part of the private-write threat model.

## 2.7 Evidence & uncertainty

### Key references

- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/03_Problems/19 Network-Layer Metadata Leakage.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/06_Appendices/Appendix C — Global Problem Catalog & Radar.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^3cb481`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Transfers/01_Report/6 Cross-Pattern Problems.md#^be95db`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/5 Problem Matrix Transfers & DeFi.md`
- `Private-Writes/Private Writes/Phase A - Discovery & Landscape Mapping/Private Defi/Report/Synthesis for PhaseB.md`

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Uncertainty / notes |
|---|---|---|
| P19-C1 | Cryptocurrency P2P networking can enable user deanonymization by linking transaction broadcast behavior to IP addresses (network-layer source inference). | Attack success depends on adversary placement, network topology, and protocol details. |
| P19-C2 | Network-protocol changes do not automatically fix anonymity; analyses of post-change protocols can still find poor anonymity properties under plausible models. | Models may not capture all real-world dynamics; results can vary by deployment. |
| P19-C3 | Propagation-layer redesigns (e.g., Dandelion) are proposed specifically to improve anonymity by obscuring the transaction source during broadcast. | Adoption and parameter choices matter; improvements can be undermined by powerful adversaries. |
| P19-C4 | Ethereum's P2P layer can leak metadata sufficient to deanonymize some validators, suggesting that even infrastructure participants have meaningful network-layer privacy exposure. | Validator deanonymization results may shift with client changes, relay usage, and network evolution. |
| P19-C5 | Network-layer metadata leakage persists even when on-chain data is private; an adversary can correlate timing and network identifiers with otherwise private actions. | Strength of correlation depends on user behavior and whether network privacy layers (e.g., Tor) are used correctly. |
| P19-C6 | Overall, network-layer metadata (IP, timing, RPC/relay selection) remains a structural leak vector that can undermine private transfers unless explicitly addressed. | Synthesis claim; mitigations can introduce performance/usability tradeoffs and new trust assumptions. |


### Key uncertainties (Sprint 1)

- The practical adversary model to use for “metadata correlation” across patterns (who observes what, and at what scale).
- The extent to which UX-driven defaults (preferred endpoints, automation) can be changed without pushing users into worse failure modes.
- Where the boundary should sit between “submission privacy” and other adjacent tracks (e.g., ordering privacy), without treating network privacy as optional.

### What would change the score

- Evidence of broadly deployable submission-layer privacy approaches that materially reduce correlation of repeated private actions under realistic conditions (including time-sensitive scenarios).
- Demonstrated patterns where using relayers/sequencers does not create a stable routing fingerprint for most users, and where residual metadata leakage is explicitly bounded and measured.

---