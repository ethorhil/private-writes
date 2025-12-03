
### **Purpose & Scope (Phase A)**

Phase A of the **Private Transfers** track is a **mapping and diagnosis exercise**. Its goal is to describe the main ways users can move value privately on Ethereum and adjacent systems, normalize them into seven concrete **private-transfer patterns**, and compare those patterns using a shared set of metrics:

- [[Privacy]]
- [[L1 Gas per Transfer]]
- [[TPS Potential]]
- [[Programmability & Flexibility]]
- [[UX Complexity]]
- [[Readiness]]
- [[Selective Disclosure]]
- [[Trust Assumptions]]

Phase A also aggregates recurring system-level challenges into a consolidated **[[6 Cross-Pattern Problems|cross-pattern problem radar]]**.

Equally important is what Phase A **does not** do. It does **not** select “winning” designs, recommend where PSE should invest, or propose strategy. All pattern scores are **descriptive rather than prescriptive** — they reflect the current, maturity-weighted shape of real deployments rather than theoretical maxima.  
The outcome is a **shared factual baseline** for understanding how private transfers work today, why they matter for user protection and compliant on-chain finance, and which structural friction points consistently appear across mechanisms.

---

## **High-Level Overview of the Seven Patterns**

### **[[L1 Overlay – Stealth  OTR]]**

Adds address-level privacy via one-time stealth addresses. Sender remains public; amounts remain public. Low gas overhead and inherits Ethereum’s trust model.

### **[[L1 Shielded Pools]]**

Zcash-style nullifier/UTXO pools deployed on L1. Strong privacy (sender, receiver, amount), but high proving costs and low TPS.

### **[[Burn-and-Mint Privacy]]**

Users burn tokens in one context and mint in another with a ZK proof, breaking origin–destination linkage. Strong unlinkability; currently early-stage with non-trivial costs and limited ecosystem maturity.

### **[[Permissioned Privacy]]**

Transfers occur inside an identity-gated or membership-controlled environment with selective disclosure. The same permissioning logic can be layered on any mechanism without changing its core classification.

### **[[Private Rollups (Full DA)]]**

Off-chain private execution with data and proofs posted to L1. Strong privacy, higher throughput than L1-native systems, and trust-minimized through full data availability.

### **[[Private Plasma]]**

Off-chain private execution with periodic commitments to L1. Extremely high throughput and low L1 cost, but introduces exit fragility and operator dependence.

### **[[Private Validium]]**

Execution proved on L1 but data held off-chain. Supports high throughput and programmability, but relies on DA committees and has the weakest trust model in the taxonomy.

Across all patterns, **membership (open vs permissioned)** and **selective disclosure** are **cross-cutting axes**, not standalone patterns.

---

## **Key Trade-Offs Across Patterns**

### **[[Privacy]] vs [[L1 Gas per Transfer|L1 Cost]]**

Stronger privacy (Shielded Pools, Burn-and-Mint, Private Rollups, Plasma, Validium) generally increases proving or DA costs. Overlays trade weaker privacy for cheaper transfers and simpler UX.

### **[[TPS Potential|Throughput& DA Model]] vs [[Trust Assumptions|Trust]]**

Throughput aligns with where data lives:

- L1-native designs cap out at Ethereum throughput.
- Rollups batch and compress, improving TPS.
- Plasma and Validium achieve the highest TPS by moving data off-chain — at the cost of increased trust or exit risk.
    
### **[[Programmability & Flexibility|Programmability vs Simplicity]]**

Overlays, Burn-and-Mint, and Plasma offer simplicity but limited contract expressiveness. Rollups and Validium unlock rich private application logic with greater complexity.

### **[[UX Complexity|UX Friction]]**

Stronger privacy often comes with:

- note management
- relayer flows
- multiple key types
- exit responsibilities (Plasma/Validium)
    
Permissioned systems and some Validium deployments provide smoother UX after onboarding.

### **[[Readiness]]**

Higher readiness today appears in Overlays, Shielded Pools, Permissioned Privacy deployments, and a subset of Private Rollups. Burn-and-Mint and Plasma are emerging. Validium inherits readiness from StarkEx-style systems.

---

## **Cross-Pattern Problems**

1. **[[01 Transaction Graph Leakage|Privacy leakage beyond cryptography]]** — timing, metadata, bridging flows, execution paths.
2. **[[02 Fragmented Anonymity Sets|Fragmented anonymity]]** — pools and L2s divide users into smaller sets.
3. **[[03 High L1 Costs for Private Verification and Data Availability|DA costs, scalability limits, and exit fragility]]** — tension between cost, performance, and trust.
4. **[[08 Multi-Key Management Complexity|UX and key-management challenges]]** — operational failures are common.
5. **[[14 Missing Selective-Disclosure Standards|Immature selective disclosure & compliance integration]]** — lack of standards.
6. **[[12 Lack of Private-to-Private Composability|Limited private composability]]** — multi-app privacy collapses.
7. **[[18 Incentive Fragility in Privacy Infrastructure|Incentive and governance risks]]** — provers, relayers, operators, DA committees.

These structural issues cut across mechanisms and shape the ecosystem landscape.

---

## **Related Mechanisms Not Scored**

General private compute (FHE, iO), TEEs/MPC execution, ordering-privacy systems, identity tooling, and cross-domain privacy transports do not define a private-transfer **state model** and are therefore not included as patterns.

---
## **Known Limitations & Phase B Questions**

Scores are shaped by heterogeneous deployments, inconsistent data, DA assumptions, and emerging roadmaps. These are expected limitations for a first-pass ecosystem map.

Phase B (not part of this report) will address questions such as:

- Which structural problems are most important to address?
- How do different patterns fit PSE’s capabilities and priorities?
- What prototypes or benchmarks would meaningfully advance the field?
- How should identity and ordering privacy integrate with transfer privacy?