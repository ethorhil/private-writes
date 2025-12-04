
**Pattern:** [[Private Validium]]

**Type:** ZK-powered Validium system for private (and semi-private) asset transfers and application-specific logic  
**State model:** Off-chain private state + on-chain validity proofs; accounts and balances maintained in operator-managed data structures with ZK constraints  
**DA model:** Off-chain DA (operator/committee provides availability; Ethereum verifies proofs only)  
**Selective disclosure:** Limited — no built-in user-controlled selective-disclosure model; visibility determined by application logic and operator policies  
**Readiness:** Production-grade (multi-year deployments across major apps; mature prover stack)

Links:

- GitHub: [https://github.com/starkware-libs](https://github.com/starkware-libs)
- Docs: [https://docs.starkware.co](https://docs.starkware.co/)
- Audit: Multiple audits across StarkEx integrations (e.g., dYdX, Immutable)