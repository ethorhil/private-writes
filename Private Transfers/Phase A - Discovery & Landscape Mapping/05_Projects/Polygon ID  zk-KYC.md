
**Patterns supported (via deployments):** [[Permissioned Privacy]] deployments that use Polygon ID as a zk-KYC / attribute-proof backend.

**Type:** zkSNARK-based identity and attribute-proof primitive used as a backend for private KYC-gated transfers and airdrops.

**Primitive Catalog entry:** [[8 Scope Boundaries, Related Mechanisms, and Limitations#Primitive Catalog (Identity, Anonymous Signaling, Private Compute, Ordering Privacy)|Polygon-ID]]

**State model:** Off-chain verifiable credentials + on-chain verification contracts; verification requires zkSNARK proof of specific attributes (age, nationality, KYC pass, etc.)

**DA model:** Full L1 DA (proof verification and gating executed on-chain; data itself remains off-chain)

**Proof system:** Groth16 zkSNARK — Polygon ID / iden3 circuits (auth, credential queries, etc.) are written in Circom and use Groth16; the JS SDK explicitly exposes Groth16 provers, and ecosystem analyses describe the identity stack as Groth16‑based (with future plans to move towards STARK‑based proofs).

**Selective disclosure:** Yes — users can selectively prove individual attributes without revealing identity or raw data

**Readiness:** Production-ready (used in airdrops, KYC-gated minting, enterprise pilots; widely maintained by Polygon)

Links:

- Docs: [https://polygonid.com](https://polygonid.com)
- Universal Verifier examples: [https://medium.com/@raam/](https://medium.com/@raam/)... (as referenced in the research)
- GitHub: https://github.com/0xpolygonid