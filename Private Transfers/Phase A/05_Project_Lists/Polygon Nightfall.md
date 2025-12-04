

**Pattern:** [[Private Rollups (Full DA)]]

**Type:** Hybrid Optimistic + ZK-based private transfer system (Optimistic rollup settlement + zkSNARK privacy for transfers)  
**State model:** Account-based rollup with private UTXO-style note commitments for confidential transfers  
**DA model:** Full L1 DA (rollup publishes data + proof roots to Ethereum for permissionless verification)  
**Selective disclosure:** Yes — supports compliance-oriented selective disclosure via zk proofs (e.g., proving constraints without revealing amounts or counterparties)  
**Readiness:** Production-ready (enterprise-focused; maintained by EY/Polygon with stable deployments and business integrations)

Links:

- GitHub: [https://github.com/EYBlockchain/nightfall](https://github.com/EYBlockchain/nightfall)
- Docs: [https://nightfall-docs.polygon.technology](https://nightfall-docs.polygon.technology/ 
- Audit: EY/Polygon audits across rollup and ZK components