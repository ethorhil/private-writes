
**Pattern:** [[Private Rollups (Full DA)]]

**Type:** General‑purpose encrypted L2 (“Ethereum, but encrypted”)  
**State model:** Dual model – public account state plus private UTXO-style notes inside Noir smart contracts (both public and private variables)  
**DA model:** zk‑rollup on Ethereum (encrypted tx data posted to L1 using calldata/blobs; exploring optional higher‑throughput modes later)  
**Selective disclosure:** Planned granular view keys and purpose‑bound proofs (per‑contract viewing and derived compliance proofs)  
**Readiness:** Active public testnet (“Aztec Sandbox”) for Noir contracts; mainnet targeted after audits and decentralization milestones

Links:

- GitHub: [https://github.com/AztecProtocol/aztec3](https://github.com/AztecProtocol/aztec3)
- Docs: [https://docs.aztec.network](https://docs.aztec.network/)
- Audit: In progress (new prover, Noir compiler, and protocol scheduled for multi‑stage external audits pre‑mainnet)