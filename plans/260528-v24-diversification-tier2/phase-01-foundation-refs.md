# Phase 01 — Foundation refs (anti-slop + visual-direction-guide)

## Context links
- [brainstorm.md](./brainstorm.md) § Item F+T (Dials with atmosphere), Item R (Gapless bento rule)
- [references/anti-slop-rules.md](../../references/anti-slop-rules.md)
- [references/visual-direction-guide.md](../../references/visual-direction-guide.md)

## Overview
- **Priority:** High (foundation referenced by Phase 02-06)
- **Status:** pending
- **Parallel-safe with:** Phase 02, 03
- **Description:** Add 2 dials (DESIGN_VARIANCE + VISUAL_DENSITY) with atmosphere spectrum + per-vibe defaults to visual-direction-guide.md. Add Empty bento Tier 1 rule + diversification rule reference to anti-slop-rules.md.

## Key insights
- 2 dials add to existing motion intensity (0-3/3) — together = 3 dial system
- Per-vibe defaults derived from existing 11 vibe characterizations (visual-direction-guide.md spatial language descriptions)
- Atmosphere spectrum inline in each dial (descriptive labels for ranges)
- Empty bento Tier 1 rule references gapless mandate in macrostructure-catalog.md (Phase 03 creates)
- Diversification rule reference points to .perfect-ui/log.json schema (Phase 04 creates)

## Requirements

### Functional
- visual-direction-guide.md gets new § "Two dials — DESIGN_VARIANCE + VISUAL_DENSITY (Phase 2)"
- Each dial has: range 1-10 + atmosphere descriptive labels (3 brackets) + behavior description
- Per-vibe defaults table for all 11 vibes
- Diversification rule reference (cross-link to forthcoming `.perfect-ui/log.json` schema)
- anti-slop-rules.md gets Empty bento Tier 1 rule + matrix update
- anti-slop-rules.md gets brief Diversification rule reference (forward-link to macrostructure-catalog.md)

### Non-functional
- visual-direction-guide.md grows ~+80 lines (new § + matrix)
- anti-slop-rules.md grows ~+20 lines (1 new Tier 1 rule + 1 matrix row + diversification ref note)
- Existing per-vibe characterizations untouched (additive layer)
- Cross-references resolve after Phase 03 + Phase 04 complete

## Architecture

### visual-direction-guide.md new section

Insert AFTER existing `## Vibe × Motion Intensity Matrix` (around line 240+), BEFORE `## Output Artifact Template`:

```markdown
## Two dials — DESIGN_VARIANCE + VISUAL_DENSITY (Phase 2)

Beyond motion intensity (Phase 2e), two additional dials lock at Phase 2. Combined with motion intensity, perfect-ui has a 3-dial system.

### DESIGN_VARIANCE (1-10)
Drives layout asymmetry, grid commitment, spatial language.

| Range | Atmosphere | Behavior |
|-------|------------|----------|
| 1-3 | Predictable / Art Gallery Symmetric | Flex `justify-center`, strict 12-col, equal paddings, symmetric grids |
| 4-7 | Offset / Daily App Asymmetric | Margin offsets (-2rem), mixed aspect ratios, left-aligned headers over centered content |
| 8-10 | Artsy / Chaotic Asymmetric | Masonry, fractional grid units (`2fr 1fr 1fr`), massive empty zones (`padding-left: 20vw`) |

**Mobile override:** variance 4+ aggressively falls back to single-column at <768px to prevent horizontal scroll.

### VISUAL_DENSITY (1-10)
Drives spacing scale, card usage, font scaling, chrome density.

| Range | Atmosphere | Behavior |
|-------|------------|----------|
| 1-3 | Art Gallery / Airy | Generous whitespace, huge section gaps (py-32+), expensive feel |
| 4-7 | Daily App / Balanced | Normal SaaS spacing (py-16 to py-24) |
| 8-10 | Cockpit / Dense | Tiny paddings (p-2 to p-4), 1px lines instead of cards, monospaced numbers |

### Per-vibe defaults

| Vibe | DESIGN_VARIANCE | VISUAL_DENSITY |
|------|-----------------|----------------|
| Minimal | 3 | 3 |
| Editorial | 6 | 4 |
| Brutalist | 8 | 7 |
| Retro-futuristic | 7 | 5 |
| Organic | 4 | 3 |
| Luxury | 4 | 3 |
| Playful | 6 | 5 |
| Industrial | 5 | 7 |
| Art-deco | 5 | 4 |
| Glass-tech | 6 | 4 |
| Hand-crafted | 5 | 3 |

User confirms or overrides at Phase 2. Macrostructure choice (see `macrostructure-catalog.md`) can adjust ±2 from vibe default.

### Diversification rule (cross-run)

Read `.perfect-ui/log.json` at Phase 0.5. New run must differ from last entry on at least one dial by ≥3 points. Warning emitted if violated; user override allowed.
```

### anti-slop-rules.md Empty bento rule

Append to existing Tier 1 rules (after rule #12):

```markdown
13. **Empty Bento Grid cells / missing corners / voids** — when using Bento Grid macrostructure (see `macrostructure-catalog.md` § Bento Grid), `grid-flow-dense` is mandatory + col-span/row-span must mathematically interlock. Empty cells = templated AI feel. Use `auto-flow: dense` + verify with visual inspection.
```

Add row to Applicability Matrix:

```markdown
| Empty bento grid cells (missing corners / voids; `grid-flow-dense` missing on Bento macrostructure) | `[universal]` | 1 |
```

### anti-slop-rules.md Diversification rule reference

Add small note after Honest Copy Mandate (after Phase 01 v2.3 content), before § Typography:

```markdown
## Diversification Rule (cross-run)

For projects with multiple perfect-ui runs (tracked in `.perfect-ui/log.json`), each new run must avoid replicating recent picks:

- **Macrostructure** must differ from the last 3 entries (hard rule — see `macrostructure-catalog.md` § Diversification rule)
- **Vibe + wildcard** combo should differ from last entry (warn if repeated; user override allowed)
- **DESIGN_VARIANCE + VISUAL_DENSITY** dials should differ ≥3 points on at least one dial from last entry (warn)
- **Motion personality** should differ from last entry (warn)

Read at Phase 0.5; surface as one-line summary ("Last 3 builds: ..."). Hard rule violations block; warnings allow override. See `workflow-brainstorm.md` for read logic.
```

## Related code files

**Modify (2 files):**
- `references/visual-direction-guide.md` (insert § 2 dials, +80 lines)
- `references/anti-slop-rules.md` (Empty bento Tier 1 rule + matrix row + Diversification Rule §, +20 lines)

**Create / Delete:** None

## Implementation steps

1. **Read visual-direction-guide.md** to locate insertion point (after Vibe × Motion Intensity Matrix, before Output Artifact Template)
2. **Insert § Two dials section** (~80 lines per Architecture above)
3. **Read anti-slop-rules.md** to locate:
   - End of Tier 1 rules (after rule #12 added in v2.3)
   - Applicability Matrix tag table (insert new row)
   - Insertion point for Diversification Rule § (after Honest Copy Mandate, before Typography)
4. **Insert Empty bento Tier 1 rule** (rule #13)
5. **Insert matrix row** for Empty bento
6. **Insert § Diversification Rule** with cross-references
7. **Verify cross-references** — links to macrostructure-catalog.md (Phase 03), workflow-brainstorm.md (Phase 04), `.perfect-ui/log.json` (Phase 04)

## Todo list
- [ ] Read visual-direction-guide.md, find insertion point
- [ ] Insert § Two dials (DESIGN_VARIANCE + VISUAL_DENSITY + atmosphere + per-vibe defaults)
- [ ] Read anti-slop-rules.md, locate insertion points
- [ ] Insert Empty bento Tier 1 rule (#13)
- [ ] Update Applicability Matrix (+1 row)
- [ ] Insert § Diversification Rule with cross-refs
- [ ] Verify cross-refs (placeholders OK; resolved by Phase 03/04)

## Success criteria
- visual-direction-guide.md has § Two dials with 11 vibe defaults table
- anti-slop-rules.md has Tier 1 rule #13 + matrix row + § Diversification Rule
- Total growth: +80 visual + +20 anti-slop = +100 lines
- Existing content untouched
- Cross-references documented (may be unresolved until Phase 03/04 complete)

## Risk assessment
- **Risk:** Per-vibe defaults conflict with existing vibe characterizations (verbose duplication) → keep matrix compact, reference existing characterizations not duplicate them
- **Risk:** Atmosphere spectrum labels feel arbitrary → use Hallmark/stitch-design-taste vocabulary directly ("Art Gallery" / "Cockpit") — already vetted by ecosystem
- **Risk:** Empty bento rule fires before macrostructure-catalog.md exists → use forward-reference; Phase 03 creates target

## Security considerations
None — markdown only.

## Next steps
- Phase 02 (motion-patterns) parallel-safe with this phase
- Phase 03 (macrostructure-catalog) references dials from this phase
- Phase 04 references diversification rule documented here
- Phase 06 (index.html) may add Mandate card referencing dials
