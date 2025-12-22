
## TL;DR

In this project, **private DeFi** means **provably-correct DeFi state updates**—swaps/AMMs, LP joins/exits, collateral & debt adjustments, liquidations, and “simple perps/margin” decomposable into **collateral + swap + liquidation**—where correctness is enforced via **ZK proofs or encrypted execution** while hiding some combination of **who acted, which position/order was modified, the size/terms, and cross-write linkability**, and still exposing (or proving consistency of) the **minimum global state** needed for safety and composability (e.g., reserves/invariant-relevant fields, aggregate debt/utilisation, oracle references, state commitments) over a **~1–3 year horizon**.

### Key projects / approaches in scope

* **Privacy-native L2 / private rollup hosting DeFi natively** (e.g., *Aztec-style*): private execution for swaps/lending/liquidations with public/provable global surfaces.
* **Shielded-pool “overlay / router” into public DeFi** (e.g., *Railgun*-like): shield → interact with public liquidity via adapters/relayers → unshield; privacy focused on user linkability and per-user state.
* **Shielded DEX app-chain designs** (e.g., *Penumbra-style*): default-shielded trading/LP writes as a reference architecture for “notes-as-state” DeFi.
* **Validity-proved private execution with off-chain encrypted DA** (*validium-style*): high-throughput private swaps/lending/perps with explicit DA/exit trust trade-offs.
* **Burn/lock → mint “z-assets” private domains** (e.g., *Panther-style*): DeFi occurs over wrapped private assets; entry/exit patterns become the key leakage surface.
* **Eligibility-gated / compliance-aware private DeFi**: ZK membership proofs + selective disclosure/view keys as a *guardrail* on private writes (not a new DeFi primitive).
* **TEE-based confidential EVM / confidential L2 execution** (e.g., *Secret Network*, *Obscuro/TEN*): encrypted state execution with a distinct trust model (attestation vs pure ZK).
* **Encrypted orderflow + MEV-aware delivery with public settlement** (e.g., *Shutter*, *CowSwap-style auctions*, *SUAVE/Flashbots-style relays*): reduces pre-trade leakage/sandwiching even when onchain state remains public.
* **Shared sequencing for cross-rollup atomic bundles** (e.g., *Espresso*, *Astria*): enables multi-venue bundles and a natural “hook point” for privacy-aware ordering/encrypted intents.

### Big questions we still have

* **Minimum public/provable state:** What global state must remain public (or provably consistent) for AMMs/lending to be safe/composable, and how much *inevitable* leakage does that create—especially for whales, liquidations, and thin pools?
* **Liquidations/keepers:** Can we make liquidations and keeper actions privacy-compatible **without** creating privileged actors, opaque solvency risk, or new MEV / governance power?
* **Anonymity & liquidity fragmentation:** How do we avoid anonymity-set splintering across assets/products/L2s and keep private DeFi usable/liquid, rather than “privacy as mild obfuscation”?
* **UX/proving budgets:** What latency, device, fee, and relayer constraints define “usable” private DeFi—and what patterns avoid privacy bypass via dashboards, analytics, and operational tooling?
* **Selective disclosure at scale:** How do compliance/attestation gates and view keys scale without “view-key sprawl” or silent deanonymisation through correlated disclosures?

(For working lists: see [[Project List – DeFi]], [[2 Mechanisms & Patterns in DeFi]], and [[4 Open Problems – DeFi]])

# Summary – Private DeFi

## 1. Working scope of "DeFi" in this pass

**In scope:**

* **Swaps and AMMs**
  * Opening / closing swap positions
  * Joining / exiting liquidity pools
* **Lending / borrowing**
  * Supplying collateral, drawing debt, repaying, adjusting positions
* **Basic position management**
  * Rebalancing or rolling simple positions
  * Simple leveraged / perp-style positions built from **collateral + swap + liquidation**
    (e.g., GMX-style perps, margin on top of spot), limited to *current or near-term feasible*
    constructions (no exotic payoffs or complex path-dependent funding logic in this pass)

These represent the minimal DeFi primitives that:
* interact with **financial logic** (market making, debt positions, collateral ratios);
* touch shared **onchain state** beyond balance transfers;
* appear as **distinct write patterns** from Transfers or Governance;
* are already reflected in systems like Aztec Connect, Railgun, Secret Network, Penumbra-style DEXes, and emerging zk rollups.

Perps / margin DEXes implemented as “lending + swap + liquidation” are **in scope**, but we map them to the same primitive write types (trade, collateral supply/withdrawal, debt mint/repay, liquidation) instead of creating a separate derivatives taxonomy.
More complex derivatives (orderbook perps, options, tranching) are deferred.

DeFi-adjacent systems like LSDs, yield aggregators, and restaking layers are **in scope only insofar as they reuse these primitives** (deposit/withdraw, trade, borrow/repay, liquidate). Their internal, domain-specific logic is not mapped.

**Explicitly *out of scope* for this pass (may be noted but not mapped in detail):**
* Exotic derivatives and structured products
  * Path-dependent options, bespoke structured notes, tranching, complex structured products
  * (Perps / simple margin from lending + swaps remain in scope as noted above.)
* Highly specialised DeFi protocols with bespoke financial logic
* Full DeFi ecosystem / project mapping
* Governance and identity systems
* RWA / undercollateralised credit **off-chain processes** (credit scoring, legal enforcement).
  Onchain they are treated as ordinary lending primitives with external attestations.
* MEV / orderflow auctions and blockspace markets (Flashbots, PBS, SUAVE, etc.) as **infrastructure**.
  We assume some form of encrypted / MEV-aware transaction delivery but do not treat MEV markets themselves as DeFi writes.
* Cross-domain bridges and messaging layers (lock/mint, burn/release, bridge+swap UX) — belong to **Transfers / infra**; referenced only where needed for cross-domain unlinkability or end-to-end flows.

(See [[DeFi – What I Took From Transfers]] for how this scope was constructed.)

## 2. What *counts* as "DeFi" here vs other domains

**Heuristics for "this is DeFi, not Transfers":**
* The write changes **a position in a financial protocol**, not just a balance
* The protocol applies **pricing / risk / payoff rules**, not just “move value from A to B”
* There is some notion of **pool, market, or position** (LP shares, debt positions, perp positions, etc.)
* The write may be initiated by a user **or a system actor** (liquidator, keeper, auction bidder, protocol automaton), but it always mutates shared protocol state

**Heuristics for "this belongs in Transfers":**
* The primary effect is moving value between accounts
* No persistent position / pool / market is updated
* The protocol applies no financial transformation beyond “who owns what”

**Heuristics for "this belongs in Governance":**
* The write is a vote, delegation, or governance action
* The primary privacy target is **preference / choice**, not financial exposure
These heuristics will be kept aligned with the Transfers and Governance tracks.

## 3. Boundary examples

* **Private DEX trade on a shielded rollup**
  → **In scope** (swap execution)

* **Private salary payment using a shielded pool**
  → **Out of scope** (Transfers)

* **Private on-chain vote to change interest rate model**
  → **Out of scope** (Governance)

* **Private liquidation of an undercollateralised position**
  → **In scope** (liquidation / keeper write; aggregate liquidation flows may remain visible)

* **Private distribution of protocol revenue to token holders**
  → **In scope, lower priority** (claim / reward write)

* **Private deposit into a yield aggregator (e.g., Yearn)**
  → **In scope** (user-facing “strategy share” position; downstream strategy actions not mapped)

* **Private staking of ETH into Lido for stETH**
  → **In scope, edge case (LSD)** (deposit → receive derivative token; validator / restaking mechanics not mapped)

* **Private bridging from Ethereum to Arbitrum**
  → **Out of scope** (Transfers / cross-domain infra; may matter for unlinkability but not a DeFi write)

* **Opening a large perp position on a GMX-style DEX**
  → **In scope** (collateral deposit + leveraged trade + liquidation path decomposed into primitives)

* **Private off-chain RFQ settling on-chain via aggregator**
  → **In scope** (on-chain settlement is a swap; off-chain negotiation is out of scope)

* **Private oracle price update for a lending protocol**
  → **Out of scope as a DeFi write** (oracle infrastructure), though oracle data inside private DeFi proofs **is in scope** for threat/trust modeling.

### 3.1 High-priority DeFi writes that benefit from privacy

* **Large portfolio rebalance / whale swap across multiple pools**
  *Trade execution + liquidity shifts; privacy avoids MEV attacks and signalling strategic intent.*

* **Liquidation / auction of a large collateralised position**
  *Liquidation action; privacy avoids bid sniping, collusion, and targeted liquidations.*

* **Large leveraged perp position lifecycle**
  *Opening / adjusting / closing; privacy protects liquidation thresholds and leverage.*

* **Cross-protocol debt refinancing**
  *Borrow/repay / collateral shifts across protocols; privacy prevents front-running and targeted monitoring.*

* **Vault / aggregator rotation of large TVL**
  *Withdraw + swaps + deposits; privacy avoids slippage and MEV tax.*

* **Institutional DeFi under compliance constraints**
  *Same primitives plus eligibility proofs; privacy protects competitive strategy while enabling gated access.*

## 4. First working definition of "private DeFi write"

> A **private DeFi write** is a cryptographically validated transaction or state update inside a DeFi protocol (AMM, lending market, perp/margin system, simple yield/staking system, etc.)—such as a swap, liquidity change, borrowing/repayment, liquidation, or similar position update—validated via a zero-knowledge proof or encrypted execution rather than by revealing raw transaction details.
>
> From an external observer’s perspective, some combination of:
>
> * **who** is acting,
> * **which position/order** they modify,
> * **the size or terms** of the update, and
> * **how this write links to their other actions**
>   is intentionally hidden or hard to link, while the system still:
> * enforces correct pricing and risk rules, and
> * exposes sufficient aggregate / global state (pool reserves, aggregate debt, oracle prices) for auditability, safety, and composability.

This includes both **user-initiated writes** and necessary **system / keeper writes** (liquidations, auctions, protocol-controlled adjustments). It **excludes**:

* simple balance transfers (Transfers domain)
* governance votes / delegations (Governance domain)

For clarity, we reuse three privacy notions:

* **Per-write privacy:** each write hides per-user details except what is strictly required.
* **Cross-write unlinkability:** multiple writes by the same user or on the same exposure are not trivially linkable.
* **Cross-domain unlinkability:** bridging across domains does not trivially deanonymise private DeFi activity.

This definition aligns with the broader Private Writes program and is grounded in mechanisms feasible with current and near-term ZK / private-execution tooling.

## 5. Open scoping questions

* **Adjacent categories:**
  *Perps / margin* are included only when decomposable into primitives (collateral + swap + liquidation).
  *LSDs / restaking / aggregators* are included only via user-facing primitives.
  *RWAs / undercollateralised credit* are treated as lending primitives gated by external attestations.

* **MEV / orderflow (infra vs DeFi):**
  MEV markets remain infrastructure. The DeFi scope models searchers and block builders in the threat model and assumes access to some MEV-aware delivery mechanism (encrypted mempool, batch auctions, commit-reveal).

* **Identity / attestations / compliance:**
  Identity and attestations systems supply eligibility proofs. These serve as guards on private writes rather than introducing new DeFi primitives.

* **Composed protocols (aggregators, restaking):**
  Treated as **meta-strategies** over primitive writes. Only user-facing entry/exit/claim writes are modeled.

* **System / keeper vs user writes:**
  Private liquidation and keeper logic follow the same privacy goals as user actions, acknowledging that some aggregate liquidation data may remain public.

* **Minimum required public state:**
  Protocols must maintain or periodically prove:

  * AMM reserves / invariant-relevant state
  * Aggregate collateral, debt, and utilisation metrics
  * Oracle prices or equivalent references
  * State commitments for data availability / exit
    These form the necessary public or provable surfaces; privacy focuses on concealing **per-user** state and linkages.
