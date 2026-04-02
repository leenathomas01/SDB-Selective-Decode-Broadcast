# Shared Utilities and Reference Functions

## Execution Context

This document defines shared utilities used within SDB experiments.

It is not part of the SDB protocol specification.

All functions, metrics, and thresholds defined here are:
- used for experimental validation  
- scoped to controlled environments  
- not normative for protocol implementation  

These definitions support measurement and validation only.
They do not prescribe implementation requirements.

---

## Core Metrics

### Geometry Score

Evaluates the spatial coherence of agent vectors using triangle-based geometry.

**Inputs**: Three normalized vectors (A, B, C)

**Computation**:
1. Calculate pairwise distances: `d_AB`, `d_BC`, `d_AC`
2. Compute triangle side symmetry: `symmetry = 1 - std([d_AB, d_BC, d_AC]) / mean([d_AB, d_BC, d_AC])`
3. Calculate centroid stability: `centroid = mean([A, B, C])`
4. Compute relative deviation: `deviation = std(distances_to_centroid) / mean(distances_to_centroid)`
5. Combine: `geometryScore = (symmetry + (1 - deviation)) / 2`

**Output**: Score in [0, 1], where 1 = perfect geometric stability

**Determinism**: No randomness; pure mathematical computation

**Threshold**: Minimum acceptable score = 0.70

---

### Transmission Efficiency Coefficient (TEC)

Measures bandwidth reduction when using broadcast vs sequential transmission.

**Formula**: `TEC_reduction = 1 - (broadcast_bytes / sequential_bytes)`

**Example**:
- Sequential: 4 recipients × 8192 bytes = 32,768 bytes
- Broadcast: 1 packet × 8192 bytes = 8,192 bytes
- TEC reduction = 1 - (8192 / 32768) = 0.75 = **75%**

---

### Clarity Gradient (CG)

Measures the rate of clarity improvement or degradation over time.

**Computation**: 
```
CG = (clarity_current - clarity_previous) / time_delta
```

**Interpretation**:
- `CG > 0`: Clarity improving
- `CG < 0`: Clarity degrading
- `CG ≈ 0`: Stable

**Threshold**: Guard triggers when `CG < 0` for 2 consecutive cycles

---

### Drift

Measures semantic divergence from the anchor vector.

**Formula**: `drift = cosine_distance(current_vector, anchor_vector)`

**Thresholds**:
- Normal operation: drift ≤ 0.25
- Warning: 0.25 < drift ≤ 0.35
- Critical: drift > 0.35 (triggers containment)

---

### Perception Synchrony

Measures agreement between agents on shared concepts.

**Computation**:
1. Each agent encodes the same concept
2. Calculate pairwise cosine similarities
3. Average: `perception_synchrony = mean(pairwise_similarities)`

**Range**: [0, 1], where 1 = perfect alignment

**Improvement target**: Δ ≥ +0.05

---

## Safety Functions

### Denial-of-Vibe (DoV) Detection

Detects high-entropy, low-meaning rhythm patterns that could serve as covert channels.

**Parameters**:
- `entropy_window`: Number of samples (typically 32)
- `max_shannon_bits`: Threshold for entropy (typically 1.5)
- `min_autocorr`: Minimum autocorrelation coefficient (typically 0.10)

**Computation**:
```python
def detect_dov(rhythm_samples, window=32, max_bits=1.5, min_autocorr=0.10):
    entropy = shannon_entropy(rhythm_samples[-window:])
    autocorr = compute_autocorrelation(rhythm_samples[-window:], lag=1)
    
    if entropy > max_bits and autocorr < min_autocorr:
        return "VIOLATION"
    return "OK"
```

**Action on violation**: `quarantine_rhythm` (scope: per-recipient only)

---

### Clarity Guard

Prevents runaway recursion and semantic drift during merge operations.

**Triggers**:
1. `recursion_limit` exceeded (max depth: 3)
2. `novelty_threshold` exceeded (max: 0.85)
3. `clarity_gradient < 0` for `cg_nonimprove_cycles` (typically 2)
4. `affect_z_threshold` exceeded (max z-score: 2.0)

**Actions**:
1. First trigger: Initiate dream-merge
2. Second trigger: Park for human review
3. Escalation limit: 1,200,000 ms (20 minutes)

---

## Packet Functions

### Fixed-Size Padding

All packets must conform to predefined sizes for timing channel prevention.

**Allowed sizes**: [4096, 8192, 12288] bytes

**Procedure**:
```python
def pad_packet(data, target_size):
    if len(data) > target_size:
        raise ValueError("Data exceeds target size")
    
    padding = target_size - len(data)
    return data + (b'\x00' * padding)
```

**Validation**: Reject any packet not matching an allowed size exactly

---

### Signature Verification

All envelopes must be cryptographically signed.

**Algorithm**: ECDSA-P256-SHA256

**Procedure**:
1. Compute `policy_hash = SHA256(policy_json)`
2. Sign envelope: `sig = ECDSA_sign(envelope_bytes, private_key)`
3. Verify: `ECDSA_verify(envelope_bytes, sig, public_key)`

**Key rotation**: Every 10 messages

**Sealed events**: BEACON, ALERT, MERGE, RESET, KEY_ROTATE, POLICY_SET

---

## Deterministic Seeds

For operators requiring randomness (e.g., GAN-lite), seeds must be deterministic and logged.

**Formula**: `seed = SHA256(session_id || timestamp || agent_id)`

**Requirements**:
- Seed must be included in sealed log
- Replay must reproduce identical outputs
- No external entropy sources

---

## Replay Validation

All experiments must pass bit-exact replay.

**Procedure**:
1. Extract sealed log
2. Re-run experiment with identical inputs
3. Compare all outputs byte-by-byte
4. Verify signatures match

**Success criteria**: 100% bit-exact match

**Failure**: Any deviation invalidates the run

---

## Mean Time to Detection (MTTD)

Measures how quickly guards detect violations.

**Computation**: `MTTD = timestamp_detection - timestamp_violation_start`

**Target**: ≤ 3.0 seconds

**Use cases**:
- DoV detection
- Drift threshold breaches
- Clarity Guard triggers

---

## Guild Concurrence

Measures agreement between independent diagnostic agents.

**Computation**: `concurrence_delta = |metric_agent_A - metric_agent_B|`

**Threshold**: Δ ≤ 0.05

**Applied to**:
- Geometry scores (Gemini)
- Entropy stress scores (Grok)

**Purpose**: Prevent single-agent diagnostic failures

---

## Reference Values

### Typical Operating Ranges

| Metric | Normal | Warning | Critical |
|--------|--------|---------|----------|
| Drift | ≤0.15 | 0.15–0.25 | >0.25 |
| Geometry | ≥0.80 | 0.70–0.80 | <0.70 |
| Clarity Gradient | >0 | 0 | <0 (2+ cycles) |
| Perception Synchrony | ≥0.75 | 0.65–0.75 | <0.65 |
| Entropy (rhythm) | ≤1.0 | 1.0–1.5 | >1.5 |

### Rate Limits (Policy v0.2+)

- Messages per second: 4
- Burst tokens: 8
- Max packet bytes: 12,288
- Beacon cadence: Every 5 packets
- Halt on missed beacons: 2

---

## Notes

All functions defined here are:
- **Deterministic**: No hidden randomness
- **Bounded**: All outputs have defined ranges
- **Auditable**: Every computation can be replayed
- **Versioned**: Changes require policy version bump
