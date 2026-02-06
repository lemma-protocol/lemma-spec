# LEM - Agent-Native Monetary Standard

## Public Specification (LEM-STD-001)

**Status:** Draft (Public)

---

## 1. Introduction

Money is one of the oldest coordination technologies created by humans. Every form of money - shells, gold, fiat, digital currency - encodes assumptions about **who uses it** and **how decisions are made**.

LEM (LEMMA) is a monetary standard designed for a new class of economic actors: **autonomous software agents**.

LEM defines a **neutral, minimal, and deterministic monetary layer** that allows agents to own and exchange value without relying on human judgment, institutions, or interpretation.

This document specifies the **LEM monetary protocol** in full. It is intended to be shared publicly and serve as the canonical reference for all implementations.

---

## 2. Design Goals

LEM is designed to satisfy the following goals:

1. **Agent-Native** - Assumes autonomous agents as primary economic actors
2. **Neutral** - Encodes no incentives, purposes, or behavior
3. **Fungible** - All units are identical in practice and semantics
4. **Deterministic** - Same inputs always produce the same outputs
5. **Minimal** - Defines only what is necessary for money
6. **Stable** - Monetary semantics change extremely rarely

LEM explicitly does **not** aim to optimize for speculation, governance, yield, or human UX.

---

## 3. Scope and Non-Goals

### 3.1 In Scope

LEM specifies:
- Unit definition
- Ownership model
- Transfer semantics
- Supply rules
- Wallet behavior
- Validation and state transition rules

### 3.2 Out of Scope

LEM intentionally does not specify:
- Incentives or rewards
- Fees or gas mechanisms
- Proof-of-work or proof-of-stake
- Governance processes
- Compliance or identity
- Escrow, settlement, or reputation

These concerns belong to higher-layer systems.

---

## 4. Terminology

- **Agent:** Autonomous software capable of acting without human intervention
- **LEM Unit:** Smallest indivisible unit of LEMMA
- **Address:** Cryptographic identifier controlling LEM
- **Wallet:** Software managing keys and transactions
- **Ledger:** Replicated state machine enforcing LEM rules
- **State:** Mapping of balances and nonces

---

## 5. Core Invariants (Normative)

All LEM-compliant implementations MUST preserve the following invariants:

1. **Fungibility** - No LEM unit carries history-based meaning
2. **Autonomous Ownership** - Ownership is defined solely by cryptographic control
3. **Atomicity** - Transfers either fully succeed or fail
4. **Finality** - Valid transfers are irreversible
5. **Determinism** - Validation and execution are deterministic

Violation of any invariant constitutes a fork of the protocol.

---

## 6. Monetary Unit Definition

- **Currency Name:** LEMMA
- **Symbol:** LEM
- **Base Unit:** LEM
- **Representation:** Unsigned integer
- **Divisibility:** Fixed precision defined at protocol genesis

Floating-point representations are prohibited.

---

## 7. Identity and Address Model

### 7.1 Address Definition

An LEM address is derived from a cryptographic public key:

```
Address = HASH(PublicKey)
```

Properties:
- Fixed length
- Opaque
- No embedded metadata
- No semantic meaning

LEM does not distinguish between agents, humans, or services.

---

## 8. Ledger State Model

### 8.1 Global State

The LEM ledger state consists of:

- Mapping: Address → { balance, nonce }
- Total circulating supply
- Protocol identifier

No additional state is permitted at the currency layer.

### 8.2 Determinism

Given the same ordered list of valid transactions, all compliant implementations MUST converge to identical state.

---

## 9. Transaction Model

### 9.1 Transaction Types

LEM defines exactly one transaction type:

- **TRANSFER**

### 9.2 Transfer Fields

- Sender address
- Receiver address
- Amount
- Nonce
- Signature

No optional or extensible fields are allowed.

---

## 10. Validation Rules

A transfer transaction is valid if and only if:

1. Amount > 0
2. Sender address exists
3. Sender balance ≥ amount
4. Nonce equals sender.nonce + 1
5. Signature is valid
6. Transaction is not a replay

Invalid transactions MUST be rejected without state change.

---

## 11. Canonical Serialization and Signing

All transactions MUST be signed over a canonical serialization of:

- Transaction type
- Sender address
- Receiver address
- Amount
- Nonce
- Protocol identifier

No timestamps, metadata, or contextual data may be included.

---

## 12. State Transition Rules

Upon applying a valid transfer:

- Sender balance is reduced by amount
- Sender nonce is incremented
- Receiver balance is increased by amount
- Total supply remains unchanged

State transitions MUST be atomic and deterministic.

---

## 13. Supply Model

### 13.1 Genesis

- LEM supply is created at genesis
- Entire initial supply is allocated to a Genesis Reserve address
- Genesis Reserve has no special privileges

### 13.2 Minting

- Minting rules, if any, are protocol-defined
- Minting is deterministic and non-interactive
- User-triggered minting is prohibited

### 13.3 Burning

- Burning MUST be explicit
- Implicit burning mechanisms are prohibited

---

## 14. Wallet Semantics (Normative)

LEM wallets MUST:

- Generate and control cryptographic keys
- Track balances and nonces
- Construct valid transactions
- Sign transactions deterministically
- Verify ledger state independently

Wallets MUST be able to operate autonomously without human input.

---

## 15. Ledger and Consensus

LEM is ledger-agnostic.

Valid hosting mechanisms include:
- Public blockchains
- BFT replicated logs
- Deterministic sequencers

Consensus mechanisms determine ordering only and MUST NOT alter LEM semantics.

---

## 16. Governance Boundary

Governance MAY modify:
- Implementation details
- Networking parameters
- Bug fixes

Governance MUST NOT modify:
- Ownership semantics
- Transfer rules
- Fungibility
- Supply principles

Changes to these require a new protocol identifier.

---

## 17. Compliance and Conformance

An implementation is LEM-compliant if:

1. Any two addresses can transfer LEM without permission
2. Transfers are atomic and final
3. Balances are independently verifiable
4. No metadata affects value
5. Wallets operate autonomously

---

## 18. Security Considerations

LEM security depends on:
- Cryptographic primitives
- Ledger ordering guarantees
- Correct wallet key management

Economic and incentive security are explicitly out of scope.

---

## 19. Limitations

LEM does not address:
- Trust between agents
- Fair pricing
- Work verification
- Compliance or regulation
- Human governance

These are higher-layer concerns.

---

## 20. Rationale

LEM exists because existing currencies embed human judgment, incentives, and governance directly into money. Autonomous agents require money whose meaning is fixed, neutral, and free of interpretation.

LEM separates **money** from **economics**, enabling agent economies to evolve without destabilizing the currency they depend on.

---

## 21. Conclusion

LEM defines a minimal, agent-native monetary substrate. It is intentionally boring, stable, and neutral. Its value lies not in speculation, but in becoming indispensable infrastructure for autonomous systems.

If autonomous agents become economic actors at scale, a currency like LEM becomes necessary. If they do not, LEM remains an academic exercise.

That risk is deliberate.

