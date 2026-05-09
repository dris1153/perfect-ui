---
title: 2D-priority pivot — ban AI-generated 3D models, threejs for shaders only
date: 2026-05-10
status: approved
type: brainstorm
---

# Brainstorm — 2D Priority + Effect-Only Threejs

## Problem Statement

Current skill allows hero 3D model scenes (rotating product GLB on glass podium with HDRI). Direct evidence from `plans/260509-ai-vs-human-analysis/synthesis.md`:

- 0/7 human-crafted pages used real-time 3D model rendering
- Augen used a STATIC 3D RENDER as 2D image (Blender → PNG)
- Overlay used WebGL for SHADER-based atmospheric color effect
- Other human pages used 0 WebGL — pure 2D craft

The skill's current `threejs-integration-patterns.md` recommends GLB rendering / OrbitControls / product configurators — exactly what NO real human-crafted landing does. The skill is teaching AI fingerprints unintentionally.

## Approved Decisions

| Item | Decision |
|------|----------|
| Scope of "no 3D model" | **Loose** — ban AI-generated GLB/GLTF as hero subject; user-provided real-product GLB allowed (logged override) |
| Phase 5 rename | **"Visual Effect Layer"** |
| 2D asset expansion | All 4 — static 3D render template, SVG illustrations, asset cohesion rules, vibe×style catalog |
| `threejs-integration-patterns.md` | **Full rewrite** — shader/effect catalog, no GLB/GLTF; rename to `visual-effect-patterns.md` |

## Approaches Considered

### A. Strict ban (rejected)
Forbid all `<mesh>` even with primitive geometry. Too restrictive — particle fields rendered with point clouds need primitives.

### B. Moderate (rejected)
Ban GLB/GLTF, allow primitives. Doesn't address user-provided product GLB use case (rare but legitimate).

### C. Loose with override (CHOSEN)
- Forbid AI-generated 3D models as hero subject
- Allow primitives for shader canvases / particle fields
- Allow user-provided real-product GLB with logged override
- Encourage static 3D render → 2D image (Augen pattern) as alternative

### D. Static-only (rejected)
Allow only static renders. Too restrictive — shader effects (overlay's color gradient) genuinely earn their place.

## Key Insight: Three Categories

| Category | Status | Examples |
|----------|--------|----------|
| **3D model as hero** | FORBIDDEN (Tier 1, unless user-GLB override) | Rotating product, character, AI-generated 3D blob, GLTF showcase |
| **Static 3D render → 2D** | ALLOWED, encouraged | Augen head silhouette, hero illustration rendered in Blender/Spline exported as PNG |
| **Visual effect (shader/particle)** | ALLOWED | Overlay color gradient WebGL, particle field, scroll-driven distortion, displacement plane |

## Implementation Outline

### File changes
```
RENAME: references/threejs-integration-patterns.md → references/visual-effect-patterns.md
REWRITE: visual-effect-patterns.md (shader/particle/effect focus)
NEW:    references/2d-illustration-catalog.md (11 vibes × illustration styles)
UPDATE: SKILL.md (Phase 4 expand + Phase 5 rename + Hard Rules + refs)
UPDATE: references/visual-asset-prompt-library.md (3 new sections)
UPDATE: references/visual-direction-guide.md (effect layer pairing matrix)
UPDATE: references/anti-slop-rules.md (Tier 1 AI-gen 3D model)
UPDATE: references/workflow-phases.md (Phase 4 + 5 updates)
UPDATE: README.md (FAQ + phase desc)
```

### New terminology
- **3D model** = forbidden for hero unless user-provided real product
- **Static 3D render** = OK as 2D image asset (use Blender, Spline, KeyShot, etc., export PNG)
- **Visual effect** = shaders, particles, atmospheric layer (real-time WebGL/CSS, no model showcase)

### Vibe × illustration style catalog (new)
| Vibe | Recommended 2D illustration style |
|------|-----------------------------------|
| Minimal | SVG geometric + line-art |
| Editorial | Silkscreen poster, hand-drawn ink, woodblock-style |
| Brutalist | Risograph, photocopy, harsh halftone |
| Retro-futuristic | Synthwave gradient, vector wireframe-as-2D, vaporwave collage |
| Organic | Watercolor, ink wash, botanical drawing |
| Luxury | Engraved line-art, etched portrait, photographic still-life |
| Playful | Cut-paper collage, claymation render-to-2D, cartoon sketch |
| Industrial | Technical schematic, architectural section, blueprint |
| Art-deco | Geometric sunburst, fan motif, heritage poster |
| Glass-tech | Static 3D render → 2D (Blender/Spline export), refractive forms |
| Hand-crafted | Risograph, printmaking, sketchbook |

## Risks

| Risk | Mitigation |
|------|-----------|
| User legit needs real-time product GLB display | Loose-scope override path allows it with log |
| `visual-effect-patterns.md` rename breaks external bookmarks | Internal-only file, low impact |
| Vibe × style catalog adds another maintenance touch-point | Maps to existing 11 vibes, no new vibes |
| Confusion: "3D" word retained in effect contexts | Documentation clear: "3D effect" = shader, not model |

## Success Criteria

- [ ] No GLB/GLTF examples remain in `visual-effect-patterns.md` (renamed)
- [ ] Phase 5 in SKILL.md reads "Visual Effect Layer"
- [ ] Hard Rules explicitly forbids AI-generated 3D model as hero
- [ ] Anti-slop Tier 1 includes AI-gen 3D model rule
- [ ] New `2d-illustration-catalog.md` covers 11 vibes
- [ ] `visual-asset-prompt-library.md` has Static 3D render + SVG illustration sections
- [ ] `quick_validate.py` passes
- [ ] README.md FAQ explains the 3D distinction

## Unresolved Questions

1. Should Three.js be a hard prereq mention or just one option for shaders? CSS gradients + Lottie can deliver atmospheric without WebGL.
2. Does the loose override (user-provided GLB) need a separate "product-showcase landing" anatomy variant for hardware brands?
3. Should we add a "Phase 5 Decision Tree" question: shader vs CSS vs Lottie vs none?
