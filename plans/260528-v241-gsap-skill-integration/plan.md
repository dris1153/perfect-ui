---
name: v241-gsap-skill-integration
status: completed
priority: medium
mode: auto
created: 2026-05-28
completed: 2026-05-28
target: NEW gsap-integration.md + workflow-implement + workflow-audit + motion-patterns + public surfaces
blockedBy: []
blocks: []
---

# Plan — perfect-ui v2.4.1 GSAP Skill Integration (Patch)

Standalone patch release. Add GSAP skill triggering workflow — perfect-ui auto-detects when GSAP is needed (motion intensity 3/3 OR keyword match), invokes installed gsap-* skills (8 official GreenSock skills) via active Skill tool call. Falls back to inline patterns if skills missing. Preserves v2.2.0 self-contained mandate via optional + fallback design.

## Source of truth
[brainstorm.md](./brainstorm.md) — full design, Q1-Q6 locked decisions, skill selection logic, file impact summary.

## Context links
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.4.0"`)
- Existing motion patterns: [references/motion-patterns.md](../../references/motion-patterns.md)
- Workflow protocols (post-split): [references/workflow-implement.md](../../references/workflow-implement.md), [references/workflow-audit.md](../../references/workflow-audit.md)
- Public docs: [README.md](../../README.md), [index.html](../../index.html)
- Roadmap: NOT folded into v2.5.0 (v2.5.0 keeps G+H+Q original items)
- 8 installed gsap skills: `~/.claude/skills/gsap-{core,scrolltrigger,react,timeline,plugins,performance,frameworks,utils}/`

## Resolved decisions (from brainstorm Q-section)

| # | Decision |
|---|----------|
| Q1 | Trigger conditions = motion intensity 3/3 OR keyword detection (GSAP / ScrollTrigger / scroll choreography / scrub / pin) |
| Q2 | Active Skill tool call mechanism |
| Q3 | Skills OPTIONAL with inline fallback |
| Q4 | NEW `references/gsap-integration.md` (~100 lines) |
| Q5 | v2.4.1 patch standalone (not v2.5.0 fold) |
| Q6 | Phase 2.6 dialog unchanged (auto-detect at Phase 7) |

## Resolved sub-decisions (from plan args defaults)

1. Skill detection mechanism: Bash `ls ~/.claude/skills/gsap-core` (silent check) — documented in gsap-integration.md
2. Active Skill tool invocation: sequential calls per use case (e.g., `Skill(skill="gsap-core", ...)` then `Skill(skill="gsap-scrolltrigger", ...)` if scroll needed)
3. Fallback inline patterns depth: ~20 lines (useGSAP React hook + ScrollTrigger basic setup + timeline chain example)
4. README v2.4.1: 1 paragraph (concise) + 1 new FAQ ("What about GSAP skills?")
5. SKILL.md References table: 1 row entry for gsap-integration.md
6. Phase Method Map: update existing Phase 7 row to mention GSAP detection (no new row)

## Goal

1. `gsap-integration.md` exists documenting detection triggers + skill selection + invocation pattern + fallback
2. Phase 7 (workflow-implement.md) auto-detects GSAP need + invokes skills OR falls back to inline
3. Phase 8 (workflow-audit.md) has 3 GSAP-specific anti-slop checks
4. motion-patterns.md cross-links to gsap-integration.md
5. SKILL.md frontmatter v2.4.1 + References table +1 row
6. README.md v2.4.1 paragraph + new FAQ
7. index.html hero + footer v2.4.1
8. Backward compat: existing v2.4.0 flows render schema-identically (additive)
9. Skills optional: fallback inline patterns work for users without gsap-skills

## Phases

| # | Phase | Files | Status | Effort |
|---|-------|-------|--------|--------|
| 01 | NEW gsap-integration.md (~100 lines, all content) | [phase-01-gsap-integration-ref.md](./phase-01-gsap-integration-ref.md) | completed | M |
| 02 | workflow-implement.md + workflow-audit.md (Phase 7 GSAP detection + Phase 8 GSAP anti-slop) | [phase-02-workflow-integration.md](./phase-02-workflow-integration.md) | completed | M |
| 03 | motion-patterns.md cross-link section | [phase-03-motion-patterns-link.md](./phase-03-motion-patterns-link.md) | completed | S |
| 04 | Public surfaces (SKILL.md v2.4.1 + README + index.html) | [phase-04-public-surfaces.md](./phase-04-public-surfaces.md) | completed | M |

## Key dependencies

```
Phase 01 (NEW gsap-integration.md — foundation)
   ↓
Phase 02 (workflow-implement + workflow-audit cross-link to Phase 01)
   ↓
Phase 03 (motion-patterns.md cross-link)  ⊥  Phase 04 (public surfaces)
```

- Phase 01 must run first (foundation file referenced by Phase 02-04)
- Phase 02 references gsap-integration.md from Phase 7 + Phase 8
- Phase 03 and Phase 04 are parallel-safe (different files)

## File ownership (parallel-safe contracts)

| File | Owner phase | Action | Approx. lines |
|------|-------------|--------|---------------|
| `references/gsap-integration.md` | 01 | CREATE | +100 |
| `references/workflow-implement.md` | 02 | MODIFY (+ Phase 7 GSAP detection logic) | +30 |
| `references/workflow-audit.md` | 02 | MODIFY (+ 3 GSAP-specific anti-slop checks) | +10 |
| `references/motion-patterns.md` | 03 | MODIFY (+ § GSAP skill integration cross-link) | +15 |
| `SKILL.md` | 04 | MODIFY (frontmatter v2.4.1 + References table +1 row + Phase Method Map Phase 7 note) | +5 |
| `README.md` | 04 | MODIFY (L5 version + v2.4.1 paragraph + 1 new FAQ + credits mention) | +15 |
| `index.html` | 04 | MODIFY (hero + footer version 2.4.1) | +3 |

**Total net new content:** ~+180 lines (1 NEW + 6 MODIFIED). Small patch.

## Success criteria (overall)

- [ ] `references/gsap-integration.md` exists with: detection triggers + 8-skill selection table + invocation pseudo-code + fallback inline patterns + anti-slop checks + extensibility note
- [ ] `workflow-implement.md` Phase 7 has GSAP detection step + active Skill tool call pattern documented
- [ ] `workflow-audit.md` Phase 8 has 3 GSAP-specific anti-slop checks (bundle bloat, intensity mismatch, scroll without ScrollTrigger)
- [ ] `motion-patterns.md` has cross-link to gsap-integration.md
- [ ] SKILL.md frontmatter `version: "2.4.1"` + References table +1 row + Phase 7 Method Map note
- [ ] README.md L5 version 2.4.1 + v2.4.1 paragraph + new FAQ + credits update
- [ ] index.html hero + footer = v2.4.1
- [ ] No anti-slop self-violations in new content
- [ ] Backward compat: v2.4.0 examples render identically when intensity ≠ 3/3 and no GSAP keywords
- [ ] Fallback inline patterns functional for users without gsap-skills installed

## Out of scope

- v2.5.0 items (G study verb, H component-scope, Q design_plan block) — unchanged
- Framer Motion / Lenis / Lottie skill integration — no official skills available; defer until they exist
- GSAP version detection / migration logic — gsap-skills handle internally
- Auto-install of gsap-skills if missing — user responsibility
- Per-skill wrapper / proxy logic — direct invocation only
- New Mermaid node for GSAP integration (auto-detect is implicit within Phase 7)
- New Hard Rule for GSAP — folded into existing Hard Rule #7 (motion) via implicit reference

## Risks

| Risk | Mitigation |
|------|------------|
| User has gsap-skills installed but workflow doesn't detect | Document detection via Bash `ls` check in gsap-integration.md; verify in Phase 02 logic |
| Active Skill tool invocation fails / returns unexpected output | Fallback to inline patterns documented in gsap-integration.md |
| v2.4.1 breaks v2.4.0 examples (regression) | Additive only — existing intensity 0-2/3 paths untouched |
| Bloat: workflow-implement.md grows for GSAP-specific logic | Centralize in gsap-integration.md; workflow-implement.md just cross-links + minimal detection step |
| Self-contained mandate (v2.2.0) violated | Skills OPTIONAL — fallback inline patterns preserve self-contained behavior for users without gsap-skills |
| Future Framer Motion / Lenis skills don't follow same pattern | Architecture documented as EXTENSIBLE in gsap-integration.md; future patches replicate model |

## Final verification (last task before plan.md status → completed)

1. Run grep: `grep -rE 'v?2\.4\.0' SKILL.md README.md index.html` → 0 stale matches (excluding historical context)
2. Run grep: `grep -rE 'v?2\.4\.1' SKILL.md README.md index.html` → ≥4 matches (frontmatter + L5 + hero + footer)
3. Verify `references/gsap-integration.md` exists + ~100 lines
4. Verify `workflow-implement.md` Phase 7 has GSAP detection step
5. Verify `workflow-audit.md` Phase 8 has 3 GSAP-specific checks
6. Verify `motion-patterns.md` has cross-link to gsap-integration.md
7. Verify SKILL.md References table has gsap-integration.md row
8. Backward compat smoke test: read README Example 1 (coffee landing) — confirm Phase 1-8 schema-identical (coffee landing uses motion intensity 1-2/3, no GSAP — no behavior change)
