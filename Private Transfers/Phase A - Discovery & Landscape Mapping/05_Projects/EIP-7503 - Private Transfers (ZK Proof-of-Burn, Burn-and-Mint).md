
**Pattern:** [[Burn-and-Mint Privacy]]

**Type:** ZK Proof-of-Burn mechanism enabling unlinkable private transfers of ETH/ERC-20

**State model:** No persistent private state; users burn on one address and mint to another via ZK proof linking them privately

**DA model:** Full L1 DA (burn + mint proofs, commitments, and nullifiers posted on L1)

**Proof system:** zkSNARK proof‑of‑burn (implementation‑agnostic; reference uses Groth16) — the EIP specifies a ZK proof‑of‑burn mechanism but is intentionally proof‑system agnostic; current reference code and write‑ups use Circom + Groth16 for the concrete circuits.

**Selective disclosure:** Minimal — no native view-key model; users may reveal secrets or generate custom proofs, but no protocol-level SD feature

**Readiness:** Early-stage; EIP remains draft/stagnant; prototype implementations (e.g., Intmax zERC20) on testnet but not production-audited

Links:

- EIP: [https://eips.ethereum.org/EIPS/eip-7503](https://eips.ethereum.org/EIPS/eip-7503)
- Prototype (Intmax zERC20): [https://github.com/Intmax/](https://github.com/Intmax/)
- Audit: None (EIP & prototypes only)