

**Pattern:** [[Private Rollups (Full DA)]]

**Type:** Hybrid Optimistic + ZK-based private transfer system (Optimistic rollup settlement + zkSNARK privacy for transfers)

**State model:** Account-based rollup with private UTXO-style note commitments for confidential transfers

**DA model:** Full L1 DA (rollup publishes data + proof roots to Ethereum for permissionless verification)

**Proof system:** Groth16 zkSNARK — Nightfall's privacy mechanism is explicitly described as "a zksnark using the Groth16 protocol" in the official documentation for Nightfall 3.

**Selective disclosure:** Yes — supports compliance-oriented selective disclosure via zk proofs (e.g., proving constraints without revealing amounts or counterparties)

**Readiness:** Production-ready (enterprise-focused; maintained by EY/Polygon with stable deployments and business integrations)
**Rollup / full‑DA configuration :** classified as [[Private Rollups (Full DA)]], with transaction data and proof roots posted to Ethereum for full L1 data availability.  
**Validium / volition-style configuration:** classified separately as [[Private Validium]] in the ecosystem map, where some activity uses off-chain data availability anchored by zk validity proofs.

Links:

- GitHub: [https://github.com/EYBlockchain/nightfall](https://github.com/EYBlockchain/nightfall)
- Docs: [https://nightfall-docs.polygon.technology](https://nightfall-docs.polygon.technology/ 
- Audit: EY/Polygon audits across rollup and ZK components