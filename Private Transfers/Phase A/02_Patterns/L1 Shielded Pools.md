
L1 shielded pools move privacy from the addressing layer into the **state model itself**. Users hold encrypted **UTXO/nullifier notes** inside an on-chain pool contract, and prove in zero knowledge that they are spending valid notes and creating new ones without revealing sender, receiver, or amount. The pool lives directly on Ethereum L1, so DA is guaranteed by calldata and state, and correctness is enforced by on-chain proof verification.

This design offers **strong privacy guarantees** at the cost of **heavy per‑transfer proving and verification costs** and **limited throughput**—only a modest number of zk transfers fit in each block. Programmability ranges from simple mixers to more expressive shielded DeFi (e.g., multi‑asset pools). UX is typically more complex than overlays: users must manage notes, relayers, and multiple keys. Membership can be open or permissioned, and **selective disclosure capabilities vary widely** (from no SD to advanced viewing-key or association-set–style proofs). Examples include Tornado-like mixers, Railgun-like systems, Privacy Pools, zkBob, and Panther-style designs.

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