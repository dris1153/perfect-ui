# Phase 02 — Motion personalities + Brand Motion Identity

## Context links
- [brainstorm.md](./brainstorm.md) § Item K (Motion personalities), Phase 2.6 Brand Motion Identity
- [references/motion-patterns.md](../../references/motion-patterns.md)

## Overview
- **Priority:** High (referenced by Phase 04 workflow-brainstorm.md split + Phase 2.6 dialog)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 03
- **Description:** Add § Motion Personalities + Brand Motion Identity matrix to motion-patterns.md. 4 personalities (Playful/Premium/Corporate/Energetic) × Intensity (0-3/3) = independent axes. Per-vibe personality defaults.

## Key insights
- Personality drives character (easing curve + duration palette + entrance pattern)
- Intensity drives amount (already exists as 0-3/3 scale)
- Independent axes — Premium vibe can be 1/3 OR 3/3 intensity
- Brand Motion Identity = 3 constants locked: signature easing + duration palette + entrance pattern
- Phase 2.6 dialog reads this matrix; Phase 04 creates the dialog

## Requirements

### Functional
- motion-patterns.md gets new § "Motion Personalities (Phase 2.6)" with 4-row table
- Each personality has: signature easing curve + duration palette (quick/standard/slow) + entrance pattern + vibe defaults
- Brand Motion Identity subsection explains 3 locked constants
- Personality × Intensity matrix shows independent axes
- Per-vibe personality default mapping (11 vibes → 4 personalities)

### Non-functional
- motion-patterns.md grows ~+80 lines
- Existing motion intensity scale (0-3/3) untouched (additive layer)
- Existing per-vibe easing untouched (Brand Motion Identity REPLACES easing locked at Phase 2.6 — explain transition)

## Architecture

### Motion Personalities new section

Insert in motion-patterns.md AFTER existing `## Vibe × Motion Intensity Matrix` or equivalent:

```markdown
## Motion Personalities (Phase 2.6)

Select ONE archetype per project. Independent of intensity (0-3/3). Personality drives character (easing + duration + entrance pattern). Intensity drives amount (how much motion).

### The 4 personalities

| Personality | Signature easing | Duration palette (quick / standard / slow) | Entrance pattern | Best for vibes |
|-------------|------------------|--------------------------------------------|------------------|----------------|
| **Playful** | `ease-out-back` (10-20% overshoot) — `cubic-bezier(0.34, 1.56, 0.64, 1)` | 150ms / 250ms / 400ms | Spring bounce | Playful, Organic |
| **Premium** | `cubic-bezier(0.4, 0, 0.2, 1)` (Material Design standard) | 250ms / 400ms / 600ms | Subtle fade-up | Minimal, Editorial, Luxury, Hand-crafted |
| **Corporate** | `cubic-bezier(0.2, 0, 0, 1)` (sharp deceleration) | 200ms / 300ms / 400ms | Crisp slide | Industrial, Art-deco |
| **Energetic** | `ease-out-expo` (15-30% overshoot) — `cubic-bezier(0.16, 1, 0.3, 1)` | 100ms / 200ms / 350ms | Quick translate | Brutalist, Retro-futuristic, Glass-tech |

### Brand Motion Identity (3 locked constants)

Once personality is picked at Phase 2.6, 3 constants are LOCKED for the entire project:

1. **Signature easing** — one cubic-bezier curve used in 80% of animations. Other 20% may use neutral `ease-out` for utility transitions.
2. **Duration palette** — 3 values (quick / standard / slow). NEVER use arbitrary durations like 312ms or 583ms. All animations snap to one of these 3.
3. **Entrance pattern** — consistent reveal style. Don't mix fade-up + slide + scale randomly across the page. Pick one entrance pattern, use it everywhere.

### Personality × Intensity matrix

Personality locks character. Intensity locks scope. Both axes locked independently at Phase 2e (intensity) + Phase 2.6 (personality).

| | Intensity 0/3 (no motion) | Intensity 1/3 (minimal) | Intensity 2/3 (moderate) | Intensity 3/3 (full) |
|---|---------------------------|--------------------------|--------------------------|----------------------|
| **Playful** | hover only | + 1 entrance per section | + scroll-linked bounce | + spring choreography |
| **Premium** | hover only | + subtle fade-up entries | + Lenis smooth scroll | + GSAP timeline reveals |
| **Corporate** | hover only | + crisp slide entrance | + scroll-linked slide | + multi-element sequences |
| **Energetic** | hover only | + quick translate snaps | + scroll-driven overshoots | + bold choreography |

### Per-vibe personality defaults

| Vibe | Default personality | Override allowed |
|------|---------------------|-------------------|
| Minimal | Premium | Yes (most allow Energetic for tech-startup feel) |
| Editorial | Premium | Yes |
| Brutalist | Energetic | No (Corporate would betray vibe) |
| Retro-futuristic | Energetic | No |
| Organic | Playful | Yes (Premium for wellness brands) |
| Luxury | Premium | No (other personalities cheapen) |
| Playful | Playful | No |
| Industrial | Corporate | Yes (Energetic for tech-industrial) |
| Art-deco | Corporate | Yes (Premium for luxury heritage) |
| Glass-tech | Energetic | Yes (Premium for restraint) |
| Hand-crafted | Premium | Yes (Playful for whimsical) |

User confirms or overrides at Phase 2.6. Mismatches logged in `plans/{date}-{slug}/overrides.md`.
```

### Transition note about per-vibe easing

Add brief note explaining how this RELATES to existing per-vibe easing library:

```markdown
### Relationship to per-vibe easing (deprecated separation)

Pre-v2.4: each of 11 vibes had its own paired cubic-bezier (in § Easing Library). Post-v2.4: personality REPLACES that per-vibe pairing. Each vibe gets a default personality (table above); user can override.

For backward compatibility, the § Easing Library section is preserved but cross-references the personality system. New projects pick personality directly; legacy projects continue using vibe-paired easing if not migrated.
```

## Related code files

**Modify:** `references/motion-patterns.md` (insert ~80 lines)

**Create / Delete:** None

## Implementation steps

1. **Read motion-patterns.md** to identify insertion point (after existing Vibe × Motion Intensity Matrix or equivalent)
2. **Insert § Motion Personalities (Phase 2.6)** per Architecture above
3. **Add transition note** about per-vibe easing relationship
4. **Verify cross-references** — Phase 2.6 dialog in workflow-brainstorm.md (Phase 04 creates)

## Todo list
- [ ] Read motion-patterns.md, find insertion point
- [ ] Insert § Motion Personalities table (4 personalities)
- [ ] Insert Brand Motion Identity (3 locked constants)
- [ ] Insert Personality × Intensity matrix
- [ ] Insert Per-vibe personality defaults table (11 vibes)
- [ ] Add transition note about Easing Library relationship
- [ ] Verify file size growth ~+80 lines

## Success criteria
- motion-patterns.md has § Motion Personalities (Phase 2.6)
- 4 personalities defined with signature easing + duration palette + entrance pattern
- Brand Motion Identity 3 constants documented
- Personality × Intensity matrix (4 × 4) present
- Per-vibe defaults for all 11 vibes
- Cross-references documented (workflow-brainstorm.md to be created in Phase 04)
- Existing content untouched

## Risk assessment
- **Risk:** Existing per-vibe easing library conflicts with personality system → transition note explains; coexist gracefully
- **Risk:** "Default personality" recommendations feel arbitrary → derived from vibe character (Playful vibe = Playful personality is intuitive)
- **Risk:** Phase 2.6 dialog format not yet defined → Phase 04 owns that; Phase 02 just documents source-of-truth matrix

## Security considerations
None.

## Next steps
- Phase 04 creates Phase 2.6 dialog in workflow-brainstorm.md sub-file (references this matrix)
- Phase 05 SKILL.md Mermaid diagram adds Phase 2.6 node
- Phase 06 README v2.4.0 paragraph mentions Motion Personalities
