# Phase 06 — Section number cascade + final audit

## Context links
- [brainstorm.md § Final order](./brainstorm.md)
- [plan.md § Final section order](./plan.md)
- Target: [index.html](../../index.html)

## Overview
- **Priority:** Critical (page coherence depends on correct numbering)
- **Status:** pending
- **Effort:** S (~20 minutes)
- **Description:** Update existing section labels to match new order, run final anti-slop self-audit, validate page end-to-end.

## Key insights
- This phase MUST run last — depends on all 4 new sections being inserted (phases 02-05).
- Numbering update = 4 label edits in existing sections.
- Final audit = grep + visual checks per brainstorm validation criteria.

## Requirements
- Functional: section labels sequential 01-09 matching new order.
- Functional: anti-slop self-audit clean.
- Non-functional: mobile + desktop pass visual smoke test.

## Architecture
**Edits:** 4 label number changes in existing sections.

| Section | Old label | New label |
|---|---|---|
| Scope | `— 01` (line 410) | `— 02` |
| Pipeline | `— 02` (line 448) | `— 03` |
| Vibes | `— 03` (line 547) | `— 04` |
| Anti-slop | `— 04` (line 656) | `— 05` |
| Getting Started | `— 05` (line 716) | `— 08` |

(Why section uses `— Why`, Mandates `— 06`, In practice `— 07`, Beyond `— 09` — set during their creation phases.)

## Related code files
- **Modify:** `d:\Workspace\dris1153\Personal\claude-skills\perfect-ui\index.html` (5 label number edits)
- **Read for verification:** all section blocks

## Implementation steps

### 1. Update section labels

Use Edit tool for each (replace_all=false since each is unique with surrounding context):

| # | Find context | Replace |
|---|---|---|
| 1 | `<span class="label">— 01</span>` near `<h2><em>Scope.</em>` | `<span class="label">— 02</span>` |
| 2 | `<span class="label">— 02</span>` near `<h2><em>Pipeline.</em>` | `<span class="label">— 03</span>` |
| 3 | `<span class="label">— 03</span>` near `<h2><em>Eleven vibes.</em>` | `<span class="label">— 04</span>` |
| 4 | `<span class="label">— 04</span>` near `<h2><em>Anti-slop.</em>` | `<span class="label">— 05</span>` |
| 5 | `<span class="label">— 05</span>` near `<h2><em>Getting started.</em>` | `<span class="label">— 08</span>` |

### 2. Anti-slop self-audit (grep checks)

Run these greps against final `index.html`. Each must return ZERO hits or only acceptable matches:

| Pattern | Expected | If hit | Action |
|---|---|---|---|
| `from 'lucide` / `from "lucide` | 0 | Real import | Remove |
| `from '@heroicons` | 0 | Real import | Remove |
| `purple-` (Tailwind class) | 0 | Real class | Replace with editorial accent |
| `from-purple` / `to-blue` (gradient) | 0 | Real gradient | Replace with palette tokens |
| `h-screen` (as Tailwind class, not text) | 0 | Real class | Replace with explicit min-height |
| Emoji unicode (e.g., U+1F300-1F9FF) | 0 | Real emoji | Replace with custom SVG |
| `Get Started` (CTA copy) | only as forbidden-pattern reference | Used as actual CTA copy | Replace with specific verb |
| `v0.0.1` | 0 | Phase 01 didn't run | Run phase 01 |
| `docs.html` | 0 | Phase 01 didn't run | Run phase 01 |

**Note:** Pattern names appearing in QUOTED context (within `.tier li`, `.why-col-ai li`, mandate descriptions) are documentation references — NOT violations. Audit checks for ACTUAL usage as Tailwind classes / imports / CTA labels.

### 3. Visual end-to-end smoke test

Open `file:///d:/Workspace/dris1153/Personal/claude-skills/perfect-ui/index.html` in browser:

**Desktop (≥1280px):**
- [ ] Hero renders correctly, version shows `v2.0.0`
- [ ] Section 01 (Why) — stat row + 2-col comparison panel + accent dot rule
- [ ] Section 02 (Scope) — handles + refuses 2-col
- [ ] Section 03 (Pipeline) — phase cards including expanded ∞ card with 3 bullets
- [ ] Section 04 (Vibes) — 11-row table
- [ ] Section 05 (Anti-slop) — 3 tier cards
- [ ] Section 06 (Mandates) — 4×2 mandate grid
- [ ] Section 07 (In practice) — tabs, default Coffee tab visible
- [ ] Section 08 (Getting started) — trigger phrases + Flags subsection + file structure
- [ ] Section 09 (Beyond) — 5-row table
- [ ] Footer renders correctly

**Mobile (<900px, browser DevTools mobile view):**
- [ ] All sections stack to single column
- [ ] Tab list becomes vertical pill list
- [ ] No horizontal scroll
- [ ] Comparison panel rule disappears
- [ ] Vibes table headers hidden (existing pattern)
- [ ] Mandate grid: 1-col at <600px or 2-col at 600-900px

**Interactivity:**
- [ ] Click each tab → correct panel shows
- [ ] Tab keyboard nav: Tab to focus → Arrow Left/Right cycles → Home/End jumps to ends
- [ ] Disable JS → all 3 tab panels visible, tab list hidden
- [ ] All anchor links resolve (README, SKILL)
- [ ] `.phase` and `.mandate` cards show accent border on hover

**Accessibility:**
- [ ] Tab `aria-selected` toggles correctly
- [ ] Focus visible (accent outline) on all interactive elements
- [ ] Headings hierarchy: H1 (hero) → H2 (sections) → H3 (sub-blocks). No skipped levels.

### 4. Final line count + page weight check

```bash
wc -l index.html  # target: 1100-1300
# weight via DevTools network tab — expect <70KB unminified (was ~30KB)
```

## Todo list
- [ ] 5 label number updates (Scope → 02, Pipeline → 03, Vibes → 04, Anti-slop → 05, Getting Started → 08)
- [ ] Run grep audit (9 patterns)
- [ ] Visual smoke test desktop
- [ ] Visual smoke test mobile
- [ ] Tab interactivity test
- [ ] No-JS fallback test
- [ ] Accessibility quick-check
- [ ] Line count + weight check

## Success criteria
- [ ] Section labels: 01 Why · 02 Scope · 03 Pipeline · 04 Vibes · 05 Anti-slop · 06 Mandates · 07 In practice · 08 Getting started · 09 Beyond
- [ ] All grep audits pass (zero hits or acceptable doc-reference matches only)
- [ ] Desktop: all 9 sections render correctly
- [ ] Mobile: no horizontal scroll, all sections accessible
- [ ] Tabs work + graceful no-JS degradation
- [ ] Page weight < +10KB unminified vs original
- [ ] No console errors when page loads

## Risk assessment
| Risk | Severity | Mitigation |
|---|---|---|
| Wrong label number applied (off-by-one) | Medium | Use specific context in find string (heading text included) so each Edit is unique |
| Phase 02-05 didn't run completely → cascade hits wrong line numbers | High | Phase 06 verifies all 4 new sections present BEFORE running label updates |
| Audit catches false-positive in documentation context | Low | Pattern context check — quoted/docs context OK, actual usage NOT OK. Documented in step 2. |
| Page weight exceeds budget | Low | New content is mostly text + reused styles. ~6-8KB expected, well under 10KB budget. |
| Browser rendering inconsistencies (Safari vs Chrome) | Low | All CSS uses widely-supported features (grid, flex, custom props). No experimental features. |

## Security considerations
- Final visual audit confirms no inline scripts other than the no-js class removal + tabs IIFE. Both are static, no user input, no XSS surface.
- Verify no external resources added beyond existing Google Fonts.

## Next steps
- Plan complete. Hand off to `ck:cook` for execution OR user implements manually phase by phase.
- Optional follow-up: add changelog entry to `docs/project-changelog.md` if project tracks changelog (none currently exists at that path — skip unless requested).
