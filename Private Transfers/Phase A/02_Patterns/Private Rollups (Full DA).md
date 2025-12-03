
Private rollups (full DA) shift private transfers into a **separate state machine** that executes off‑chain but posts both **transaction data and validity proofs** to Ethereum. This means users enjoy **strong privacy at the transaction level** while inheriting **L1-grade data availability and verifiability**: anyone can reconstruct the rollup state from on-chain data, and zk proofs ensure correctness.

By batching transactions and proofs, private rollups can achieve **higher throughput and lower amortized L1 cost per transfer** than L1-native shielded pools, while also supporting **more expressive private logic** (e.g., private DeFi or application-specific private contracts). Trade-offs include **increased complexity**, reliance on specialized prover infrastructure, and **UX friction** around notes, keys, and bridging flows. Membership can be open or permissioned, and selective disclosure ranges from none to protocol-level SD, depending on the specific design. Representative systems in this family include Aztec-like, Nightfall-like, and other zk rollup–based private transfer solutions.

**One-sentence definition**

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