## **Private Transfers Comparison Table**

### **1. Scoring Methodology**

#### **1.1 Maturity-Weighted Scoring**

Pattern scores are computed as a maturity-weighted average of the live projects inside each pattern.

#### **1.2 Interpretation Rule**

Pattern scores represent the **current real-world deployment characteristics**, not theoretical maxima or minima.

#### **1.3 Rubric (1–5 Scale)**

Scores are normalized across patterns.  
Higher = better across all columns.

---

### **2. Master Comparison Table**

| Pattern                        | Privacy | L1 Gas / Transfer | TPS Potential | Programmability / Flexibility | UX Complexity | Readiness | Selective Disclosure | Trust Assumptions |
| ------------------------------ | :-----: | :---------------: | :-----------: | :---------------------------: | :-----------: | :-------: | :------------------: | :---------------: |
| **L1 Overlay – Stealth / OTR** |    2    |         3         |       3       |               2               |       3       |     3     |          4           |         3         |
| **L1 Shielded Pools**          |    5    |         1         |       2       |               3               |       2       |     3     |          3           |         3         |
| **Burn-and-Mint Privacy**      |    5    |         1         |       2       |               2               |       3       |     2     |          1           |         4         |
| **Permissioned Privacy**       |    2    |         3         |       2       |               3               |       4       |     4     |          5           |         2         |
| **Private Rollups (Full DA)**  |    5    |         4         |       4       |               4               |       2       |     3     |          4           |         4         |
| **Private Plasma**             |    5    |         5         |       5       |               2               |       2       |     2     |          1           |         3         |
| **Private Validium**           |    4    |         5         |       5       |               4               |       4       |     4     |          4           |         1         |

---

### **3. Score Justification Appendix**

#### **3.1 L1 Overlay – Stealth / OTR**

**Privacy — 2**  
Hides only the receiver link; amounts and sender remain public.

**L1 Gas — 3**  
Typical cost around 60k–80k gas.

**TPS — 3**  
Matches base L1 throughput.

**Programmability — 2**  
Designed for payments; no private VM.

**UX — 3**  
Manual monitoring in some implementations; automated flows in others.

**Readiness — 3**  
Multiple mainnets with moderate adoption.

**Selective Disclosure — 4**  
Viewing keys allow optional auditor visibility.

**Trust Assumptions — 3**  
Non-custodial overall; some deployments use trusted services for UX.

---

#### **3.2 L1 Shielded Pools**

**Privacy — 5**  
Fully hides sender, receiver, and amounts.

**L1 Gas — 1**  
Proof-based transfers require very high gas.

**TPS — 2**  
Limited by L1 proof verification.

**Programmability — 3**  
Mixers are rigid; some systems support private DeFi.

**UX — 2**  
Note handling and relayers add friction.

**Readiness — 3**  
Some mature deployments; others in beta.

**Selective Disclosure — 3**  
Varies widely across projects; median supports limited opt-in proofs.

**Trust Assumptions — 3**  
Trusted setups and relayers, but non-custodial funds.

---

#### **3.3 Burn-and-Mint Privacy**

**Privacy — 5**  
Strong unlinkability between burn and mint.

**L1 Gas — 1**  
Burn + proof-mint is costly.

**TPS — 2**  
Limited by verification bottlenecks.

**Programmability — 2**  
Focused on transfers; not a general private compute model.

**UX — 3**  
Sender flow is simple; receiver performs withdrawal proof.

**Readiness — 2**  
Early-stage experiments and wrapper prototypes.

**Selective Disclosure — 1**  
No built-in viewing keys.

**Trust Assumptions — 4**  
Cryptographic trust only; no custodial parties.

---

#### **3.4 Permissioned Privacy**

**Privacy — 2**  
Balances and flows remain visible; identity is abstracted through permissioning.

**L1 Gas — 3**  
Moderate overhead for compliance checks.

**TPS — 2**  
Bound by L1 throughput.

**Programmability — 3**  
Rich compliance logic but not private smart-contract execution.

**UX — 4**  
Post-onboarding transfers feel like normal ERC-20 flows.

**Readiness — 4**  
Broad enterprise and RWA adoption.

**Selective Disclosure — 5**  
Granular, policy-driven selective visibility.

**Trust Assumptions — 2**  
Relies on issuers, registries, and compliance operators.

---

#### **3.5 Private Rollups (Full DA)**

**Privacy — 5**  
Encrypted balances and private transfers.

**L1 Gas — 4**  
Amortized through proof batching.

**TPS — 4**  
Dozens to hundreds of TPS with batching.

**Programmability — 4**  
Supports private smart-contract logic.

**UX — 2**  
Custom wallets, proofs, and L2 flows increase complexity.

**Readiness — 3**  
A few production deployments; others early.

**Selective Disclosure — 4**  
Viewing keys and policy-based disclosures supported in several designs.

**Trust Assumptions — 4**  
Cryptographic correctness + sequencer neutrality; full DA ensures exits.

---

#### **3.6 Private Plasma**

**Privacy — 5**  
Private transfers with minimal on-chain footprint.

**L1 Gas — 5**  
Only a few bytes posted per transaction.

**TPS — 5**  
Thousands of TPS due to off-chain execution.

**Programmability — 2**  
Payments-focused; no general private VM.

**UX — 2**  
Users must maintain local state for safety.

**Readiness — 2**  
Very early deployments and prototypes.

**Selective Disclosure — 1**  
No built-in disclosure mechanisms.

**Trust Assumptions — 3**  
Exit safety depends on operator availability and local data retention.

---

#### **3.7 Private Validium**

**Privacy — 4**  
Private balances but operator/DAC can see plaintext state.

**L1 Gas — 5**  
Amortized verification makes per-tx cost very low.

**TPS — 5**  
Thousands of TPS, horizontally scalable.

**Programmability — 4**  
Often fully VM-capable.

**UX — 4**  
Gasless flows and Web2-style UX in many deployments.

**Readiness — 4**  
Multiple production app-chains with large volume.

**Selective Disclosure — 4**  
Supports sophisticated disclosure and policy proofs.

**Trust Assumptions — 1**  
Strong dependency on DA committees; no trustless exit if DA fails.

---

### **4. Inconsistencies & Gaps**

- Programmability and selective-disclosure capabilities overlap in some patterns.
    
- UX is heavily influenced by data-availability assumptions.
    
- Patterns like Shielded Pools and Private Rollups contain wide internal variance.
    
- Limited empirical UX data for Plasma and Validium.
    
- Some gas data is benchmark-based rather than on-chain.
    
- Roadmaps for key systems (e.g., new private rollups, encrypted Validium) may shift pattern scores.
    
