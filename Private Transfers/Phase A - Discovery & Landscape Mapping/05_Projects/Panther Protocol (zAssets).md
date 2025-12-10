**Pattern:** [[L1 Shielded Pools]], [[Permissioned Privacy]]

**Type:** Shielded zAsset system with compliance‑aware DeFi features

**State model:** UTXO‑style shielded zAsset pools (commitments + nullifiers) managed by contracts; additional contract state for limits, allowlists, and compliance flags

**DA model:** Full L1 (or L2) DA where deployed – encrypted notes and Merkle tree updates live on‑chain; heavy computation (zk proof generation) done off‑chain

**Proof system:** Groth16 zkSNARK — Panther's privacy system for zAssets uses zk‑SNARKs with the Groth16 proof system to provide confidential transfers and selective disclosure.

**Selective disclosure:** Yes – viewing key model for regulators/auditors; users can opt to reveal zAsset transaction details while keeping them hidden from the public mempool/chain observers

**Readiness:** R&D / pilot networks (testnets + early institutional pilots; significant zk + compliance complexity, still pre‑mass‑production)

Links:

- GitHub: [https://github.com/pantherprotocol](https://github.com/pantherprotocol)
- Docs: [https://docs.pantherprotocol.io](https://docs.pantherprotocol.io/)
- Audit: Multiple audits (incl. Veridise) focusing on shielded transfers + compliance limit enforcement
    