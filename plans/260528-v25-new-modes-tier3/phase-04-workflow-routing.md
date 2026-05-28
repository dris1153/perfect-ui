# Phase 04 — workflow-phases.md + workflow-audit.md routing

## Context links
- [brainstorm.md](./brainstorm.md) § Workflow integration
- [phase-01-study-mode.md](./phase-01-study-mode.md), [phase-02-component-scope.md](./phase-02-component-scope.md), [phase-03-preemit-gate.md](./phase-03-preemit-gate.md) — depends on (cross-references)

## Overview
- **Priority:** Critical (routes all 3 new modes into existing workflow)
- **Status:** pending
- **Depends on:** Phase 01, 02, 03 (NEW files must exist for cross-references)
- **Description:** Add Phase 0 `--study` mode detection + Phase 0.5 component-scope detection to workflow-phases.md. Add component-scope subset filtering to workflow-audit.md.

## Key insights
- workflow-phases.md owns mode routing (Phase 0 / 0.5)
- workflow-audit.md needs component-scope-aware filtering (skip visual checks for component-scope)
- Both modifications are integration glue — short additions referencing NEW files
- Backward compat critical — existing `--new` / `--redesign` / page-scope flows untouched

## Requirements

### Functional
- workflow-phases.md Phase 0 adds `--study <URL>` mode branch (referencing study-mode.md)
- workflow-phases.md Phase 0.5 adds component-scope detection step (referencing component-scope.md)
- workflow-audit.md adds component-scope subset filtering (skip visual checks Step F)

### Non-functional
- workflow-phases.md grows ~+30 lines
- workflow-audit.md grows ~+10 lines
- Existing protocol content untouched (additive only)

## Architecture

### workflow-phases.md — Phase 0 `--study` mode

Insert AFTER existing Phase 0 mode detection rules, BEFORE Phase 0.1:

```markdown
### `--study <URL>` mode (NEW v2.5.0)

If `--study <URL>` flag passed OR user provides URL with intent keywords ("study this", "extract DNA", "use as reference"), enter Study Mode.

Routing:
1. Phase 0 detects `--study` mode
2. Run `study-mode.md § URL safety` refusal check
3. If passes: run `study-mode.md § URL fetch` + `§ DNA extraction`
4. Emit diagnosis report per `study-mode.md § Diagnosis report format`
5. Wait for user response (3-way branch):
   - "Build with this DNA" → continue to Phase 0.5 with extracted DNA as locked inputs
   - "Lock the DNA" → emit `design.md`, end session
   - Silence / "stop" → diagnosis IS deliverable, end session
6. If "build with DNA" → Phase 0.5 uses Studied-DNA input mode (`workflow-brainstorm.md § Studied-DNA input mode`); diversification suspended

See `study-mode.md` for full protocol.
```

### workflow-phases.md — Phase 0.5 component-scope detection

Insert AFTER existing Phase 0.5 Step 6 (Read project memory log), BEFORE Step "No refusals":

```markdown
### Step 7 — Component-scope detection (NEW v2.5.0)

After type detection, check component-scope signals (per `component-scope.md § When this applies`):

1. Multi-signal check: brief ≤30 words + UI element keyword + `--component` flag
2. If 2+ signals fire → component scope confirmed. State explicitly: *"Component-scope: 2 signals matched (short brief + 'button' keyword). Skipping macrostructure / nav / footer / hero enrichment."*
3. If only 1 signal fires (ambiguous) → ask via `AskUserQuestion`: *"One component or whole page?"*. Default to component if user doesn't engage
4. If 0 signals fire OR page-flow signals dominate → stay in page scope (current behavior)

Component-scope routing:
- Skip Phase 2.5 macrostructure pick, Phase 2c spatial language, hero enrichment
- Keep Phase 2 vibe/palette/typography, Phase 2.6 Brand Motion Identity
- Phase 7 collapses page-level emission (see `workflow-implement.md § Step 1.6`)
- Phase 8 runs subset (see `workflow-audit.md § Component-scope subset`)
- Skip `.perfect-ui/log.json` write (component runs don't rotate)

See `component-scope.md` for full protocol + signal list.
```

### workflow-audit.md — Component-scope subset filtering

Insert NEW § Step Y — Component-scope subset (v2.5.0+) AFTER existing § Step F (Visual checks), BEFORE § Step G:

```markdown
### Step Y — Component-scope subset (v2.5.0+, runs ONLY if component-scope detected at Phase 0.5)

When Phase 0.5 detected component-scope (see `component-scope.md`), Phase 8 audit runs a filtered subset:

**Skip:**
- Step F Visual checks (no full page to render)
- Macrostructure-specific checks (component has no macrostructure)
- Diversification rule check (component runs don't rotate)
- Marketing-only grep checks (component is element, not section)

**Keep:**
- Step B `[universal]` grep checks — emoji / icon libraries / forbidden fonts / inline hex / motion respect
- Anti-slop universal subset (contrast 46-50, a11y typography gates)
- 8-state coverage check — verify component renders correctly in all 8 states (default / hover / focus / active / disabled / loading / error / success)

Output report format (component-scope):

```markdown
# Anti-slop audit — {slug} (component-scope)

## Context
- Component: <type>
- Vibe: <vibe>
- Motion personality: <personality>

## Filter
- Applicable: universal rules only + 8-state coverage
- Skipped: visual / macrostructure / diversification / marketing

## Grep + 8-state results
| Check | Result |
|-------|--------|
| ... | ... |

## Verdict
- PASS / FAIL
```

See `component-scope.md` for full short-circuit logic.
```

## Related code files

**Modify:**
- `references/workflow-phases.md` (+ Phase 0 `--study` mode + Phase 0.5 component-scope detection, ~+30 lines)
- `references/workflow-audit.md` (+ Step Y component-scope subset, ~+10 lines)

**Create / Delete:** None

## Implementation steps

1. Read workflow-phases.md to identify insertion points (Phase 0 end before 0.1; Phase 0.5 Step 6 end before "No refusals")
2. Insert `--study` mode section in Phase 0
3. Insert Step 7 component-scope detection in Phase 0.5
4. Read workflow-audit.md to identify insertion point (after Step F Visual, before Step G Performance)
5. Insert Step Y component-scope subset
6. Verify cross-references to study-mode.md / component-scope.md / preemit-design-plan.md resolve

## Todo list
- [ ] Read workflow-phases.md, find insertion points
- [ ] Insert `--study` mode section in Phase 0
- [ ] Insert Step 7 component-scope detection in Phase 0.5
- [ ] Read workflow-audit.md, find insertion point
- [ ] Insert Step Y component-scope subset
- [ ] Verify cross-references resolve

## Success criteria
- workflow-phases.md Phase 0 has `--study` mode section
- workflow-phases.md Phase 0.5 has Step 7 (component-scope detection)
- workflow-audit.md has Step Y (component-scope subset)
- File growth: workflow-phases ~+30; workflow-audit ~+10
- Existing protocol content untouched
- Cross-references resolve (study-mode.md / component-scope.md / preemit-design-plan.md)
- Backward compat: existing `--new` / `--redesign` / page-scope flows unchanged

## Risk assessment
- **Risk:** Phase 0 mode detection ordering — `--study` interacts with `--new` / `--redesign` → `--study` takes precedence (explicit URL extraction); `--new` / `--redesign` mutually exclusive
- **Risk:** Phase 0.5 Step 7 insertion conflicts with existing numbering → use Step 7 (decimal-free; existing v2.4 used Step 6 for log read)
- **Risk:** workflow-audit.md Step Y label conflicts with existing letter sequence (A-H) → Y deliberately distinct (clear it's a NEW v2.5.0 step, not in sequence)
- **Risk:** Cross-references break post-edit → run grep after to verify

## Security considerations
None — documentation routing only.

## Next steps
- Phase 05 SKILL.md Mermaid diagram adds 2 nodes (Phase 0 --study, Phase 0.5 component-scope)
- Phase 05 SKILL.md Phase Method Map +3 rows
- Phase 05 documents all changes in README + index.html
