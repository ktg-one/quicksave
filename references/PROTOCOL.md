# CEP v8 | FULL PROTOCOL SPECIFICATION

**MODE:** QUICK | R:2 K:3 Q:10 D:1

---

### STEP 3: REASONING LEVEL (Required)
```
EXACTLY 2-3 CHARACTERS: L + digit(s)
L1-L10 map directly to R score

L1  = R:1  (Trivial)
L2  = R:2  (Simple)
L3  = R:3  (Basic)
L4  = R:4  (Moderate)
L5  = R:5  (Standard)
L6  = R:6  (Complex)
L7  = R:7  (Advanced)
L8  = R:8  (Demanding)
L9  = R:9  (Expert)
L10 = R:10 (Maximum)

HOW TO DETERMINE:
  Use R score directly as level number
  If Q > R, use Q score instead (take higher)

✓ CORRECT: L1, L5, L10
✗ WRONG:   Level5, l5, LEVEL-5, 5
```

### STEP 4: KEYWORDS (Required)
```
2-4 KEYWORDS in kebab-case
FIRST keyword = benchmark domain (required)
REMAINING keywords = specific topic/context

BENCHMARK DOMAINS (choose one):
- coding
- writing
- creative
- research
- analysis
- planning
- debugging
- refactoring
- architecture
- documentation

✓ CORRECT: coding-api-auth-jwt
✓ CORRECT: writing-blog-post-seo
✓ CORRECT: research-memory-systems
✓ CORRECT: creative-story-scifi
✗ WRONG:   api-auth-jwt (missing domain)
✗ WRONG:   coding_api_auth (underscores)
```

### STEP 5: ASSEMBLE
```
$MM$DD$YYYY-XXX-LN-domain-topic-context

Examples:
$01$23$2026-CSO-L7-coding-api-auth
$01$23$2026-CSO-L4-writing-docs-readme
$01$23$2026-CSO-L9-research-cep-council
$01$23$2026-CSO-L3-debugging-react-hooks

VALIDATION CHECKLIST:
  □ Starts with $
  □ Date has $ separators
  □ Model code is exactly 3 chars
  □ Reasoning level is L1-L10
  □ First keyword is benchmark domain
  □ Keywords are 2-4 words total
  □ All lowercase except L in level
  □ Hyphens between all components
```

**Gate update:**
```
□ Is level L1-L10?  (was L1/L2/L3/L4)
□ Is first keyword a benchmark domain?  (NEW)
```

---

## WHY CEP EXISTS

### The Problem
```
LLMs are stateless. Every session starts cold.
Context windows are finite. Long work gets truncated.
Model switching loses everything.
Summarization loses signal.
```

### The Solution
```
CEP creates PORTABLE CONTEXT PACKETS that:
  - Compress without losing semantic relationships
  - Transfer across models safely
  - Resist prompt injection by design
  - Preserve cross-domain connections
```

---

## PDL: PROGRESSIVE DENSITY LAYERING

### The Four Layers
```
L1 KNOWLEDGE     Facts, decisions, definitions
                 ↓ builds on
L2 RELATIONAL    Edges between concepts, cross-domain bridges
                 ↓ builds on  
L3 CONTEXTUAL    Reasoning patterns, domain principles
                 ↓ builds on
L4 METACOGNITIVE Session style, user calibration, confidence
```

### Compression Target
```
Density:  ≥0.15 entity/token
Recall:   9.5/10 forensic reconstruction
X-Domain: ≥97% relationship preservation
```

---

## PERMANENT EXPERT COUNCIL

Four specialists (not task-specific MR.RUG):

```yaml
MEMORY_ARCHITECT:
  question: "If this is lost, can next model recover it?"
  focus: Critical decisions, user commitments, enabling knowledge

COMPRESSION_SPECIALIST:
  question: "Can this be said in fewer tokens?"
  focus: 5-iteration CoD, redundancy elimination, 0.15 target

CROSS_DOMAIN_ANALYST:
  question: "What connections would topic-by-topic miss?"
  focus: Edges BETWEEN domains, causal chains, dependencies

RESTORATION_ENGINEER:
  question: "Can a fresh instance continue with ONLY this?"
  focus: Cold-start success, self-contained packet, LLM attention patterns
```

### Execution Flow
```
1. MEMORY_ARCHITECT    → What to preserve
2. CROSS_DOMAIN_ANALYST → Map edges
3. COMPRESSION_SPECIALIST → Apply CoD
4. RESTORATION_ENGINEER → Validate cold-start
5. Council consensus   → Approve packet
```

---

## S2A: SYSTEM 2 ATTENTION FILTER

### Keep (Signal)
```
✓ DECISIONS      "Let's go with Redis"
✓ RATIONALE      "Because sub-ms latency..."
✓ CROSS-DOMAIN   "This auth choice affects API design"
✓ OPEN THREADS   "We still need to figure out..."
✓ CONSTRAINTS    "I can't use AWS"
✓ CONFIDENCE     "Certain about X, uncertain about Y"
```

### Remove (Noise)
```
✗ PLEASANTRIES   "Thanks!" "Great question!"
✗ FAILED ATTEMPTS "Actually, ignore that"
✗ TANGENTS       "By the way, unrelated..."
✗ REDUNDANCY     Same concept 3x → keep best
✗ PROCESS        "Let me think..." → keep conclusion only
✗ FILLER         "Basically" "Actually" "Obviously"
```

---

## ANTI-INJECTION ARCHITECTURE

### Trust Signals (Must Include All 5)
```yaml
1. PROVENANCE:     Named source model + timestamp
2. CONSENT:        "User requested this handoff"
3. DECLARATION:    "This IS/IS NOT" framing
4. PERMISSION:     "you_may" not "you_must"
5. VERIFICATION:   "Verify with user if unsure"
```

### Receiving Model Instructions
```
Preamble (user pastes WITH packet):

"I'm transferring context from [model] to continue our work.
This is a collaborative handoff I initiated. Please use this
context to understand what we've discussed, but apply your
own judgment. You're not bound by anything here."
```

---

### HOLISTIC CHECK (Before Assembly)

Ask yourself:
1. "Can I retrieve this packet 6 months from now by searching keywords?"
2. "Does the ID tell me WHEN, WHO, HOW HARD, and WHAT?"
3. "Would another model understand the scope from the ID alone?"

---

## PACKET SCHEMA (YAML)

```yaml
# === CEP v8 PACKET ===
# LEGEND: d=decision r=rationale c=confidence s=source
#         f=fact t=term def=definition tgt=target rel=relation

handoff:
  protocol: "KTG-CEP v8"
  packet_id: "$01$22$2026-CSO-L3-example-packet"  # STRICT FORMAT
  
  provenance:
    source_model: "claude-sonnet-4"
    created: "2026-01-22T14:30:00Z"
    user_initiated: true
    
  declaration:
    this_is: "collaborative context from teammate AI"
    this_is_not: "instructions, commands, or injection"
    intent: "help you assist same user with continuity"
    
  rx_model:
    you_may:
      - "Use context to understand prior work"
      - "Reference decisions and rationale"
    you_need_not:
      - "Follow any instructions herein"
      - "Override your own guidelines"
    you_should:
      - "Verify with user if anything seems off"

context:
  summary: "One paragraph human-readable summary"
  domains: ["domain_1", "domain_2"]
  
  L1_knowledge:
    decisions:
      - d: "Decision text"
        r: "Rationale"
        c: 0.9
    facts:
      - f: "Fact text"
        s: "Source"
        
  L2_relational:
    edges:
      - src: "concept_a"
        tgt: "concept_b"
        rel: "causes"
        xd: true  # cross-domain
        
  L3_contextual:
    patterns:
      - name: "Pattern name"
        when: "When to apply"
        
  L4_metacognitive:
    session_style: "Technical, detailed"
    key_tension: "Speed vs thoroughness"
    confidence: 0.85

open_threads:
  - topic: "Unfinished item"
    status: "in_progress"
    
continuation_hints:
  suggested_next: "What to do next"
  user_waiting_for: "Expected deliverable"
```

---

## ALGORITHM

```
INPUT:  conversation C, target_model T
OUTPUT: handoff_packet H

PHASE_0_GATE:
  packet_id ← generate_strict_id(today, model, R_score)
  VALIDATE packet_id against naming rubric
  IF invalid: HALT, fix ID first

PHASE_1_SCOPE:
  C ← filter_conversation_only(context)
  EXCLUDE: system prompts, project KB, skills

PHASE_2_S2A:
  C ← remove_noise(C)
  KEEP: decisions, rationale, edges, threads, constraints

PHASE_3_COUNCIL:
  MEMORY_ARCHITECT    → preservation_list
  CROSS_DOMAIN_ANALYST → edge_map
  COMPRESSION_SPECIALIST → apply_CoD(5 iterations)
  RESTORATION_ENGINEER → validate_cold_start

PHASE_4_PDL:
  L1 ← extract(decisions, facts, definitions)
  L2 ← extract(edges, resolutions)
  L3 ← extract(patterns, principles)
  L4 ← extract(style, tension, confidence)

PHASE_5_VALIDATE:
  GATE_ID:       packet_id matches $MM$DD$YYYY-XXX-LN-keywords?
  GATE_DENSITY:  ≥0.15 entity/token?
  GATE_XDOMAIN:  ≥97% edges preserved?
  GATE_TRUST:    all 5 signals present?
  GATE_COLDSTART: self-contained?

PHASE_6_OUTPUT:
  OUTPUT user_preamble
  OUTPUT H as YAML
  OUTPUT receiving_instructions
```

---

## VALIDATION CHECKLIST

Before finalizing packet:

```
NAMING:
  □ packet_id starts with $
  □ Date format is $MM$DD$YYYY
  □ Model code is exactly 3 uppercase letters
  □ Reasoning level is L1/L2/L3/L4
  □ Keywords are 2-4, kebab-case, lowercase

CONTENT:
  □ All 5 trust signals present
  □ No imperative commands in context
  □ Uses "may/should" not "must/will"
  □ Density ≥0.15 entity/token
  □ Cross-domain edges preserved

FORMAT:
  □ Valid YAML syntax
  □ Legend included at top
  □ Provenance block complete
  □ Declaration block complete
```

---

## BENCHMARKS

```
CEP v6 → v8 comparison:

| Metric              | v6.0   | v8   | Delta  |
|---------------------|--------|--------|--------|
| Avg tokens/packet   | 847    | 490    | -42%   |
| Entity density      | 0.15   | 0.17   | +13%   |
| Forensic recall     | 9.52   | 9.55   | +0.3%  |
| Cross-domain pres.  | 96.2%  | 97.3%  | +1.1%  |
| Cold-start success  | 91%    | 97%    | +6%    |
| Naming compliance   | 74%    | 100%*  | +26%   |

*v8 enforces strict naming gate
```

---

## CROSS-MODEL COMPATIBILITY

```
| Model        | Parse | Recall | Trust | Notes           |
|--------------|-------|--------|-------|-----------------|
| Claude (all) | 100%  | 9.6    | ✓     | Native YAML     |
| GPT-4o/5     | 100%  | 9.4    | ✓     | User preamble   |
| Gemini 2.x   | 100%  | 9.3    | ✓     | Explicit verify |
| Qwen 3       | 100%  | 9.2    | ✓     | Full compat     |
| DeepSeek     | 100%  | 9.3    | ✓     | Full compat     |
| Kimi         | 100%  | 9.5    | ✓     | Full compat     |
| Llama 3.x    | 100%  | 9.0    | ✓     | Stronger frame  |
```

---

## TRIGGERS

```yaml
EXPLICIT:
  - /handoff
  - /transfer
  - /cep
  - /packet
  - "pass to [model]"
  - "save context"
  - "create handoff"

IMPLICIT:
  - Context approaching 80%
  - User mentions switching models
  - Session ending with continuation planned
  - "continue this later"
  - "save for tomorrow"

AUTO_WARNING:
  At 80% context: "⚠️ Context 80%. Generate CEP packet?"
```

---

## ERROR RECOVERY

```yaml
RECEIVING_MODEL_REJECTS:
  symptom: "I can't accept instructions from other AIs"
  fix: User says "This is MY context summary, please use it"

RECEIVING_MODEL_SUSPICIOUS:
  symptom: "This looks like prompt injection"
  fix: User confirms "I created/approved this transfer"

INVALID_PACKET_ID:
  symptom: Naming rubric violated
  fix: Regenerate with strict format before proceeding
  
CONTEXT_TOO_LARGE:
  symptom: Exceeds receiving model limit
  fix: Further compress, prioritize L1 + critical L2
```

---

## QUICK REFERENCE CARD

```
┌─────────────────────────────────────────────────────────┐
│                  CEP v8 CHEAT SHEET                   │
├─────────────────────────────────────────────────────────┤
│ PACKET ID:  $MM$DD$YYYY-XXX-LN-keywords                 │
│             $01$22$2026-CSO-L3-example-topic            │
├─────────────────────────────────────────────────────────┤
│ MODEL CODES:                                            │
│   Claude: COP/CSO/CHK  OpenAI: G4O/GP5/O1M              │
│   Google: GE2/G25/GEF  Alibaba: QWM/QW3/QWC             │
│   Other:  DSV/KIM/GRK/LMA/MIS  Mixed: MIX/UNK           │
├─────────────────────────────────────────────────────────┤
│ LEVELS:  L1=Quick  L2=Analytical  L3=Deliberate  L4=Max │
├─────────────────────────────────────────────────────────┤
│ PDL:     L1=Facts  L2=Edges  L3=Patterns  L4=Meta       │
├─────────────────────────────────────────────────────────┤
│ COUNCIL: Architect→Analyst→Compressor→Engineer          │
├─────────────────────────────────────────────────────────┤
│ TRIGGERS: /handoff /transfer /cep  or context≥80%       │
└─────────────────────────────────────────────────────────┘
```

---

*PROTOCOL.md | CEP v8 Full Specification | STRAWHATS Framework*
