---
name: v24-diversification-tier2
status: completed
priority: medium
mode: auto
created: 2026-05-28
completed: 2026-05-28
target: workflow split, macrostructure layer, dials, motion personalities, hero catalog
blockedBy: []
blocks: []
---

# Plan — perfect-ui v2.4.0 Diversification (Tier 2)

7 items from roadmap Tier 2 (D+E+F+K+T+O+R) + 1 architectural change (workflow-phases.md split). Major structural release.

## Source of truth
[brainstorm.md](./brainstorm.md) — full design, Q1-Q10 locked decisions, per-item specifications.
[roadmap brainstorm](../260528-taste-skill-research-upgrades/brainstorm.md) — parent v2.3 → v2.4 → v2.5 strategy.

## Context links
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.3.0"`)
- Public docs: [README.md](../../README.md), [index.html](../../index.html)
- Existing workflow (~820 lines): [references/workflow-phases.md](../../references/workflow-phases.md)
- Existing motion patterns: [references/motion-patterns.md](../../references/motion-patterns.md)
- Existing visual direction: [references/visual-direction-guide.md](../../references/visual-direction-guide.md)
- Existing section archetypes (A1-A4 hero): [assets/nextjs-skeleton/section-archetypes.md](../../assets/nextjs-skeleton/section-archetypes.md)
- Anti-slop rules: [references/anti-slop-rules.md](../../references/anti-slop-rules.md)
- Prior completed v2.3 plan: [260528-v23-completeness-tier1/plan.md](../260528-v23-completeness-tier1/plan.md)

## Resolved decisions (from brainstorm Q-section)

| # | Decision |
|---|----------|
| Q1 | NEW `macrostructure-catalog.md` (~200 lines) |
| Q2 | Hallmark vocabulary (Marquee Hero / Bento Grid / Long Document / Manifesto / Stat-Led / Workbench / Letter) |
| Q3 | Full `.perfect-ui/log.json` 20-entry rolling |
| Q4 | Per-vibe DESIGN_VARIANCE + VISUAL_DENSITY defaults |
| Q5 | Personality × Intensity matrix (independent axes) |
| Q6 | Hero composition catalog expanded in section-archetypes.md |
| Q7 | Gapless Bento inline in macrostructure-catalog.md |
| Q8 | Atmosphere spectrum inline in dial definition |
| Q9 | NEW Phase 2.6 (Brand Motion Identity) separate from Phase 2e |
| Q10 | PROACTIVE SPLIT — workflow-phases.md → 4 sub-references |

## Resolved sub-decisions (from plan args defaults)

1. Workflow split granularity: 4 sub-files (brainstorm/plan/implement/audit) — confirmed
2. macrostructure-catalog per-macro depth: ~25-30 lines each (7 macros × 28 lines = ~200 line file)
3. Empty bento detection: Phase 8 audit greps for `grid-flow-dense` presence + visual check via vision model
4. log.json write timing: Phase 7-end (skill writes; user doesn't action)
5. Hero archetype IDs: extend existing A1-A4 → add A5-A13 (no conflict; A1-A4 untouched, A5-A13 new)
6. Phase 2.6 dialog: separate `AskUserQuestion` (cleaner)
7. index.html new Mandate "Diversify each run": ADD new card #9 (or fold based on space)
8. README v2.4.0 paragraph: 1 paragraph multi-topic (concise)

## Goal

1. `.perfect-ui/log.json` format defined + Phase 0.5 read + Phase 7 write
2. `macrostructure-catalog.md` exists with 7 fully-spec'd macrostructures (Hallmark vocab)
3. `visual-direction-guide.md` has DESIGN_VARIANCE + VISUAL_DENSITY dials with atmosphere spectrum + per-vibe defaults
4. `motion-patterns.md` has Motion Personalities table + Brand Motion Identity matrix
5. `workflow-phases.md` split into 4 sub-references; main file shrinks ~820 → ~250-300
6. New Phase 2.6 (Brand Motion Identity) integrated in workflow
7. Hero composition catalog A5-A13 added to section-archetypes.md
8. Empty bento Tier 1 rule in anti-slop-rules.md
9. Version 2.4.0 in 4 critical locations
10. Diversification rule documented and enforceable
11. Backward compat: existing v2.3 outputs schema-identical

## Phases

| # | Phase | Files | Status | Effort |
|---|-------|-------|--------|--------|
| 01 | Foundation refs — anti-slop + visual-direction-guide (dials + atmosphere + defaults) | [phase-01-foundation-refs.md](./phase-01-foundation-refs.md) | completed | M |
| 02 | Motion personalities + Brand Motion Identity matrix | [phase-02-motion-personalities.md](./phase-02-motion-personalities.md) | completed | M |
| 03 | NEW macrostructure-catalog.md + section-archetypes.md Hero catalog A5-A16 | [phase-03-macrostructure-hero-catalog.md](./phase-03-macrostructure-hero-catalog.md) | completed | L |
| 04 | workflow-phases.md split (4 NEW sub-files) + Phase 2.5 + 2.6 + log.json read/write logic | [phase-04-workflow-split.md](./phase-04-workflow-split.md) | completed | L |
| 05 | SKILL.md — v2.4.0 + Mermaid 2.5+2.6 + References table + Hard Rule #10 | [phase-05-skill-md.md](./phase-05-skill-md.md) | completed | M |
| 06 | Public surfaces — README.md + index.html | [phase-06-public-surfaces.md](./phase-06-public-surfaces.md) | completed | M |

## Key dependencies

```
Wave 1 (parallel-safe):
  Phase 01 (anti-slop + visual-direction-guide)
  Phase 02 (motion-patterns)
  Phase 03 (macrostructure-catalog + section-archetypes)
        ↓
Wave 2:
  Phase 04 (workflow split — references all above)
        ↓
Wave 3 (parallel-safe):
  Phase 05 (SKILL.md — references new files post-split)
  Phase 06 (README + index.html — documents all changes)
```

- Phase 01, 02, 03 each own distinct files; can run in parallel
- Phase 04 references new files from 01-03 (cross-link macrostructure-catalog from workflow-plan.md sub-file)
- Phase 05 + 06 both reference all preceding output — parallel-safe with each other (different files)

## File ownership (parallel-safe contracts)

| File | Owner phase | Action | Approx. lines |
|------|-------------|--------|---------------|
| `references/anti-slop-rules.md` | 01 | MODIFY (+ Empty bento Tier 1 rule + diversification rule reference) | +20 |
| `references/visual-direction-guide.md` | 01 | MODIFY (+ § 2 dials + atmosphere + per-vibe defaults table) | +80 |
| `references/motion-patterns.md` | 02 | MODIFY (+ § Motion Personalities + per-vibe defaults) | +80 |
| `references/macrostructure-catalog.md` | 03 | CREATE | +200 |
| `assets/nextjs-skeleton/section-archetypes.md` | 03 | MODIFY (+ Hero archetypes A5-A13) | +50 |
| `references/workflow-brainstorm.md` | 04 | CREATE (extracted from workflow-phases.md) | +150 |
| `references/workflow-plan.md` | 04 | CREATE (extracted) | +150 |
| `references/workflow-implement.md` | 04 | CREATE (extracted) | +100 |
| `references/workflow-audit.md` | 04 | CREATE (extracted) | +150 |
| `references/workflow-phases.md` | 04 | MODIFY (content moves out, Phase 2.6 added, cross-refs to sub-files) | net -350 to -400 (820→~300-350 after split + Phase 2.6 add) |
| `SKILL.md` | 05 | MODIFY (frontmatter version + Phase 2.6 in Mermaid + References table + Phase Method Map) | +30 |
| `README.md` | 06 | MODIFY (L5 version + v2.4.0 paragraph + new FAQ + credits) | +30 |
| `index.html` | 06 | MODIFY (version hero + footer + Mandate card + Pipeline) | +25 |

**Total new content estimate:** ~+650 lines across 5 NEW files + ~+285 in MODIFIED files = ~+935 net new content.
**Workflow-phases.md net shrinkage:** ~820 → ~300-350 (-450 to -520 lines moved to sub-files).

## Success criteria (overall)

- [ ] 5 new files exist with target line counts
- [ ] workflow-phases.md shrunk from ~820 → ~300-350 lines (content moved to sub-references)
- [ ] Phase 2.6 (Brand Motion Identity) integrated in workflow + Mermaid diagram
- [ ] macrostructure-catalog.md has 7 macros with Hallmark vocabulary
- [ ] visual-direction-guide.md has 2 dials + atmosphere spectrum + per-vibe defaults (11 vibes)
- [ ] motion-patterns.md has Motion Personalities table + Brand Motion Identity locked constants
- [ ] section-archetypes.md has Hero catalog A1-A13 (extended)
- [ ] anti-slop-rules.md has Empty bento Tier 1 rule
- [ ] SKILL.md frontmatter `version: "2.4.0"` + Phase 2.6 reference + 5 new files in References table
- [ ] README.md v2.4.0 update paragraph + new FAQ + credits acknowledge
- [ ] index.html hero + footer version 2.4.0 + new Mandate card
- [ ] Diversification rule documented: macrostructure differ-from-last-3 hard rule; dials differ-≥3 warn rule
- [ ] `.perfect-ui/log.json` schema defined + Phase 0.5 read + Phase 7 write logic
- [ ] Cross-references intact post-workflow-phases-split (no broken links)
- [ ] Backward compat: v2.3 examples render schema-identically

## Out of scope

- v2.5 items (G study verb, H component-scope, Q design_plan block)
- Per-vibe Personality default beyond initial 4 → 11 mapping
- Macrostructure-specific section archetype expansion beyond Hero catalog (defer to v2.5)
- Automatic macrostructure picking (always user-confirms or vibe-default)
- log.json analytics features (just append-and-read, no analysis)
- Cross-project log sharing (per-project only)
- Macrostructure × Type tier filtering (Workbench available everywhere; consumer choice)
- Personality × Intensity 3D matrix beyond per-vibe defaults

## Risks

| Risk | Mitigation |
|------|------------|
| 5 new files at once = bloat | Each file has distinct concern; cross-references audit in Phase 04 |
| workflow-phases.md split breaks existing cross-references in SKILL.md / other refs | Phase 05 includes cross-reference audit + verify all "see workflow-phases.md § Phase X" links resolve to correct sub-file |
| log.json schema drift across versions | Lock schema in macrostructure-catalog.md + cross-ref in workflow-brainstorm.md |
| Diversification rule too rigid (every run blocks) | Soft enforcement — warn for vibe/dial repeats; hard enforce only macrostructure-last-3 |
| Per-vibe dial defaults conflict with macrostructure defaults | Resolution: vibe sets default, macrostructure adjusts ±2, user override wins |
| Phase 2.6 disrupts existing Phase 2/2e numbering | Insert AFTER 2e; don't renumber existing phases |
| Hero catalog A5-A13 conflicts with existing A1-A4 | Verified: A1-A4 are landing-specific; A5-A13 extend the catalog. Document continuity. |
| Workflow split files diverge over time (multi-source-of-truth) | Lock convention: main workflow-phases.md owns phase numbering; sub-files own protocol detail |
| Backward compat regression (v2.3 outputs change) | Phase 06 includes smoke test step |

## Final verification (last task before plan.md status → completed)

1. Run grep: `grep -rE 'v?2\.3\.0' SKILL.md README.md index.html` → 0 stale matches (excluding historical context)
2. Run grep: `grep -rE 'v?2\.4\.0' SKILL.md README.md index.html` → ≥4 matches (frontmatter + L5 + hero + footer)
3. Verify all 5 new reference files exist + sized appropriately
4. Verify `workflow-phases.md` shrunk by ~450-500 lines (content moved)
5. Verify all cross-references from main workflow-phases.md to sub-files resolve
6. Verify `macrostructure-catalog.md` has 7 sections + Hallmark vocabulary
7. Verify Phase 2.6 in Mermaid diagram + Phase Method Map
8. Backward compat smoke test: read existing Example 1 (coffee landing in README) — confirm Phase 1-8 schema-identical
