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