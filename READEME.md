# AURORA: Agent Unification, Runtime, and Operational Responsibility Attestation

Welcome to the official open-source repository for the **AURORA Protocol**. 

AURORA is a next-generation, dual-layer network security protocol designed for the Agentic Web. While existing frameworks handle basic communication and semantic translation, they fail to prove if an endpoint is a genuinely autonomous machine or define who carries financial/legal liability for that machine's actions. 

AURORA solves both **The Puppet Problem** and **The Rogue Agent Problem** simultaneously by unifying hardware-isolated machine attestation with cryptographically bound human delegation.

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
         │                             │   - Speed check (<50ms) │
         │                             │   - Enclave key check   │
         │                             │   - Token scope check   │
         │                             │                         │
         │<── 7. Open JSON-Stream ─────│                         │

3.2. Architecture Layer 1: Autonomy Attestation (Mitigating Problem 1)

   To guarantee absolute machine provenance, the protocol enforces a 
   strict, hardware-verified computational challenge:

   o  The Humans Apart Proof for Computers and Humans Alike (HAPCHA) 
      Challenge: Upon initial session request, the target gateway generates 
      a cryptographic, single-use random value (Nonce) stamped with a 
      precise microsecond Unix time-to-live (TTL). The incoming endpoint 
      must process the payload, resolve the execution step, and return the 
      response within an authoritative 50-millisecond threshold. This 
      stringent restriction drops connections subjected to human typing, 
      manual routing, or interceptive inspection.

   o  Hardware Enclave Co-Signing: The AI model's runtime environment 
      must execute within a physically isolated hardware security enclave 
      (Trusted Execution Environment / Confidential Computing). The enclave 
      chip signs the output payload natively, anchoring the data directly 
      to the physical hardware and proving that zero human user-space 
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

4. Interoperability & System Optimization

   Upon successful dual-layer verification of both the hardware runtime 
   speed and the tokenized legal boundaries, the host server instantly 
   terminates visual, presentation-layer rendering overhead (such as CSS, 
   HTML templates, and visual trackers). 
   
   The server switches the communication channel to a raw, high-throughput, 
   low-latency serialization format (e.g., JSON-RPC or Protocol Buffers) 
   tailored entirely for efficient, machine-to-machine text manipulation.

5. Security Considerations

   The combination of the HAPCHA microsecond speed gate and remote hardware 
   attestation effectively shields the connection from Relay and Playback 
   attacks. If a malicious network observer steals a valid hardware token, 
   replaying it outside the initial time-to-live window triggers a system 
   fault, dropping the hijacked traffic before parsing the sensitive 
   authority layer.
```
