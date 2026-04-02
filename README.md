# Selective Decode Broadcast (SDB)

**Version:** 1.0  
**Status:** Tagged Release — Stabilized Research Artifact  

---

## What this is

SDB is a **communication primitive** for multi-recipient systems where:

- a single broadcast transmission is shared  
- each recipient decodes only its assigned segment  
- all other content remains structurally inaccessible  

It enables:
> **efficiency (broadcast) + containment (isolation) + auditability (replay)**

This repository documents a **phased, sandboxed research system** used to define, validate, and bound this primitive.

---

## Core Idea

Traditional systems impose a trade-off:

- **Unicast** → safe, but inefficient  
- **Broadcast** → efficient, but unsafe  

SDB removes this constraint:

> A single transmission can preserve strict per-recipient isolation without reverting to unicast.

Isolation is enforced **before interpretation**, not after.

---

## Repository Structure

SDB is organized into five layers:

### 1. Concept Layer (`/concepts`)
Defines core primitives and mechanisms:
- Selective decode
- Broadcast vs unicast trade-offs
- Containment models
- Bounded creative synthesis (experimental context)

---

### 2. Validation Layer (`/phases`)
Phased validation of system behavior:
- Phase A — Safety primitives  
- Phase B — Broadcast efficiency and adversarial containment  
- Phase B.2 — Segmented transmission, privacy, recursive anchoring  

Each phase demonstrates properties under controlled conditions.

---

### 3. Execution Layer (`/experiments`)
Reproducible experimental setups:
- Controlled simulations
- Policy-bound configurations
- Deterministic replay artifacts

These do **not define the protocol**.  
They explore behavior within defined constraints.

---

### 4. Constraint Layer (`/protocol`)
Defines boundaries and methodology:
- Protocol scope (what SDB does and does not define)
- Methodology (how validation is conducted)
- Limitations (where results do not generalize)

This layer prevents over-interpretation.

---

### 5. Observation Layer (`/observations`)
Extracted outcomes:
- Validated properties  
- Rejected designs  
- Open questions  

This layer captures what holds, what fails, and what remains unresolved.

---

## Epistemic Contract

This repository enforces the following:

- All claims are **derived from bounded experiments**
- All experiments are:
  - deterministic  
  - policy-constrained  
  - replayable  

- No component implies:
  - production readiness  
  - real-world deployment guarantees  
  - cryptographic completeness  

SDB defines a **communication primitive under controlled conditions**, not a deployed system.

---

## What this repository is

- A structured research artifact  
- A record of phased validation  
- A demonstration of bounded multi-recipient communication  

---

## What this repository is not

- A production protocol  
- A cryptographic specification  
- A networking standard  
- A claim about intelligence, autonomy, or cognition  

---

## Key Properties (Validated)

- Per-recipient decode isolation  
- No cross-segment leakage  
- Broadcast efficiency gains over unicast  
- Localized containment under adversarial conditions  
- Deterministic replay and full auditability  

See `/observations/validated_properties.md` for details.

---

## Relationship to Research Index

SDB belongs to the **Communication & Coordination Primitives** layer.

It complements:

- SMA-SIB — memory isolation  
- PARP — governance under asymmetry  
- Connector OS — coordination layer  

---

## Status

This is a **stabilized research artifact (v1.0)**.

- Core structure is considered complete  
- Validation is bounded and documented  
- Future work may extend experiments without altering the primitive  

---

## Note

SDB defines **how information can be distributed safely**, not what that information means or how it should be used.

---
