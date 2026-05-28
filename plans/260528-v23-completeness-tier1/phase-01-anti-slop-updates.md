# Phase 01 — Anti-slop rules updates (4 new patterns + tag matrix)

## Context links
- [brainstorm.md](./brainstorm.md) § Item B (Honest copy), Item N (Hero 2-line), Item S (Meta-label ban), Item V (Hero filler-text)
- [references/anti-slop-rules.md](../../references/anti-slop-rules.md) — file to modify

## Overview
- **Priority:** High (foundation referenced by other phases)
- **Status:** pending
- **Parallel-safe with:** Phase 02, 03, 04 (different files, no shared content)
- **Description:** Add 4 new anti-slop patterns + § Honest Copy Mandate + update § Applicability Matrix tag table.

## Key insights
- 3 new patterns are direct anti-slop additions (hero line / meta-label / filler-text)
- Honest Copy is a § with positive guidance + 3 accepted paths (placeholder / pick different macrostructure / refuse section)
- Tag matrix at top of file needs 4 new rows
- All 4 new rules need tier classification (Tier 1 / 2 / 3 + applicability)

## Requirements

### Functional
- § Honest Copy Mandate added after § Applicability Matrix, before § Typography
- Hero line rule: vibe-specific (pull defaults from visual-direction-guide.md Phase 04 output)
- Meta-label ban: universal Tier 1
- Hero filler-text ban: Tier 2 (text only; icons OK)
- Tag matrix gets 4 new rows with `[universal]` / `[marketing-only]` / `[landing/portfolio-only]` tag

### Non-functional
- Existing rules content untouched
- Cross-references in other files (workflow-phases.md, anatomies) must resolve to new sections

## Architecture

### § Honest Copy Mandate (new section, insert after Applicability Matrix)

```markdown
## Honest Copy Mandate (universal)

If the user did not supply a metric / testimonial / logo / case-study count, the skill does NOT invent one. Three accepted paths:

1. **Em-dash placeholder + label (default)** — `— metric to confirm` rendered as a visible grey block. Layout reserves space; user fills in later. HTML/JSX pattern:
   ```tsx
   <span className="placeholder bg-bg-muted px-2 rounded text-ink-muted">
     — metric to confirm
   </span>
   ```
2. **Pick a different macrostructure** — if a stat-led hero requires N metrics and only M < N are available, switch to a non-stat hero (typography-led, image-led).
3. **Refuse the section entirely** — if a "trusted by 50,000+ teams" logo bar has 0 real logos to show, do not include the logo bar. Honest absence beats fabricated presence.

Forbidden patterns (already in tier matrix; restated here for context):
- "+47% conversion", "trusted by 50,000+ teams", "10× faster" with no source
- John Doe / Jane Smith testimonials with realistic-looking avatars
- Generic startup logos (Acme / Globex / Initech / Nexus)
- "1M+ users", "99.99% uptime", round-fake numbers
- Fabricated case-study counts (8 case studies displayed when user has 2)

Phase 7 implementation must use placeholder rendering; Phase 8 audit greps for forbidden numbers + names per `[marketing-only]` rules.
```

### 3 new anti-slop rules

**Insert in § Tier 1 — Strong AI tells** (after existing rules):

```markdown
11. **Hero H1 line count exceeds vibe-specific limit** — see `visual-direction-guide.md` § Hero H1 line range column. Universal ceiling: 4+ lines is catastrophic failure regardless of vibe. Enforcement: container `max-w-5xl` / `max-w-6xl` + H1 `clamp(3rem, 5vw, 5.5rem)`. If headline exceeds 90 chars, rewrite shorter; never break the line cap by reducing font below `--text-display-s`.

12. **Meta-label headers** — "SECTION 01" / "QUESTION 05" / "ABOUT US" / "CHAPTER THREE" / numbered eyebrows / uppercase mono-cap section labels. No exception even for ordinal content. Vibe-paired typography hierarchy (display weight, color) communicates section identity instead.
```

**Insert in § Tier 2 — AI compositional tendencies** (after existing rules):

```markdown
18. **Hero filler text** — "Scroll to explore" / "Swipe down" / "Continue below" / similar prompt-text in hero. Tier 2 violation. Hero composition must communicate "more below" without typed instructions. Icons (↓, chevron, bouncing arrow) are OK — they're visual hints, not text filler. Aggressive bouncing animation = additional Tier 2 hit (generic motion-on-everything rule).
```

### Applicability Matrix update (4 new rows in tag table)

Add to existing table near top of file:

```markdown
| Rule | Tag | Tier |
|------|-----|------|
| Honest Copy Mandate (no fabricated metrics) | `[universal]` | (positive guidance — referenced by Tier 2 fake stats rule) |
| Hero H1 line count exceeds vibe-specific limit | `[universal]` | 1 |
| Meta-label headers | `[universal]` | 1 |
| Hero filler text | `[marketing-only]` | 2 |
```

## Related code files

**Modify:** `references/anti-slop-rules.md` (single file, 4 surgical edits)

**Create / Delete:** None

## Implementation steps

1. Read full `references/anti-slop-rules.md` to identify exact insertion points:
   - § Applicability Matrix tag table (top of file, after intro)
   - End of § Tier 1 rules
   - End of § Tier 2 rules
   - After § Applicability Matrix, before § Typography (insert § Honest Copy Mandate)
2. Insert § Honest Copy Mandate with em-dash placeholder spec + 3 paths
3. Append 2 new Tier 1 rules (Hero H1 line count + Meta-label headers)
4. Append 1 new Tier 2 rule (Hero filler text)
5. Update § Applicability Matrix tag table with 4 new rows
6. Verify cross-references — workflow-phases.md Phase 7 + Phase 8 will reference these in Phase 02/05

## Todo list
- [ ] Read anti-slop-rules.md, locate insertion points
- [ ] Insert § Honest Copy Mandate (~30 lines)
- [ ] Append 2 Tier 1 rules (Hero line + Meta-label)
- [ ] Append 1 Tier 2 rule (Hero filler text)
- [ ] Update Applicability Matrix tag table (+4 rows)
- [ ] Verify file post-edit: § Honest Copy present, 3 new tier rules present, matrix updated

## Success criteria
- § Honest Copy Mandate section exists with em-dash placeholder + 3 paths
- 3 new rules added (2 Tier 1 + 1 Tier 2)
- Applicability Matrix tag table has 4 new rows
- Existing content untouched
- File size ≤+60 lines (target ~+50)
- No syntax errors in markdown (proper backticks, tables)

## Risk assessment
- **Risk:** Insertion at wrong section breaks Applicability Matrix structure → re-read file post-edit to verify table integrity
- **Risk:** Cross-reference to visual-direction-guide.md § Hero H1 line range column resolves before Phase 04 completes → Phase 04 runs in parallel; ensure both phases write consistent column name
- **Risk:** Tier classification debate (filler-text could be Tier 1 if very obvious) → user decided Tier 2 in brainstorm Q6 (filler-text is less severe than 2 equal CTAs / icon library import)

## Security considerations
None — markdown-only edits.

## Next steps
- Phase 02 references § Honest Copy Mandate in workflow-phases.md Phase 7 constraint
- Phase 03 may cross-link Strategic Omissions to anti-slop rules (e.g., honest copy applies to all anatomies)
- Phase 04 supplies the vibe-specific Hero H1 line ranges that this phase's rule #11 cites
- Phase 05 SKILL.md Hard Rule #3 update references honest copy
