# Phase 04 — Hero H1 line range column (visual-direction-guide.md)

## Context links
- [brainstorm.md](./brainstorm.md) § Item N (Hero 2-line iron rule)
- [references/visual-direction-guide.md](../../references/visual-direction-guide.md) — file to modify

## Overview
- **Priority:** Medium (small focused edit; required for Phase 01 cross-reference)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 02, 03 (different file)
- **Description:** Add compact "Hero H1 line range" column to vibe matrix in visual-direction-guide.md. 11 vibes × 1 column. Format: "1" / "1-2" / "2-3".

## Key insights
- visual-direction-guide.md already has per-vibe matrix (palette, typography, motion intensity, illustration style, etc.)
- New column should be compact (≤6 chars per cell) to avoid stretching matrix beyond comfortable width
- Vibe → line range per brainstorm spec (resolved Q4)
- Phase 01 anti-slop rule #11 cites this column ("see `visual-direction-guide.md` § Hero H1 line range column")

## Requirements

### Functional
- Add "Hero H1 lines" column to vibe matrix (or whichever existing per-vibe table is the canonical lookup)
- All 11 vibes have value: minimal=1-2 / editorial=1-3 / brutalist=1 / retro-futuristic=1-2 / organic=2-3 / luxury=1-2 / playful=2-3 / industrial=1-2 / art-deco=1-2 / glass-tech=1-2 / hand-crafted=2-3
- Universal ceiling note (4+ lines = catastrophic failure regardless of vibe) added near matrix

### Non-functional
- Compact format (numeric range, no verbose explanation)
- No regression to existing columns
- Markdown table renders correctly post-edit (column alignment intact)

## Architecture

### vibe matrix update

Locate existing vibe matrix (likely a table near top of visual-direction-guide.md after intro). Add new column after Motion intensity column (or at appropriate position).

Example (existing format imagined):

```markdown
| Vibe | Palette | Typography | Spatial | Motion | Hero H1 lines | Illustration |
|------|---------|------------|---------|--------|---------------|--------------|
| Minimal | ... | ... | ... | 1/3 | 1-2 | ... |
| Editorial | ... | ... | ... | 1-2/3 | 1-3 | ... |
| Brutalist | ... | ... | ... | 0-1/3 | 1 | ... |
| Retro-futuristic | ... | ... | ... | 3/3 | 1-2 | ... |
| Organic | ... | ... | ... | 2/3 | 2-3 | ... |
| Luxury | ... | ... | ... | 1-2/3 | 1-2 | ... |
| Playful | ... | ... | ... | 2-3/3 | 2-3 | ... |
| Industrial | ... | ... | ... | 0-1/3 | 1-2 | ... |
| Art-deco | ... | ... | ... | 1-2/3 | 1-2 | ... |
| Glass-tech | ... | ... | ... | 2-3/3 | 1-2 | ... |
| Hand-crafted | ... | ... | ... | 0-1/3 | 2-3 | ... |
```

### Universal ceiling note

Add brief paragraph BELOW the matrix:

```markdown
**Universal Hero H1 ceiling:** 4+ lines = catastrophic failure regardless of vibe. Enforce via container `max-w-5xl` / `max-w-6xl` + H1 `clamp(3rem, 5vw, 5.5rem)`. If headline copy exceeds 90 chars, rewrite shorter; never break the line cap by reducing font below `--text-display-s`. See `anti-slop-rules.md § Tier 1 rule #11` for full enforcement spec.
```

## Related code files

**Modify:** `references/visual-direction-guide.md` (single file, surgical column addition + 1 note)

**Create / Delete:** None

## Implementation steps

1. **Read full visual-direction-guide.md** to locate canonical vibe matrix and confirm existing columns
2. **Add "Hero H1 lines" column** to matrix at appropriate position (after motion intensity OR at end before per-vibe deep sections)
3. **Fill 11 vibe rows** with compact range values
4. **Add universal ceiling note** below matrix
5. **Verify markdown table** renders correctly (column count consistent across rows, alignment intact)

## Todo list
- [ ] Read visual-direction-guide.md, locate vibe matrix
- [ ] Add Hero H1 lines column
- [ ] Fill 11 vibe rows
- [ ] Add universal ceiling note below matrix
- [ ] Verify table syntax + alignment

## Success criteria
- Vibe matrix has new "Hero H1 lines" column
- All 11 vibes have value (no empty cell)
- Universal ceiling note present below matrix
- File size growth ≤+20 lines
- Markdown table syntactically valid
- Cross-reference from anti-slop-rules.md Tier 1 rule #11 resolves to this column

## Risk assessment
- **Risk:** Matrix already too wide; adding column overflows comfortable reading → use compact format (≤6 chars per cell)
- **Risk:** Existing matrix structure unfamiliar → read file first; choose insertion position that minimizes column reordering
- **Risk:** Brutalist single-line value debated (could be 1-2) → user locked "1" in brainstorm; honor that
- **Risk:** Column position changes break cross-references in other files → no other file currently references this matrix's column positions (only the column existence)

## Security considerations
None.

## Next steps
- Phase 01 references this column from anti-slop-rules.md Tier 1 rule #11
- Phase 05 SKILL.md may mention Hero H1 ceiling in Hard Rule update; cross-link
