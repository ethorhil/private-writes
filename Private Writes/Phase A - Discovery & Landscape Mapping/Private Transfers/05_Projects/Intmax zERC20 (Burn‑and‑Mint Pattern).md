
**Pattern:** [[Burn-and-Mint Privacy]]

**Type:** Cross‑chain private ERC‑20 using burn‑and‑mint with zk proof‑of‑burn

**State model:** Account-based token wrappers plus a global Merkle tree of burns and nullifiers; withdrawals (mints) prove inclusion + non‑reuse of a burned note

**DA model:** Hybrid – each burn and proof‑based mint is an on‑chain tx (Ethereum or L2); global tree can span multiple chains via a coordination contract

**Proof system:** Recursive zkSNARK stack (exact backend not publicly specified) — Intmax describes a stateless zk‑rollup architecture with per‑transaction ZK proofs and recursive aggregation; public materials emphasize recursive ZK proofs but do not clearly name a specific Groth16/PLONK/STARK backend.

**Selective disclosure:** None built‑in (link between burn and mint is hidden; users can only de‑anonymize manually by revealing secrets or custom proofs)

**Readiness:** Experimental (EIP‑7503 draft for L1 ETH; Intmax zERC20 live on testnets like Arbitrum/Optimism, not yet widely deployed on mainnet)

Links:

- GitHub: – (zERC20 reference impls are published under Intmax repos)
- Docs: See EIP‑7503 + zERC20 design docs / Medium posts
- Audit: Prototype stage; cryptographic and contract audits still emerging