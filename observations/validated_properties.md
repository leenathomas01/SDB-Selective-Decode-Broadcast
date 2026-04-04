# Validated Properties

## Scope

This document summarizes properties that were **empirically validated** through phased experiments in this repository.

These are not theoretical claims.  
They held consistently under:
- bounded conditions  
- deterministic execution  
- replay validation  

---

## 1. Per-Recipient Decode Isolation

**Validated in:** Phase B.2

- Each recipient decoded only its assigned segment  
- Non-target decoding attempts failed deterministically  
- No cross-segment leakage observed  

**Conclusion:**  
Selective decode isolation is structurally enforceable.

---

## 2. Broadcast Efficiency with Containment

**Validated in:** Phase B.1, Phase B.2

- Single transmission replaced multiple unicasts  
- ~50% reduction in transmission cost observed  
- No increase in drift or misinterpretation  

**Conclusion:**  
Efficiency and containment can coexist.

---

## 3. Localized Failure and Quarantine

**Validated in:** Phase B.1a

- Adversarial inputs triggered local quarantine only  
- No cascade effects across recipients  
- Other recipients continued normal operation  

**Conclusion:**  
Structural containment localizes failure deterministically.

---

## 4. Diagnostic Redundancy

**Validated in:** Phase A, Phase B.2

- Independent diagnostics converged within tolerance bounds  
- No single diagnostic source was authoritative  

**Conclusion:**  
Redundant diagnostics improve robustness and auditability.

---

## 5. Bounded Recursive Stabilization

**Validated in:** Phase B.2

- Consensus anchoring reduced drift  
- Anchor fidelity improved  
- No runaway behavior observed  

**Conclusion:**  
Recursive stabilization can be bounded and reversible.

---

## 6. Replayability and Auditability

**Validated in:** All Phases

- All runs were deterministic and replayable  
- Logs supported full reconstruction of behavior  

**Conclusion:**  
The system supports reproducible experimentation.

---

## Summary

The following properties are considered **validated within scope**:

- Selective decode isolation  
- Efficient broadcast with containment  
- Localized quarantine  
- Diagnostic redundancy  
- Bounded recursive stabilization  
- Deterministic replay  

No claims beyond these properties are made.
