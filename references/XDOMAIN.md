# XDOMAIN EXTRACTION

## PURPOSE
```
Preserve relations BETWEEN conceptual domains, not just facts WITHIN domains.
Standard summarization treats topics as isolated.
PDL preserves their connections.
```

## FORMAL
```
D = {d_1, d_2, ..., d_k}  // domains in conversation
C = conversation
P = compressed packet

CONSTRAINT:
  ∀ r(d_i, d_j) ∈ C WHERE i ≠ j:
    ∃ r'(d_i, d_j) ∈ P
    such that fresh_instance can infer original relationship

THRESHOLD: 0.95 preservation
```

## DETECTION_SIGNALS
```
EXPLICIT:
  - User says "X relates to Y because..."
  - Decision references multiple domains
  - Constraint spans domains

IMPLICIT:
  - Same entity appears in different domain contexts
  - Reasoning chain crosses domain boundaries
  - Conflict involves different-domain concepts

STRUCTURAL:
  - Concepts from D_i and D_j in same L2.edge
  - L1.decision.rationale references multiple domains
  - L3.archetype spans domains
```

## EXTRACTION_PROCEDURE
```
STEP_1: Identify domains
  SCAN C for topic clusters
  ASSIGN d_1..d_k labels
  
STEP_2: Map concepts to domains
  FOR each concept IN L1:
    ASSIGN primary domain
    FLAG if appears in multiple domains
    
STEP_3: Extract intra-domain edges
  FOR each domain d_i:
    EXTRACT relationships within d_i
    ADD to L2.edges with x=false
    
STEP_4: Extract cross-domain edges (CRITICAL)
  FOR each concept_pair (c_i, c_j):
    IF domain(c_i) ≠ domain(c_j):
      IF relationship_exists(c_i, c_j):
        EXTRACT relationship
        ADD to L2.edges with x=true
        MARK as high_priority (never prune)

STEP_5: Validate
  original_xdomain_count = count(C.cross_domain_relations)
  preserved_xdomain_count = count(P.L2.edges WHERE x=true)
  ratio = preserved / original
  
  IF ratio < 0.95:
    RE-SCAN C for missed cross-domain relations
    REPEAT STEP_4
```

## EXAMPLES
```
EXAMPLE_1:
  domains: [publication_strategy, imposter_syndrome]
  xdomain_relation: "fear of credential dismissal delays publication timing"
  
  L2.edge: {
    "s": "credential_anxiety",
    "t": "publication_timing", 
    "r": "delays",
    "x": true
  }
  
  WHY_MATTERS: Next session knows to push immediate publication despite anxiety

EXAMPLE_2:
  domains: [technical_architecture, business_requirements]
  xdomain_relation: "latency constraint drives cache decision"
  
  L2.edge: {
    "s": "50ms_latency_requirement",
    "t": "redis_cache_choice",
    "r": "requires",
    "x": true
  }
  
  WHY_MATTERS: Next session understands WHY redis, not just THAT redis

EXAMPLE_3:
  domains: [prompt_engineering, model_behavior]
  xdomain_relation: "CoD technique causes memory preservation"
  
  L2.edge: {
    "s": "chain_of_density",
    "t": "context_extension",
    "r": "enables",
    "x": true
  }
  
  WHY_MATTERS: Core insight that CEP is built on
```

## PRUNE_PROTECTION
```
L2.edges WHERE x=true:
  NEVER_PRUNE
  
RATIONALE:
  - Intra-domain edges recoverable from L1 facts
  - Cross-domain edges encode RELATIONSHIPS that facts alone don't capture
  - Fresh instance needs xdomain to understand WHY decisions connected
```

## VALIDATION_GATE
```
GATE_XDOMAIN:
  query: "cross_domain_preservation >= 0.95?"
  
  calc:
    original = scan(C).count(xdomain_relations)
    preserved = P.L2.edges.filter(x=true).count()
    ratio = preserved / original
    
  pass: ratio >= 0.95
  fail: 
    1. List missed xdomain relations
    2. Re-extract with explicit focus
    3. Re-validate
    4. If still fail after 2 iterations: tag "xdomain_partial" with achieved ratio
```
