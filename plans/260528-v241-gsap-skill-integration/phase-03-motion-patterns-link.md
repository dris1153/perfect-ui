# Phase 03 — motion-patterns.md cross-link section

## Context links
- [brainstorm.md](./brainstorm.md) § File-level impact summary
- [phase-01-gsap-integration-ref.md](./phase-01-gsap-integration-ref.md) — foundation (depends on)
- [references/motion-patterns.md](../../references/motion-patterns.md) — file to modify

## Overview
- **Priority:** Medium (cross-reference for discoverability)
- **Status:** pending
- **Parallel-safe with:** Phase 04 (different files)
- **Description:** Add brief § "GSAP skill integration (v2.4.1+)" to motion-patterns.md cross-linking to gsap-integration.md. Concise — full detail lives in gsap-integration.md.

## Key insights
- motion-patterns.md already documents GSAP as Tier 4 motion library
- New section provides discoverability + cross-link, doesn't duplicate gsap-integration.md content
- Insert near existing § Easing Library OR at end of file as a "see also" section

## Requirements

### Functional
- Add § "GSAP skill integration (v2.4.1+)" with ~15 lines
- Brief intro: when/why GSAP skill integration applies
- Cross-link to gsap-integration.md for detection logic + skill selection + invocation patterns
- Note: GSAP skills OPTIONAL; falls back to inline patterns if not installed

### Non-functional
- motion-patterns.md grows ~+15 lines
- KISS — keep section short, point at gsap-integration.md
- Existing content untouched

## Architecture

### New section in motion-patterns.md

Insert AFTER existing § Easing Library OR at end of file (before final cross-references section):

```markdown
## GSAP skill integration (v2.4.1+)

When motion intensity hits 3/3 OR user brief contains GSAP-specific keywords ("GSAP" / "ScrollTrigger" / "scroll choreography" / "scrub" / "pin"), perfect-ui can auto-invoke official gsap-* skills (8 skills: gsap-core, gsap-scrolltrigger, gsap-react, gsap-timeline, gsap-plugins, gsap-performance, gsap-frameworks, gsap-utils) for implementation guidance.

Skills are OPTIONAL — if not installed at `~/.claude/skills/gsap-*`, perfect-ui falls back to inline patterns documented in `gsap-integration.md § Fallback inline patterns`.

Detection happens at Phase 7 entry (see `workflow-implement.md § Step 2.5`). Skill selection (which gsap-* to invoke) follows the table in `gsap-integration.md § The 8 gsap skills`.

For full integration logic, invocation pseudo-code, and fallback patterns, see `gsap-integration.md`.

### Quick reference

| Use case | gsap-* skill |
|----------|-------------|
| Basic tweens, easing | gsap-core |
| Scroll-driven animation | gsap-scrolltrigger |
| React / Next.js | gsap-react |
| Vue / Svelte | gsap-frameworks |
| Multi-step choreography | gsap-timeline |
| Flip / Draggable / SplitText / MorphSVG | gsap-plugins |
| Performance optimization | gsap-performance |
| Math / array helpers | gsap-utils |
```

## Related code files

**Modify:** `references/motion-patterns.md` (insert ~15 lines)

**Create / Delete:** None

## Implementation steps

1. **Read motion-patterns.md** to identify insertion point (after Easing Library OR before cross-references)
2. **Insert § GSAP skill integration (v2.4.1+)** per Architecture above
3. **Verify cross-references** — gsap-integration.md, workflow-implement.md

## Todo list
- [ ] Read motion-patterns.md, identify insertion point
- [ ] Insert § GSAP skill integration (v2.4.1+) with quick reference table
- [ ] Verify cross-references

## Success criteria
- motion-patterns.md has new § "GSAP skill integration (v2.4.1+)"
- Quick reference table maps 8 skills to use cases
- Cross-references to gsap-integration.md + workflow-implement.md present
- File growth ~+15 lines
- Existing content untouched

## Risk assessment
- **Risk:** Section duplicates gsap-integration.md content → keep brief, point at gsap-integration.md for details
- **Risk:** Quick reference table conflicts with gsap-integration.md table → cross-link, treat motion-patterns.md as discovery surface
- **Risk:** Section placement disrupts existing flow → choose end-of-file location to preserve current structure

## Security considerations
None.

## Next steps
- Phase 04 SKILL.md References table adds gsap-integration.md row + version bump + public surfaces
