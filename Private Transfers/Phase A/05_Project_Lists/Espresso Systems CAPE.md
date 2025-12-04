
**Pattern:** [[Permissioned Privacy]]

**Type:** Configurable‑privacy token wrapper (policy‑controlled confidential ERC‑20)  
**State model:** Account-based wrapped token with UTXO‑style shielded transfers under the hood (commitments + nullifiers, encrypted ownership)  
**DA model:** Hybrid – early pilots verify zk proofs and update state on Ethereum; longer term, transactions live on Espresso’s L1 with periodic checkpoints to Ethereum  
**Selective disclosure:** Yes – per‑asset viewing policies; issuers and designated regulators get viewing keys / policy contracts to decrypt flows or freeze funds  
**Readiness:** Prototype / enterprise pilots (testnets + PoCs with institutions; not a public retail product yet)

Links:
- GitHub: [https://github.com/EspressoSystems/cape](https://github.com/EspressoSystems/cape)
- Docs: [https://docs.cape.tech](https://docs.cape.tech/)
- Audit: Internal + external reviews as part of Espresso Systems; specific CAPE audits attached to enterprise pilots