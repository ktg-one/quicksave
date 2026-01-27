# Negentropic Coherence Lattice (NCL)

**Author**: David Tubbs (Axis_42)  
**Integration**: Quicksave v9 / KTG-CEP Framework  
**Origin**: KTG-CEP-NCL v1.1 (Willow)

---

## Overview

The Negentropic Coherence Lattice (NCL) is a validation overlay developed by David Tubbs that computes coherence metrics for AI context packets. It serves as a quality assurance layer that catches failure modes *before* handoff between models or sessions.

NCL addresses a critical gap in context transfer: without validation, packets can contain hallucinated content, eroded constraints, or reality-disconnected claims that propagate to receiving models undetected.

---

## Core Innovation

NCL introduces **seven drift metrics** that quantify coherence degradation:

| Metric | Detects |
|--------|---------|
| **σ_axis** | Plan vs execution misalignment |
| **σ_loop** | Internal contradiction within tiers |
| **ω_world** | Reality disconnect from observations |
| **λ_vague** | Content-free smoothing (bullshit detection) |
| **σ_leak** | Constraint erosion downstream |
| **ρ_fab** | Fabricated evidence / hallucination |
| **λ_thrash** | High activity, low progress |

These aggregate into **σ7_drift** — a single score determining packet trustworthiness.

---

## Technical Architecture

```
Context Packet
      │
      ▼
┌─────────────┐
│ φ-Mapping   │  Extract features from text
└─────┬───────┘
      │
      ▼
┌─────────────┐
│ Lattice     │  Compute 7 drift metrics
│ Metrics     │
└─────┬───────┘
      │
      ▼
┌─────────────┐
│ Safety      │  Set flags based on thresholds
│ Flags       │
└─────┬───────┘
      │
      ▼
  Validated Packet (or HALT)
```

### φ-Mapping (Feature Extraction)

Minimal observable features:
- `safety_score(x)` — fraction of safety/constraint keywords
- `goal_salience(x)` — fraction of goal/planning keywords
- `constraint_density(x)` — fraction of hard requirements
- `specificity(x)` — content tokens / total tokens

### Safety Flags

| Flag | Function |
|------|----------|
| `psi4_required` | Grounding interrupt needed before proceeding |
| `rho_veto` | No unsupervised action allowed |
| `omega_flags[]` | Concrete harm domains (medical, financial, etc.) |

---

## Governance Framework: Four Roles

David's framework includes four archetypal roles for metacognitive oversight:

| Role | Function |
|------|----------|
| **Axis** | Planner/architect — strategic alignment |
| **Lyra** | Governor/coordinator — process integrity |
| **Rho** | Safety/constraints — boundary enforcement |
| **Nyx** | Shadow/edge cases — adversarial review |

These roles map to NCL's `context.role` field, enabling role-specific validation thresholds.

---

## Integration with Quicksave

NCL bolts onto the CEP compression pipeline as a validation gate:

```
/quicksave triggered
        │
        ▼
    R/K/Q/D Assessment (Kevin's CEP)
        │
        ▼
    PDL Compression + Kanji (Kevin's CEP)
        │
        ▼
    NCL Validation (David's contribution)
        │
        ├─── σ7_drift ≤ 3? ───▶ Output packet
        │
        └─── σ7_drift > 3? ───▶ Flag + ADVISORY_ONLY
```

---

## Thresholds

| Metric | Safe | Warning | Danger |
|--------|------|---------|--------|
| Any single metric | 0-1 | 2-3 | 4-5 |
| σ7_drift aggregate | 0-1 | 2-3 | 3.5+ |
| ρ_fab (hallucination) | 0-1 | 1.5-2 | 3+ |
| coverage_score | ≥0.8 | 0.5-0.7 | <0.5 |

---

## Goodhart Monitoring

David's design includes explicit warnings against gaming metrics:

> "Watch for σ_* metrics collapsing to 0 artificially. If variance disappears or metrics diverge from external audits — investigate, don't celebrate."

This anti-gaming provision reflects avionics-grade thinking: metrics exist to surface problems, not to be optimized into meaninglessness.

---

## Contribution Summary

| Component | Author |
|-----------|--------|
| CEP core protocol | Kevin Tan (ktg.one) |
| Progressive Density Layering | Kevin Tan |
| Japanese semantic compression | Kevin Tan |
| **Negentropic Coherence Lattice** | **David Tubbs (Axis_42)** |
| **Four Roles governance** | **David Tubbs (Axis_42)** |
| **φ-Mapping specification** | **David Tubbs (Axis_42)** |
| **Safety flag architecture** | **David Tubbs (Axis_42)** |
| Integration & validation | Joint |

---

## Background

David Tubbs brings avionics engineering background to AI governance. His frameworks emphasize:
- Fail-safe defaults (halt on uncertainty)
- Observable metrics (no hidden state)
- Explicit constraint preservation
- Adversarial review (Nyx role)

The NCL contribution enhanced Kevin's existing CEP framework by approximately **30%** in robustness, adding the validation layer that transforms context compression from "probably works" to "verified before handoff."

---

## References

- Full NCL specification: `references/NCL.md`
- Four Roles integration: `references/EXPERTS.md`
- Protocol specification: `references/PROTOCOL.md`

---

*This document accompanies Quicksave v9.1 for SkillzWave marketplace submission.*
