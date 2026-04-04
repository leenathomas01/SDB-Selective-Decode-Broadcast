# Rejected Designs

## Purpose

This document records design approaches that were:
- considered during exploration,
- explicitly tested or reasoned about,
- and deliberately rejected.

Recording rejected designs prevents future reintroduction of known failure modes.

---

## 1. Trust-Based Broadcast Decoding

### Description
Allowing recipients to:
- receive the full broadcast,
- but “agree” to decode only their part.

### Reason for Rejection
- Relies on behavioral compliance.
- Impossible to audit.
- Unsafe under adversarial conditions.

Conclusion:
> Trust-based containment is insufficient.

---

## 2. Shared Grammar with Post-Hoc Filtering

### Description
Using:
- a common grammar for all recipients,
- followed by filtering or role-based interpretation.

### Reason for Rejection
- Allows partial interpretation of non-target content.
- Enables inference through grammar structure.
- Breaks isolation guarantees.

Conclusion:
> Filtering after decode is too late.

---

## 3. Global Halt on Anomaly

### Description
Triggering:
- full system halt when any recipient detects an issue.

### Reason for Rejection
- Overly fragile.
- Allows one faulty or adversarial segment to disrupt all participants.
- Poor scalability.

Conclusion:
> Global halts do not scale in multi-recipient systems.

---

## 4. Unbounded Recursive Updates

### Description
Allowing recursive consensus updates without:
- entropy weighting,
- drift thresholds,
- or convergence checks.

### Reason for Rejection
- Risk of oscillation or runaway behavior.
- Difficult to reason about stability.
- Hard to audit post-facto.

Conclusion:
> Recursive mechanisms must be bounded and observable.

---

## 5. Heuristic or Model-Based Safety Filters

### Description
Relying on:
- learned anomaly detection,
- heuristic suppression of unsafe behavior.

### Reason for Rejection
- Non-deterministic behavior.
- Difficult to reproduce.
- Unclear failure modes.

Conclusion:
> Structural guarantees are preferred over heuristic ones.

---

## 6. Fully Shared State Between Recipients

### Description
Allowing recipients to:
- influence shared mutable state during decode or validation.

### Reason for Rejection
- Enables indirect coupling.
- Creates hidden channels.
- Violates containment assumptions.

Conclusion:
> Shared mutable state undermines isolation.

---

## Summary

The protocol intentionally rejects:
- trust-based decoding,
- post-hoc containment,
- global halts,
- unbounded recursion,
- heuristic-only safety,
- and shared mutable state.

These rejections are as important as the accepted designs.
