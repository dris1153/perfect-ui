# Phase 03 — SKILL.md scope update

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Files modified > SKILL.md
- [brainstorm.md](./brainstorm.md) § Honest trade-offs
- [phase-01-foundation-files-and-anti-slop-matrix.md](./phase-01-foundation-files-and-anti-slop-matrix.md) — depends on
- [phase-02-workflow-phases-update.md](./phase-02-workflow-phases-update.md) — depends on
- [SKILL.md](../../SKILL.md) — file to modify (301 lines)

## Overview
- **Priority:** High (skill manifest — drives skill discovery + activation)
- **Status:** pending
- **Depends on:** Phase 01 + Phase 02
- **Description:** Rewrite SKILL.md § Scope to remove refusal language; reword Hard Rule #1 + #8; bump version 2.0.0 → 2.1.0; update references list to include 2 new foundation files.

## Key insights
- SKILL.md frontmatter `description` field drives skill auto-activation — must NOT lose existing trigger phrases
- Hard Rules are skill identity — soften wording, don't gut them
- Version bump 2.0.0 → 2.1.0 = minor (additive scope softening, backward compat)

## Requirements

### Functional
- § Scope section rewritten — 2-tier matrix (Special / Generic) replacing refusal list
- Hard Rule #1: keep "NO emoji" mandate but remove "marketing-style sites only" framing
- Hard Rule #8: reword to "type-aware where it matters" — clarify landing/portfolio have rich anatomy, others use generic
- References list updated to include `generic-page-anatomy.md` + `generic-page-skeleton.md`
- `version` field in frontmatter (if present) updated to `2.1.0`
- Trigger phrases / description field MUST retain landing/portfolio activation keywords + add general page-design keywords

### Non-functional
- Keep file structure (headings unchanged where possible)
- Preserve existing process flow diagram references
- Diff should show targeted edits, not wholesale rewrite

## Architecture

### § Scope section — new structure
Replace existing § Scope (which lists explicit refusals) with:

```markdown
## Scope

This skill applies to **any web page output** — single-page sites, multi-section landings, content pages, portfolios, internal app surfaces.

**Two-tier treatment:**

| Tier | Types | Treatment |
|------|-------|-----------|
| **Special** | `landing`, `portfolio` | Rich anatomy + skeleton + section-archetypes per vibe + full anti-slop audit |
| **Generic** | Any other type (`blog`, `about`, `pricing`, `contact`, `coming-soon`, `dashboard`, `admin`, `e-commerce`, free text...) | Generic anatomy + skeleton + universal anti-slop subset |

**Universal toolkit (applies to both tiers):** vibe + palette + typography + custom icons + 2D illustrations + visual effects + motion + custom SVG cohesion.

**No refusals.** Skill accepts any `--type` value. For types where evidence base (12 marketing landings) doesn't directly cover patterns (e.g., dashboard, admin, e-commerce), skill logs notice and proceeds with best-effort universal craft.

When another skill is genuinely a better fit, skill suggests but does not force redirect — see § Beyond at end.
```

### Hard Rule #1 — reword
**Current:** "NO emoji anywhere — not in copy, headings, or as icons. Use a custom SVG instead." (in context of "marketing-style sites only")

**New:** "NO emoji anywhere — not in copy, headings, or as icons, regardless of page type. Use a custom SVG instead."

(Tiny change — explicit "regardless of page type" makes it clear this applies to dashboards too.)

### Hard Rule #8 — reword
**Current:** "Type-aware everything — Phase 1 brief, Phase 6 plan, anatomy, and skeleton ALL branch by `--type`."

**New:** "Type-aware where it matters — landing/portfolio have rich anatomy + skeleton + section archetypes; all other types use generic anatomy + generic skeleton. Phase 1 brief always asks page-purpose; Phase 6 plan branches by tier; Phase 8 audit honors applicability matrix per `--type`."

### Version bump
- Frontmatter (if SKILL.md has YAML frontmatter): `version: "2.0.0"` → `version: "2.1.0"`
- Body version mention (if exists in introduction): update accordingly

### References list update
Locate section listing reference files (e.g., "Workflow Phases → references/workflow-phases.md"). Add:
- `references/generic-page-anatomy.md` — generic-tier anatomy for non-landing/portfolio types
- `assets/nextjs-skeleton/generic-page-skeleton.md` — generic-tier Next.js skeleton

### Process flow diagram (if present)
Update Phase 0.5 node label from "Detect type or REFUSE" to "Detect type → tier route".

## Related code files

**Modify:**
- `SKILL.md`
  - § Scope section: full rewrite (~30 lines new replacing ~25 lines existing)
  - Hard Rule #1: 1-line tweak
  - Hard Rule #8: 1-paragraph reword
  - Frontmatter `version`: 2.0.0 → 2.1.0
  - References list: add 2 entries
  - Process flow diagram (if present): 1-node label update

**Create:** None
**Delete:** Existing refusal list within § Scope

## Implementation steps

1. **Read existing `SKILL.md`** to locate exact line ranges:
   - § Scope section
   - Hard Rule #1
   - Hard Rule #8
   - References list
   - Frontmatter version field
   - Process flow diagram (if present)

2. **Update frontmatter `version`** → `2.1.0` (if frontmatter exists with version field)

3. **Rewrite § Scope** — replace refusal-based content with 2-tier matrix per Architecture above

4. **Reword Hard Rule #1** — small edit, append "regardless of page type"

5. **Reword Hard Rule #8** — replace paragraph per Architecture above

6. **Update references list** — add 2 new entries (generic-page-anatomy.md + generic-page-skeleton.md)

7. **Update process flow diagram** (if present) — Phase 0.5 node label

8. **Validation pass:**
   - Re-read SKILL.md
   - Confirm no "refuse" / "off-scope" / "out of scope" prose remains
   - Confirm trigger phrases for landing/portfolio still present
   - Confirm version is 2.1.0
   - Confirm 2 new file references added

## Todo list
- [ ] Read SKILL.md, locate line ranges
- [ ] Update frontmatter version → 2.1.0
- [ ] Rewrite § Scope section
- [ ] Reword Hard Rule #1
- [ ] Reword Hard Rule #8
- [ ] Update references list (+ 2 entries)
- [ ] Update process flow diagram if present
- [ ] Final read-through

## Success criteria
- SKILL.md frontmatter version = 2.1.0
- § Scope contains 2-tier matrix; no refusal list
- Hard Rule #1 includes "regardless of page type"
- Hard Rule #8 reworded to "type-aware where it matters"
- References list includes generic-page-anatomy.md + generic-page-skeleton.md
- Skill discovery (description / trigger phrases) preserves landing/portfolio activation keywords

## Risk assessment
- **Risk:** Lose skill activation phrases in description rewrite → keep description additive (add new keywords, don't replace existing)
- **Risk:** Hard rule rewording weakens enforcement → wording changes are framing-only, mandate strength preserved
- **Risk:** Diagram update breaks Mermaid syntax → if updating Mermaid, validate syntax post-edit

## Security considerations
None.

## Next steps
- Phase 04 (README) references SKILL.md scope decisions for consistency
- Phase 05 (index.html) references SKILL.md scope decisions for consistency
