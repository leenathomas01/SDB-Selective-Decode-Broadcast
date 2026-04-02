# Overview

## Purpose

This document provides a structured entry into the SDB system.

It explains:
- how the repository is organized  
- how concepts, validation, and experiments relate  
- how to interpret results without overextension  

---

## System Framing

SDB is a **bounded communication primitive** explored through a layered research process.

The repository separates:

- what is defined  
- what is validated  
- how validation is executed  
- what is concluded  
- what remains constrained  

This separation is intentional and enforced.

---

## Layered Structure

### 1. Concept Layer

Defines the core primitives:

- Selective decode  
- Broadcast vs unicast trade-offs  
- Containment models  

These are **definitions**, not results.

They describe what the system is intended to do.

---

### 2. Validation Layer

Phases test the primitive under controlled conditions:

- Phase A — Safety primitives  
- Phase B — Broadcast efficiency and adversarial containment  
- Phase B.2 — Segmented transmission and advanced coordination  

Each phase:
- introduces a specific condition  
- evaluates behavior under that condition  
- records outcomes independently  

Phases do not redefine concepts.  
They demonstrate them.

---

### 3. Execution Layer

Experiments provide the mechanism for validation:

- deterministic configurations  
- policy-constrained environments  
- replayable logs and outputs  

They define:
> how tests are run, not what the system is

Execution artifacts include:
- experiment specifications  
- configuration files  
- shared utilities and metrics  

---

### 4. Constraint Layer

This layer bounds interpretation:

- **Protocol scope** — what SDB defines and excludes  
- **Methodology** — how validation is conducted  
- **Limitations** — where results do not generalize  

This layer prevents:
- over-claiming  
- misinterpretation  
- unintended extension  

---

### 5. Observation Layer

This layer captures outcomes:

- validated properties  
- rejected designs  
- open questions  

It represents:
> what holds, what fails, and what remains unresolved  

Observations are derived from phases and experiments, not assumed.

---

## How to Read This Repository

A typical path:

1. Start with **concepts** to understand definitions  
2. Move to **phases** to see how they are validated  
3. Refer to **experiments** for execution details  
4. Use **observations** to understand outcomes  
5. Consult **constraints** to understand limits  

This order preserves the intended interpretation.

---

## Interpretation Rules

To maintain consistency, the following rules apply:

- Concepts define mechanisms; they do not claim results  
- Phases validate behavior; they do not extend definitions  
- Experiments execute tests; they do not define protocol  
- Observations summarize outcomes; they do not generalize beyond scope  
- Constraints override interpretation when ambiguity exists  

---

## Execution vs Protocol

SDB distinguishes clearly between:

- **Protocol (definition)**  
- **Execution (experimentation)**  

Execution artifacts (e.g., metrics, policies, utilities) are:
- tools for validation  
- not part of the protocol itself  

This distinction is maintained throughout the repository.

---

## Boundaries

All results in this repository are:

- obtained under sandboxed conditions  
- constrained by explicit policies  
- validated through deterministic replay  

They do not imply:
- real-world deployment viability  
- security guarantees beyond defined scope  
- performance outside tested conditions  

---

## Summary

SDB is not presented as a finished system.

It is a **structured investigation into a communication primitive**, where:

- definitions are explicit  
- validation is phased  
- execution is reproducible  
- conclusions are bounded  

The repository is designed to make each of these steps visible and auditable.

---
