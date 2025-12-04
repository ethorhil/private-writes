

**Pattern:** [[L1 Overlay – Stealth  OTR]]

**Type:** Stealth‑address wallet with smart‑account receivers (Safe‑based)  
**State model:** Funds end up in per‑payment Safe smart accounts (one per stealth address); Fluidkey backend tracks addresses via a shared viewing key, while on‑chain state stays standard ERC‑20 / ETH account model  
**DA model:** Full L1 / L2 DA (all deposits and Safe transactions are normal chain writes; Fluidkey adds off‑chain indexing and relaying)  
**Selective disclosure:** Yes – viewing key–based; Fluidkey (or an auditor you share the key with) can see all your incoming payments while the public chain only sees unrelated addresses  
**Readiness:** Production but young (mainnet + major L2s, leveraging battle‑tested Safe contracts; closed‑source service layer, growing user base)

Links:

- GitHub: [https://github.com/fluidkey](https://github.com/fluidkey)
- Docs: [https://docs.fluidkey.com](https://docs.fluidkey.com/)
- Audit: Safe contracts audited; Fluidkey-specific infra partially unaudited / proprietary