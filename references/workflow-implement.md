# Workflow — Phase 7 Implement (Inline implement protocol)

Detailed protocol for Phase 7. See `workflow-phases.md` for full pipeline navigation.

Skill implements directly from `plan.md` + `phase-XX-*.md` files. Per CLAUDE.md: NO auto-commit — user reviews + commits manually after each phase.

## Step 1 — Phase execution order
Follow `plan.md` dependency graph. Default sequential unless plan marks phases parallel-safe. Mark each phase status `in_progress` before starting; `completed` after success criteria all check.

## Step 2 — Per-phase constraints (enforce throughout)

**Imports:**
- Import icons from `app/components/icons` — NEVER `npm install` any icon library
- All fonts via `next/font/local` or `next/font/google` — NO `<link>` CDN
- 3D components: `'use client'` + `dynamic(() => import(...), { ssr: false })`
- React Three Fiber used as shader runner only — no `<GLTFLoader>` / `useGLTF` / `<OrbitControls>` unless user-GLB override logged

**Colors + tokens:**
- Use Tailwind theme tokens for all colors — no inline hex outside SVG icon paths
- Single accent token, ≤ 10% surface area
- Off-black / off-white only (never pure `#000` / `#FFF`)

**Layout + composition:**
- Hero composition follows `visual-direction.md` § Spatial Language (no centered-H1 unless vibe = minimal)
- `min-h-[100dvh]` not `h-screen`
- `text-wrap: balance` on h1/h2/h3; `text-wrap: pretty` on `<p>`

**Copy:**
- Real draft copy — no Lorem, no AI cliché vocabulary (per applicability matrix tier)
- Realistic data (no John Doe / 99.99% / Acme Corp)
- **Honest copy** — if metric / testimonial / logo / case-study count not supplied by user, use em-dash placeholder + label (`— metric to confirm`) rendered as visible grey block. Never invent. See `anti-slop-rules.md § Honest Copy Mandate` for 3 accepted paths.

**Motion (per `motion-patterns.md` § Motion Personalities + Vibe × Motion Intensity Matrix, locked Phase 2e + 2.6):**
- Apply motion ONLY at locked intensity (0/3 → 3/3)
- Use locked Brand Motion Identity (signature easing + duration palette + entrance pattern from Phase 2.6 personality)
- Stack escalation: CSS → Framer Motion → Lenis → GSAP (only escalate if prior tier insufficient)
- NO generic fade-up on every element (≤30% sections animate at 2/3 intensity)
- NO motion on body `<p>` text
- Use personality-paired `cubic-bezier(...)` easing (see `motion-patterns.md` § Motion Personalities) — NOT `ease-in-out` / `ease-out` named keywords
- `prefers-reduced-motion` MUST be respected (Framer Motion `useReducedMotion()` or CSS `@media`)
- Mobile auto-degrades intensity by 1 step at < 768px
- Total motion JS bundle ≤ 100KB gz

## Step 3 — Mid-implementation spot-checks
After each section completes, verify:
- **Imports list** — any forbidden icon / font library?
- **Color values** — any inline hex outside theme tokens (excluding SVG paths)?
- **Copy** — any "Elevate / Seamless / Unleash / Empower / Game-changer / Next-gen"?
- **Motion** — any `ease-in-out 0.3s` default? Any motion on body `<p>`?
- **Icons** — any emoji used in place of icon?
- **3D** — any `OrbitControls` / `MeshNormalMaterial` / `useGLTF` without override log?
- **Bento Grid (if used)** — `grid-flow-dense` present? No empty cells / voids?

## Step 4 — Commit pattern (when user commits manually)
- One phase = one focused commit (not one mega-commit at end)
- Commit message: conventional commits format (`feat:` / `fix:` / `refactor:` / `docs:` / `chore:`)
- No AI-tool references in commit messages
- Stage files explicitly (no `git add .`) to avoid accidentally committing secrets / build artifacts
- Pre-commit hooks pass (lint, type-check) — never `--no-verify`

## Step 5 — Phase completion check
- Mark phase status `completed` in `phase-XX-*.md`
- Update `plan.md` phase table status
- Update `plan.md` § Success criteria checkboxes
- Notify user phase is done; await confirmation before starting next phase

## Step 6 — Project memory log write (v2.4.0+)

After Phase 7 completes (all plan phases marked `completed`), append a new entry to `.perfect-ui/log.json` at project root. Schema:

```json
{
  "date": "{YYYY-MM-DD}",
  "brief": "{1-line summary from brief.md}",
  "vibe": "{anchor from brief.md}",
  "wildcard": "{adjective from brief.md}",
  "macrostructure": "{name from Phase 2c}",
  "design_variance": {value 1-10 from Phase 2},
  "visual_density": {value 1-10 from Phase 2},
  "motion_personality": "{Playful|Premium|Corporate|Energetic from Phase 2.6}",
  "motion_intensity": {value 0-3 from Phase 2e},
  "illustration_style": "{from 2d-illustration-catalog.md picked at Phase 4}"
}
```

Insert at the FRONT of the JSON array. Trim to last 20 entries (oldest dropped). Create `.perfect-ui/` directory if missing. Suggest adding `.perfect-ui/` to `.gitignore` on first scan (respect existing `.gitignore`).

This entry is what `workflow-brainstorm.md` § Phase 0.5 reads on the NEXT run for diversification enforcement.

## Cross-references

- `workflow-phases.md` — full pipeline navigation
- `workflow-brainstorm.md` — Phase 0.5 reads log.json written by this file
- `workflow-plan.md` — Phase 6 plan protocol (this file consumes plan)
- `workflow-audit.md` — Phase 8 audit protocol
- `motion-patterns.md § Motion Personalities` — Brand Motion Identity used here
- `anti-slop-rules.md` — Honest Copy Mandate + Diversification Rule
- `macrostructure-catalog.md` — macrostructure name + gapless bento mandate
