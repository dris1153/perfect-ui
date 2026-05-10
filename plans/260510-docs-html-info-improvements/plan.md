---
name: docs-html-info-improvements
status: completed
priority: medium
mode: fast
created: 2026-05-10
completed: 2026-05-10
target: index.html
blockedBy: []
blocks: []
---

# Plan — `index.html` info improvements

Add 4 new sections + inline expansions to `index.html` (perfect-ui skill docs page) while preserving editorial vibe (cream/ink/dusk-rose, Instrument Serif + Geist, asymmetric 12-col grid).

## Source of truth
[brainstorm.md](./brainstorm.md) — full specs, content, cohesion guardrails, risks.

## Context links
- Target file: [index.html](../../index.html) (779 lines)
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.0.0"`)
- Content sources: [README.md](../../README.md), [synthesis.md](../260509-ai-vs-human-analysis/synthesis.md)

## Goal
Page from 779 → ~1200 lines. 6 sections → 9 sections. No new fonts, no new accent colors, no anti-slop self-violations.

## Phases

| # | Phase | File | Status | Effort |
|---|-------|------|--------|--------|
| 01 | Inline fixes (low-risk isolated edits) | [phase-01-inline-fixes.md](./phase-01-inline-fixes.md) | completed | XS |
| 02 | Add "Why it exists" section | [phase-02-add-why-section.md](./phase-02-add-why-section.md) | completed | M |
| 03 | Add "Mandates" section | [phase-03-add-mandates-section.md](./phase-03-add-mandates-section.md) | completed | M |
| 04 | Add "In practice" section + tabs JS | [phase-04-add-examples-section-tabs.md](./phase-04-add-examples-section-tabs.md) | completed | L |
| 05 | Add "Beyond perfect-ui" section | [phase-05-add-beyond-section.md](./phase-05-add-beyond-section.md) | completed | S |
| 06 | Section number cascade + final audit | [phase-06-section-number-cascade.md](./phase-06-section-number-cascade.md) | completed | S |

## Final section order

```
Hero
01  Why it exists       ← NEW (phase 02)
02  Scope               (existing, renumbered)
03  Pipeline            (existing — phase ∞ card expanded in phase 01)
04  Vibes               (existing)
05  Anti-slop tiers     (existing)
06  Mandates            ← NEW (phase 03)
07  In practice         ← NEW (phase 04)
08  Getting started     (existing — CLI flags table added in phase 01)
09  Beyond perfect-ui   ← NEW (phase 05)
Footer
```

## Key dependencies

- Phases 01-05 are sequential by safety, not technical dependency. Each adds isolated content blocks.
- Phase 06 (number cascade) MUST run last — depends on all sections being in place.
- No external blockers. Self-contained `index.html` edit.

## Success criteria (overall)

- [x] All 4 new sections rendered (Why / Mandates / In practice / Beyond)
- [x] Section numbers sequential — Why · 02 Scope · 03 Pipeline · 04 Vibes · 05 Anti-slop · 06 Mandates · 07 In practice · 08 Getting started · 09 Beyond
- [x] Anti-slop self-audit clean — zero icon library imports, zero Tailwind anti-pattern classes, anti-pattern names only in quoted context
- [x] Tabs ARIA-compliant (role/aria-selected/keyboard nav) + no-JS fallback (CSS shows all panels when `.no-js` present)
- [x] No new font imports, no new accent colors
- [x] Page weight: 779 → 1243 lines (~+48.5KB total, well under target)
- [x] All inline fixes applied (version v2.0.0 in hero+footer, index.html filename, splash criteria, CLI flags table)

## Outcome

- File grew 779 → 1243 lines (~+59%)
- Section count 6 → 9 (+ Hero/Footer)
- 10 `<section>` open tags = 10 closing tags (structural integrity verified)
- Bonus fix: discovered + corrected second `v0.0.1` reference in footer (line 1066) not noted in original brainstorm
- All audit greps return zero violations
