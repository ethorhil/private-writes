This note is the DeFi-only, short-form “pain points” list; it should stay summary-level and point to the canonical P01–P19 mapping in [[5 Problem Matrix Transfers & DeFi]] , and any genuinely unmapped DeFi issues should be logged as candidates in [[Additional Problems — DeFi]] rather than expanded here.

### Protocol / mechanism pain

- **Anonymity sets splinter across DeFi “silos”:** Usage naturally shards by asset, product, and sophistication; whales/institutions can stratify even inside a given pool, making high-value flows easier to fingerprint. This means privacy is often weakest exactly for the users and markets where positions are large, repeated, or time-sensitive (e.g., rolling debt, rebalancing LP, managing leverage).

- **“Necessary” global state still leaks coarse activity:** AMM reserve vectors, aggregate borrowed/available, utilisation, and related public/provable surfaces move in noticeable jumps on large trades/liquidations, leaking “someone just moved N% of the pool” even if actor/terms are hidden. In thin or highly correlated markets, these jumps can be enough to infer trade direction, approximate size, and sometimes even the likely intent (e.g., deleveraging vs. rotation).

- **Liquidations/auctions + keepers are hard to make privacy-compatible:** Naive designs either hide undercollateralisation until it’s too late, or concentrate visibility in privileged keepers—creating privileged MEV and governance power (and reintroducing targeted liquidations). The open problem is to prove liquidation eligibility and execute quickly under adversarial conditions without handing any single actor an information monopoly or the ability to censor competitors.

- **Verifiability vs opaque logic (“who watches the watcher”):** Complex AMM/lending/vault logic enforced by proofs or TEEs is **harder to audit via public re-execution**, shifting assurance onto circuits/attestations/audits; buggy or malicious logic may go unnoticed until insolvency. Put differently, the trust burden moves from “everyone can re-run it” to “we believe the circuit/enclave is correct,” which raises the bar for formal verification, monitoring, and escape-hatch design.

  

### UX / product pain


- **Long-lived unlinkability is brittle in real workflows:** Privacy across *multiple actions* is hard to maintain; deposit/withdraw patterns can still be deanonymized if users aren’t careful, and manual shield → relayer → unshield flows don’t scale for typical users. Real users also do repetitive position management (top-ups, partial closes, claims, rebalances), so small timing/amount correlations can accumulate and re-link a “private” history over weeks.

- **Client/prover UX is a binding constraint:** Users must generate proofs reliably; mobile and low-power devices are stress points; “proving/latency budgets” determine whether private DeFi writes feel usable or remain theoretical. Techniques like delegated proving, batching, and hardware acceleration help, but they introduce new trust, fee, and failure-mode trade-offs that have to be handled explicitly in the UX.

- **Dashboards / PnL / analytics pressure creates privacy bypasses:** The easiest way to build “rich UX” can become “just log to an analytics backend,” creating systematic leakage that defeats protocol-level privacy. Without privacy-preserving analytics (local computation, view-key–scoped queries, or ZK’d aggregates), teams can accidentally recreate a centralized correlation layer that links users and positions.

  

### Infra / ecosystem pain


- **Orderflow/MEV is in the threat model by default:** Large swaps/perps are actively exploited via MEV and surveillance; even strong protocol privacy can be undone if orderflow leaks in the mempool—yet many approaches are “crowded on research, thin on production.” End-to-end integration matters: if the transaction leaks at RPC, relayer, sequencer, or builder layers, the attacker doesn’t need on-chain visibility to front-run or target.

- **Cross-domain unlinkability breaks at boundaries:** Bridges/L2 transitions (and DeFi-adjacent wrapped assets like stETH/LP tokens) create recognizable amount/timing patterns; observers can stitch “round trips,” turning private DeFi into “mild obfuscation” if boundaries aren’t handled well. The hardest moments are often entry/exit points (bridge, wrap, claim) where users must touch public state, so systems may need buffering hubs, standardized denominations, or delayed exits to hide edges.

- **Data availability + exits become acute under market stress:** Private rollup/validium designs often rely on off-chain encrypted user state; during stress—when positions are at risk—operators/DA committees can be incentivized to fail or censor, with DeFi-specific time pressure (“couldn’t exit before liquidation / rollup halted”). Robust escape hatches (forced exits, guaranteed DA, or credible censorship-resistance) are therefore core risk controls, not “nice-to-have” decentralization features.

- **Regulation + selective disclosure complexity:** Overlay-style systems can look mixer-like; “business DeFi” wants partial transparency (LPs/auditors/regulators) without full exposure, but view keys/attestations can create view-key sprawl and “silent deanonymisation” when many disclosures are correlated. A workable model likely needs narrowly scoped, auditable disclosure (who can see what, for how long, and under what consent) so compliance doesn’t become a permanent, accidental surveillance channel.

- **Tooling and audit scarcity:** New languages/proof tooling and a larger audit surface make private DeFi harder to review; practitioners flagged that bugs are harder to detect and potentially catastrophic, and that developer/auditor scarcity is a practical blocker. Until there are more standard libraries, reproducible build pipelines, and auditors who can reason about both financial logic and ZK/TEE assumptions, security cycles will remain slow and expensive.

  

See [[Phase A – Private Transfers Index]] for transfer patterns and the 19 problems. *(Link name may need adjustment to match the vault’s canonical note title.)*