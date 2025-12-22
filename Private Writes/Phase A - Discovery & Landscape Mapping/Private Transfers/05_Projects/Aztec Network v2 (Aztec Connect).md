
**Pattern:** [[Private Rollups (Full DA)]]

**Type:** Shielded zk‑rollup for private payments + DeFi bridges

**State model:** Encrypted UTXO note set with nullifiers (private balances), plus minimal public bridge state

**DA model:** Full DA zk‑rollup on Ethereum – encrypted notes and nullifiers posted as calldata to L1

**Proof system:** PLONK‑family zkSNARK — Aztec 2.0 / Aztec Connect uses Aztec's in‑house PLONK proving system, with TurboPlonk used on the prover side and standard PLONK as the aggregated verifier.

**Selective disclosure:** Yes, via optional viewing keys (users can reveal their note history to third parties; essentially all‑or‑nothing)

**Readiness:** Battle‑tested (mainnet 2021–2024, now sunset to focus on v3)

Links:

- GitHub: [https://github.com/AztecProtocol/aztec-connect](https://github.com/AztecProtocol/aztec-connect)
- Docs: [https://guide.aztec.network/aztec-connect](https://guide.aztec.network/aztec-connect)
- Audit: Multiple audits (ABDK, ConsenSys Diligence, Code4rena contest; trusted setup ceremonies “Ignition” & “Powers of Tau”)
