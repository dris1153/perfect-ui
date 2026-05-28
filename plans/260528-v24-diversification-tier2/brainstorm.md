# perfect-ui v2.4.0 — Diversification (Tier 2)

**Date:** 2026-05-28
**Status:** Brainstorm complete, awaiting plan approval
**Skill version impact:** v2.3.0 → v2.4.0 (minor — additive structural, backward-compatible)
**Parent roadmap:** [260528-taste-skill-research-upgrades/brainstorm.md](../260528-taste-skill-research-upgrades/brainstorm.md)

---

## Problem statement

v2.3 closed completeness gaps. v2.4 addresses **structural variety** — Hallmark's core insight that "two pages by the skill for two different briefs shouldn't share the same hero → 3-feature → CTA → footer rhythm." Currently perfect-ui has 11 vibes × ~4 section archetypes = 44 fixed pairs, but no mechanism to enforce diversification across runs in the same project. v2.4 introduces:

1. **Project memory** — `.perfect-ui/log.json` tracks past picks
2. **Macrostructure layer** — 7 named page-shape macrostructures (Hallmark-vocabulary) tách biệt khỏi vibe
3. **2 dials** — DESIGN_VARIANCE + VISUAL_DENSITY (numeric + descriptive labels)
4. **Motion personalities** — 4 archetypes (Playful/Premium/Corporate/Energetic) × intensity matrix
5. **Brand Motion Identity** — Phase 2.6 locks 3 motion constants
6. **Hero composition catalog** — 10 alternatives in section-archetypes.md
7. **Gapless Bento Grid mandate** — inline in macrostructure-catalog.md

Plus **proactive workflow-phases.md split** — break 820-line monolith into 4 sub-references (Q10).

## Requirements (locked from Q1-Q10)

| ID | Decision | Source Q |
|----|----------|----------|
| R1 | NEW `macrostructure-catalog.md` (~200 lines, 7 macrostructures fully spec'd) | Q1 |
| R2 | Adopt Hallmark's vocabulary: Marquee Hero · Bento Grid · Long Document · Manifesto · Stat-Led · Workbench · Letter | Q2 |
| R3 | Full `.perfect-ui/log.json` (20-entry rolling JSON array) | Q3 |
| R4 | Per-vibe DESIGN_VARIANCE + VISUAL_DENSITY defaults (derive from existing 11 vibe characterizations) | Q4 |
| R5 | Personality × Intensity matrix (independent axes — both locked at Phase 2e/2.6) | Q5 |
| R6 | Hero composition catalog (10 alternatives) expanded in section-archetypes.md | Q6 |
| R7 | Gapless Bento Grid rule inline in macrostructure-catalog.md § Bento Grid | Q7 |
| R8 | Atmosphere descriptive spectrum inline in dial definitions (per dial) | Q8 |
| R9 | New Phase 2.6 (Brand Motion Identity) separate from Phase 2e intensity | Q9 |
| R10 | Proactive file split — workflow-phases.md → 4 sub-references (workflow-brainstorm.md, workflow-plan.md, workflow-implement.md, workflow-audit.md) | Q10 |

## Evaluated approaches

Each major decision had 2-3 options presented via Q1-Q10. Selected per user picks. No alternative architecture at v2.4 level — additive structural layer on top of v2.3.

## Final design — per-item specifications

### Item D — Project memory + Diversification rule

**NEW file format `.perfect-ui/log.json` at project root:**

```json
[
  {
    "date": "2026-05-28",
    "brief": "Specialty coffee subscription — Tokyo home-brew",
    "vibe": "editorial",
    "wildcard": "agrarian",
    "macrostructure": "Marquee Hero",
    "design_variance": 6,
    "visual_density": 3,
    "motion_personality": "Premium",
    "motion_intensity": 2,
    "illustration_style": "silkscreen"
  },
  ...
]
```

20-entry rolling buffer (oldest dropped). Append at Phase 7 completion. Read at Phase 0.5 + Phase 2.

**Diversification rule (enforced Phase 2):**
- Macrostructure: must differ from last 3 entries
- Vibe + wildcard combo: should differ from last 1 entry (warn if repeat; allow override)
- DESIGN_VARIANCE + VISUAL_DENSITY: at least 1 dial differs ≥3 points from last entry
- Motion personality: should differ from last 1 entry (warn if same)

**workflow-phases.md update (Phase 0.5 + Phase 2 integration):**
- Phase 0.5 reads log.json, surfaces "Last 3 entries:" line
- Phase 2 dials/macrostructure picks enforce diversification rule

**`.gitignore` recommendation:** add `.perfect-ui/` (skill suggests on first scan).

### Item E — Macrostructure layer (NEW `macrostructure-catalog.md`)

**Structure (~200 lines):**

```
# Macrostructure Catalog

## What macrostructures are
[Page-shape archetypes — independent of vibe. Vibe locks visual identity; macrostructure locks page rhythm.]

## The 7 macrostructures

### 1. Marquee Hero
- Hero archetypes: A1 (full-bleed declarative) | A2 (asymmetric 70/30)
- Section rhythm: Hero → social-proof → 2-3 features → CTA → footer
- Best for: brand statements, declarative launches
- Default dials: variance 7, density 3
- Diversification axes: paper=any, accent=any
- AI tell to avoid: 5-section equal-weight cards underneath

### 2. Bento Grid
- Hero archetypes: A3 (mini hero + bento canvas) | A4 (no hero, full-bleed grid)
- Section rhythm: Mini hero → 6-12 cell bento → CTA → footer
- Best for: SaaS feature showcase, modular product
- **Gapless mandate:** `grid-flow-dense` required. Mathematical verification of col-span / row-span interlock. Empty cells = Tier 1 violation. (See `anti-slop-rules.md` for tier classification.)
- Default dials: variance 7, density 6
- AI tell to avoid: 3×3 perfect grid (use 8-cell asymmetric mix)

### 3. Long Document
- Hero archetypes: A5 (editorial spread) | A6 (number + headline)
- Section rhythm: Editorial hero → numbered section 01-05 → CTA → footer
- Best for: case studies, manifestos, deep narratives
- Note: numbered sections allowed here per macrostructure context (universal meta-label ban — see anti-slop rule #12 — relaxed for Long Document genuinely ordinal content)
- Default dials: variance 3, density 3

### 4. Manifesto
- Hero archetypes: A7 (massive typography only) | A8 (statement + signature)
- Section rhythm: Statement → quote chain → small footer
- Best for: brand identity, mission statement, atelier sites
- Default dials: variance 9, density 2

### 5. Stat-Led
- Hero archetypes: A9 (number-led headline) | A10 (proof bar above hero)
- Section rhythm: Stat hero → logos → 3-4 stat cards → testimonial → CTA → footer
- Best for: B2B SaaS proof-heavy landings
- **Honest copy enforcement:** every stat needs source OR em-dash placeholder. No fabrication.
- Default dials: variance 5, density 5

### 6. Workbench
- Hero archetypes: A4 (no hero) | A11 (compact toolbar hero)
- Section rhythm: Tool surface → sidebar nav → main content area
- Best for: app surfaces, dashboards, admin
- Note: generic tier only; not for landing
- Default dials: variance 4, density 7

### 7. Letter
- Hero archetypes: A12 (correspondence opener) | A13 (handwritten note)
- Section rhythm: Letter opening → body paragraphs → signature → contact
- Best for: about pages, founder letters, personal portfolios variant
- Default dials: variance 6, density 3

## Diversification rule (cross-run)

Read `.perfect-ui/log.json`. Macrostructure pick must NOT match any of the last 3 entries.

## Macrostructure × Vibe interaction

Same macrostructure with different vibe = different feel (Bento Grid + Editorial vibe ≠ Bento Grid + Brutalist vibe). Macrostructure × vibe gives 7 × 11 = 77 combinations.

## Picking a macrostructure (Phase 2 sub-step)

After vibe lock, pick macrostructure based on:
1. Page-purpose
2. Brief inspirations
3. Diversification from log
```

### Item F + T — DESIGN_VARIANCE + VISUAL_DENSITY dials (with atmosphere spectrum)

**Add to `visual-direction-guide.md` § 2 new dials sub-section:**

```markdown
## Two dials — DESIGN_VARIANCE + VISUAL_DENSITY (Phase 2)

Beyond motion intensity (Phase 2e), two more dials lock at Phase 2:

### DESIGN_VARIANCE (1-10)
- **1-3 = Predictable / Art Gallery Symmetric** — flex justify-center, strict 12-col, equal paddings
- **4-7 = Offset / Daily App Asymmetric** — margin offsets, mixed aspect ratios, left-aligned headers
- **8-10 = Artsy / Chaotic Asymmetric** — masonry, fractional grid units, massive empty zones
- Universal mobile collapse rule: variance 4+ aggressively falls back to single-column at <768px

### VISUAL_DENSITY (1-10)
- **1-3 = Art Gallery / Airy** — lots of whitespace, huge section gaps, expensive feel
- **4-7 = Daily App / Balanced** — normal SaaS spacing
- **8-10 = Cockpit / Dense** — tiny paddings, 1px lines instead of cards, monospaced numbers

### Per-vibe defaults

| Vibe | DESIGN_VARIANCE | VISUAL_DENSITY |
|------|-----------------|----------------|
| Minimal | 3 | 3 |
| Editorial | 6 | 4 |
| Brutalist | 8 | 7 |
| Retro-futuristic | 7 | 5 |
| Organic | 4 | 3 |
| Luxury | 4 | 3 |
| Playful | 6 | 5 |
| Industrial | 5 | 7 |
| Art-deco | 5 | 4 |
| Glass-tech | 6 | 4 |
| Hand-crafted | 5 | 3 |

User confirms or overrides at Phase 2.

### Diversification rule (cross-run)

Read `.perfect-ui/log.json`. New run must differ from last entry on at least one dial by ≥3 points.
```

### Item K — 4 Motion Personalities + Phase 2.6 Brand Motion Identity

**`motion-patterns.md` § new section:**

```markdown
## Motion Personalities (Phase 2.6)

Select ONE archetype per project. Independent of intensity (0-3/3). Personality drives character; intensity drives amount.

| Personality | Signature easing | Duration palette (quick/standard/slow) | Entrance pattern | Vibe defaults |
|-------------|------------------|----------------------------------------|------------------|---------------|
| **Playful** | ease-out-back (10-20% overshoot) | 150ms / 250ms / 400ms | Spring bounce | Playful, Organic |
| **Premium** | cubic-bezier(0.4, 0, 0.2, 1) | 250ms / 400ms / 600ms | Subtle fade-up | Minimal, Editorial, Luxury, Hand-crafted |
| **Corporate** | cubic-bezier(0.2, 0, 0, 1) | 200ms / 300ms / 400ms | Crisp slide | Industrial, Art-deco |
| **Energetic** | ease-out-expo (15-30% overshoot) | 100ms / 200ms / 350ms | Quick translate | Brutalist, Retro-futuristic, Glass-tech |

### Brand Motion Identity (3 locked constants)

Once personality picked, 3 constants are LOCKED for project:
1. **Signature easing** — single cubic-bezier curve used in 80% of animations
2. **Duration palette** — quick/standard/slow values
3. **Entrance pattern** — consistent reveal style (no mixing fade-up + slide + scale randomly)

Phase 2.6 dialog (new sub-phase between 2e motion intensity and Phase 3):
```
AskUserQuestion header: "Brand Motion Identity"
Question: "Motion personality (drives signature easing + duration + entrance pattern)?"
Default = vibe-derived (per matrix above)
Options: Playful · Premium · Corporate · Energetic
```

### Personality × Intensity matrix

Personality locks character. Intensity locks scope. Both axes independent.

- Premium + 1/3 = subtle premium hover only
- Premium + 3/3 = full premium choreography (scroll-linked + smooth)
- Energetic + 1/3 = quick CSS-only snaps
- Energetic + 3/3 = bold scroll choreography with overshoot
```

### Item O — Hero composition catalog (10 alternatives)

**Append to `section-archetypes.md`:**

```markdown
## Hero composition catalog (10 alternatives)

Beyond left-text/right-image (the most overused AI hero pattern), 10 alternatives. Pick by macrostructure + vibe.

| ID | Name | Layout | Best for vibe | Best for macrostructure |
|----|------|--------|---------------|-------------------------|
| A1 | Full-bleed declarative | Single H1 over full-bleed image, no flex | Editorial, Luxury | Marquee Hero |
| A2 | Asymmetric 70/30 | Text 70%, image 30% (right) | Editorial | Marquee Hero |
| A3 | Mini hero + canvas | Tiny H1 + huge bento grid below | Minimal, Glass-tech | Bento Grid |
| A4 | No hero, full-bleed grid | Page opens directly to grid | Brutalist, Glass-tech | Bento Grid |
| A5 | Editorial spread | Magazine 2-column spread | Editorial | Long Document |
| A6 | Number + headline | Massive number (00) + headline next | Editorial, Art-deco | Long Document |
| A7 | Massive typography only | Single statement, no image | Brutalist, Minimal | Manifesto |
| A8 | Statement + signature | Quote + author name | Editorial, Hand-crafted | Manifesto, Letter |
| A9 | Number-led headline | Big stat (47.2%) + supporting text | Industrial | Stat-Led |
| A10 | Proof bar above hero | Logos row → hero below | Glass-tech | Stat-Led |
| A11 | Compact toolbar hero | Top bar + main canvas | Industrial | Workbench |
| A12 | Correspondence opener | "Dear..." letter style | Editorial, Hand-crafted | Letter |
| A13 | Handwritten note | Sketch + signature | Hand-crafted | Letter |

Default: anti-pattern check. If brief default = left-text/right-image, force pick from this catalog.
```

### Item R — Gapless Bento Grid mandate

Embedded in `macrostructure-catalog.md` § 2. Bento Grid (above). Also flag in anti-slop-rules.md tag matrix:

```markdown
| Empty bento grid cells (missing corners / voids) | `[universal]` | 1 |
```

## File-level impact summary

**New files (5):**
- `references/macrostructure-catalog.md` (~200 lines, 7 macrostructures)
- `references/workflow-brainstorm.md` (~150 lines, from Q10 split)
- `references/workflow-plan.md` (~150 lines, from Q10 split)
- `references/workflow-implement.md` (~100 lines, from Q10 split)
- `references/workflow-audit.md` (~150 lines, from Q10 split)

**Modified files (~7):**
- `references/workflow-phases.md` — split content moved out, leaves ~250-300 lines (Phase 0/0.1/0.5/2/2.6/3/4/5 + cross-refs to sub-files)
- `references/motion-patterns.md` — § Motion Personalities + per-vibe defaults
- `references/visual-direction-guide.md` — § 2 dials + per-vibe defaults
- `references/anti-slop-rules.md` — Empty bento Tier 1 rule + diversification rule reference
- `assets/nextjs-skeleton/section-archetypes.md` — Hero composition catalog (A1-A13)
- `SKILL.md` — frontmatter version 2.4.0 + Phase 2.6 reference + new files in References table
- `README.md` — v2.4.0 update + 1-2 new FAQ
- `index.html` — version + Mandates update (Diversification mandate)

**Total estimated new content:** ~+650 lines across 5 new files + ~+200 in modifications = ~+850 lines net.

**Workflow-phases.md size after split:** 820 → ~250-300 (massive reduction in main file).

**Cross-version concern:** After v2.4, repo will have 17 reference files. Still manageable. v2.5 will add 2-3 more.

## Implementation considerations

- **JSON log file:** simple append + rotation logic. Use Node fs API if cook implements; manual user check OK.
- **Cross-file consistency:** macrostructure ↔ hero archetypes ↔ vibe defaults must all reference consistent vocabulary
- **Workflow split semantics:** workflow-phases.md becomes a navigation hub; sub-files own the protocol details
- **Backward compat:** existing landing/portfolio/generic Phase outputs schema-identical (additive layer)
- **Diversification rule severity:** macrostructure mismatch with last 3 = enforce; dial repeat = warn; vibe repeat = warn (user override OK)

## Success criteria (overall)

1. `.perfect-ui/log.json` written after Phase 7 + read at Phase 0.5 + Phase 2
2. macrostructure-catalog.md exists with 7 macrostructures fully spec'd
3. workflow-phases.md split into 4 sub-references; original file reduced to navigation + Phase 0/0.5/2/2.6/3-5 + Phase 8 summary
4. 2 dials defined with atmosphere spectrum labels + per-vibe defaults
5. Motion Personalities table + Phase 2.6 dialog
6. Hero composition catalog (10-13 alternatives) in section-archetypes.md
7. Empty bento Tier 1 rule in anti-slop matrix
8. Version 2.4.0 in 4 critical locations
9. Diversification rule enforced (macrostructure must differ from last 3; dials differ from last by ≥3)

## Risks

| Risk | Mitigation |
|------|------------|
| 5 new files at once = bloat | KISS verification — each file has distinct concern; cross-references minimize redundancy |
| Workflow split breaks existing references | Phase 5 of plan = exhaustive cross-reference audit |
| log.json schema drift | Lock schema in macrostructure-catalog.md + cross-ref in workflow-brainstorm.md |
| Diversification rule too rigid (every run blocks) | Diversification = warnings + soft enforcement (warn user, allow override). Only macrostructure-last-3 is hard rule. |
| Per-vibe dial defaults conflict with macrostructure defaults | Resolution rule: vibe sets defaults; macrostructure can adjust ±2; user override always wins |
| Motion personalities × intensity = too many combinations | Default = vibe-driven (4 personalities × 4 intensities = 16 valid combinations; matrix table shows allowable) |

## Out of scope (defer)

- v2.5 items (G study verb, H component-scope, Q design_plan block)
- Macrostructure variants per type (landing-specific Workbench vs generic Workbench)
- Per-macrostructure section archetype expansion (defer to v2.5 if needed)
- Personality × intensity × vibe 3D matrix (too complex; per-vibe defaults already give 11 × 4 × 4 = 176 valid; enough)
- Auto-pick macrostructure (always user-chooses or vibe-default; never silent auto)
- Lottie / Spring-physics specific motion personalities (4 is enough; expand if v2.5+ demand)

## Next steps

1. User approve this brainstorm → proceed `/ck:plan`
2. Plan dự kiến: 6-7 phases (large) — break by file ownership
3. Each phase parallel-safe by file ownership where possible

## Unresolved questions (resolve in /ck:plan or execution)

- Workflow split granularity: 4 sub-files OR more? (e.g., split Phase 4 + Phase 5 out too?) — defer to plan
- macrostructure-catalog.md per-macrostructure depth: how detailed each? (1 page each vs 1 paragraph each)
- Empty bento detection: how does Phase 8 audit verify gapless? (grep `grid-flow-dense` presence OR visual check via vision model)
- `.perfect-ui/log.json` write timing: Phase 7 completion OR after user commit? (commit-time would require user-action; Phase 7-end simpler)
- Hero archetype IDs (A1-A13) conflict with existing section-archetypes.md numbering? (verify before plan)
- Phase 2.6 dialog UX: separate AskUserQuestion call after 2e, or combine? (separate cleaner; combined fewer prompts)
- Version 2.4.0 mandate update in index.html: add new Mandate card "Diversify each run" OR fold into existing? (defer to plan)
- README v2.4.0 paragraph: 1 paragraph or 2 (one for macrostructure, one for diversification)?
