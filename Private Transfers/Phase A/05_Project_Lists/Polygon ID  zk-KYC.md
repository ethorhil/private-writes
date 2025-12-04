
**Pattern:** [[Permissioned Privacy]]

**Type:** zkSNARK-based identity and attribute-proof system enabling private KYC-gated transfers and airdrops  
**State model:** Off-chain verifiable credentials + on-chain verification contracts; verification requires zkSNARK proof of specific attributes (age, nationality, KYC pass, etc.)  
**DA model:** Full L1 DA (proof verification and gating executed on-chain; data itself remains off-chain)  
**Selective disclosure:** Yes — users can selectively prove individual attributes without revealing identity or raw data  
**Readiness:** Production-ready (used in airdrops, KYC-gated minting, enterprise pilots; widely maintained by Polygon)

Links:

- Docs: [https://polygonid.com](https://polygonid.com)
- Universal Verifier examples: [https://medium.com/@raam/](https://medium.com/@raam/)... (as referenced in the research)
- GitHub: https://github.com/0xpolygonid