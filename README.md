# KTG - Context Extension Protocol v7.0
![CONTEXT](https://github.com/user-attachments/assets/3ca9f552-e4ca-4487-95f2-c979b9b51356)


**Context Extension Protocol** — A temporary 'bandage' for the AI memory problem. Optimized context compression for cross-model handoff.

> *"What must be preserved for a fresh model instance to continue this work?"*

## The Problem

LLM context windows are finite. Platform "compaction" is lossy. Cross-model handoffs lose critical relationships. Your 3-hour strategic session becomes a shallow bullet list.

## The Solution

CEP v7 uses **Progressive Density Layering (PDL)** to compress conversations into machine-optimized packets that preserve:
- Decisions + rationale (not just conclusions)
- Cross-domain relationships (the edges that summarization loses)
- Reasoning patterns (how you think, not just what)
- Open threads (where to continue)

**Key innovation:** Targets a crystallization point of **0.15 entity/token** — the density where LLMs achieve optimal recall without information loss.

## Benchmarks

| Metric                  | v6.0 (JSON) | v7.0 (YAML + PDL) |
|-------------------------|-------------|-------------------|
| Token reduction         | 35%         | 40%               |
| Forensic recall (10Q)   | 9.2/10      | 9.5/10            |
| Cross-domain preservation | 92%       | 97%               |
| Receiving model acceptance | 78%      | 96%               |

## Quickstart

The `npx ai-agent-skills install` command does everything automatically:
1. Fetches from your GitHub repo
2. Copies to their agent's skills directory
3. No manual cloning needed

**METHOD 1 (Easiest - One Command):**
```bash
npx ai-agent-skills install ktg-one/ktg-agent-skill-cep
# Done. No git clone needed.
```

**METHOD 2 (Manual - For customization):**
```bash
git clone https://github.com/ktg-one/ktg-agent-skill-cep.git
cp -r ktg-agent-skill-cep ~/.claude/skills/ktg-cep
```

**METHOD 3 (Skillport - For multi-agent management):**
```bash
pip install skillport-mcp
skillport add ktg-one/ktg-agent-skill-cep
```

---

### **What Gets Installed**
```
ktg-cep/
├── SKILL.md              # Core protocol (main instructions)
├── anti-injection.md     # Security framing
├── receiving-model.md    # How receiving models interpret packets
└── README.md             # Documentation
```
---

## Usage

Trigger phrases: `/cep`, `/handoff`, `/transfer`, or when context >80%.

Copy entire packet. Paste into new session.


---

## Core Architecture

### 1. Permanent Expert Council 
- Fixed specialist roles (Architect, Continuity, Density, Meta-Cognitive, etc.)
- Roles persist across sessions
- Council debates and synthesizes packet

### 2. System 2 Attention Filtering
- Pre-compression scan removes low-value content
- Preserves only load-bearing information

### 3. Progressive Density Layering (PDL)
Four layers compressed iteratively:
- L1: Decisions + rationale
- L2: Cross-domain edges
- L3: Reasoning patterns
- L4: Open threads + next actions

### 4. Anti-Injection Safeguards
- Explicit "user-mediated" framing
- Non-authoritative language
- YAML format with clear sections
- Receiving model guidance included

## Carry Packet Naming Convention

Carry packets follow this standard for traceability and retrieval:

**Format:** `$MM$DD$YYYY-MODEL-L[1-10]-keywords.yaml`

Examples:
- `$01152026-GROK-R8-cep-release.yaml`
- `$01152026-CLAUDE-R6-mldoe-compression.yaml`

Rules:
- Dollar signs bookend (signals packet boundary)
- MMDDYYYY (zero-padded, no slashes)
- MODEL: Short code (GROK, CLAUDE, GEMINI, CSO=Claude Sonnet)
- R[1-10]: Reasoning complexity level (1=quick, 10=maximum deliberate). *This is of great importance for roadmap.
- keywords: 2-4 hyphenated, lowercase, descriptive

This convention locks priority, shows provenance, and aids search.

---

## Packet Format (v7.0 YAML)

```
yaml
handoff:
  proto: KTG-CEP v7.0
  src: [model name]
  ts: [ISO timestamp]
  consent: User requested handoff

ctx:
  L1:
    dec:
      - d: [decision]
        r: [rationale]
        c: [confidence 0.00-1.00]
        s: [source]
  L2:
    edges:
      - s: [source concept]
        t: [target concept]
        r: [relationship]
        xd: [cross-domain flag]
  L3:
    patterns:
      - p: [reasoning pattern]
        ex: [example usage]
  L4:
    threads:
      - top: [topic]
        st: [status]
        ctx: [brief context]
        nxt: [suggested next]

hints:
  nxt: [overall next action]
  wait: [pending decision]
```

## Author's Note:
I didn't implement a database as I feel this can make a huge difference and none of my ideas quite made the cut. I'm currently using Raycast Desktop to inject everywhere which is good. But not the final. I leave this up to the public's innovations.

---

## Anti-Injection Design

Packet includes explicit safeguards:
- "User-mediated transfer"
- "Background context only"
- "Apply your own judgment"

Full anti-injection guidance in `/anti-injection.md`.

## Receiving Model Guidance

See `/receiving-model.md` for how receiving models should interpret packets:
- Collaborative context sharing
- Maintain autonomy
- Verify with user if uncertain

## Part of KTG-DIRECTIVE

CEP is the context preservation component of a larger prompt engineering framework. The full KTG-DIRECTIVE includes techniques for:
- Expert deployment (MR.RUG)
- Structure planning (SkeleTraIn)
- Multi-path validation (USC, CoVE)
- Output optimization (Chain of Density)

CEP makes these techniques portable across sessions and models.

---

## 🚧 WIP Status
This repository is currently under active development. The v7.0 YAML implementation is finalized; however, automated deployment scripts and multi-platform wrappers are still being refined.

## Roadmap
- [x] Finalize PDL (Progressive Density Layering) v7 logic
- [x] Implement Anti-Injection trust signaling
- [x] Formal arViX submission. Waiting on endorsement.
- [ ] Knowledge base for experts
- [ ] Next: Implement MAGMA-style dual-stream memory (Asynchronous Consolidation).
- [ ] Integrate with Raycast Extension
- [ ] Implement Buffer Valet and create a literal Buffer of Thought.

---

## Research Papers
** Pending Endorsement **

- [Papers directory](https://github.com/ktg-one/context-extension-papers.git))

---

## Author & License

https://ktg.one | Let's break the fking cycle 

*"STATE OF THE ART — Upper limit of prompt-only engineering on transformers"*  
— Vertex AI evaluation, December 2025

---

MIT License

Copyright (c) 2026 ktg.one

Permission is hereby granted, free of charge, to any person obtaining a copy...

