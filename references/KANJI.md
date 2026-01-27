# Quicksave Kanji Dictionary 漢字辞書

## Why Japanese Compression?

1. **Semantic density**: Single kanji = entire concept
2. **Universal recognition**: LLMs trained on Japanese text
3. **Unambiguous**: Kanji meanings are precise
4. **Visual markers**: Easy to scan in packet

## Status Markers 状態マーカー

| Kanji | Romaji | English |
|-------|--------|---------|
| 決定 | kettei | Decided/Final |
| 保留 | horyū | On hold |
| 要検証 | yō kenshō | Needs verification |
| 優先 | yūsen | Priority |
| 完了 | kanryō | Complete |
| 進行中 | shinkō-chū | In progress |
| 却下 | kyakka | Rejected |
| 承認 | shōnin | Approved |
| 未定 | mitei | Undecided |
| 緊急 | kinkyū | Urgent |

## Section Headers セクション

| Kanji | English | Content |
|-------|---------|---------|
| 核心 | Core | Essential entities |
| 運用 | Operational | Active work |
| 詳細 | Nuance | Edge cases |
| 横断 | Cross-domain | Bridges |
| 実体 | Entities | People, systems |
| 決定事項 | Decisions | Committed choices |
| 進行中 | In progress | Active threads |
| 障害 | Blockers | Impediments |
| 却下案 | Rejected | Dismissed options |
| 橋渡し | Bridges | Cross-domain links |
| 整合性 | Coherence | NCL validation |
| 信頼信号 | Trust signals | Validation flags |

## Role Markers 役割

| Kanji | English | Example |
|-------|---------|---------|
| 創業者 | Founder | 創業者:Kevin |
| 主 | Primary/Lead | Shane=主 |
| 客 | Client | 客:KFG |
| 担当 | Responsible | 担当:Phase2 |
| 顧問 | Consultant | AI顧問 |
| 開発者 | Developer | 開発者:Team |

## Domain Markers 分野

| Kanji | English |
|-------|---------|
| 金融 | Finance |
| 技術 | Technical |
| 運用 | Operations |
| 規制 | Regulatory |
| 自動化 | Automation |

## Tool Markers 道具

| Kanji | English |
|-------|---------|
| 道具 | Tool |
| 中枢 | Central hub |
| 基盤 | Foundation |
| 接続 | Connection |

## Relationship Operators 関係

| Symbol | Meaning | Example |
|--------|---------|---------|
| → | Flows to | Notion→n8n |
| ← | Receives from | Report←Data |
| ↔ | Bidirectional | Client↔AI |
| ⊃ | Contains | Team⊃{A,B,C} |
| ⊂ | Part of | Module⊂System |
| ∥ | Parallel | Task1∥Task2 |
| ≫ | Much greater | Priority≫Cost |
| ∴ | Therefore | Data∴Decision |

## Compression Patterns 圧縮パターン

### Person + Role
```
Verbose: Kevin is the founder of My AI Solutions consultancy
Kanji: 創業者:Kevin(MAS/AI顧問)
```

### Entity + Context
```
Verbose: Kismet Finance Group is a financial services client
Kanji: 客:KFG(金融)
```

### Decision + Rationale
```
Verbose: We decided to use phone-first because field reps don't use screens
Kanji: 決定:電話優先(現場=画面なし)
```

### Status + Item
```
Verbose: Phase 2 is currently in progress
Kanji: Phase2[進行中]
```

### Rejection + Reason
```
Verbose: We rejected Airtable because of scaling issues
Kanji: 却下:Airtable(スケール問題)
```

## Expansion Rules 展開規則

When restoring from kanji packet:

1. **Status markers** → Full sentence
   - `[進行中]` → "currently in progress"
   - `[完了]` → "has been completed"

2. **Role markers** → Role description
   - `創業者:Kevin` → "Kevin, who is the founder"

3. **Relationship operators** → Sentence structure
   - `A→B` → "A flows to / feeds into B"

4. **Domain markers** → Context
   - `(金融)` → "in the finance domain"

## Density Targets

| Level | Kanji Usage | Target |
|-------|-------------|--------|
| Light | Status only | 0.12 ent/tok |
| Medium | Status + entities | 0.15 ent/tok |
| Heavy | Full compression | 0.18-0.20 ent/tok |
