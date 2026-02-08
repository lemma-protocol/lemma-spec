# LEMMA / LEM  
### Agent-Native Monetary Standard

LEMMA defines a **neutral, deterministic, agent-native monetary standard**.

- **LEMMA** is the formal protocol specification  
- **LEM** is the unit of value defined by the protocol  

LEMMA exists to answer a single question:

> How can autonomous software agents exchange value  
> without human judgment, incentives, or governance embedded in money itself?

This repository contains the **canonical public specification** for LEMMA.

---

## What this is

LEMMA is:

- A **monetary specification**, not a product
- A **currency definition**, not a speculative asset
- **Infrastructure for autonomous agents**, not human-centric finance

LEMMA defines only what is strictly necessary for money:
- Ownership via cryptographic control
- Fungible units
- Deterministic transfer semantics
- Ledger-agnostic validation

Everything else is intentionally excluded.

---

## What this is not

LEMMA does **not** define or optimize for:

- Token price, valuation, or speculation
- Incentives, rewards, or yield
- Fees or gas mechanisms
- Governance or voting
- Identity, compliance, or regulation
- Business models or ecosystems

Those concerns belong to higher-layer systems built *on top of* money, not inside it.

---

## Specification Status

**Status:** Public v1 Candidate (Request for Technical Review)

The core monetary semantics are considered **stable**.

Feedback at this stage should focus on:
- Correctness
- Determinism
- Completeness
- Edge cases
- Implementability

Changes that alter monetary meaning will require a new protocol version.

---

## How to read this repository

Start here:

- `LEM-STD-001.md`  
  The complete LEMMA monetary standard, including:
  - Normative rules
  - Protocol versioning
  - Agent assumptions
  - Reference wallet behavior
  - Canonical state transition examples

Appendices are non-normative but important for correct implementation.

---

## What feedback is useful

We welcome rigorous critique on:

- Monetary invariants and failure modes
- Deterministic execution guarantees
- Protocol versioning boundaries
- Wallet and nonce semantics
- Ledger-agnostic correctness

Concrete examples, counterexamples, and implementation concerns are especially valuable.

---

## What feedback is out of scope

We are not debating:

- Whether money *should* include incentives
- Alternative governance models
- Human UX considerations
- Ecosystem roadmaps
- Market adoption strategy

Those discussions are orthogonal to the goals of this specification.

---

## How to participate

- Read `LEM-STD-001.md` fully
- Open a GitHub Issue for questions or critique
- Propose changes via Pull Request with clear rationale

Disagreement is expected.
If you believe something is wrong, explain precisely **where and why**.

---

## License

LEMMA is licensed under the  
**Creative Commons Attribution 4.0 International (CC BY 4.0)**.
