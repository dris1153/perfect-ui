# Phase 03 — Macrostructure catalog + Hero catalog A5-A13

## Context links
- [brainstorm.md](./brainstorm.md) § Item E (Macrostructure layer), Item O (Hero composition catalog), Item R (Gapless Bento Grid mandate)
- [assets/nextjs-skeleton/section-archetypes.md](../../assets/nextjs-skeleton/section-archetypes.md) — existing A1-A4

## Overview
- **Priority:** High (NEW catalog file, referenced by Phase 04 workflow split)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 02
- **Description:** CREATE `references/macrostructure-catalog.md` (~200 lines, 7 macros with Hallmark vocabulary). Extend section-archetypes.md A1-A4 → A5-A13 (9 new hero archetypes mapped to macrostructures).

## Key insights
- 7 macrostructures use Hallmark vocabulary directly (Q2 locked)
- Each macro spec: hero archetypes (cross-link to section-archetypes.md) + section rhythm + best-for + dial defaults + diversification axes + AI tells to avoid
- Bento Grid section has Gapless mandate (inline)
- Hero catalog extends A1-A4 (landing-specific) with A5-A13 (cross-macrostructure)
- Per-macro depth: ~25-28 lines each × 7 = ~196 line catalog
- Catalog has intro + diversification rule section = ~200 total

## Requirements

### Functional
- NEW `references/macrostructure-catalog.md` exists with 7 macrostructures
- Each macro section: name + hero archetypes + section rhythm + best-for + dial defaults + diversification axes + AI tells to avoid
- Bento Grid section has Gapless mandate (`grid-flow-dense` + verification rule)
- section-archetypes.md gets new heroes A5-A13 (each with: layout description + best-for vibes + best-for macrostructures)
- Cross-references: macrostructure-catalog.md → section-archetypes.md (hero IDs) and visual-direction-guide.md (dial defaults)

### Non-functional
- macrostructure-catalog.md ~200 lines (target)
- section-archetypes.md grows ~+50 lines (9 new hero archetypes)
- Existing section-archetypes.md A1-A4 untouched
- Hallmark vocabulary preserved verbatim (no perfect-ui-specific renaming)

## Architecture

### NEW macrostructure-catalog.md structure

```markdown
# Macrostructure Catalog

Page-shape archetypes — independent of vibe. Vibe locks visual identity (palette + typography + spatial language); macrostructure locks page rhythm (section sequence + page chrome density + hero pattern).

Same macrostructure with different vibes = different feel. 7 macrostructures × 11 vibes = 77 valid combinations. Diversification rule prevents repetition across runs in same project.

## When to pick a macrostructure (Phase 2)

After vibe is locked (Phase 1) and palette + typography are chosen (Phase 2a-2b), pick macrostructure at Phase 2c. The macrostructure choice drives:
- Hero archetype (see `assets/nextjs-skeleton/section-archetypes.md` § Hero Archetypes)
- Section rhythm (which sections, what order)
- DESIGN_VARIANCE + VISUAL_DENSITY defaults (overriding vibe defaults from `visual-direction-guide.md`)

Diversification rule: macrostructure pick must NOT match any of the last 3 entries in `.perfect-ui/log.json`.

## The 7 macrostructures

### 1. Marquee Hero
- **Hero archetypes:** A1 (Editorial Asymmetric 60/40) | A5 (Full-bleed declarative)
- **Section rhythm:** Hero → social-proof → 2-3 features → CTA → footer
- **Best for:** brand statements, declarative launches, single-product landings
- **Dial defaults:** DESIGN_VARIANCE 7, VISUAL_DENSITY 3
- **Diversification axes:** paper (any), accent (any), display style (any)
- **AI tell to avoid:** 5-section equal-weight feature cards underneath the hero

### 2. Bento Grid
- **Hero archetypes:** A6 (Mini hero + bento canvas) | A7 (No hero, full-bleed grid)
- **Section rhythm:** Mini hero → 6-12 cell bento → CTA → footer
- **Best for:** SaaS feature showcase, modular product, integration ecosystems
- **Dial defaults:** DESIGN_VARIANCE 7, VISUAL_DENSITY 6
- **Gapless mandate (Tier 1 anti-slop rule):** `grid-flow-dense` is MANDATORY on all bento grids. Mathematical verification: every col-span/row-span value must interlock with neighbors — no missing corners, no voids, no empty cells. Empty cells = templated AI feel.
- **Diversification axes:** any vibe
- **AI tell to avoid:** 3×3 perfect symmetric grid (use 8-cell asymmetric mix with varied spans)

### 3. Long Document
- **Hero archetypes:** A2 (Minimal Centered) | A8 (Editorial spread) | A9 (Number + headline)
- **Section rhythm:** Editorial hero → numbered section 01-05 → CTA → footer
- **Best for:** case studies, manifestos, deep narratives, editorial-led pages
- **Dial defaults:** DESIGN_VARIANCE 3, VISUAL_DENSITY 3
- **Note:** numbered sections ALLOWED in this macrostructure (universal meta-label ban — see `anti-slop-rules.md` Tier 1 rule #12 — is relaxed for genuinely ordinal Long Document content). Cap at ≤5 numbered sections.
- **Diversification axes:** display style (serif vs sans), accent hue (warm vs cool)
- **AI tell to avoid:** numbered sections without actual ordinal content (decorative numbers)

### 4. Manifesto
- **Hero archetypes:** A10 (Massive typography only) | A11 (Statement + signature)
- **Section rhythm:** Statement → quote chain → small footer
- **Best for:** brand identity, mission statement, atelier sites, foundry-adjacent
- **Dial defaults:** DESIGN_VARIANCE 9, VISUAL_DENSITY 2
- **Diversification axes:** any
- **AI tell to avoid:** centered statement at variance < 4 (defeats macrostructure point)

### 5. Stat-Led
- **Hero archetypes:** A12 (Number-led headline) | A13 (Proof bar above hero)
- **Section rhythm:** Stat hero → logos → 3-4 stat cards → testimonial → CTA → footer
- **Best for:** B2B SaaS proof-heavy landings, fintech, enterprise marketing
- **Dial defaults:** DESIGN_VARIANCE 5, VISUAL_DENSITY 5
- **Honest copy enforcement (CRITICAL):** every stat MUST have source OR em-dash placeholder (`— metric to confirm`). Fabricated stats are immediate fail. See `anti-slop-rules.md § Honest Copy Mandate` for 3 accepted paths.
- **Diversification axes:** logo bar (top vs after hero), card layout (3-col vs 2x2)
- **AI tell to avoid:** round-fake stats (99.99% / 10x faster / 1M+ users)

### 6. Workbench
- **Hero archetypes:** A7 (No hero, full-bleed) | A14 (Compact toolbar hero)
- **Section rhythm:** Tool surface → sidebar nav → main content area → optional bottom bar
- **Best for:** app surfaces (dashboards, admin panels), generic tier only
- **Note:** NOT for landing tier — landing macrostructures don't use Workbench. Generic tier appropriate when `--type=dashboard|admin|app`.
- **Dial defaults:** DESIGN_VARIANCE 4, VISUAL_DENSITY 7
- **Diversification axes:** sidebar position (left vs right vs collapsible)
- **AI tell to avoid:** sidebar + cards + breadcrumbs + top bar = chrome overload

### 7. Letter
- **Hero archetypes:** A15 (Correspondence opener "Dear...") | A16 (Handwritten note + sketch)
- **Section rhythm:** Letter opening → body paragraphs → signature → contact
- **Best for:** about pages, founder letters, personal portfolios variant, brand stories
- **Dial defaults:** DESIGN_VARIANCE 6, VISUAL_DENSITY 3
- **Diversification axes:** opener style (formal "Dear" vs casual "Hi"), signature placement
- **AI tell to avoid:** "Hi I'm a passionate designer who loves coffee" — see `portfolio-anatomy.md` anti-clichés

## Macrostructure × Vibe interaction

Same macrostructure with different vibe = different feel:
- **Bento Grid + Editorial vibe** = magazine-spread bento with serif display, asymmetric column weights, paper textures
- **Bento Grid + Brutalist vibe** = monolithic cells with hard divider lines, no shadows, sharp corners
- **Bento Grid + Glass-tech vibe** = refractive glass cells with backdrop-blur, subtle inner shadows, hairline borders

Vibe locks the SURFACE; macrostructure locks the SHAPE. They combine multiplicatively.

## Diversification rule

Read `.perfect-ui/log.json` at Phase 0.5 (see `workflow-brainstorm.md` § Step 2.5 — log read).

**Hard rule:** macrostructure pick must NOT match any of the last 3 entries. If user demands same macrostructure, log override in `plans/{date}-{slug}/overrides.md`.

**Soft rule (warning, override allowed):**
- Vibe + wildcard combo same as last entry (warn)
- DESIGN_VARIANCE OR VISUAL_DENSITY same as last (warn — at least one dial should differ ≥3 points)
- Motion personality same as last (warn)

State diversification check verbosely at Phase 2:
> "Last 3 macrostructures: Marquee Hero (Tracejam) · Bento Grid (Foundry) · Long Document (Maple). Picking Marquee Hero again would violate the hard rule — choosing from {Manifesto, Stat-Led, Workbench, Letter} this time."

## Cross-references

- Hero archetypes: `assets/nextjs-skeleton/section-archetypes.md` § Hero Archetypes (A1-A16)
- Dial defaults (DESIGN_VARIANCE + VISUAL_DENSITY): `visual-direction-guide.md` § Two dials
- Anti-slop rules (Gapless bento, Honest copy, Meta-label ban exception for Long Document): `anti-slop-rules.md`
- Phase 2 workflow integration: `workflow-brainstorm.md` § Step 2c (macrostructure pick)
- Project memory log: `.perfect-ui/log.json` (schema in `workflow-brainstorm.md` § log format)
```

### section-archetypes.md Hero catalog extension

Append AFTER existing A4 in section-archetypes.md (before any other section like Features or Testimonials):

```markdown
### A5. Full-bleed declarative
**Use when:** vibe + wildcard demands authoritative single H1 over full-bleed image, macrostructure = Marquee Hero
**Layout:** H1 centered horizontal but offset vertically (bottom 40%), image full-bleed background with subtle gradient overlay, single CTA below H1
**Best for vibes:** Editorial, Luxury, Brutalist
**Best for macrostructures:** Marquee Hero

### A6. Mini hero + bento canvas
**Use when:** macrostructure = Bento Grid, page has tools/features showcase
**Layout:** Small H1 + 1-line subhead (max 3 lines combined) above 8-12 cell bento grid covering 60%+ of viewport
**Best for vibes:** Minimal, Glass-tech, Industrial
**Best for macrostructures:** Bento Grid

### A7. No hero, full-bleed grid
**Use when:** macrostructure = Bento Grid OR Workbench, page opens directly to content
**Layout:** Nav bar → full-bleed bento grid OR full-bleed app shell. No traditional hero.
**Best for vibes:** Brutalist, Glass-tech, Industrial
**Best for macrostructures:** Bento Grid, Workbench

### A8. Editorial spread
**Use when:** macrostructure = Long Document, content is narrative
**Layout:** 2-column magazine spread (lead text + opener image side-by-side), generous py-32 padding
**Best for vibes:** Editorial, Hand-crafted
**Best for macrostructures:** Long Document

### A9. Number + headline
**Use when:** macrostructure = Long Document with ordinal sections
**Layout:** Massive number (00, 01 etc) left + headline right, asymmetric 30/70 split
**Best for vibes:** Editorial, Art-deco, Industrial
**Best for macrostructures:** Long Document

### A10. Massive typography only
**Use when:** macrostructure = Manifesto, declarative single statement
**Layout:** Single H1 sized `clamp(4rem, 12vw, 12rem)`, no image, no CTA, full viewport height
**Best for vibes:** Brutalist, Minimal, Art-deco
**Best for macrostructures:** Manifesto

### A11. Statement + signature
**Use when:** macrostructure = Manifesto OR Letter, voice is personal
**Layout:** Quote/statement large + signature line below (italic, smaller)
**Best for vibes:** Editorial, Hand-crafted, Luxury
**Best for macrostructures:** Manifesto, Letter

### A12. Number-led headline
**Use when:** macrostructure = Stat-Led, primary message is numerical
**Layout:** Headline number `clamp(5rem, 14vw, 15rem)` + supporting headline beneath
**Best for vibes:** Industrial, Glass-tech, Retro-futuristic
**Best for macrostructures:** Stat-Led

### A13. Proof bar above hero
**Use when:** macrostructure = Stat-Led, social proof is hero-eligible
**Layout:** Logo row (5-7 logos) at top → standard hero below
**Best for vibes:** Glass-tech, Minimal, Editorial
**Best for macrostructures:** Stat-Led
```

(Optional A14-A16 — Workbench compact toolbar, Letter correspondence opener, Letter handwritten note — can be added later or in this phase based on time. Prioritize A5-A13 first.)

## Related code files

**Create:**
- `references/macrostructure-catalog.md` (~200 lines)

**Modify:**
- `assets/nextjs-skeleton/section-archetypes.md` (+ A5-A13, ~+50 lines; A14-A16 stretch goal)

## Implementation steps

1. **Write `references/macrostructure-catalog.md`** per Architecture above (~200 lines, 7 macros)
2. **Read section-archetypes.md** to locate insertion point (after A4 hero archetype, before next major section)
3. **Append A5-A13 hero archetypes** to section-archetypes.md
4. **Optional: append A14-A16** (Workbench + Letter heroes) if scope allows
5. **Verify cross-references** — macrostructure-catalog cites section-archetypes.md A-IDs; section-archetypes cites macrostructure names

## Todo list
- [ ] Write macrostructure-catalog.md with 7 macrostructures
- [ ] Add intro + when-to-pick + diversification rule sections
- [ ] Add Macrostructure × Vibe interaction section
- [ ] Add Cross-references section
- [ ] Read section-archetypes.md, find insertion point
- [ ] Append A5-A13 hero archetypes (9 minimum)
- [ ] Stretch: append A14-A16 (Workbench + Letter)
- [ ] Verify cross-references between 2 files

## Success criteria
- macrostructure-catalog.md exists, ~200 lines, 7 macros fully spec'd
- 7 sections each have: hero archetypes + section rhythm + best-for + dial defaults + diversification axes + AI tells to avoid
- Bento Grid has Gapless mandate documented
- Stat-Led has Honest copy enforcement note
- Long Document has meta-label ban exception note
- Diversification rule section explains hard + soft rules
- section-archetypes.md has A5-A13 (9 new) + optionally A14-A16
- Cross-references resolve

## Risk assessment
- **Risk:** ~200 lines spread across 7 macros = ~28 lines each, may be too compressed → use compact bullets, link to dependencies
- **Risk:** Hero archetype A IDs conflict with existing A1-A4 → verified safe (A1-A4 untouched, A5-A13 new)
- **Risk:** Macrostructure × Vibe table could be 7×11 = 77 cells → only list 3 illustrative combinations; full matrix implied
- **Risk:** Workbench macrostructure only for generic tier — confusion for landing users → explicit note in Workbench section

## Security considerations
None.

## Next steps
- Phase 04 workflow-brainstorm.md references this catalog (Step 2c macrostructure pick)
- Phase 04 workflow-audit.md references gapless bento + meta-label exception
- Phase 05 SKILL.md References table adds macrostructure-catalog.md
- Phase 06 README documents the macrostructure layer concept
