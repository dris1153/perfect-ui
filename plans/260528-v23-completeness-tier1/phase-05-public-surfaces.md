# Phase 05 — Public surfaces (SKILL.md + README.md + index.html + version)

## Context links
- [brainstorm.md](./brainstorm.md) § Implementation considerations, Resolved sub-decisions
- [phase-01-anti-slop-updates.md](./phase-01-anti-slop-updates.md) — depends on (Honest Copy Mandate referenced from SKILL Hard Rule)
- [phase-02-preflight-scan.md](./phase-02-preflight-scan.md) — depends on (Phase 0.1 referenced in SKILL.md process flow)
- [phase-03-strategic-omissions.md](./phase-03-strategic-omissions.md) — depends on (Strategic Omissions audit class referenced in SKILL/README)
- [phase-04-hero-line-matrix.md](./phase-04-hero-line-matrix.md) — depends on (Hero ceiling mentioned in Hard Rules update)
- [SKILL.md](../../SKILL.md), [README.md](../../README.md), [index.html](../../index.html)

## Overview
- **Priority:** Final integration — public surfaces summarize 4 prior phases + version bump
- **Status:** pending
- **Depends on:** Phase 01-04 (must complete before this phase runs)
- **Description:** Bump version 2.2.0 → 2.3.0 in 4 locations. Update SKILL.md Hard Rule #3 (fold honest copy). Add Phase 0.1 to SKILL.md process flow. Update README.md v2.3.0 paragraph + 1 new FAQ + changelog mention. Update index.html Mandates section.

## Key insights
- 4 prior phases run in parallel; this phase integrates and documents them
- Hard Rule #3 (anti-slop defaults) gets honest copy added (no new Hard Rule #10 per sub-decision 4)
- index.html In Practice tab update DEFERRED to v2.5 per sub-decision 2
- README changelog gets first-mention of "taste-skill ecosystem inspiration" per Q7 (general, no per-rule attribution)

## Requirements

### Functional
- SKILL.md frontmatter `version: "2.3.0"`
- SKILL.md Hard Rule #3 updated to include honest copy: "...no fabricated metrics (use em-dash placeholder per `anti-slop-rules.md § Honest Copy Mandate`)..."
- SKILL.md process flow Mermaid diagram has Phase 0.1 node (between Phase 0 and Phase 0.5)
- SKILL.md § References table adds `references/preflight-scan.md` entry
- SKILL.md Phase Method Map updated if Phase 0.1 affects orchestration
- README.md L5 version 2.3.0
- README.md adds v2.3.0 update paragraph (after existing v2.2.0 paragraph)
- README.md adds 1 new FAQ entry ("What's new in v2.3.0?" or "What does pre-flight scan do?")
- README.md credits/footer section mentions "Inspired by patterns from taste-skill ecosystem (Hallmark, gpt-taste, stitch-design-taste, motion-design, et al.)" — single line, general attribution
- index.html hero meta: `<span>v2.3.0</span>`
- index.html footer: `<em>perfect-ui</em> — v2.3.0`
- index.html Mandates section updated (add honest copy mandate card + Hero discipline mandate card, OR fold into existing Mandate #3)

### Non-functional
- Backward compat: landing/portfolio examples render schema-identically (no breaking Phase output changes)
- Anti-slop self-audit: this phase's edits don't introduce new violations
- Cross-references resolve: SKILL.md preflight-scan.md link, README FAQ links, index.html Mandate references

## Architecture

### SKILL.md edits

1. **Frontmatter** (line ~7):
   ```yaml
   metadata:
     author: dris1153
     version: "2.3.0"
   ```

2. **Hard Rule #3** (update):
   ```
   3. **NO AI slop defaults** — no Inter font alone, no purple/blue gradient hero (marketing-only rule but watch for it leaking into generic tier), no centered 3-card feature row, no "Elevate / Seamless / Unleash" copy in headlines, no "Hi, I'm X, a passionate designer who loves coffee" portfolio cliché, **NO fabricated metrics / testimonials / logos** — use em-dash placeholder (`— metric to confirm`) when user doesn't supply data. Tier-filtered per § Applicability Matrix — see `references/anti-slop-rules.md` § Honest Copy Mandate for the 3 accepted paths.
   ```

3. **Process flow Mermaid diagram** — add Phase 0.1 node:
   ```mermaid
   M[Phase 0: Detect Mode: new vs redesign] --> P[Phase 0.1: Pre-flight scan — auto-detect existing tokens]
   P --> T[Phase 0.5: Detect Type → tier route]
   ```

4. **§ References table** — add row:
   ```
   | Pre-flight scan (auto-detect existing tokens before Phase 2) | `references/preflight-scan.md` |
   ```

5. **§ Phase Method Map** — add row:
   ```
   | 0.1 | Auto-detect pre-flight scan (see `references/preflight-scan.md`) | Read existing tokens, preserve, introduce only what's missing |
   ```

### README.md edits

1. **L5 version**: `**Version:** 2.3.0`

2. **v2.3.0 update paragraph** (after existing v2.2.0 paragraph):
   ```markdown
   **v2.3.0 update:** Completeness pass. Skill now enforces what AI typically forgets — Strategic Omissions checklist (legal links / 404 / form validation / a11y skip-link / cookie consent / etc.) added to all 3 anatomy files. Honest copy mandate explicit: no fabricated metrics; use em-dash placeholder when data missing. Pre-flight scan (auto-detect) reads existing project tokens / fonts / motion library before designing — preserves what's there, introduces what's missing. Hero discipline tightened: line-count limit per vibe (universal 4+ ban) + meta-label ban ("SECTION 01" / "CHAPTER THREE" headers forbidden) + filler-text ban ("Scroll to explore" / "Swipe down" forbidden; icons OK).
   ```

3. **New FAQ entry** (insert near end of FAQ):
   ```markdown
   **Q: What does the pre-flight scan do (v2.3.0+)?**
   A: Before Phase 2 visual direction locks, skill auto-detects existing project state — fonts loaded via `next/font` or `<link>`, palette in `:root`, motion libraries (`framer-motion`, `gsap`), spacing scale, framework, existing icon library (flagged for replacement per Hard Rule #2). On greenfield repos, silent. On populated repos, emits a findings block: what perfect-ui will preserve, what it will introduce. Cache in `.perfect-ui/preflight.json`; refresh with "refresh pre-flight". See `references/preflight-scan.md`.
   ```

4. **Credits / footer addition** (insert near end of Credits section):
   ```markdown
   - v2.3.0+ patterns inspired by the taste-skill ecosystem (Hallmark, gpt-taste, stitch-design-taste, motion-design, redesign-existing-projects, et al.)
   ```

### index.html edits

1. **Hero version**: `<span>v2.3.0</span>`

2. **Footer version**: `<span><em>perfect-ui</em> — v2.3.0</span>`

3. **Mandates section update** — fold honest copy into Mandate #3 OR add new card:

   Option A (fold into #3, matches sub-decision 4):
   ```html
   <div class="mandate">
     <span class="mandate-num">— 03</span>
     <h3>NO AI slop defaults</h3>
     <p>Inter alone, purple/blue gradient hero, two equal CTAs, "Elevate / Seamless / Unleash" copy, fabricated metrics (use <code>— metric to confirm</code> placeholder instead).</p>
   </div>
   ```

   Option B (add new card #9, but this changes mandate count — riskier):
   - Skip — sub-decision 4 says fold into #3

Use Option A.

Optional additions (if space allows in same section):
- Mandate card for Hero discipline (line-count + no meta-labels + no filler text)
- Defer if section becomes crowded

## Related code files

**Modify (3 files):**
- `SKILL.md` (frontmatter + Hard Rule #3 + Mermaid diagram + References table + Phase Method Map)
- `README.md` (L5 version + v2.3.0 paragraph + new FAQ + credits)
- `index.html` (hero version + footer version + Mandate #3 update)

**Create / Delete:** None

## Implementation steps

1. **Verify Phase 01-04 complete** (cross-references must resolve)
2. **Update SKILL.md** — frontmatter version, Hard Rule #3, Mermaid Phase 0.1 node, References table, Phase Method Map
3. **Update README.md** — L5 version, append v2.3.0 paragraph, insert new FAQ entry, append credits line
4. **Update index.html** — hero version, footer version, Mandate #3 (fold honest copy)
5. **Final verification:**
   - Grep `v?2\.3\.0` → ≥4 matches across 3 files
   - Grep `v?2\.2\.0` in SKILL.md / README.md / index.html → 0 matches (excluding historical Anti-Rationalization rows that mention v2.2.0 as state-prior-to-v2.3 context)
   - Smoke test: read README Example 1 (coffee landing) — confirm flow still describes same Phase 1-8 outcomes (no breaking change)

## Todo list
- [ ] Verify Phase 01-04 complete
- [ ] Read SKILL.md, identify Mermaid diagram + References table line ranges
- [ ] Update SKILL.md frontmatter version
- [ ] Update SKILL.md Hard Rule #3 (fold honest copy)
- [ ] Update SKILL.md Mermaid diagram (add Phase 0.1)
- [ ] Update SKILL.md References table (+ preflight-scan.md)
- [ ] Update SKILL.md Phase Method Map (+ row 0.1)
- [ ] Update README.md L5 version
- [ ] Append v2.3.0 update paragraph
- [ ] Insert new FAQ entry (pre-flight scan)
- [ ] Append credits line
- [ ] Update index.html hero version
- [ ] Update index.html footer version
- [ ] Update index.html Mandate #3 (fold honest copy)
- [ ] Final grep verification (v2.3.0 ≥4, no stale v2.2.0)
- [ ] Smoke test backward compat

## Success criteria
- Version 2.3.0 in 4 locations (SKILL frontmatter + README L5 + index hero + index footer)
- 0 stale v2.2.0 references (excluding historical Anti-Rationalization context)
- SKILL.md Process flow has Phase 0.1 node
- SKILL.md References table has preflight-scan.md row
- README.md has v2.3.0 update paragraph + new FAQ + credits line
- index.html Mandate #3 mentions honest copy with em-dash placeholder
- Backward compat: existing Examples render schema-identically

## Risk assessment
- **Risk:** Hard Rule #3 grows too long after honest copy fold → split into bullet list for readability
- **Risk:** Mermaid diagram syntax breaks when adding Phase 0.1 → verify with markdown preview post-edit
- **Risk:** v2.3.0 grep miss-counts if grep matches "v2.3.0" inside historical context (Anti-Rationalization rows that mention "as of v2.3.0" forward-reference) → narrow grep to specific files; allow context mentions
- **Risk:** index.html § Mandates becomes too dense after honest copy fold → fold cleanly; defer Hero discipline card to future version if space tight
- **Risk:** Cross-references break if file order changes → re-read each file post-edit

## Security considerations
None — markdown / HTML edits.

## Next steps
- Plan-level final verification (per plan.md § Final verification)
- Update plan.md status → completed
- Update phase table all rows → completed
- User reviews diff, commits manually per CLAUDE.md "No auto-commit"
- Optional: invoke /ck:journal for v2.3.0 release summary
