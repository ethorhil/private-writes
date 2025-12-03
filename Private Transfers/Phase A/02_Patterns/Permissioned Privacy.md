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