
This section provides short, comparable snapshots of the seven **private-transfer patterns** used throughout Phase A. Each snapshot summarizes _what the pattern is_, _how it works at a high level_, and _its characteristic strengths and trade‑offs_, without re-scoring or changing the taxonomy.

Readers who need full technical detail, examples, and references should consult **Appendix A — Pattern Definition Cards**.

---

## 4.1 [[L1 Overlay – Stealth  OTR]]

L1 overlays add **address-level privacy** on top of Ethereum’s existing account model. Instead of changing how state is represented, they route payments through **one-time “stealth” addresses** derived for the recipient, so an observer cannot easily link an incoming payment to the recipient’s main public address. Balances remain standard ERC‑20 or ETH balances on L1; overlays simply change how funds are sent and discovered.

Because overlays inherit Ethereum’s full DA and trust assumptions, they keep **amounts and the sender’s funding address public**, but hide which long‑term account the receiver actually controls. They typically aim for **low added gas cost**, minimal changes to existing wallets and contracts, and **open membership**. Selective disclosure is often handled via **viewing keys or derivation paths** that allow a user to prove or reconstruct their own history for auditors. Representative deployments include systems like Umbra and Fluidkey, which differ mainly in UX and notifier infrastructure.

---

## 4.2 [[L1 Shielded Pools]]

L1 shielded pools move privacy from the addressing layer into the **state model itself**. Users hold encrypted **UTXO/nullifier notes** inside an on-chain pool contract, and prove in zero knowledge that they are spending valid notes and creating new ones without revealing sender, receiver, or amount. The pool lives directly on Ethereum L1, so DA is guaranteed by calldata and state, and correctness is enforced by on-chain proof verification.

This design offers **strong privacy guarantees** at the cost of **heavy per‑transfer proving and verification costs** and **limited throughput**—only a modest number of zk transfers fit in each block. Programmability ranges from simple mixers to more expressive shielded DeFi (e.g., multi‑asset pools). UX is typically more complex than overlays: users must manage notes, relayers, and multiple keys. Membership can be open or permissioned, and **selective disclosure capabilities vary widely** (from no SD to advanced viewing-key or association-set–style proofs). Examples include Tornado-like mixers, Railgun-like systems, Privacy Pools, zkBob, and Panther-style designs.

---

## 4.3 [[Burn-and-Mint Privacy]]

Burn-and-mint systems provide privacy by **breaking the link** between origin and destination across two contexts—often two addresses, pools, or even chains. A user **burns** tokens in one place and later **mints** new tokens elsewhere, supplying a ZK proof that the burn and mint are related and well-formed, without revealing which specific burn funds which mint.

This pattern offers **strong unlinkability** and can be relatively simple conceptually, but most deployments are **early-stage**. Current designs tend to have **non-trivial gas costs** (burn + mint + proof verification) and limited ecosystem maturity compared to shielded pools or rollups. Programmability is typically focused on transfer semantics rather than general-purpose private smart contracts. Membership can be open or permissioned, and selective disclosure is usually minimal or ad-hoc, though richer SD profiles could be layered on in future implementations.

---

## 4.4 [[Permissioned Privacy]]

Permissioned Privacy refers to systems where **controlled membership and compliance-friendly selective disclosure are the primary design drivers**. Transfers occur in an **access‑controlled environment**—for example, tokenization platforms that require KYC or credential checks before users can hold or move assets. Within this environment, transactions may be locally private, but participants can produce structured proofs or disclosures for auditors, regulators, or counterparties as needed.

Mechanistically, Permissioned Privacy deployments can sit on top of **multiple underlying mechanisms** (e.g., L1 tokens, shielded pools, rollups, Validium). In the taxonomy, they are treated as a distinct pattern **only when permissioning and disclosure policy define the system**, not merely as attributes added to an otherwise open pattern. These systems often exhibit **smoother UX after onboarding**, as transfers may look similar to ordinary token transfers, and they tend to support **richer, policy-driven selective disclosure** than most open systems. Membership is explicitly permissioned; SD is typically protocol-level or rich‑policy; trust assumptions depend on both the underlying mechanism and the governance of the permissioning layer.

---

## 4.5 [[Private Rollups (Full DA)]]

Private rollups (full DA) shift private transfers into a **separate state machine** that executes off‑chain but posts both **transaction data and validity proofs** to Ethereum. This means users enjoy **strong privacy at the transaction level** while inheriting **L1-grade data availability and verifiability**: anyone can reconstruct the rollup state from on-chain data, and zk proofs ensure correctness.

By batching transactions and proofs, private rollups can achieve **higher throughput and lower amortized L1 cost per transfer** than L1-native shielded pools, while also supporting **more expressive private logic** (e.g., private DeFi or application-specific private contracts). Trade-offs include **increased complexity**, reliance on specialized prover infrastructure, and **UX friction** around notes, keys, and bridging flows. Membership can be open or permissioned, and selective disclosure ranges from none to protocol-level SD, depending on the specific design. Representative systems in this family include Aztec-like, Nightfall-like, and other zk rollup–based private transfer solutions.

---

## 4.6 [[Private Plasma]]

Private Plasma patterns combine **off-chain private execution** with **periodic commitments of state roots to L1**, protected by **challenge and exit games**. Users (or designated helpers) must maintain enough local data to exit safely if operators misbehave or go offline. Privacy is provided by handling balances and transfers off-chain, often using zk proofs to demonstrate correct updates without revealing details.

The main advantage is **very high throughput and low L1 cost**, since only commitments and occasional proofs touch Ethereum. However, this comes with **exit fragility and operational risk**: if users lose local data or fail to act in time, they may not be able to reclaim funds during disputes. Programmability tends to be more constrained than in full rollups, focusing on payments or narrow function sets. Current deployments are relatively early and heterogeneous, but they share this core profile of **excellent performance, strong privacy, and heightened dependence on operator behavior and user data retention**.

---

## 4.7 [[Private Validium]]

Most private Validium systems use **validity proofs for execution correctness** (optimiums are not common), like rollups, but keep **transaction data off-chain** under the control of a DA committee, operator set, or similar infrastructure. This enables **very high throughput and low L1 costs** while still providing strong integrity guarantees for the executed logic.

Because data is not fully available on-chain, users must trust the DA providers not to withhold or censor data; if they do, users generally cannot reconstruct the full state or independently exit. Validium designs often support **rich private programmability**—for example, app-specific private exchanges or more general private VMs—and can be deployed in both open and permissioned modes. Selective disclosure capabilities vary, but many real-world deployments lean toward **better SD and compliance tooling** than purely open systems, especially in institutional or RWA-focused contexts. Representative systems include StarkEx-style deployments and early “Prividium”-style private Validium chains.

---

### 4.8 How to Use These Snapshots

These snapshots are intended as **navigational summaries**, not exhaustive specifications or rankings. They:

- Anchor each pattern in a **clear mental model**.
- Highlight **characteristic privacy, cost, UX, and trust trade-offs**.
- Provide a bridge between the high-level narrative (Section 1–3) and the quantitative comparison.

In **Section 5**, these same patterns are evaluated using a maturity‑weighted scoring methodology to provide a structured comparative view.