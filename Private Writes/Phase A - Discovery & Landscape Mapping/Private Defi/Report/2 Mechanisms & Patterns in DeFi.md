
## TL;DR

Private DeFi is rarely “a new DeFi primitive.” It is almost always **existing DeFi primitives implemented over a different private-write substrate**.

This note maps the **seven Transfers mechanism families** to DeFi as **execution + data-availability environments**, and then extracts **DeFi-specific pattern extensions** that show up across substrates.

The key takeaway is that DeFi amplifies three constraints that are less acute in simple transfers:

1. **Minimum public/provable global state**: pricing and risk logic usually requires some shared state (reserves, utilisation, oracle references). Even with perfect per-user privacy, these surfaces can leak coarse activity.
2. **Time-sensitive liveness**: liquidations and deleveraging put hard deadlines on throughput, sequencing, exits, and DA availability.
3. **Lifecycle unlinkability**: DeFi workflows are multi-write (collateral → borrow → swap → repay/adjust), making “graph motifs” and relayer/sequencer routing a dominant leak channel.

If you only read one section, read **§3 DeFi-specific pattern extensions** — it describes the patterns that DeFi adds on top of Transfers.

(For scope/definitions: [[1 Definitions, Scope & Boundaries]]. For problem statements: [[4 Open Problems – DeFi]] and [[5 Problem Matrix Transfers & DeFi]]. For a checklist-style list: [[2 Mechanisms & Patterns in DeFi]].)

---

## 1) DeFi writes we care about (the “unit tests”)

We treat these as the minimal “worst-case” writes that stress private-write systems:

- **Swap / trade** (AMM-style)
- **LP join / LP exit** (mint/burn shares)
- **Supply collateral / withdraw collateral**
- **Borrow / repay** (mint/burn debt)
- **Position updates** (roll, rebalance, migrate, refinance)
- **Liquidation / auction / keeper actions** (system-initiated writes)
- **Vault / aggregator entry/exit** (shares as a position)

A useful decomposition is:

- **User-private state**: balances/notes, positions, debt, collateral, parameters, identity/eligibility proofs.
- **Protocol-global state** (often needs to be public or provably consistent): AMM reserves/invariant fields, aggregate debt/utilisation, oracle references, risk params, state roots.

DeFi privacy work is usually about **hiding per-user state and linkability** while still enforcing protocol correctness relative to a **minimum global surface**.

---

## 2) How the seven Transfers mechanism families apply to DeFi

Below, each family is described as an execution/DA environment for DeFi. “Privacy level” is qualitative and relative.

### 2.1 L1 Overlay – Stealth / OTR (wallet-layer privacy)

**What it is (as a substrate):**
- DeFi contracts remain public/unchanged.
- Privacy is achieved by wallet patterns: stealth/meta-addresses, one-address-per-position, relayers/paymasters, encrypted orderflow delivery.

**What it can hide well:**
- **Actor identity / address linkability** (“who”).
- Some **lifecycle linkability** if address rotation + relayers are done correctly.

**What it does *not* hide (by itself):**
- **Which protocol/pool/market** was touched.
- **Amounts and price impact** (unless combined with other mechanisms).
- Any public protocol state changes (AMM reserve movements, utilisation changes).

**DeFi fit:**
- Good as a *baseline* privacy layer for users who want to avoid being a known whale/treasury address.
- Useful for “private DeFi UX” in the sense of *unlinkability* rather than hiding trade economics.

**Key failure modes:**
- Relayer choice / paymaster funding becomes a fingerprint.
- Multi-step workflows still create a graph motif even if addresses rotate.

---

### 2.2 L1 Shielded Pools (notes/commitments as the state model)

**What it is (as a substrate):**
- Users hold value as **notes/commitments** in a shielded pool; updates are authorized by ZK proofs.

There are two distinct DeFi deployments over shielded pools:

#### A) “Notes-as-state” DeFi inside the shielded domain

**Pattern:** AMM/lending/positions are represented as notes and mutated privately.

- A swap becomes: consume input notes + a private state transition that updates pool state commitments + produce output notes.
- Lending becomes: consume collateral notes, create/update a debt-position note, etc.

**Privacy:**
- Strong per-user privacy (positions and linkability can be hidden).

**Hard part (DeFi-specific):**
- Some global surfaces may still need to be **public or provably consistent** (e.g., invariant-relevant state, oracle references).
- Quoting prices / expressing intent without leaking becomes tricky.

#### B) “Privacy overlay / router” into public DeFi

**Pattern:** shield → interact with public protocol via adapters/relayers → unshield.

**Privacy:**
- Primarily hides **who** is trading / providing liquidity.
- Does *not* hide the fact that a specific pool moved or that utilisation changed.

**Hard part:**
- End-to-end unlinkability at boundaries (shield/unshield patterns).
- Adapters/relayers become powerful observation points and potential censorship points.

**DeFi fit (overall):**
- A strong starting point for incremental “private DeFi” because it can reuse public liquidity.
- But it inherits the fundamental leakage of public market state.

---

### 2.3 Burn-and-Mint Privacy (wrapped “z-assets” and private domains)

**What it is (as a substrate):**
- Users lock/burn an asset in a public domain and mint a private representation (z-asset) in a private domain.

**How DeFi uses it:**
- DeFi runs *inside* the private domain over z-assets.
- The most privacy-sensitive part becomes **entry/exit** and cross-domain round-trips.

**What it can hide well:**
- Activity *inside* the private domain (positions, trading behavior), depending on the private execution model.

**What tends to leak:**
- Entry/exit timing and amounts (especially if volume is low).
- Asset-specific flows (z-asset domains naturally fragment liquidity + anonymity).

**DeFi fit:**
- Natural for cross-chain privacy and “private assets as the unit of account.”
- Often best when paired with a “privacy hub” to thicken anonymity sets across routes.

---

### 2.4 Permissioned Privacy (eligibility + selective disclosure as a guardrail)

**What it is (as a substrate):**
- ZK membership proofs / attestations that gate access (KYC/whitelist/role).
- Selective disclosure / view keys for audits, solvency checks, or dispute resolution.

**How it applies to DeFi:**
- It is usually not a standalone DeFi execution environment; it is an **overlay constraint** you apply to any private DeFi system.

**DeFi-specific tension:**
- Repeated eligibility proofs can become a stable pseudonym.
- View-key sprawl and correlated disclosures can silently deanonymise long-lived positions.

---

### 2.5 Private Rollups (full DA) — native private execution with onchain DA

**What it is (as a substrate):**
- Private execution happens in an L2/rollup with validity proofs posted to L1.
- DA is onchain (or otherwise trust-minimised), enabling more user-resilient exits than validium-style designs.

**How DeFi uses it:**
- DeFi contracts run natively in the rollup execution environment.
- Private-to-private composability is possible *within the rollup* (swap → borrow → repay) without declassification.

**Key DeFi design choice:**
- **Hybrid public/private state**: keep some global surfaces public/provable while keeping per-user positions private.

**DeFi fit:**
- Best substrate when you want a coherent “private DeFi stack” with composability.

**Key risks:**
- Proof/DA cost per DeFi operation can be high.
- Liveness and exits must be evaluated under liquidation stress (see §4 metrics and [[4 Open Problems – DeFi]]).

---

### 2.6 Private Plasma (placeholder family; limited DeFi fit)

**What it is (as a substrate):**
- Offchain execution with dispute/exit games on L1.

**Why it is hard for DeFi (in practice):**
- DeFi state is complex and time-sensitive; interactive disputes and long exit windows are economically costly.
- The “exit during stress” requirement is more stringent for positions than transfers.

In this DeFi pass, Plasma-style private DeFi is treated as a **low-readiness** substrate unless a concrete, modernized design is in scope.

---

### 2.7 Private Validium — validity proofs with off-chain encrypted DA

**What it is (as a substrate):**
- Validity proofs ensure state transitions are correct.
- Data availability is offchain (operator/committee serves encrypted state).

**DeFi fit:**
- Attractive for high throughput private swaps/lending/perps.

**DeFi-specific risk amplification:**
- If DA is withheld or censorship occurs, users may not be able to **withdraw collateral or close debt** before liquidation.
- Market stress creates adversarial incentives for operators/committees.

For DeFi, the question is less “is the proof correct?” and more “can users always access the data needed to protect themselves in time?”

---

## 3) DeFi-specific pattern extensions (what DeFi adds on top)

These patterns show up across multiple substrates; they are “DeFi-shaped” because they address pricing/risk/liquidations rather than simple ownership updates.

### 3.1 Notes-as-state AMMs and lending

**Pattern:** represent positions (LP shares, collateral, debt) as notes/commitments.

- Works naturally in shielded pools and private rollups.
- Requires careful circuit design to enforce:
  - AMM invariants and fee rules
  - interest accrual and utilisation updates
  - collateral ratio checks and liquidation eligibility

**Core tension:** the more pricing/risk state you keep private, the harder it becomes to:
- quote prices,
- prove solvency to third parties,
- interoperate with public markets.

### 3.2 Hybrid public/private contract state

**Pattern:** make **global market state** public (or publicly provable) while keeping per-user state private.

Examples of “public/provable surfaces” that often remain visible:
- AMM reserve vector / invariant-relevant fields
- Aggregate debt, utilisation, total collateral (or commitments plus proofs of consistency)
- Oracle references / timestamps

**Why it matters:**
- It is often the pragmatic way to preserve safety and composability.
- But it creates residual leakage: observers can see *that* a large swap/liquidation happened even if they can’t see who.

### 3.3 Intent-based trading + encrypted orderflow (MEV-aware envelope)

**Pattern:** hide trade intent until ordering/settlement, using:
- encrypted mempools / threshold encryption,
- private relays,
- batch auctions / frequent batch clearing,
- commit–reveal.

**Why it’s DeFi-specific:**
- Even with private state, DeFi is vulnerable to pre-trade leakage (sandwiching, liquidation sniping).
- Orderflow privacy is often required to make private DeFi *economically meaningful*.

### 3.4 Privacy-compatible liquidations, keepers, and auctions

**Pattern:** undercollateralisation triggers and liquidation eligibility are proven without revealing full position state.

Design knobs:
- proofs of “position is liquidatable” without revealing the position,
- commit–reveal auctions to reduce sniping/collusion,
- keeper designs that avoid privileged visibility or monopoly execution rights.

**Core tension:**
- Hide too much → solvency risk or delayed liquidations.
- Reveal to a privileged set → reintroduces surveillance, MEV, and governance power.

### 3.5 Vault/aggregator entry/exit privacy

**Pattern:** user-facing vault shares are private, while the strategy composes swaps/borrows downstream.

- Helps prevent “who deposited/withdrew when” leakage.
- Does not automatically hide the strategy’s market impact if downstream actions are public.

### 3.6 “Privacy hub” buffering cross-domain flows

**Pattern:** a shared shielded pool / shielded bridge hub sits between:
- public domains ↔ private DeFi domains ↔ other L2s/app-chains.

Goal:
- thicken anonymity sets,
- reduce amount/timing correlation at boundaries,
- make “round trips” harder to stitch.

### 3.7 Shared sequencing for atomic multi-venue bundles

**Pattern:** shared sequencers enable atomic bundles across rollups/venues (swap + borrow + repay), and create a natural hook point for privacy-aware ordering.

Trade-offs:
- introduces sequencing trust and failure modes,
- can become a new central observation point if not privacy-preserving.

### 3.8 TEE-based confidential EVM / confidential L2 execution

**Pattern:** encrypted contract state executed inside enclaves; chain sees ciphertext + attestations.

Why it matters for DeFi:
- Can support more EVM-like programmability with different trust assumptions.
- Verification/audit and side-channel / operator trust become first-order concerns.

---

## 4) Reinterpreting the Transfers metric lens for DeFi

Transfers Phase A metrics remain useful if we change the unit from “transfer” to “DeFi operation.”

### 4.1 Cost metrics (replace “L1 gas per transfer”)

Track per operation type (swap, LP join/exit, borrow/repay, liquidation):

- **L1 verification cost** (gas) per batch and per op
- **DA bytes** per op (calldata / blobs / commitments)
- **Proving time** (client-side and/or prover) per op
- **End-to-end latency** (submission → inclusion → finality), especially for liquidations and close/repay

### 4.2 Throughput metrics (replace “TPS for transfers”)

- **Ops/sec under normal load** for the common case (small swaps, position updates)
- **Stress-mode throughput** during liquidation waves
- **Hot-spot contention**: what happens when many ops hit the same market?

### 4.3 Programmability & composability

- Can you express financial logic safely (interest curves, liquidation rules, invariant math) in the private execution model?
- Can private contracts call other private contracts atomically?
- What is the interoperability story with public EVM DeFi?

### 4.4 UX and operational overhead

- Key/state management for long-lived positions (notes/witnesses)
- Relayer/paymaster dependence and failure modes
- How users monitor positions without creating analytics backdoors

### 4.5 Trust & exit assumptions

DeFi puts a spotlight on:
- DA operator/committee trust
- sequencer censorship risk
- time-to-self-rescue (exit + close positions) under stress

---

## 5) Mapping DeFi operations to the “minimum public/provable surface”

A practical way to think about private DeFi design is: **what must remain public (or publicly checkable) to keep the protocol safe?**

| DeFi write | What must be enforced | Typical minimum public/provable surface | Residual leakage even with perfect per-user privacy |
| --- | --- | --- | --- |
| Swap (AMM) | Pricing + invariant + fees | Reserves/invariant fields *or* a proof that the committed state evolves correctly; oracle refs for hybrid designs | Large swaps move global state; pool-specific activity becomes visible |
| LP join/exit | Share mint/burn correctness | Total liquidity / share supply (or commitments + proofs) | Large adds/removes are visible via pool state changes |
| Borrow/repay | Debt accounting + interest + utilisation | Aggregate debt/utilisation; risk params; oracle refs | Utilisation jumps reveal coarse credit activity |
| Collateral adjust | Collateral ratio constraints | Risk params; oracle refs; sometimes aggregate collateral metrics | Large position management correlates with volatility events |
| Liquidation / auction | “Liquidatable” predicate + execution correctness | Proof that a position is eligible; public auction clearing or commitments; oracle refs | Liquidation events are inherently attention magnets; timing is revealing |
| Vault deposit/withdraw | Share accounting | Total shares/TVL (or commitments + proofs) | Strategy-level actions can reveal flows even if user shares are private |

This table is deliberately high level; exact surfaces depend on whether the design chooses **public markets with private positions** vs **private markets with different quoting/clearing mechanisms**.

---

## 6) Mechanism trade-offs summary (DeFi view)

The table below summarizes “what each substrate tends to be good for” in DeFi.

| Mechanism family (substrate) | Best for (DeFi) | Main DeFi limitation / risk |
| --- | --- | --- |
| L1 Overlay | Hiding the *actor* interacting with public DeFi; incremental privacy UX | Doesn’t hide market activity; lifecycle graph + relayer fingerprints remain |
| L1 Shielded Pools | Notes-as-state DeFi; or privacy router into public DeFi | Either heavy private-market design, or public-state leakage persists; boundary unlinkability hard |
| Burn-and-Mint | Cross-domain private assets; private domain accounting | Entry/exit correlation; fragmentation across assets/domains |
| Permissioned Privacy | Eligibility + selective disclosure on top of private DeFi | Credentials/view keys can become stable identifiers over long-lived positions |
| Private Rollups (full DA) | “Private DeFi stack” with composability and stronger exits | Higher proof/DA cost per op; liveness under stress is critical |
| Private Plasma | (Rare) offchain execution with dispute exits | Poor fit for time-sensitive DeFi; complex state + exit delays |
| Private Validium | High-throughput private execution | DA/exit trust and censorship are amplified by liquidation deadlines |
