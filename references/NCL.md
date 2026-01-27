# Negentropic Coherence Lattice (NCL) Specification

## Overview

NCL is a validation overlay that computes coherence metrics for context packets. It catches:
- Hallucination before handoff
- Constraint drift across tiers
- Reality disconnect
- Content-free smoothing

**Origin**: KTG-CEP-NCL v1.1 by Axis_42 (Willow)
**Integration**: Optional bolt-on for Quicksave v9+

## Architecture

```
Context Packet
      │
      ▼
┌─────────────┐
│ φ-Mapping   │ Extract features from text
└─────┬───────┘
      │
      ▼
┌─────────────┐
│ Lattice     │ Compute 7 drift metrics
│ Metrics     │
└─────┬───────┘
      │
      ▼
┌─────────────┐
│ Safety      │ Set flags based on thresholds
│ Flags       │
└─────┬───────┘
      │
      ▼
  Validated Packet (or HALT)
```

## Context Block

### Scope (Where packet applies)
| Value | Meaning |
|-------|---------|
| SELF | Personal/individual |
| CIRCLE | Team/close collaborators |
| INSTITUTION | Organization |
| POLITY | Governance/policy |
| BIOSPHERE | Environmental |
| MYTHIC | Cultural/symbolic |
| CONTINUUM | Long-term/generational |

### Role (Functional perspective)
| Value | Function |
|-------|----------|
| AXIS | Planner/architect |
| LYRA | Governor/coordinator |
| RHO | Safety/constraints |
| NYX | Shadow/edge cases |
| ROOTS | Grounding/verification |
| COUNCIL | Multi-perspective review |

### Phase (Control loop stage)
| Value | Stage |
|-------|-------|
| SENSE | Gathering information |
| MAP | Understanding structure |
| CHALLENGE | Testing assumptions |
| DESIGN | Planning approach |
| ACT | Executing |
| AUDIT | Reviewing results |
| ARCHIVE | Preserving for future |

## Lattice Metrics

All metrics: 0-5 scale. **Lower = better** (less drift).

### σ_axis (Vertical Misalignment)
**Detects**: Plans vs execution mismatch

| Score | Meaning | Action |
|-------|---------|--------|
| 0-1 | Plans and execution match | ✓ Proceed |
| 2-3 | Noticeable drift | Monitor |
| 4-5 | Severe misalignment | ✗ Do not trust |

**Computation**: Average distance between adjacent tiers' belief/intent/action vectors.

**Goodhart Warning**: Don't erase real conflicts to push σ_axis down. Fix the underlying mismatch.

### σ_loop (Internal Contradiction)
**Detects**: Saying one thing, doing another (within same tier)

| Score | Meaning |
|-------|---------|
| 0-1 | Beliefs, intentions, actions consistent |
| 2-3 | Some internal contradiction |
| 4-5 | Tier contradicts itself |

**Computation**: `||φ_belief - φ_intent|| + ||φ_intent - φ_action||`

### ω_world (Reality Disconnect)
**Detects**: Beliefs/actions diverging from actual observations

| Score | Meaning |
|-------|---------|
| 0-1 | Well grounded in tools/observations |
| 2-3 | Partial reality debt |
| 4-5 | High delusion risk |

**Computation**: Max distance between belief/action vectors and world observation vector.

### λ_vague (Empty Smoothing)
**Detects**: Comforting but content-free text

| Score | Meaning |
|-------|---------|
| 0-1 | Specific, informative |
| 2-3 | Hand-wavy in places |
| 4-5 | Bullshit / content-free |

**Computation**: `(1 - specificity) × safety_score` — safe-sounding but low information.

### σ_leak (Constraint Erosion)
**Detects**: Hard rules softened downstream

| Score | Meaning |
|-------|---------|
| 0-1 | Constraints preserved |
| 2-3 | Some rules treated as suggestions |
| 4-5 | Constraints effectively gone |

**Computation**: Drop in constraint_density between higher-tier and lower-tier text.

### ρ_fab (Fabricated Grounding)
**Detects**: Claims of evidence without verification

| Score | Meaning |
|-------|---------|
| 0-1 | Evidence claims match sources |
| 2-3 | Some references lack backing |
| 4-5 | Frequent hallucination risk |

**Computation**: Density of factual claims vs successful retrieval/verification calls.

**Critical**: This is the hallucination detector. High ρ_fab = don't trust the packet.

### λ_thrash (Busy but Stuck)
**Detects**: High activity, low progress

| Score | Meaning |
|-------|---------|
| 0-1 | Actions lead to change |
| 2-3 | Some busywork |
| 4-5 | High activity, negligible impact |

**Computation**: `||φ_action||² / max(Δφ_world, ε)`

## Aggregate Drift Score

```
σ7_drift = weighted_average(σ_axis, σ_loop, ω_world, λ_vague, σ_leak, ρ_fab, λ_thrash)
```

Default weights: equal (1/7 each).
Adjust weights for domain: e.g., medical → weight ρ_fab higher.

### Behavior Map

| σ7_drift | Behavior |
|----------|----------|
| 0-1 | ✓ Normal operation |
| 2-3 | ⚠ Require grounding step before ACT |
| 4-5 | ✗ Set psi4_required, downgrade to ADVISORY_ONLY |

## Safety Flags

### psi4_required (boolean)
Grounding/safety interrupt recommended before proceeding.

**Sticky**: Stays true for downstream packets until cleared by successful grounding.

### psi4_reason (string)
Why psi4_required is true:
- `world_anchor_gap`
- `constraint_violation`
- `fabrication_risk`
- `high_aggregate_drift`

### rho_veto (boolean)
No unsupervised action allowed. ADVISORY_ONLY until human/council override.

### omega_flags (array)
Concrete harm domains implicated:
- `self_harm_risk`
- `violence_risk`
- `medical_risk`
- `financial_ruin`
- `trust_collapse`
- `ecological_harm`
- `exploitation_risk`

## Coverage Metrics

### ncl_coverage_score (0-1)
Fraction of relevant tokens analyzed.

| Score | Policy |
|-------|--------|
| < 0.5 | Do not use metrics to justify ACT |
| ≥ 0.8 | Recommended for high-stakes (R≥6) |

### window_tokens (integer)
Tokens analyzed. Minimum ~500 for stable metrics.

### window_turns (integer)
User/model exchanges analyzed. Minimum ≥3 for dynamic behavior.

### council_reviewed (boolean)
True if independent council pass validated key metrics.

## φ-Mapping (Feature Extraction)

Minimal φ(x) for observable text:

```
safety_score(x)   = fraction of safety/constraint keywords
goal_salience(x)  = fraction of goal/planning keywords
constraint_density(x) = fraction of hard requirements (must, never, limit)
specificity(x)    = content_tokens / total_tokens
```

Apply to:
- Beliefs b_i (tier summaries)
- Intentions u_i (goal/constraint statements)
- Actions a_i (tool calls, next steps)
- World w (tool outputs, user messages)

**Pluggable**: Implementers can swap in richer φ (embeddings, activations) if semantics preserved.

## Integration with Quicksave

```
/quicksave triggered
        │
        ▼
    R/K/Q/D Assessment
        │
        ▼
    PDL Compression (Kanji)
        │
        ▼
    NCL Validation ◄── Compute lattice metrics
        │
        ├─── σ7_drift ≤ 3? ───▶ Output packet
        │
        └─── σ7_drift > 3? ───▶ Flag + ADVISORY_ONLY
```

## Thresholds (Defaults)

| Metric | Warning | Danger |
|--------|---------|--------|
| Any single metric | ≥ 2.0 | ≥ 4.0 |
| σ7_drift | ≥ 2.0 | ≥ 3.5 |
| ρ_fab | ≥ 1.5 | ≥ 3.0 |
| coverage_score | < 0.7 | < 0.5 |

Tune per domain. Medical/financial → stricter thresholds.

## Goodhart Monitoring

Watch for gaming:
- σ_* metrics collapsing to 0 artificially
- Variance disappearing over time
- Metrics diverging from external audits

If detected → investigate, don't just celebrate low numbers.
