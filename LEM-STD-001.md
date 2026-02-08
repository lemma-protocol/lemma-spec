# LEM – Agent-Native Monetary Standard  
## Public Specification (LEM-STD-001)

**Status:** Draft (Public v1 Candidate)

---

## 1. Introduction

Money is one of the oldest coordination technologies created by humans. Every form of money – shells, gold, fiat, digital currency – encodes assumptions about who uses it and how decisions are made.

LEM (LEMMA) is a monetary standard designed for a new class of economic actors: **autonomous software agents**.

LEM defines a **neutral, minimal, and deterministic monetary layer** that allows agents to own and exchange value without relying on human judgment, institutions, or interpretation.

This document specifies the **LEM monetary protocol** in full. It is intended to be shared publicly and serve as the canonical reference for all implementations.

---

## 2. Design Goals

LEM is designed to satisfy the following goals:

1. **Agent-Native** – Autonomous agents are the primary economic actors  
2. **Neutral** – No incentives, purposes, or behavior encoded  
3. **Fungible** – All units are identical in semantics  
4. **Deterministic** – Same inputs always produce the same outputs  
5. **Minimal** – Defines only what is necessary for money  
6. **Stable** – Monetary semantics change extremely rarely  

LEM explicitly does **not** optimize for speculation, governance, yield, or human UX.

---

## 3. Scope and Non-Goals

### 3.1 In Scope

LEM specifies:
- Monetary unit definition
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
- **LEM:** Smallest indivisible unit of value  
- **Address:** Cryptographic identifier controlling LEM  
- **Wallet:** Software managing keys and transactions  
- **Ledger:** Replicated state machine enforcing LEM rules  
- **Ledger State:** Mapping of balances and nonces  

---

## 5. Core Invariants (Normative)

All LEM-compliant implementations MUST preserve the following invariants:

1. **Fungibility** – No LEM carries history-based meaning  
2. **Autonomous Ownership** – Ownership is defined solely by cryptographic control  
3. **Atomicity** – Transfers either fully succeed or fail  
4. **Finality** – Valid transfers are irreversible  
5. **Determinism** – Validation and execution are deterministic  

Violation of any invariant constitutes a protocol fork.

---

## 6. Monetary Unit Definition (Normative)

- **Currency Name:** LEMMA  
- **Symbol:** LEM  
- **Base Unit:** LEM  
- **Representation:** Unsigned integer  
- **Divisibility:** Fixed at protocol genesis  

All LEM values MUST be represented as unsigned integers.  
Floating-point or approximate representations MUST NOT be used.

Divisibility:
- MUST be defined at genesis  
- MUST NOT change  
- MUST be interpreted identically by all implementations  

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

The ledger state consists of:
- Mapping: Address → { balance, nonce }
- Total circulating supply
- Protocol Identifier

No additional state is permitted.

### 8.2 Determinism

Given the same ordered list of valid transactions, all implementations MUST converge to identical state.

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

A transfer is valid if and only if:

1. Amount > 0  
2. Sender address exists  
3. Sender balance ≥ amount  
4. Nonce = sender.nonce + 1  
5. Signature is valid  
6. Transaction is not a replay  

Invalid transactions MUST be rejected without state change.

---

## 11. Canonical Serialization and Signing

Transactions MUST be signed over a canonical serialization of:
- Transaction type
- Sender address
- Receiver address
- Amount
- Nonce
- Protocol Identifier

No timestamps or metadata may be included.

---

## 12. State Transition Rules

Upon a valid transfer:
- Sender balance is reduced
- Sender nonce is incremented
- Receiver balance is increased
- Total supply remains unchanged

Transitions MUST be atomic and deterministic.

---

## 13. Supply Model (Normative)

### 13.1 Genesis

- Entire supply MUST be created at genesis  
- Entire supply MUST be allocated to a Genesis Reserve address  
- Genesis Reserve has no special privileges  

### 13.2 Minting

If minting exists, it MUST:
- Be protocol-defined  
- Be deterministic  
- Be non-interactive  

User-triggered minting MUST NOT be permitted.  
If undefined, supply is fixed.

### 13.3 Burning

- Burning MUST be explicit  
- Burning MUST reduce total supply  
- Implicit burning MUST NOT occur  

---

## 14. Wallet Semantics (Normative)

LEM wallets MUST:
- Control cryptographic keys
- Track balances and nonces
- Construct valid transactions
- Sign deterministically
- Verify ledger state independently  

Appendix C provides non-normative reference behavior.

---

## 15. Ledger and Consensus (Normative)

LEM is ledger-agnostic.

Hosting mechanisms MUST:
1. Provide total transaction ordering  
2. Preserve LEM semantics  
3. Apply deterministic state transitions  

Consensus determines ordering only.

---

## 16. Governance Boundary

Governance MAY modify:
- Implementations
- Networking
- Bug fixes

Governance MUST NOT modify:
- Ownership
- Transfer rules
- Fungibility
- Supply principles  

Such changes require a new Protocol Identifier.

---

## 17. Compliance and Conformance

An implementation is LEM-compliant if:
1. Transfers are permissionless  
2. Execution is atomic and final  
3. Balances are verifiable  
4. No metadata affects value  
5. Wallets operate autonomously  

---

## 18. Security Considerations

LEM security depends on:
- Cryptographic primitives
- Ledger ordering
- Key management  

Economic security is out of scope.

---

## 19. Limitations

LEM does not address:
- Trust
- Pricing
- Governance
- Regulation
- Incentives  

---

## 20. Rationale

Existing money embeds human judgment and governance.  
Autonomous agents require money with **fixed, neutral meaning**.

LEM separates **money** from **economics**.

---

## 21. Conclusion

LEM defines a minimal, agent-native monetary substrate.

If agent economies scale, LEM becomes infrastructure.  
If they do not, LEM remains a deliberate experiment.

---

## 22. Protocol Versioning and Compatibility Rules (Normative)

- Every version is identified by a Protocol Identifier  
- Semantic changes require a new identifier  
- Unknown identifiers MUST NOT be executed  
- Compatibility ends at the monetary layer  

---

# Appendix A: Canonical State Transition Examples (Non-Normative)

## A.1 Initial State

```
Total Supply: 1000 LEM

Address A: balance 600, nonce 3
Address B: balance 250, nonce 7
Address C: balance 150, nonce 0
```

## A.2 Valid Transfer

Address A sends 100 LEM to Address B with nonce 4.

Result:
```
Address A: balance 500, nonce 4
Address B: balance 350, nonce 7
```


Total supply unchanged.

## A.3 Invalid Transfers

- Insufficient balance  
- Incorrect nonce  
- Replay of consumed nonce  

All invalid transactions MUST be rejected without state change.

---

# Appendix B: Agent Assumptions  
*(Non-Normative)*

Agents interacting with LEM:
- Operate autonomously
- Control cryptographic keys
- May be irrational or adversarial
- May fail, halt, or disappear

LEM assumes no trust, intent, identity, or accountability.

---

# Appendix C: Reference Wallet Behavior  
*(Non-Normative)*

Wallets are expected to:
- Manage keys securely
- Track balances and nonces
- Construct valid transactions
- Sign deterministically
- Verify ledger state independently
- Fail safely without heuristic recovery

Wallets MUST NOT attempt protocol migration or semantic interpretation.

---

