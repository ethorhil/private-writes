# P07 — Upgrade and Governance Risks for Private Circuits

## 1.1 Problem overview (tl;dr)

Upgrading private circuits and proving systems introduces governance and trust risks. Users must trust that upgrades preserve privacy and correctness; upgrade authority becomes a central point of control. Frequent or opaque upgrades can fragment ecosystems and weaken verifiability.

## 1.2 Stakeholders & pain

- **Users**: Must trust upgrades; may face forced migrations, stuck funds, or privacy regressions.
- **Protocol teams**: Need agility to patch circuits and proving systems while maintaining user trust.
- **Auditors/security reviewers**: Hard to verify circuit changes and proving system updates in time.
- **Integrators**: Must track versions and compatibility; risk breakage across upgrades.

## 1.3 Why it matters (impact)

- Upgrades can silently change privacy guarantees or soundness.
- Governance capture/coercion can weaponize upgrade paths.
- Ecosystem fragmentation increases integration costs and weakens composability.

## 1.4 Current approaches / solution landscape

- Timelocks, multisigs, security councils, and on-chain governance for upgrade authority.
- Public audits, reproducible builds, and transparent release processes.
- "No-upgrade" or minimization of trusted upgrade paths (often impractical).

## 1.5 Gaps / failure modes

- Users can't easily verify circuit/prover changes.
- Upgrade keys concentrate power; emergency upgrades bypass deliberation.
- Multiple versions create incompatibilities (note formats, pools, SDKs).

## 1.6 Success looks like

- Upgrade processes are transparent, externally verifiable, and auditable.
- Upgrade authority is credibly constrained (delays, quorum, escape hatches).
- Ecosystems avoid fragmentation (compatible note formats, migration tooling).

## 2.1 Header

If you remove/neutralize upgrade governance risks for private circuits, you unlock safer iteration and more credible privacy guarantees for users and integrators.

## 2.2 Body

### What is the core of the problem?

Private systems often embed correctness and privacy guarantees in circuits and proving systems. When these components change, users must trust that upgrades preserve soundness and do not introduce backdoors or weaken privacy. Unlike public smart contract upgrades, circuit upgrades can be harder for users to interpret and verify.

### Why is it hard?

Upgrades require:
- Updating on-chain verifiers or consensus rules
- Coordinated migrations of wallets/clients
- Deep cryptographic review of new circuits/provers

Upgrade authority becomes a governance choke point. If captured, coerced, or compromised, it can change the system's rules or privacy properties.

### How does it fail in practice?

- Emergency upgrades under pressure bypass governance checks.
- Upgrade keys are held by small groups; capture/coercion risk remains.
- Repeated upgrades fragment ecosystems (multiple versions, inconsistent support).

## 2.3 Scope & boundaries

In scope:
- Upgrades to private circuits and proving systems
- Governance and trust assumptions around upgrade authority
- User verifiability and ecosystem fragmentation risks

Out of scope:
- General L1/L2 governance design not specific to private circuits
- Non-upgrade-related protocol risk

## 2.4 Assumptions

- Private logic is largely encoded in circuits/provers (not fully transparent to users).
- Upgrades are necessary over time (bugs, performance, cryptographic changes).

## 2.5 Metrics / signals

- Time-to-patch critical circuit/prover bugs
- Upgrade transparency: public diffs, audits, reproducible builds
- Governance decentralization: number/diversity of key holders, delay windows
- Fragmentation: number of concurrent versions supported

## 2.6 Score (1–5)

- **Severity**: 4  
- **Tractability**: 2  
- **Uncrowdedness**: 3  
- **Leverage**: 4  

## 2.7 Evidence & uncertainty

### Key references

- Appendix C: "Global Problem Catalog & Radar"
- Problem file: "Upgrade and Governance Risks for Private Circuits"

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Confidence |
|---|---|---|
| P07-C1 | Zcash's network upgrade mechanism specifies an activation point after which non-upgraded nodes will follow a separate "legacy chain," illustrating that protocol upgrades can partition participants and are operationally high-stakes. | High |
| P07-C2 | The Zcash network upgrade process is deliberately structured (ZIP-defined mechanism + documented guidance), reflecting the coordination overhead involved in upgrading privacy-critical logic across node software and ecosystem infrastructure. | Medium |
| P07-C3 | Zcash Foundation disclosed a "counterfeiting vulnerability" and noted that remediation was delivered via the Sapling upgrade, showing that subtle failures in privacy/cryptographic logic can necessitate urgent upgrades. | Medium-High |
| P07-C4 | Security guidance for upgradeable smart contracts emphasizes that upgradeability shifts trust to the upgrade authority and should be paired with safeguards (e.g., audits, transparency, and safe operational processes). | Medium |
| P07-C5 | Rollup security frameworks treat upgradeability as a core trust assumption and gate higher "decentralization stages" on secure upgradeability properties (e.g., meaningful delays/exit windows), reinforcing that upgrade mechanisms are a material risk surface. | Medium |
| P07-C6 | Applying this to private circuits/provers, upgrade authority and review processes can become de facto governance chokepoints; end-user verifiability typically depends on external artifacts (specs/audits/reproducibility), and evidence for those artifacts is often uneven across implementations. | Medium (partly inference) |
