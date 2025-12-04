

**Pattern:** [[L1 Shielded Pools]]

**Type:** Selective-disclosure shielded pool (Tornado-style UTXO mixer with association-set proofs)  
**State model:** UTXO note commitments + Merkle tree + nullifiers; deposit and withdrawal proofs built over deposit-set and subset-set Merkle roots  
**DA model:** Full L1 DA (all encrypted commitments, nullifiers, and subset proofs posted to Ethereum L1)  
**Selective disclosure:** Yes — core feature. Withdrawals can include _association-set proofs_ (proof-of-innocence): user proves their funds originate from a “good subset” or exclude a “bad subset” without revealing which deposit is theirs  
**Readiness:** Live

**Links:**

- GitHub: [https://github.com/ameensol/privacy-pools](https://github.com/ameensol/privacy-pools)
- Docs/Spec: [https://github.com/ameensol/privacy-pools/tree/main/spec](https://github.com/ameensol/privacy-pools/tree/main/spec)

