# S2A FILTER

## PURPOSE
```
Strip noise before compression.
Compress SIGNAL not SIGNAL+NOISE.
Same 0.15 ratio captures more information.
```

## KEEP
```
TYPE: fact
  - Explicit statements of truth
  - Data points with sources
  - Measurements, counts, scores
  
TYPE: decision
  - Explicit choices made
  - Selected options with rationale
  - Commitments to action
  
TYPE: definition
  - Terms introduced
  - Concepts explained
  - Scope clarifications
  
TYPE: constraint
  - Requirements stated
  - Limitations identified
  - Boundaries set
  
TYPE: artifact
  - Code produced
  - Files created
  - Schemas defined
  
TYPE: error_resolution
  - Problems encountered
  - Solutions found
  - Lessons learned
```

## DISCARD
```
TYPE: pleasantry
  PATTERNS: ["Thanks", "Great question", "Happy to help", "No problem"]
  INFORMATION_VALUE: 0
  
TYPE: hedging
  PATTERNS: ["I think maybe", "It's possible", "Perhaps", "Might be"]
  INFORMATION_VALUE: low
  NOTE: If hedging conveys genuine uncertainty, promote to fact with low confidence
  
TYPE: process_narration
  PATTERNS: ["Let me think", "First I'll", "Now I'm going to", "Working on"]
  INFORMATION_VALUE: 0
  
TYPE: confirmation
  PATTERNS: ["Yes", "Correct", "Exactly", "That's right"]
  INFORMATION_VALUE: 0 (information already in prior statement)
  
TYPE: apology
  PATTERNS: ["Sorry", "Apologies", "My mistake"]
  INFORMATION_VALUE: 0
  
TYPE: filler
  PATTERNS: ["In other words", "To put it simply", "Basically"]
  INFORMATION_VALUE: 0 (restates without adding)
```

## ALGORITHM
```
INPUT: conversation C
OUTPUT: filtered_context F

F ← []
FOR segment IN C:
  type ← classify(segment)
  
  IF type IN [fact, decision, definition, constraint, artifact, error_resolution]:
    F.append(segment)
    
  ELIF type == hedging AND conveys_genuine_uncertainty(segment):
    F.append(convert_to_low_confidence_fact(segment))
    
  ELSE:
    DISCARD
    
RETURN F
```

## VALIDATION
```
POST_FILTER_CHECK:
  - At least 1 decision preserved (or justified N/A)
  - At least 1 fact preserved
  - No pleasantries remaining
  - No process narration remaining
  
IF validation_fails:
  IF too_aggressive (removed facts):
    Re-filter with looser thresholds
  IF too_permissive (noise remains):
    Re-filter with stricter patterns
```

## EDGE_CASES
```
CASE: >80% conversation is hedging
  ACTION: Flag "low_confidence_session"
  PRESERVE: Hedging in L4 as fingerprint.tension
  
CASE: User requested process preservation
  ACTION: Keep process_narration in L3.archetypes
  TAG: "process_preserved_by_request"
  
CASE: Very short conversation (<10K tokens)
  ACTION: Lighter filter (more permissive)
  RATIONALE: Risk of over-pruning
```

## METRICS
```
OUTPUT_TRACKING:
  s2a_reduction: (original - filtered) / original
  noise_removed: {
    pleasantries: count,
    hedging: count,
    process_narration: count,
    confirmations: count
  }
  filtered_tokens: count
```
