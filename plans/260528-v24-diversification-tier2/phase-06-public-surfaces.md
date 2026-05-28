# Phase 06 — Public surfaces (README + index.html)

## Context links
- [brainstorm.md](./brainstorm.md) § Implementation considerations
- [phase-05-skill-md.md](./phase-05-skill-md.md) — depends on (consistency with SKILL.md updates)
- [README.md](../../README.md), [index.html](../../index.html)

## Overview
- **Priority:** Final integration — public-facing docs
- **Status:** pending
- **Depends on:** Phase 05 (SKILL.md must be updated first for cross-file consistency)
- **Parallel-safe with:** Phase 05 only conceptually — they need to align but each touches different files
- **Description:** Bump version 2.3.0 → 2.4.0 in README L5 + index.html hero + footer. Add v2.4.0 update paragraph to README. Add new FAQ entry. Add new Mandate card (Diversification) to index.html. Update credits acknowledge in README.

## Key insights
- README v2.4.0 paragraph mentions: macrostructure layer + dials + motion personalities + diversification + workflow split
- index.html Mandates section may add new card #9 "Diversify each run" or fold into existing
- index.html Pipeline section already has Phase 0.1 (v2.3); v2.4 adds Phase 2c + 2.6 — may add cards to pipeline section
- Decision per brainstorm sub-decision 7: ADD new Mandate card (don't fold)
- Decision per brainstorm sub-decision 8: 1 paragraph multi-topic for README (concise)

## Requirements

### Functional
- README.md L5 version 2.3.0 → 2.4.0
- README.md adds v2.4.0 update paragraph (single, multi-topic)
- README.md adds 1-2 new FAQ entries (macrostructure / motion personality / log.json)
- README.md credits acknowledge mentions: Hallmark (macrostructure layer) + motion-design (4 personalities)
- index.html hero version 2.3.0 → 2.4.0
- index.html footer version 2.3.0 → 2.4.0
- index.html Mandates section adds new card #9 "Diversify each run"
- index.html Pipeline section may add Phase 2c + 2.6 cards (optional)

### Non-functional
- Tone consistent with existing README (casual technical)
- index.html ARIA tab contract preserved
- Backward compat: existing Examples render schema-identically
- Anti-slop self-audit: no violations introduced

## Architecture

### README.md edits

1. **L5 version**: `**Version:** 2.4.0`

2. **v2.4.0 update paragraph** (after existing v2.3.0 paragraph):

```markdown
**v2.4.0 update:** Diversification pass. Skill now enforces structural variety across runs — `.perfect-ui/log.json` tracks past picks (macrostructure / vibe / dials / motion personality); macrostructure pick must differ from last 3 entries (hard rule). NEW macrostructure layer adds 7 page-shape archetypes (Marquee Hero / Bento Grid / Long Document / Manifesto / Stat-Led / Workbench / Letter) independent of vibe — 7 macros × 11 vibes = 77 valid combinations. 2 new dials (DESIGN_VARIANCE + VISUAL_DENSITY with atmosphere spectrum labels) + per-vibe defaults locked at Phase 2. 4 motion personalities (Playful / Premium / Corporate / Energetic) with Brand Motion Identity (3 locked constants: signature easing + duration palette + entrance pattern) added as Phase 2.6. workflow-phases.md split into 4 sub-references for navigability.
```

3. **New FAQ entries** (insert near end of FAQ):

```markdown
**Q: What's a macrostructure (v2.4.0+)?**
A: A macrostructure is a named page-shape archetype — independent of vibe. 7 macrostructures exist: Marquee Hero (declarative launches), Bento Grid (SaaS feature showcase), Long Document (case studies / manifestos), Manifesto (brand statements), Stat-Led (B2B proof-heavy), Workbench (app surfaces), Letter (founder letters / personal portfolios). Vibe locks the surface; macrostructure locks the shape. Same vibe + different macrostructures = different page rhythms. Diversification rule (cross-run): macrostructure pick must NOT match any of the last 3 entries in `.perfect-ui/log.json`. See `references/macrostructure-catalog.md`.

**Q: What's the Brand Motion Identity (v2.4.0+)?**
A: At Phase 2.6, skill picks 1 of 4 motion personalities — Playful, Premium, Corporate, or Energetic. Personality locks 3 constants for the entire project: signature easing curve (used in 80% of animations), duration palette (3 values: quick / standard / slow), entrance pattern (consistent reveal style). Personality is independent of motion intensity (0-3/3 from Phase 2e) — Premium personality can be 1/3 or 3/3 intensity. See `references/motion-patterns.md § Motion Personalities`.
```

4. **Credits acknowledge update**:

```markdown
- v2.3.0+ patterns inspired by the taste-skill ecosystem (Hallmark, gpt-taste, stitch-design-taste, motion-design, redesign-existing-projects, et al.)
- v2.4.0 macrostructure layer adopted from Hallmark's named-archetype framework
- v2.4.0 motion personalities adapted from LottieFiles motion-design skill (Playful / Premium / Corporate / Energetic)
```

### index.html edits

1. **Hero version**: `<span>v2.4.0</span>`

2. **Footer version**: `<span><em>perfect-ui</em> — v2.4.0</span>`

3. **Mandates section — ADD new card #9**:

Find existing Mandates grid. Mandate count was 8; if v2.3 didn't add #9, this becomes the new #9:

```html
<div class="mandate">
  <span class="mandate-num">— 09</span>
  <h3>Diversify each run</h3>
  <p>Same skill, different output each time. Macrostructure must differ from last 3 entries in <code>.perfect-ui/log.json</code>. Vibe / dials / motion personality should differ from last entry (soft warning).</p>
</div>
```

If grid layout `mandates` was 4-column, 9 cards = 2.25 rows. Adjust CSS if needed (existing grid likely handles odd count).

4. **Pipeline section — optional add Phase 2c + 2.6 cards**:

If space allows, add 2 cards in the existing Pipeline grid (between Phase 02 Visual direction card and Phase 03 Custom icons card):

```html
<div class="phase">
  <span class="phase-num">— 02c</span>
  <h3>Macrostructure pick</h3>
  <p>Choose 1 of 7 page-shape archetypes (Marquee Hero / Bento Grid / Long Document / Manifesto / Stat-Led / Workbench / Letter). Diversification check against project memory.</p>
  <span class="ref">macrostructure-catalog.md</span>
</div>

<div class="phase">
  <span class="phase-num">— 02.6</span>
  <h3>Brand Motion Identity</h3>
  <p>Pick motion personality (Playful / Premium / Corporate / Energetic). Locks 3 constants: signature easing + duration palette + entrance pattern.</p>
  <span class="ref">motion-patterns.md § Motion Personalities</span>
</div>
```

5. **Anti-slop self-audit** (final check):
- No new icon library imports introduced
- No Inter/Roboto font references
- No `h-screen` introductions
- No emoji
- No purple-blue gradient
- No inline hex outside CSS vars

## Related code files

**Modify (2 files):**
- `README.md` (L5 version + v2.4.0 paragraph + new FAQ entries + credits update)
- `index.html` (hero version + footer version + Mandate #9 card + optional Pipeline cards)

**Create / Delete:** None

## Implementation steps

1. **Update README.md L5 version** → 2.4.0
2. **Append v2.4.0 update paragraph** (after existing v2.3.0 paragraph)
3. **Insert 2 new FAQ entries** (macrostructure + Brand Motion Identity)
4. **Update credits acknowledge** (Hallmark + motion-design specific attribution for v2.4)
5. **Update index.html hero version** → v2.4.0
6. **Update index.html footer version** → v2.4.0
7. **Add Mandate card #9** (Diversification)
8. **(Optional) Add Pipeline cards** for Phase 2c + 2.6
9. **Run anti-slop self-audit** greps
10. **Final cross-reference check** — verify all links and version mentions consistent

## Todo list
- [ ] Update README.md L5 version
- [ ] Append v2.4.0 update paragraph
- [ ] Insert macrostructure FAQ entry
- [ ] Insert Brand Motion Identity FAQ entry
- [ ] Update credits acknowledge (Hallmark + motion-design specific)
- [ ] Update index.html hero version
- [ ] Update index.html footer version
- [ ] Add Mandate card #9 (Diversification)
- [ ] (Optional) Add Pipeline cards 2c + 2.6
- [ ] Run anti-slop self-audit
- [ ] Final cross-reference check

## Success criteria
- README.md L5 + v2.4.0 paragraph + 2 new FAQ + credits update
- index.html hero + footer = v2.4.0
- New Mandate card #9 in Mandates section
- (Optional) 2 new Pipeline cards for 2c + 2.6
- 0 anti-slop self-violations
- Backward compat: existing Examples (Coffee landing, Portfolio redesign, Blog, Dashboard) render schema-identically

## Risk assessment
- **Risk:** v2.4.0 paragraph too long → keep single paragraph, multi-topic, concise
- **Risk:** index.html Mandate count layout breaks at 9 cards → CSS grid likely auto-handles
- **Risk:** Pipeline cards 2c + 2.6 disrupt section ordering → place between existing cards 02 and 03
- **Risk:** ARIA tab contract violated when adding cards → no ARIA changes needed (Mandates and Pipeline are static cards, not tabs)

## Security considerations
None.

## Next steps
- Final plan-level verification (per plan.md § Final verification):
  1. Grep `v2\.4\.0` → ≥4 matches across SKILL.md / README.md / index.html
  2. Grep `v2\.3\.0` → 0 matches in critical locations (except historical context)
  3. Verify all 5 new reference files exist
  4. Verify workflow-phases.md shrunk + sub-files exist
  5. Smoke test Phase 1-8 backward compat with v2.3 examples
- Update plan.md status → completed
- Mark all phase rows → completed
- User reviews diff, commits manually per CLAUDE.md "No auto-commit"
- Optional: invoke /ck:journal for v2.4.0 release summary
