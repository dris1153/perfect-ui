# Phase 05 — index.html cleanup + version bump

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Per-file change scope > HIGH
- [phase-03-skill-md-cleanup.md](./phase-03-skill-md-cleanup.md) — depends on (scope consistency)
- [260528-open-scope-page-types/phase-05-index-html-update.md](../260528-open-scope-page-types/phase-05-index-html-update.md) — prior plan that built current index.html structure (completed)
- [index.html](../../index.html) — file to modify (~1245 lines pre-edit, 14 ck: hits)

## Overview
- **Priority:** Medium-High (published docs page — visual face of skill)
- **Status:** pending
- **Depends on:** Phase 03 (scope decisions locked in SKILL.md)
- **Parallel-safe with:** Phase 04 (README — different file)
- **Description:** Remove ck:/ckm: from index.html (14 hits). Phase cards in § Pipeline mention "delegate to ck:brainstorm" / "ck:plan" / "ck:cook" / "code-reviewer agent". § Beyond reduced from 3 rows (post-v2.1.0) but ck-skill names need replacement. Hero + footer version 2.1.0 → 2.2.0.

## Key insights
- index.html has editorial vibe + ARIA tabs preserved — no structural changes, only content
- Anti-slop self-audit applies to this file — no emoji, no Inter/Roboto, no purple gradient, no h-screen, no inline hex outside CSS vars
- Phase cards in § Pipeline are likely main hit cluster (Phase 1, 6, 7, 8 cards mention ck-skill names)
- § Beyond was just rewritten in v2.1.0 with 3 rows containing ck:frontend-development, ck:shopify, ck:frontend-design — needs full generic-ization
- § In Practice tabs (Phase 7 work) — verify panels don't mention ck-skills in flow descriptions

## Requirements

### Functional
- 0 ck:/ckm: matches in index.html post-edit
- Phase cards (Phase 1, 6, 7, 8) use inline-protocol or capability phrasing
- § Beyond's 3 rows replaced with generic capability descriptions (matches SKILL.md § Beyond + README Related Skills exactly)
- Tab panels' flow descriptions in § In Practice (if mention ck-skills) updated
- Hero version + footer version both → 2.2.0
- File tree in § Getting Started — verify file paths only (no ck-skill names expected)

### Non-functional
- ARIA tab contract preserved (role, aria-selected, aria-controls, keyboard nav)
- No-JS fallback preserved (.no-js class strategy)
- No new fonts, no new accent colors (cream + ink + dusk-rose only)
- Section count remains 9 (no add/remove)
- File size change: -10 to +20 lines (mostly word replacements + 1 capability paragraph)

## Architecture

### Phase cards in § Pipeline

**Phase 01 card** (Discovery) — currently:
```html
<p>Delegate to <code>ck:brainstorm</code>. Brief branches per type. Locks vibe + audience + conversion goal.</p>
<span class="ref">ck:brainstorm</span>
```

**New**:
```html
<p>Inline brainstorm protocol. Brief branches per type. Locks vibe + audience + conversion goal.</p>
<span class="ref">workflow-phases.md § Phase 1</span>
```

**Phase 04 card** (2D visual assets) — currently mentions catalog; verify no ck-skill names.

**Phase 05 card** (Visual effect layer) — currently mentions CSS first; verify (might say "ck:threejs as shader runner"); update to "React Three Fiber as shader runner".

**Phase 06 card** (Plan) — currently:
```html
<p>Delegate to <code>ck:plan</code>. Type-aware: landing sections vs portfolio sections + case study route.</p>
<span class="ref">ck:plan</span>
```

**New**:
```html
<p>Inline plan protocol. Type-aware: landing sections vs portfolio sections + case study route + generic page-purpose-driven sections.</p>
<span class="ref">workflow-phases.md § Phase 6</span>
```

**Phase 07 card** (Implement) — currently:
```html
<p>Delegate to <code>ck:cook</code>. Apply locked motion intensity. Custom icons only. Real draft copy.</p>
<span class="ref">ck:cook</span>
```

**New**:
```html
<p>Inline implement protocol. Apply locked motion intensity. Custom icons only. Real draft copy.</p>
<span class="ref">workflow-phases.md § Phase 7</span>
```

**Phase 08 card** (Anti-slop audit) — currently:
```html
<p>Final gate. Tier 1 hits = block ship. Grep + visual checks. <code>code-reviewer</code> agent.</p>
<span class="ref">anti-slop-rules.md</span>
```

**New**:
```html
<p>Inline tier-filtered audit. Tier 1 hits = block ship. Grep + visual checks via vision-capable model.</p>
<span class="ref">anti-slop-rules.md + workflow-phases.md § Phase 8</span>
```

### § Beyond rewrite (already 3 rows from v2.1.0; just replace ck-skill names)

**Current** (3 rows mention `ck:frontend-development`, `ck:shopify`, `ck:frontend-design`):

**New**:
```html
<div class="beyond-row">
  <div class="beyond-need">Full app architecture, complex client-side state, deep multi-page IA</div>
  <div class="beyond-skill">General frontend engineering workflow</div>
</div>

<div class="beyond-row">
  <div class="beyond-need">Full e-commerce backend (products, cart, checkout, inventory, payment)</div>
  <div class="beyond-skill">Dedicated e-commerce platform workflow</div>
</div>

<div class="beyond-row">
  <div class="beyond-need">Exact design replication from screenshot / Figma reference</div>
  <div class="beyond-skill">Vision-driven design-to-code workflow</div>
</div>
```

The `.beyond-skill code` styling currently wraps `<code>` tags around skill names. Since we're removing skill names, just plain text inside `.beyond-skill` div. CSS still applies background + border-left styling — adjust if needed.

### Tab panels in § In Practice

Currently 4 tabs (Coffee landing, Portfolio redesign, Blog page, Dashboard).

Check each panel's `<ol class="tab-flow">` for ck-skill mentions:
- Panel 1 (Coffee): "Phase 1 → `ck:brainstorm` locks vibe..." → "Phase 1 → inline brainstorm protocol locks vibe..."
- Panel 1 (Coffee): "Phase 4 → silkscreen-style poster hero illustration via `ck:ai-artist`" → "via text-to-image with style control"
- Panel 1 (Coffee): "Phase 6-8 → `ck:plan` + `ck:cook` + Tier 1/2/3 audit" → "Phase 6-8 → inline plan + implement + Tier 1/2/3 audit"
- Panel 2 (Portfolio): Similar pattern — update Phase 1/6/8 references
- Panel 3 (Blog): "Phase 6 → `ck:plan` outputs..." / "Phase 7 → `ck:cook` builds it" → inline protocol phrasing
- Panel 4 (Dashboard): Similar pattern

### Version bump (2 locations)

- Hero meta: `<span>v2.1.0</span>` → `<span>v2.2.0</span>`
- Footer: `<span><em>perfect-ui</em> — v2.1.0</span>` → `<span><em>perfect-ui</em> — v2.2.0</span>`

### File tree in § Getting Started

Currently shows file structure tree. Verify no ck-skill mentions (paths are skill-local). Likely already OK.

### Anti-slop self-audit (final check)

- grep `lucide|heroicons|phosphor` → 0 matches
- grep `Inter|Roboto|Arial` as font-family → 0 matches
- grep `h-screen` → 0 matches
- grep emoji unicode ranges → 0 matches
- grep `from-purple-` `to-blue-` → 0 matches
- grep raw hex outside CSS custom prop defs → 0 matches outside SVG paths

## Related code files

**Modify:** `index.html` (single file, multiple sections)

**Create / Delete:** None

## Implementation steps

1. **Read index.html** with grep -n for ck:/ckm: line numbers (14 hits)
2. **Update hero version** → v2.2.0
3. **Update Phase 1 card** body + ref
4. **Update Phase 5 card** (if mentions ck:threejs)
5. **Update Phase 6 card** body + ref
6. **Update Phase 7 card** body + ref
7. **Update Phase 8 card** body + ref (remove code-reviewer agent mention)
8. **Update tab panels in § In Practice** — Panel 1/2/3/4 flow descriptions
9. **Update § Beyond rows** (3 rows) — remove ck-skill code tags, use plain text capability descriptions
10. **Update footer version** → v2.2.0
11. **Anti-slop self-audit greps** — verify 0 violations
12. **No-JS validation** — confirm .no-js strategy still works (4 panels visible)
13. **Section count check** (= 9, unchanged)
14. **Final grep** — `grep -E 'ck:|ckm:|code-reviewer' index.html` returns 0 matches

## Todo list
- [ ] Read index.html, grep ck:/ckm: line numbers
- [ ] Bump hero version → v2.2.0
- [ ] Update Phase 1 card
- [ ] Update Phase 5 card (if needed)
- [ ] Update Phase 6 card
- [ ] Update Phase 7 card
- [ ] Update Phase 8 card
- [ ] Update 4 tab panels (Phase flow descriptions)
- [ ] Update § Beyond 3 rows (generic capability)
- [ ] Bump footer version → v2.2.0
- [ ] Anti-slop self-audit greps
- [ ] No-JS strategy verify
- [ ] Section count check (= 9)
- [ ] Final grep verification (0 matches)

## Success criteria
- 0 ck:/ckm: matches in index.html
- 0 "code-reviewer agent" mentions
- Hero + footer version = v2.2.0
- Phase cards (1, 6, 7, 8) use inline-protocol phrasing
- § Beyond 3 rows use generic capability descriptions
- 4 tab panels use inline-protocol or capability phrasing
- ARIA tab contract intact (verify with grep aria-selected/aria-controls)
- No anti-slop self-violations
- Section count = 9 (unchanged)
- Net line change: -5 to +20 lines

## Risk assessment
- **Risk:** Removing `<code>` tags inside `.beyond-skill` might break CSS styling → keep `<code>` tags around capability phrases if needed, or adjust styling
- **Risk:** Phase card "ref" pointers updated but pointing to nonexistent sections → verify workflow-phases.md has § Phase 1 / § Phase 6 / § Phase 7 / § Phase 8 headings (created in Phase 01)
- **Risk:** § In Practice tab panels accidentally break ARIA contract → check 4 tabpanel role attributes intact
- **Risk:** Removing ck-skill names without replacement leaves vague description → use capability phrasing consistently

## Security considerations
None — static HTML edits.

## Next steps
- After Phase 04 + 05 complete: final cross-file consistency check (SKILL.md ↔ README ↔ index.html scope + § Beyond language matches)
- Run final aggregate grep: `grep -rE 'ck:|ckm:|code-reviewer\s+agent' SKILL.md README.md index.html references/ assets/` → 0 matches
- Update plan.md status to completed
- Optionally: visual diff index.html before/after to confirm layout integrity
