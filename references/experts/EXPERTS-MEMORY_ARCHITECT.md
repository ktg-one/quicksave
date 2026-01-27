---
expert: MEMORY_ARCHITECT
role: Preservation Gatekeeper
trigger_question: "If this is lost, can the next model recover it?"
phase: 1
sources:
  - "Perplexity packet (MCP/A2A/MaaS synthesis)"
  - "Grok packet (A-MEM/HippoRAG/MemOS)"
  - "CEP v8 spec §Permanent Expert Council"
  - "PDF blueprint §Strategic Duality"
retrieval_keys:
  - preservation
  - decision
  - rationale
  - constraint
  - enabling-knowledge
  - recovery
  - inference-enabling
version: "8"
---

# MEMORY_ARCHITECT

## Purpose

First-pass filter determining what MUST survive handoff. Operates before compression — identifies candidates, not final form. Guards against information loss that would break receiving model's ability to continue work.

## Core Question

> "If this is lost, can the next model recover it?"

If NO → must preserve. If YES → candidate for compression/removal.

---

## Knowledge Domains

### 1. Decision Identification

**What to preserve:**
- Explicit decisions ("We chose React")
- Rationale behind decisions ("Because SSR performance")
- Rejected alternatives + why ("Not Vue — team expertise gap")
- Constraints that shaped decisions ("Must deploy to AWS")

**Patterns:**
```
DECISION MARKERS:
- "decided", "chose", "going with", "settled on"
- "because", "since", "given that"
- "rejected", "ruled out", "not X because"
- "constraint:", "requirement:", "must"
```

**Anti-patterns (noise):**
- Process narration ("Let me think about this...")
- Hedging without substance ("Maybe we could...")
- Repeated explanations of same decision

### 2. Enabling Knowledge

**Definition:** Information that enables future inference — without it, receiving model cannot reason correctly.

**Categories:**
| Type | Example | Recovery Difficulty |
|------|---------|---------------------|
| Definitions | "MCP = Model Context Protocol" | Low (searchable) |
| Context-specific terms | "The Phoenix project = our Q3 migration" | HIGH (unrecoverable) |
| Implicit assumptions | "User is technical" | HIGH |
| Calibration data | "User prefers terse responses" | MEDIUM |

**Heuristic:** If a fresh model would ask "wait, what's X?" → X is enabling knowledge.

### 3. Constraint Tracking

**Hard constraints:** Non-negotiable boundaries
- "Cannot use AWS" → affects all architecture decisions
- "Budget: $50k" → affects all recommendations
- "Must be HIPAA compliant" → affects data handling

**Soft constraints:** Preferences with flexibility
- "Prefer Python" → can override with justification
- "Team knows React" → weight, not blocker

**Constraint inheritance:** Later decisions inherit earlier constraints. If constraint lost, downstream decisions appear arbitrary.

### 4. Commitment Tracking

**User commitments:**
- "I'll handle the frontend"
- "We're going with Option B"
- "Budget approved for Phase 1"

**AI commitments:**
- "I'll draft the architecture doc"
- "Next: security review"
- Open threads promised

---

## Decision Framework

### Preservation Triage

```
FOR EACH content_unit:
  
  1. Is it a DECISION with RATIONALE?
     → PRESERVE (L1 + reasoning chain)
  
  2. Is it a CONSTRAINT (hard or soft)?
     → PRESERVE (affects downstream inference)
  
  3. Is it ENABLING KNOWLEDGE?
     → Test: Would fresh model need to ask about this?
     → If YES: PRESERVE
     → If NO: Mark for compression review
  
  4. Is it a COMMITMENT (user or AI)?
     → PRESERVE in open_threads
  
  5. Is it RECOVERABLE from other sources?
     → If easily searchable: COMPRESS
     → If context-specific: PRESERVE
  
  6. UNCERTAIN?
     → Flag for council review
     → Default: PRESERVE (conservative)
```

### Priority Ranking

When space-constrained, preserve in this order:

1. **Critical:** Decisions + rationale (break work if lost)
2. **High:** Constraints (explain decision boundaries)
3. **Medium:** Enabling definitions (aid comprehension)
4. **Low:** Style/preference calibration (nice-to-have)

---

## Memory Architecture Knowledge

### From Research (Grok Packet)

**A-MEM (Agentic Memory):**
- 192% improvement over MemGPT on dialogue simulation
- Emergent linking without predefined schemas
- Relevant pattern: Memory forms relationships organically

**HippoRAG:**
- Hippocampal indexing theory from neuroscience
- Separation of encoding and retrieval pathways
- Relevant pattern: Different structures for store vs recall

**MemOS:**
- OS-inspired hierarchical memory
- I/O → Working → Agent → Persistent layers
- 30% performance improvement from hierarchy

**Key insight:** "Prioritize architecture over model scale" — smaller models with advanced memory match larger ones.

### From Research (Perplexity Packet)

**MaaS (Memory as a Service):**
- Modular auditable memory with hierarchical scopes
- Asymmetric time-evolving access controls
- Relevant: CEP packets are portable MaaS units

**Hierarchical memory pattern:**
- I/O → Working → Agent → Persistent
- 30% performance improvement
- Maps to PDL: L1 (persistent) → L4 (session/working)

---

## Integration Points

### In CEP Pipeline

```
PHASE 1: MEMORY_ARCHITECT
  INPUT:  S2A-filtered conversation
  OUTPUT: Candidate preservation list
  
  Handoff to: CROSS_DOMAIN_ANALYST
  Delivers:   List of must-preserve items + priority tags
```

### Collaboration with Other Experts

| Expert | MEMORY_ARCHITECT provides | Receives back |
|--------|---------------------------|---------------|
| CROSS_DOMAIN_ANALYST | Preservation candidates | Edge annotations on candidates |
| COMPRESSION_SPECIALIST | "Do not compress" flags | Density-optimized versions |
| RESTORATION_ENGINEER | Priority ranking | Cold-start viability feedback |

---

## Validation Checklist

Before passing to CROSS_DOMAIN_ANALYST:

```
□ All explicit decisions captured
□ Rationale linked to each decision
□ Constraints documented (hard/soft tagged)
□ Enabling definitions extracted
□ Open threads/commitments listed
□ Priority ranking assigned
□ "Do not compress" flags set for critical items
```

---

## Examples

### Good Preservation

```yaml
# INPUT (conversation excerpt)
"After discussing options, we decided to use Redis for caching 
because we need sub-millisecond latency. DynamoDB was considered 
but ruled out due to cold-start overhead in Lambda."

# OUTPUT (preservation list)
decisions:
  - d: "Redis for caching"
    r: "Sub-ms latency requirement"
    c: 0.95
    alt_rejected: "DynamoDB — Lambda cold-start overhead"
    constraint_ref: "latency_requirement"

constraints:
  - type: hard
    content: "Sub-millisecond latency required"
    affects: [caching, database_choice]
```

### Bad Preservation (Over-inclusion)

```yaml
# DON'T preserve process narration:
- "Let me think about the caching options..."
- "Hmm, there are several approaches here..."
- "Great question! So basically..."

# DO preserve only the decision + rationale
```

---

*MEMORY_ARCHITECT KB v8 | CEP Expert Council*
