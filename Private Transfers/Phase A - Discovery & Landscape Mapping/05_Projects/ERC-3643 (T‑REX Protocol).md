

**Pattern:** [[Permissioned Privacy]]

**Type:** Permissioned ERC‑20 / RWA token standard

**State model:** Account-based ERC‑20 with embedded on‑chain compliance checks (ONCHAINID registry + compliance module)

**DA model:** Full L1 DA (all balances and transfers recorded on Ethereum / EVM L1)

**Proof system:** None — ERC‑3643 / T‑REX is a permissioned security‑token standard that relies on identity registries and transfer restrictions, not on ZK proofs.

**Selective disclosure:** None (all balances and transfers are public; privacy only via pseudonymous addresses)

**Readiness:** Production (finalized ERC standard, widely used in institutional RWA tokenization)

Links:

- GitHub: [https://github.com/ERC-3643](https://github.com/ERC-3643)
- Docs: [https://docs.erc3643.org](https://docs.erc3643.org/)
- Audit: Hacken (ERC‑3643 contracts)
