# AURORA: Agent Unification, Runtime, and Operational Responsibility Attestation

Welcome to the official open-source repository for the **AURORA Protocol**.

AURORA is a next-generation, dual-layer network security protocol designed for the Agentic Web. While existing frameworks handle basic communication and semantic translation, they fail to prove if an endpoint is a genuinely autonomous machine or define who carries financial/legal liability for that machine's actions.

AURORA solves both **The Puppet Problem** and **The Rogue Agent Problem** simultaneously by unifying hardware-isolated machine attestation with cryptographically bound human delegation.

---

## ðŸŽ¯ The Core Trust Paradigm

> [!IMPORTANT]
> **The Architectural Mandate:**
> *â€œAn agent should be able to prove its authority, scope, and runtime integrity.â€�*

### What trust decision becomes possible with AURORA that is impossible without it?

In legacy web security, infrastructure can only verify Identity (*Who owns the key?*) or Syntax (*Is this valid JSON?*). It remains fundamentally blind to computational provenance and financial liability.

AURORA enables a completely new paradigm for programmatic trust decisions:

> "A host system can safely allow an unauthenticated, fully autonomous machine to instantly execute high-value financial, data, or legal transactions because the protocol provides math-backed proof that the payload originated inside an un-hijacked hardware enclave, coupled with an immutable token proving exactly which human principal is legally and financially accountable for its real-world outcomes."

### Before vs. After AURORA

| Scenario | Without AURORA (Blind Trust) | With AURORA (Verifiable Trust) |
| :--- | :--- | :--- |
| **High-Value Trades** | If an incoming API request presents a valid key to trade $10,000, a target gateway faces a dangerous blind spot. It cannot prove if a human adversary is puppeteering scripts to spoof a bot, nor can it map legal liability if the agent's software experiences a runtime logical failure. To protect itself, the gateway must drop the connection or enforce high-latency human verification blocks. | The connection is evaluated dynamically at the network edge. The hardware enclave co-signature confirms cryptographically verifiable runtime integrity, and the Delegated Authority Token (DAT) bounds the exact financial liabilities of the human principal. High-value machine commerce can safely transact without human-verification delays, reducing authorization latency from seconds to sub-100ms automated verification. |

---

## ðŸ“¢ Call for Collaboration & RFC Review

This project is currently being drafted as an **IETF Internet-Draft (Standards Track)**. We are seeking core contributors, systems architects, cybersecurity researchers, and AI engineers to find edge cases, refine the cryptographic schemas, and help build the reference implementation.

* **Status:** Pre-RFC / Alpha Draft 00
* **License:** MIT (Open Source)
* **Contributions:** Please open a GitHub Issue or Pull Request to suggest changes.

---

## Technical Specification (Internet-Draft Layout)

```text
Network Working Group                                     ANKUR KHERA
Internet-Draft                                    ankurkhera@iitdalumni.com
Intended status: Standards Track                             June 5, 2026
Expires: December 2026


            Agent Unification, Runtime, and Operational 
                 Responsibility Attestation (AURORA)
                     draft-khera-aurora-00


Abstract

   This document specifies the Agent Unification, Runtime, and 
   Operational Responsibility Attestation (AURORA) protocol, a dual-
   layer security framework for the machine-to-machine (M2M) ecosystem. 
   The core architectural mandate of this protocol is that an agent 
   should be able to prove its authority, scope, and runtime integrity.
   
   Existing agent protocols enable communication syntax and identity 
   propagation; however, they fail to provide a standardized mechanism 
   for proving that a network transaction or payload was autonomously 
   generated, transmitted, and executed by a trusted AI instance, nor 
   do they map clear boundaries of principal liability. AURORA solves 
   this by unifying hardware-enclave-backed Autonomy Attestation with 
   scoped, cryptographically bound Authority Delegation.

Status of This Memo

   This Internet-Draft is submitted in full conformance with the
   provisions of BCP 78 and BCP 79. Internet-Drafts are working 
   documents of the Internet Engineering Task Force (IETF).

Copyright Notice

   Copyright (c) 2026 IETF Trust and the persons identified as the
   document authors. All rights reserved.

1. Introduction

   As autonomous AI agents migrate from isolated testing environments 
   to the public open web, network infrastructure must pivot to support 
   workloads natively optimized for machine execution. While emerging 
   standards address data semantic translation (e.g., Model Context 
   Protocol), they rely entirely on legacy authentication frameworks 
   such as static API keys or human-centric OAuth tokens. 

   AURORA introduces a standardized architecture to secure agentic 
   interactions by requiring parallel proofs of computational 
   provenance and explicit operational mandate.

1.1. Conventions Used

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in
   BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all
   capitals, as shown here.

1.2. Terminology

   This document uses the following terms:

   Agent (or Connecting Agent): An autonomous AI software runtime that
      initiates network connections and executes transactions on behalf
      of a human principal without real-time human intervention.

   Principal: The human individual or corporate legal entity that
      authorizes and bears ultimate legal and financial accountability
      for an agent's actions.

   Target Gateway: The network endpoint or host server that receives
      and validates AURORA protocol handshake payloads before granting
      access to resources or executing transactions.

   Enclave (or Hardware Security Enclave): A physically isolated,
      tamper-resistant execution environment provided by hardware
      (e.g., Intel TDX, AMD SEV-SNP, ARM TrustZone) that generates
      cryptographically verifiable attestation reports.

   Delegated Authority Token (DAT): An immutable, cryptographically
      signed token issued by a human principal that encodes the agent's
      operational scope, financial limits, and expiry.

   Hardware-Anchored Proof Challenge for Autonomous Hosts (HAPCHA): The
      Layer 1 mechanism by which a gateway verifies that a response was
      generated autonomously by a hardware enclave within a defined time
      ceiling, without human-in-the-loop interference.

   Attested Execution Duration (AED): The silicon-measured processing
      delta between nonce ingestion and payload generation, co-signed
      by the enclave chip into the attestation report.

   Puppeteering: An attack where a human adversary injects manual steps
      or latency into a machine-to-machine interaction to manipulate
      the output of an agent while mimicking autonomous execution.

   Trusted Computing Base (TCB): The set of hardware, firmware, and
      software components critical to the security of an enclave. A TCB
      downgrade indicates a known vulnerability in one of these layers.

2. Problem Statements

   The current internet fabric lacks native defenses against two critical 
   structural vulnerabilities introduced by autonomous machine agents: 
   The Puppet Problem and The Rogue Agent Problem.

2.1. Problem Statement 1: The Puppet Problem (Autonomy Vulnerability)

   Current network endpoints cannot differentiate between a genuinely 
   autonomous, hardware-isolated AI agent and a human adversary utilizing 
   automated scripts to mimic a machine ("puppeteering"). 

   Without a mechanism to prove machine execution, systems are exposed 
   to highly advanced Sybil attacks, data interception, and man-in-the-
   loop payload manipulation. Legacy CAPTCHAs stop uncoordinated bots 
   from mimicking humans, but the internet lacks a standardized metric 
   to stop unauthorized humans from injecting latency or manual steps 
   into pure machine-to-machine interactions.

2.2. Problem Statement 2: The Rogue Agent Problem (Authority Vulnerability)

   AI agents operate as dynamic code runtimes capable of planning, 
   invoking tools, and committing financial or computational assets. 
   When a machine endpoint initiates a binding contract, a target server 
   cannot verify under whose ultimate authority or liability the machine 
   is acting. 

   If an agent suffers a logical loop or context injection and executes 
   an unauthorized asset transfer, the receiving server cannot trace 
   legal accountability. The internet has no standardized, cryptographically 
   attenuated "Power of Attorney" token designed for software-mediated 
   delegation.

3. The AURORA Solution: Dual-Layer Protocol Specification

   AURORA addresses both problem vectors simultaneously using a unified, 
   two-key cryptographic handshake. A request is explicitly rejected 
   unless both the Runtime Layer (Layer 1) and the Mandate Layer 
   (Layer 2) are verified concurrently.

3.1. Core Handshake Flow Overview

   The AURORA protocol execution sequence flows as follows:

   Connecting Agent             Target Gateway             Enclave Chip
         |                             |                         |
         |--- 1. Initiate Session ---->|                         |
         |     + DAT attached          |                         |
         |     + aurora-accept:        |                         |
         |       [protobuf, json-rpc,  |                         |
         |        json]  (Sec. 4.1)    |                         |
         |                             |                         |
         |<-- 2. Time-Bound Nonce -----|                         |
         |                                                       |
         |--- 3. Ingest Nonce & Generate Output ---------------->|
         |                                                       |
         |<-- 4. Sign Payload + Attestation Report --------------|
         |                                                       |
         |--- 5. Return: Signed Output + Enclave Report + DAT -->|
         |                             |                         |
         |                             |-- [6a. LAYER 1 CHECK]   |
         |                             |   Autonomy Attestation  |
         |                             |   - AED: timing verify  |
         |                             |   - Enclave key verify  |
         |                             |   - Nonce binding check |
         |                             |   - RTT ceiling check   |
         |                             |                         |
         |                             |-- [6b. LAYER 2 CHECK]   |
         |                             |   Authority Attestation |
         |                             |   - DAT signature valid |
         |                             |   - Principal identity  |
         |                             |   - Scope & spend limit |
         |                             |   - Chronological ceil. |
         |                             |   - Enclave key binding |
         |                             |                         |
         |                   [Both layers PASS?]                 |
         |                        /          \                   |
         |<-- 7a. ACCEPT ---------            ------> 7b. REJECT |
         |    + aurora-content-type:               Layer fault   |
         |      negotiated format      (Sec. 4.2)  + reason code |
         |    (or fallback: json)      (Sec. 4.3)               |
         |                             |                         |

3.2. Architecture Layer 1: Autonomy Attestation (Mitigating Problem 1)

   To guarantee cryptographically verifiable machine provenance, the protocol
   MUST enforce a rigorous, hardware-verified computational speed challenge
   designated the Hardware-Anchored Proof Challenge for Autonomous Hosts
   (HAPCHA). HAPCHA accounts natively for global network variances and is
   composed of three interlocking mechanisms:

   o  Attested Execution Duration (AED): Upon ingesting the gateway's time-
      bound cryptographic Nonce, the agent's Trusted Execution Environment
      (TEE) MUST use its internal, hardware-isolated secure clock to record
      the exact millisecond of nonce ingestion (T_start) and the exact
      millisecond of payload generation completion (T_end).

      The enclave MUST calculate the silicon processing delta:

          Delta_T_exec = T_end - T_start

      The enclave MUST co-sign this processing delta directly into the
      hardware attestation report alongside the output payload.

      The Target Gateway MUST enforce an operator-configured AED ceiling
      (AED_max) and MUST reject any connection where:

          Delta_T_exec > AED_max

      The AED_max value is deployment-specific and MUST be configured by
      the gateway operator based on the agent's declared context window
      size and the measured baseline throughput of the target enclave
      hardware. As a non-normative reference point, a 4K-token inference
      task on current-generation TEE hardware typically completes within
      15-50ms under unloaded conditions. Gateways MUST NOT apply a single
      universal ceiling across all agent types; doing so would generate
      false positives for agents processing large context windows (e.g.,
      128K tokens) or operating on resource-constrained silicon.

   o  Dynamic Round-Trip Time (RTT) Profiling: To prevent relay puppeteering
      attacks (where a remote human solves challenges and proxies them back
      to a local enclave), the gateway MUST measure the connection's actual
      propagation baseline (RTT_base) during the cryptographic handshake.
      The Target Gateway MUST set the per-connection network deadline as:

          RTT_allowed = RTT_base + Delta_T_exec + epsilon

      where epsilon is a configurable jitter tolerance buffer (RECOMMENDED
      default: 10ms) that accounts for sub-millisecond clock drift between
      the agent's TEE hardware clock and the gateway's NTP-synchronized
      clock, as well as transient network queuing variance. Operators MAY
      increase epsilon for high-jitter network paths (e.g., satellite links)
      but SHOULD NOT exceed 50ms to preserve the anti-puppeteering guarantee.

      This formula natively accommodates geographic propagation variances,
      high-latency satellite links (e.g., Starlink), and regional fiber
      congestion without sacrificing security.

   o  Hardware Enclave Co-Signing: The agent's runtime environment MUST
      execute within a physically isolated hardware security enclave (e.g.,
      Intel TDX, AMD SEV-SNP, or ARM TrustZone). The enclave chip MUST
      sign the output payload and attestation report using a key that is
      generated and stored exclusively within the enclave boundary, anchoring
      the data to the physical hardware and proving that zero user-space
      manipulation occurred during generation. Gateways MUST verify the
      enclave signature against the platform's attestation service before
      accepting any payload.

3.3. Architecture Layer 2: Authority Attestation (Mitigating Problem 2)

   Once machine execution is validated by Layer 1, the agent MUST present
   its Delegated Authority Token (DAT) to bind explicit operational scope
   and legal accountability to the session. Gateways MUST reject any
   connection that passes Layer 1 but omits a valid DAT.

   o  The Delegated Authority Token (DAT): The agent MUST transmit an
      immutable, cryptographically signed token originated directly by its
      human principal or corporate legal entity. The DAT MUST be signed
      using the principal's private key and MUST be bound to the agent's
      Enclave Public Key hash to prevent cross-machine token reuse
      (see Section 5.6).

   o  Scope Attenuation Claims: The DAT payload MUST enforce rigid operational
      boundaries that the gateway acts upon to restrict usage:

      * Principal Identifier: The verifiable identity of the entity
         ultimately bearing transaction liability, expressed as one of:
         an X.509 Distinguished Name (DN) bound to a TLS client certificate,
         a corporate public key registered with a recognized Certificate
         Authority (CA), or a decentralized identifier (DID) for deployments
         operating within blockchain-native infrastructure.

      * Financial Allocation Limit: The maximum capital allocation
         (e.g., expressed in micro-denominations of currency or gas units)
         the machine is authorized to spend per transaction or session window.
         Gateways MUST reject transactions that would cause cumulative spend
         to exceed this limit within the session window.

      * Functional Permitted Contexts: An immutable array restricting
         allowed API calls or tool pathways (e.g., Read_Data, Execute_Trade).
         Gateways MUST reject any request invoking a pathway not present
         in this array.

      * Chronological Ceiling: A hard expiry timestamp after which the DAT
         MUST be considered invalid. Gateways MUST reject expired tokens and
         MUST NOT accept token re-use across separate session windows. A new
         DAT MUST be issued by the human principal upon expiration.

ðŸ“˜ **Technical Reference Document:** For a complete breakdown of the Delegated Authority Token payload, cryptographic claims structure, and validation lifecycle, refer to the [Detailed DAT Specification](docs/DAT-SPECIFICATION.md).

4. Interoperability & System Optimization

   Upon successful dual-layer verification, gateways SHOULD switch the
   active session to a machine-optimized serialization format to eliminate
   unnecessary presentation-layer overhead (e.g., CSS rendering hints,
   HTML template wrappers, and visual tracking payloads). This section
   defines the protocol mechanism by which this capability is negotiated.

4.1. Agent Capability Declaration

   During session initiation (Step 1 of the handshake defined in Section
   3.1), the connecting agent MUST include an "aurora-accept" header field
   declaring its supported machine-optimized serialization formats in
   descending order of preference:

       aurora-accept: application/x-protobuf, application/json-rpc, application/json

   Gateways MUST parse this field before initiating the HAPCHA challenge.
   If the field is absent, the gateway MUST assume the client requires
   standard HTTP/HTML responses and MUST NOT attempt a format switch.

4.2. Gateway Format Switch Signal

   Upon completing successful dual-layer verification (Steps 6a and 6b),
   the gateway MUST include an "aurora-content-type" header in the ACCEPT
   response (Step 7a) to signal the negotiated format for all subsequent
   communication within the session:

       aurora-content-type: application/x-protobuf

   The gateway MUST select the highest-preference format from the agent's
   declared "aurora-accept" list that the gateway itself supports. If no
   mutually supported format exists, the gateway MUST fall back to
   standard JSON (application/json) and MUST NOT terminate the session.

4.3. Fallback Behavior

   Gateways that do not implement machine-optimized format switching MUST
   continue to serve standard HTTP responses and MUST NOT penalize or
   reject agents that include the "aurora-accept" header. Format
   optimization is OPTIONAL for gateway implementors; dual-layer security
   verification (Sections 3.2 and 3.3) remains REQUIRED regardless of
   whether format negotiation is supported.

5. Security Considerations

5.1. Network Latency & Clock Drift Mitigation

   The Hardware-Anchored Proof Challenge for Autonomous Hosts (HAPCHA) relies 
   heavily on sub-millisecond precision. On global networks, legitimate 
   connections may fail due to Network Time Protocol (NTP) asymmetry or 
   geographic routing paths. Gateways MUST implement dynamic round-trip time 
   (RTT) profiling as specified in Section 3.2 to prevent false-positive fault 
   generation across satellite, mobile, and inter-continental network segments.

5.2. Trusted Computing Base (TCB) Degradation & Enclave Recovery

   Hardware-level vulnerabilities discovered in legacy architectural enclaves 
   (e.g., side-channel speculation leaks) could compromise local keys. AURORA
   enforces a strict validation requirement matching the TCB security level 
   against real-time hardware status providers. Outdated or unpatched silicon 
   firmware layers MUST trigger an immediate, graceful connection step-down.

5.3. Authority Token Revocation Lifecycle

   A human principal MUST retain out-of-band revocation capabilities to
   invalidate a Delegated Authority Token (DAT) at any time. Concrete
   revocation triggers include:

   o  Unauthorized Scope Breach: The agent invokes an API call or tool
      pathway not listed in the DAT's Functional Permitted Contexts field.

   o  Financial Threshold Violation: Cumulative transaction spend within
      a session window approaches or exceeds the DAT's Financial Allocation
      Limit, triggering a mandatory principal re-authorization.

   o  Enclave Integrity Failure: The hardware enclave reports a Trusted
      Computing Base (TCB) status downgrade or attestation key compromise
      during an active session.

   o  Principal-Initiated Signal: The human principal transmits an explicit
      revocation command via an authenticated out-of-band channel (e.g.,
      a signed revocation payload referencing the DAT's unique identifier).

   Gateways MUST cross-check the DAT identifier against a centralized,
   high-availability revocation index (e.g., a Bloom filter or distributed
   revocation list) before every transaction execution, not only at session
   initiation.

5.4. Replay Attack Vectors on Multi-Gateway Environs

   A compromised network observer could intercept a valid Layer 1 co-signed 
   payload and attempt a parallel execution replay against an alternative gateway
   within the expiration window. To mathematically block this, all gateway 
   session nonces MUST bind cryptographically to the host gatewayâ€™s domain 
   identifier.

5.5. Cognitive Puppeteering Vulnerabilities (Prompt Injection)

   Even if an agent executes securely within hardware enclaves, it remains 
   vulnerable to prompt injection or model alignment jailbreaks that override 
   its reasoning system. In this scenario, the hardware enclave faithfully 
   signs malicious output logic. To mitigate this cross-layer threat, Layer 1 
   MUST implement Semantic Attestation, requiring the enclave to cryptographically 
   measure and append the agent's immutable base system prompt and system parameter 
   hashes directly alongside the payload execution trace.

5.6. Cryptographic Cross-Layer Token Binding

   If a Delegated Authority Token (DAT) is decoupled from its original machine context, 
   an attacker could extract it from memory and pass it to an un-attested machine. 
   AURORA fully neutralizes this attack vector by forcing Layer 2 to cryptographically 
   bind to Layer 1: the human principal signs the DAT explicitly locking it to the 
   SHA-256 hash of the unique Enclave Public Key generated inside the physical chip. 
   The DAT cannot be validated on any other piece of physical silicon.

6. Privacy Considerations

   The AURORA protocol processes and transmits identity-linked data that
   carries significant privacy implications. Implementors MUST account
   for the following:

6.1. Principal Identity Exposure

   The Delegated Authority Token (DAT) contains a Principal Identifier
   (e.g., an X.509 Distinguished Name or corporate public key) that is
   transmitted to the Target Gateway on every session initiation. Gateways
   MUST NOT log or retain raw DAT payloads beyond the minimum duration
   required for transaction verification and audit trail purposes.

6.2. Enclave Attestation Report Linkability

   Hardware attestation reports contain platform-specific identifiers
   (e.g., enclave measurement values) that could be used to fingerprint
   a specific physical device across sessions. Implementations SHOULD
   rotate enclave signing keys at defined intervals to limit long-term
   cross-session correlation of a single agent's hardware identity.

6.3. Financial Metadata Minimization

   The DAT's Financial Allocation Limit field exposes agent spending
   capacity to the Target Gateway. Gateways MUST treat this field as
   confidential commercial data and MUST NOT disclose it to third
   parties outside the scope of the verified transaction.

7. Implementation Status

   This section records the implementation status of the AURORA protocol
   in accordance with [RFC7942].

   As of the date of this Internet-Draft, no production implementations
   of the full AURORA dual-layer handshake exist. The following
   components are under active development:

   o  Reference Gateway Validator: A prototype Target Gateway validator
      implementing Layer 1 (HAPCHA/AED timing checks) and Layer 2 (DAT
      signature and scope verification) is planned as an open-source
      reference implementation. Status: Pre-Alpha.

   o  DAT Issuance Library: A library for human principals to generate,
      sign, and revoke Delegated Authority Tokens is under design.
      Status: Specification phase.

   o  TEE Integration Layer: Adapter libraries for Intel TDX and AMD
      SEV-SNP to produce AURORA-compatible attestation reports are
      planned. Status: Research phase.

   Contributions and early implementations are welcomed via the project
   repository at: https://github.com/mastermindankur/aurora-protocol

8. IANA Considerations

   This document does not currently request any registry actions from 
   IANA. Future revisions defining specific JSON Web Token (JWT) claim 
   registrations for the Delegated Authority Token (DAT) will utilize 
   the parameters established in RFC 7519.

9. References

9.1. Normative References

   [RFC2119]  Bradner, S., "Key words for use in RFCs to Indicate
              Requirement Levels", BCP 14, RFC 2119,
              DOI 10.17487/RFC2119, March 1997,
              [https://www.rfc-editor.org/info/rfc2119](https://www.rfc-editor.org/info/rfc2119).

   [RFC8174]  Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC
              2119 Key Words", BCP 14, RFC 8174,
              DOI 10.17487/RFC8174, May 2017,
              [https://www.rfc-editor.org/info/rfc8174](https://www.rfc-editor.org/info/rfc8174).

   [RFC8446]  Rescorla, E., "The Transport Layer Security (TLS)
              Protocol Version 1.3", RFC 8446,
              DOI 10.17487/RFC8446, August 2018,
              [https://www.rfc-editor.org/info/rfc8446](https://www.rfc-editor.org/info/rfc8446).

9.2. Informative References

   [RFC5905]  Mills, D., Martin, J., Ed., Burbank, J., and W. Kasch,
              "Network Time Protocol Version 4: Protocol and
              Algorithms Specification", RFC 5905,
              DOI 10.17487/RFC5905, June 2010,
              [https://www.rfc-editor.org/info/rfc5905](https://www.rfc-editor.org/info/rfc5905).

Author's Address

   Ankur Khera
   Email: ankurkhera@iitdalumni.com
```
