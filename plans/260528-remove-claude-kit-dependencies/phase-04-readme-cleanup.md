# Phase 04 — README.md cleanup

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Per-file change scope > HIGH
- [phase-03-skill-md-cleanup.md](./phase-03-skill-md-cleanup.md) — depends on (scope consistency)
- [README.md](../../README.md) — file to modify (~390 lines pre-edit, 26 ck: hits)

## Overview
- **Priority:** Medium-High (public-facing docs — drift from SKILL.md confuses users)
- **Status:** pending
- **Depends on:** Phase 03 (scope decisions locked in SKILL.md)
- **Parallel-safe with:** Phase 05 (index.html — different file, different content)
- **Description:** Remove ck:/ckm: from README.md (26 hits). Update Examples (flow descriptions mention ck-skills). Remove FAQ entry "Does this skill work without ck:brainstorm / ck:plan / ck:cook skills?". Generic-ize Related Skills table (5 rows → 3 rows). Bump version 2.1.0 → 2.2.0.

## Key insights
- README has 26 hits — highest count. Most are in:
  - § Examples (Example 1, 2, 3, 4 flow descriptions reference ck:brainstorm, ck:plan, ck:cook, ck:ai-artist)
  - § Tech Stack Output (mentions `next/font/local` styling — likely OK; verify)
  - § FAQ entry about working without ck-skills (full entry to remove)
  - § Related Skills (5-row table at bottom)
  - § Credits / footer (passing mentions)
- Preserve quick_validate.py reference (skill-creator is Anthropic tool, not Claude Kit — per Decision 4)
- Version mention at line 5: `**Version:** 2.1.0` → `**Version:** 2.2.0`

## Requirements

### Functional
- 0 ck:/ckm: matches in README.md post-edit
- Examples (1-4) flow descriptions use inline-protocol or capability phrasing
- FAQ entry "Does this skill work without ck:brainstorm / ck:plan / ck:cook skills?" removed (no longer applicable post-v2.2.0)
- Add new FAQ entry: "Is the workflow self-contained?"
- Related Skills table reduced from 5 rows to 3 generic capability rows
- Version 2.1.0 → 2.2.0
- skill-creator/quick_validate.py reference preserved
- "code-reviewer" agent mentions removed

### Non-functional
- Tone matches existing README (casual but technical)
- Examples follow existing format (Input quote + numbered skill-flow steps)
- File size ± 30 lines (removing FAQ entry + Related Skills shrink, intro paragraph add slightly)

## Architecture

### Examples (1-4) flow descriptions

Examples currently mention specific ck-skills in flow steps. Replacement pattern:

| Current phrase | New phrase |
|----------------|-----------|
| "Phase 1 — delegates to `ck:brainstorm`:" | "Phase 1 — inline brainstorm protocol:" |
| "Phase 4 — silkscreen-style poster hero illustration via `ck:ai-artist`" | "Phase 4 — silkscreen-style poster hero illustration via text-to-image with style control" |
| "Phase 6 — `ck:plan` outputs phased Next.js implementation" | "Phase 6 — inline plan protocol outputs phased Next.js implementation" |
| "Phase 7 — `ck:cook` builds it" | "Phase 7 — inline implement protocol builds it" |
| "Phase 8 — Tier-1/2/3 anti-slop audit passes" | (no change — audit doesn't name ck-skill) |
| "via `ck:ai-multimodal`" / "via `ckm:design`" | "via vision-capable model" / "via vector icon design pipeline" |

Apply to Example 1 (coffee landing), Example 2 (portfolio redesign), Example 3 (blog page), Example 4 (dashboard).

### FAQ entry removal + addition

**Remove**:
```
**Q: Does this skill work without `ck:brainstorm` / `ck:plan` / `ck:cook` skills?**
A: It's designed to orchestrate them. Without them, the workflow degrades — Claude does each phase inline but loses the structured brainstorm-plan-cook discipline. Strongly recommend having them installed.
```

**Add new entry** (in same FAQ location):
```
**Q: Is the workflow self-contained?**
A: Yes (as of v2.2.0). All brainstorm / plan / implement / audit protocols are inline in `references/workflow-phases.md`. Skill no longer depends on external orchestration skills. Asset generation (icons, illustrations, effects) is described by capability — use any text-to-image / vision / vector tool that fits the capability description.
```

### Related Skills table generic-ize

**Current** (5 rows: ck:frontend-development, ck:frontend-design, ck:ui-ux-pro-max, ck:shopify, ckm:design):

**New** (3 rows, generic capability):
```
| Need | Suggested approach |
|------|-------------------|
| Full app architecture, complex client-side state, deep multi-page IA | General frontend engineering workflow (state management, routing framework, type-safe API layer) |
| Full e-commerce backend (cart, checkout, inventory, payment integration) | Dedicated e-commerce platform workflow with backend orchestration |
| Exact design replication from screenshot / Figma reference | Vision-driven design-to-code workflow (multimodal model + visual diff loop) |
```

Matches SKILL.md § Beyond + index.html § Beyond exactly (consistency).

### Version + intro paragraph

Line 5: `**Version:** 2.1.0` → `**Version:** 2.2.0`

Update intro paragraph or "What it does" section to mention v2.2.0:
- After existing "v2.1.0 update: ..." paragraph, append:
```
**v2.2.0 update:** Workflow is now self-contained. All orchestration (brainstorm, plan, implement, audit) is inlined in `references/workflow-phases.md`. Asset generation tools are described by capability (text-to-image with style control, vision-capable analysis, etc.) — no specific external skill dependencies. Skill runs in any Claude Code setup.
```

### Trigger phrases (preserve all)

Check § When to Trigger / Trigger phrases section. If any mentions ck-skill activation phrase, remove that phrase but keep all other activation triggers.

### Credits / Footer

Any "Credits" section that mentions ck-skill ecosystem — update to neutral phrasing. Likely minor (1-2 hits).

## Related code files

**Modify:** `README.md` (single file, multiple sections)

**Create / Delete:** None

## Implementation steps

1. **Read README.md** with grep -n for ck:/ckm: line numbers
2. **Update version line 5** → 2.2.0
3. **Append v2.2.0 update paragraph** to § What it does
4. **Update Example 1 flow descriptions** (coffee landing — ck:brainstorm / ck:ai-artist mentions)
5. **Update Example 2 flow descriptions** (portfolio redesign — ck:plan / ck:cook mentions)
6. **Update Example 3 flow descriptions** (blog page — ck:brainstorm / ck:plan / ck:cook mentions)
7. **Update Example 4 flow descriptions** (dashboard — ck:brainstorm / ck:plan / ck:cook mentions)
8. **Replace FAQ entry** ("Does this skill work without ck:...") with new entry ("Is the workflow self-contained?")
9. **Reduce Related Skills table** from 5 rows to 3 generic-capability rows
10. **Final grep** — `grep -E 'ck:|ckm:|code-reviewer' README.md` returns 0 matches
11. **Preserve check** — confirm skill-creator/quick_validate.py reference still present
12. **Activation keyword preservation check**

## Todo list
- [ ] Read README.md, grep ck:/ckm: line numbers
- [ ] Bump version 2.1.0 → 2.2.0 (line 5)
- [ ] Append v2.2.0 update paragraph
- [ ] Update Example 1 flow descriptions
- [ ] Update Example 2 flow descriptions
- [ ] Update Example 3 flow descriptions
- [ ] Update Example 4 flow descriptions
- [ ] Replace FAQ "Does this skill work without ck:..." entry
- [ ] Reduce Related Skills table to 3 generic rows
- [ ] Final grep verification (0 matches)
- [ ] Preserve skill-creator quick_validate.py reference
- [ ] Activation keyword preservation check

## Success criteria
- 0 ck:/ckm: matches in README.md
- 0 "code-reviewer agent" mentions
- Version 2.2.0 in line 5
- 4 examples present, all use inline-protocol or capability phrasing
- FAQ "Does this skill work without ck:..." entry removed
- New FAQ "Is the workflow self-contained?" entry present
- Related Skills table has 3 rows, no specific skill names
- skill-creator/quick_validate.py reference preserved
- File size within ± 50 lines of pre-edit

## Risk assessment
- **Risk:** Lose tonal consistency with existing examples → mirror existing format exactly (Input quote + numbered Skill flow)
- **Risk:** FAQ replacement entry contradicts SKILL.md scope → cross-check Phase 03 SKILL.md output before finalizing
- **Risk:** Related Skills table reduction strands orphan info (e.g., ck:ui-ux-pro-max distinction) → accept; users can find component-level UI guidance elsewhere
- **Risk:** Examples mention specific tool that's not in capability list → use generic capability vocabulary

## Security considerations
None.

## Next steps
- Phase 05 (index.html) updates separately — parallel-safe with this phase
- Final cross-file consistency check: SKILL.md § Beyond ≡ README Related Skills ≡ index.html § Beyond (all 3 capabilities match)
