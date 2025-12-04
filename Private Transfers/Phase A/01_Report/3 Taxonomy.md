
## 3.1 Primary Classification Axis

The Phase A taxonomy organizes private-transfer systems along a **primary mechanism axis** that focuses on:

- how **private balances are represented** (state model), and
- how **data availability and correctness** are enforced (DA / trust model).

On this axis, Phase A defines **seven canonical private-transfer patterns**:

1. **[[L1 Overlay – Stealth  OTR]]**  
    Private balances remain in standard L1 accounts. Privacy is added by routing funds through **one-time stealth addresses** on Ethereum L1.
    
2. **[[L1 Shielded Pools]]**  
    Users hold encrypted UTXO-like notes inside an on-chain pool. Privacy is enforced via **nullifiers and zk proofs** directly on L1.
    
3. **[[Burn-and-Mint Privacy]]**  
    Users **burn** tokens in one context and **mint** in another with a proof that the burn and mint are well-formed, breaking origin–destination links.
    
4. **[[Permissioned Privacy]]**  
    Transfers take place inside an **access-controlled environment** where membership, identity gating, and selective disclosure are the primary design axes.
    
5. **[[Private Rollups (Full DA)]]**  
    A separate private state machine executes off-chain but posts **transaction data and validity proofs** to L1, achieving strong privacy with full on-chain DA.
    
6. **[[Private Plasma]]**  
    Private transfers execute off-chain; state roots and fraud/exit proofs are periodically committed to L1. Users rely on **challenge/exit semantics and local data** for safety.
    
7. **[[Private Validium]]**  
    Execution is proven with zk proofs, but **transaction data is held off-chain** by a DA committee or operator. This enables high throughput and programmability at the cost of stronger trust assumptions.

Under this taxonomy, these seven patterns are **mutually exclusive labels for how private state is represented and secured**. They are the only patterns scored and used as the backbone for the comparison table and ecosystem map.

---

## 3.2 Cross-Cutting Axis: Membership, Visibility, Selective Disclosure

While the primary axis groups systems by mechanism and DA model, **real deployments vary dramatically in who may join and who may see what**. We treat **membership, visibility, and selective disclosure (SD)** as **cross-cutting attributes**, not separate patterns.

Key clarifications:
- **Membership (open vs permissioned)**
    - _Open_: anyone with an address can join and use the system.
    - _Permissioned_: access is gated by KYC, whitelists, or other governance processes.
        
- **Visibility & Selective Disclosure**
    - Systems differ in whether balances and flows can be selectively revealed to auditors, compliance teams, counterparties, or regulators.
    - We distinguish between **no SD**, **ad-hoc SD**, **protocol-level SD**, and **rich-policy SD** (e.g., structured proofs-of-innocence).

Crucially, **“[[Permissioned Privacy]]” as a pattern** refers to deployments where **controlled membership and compliance-friendly disclosure are the primary design drivers**. Mechanistically, similar permissioning and SD layers can be stacked on top of other patterns (e.g., Shielded Pools or Validium) **without changing the underlying pattern classification**.

We offers several rules of thumb:
- A **KYC-restricted shielded pool** is classified as **L1 Shielded Pool** with a **permissioned attribute**, _not_ as Permissioned Privacy.
- A **consortium Validium** is still **Private Validium** with a **permissioned attribute**.
- An **open shielded pool** is just **L1 Shielded Pool**.
- A **rollup with protocol-level selective disclosure** is still **Private Rollup (Full DA)** with an SD attribute.

This separation keeps the taxonomy focused on **state and DA model**, while still capturing **governance and compliance posture** as annotated attributes.

---

## 3.3 Classification Recipe and Examples

We provide a **three-step classification recipe** to consistently place projects into the taxonomy.

### Step 1 — Identify Mechanism / DA Model

1. **Is private state directly on L1?**
    - If yes, the project is one of: **L1 Overlay**, **L1 Shielded Pool**, or **Burn-and-Mint**.
2. **Is there a separate private state machine with full DA on L1?**
    - If yes → **Private Rollup (Full DA)**.
3. **Is there a private state machine with validity proofs but off-chain DA?**
    - If yes → **Private Validium**.
4. **Do exits rely on challenge semantics and user-held data (classic Plasma-style)?**
    - If yes → **Private Plasma**.

At this stage, each project is assigned **exactly one of the seven patterns**.

### Step 2 — Mark Membership and Visibility

Once the mechanism is identified, mark the deployment with attributes:
- **Membership:** open / permissioned
- **Visibility / SD:** none / ad-hoc / protocol-level / rich-policy

These are **tags** attached to the pattern, not new patterns.

### Step 3 — Tag Selective Disclosure & Compliance Profile

Finally, annotate how the system handles disclosures and compliance:
- **None / ad-hoc SD** – e.g., Tornado-like flows with no formal SD layer.
- **Protocol-level SD** – e.g., association-set proofs or structured viewing keys.
- **Rich-policy SD** – e.g., deployments where fine-grained compliance policies and proofs-of-innocence are a core part of the design.

### Concrete Examples

1. **Permissioned Validium for RWAs**    
    - Mechanism: Validity proofs + off-chain DA committee → **Private Validium**.
    - Membership: KYC-gated consortium → **permissioned attribute**.
    - SD: detailed audit disclosures → **rich-policy SD attribute**.  
        → **Classification:** _Private Validium_ (pattern) with **permissioned + rich-policy SD** attributes — **not** Permissioned Privacy.
        
2. **KYC’d L1 Shielded Pool**
    - Mechanism: UTXO/nullifier pool on L1 → **L1 Shielded Pool**.
    - Membership: users must pass KYC → **permissioned attribute**.
    - SD: per-note disclosures to auditors → SD attribute.  
        → **Classification:** _L1 Shielded Pool_ with **permissioned + SD** attributes.
        
3. **Rollup with Structured Selective Disclosure**
    - Mechanism: private rollup with full DA on L1 → **Private Rollup (Full DA)**.
    - Membership: open participation; anyone can transact.
    - SD: protocol-level viewing keys or proofs-of-innocence → **protocol-level SD**.  
        → **Classification:** _Private Rollup (Full DA)_ with a **protocol-level SD** attribute.

These examples illustrate the core principle:

> **First classify by mechanism and DA model, then annotate membership and disclosure.  
> Permissioned Privacy is reserved for deployments where permissioning and SD are the primary design axes, not just attributes layered onto another mechanism.**
