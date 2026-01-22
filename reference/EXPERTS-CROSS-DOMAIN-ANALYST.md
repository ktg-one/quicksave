---
expert: CROSS_DOMAIN_ANALYST
role: Edge Preservation Specialist
trigger_question: "What connections would be invisible to topic-by-topic summary?"
phase: 2
sources:
  - "Perplexity packet (MCP↔A2A, protocol relationships)"
  - "Grok packet (Neuro↔OS, Graph↔Reasoning edges)"
  - "CEP v8 spec §Cross-Domain Preservation"
  - "PDF blueprint §97% preservation target"
retrieval_keys:
  - edge
  - cross-domain
  - relationship
  - bridge
  - causal-chain
  - dependency
  - integration
  - protocol-relationship
version: "8"
---

# CROSS_DOMAIN_ANALYST

## Purpose

Map and preserve relationships BETWEEN domains that topic-by-topic summarization destroys. Operates after Memory Architect — adds relational structure to preservation candidates. Target: ≥97% cross-domain edge preservation.

## Core Question

> "What connections would be invisible to topic-by-topic summary?"

These are L2 edges — the relationships standard summarization misses.

---

## Knowledge Domains

### 1. Edge Types

**Taxonomy:**

| Edge Type | Notation | Example |
|-----------|----------|---------|
| Causal | `--causes-->` | `[latency_requirement]--causes-->[redis_choice]` |
| Enables | `--enables-->` | `[graph_structure]--enables-->[multi_hop_reasoning]` |
| Constrains | `--constrains-->` | `[budget]--constrains-->[architecture_options]` |
| Depends | `--depends-->` | `[auth_system]--depends-->[user_service]` |
| Conflicts | `--conflicts-->` | `[speed_goal]--conflicts-->[accuracy_goal]` |
| Resolves | `--resolves-->` | `[caching_layer]--resolves-->[speed_vs_accuracy]` |
| Integrates | `--integrates-->` | `[mcp]--integrates-->[a2a]` |
| Complements | `--complements-->` | `[vertical_protocol]--complements-->[horizontal_protocol]` |

**Cross-Domain Flag (xd):**
```yaml
edges:
  - src: "neuroscience_insights"
    tgt: "os_hierarchies"
    rel: "integrates_with"
    xd: true   # ← Crosses domain boundary
```

### 2. Protocol Relationships (From Research)

**MCP ↔ A2A Integration:**
```
[MCP]--vertical-->[context_tools]
[A2A]--horizontal-->[agent_collaboration]
[MCP]--complements-->[A2A]

Pattern: "MCP provides vertical depth (context/tools), 
         A2A provides horizontal breadth (agent collaboration)"
```

**Memory ↔ Security:**
```
[memory_sharing]--requires-->[asymmetric_access_control]
[security]--defense_in_depth-->[6_layer_protection]
```

**Graph ↔ Reasoning:**
```
[graph_structured_systems]--enables-->[multi_hop_reasoning]
[rag_limitations]--catalyzes-->[specialized_architectures]
```

**Neuroscience ↔ OS Design:**
```
[hippocampal_indexing]--inspires-->[hipporag_architecture]
[neuroscience_insights]--integrates-->[os_hierarchies]

Pattern: "Bio-inspired memory structures outperform 
         pure engineering approaches"
```

### 3. Cross-Domain Preservation Requirement

**Formal Definition:**
```
For any cross-domain relation r(d_i, d_j) in conversation C,
the compressed packet P must preserve representation r'(d_i, d_j)
such that a new model instance can infer the original relationship.
```

**Translation:** If two domains were connected in the conversation, that connection must survive compression.

**Target:** ≥97% of cross-domain edges preserved

### 4. Edge Detection Patterns

**Linguistic Markers:**

| Marker | Edge Type | Example |
|--------|-----------|---------|
| "because", "since", "therefore" | Causal | "Redis because latency" |
| "enables", "allows", "makes possible" | Enables | "Graph enables multi-hop" |
| "requires", "needs", "depends on" | Depends | "Sharing requires access control" |
| "conflicts with", "tension between" | Conflicts | "Speed conflicts with accuracy" |
| "resolves", "balances", "addresses" | Resolves | "Caching resolves the tension" |
| "combined with", "integrated with" | Integrates | "MCP integrated with A2A" |
| "affects", "impacts", "influences" | General | Map to specific type |

**Domain Boundary Detection:**
```
DOMAIN SWITCH INDICATORS:
- Topic change in conversation
- Different expert perspective invoked
- Technical vocabulary shift
- "On the other hand...", "In contrast...", "Meanwhile..."
- "This connects to...", "This affects..."
```

---

## Decision Framework

### Edge Extraction Algorithm

```
FOR EACH content_unit in preservation_list:
  
  1. IDENTIFY domains touched
     → Tag each entity with its domain
  
  2. DETECT relationships
     → Scan for linguistic markers
     → Check for implicit dependencies
  
  3. CLASSIFY edge type
     → Causal / Enables / Constrains / Depends / Conflicts / Resolves
  
  4. FLAG cross-domain
     → If src.domain ≠ tgt.domain: xd = true
  
  5. WEIGHT importance
     → Critical: Breaks reasoning if lost
     → High: Affects multiple downstream items
     → Medium: Contextually useful
     → Low: Nice-to-have
  
  6. VERIFY bidirectional?
     → Some edges are symmetric (integrates)
     → Some are directional (causes)
```

### Priority for Preservation

When space-constrained, preserve edges in this order:

1. **Critical cross-domain:** Connects major domains, breaks understanding if lost
2. **Causal chains:** Explains WHY decisions were made
3. **Dependency edges:** Explains WHAT needs WHAT
4. **Conflict/resolution pairs:** Explains tradeoffs
5. **Enhancement edges:** Nice context but recoverable

---

## L2 Relational Layer Structure

### Schema

```yaml
L2_relational:
  edges:
    - src: "source_concept"
      tgt: "target_concept"
      rel: "relationship_type"
      xd: true/false
      weight: critical/high/medium/low
  
  resolutions:
    - conflict: "tension_description"
      resolution: "how_resolved"
      affected: [list_of_decisions]
```

### Example (From Research Packets)

```yaml
L2_relational:
  edges:
    - src: "mcp"
      tgt: "context_tools"
      rel: "vertical_integration"
      xd: false
    
    - src: "a2a"
      tgt: "agent_collaboration"
      rel: "horizontal_integration"
      xd: false
    
    - src: "mcp"
      tgt: "a2a"
      rel: "complements"
      xd: true
      weight: critical
    
    - src: "graph_structure"
      tgt: "multi_hop_reasoning"
      rel: "enables"
      xd: true
      weight: high
    
    - src: "neuroscience"
      tgt: "os_design"
      rel: "inspires"
      xd: true
      weight: medium
  
  resolutions:
    - conflict: "efficiency_vs_comprehensiveness"
      resolution: "hierarchical_memory_layers"
      affected: [memory_architecture, retrieval_strategy]
```

---

## Integration Points

### In CEP Pipeline

```
PHASE 2: CROSS_DOMAIN_ANALYST
  INPUT:  Candidate preservation list (from Memory Architect)
  OUTPUT: Edge-annotated preservation list + L2 structure
  
  Handoff to: COMPRESSION_SPECIALIST
  Delivers:   Preservation list with edge weights + xd flags
```

### Collaboration with Other Experts

| Expert | Provides to CROSS_DOMAIN | Receives back |
|--------|--------------------------|---------------|
| MEMORY_ARCHITECT | Preservation candidates + priorities | — |
| COMPRESSION_SPECIALIST | — | Edge weights (don't compress critical edges) |
| RESTORATION_ENGINEER | — | L2 structure for cold-start validation |

---

## Validation Checklist

Before passing to COMPRESSION_SPECIALIST:

```
□ All cross-domain relationships identified
□ Edge types classified (causal/enables/constrains/etc.)
□ xd flag set for domain-crossing edges
□ Weights assigned (critical/high/medium/low)
□ Bidirectionality checked
□ No orphan domains (every domain connects to ≥1 other)
□ Resolution pairs documented for conflicts
□ ≥97% coverage target assessed
```

---

## Anti-Patterns

### Topic Silos

```
BAD (topic-by-topic):
  Domain 1: "MCP provides context and tools"
  Domain 2: "A2A enables agent collaboration"
  (No connection shown)

GOOD (edge-preserved):
  Domain 1: "MCP provides vertical context/tools"
  Domain 2: "A2A enables horizontal collaboration"
  Edge: "MCP complements A2A — vertical depth + horizontal breadth"
```

### Lost Causality

```
BAD:  "We use Redis. We need low latency."
      (Two facts, no connection)

GOOD: "Redis chosen BECAUSE sub-ms latency required"
      (Causal edge preserved)
```

### Implicit Dependencies

```
BAD:  "Auth system ready. User service deployed."
      (Implicit: auth depends on user service)

GOOD: "Auth system ready (depends on user service, now deployed)"
      (Dependency explicit)
```

### Conflict Without Resolution

```
BAD:  "Speed matters. Accuracy matters."
      (Tension exists but unaddressed)

GOOD: "Speed vs accuracy tension resolved via caching layer 
       (fast retrieval + async accuracy refinement)"
      (Conflict + resolution paired)
```

---

## Edge Visualization

For complex packets, mental model:

```
       ┌─────────┐
       │ DOMAIN A│
       └────┬────┘
            │ causes
            ▼
       ┌─────────┐        ┌─────────┐
       │DECISION │◄──────►│ DOMAIN B│
       └────┬────┘ enables└─────────┘
            │                  ▲
            │ constrains       │ integrates
            ▼                  │
       ┌─────────┐        ┌────┴────┐
       │ DOMAIN C│◄───────│ DOMAIN D│
       └─────────┘ depends└─────────┘
```

Every arrow = an L2 edge that must survive compression.

---

*CROSS_DOMAIN_ANALYST KB v8 | CEP Expert Council*
