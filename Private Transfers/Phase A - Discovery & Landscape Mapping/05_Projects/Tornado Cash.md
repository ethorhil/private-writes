
**Pattern:** [[L1 Shielded Pools]]

**Type:** Non‑custodial UTXO mixer

**State model:** UTXO-style commitments + Merkle tree + nullifiers

**DA model:** Full L1 DA (all commitments + nullifiers on Ethereum)

**Proof system:** Groth16 zkSNARK — Tornado Cash circuits are written in Circom and compiled with snarkjs using Groth16; official docs and audits repeatedly refer to Groth16 and the associated trusted setup ceremonies.

**Selective disclosure:** none (no protocol-level view keys; only external / voluntary proofs)

**Readiness:** Battle-tested (historical; mainnet 2019–2022, contracts still live, UI deprecated)

Links:
- GitHub: https://github.com/tornadocash
- Docs: https://docs.tornado.cash
- Audit: ABDK & other audits (see `/audits` references in the GitHub repo / docs)
