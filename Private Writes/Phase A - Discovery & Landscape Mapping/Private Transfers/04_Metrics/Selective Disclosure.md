Quality and richness of mechanisms for revealing information selectively to auditors, regulators, or counterparties.

### Relation to the selective disclosure design axis

In the Phase A taxonomy (§3.2), the **selective disclosure axis** describes how and how well systems can reveal specific views of private state to particular parties (auditors, compliance teams, counterparties, regulators). We distinguish between **no SD**, **ad‑hoc SD**, **protocol-level SD**, and **rich-policy SD**.

The **Selective Disclosure** metric is the numeric expression of this axis in the comparison table (§5.2). It does not measure privacy strength per se; instead, it captures how structured, robust, and policy-aware a pattern’s disclosure mechanisms are, assuming its underlying privacy model.

A useful way to interpret the 1–5 rubric is:

- **5 — Rich‑policy SD**  
  Fine‑grained, protocol-level SD with expressive, machine-readable policies (e.g., role-based views, per-transaction proofs-of-innocence, revocable and time-bounded access). Tooling and APIs make it practical for auditors and institutions to consume these disclosures at scale.

- **4 — Strong protocol-level SD**  
  Protocol-level viewing keys or proofs that support recurring audits and counterparty checks, with reasonable control over scope (what is revealed) and audience (to whom). Some policy concepts are encoded, even if not fully general.

- **3 — Basic protocol-level SD**  
  Built-in viewing keys or standardized proofs that let specific parties see balances or flows, but with limited policy expressiveness (e.g., “reveal everything to this auditor,” rather than fine-grained controls).

- **2 — Ad-hoc SD**  
  Disclosures are possible but not standardized: operators or users can construct custom reports or proofs, or share raw logs, but there is no common protocol-level mechanism or schema.

- **1 — No meaningful SD**  
  The system provides no structured way to selectively disclose private state. Auditors or regulators must rely on off-chain attestations, heuristics, or external data, and cannot obtain protocol-backed views.

Membership and visibility (open vs permissioned, who can see what by default) interact with this axis but are tracked as separate **attributes** in the taxonomy. The Selective Disclosure metric focuses specifically on the **quality of SD mechanisms**, not on who is allowed to receive disclosures in a given deployment.

