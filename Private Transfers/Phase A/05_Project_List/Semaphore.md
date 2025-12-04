**Pattern:** [[L1 Shielded Pools]] / Primitive for anonymity sets (used by MicroMix mixers and private signaling apps)

**Type:** Anonymous signaling primitive enabling unlinkable membership proofs; can be used as a mixer backend (e.g., MicroMix)  
**State model:** Merkle tree of identity commitments; nullifier-based spend model when used for transfers  
**DA model:** Full L1 DA (identity commitments + nullifiers stored on-chain; proofs verified with zkSNARKs)  
**Selective disclosure:** None — users can only self-reveal by publishing the identity secret; no view-key or partial-disclosure mechanism  
**Readiness:** Production as a cryptographic primitive (PSE-maintained, audited, widely used in voting/identity demos); early-stage when used as a mixer (e.g. MicroMix prototypes)

Links:
- GitHub: [https://github.com/semaphore-protocol](https://github.com/semaphore-protocol)
- Docs: [https://semaphore.pse.dev](https://semaphore.pse.dev)
- Audit: EF/PSE-sponsored audits of Semaphore circuits and contracts