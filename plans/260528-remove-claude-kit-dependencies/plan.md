---
name: remove-claude-kit-dependencies
status: completed
priority: medium
mode: auto
created: 2026-05-28
completed: 2026-05-28
target: SKILL.md, README.md, index.html, references/, assets/
blockedBy: []
blocks: []
---

# Plan — Remove Claude Kit dependencies (self-contained perfect-ui v2.2.0)

Gỡ tất cả `ck:` / `ckm:` references + `code-reviewer` agent delegation khỏi active files. Inline brainstorm/plan/cook/audit workflows tailored cho perfect-ui (NOT copy 100% từ ck-skills). Asset gen tools → capability-based descriptions. § Beyond + Related Skills generic-ized.

## Source of truth
[brainstorm.md](./brainstorm.md) — full design, grep audit (12 files / 119 occurrences), evaluated approaches, capability mapping, trade-offs.

## Context links
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.1.0"`)
- Workflow detail: [references/workflow-phases.md](../../references/workflow-phases.md)
- Public docs: [README.md](../../README.md), [index.html](../../index.html)
- Related prior plans: [260528-open-scope-page-types/plan.md](../260528-open-scope-page-types/plan.md) (completed, v2.1.0)

## Resolved decisions (from brainstorm unresolved Q-section)

1. **workflow-phases.md target size** → accept ~800 lines; split only if execution exceeds 1200
2. **Historical plans/ folder** → untouched (artifacts of past state, do NOT rewrite history)
3. **Anti-rationalization rows** → keep existing + update wording to reflect v2.2.0 self-contained mode
4. **quick_validate.py in README** → keep (skill-creator is Anthropic tool, not Claude Kit)

## Goal

1. `grep -rE 'ck:|ckm:|code-reviewer agent' SKILL.md README.md index.html references/ assets/` → 0 matches
2. Phase 1/6/7/8 contain inline workflow protocols (HEAVY depth)
3. Asset gen references → capability-based (no specific tool names)
4. § Beyond + Related Skills → 3 generic capability rows each
5. Version 2.1.0 → 2.2.0 in SKILL.md, README.md, index.html (hero + footer)
6. Backward compat: landing/portfolio output flows identical pre/post

## Phases

| # | Phase | Files | Status | Effort |
|---|-------|-------|--------|--------|
| 01 | workflow-phases.md heavy inline expansion | [phase-01-workflow-phases-inline.md](./phase-01-workflow-phases-inline.md) | completed | L |
| 02 | Reference files capability cleanup | [phase-02-reference-files-capability-cleanup.md](./phase-02-reference-files-capability-cleanup.md) | completed | M |
| 03 | SKILL.md cleanup + version bump | [phase-03-skill-md-cleanup.md](./phase-03-skill-md-cleanup.md) | completed | M |
| 04 | README.md cleanup | [phase-04-readme-cleanup.md](./phase-04-readme-cleanup.md) | completed | M |
| 05 | index.html cleanup + version bump | [phase-05-index-html-cleanup.md](./phase-05-index-html-cleanup.md) | completed | M |

## Key dependencies

```
Phase 01 (workflow-phases.md = canonical inline workflows)
   ↓ (other files reference inline workflows + capability descriptions)
Phase 02 (reference files capability cleanup — 8 files)
   ↓ (SKILL.md references both inline workflows + capability descriptions)
Phase 03 (SKILL.md cleanup + version)
   ↓ (README + index.html consistent with SKILL.md)
Phase 04 (README.md) ⊥ Phase 05 (index.html) — parallel-safe, different files
```

## File ownership (parallel-safe contracts)

| File | Owner phase | Action | Hit count |
|------|-------------|--------|-----------|
| `references/workflow-phases.md` | 01 | MODIFY (heavy inline + tool routing) | 22 |
| `references/visual-asset-prompt-library.md` | 02 | MODIFY (tool routing → capability table) | 7 |
| `references/2d-illustration-catalog.md` | 02 | MODIFY (per-style tool routing) | 15 |
| `references/custom-icon-pipeline.md` | 02 | MODIFY (icon gen routing) | 5 |
| `references/redesign-audit-checklist.md` | 02 | MODIFY (audit refs) | 4 |
| `references/visual-effect-patterns.md` | 02 | MODIFY (ck:threejs → React Three Fiber) | 1 |
| `references/visual-direction-guide.md` | 02 | MODIFY (minor mention) | 1 |
| `references/motion-patterns.md` | 02 | MODIFY (minor mention) | 1 |
| `assets/nextjs-skeleton/section-archetypes.md` | 02 | MODIFY (minor mention) | 1 |
| `SKILL.md` | 03 | MODIFY (orchestration + rules + § Beyond + version) | 22 |
| `README.md` | 04 | MODIFY (examples + FAQ + Related Skills + version) | 26 |
| `index.html` | 05 | MODIFY (phase cards + § Beyond + version) | 14 |

## Success criteria (overall)

- [ ] Final grep: `grep -rE 'ck:|ckm:' SKILL.md README.md index.html references/ assets/` returns 0 matches
- [ ] Final grep: `grep -rE 'code-reviewer\s+(agent|sub-?agent)' SKILL.md README.md index.html references/ assets/` returns 0 matches (or only neutral mentions)
- [ ] workflow-phases.md has 4 inline protocols (Phase 1/6/7/8) with question scripts, templates, checklists
- [ ] Capability descriptions used consistently across asset-related references
- [ ] § Beyond and Related Skills have exactly 3 rows, no specific skill names
- [ ] Version 2.2.0 in SKILL.md frontmatter, README line 5, index.html hero + footer
- [ ] No anti-slop self-violations in new content (Tier 1 audit passes)
- [ ] Cross-references between files resolve (no broken links to removed ck-skill names)
- [ ] Backward compat: landing/portfolio workflow outputs schema-identical (brief.md, plan.md, phase files, etc.)

## Out of scope

- Historical plans/ folder cleanup (per decision 2 above)
- Removing skill-creator references (per decision 4)
- Building competing ck-skill ecosystem (just removing dependency, not replacing skills outside perfect-ui)
- Adding new asset-gen capabilities (just describing existing ones generically)
- Plan-file format changes (existing format works)

## Risks

| Risk | Mitigation |
|------|------------|
| workflow-phases.md exceeds 1200 lines | Split into sub-references only if exceeded; target 800 |
| Inline content drifts from ck-skills nuance | Capture essence (workflow + outputs + constraints), not implementation details |
| Capability descriptions too vague | Pair each capability with concrete prompt template inline |
| Phase 8 audit becomes verbose in-thread | Grep checks short by design; visual check single AI call |
| Missing some ck: occurrence (false negative in grep) | Final verification step runs grep + manual scan of high-hit files |
| Anti-rationalization table rows reference ck-skills | Update wording — keep concept, replace skill names with capability descriptions |

## Final verification (last task before plan.md status → completed)

1. Run grep audit: zero match for `ck:|ckm:|code-reviewer agent` in active files
2. Verify version 2.2.0 in 4 locations (SKILL frontmatter, README L5, index.html hero, index.html footer)
3. Spot-check 1 file per phase to confirm cross-file consistency (e.g. SKILL.md § Beyond ≡ index.html § Beyond ≡ README Related Skills — all 3 reference same 3 capabilities)
4. Confirm landing/portfolio anatomy + skeleton files untouched (zero risk of regression)

## Outcome

- **Final grep:** 0 matches for `\b(ck|ckm):` and 0 matches for `code-reviewer (agent|subagent)` across SKILL.md, README.md, index.html, references/, assets/ (excludes plans/ historical artifacts per design decision)
- **Version 2.2.0:** confirmed in SKILL.md frontmatter, README L5, index.html hero L564, index.html footer L1225
- **Files modified (12 total):**
  - HIGH: SKILL.md (frontmatter desc + version + Hard Rules + Mermaid + Phase 1/6/7/8 headings + § Beyond + § Phase Method Map + Anti-Rationalization), README.md (version + v2.2.0 paragraph + pipeline list + Examples 1-4 + Suggested + Tech Stack + FAQ + Related Workflows), index.html (hero version + Phase cards 01/06/07/08 + Coffee tab panel + § Beyond + footer version), references/workflow-phases.md (Phase 1 inline brainstorm protocol + Phase 4 capability table + Phase 5 GLB exception + Phase 6 inline plan protocol + Phase 7 inline implement protocol + Phase 8 inline audit runner)
  - MEDIUM: references/2d-illustration-catalog.md (14 hits → capability descriptions), references/visual-asset-prompt-library.md (Tool Routing → Capability Routing), references/custom-icon-pipeline.md (Method 2 Paths A/B/C), references/redesign-audit-checklist.md (Steps 1, 4, audit template, hand-off)
  - MINOR: references/visual-effect-patterns.md (1 hit)
- **Files untouched:** all anti-slop / loading-ui / anatomy / skeleton / motion-patterns / visual-direction-guide / section-archetypes files (false positives from substring match); plans/ historical artifacts
- **workflow-phases.md size:** 573 → 804 lines (within ~800 target, well under 1200 hard limit)
- **Backward compat:** landing/portfolio flow behavior identical (Phase 1/6/7/8 inline protocols generate same brief.md / plan.md / phase files / audit reports as pre-v2.2.0 delegation)
- **No commits created** — per user CLAUDE.md "No auto-commit" preference. User reviews and commits manually.
