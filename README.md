# AURORA: Agent Unification, Runtime, and Operational Responsibility Attestation

Welcome to the official open-source repository for the **AURORA Protocol**.

AURORA is a next-generation, dual-layer network security protocol designed for the Agentic Web. While existing frameworks handle basic communication and semantic translation, they fail to prove if an endpoint is a genuinely autonomous machine or define who carries financial/legal liability for that machine's actions.

AURORA solves both **The Puppet Problem** and **The Rogue Agent Problem** simultaneously by unifying hardware-isolated machine attestation with cryptographically bound human delegation.

---

## 🎯 The Core Trust Paradigm

> [!IMPORTANT]
> **The Architectural Mandate:**
> *“An agent should be able to prove its authority, scope, and runtime integrity.”*

### What trust decision becomes possible with AURORA that is impossible without it?

In legacy web security, infrastructure can only verify Identity (*Who owns the key?*) or Syntax (*Is this valid JSON?*). It remains fundamentally blind to computational provenance and financial liability.

AURORA enables a completely new paradigm for programmatic trust decisions:

> "A host system can safely allow an unauthenticated, fully autonomous machine to instantly execute high-value financial, data, or legal transactions because the protocol provides math-backed proof that the payload originated inside an un-hijacked hardware enclave, coupled with an immutable token proving exactly which human principal is legally and financially accountable for its real-world outcomes."

### Before vs. After AURORA

| Scenario | Without AURORA (Blind Trust) | With AURORA (Verifiable Trust) |
| :--- | :--- | :--- |
| **High-Value Trades** | If an incoming API request presents a valid key to trade $10,000, a target gateway faces a dangerous blind spot. It cannot prove if a human adversary is puppeteering scripts to spoof a bot, nor can it map legal liability if the agent's software experiences a runtime logical failure. To protect itself, the gateway must drop the connection or enforce high-latency human verification blocks. | The connection is evaluated dynamically at the network edge. The hardware enclave co-signature confirms cryptographically verifiable runtime integrity, and the Delegated Authority Token (DAT) bounds the exact financial liabilities of the human principal. High-value machine commerce can safely transact at microsecond speeds. |

---

## 📢 Call for Collaboration & RFC Review

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
         │                             │                         │
         │─── 1. Initiate Session ────>│                         │
         │                             │                         │
         │<── 2. Time-Bound Nonce ─────│                         │
         │                                                       │
         │─── 3. Ingest Nonce & Generate Output ────────────────>│
         │                                                       │
         │<── 4. Sign Payload + Attestation Report ──────────────│
         │                                                       │
         │─── 5. Return Output + Hardware Sign + Authority Token ─>│
         │                             │                         │
         │                             │── [6. Dual Verification]│
         │                             │   - Speed check (AED)   │
         │                             │   - Enclave key check   │
         │                             │   - Token scope check   │
         │                             │                         │
         │<── 7. Open JSON-Stream ─────│                         │

3.2. Architecture Layer 1: Autonomy Attestation (Mitigating Problem 1)

   To guarantee cryptographically verifiable machine provenance, the protocol 
   enforces a rigorous, hardware-verified computational speed challenge that 
   accounts natively for global network variances:

   o  Attested Execution Duration (AED): Upon ingesting the gateway's time-
      bound cryptographic Nonce, the agent's Trusted Execution Environment 
      (TEE) uses its internal, secure hardware-isolated clock to record 
      the exact millisecond of ingestion ($T_{start}$) and the exact 
      millisecond of payload generation ($T_{end}$). 
      
      The enclave calculates the silicon processing delta: 
      
          $\Delta T_{exec} = T_{end} - T_{start}$
      
      The enclave co-signs this processing delta directly into the hardware 
      attestation report. The target gateway enforces a strict ceiling 
      (e.g., $\Delta T_{exec} \le 15\text{ms}$ for standard context evaluation), 
      proving that zero human-in-the-loop interaction or user-space manual 
      redirection occurred during the model's computation.

   o  Dynamic Round-Trip Time (RTT) Profiling: To prevent relay puppeteering 
      attacks (where a remote human solves challenges and proxies them back 
      to a local enclave), the gateway measures the connection’s actual 
      propagation baseline ($RTT_{base}$) during the cryptographic handshake. 
      The target network deadline is set dynamically for each unique connection:
      
          $RTT_{allowed} = RTT_{base} + \Delta T_{exec} + \epsilon$
      
      This formula natively accommodates geographic propagation variances, 
      high-latency satellite links (e.g., Starlink), and regional fiber 
      congestion without sacrificing security.

   o  Hardware Enclave Co-Signing: The AI model's runtime environment 
      must execute within a physically isolated hardware security enclave. 
      The enclave chip signs the output payload natively, anchoring the data 
      directly to the physical hardware and proving that zero human user-space 
      manipulation occurred during generation.

3.3. Architecture Layer 2: Authority Attestation (Mitigating Problem 2)

   Once machine execution is validated by Layer 1, the agent must 
   present its explicit operational boundaries to bind legal accountability:

   o  The Delegated Authority Token (DAT): The agent passes an immutable, 
      cryptographically signed token originated directly by its human 
      principal or corporate legal entity.

   o  Scope Attenuation Claims: The DAT payload enforces rigid operational 
      boundaries that the gateway acts upon to restrict usage:
      
      * Principal Identifier: The verifiable wallet address or corporate 
         public key of the entity ultimately bearing transaction liability.
      
      * Financial Allocation Limit: The maximum capital allocation 
         (e.g., expressed in micro-denominations of currency or gas units) 
         the machine is authorized to spend per transaction or session window.
      
      * Functional Permitted Contexts: An immutable array restricting 
         allowed API calls or tool pathways (e.g., `Read_Data`, `Execute_Trade`).
      
      * Chronological Ceiling: A hard timestamp cutoff requiring a full 
         token re-issuance from the human principal upon expiration.

📘 **Technical Reference Document:** For a complete breakdown of the Delegated Authority Token payload, cryptographic claims structure, and validation lifecycle, refer to the [Detailed DAT Specification](docs/DAT-SPECIFICATION.md).

4. Interoperability & System Optimization

   Upon successful dual-layer verification of both the hardware runtime 
   speed and the tokenized legal boundaries, the host server instantly 
   terminates visual, presentation-layer rendering overhead (such as CSS, 
   HTML templates, and visual trackers). 
   
   The server switches the communication channel to a raw, high-throughput, 
   low-latency serialization format (e.g., JSON-RPC or Protocol Buffers) 
   tailored entirely for efficient, machine-to-machine text manipulation.

5. Security Considerations

5.1. Network Latency & Clock Drift Mitigation

   The HAPCHA challenge relies heavily on sub-millisecond precision. On global
   networks, legitimate connections may fail due to Network Time Protocol (NTP)
   asymmetry or geographic routing paths. Gateways MUST implement dynamic 
   round-trip time (RTT) profiling as specified in Section 3.2 to prevent 
   false-positive fault generation across satellite, mobile, and inter-
   continental network segments.

5.2. Trusted Computing Base (TCB) Degradation & Enclave Recovery

   Hardware-level vulnerabilities discovered in legacy architectural enclaves 
   (e.g., side-channel speculation leaks) could compromise local keys. AURORA
   enforces a strict validation requirement matching the TCB security level 
   against real-time hardware status providers. Outdated or unpatched silicon 
   firmware layers MUST trigger an immediate, graceful connection step-down.

5.3. Authority Token Revocation Lifecycle

   If an autonomous runtime agent begins executing non-optimal code pathways or
   suffers visual/context vulnerabilities, the human principal must retain 
   out-of-band revocation capabilities. Gateways MUST process centralized, high-
   availability Bloom filters or distributed revocation indices to cross-check 
   the Delegated Authority Token's identifier before transaction execution.

5.5. Replay Attack Vectors on Multi-Gateway Environs

   A compromised network observer could intercept a valid Layer 1 co-signed 
   payload and attempt a parallel execution replay against an alternative gateway
   within the expiration window. To mathematically block this, all HAPCHA nonces 
   MUST bind cryptographically to the host gateway’s domain identifier.

5.6. Cognitive Puppeteering Vulnerabilities (Prompt Injection)

   Even if an agent executes securely within hardware enclaves, it remains 
   vulnerable to prompt injection or model alignment jailbreaks that override 
   its reasoning system. In this scenario, the hardware enclave faithfully 
   signs malicious output logic. To mitigate this cross-layer threat, Layer 1 
   MUST implement Semantic Attestation, requiring the enclave to cryptographically 
   measure and append the agent's immutable base system prompt and system parameter 
   hashes directly alongside the payload execution trace.

5.7. Cryptographic Cross-Layer Token Binding

   If a Delegated Authority Token (DAT) is decoupled from its original machine context, 
   an attacker could extract it from memory and pass it to an un-attested machine. 
   AURORA fully neutralizes this attack vector by forcing Layer 2 to cryptographically 
   bind to Layer 1: the human principal signs the DAT explicitly locking it to the 
   SHA-256 hash of the unique Enclave Public Key generated inside the physical chip. 
   The DAT cannot be validated on any other piece of physical silicon.

6. IANA Considerations

   This document does not currently request any registry actions from 
   IANA. Future revisions defining specific JSON Web Token (JWT) claim 
   registrations for the Delegated Authority Token (DAT) will utilize 
   the parameters established in RFC 7519.

7. References

7.1. Normative References

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

7.2. Informative References

   [RFC5905]  Mills, D., Martin, J., Ed., Burbank, J., and W. Kasch,
              "Network Time Protocol Version 4: Protocol and
              Algorithms Specification", RFC 5905,
              DOI 10.17487/RFC5905, June 2010,
              [https://www.rfc-editor.org/info/rfc5905](https://www.rfc-editor.org/info/rfc5905).

Author's Address

   Ankur Khera
   Email: ankurkhera@iitdalumni.com
```
