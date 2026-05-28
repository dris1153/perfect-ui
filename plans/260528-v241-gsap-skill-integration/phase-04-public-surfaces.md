# Phase 04 — Public surfaces (SKILL.md v2.4.1 + README.md + index.html)

## Context links
- [brainstorm.md](./brainstorm.md) § File-level impact summary
- [phase-01-gsap-integration-ref.md](./phase-01-gsap-integration-ref.md) — depends on (References table entry)
- SKILL.md, README.md, index.html

## Overview
- **Priority:** Final integration — version bump + public docs
- **Status:** pending
- **Depends on:** Phase 01-03 (cross-references must resolve before docs reference them)
- **Parallel-safe with:** Phase 03 (different files)
- **Description:** Bump version 2.4.0 → 2.4.1 in 4 locations. Add SKILL.md References table row + Phase 7 Method Map note. Add README v2.4.1 paragraph + new FAQ. Update index.html hero + footer version.

## Key insights
- Patch release (v2.4.1) — minimal mandate changes
- SKILL.md gets 1 new References table row + Phase 7 Method Map mention
- README gets 1 paragraph + 1 FAQ (concise per sub-decision 4)
- index.html only version bumps (no new Mandate or Pipeline card needed for patch)
- No Hard Rule changes (folded into existing motion rule #7)

## Requirements

### Functional
- SKILL.md frontmatter `version: "2.4.1"`
- SKILL.md References table adds row for `gsap-integration.md`
- SKILL.md Phase Method Map Phase 7 row updated with GSAP detection note
- README.md L5 version 2.4.1
- README.md adds v2.4.1 mini-paragraph (after v2.4.0 paragraph)
- README.md adds 1 new FAQ "What about GSAP skills?"
- README.md credits acknowledge updated (GSAP integration borrowed concept)
- index.html hero version 2.4.1
- index.html footer version 2.4.1

### Non-functional
- Backward compat: v2.4.0 examples render schema-identically
- Anti-slop self-audit: no violations in new content
- Cross-references resolve

## Architecture

### SKILL.md edits

1. **Frontmatter version**: `version: "2.4.1"`

2. **References table — add row** after macrostructure-catalog.md row:
```markdown
| GSAP skill integration (intensity 3/3 + keyword detection → optional gsap-* skill triggering with inline fallback) | `references/gsap-integration.md` |
```

3. **Phase Method Map Phase 7 row update**:
```markdown
| 7 | Inline implement protocol (see `references/workflow-implement.md`) — writes log.json at end + auto-detects GSAP need (see `references/gsap-integration.md`) | Build the site |
```

### README.md edits

1. **L5 version**: `**Version:** 2.4.1`

2. **v2.4.1 paragraph** (after existing v2.4.0 paragraph):
```markdown
**v2.4.1 update:** GSAP skill integration patch. When motion intensity hits 3/3 OR user brief mentions GSAP / ScrollTrigger / scroll choreography keywords, perfect-ui auto-detects and invokes installed official gsap-* skills (8 skills: gsap-core, gsap-scrolltrigger, gsap-react, gsap-timeline, gsap-plugins, gsap-performance, gsap-frameworks, gsap-utils) via active Skill tool calls — no logic duplication. Skills are OPTIONAL: perfect-ui falls back to inline GSAP patterns if skills not installed, preserving v2.2.0 self-contained behavior. Architecture extensible for future Framer Motion / Lenis / Lottie integrations when official skills become available. See `references/gsap-integration.md`.
```

3. **New FAQ entry** (insert near end of FAQ):
```markdown
**Q: What about GSAP skills (v2.4.1+)?**
A: If you have official gsap-* skills installed at `~/.claude/skills/gsap-*` (gsap-core / gsap-scrolltrigger / gsap-react / gsap-timeline / gsap-plugins / gsap-performance / gsap-frameworks / gsap-utils), perfect-ui auto-detects GSAP need (motion intensity 3/3 OR keyword match in brief) and invokes the relevant skills via active Skill tool calls — no source logic duplication. Skills are optional; if missing, perfect-ui falls back to inline GSAP patterns (useGSAP hook, ScrollTrigger basic setup, timeline chain). Detection trigger conditions, skill selection logic, invocation pseudo-code, and fallback patterns live in `references/gsap-integration.md`.
```

4. **Credits acknowledge update** (single new line):
```markdown
- v2.4.1 GSAP skill integration leverages official GreenSock gsap-* skills (gsap-core, gsap-scrolltrigger, gsap-react, gsap-timeline, gsap-plugins, gsap-performance, gsap-frameworks, gsap-utils) when installed
```

### index.html edits

1. **Hero version**: `<span>v2.4.1</span>`
2. **Footer version**: `<span><em>perfect-ui</em> — v2.4.1</span>`

No new Mandate card needed for patch. No Pipeline section update needed (GSAP detection is implicit within Phase 7).

## Related code files

**Modify (3 files):**
- `SKILL.md` (frontmatter version + References table +1 row + Phase Method Map Phase 7 update)
- `README.md` (L5 version + v2.4.1 paragraph + new FAQ + credits update)
- `index.html` (hero + footer version)

**Create / Delete:** None

## Implementation steps

1. **Verify Phase 01-03 complete** (gsap-integration.md exists; cross-references in place)
2. **Update SKILL.md frontmatter version** → "2.4.1"
3. **Add SKILL.md References table row** for gsap-integration.md
4. **Update SKILL.md Phase Method Map Phase 7 row** with GSAP detection note
5. **Update README.md L5 version** → 2.4.1
6. **Append v2.4.1 update paragraph** after v2.4.0 paragraph
7. **Insert new FAQ entry** about GSAP skills
8. **Append credits acknowledge line**
9. **Update index.html hero version** → v2.4.1
10. **Update index.html footer version** → v2.4.1
11. **Final verification:**
    - Grep `v?2\.4\.1` → ≥4 matches across 3 files
    - Grep `v?2\.4\.0` in SKILL.md / README.md / index.html → 0 matches in critical locations (allow historical context in changelog paragraphs)
    - Smoke test: README Example 1 (coffee landing) flow still describes Phase 1-8 schema-identically

## Todo list
- [ ] Verify Phase 01-03 complete
- [ ] Update SKILL.md frontmatter version → 2.4.1
- [ ] Add SKILL.md References table row (gsap-integration.md)
- [ ] Update SKILL.md Phase 7 Method Map row (GSAP detection note)
- [ ] Update README.md L5 version
- [ ] Append v2.4.1 mini-paragraph
- [ ] Insert GSAP FAQ entry
- [ ] Append credits acknowledge line
- [ ] Update index.html hero version
- [ ] Update index.html footer version
- [ ] Final grep verification (v2.4.1 ≥4, no stale v2.4.0 in critical locations)
- [ ] Smoke test backward compat

## Success criteria
- Version 2.4.1 in 4 locations (SKILL frontmatter + README L5 + index hero + index footer)
- SKILL.md References table has gsap-integration.md row
- SKILL.md Phase 7 Method Map mentions GSAP detection
- README.md v2.4.1 paragraph + new FAQ + credits update
- index.html versions updated (no new Mandate / Pipeline card)
- 0 stale v2.4.0 references (excluding historical changelog paragraphs)
- Backward compat: existing Examples render schema-identically

## Risk assessment
- **Risk:** Hard Rule changes needed for GSAP integration → no Hard Rule added (folded into existing #7 motion rule implicitly via cross-reference to gsap-integration.md)
- **Risk:** v2.4.1 paragraph too long → keep to 1 paragraph, multi-topic, concise
- **Risk:** Index.html Mandate count layout breaks → no new Mandate; layout unchanged
- **Risk:** Cross-references break if file order changes → re-read each file post-edit; spot-check links

## Security considerations
None — markdown / HTML edits.

## Next steps
- Plan-level final verification (per plan.md § Final verification)
- Update plan.md status → completed
- Update phase table all rows → completed
- User reviews diff, commits manually per CLAUDE.md "No auto-commit"
- Optional: invoke /ck:journal for v2.4.1 patch summary
