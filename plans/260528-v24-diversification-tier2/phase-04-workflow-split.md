# Phase 04 — Workflow phases split (4 NEW sub-files) + Phase 2.6 + log.json

## Context links
- [brainstorm.md](./brainstorm.md) § Q10 (proactive workflow split), § Item D (log.json read/write), § Phase 2.6
- [references/workflow-phases.md](../../references/workflow-phases.md) — 820 lines, split into main hub + 4 sub-files
- Depends on Phase 01 + 02 + 03 (cross-references)

## Overview
- **Priority:** Critical (largest structural change in v2.4)
- **Status:** pending
- **Depends on:** Phase 01, 02, 03 (cross-references from this phase to those files)
- **Description:** Split workflow-phases.md (~820 lines) into main hub (~300-350 lines) + 4 sub-references (workflow-brainstorm.md, workflow-plan.md, workflow-implement.md, workflow-audit.md). Add Phase 2.6 (Brand Motion Identity) section. Add `.perfect-ui/log.json` read logic (Phase 0.5) and write logic (Phase 7).

## Key insights
- Split = move content out, not rewrite. Preserve existing protocol text.
- Main workflow-phases.md becomes navigation hub for Phase 0/0.1/0.5/2/2.6/3/4/5 + cross-refs to sub-files for Phase 1/6/7/8
- New Phase 2.6 inserted between existing Phase 2e (motion intensity) and Phase 3 (custom icons)
- log.json read happens at Phase 0.5 (after type detected, before brief)
- log.json write happens at Phase 7-end (after implementation completes)
- Each sub-file has its own internal table of contents

## Requirements

### Functional
- NEW `references/workflow-brainstorm.md` (~150 lines, Phase 1 inline brainstorm protocol from current workflow-phases.md ~200-300)
- NEW `references/workflow-plan.md` (~150 lines, Phase 6 inline plan protocol from current ~470-600)
- NEW `references/workflow-implement.md` (~100 lines, Phase 7 inline implement protocol from current ~620-700)
- NEW `references/workflow-audit.md` (~150 lines, Phase 8 inline audit runner from current ~750-820)
- workflow-phases.md reduced: Phase 0, 0.1, 0.5, 2, 2.6, 3, 4, 5 inline + cross-refs to sub-files for 1, 6, 7, 8
- workflow-phases.md adds new Phase 2.6 section (Brand Motion Identity)
- Phase 0.5 reads `.perfect-ui/log.json` and surfaces diversification check
- Phase 7-end writes new entry to `.perfect-ui/log.json`
- workflow-brainstorm.md has log.json schema documented inline
- workflow-audit.md references gapless bento detection (grep + visual check)

### Non-functional
- Net line change for workflow-phases.md: -500 to -520 (820 → ~300-320)
- Cross-references from main hub to sub-files must resolve
- All existing protocol detail preserved (no content lost in split)
- Phase 2.6 ~25-30 lines new
- log.json schema + read/write logic ~30 lines

## Architecture

### Split source mapping

Current workflow-phases.md sections to extract:

| Current section | Lines (approx) | New file |
|-----------------|----------------|----------|
| Phase 1 — Discovery (inline brainstorm protocol) | ~200-340 | `workflow-brainstorm.md` |
| Phase 6 — Plan (inline plan protocol) | ~440-600 | `workflow-plan.md` |
| Phase 7 — Implement (inline implement protocol) | ~620-700 | `workflow-implement.md` |
| Phase 8 — Anti-Slop Review (inline audit runner) | ~720-820 | `workflow-audit.md` |

Each sub-file:
- Frontmatter title + brief intro
- Full original protocol content (preserved verbatim)
- Cross-references back to main workflow-phases.md (for context navigation)

### Main workflow-phases.md after split (~300 lines)

```markdown
# Workflow Phases — Detailed Walkthrough

Self-contained 8-phase pipeline. The skill conducts every phase directly — no external orchestration skills are invoked. Phases branch by `--type` and tier (special / generic).

For asset generation, the skill describes the *capability* required and uses whichever tool fits (text-to-image, vision-capable analysis, vector trace, React Three Fiber, etc.).

## Phase navigation

Detailed protocols for Phase 1, 6, 7, 8 live in dedicated sub-references:
- **Phase 1 (Discovery)** → `workflow-brainstorm.md`
- **Phase 6 (Plan)** → `workflow-plan.md`
- **Phase 7 (Implement)** → `workflow-implement.md`
- **Phase 8 (Audit)** → `workflow-audit.md`

This main file documents Phase 0, 0.1, 0.5, 2 (all sub-steps including new 2.6), 3, 4, 5.

## Phase 0 — Mode Detection
[existing content preserved]

## Phase 0.1 — Pre-flight scan (auto-detect)
[existing content preserved, expand: now includes log.json read mention]

## Phase 0.5 — Type Detection (No Refusals)
[existing content preserved; ADD log.json read step]

### Step 6 — Read project memory (log.json)

After type detection, before Phase 1, read `.perfect-ui/log.json` if it exists. Surface diversification check:

```
Last 3 builds:
  · Marquee Hero (Tracejam, editorial + warm)
  · Long Document (Maple, editorial + cool)
  · Bento Grid (Foundry, glass-tech)

Diversification rule: macrostructure must NOT be {Marquee Hero, Long Document, Bento Grid}.
Choosing from {Manifesto, Stat-Led, Workbench, Letter} this time.
```

If log.json doesn't exist, silent (first build).

See `macrostructure-catalog.md § Diversification rule` for full rules.

## Phase 2 — Visual Direction
[existing 2a-2e content preserved]

### Phase 2c — Macrostructure pick (NEW v2.4)
After palette + typography + spatial language locked (2a-2c), pick macrostructure. See `macrostructure-catalog.md`.

User picks from 7 macrostructures (Marquee Hero / Bento Grid / Long Document / Manifesto / Stat-Led / Workbench / Letter).

Diversification rule enforces: macrostructure must NOT match any of last 3 entries in log.json. Hard rule; user override allowed with log entry.

### Phase 2d, 2e (intensity)
[existing content preserved]

### Phase 2.6 — Brand Motion Identity (NEW v2.4)

After motion intensity locked (2e), pick motion personality.

```
AskUserQuestion header: "Brand Motion Identity"
Question: "Pick a motion personality (drives signature easing + duration palette + entrance pattern)?"
Options: Playful · Premium · Corporate · Energetic
Default = vibe-derived (see `motion-patterns.md` § Per-vibe personality defaults)
```

3 constants are LOCKED after pick:
1. **Signature easing** — single cubic-bezier curve
2. **Duration palette** — 3 values (quick/standard/slow)
3. **Entrance pattern** — consistent reveal style

See `motion-patterns.md § Motion Personalities` for full table.

## Phase 3 — Custom Icon Set
[existing content preserved]

## Phase 4 — 2D Visual Assets
[existing content preserved]

## Phase 5 — Visual Effect Layer
[existing content preserved]

## Phase 6 — Plan
See `workflow-plan.md` for full inline plan protocol.

## Phase 7 — Implement
See `workflow-implement.md` for full inline implement protocol.

After Phase 7 completes (implementation marked done), append new entry to `.perfect-ui/log.json`:

```json
{
  "date": "{YYYY-MM-DD}",
  "brief": "{1-line summary}",
  "vibe": "{anchor}",
  "wildcard": "{adjective}",
  "macrostructure": "{name}",
  "design_variance": {value 1-10},
  "visual_density": {value 1-10},
  "motion_personality": "{Playful|Premium|Corporate|Energetic}",
  "motion_intensity": {value 0-3},
  "illustration_style": "{from 2d-illustration-catalog.md}"
}
```

Trim log.json to last 20 entries (oldest dropped). Create `.perfect-ui/` directory if missing; respect existing `.gitignore` (suggest adding `.perfect-ui/` on first scan).

## Phase 8 — Anti-Slop Review
See `workflow-audit.md` for full inline audit runner.
```

### Sub-file structure (each sub-file)

```markdown
# Workflow — [Phase Name]

Detailed protocol for Phase N. See `workflow-phases.md` for full phase pipeline navigation.

[Original protocol content from current workflow-phases.md, preserved verbatim]

## Cross-references
- `workflow-phases.md` — full pipeline navigation
- [Other relevant references]
```

### log.json schema (canonical in workflow-brainstorm.md)

Add at top of workflow-brainstorm.md:

```markdown
## Phase 0.5 — Read project memory

`.perfect-ui/log.json` at project root tracks past picks for diversification. Schema:

```json
[
  {
    "date": "2026-05-28",
    "brief": "Specialty coffee subscription — Tokyo home-brew",
    "vibe": "editorial",
    "wildcard": "agrarian",
    "macrostructure": "Marquee Hero",
    "design_variance": 6,
    "visual_density": 3,
    "motion_personality": "Premium",
    "motion_intensity": 2,
    "illustration_style": "silkscreen"
  },
  {...}
]
```

20-entry rolling buffer. Read at Phase 0.5 (this file). Written at Phase 7-end (`workflow-implement.md`).

See `macrostructure-catalog.md § Diversification rule` for hard rule details.
```

## Related code files

**Create (4 NEW):**
- `references/workflow-brainstorm.md` (~150 lines)
- `references/workflow-plan.md` (~150 lines)
- `references/workflow-implement.md` (~100 lines)
- `references/workflow-audit.md` (~150 lines)

**Modify:**
- `references/workflow-phases.md` (~820 → ~300-350 after split; net -450 to -500)

## Implementation steps

1. **Read full workflow-phases.md** to identify exact line ranges for Phase 1, 6, 7, 8 protocol blocks
2. **Extract Phase 1 protocol** → write to NEW `workflow-brainstorm.md` (preserve verbatim + add log.json schema section)
3. **Extract Phase 6 protocol** → write to NEW `workflow-plan.md` (preserve verbatim)
4. **Extract Phase 7 protocol** → write to NEW `workflow-implement.md` (preserve verbatim + add log.json write logic)
5. **Extract Phase 8 protocol** → write to NEW `workflow-audit.md` (preserve verbatim + add gapless bento detection note)
6. **Rewrite main workflow-phases.md:**
   - Keep Phase 0, 0.1, 0.5, 2 (a-e), 3, 4, 5 inline content
   - Add new Phase 2c (Macrostructure pick) section
   - Add new Phase 2.6 (Brand Motion Identity) section
   - Replace Phase 1, 6, 7, 8 inline content with brief intro + cross-link to sub-files
   - Add log.json read step at Phase 0.5
   - Add log.json write step at Phase 7 cross-link
7. **Verify cross-references** — all sub-files reference back to main; main cross-refs to all sub-files; macrostructure-catalog reachable from Phase 2c
8. **Run grep** — confirm Phase 1/6/7/8 inline detail no longer duplicated in main (only in sub-files)

## Todo list
- [ ] Read full workflow-phases.md
- [ ] Identify line ranges for Phase 1, 6, 7, 8
- [ ] Write workflow-brainstorm.md (with log.json schema)
- [ ] Write workflow-plan.md
- [ ] Write workflow-implement.md (with log.json write logic)
- [ ] Write workflow-audit.md
- [ ] Rewrite main workflow-phases.md (preserve Phase 0/0.1/0.5/2/3/4/5, add 2c + 2.6, cross-link to sub-files)
- [ ] Add Phase 2c (Macrostructure pick) section
- [ ] Add Phase 2.6 (Brand Motion Identity) section
- [ ] Add log.json read at Phase 0.5
- [ ] Verify cross-references all resolve
- [ ] Grep duplication check

## Success criteria
- 4 NEW sub-reference files exist with target line counts (150/150/100/150)
- workflow-phases.md shrunk to ~300-350 lines
- Phase 2c (Macrostructure pick) section present
- Phase 2.6 (Brand Motion Identity) section present
- log.json read documented at Phase 0.5
- log.json write documented at Phase 7 cross-link
- All cross-references resolve (no broken links)
- No content lost (Phase 1/6/7/8 detail preserved in sub-files)

## Risk assessment
- **Risk:** Content drift during extraction (modifications creep in) → preserve verbatim; use Read + Write, no Edit on extracted content
- **Risk:** Cross-references break → run grep after split to verify all "see workflow-phases.md § Phase X" references map correctly
- **Risk:** Phase 2.6 disrupts existing Phase 2/2e numbering → insert AFTER 2e (cleanest)
- **Risk:** log.json schema diverges across sub-files → canonical schema in workflow-brainstorm.md; cross-ref from workflow-implement.md
- **Risk:** Main file becomes too thin (just nav) → keep Phase 0/0.1/0.5/2/2.6/3/4/5 inline content; only Phase 1/6/7/8 extracted

## Security considerations
None — file reorganization.

## Next steps
- Phase 05 SKILL.md References table adds 4 new sub-files + macrostructure-catalog
- Phase 05 SKILL.md Mermaid diagram adds Phase 2.6 node
- Phase 05 SKILL.md Phase Method Map adds 2c + 2.6 rows
- Phase 06 README + index.html document the file split
