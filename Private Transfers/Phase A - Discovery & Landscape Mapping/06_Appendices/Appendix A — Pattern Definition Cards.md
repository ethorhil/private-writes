## 1. **L1 Overlay – Stealth / OTR**

L1 overlays add **address-level privacy** on top of Ethereum’s existing account model. Instead of changing how state is represented, they route payments through **one-time “stealth” addresses** derived for the recipient, so an observer cannot easily link an incoming payment to the recipient’s main public address. Balances remain standard ERC‑20 or ETH balances on L1; overlays simply change how funds are sent and discovered.

Because overlays inherit Ethereum’s full DA and trust assumptions, they keep **amounts and the sender’s funding address public**, but hide which long‑term account the receiver actually controls. They typically aim for **low added gas cost**, minimal changes to existing wallets and contracts, and **open membership**. Selective disclosure is often handled via **viewing keys or derivation paths** that allow a user to prove or reconstruct their own history for auditors. Representative deployments include systems like Umbra and Fluidkey, which differ mainly in UX and notifier infrastructure.
#### **One-sentence definition**

A pattern where the sender derives a fresh, one-time address for the recipient so the on-chain payment cannot be linked to the recipient’s public identity.

#### **Mechanism summary**
- Sender and recipient derive a unique stealth address via off-chain exchange.
- Funds are sent to this address, unlinking transfer and identity.
- Recipient scans for outputs they can spend.
- Uses standard L1 transactions; no private state.

#### **What problem it solves**
- Prevents public linkage to a recipient.
- Reduces transaction-graph exposure.

#### **Key strengths**
- Minimal protocol assumptions.
- Easy integration with existing wallets/tokens.
- No private state required.

#### **Key limitations**
- Sender and amounts remain public.
- Requires scanning or delegated monitoring.
- Susceptible to metadata clustering.

#### **When to use**

- Lightweight receiver privacy on L1.
- Zero-friction integration with existing infrastructure.

#### **What it is NOT**

- Not a full shielded system.
- Not a mixer or rollup.

#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Balances remain as standard ERC‑20/ETH on Ethereum L1; privacy is added via one‑time stealth addresses, so data availability and correctness are fully inherited from L1.
- **Cross‑cutting axes:** Deployments are typically **open membership** with **public default visibility** (senders and amounts remain public) and at most **ad‑hoc selective disclosure** via off‑chain reporting or wallet tooling.
- **DA/trust axis → Trust Assumptions:** Overlays sit near the **trust‑minimized / on‑chain DA** end of the DA/trust axis, since users do not rely on additional operators or DA committees for safety. In the master comparison table (§5.2), this is reflected in a **Trust Assumptions** score of **3**, indicating that users inherit Ethereum L1’s availability and censorship surface without introducing new centralized DA points.

### Threat model

**Adversaries and capabilities**

- **On-chain observers / analytics firms:** Can see the full L1 transaction graph, including stealth-address creation, funding flows, and timing information. They cannot directly break the stealth-address derivation, but can use clustering and metadata analysis.
- **Counterparties and application front-ends:** May log or leak auxiliary metadata (IP addresses, user agents, timing correlations) that make it easier to link stealth addresses back to long-lived identities.
- **Optional scanning / monitoring services:** If recipients outsource scanning for incoming funds, these services can see which stealth outputs belong to which users and may leak or correlate that information.

**Assets and properties at risk**

- **Recipient privacy and linkability:** The main asset is the unlinkability between a recipient’s public identity (or main address) and the stealth address receiving funds. Sender identity and amounts remain public on L1.
- **Graph-level privacy:** Adversaries aim to reconstruct payment flows and social/organizational relationships from the public graph, even when recipients use stealth addresses.
- **Funds safety:** Asset safety is essentially that of ordinary ERC-20/ETH transfers on Ethereum L1; the overlay does not introduce new DA-related failure modes.

**High-level threats and mitigations**

- **De-anonymization via metadata and heuristics:**  
  Adversaries combine timing, amount patterns, reuse of funding sources, and off-chain metadata to link stealth outputs to real-world identities. Mitigations include careful wallet design (e.g., separating funding sources), avoiding address reuse, and minimizing side channels in application front-ends.

- **Scanning failures or dependence on third parties:**  
  If recipients rely on third-party scanners or relays, outages or misbehavior can delay detection of incoming funds, though not prevent eventual spending. Self-hosted scanning and redundant monitoring reduce this operational dependency.

- **Key compromise or poor hygiene:**  
  Compromise of stealth keys or main keys reveals linkages and may lead to asset loss, just as in ordinary L1 usage. Better key management and hardware wallets mitigate this risk.

Because **L1 Overlays** do not introduce a new off-chain DA layer, they largely **inherit Ethereum L1’s DA/trust properties**. The main risks are around **privacy leakage and operational dependencies** (e.g., scanners), not catastrophic DA failures. This is why the pattern receives a **mid-range Trust Assumptions score (3)** in the comparative evaluation: it is close to L1-equivalent on the DA/trust axis, with only modest additional operational assumptions.

---

## 2. **L1 Shielded Pools**


L1 shielded pools move privacy from the addressing layer into the **state model itself**. Users hold encrypted **UTXO/nullifier notes** inside an on-chain pool contract, and prove in zero knowledge that they are spending valid notes and creating new ones without revealing sender, receiver, or amount. The pool lives directly on Ethereum L1, so DA is guaranteed by calldata and state, and correctness is enforced by on-chain proof verification.

This design offers **strong privacy guarantees** at the cost of **heavy per‑transfer proving and verification costs** and **limited throughput**—only a modest number of zk transfers fit in each block. Programmability ranges from simple mixers to more expressive shielded DeFi (e.g., multi‑asset pools). UX is typically more complex than overlays: users must manage notes, relayers, and multiple keys. Membership can be open or permissioned, and **selective disclosure capabilities vary widely** (from no SD to advanced viewing-key or association-set–style proofs). Examples include Tornado-like mixers, Railgun-like systems, Privacy Pools, zkBob, and Panther-style designs.

#### **One-sentence definition**

A pattern where transfers occur inside a shared shielded pool using commitments and nullifiers so that senders, receivers, and amounts are hidden.

#### **Mechanism summary**

- Users deposit assets as commitments.
- Transfers create new commitments and nullify old ones.
- Anonymity increases with pool size.
- Only proofs/nullifiers are revealed on-chain.

#### **What problem it solves**

- Full transactional graph privacy.
- Privacy for senders, receivers, and amounts.

#### **Key strengths**

- Strongest L1-native privacy.
- Anonymity set grows as pool grows.
- Multi-asset capable.

#### **Key limitations**

- Heavy proof costs.
- Users must manage notes/keys.
- High on-chain overhead.

#### **When to use**

- When full privacy is required at L1.
- When apps can manage private note state.

#### **What it is NOT**

- Not an overlay.
- Not a scalability solution.

#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Users hold encrypted UTXO-like notes inside an on-chain pool; commitments and nullifiers are posted directly to Ethereum L1, so data availability and correctness are enforced at the base layer rather than by an off-chain DA committee.
- **Cross-cutting axes:** The pattern is **membership-agnostic**: real deployments can be fully **open** or **permissioned** (e.g., KYC-gated shielded pools), which we treat as attributes rather than separate patterns. Default **visibility** is that senders, receivers, and amounts are hidden in the pool, and many deployments offer at most **basic or protocol-level selective disclosure** (e.g., viewing keys or association-set proofs) for auditors or compliance teams.
- **DA/trust axis → Trust Assumptions:** Because all commitments and nullifiers live on L1, L1 Shielded Pools sit near the **trust-minimized / on-chain DA** end of the DA/trust axis: users do not depend on additional DA committees to reconstruct the private state. In the master comparison table (§5.2), this corresponds to a **Trust Assumptions** score of **3**, aligning Shielded Pools with other L1-native patterns that introduce minimal additional DA/trust beyond Ethereum itself.

### Threat model

**Adversaries and capabilities**

- **On-chain observers:** Can see deposits, withdrawals, and on-chain proof/nullifier data, but not the internal mapping from commitments to owners. They use timing, amount patterns, and external information to narrow potential links.
- **Pool operators / relayers / infrastructure providers:** May see transaction metadata (e.g., IPs, timing, fee payment details) and can censor, delay, or reorder user transactions at the interface layer.
- **Protocol implementers / circuit authors:** A bug or backdoor in the zk-circuits, parameter generation, or contract logic can enable undetected inflation or deanonymization.
- **On-chain adversaries (L1 validators):** Can censor or reorder shielded-pool transactions, but cannot directly break privacy or forge valid zk-proofs.

**Assets and properties at risk**

- **User funds and supply integrity:** Bugs in circuits or contract logic can, in the worst case, allow undetected inflation or theft. DA for commitments and nullifiers is guaranteed by L1, but correctness depends on the implementation.
- **Transactional privacy:** Privacy can be weakened by small anonymity sets, timing/amount leakage, or compromised viewing keys.
- **Key and note safety:** Loss or compromise of viewing/spending keys can lead to asset loss or unintended disclosure.

**High-level threats and mitigations**

- **Protocol or circuit bugs (inflation / theft):**  
  Mitigated by formal verification, audits, multi-party parameter ceremonies, and conservative upgrade processes. Still, this is a central “trust in implementation” assumption beyond L1.

- **Deanonymization via side channels:**  
  Timing analysis, amount correlation, or network-level metadata can reduce effective anonymity. Larger pools, fixed denomination notes, use of relays, and privacy-preserving network layers (e.g., Tor) help mitigate this.

- **Censorship or poor UX at the interface layer:**  
  Relayers or front-ends may censor or degrade service for certain users. Allowing direct on-chain interactions, multiple relay providers, and fallback interfaces mitigates this.

Because **all commitments and nullifiers are stored on Ethereum L1**, L1 Shielded Pools sit near the **trust-minimized, on-chain DA side** of the **DA/trust axis**. Users do not rely on external DA committees for safety, but they **do** rely on the correctness of zk-circuits and implementation. This combination justifies a **Trust Assumptions score of 3** in the comparative evaluation: stronger than off-chain DA patterns, but still with meaningful protocol-level trust in circuits and operators.


---

## 3. **Burn-and-Mint Privacy**

^ccbe02
Burn-and-mint systems provide privacy by **breaking the link** between origin and destination across two contexts—often two addresses, pools, or even chains. A user **burns** tokens in one place and later **mints** new tokens elsewhere, supplying a ZK proof that the burn and mint are related and well-formed, without revealing which specific burn funds which mint.

This pattern offers **strong unlinkability** and can be relatively simple conceptually, but most deployments are **early-stage**. Current designs tend to have **non-trivial gas costs** (burn + mint + proof verification) and limited ecosystem maturity compared to shielded pools or rollups. Programmability is typically focused on transfer semantics rather than general-purpose private smart contracts. Membership can be open or permissioned, and selective disclosure is usually minimal or ad-hoc, though richer SD profiles could be layered on in future implementations.

#### **One-sentence definition**

A pattern where users burn tokens in one context and mint equivalent tokens elsewhere so no on-chain link exists between the burn and mint.

#### **Mechanism summary**

- Tokens are burned to sever provenance.
- zk-proof validates eligibility to mint without linking events.
- Tokens reappear at a fresh address.
- Maintains supply consistency.

#### **What problem it solves**

- Breaks transfer linkage.
- Enables strongly unlinkable transfers.

#### **Key strengths**

- Clean unlinkability.
- Simple conceptual model.
- Stateless.

#### **Key limitations**

- Requires strong anti–double-mint guarantees.
- Statelessness limits expressiveness.
- Not suitable for multi-step workflows.

#### **When to use**

- Unlinkable transfers without maintaining private history.
- Simple fungible token models.

#### **What it is NOT**

- Not a shielded pool.
- Not an L2 pattern.

#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Burn-and-mint designs are effectively **stateless**: tokens are destroyed in one context and re-created in another, with a proof that the burn and mint are consistent. All events and proofs are recorded on-chain (typically Ethereum L1), so data availability and supply correctness are enforced by the base layer rather than by an off-chain DA committee.

- **Cross-cutting axes:** The pattern itself is **membership-agnostic**: deployments may be fully **open** or **permissioned**, which we treat as attributes rather than separate mechanisms. Default **visibility** and **selective disclosure** inherit from the environments being burned from and minted into: canonical deployments look like standard fungible tokens with **public balances** and at most **ad-hoc SD** (e.g., off-chain reporting or bespoke proofs) unless additional SD layers are added.

- **DA/trust axis → Trust Assumptions:** Because all necessary data to verify burns and mints lives on-chain and there is no long-lived off-chain private state to reconstruct, Burn-and-Mint sits toward the **trust-minimized / on-chain DA** end of the DA/trust axis. In the master comparison table (§5.2), this is reflected in a **Trust Assumptions** score of **4**, indicating strong L1-backed guarantees with only minor additional trust in proving and operational infrastructure for liveness.

### Threat model

**Adversaries and capabilities**

- **On-chain observers / analytics firms:** Can see burn and mint events, but the design aims to prevent them from linking specific burns to specific mints, even with sophisticated graph analysis.
- **Provers / bridge or minting contracts:** Can attempt to accept invalid proofs, misconfigure eligibility criteria, or mishandle edge cases (e.g., replayed proofs), potentially enabling double-mints or unauthorized mints.
- **Application front-ends / relayers:** May leak metadata (IP addresses, timing, origin smart contract) that narrows the anonymity set.

**Assets and properties at risk**

- **Supply integrity and user balances:** The critical safety property is that total minted tokens never exceed what has been burned (modulo fees). Bugs in proofs or contract logic can violate this, leading to inflation or theft.
- **Unlinkability between burns and mints:** Privacy hinges on preventing observers from matching burns to subsequent mints, even when they know the general flow and timing.
- **Liveness of minting:** If proving or mint contracts are censored or misconfigured, users may be unable to mint after a valid burn.

**High-level threats and mitigations**

- **Double-mint or inflation via protocol bugs:**  
  Mitigated by careful circuit design, audits, and strict on-chain verification of proofs and nullifiers (if used). A critical bug here can permanently damage trust in the system.

- **De-anonymization via side channels:**  
  Small anonymity sets, distinctive amounts, or tight burn/mint timing can leak linkages. Larger anonymity sets, standardized denominations, and randomized delays between burn and mint help mitigate this.

- **Censorship or liveness failures at the minting interface:**  
  Censoring mints or requiring centralized infrastructure to submit proofs can temporarily block users from redeeming. Supporting direct on-chain proof submission and multiple front-ends reduces this risk.

Because **all burns, mints, and proofs are recorded on-chain and there is no long-lived off-chain private state to reconstruct**, Burn-and-Mint designs sit toward the **trust-minimized / on-chain DA end** of the **DA/trust axis**. Users rely primarily on L1 and the correctness of the proving and contract logic, not on external DA committees. This justifies a **Trust Assumptions score of 4** in the comparative evaluation: strong L1-backed guarantees with only modest additional trust in proving infrastructure.


---

## 4. **Permissioned Privacy**


Permissioned Privacy refers to systems where **controlled membership and compliance-friendly selective disclosure are the primary design drivers**. Transfers occur in an **access‑controlled environment**—for example, tokenization platforms that require KYC or credential checks before users can hold or move assets. Within this environment, transactions may be locally private, but participants can produce structured proofs or disclosures for auditors, regulators, or counterparties as needed.

Mechanistically, Permissioned Privacy deployments can sit on top of **multiple underlying mechanisms** (e.g., L1 tokens, shielded pools, rollups, Validium). In the taxonomy, they are treated as a distinct pattern **only when permissioning and disclosure policy define the system**, not merely as attributes added to an otherwise open pattern. These systems often exhibit **smoother UX after onboarding**, as transfers may look similar to ordinary token transfers, and they tend to support **richer, policy-driven selective disclosure** than most open systems. Membership is explicitly permissioned; SD is typically protocol-level or rich‑policy; trust assumptions depend on both the underlying mechanism and the governance of the permissioning layer.

#### **One-sentence definition**

A pattern where transfers occur in an access-controlled environment with identity or credential gating and selective disclosure.

#### **Clarifying notes (added)**

_In this taxonomy, “Permissioned Privacy” refers to systems where the primary design axis is controlled membership and compliance-friendly selective disclosure. Mechanistically, similar permissioning and disclosure layers can also be added on top of other mechanisms (e.g., Shielded Pools or private L2s); we name it as a pattern here for communicative clarity._

#### **Mechanism summary**

- Access restricted to verified members.
- Privacy via commitments or attestations.
- Selective disclosure supports audits/compliance.
- Policy logic enforced at the protocol level.

#### **What problem it solves**

- Compliant private transfers.
- Confidentiality with structured auditability.

#### **Key strengths**

- Built-in selective disclosure.
- Strong governance and visibility control.
- Compatible with regulated deployments.

#### **Key limitations**

- Limited anonymity set.
- Depends on identity frameworks.
- Not suited to open participation.

#### **When to use**

- Regulated environments.
- Systems requiring controlled access.

#### **What it is NOT**

- Not an open anonymity system.
- Not a shielded pool.

#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Permissioned Privacy describes systems where the primary design drivers are **controlled membership and structured selective disclosure**, rather than a specific DA mechanism. In practice, many deployments are implemented as **permissioned chains**, **Validium-like systems**, or **governed rollups** where a small, governed operator set controls sequencing and data availability.

- **Cross-cutting axes:** By definition, membership is **permissioned**: access is gated by identity, credentials, or governance decisions. Default **visibility** is constrained within the permissioned domain (participants and operators), and these systems generally sit toward the **protocol-level / rich-policy end** of the selective disclosure axis, with built-in audit and compliance hooks.

- **DA/trust axis → Trust Assumptions:** Because data availability and state recovery typically depend on a **governed operator set or DA committee**, Permissioned Privacy patterns sit toward the **heavier DA/operator trust** side of the DA/trust axis. In the master comparison table (§5.2), this is reflected in a **Trust Assumptions** score of **2**, indicating that users cannot recover the full state from Ethereum L1 alone and must trust the permissioned infrastructure for both availability and censorship resistance.

### Threat model

**Adversaries and capabilities**

- **Governance / operator set:** Controls membership, transaction ordering, and often key or policy management. Can censor specific users, freeze assets, alter disclosure policies, or degrade service.
- **Identity / credential providers:** Issue and revoke credentials or identities that gate access. Malicious or compromised issuers can grant unauthorized access or silently revoke legitimate users.
- **Infrastructure operators (sequencers, DA providers, custodians):** Depending on the concrete instantiation (e.g., permissioned chain, Validium-like system), these actors may see full plaintext state and can withhold data or selectively serve it.
- **Insiders with privileged visibility:** Compliance teams or auditors with broad viewing rights may intentionally or accidentally leak sensitive information.

**Assets and properties at risk**

- **User funds and access rights:** Governance or operators can freeze, seize, or block transfers, either per policy or maliciously. Users’ ability to transact depends on maintaining good standing in the identity/credential system.
- **Confidential transactional data:** Balances, flows, and identities are typically visible to some subset of privileged actors (operators, auditors, regulators). Misuse or leakage of this data is a central risk.
- **Policy correctness and non-discrimination:** Errors or bias in policies or their enforcement can lead to arbitrary or unfair restrictions on users.

**High-level threats and mitigations**

- **Arbitrary censorship or asset freezes:**  
  In many deployments, this is an explicit feature (e.g., regulator-initiated freezes). Governance structures, legal oversight, and transparent policy definitions are the main mitigations, not cryptographic ones.

- **Data misuse and insider threats:**  
  Privileged access to rich transactional data creates strong incentives for abuse or exfiltration. Role-based access control, audit logs, HSMs, and strict operational procedures mitigate but do not eliminate this risk.

- **Data withholding / operator failure (when built on off-chain DA):**  
  If the underlying mechanism uses off-chain DA (e.g., Validium-like deployments), users may not be able to reconstruct state or exit without cooperation from operators or committees. Redundant providers and contractual obligations help, but the trust remains institutional rather than purely cryptographic.

Because **Permissioned Privacy** systems are explicitly designed around **governed membership and structured selective disclosure**, they typically sit toward the **heavier-trust side** of the **DA/trust axis**: users must trust operators, committees, and identity frameworks for both availability and policy enforcement. This is reflected in a **Trust Assumptions score of 2** in the comparative evaluation: stronger institutional guarantees than ad hoc systems, but significantly more trust in centralized or consortium actors than fully L1-backed patterns.


---

## 5. **Private Rollups (Full DA)**


Private rollups (full DA) shift private transfers into a **separate state machine** that executes off‑chain but posts both **transaction data and validity proofs** to Ethereum. This means users enjoy **strong privacy at the transaction level** while inheriting **L1-grade data availability and verifiability**: anyone can reconstruct the rollup state from on-chain data, and zk proofs ensure correctness.

By batching transactions and proofs, private rollups can achieve **higher throughput and lower amortized L1 cost per transfer** than L1-native shielded pools, while also supporting **more expressive private logic** (e.g., private DeFi or application-specific private contracts). Trade-offs include **increased complexity**, reliance on specialized prover infrastructure, and **UX friction** around notes, keys, and bridging flows. Membership can be open or permissioned, and selective disclosure ranges from none to protocol-level SD, depending on the specific design. Representative systems in this family include Aztec-like, Nightfall-like, and other zk rollup–based private transfer solutions.

#### **One-sentence definition**

A pattern where private execution occurs inside a rollup with full data availability on L1.

#### **Mechanism summary**

- Private state transitions proven by zk-proofs.
- Full DA ensures reconstructability.
- Operators batch private transactions.
- L1 consensus ensures state recoverability.

#### **What problem it solves**

- High-throughput private execution with strong L1 guarantees.

#### **Key strengths**

- Full DA + privacy.
- Supports private smart contracts.
- Strong sovereignty.

#### **Key limitations**

- High L1 footprint.
- Proof generation cost.
- Users must manage private rollup state.

#### **When to use**

- When recoverability is essential.
- When strong L1 guarantees are required.

#### **What it is NOT**

- Not a Validium.
- Not an overlay.
#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Private Rollups (Full DA) maintain a separate private state machine but post both **transaction data** and **validity proofs** to Ethereum L1. L1 therefore has all the information needed to reconstruct the rollup state and enforce correctness, even if all off-chain operators misbehave or disappear.

- **Cross-cutting axes:** The pattern is **membership-agnostic**: deployments can be fully **open** or **permissioned**, which we treat as attributes rather than distinct mechanisms. Default **visibility** is that balances and flows inside the rollup are hidden from the public chain, and many deployments aim for **protocol-level selective disclosure** (e.g., viewing keys or structured proofs) for auditors and institutions.

- **DA/trust axis → Trust Assumptions:** Because all necessary data is available on L1 and exits can be enforced via proofs and forced transactions, Private Rollups sit near the **trust-minimized / full-DA** end of the DA/trust axis, while still relying on sequencers for liveness and UX. In the master comparison table (§5.2), this is reflected in a **Trust Assumptions** score of **4**, indicating **strong fallback with minor extra trust** beyond Ethereum itself.

### Threat model

**Adversaries and capabilities**

- **Sequencer / rollup operator(s):** Can censor or delay specific transactions, reorder them for MEV extraction, and temporarily halt the rollup. They typically see full plaintext rollup state and flows.
- **Prover(s):** Can attempt to construct proofs for an intended (but unfair) state evolution, but cannot generate a mathematically invalid proof that will be accepted by the L1 verifier contract.
- **On-chain adversary (L1 validators):** Can censor interactions with the rollup contract or cause short-term reorgs, but cannot forge validity proofs or alter the rollup state without a valid proof.

**Assets and properties at risk**

- **User funds safety:** Assets bridged into the rollup are logically controlled by the rollup contract. As long as transaction data and proofs are posted to L1, users can in principle reconstruct state and, via exits or force-inclusion mechanisms, reclaim funds even if sequencers misbehave.
- **Availability and liveness:** A halted or censoring sequencer can delay transaction inclusion and exits, degrading UX and creating periods where users cannot act, even though their funds remain recoverable in principle.
- **Privacy:** External L1 observers only see encrypted or abstracted rollup data, but sequencers and provers usually see full plaintext state unless additional cryptographic measures (e.g., FHE/TEE) are used.

**High-level threats and mitigations**

- **Invalid state updates:** Mitigated by zk-validity proofs and on-chain verification. An honest verifier contract on L1 rejects invalid proofs, so operators cannot unilaterally finalize incorrect state transitions.
- **Data withholding before posting to L1:** A sequencer can delay or refuse to post batches, temporarily preventing users from exiting. Many designs mitigate this via timeouts, escape hatches, or permissionless sequencing paths that let users force data onto L1.
- **Censorship and unfair ordering:** Not prevented by validity proofs. Decentralized sequencer sets, explicit sequencing rules, or alternative inclusion paths can reduce but not eliminate these risks.

Because **all transaction data and proofs are ultimately posted to L1**, Private Rollups (Full DA) sit near the **trust‑minimized / full‑DA end** of the **DA/trust design axis**. Users do not rely on an external DA committee for long-term safety, but they still depend on sequencers for liveness and short-term censorship resistance. This is why the pattern receives a **Trust Assumptions** score of **4** in the comparative evaluation.


---

## 6. **Private Plasma**

Private Plasma patterns combine **off-chain private execution** with **periodic commitments of state roots to L1**, protected by **challenge and exit games**. Users (or designated helpers) must maintain enough local data to exit safely if operators misbehave or go offline. Privacy is provided by handling balances and transfers off-chain, often using zk proofs to demonstrate correct updates without revealing details.

The main advantage is **very high throughput and low L1 cost**, since only commitments and occasional proofs touch Ethereum. However, this comes with **exit fragility and operational risk**: if users lose local data or fail to act in time, they may not be able to reclaim funds during disputes. Programmability tends to be more constrained than in full rollups, focusing on payments or narrow function sets. Current deployments are relatively early and heterogeneous, but they share this core profile of **excellent performance, strong privacy, and heightened dependence on operator behavior and user data retention**.

#### **One-sentence definition**

A pattern where private transfers occur inside an off-chain Plasma tree with on-chain exit guarantees but without full data availability.

#### **Mechanism summary**

- Private off-chain state maintained by operator.
- Only commitments posted to L1.
- Exits rely on user-held data.
- Transactions updated via proofs.

#### **What problem it solves**

- High-throughput private transfers with minimal L1 load.

#### **Key strengths**

- Very low L1 footprint.
- Strong privacy in Plasma tree.
- Users can exit if they retain data.

#### **Key limitations**

- Fragile exits if data lost.
- Operator withholding risk.
- Limited programmability.

#### **When to use**

- Data-light private transfers.
- Users prepared to hold their state.

#### **What it is NOT**

- Not a rollup.
- Not a Validium.
#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Private Plasma keeps private balances in an off-chain Plasma tree. Only commitments or aggregated roots (plus limited proofs) are posted to L1; users rely on retaining their own history and using challenge/exit semantics to enforce correctness and withdraw.

- **Cross-cutting axes:** Membership is **deployment-dependent** (open or permissioned), so we treat it as an attribute rather than a distinct mechanism. Default **visibility** is that balances and flows inside the Plasma tree are hidden from L1 observers, with state visible only to participants and operators. Today, most designs provide **no protocol-level selective disclosure** beyond whatever logs or reports operators can generate, which is why the **Selective Disclosure** column in §5.2 scores Private Plasma at **1 (no meaningful SD)**.

- **DA/trust axis → Trust Assumptions:** Because data availability is **not guaranteed on L1** and users must retain local data or depend on honest operators to exit safely, Private Plasma sits in the **middle of the DA/trust axis**: more fragile than full-DA rollups, but with stronger exit guarantees than pure Validium-style DA committees. In the master comparison table (§5.2), this corresponds to a **Trust Assumptions** score of **3**, reflecting **conditional safety with user responsibilities** under the rubric in `Trust Assumptions.md`.

### Threat model

**Adversaries and capabilities**

- **Plasma operator(s):** Can censor transactions, reorder them, withhold off-chain data, and attempt to publish invalid state roots. Operators see all off-chain transaction data (honest-but-curious at best, fully malicious at worst).
- **Data withholding adversary:** The operator or any party controlling the Plasma data store can selectively withhold history from users, making it hard or impossible for them to construct exit proofs.
- **On-chain adversary:** L1 validators / miners can censor Plasma contract interactions or contribute to short-term reorgs, but cannot forge valid Plasma exits or invalidate honest fraud proofs.

**Assets and properties at risk**

- **User funds safety:** Users can lose the practical ability to exit if they fail to retain their own history or if operators strategically withhold data during exit windows.
- **Availability and liveness:** A halting or censoring operator can freeze the system or force mass-exit events, stressing L1 capacity and user monitoring.
- **Privacy:** Off-chain transaction privacy is not protected against the operator; only external observers on L1 are kept from seeing balances and flows.

**High-level threats and mitigations**

- **Invalid state updates:** Mitigated by fraud/exit proofs and challenge periods; an honest user with sufficient data can contest invalid roots and exit safely.
- **Data withholding and targeted censorship:** Partially mitigated by users or watchtowers retaining their own transaction history and actively monitoring the chain; not mitigated for users who lose state or are offline during critical windows.
- **Operator halt / mass-exit scenarios:** Mitigated in principle by exit mechanisms, but in practice constrained by L1 bandwidth and user responsiveness.

These assumptions explain why **Private Plasma** sits in the *middle* of the **DA/trust axis** and receives an intermediate **Trust Assumptions** score: safety is achievable, but only under **user-held data + active monitoring** assumptions rather than purely L1-enforced data availability.



---

## 7. **Private Validium**


Most private Validium systems use **validity proofs for execution correctness** (optimiums are not common), like rollups, but keep **transaction data off-chain** under the control of a DA committee, operator set, or similar infrastructure. This enables **very high throughput and low L1 costs** while still providing strong integrity guarantees for the executed logic.

Because data is not fully available on-chain, users must trust the DA providers not to withhold or censor data; if they do, users generally cannot reconstruct the full state or independently exit. Validium designs often support **rich private programmability**—for example, app-specific private exchanges or more general private VMs—and can be deployed in both open and permissioned modes. Selective disclosure capabilities vary, but many real-world deployments lean toward **better SD and compliance tooling** than purely open systems, especially in institutional or RWA-focused contexts. Representative systems include StarkEx-style deployments and early “Prividium”-style private Validium chains.

#### **One-sentence definition**

A pattern where private execution occurs inside a validity-proven system with off-chain data availability.

#### **Mechanism summary**

- Private state transitions proven by zk-validity proofs.
- Only commitments posted on-chain.
- DA committee ensures data availability.
- High throughput from off-chain execution.

#### **What problem it solves**

- High-throughput private execution with flexible privacy.

#### **Key strengths**

- High scalability.
- Flexible private logic possible.
- Separates DA from validity.

#### **Key limitations**

- Users cannot recover state from L1 alone.
- DA providers introduce trust.
- Sovereignty depends on off-chain data access.


#### **When to use**

- When throughput is top priority.
- Environments accepting DA trust.


#### **What it is NOT**

- Not a rollup.
- Not Plasma.

#### **Design-space position & Trust Assumptions**

- **Mechanism / DA model (primary axis):** Private Validium keeps private execution and state in an off-chain environment, proving correctness with zk-validity proofs while keeping most transaction data off-chain. Ethereum L1 (or another base chain) verifies proofs and commitments, but does not store the data needed to reconstruct the full private state.

- **Cross-cutting axes:** The pattern is **membership-agnostic**: deployments can be **open** or **permissioned**, which we treat as attributes rather than distinct mechanisms. Default **visibility** is that balances and flows are hidden from the base chain, with state visible only to users and DA providers. Many real-world deployments are built around **strong selective disclosure** (e.g., structured reports, auditor views, or policy-driven proofs), which is why the **Selective Disclosure** column in §5.2 scores Private Validium at **4**.

- **DA/trust axis → Trust Assumptions:** Because users **cannot reconstruct state from L1 alone** and must rely on a DA committee or operator set to provide data, Private Validium sits at the **heaviest-trust end** of the DA/trust axis. If the DA committee withholds or loses data, users cannot safely exit or recover balances despite having validity proofs. In the master comparison table (§5.2), this is reflected in a **Trust Assumptions** score of **1**, corresponding to **centralized / DA-committee-heavy DA** under the rubric in `Trust Assumptions.md`.


### Threat model

**Adversaries and capabilities**

- **DA committee / data providers:** Can selectively withhold or delay transaction data, refuse to serve historical state, or serve different histories to different users. They typically see full plaintext state and flows.
- **Validium operator / prover:** Can censor, reorder, or exclude transactions from batches, and attempt to produce proofs for an intended but unfair state (e.g., front‑running or MEV extraction), but cannot generate a *mathematically invalid* proof that passes L1 verification.
- **On-chain adversary (base chain validators):** Can censor Validium contract interactions or cause short‑term reorgs, but cannot forge zk‑validity proofs or bypass the Validium contract’s verification logic.

**Assets and properties at risk**

- **User funds safety:** If the DA committee withholds data or loses it, users may permanently lose the ability to reconstruct the private state and prove ownership, even though commitments and proofs remain on-chain.
- **Availability and liveness:** Operators and DA providers can stall the system, indefinitely delaying new batches or user exits. Users are dependent on them for both day‑to‑day activity and recovery from failures.
- **Privacy:** DA providers and operators usually see full transaction data; privacy primarily protects users against external observers on the base chain, not against these core infrastructure actors.

**High-level threats and mitigations**

- **Data withholding / data loss:** There is no fully trustless L1 fallback if the DA committee withholds or loses data. Many deployments mitigate this via multi‑party committees, contractual guarantees, or replication across providers—but these remain *trust‑based* mitigations.
- **Censorship and unfair ordering:** Operators can censor specific users or reorder transactions. Rate‑limits, governance controls, or multi‑operator setups can reduce single‑party power, but censorship resistance is weaker than in full‑DA rollups.
- **State corruption attempts:** zk‑validity proofs and on-chain verification prevent operators from finalizing *invalid* state transitions, but they do not protect against valid yet unfair transitions (e.g., MEV, targeted reverts).

These assumptions explain why **Private Validium** sits at the **heaviest‑trust end** of the **DA/trust axis** and receives a **Trust Assumptions** score of **1** in the comparative evaluation: users cannot recover state from L1 alone and must rely on DA committees and operators for both safety and availability.



---

## Related Mechanisms Not Scored

Several mechanism families are closely related to private transfers but fall outside the seven scored patterns (**L1 Overlays, L1 Shielded Pools, Burn-and-Mint, Permissioned Privacy, Private Rollups, Private Plasma, Private Validium**). These families operate at different layers or provide general private compute.

#### **General private compute / private VMs**

Private smart-contract platforms (FHE-based EVMs, iO schemes) allow arbitrary private computation. Several patterns—**PR, VV, PL**—can be instantiated on top depending on DA model.

#### **TEE-/MPC-based private execution**

Off-chain private logic executed inside TEEs or MPC resembles **PR/VV/PL** semantics with different trust anchors.

#### **Transaction submission & ordering privacy**

Encrypted mempools and orderflow-protection hide routing and ordering, not state representation. Any pattern can sit beneath them.

#### **Identity & credential systems**

zk-credentials and selective-disclosure identity layers integrate with PP but do not define private balances.

#### **Cross-domain & channel-based privacy**

Shielded bridges and channels are Plasma-like or Validium-like transports wrapping one of the seven patterns.

---

## Membership & Visibility as a Cross-Cutting Axis

Real systems vary not only by mechanism but also by _who may join_ and _who may view what_. Membership, identity-binding, and selective disclosure frequently apply across mechanisms.

**Core clarification:**  
**Permissioned Privacy** is retained as a named pattern, but mechanistically, permissioning can be layered atop **SP, PR, PL, VV** without changing the underlying mechanism.

#### **Rules of Thumb**

- **KYC-restricted shielded pool →** SP + permissioned attribute

- **Consortium Validium →** VV + permissioned attribute

- **Open shielded pool →** SP (not PP)

- **Rollup with structured disclosure →** PR + SD attribute


---

## Classification Recipe / Cheat Sheet

#### **Step 1 — Mechanism / DA Model**

- Balances on L1 → **LO / SP / BM**

- Private state + full DA on L1 → **PR**

- Private state + proofs + off-chain DA → **VV**

- Challenge-style exits + user-held data → **PL**


#### **Step 2 — Membership / Visibility**

Mark as **open** or **permissioned**. This is an attribute, not a pattern.

#### **Step 3 — Selective Disclosure / Compliance**

Mark SD level: **none / ad-hoc / protocol-level / rich-policy**.

