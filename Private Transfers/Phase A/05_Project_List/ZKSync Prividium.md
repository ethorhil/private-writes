
**Pattern:** [[Private Validium]]

**Type:** Permissioned private zk-rollup for institutional flows with role-gated transaction execution  
**State model:** Account-based private L2 with encrypted transaction data; batch proofs update a public L1 state root  
**DA model:** Off-chain DA (operator maintains private state; only proofs + roots posted to Ethereum)  
**Selective disclosure:** Yes — fine-grained, role-controlled access; auditors and authorized parties can query private logs without exposing global ledger  
**Readiness:** Production-grade institutional deployments (live private chains, identity-integrated, full compliance stack, frequent L1 proofs)

Links:

- Docs: [https://docs.zksync.io/zk-stack/prividium/overview](https://docs.zksync.io/zk-stack/prividium/overview)
- GitHub: [https://github.com/matter-labs](https://github.com/matter-labs)
- Audit: Private audits integrated into institutional deployments