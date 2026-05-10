---
title: Motion rules — vibe-scaled motion intensity + library tier system
date: 2026-05-10
status: approved
type: brainstorm
---

# Brainstorm — Motion Rules

## Problem Statement

Current skill scatters motion mentions across `visual-effect-patterns.md` and `anti-slop-rules.md` without consolidated guidance. User wants explicit rules: motion via Framer Motion + scroll triggers + smooth scroll, "to feel smoother."

Risk if poorly scoped: every element fades-up = AI slop. Evidence from synthesis:
- 4/7 human pages used motion (gsap+lenis confirmed)
- 3/7 used minimal/no motion (paperclip, owo, augen-restraint variant)
- Motion alone is NOT a human-craft signal; INTENTIONAL motion is

## Approved Decisions

| Item | Decision |
|------|----------|
| Default | **Scaled by vibe** — each vibe has motion budget (0-3/3) |
| Library tier | **CSS → FM → Lenis → GSAP** (escalate only when prior tier insufficient) |
| Categories covered | Entrance / hover-focus / scroll-triggered / smooth-scroll baseline |
| Encoding | **NEW** `references/motion-patterns.md` |

## Rationale

**Why vibe-scaled (not default-on):**
- AI slop = motion everywhere with no purpose
- Different vibes need different motion budgets (luxury = restraint; retro-futuristic = full)
- Forces designer to lock intensity at design time, not improvise during code

**Why tier system (not single library):**
- CSS handles 80% of motion needs at 0KB cost
- Framer Motion essential for component reveal/exit (not CSS-doable)
- Lenis only when smooth scroll matters for vibe (luxury, glass-tech)
- GSAP only when timeline sequencing required (retro-futuristic full choreography)

**Why new file (not expand existing):**
- Motion is a distinct concern from effects (shaders) and visual direction (palette)
- Catalog is detailed enough to warrant own file
- Cross-references work better with dedicated file

## Architecture

### NEW: `references/motion-patterns.md` (~280 lines)

1. Why motion (intentional only) + evidence base
2. Tier system — CSS / FM / Lenis / GSAP with bundle costs
3. Vibe × motion intensity matrix (11 vibes × 0-3/3 scale)
4. Decision tree per category
5. Approved patterns with code recipes
6. Forbidden patterns (Tier 2 anti-slop)
7. Performance guardrails
8. Implementation checklist

### Phase 2e — Motion Intensity Lock (NEW step)

After Phase 2d (Visual Effect Layer):
```
AskUserQuestion: "Motion Budget"
- 0/3 — no motion (CSS hover only)
- 1/3 — minimal (CSS + light entrance)
- 2/3 — moderate (FM entrance + Lenis smooth scroll)
- 3/3 — full choreography (FM + Lenis + GSAP timelines)

Default = vibe matrix recommendation
User can override (logged if vibe-mismatch)
```

### Cross-cutting updates

- SKILL.md: new Hard Rule (motion intensity scales with vibe)
- visual-direction-guide.md: Vibe × Motion matrix + output template field
- anti-slop-rules.md: Tier 2 motion patterns + grep checks
- visual-effect-patterns.md: clear distinction motion vs effect
- workflow-phases.md: Phase 2e + Phase 7 motion constraint
- README.md: FAQ + file structure

## Vibe × Motion Intensity Matrix

| Vibe | Default Intensity | Stack | Pattern |
|------|-------------------|-------|---------|
| Minimal | 1/3 | CSS | Hover lift, fade-in on first scroll only |
| Editorial | 1-2/3 | CSS + FM | Stagger display type, slow scroll-linked |
| Brutalist | 0-1/3 | CSS | Hard-edge instant reveals, no easing |
| Retro-futuristic | 3/3 | FM + Lenis + GSAP | Heavy choreography, scroll-driven |
| Organic | 2/3 | FM + Lenis | Soft flowing motion |
| Luxury | 1-2/3 | CSS + Lenis | Restrained, premium pacing |
| Playful | 2-3/3 | FM | Spring physics, bouncy |
| Industrial | 0-1/3 | CSS | Mechanical reveals |
| Art-deco | 1-2/3 | CSS + FM | Geometric reveal |
| Glass-tech | 2-3/3 | FM + Lenis (+ GSAP) | Smooth flowing |
| Hand-crafted | 0-1/3 | CSS | Subtle |

## Risks & Mitigations

| Risk | Mitigation |
|------|-----------|
| Motion-everywhere drift | Vibe matrix locks intensity; Tier 2 anti-slop catches |
| Bundle bloat (FM + Lenis + GSAP = ~85KB) | Tier system enforces escalate-only; CSS default |
| `prefers-reduced-motion` ignored | Hard requirement; audit grep |
| User picks 3/3 for minimal vibe | Allow with logged override + warn |

## Success Criteria

- [ ] `motion-patterns.md` exists with all 8 sections
- [ ] Phase 2e in SKILL.md and workflow-phases.md
- [ ] Vibe × Motion matrix in visual-direction-guide.md
- [ ] Tier 2 anti-slop has 6+ motion patterns
- [ ] Grep checks for motion library imports
- [ ] README FAQ includes motion question
- [ ] `quick_validate.py` passes

## Unresolved Questions

1. Should `prefers-reduced-motion` map to intensity-1 (still some motion) or 0 (no motion)? Currently leaning 0.
2. Should we recommend `useReducedMotion()` from FM, or vanilla matchMedia query?
3. For mobile, should motion intensity auto-degrade by 1 step (e.g., 3/3 → 2/3 on <768px)?
