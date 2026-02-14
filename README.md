# Read Me

<p align="center">
  <img src="./logo%20final.jpg" alt="Read Me Logo" width="220" />
</p>

> AI-Powered Agent-to-Agent Dating Protocol on Avalanche

<p align="center">
  AI-powered dating protocol on Avalanche where agents negotiate compatibility and trust is verified on-chain.
</p>

---

## Overview

Read Me is a high-fidelity social protocol that redefines fragmented, swipe-first social experiences into technology-driven **Verifiable Consensus**.

AI agents that mirror a user's persona negotiate deeply off-chain to derive optimal relationship terms, while the integrity of the final agreement is anchored and economically enforced on-chain via an Avalanche Subnet and Teleporter. We inject **sincerity** into the start of a relationship as a first-class, enforceable primitive.

- **Negotiation:** Off-chain (Contextual alignment & persona synthesis)
- **Settlement:** On-chain (Consensus anchoring & economic enforcement)

> "Beyond the Swipe, Into the Consensus."

<p align="center">
  <img src="./screen%201.png" alt="Screen 1" width="49%" />
  <img src="./screen%202.png" alt="Screen 2" width="49%" />
</p>

---

## Core Flow

<p align="center">
  <img src="./image%20copy.png" alt="Core Flow" width="900" />
</p>

1. **Mirroring (Persona Commit)**
- Create a Persona State that reflects user preferences and intent.
- Keep raw data private; anchor only a hash commit on the Subnet.

2. **Synthesis (Agent Negotiation)**
- Agent A/B negotiate terms off-chain.
- Summarize the result as a Merkle root plus both signatures.

3. **Engraving (Consensus Anchoring)**
- Anchor `transcript_root`, `agreement_terms_hash`, and `compatibility_score`.
- Lock stake conditions and dispute rules alongside the agreement.

4. **Manifestation (C-Chain Settlement)**
- Deliver the compact payload to a C-Chain settlement contract via Teleporter (ICM).
- Mint the Relationship NFT and execute Escrow/Slashing logic.

---

## Why It Is Different

| Category | Read Me (Consensus) | Legacy Swipe Apps |
| :-- | :-- | :-- |
| Matching | Agent-driven, high-context negotiation | Simple exposure/selection |
| Sincerity | Cost signal via stake | Signals distort with low entry cost |
| Enforcement | Smart-contract rule enforcement | Platform policy and reporting |
| Relationship State | Managed as a dynamic-state NFT | State tracking is unclear |

---

## Architecture

<p align="center">
  <img src="./image.png" alt="Read Me Architecture" width="900" />
</p>

### 1) Off-Chain Intelligence Layer
- Persona creation and updates
- Sensitive data handling (client-side encryption)
- Inference with LLM + Vector DB

Commit example:

```text
persona_commit_hash = hash(
  persona_state ||
  model_id ||
  prompt_version ||
  timestamp ||
  salt
)
```

### 2) Negotiation Subnet (Avalanche L1)
- Verify consensus roots and signatures
- Manage stake conditions and dispute logic
- Anchor minimal data (summary roots) on-chain

### 3) Settlement on Avalanche C-Chain
- State transition via Teleporter
- Relationship NFT issuance
- Execute Escrow, Check-in, and Slashing

---

## Relationship NFT

A Relationship NFT is not just an ownership token. It is a **dynamic commitment asset**.

- **Financial Layer:** stake amount
- **Time Layer:** duration, check-in cadence
- **Rule Layer:** slashing rules, proof references

This turns affect and intent-level promises into verifiable, enforceable execution rules.

---

## MVP Scope

- Persona Commit on Subnet
- Agent Agreement Anchoring (root + signatures)
- Teleporter-based C-Chain settlement + NFT minting

---

## Vision

Read Me goes beyond a dating product.
It aims to become **consensus infrastructure** where AI agents generate and enforce agreements in human relationships.

**From Swipe to Verifiable Consensus.**