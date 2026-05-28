# Phase 01 — NEW gsap-integration.md

## Context links
- [brainstorm.md](./brainstorm.md) § Architecture · § File-level impact summary
- Skill selection logic (locked in brainstorm Q1 + plan args)

## Overview
- **Priority:** High (foundation file — referenced by Phase 02-04)
- **Status:** pending
- **Description:** CREATE `references/gsap-integration.md` (~100 lines). Documents detection triggers, 8-skill selection table, active Skill tool invocation pattern, fallback inline patterns, GSAP-specific anti-slop checks, and extensibility note for future animation library skills.

## Key insights
- This file is the single source of truth for GSAP integration logic
- Other phases (workflow-implement, workflow-audit) just cross-link here
- Fallback inline patterns must work for users without gsap-skills (preserve v2.2.0 self-contained)
- Extensibility note documents architecture model for future Framer Motion / Lenis integrations

## Requirements

### Functional
- 7 sections: When this applies / 8 skills with selection logic / Active Skill tool invocation / Fallback inline patterns / Anti-slop checks / Extensibility / Cross-references
- Detection triggers documented per R1 (intensity 3/3 OR keyword match)
- Skill selection table maps trigger → skill subset
- Active Skill tool invocation as pseudo-code (concrete pattern)
- Fallback inline patterns ~20 lines (useGSAP hook + ScrollTrigger basic + timeline chain)
- 3 GSAP-specific anti-slop checks documented
- Cross-references to motion-patterns.md, workflow-implement.md, workflow-audit.md, preflight-scan.md

### Non-functional
- File size ~100 lines (target)
- KISS — keep patterns minimal, cross-reference to gsap-skills for depth
- Preserve self-contained: fallback section is functional standalone

## Architecture

### Structure (~100 lines)

```markdown
# GSAP Skill Integration

When motion intensity hits 3/3 OR user brief contains GSAP-specific keywords, perfect-ui triggers official gsap-* skills (installed at `~/.claude/skills/gsap-*`) for implementation. Falls back to inline patterns if skills not installed.

## When this applies (auto-detect at Phase 7)

Triggers (any one fires):
1. Motion intensity (from Phase 2e) = 3/3 — choreographed motion typically needs GSAP
2. User brief / inspirations contain keywords: "GSAP", "ScrollTrigger", "scroll choreography", "scrub", "pin section", "scroll-driven", "scroll-linked"
3. Phase 2d effect choice = "Scroll-driven distortion" (requires Lenis + GSAP ScrollTrigger)

Auto-detection runs at Phase 7 entry (see `workflow-implement.md § Step 2 — GSAP integration check`).

## Skill detection mechanism

Before invoking, check skills exist:

```bash
ls ~/.claude/skills/gsap-core/SKILL.md 2>/dev/null
```

If file exists → skills installed, proceed with active Skill tool call.
If missing → use fallback inline patterns (below).

## The 8 gsap skills (selection logic)

Always invoke `gsap-core` (foundation). Add others based on use case:

| Trigger condition | Skills to invoke |
|-------------------|------------------|
| Default (any GSAP use) | `gsap-core` |
| React / Next.js project (from pre-flight scan or stack lock) | + `gsap-react` |
| Vue / Svelte / SvelteKit | + `gsap-frameworks` |
| Scroll-driven animation (Phase 2d = "scroll-driven distortion" OR keyword "ScrollTrigger" / "scrub" / "pin") | + `gsap-scrolltrigger` |
| Multi-step sequencing (timelines, choreography) | + `gsap-timeline` |
| Plugins needed (Flip / Draggable / SplitText / MorphSVG / DrawSVG) | + `gsap-plugins` |
| Performance review / <60fps issue | + `gsap-performance` |
| Math / array / value mapping helpers | + `gsap-utils` |

Typical bundle for GSAP-intensive landing (Next.js + scroll + timeline):
- `gsap-core` + `gsap-react` + `gsap-scrolltrigger` + `gsap-timeline` (4 skills)

## Active Skill tool invocation pattern

Sequential calls per use case (not single batch). Each skill loads patterns + best practices that inform Phase 7 implementation.

Pseudo-code:

```
if gsap_needed:
    if skills_installed:
        Skill(skill="gsap-core", args=f"implement GSAP for {brief.summary} at intensity 3/3, personality {motion_personality}")
        if framework == "react" or framework == "nextjs":
            Skill(skill="gsap-react", args="useGSAP hook setup + cleanup pattern for {component_count} components")
        elif framework in ("vue", "svelte"):
            Skill(skill="gsap-frameworks", args=f"{framework} lifecycle + cleanup for GSAP")
        if scroll_animation_needed:
            Skill(skill="gsap-scrolltrigger", args="ScrollTrigger setup for {scroll_pattern} pattern")
        if timeline_needed:
            Skill(skill="gsap-timeline", args="timeline chain for {sequence_description}")
        if plugins_needed:
            Skill(skill="gsap-plugins", args=f"register and use {plugin_list}")
        # gsap-performance only if existing issue
        # gsap-utils only if utility functions needed
    else:
        # Fall back to inline patterns below
        use_inline_fallback()
```

## Fallback inline patterns (skills not installed)

For users without gsap-skills, use these minimal patterns directly. For deeper guidance, recommend user installs `~/.claude/skills/gsap-*`.

### useGSAP hook (React)
```tsx
import { useGSAP } from '@gsap/react';
import { gsap } from 'gsap';

useGSAP(() => {
  gsap.to(".target", { x: 100, duration: 1 });
}, { scope: containerRef });
```

### ScrollTrigger basic
```tsx
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

gsap.to(".target", {
  x: 100,
  scrollTrigger: {
    trigger: ".target",
    start: "top center",
    end: "bottom center",
    scrub: 1,
  },
});
```

### Timeline chain
```tsx
const tl = gsap.timeline({ defaults: { duration: 0.6, ease: "power2.out" } });
tl.from(".a", { opacity: 0, y: 20 })
  .from(".b", { opacity: 0, y: 20 }, "-=0.4")
  .from(".c", { opacity: 0, y: 20 }, "-=0.4");
```

For React cleanup, framework specifics, plugin registration, performance, and utility helpers — install the gsap-* skills.

## Anti-slop GSAP-specific checks (Phase 8 audit)

Run at Phase 8 (see `workflow-audit.md § Step E — GSAP-specific checks` post-v2.4.1):

1. **GSAP imported but unused / underused (<3 use cases):** bundle bloat = Tier 2 violation. Either commit to GSAP or remove and use Framer Motion / CSS.
2. **GSAP imported but motion intensity locked at 0-1/3:** contradicts vibe-locked intensity = Tier 2 violation. GSAP is for intensity 3/3; lower intensities should use CSS or FM.
3. **`window.addEventListener('scroll')` for scroll animation when ScrollTrigger available:** performance violation = Tier 2. Use ScrollTrigger instead.

## Extensibility

Architecture supports future addition of other animation library skills when official skills become available. Current state: only GSAP populated (8 skills). Future patches replicate this model:

- `references/{library}-integration.md` — detection + selection + fallback
- `workflow-implement.md` — detection step references the integration file
- `workflow-audit.md` — library-specific anti-slop checks
- Fallback patterns preserve self-contained behavior

Examples for future:
- Framer Motion: detection = intensity 2-3/3, install detection = `~/.claude/skills/framer-motion-*`
- Lenis: detection = Phase 2d "cursor-reactive scroll" OR keyword "smooth scroll"
- Lottie: detection = vibe = Playful + complex character motion + Phase 4 illustration style = "Lottie animation"

## Cross-references

- `motion-patterns.md § Easing Library` + `§ Motion Personalities` — intensity 3/3 personality drives skill selection
- `workflow-implement.md § Step 2` — Phase 7 detection step references this file
- `workflow-audit.md § Step E` — Phase 8 GSAP-specific checks
- `preflight-scan.md` — framework detection feeds skill selection (React vs Vue/Svelte)
- 8 installed gsap skills: `~/.claude/skills/gsap-{core,scrolltrigger,react,timeline,plugins,performance,frameworks,utils}/`
```

## Related code files

**Create:** `references/gsap-integration.md` (NEW)

**Modify / Delete:** None

## Implementation steps

1. **Write the new file** per Architecture above
2. Verify all 7 sections present
3. Confirm fallback inline patterns are functional (basic GSAP setups)
4. Verify cross-references to other files documented (they'll be created/updated in Phase 02-03)

## Todo list
- [ ] Write `references/gsap-integration.md` with all 7 sections
- [ ] Detection triggers section
- [ ] Skill detection mechanism
- [ ] 8-skill selection table
- [ ] Active Skill tool invocation pseudo-code
- [ ] Fallback inline patterns (~20 lines)
- [ ] 3 GSAP-specific anti-slop checks
- [ ] Extensibility note
- [ ] Cross-references section

## Success criteria
- File exists, ~100 lines, all 7 sections
- Detection triggers per R1 documented
- 8 skills mapped in selection table
- Active Skill invocation as concrete pseudo-code
- Fallback inline patterns functional standalone
- Anti-slop checks reference workflow-audit.md (Phase 02 wires the connection)
- Cross-references resolve (placeholders OK; Phase 02-03 finalize)

## Risk assessment
- **Risk:** Fallback patterns too thin → keep to ~20 lines basic, recommend gsap-skills for depth
- **Risk:** Active invocation pseudo-code too abstract → use concrete `Skill(skill="...", args="...")` syntax
- **Risk:** Detection trigger keywords miss real cases → keyword list comprehensive (GSAP / ScrollTrigger / scrub / pin / scroll choreography / scroll-driven / scroll-linked)
- **Risk:** Extensibility section invites premature abstraction → document as note only; no implementation for non-GSAP yet

## Security considerations
None — documentation only.

## Next steps
- Phase 02 wires workflow-implement.md + workflow-audit.md to this file
- Phase 03 wires motion-patterns.md cross-link
- Phase 04 SKILL.md References table adds 1 row
