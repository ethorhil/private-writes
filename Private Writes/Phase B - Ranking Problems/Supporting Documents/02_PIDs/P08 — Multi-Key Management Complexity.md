# P08 — Multi-Key Management Complexity

## 1.1 Problem overview (tl;dr)

Private systems often require multiple keys (spend/view keys, encryption keys, viewing keys, recovery keys). This complexity is hidden until users need to recover accounts, delegate view access, or integrate with apps. Poor UX increases custody risk and reduces adoption.

## 1.2 Stakeholders & pain

- **Users**: Confusing key types; high risk of loss or accidental disclosure.
- **Wallets**: Must abstract complexity while supporting advanced features (view keys, recovery).
- **Apps/Integrators**: Need consistent key interfaces for private assets and identities.
- **Compliance/auditors**: Need view delegation without spending authority.

## 1.3 Why it matters (impact)

- Key mishandling leads to irreversible loss or privacy compromise.
- Complexity pushes users to custodians, weakening self-sovereignty.
- Delegation (view keys) introduces new privacy and security risks.

## 1.4 Current approaches / solution landscape

- Unified key derivation schemes (HD wallets) for shielded pools.
- Viewing keys / selective disclosure mechanisms.
- Wallet abstractions that hide key structure (but still need recovery/delegation flows).

## 1.5 Gaps / failure modes

- Users can't reason about which keys reveal what.
- Recovery flows are brittle and inconsistent.
- Delegation often requires exporting sensitive material.

## 1.6 Success looks like

- Simple mental model for users (few key concepts).
- Safe delegation primitives (view-only, scoped, revocable).
- Standard interfaces across wallets/apps.

## 2.1 Header

If you make multi-key privacy systems usable without custody, you unlock broader adoption and safer delegation/compliance workflows.

## 2.2 Body

### What is the core of the problem?

Privacy systems often separate spending authority from viewing/decryption authority. Users may need different keys for:
- Spending
- Viewing incoming/outgoing transactions
- Decrypting notes/messages
- Recovering accounts

This is necessary for privacy features but creates UX and security pitfalls.

### Why is it hard?

- Key roles are cryptographically distinct; can't always be merged.
- Delegation requires careful scoping (what can a viewer see?).
- Recovery must handle multiple key types and derivations.

### How does it fail in practice?

- Users export full keys to share view access, leaking more than intended.
- Wallets hide complexity but fail during recovery/migration.
- Custodians manage keys for users, recreating trusted intermediaries.

## 2.3 Scope & boundaries

In scope:
- Key management complexity for private assets/identities
- Delegation and recovery flows
- Standards for key interfaces

Out of scope:
- General key management for public crypto assets

## 2.4 Assumptions

- Privacy requires separating spend vs view/decrypt capabilities.
- Users will need recovery and delegation features.

## 2.5 Metrics / signals

- Frequency of key-related loss incidents
- Wallet support for view-only delegation
- Recovery success rates
- Adoption of unified key standards

## 2.6 Score (1–5)

- **Severity**: 4  
- **Tractability**: 3  
- **Uncrowdedness**: 3  
- **Leverage**: 4  

## 2.7 Evidence & uncertainty

### Key references

- Appendix C: "Global Problem Catalog & Radar"
- Problem file: "Multi-Key Management Complexity"

### Sprint 2 key claims (ClaimID → evidence map)

| Claim ID | Claim | Confidence |
|---|---|---|
| P08-C1 | Zcash shielded wallet/key material is explicitly multi-component (e.g., multiple derived keys including spending key components and viewing-key-related material), not a single "one keypair" abstraction. | High |
| P08-C2 | ZIP 316 introduces Unified Addresses and Unified Viewing Keys to reduce user-facing friction and cognitive overhead from multiple receiver/address types, reflecting the ecosystem need to manage multiple keys/address domains. | High |
| P08-C3 | ZIP 310 distinguishes security properties of different Sapling viewing keys (e.g., what can be learned from full viewing keys vs incoming viewing keys), making "view delegation" a first-class feature with non-trivial privacy consequences. | High |
| P08-C4 | ERC-5564 (Stealth Addresses) defines separate spending and viewing keys and requires recipients to scan announcements (using view tags), adding ongoing scanning and key-management overhead in "stealth address" style privacy. | Medium-High |
| P08-C5 | Even when wallets hide internal key structure, multi-key delegation and recovery workflows create user-facing UX and security failure modes (loss, accidental disclosure, mis-scoping of viewing access); evidence for exact prevalence is limited and implementation-dependent. | Medium-Low (inference) |
