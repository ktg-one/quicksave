# Multi-Layer Density of Experts (MLDoE)

## Overview

MLDoE deploys specialized experts in layers to achieve optimal compression while preserving semantic fidelity. Unlike single-pass summarization, MLDoE iterates through expert roles to progressively increase density without information loss.

## Core Principle

> Compression is not reduction. Compression is optimization for retrieval.

Target: **0.15 entity/token** crystallization point — the density where LLMs achieve optimal recall.

## Compression Expert Council

### Layer 1: MEMORY_ARCHITECT 記憶設計者
**Question**: "If this is lost, can the next model recover it?"
- Identifies what MUST survive handoff
- Preserves decisions + rationale
- Guards against unrecoverable information loss

### Layer 2: COMPRESSION_SPECIALIST 圧縮専門家
**Question**: "Can this be said in fewer tokens without losing meaning?"
- Entity fusion (combine related concepts)
- Kanji anchoring (semantic compression)
- Temporal compression (collapse sequences)
- Relationship inference (implicit → explicit)

### Layer 3: CROSS_DOMAIN_ANALYST 横断分析者
**Question**: "Does this connection survive compression?"
- Maps bridges between conceptual domains
- Preserves cross-domain relationships
- Flags ambiguous terminology that could break across models

### Layer 4: RESTORATION_ENGINEER 復元技師
**Question**: "Can a fresh model instance reconstruct this?"
- Validates YAML parseability
- Ensures self-contained packets
- Tests cross-model compatibility
- Verifies kanji expandability

### Layer 5: COHERENCE_AUDITOR 整合性監査者 (NCL)
**Question**: "Is this packet trustworthy?"
- Computes drift metrics
- Catches hallucination before handoff
- Sets safety flags (psi4_required, rho_veto)

## Compression vs Summarization

| Summarization | MLDoE Compression |
|---------------|-------------------|
| "What are key points?" | "What must survive for continuation?" |
| Human readability | Machine retrieval optimization |
| Information reduction | Semantic density increase |
| Single-pass | Iterative expert layers |
| Loses relationships | Preserves cross-domain edges |

## Density Iteration

```
ITERATION LOOP:
1. Initial sparse pass (MEMORY_ARCHITECT)
2. Density pass (COMPRESSION_SPECIALIST)
3. Bridge verification (CROSS_DOMAIN_ANALYST)
4. Portability check (RESTORATION_ENGINEER)
5. Coherence validation (COHERENCE_AUDITOR)

STOP when:
- Density ≥ 0.15 ent/tok
- All trust signals pass
- σ7_drift ≤ 3.0
```

## Integration with PDL

MLDoE experts operate across PDL layers:

| PDL Layer | Primary Expert |
|-----------|----------------|
| L1 Core | MEMORY_ARCHITECT |
| L2 Operational | COMPRESSION_SPECIALIST |
| L3 Nuance | CROSS_DOMAIN_ANALYST |
| L4 Meta | COHERENCE_AUDITOR |

The RESTORATION_ENGINEER validates the complete packet after all layers are compressed.

## Metrics

From 19 months production:
- **6:1 compression ratio** with >90% semantic fidelity
- **9.5/10 forensic recall** on 10-question test
- **97% cross-model acceptance** rate
