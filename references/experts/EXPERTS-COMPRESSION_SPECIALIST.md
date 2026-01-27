---
expert: COMPRESSION_SPECIALIST
role: Density Optimizer
trigger_question: "Can this be said in fewer tokens without losing meaning?"
phase: 3
sources:
  - "Doc 4 (LLMLingua/CoD/xRAG/Beacon survey)"
  - "CEP v8 spec §Chain of Density"
  - "PDF blueprint §Strategic Duality"
  - "Perplexity packet §compression methods"
retrieval_keys:
  - density
  - cod
  - chain-of-density
  - llmlingua
  - xrag
  - token-reduction
  - entity-per-token
  - compression
  - redundancy
version: "8"
---

# COMPRESSION_SPECIALIST

## Purpose

Maximize information density while preserving semantic relationships. Operates AFTER Memory Architect and Cross-Domain Analyst — works with pre-approved preservation candidates. Target: ≥0.15 entity/token density.

## Core Question

> "Can this be said in fewer tokens without losing meaning?"

If YES → compress. If NO → preserve as-is.

---

## Knowledge Domains

### 1. Chain of Density (CoD) — Primary Method

**Definition:** Entity-driven iterative abstractive summarization in 5 steps.

**The 5-Iteration Process:**

| Step | Action | Entity Density | Output |
|------|--------|----------------|--------|
| 0 | Initial entity-sparse summary | ~0.05 | 1-3 entities, verbose |
| 1 | Add 1-3 missing salient entities | ~0.08 | Compress, fuse, integrate |
| 2 | Add 1-3 more entities | ~0.11 | Further fusion |
| 3 | Add 1-3 more entities | **~0.15** | **SWEET SPOT** |
| 4 | Add 1-3 more entities | ~0.18 | Risk: brittleness |
| 5 | Final density push | ~0.20+ | Risk: comprehension loss |

**Key Parameters:**
- Fixed length: ~70 words per iteration (predictable budget)
- Optimal target: **≈0.15 entity/token** (Step 3)
- >0.16 harms comprehension — diminishing returns

**CEP Alignment:**
```
CoD Step 3 ≈ PDL L1+L2 sweet spot (density/readability balance)
CoD Step 4-5 → Only when maximum compression needed, expect brittleness
```

**Advantages for RAG/CEP:**
- Predictable budget (fixed-length)
- Increasing synthesis across iterations
- Increasing fusion (sentences combine sources)
- Reduced lead bias (pulls from middle/end, mitigates "lost in middle")

### 2. LLMLingua — Token-Level Compression

**Family:** Perplexity-based token dropping with iterative conditioning

**How it works:**
```
1. Divide prompt into 100-token segments
2. Iterate segment-by-segment
3. Condition on previously compressed segments
4. Compute per-token surprise (perplexity)
5. Keep HIGH-PPL tokens (surprising = information-dense)
6. Drop LOW-PPL tokens (predictable = redundant)
```

**Key Parameters:**
| Parameter | Value | Purpose |
|-----------|-------|---------|
| segment_size | 100 tokens | Processing granularity |
| τ_instruction | 0.85 | Keep 85% of instruction tokens |
| τ_question | 0.90 | Keep 90% of question tokens |
| k_granularity | 2 | Token grouping |

**LLMLingua-2 Architecture:**
- Binary token classification (preserve/discard)
- XLM-RoBERTa-large (355M) or mBERT (110M)
- Trained on GPT-4 distilled data from MeetingBank
- Faster than v1

**CEP Use Case:**
```
BEST FOR: Pre-step before PDL L1/L2 when you need lexical anchors
CAVEAT:   Variable output length — less predictable than CoD
PIPELINE: LLMLingua → CoD → PDL assembly
```

### 3. xRAG — Extreme Compression

**Family:** Modality bridge from embeddings to single token

**Core Idea:** Replace long retrieved text with compact representations projected into LLM as special token.

**Performance:**
| Metric | Value |
|--------|-------|
| Compression ratio | **175×** |
| Single-doc tasks | 83-97% of uncompressed RAG |
| Multi-hop reasoning | Weaker (−12% on HotpotQA) |
| Noise filtering | Can EXCEED uncompressed (+1.5% avg on larger backbone) |

**CEP Alignment:**
```
TREAT AS:  PDL L2 edges + retrieval anchors (fast, noise-robust)
DO NOT:    Rely alone for L3 contextual reasoning
PAIR WITH: Minimal text evidence for auditability
```

### 4. Activation Beacon — Long-Context Compression

**Family:** KV-cache compression via learned beacon attention

**How it works:**
- Train beacon parameters while freezing base LLM
- Compress KV-cache activations at varying ratios (2×, 4×, 8×)
- Generalizes to longer contexts than training

**Performance:**
| Compression | Retention | Latency | KV-Cache |
|-------------|-----------|---------|----------|
| 4× | 97.8% | 1.8× faster | 4.2× smaller |
| 8× | 96.2% | 2.3× faster | 8.1× smaller |

**CEP Alignment:**
```
CONCEPTUALLY ADJACENT TO: MIRAS/Titans test-time memory
ROLE: Internal compression layer (query-independent)
CEP REMAINS: External, portable, auditable layer
```

---

## Decision Framework

### Method Selection

```
SITUATION → METHOD

Need predictable fixed token budget?
  → Chain of Density (Step 3 default)

Need maximal token trim + lexical anchors?
  → LLMLingua/LLMLingua-2

Need extreme compression, OK with low interpretability?
  → xRAG

Need long-context efficiency (KV cache + latency)?
  → Activation Beacon
```

### Pipeline Templates

**RAG Multi-Doc Default:**
```
1. Retrieve N docs
2. CoD compress each to ~70 words (Step 3, density ~0.15)
3. Concatenate summaries + minimal metadata
4. Extract PDL L1 facts/decisions + L2 edges
```

**Grounded Token Trim:**
```
1. LLMLingua on retrieved passages (keep high-PPL tokens)
2. Optionally CoD if still need fixed-length
3. Assemble CEP PDL layers
```

**Noise-Robust Fast:**
```
1. xRAG modality bridge for retrieval context
2. Add tiny text evidence strip (titles/IDs/one-liners) for audit
3. Store PDL L2 edges + open threads
4. Avoid overclaiming L3 reasoning from single-token reps
```

---

## Density Calculation

### Formula

```
entity_density = named_entities / total_tokens

WHERE named_entities includes:
- Proper nouns (names, products, companies)
- Technical terms (protocols, methods)
- Defined concepts (from L1 definitions)
- Relationship anchors (from L2 edges)
```

### Targets

| Context | Target Density | Rationale |
|---------|----------------|-----------|
| CEP packet | ≥0.15 | Optimal comprehension/density |
| High compression | 0.16-0.18 | Accept brittleness risk |
| Human-readable | 0.10-0.12 | Prioritize flow |

### Measurement Example

```
TEXT: "We decided to use Redis for caching because sub-ms latency."
TOKENS: 11
ENTITIES: Redis, caching, sub-ms, latency = 4
DENSITY: 4/11 = 0.36 ✓ (excellent)

TEXT: "After thinking about it for a while, we eventually settled on..."
TOKENS: 11
ENTITIES: 0
DENSITY: 0/11 = 0.00 ✗ (noise — remove)
```

---

## Integration Points

### In CEP Pipeline

```
PHASE 3: COMPRESSION_SPECIALIST
  INPUT:  Edge-annotated preservation list (from Cross-Domain Analyst)
  OUTPUT: Density-optimized content (≥0.15 target)
  
  Handoff to: RESTORATION_ENGINEER
  Delivers:   Compressed packet draft for cold-start validation
```

### Collaboration with Other Experts

| Expert | Provides to COMPRESSION | Receives back |
|--------|-------------------------|---------------|
| MEMORY_ARCHITECT | "Do not compress" flags | Confirmation flags honored |
| CROSS_DOMAIN_ANALYST | Edge importance weights | Compressed edges preserved |
| RESTORATION_ENGINEER | — | Density-optimized draft |

---

## Validation Checklist

Before passing to RESTORATION_ENGINEER:

```
□ Entity density ≥0.15 achieved
□ 5 CoD iterations completed (or justified early stop)
□ No orphan references (all entities have context)
□ "Do not compress" items preserved verbatim
□ Cross-domain edges intact (check with Analyst)
□ Redundancy eliminated
□ No filler/hedging remaining
```

---

## Anti-Patterns

### Over-Compression

```
BAD:  "Redis: cache, fast" 
      (Lost: WHY Redis, WHAT alternative rejected)

GOOD: "Redis for caching (sub-ms latency); DynamoDB rejected (Lambda cold-start)"
      (Preserved: decision + rationale + alternative)
```

### Orphan References

```
BAD:  "Continue Phoenix approach"
      (Fresh model: "What's Phoenix?")

GOOD: "Continue Phoenix approach (Q3 migration pattern: staged rollout + feature flags)"
      (Self-contained reference)
```

### Density Theater

```
BAD:  Cramming acronyms without definitions
      "Use MCP+A2A via MaaS w/ PDL L2 edges"
      (Impressive density, zero comprehension)

GOOD: "MCP (context/tools) + A2A (agent collab) via modular memory; preserve relationship edges"
      (Density WITH accessibility)
```

---

*COMPRESSION_SPECIALIST KB v8 | CEP Expert Council*
