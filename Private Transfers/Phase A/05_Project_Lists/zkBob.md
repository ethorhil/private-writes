
**Pattern:** [[L1 Shielded Pools]]

**Type:** Multi-asset shielded pool enabling private transfers of stablecoins (e.g., BOB/USDC) with simplified UX  
**State model:** UTXO commitments + nullifiers; per-asset shielded pools with encrypted note data  
**DA model:** Full L1 DA (encrypted notes + nullifiers published on-chain; proofs verified on-chain)  
**Selective disclosure:** Partial — users can share note secrets or viewing data for compliance, but no full protocol-native selective-disclosure layer  
**Readiness:** Production (Polygon deployment), active users, mature circuits; optimized for low-fee environments

Links:
- GitHub: [https://github.com/zkBob](https://github.com/zkBob)
- Docs: [https://docs.zkbob.com](https://docs.zkbob.com)
- Audit: Multiple audits (Nethermind, independent ZK reviewers)