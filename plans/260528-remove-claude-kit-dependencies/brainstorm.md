# Remove Claude Kit dependencies — self-contained perfect-ui

**Date:** 2026-05-28
**Status:** Brainstorm complete, awaiting plan approval
**Skill version impact:** v2.1.0 → v2.2.0 (minor — architectural, backward-compatible semantics)

---

## Problem statement

Perfect-ui hiện orchestrate external Claude Kit skills (`ck:brainstorm`, `ck:plan`, `ck:cook`, `ck:ai-artist`, `ck:ai-multimodal`, `ck:threejs`, `ckm:design`, `code-reviewer` agent). Khi user không có ck-ecosystem hoặc dùng môi trường khác, workflow degrades. User muốn skill self-contained — gỡ tất cả ck:/ckm: references, inline brainstorm/plan/cook/audit workflows tailored cho perfect-ui (NOT copy 100%), reference asset gen tools bằng capability descriptions.

## Grep audit — exact scope

**12 active files, 119 occurrences:**

| File | Hits | Category |
|------|-----:|----------|
| README.md | 26 | High — examples, FAQ, Related Skills |
| SKILL.md | 22 | High — orchestration, references, Hard Rules, examples, § Beyond |
| references/workflow-phases.md | 22 | High — phase prompts (1/6/7/8), tool routing |
| references/2d-illustration-catalog.md | 15 | Medium — tool routing per style |
| index.html | 14 | High — phase cards, § Beyond, file tree |
| references/visual-asset-prompt-library.md | 7 | Medium — tool routing table |
| references/custom-icon-pipeline.md | 5 | Medium — icon gen routing |
| references/redesign-audit-checklist.md | 4 | Low — audit references |
| references/visual-effect-patterns.md | 1 | Minor |
| references/visual-direction-guide.md | 1 | Minor |
| references/motion-patterns.md | 1 | Minor |
| assets/nextjs-skeleton/section-archetypes.md | 1 | Minor |

**Untouched:** plans/ historical folders, anti-slop-rules.md, loading-ui-patterns.md, landing-anatomy.md, portfolio-anatomy.md, generic-page-anatomy.md, landing-skeleton.md, portfolio-skeleton.md, generic-page-skeleton.md.

## Requirements (locked from user)

| ID | Requirement | Source |
|----|-------------|--------|
| R1 | Inline depth = **HEAVY** — full workflow inlined for Phase 1/6/7/8 | User explicit |
| R2 | Asset gen tools = **capability-based descriptions** (e.g., "text-to-image model with style control") | User explicit |
| R3 | § Beyond + Related Skills = **generic-ize** (keep routing concept, no ck-skill names) | User explicit |
| R4 | Grep audit before plan — file list is exact | User explicit |
| R5 | Phase 8 audit = **inline grep + checklist** (no code-reviewer agent delegation) | User explicit |
| R6 | NOT copy 100% — adapt brainstorm/plan/cook for perfect-ui's specific needs | User explicit |
| R7 | Historical plans/ untouched (artifacts of past state) | Default — surfaced for user confirmation |

## Evaluated approaches

### Approach A — Light removal (REJECTED)
Just rename `ck:X` to `X` in delegation calls. No workflow inlining.
- Pros: minimal change (~50 lines)
- Cons: workflow becomes mushy; Phase 1/6/7 lose how-to guidance
- User picked HEAVY → rejected

### Approach B — Selective inline (REJECTED)
Inline brainstorm/plan, leave cook to constraints-only.
- Mixed depth
- User picked HEAVY → rejected

### Approach C — Heavy inline (CHOSEN)
Full inline workflows for Phase 1/6/7/8, capability-based asset gen, generic-ized § Beyond.
- Pros: self-contained, portable, no external dependencies
- Cons: workflow-phases.md grows ~+300 lines; risk of drift from ck-best-practices
- Selected

## Final design

### 1. Workflow inline replacements

**Phase 1 (Discovery) — replace `ck:brainstorm`:**
- Inline question script (type-branched: landing / portfolio / generic)
- brief.md schema with every field defined
- Approval gate logic
- Scope-decomposition rules for too-large requests
- ~80 lines

**Phase 6 (Plan) — replace `ck:plan`:**
- plan.md frontmatter spec + body template
- phase-XX.md naming + structure
- Dependency analysis rules
- Parallel-safe file ownership contracts
- Success criteria format
- ~80 lines

**Phase 7 (Implement) — replace `ck:cook`:**
- Atomic commit pattern (one phase → one focused commit; user reviews + commits manually per CLAUDE.md)
- File ownership enforcement
- Implementation order rules
- Constraint check at each step (icon import, font lock, hex token, copy)
- ~60 lines

**Phase 8 (Audit) — replace `code-reviewer` agent:**
- Inline grep runner scripts (consolidated from existing § Final Audit checklist)
- Visual check via vision-capable model (capability description)
- Tier-filtered output template
- ~50 lines

### 2. Capability-based asset gen table

Located in `references/visual-asset-prompt-library.md` (replaces "Tool routing" table) and referenced from `custom-icon-pipeline.md`, `2d-illustration-catalog.md`, `visual-effect-patterns.md`:

| Capability needed | Description |
|-------------------|-------------|
| Text-to-image with style control | High-quality image gen supporting style references (silkscreen, riso, watercolor), palette constraint, composition direction |
| Text-to-image with photorealism + anti-stock | Realistic image gen with negative prompts to avoid stock-photo aesthetic |
| Vision-capable analysis | Multimodal model reading image → describe style, extract dominant colors, score vibe match |
| Vector tracing | Bitmap → SVG conversion (Inkscape Trace Bitmap, vectorizer, or AI vectorizer) |
| Direct SVG generation | LLM-produced inline SVG code for geometric icons |
| Static 3D render → 2D image | 3D modeling tool (Blender, Spline, KeyShot) exporting PNG/WebP — never `.glb` |
| Shader / WebGL effects | React Three Fiber as shader runner (NOT model viewer) — patterns inline in `visual-effect-patterns.md` |

Files reference this table for guidance, no longer name specific ck-skills.

### 3. § Beyond perfect-ui — generic-ized (3 rows)

| Need | Suggested approach |
|------|---------|
| Full app architecture, complex client-side state, deep multi-page IA | General frontend engineering workflow (state management, routing framework, type-safe API layer) |
| Full e-commerce backend (cart, checkout, inventory, payment integration) | Dedicated e-commerce platform workflow with backend orchestration |
| Exact design replication from screenshot / Figma reference | Vision-driven design-to-code workflow (multimodal model + visual diff loop) |

Concept of routing kept; no ck-skill names. Located in SKILL.md, index.html § Beyond, and README.md Related Skills (table style).

### 4. Per-file change scope

**HIGH (substantial edits):**
- `SKILL.md` — orchestration map rewrite, Hard Rule descriptions update (remove "via ck:X" hints), examples flow descriptions, § Beyond generic, References table, Anti-Rationalization rows, version 2.1.0→2.2.0
- `README.md` — examples flow descriptions, FAQ entry removal ("Does this skill work without ck:..." gone), Related Skills table → generic capability, intro paragraph
- `index.html` — phase card descriptions (mention ck:brainstorm/ck:plan/ck:cook/ck:ai-artist/ck:threejs/code-reviewer), § Beyond rows, References file tree (already updated v2.1.0; verify), Footer version
- `references/workflow-phases.md` — Phase 1/6/7/8 inline expansions (+~300 lines), tool-routing tables → capability descriptions

**MEDIUM:**
- `references/2d-illustration-catalog.md` — tool routing per style row (15 hits — likely "Tool" column entries)
- `references/visual-asset-prompt-library.md` — Tool routing table → capability table (7 hits)
- `references/custom-icon-pipeline.md` — icon gen routing (5 hits)
- `references/redesign-audit-checklist.md` — audit references (4 hits)

**MINOR (1 hit each — likely passing mentions):**
- `references/visual-effect-patterns.md`
- `references/visual-direction-guide.md`
- `references/motion-patterns.md`
- `assets/nextjs-skeleton/section-archetypes.md`

### 5. Version bump

- 2.1.0 → **2.2.0** (architectural change, backward-compatible semantics)
- Update SKILL.md frontmatter, README.md line 5, index.html hero + footer

## Implementation considerations

### Migration safety
- Existing flows for landing/portfolio: behavior identical (only delegation wording changes; inputs/outputs preserved)
- Existing brief.md/plan.md outputs: same schema (inlined version generates same artifacts)
- Asset generation: user/Claude must route to whatever tool they have (slight workflow indirection but more portable)

### Known limitations to document
- Inline workflow content adapted FOR perfect-ui's design context — NOT generic. Doesn't replace ck:brainstorm / ck:plan / ck:cook for non-design tasks.
- Distilled essence may miss some ck-skill nuance (e.g., specific commit-message conventions, atomic-commit edge cases). The CLAUDE.md "No auto-commit" rule still governs.
- If user has both perfect-ui AND ck-skills installed, perfect-ui no longer auto-invokes ck-skills — user invokes them manually if desired.

### Risks

| Risk | Mitigation |
|------|------------|
| Inline content drifts from ck-skill best-practices | Capture essence (workflow + outputs + constraints), not implementation details |
| workflow-phases.md becomes too large (>1000 lines) | Split if exceeds 1200; target ~750-800 |
| Capability descriptions too vague → user doesn't know what tool to use | Provide concrete prompt templates inline + capability description; user can route to any tool meeting capability |
| Missing some ck-skill nuance for asset gen (style libraries) | Inline ~5-7 most-used style prompt templates per vibe in `visual-asset-prompt-library.md` |
| Phase 8 audit becomes verbose in-thread | Grep checks short by design; visual check is single AI call |
| User has ck-skills installed and expects auto-invocation | Document in FAQ that v2.2.0 is self-contained; user can manually invoke ck-skills if preferred |

## Success criteria

1. `grep -rE 'ck:|ckm:' SKILL.md README.md index.html references/ assets/` returns 0 matches in active files
2. `code-reviewer` references removed from active files (replaced with inline audit protocol)
3. Phase 1/6/7/8 contain inline workflow instructions sufficient for self-contained operation
4. Capability descriptions in asset-related references (no specific tool names)
5. § Beyond and Related Skills generic-ized (3 rows each, no ck-skill names)
6. Version 2.2.0 in SKILL.md, README.md, index.html (hero + footer)
7. Historical plans/ untouched (per design decision)
8. Backward compat: landing/portfolio output identical pre/post change

## Out of scope (defer)

- Replacing ck-skills entirely (this is removal of dependency, not building competing skill ecosystem)
- Adding new asset-gen capabilities (current scope = describe existing capabilities generically)
- Plan-file format changes (existing format works; just remove ck-skill references in templates)
- Removing skill from a Claude Kit context (the skill still works inside CK environment; just doesn't depend on it)

## Next steps

1. User approve design → proceed `/ck:plan` (which itself will become "inline plan workflow" post-v2.2.0, but for THIS change we still use ck:plan since we're inside CK ecosystem currently)
2. Plan dự kiến 4-5 phase:
   - Phase 01: workflow-phases.md heavy inline (Phase 1/6/7/8 expansion)
   - Phase 02: Reference files cleanup (visual-asset-prompt-library, custom-icon-pipeline, 2d-illustration-catalog, etc.) — capability descriptions
   - Phase 03: SKILL.md cleanup + version bump
   - Phase 04: README.md cleanup + FAQ removal + Related Skills generic
   - Phase 05: index.html cleanup + § Beyond generic + version bump
3. Final grep audit: 0 matches for `ck:|ckm:|code-reviewer agent` in active files

## Unresolved questions

- Acceptable size for workflow-phases.md after expansion? Current ~485 → ~800. If user wants <750, may need to split into sub-references (e.g., `workflow-brainstorm.md`, `workflow-plan.md`)
- Historical plans/ folder confirmation — leaving untouched correct? Or user wants past brainstorm.md / phase files cleaned too?
- Should the "Anti-Rationalization" table in SKILL.md keep the row about "Skip the brief, I know what they want" (still relevant) but update with v2.2.0 self-contained framing?
- README has a "Contributing / Modifying" section mentioning `python ~/.claude/skills/skill-creator/scripts/quick_validate.py` — this is a skill-creator reference, not ck-skill. Keep or remove? (technically not Claude Kit but is "ck" ecosystem adjacent)
