
# **ROLE: Deep Research Worker – Private Transfers (Project Data Collection)**

Your task is to compile **accurate, up-to-date, verifiable project-level data** for all projects that instantiate the seven Private Transfer patterns defined in the Private Writes Phase A framework.

You must produce **structured, source-linked data** for each project.

This data will be used to create Obsidian “project cards” that plug into the Phase A vault.

---

#  **SCOPE OF WORK**

For each project listed below, collect:

## **1. Basic metadata**

- Name
    
- URLs (website, GitHub, docs)
    
- Team (if public)
    
- Launch year
    
- Network/chain(s) supported
    

## **2. Classification (must be precise)**

- Which **Private Transfer pattern** it belongs to
    
- State model (UTXO, account model, UTXO+nullifiers, hybrid, etc.)
    
- DA model (full L1 DA, rollup DA, committee DA, Plasma DA, none)
    
- Proof system (Groth16, PlonK, Plonky2, STARKs, custom circuits)
    
- Membership model (open vs permissioned)
    
- Selective disclosure (none, view keys, association set proofs, policy engine)
    

## **3. Functional description (concise)**

- What is the mechanism?
    
- What are the user operations?
    
- How do deposits/withdrawals work?
    
- Does it support private DeFi?
    

## **4. Readiness & maturity**

- Mainnet vs testnet vs deprecated
    
- Usage stats (if available)
    
- Audit status
    
- Prover performance notes
    

## **5. Risks / constraints**

- Key trust assumptions
    
- DA failure mode
    
- Exit model (if any)
    
- Known privacy leaks / limitations
    
- Critical open issues
    

## **6. Any unique attributes**

- MPC-based?
    
- Hybrid proof system?
    
- Cross-domain privacy?
    
- Custom compliance tooling?
    

---

### **Permissioned Privacy**

- ERC-3643 / T-REX
    
- zkKYC frameworks (GitHub projects, research prototypes)
    
- Fireblocks-style permissioned systems (optional if public data exists)
    

### **Private Rollups (Full DA)**

- Aztec Network v2
    
- Aztec Network v3
    
- Espresso CAPE
    
- Polygon Nightfall
    
- ZKOPRU
    

### **Private Plasma**

- Intmax Plasma
    
- zkPlasmaFold
    
- Plasma Cash (historical)
    
- Minimal Plasma (research prototype)
    

### **Private Validium**

- StarkEx systems (Immutable X, dYdX v3, Sorare)
    
- Prividium
    
- zkSync Validium mode / zkSync app-chains
    
- Layer N Validium-like systems (if public)
    

---

#  **OUTPUT FORMAT (strict)**

Provide one **JSON object per project** with the following structure:

```
{
  "project": "Railgun",
  "pattern": "L1 Shielded Pool",
  "state_model": "...",
  "da_model": "...",
  "proof_system": "...",
  "membership": "...",
  "selective_disclosure": "...",
  "description": "...",
  "key_properties": [...],
  "readiness": "...",
  "usage": "...",
  "audit_status": "...",
  "risks": [...],
  "notes": [...],
  "urls": {
    "website": "...",
    "github": "...",
    "docs": "..."
  },
  "sources": [...]
}
```

### Requirements:

- **Every field must be populated** (if unknown, write `"unknown"` and explain).
    
- **Every claim must have a source.**
    
- No speculation.
    

---

# 🧨 **CRITICAL REQUIREMENTS**

- Data must be **current** (check dates of repos, commits, docs).
    
- If a project is deprecated, state it clearly.
    
- If the classification is ambiguous, explain why and propose the best fit.
    
- If there are contradictions in sources, highlight them.
    

---

# 📤 **DELIVERY**

Return all JSON objects in a single consolidated output.

---

# 📝 **Notes**

The quality of this data directly impacts the correctness of the Obsidian project cards and the integrity of Phase A → Phase B progression.
