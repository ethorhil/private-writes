**Patterns supported (via deployments):** [[L1 Shielded Pools]]-style mixer deployments (e.g., MicroMix) and anonymous signaling deployments that plug this primitive into a transfer or voting pattern.

**Type:** Anonymous signaling primitive enabling unlinkable membership proofs; can be used as a mixer backend (e.g., MicroMix)

**Primitive Catalog entry:** [[8 Scope Boundaries, Related Mechanisms, and Limitations#Primitive Catalog (Identity, Anonymous Signaling, Private Compute, Ordering Privacy)|Semaphore]]


**State model:** Merkle tree of identity commitments; nullifier-based spend model when used for transfers

**DA model:** Full L1 DA (identity commitments + nullifiers stored on-chain; proofs verified with zkSNARKs)

**Proof system:** Groth16 zkSNARK — Semaphore's circuits and Solidity verifier are based on Groth16; the official contracts and docs describe an extended Groth16 verifier and BN254 curve assumptions.

**Selective disclosure:** None — users can only self-reveal by publishing the identity secret; no view-key or partial-disclosure mechanism

**Readiness:** Production as a cryptographic primitive (PSE-maintained, audited, widely used in voting/identity demos); early-stage when used as a mixer (e.g. MicroMix prototypes)

Links:
- GitHub: [https://github.com/semaphore-protocol](https://github.com/semaphore-protocol)
- Docs: [https://semaphore.pse.dev](https://semaphore.pse.dev)
- Audit: EF/PSE-sponsored audits of Semaphore circuits and contracts