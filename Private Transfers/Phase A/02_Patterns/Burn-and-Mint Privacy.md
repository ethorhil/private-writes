Burn-and-mint systems provide privacy by **breaking the link** between origin and destination across two contexts—often two addresses, pools, or even chains. A user **burns** tokens in one place and later **mints** new tokens elsewhere, supplying a ZK proof that the burn and mint are related and well-formed, without revealing which specific burn funds which mint.

This pattern offers **strong unlinkability** and can be relatively simple conceptually, but most deployments are **early-stage**. Current designs tend to have **non-trivial gas costs** (burn + mint + proof verification) and limited ecosystem maturity compared to shielded pools or rollups. Programmability is typically focused on transfer semantics rather than general-purpose private smart contracts. Membership can be open or permissioned, and selective disclosure is usually minimal or ad-hoc, though richer SD profiles could be layered on in future implementations.

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

[[tornado ca]]