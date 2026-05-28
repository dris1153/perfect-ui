---
name: v25-new-modes-tier3
status: completed
priority: medium
mode: auto
created: 2026-05-28
completed: 2026-05-28
target: study-mode + component-scope + preemit-design-plan + workflow integration + public surfaces
blockedBy: []
blocks: []
---

# Plan — perfect-ui v2.5.0 New Modes (Tier 3) — FINAL ROADMAP CYCLE

3 items from roadmap Tier 3 (G+H+Q): Study verb + Component-scope branch + Pre-emit `<design_plan>` block. Final cycle of 3-version roadmap (v2.3 → v2.4 → v2.5).

## Source of truth
[brainstorm.md](./brainstorm.md) — full design, Q1-Q7 locked decisions, per-item specifications.
[roadmap brainstorm](../260528-taste-skill-research-upgrades/brainstorm.md) — parent 3-version strategy (now completing).

## Context links
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.4.1"`)
- Workflow split files (post-v2.4): [workflow-phases.md](../../references/workflow-phases.md) · [workflow-brainstorm.md](../../references/workflow-brainstorm.md) · [workflow-implement.md](../../references/workflow-implement.md) · [workflow-audit.md](../../references/workflow-audit.md)
- Macrostructure catalog: [macrostructure-catalog.md](../../references/macrostructure-catalog.md)
- GSAP integration: [gsap-integration.md](../../references/gsap-integration.md)
- Public docs: [README.md](../../README.md), [index.html](../../index.html)
- Prior completed plans (v2.3 / v2.4 / v2.4.1) — all in `plans/`

## Resolved decisions (from brainstorm Q-section)

| # | Decision |
|---|----------|
| Q1 | Full Hallmark parity for Study verb (URL safety + fetch + extraction + diagnosis + 3-way branch) |
| Q2 | Multi-signal component-scope detection (brief ≤30 words + UI element keyword + `--component` flag — 2+ signals confirms) |
| Q3 | Phase 7 pre-emit gate for `<design_plan>` block |
| Q4 | Single v2.5.0 release (1 cycle, all 3 items) |
| Q5 | `--study <URL>` flag syntax |
| Q6 | Component output = component file + standalone `.preview.html` 8-state demo |
| Q7 | `<design_plan>` block full 10-field superset |

## Resolved sub-decisions (from plan args defaults)

1. Study verb refusal list: 7 most common patterns + extensible note
2. design_plan block placement: BOTH (CSS comment as durable record + plans/{slug}/plan.md § Pre-emit verification as audit trail)
3. Component-scope preview wrapper: auto-detect framework from pre-flight scan (React → `.preview.tsx`, Vue → `.preview.vue`, Svelte → `.preview.svelte`, vanilla → `.preview.html`)
4. SKILL.md: add NEW Hard Rule #11 "Pre-emit verification" (cleaner separation from #9/10)
5. index.html Pipeline: 2 separate cards (Phase 0a — Study verb, Phase 0.5b — Component-scope)
6. README v2.5.0: single concise paragraph + 3 FAQs (1 per item)
7. design_plan block validation: collect all errors then report (user fixes once)

## Goal

1. `study-mode.md` exists — full Hallmark parity protocol
2. `component-scope.md` exists — multi-signal detection + 8-state preview output
3. `preemit-design-plan.md` exists — 10-field block schema
4. Phase 0 handles `--study <URL>` mode
5. Phase 0.5 detects component-scope (multi-signal)
6. Phase 7 entry runs design_plan verification (page-scope full 10 fields; component-scope subset)
7. Component-scope short-circuits skip-able phases (Phase 2.5 macro, Phase 8 visual, log.json write)
8. Studied-DNA stamp in CSS for `--study` builds
9. Version 2.5.0 in 4 critical locations
10. Backward compat: existing `--new` / `--redesign` / page-scope outputs schema-identical

## Phases

| # | Phase | Files | Status | Effort |
|---|-------|-------|--------|--------|
| 01 | NEW study-mode.md (full Hallmark parity protocol) | [phase-01-study-mode.md](./phase-01-study-mode.md) | completed | L |
| 02 | NEW component-scope.md + workflow-brainstorm.md studied-DNA mode | [phase-02-component-scope.md](./phase-02-component-scope.md) | completed | M |
| 03 | NEW preemit-design-plan.md + workflow-implement.md Phase 7 gate | [phase-03-preemit-gate.md](./phase-03-preemit-gate.md) | completed | M |
| 04 | workflow-phases.md (Phase 0 + 0.5 routing) + workflow-audit.md (subset filtering) | [phase-04-workflow-routing.md](./phase-04-workflow-routing.md) | completed | M |
| 05 | Public surfaces (SKILL.md v2.5.0 + README + index.html) | [phase-05-public-surfaces.md](./phase-05-public-surfaces.md) | completed | M |

## Key dependencies

```
Wave 1 (parallel-safe — distinct NEW files):
  Phase 01 (study-mode.md)
  Phase 02 (component-scope.md + workflow-brainstorm.md)
  Phase 03 (preemit-design-plan.md + workflow-implement.md)
        ↓
Wave 2:
  Phase 04 (workflow-phases.md + workflow-audit.md — routes to all above)
        ↓
Wave 3:
  Phase 05 (SKILL.md + README.md + index.html — integrates everything)
```

- Phase 01, 02, 03 each own distinct files; can run in parallel
- Phase 04 references all 3 new mode files
- Phase 05 references all preceding output

## File ownership (parallel-safe contracts)

| File | Owner phase | Action | Approx. lines |
|------|-------------|--------|---------------|
| `references/study-mode.md` | 01 | CREATE | +180 |
| `references/component-scope.md` | 02 | CREATE | +100 |
| `references/workflow-brainstorm.md` | 02 | MODIFY (+ studied-DNA input mode section) | +30 |
| `references/preemit-design-plan.md` | 03 | CREATE | +80 |
| `references/workflow-implement.md` | 03 | MODIFY (+ Phase 7 pre-emit gate + component-scope short-circuit) | +40 |
| `references/workflow-phases.md` | 04 | MODIFY (+ Phase 0 `--study` mode + Phase 0.5 component-scope detection) | +30 |
| `references/workflow-audit.md` | 04 | MODIFY (+ component-scope subset filtering) | +10 |
| `SKILL.md` | 05 | MODIFY (frontmatter v2.5.0 + Mermaid +2 nodes + References +3 rows + Phase Method Map +3 rows + Hard Rule #11 + Anti-Rationalization) | +40 |
| `README.md` | 05 | MODIFY (L5 version + v2.5.0 paragraph + 3 new FAQs + credits) | +40 |
| `index.html` | 05 | MODIFY (hero + footer v2.5.0 + 2 Pipeline cards + Mandate update) | +30 |

**Total new content estimate:** ~+360 lines new files + ~+220 lines modifications = ~+580 net new content.

## Success criteria (overall)

- [x] 3 new files exist with target line counts
- [x] `--study <URL>` mode routes to study-mode.md protocol
- [x] Component-scope detection at Phase 0.5 (multi-signal logic documented)
- [x] Phase 7 entry runs design_plan verification (full 10 fields page-scope; subset component-scope)
- [x] Studied-DNA stamp format documented in study-mode.md
- [x] 8-state preview wrapper format auto-detects framework
- [x] Component-scope skips: Phase 2.5 macrostructure, Phase 8 visual checks, log.json write
- [x] Component-scope keeps: Phase 0 pre-flight, Phase 1 genre, Phase 2 vibe/palette/typography, Phase 2.6 Brand Motion Identity, anti-slop universal subset
- [x] SKILL.md frontmatter `version: "2.5.0"` + 3 new References + Hard Rule #11 + Mermaid +2 nodes
- [x] README.md v2.5.0 paragraph + 3 new FAQs + credits
- [x] index.html hero + footer v2.5.0 + 2 Pipeline cards
- [x] Backward compat: existing v2.4.x flows render schema-identically when no `--study` flag and not component-scope
- [x] Self-contained preserved: no external skill dependencies for 3 new modes (gsap-skills optional from v2.4.1)

## Out of scope

- v2.6+ items (no items currently planned in roadmap; v2.5.0 is FINAL cycle)
- Multi-page macrostructure orchestration
- design_plan block versioning / schema migration
- Study verb deep DNA reconstruction (extracted DNA = inputs to Phase 1; doesn't auto-recreate exact site)
- Component-scope cross-component dependency analysis (single component only)
- WebFetch authentication / private URL access
- Hard Rule #11 enforcement automation (manual user verification at Phase 7 entry)
- Storybook story file emission (defer; .preview.* is default)

## Risks

| Risk | Mitigation |
|------|------------|
| Study verb URL fetch fails / blocked | Graceful fallback to screenshot prompt; refuse non-readable sources |
| Component-scope auto-detect false positive | Default to page-scope; require 2+ signals to confirm component; escape hatch (`--page-scope` override) |
| `<design_plan>` block 10 fields = friction at every Phase 7 entry | Many fields auto-verifiable (no user prompt); collect-all-errors approach (one fix pass per emit) |
| Studied-DNA stamp drift (code diverges from stamped DNA) | Phase 8 audit checks stamp matches actual implementation; flag drift |
| Component-scope output format ambiguity (Storybook vs preview) | Pre-flight scan detects Storybook → conditional emission; default `.preview.*` |
| Study verb refusal list missing patterns | List 7 most common + "extensible — log overrides" note |
| Phase 7 pre-emit gate blocks legitimate workflows | Provide override mechanism (logged in `plans/{slug}/overrides.md`) |
| v2.5.0 = largest cycle, review fatigue | Phase breakdown keeps each phase file <200 lines; parallel-safe Wave 1 enables concurrent review |

## Final verification (last task before plan.md status → completed)

1. Run grep: `grep -rE 'v?2\.4\.1' SKILL.md README.md index.html` → 0 stale matches (excluding historical changelog paragraphs)
2. Run grep: `grep -rE 'v?2\.5\.0' SKILL.md README.md index.html` → ≥4 matches (frontmatter + L5 + hero + footer)
3. Verify all 3 new reference files exist + sized appropriately
4. Verify Phase 0 `--study` mode in workflow-phases.md
5. Verify Phase 0.5 component-scope detection in workflow-phases.md
6. Verify Phase 7 pre-emit gate in workflow-implement.md
7. Verify SKILL.md Hard Rule #11 + 3 new References rows + Mermaid +2 nodes
8. Backward compat smoke test: read README Example 1 (coffee landing, page-scope, `--new`) — confirm Phase 1-8 schema-identical (no behavior change for non-study / non-component briefs)
