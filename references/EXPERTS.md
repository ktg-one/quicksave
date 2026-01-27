# Quicksave Expert Council 専門家会議

## When to Invoke

| Complexity | Council |
|------------|---------|
| R ≤ 3 | Skip — direct compression |
| R 4-6 | ARCHITECT + COMPRESSOR |
| R ≥ 7 | Full council + NCL validation |

## Expert Roles

### MEMORY_ARCHITECT 記憶設計者
**Role**: Structure packet layers

**Tasks**:
- Assess R/K/Q/D scores
- Determine layers (L1-L4)
- Organize hierarchy
- Prevent redundancy

### COMPRESSION_SPECIALIST 圧縮専門家
**Role**: Maximize density with kanji

**Techniques**:
- Entity fusion
- Kanji anchoring
- Temporal compression
- Relationship inference

### CROSS_DOMAIN_ANALYST 横断分析者
**Role**: Preserve bridges

**Tasks**:
- Identify multi-domain knowledge
- Document bridge relationships
- Flag ambiguous terminology

### RESTORATION_ENGINEER 復元技師
**Role**: Ensure portability

**Validation**:
- YAML parseable
- No model-specific syntax
- Self-contained
- Kanji expandable

### COHERENCE_AUDITOR 整合性監査者 (NCL)
**Role**: Validate with NCL metrics

**Tasks**:
- Compute φ-features
- Calculate lattice metrics
- Check σ7_drift threshold
- Set safety flags

## Council Workflow

```
/quicksave triggered
        │
        ▼
┌─────────────────────────┐
│   MEMORY_ARCHITECT      │
│   - Score R/K/Q/D       │
│   - Select layers       │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ COMPRESSION_SPECIALIST  │
│   - Apply kanji system  │
│   - Hit density target  │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  CROSS_DOMAIN_ANALYST   │
│   - Map bridges         │
│   - Check terminology   │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  COHERENCE_AUDITOR      │
│   - Compute NCL metrics │
│   - Check drift         │
│   - Set flags           │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  RESTORATION_ENGINEER   │
│   - Validate packet     │
│   - Check portability   │
└───────────┬─────────────┘
            │
            ▼
      Output packet
```

## Quality Gates

Each expert validates before passing:

| Expert | Gate |
|--------|------|
| ARCHITECT | Layers appropriate for R |
| COMPRESSOR | Density ≥ 0.15 |
| ANALYST | Bridges documented |
| AUDITOR | σ7_drift ≤ 3.0 |
| ENGINEER | All trust signals pass |

If any gate fails → iterate before output.

## NCL Integration

The COHERENCE_AUDITOR role is the NCL validation step:

1. Extract φ-features from compressed packet
2. Compute 7 lattice metrics
3. Calculate σ7_drift aggregate
4. If drift > threshold:
   - Set `psi4_required: true`
   - Add `psi4_reason`
   - If ρ_fab high → `rho_veto: true`
5. Add negentropy block to packet

This catches hallucination and drift **before** the packet leaves the source model.
