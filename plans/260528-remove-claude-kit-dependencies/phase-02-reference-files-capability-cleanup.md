# Phase 02 — Reference files capability cleanup

## Context links
- [brainstorm.md](./brainstorm.md) § Capability-based asset gen table
- [phase-01-workflow-phases-inline.md](./phase-01-workflow-phases-inline.md) — defines capability mapping reference (depends on)
- Files to modify (8 total):
  - `references/visual-asset-prompt-library.md` (7 hits)
  - `references/2d-illustration-catalog.md` (15 hits)
  - `references/custom-icon-pipeline.md` (5 hits)
  - `references/redesign-audit-checklist.md` (4 hits)
  - `references/visual-effect-patterns.md` (1 hit)
  - `references/visual-direction-guide.md` (1 hit)
  - `references/motion-patterns.md` (1 hit)
  - `assets/nextjs-skeleton/section-archetypes.md` (1 hit)

## Overview
- **Priority:** High (capability descriptions referenced by SKILL.md / README / index.html in later phases)
- **Status:** pending
- **Depends on:** Phase 01 (uses capability mapping vocabulary established there)
- **Description:** Replace specific ck:/ckm: tool references with capability-based descriptions across 8 reference files. Tool routing tables → capability tables. Total: 34 occurrences across 8 files.

## Key insights
- Most hits are in routing tables / instruction blocks ("use ck:ai-artist to generate...")
- Two files have substantial work: `2d-illustration-catalog.md` (15 hits — per-style tool column) and `visual-asset-prompt-library.md` (7 hits — main tool routing table)
- Four files have 1 hit each (minor passing mentions) — quick edits
- Capability vocabulary established in Phase 01 (visual-asset-prompt-library.md capability table) — reuse exact phrasing

## Requirements

### Functional
- Tool routing tables → capability tables across all 8 files
- Inline mentions ("invoke ck:ai-artist") → "use a text-to-image model with style control"
- Consistent capability terminology across files (use Phase 01's vocabulary)
- 0 ck:/ckm: matches in any of the 8 files post-edit

### Non-functional
- Each file size unchanged ± ~10 lines (only word replacements, no structural changes)
- Cross-references between these files preserved

## Architecture

### Capability vocabulary (from Phase 01)

Standard replacement phrases:

| Old ck: reference | New capability phrase |
|-------------------|----------------------|
| `ck:ai-artist --mode search` | text-to-image with curated style prompt library |
| `ck:ai-artist --mode wild` | text-to-image with creative direction freedom |
| `ck:ai-multimodal` (Imagen) | high-quality text-to-image with palette + lighting + composition control |
| `ck:ai-multimodal` (Nano Banana) | text-to-image with photorealism + anti-stock negatives |
| `ck:ai-multimodal` (analyze) | vision-capable model for image validation |
| `ckm:design` icon CLI | vector icon design pipeline (text-to-SVG or text-to-image + vector trace) |
| `ckm:design` social-photos | multi-platform social image composition |
| `ck:threejs` | React Three Fiber + inline shader patterns library |
| `ck:media-processing` | image post-processing pipeline (resize, optimize, format convert) |

### Per-file edit summary

**`references/visual-asset-prompt-library.md` (7 hits — main routing table)**
- Section: "Tool routing (by style)" table → "Capability routing (by style)" table
- 7 row entries with ck:X / ckm:X → capability descriptions
- No structural change

**`references/2d-illustration-catalog.md` (15 hits)**
- Likely per-style "Tool" column entries across illustration style catalog table
- Replace each ck:X / ckm:X with capability description
- Verify: this catalog has rows for 11 illustration styles — ~14-15 tool mentions expected

**`references/custom-icon-pipeline.md` (5 hits)**
- Mentions in decision tree and validation section
- "ckm:design icon CLI" → "vector icon design pipeline"
- "ck:ai-multimodal Imagen" → "high-quality text-to-image with palette + lighting + composition control"
- "AI-generated + traced via ckm:design" → "AI-generated + traced via vector trace tool"

**`references/redesign-audit-checklist.md` (4 hits)**
- Likely audit step references
- "via ck:ai-multimodal analyze" → "via vision-capable model"
- "delegate to code-reviewer" if present → "run inline audit checklist (see workflow-phases.md § Phase 8)"

**`references/visual-effect-patterns.md` (1 hit)**
- Likely 1 mention of `ck:threejs` for shader patterns
- → "React Three Fiber as shader runner"

**`references/visual-direction-guide.md` (1 hit)**
- Likely 1 passing mention
- Replace per capability vocabulary

**`references/motion-patterns.md` (1 hit)**
- Likely 1 mention (possibly `ck:threejs` for GSAP integration)
- Replace per capability vocabulary

**`assets/nextjs-skeleton/section-archetypes.md` (1 hit)**
- Likely 1 passing mention
- Replace per capability vocabulary

## Related code files

**Modify (8 files):**
- `references/visual-asset-prompt-library.md`
- `references/2d-illustration-catalog.md`
- `references/custom-icon-pipeline.md`
- `references/redesign-audit-checklist.md`
- `references/visual-effect-patterns.md`
- `references/visual-direction-guide.md`
- `references/motion-patterns.md`
- `assets/nextjs-skeleton/section-archetypes.md`

**Create / Delete:** None

## Implementation steps

1. **Read each file** to identify exact line ranges of ck:/ckm: hits (use Grep with -n for line numbers)
2. **For each file: surgical Edit calls** replacing ck:/ckm: with capability vocabulary from Architecture table above
3. **Verify capability terminology consistency** — same phrase used across files for same capability
4. **Final per-file grep** — confirm 0 matches in each file
5. **Aggregate grep** — `grep -rE 'ck:|ckm:' references/ assets/` returns only matches outside Phase 02 scope (i.e., should be 0 since Phase 01 already cleaned workflow-phases.md)

## Todo list
- [ ] Read 8 files to identify hit line ranges
- [ ] Replace ck:/ckm: in `visual-asset-prompt-library.md` (7 hits)
- [ ] Replace ck:/ckm: in `2d-illustration-catalog.md` (15 hits)
- [ ] Replace ck:/ckm: in `custom-icon-pipeline.md` (5 hits)
- [ ] Replace ck:/ckm: in `redesign-audit-checklist.md` (4 hits)
- [ ] Replace ck:/ckm: in `visual-effect-patterns.md` (1 hit)
- [ ] Replace ck:/ckm: in `visual-direction-guide.md` (1 hit)
- [ ] Replace ck:/ckm: in `motion-patterns.md` (1 hit)
- [ ] Replace ck:/ckm: in `section-archetypes.md` (1 hit)
- [ ] Aggregate grep verification across references/ + assets/

## Success criteria
- 0 ck:/ckm: matches in any of the 8 files
- Capability vocabulary used consistently across files
- Tool routing tables in `visual-asset-prompt-library.md` and `2d-illustration-catalog.md` are now capability tables
- File sizes within ± 10 lines of pre-edit (word-level replacements only)
- Cross-references intact (links between reference files resolve)

## Risk assessment
- **Risk:** Inconsistent capability phrasing across files → mitigated by Architecture vocabulary table; use Find-and-Replace patterns consistently
- **Risk:** 2d-illustration-catalog.md 15 hits scattered across style rows — easy to miss one → final per-file grep catches misses
- **Risk:** Some "1 hit" files may have indirect mentions (e.g., footnote linking to ck:skill) → grep with `-n` reveals exact location

## Security considerations
None — documentation-only changes.

## Next steps
- Phase 03 SKILL.md cleanup uses same capability vocabulary in § Beyond and orchestration map
