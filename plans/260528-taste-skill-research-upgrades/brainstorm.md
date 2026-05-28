# Taste-skill research + upgrade roadmap

**Date:** 2026-05-28
**Status:** Brainstorm complete, awaiting first per-version plan
**Skill version impact:** v2.2.0 → v2.3.0 → v2.4.0 → v2.5.0 (sequential 3-release roadmap)

---

## Research context

User asked: "tham khảo các skill của repo tasteskill.dev (đã add vào ~/.claude/skills/) — xem có thể học gì để upgrade perfect-ui."

### Skills reviewed (4 of 15+ taste-related installed locally)

| Skill | Reviewed | Why this one |
|-------|----------|--------------|
| `design-taste-frontend` | SKILL.md (227 lines) | Main "taste-skill" — direct competitor to perfect-ui |
| `hallmark` v1.0.0 | SKILL.md (553 lines) | Most sophisticated anti-AI-slop framework; closest peer |
| `high-end-visual-design` | SKILL.md (99 lines) | Premium agency-tier patterns |
| `redesign-existing-projects` | SKILL.md (179 lines) | Audit + redesign-only competitor |

### Skills NOT deep-scanned (defer if needed)
- `gpt-taste` — GPT-optimized variant of design-taste-frontend
- `image-to-code` — design-reference-first approach
- `imagegen-frontend-web` / `imagegen-frontend-mobile` — image gen specifically
- `industrial-brutalist-ui` / `minimalist-ui` — specific vibe skills
- `motion-design` — overlap with motion-patterns.md
- `stitch` / `stitch-design-taste` — Stitch export
- `brandkit` — brand identity (perfect-ui already supports via icons phase)
- `web-design-guidelines` — likely overlapping universal rules
- `hallmark/references/*` + `hallmark/docs/*` — full deeper Hallmark spec

## Key findings — 9 upgrade opportunities

### Tier 1 — Quick wins (chosen)

#### A. Strategic Omissions checklist
**Source:** `redesign-existing-projects` § Strategic Omissions (What AI Typically Forgets)
**Gap in perfect-ui:** anti-slop-rules + anatomies don't enforce these
**Pattern:** Add to landing/portfolio/generic anatomy checklists:
- Legal links in footer (privacy/terms)
- "Back" navigation paths
- Custom 404 page consideration
- Form validation (when forms present)
- Skip-to-content a11y link
- Cookie consent (when jurisdiction requires)
**Estimated impact:** ~50-80 lines across 3 anatomy files + anti-slop-rules.md tag matrix update

#### B. Honest copy mandate
**Source:** `hallmark` § Disciplines that hold across every verb #2
**Gap in perfect-ui:** anti-slop says "no fake stats" but no positive guidance
**Pattern:** Explicit rule "if user did not supply a metric, do NOT invent one. Use `—` plus labelled grey block (`metric to confirm`) OR pick a different macrostructure. Same rule for testimonials, logos, case-study counts."
**Estimated impact:** ~20-30 lines in anti-slop-rules.md + workflow-phases.md Phase 7 constraints

#### C. Pre-flight scan for new mode (not just redesign)
**Source:** `hallmark` § Pre-flight scan (Step 0)
**Gap in perfect-ui:** redesign-audit-checklist.md does this but only for redesign mode. New mode in existing repo silently assumes greenfield.
**Pattern:** Before Phase 2, scan for `package.json` font stack, existing CSS custom properties, motion library presence, framework. Output a pre-flight findings block. Preserve found tokens; introduce only what's missing.
**Estimated impact:** ~40-60 lines new section in workflow-phases.md § Phase 0 + new optional `references/preflight-scan.md`

### Tier 2 — Strategic structural upgrades (chosen)

#### D. Project memory + Diversification rule
**Source:** `hallmark` § Project memory (`.hallmark/log.json`) + diversification rule
**Gap in perfect-ui:** No mechanism to prevent repetition across runs in same project
**Pattern:** Write `.perfect-ui/log.json` after every build (tracks vibe + macrostructure + asset style + brief summary). Read it at Phase 0.5. Force diversification rule: next build must differ from last on ≥1 axis (vibe-anchor change OR macrostructure change OR illustration-style change). 20-entry rolling log.
**Estimated impact:** ~80 lines workflow-phases.md + new section in landing/portfolio/generic anatomy

#### E. Macrostructure layer (separate from vibe)
**Source:** `hallmark` § Step 2 Pick macrostructure (21 named macrostructures)
**Gap in perfect-ui:** section-archetypes.md ties archetypes to vibe directly (Editorial = A1 60/40 + F1 zig-zag). Same vibe always gets same skeleton.
**Pattern:** Introduce 5-7 named **page-shape macrostructures** independent of vibe:
- Marquee Hero (giant declarative headline + minimal supporting)
- Bento Grid (tile-based feature display)
- Long Document (editorial flow, narrative)
- Manifesto (statement-driven, type-first)
- Stat-Led (numerical hero + proof bars)
- Workbench (tools/utility surfaces — landing variant only)
- Letter (correspondence/conversational tone)

Then matrix: 11 vibes × 7 macrostructures = 77 combinations (vs. current 11 vibes × ~4 archetypes = 44 fixed pairs). Same vibe can have different macrostructures across runs (drives diversification).
**Estimated impact:** ~200 lines new `references/macrostructure-catalog.md` + integration in Phase 2 + section-archetypes.md update + Phase 6 plan template

#### F. DESIGN_VARIANCE + VISUAL_DENSITY dials
**Source:** `design-taste-frontend` § Active Baseline Configuration
**Gap in perfect-ui:** Only motion intensity (0-3/3); no explicit knobs for layout asymmetry or chrome density
**Pattern:** Phase 2 adds 2 dials (0-10 scale, vibe-recommended default):
- **DESIGN_VARIANCE** (1=Perfect Symmetry, 10=Artsy Chaos) — drives layout asymmetry. Above 4 → forbids centered hero unless minimal vibe (already in perfect-ui, now formalized as dial)
- **VISUAL_DENSITY** (1=Art Gallery/Airy, 10=Pilot Cockpit/Packed) — drives spacing, card usage, font scale
**Estimated impact:** ~40-60 lines Phase 2 + per-vibe default matrix in visual-direction-guide.md

### Tier 3 — Bigger new behaviors (chosen — defer to v2.5)

#### G. Study verb / DNA extraction mode
**Source:** `hallmark study` verb
**Gap in perfect-ui:** Only `--new` and `--redesign` modes; no mode for "use this reference as DNA inspiration"
**Pattern:** New mode `--study <URL or screenshot>` extracts macrostructure + accent OKLCH + type-pair + nav archetype from reference, generates **diagnosis report** (not pixel copy), then offers to build user's content using extracted DNA.
**Estimated impact:** ~150 lines new workflow phase + new mode arg + URL safety check + screenshot fallback

#### H. Component-scope branch
**Source:** `hallmark` § When the brief is a component, not a page
**Gap in perfect-ui:** Assumes full page output; one-off component brief gets unnecessary page-level apparatus
**Pattern:** Detect component-scope signals at Phase 0.5 (≤30 word brief naming single UI element). Skip macrostructure/nav/footer/enrichment. Emit 2 files: component + 8-state demo wrapper (default/hover/focus/active/disabled/loading/error/success).
**Estimated impact:** ~100 lines new branch in Phase 0.5 + new `references/component-scope.md`

#### I. Pre-emit 6-axis self-critique
**Source:** `hallmark` § Pre-emit self-critique (Philosophy/Hierarchy/Execution/Specificity/Restraint/Variety)
**Gap in perfect-ui:** Phase 8 audit is checklist-based; no model-driven quality score
**Pattern:** Before emitting Phase 7 output, model scores 1-5 on 6 axes. Anything < 3 triggers revision pass. Stamp `/* perfect-ui pre-emit critique: P5 H4 E5 S4 R5 V5 */` in CSS comment.
**Estimated impact:** ~30 lines Phase 7-8 + new `references/preemit-critique.md`

## Findings NOT adopted (rejected or out of scope)

| Item | Source | Why rejected |
|------|--------|--------------|
| 22 named themes (catalog) | Hallmark | Perfect-ui already has 11 vibes — adding 11 more = bloat without proportional value |
| 65+ slop-test gates | Hallmark | Perfect-ui's Tier 1/2/3 (~45 rules) covers same ground at lower complexity |
| 4 genre files (eager-load) | Hallmark | Adds complexity; perfect-ui's vibe anchor already does this |
| Studied-DNA branch in theme route | Hallmark | Same as Tier 3 G (study verb) |
| `hallmark audit` separate verb | Hallmark | Perfect-ui's Phase 8 inline audit covers this |
| Lock-the-system / portable design.md | Hallmark | Perfect-ui's plans/ folder already persists design decisions |
| Multi-format exports (DTCG, shadcn vars, Tailwind v4 @theme) | Hallmark | Tailwind tokens enough for current scope; add only when users ask |
| RSC safety / interactivity isolation rules | design-taste-frontend | Implicit in landing-skeleton.md / generic-page-skeleton.md |
| Bento 2.0 5-card archetypes | design-taste-frontend | App-surface specific; perfect-ui's generic tier already handles |
| Double-Bezel / Button-in-Button patterns | high-end-visual-design | Specific component recipes — out of scope (perfect-ui is system-level, not component-level) |
| Fix Priority ordering | redesign-existing-projects | Perfect-ui's Phase 6 plan already orders sections by dependency |

## Phasing strategy (user-confirmed: sequential)

### v2.3.0 — Quick wins (Tier 1: A+B+C)
**Theme:** "Completeness — fewer AI omissions"
**Scope:** ~110-170 lines across 4-5 files
**Files modified:**
- `references/anti-slop-rules.md` — § Strategic Omissions + § Honest Copy
- `references/landing-anatomy.md` — Strategic Omissions checklist
- `references/portfolio-anatomy.md` — Strategic Omissions checklist
- `references/generic-page-anatomy.md` — Strategic Omissions checklist
- `references/workflow-phases.md` § Phase 0 — pre-flight scan for new mode
- NEW `references/preflight-scan.md` (~50 lines)
- `SKILL.md` — version + Hard Rules update mention honest copy
- `README.md` — v2.3.0 update paragraph
- `index.html` — Mandates section update
**Estimated effort:** 1 brainstorm + 1 plan + 1 cook cycle, 3-4 phase files

### v2.4.0 — Structural innovation (Tier 2: D+E+F)
**Theme:** "Diversification — same skill, different output each run"
**Scope:** ~320 lines + 1 new reference file
**Files modified:**
- NEW `references/macrostructure-catalog.md` (~200 lines, 7 named macrostructures × 11 vibes matrix)
- `references/workflow-phases.md` § Phase 0.5 (read .perfect-ui/log.json), § Phase 2 (DESIGN_VARIANCE + VISUAL_DENSITY dials + macrostructure pick), § Phase 6 (carry macrostructure into plan template)
- `references/visual-direction-guide.md` — add per-vibe DESIGN_VARIANCE + VISUAL_DENSITY defaults
- `assets/nextjs-skeleton/section-archetypes.md` — update to be macrostructure-aware
- `SKILL.md` — version + new Hard Rule for diversification + Phase 2 update
- `README.md` — v2.4.0 update + new FAQ entries
- `index.html` — Pipeline cards + new Mandate "Don't repeat yourself across runs"
**Estimated effort:** 1 brainstorm + 1 plan + 1 cook cycle, 4-5 phase files

### v2.5.0 — New modes (Tier 3: G+H+I)
**Theme:** "Beyond new/redesign — study, component, self-critique"
**Scope:** ~280 lines + 2 new reference files
**Files modified:**
- NEW `references/study-mode.md` (~150 lines)
- NEW `references/component-scope.md` (~100 lines)
- NEW `references/preemit-critique.md` (~30 lines)
- `references/workflow-phases.md` § Phase 0 (add `--study` mode detection), § Phase 0.5 (component-scope branch), § Phase 7-8 (pre-emit critique stamp)
- `SKILL.md` — version + 3 new mode docs + Hard Rule update for component-scope
- `README.md` — v2.5.0 update + 3 new examples (study, component, critique)
- `index.html` — Pipeline cards + new Examples tab
**Estimated effort:** 1 brainstorm + 1 plan + 1 cook cycle, 4-5 phase files

## Cross-version concerns

- **workflow-phases.md size:** currently 804 lines. After all 3 versions: estimated 1100-1200 lines. **If exceeds 1200 hard limit:** split into sub-references (`workflow-brainstorm.md`, `workflow-plan.md`, etc.). Surface this as a question in v2.4 or v2.5 brainstorm if needed.
- **Backward compatibility:** All 3 versions must preserve existing landing/portfolio/generic workflows. Pure additive changes (new dials default to vibe matrix values; new mode is opt-in; component-scope detection is conservative).
- **plans/ folder grows:** 3 new plan folders (260528-v2.3, 260528-v2.4, 260528-v2.5 — or whenever each is started). Aligns with skill's growing maturity.

## Success criteria (cross-version)

1. perfect-ui scope preserved (landing + portfolio + generic, no scope creep into competing skill domains)
2. KISS character preserved (no eager-load of 4-5 reference files per build like Hallmark)
3. Each version backward compat (landing/portfolio examples from v2.2.0 work identically)
4. Each version has its own brainstorm + plan + execution
5. Final state: perfect-ui v2.5.0 has 9 distinct improvements borrowed from research, all integrated coherently

## Risks

| Risk | Mitigation |
|------|------------|
| Scope creep — temptation to add 10th, 11th upgrade mid-stream | Lock the 9-item list in this brainstorm; new ideas → defer to v2.6+ |
| workflow-phases.md exceeds 1200 lines | Split into sub-references when triggered (probably in v2.4) |
| Loss of perfect-ui's evidence-based positioning | Each new feature reference base evidence (synthesis.md if applicable) or label as "borrowed from taste-skill ecosystem" with attribution |
| Cross-version drift (v2.3 ships → user uses it → v2.4 changes behavior) | Each version's plan documents explicit migration path / behavioral diff |
| User loses confidence mid-roadmap (e.g., after v2.3 decides v2.4/v2.5 not worth it) | OK — each version is shippable in isolation; v2.3 alone improves skill. Sequential ≠ committed to finish all 3. |

## Out of scope (defer or never)

- Adopting Hallmark's full theme catalog (22 themes) — bloat without proportional value
- Adopting full slop-test gate count (65+) — perfect-ui's Tier 1/2/3 is sufficient
- Multi-format token exports (DTCG, Tailwind v4 @theme, shadcn vars) — add only on user request
- Genre-scoped reference files (eager load 1 per build) — perfect-ui's vibe anchor does this implicitly
- Project memory diversification at vibe-only level (perfect-ui still allows same vibe across runs IF macrostructure differs — see E)
- Building competing skill ecosystem — perfect-ui stays focused on landing/portfolio/generic page surfaces

## Next steps

1. User approve this roadmap (or scope-down to subset)
2. Start v2.3.0 cycle: `/ck:brainstorm` for v2.3 specifics → `/ck:plan` → `/ck:cook`
3. User reviews v2.3.0 output, decides whether to proceed with v2.4.0
4. Repeat for v2.5.0 if appetite remains

## Unresolved questions (resolve in per-version brainstorms)

1. **v2.3 specifics:** Strategic Omissions are conditional (e.g., cookie consent only EU sites) — how to express conditionality in checklist?
2. **v2.4 specifics:** Macrostructure naming convention — adopt Hallmark's vocabulary (Marquee Hero, Bento Grid, Long Document, Manifesto, Stat-Led, Workbench, Letter) or invent perfect-ui-specific names?
3. **v2.4 specifics:** Per-vibe DESIGN_VARIANCE + VISUAL_DENSITY defaults — derive from existing 11 vibes or fresh recommendations?
4. **v2.5 specifics:** Study mode for URL — fetch via WebFetch (existing tool) or assume user pastes HTML/screenshot manually?
5. **v2.5 specifics:** Component-scope output — 8-state demo wrapper format (HTML / React / Vue / Svelte)?
6. **Cross-version:** Should we attribute borrowed concepts in references files ("Pattern borrowed from Hallmark v1.0.0 — see https://...")? Cleaner OR more honest about sourcing?

---

## Addendum: Deep-scan batch 2 — 11 skills total (added 2026-05-28)

After Tier 1/2/3 roadmap was drafted, user requested deep-scan of remaining 7 skills before commitment. Findings below.

### Skills scanned in batch 2 (7 added; 11 total)

| Skill | New patterns |
|-------|--------------|
| `web-design-guidelines` | None — delegation skill fetching Vercel Labs guidelines |
| `motion-design` (LottieFiles) | 3 Pillars framework · 3 Motion Layers · 4 Motion Personalities · Brand Motion Identity · 8-step checklist |
| `image-to-code` | 9-dial baseline configuration · Image-first workflow mandate |
| `imagegen-frontend-web` | 1-image-per-section rule · 10 hero compositions catalog · 8-dial baseline |
| `imagegen-frontend-mobile` | Mobile-specific (out of perfect-ui scope) |
| `gpt-taste` (GPT variant) | Python-driven RNG · AIDA mandate · Hero 2-line iron rule · Gapless bento grid · Meta-label ban · Mandatory `<design_plan>` block |
| `stitch` | API wrapper — no patterns |
| `stitch-design-taste` | Atmosphere descriptive spectrum · Inline image typography hero · Hero filler-text ban · `<kbd>` keystroke styling |
| `brandkit` | Brand identity image gen (out of scope — perfect-ui generates code not brand decks) |
| `industrial-brutalist-ui` | Deeper brutalist vibe specifics (already in visual-direction-guide.md) |
| `minimalist-ui` | Deeper minimalist vibe specifics (already in visual-direction-guide.md) |

### New upgrade candidates (J-W)

**Adopt into v2.3 (Tier 1 quick wins):**
- **N. Hero 2-line iron rule** (gpt-taste) — H1 max 2-3 lines; force ultra-wide containers + smaller fonts. ~10 lines edit
- **S. Meta-label ban** (gpt-taste) — Ban "SECTION 01" / "QUESTION 05" / "ABOUT US" labels. ~5 lines anti-slop matrix
- **V. Hero filler-text ban** (stitch-design-taste) — Ban "Scroll to explore" / scroll arrows / bouncing chevrons in hero. ~5 lines anti-slop matrix

**Adopt into v2.4 (Tier 2 structural):**
- **K. 4 Motion Personalities + Brand Motion Identity** (motion-design) — Playful/Premium/Corporate/Energetic. Brand Motion Identity locks 3 constants (signature easing, duration palette, entrance pattern). ~40 lines motion-patterns.md. Complements existing motion intensity scale.
- **T. Atmosphere descriptive spectrum** (stitch-design-taste) — Augment F (DESIGN_VARIANCE + VISUAL_DENSITY) with descriptive labels ("Art Gallery Airy" 1-3 / "Daily App Balanced" 4-7 / "Cockpit Dense" 8-10). ~15 lines in dial definition.
- **O. Hero composition catalog (10 alternatives)** (imagegen-frontend-web) — Beyond left-text/right-image: centered over bg, bottom-left, bottom-right, top-left lead, stacked center, image-as-canvas, off-grid editorial, mini minimalist, right-text/left-image. ~30 lines section-archetypes.md.
- **R. Gapless Bento Grid mandate** (gpt-taste) — `grid-flow-dense` required + mathematical verification of col/row span interlock. ~10 lines in E (macrostructure-catalog.md, when Bento Grid macrostructure picked).

**Adopt into v2.5 (Tier 3 new modes) — REPLACE Tier 3 I with stronger pattern:**
- **Q. Structured `<design_plan>` block** (gpt-taste) — REPLACES or augments **I. Pre-emit 6-axis self-critique**. Q is more concrete: structured pre-flight block containing (1) randomization roll (Hero Layout / Component Arsenal / GSAP / Fonts), (2) AIDA check, (3) Hero math verification (max-w class chosen to guarantee 2-3 line flow), (4) Bento density verification (col/row math), (5) Label sweep + button contrast check. ~40 lines Phase 7-8 + new `references/preemit-design-plan.md`.

**Skip (overlap or out of scope):**
- J. Motion 3 Pillars (motion-design) — motion-patterns.md already structured; adding philosophical layer = bloat
- M. AIDA mandate (gpt-taste) — landing-anatomy.md already implies via section list; explicit mandate is duplicative
- L. Extra dials (ART_DIRECTION, IMAGE_USAGE_PRIORITY, etc.) — keep F's 2 dials only (KISS); descriptive spectrum (T) adds value without adding dial count
- P. Image-first workflow mode (image-to-code) — substantially overlaps G (study verb); same conceptual category
- U. Inline image typography hero (stitch-design-taste) — too niche; might fit O hero composition catalog as 1 of 10
- W. `<kbd>` keystroke styling — out of landing/portfolio scope; could be in generic-page-anatomy if user requests

### Roadmap update (total: 16 items distributed across 3 versions)

**v2.3.0 — Tier 1 → 6 items** (was 3, add N+S+V):
- A. Strategic Omissions · B. Honest copy mandate · C. Pre-flight scan
- + N. Hero 2-line iron rule · S. Meta-label ban · V. Hero filler-text ban
- **Total v2.3 effort:** ~150-200 lines (vs original ~110-170)

**v2.4.0 — Tier 2 → 7 items** (was 3, add K+T+O+R):
- D. Project memory · E. Macrostructure layer · F. DESIGN_VARIANCE + VISUAL_DENSITY dials
- + K. 4 Motion Personalities · T. Atmosphere spectrum · O. Hero composition catalog · R. Gapless bento mandate
- **Total v2.4 effort:** ~400-450 lines + 1 new file (vs original ~320)

**v2.5.0 — Tier 3 → 3 items** (replace I with Q):
- G. Study verb · H. Component-scope branch · ~~I. Pre-emit 6-axis critique~~ → **Q. Structured `<design_plan>` block**
- **Total v2.5 effort:** ~300 lines + 2-3 new files (similar to original ~280)

### Cross-version concerns updated

- **workflow-phases.md size:** With Tier 1 (~+100 lines) + Tier 2 (~+200) + Tier 3 (~+250) = ~+550 lines on top of 804 = ~1350 lines. **Exceeds 1200 hard limit** → must split into sub-references (`workflow-brainstorm.md` ~150 lines, `workflow-plan.md` ~150 lines, `workflow-implement.md` ~100 lines, `workflow-audit.md` ~150 lines, leave Phase 0/0.5/2/3/4/5 in main file). Surface in v2.4 brainstorm.
- **References file count:** Currently 12 files in `references/`. After all 3 versions: +5 new files (preflight-scan.md, macrostructure-catalog.md, study-mode.md, component-scope.md, preemit-design-plan.md). Total = 17. Still manageable.

### Brutal honesty addendum

- 16 items across 3 versions is **large** — perfect-ui will grow from v2.2.0 (~800 line workflow + 13 ref files) to v2.5.0 (~1350 workflow split into 4-5 files + 17 ref files). That's roughly Hallmark-sized.
- Risk: blanket-adopting 16 items = loss of KISS character. Hallmark has 65+ slop gates and 4 genre files; perfect-ui v2.5.0 would approach that complexity.
- Mitigation: each version is shippable independently; user can early-exit after v2.3 if value insufficient. Sequential rollout = early validation.
- Alternative path if user finds 16 too much: **scope down to v2.3 only** (6 items, smallest commitment). Or **scope down to v2.3+v2.4** (13 items, defer Tier 3 indefinitely).

### Decision pending (resolve before locking final roadmap)

1. **Adopt all 16 items as above** (full deep-scan harvest)?
2. **Adopt selective subset** (which items to skip)?
3. **Scope down to v2.3 only** (smallest commitment, prove value first)?
4. **Keep original 9 items, skip all 7 deep-scan finds** (stick with first design)?
