# Phase 02 — workflow-implement.md + workflow-audit.md integration

## Context links
- [brainstorm.md](./brainstorm.md) § Workflow integration · § Architecture
- [phase-01-gsap-integration-ref.md](./phase-01-gsap-integration-ref.md) — foundation (depends on)
- [references/workflow-implement.md](../../references/workflow-implement.md) — file to modify
- [references/workflow-audit.md](../../references/workflow-audit.md) — file to modify

## Overview
- **Priority:** High (workflow surface — where detection logic activates)
- **Status:** pending
- **Depends on:** Phase 01 (gsap-integration.md must exist for cross-references)
- **Description:** Add GSAP detection step to Phase 7 (workflow-implement.md). Add 3 GSAP-specific anti-slop checks to Phase 8 (workflow-audit.md).

## Key insights
- workflow-implement.md owns Phase 7 detection logic — minimal lines, cross-link to gsap-integration.md for details
- workflow-audit.md adds Step E (GSAP-specific) AFTER existing Step E (Visual checks). Renumber accordingly.
- Both modifications additive — no existing protocol broken

## Requirements

### Functional
- workflow-implement.md gets new sub-section in § Step 2 — Per-phase constraints OR new § Step 6 — GSAP integration check
- Detection logic: check trigger conditions, if active → call gsap-integration.md
- workflow-audit.md gets 3 new GSAP-specific anti-slop grep checks
- Cross-references to gsap-integration.md resolve

### Non-functional
- workflow-implement.md grows ~+30 lines (concise)
- workflow-audit.md grows ~+10 lines (3 grep checks + intro)
- Existing protocol content untouched

## Architecture

### workflow-implement.md — Phase 7 GSAP detection step

Insert AFTER existing § Step 2 — Per-phase constraints (`Motion` subsection), BEFORE § Step 3 — Mid-implementation spot-checks:

```markdown
### Step 2.5 — GSAP integration check (v2.4.1+)

If motion intensity (Phase 2e) = 3/3 OR brief contains keywords ("GSAP", "ScrollTrigger", "scrub", "pin", "scroll choreography", "scroll-driven"), invoke GSAP skill integration workflow per `gsap-integration.md`.

Auto-detect at entry to Phase 7:

```
1. Check trigger conditions:
   - motion_intensity == 3/3?
   - brief.text contains GSAP keyword?
   - phase_2d_effect == "scroll-driven distortion"?
2. If yes:
   a. Check skills installed: `ls ~/.claude/skills/gsap-core/SKILL.md`
   b. If installed: invoke gsap-* skills per selection logic (see `gsap-integration.md § The 8 gsap skills`)
   c. If not installed: use fallback inline patterns (see `gsap-integration.md § Fallback inline patterns`)
3. If no: skip GSAP integration; CSS / Framer Motion / Lenis cover intensity 0-2/3
```

See `gsap-integration.md` for full detection rules + skill selection table + invocation pseudo-code + fallback patterns.
```

Also add a brief mention in `**Motion** subsection` of Step 2:

```markdown
**Motion (per `motion-patterns.md` § Motion Personalities + Vibe × Motion Intensity Matrix, locked Phase 2e + 2.6):**
... (existing content)
- **GSAP integration (v2.4.1+):** if intensity = 3/3 OR GSAP keyword detected, invoke gsap-* skills or fallback inline. See `gsap-integration.md`.
```

### workflow-audit.md — GSAP-specific anti-slop checks

Insert NEW § Step E — GSAP-specific checks (v2.4.1+) AFTER existing § Step D, BEFORE existing § Step E (Visual checks). RENUMBER existing E → F, F → G, G → H, H → I if applicable.

OR easier: keep existing Step E (Visual) and insert new content as new § Step F that runs conditionally:

Actually cleanest: insert as new § AFTER existing Step F (Performance), as a conditional bolt-on:

```markdown
### Step F.5 — GSAP-specific checks (run only if GSAP detected in Phase 7)

If GSAP is imported in app code, run these 3 checks (per `gsap-integration.md § Anti-slop GSAP-specific checks`):

```bash
# Check 1: GSAP imported but unused / underused (<3 use cases) — Tier 2 bundle bloat
gsap_imports=$(grep -rE "from ['\"]gsap['\"]" app/ | wc -l)
gsap_use_count=$(grep -rE "gsap\.(to|from|fromTo|timeline|set|killTweensOf)" app/ | wc -l)
# If gsap_imports > 0 AND gsap_use_count < 3 → FAIL (Tier 2)

# Check 2: GSAP imported but motion intensity locked at 0-1/3 — Tier 2 mismatch
# Read motion_intensity from session context (visual-direction.md or plans/{date}-{slug}/visual-direction.md)
# If gsap imported AND motion_intensity ≤ 1 → FAIL (Tier 2)

# Check 3: window.addEventListener('scroll') for scroll animation when ScrollTrigger available — Tier 2 perf
grep -rE "window\.addEventListener\(['\"]scroll['\"]" app/
# If matches found AND gsap-scrolltrigger imported AND used elsewhere → FAIL (Tier 2)
```

Document violations in audit report per `Step H — Output report` template. Reference `gsap-integration.md` for fix guidance.
```

## Related code files

**Modify (2 files):**
- `references/workflow-implement.md` (+ Step 2.5 + brief Motion subsection update; ~+30 lines)
- `references/workflow-audit.md` (+ Step F.5 GSAP checks; ~+10 lines)

**Create / Delete:** None

## Implementation steps

1. **Read workflow-implement.md** to identify insertion point (Step 2 Motion subsection + before Step 3)
2. **Insert Step 2.5** (GSAP integration check) per Architecture above
3. **Add brief mention** in Step 2 Motion subsection
4. **Read workflow-audit.md** to identify insertion point (after Step F Performance, before Step G/H output)
5. **Insert Step F.5** (GSAP-specific checks)
6. **Verify cross-references** — both files cite gsap-integration.md correctly

## Todo list
- [ ] Read workflow-implement.md, find Step 2/3 boundary
- [ ] Insert Step 2.5 — GSAP integration check
- [ ] Add Motion subsection brief mention
- [ ] Read workflow-audit.md, find Step F/G boundary
- [ ] Insert Step F.5 — GSAP-specific checks
- [ ] Verify cross-references to gsap-integration.md

## Success criteria
- workflow-implement.md Step 2.5 present with detection logic
- workflow-audit.md Step F.5 present with 3 grep checks
- Both reference gsap-integration.md correctly
- Existing protocol content untouched
- File growth: workflow-implement ~+30; workflow-audit ~+10

## Risk assessment
- **Risk:** Step numbering conflicts after insertion → use F.5 (decimal) to avoid renumbering existing F/G/H
- **Risk:** Motion subsection mention duplicates Step 2.5 → keep brief, refer to Step 2.5 for details
- **Risk:** GSAP-specific checks fire false positives (Framer Motion projects without GSAP) → gate by "if GSAP detected in Phase 7"; document gate clearly

## Security considerations
None.

## Next steps
- Phase 03 motion-patterns.md cross-link to gsap-integration.md
- Phase 04 SKILL.md References table adds gsap-integration.md row
