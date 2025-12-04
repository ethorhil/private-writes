
**Pattern:** [[Private Plasma]]

**Type:** High-throughput private Plasma chain using client-side proving + operator-posted state roots, extended with zk-privacy (zkPlasmaFold)  
**State model:** Off-chain private balances represented in a UTXO-like model; users maintain client-side proofs of their balances enabling instant trustless exits  
**DA model:** Minimal L1 DA — only periodic state roots + tiny calldata (≈5 bytes per tx) published; bulk transaction data stays off-chain  
**Selective disclosure:** Not built-in, but future selective-disclosure extensions are being explored (e.g., provable compliance while maintaining private state)  
**Readiness:** Experimental R&D (EF PSE project); demonstrated 14k+ TPS (non-private), privacy-extension in zkPlasmaFold underway

Links:

- PlasmaFold (EF PSE): [https://hackmd.io/@PierreDM/B1jw2YcEgg](https://hackmd.io/@PierreDM/B1jw2YcEgg)
- Reference Plasma literature: ethereum.org / Plasma tutorials