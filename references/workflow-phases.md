# Workflow Phases — Detailed Walkthrough

Self-contained 8-phase pipeline. The skill conducts every phase directly — no external orchestration skills are invoked. Phases branch by `--type` and tier (special / generic). For asset generation, the skill describes the *capability* required and uses whichever tool fits (text-to-image, vision-capable analysis, vector trace, React Three Fiber, etc.).

## Phase 0 — Mode Detection

### Detection rules
```
if user supplies URL → redesign
elif user attaches screenshot/image of existing site → redesign
elif user says "redesign" / "rework" / "v2" / "iterate" → redesign
elif user supplies repo path with existing site → redesign
elif user describes content with no existing site → new
else → AskUserQuestion to disambiguate
```

### For redesign mode (extra step before Phase 0.5)
Run audit per `redesign-audit-checklist.md`. Output: `plans/{date}-{slug}/audit.md` with sections:
- **Current vibe** (one sentence)
- **Detected type** (landing | portfolio — informs Phase 0.5)
- **Keep** (3 elements that work)
- **Kill** (5 elements that don't)
- **Original conversion goal** (inferred)
- **Why redesign now** (user's stated reason)

Then proceed to Phase 0.5 with audit context attached.

---

## Phase 0.1 — Pre-flight scan (auto-detect)

See `preflight-scan.md` for full protocol. Auto-detect logic:

- If target directory has existing project files (`package.json` / `tailwind.config.*` / framework configs / `*.css` / `index.html`) → run scan, emit findings block before Phase 0.5
- If empty repo → silent, one-line note (`Pre-flight: no signals`), proceed to Phase 0.5
- Cache findings in `.perfect-ui/preflight.json` at project root; reuse unless user requests `refresh pre-flight` OR config mtimes are newer than cache

Preserved tokens / fonts / motion library are carried into Phase 2 visual direction dialog. perfect-ui only introduces what's missing. If user explicitly says `ignore existing project` / `fresh start`, skip scan and proceed.

For redesign mode (Phase 0 set `redesign`), pre-flight runs IN ADDITION to `redesign-audit-checklist.md` — preflight scans tokens, audit assesses visual design.

---

## Phase 0.5 — Type Detection (No Refusals)

Two tiers based on `--type`:
- **Special tier** — `landing` | `portfolio`. Rich anatomy + skeleton + section archetypes per vibe + full anti-slop audit.
- **Generic tier** — any other type. Generic anatomy + generic skeleton + universal anti-slop subset.

### Step 1 — Parse `--type` flag
If `--type` is passed, accept any string. No validation against an enum:
- `landing` | `portfolio` → special tier
- anything else → generic tier (carry the supplied string as type name)

### Step 2 — Auto-detect from input description (when no flag)
Match keywords (case-insensitive). First match wins:

```
landing | marketing page | sales page | hero page | funnel | conversion → landing (special)
portfolio | hire-me page | work showcase | personal site | hire me      → portfolio (special)
blog | article | post                                                    → blog (generic)
about | team | company info                                              → about (generic)
pricing | plans | tiers                                                  → pricing (generic)
contact | reach out | get in touch                                       → contact (generic)
coming soon | waitlist | early access                                    → coming-soon (generic)
404 | error page | not found                                             → error-page (generic)
legal | terms | privacy                                                  → legal (generic)
dashboard | admin panel | admin dashboard | internal tool                → dashboard (generic) ⚠ disclose
e-commerce | storefront | product catalog | online store | shop          → e-commerce (generic) ⚠ disclose
full app | SaaS app | user dashboard                                     → app (generic) ⚠ disclose
```

Other matches → use the matched keyword as type name in generic tier.

### Step 3 — AskUserQuestion fallback (when no flag and no detection)
```
Header: "Page Type"
Question: "What type of page are you designing?"
Options:
- Landing page (marketing / conversion)
- Portfolio / personal site
- Blog / article
- About / team page
- Pricing page
- Contact / coming-soon / waitlist
- Dashboard / admin
- E-commerce / store
- Other (free text → generic tier)
```

### Step 4 — Tier routing
- **Special tier** (`landing` | `portfolio`):
  - Phase 1: type-specific brief template (landing or portfolio variant below)
  - Phase 6: type-specific plan template (landing or portfolio output below)
  - Phase 7: `assets/nextjs-skeleton/landing-skeleton.md` or `portfolio-skeleton.md`
  - Phase 8: full anti-slop audit — all rules per § Applicability Matrix apply
- **Generic tier** (any other type):
  - Phase 1: generic brief template (vibe / inspirations + Page-Purpose Exercise from `generic-page-anatomy.md`)
  - Phase 6: generic plan template (sections driven by page-purpose, not template — see Phase 6 § Generic tier plan output below)
  - Phase 7: `assets/nextjs-skeleton/generic-page-skeleton.md`
  - Phase 8: filtered audit per § Applicability Matrix — `[universal]` rules + `[marketing-only]` rules only when marketing intent = true

### Step 5 — Evidence-base disclosure (generic tier, app-surface types)
When detected type ∈ {`dashboard`, `admin`, `e-commerce`, `app`} OR user-supplied free text suggests app surface, log this notice once at start of session:

> Note: skill's evidence base (12 marketing landings analyzed — see `plans/260509-ai-vs-human-analysis/synthesis.md`) does NOT cover dashboard / admin / e-commerce / app-surface patterns directly. Universal craft toolkit (vibe lock, custom icons, motion rules, anti-slop universal subset) still applies. Output quality is best-effort, not evidence-backed.

### Carry type and intent into all downstream phases
Type, tier, AND the `marketing intent` flag from generic-anatomy Page-Purpose Exercise (Q5) are carried into every subsequent phase prompt. Phase 8 uses the intent flag to decide whether `[marketing-only]` rules apply for generic-tier pages.

### No refusals
The skill does NOT refuse any `--type` value. Dashboard / admin / SaaS-app / e-commerce are accepted with the evidence-base disclosure above. When another skill is genuinely a better fit (full app architecture, full Shopify backend, exact screenshot replication), skill suggests via SKILL.md § Beyond — never force-redirects.

---

## Phase 1 — Discovery (inline brainstorm protocol)

Skill conducts brainstorm directly via `AskUserQuestion`. Output: `plans/{date}-{slug}/brief.md`.

### Step 1 — Scope sanity check
- If user request describes 3+ independent concerns (e.g. "build a landing + dashboard + admin"), flag for decomposition before continuing. Each becomes its own brief → plan → implement cycle.
- If trivial (single-section update, copy tweak, color swap), produce a 5-line brief inline and skip the approval gate.

### Step 2 — Question script (branched by type)

Use `AskUserQuestion` in this order. Lock each answer before asking next.

#### If type = landing
1. **Product** — one sentence: what + who + why now
2. **Audience** — specific role (e.g. "freelance designer earning $80k+ who codes side projects" — NOT "everyone" / "users")
3. **Conversion goal** — single CTA destination: signup / demo / buy / waitlist / contact
4. **Vibe anchor** — pick 1 of: minimal | editorial | brutalist | retro-futuristic | organic | luxury | playful | industrial | art-deco | glass-tech | hand-crafted
5. **Wildcard adjective** — 1 word the brand owns (e.g. "agrarian", "harsh", "tender")
6. **Inspirations** — 3 reference URLs (real, current)
7. **Anti-references** — 2 landings to avoid
8. **Constraints** — technical / deadline / budget

#### If type = portfolio
1. **Owner one-liner** — you + craft, plainly stated. NOT cute.
2. **Audience** — specific: hiring managers at tech cos / agency clients / freelance leads / fellow craft community
3. **Single goal** — hire me / book a call / freelance inquiry / "available from {date}"
4. **Work focus** — project types featured + count: 4 / 6 / 8 / 12
5. **Case study depth** — gallery thumbnails | 1-2 deep dives | hybrid (drives Phase 6 plan complexity)
6. **Vibe anchor** — same 11-option list as landing
7. **Wildcard adjective** — 1 word tied to your craft
8. **Inspirations** — 3 portfolio URLs you admire
9. **Anti-references** — 2 portfolio styles to avoid (e.g. "no hover-overload bento grids")
10. **Constraints**

#### If tier = generic (any other type)
1. **Page purpose** — pick ONE: inform / convert / navigate / display data / collect input / tell a story
2. **Marketing intent flag** — true / false (drives which anti-slop rules apply in Phase 8)
3. **Audience** + **primary action** (may be "none" for legal / 404)
4. **Vibe anchor** + **wildcard adjective** (same 11-option list)
5. **Inspirations** — 3 URLs (or 2 + 1 visual-style reference)
6. **Anti-references** — 2 to avoid
7. **Constraints** — technical / deadline / chrome density

### Step 3 — Write brief.md

Output `plans/{date}-{slug}/brief.md`:

```markdown
# Brief — {slug}

## Type & tier
- Type: {landing | portfolio | blog | pricing | dashboard | ...}
- Tier: {special | generic}
- Marketing intent: {true | false}  # generic tier only

## Audience
{specific role}

## Goal / primary action
{single CTA destination, or "none" for informational}

## Vibe
- Anchor: {one of 11}
- Wildcard: {adjective}

## Inspirations
1. {URL}
2. {URL}
3. {URL}

## Anti-references
1. {URL or pattern}
2. {URL or pattern}

## Constraints
{technical / deadline / budget / chrome density}

## (generic tier only) Page-Purpose Exercise
- Job: {inform / convert / navigate / display / collect / story}
- Success: {metric or qualitative}
- Primary action: {action, or "none"}
```

### Step 4 — Approval gate
User reviews `brief.md`. Skill does NOT propose colors, fonts, or copy yet. Only proceed to Phase 2 once user explicitly approves.

### Step 5 — Forbidden brief patterns (auto-refuse, ask user to refine)
- "Build a website" without audience or conversion goal → push back, ask for specifics
- Generic vibe ("modern", "clean", "professional") without anchor → push back, force pick from 11
- 3 inspirations all from the same era or aesthetic → ask for variety (at least 1 wildcard reference)
- Vibe + wildcard that obviously contradict (e.g. "minimal + maximalist") → ask user to reconcile

### Quality bar (all tiers)
Brief is approved only when:
- [ ] Audience is specific
- [ ] Goal locked (one destination, or explicitly "none" for informational)
- [ ] Vibe is exactly 1 anchor + 1 wildcard (not a list)
- [ ] 3 real inspiration URLs (or ≥2 + visual-style reference)

### Portfolio-specific extra quality checks
- [ ] Work focus is specific ("brand identity for early-stage tech" not "design")
- [ ] Case study depth chosen
- [ ] Anti-references include hover-overload / "Hi I'm passionate" if user mentioned similar issues

---

## Phase 2 — Visual Direction

### 2a. Color palette dialog
Use `AskUserQuestion` with header "Palette".

Derive 3 candidate palettes from the vibe in brief:

```
Vibe: editorial luxury → candidates:
1. Cream base (#F5F1E8) + ink (#1A1715) + dusk-rose accent (#B8635A)
2. Bone (#EDE6D6) + charcoal (#221F1B) + olive accent (#7A8A4A)
3. Off-white (#F8F6F1) + deep navy (#0E1A2B) + ochre accent (#C89A3A)
```

Show 3 candidates. User picks one. Lock it.

### 2b. Typography pair dialog
Use `AskUserQuestion` with header "Typography".

Same drill: 3 candidate display+body pairs from vibe.

```
Vibe: brutalist → candidates:
1. Display: PP Neue Machina Inktrap | Body: PP Neue Montreal
2. Display: Migra | Body: GT America Mono
3. Display: Hubot Sans | Body: Söhne
```

Validate forbidden list: refuse if user picks Inter/Roboto/Arial/Open Sans/Space Grotesk (unless they push back twice — log the override).

### 2c. Spatial language
Single `AskUserQuestion`:
- Asymmetric editorial
- Minimal grid
- Brutalist density
- Atmospheric (gradients + grain)

### 2d. Visual Effect Layer (always proposed)
Single `AskUserQuestion` with the visual-effect options from SKILL.md Phase 2d. **Note:** No 3D-model option — that decision is forbidden by Hard Rule 4.

### 2e. Motion Intensity Lock (always asked)
Single `AskUserQuestion` with header "Motion Budget":
- 0/3 — no motion (CSS hover only)
- 1/3 — minimal (CSS + light entrance)
- 2/3 — moderate (FM entrance + Lenis smooth scroll)
- 3/3 — full choreography (FM + Lenis + GSAP timelines)

Default = vibe matrix from `motion-patterns.md` § Vibe × Motion Intensity. If user picks intensity that mismatches vibe (e.g., 3/3 for minimal), flag with confirmation prompt and log override in `plans/{date}-{slug}/overrides.md`.

### Output artifact
`plans/{date}-{slug}/visual-direction.md`:
```markdown
# Visual Direction
- Vibe: {anchor} + {wildcard}
- Palette: {role: hex} × 4
- Tailwind tokens: {snippet}
- Display font: {name}, weights [...]
- Body font: {name}, weights [...]
- Spatial language: {choice}
- Motion intensity: {0/3 | 1/3 | 2/3 | 3/3} (Phase 2e)
- Motion stack: {CSS only | CSS + FM | CSS + FM + Lenis | FM + Lenis + GSAP}
- Easing: {cubic-bezier values from motion-patterns.md § Easing Library}
- 3D layer: {none | hero-scene | scroll-triggered | interactive-accent}
- Forbidden: Inter, Roboto, AI purple gradient, centered hero (unless minimal)
```

---

## Phase 3 — Custom Icon Set

See `custom-icon-pipeline.md` for full decision tree. Quick reference:

### Icon inventory worksheet
For each icon, fill: `name | section | metaphor | complexity | method`

```
nav-logo-mark      | header     | mountain peak (brand-specific) | high  | AI gen + trace
feature-speed      | features   | arc + dot (momentum)           | low   | direct SVG
feature-secure     | features   | folded paper (private)         | med   | direct SVG (avoid shield cliché)
feature-flow       | features   | ribbon path                    | med   | direct SVG
cta-arrow          | hero CTA   | thin arrow with custom angle    | low  | direct SVG
social-twitter     | footer     | hand-drawn X                   | med   | AI gen + trace
social-github      | footer     | hand-drawn cat silhouette      | med   | AI gen + trace
testimonial-quote  | testimonials | open quote mark              | low   | direct SVG
```

### Cohesion check (before generating)
All icons in the set MUST share:
1. **Stroke weight** — pick one: 1px (thin), 1.5px (default), 2px (bold)
2. **Corner radius** — sharp / rounded / mixed-by-rule
3. **Fill style** — outlined / filled / duotone (one only)
4. **Visual metaphor language** — handcrafted / geometric / organic / pixel

If a needed icon can't fit the cohesion, redesign the metaphor — don't break cohesion.

### Generation
- **Direct SVG:** Claude writes inline. Target viewBox `0 0 24 24` for system icons, `0 0 48 48` for hero glyphs.
- **AI gen + trace:** use a vector icon design pipeline (text-to-SVG, or text-to-image with high-quality palette + lighting + composition control, followed by vector tracing via Inkscape Trace Bitmap or equivalent vectorizer). Mention the trace step to user; don't auto-trace.

### Output structure (Next.js)
```
app/components/icons/
├── index.ts              (re-exports)
├── icon.tsx              (base wrapper: size, color, stroke props)
├── nav-logo-mark.tsx
├── feature-speed.tsx
├── feature-secure.tsx
└── ...
```

Each icon component:
```tsx
import { Icon, type IconProps } from './icon';
export const FeatureSpeed = (props: IconProps) => (
  <Icon {...props}>
    <path d="M..." />
  </Icon>
);
```

---

## Phase 4 — 2D Visual Assets

**2D craft is the default visual language.** Pick illustration style from `2d-illustration-catalog.md` based on locked vibe.

### Pre-step: pick illustration style from catalog
Open `references/2d-illustration-catalog.md` § Vibe → Style Mapping table. Find row matching locked vibe. Pick primary style — use secondary only if primary fails to deliver hero.

### Asset checklist
- [ ] Hero illustration / scene / static 3D render exported as PNG (1)
- [ ] Section dividers / accents (2-4)
- [ ] Background texture (1, tileable)
- [ ] Open Graph image (1, 1200×630)
- [ ] Favicon source (1, square)
- [ ] Avatars / portraits (per testimonials, owner portrait if portfolio)

### Prompt template (apply to ALL prompts)
```
Subject: {what}
Style: {pick from 2d-illustration-catalog} (e.g., "silkscreen poster", "hand-drawn ink", "static 3D render")
Vibe: {vibe-anchor} + {wildcard}
Palette: {3 colors with hex from locked direction}
Lighting: {keyword matched to style}
Composition: {asymmetric | centered | rule-of-thirds}
Negative space: {where empty}
Style refs: {2-3 artistic references from catalog row}
Forbidden: AI purple/blue gradient, neon glow, generic tech illustration,
  Microsoft-clip-art aesthetic, gradient mesh, default Octane 3D render,
  AI-generated 3D blob characters, generic AI 3D-rendered scenes
Aspect ratio: {1:1 | 16:9 | 9:16}
```

Examples in `visual-asset-prompt-library.md`. Static 3D render templates in same file § Static 3D Render → 2D Image Templates.

### Capability routing (by style)
| Style | Capability needed | Notes |
|-------|-------------------|-------|
| Silkscreen / hand-drawn / cut-paper / risograph / watercolor | Text-to-image with style control (curated style prompt library) | Best style match from a catalog of style references |
| Engraved line-art / vintage patent | Text-to-image with creative direction freedom (wild / non-deterministic mode) | Useful for atmospheric / non-photographic outputs |
| Geometric flat (SVG) | Direct SVG generation by LLM (inline code) | Preferred for production-quality vector |
| Architectural schematic | Text-to-image with technical aesthetic, or direct SVG | Crisp lines + measurement annotations |
| Static 3D render → 2D | 3D modeling tool (Blender / Spline / KeyShot) exporting PNG/WebP — OR high-quality text-to-image with palette + lighting + composition control | Output is PNG/WebP, NEVER `.glb` |
| Photographic | Real photos preferred for portfolios with real work; AI fallback uses text-to-image with photorealism + anti-stock negatives | Avoid stock-photo aesthetic |
| Synthwave gradient | Text-to-image with style control (synthwave preset) | Retro-futuristic vibe ONLY |
| OG image | Multi-platform social image composition (HTML→screenshot or text-to-image) | Manual composition fallback |

### Forbidden in this phase
- AI-generated 3D models (`.glb`/`.gltf`) — even if "for the hero"
- Stock illustrations from `unDraw` / `Storyset` libraries
- Default Octane render aesthetic outputs
- Style mixing across assets (silkscreen hero + synthwave dividers)
- Palette drift (using colors not in locked palette)

### Validation loop
After every generation:
1. View image with a vision-capable model (analyze image content)
2. Check: does it match locked palette? (extract dominant colors, compare)
3. Check: does it match the chosen catalog style? (describe style in 3 words, compare to row)
4. Check: does it match vibe adjective from brief?
5. If drift > 30%, regenerate with stronger negative prompt
6. After ≥ 3 assets generated, run cross-asset cohesion audit (do they all feel one hand?)

---

## Phase 5 — Visual Effect Layer (conditional)

Skip entirely if Phase 2d returned "none". **Scope: shaders, particles, atmospheric layers — NOT 3D models.**

### Decision matrix
| Phase 2d choice | Effect scope | Stack |
|----------------|---------|-------|
| CSS-only atmosphere | Gradient + grain overlay + subtle CSS animation | CSS only (Tier 1) |
| Shader background | Procedural noise / fluid / displacement on fullscreen plane | RTF shader (Tier 3) |
| Particle field | 5000+ shader-driven points | RTF + bufferGeometry + shader (Tier 3) |
| Scroll-driven distortion | Lenis + GSAP ScrollTrigger drives shader uniform | Lenis + GSAP + RTF shader (Tier 2-3) |
| Cursor-reactive accent | Mouse coords drive CSS conic gradient OR shader uniform | CSS preferred (Tier 1), shader fallback (Tier 3) |
| Lottie animation | After-Effects-style 2D motion | Lottie (Tier 4) |

**Tier 1 = CSS preferred. Try CSS first, only escalate to WebGL when CSS proves insufficient.**

### Pattern lookup (only if shader/particle approach chosen)
See `visual-effect-patterns.md` for inline shader/particle patterns. Common targets:
- Fragment shader noise (background atmospheric layer)
- Particle field with GPU compute (~5000+ shader-driven points)
- Scroll-driven shader uniform (Lenis + GSAP ScrollTrigger driving displacement)
- Cursor-reactive shader (mouse coords → uniform)
- Postprocessing grain (CSS noise PNG preferred; shader fallback for procedural)

### Forbidden in this phase
- AI-generated `.glb`/`.gltf` as hero subject (use Phase 4 static 3D render instead)
- `OrbitControls` enabled (signals viewer demo)
- `MeshNormalMaterial` rainbow (Three.js default)
- Heavy bundle (>100KB) for what CSS can deliver
- Effect-for-effect's-sake (decorative without narrative)

### User-provided GLB exception (rare, logged)
If user explicitly provides real-product GLB:
1. Confirm model shows real shippable product (not generic shape)
2. Log override in `plans/{date}-{slug}/overrides.md`
3. Apply standard React Three Fiber guardrails (Draco compression, `<Suspense>` fallback, `dpr={[1, 2]}` cap, lazy-load with `dynamic({ ssr: false })`)

See `visual-effect-patterns.md` for full integration guide.

---

## Phase 6 — Plan (inline plan protocol)

Skill writes plan files directly. Output: `plans/{date}-{slug}/plan.md` + `phase-XX-*.md` files.

### Step 1 — plan.md frontmatter + body schema

```markdown
---
name: {slug}
status: pending
priority: {high|medium|low}
created: {date}
target: {type} {new|redesign}
blockedBy: []
blocks: []
---

# Plan — {summary}

## Source of truth
[brief.md](./brief.md) · [visual-direction.md](./visual-direction.md)

## Context links
- Existing icons: `app/components/icons/`
- Existing assets: `public/{type}/`

## Goal
{1-3 sentence outcome statement}

## Phases
{table with #, name, file link, status, effort}

## Key dependencies
{which phases block which}

## File ownership
{table mapping file paths → owner phase}

## Success criteria (overall)
{checkbox list — measurable per phase}

## Risks
{table — risk, mitigation}
```

### Step 2 — Phase decomposition rules

Each phase = one logical concern. Tier-branched output:

**If type = landing — phases (in order):**
1. Project scaffold + Tailwind theme tokens from `visual-direction.md`
2. Font loading via `next/font` (display + body)
3. Layout primitives (`Container`, `Section`, `Grid`)
4. Hero section
5. Content sections (social-proof, features, how-it-works, testimonials, pricing?, FAQ, final-CTA, footer)
6. *{if 3D}* Visual effect layer integration
7. Animations + scroll behavior (locked Phase 2e intensity)
8. Responsive + a11y polish + tier-filtered anti-slop audit

**If type = portfolio — phases (in order):**
1. Project scaffold + Tailwind theme tokens
2. Font loading via `next/font`
3. Layout primitives
4. Hero (intro) section
5. Selected Work Grid section
6. Featured Case Study section(s) — count from brief
7. About / Bio section
8. *{if applicable}* Process / Approach section
9. Contact / Availability CTA section
10. Footer
11. *{if case studies have own pages}* Per-project page template at `app/work/[slug]/page.tsx`
12. *{if 3D}* Visual effect layer integration
13. Animations + scroll behavior
14. Responsive + a11y polish + tier-filtered anti-slop audit

**If tier = generic (any other type) — phases driven by Page-Purpose Exercise (NOT a fixed template):**
1. Project scaffold + Tailwind theme tokens
2. Font loading via `next/font`
3. Layout primitives (adjust to page chrome density)
4. Page-purpose definition (consume Phase 1 brief answers)
5. Section selection — pick from `generic-page-anatomy.md` § Section Pattern Library based on purpose. Do NOT default to a hero+features+CTA stack.
6. Implement chosen sections in dependency order
7. *{if 3D}* Visual effect layer integration
8. Animations + scroll behavior (respect locked motion intensity from Phase 2e)
9. Responsive + a11y polish
10. Tier-filtered anti-slop audit per § Applicability Matrix

Example section stacks by generic type:
- `blog` → nav + hero + article-list + footer
- `pricing` → nav + hero + pricing-tiers + FAQ + final-CTA + footer
- `about` → nav + hero + team-grid + values + contact-cta + footer
- `contact` / `coming-soon` → minimal nav + hero + form + footer
- `dashboard` → app-shell (sidebar + topbar) + filter-bar + data-grid + empty-state
- `404` → minimal banner + return-home link
- `legal` → nav + long-form-prose + footer
- custom → user / page-purpose drives

### Step 3 — Dependency analysis (per phase)

For each phase, identify:
- **Inputs:** files produced by previous phases (read-only)
- **Outputs:** files / components produced by this phase
- **Blockers:** must wait for which phases
- **Parallel candidates:** can run alongside which other phases

Default rule: Layout primitives → Sections (sections depend on primitives). Sections within the same depth are parallel-safe.

### Step 4 — File ownership contracts (parallel-safe)

For each phase, declare exact file paths owned. No other phase may write to these files. File-level granularity, not function-level.

Example:
```
| File | Owner phase | Action |
|------|-------------|--------|
| app/page.tsx | 04 (Hero) | CREATE/MODIFY |
| app/components/sections/hero.tsx | 04 | CREATE |
| app/components/sections/features.tsx | 05 | CREATE |
```

If two phases need to modify the same file, restructure tasks OR designate one phase as "shared file integrator" (which handles all modifications to that file).

### Step 5 — Per-phase success criteria + risks

Each `phase-XX-*.md` must include:
- **Explicit checkable success criteria** (measurable, not "looks good")
- **≥2 identified risks** with mitigations

### Step 6 — Hard constraints to surface in every phase

- Custom icons only (NEVER icon library imports)
- Locked palette as Tailwind tokens — no inline hex outside SVG paths
- Real draft copy — no Lorem, no AI clichés (per applicability matrix tier)
- `min-h-[100dvh]` not `h-screen`
- All fonts via `next/font` — no `<link>` CDN
- 3D components: `'use client'` + `dynamic({ ssr: false })`
- Type-specific anti-slop:
  - portfolio → no "Hi I'm passionate" opener, no skill bars
  - landing → no two equal-weight CTAs, no 3-col equal-feature-grid
  - generic + marketing intent → no AI gradient hero, no fake stats, no generic SaaS CTA labels
  - generic + no marketing intent (dashboard / 404 / legal) → `[universal]` rules only

### Step 7 — Approval gate
User reviews `plan.md` + each `phase-XX-*.md`. Iterate until approved. Only proceed to Phase 7 once approved.

### Step 8 — Forbidden plan patterns (auto-refuse, push back)
- Phase that touches >10 files = too broad; decompose
- Phase that exceeds ~200 lines of phase file detail = too large; split
- Two phases owning the same file = conflict; restructure
- Vague success criteria ("works correctly") = push back, force measurable

---

## Phase 7 — Implement (inline implement protocol)

Skill implements directly from `plan.md` + `phase-XX-*.md` files. Per CLAUDE.md: NO auto-commit — user reviews + commits manually after each phase.

### Step 1 — Phase execution order
Follow `plan.md` dependency graph. Default sequential unless plan marks phases parallel-safe. Mark each phase status `in_progress` before starting; `completed` after success criteria all check.

### Step 2 — Per-phase constraints (enforce throughout)

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

**Motion (per `visual-direction.md` § Motion Intensity, locked Phase 2e):**
- Apply motion ONLY at locked intensity (0/3 → 3/3)
- Stack escalation: CSS → Framer Motion → Lenis → GSAP (only escalate if prior tier insufficient)
- NO generic fade-up on every element (≤30% sections animate at 2/3 intensity)
- NO motion on body `<p>` text
- Use vibe-paired `cubic-bezier(...)` easing (see `motion-patterns.md` § Easing Library) — NOT `ease-in-out` / `ease-out` named keywords
- `prefers-reduced-motion` MUST be respected (Framer Motion `useReducedMotion()` or CSS `@media`)
- Mobile auto-degrades intensity by 1 step at < 768px
- Total motion JS bundle ≤ 100KB gz

### Step 3 — Mid-implementation spot-checks
After each section completes, verify:
- **Imports list** — any forbidden icon / font library?
- **Color values** — any inline hex outside theme tokens (excluding SVG paths)?
- **Copy** — any "Elevate / Seamless / Unleash / Empower / Game-changer / Next-gen"?
- **Motion** — any `ease-in-out 0.3s` default? Any motion on body `<p>`?
- **Icons** — any emoji used in place of icon?
- **3D** — any `OrbitControls` / `MeshNormalMaterial` / `useGLTF` without override log?

### Step 4 — Commit pattern (when user commits manually)
- One phase = one focused commit (not one mega-commit at end)
- Commit message: conventional commits format (`feat:` / `fix:` / `refactor:` / `docs:` / `chore:`)
- No AI-tool references in commit messages
- Stage files explicitly (no `git add .`) to avoid accidentally committing secrets / build artifacts
- Pre-commit hooks pass (lint, type-check) — never `--no-verify`

### Step 5 — Phase completion check
- Mark phase status `completed` in `phase-XX-*.md`
- Update `plan.md` phase table status
- Update `plan.md` § Success criteria checkboxes
- Notify user phase is done; await confirmation before starting next phase

---

## Phase 8 — Anti-Slop Review (Tier-Filtered)

See `anti-slop-rules.md` § Final Audit for the full machine-runnable checklist and `anti-slop-rules.md` § Applicability Matrix for the rule-to-type mapping that drives filtering.

### Audit filter logic
1. Read current session `--type` and tier (special vs generic — set in Phase 0.5)
2. Read `marketing intent` flag from Phase 1 brief (generic tier only — see `generic-page-anatomy.md` Q5)
3. Build filtered rule set:
   - Special tier (`landing` | `portfolio`) → ALL rules apply
   - Generic tier + marketing intent = true → `[universal]` + `[marketing-only]` rules apply
   - Generic tier + marketing intent = false → `[universal]` rules only
   - `[landing/portfolio-only]` rules never apply to generic tier
4. Run grep checks on filtered subset
5. Output PASS/FAIL with applicable-rule count and skipped-rule count

### Inline audit runner

Skill runs audit directly in-thread — no external agent delegation. Output: `plans/{date}-{slug}/anti-slop-report.md`.

#### Step A — Session context inputs
- `--type` (set in Phase 0.5)
- Tier (special / generic — set in Phase 0.5)
- Marketing intent flag (set in Phase 1 for generic tier; implicit `true` for special tier)

#### Step B — `[universal]` grep checks (always run)

```bash
# Emoji (Tier 1)
grep -rE '[\x{1F300}-\x{1FAFF}]' app/

# Icon libraries (Tier 1)
grep -rE 'lucide-react|@heroicons|phosphor|@tabler|react-icons|font-awesome|material-icons' app/ package.json

# Forbidden fonts alone (Tier 3, compensable if paired with distinctive display)
grep -rE 'Inter|Roboto|"Open Sans"|Space Grotesk|Poppins|Lato|Montserrat|Nunito' app/ tailwind.config.*

# DM Sans + Space Grotesk pair (Tier 1 — both present together = fail)
# Run two greps and confirm both return matches → fail

# h-screen (Tier 1)
grep -rE '\bh-screen\b' app/

# Inline hex outside tokens (universal hygiene)
grep -rE '#[0-9a-fA-F]{6}' app/components/

# Generic ease-in-out / ease-out (Tier 2 motion)
grep -rE '(ease-in-out|ease-out|"easeInOut"|"easeOut")' app/components/

# prefers-reduced-motion respect (required when motion library imported)
grep -rE 'useReducedMotion|prefers-reduced-motion' app/

# 3D model imports (Tier 1 — must be empty unless user-GLB override logged)
grep -rE 'GLTFLoader|FBXLoader|OBJLoader|useGLTF|gltfjsx|OrbitControls' app/

# Default Three.js material clichés
grep -rE 'MeshNormalMaterial' app/
```

#### Step C — `[marketing-only]` grep checks (run if tier = special OR generic+marketing-intent)

```bash
# AI clichés in load-bearing copy
grep -rEi 'elevate|seamless|unleash|empower|unlock|game.?changer|next.?gen|cutting.?edge|delve|tapestry|leverage' app/lib/content.ts app/components

# Round fake stats
grep -rE '10K\+|99\.99%|10x faster|1M\+' app/

# Generic SaaS CTA labels
grep -rE '"Get Started"|"Sign In"|"Subscribe"|"Start Free"|"Sign Up Free"' app/

# AI purple/blue gradient hero (Tier 1)
grep -rE 'from-purple-.*to-blue-|from-blue-.*to-purple-' app/

# Generic placeholders
grep -rE 'John Doe|Jane Smith|Acme Corp|Lorem ipsum' app/
```

#### Step D — `[landing/portfolio-only]` grep checks (run only if type = portfolio)

```bash
# Cliché openers (Tier 1)
grep -rEi "hi,?\s+i'?m\s+\w+|hello,?\s+world|welcome to my (portfolio|corner)|passionate (designer|developer|creative)" app/

# Skill bar / proficiency (Tier 1)
grep -rEi 'proficiency|years of experience.{0,30}\d+\+|skill.?bar' app/

# 4D framework cliché
grep -rEi 'discover.{0,5}define.{0,5}develop.{0,5}deliver' app/

# Multi-disciplinary cliché
grep -rEi 'multi.?disciplinary creative|based in [a-z ]+' app/
```

#### Step E — Visual checks (screenshot-driven, via vision-capable model)

For key sections (hero, mid-page, footer):
1. Render screenshot (browser automation or static render)
2. Send to vision-capable model with prompt:
   > Extract dominant colors. Count distinct accent values. Describe vibe in 3 words. Score vibe-match (1-10) against `{locked vibe}`. Identify any AI tells visible: purple gradient, browser-mockup, generic illustration, centered-H1 at high variance, equal-weight dual CTAs.
3. Tier-specific visual gates:
   - `landing` → hero NOT centered-H1 at variance > 4 (unless vibe = minimal)
   - `portfolio` → actual work visible above the fold (not just bio + personality)
   - `generic` + marketing intent → no AI gradient hero, no fake stats, no two-equal-weight CTAs
   - `generic` + no marketing intent (dashboard / 404 / legal) → vibe consistency + icon cohesion only

#### Step F — Performance + a11y checks

- Lighthouse mobile performance ≥ 90 (≥ 80 if 3D or data-heavy app surface)
- LCP ≤ 2.5s; CLS ≤ 0.1
- Color contrast WCAG AA pass
- Keyboard navigable (tab through interactive elements)
- All icons have `aria-hidden="true"` or `aria-label`

#### Step G — Output report

Write `plans/{date}-{slug}/anti-slop-report.md`:

```markdown
# Anti-slop audit — {slug}

## Context
- Type: {type}
- Tier: {special | generic}
- Marketing intent: {true | false}

## Filter
- Applicable rules: N
- Skipped rules: M (per § Applicability Matrix)

## Grep results
| Check | Result | Notes |
|-------|--------|-------|
| Emoji | PASS / FAIL ({count} hits) | {file:line if FAIL} |
| Icon libraries | PASS / FAIL | ... |
| ... | ... | ... |

## Visual checks
| Check | Score | Notes |
|-------|-------|-------|
| Vibe match | {1-10} | {3 words from model} |
| Distinct accents | {count} | (target: 1) |
| ... | ... | ... |

## Performance / a11y
- Lighthouse mobile: {score}
- LCP: {ms}
- CLS: {value}
- Contrast pass: {yes/no}

## Verdict
- PASS — no Tier 1 violations, ≤ 0 Tier 2 stacked with Tier 1
- FAIL — return to Phase 7 to fix {list specific items}
```

If any Tier 1 violation OR (≥1 Tier 1 + ≥2 Tier 2 stacked) → return to Phase 7 to fix. Repeat audit until clean.
