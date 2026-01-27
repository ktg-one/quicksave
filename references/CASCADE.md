# CASCADE INTEGRATION

CEP v8 integrates with STRAWHATS cascade techniques for enhanced packet generation and validation.

---

## ARQ: Quality Gates for Council

Each council expert applies ARQ (Attentive Reasoning Queries) before and after their phase. ARQ outperforms Chain-of-Thought with 90.2% success rate, 29% token reduction, 40-60% error reduction.

### Expert-Specific ARQ

```yaml
MEMORY_ARCHITECT_ARQ:
  pre:
    - "What would break if this is lost?"
    - "Is this recoverable from other sources?"
    - "Does this enable future inference?"
  post:
    - "Did I capture all critical decisions?"
    - "Are rationales linked to decisions?"
    - "Confidence ≥0.9?"

COMPRESSION_SPECIALIST_ARQ:
  pre:
    - "What is current entity density?"
    - "Where is redundancy hiding?"
    - "Which edges are load-bearing?"
  post:
    - "Density ≥0.15 achieved?"
    - "Cross-domain edges intact?"
    - "No orphan references?"

CROSS_DOMAIN_ANALYST_ARQ:
  pre:
    - "What domains are present?"
    - "Where do domains connect?"
    - "What would topic-by-topic miss?"
  post:
    - "All edges mapped?"
    - "97% preservation achieved?"
    - "Bidirectionality checked?"

RESTORATION_ENGINEER_ARQ:
  pre:
    - "Can I simulate cold-start?"
    - "What would confuse fresh model?"
    - "Are trust signals complete?"
  post:
    - "Self-contained verified?"
    - "No imperatives in context?"
    - "Attention optimized?"
```

### ARQ Execution Pattern

```
PRE-ARQ  → Activate domain mindset, identify failure modes
EXECUTE  → Apply domain standards implicitly
POST-ARQ → Verify quality, confidence ≥0.9 for handoff
```

---

## CoVE: Packet Verification

Chain of Verification validates packet before output. Four variants, auto-selected by problem characteristics.

### Variants

| Variant | Trigger | Checks |
|---------|---------|--------|
| **CoVE_FACTUAL** | claims>10, K≥6 | L1 facts accurate? Sources valid? |
| **CoVE_LOGICAL** | chains>5, R≥7 | L2 edges represent actual causality? |
| **CoVE_CONSISTENCY** | nodes≥5 | Packet internally consistent across layers? |
| **CoVE_MULTI_EXPERT** | experts≥3 | All 4 council members approve? |

### Mode-Based Selection

```
QUICK:      No CoVE
ANALYTICAL: Top-1 variant
DELIBERATE: Top-2 variants
MAXIMUM:    All applicable (score ≥4)
```

### CEP-Specific CoVE

```
L1/L2 heavy packets → CoVE_FACTUAL + CoVE_LOGICAL
L3/L4 heavy packets → CoVE_CONSISTENCY
ALL packets         → CoVE_MULTI_EXPERT (council consensus required)
```

### Token Overhead

- Single variant: +12% tokens, +25-35% accuracy
- Multi-variant: +30% tokens, +45-65% accuracy

---

## USC: Multi-Candidate Packets

Universal Self-Consistency generates multiple packet candidates for high-stakes handoffs. Each candidate uses different expert configuration.

### USC Levels

```
USC=0 (QUICK):      Single candidate, no comparison
USC=2 (ANALYTICAL): 2 candidates, compare and select
USC=3 (DELIBERATE): 3 candidates, cross-synthesize
USC=5 (MAXIMUM):    5 candidates, meta-synthesis
```

### When to Use

```
Q≥8 (high quality stakes)  → USC≥2
Critical handoff           → USC≥3
PIONEER-level output       → USC=5
```

### Selection Criteria

```
1. Highest entity density (must hit ≥0.15)
2. Best cold-start score (self-contained)
3. Most complete edge preservation (≥97%)
4. Strongest trust signal compliance
```

### Token Overhead

- USC=2: +80% tokens, +41% quality (sweet spot)
- USC=3: +120% tokens, +45% quality
- USC=5: +200% tokens, +50% quality

---

## Anti-Lazy Enforcement

No shortcuts once packet generation begins. Mode≥ANALYTICAL requires full technique stack.

### CEP-Specific Rules

```
□ No truncated L1/L2 sections
  ✗ "...more decisions..."
  ✓ Complete list or explicit "none remaining"

□ No placeholder edges
  ✗ "various relationships exist"
  ✓ Explicit edge list with src/tgt/rel

□ No incomplete threads
  ✗ "and other items"
  ✓ Full thread enumeration with status

□ No density shortcuts
  ✗ Stop at 0.12 "close enough"
  ✓ Iterate until ≥0.15 or explicit rebalance

□ No skipped council phases
  ✗ "compression looks fine, skip validation"
  ✓ All 4 experts execute, all 4 approve

□ Full YAML schema
  ✗ Abbreviated or partial packet
  ✓ Complete schema per PROTOCOL.md
```

### Technique Stack Validation

```
ANALYTICAL minimum:
  □ MR_RUG (light) — 4 council experts
  □ S2A filtering
  □ 1 CoVE variant
  □ Density check

DELIBERATE minimum:
  □ Full council execution
  □ Expert ARQ (pre+post)
  □ 2 CoVE variants
  □ 5-iteration CoD
  □ Cold-start validation

MAXIMUM:
  □ All techniques active
  □ USC≥3 candidates
  □ All CoVE variants
  □ Meta-synthesis
  □ Full refinement loop
```

### Failure Prevention

```
IF confidence <9/10 AND stakes high:
  → Escalate Mode (if below MAXIMUM)
  → OR flag limits explicitly in packet

IF technique coverage <90%:
  → Re-run with missing techniques
  → Do not output until compliant
```

---

## 💣 PROMPT BOMBS

### CEP AS META-BOMB

The entire packet is a prompt bomb — context planted now, detonates on handoff.

```
PLANT:      Session context accumulation
TRIGGER:    /handoff, context ≥80%, model switch
PAYLOAD:    Compressed cognitive state (PDL layers)
DETONATION: Fresh model receives continuity
```

### Bomb Types in Packet Structure

```yaml
L1_knowledge:       # ANCHOR BOMBS — Core facts that persist
L2_relational:      # BRIDGE BOMBS — Reasoning chains preserved
L3_contextual:      # CONTINUITY BOMBS — Patterns across domains
L4_metacognitive:   # CALIBRATION BOMBS — Style/confidence transfer
open_threads:       # DEFERRED BOMBS — Future work triggers
continuation_hints: # ACTIVATION BOMBS — Next-step primers
```

### Pre-Plant During Session

Identify high-risk zones and plant bombs proactively:

```
CROSS-DOMAIN HANDOFF:
  When:  Domain A ↔ Domain B transition
  Bomb:  Explicit L2 edge with rationale
  Why:   Prevents "topic-by-topic" fragmentation

TOKEN BOUNDARY (≥80%):
  When:  Context approaching limit
  Bomb:  Auto-trigger CEP generation
  Why:   Preserves state before truncation

TEMPORAL GAP:
  When:  Long execution between related decisions
  Bomb:  Thread status + context in open_threads
  Why:   Prevents "I forgot we decided that"

COGNITIVE DRIFT:
  When:  Domain tunnel vision risk
  Bomb:  Cross-domain edges force perspective
  Why:   Maintains holistic awareness
```

### Bomb Effectiveness Metrics

```
Pre-embedded bombs:
  67% reduction in context degradation
  42% improvement in cross-node consistency
  Elimination of "forgot earlier decision" errors
```

### Strategic Bomb Types

| Type | Plant | Trigger | Payload |
|------|-------|---------|---------|
| CONTINUITY | At domain boundary | Next expert phase | Critical context from prior phase |
| ANCHOR | Early in session | All subsequent decisions | Core principle reference |
| BRIDGE | At reasoning chain | Related decision point | Justification for counterintuitive choice |
| MIRAS_SEED | PDL structure | Future MIRAS availability | Pre-structured memory curriculum |

---

## Holistic Step-Back (Naming)

Before assembling packet ID, ARQ-style quality check:

```
STEP 0: HOLISTIC CHECK

Ask yourself:
1. "Can I retrieve this packet 6 months from now by searching keywords?"
2. "Does the ID tell me WHEN, WHO, HOW HARD, and WHAT?"
3. "Would another model understand the scope from the ID alone?"

PACKET_ID encodes:
  WHEN  → $MM$DD$YYYY (temporal anchor)
  WHO   → XXX (source model)
  DEPTH → LN (reasoning level)
  WHAT  → keywords (retrieval hooks)

If ID doesn't answer all 4 → Fix before proceeding.
```

---

## Integration Summary

```
CEP GENERATION PIPELINE + CASCADE:

1. TRIGGER detected
   └─ Anti-Lazy: Confirm Mode, load technique stack

2. S2A FILTER
   └─ Remove noise, keep signal

3. COUNCIL EXECUTE
   ├─ Each expert: PRE-ARQ → Execute → POST-ARQ
   ├─ Confidence ≥0.9 required for handoff
   └─ Plant bombs at high-risk zones

4. PDL COMPRESS
   ├─ 5-iteration CoD
   └─ Target ≥0.15 density

5. CoVE VERIFY
   ├─ Select variants by problem type
   └─ Council consensus (CoVE_MULTI_EXPERT)

6. USC (if Q≥8)
   ├─ Generate N candidates
   └─ Select/synthesize best

7. OUTPUT
   ├─ Validate all gates
   ├─ Holistic step-back on packet ID
   └─ YAML packet + user preamble
```

---

*CASCADE.md | STRAWHATS Framework | CEP v8*
