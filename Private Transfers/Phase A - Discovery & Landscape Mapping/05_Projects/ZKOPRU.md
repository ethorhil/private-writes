
**Pattern:** [[Private Rollups (Full DA)]]

**Type:** ZK‑Optimistic rollup for private multi‑asset payments and swaps (research prototype).

**State model:** UTXO‑based shielded notes with commitments and nullifiers; supports ETH, ERC‑20s, and NFTs.

**DA model:** Full L1 DA – encrypted tx data included in Ethereum calldata for each batch (true rollup).

**Proof system:** Groth16 zkSNARK — security audits and specs for ZKOPRU state that it uses the Groth16 zk‑SNARK to provide range proofs and hide balances in its privacy‑preserving optimistic rollup.

**Selective disclosure:** None built‑in – strong default privacy; no view‑key or auditor‑key system, only voluntary off‑chain reveal.

**Readiness:** Alpha‑stage research implementation; Görli testnet + experimental mainnet attempt, now inactive.

Links:
- GitHub: https://github.com/zkopru-network/zkopru
- Docs: [https://docs.zkopru.network](https://docs.zkopru.network)
- Audit: No ZKOPRU‑specific public audits referenced in the collected research (prototype, not productized).