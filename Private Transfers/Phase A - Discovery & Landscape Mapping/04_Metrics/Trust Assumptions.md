Strength of security guarantees against data withholding, censorship, and operator misbehavior:
from fully trust-minimized (L1-equivalent) to DA-committee- or operator-heavy patterns.

### Relation to the DA/trust design axis

In the Phase A taxonomy (§3.1–§3.2), the **DA/trust axis** describes where transaction data resides, who can reconstruct the private state, and what users must assume about operators or DA committees to remain safe. The **Trust Assumptions** metric is the numeric expression of that axis in the comparative evaluation table: higher scores mean “closer to L1-equivalent, trust-minimized safety,” while lower scores mean “heavier reliance on off-chain actors for data availability and censorship resistance.”

When scoring a pattern on this metric, we deliberately hold **membership**, **visibility**, and **selective disclosure** constant. Trust Assumptions focuses only on the _additional_ trust surface introduced by the mechanism and DA model beyond Ethereum L1 itself.

A useful way to interpret the 1–5 rubric is:

- **5 — L1-equivalent trust minimization**  
  All data required to reconstruct the private state is permanently available on L1 (or an equally decentralized DA layer with L1-enforced guarantees). Even if all off-chain operators disappear or turn malicious, an honest user can still recover or safely exit using L1 alone.

- **4 — Strong fallback, minor extra trust**  
  Sequencers or operators are required for liveness, but data and exit proofs are still anchored on L1 in a way that prevents catastrophic loss. Malicious or censored operators can be bypassed by honest users using challenge, exit, or force-transaction mechanisms, albeit with some UX or latency cost.

- **3 — Conditional safety, user responsibilities**  
  Safety depends on users or watchtowers retaining local data or monitoring the system, and on some off-chain parties remaining honest. Well-prepared users can usually exit or recover, but large-scale operator failures or targeted data withholding can harm unprepared users.

- **2 — Heavy DA / operator trust**  
  One or more operators or DA committees control access to the data needed to reconstruct the state. Misbehavior or collusion among these actors can cause partial or systemic loss of funds or state, and there is no fully trustless fallback if the entire group withholds data.

- **1 — Centralized DA / opaque state**  
  A single or extremely concentrated operator effectively controls data availability. Users cannot reconstruct the state or exit to safety without this operator; the system behaves like a private sidechain in terms of availability and trust.