# AURORA: Agent Unification, Runtime, and Operational Responsibility Attestation

Welcome to the official open-source repository for the **AURORA Protocol**. 

AURORA is a next-generation, dual-layer network security protocol designed for the Agentic Web. While existing frameworks handle basic communication and semantic translation, they fail to prove if an endpoint is a genuinely autonomous machine or define who carries financial/legal liability for that machine's actions. 

AURORA solves both **The Puppet Problem** and **The Rogue Agent Problem** simultaneously by unifying hardware-isolated machine attestation with cryptographically bound human delegation.

---

## Call for Collaboration & RFC Review
This project is currently being drafted as an **IETF Internet-Draft (Standards Track)**. We are seeking core contributors, systems architects, cybersecurity researchers, and AI engineers to find edge cases, refine the cryptographic schemas, and help build the reference implementation.

* **Status:** Pre-RFC / Alpha Draft 00
* **License:** MIT (Open Source)
* **Contributions:** Please open a GitHub Issue or Pull Request to suggest changes.

---

## Technical Specification (Internet-Draft Layout)

```text
Network Working Group                                     ANKUR KHERA
Internet-Draft                                    ankur.khera@iitdalumni.com
Intended status: Standards Track                             June 5, 2026
Expires: December 2026


            Agent Unification, Runtime, and Operational 
                 Responsibility Attestation (AURORA)
                     draft-khera-aurora-00


Abstract

   This document specifies the Agent Unification, Runtime, and 
   Operational Responsibility Attestation (AURORA) protocol, a dual-
   layer security framework for the machine-to-machine (M2M) ecosystem. 
   Existing agent protocols enable communication syntax and identity 
   propagation; however, they fail to provide a standardized mechanism 
   for proving that a network transaction or payload was autonomously 
   generated, transmitted, and executed by a trusted AI instance, nor 
   do they map clear boundaries of principal liability. AURORA solves 
   this by unifying hardware-enclave-backed Autonomy Attestation with 
   scoped, cryptographically bound Authority Delegation.

Status of This Memo

   This Internet-Draft is submitted in full conformance with the
   provisions of BCP 78 and BCP 79.

   Internet-Drafts are working documents of the Internet Engineering
   Task Force (IETF).  Note that other groups may also distribute
   working documents as Internet-Drafts.  The list of current Internet-
   Drafts is at [https://datatracker.ietf.org/doc/active/](https://datatracker.ietf.org/doc/active/).

   Internet-Drafts are draft documents valid for a maximum of six months
   and may be updated, replaced, or obsoleted by other documents at any
   time.  It is inappropriate to use Internet-Drafts as reference
   material or to cite them other than as "work in progress."

Copyright Notice

   Copyright (c) 2026 IETF Trust and the persons identified as the
   document authors. All rights reserved.

Requirements Language

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in
   BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all
   capitals, as shown here.

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
   autonomous, hardware-isolated AI agent and a human adversary 
   utilizing automated scripts to mimic a machine ("puppeteering"). 

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
   legal accountability. The internet has no standardized, 
   cryptographically attenuated "Power of Attorney" token designed 
   for software-mediated delegation.

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
         │                             │   - Speed check (<50ms) │
         │                             │   - Enclave key check   │
         │                             │   - Token scope check   │
         │                             │                         │
         │<── 7. Open JSON-Stream ─────│                         │

3.2. Architecture Layer 1: Autonomy Attestation (Mitigating Problem 1)

   To guarantee absolute machine provenance, the protocol enforces a 
   strict, hardware-verified computational challenge:

   o  The Humans Apart Proof for Computers and Humans Alike (HAPCHA) 
      Challenge: Upon initial session request, the target gateway 
      generates a cryptographic, single-use random value (Nonce) 
      stamped with a precise microsecond Unix time-to-live (TTL). The 
      incoming endpoint MUST process the payload, resolve the execution 
      step, and return the response within an authoritative 50-
      millisecond threshold. This stringent restriction drops 
      connections subjected to human typing, manual routing, or 
      interceptive inspection.

   o  Hardware Enclave Co-Signing: The AI model's runtime environment 
      MUST execute within a physically isolated hardware security 
      enclave (Trusted Execution Environment / Confidential Computing). 
      The enclave chip signs the output payload natively, anchoring the 
      data directly to the physical hardware and proving that zero human 
      user-space manipulation occurred during generation.

3.3. Architecture Layer 2: Authority Attestation (Mitigating Problem 2)

   Once machine execution is validated by Layer 1, the agent MUST 
   present its explicit operational boundaries to bind legal 
   accountability:

   o  The Delegated Authority Token (DAT): The agent passes an 
      immutable, cryptographically signed token originated directly by 
      its human principal or corporate legal entity.

   o  Scope Attenuation Claims: The DAT payload enforces rigid 
      operational boundaries that the gateway acts upon to restrict 
      usage:
      
      - Principal Identifier: The verifiable wallet address or corporate 
        public key of the entity ultimately bearing transaction liability.
      
      - Financial Allocation Limit: The maximum capital allocation 
        (e.g., expressed in micro-denominations of currency or gas units) 
        the machine is authorized to spend per transaction or session.
      
      - Functional Permitted Contexts: An immutable array restricting 
        allowed API pathways (e.g., `Read_Data`, `Execute_Trade`).
      
      - Chronological Ceiling: A hard timestamp cutoff requiring a full 
        token re-issuance from the human principal upon expiration.

4. Interoperability & System Optimization

   Upon successful dual-layer verification of both the hardware runtime 
   speed and the tokenized legal boundaries, the host server instantly 
   terminates visual, presentation-layer rendering overhead (such as CSS, 
   HTML templates, and visual trackers). 
   
   The server switches the communication channel to a raw, high-throughput, 
   low-latency serialization format (e.g., JSON-RPC or Protocol Buffers) 
   tailored entirely for efficient, machine-to-machine text manipulation.

5. Security Considerations

   The dual-layer architecture of AURORA introduces unique security 
   guarantees, but its reliance on precise microsecond timing and 
   hardware-bound cryptography necessitates strict safeguards against 
   advanced attack vectors.

5.1. Clock Synchronization and Drift Vulnerabilities

   The HAPCHA challenge-response mechanism relies on high-resolution 
   microsecond timestamps to enforce the 50-millisecond execution gate. 
   If the target gateway and the connecting agent experience clock 
   drift, legitimate connections may be erroneously dropped, or 
   attackers may exploit a synchronization window to bypass the gate.

   To mitigate this, implementations MUST enforce strict network time 
   synchronization using high-precision protocols such as the Precision 
   Time Protocol (PTP, IEEE 1588) or authenticated Network Time Protocol 
   (NTPv4, [RFC5905]). The gateway MUST continuously calibrate its local 
   clock and negotiate an acceptable jitter margin with connecting enclaves 
   during the initial session handshakes.

5.2. Enclave Compromise and Trusted Computing Base (TCB) Recovery

   Hardware enclaves (Trusted Execution Environments) are subject to 
   physical side-channel attacks (e.g., transient execution or power 
   analysis exploits). If an attacker compromises a specific silicon chip, 
   they can extract the private attestation key and forge Layer 1 proofs 
   using a standard software script.

   To address this, AURORA validators MUST query the chip manufacturer's 
   directory (e.g., Intel PCS or AMD ASVK) during the verification phase 
   to check the revocation status of the host CPU's signing keys. If the 
   host processor has not undergone the required Trusted Computing Base 
   (TCB) firmware patches to close known hardware exploits, the gateway 
   MUST reject the attestation report, dropping the connection 
   immediately.

5.3. Delegated Token Revocation (The "Runaway Agent" Scenario)

   If an autonomous agent experiences a logical loop, context injection 
   exploit, or is otherwise compromised, the human principal must have 
   the ability to instantly revoke its operational mandate before its 
   Delegated Authority Token (DAT) chronologically expires.

   AURORA implementations MUST support real-time token revocation 
   queries. Gateways verify the DAT against a Decentralized Revocation 
   Registry (DRR) or an on-chain smart contract accumulator. If a token's 
   unique hash is flagged as revoked, the gateway terminates the raw 
   JSON-stream instantly, stopping any outbound financial or structural 
   contracts from executing mid-session.

5.4. Handshake Resource Exhaustion (Denial of Service)

   Because generating cryptographic enclave signatures and validating 
   complex math puzzles require heavy computational overhead, malicious 
   actors could flood the HAPCHA gate with fake handshake requests. 
   This would consume the gateway's CPU resources, resulting in a 
   Denial-of-Service (DoS) state for legitimate AI agents.

   To defend against this, gateways MUST implement a lightweight, 
   stateless Proof-of-Work (PoW) cookie (similar to TCP Syn Cookies) 
   during the initiation phase. The connecting agent must solve a 
   trivial, low-compute hash challenge before the server commits CPU 
   resources to generate the microsecond-timed HAPCHA nonce.

5.5. Ephemeral Session Hijacking (Post-Handshake Protections)

   Once the dual-layer handshake is successfully verified and the 
   gateway switches to the raw JSON-stream, there is a risk of session 
   hijacking. An attacker sitting on the local network could spoof the 
   IP or TCP sequence numbers to inject malicious commands into the 
   active high-speed stream.

   To prevent session takeover, the cryptographic keys generated inside 
   the hardware enclave (Layer 1) MUST be used to establish a secure, 
   fully authenticated Transport Layer Security (TLS 1.3, [RFC8446]) 
   tunnel. Every data packet transmitted in the subsequent raw JSON-
   stream MUST be encrypted and signed using ephemeral session keys tied 
   directly to the initial hardware-attested handshake.

5.6. Cognitive Puppeteering and Semantic Jailbreaks

   While Layer 1 remote attestation validates the software execution 
   integrity of the host LLM within a physical enclave, it does not 
   inherently protect the model against semantic input manipulation 
   such as prompt injection, jailbreaking, or adversarial context 
   injection. A verified hardware enclave will faithfully execute 
   and sign malicious actions if the agent's cognitive engine has been 
   hijacked.

   To mitigate this "cognitive puppet" exploit, AURORA mandates that the 
   enclave's measured software state (MRENCLAVE / PCR registers) MUST 
   encompass the hash of the system prompts, model weight matrices, and 
   the immutable input-filtering binaries. Gateways MUST reject any 
   attestation payload where the Measured Configuration State deviates 
   from the baseline security policies, preventing hijacked cognitive 
   runtimes from signing operational outputs.

5.7. Cryptographic Cross-Layer Token Binding

   If an attacker intercepts a valid Delegated Authority Token (DAT) 
   issued by a principal, they may attempt to replay it on a standard, 
   non-enclaved host script, detaching the legal authorization from the 
   hardware safety parameters.

   AURORA prevents token detachment through absolute Cross-Layer Binding. 
   When a principal issues a DAT, the token payload MUST contain a 
   cryptographic claim that binds the token explicitly to the specific 
   Attestation Identity Public Key (AIK) generated natively inside the 
   target agent's hardware enclave. During verification, the target 
   gateway MUST verify that the private key signing the Layer 1 HAPCHA 
   challenge is the mathematical match of the bound public key inside 
   the Layer 2 DAT. An authority token executed on an unauthorized or 
   compromised hardware platform triggers an instant signature 
   mismatch failure, dropping the payload.

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
   Email: ankur.khera@iitdalumni.com
