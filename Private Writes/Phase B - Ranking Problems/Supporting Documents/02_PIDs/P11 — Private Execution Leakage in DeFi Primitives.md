# P11 — Private Execution Leakage in DeFi Primitives

## 1.1 Problem overview (tl;dr)

Even if execution is private, DeFi primitives often leak information through public state updates (prices, reserves, interest rates, liquidations). These signals enable inference about private activity and can be exploited economically (MEV, liquidation hunting). Privacy-preserving DeFi must balance secrecy with the need for shared state.

## 1.2 Stakeholders & pain

- **Users**: Want private trades/positions; still leak info via state changes.
- **Protocols**: Need to design primitives that minimize leakage without breaking functionality.
- **MEV/searchers**: Exploit leakage for profit; can harm users.
- **Researchers/builders**: Need new designs for private AMMs, lending, liquidation.

## 1.3 Why it matters (impact)

- Private execution alone doesn't guarantee privacy.
- Leakage enables targeted attacks (sandwiching, liquidation sniping).
- Weak privacy reduces adoption of private DeFi.

## 1.4 Current approaches / solution landscape

- Batch auctions / delayed execution to reduce signal granularity.
- Private AMMs with hidden reserves or MPC-based pricing.
- Obfuscation via noise or aggregation (often reduces efficiency).

## 1.5 Gaps / failure modes

- Core primitives require public outputs (prices, rates).
- Thin liquidity amplifies leakage (small trades move price).
- Liquidations inherently reveal distress.

## 1.6 Success looks like

- DeFi primitives that preserve privacy while maintaining usability.
- Reduced inference from public state.
- MEV-resistant private execution with minimal leakage.

## 2.1 Header

If you reduce leakage from DeFi primitives under private execution, you make private DeFi meaningfully private and reduce economic exploitation.

## 2.2 Body

### What is the core of the problem?

DeFi requires shared state. Even if inputs are hidden, outputs like:
- Pool prices/reserves
- Interest rates/utilization
- Liquidation events

can reveal information about private actions.

### Why is it hard?

- Market-making and lending depend on transparent pricing and risk signals.
- Hiding too much breaks price discovery or solvency guarantees.
- Aggregation/batching reduces leakage but adds latency and complexity.

### How does it fail in practice?

- Observers infer trade direction/size from price impact.
- Liquidation events reveal distressed positions.
- MEV persists via public outputs and timing signals.

## 2.3 Scope & boundaries

In scope:
- Leakage via DeFi shared state under private execution
- AMMs, lending, liquidations, derivatives primitives

Out of scope:
- Privacy of user identities unrelated to DeFi state leakage

## 2.4 Assumptions

- Private execution systems will support DeFi primitives.
- Some public outputs are unavoidable for price discovery/solvency.

## 2.5 Metrics / signals

- Inference accuracy from public state (trade size/direction)
- Frequency of MEV/exploitation under private execution
- Leakage reduction vs efficiency tradeoff

## 2.6 Score (1–5)

- **Severity**: 4  
- **Tractability**: 2  
- **Uncrowdedness**: 4  
- **Leverage**: 4  

## 2.7 Evidence & uncertainty

### Key references

- Appendix C: "Global Problem Catalog & Radar"
- Problem file: "Private Execution Leakage in DeFi Primitives"

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Confidence |
|---|---|---|
| P11-C1 | Uniswap v2's constant-product AMM design updates publicly measurable pool state (reserves/prices); when those outputs are observable, they reveal information about trade direction and approximate size via price impact/slippage. | High |
| P11-C2 | Maker Protocol liquidations transfer collateral from undercollateralized vaults and trigger auctions; such liquidation events provide strong public signals that some position crossed risk thresholds and reveal information about the liquidation size and timing. | Medium-High |
| P11-C3 | Aave's interest rate model derives borrowing/supplying rates from on-chain reserve state (including utilization), implying that utilization and rate changes can leak aggregate borrowing/supplying activity even if individual positions were private. | Medium-High |
| P11-C4 | Flash Boys 2.0 documents that visible transaction-order dependencies in decentralized exchanges are economically exploited (MEV), motivating private execution while also underscoring how economically salient signals are rapidly arbitraged. | High |
| P11-C5 | Rialto (privacy-preserving exchange marketplace) aims to retain market price discovery while providing confidentiality/unlinkability, reflecting an intrinsic tension between privacy and the need to reveal some market-clearing information. | Medium |
| P11-C6 | Even with private execution, shared-state DeFi primitives often must expose outputs (prices, liquidations, funding/interest rates), enabling inference—especially in low-liquidity or highly patterned activity; quantification is market- and implementation-specific. | Medium (partly inference) |
