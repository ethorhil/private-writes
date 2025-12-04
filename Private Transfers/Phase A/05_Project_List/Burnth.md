
**Pattern:** [[Burn-and-Mint Privacy]]

**Type:** EIP-7503-style private transfer tool implementing ZK Proof-of-Burn to enable unlinkable transfers  
**State model:** No persistent private state; users burn tokens to unspendable addresses and later mint them at a new address using a ZK proof that hides linkage  
**DA model:** Full L1 DA — burns and mints recorded as standard L1 events; nullifiers and hash chains stored minimally on-chain  
**Selective disclosure:** None — only full reveal of secrets can prove provenance; protocol has no partial or compliance-friendly disclosure mechanism  
**Readiness:** Early-stage / prototype (research-level tooling around EIP-7503; not audited or productionized)

Links:

- EIP-7503: [https://eips.ethereum.org/EIPS/eip-7503](https://eips.ethereum.org/EIPS/eip-7503 
- Reference implementations in community repos (Burnth variant, zERC20 lineage)