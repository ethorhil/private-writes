
Most private Validium systems use **validity proofs for execution correctness** (optimiums are not common), like rollups, but keep **transaction data off-chain** under the control of a DA committee, operator set, or similar infrastructure. This enables **very high throughput and low L1 costs** while still providing strong integrity guarantees for the executed logic.

Because data is not fully available on-chain, users must trust the DA providers not to withhold or censor data; if they do, users generally cannot reconstruct the full state or independently exit. Validium designs often support **rich private programmability**—for example, app-specific private exchanges or more general private VMs—and can be deployed in both open and permissioned modes. Selective disclosure capabilities vary, but many real-world deployments lean toward **better SD and compliance tooling** than purely open systems, especially in institutional or RWA-focused contexts. Representative systems include StarkEx-style deployments and early “Prividium”-style private Validium chains.

**One-sentence definition**

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