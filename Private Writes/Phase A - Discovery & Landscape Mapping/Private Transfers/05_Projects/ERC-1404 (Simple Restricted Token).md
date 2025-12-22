
**Pattern:** [[Permissioned Privacy]]

**Type:** Permissioned token standard with built-in transfer-restriction checks (KYC/KYB-gated ERC-20)

**State model:** Account-based ERC-20 with restriction hooks (`detectTransferRestriction`, `messageForTransferRestriction`)

**DA model:** Full L1 DA (all token movements and compliance checks executed on Ethereum)

**Proof system:** None — ERC‑1404 is a restricted ERC‑20 token standard; transfers are restricted via smart‑contract checks and off‑chain compliance/KYC, not via zero‑knowledge proofs.

**Selective disclosure:** None — all balances and transfers public; compliance relies on whitelisting rather than privacy

**Readiness:** Fully production (used in regulated security-token deployments, e.g. INX); audited systems and large-scale investor distributions

Links:

- Docs: [https://docs.erc1404.org](https://docs.erc1404.org/)
- GitHub: [https://github.com/ethereum/EIPs](https://github.com/ethereum/EIPs)
- Audit: Implementations audited by TokenSoft/INX partners