# perfect-ui v2.4.1 — GSAP Skill Integration

**Date:** 2026-05-28
**Status:** Brainstorm complete, awaiting plan approval
**Skill version impact:** v2.4.0 → v2.4.1 (patch — additive, backward-compatible)
**Parent context:** Standalone patch (not part of v2.3 → v2.5 roadmap). v2.5.0 sẽ vẫn tackle 3 items gốc (G+H+Q).

---

## Problem statement

User request: "thêm 1 workflow cho user add GSAP vào page, sử dụng các gsap-skills này để work, không cần copy logic về src, chỉ cần call trigger skill". 

Hiện tại perfect-ui (v2.4.0, self-contained per v2.2.0 mandate) mentions GSAP as Tier 4 motion library nhưng KHÔNG có implementation patterns. Người dùng có 8 official GreenSock gsap-skills installed locally — chứa expertise sâu (core API, scrolltrigger, react patterns, timelines, plugins, performance, frameworks Vue/Svelte, utils).

v2.4.1 thêm **GSAP skill integration workflow** — perfect-ui auto-detect khi cần GSAP, active-trigger các gsap-skills relevant via Skill tool, fallback to inline patterns nếu skills not installed.

## Honest pushback (acknowledged before locking)

1. **Tension với v2.2.0 self-contained mandate** — perfect-ui v2.2.0 explicitly removed external skill orchestration ("Skill runs in any Claude Code setup"). v2.4.1 reintroduces skill triggering for GSAP. Compromise: skills OPTIONAL with inline fallback (Q3 decision) — backward compat preserved.
2. **GSAP-only special treatment** — Framer Motion + Lenis (more common at intensity 2/3) don't have official skills. Architecture documented as EXTENSIBLE but only GSAP populated for now.
3. **Active triggering complexity** — Q2 picked active over passive. Risk: workflow becomes harder to reason about. Mitigation: trigger logic centralized in 1 NEW file (`gsap-integration.md`).

## Requirements (locked from Q1-Q6)

| ID | Decision | Source Q |
|----|----------|----------|
| R1 | Trigger conditions: (a) motion intensity = 3/3, OR (b) user keyword detection ("GSAP" / "ScrollTrigger" / "animation choreography" / "scrub" / "pin") | Q1 (option 1+3) |
| R2 | Active Skill tool call mechanism (workflow invokes gsap-* skills explicitly) | Q2 |
| R3 | Skills optional with inline fallback (preserve v2.2.0 self-contained) | Q3 |
| R4 | NEW `references/gsap-integration.md` (~100 lines) | Q4 |
| R5 | v2.4.1 patch release standalone (not folded into v2.5.0) | Q5 |
| R6 | Phase 2.6 dialog unchanged — rely on auto-detection at Phase 7 (R1) | Q6 |

## Architecture

### Detection trigger (Phase 7-entry)

In `workflow-implement.md` Phase 7 entry logic, add:

```
GSAP Skill Integration Check (NEW v2.4.1):
1. Detection:
   - motion intensity (from Phase 2e) == 3/3? → GSAP likely needed
   - User brief / inspirations contain "GSAP" / "ScrollTrigger" / "scroll choreography" / "scrub" / "pin section"? → GSAP needed
   - Phase 2d effect = "Scroll-driven distortion" (requires Lenis + GSAP ScrollTrigger)? → GSAP needed
2. If yes:
   - Check `~/.claude/skills/gsap-*/SKILL.md` paths exist
   - If installed: invoke relevant skills via Skill tool (see selection logic below)
   - If not installed: fall back to inline GSAP patterns in `motion-patterns.md § Easing Library` + `gsap-integration.md § Fallback patterns`
3. If no:
   - Skip GSAP integration; CSS / Framer Motion / Lenis cover intensity 0-2/3
```

### Skill selection logic (which gsap-* to invoke)

Always invoke `gsap-core` (foundation). Add others based on use case:

| Trigger condition | Skills to invoke |
|-------------------|------------------|
| Default | `gsap-core` |
| React / Next.js project (from pre-flight scan or stack lock) | + `gsap-react` |
| Vue / Svelte / SvelteKit | + `gsap-frameworks` |
| Scroll-driven animation (Phase 2d = "scroll-driven distortion" OR keyword "ScrollTrigger" / "scrub" / "pin") | + `gsap-scrolltrigger` |
| Multi-step sequencing (timelines) | + `gsap-timeline` |
| Plugins needed (Flip / Draggable / SplitText / MorphSVG / etc.) | + `gsap-plugins` |
| Performance review / >60fps issue | + `gsap-performance` |
| Math / array / value mapping helpers | + `gsap-utils` |

Typical bundle for a v2.4.1 GSAP-intensive landing:
- `gsap-core` + `gsap-react` + `gsap-scrolltrigger` + `gsap-timeline` (4 skills, covers ~90% of intensity 3/3 needs)

### NEW `references/gsap-integration.md` structure (~100 lines)

```markdown
# GSAP Skill Integration

When v2.4.0 motion intensity hits 3/3 OR user brief contains GSAP-specific keywords, perfect-ui triggers official gsap-* skills (installed at `~/.claude/skills/gsap-*`) for implementation. Falls back to inline patterns if skills not installed.

## When this applies (auto-detect at Phase 7)

[detection trigger list per R1]

## The 8 gsap skills (when each applies)

[Selection logic table per Skill selection section above]

## Active Skill tool invocation pattern

```
# Pseudo-code for Phase 7 implementation
if gsap_needed and gsap_skills_installed:
    Skill(skill="gsap-core", args=f"implement GSAP for {brief_summary} at intensity 3/3, personality {motion_personality}")
    if scroll_animation: Skill(skill="gsap-scrolltrigger", args="...")
    if framework == "react": Skill(skill="gsap-react", args="...")
    # etc.
elif gsap_needed:
    # Fall back to inline patterns
    use_pattern_from_motion_patterns_md()
```

Multiple skills can be invoked sequentially. Each skill returns GSAP code patterns + best practices that perfect-ui applies during Phase 7 implementation.

## Fallback patterns (if gsap-skills not installed)

[Brief inline GSAP patterns covering: useGSAP hook (React), basic ScrollTrigger setup, timeline chain, performance tips. ~20 lines. Detailed patterns assumed in gsap-* skills.]

## Anti-slop check (Phase 8 audit addition)

- GSAP imported but unused (<3 use cases): bundle bloat → Tier 2 violation
- GSAP imported but motion intensity locked at 0-1/3: contradicts vibe-locked intensity → Tier 2 violation
- `window.addEventListener('scroll')` for scroll animation when ScrollTrigger available: performance violation

## Extensibility

Architecture supports future addition of other animation library skills (Framer Motion, Lenis, Lottie) when official skills exist. Current state: only GSAP populated (8 skills).
```

## File-level impact summary

**New file (1):**
- `references/gsap-integration.md` (~100 lines)

**Modified files (6):**
- `references/motion-patterns.md` (~+15 lines: § "GSAP skill integration" cross-link + brief mention)
- `references/workflow-implement.md` (~+30 lines: Phase 7 GSAP detection + active trigger logic)
- `references/workflow-audit.md` (~+10 lines: Phase 8 GSAP-specific anti-slop checks)
- `SKILL.md` (~+5 lines: frontmatter version 2.4.1 + References table +1 row + Phase Method Map note)
- `README.md` (~+15 lines: v2.4.1 mini-paragraph + 1 FAQ "What about GSAP skills?")
- `index.html` (~+3 lines: hero + footer version 2.4.1)

**Total net new content:** ~+180 lines (1 NEW file + 6 modifications). Small patch.

## Workflow integration

```
Phase 0.5 (existing) → Phase 1 (brief) → Phase 2 (visual direction including 2.5 macro + 2.6 personality + 2e intensity)
                                          ↓
                                  Phase 2.6 NO change (per Q6 — auto-detect at Phase 7)
                                          ↓
Phase 6 (plan) → Phase 7 (implement)
                       ↓
                  [GSAP Skill Integration Check] (NEW v2.4.1)
                       ↓
                  if intensity=3/3 OR keyword match:
                       ├─ skills installed → active Skill tool calls
                       └─ skills missing → inline fallback patterns
                       ↓
                  Continue Phase 7 implementation
                       ↓
Phase 8 (audit) → tier-filtered + new GSAP-specific anti-slop checks (R4)
```

## Cross-references

- `gsap-integration.md` ↔ `motion-patterns.md § Easing Library / § Motion Personalities` (intensity 3/3 personality drives skill selection)
- `gsap-integration.md` ↔ `workflow-implement.md § Step 2` (per-phase constraints)
- `gsap-integration.md` ↔ `workflow-audit.md § Step B` (anti-slop GSAP checks)
- `gsap-integration.md` ↔ `preflight-scan.md` (framework detection feeds skill selection)

## Success criteria

1. `references/gsap-integration.md` exists with detection logic + skill selection table + fallback patterns
2. Phase 7 (`workflow-implement.md`) has GSAP detection step + active Skill tool call pattern documented
3. Phase 8 (`workflow-audit.md`) has GSAP-specific anti-slop checks
4. Cross-references between gsap-integration.md ↔ motion-patterns.md resolve
5. SKILL.md frontmatter `version: "2.4.1"` + References table +1 row
6. README.md v2.4.1 mini-paragraph + 1 new FAQ
7. index.html hero + footer version 2.4.1
8. Backward compat: existing v2.4.0 workflows (Phase 1-8) schema-identical (additive)
9. Skills optional: fallback inline patterns documented (preserve v2.2.0 self-contained for users without gsap-skills)

## Implementation considerations

- **Skill detection mechanism:** check existence of `~/.claude/skills/gsap-core/SKILL.md` etc. via Read or Bash `ls`. Document in gsap-integration.md.
- **Skill invocation pattern:** use `Skill` tool with skill name. Document concrete pseudo-code in gsap-integration.md.
- **Backward compat for v2.4.0 users:** no behavior change unless trigger conditions met. v2.4.0 users without intensity 3/3 / GSAP keywords don't see any change.
- **Self-contained fallback completeness:** inline fallback patterns (~20 lines) must be functional for basic GSAP needs (useGSAP, ScrollTrigger setup, timeline chain). Not as deep as gsap-skills but enough for greenfield projects.

## Risks

| Risk | Mitigation |
|------|------------|
| User has gsap-skills installed but workflow doesn't detect | Skill detection via Read of SKILL.md path; document detection in gsap-integration.md |
| Skill invocation fails / returns unexpected output | Workflow has fallback to inline patterns; document graceful degradation |
| v2.4.1 breaks v2.4.0 examples (regression) | Additive only — existing Phase 1-8 paths unchanged for intensity 0-2/3 + no GSAP keyword |
| Bloat: workflow-implement.md grows for GSAP-specific logic | Centralize in gsap-integration.md; workflow-implement.md just cross-links |
| Phase 8 audit adds too many GSAP-specific checks | Keep to 3 essential checks: import w/o use, intensity mismatch, scroll w/o ScrollTrigger |
| Future Framer Motion / Lenis skills don't follow same pattern | Architecture documented as EXTENSIBLE; future patches replicate gsap-integration.md model |

## Out of scope (defer)

- Framer Motion skill integration (no official skills available)
- Lenis skill integration (no official skills available)
- Lottie skill integration (LottieFiles motion-design skill exists but is meta-design, not implementation)
- v2.5.0 items (G study verb, H component-scope, Q design_plan block) — unchanged
- Per-skill deep wrapper / proxy logic — perfect-ui just invokes; gsap-skills handle their own internals
- GSAP version detection / migration (gsap-skills handle)
- Auto-install of gsap-skills if missing (user responsibility)

## Next steps

1. User approve this brainstorm → proceed `/ck:plan`
2. Plan dự kiến: 3-4 phase files
   - Phase 01: NEW gsap-integration.md
   - Phase 02: workflow-implement.md + workflow-audit.md (Phase 7 + Phase 8 updates)
   - Phase 03: motion-patterns.md cross-link
   - Phase 04: Public surfaces (SKILL.md + README.md + index.html + version)
3. Each phase parallel-safe by file ownership

## Unresolved questions (resolve in /ck:plan)

1. How does workflow detect skills installed? — propose: Bash `ls ~/.claude/skills/gsap-core` OR Read `~/.claude/skills/gsap-core/SKILL.md`. Document in gsap-integration.md.
2. Active Skill tool invocation pattern — exact pseudo-code structure (sequential vs single batch)? Propose: sequential calls per use case.
3. Fallback inline patterns depth — ~20 lines covering useGSAP + ScrollTrigger basic + timeline chain. Defer deeper patterns to gsap-skills.
4. README v2.4.1 mention vs minor changelog — propose 1 paragraph + 1 FAQ.
5. SKILL.md References table: 1 row for gsap-integration.md OR mention gsap-skills group separately? Propose 1 row (gsap-integration.md owns the cross-ref logic).
6. Phase Method Map row: 7 update mentions GSAP integration OR new row? Propose: update existing Phase 7 row to mention GSAP detection.
