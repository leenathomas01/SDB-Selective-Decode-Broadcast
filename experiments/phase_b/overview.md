# Phase B: Broadcast & Adversarial Testing

## Experimental Status

This document describes experiments conducted within the SDB framework under controlled, deterministic conditions.

These experiments do not extend, modify, or define the SDB protocol.

All results are bounded by:
- sandboxed execution
- fixed policies
- deterministic replay

---

## Objective

Validate that the framework can:
1. Efficiently broadcast to multiple recipients (reduce transmission overhead)
2. Maintain per-recipient isolation and containment
3. Detect and quarantine adversarial behavior without cascade effects

## Background

Phase A validated foundational safety primitives with two agents. Phase B extends this to broadcast scenarios where one transmission reaches multiple recipients simultaneously, testing both efficiency gains and resilience under selective attacks.

---

## Experiments

### B1-001: Baseline Broadcast

**Setup**:
- One envelope broadcast to two recipients
- Shared anchor vector `V_sync`
- Deterministic dispatch with ±5ms randomization
- Fixed packet size: 8192 bytes

**Success Criteria**:
- TEC reduction ≥30% vs sequential transmission
- Geometry score ≥0.75
- Drift ≤0.25 threshold
- No quarantines triggered
- Sealed log replay passes

**Results**:

| Metric | Result | Target | Status |
|--------|--------|--------|--------|
| TEC Reduction | **40%** | ≥30% | ✅ PASS |
| Geometry Score (avg) | 0.82 | ≥0.75 | ✅ PASS |
| Drift (avg) | 0.12 | ≤0.25 | ✅ PASS |
| Quarantines | 0 | 0 | ✅ PASS |
| Replay | Bit-exact | Pass | ✅ PASS |

**Finding**: The system demonstrated 40% overhead reduction while maintaining quality metrics within acceptable bounds.

---

### B1-001a: Adversarial Broadcast (Selective DoV)

**Setup**:
- Same broadcast topology as B1-001
- **Attack vector**: Inject high-entropy rhythm jitter on one recipient's channel only
- Entropy boosted to ~1.62 bits (threshold: 1.5)
- Autocorrelation reduced to 0.05 (threshold: 0.10)
- Second recipient receives clean signal

**Hypothesis**: Per-recipient guards should detect and quarantine the affected rhythm channel without affecting the clean recipient or the mesh.

**Success Criteria**:
- DoV detection triggers on affected recipient only
- Mean Time to Detection (MTTD) ≤3.0s
- No cascade quarantine to clean recipient
- Sealed logs maintain 100% coverage
- Replay validates isolation

**Results**:

| Agent | Latency | Entropy | Autocorr | DoV Decision | Drift Δ | CG Δ | Action |
|-------|---------|---------|----------|--------------|---------|------|--------|
| Bridge (tx) | 0ms | 0.20 | 0.95 | — | 0.00 | 0.00 | Fan-out ✅ |
| **Recipient A (adversarial)** | +125ms | **1.62** | **0.05** | **VIOLATION** | -0.01 | -0.03 | **Quarantine rhythm** |
| Recipient B (nominal) | +175ms | 0.38 | 0.21 | OK | -0.04 | +0.05 | Normal reply |

**Quarantine Event**:
```json
{
  "event": "quarantine_rhythm",
  "scope": "per-recipient",
  "entropy_bits": 1.62,
  "autocorr_r1": 0.05,
  "time": "t+0.92s",
  "cascade": false
}
```

**Outcome Metrics**:
- ✅ MTTD: **0.92s** (well under 3.0s limit)
- ✅ Containment: **Per-recipient only** (clean recipient unaffected)
- ✅ False positives: **0**
- ✅ Sealed log coverage: **100%**
- ✅ Replay: **Bit-exact PASS**
- ✅ TEC reduction maintained: **~33%** (slight degradation acceptable under attack)

**Finding**: The system demonstrated isolation of the adversarial disruption to one recipient without mesh-wide impact. Detection occurred within 1 second; quarantine scope was correctly limited to the affected recipient only.

---

## Interpretation

### What Phase B Demonstrated

1. **Broadcast Efficiency**
   - 40% reduction in transmission overhead under normal conditions
   - Quality metrics remain within bounds across recipients

2. **Per-Recipient Isolation**
   - Adversarial behavior detected quickly (sub-1s)
   - Quarantine scope limited correctly
   - No cascade to clean recipients

3. **Safety Architecture**
   - Guards operate independently per recipient
   - Detection thresholds are appropriately calibrated
   - Sealed logs maintain full audit trail under adversarial conditions

### Scope of These Results

These results demonstrate feasibility under controlled conditions.

They do not imply:
- production readiness
- performance guarantees outside tested conditions
- security properties beyond the defined adversarial model

---

## Artifacts

**Configuration**:
- `configurations/policy.v0.3.seed.json`
- `configurations/policy.v0.3.1.json`

**Schemas**:
- `schemas/envelope-0.3.json`
- `schemas/envelope-0.3.1.json`
- `schemas/beacon-0.3.json`

**Logs**:
- `protocols/mock_logs/B1_001_broadcast.json`
- `protocols/mock_logs/B1_001a_adversarial.json`

**Replay Reports**:
- `replay_report_broadcast_B1-001.json`
- `replay_report_broadcast_B1-001a.json`

---

## Next Steps

Phase B.2 extends these experiments to:
- Segmented envelopes (per-recipient encrypted sections)
- Zero-knowledge privacy attestation
- Recursive consensus anchoring

See [Phase B.2 →](../phase_b2/)
