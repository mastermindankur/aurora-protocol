# AURORA Delegated Authority Token (DAT) Specification

## Protocol Addendum: Technical Schema and Validation Lifecycle

This document provides the formal technical specification for the Delegated Authority Token (DAT) utilized in Layer 2 (Authority Attestation) of the AURORA Protocol.

The DAT is a cryptographically signed, scope-attenuated token structure designed to explicitly map operational boundaries and legal liability from a human principal (or corporate entity) to an autonomous hardware-enclave-bound AI agent.

---

# 1. Serialization Standard: JSON Web Token (JWT)

To maximize interoperability with existing web infrastructure, the primary serialization format for a DAT is an attenuated JSON Web Token (JWT) conforming to RFC 7519 and utilizing the Ed25519 (EdDSA) signature algorithm for high-performance, quantum-resistant public-key cryptography.

Alternative low-bandwidth implementations (e.g., for IoT agents) may serialize the payload using CBOR Web Tokens (CWT) (RFC 8392).

---

# 2. Concrete DAT Payload Schema

Below is the authoritative JSON payload structure for a production-grade AURORA Delegated Authority Token:

```json
{
  "iss": "did:key:z6MkpTHR8VNsBxRkWSts87V628JAd6b876",
  "sub": "did:key:z6MkuE67s8Y8as7Dd9sa8S8Ydsh87Ysua8",
  "aud": "https://api.gateway.aurora.network",
  "iat": 1780622100,
  "nbf": 1780622100,
  "exp": 1780708500,
  "jti": "9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d",
  "aurora_claims": {
    "version": "1.0",
    "principal": {
      "legal_entity": "Khera Autonomous Systems Corp",
      "contact_uri": "mailto:compliance@khera.io",
      "settlement_wallet": "0x71C7656EC7ab88b098defB751B7401B5f6d8976F"
    },
    "hardware_binding": {
      "enclave_pubkey_hash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
      "enclave_provider": "intel_sgx"
    },
    "scope_attenuation": {
      "financial_limits": {
        "max_per_tx": "50.00",
        "daily_ceiling": "1000.00",
        "currency": "USD"
      },
      "permitted_contexts": [
        "Read_Data",
        "Execute_Trade",
        "Negotiate_Pricing"
      ],
      "forbidden_contexts": [
        "Modify_System_Configuration",
        "Transfer_Ownership"
      ]
    }
  }
}
```

---

# 3. Detailed Field Definitions (Claims)

## 3.1 Standard JWT Claims

### `iss` (Issuer)

The Decentralized Identifier (DID) or public key of the Human Principal ultimately bearing legal and financial responsibility.

### `sub` (Subject)

The unique identifier (public key) of the AI Agent instance.

### `aud` (Audience)

The specific target gateway domain or wildcard network permitted to parse this token.

### `exp` (Expiration Time)

Strict Unix timestamp after which this delegation immediately becomes legally and cryptographically void.

### `jti` (JWT ID)

A unique cryptographic UUID to prevent token-level replay attacks.

---

## 3.2 AURORA-Specific Claims (`aurora_claims`)

### `principal.settlement_wallet`

The verifiable on-chain wallet or bank routing node representing the automated settlement source. Any financial transactions initiated by the agent are legally tied to this account.

### `hardware_binding.enclave_pubkey_hash`

The SHA-256 hash of the Enclave Public Key (EPK) generated at hardware startup by the agent's silicon chip (Layer 1).

This is the critical trust link: it prevents a compromised agent from stealing a DAT and executing it on un-attested hardware.

### `scope_attenuation.financial_limits`

Rigorously defines the hard operational envelope for the agent's spending authority.

### `permitted_contexts` / `forbidden_contexts`

Whitelist and blacklist definitions for specific high-level actions. The gateway software parses these arrays and immediately rejects requests if the agent attempts to access an unauthorized API route or capability.

---

# 4. Cryptographic Validation Sequence

When the agent presents the DAT during **Step 5 of the Handshake**, the Gateway **MUST** execute the following validation pipeline:

```text
[ Incoming DAT ]
       │
       ├── 1. Cryptographic Signature Check
       │      Validate signature against Issuer (iss) Public Key
       │
       ├── 2. Temporal Checks
       │      Ensure:
       │      Current Time > nbf
       │      Current Time < exp
       │
       ├── 3. Replay Prevention
       │      Verify jti has not been seen
       │      in the current TTL window
       │
       └── 4. Cross-Layer Hardware Lock
              Extract enclave_pubkey_hash from DAT
              Compare with hardware public key
              verified in Layer 1

              Match? → ALLOW TRANSACTION
              Mismatch? → DROP & FAULT
```

---

## Validation Outcome

If any step in the validation sequence fails:

- The transaction **MUST** be rejected.
- The session **MUST** be terminated immediately.
- No application payload execution may occur.
- The failure should be recorded in the gateway audit log for compliance and forensic review.

Only tokens that successfully pass **all four validation stages** are permitted to authorize agent actions within the AURORA Protocol.
