
**Pattern:** [[L1 Overlay – Stealth  OTR]]

**Type:** Stealth‑address payment overlay (receiver‑privacy for ETH/ERC‑20)  
**State model:** Standard L1 account model; Umbra contract emits “announcement” events and holds token deposits, while recipients control one‑time stealth addresses derived via ECDH  
**DA model:** Full L1 DA (all sends and withdrawals are normal Ethereum/L2 transactions; Umbra adds minimal event data and storage)  
**Selective disclosure:** Yes – recipients can share viewing keys or private keys to reveal which stealth addresses they control (for audits/tax)  
**Readiness:** Production (mainnet since 2020, active on multiple L2s; open‑source and battle‑tested in niche usage)

Links:
- GitHub: –
- Docs: –
- Audit: –