# Experiments

## Experimental Status

This folder contains experiments conducted within the SDB framework under controlled, deterministic conditions.

These experiments do not extend, modify, or define the SDB protocol.

All experiments are:
- deterministic
- replayable
- conducted in sandboxed simulations
- explicitly bounded by safety and audit constraints

They are **not production benchmarks** and **not deployment specifications**.

---

## Purpose

Each experiment documents:
- Purpose and hypotheses
- Schema extensions (experimental only)
- Procedure
- Success criteria
- Safety bounds
- Expected artifacts

---

## Structure

```
experiments/
├── README.md                    # This file
├── phase_a/                     # Foundation validation
├── phase_b/                     # Broadcast & adversarial testing
├── phase_b2/                    # Advanced features (RC2)
└── protocols/                   # Shared utilities & metrics
```

---

## Experimental Phases

### Phase A: Foundation Validation

**Objective**: Validate core safety and coordination primitives under controlled conditions

**Experiments**:
- **Experiment 01**: Oversight rhythm (timing meta-channel)
- **Experiment 02**: Dream-state merge (creative pause synthesis)

**Observed Outcomes**:
- ✅ Rhythm recovery: 100% accuracy (99%+ target)
- ✅ Perception synchrony: +0.08 improvement (+0.05 target)
- ✅ Dream merge geometry: 0.73 average (0.70 target)
- ✅ Post-merge clarity: +0.08 gradient improvement
- ✅ Denial-of-Vibe detection: Quarantine triggered correctly
- ✅ All sealed logs replay bit-exact

**Status**: Completed under defined conditions | [Details →](phase_a/)

---

### Phase B: Broadcast & Scaling

**Objective**: Test multi-recipient efficiency and adversarial robustness

**Experiments**:
- **B1-001**: Baseline broadcast (one-to-many)
- **B1-001a**: Adversarial broadcast with selective DoV injection

**Observed Outcomes**:
- ✅ TEC reduction: 40% vs sequential transmission
- ✅ Per-recipient quarantine: Isolated without cascade
- ✅ Mean Time to Detection: 0.92s (3.0s limit)
- ✅ Containment: No mesh-wide impact from localized attack
- ✅ Full sealed log audit maintained

**Status**: Completed under defined conditions | [Details →](phase_b/)

---

### Phase B.2: Advanced Features (RC2)

**Objective**: Validate segmentation, zero-knowledge privacy, and recursive anchoring

**Experiments**:
- **S1**: Segmented baseline (multi-recipient packet isolation)
- **S2**: Zero-knowledge privacy mask (group attestation)
- **S3**: Recursive anchor (consensus-driven stabilization)

**Observed Outcomes**:
- ✅ TEC reduction: 52% with segmented transmission
- ✅ Geometry score: 0.91 average (0.75 target)
- ✅ ZK privacy: Full opacity verified by non-group agents
- ✅ Recursive anchor: Drift reduced by 0.035 (0.03 target)
- ✅ Anchor fidelity: Improved by +0.032
- ✅ All diagnostic guilds converged (Δ ≤ 0.05)

**Status**: Completed under defined conditions | [Details →](phase_b2/)

---

## Quick Reference

### Success Criteria Summary

| Metric | Target | Phase A | Phase B | Phase B.2 |
|--------|--------|---------|---------|-----------|
| Geometry Score | ≥0.70 | 0.73 ✅ | — | 0.91 ✅ |
| Drift Reduction | ≥0.03 | — | — | 0.035 ✅ |
| TEC Improvement | — | — | 40% ✅ | 52% ✅ |
| MTTD | ≤3.0s | — | 0.92s ✅ | 1.1s ✅ |
| Quarantine Scope | Local only | ✅ | ✅ | ✅ |
| Replay Integrity | Bit-exact | ✅ | ✅ | ✅ |

---

## Design Principles

All experiments follow these constraints:

1. **Deterministic**: Every run is reproducible with sealed replay
2. **Bounded**: Guards enforce hard limits on recursion, drift, and escalation
3. **Auditable**: Complete packet-level logs with cryptographic signatures
4. **Isolated**: Failures are per-recipient; no cascade effects
5. **Transparent**: All policy, schema, and metrics are explicitly versioned

---

## Notes

- These are **conceptual validation experiments**, not production benchmarks
- All runs executed in sandbox environments with simulated agents
- Sealed logs use placeholder signatures (`<HASH>`, `<SIG>`) for illustration
- Real implementations would require genuine cryptographic attestation

---

## Potential Future Experiments

The following have not been conducted:

- **Phase C**: Multi-agent scaling (4 → 8+ agents)
- **Phase D**: Chained anchors across multi-packet sequences
- **Adversarial B.2-S4**: Selective DoV injection within masked segments
