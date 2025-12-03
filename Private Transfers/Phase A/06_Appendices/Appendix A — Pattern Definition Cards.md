## 1. **L1 Overlay – Stealth / OTR**

#### **One-sentence definition**

A pattern where the sender derives a fresh, one-time address for the recipient so the on-chain payment cannot be linked to the recipient’s public identity.

#### **Mechanism summary**
- Sender and recipient derive a unique stealth address via off-chain exchange.
- Funds are sent to this address, unlinking transfer and identity.
- Recipient scans for outputs they can spend.
- Uses standard L1 transactions; no private state.

#### **What problem it solves**
- Prevents public linkage to a recipient.
- Reduces transaction-graph exposure.

#### **Key strengths**
- Minimal protocol assumptions.
- Easy integration with existing wallets/tokens.
- No private state required.

#### **Key limitations**
- Sender and amounts remain public.
- Requires scanning or delegated monitoring.
- Susceptible to metadata clustering.

#### **When to use**

- Lightweight receiver privacy on L1.
- Zero-friction integration with existing infrastructure.

#### **What it is NOT**

- Not a full shielded system.
- Not a mixer or rollup.

---

## 2. **L1 Shielded Pools**

#### **One-sentence definition**

A pattern where transfers occur inside a shared shielded pool using commitments and nullifiers so that senders, receivers, and amounts are hidden.

#### **Mechanism summary**

- Users deposit assets as commitments.
- Transfers create new commitments and nullify old ones.
- Anonymity increases with pool size.
- Only proofs/nullifiers are revealed on-chain.

#### **What problem it solves**

- Full transactional graph privacy.
- Privacy for senders, receivers, and amounts.

#### **Key strengths**

- Strongest L1-native privacy.
- Anonymity set grows as pool grows.
- Multi-asset capable.

#### **Key limitations**

- Heavy proof costs.
- Users must manage notes/keys.
- High on-chain overhead.

#### **When to use**

- When full privacy is required at L1.
- When apps can manage private note state.

#### **What it is NOT**

- Not an overlay.
- Not a scalability solution.

---

## 3. **Burn-and-Mint Privacy**

#### **One-sentence definition**

A pattern where users burn tokens in one context and mint equivalent tokens elsewhere so no on-chain link exists between the burn and mint.

#### **Mechanism summary**

- Tokens are burned to sever provenance.
- zk-proof validates eligibility to mint without linking events.
- Tokens reappear at a fresh address.
- Maintains supply consistency.

#### **What problem it solves**

- Breaks transfer linkage.
- Enables strongly unlinkable transfers.

#### **Key strengths**

- Clean unlinkability.
- Simple conceptual model.
- Stateless.

#### **Key limitations**

- Requires strong anti–double-mint guarantees.
- Statelessness limits expressiveness.
- Not suitable for multi-step workflows.

#### **When to use**

- Unlinkable transfers without maintaining private history.
- Simple fungible token models.

#### **What it is NOT**

- Not a shielded pool.
- Not an L2 pattern.

---

## 4. **Permissioned Privacy**

#### **One-sentence definition**

A pattern where transfers occur in an access-controlled environment with identity or credential gating and selective disclosure.

#### **Clarifying notes (added)**

_In this taxonomy, “Permissioned Privacy” refers to systems where the primary design axis is controlled membership and compliance-friendly selective disclosure. Mechanistically, similar permissioning and disclosure layers can also be added on top of other mechanisms (e.g., Shielded Pools or private L2s); we name it as a pattern here for communicative clarity._

#### **Mechanism summary**

- Access restricted to verified members.
- Privacy via commitments or attestations.
- Selective disclosure supports audits/compliance.
- Policy logic enforced at the protocol level.

#### **What problem it solves**

- Compliant private transfers.
- Confidentiality with structured auditability.

#### **Key strengths**

- Built-in selective disclosure.
- Strong governance and visibility control.
- Compatible with regulated deployments.

#### **Key limitations**

- Limited anonymity set.
- Depends on identity frameworks.
- Not suited to open participation.

#### **When to use**

- Regulated environments.
- Systems requiring controlled access.

#### **What it is NOT**

- Not an open anonymity system.
- Not a shielded pool.

---

## 5. **Private Rollups (Full DA)**

#### **One-sentence definition**

A pattern where private execution occurs inside a rollup with full data availability on L1.

#### **Mechanism summary**

- Private state transitions proven by zk-proofs.
- Full DA ensures reconstructability.
- Operators batch private transactions.
- L1 consensus ensures state recoverability.

#### **What problem it solves**

- High-throughput private execution with strong L1 guarantees.

#### **Key strengths**

- Full DA + privacy.
- Supports private smart contracts.
- Strong sovereignty.

#### **Key limitations**

- High L1 footprint.
- Proof generation cost.
- Users must manage private rollup state.

#### **When to use**

- When recoverability is essential.
- When strong L1 guarantees are required.

#### **What it is NOT**

- Not a Validium.
- Not an overlay.

---

## 6. **Private Plasma**

#### **One-sentence definition**

A pattern where private transfers occur inside an off-chain Plasma tree with on-chain exit guarantees but without full data availability.

#### **Mechanism summary**

- Private off-chain state maintained by operator.
- Only commitments posted to L1.
- Exits rely on user-held data.
- Transactions updated via proofs.

#### **What problem it solves**

- High-throughput private transfers with minimal L1 load.

#### **Key strengths**

- Very low L1 footprint.
- Strong privacy in Plasma tree.
- Users can exit if they retain data.

#### **Key limitations**

- Fragile exits if data lost.
- Operator withholding risk.
- Limited programmability.

#### **When to use**

- Data-light private transfers.
- Users prepared to hold their state.

#### **What it is NOT**

- Not a rollup.
- Not a Validium.

---

## 7. **Private Validium**

#### **One-sentence definition**

A pattern where private execution occurs inside a validity-proven system with off-chain data availability.

#### **Mechanism summary**

- Private state transitions proven by zk-validity proofs.
- Only commitments posted on-chain.
- DA committee ensures data availability.
- High throughput from off-chain execution.

#### **What problem it solves**

- High-throughput private execution with flexible privacy.

#### **Key strengths**

- High scalability.
- Flexible private logic possible.
- Separates DA from validity.

#### **Key limitations**

- Users cannot recover state from L1 alone.
- DA providers introduce trust.
- Sovereignty depends on off-chain data access.


#### **When to use**

- When throughput is top priority.
- Environments accepting DA trust.


#### **What it is NOT**

- Not a rollup.
- Not Plasma.


---

## Related Mechanisms Not Scored

Several mechanism families are closely related to private transfers but fall outside the seven scored patterns (**L1 Overlays, L1 Shielded Pools, Burn-and-Mint, Permissioned Privacy, Private Rollups, Private Plasma, Private Validium**). These families operate at different layers or provide general private compute.

#### **General private compute / private VMs**

Private smart-contract platforms (FHE-based EVMs, iO schemes) allow arbitrary private computation. Several patterns—**PR, VV, PL**—can be instantiated on top depending on DA model.

#### **TEE-/MPC-based private execution**

Off-chain private logic executed inside TEEs or MPC resembles **PR/VV/PL** semantics with different trust anchors.

#### **Transaction submission & ordering privacy**

Encrypted mempools and orderflow-protection hide routing and ordering, not state representation. Any pattern can sit beneath them.

#### **Identity & credential systems**

zk-credentials and selective-disclosure identity layers integrate with PP but do not define private balances.

#### **Cross-domain & channel-based privacy**

Shielded bridges and channels are Plasma-like or Validium-like transports wrapping one of the seven patterns.

---

## Membership & Visibility as a Cross-Cutting Axis

Real systems vary not only by mechanism but also by _who may join_ and _who may view what_. Membership, identity-binding, and selective disclosure frequently apply across mechanisms.

**Core clarification:**  
**Permissioned Privacy** is retained as a named pattern, but mechanistically, permissioning can be layered atop **SP, PR, PL, VV** without changing the underlying mechanism.

#### **Rules of Thumb**

- **KYC-restricted shielded pool →** SP + permissioned attribute

- **Consortium Validium →** VV + permissioned attribute

- **Open shielded pool →** SP (not PP)

- **Rollup with structured disclosure →** PR + SD attribute


---

## Classification Recipe / Cheat Sheet

#### **Step 1 — Mechanism / DA Model**

- Balances on L1 → **LO / SP / BM**

- Private state + full DA on L1 → **PR**

- Private state + proofs + off-chain DA → **VV**

- Challenge-style exits + user-held data → **PL**


#### **Step 2 — Membership / Visibility**

Mark as **open** or **permissioned**. This is an attribute, not a pattern.

#### **Step 3 — Selective Disclosure / Compliance**

Mark SD level: **none / ad-hoc / protocol-level / rich-policy**.

#### **FAQ**

**PP or VV?** → VV + permissioned attribute  
**KYC’d shielded pool?** → SP + permissioned attribute  
**Channels a new pattern?** → No, PL/VV-like transports  
**FHE-rollup?** → Classify by DA: full DA → PR, off-chain DA → VV
