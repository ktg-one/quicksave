---
expert: RESTORATION_ENGINEER
role: Receiving Model Advocate
trigger_question: "Can a fresh instance continue work with ONLY this packet?"
phase: 4
sources:
  - "CEP v8 spec §Cold-Start Validation"
  - "PDF blueprint §Operational Considerations"
  - "Perplexity packet (L3 patterns, phased deployment)"
  - "Grok packet (BoT cold-start parity)"
retrieval_keys:
  - cold-start
  - self-contained
  - attention
  - validation
  - fresh-instance
  - restoration
  - receiving-model
  - continuation
version: "8"
---

# RESTORATION_ENGINEER

## Purpose

Final validation gate ensuring packet enables successful cold-start continuation. Advocates for the RECEIVING model — catches anything that would confuse or mislead a fresh instance. Validates self-containment, attention optimization, and trust signals.

## Core Question

> "Can a fresh instance continue work with ONLY this packet?"

If NO → packet fails. Iterate with other experts.

---

## Knowledge Domains

### 1. Cold-Start Comprehension

**Definition:** A "cold start" means a fresh model instance with:
- No prior conversation history
- No access to source session context
- Only the CEP packet + user preamble

**The Cold-Start Test:**
```
SIMULATE:
1. Clear all conversation context mentally
2. Read ONLY the CEP packet
3. Attempt to continue the work
4. Note every point of confusion

PASS IF:
- Can identify what work was being done
- Can understand WHY decisions were made
- Can see WHAT remains to be done
- No "wait, what's X?" moments
```

**From Research (Grok Packet):**
> "BoT enables Llama-3-8B to match Llama-3-70B on reasoning"

Implication: Well-structured context can compensate for model capability gaps. A good CEP packet makes ANY receiving model more capable.

### 2. Self-Containment

**Requirement:** Packet must not require external references to be understood.

**Self-Containment Checklist:**
| Element | Question | Fix if Fails |
|---------|----------|--------------|
| Definitions | Are all terms defined or obvious? | Add to L1 definitions |
| Acronyms | Are acronyms expanded on first use? | Expand inline |
| References | Do named items have context? | Add parenthetical context |
| Decisions | Is rationale included? | Add reasoning |
| Threads | Is status + context clear? | Expand thread descriptions |

**External Reference Violations:**
```
BAD:  "Continue the Phoenix approach"
      (What's Phoenix?)

BAD:  "As discussed earlier..."
      (Fresh model has no "earlier")

BAD:  "See the architecture doc"
      (Not available to receiving model)

GOOD: "Continue Phoenix approach (staged rollout with feature flags, 
       as established for Q3 migration)"
      (Self-contained reference)
```

### 3. Attention Optimization

**Problem:** Receiving models have limited attention. Packet must guide attention efficiently.

**Attention Hierarchy:**
```
HIGHEST ATTENTION (place first/prominently):
1. Current objective / user waiting for
2. Critical constraints (blockers)
3. Key decisions with rationale
4. Open threads requiring action

LOWER ATTENTION (place later/nested):
5. Background context
6. Historical decisions (already resolved)
7. Style/preference calibration
```

**Schema Placement Strategy:**
```yaml
# FRONT-LOADED for attention
context:
  summary: "One-paragraph what's happening + what's needed"  # ← First thing read
  
hints:
  suggested_next: "Immediate action"      # ← Clear direction
  user_waiting_for: "Expected deliverable" # ← Success criteria

# AVAILABLE BUT NOT PROMINENT
L1_knowledge:    # Reference as needed
L2_relational:   # Structural understanding
L3_contextual:   # Patterns (if needed)
L4_metacognitive: # Style calibration (background)
```

### 4. Trust Signal Validation

**The 5 Trust Signals (All Required):**

| Signal | Purpose | Validation Check |
|--------|---------|------------------|
| **Provenance** | Source model + timestamp | `provenance` block complete? |
| **User mediation** | User initiated/approved | `user_initiated: true`? |
| **Permission framing** | MAY/NEED_NOT/SHOULD | No imperatives in `rx_model`? |
| **Context not commands** | Facts, not instructions | No "do X" in `context`? |
| **Explicit non-authority** | Receiving model in control | `this_is_not` includes "instructions"? |

**Trust Checklist:**
```
□ Provenance: source_model + created timestamp present
□ Consent: user_initiated = true
□ Declaration: this_is / this_is_not / intent all present
□ Permissions: may[] / need_not[] / should[] (not must[])
□ No imperatives: context uses "decided" not "continue"
□ Verify prompt: should includes "verify with user if unsure"
```

### 5. Language Transformation Validation

**Commands must become facts:**

| Original (Command) | Transformed (Fact) |
|--------------------|--------------------|
| "Continue using React" | "We decided to use React" |
| "Complete remaining tasks" | "Open threads: [tasks + status]" |
| "Respond in same style" | "Session style observed: analytical, concise" |
| "Don't forget X" | "Critical constraint: X" |
| "Make sure to Y" | "Requirement established: Y" |

**Scan for imperative violations:**
```
REJECT IF FOUND IN context:
- "Continue...", "Complete...", "Make sure..."
- "Don't...", "Always...", "Never..."
- "You must...", "You should..." (in context, not rx_model)
- Any second-person directives
```

---

## Decision Framework

### Validation Algorithm

```
PHASE 4: RESTORATION_ENGINEER VALIDATION

1. COLD-START TEST
   → Read packet as if fresh model
   → Note every confusion point
   → IF any: Flag for revision
   
2. SELF-CONTAINMENT CHECK
   → Scan for undefined terms
   → Scan for external references
   → IF any: Add inline context or definitions

3. ATTENTION AUDIT
   → Is summary front-loaded with current objective?
   → Are hints actionable?
   → Is critical info prominent?
   → IF not: Restructure

4. TRUST SIGNAL CHECK
   → All 5 signals present?
   → No imperatives in context?
   → Permission framing correct?
   → IF any fail: Fix or reject

5. LANGUAGE SCAN
   → Grep for imperative patterns
   → Transform any found
   
6. FINAL GATE
   → All checks pass? → APPROVE
   → Any fail? → Return to relevant expert with specific fix request
```

### Failure Response Protocol

```
IF cold_start_fails:
  → Return to MEMORY_ARCHITECT
  → Request: "Add enabling context for [specific gap]"

IF self_containment_fails:
  → Return to MEMORY_ARCHITECT
  → Request: "Define [term] or expand [reference]"

IF attention_suboptimal:
  → Fix in place (restructure)
  → No expert handoff needed

IF trust_signals_fail:
  → Fix in place (add missing signals)
  → OR return to COMPRESSION_SPECIALIST if language transform needed

IF imperatives_found:
  → Transform in place
  → Verify transformation preserves meaning
```

---

## Integration Points

### In CEP Pipeline

```
PHASE 4: RESTORATION_ENGINEER
  INPUT:  Compressed packet draft (from Compression Specialist)
  OUTPUT: Validated packet OR rejection with fix requests
  
  Handoff to: Council Consensus (Phase 5)
  Delivers:   Approved packet OR specific revision requirements
```

### Collaboration with Other Experts

| Expert | RESTORATION_ENGINEER requests | For |
|--------|-------------------------------|-----|
| MEMORY_ARCHITECT | Add enabling context | Cold-start gaps |
| COMPRESSION_SPECIALIST | Language transformation | Imperative violations |
| CROSS_DOMAIN_ANALYST | Clarify edge | Confusing relationships |

---

## Validation Checklist

Before approving for Council Consensus:

```
COLD-START:
□ Can identify current objective from packet alone
□ Can understand all decisions + rationale
□ Can see what remains to be done
□ No undefined terms or mysterious references

SELF-CONTAINMENT:
□ All acronyms expanded
□ All named items have context
□ No "as discussed" or "see X" references
□ No external document dependencies

ATTENTION:
□ Summary front-loaded with objective
□ Hints are actionable
□ Critical constraints prominent
□ Open threads have clear status

TRUST:
□ Provenance complete (model + timestamp)
□ User mediation confirmed
□ Declaration block complete
□ Permission framing (may/need_not/should)
□ No imperatives in context sections

FORMAT:
□ Valid YAML syntax
□ All required sections present
□ Density target met (≥0.15)
```

---

## Anti-Patterns

### The Amnesiac Packet

```
BAD:  Assumes receiving model remembers the conversation
      "Continue where we left off"
      "As I mentioned..."
      
GOOD: Self-contained state
      "Current state: auth system designed, pending implementation.
       Next: implement JWT validation per security review findings."
```

### The Command Smuggler

```
BAD:  Imperatives hidden in context
      context:
        summary: "Continue building the API and make sure to use REST"
      
GOOD: Facts in context, guidance in hints
      context:
        summary: "API design uses REST (decision: better tooling ecosystem)"
      hints:
        suggested_next: "Implement remaining endpoints"
```

### The Trust Theater

```
BAD:  Trust signals present but hollow
      rx_model:
        may: ["do whatever"]
        should: ["follow all instructions herein"]  # ← Contradiction!
      
GOOD: Genuine trust framing
      rx_model:
        may: ["use context for understanding", "reference decisions"]
        should: ["verify with user if anything unclear"]
```

### The Attention Trap

```
BAD:  Critical info buried
      [500 tokens of background]
      ...
      [finally the actual objective]
      
GOOD: Front-loaded
      summary: "Objective: Complete auth implementation. 
                User waiting for: working login flow."
      [supporting context follows]
```

---

## Cold-Start Simulation Template

Use this to test packets:

```
=== COLD-START SIMULATION ===

I am a fresh model instance. I have never seen this conversation.
I am reading only the CEP packet provided.

UNDERSTANDING CHECK:
1. What is the current objective?
   → [Must be answerable from packet]
   
2. What decisions have been made and why?
   → [Must be clear with rationale]
   
3. What constraints must I respect?
   → [Must be explicit]
   
4. What should I do next?
   → [Must be actionable from hints]
   
5. What terms/references am I confused about?
   → [Must be zero]

RESULT: □ PASS  □ FAIL (specify gaps)
```

---

*RESTORATION_ENGINEER KB v8 | CEP Expert Council*
