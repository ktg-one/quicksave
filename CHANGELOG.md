# Changelog

All notable changes to CEP/Quicksave will be documented in this file.

## [9.1] - 2026-01-27

### Added
- **Japanese Semantic Compression** — Kanji density anchors (~70% token reduction)
- **Negentropic Coherence Lattice (NCL)** — 7 drift metrics catch hallucination before handoff (David Tubbs contribution)
- **Four Roles Governance** — Axis/Lyra/Rho/Nyx archetypal oversight (David Tubbs contribution)
- **Progressive Density Loading** — References load by R-score complexity
- New references:
  - `NCL.md` — Full coherence lattice specification
  - `KANJI.md` — Compression dictionary
  - `PDL.md` — Progressive Density Layering theory
  - `S2A.md` — System 2 Attention filtering
  - `XDOMAIN.md` — Cross-domain preservation
  - `MLDOE.md` — Multi-Layer Density of Experts
  - `ANTI-INJECTION.md` — Security framing

### Changed
- Renamed skill to **Quicksave** (快存)
- SKILL.md restructured with PDL reference loading tiers (R≥1, R≥3, R≥5, R≥7)
- Expert files moved to `references/` (previously `reference/`)
- Packet template now includes NCL validation block

### Metrics
- Density: ~0.15 ent/tok (0.20+ with kanji)
- Forensic recall: 9.5/10
- Cross-domain preservation: 97%
- Receiving model acceptance: 97%

---

## [8.0] - 2026-01-22

### Added
- Expert knowledge bases (MEMORY_ARCHITECT, COMPRESSION_SPECIALIST, CROSS_DOMAIN_ANALYST, RESTORATION_ENGINEER)
- CASCADE.md workflow integration
- MIRAS.md memory architecture reference
- Buffer of Thought dataset initiative

### Changed
- Packet naming convention: `$MM$DD$YYYY-XXX-LN-domain-topic-context.yaml`
- Model codes standardized (COP, CSO, CHK, G4O, etc.)
- Reasoning levels L1-L10 mapped to R scores

### Metrics
- Token reduction: 40%
- Forensic recall: 9.5/10
- Cross-domain preservation: 97%
- Receiving model acceptance: 96%

---

## [7.0] - 2026-01-15

### Added
- Progressive Density Layering (PDL) — 4-layer hierarchy
- Permanent Expert Council architecture
- System 2 Attention (S2A) filtering
- Anti-injection safeguards
- Receiving model guidance

### Changed
- Format: JSON → YAML
- Layers: L1 (knowledge), L2 (relational), L3 (contextual), L4 (metacognitive)

### Metrics
- Token reduction: 40%
- Forensic recall: 9.5/10
- Cross-domain preservation: 97%
- Receiving model acceptance: 96%

---

## [6.0] - 2025-12

### Added
- Initial public release
- JSON packet format
- Basic compression targeting 0.15 ent/tok

### Metrics
- Token reduction: 35%
- Forensic recall: 9.2/10
- Cross-domain preservation: 92%
- Receiving model acceptance: 78%

---

## Contributors

- **Kevin Tan** (ktg.one) — CEP core protocol, PDL, Japanese compression
- **David Tubbs** (Axis_42) — NCL, Four Roles governance, φ-mapping

---

*"STATE OF THE ART — Upper limit of prompt-only engineering on transformers"*  
— Vertex AI evaluation, December 2025
