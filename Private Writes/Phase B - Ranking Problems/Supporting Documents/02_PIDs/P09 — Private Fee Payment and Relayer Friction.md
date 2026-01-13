# P09 — Private Fee Payment and Relayer Friction

### 1.1 Problem overview (tl;dr)

Private transactions still need to pay fees. If fee payment leaks identity (e.g., via public gas funding), privacy breaks. Systems often rely on relayers or complex fee abstraction, creating UX friction, trust dependencies, and potential censorship vectors.

### 1.2 Stakeholders & pain

- **Users**: Need private fee payment without deanonymizing themselves; relayers add complexity and cost.
- **Wallets**: Must support fee abstraction and relayer networks; hard to make seamless.
- **Relayers / infrastructure**: Must be incentivized and reliable; can become central points of failure.
- **Protocols**: Need fee mechanisms that don't compromise privacy or decentralization.

### 1.3 Why it matters (impact)

- If users must fund gas publicly, transactions become linkable.
- Reliance on relayers introduces trust and censorship risk.
- UX friction reduces adoption of private systems.

### 1.4 Current approaches / solution landscape

- Relayers that pay fees and charge users in private assets.
- Meta-transactions and account abstraction (sponsored transactions).
- Private fee markets (rare, complex).

### 1.5 Gaps / failure modes

- Relayers can censor or deanonymize users.
- Fee abstraction is hard to standardize across wallets/apps.
- Private fee payment often requires trusted intermediaries.

### 1.6 Success looks like

- Users can transact privately without managing public gas funding.
- Fee mechanisms are decentralized and robust to censorship.
- Wallet UX is simple and consistent.

### 2.1 Header

If you solve private fee payment cleanly, you remove a major practical barrier to private transaction adoption and reduce reliance on trusted relayers.

### 2.2 Body

#### What is the core of the problem?

Private transactions must pay for execution (gas, sequencer fees). But if the fee payment is public (e.g., funding ETH from a KYC exchange), it can link the user to the private transaction. Relayers can hide this, but introduce new trust and UX complexity.

#### Why is it hard?

- Fees are typically paid in a public base asset.
- Private systems may not have native private fee accounting.
- Relayers must be incentivized and must not leak metadata.

#### How does it fail in practice?

- Users fund gas publicly, linking identity to private actions.
- Relayers censor, overcharge, or leak metadata.
- Wallets struggle to integrate relayers reliably.

### 2.3 Scope & boundaries

In scope:
- Fee payment mechanisms for private transactions
- Relayers and meta-transaction UX
- Censorship and trust tradeoffs

Out of scope:
- General gas fee economics in public systems

### 2.4 Assumptions

- Users want privacy against chain observers and infrastructure.
- Fee payment must be practical for mainstream use.

### 2.5 Metrics / signals

- % of private transactions using relayers
- Relayer decentralization (number, diversity)
- UX friction (steps to transact privately)
- Censorship incidents / relayer downtime

### 2.6 Score (1–5)

- **Severity**: 4  
- **Tractability**: 3  
- **Uncrowdedness**: 3  
- **Leverage**: 4  

### 2.7 Evidence & uncertainty

#### Key references

- Appendix C: "Global Problem Catalog & Radar"
- Problem file: "Private Fee Payment and Relayer Friction"

#### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Confidence |
|---|---|---|
| P09-C1 | Tornado Cash documentation describes relayers as a mechanism to solve the fee-payment dilemma by having a relayer pay gas for withdrawals and take a fee from the withdrawn amount. | High |
| P09-C2 | Tornado Cash documentation emphasizes that operational choices (including relayer usage and avoiding correlating behaviors) affect anonymity, implying relayer selection and behavior can impact privacy outcomes. | Medium |
| P09-C3 | EIP-2771 standardizes meta-transactions using a trusted forwarder that appends the original sender, making the trust boundary around relayers/forwarders explicit in the protocol design. | High |
| P09-C4 | EIP-4337 introduces bundlers and paymasters for submitting user operations and sponsoring gas; ecosystem documentation notes bundlers may apply local policies/reputation scoring, which can introduce censorship/availability friction for users. | Medium-High |
| P09-C5 | Aztec documentation describes fee abstraction via accounts and fee-paying contracts / sponsored fee payment, illustrating how private systems often rely on additional infrastructure for fee payment without exposing user identities. | Medium |
| P09-C6 | Reliance on third-party relayers/paymasters can introduce variable pricing, reliability risk, and new privacy tradeoffs (e.g., relayer fingerprinting); the magnitude varies by implementation and is not uniformly quantified. | Medium-Low (inference) |
