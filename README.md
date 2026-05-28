# Perfect UI

> Skill for Claude Code — designs and ships **landing pages** and **portfolios** that look human-crafted, not AI-generated.

**Skill name:** `perfect-ui` &nbsp;·&nbsp; **Version:** 2.2.0 &nbsp;·&nbsp; **License:** MIT

---

## What it does

Most LLMs default to the same SaaS slop when asked to design a website: Inter font, AI purple/blue gradient hero, three-column equal feature cards, lucide-react icons, "Elevate your workflow" copy. **Perfect UI is built specifically to avoid that.**

**v2.1.0 update:** Skill scope opens beyond landing/portfolio. `--type` now accepts any page type. Landing and portfolio keep rich anatomy + skeleton + section archetypes. All other types (blog, about, pricing, contact, coming-soon, error pages, legal, dashboard, admin, e-commerce, custom) use generic anatomy + skeleton with the same universal craft toolkit (vibe + palette + typography + custom icons + 2D illustrations + motion + anti-slop). No refusals.

**v2.2.0 update:** Workflow is now self-contained. All orchestration (brainstorm, plan, implement, audit) is inlined in `references/workflow-phases.md`. Asset generation tools are described by capability (text-to-image with style control, vision-capable analysis, vector tracing, React Three Fiber as shader runner, etc.) — no specific external skill dependencies. Skill runs in any Claude Code setup.

The skill drives a self-contained 8-phase pipeline:

1. **Detect mode** — new build vs redesign of existing site
2. **Detect type** — landing page vs portfolio vs generic (asks if unclear)
3. **Discover vibe** via inline brainstorm protocol — 1 anchor + 1 wildcard adjective
4. **Lock visual direction** — palette, typography pair, spatial language, optional Visual Effect Layer
5. **Custom icon set** — direct SVG OR AI-generated + vector trace. **Zero emoji. Zero icon libraries.**
6. **2D visual assets** — illustrations, photos, static 3D renders (exported as PNG), SVG. Style picked from 11 vibes × 11 styles catalog. **2D craft is the default visual language.**
7. **Optional Visual Effect Layer** — shaders, particles, atmospheric effects via CSS-first / React Three Fiber as shader runner. **NO 3D models as hero subjects** (rotating GLB / AI characters forbidden).
8. **Implementation** via inline plan + implement protocols on Next.js + Tailwind + shadcn

A final anti-slop audit (Tier 1/2/3 system) blocks ship if AI fingerprints stack.

## Why it exists

Direct comparison of 12 real landings (5 AI-generated + 7 human-made) showed: AI pages stack 10+ anti-slop violations because they default to ALL safe options simultaneously. Human pages commit to ONE aesthetic direction. Cohesion is the multiplier on craft. Full evidence: [`plans/260509-ai-vs-human-analysis/synthesis.md`](plans/260509-ai-vs-human-analysis/synthesis.md).

This skill encodes that finding as enforceable rules.

---

## Installation

The skill is auto-discovered when placed in your Claude Code skills directory. Once registered, it activates on relevant phrases ("design a landing page", "build my portfolio", etc.).

---

## Usage

### Trigger phrases

The skill activates on any of these (auto-detected from user message):

**Landing page:**
- "design a landing page for X"
- "build me a marketing page"
- "I need a hero section / sales page"
- "redesign this landing"

**Portfolio:**
- "design my portfolio"
- "build a portfolio for [name]"
- "personal site / hire-me page / work showcase"
- "redesign my portfolio"

**Generic (any other page type — supported via generic tier):**
- "design my pricing page"
- "build a blog landing"
- "create an about page"
- "design a contact page" / "coming-soon page" / "waitlist"
- "design a 404 / error page"
- "design a dashboard for my [tool]"
- "build an admin panel"
- "design a product catalog page" / "storefront homepage"
- Free-text page-type description (any custom string accepted as `--type`)

**Suggested (not refused) — see § Beyond perfect-ui in SKILL.md:**
- Full app architecture / complex multi-page IA → general frontend engineering workflow is a better fit
- Full e-commerce backend (cart, checkout, inventory, payment) → dedicated e-commerce platform workflow is a better fit
- Exact design replication from screenshot/Figma → vision-driven design-to-code workflow is a better fit

Skill still handles these page types if asked — it just suggests companions for the deeper architecture.

### Arguments

```
[description OR existing site URL] [--type any_page_type] [--new|--redesign] [--no-3d] [--stack nextjs|astro|vanilla]
```

| Flag | Default | Behavior |
|------|---------|----------|
| `--type` | _detects or asks_ | Any string accepted. `landing` / `portfolio` route to special tier (rich anatomy). Everything else routes to generic tier (universal craft toolkit). Common detected values: `blog`, `about`, `pricing`, `contact`, `coming-soon`, `error-page`, `legal`, `dashboard`, `admin`, `e-commerce`. If unspecified and not detected, asks via `AskUserQuestion` with 9 presets + free-text option. |
| `--new` / `--redesign` | _detects_ | Auto-detects from URL/screenshot presence. Override if needed. |
| `--no-3d` | propose | Skip Phase 5 entirely. Default is to propose 3D as optional. |
| `--stack` | `nextjs` | `nextjs` (Next.js + Tailwind + shadcn — recommended), `astro`, or `vanilla`. |

---

## Examples

### Example 1 — Landing page from scratch

**Input:**
> Design a landing page for a new specialty coffee subscription service targeting home-brewing enthusiasts in Japan. Vibe should feel editorial and warm.

**Skill flow:**
1. Phase 0 — detects `new` (no URL provided)
2. Phase 0.5 — detects `landing` from "landing page"
3. Phase 1 — inline brainstorm protocol:
   - Product: "Specialty single-origin coffee delivered weekly to home brewers"
   - Audience: "Home espresso enthusiasts age 28-45 in Tokyo / Osaka"
   - Conversion goal: signup
   - Vibe: editorial + agrarian (wildcard)
   - 3 inspirations confirmed
4. Phase 2 — visual direction:
   - Palette: cream `#F5F1E8` + ink `#1A1715` + dusk-rose accent `#B8635A`
   - Type: `Migra` (display) + `GT Sectra` (body)
   - Spatial: asymmetric editorial
   - 3D: declined (vibe doesn't fit)
5. Phase 3 — 8 custom icons designed (nav-mark, brewing-step icons via direct SVG, social marks)
6. Phase 4 — hero illustration generated via text-to-image with style control — silkscreen-style poster of folded letter releasing coffee beans
7. Phase 5 — skipped (declined)
8. Phase 6 — inline plan protocol produces phased Next.js implementation
9. Phase 7 — inline implement protocol builds it
10. Phase 8 — Tier-1/2/3 anti-slop audit passes; ships

### Example 2 — Portfolio redesign

**Input:**
> Redesign this portfolio: https://my-old-site.com — I want it to feel more elegant and let my work speak. Currently has too many flashy hover effects.

**Skill flow:**
1. Phase 0 — detects `redesign` (URL provided)
2. Audit per `redesign-audit-checklist.md`:
   - Current vibe: "Trying-too-hard maximalist"
   - Keep: portfolio cover photo quality, custom monogram
   - Kill: hover-effect overload, skill-bar percentages, "Hi I'm passionate" opener
3. Phase 0.5 — detects `portfolio` from "redesign this portfolio"
4. Phase 1 — inline brainstorm protocol runs portfolio brief variant (asks about work focus, case study depth, etc.)
5. Phase 2 — locks elegant vibe (PP Neue Montreal display, off-white palette, atmospheric spatial)
6. Phase 3 — minimal icon set (5 icons: monogram, project-arrow, contact-mark, 2 social)
7. Phase 4 — owner portrait re-generated as editorial environmental shot
8. Phase 5 — 3D proposed: interactive 3D logo accent. Approved.
9. Phase 6 — inline plan protocol outputs portfolio plan with `app/work/[slug]` case study route
10. Phase 7 — inline implement protocol implements
11. Phase 8 — audit catches "Welcome to my portfolio" copy left over from old site → fixes → ships

### Example 3 — Blog page (generic tier)

**Input:**
> Design a blog landing for a typography studio's writing. Editorial vibe, long-form serif.

**Skill flow:**
1. Phase 0 — detects `new` (no URL)
2. Phase 0.5 — detects `blog` keyword → generic tier
3. Phase 1 — inline brainstorm protocol runs generic brief (audience, content type, Page-Purpose Exercise → job=inform, marketing-intent=true)
4. Phase 2 — locks editorial vibe (PP Editorial Old + Söhne, cream + ink palette + ochre accent)
5. Phase 3 — minimal icon set (3 icons: tag-glyph, link-arrow, social)
6. Phase 4 — letter-form silkscreen hero accent
7. Phase 5 — declined (vibe doesn't need atmosphere)
8. Phase 6 — inline plan protocol outputs generic-tier plan: scaffold → tokens → nav → hero → article-list → footer (sections driven by page-purpose, not template)
9. Phase 7 — inline implement protocol builds it
10. Phase 8 — audit runs `[universal]` + `[marketing-only]` subset; no `[landing/portfolio-only]` rules triggered. Passes.

### Example 4 — Dashboard (generic tier with evidence disclosure)

**Input:**
> Design a dashboard for a self-hosted analytics tool. Brutalist vibe, dense info, dark mode.

**Skill logs (Phase 0.5 Step 5):**
> Note: skill's evidence base (12 marketing landings analyzed) does NOT cover dashboard / admin / e-commerce / app-surface patterns directly. Universal craft toolkit (vibe lock, custom icons, motion rules, anti-slop universal subset) still applies. Output quality is best-effort, not evidence-backed.

**Skill flow:**
1. Phase 0 — detects `new`
2. Phase 0.5 — detects `dashboard` keyword → generic tier (disclosure logged above)
3. Phase 1 — generic brief: data displayed, user role, primary action, Page-Purpose Exercise → job=display data, marketing-intent=false
4. Phase 2 — locks brutalist vibe (Söhne Mono + Söhne Breit, hi-contrast black + off-white + electric-yellow accent, motion intensity 1/3 CSS-only)
5. Phase 3 — 6 custom icons (data-source markers, filter glyphs, sort-direction, refresh-state)
6. Phase 4 — schematic illustration for empty-states
7. Phase 5 — skipped (data-heavy page, no atmosphere needed)
8. Phase 6 — generic plan: app-shell (sidebar + topbar) + filter-bar + data-grid + empty-state (no hero, no CTA — driven by page-purpose)
9. Phase 7 — inline implement protocol builds it
10. Phase 8 — audit runs `[universal]` rules only (marketing-intent=false). Marketing-only rules (two equal CTAs, AI gradient hero, 3-col feature grid) skipped — they don't apply. Passes.

---

## Hard Rules (Non-Negotiable)

These cannot be overridden without explicit double-confirmation + logged override.

1. **NO emoji anywhere** — not in copy, headings, or as icons. Use a custom SVG instead.
2. **NO icon libraries** — no Lucide, Heroicons, Phosphor, Tabler, Font Awesome, Material Icons, react-icons.
3. **NO AI slop defaults**:
   - No Inter / DM Sans / Space Grotesk paired alone (Inter as body OK *only* with distinctive display font)
   - No purple/blue gradient hero (`from-purple-* to-blue-*`)
   - No 3-column equal feature card row
   - No two equal-weight CTAs in hero
   - No "Elevate / Seamless / Unleash / Empower / Game-changer / Next-gen" copy in headlines
   - No "Hi, I'm X, a passionate designer who loves coffee" portfolio opener
4. **NO AI-generated 3D models as hero subject** — no rotating product GLB, no AI-generated 3D character, no GLTF showcase. **2D illustration is the default.** Static 3D renders (Blender/Spline export → PNG) are 2D images, allowed. User-provided real-product GLB allowed only with logged override.
5. **3D = effects only** — Phase 5 (Visual Effect Layer) is for shaders, particles, atmospheric layers. CSS first, WebGL only when CSS can't.
6. **Always propose Visual Effect Layer** — every site gets the proposal. User accepts or declines.
7. **Vibe before pixels** — never write code or generate assets before vibe + palette + typography are locked.
8. **Type-aware everything** — Phase 1 brief, Phase 6 plan, anatomy, and skeleton ALL branch by `--type`.

Full forbidden patterns (with Tier 1/2/3 enforcement): [`references/anti-slop-rules.md`](references/anti-slop-rules.md).

---

## Tech Stack Output

Default output for `--stack nextjs` (recommended):

- **Framework:** Next.js 14+ App Router with TypeScript
- **Styling:** Tailwind CSS with locked palette as theme tokens
- **Components:** shadcn/ui customized (no defaults)
- **Fonts:** `next/font/local` or `next/font/google` for distinctive display + body pair
- **2D illustrations:** AI-generated via text-to-image with style control or photorealism per [`references/2d-illustration-catalog.md`](references/2d-illustration-catalog.md), OR direct SVG, OR Blender/Spline static 3D render exported as PNG
- **Visual effects (if used):** CSS first, then React Three Fiber **as shader runner only** (NOT 3D model viewer), lazy-loaded with `ssr: false`
- **Motion (vibe-scaled, locked Phase 2e):** CSS → Framer Motion → Lenis → GSAP tier system. Total motion JS ≤100KB gz. Per [`references/motion-patterns.md`](references/motion-patterns.md).
- **Icons:** Custom SVG components in `app/components/icons/`

File scaffolds: [`assets/nextjs-skeleton/landing-skeleton.md`](assets/nextjs-skeleton/landing-skeleton.md) · [`assets/nextjs-skeleton/portfolio-skeleton.md`](assets/nextjs-skeleton/portfolio-skeleton.md)

---

## File Structure

```
perfect-ui/                                   (folder; skill name is "perfect-ui")
├── SKILL.md                                  Main entry — workflow + scope + rules
├── README.md                                 This file
├── references/
│   ├── workflow-phases.md                    Detailed phase walkthrough + activation prompts
│   ├── visual-direction-guide.md             11 vibe palettes, typography pairs, commitment audit
│   ├── custom-icon-pipeline.md               Decision tree: SVG-direct vs AI-gen + cohesion rules
│   ├── 2d-illustration-catalog.md            11 vibes × 11 illustration styles + cohesion rules
│   ├── visual-asset-prompt-library.md        Prompt templates per vibe + static 3D render + SVG patterns
│   ├── visual-effect-patterns.md             Shader / particle / atmospheric patterns (NO models)
│   ├── motion-patterns.md                    Motion tier system + vibe × intensity matrix + recipes
│   ├── landing-anatomy.md                    Landing sections + conversion patterns + anti-patterns
│   ├── portfolio-anatomy.md                  Portfolio sections + portfolio-specific anti-clichés
│   ├── anti-slop-rules.md                    Tier 1/2/3 forbidden patterns + grep audits
│   ├── loading-ui-patterns.md                Splash decision tree + 4 approved + 7 forbidden patterns
│   └── redesign-audit-checklist.md           Audit pipeline for redesign mode
├── assets/nextjs-skeleton/
│   ├── landing-skeleton.md                   Next.js scaffold for landing
│   ├── portfolio-skeleton.md                 Next.js scaffold for portfolio (incl. case study route)
│   └── section-archetypes.md                 ASCII layouts for landing + portfolio sections × vibes
└── plans/
    ├── 260509-perfect-ui-multitype/
    │   └── brainstorm.md                     Original design doc for multi-type expansion
    ├── 260509-ai-vs-human-analysis/
    │   ├── synthesis.md                      Evidence-based AI vs human comparison
    │   └── raw/human-pages-findings.md       Background research on human-made pages
    ├── 260510-2d-priority-no-3d-models/
    │   └── brainstorm.md                     Pivot to 2D-priority + effect-only threejs
    └── 260510-motion-rules/
        └── brainstorm.md                     Vibe-scaled motion intensity + tier system
```

---

## The 11 Vibe Anchors

Locked in Phase 1 brief (1 anchor + 1 wildcard adjective):

| Vibe | Best for |
|------|----------|
| **Minimal** | Premium SaaS, design tools, editorial software |
| **Editorial** | Coffee/food, magazine, lifestyle brands |
| **Brutalist** | Tech-rebel, dev tools, indie products |
| **Retro-futuristic** | Web3, gaming, synthwave aesthetic |
| **Organic** | Wellness, nature, natural products |
| **Luxury** | High-end goods, premium services |
| **Playful** | Consumer apps, kids' products, casual gaming |
| **Industrial** | Hardware, manufacturing, B2B serious |
| **Art-deco** | Hospitality, finance, heritage brands |
| **Glass-tech** | AI/ML products, futuristic tech |
| **Hand-crafted** | Artisan goods, illustrators, makers |

Per-vibe palettes + typography pairs in [`references/visual-direction-guide.md`](references/visual-direction-guide.md).

---

## Anti-Slop Tier System

The skill catches AI fingerprints by counting cumulative violations (Tier 1 / 2 / 3). See [`references/anti-slop-rules.md`](references/anti-slop-rules.md) § Tier System for full enforcement matrix.

| Tier | Examples | Enforcement |
|------|----------|-------------|
| **Tier 1** (auto-fail) | DM Sans + Space Grotesk pairing, AI purple gradient hero, lucide-react import, two equal CTAs in hero, `h-screen`, 3-column feature grid, Tailwind utility count >200, generic CTA labels ("Get Started" / "Sign In" / "Subscribe") | ≥1 hit = MUST FIX. ≥2 hits = block ship. |
| **Tier 2** (caution) | Generic browser-mockup hero, friendly bullet checklist, round fake stats, AI cute illustration, centered hero with centered H1 | 1 Tier-1 + 2+ Tier-2 = block ship. |
| **Tier 3** (compensable) | Inter font alone, AI cliché in body copy, Title Case headers | OK if visual cohesion ≥ 8/10 (commitment audit) |

Bypass requires explicit user override (twice) + logged reason in `plans/{date}-{slug}/overrides.md`.

---

## Loading UI Patterns

Most landings should NOT have a loading splash. AI pages skip splash because they don't think about it; human pages skip splash because **restraint is confident**.

Splash earns its place ONLY when:
- Heavy assets need >1.5s to load (3D scene, hero video, large image, GLB)
- Brand has a moment-worthy mark (Marblex giant logotype pattern)
- Portfolio needs curated narrative entrance (Isadeburgh scroll-trigger pattern)

4 approved patterns + 7 forbidden patterns: [`references/loading-ui-patterns.md`](references/loading-ui-patterns.md).

---

## FAQ

**Q: Can I use Inter font?**
A: As body text only, IF paired with a distinctive display font (Instrument Serif, PP Neue Montreal, Migra, etc.). Inter alone = AI fingerprint (Tier 3 — compensable but discouraged).

**Q: Can I use Tailwind without triggering the >200 utility-class indicator?**
A: Yes — keep utilities focused. The signal is utility-spam (Tailwind doing all design work). Use Tailwind theme tokens for colors/fonts/spacing, write custom components, not 50-utility-classes-per-element.

**Q: What if my vibe genuinely needs a centered hero?**
A: Pick `minimal` vibe — it's the only one where centered H1 at low DESIGN_VARIANCE is approved. Other vibes need asymmetric / split / full-bleed.

**Q: Can I generate icons with `lucide` and replace them later?**
A: No. "Just for now" never gets replaced. Generate custom SVG up-front per [`references/custom-icon-pipeline.md`](references/custom-icon-pipeline.md).

**Q: What if user explicitly requests a forbidden pattern?**
A: Refuse once. If they request again with reason, log override in `plans/{date}-{slug}/overrides.md` and proceed. Never silent-allow.

**Q: Is the workflow self-contained?**
A: Yes (as of v2.2.0). All brainstorm / plan / implement / audit protocols are inline in `references/workflow-phases.md`. Skill no longer depends on external orchestration skills. Asset generation (icons, illustrations, effects) is described by capability — use any text-to-image / vision / vector tool that fits the capability description. Skill runs in any Claude Code setup.

**Q: How do I add a new vibe (e.g., `dystopian`, `vaporwave`)?**
A: Add palette + typography pair to [`references/visual-direction-guide.md`](references/visual-direction-guide.md), add archetype mapping to [`assets/nextjs-skeleton/section-archetypes.md`](assets/nextjs-skeleton/section-archetypes.md), add 3D-pairing row if relevant.

**Q: Can I use this for blog sites?**
A: Yes — blog is supported via generic tier (since v2.1.0). Skill applies vibe lock + custom icons + motion + universal anti-slop. Generic anatomy lets page-purpose drive sections rather than prescribing a template. Landing and portfolio remain the only types with full rich anatomy + per-vibe section archetypes.

**Q: Does this skill work for dashboards / admin / e-commerce?**
A: Yes — generic tier accepts any type (since v2.1.0). Skill logs a notice that the evidence base (12 marketing landings analyzed) doesn't cover app-surface patterns directly; output is best-effort universal craft. Vibe lock, custom icons, motion rules, and `[universal]` anti-slop rules still apply. Phase 8 audit filters out `[marketing-only]` and `[landing/portfolio-only]` rules that don't make sense for non-marketing pages. For full e-commerce backend, a dedicated commerce platform workflow is a better fit for the backend; for deep app architecture, a general frontend engineering workflow covers app patterns — but perfect-ui isn't a refusal for the page surface in either case. See § Beyond perfect-ui in SKILL.md.

**Q: How does the anti-slop audit handle generic-tier pages (e.g. a 404 or dashboard)?**
A: Phase 8 reads `--type` and the marketing-intent flag from Page-Purpose Exercise. Rules in `references/anti-slop-rules.md` are tagged `[universal]`, `[marketing-only]`, or `[landing/portfolio-only]`. For a 404 with no marketing intent, only `[universal]` rules run (no emoji, no icon libraries, custom SVG cohesion, no h-screen, prefers-reduced-motion respect, etc.). Marketing-only rules like "no two equal-weight CTAs in hero" don't fire because a 404 has no hero. See § Applicability Matrix.

**Q: Can I add a rotating 3D product GLB to my hero?**
A: Generally NO. Direct evidence from 12 real landings showed 0/7 human-crafted pages used real-time 3D models. Use one of these instead:
1. **Static 3D render → 2D image** (recommended) — render in Blender / Spline / KeyShot, export PNG/WebP, use as `<Image>`. This is the Augen.pro pattern.
2. **2D illustration** matching vibe — see [`references/2d-illustration-catalog.md`](references/2d-illustration-catalog.md)
3. **Shader effect** for atmosphere — see [`references/visual-effect-patterns.md`](references/visual-effect-patterns.md)

**User-provided real-product GLB exception:** If you have a GLB of an actual shippable product (hardware brand showcase), allow with double-confirm + logged override.

**Q: What's the difference between "3D model" (forbidden) and "static 3D render" (allowed)?**
A: A 3D MODEL is a `.glb`/`.gltf` rendered in real-time in the browser — visitor sees Three.js running. A STATIC 3D RENDER is a 3D scene pre-rendered (in Blender / Spline / KeyShot) and exported as a 2D image (PNG/WebP) — visitor sees `<Image>`. Same visual look, very different performance + AI-fingerprint profile.

**Q: When does the Visual Effect Layer (Phase 5) earn its place?**
A: Only when:
- CSS can't deliver the atmosphere (then shader)
- Vibe is retro-futuristic / glass-tech (effects native to vibe)
- Effect serves narrative (scroll storytelling, brand moment), not decoration

Default: skip Phase 5. The strongest human-crafted landings (Paperclip, OWO, Augen) use NO visual effects.

**Q: What's the difference between "Visual Effect Layer" (Phase 5) and "Motion" (Phase 2e)?**
A: Visual Effect = WebGL shader / particle / atmospheric layer (geometry as shader canvas). Motion = DOM elements transforming (translate, opacity, scroll-linked). Effects are atmospheric; motion is choreographic. Effects use React Three Fiber as shader runner; motion uses CSS / Framer Motion / Lenis / GSAP. Different scope, different files, different concerns.

**Q: How do I add motion without it looking AI-default?**
A: Lock intensity at Phase 2e (0/3 to 3/3) per vibe. Cap fade-up to ≤30% sections at 2/3 intensity. Use vibe-paired cubic-bezier easing (NOT `ease-in-out` 0.3s). Never animate body `<p>` text. Always respect `prefers-reduced-motion`. Full rules: [`references/motion-patterns.md`](references/motion-patterns.md).

**Q: Should I add Lenis smooth scroll to every site?**
A: NO. Only at intensity ≥2/3 AND when vibe benefits (luxury, glass-tech, organic). Adding Lenis at intensity 1/3 is a 10KB bundle for nothing. Native scroll is fine for most landings. Augen.pro and Paperclip use NO smooth scroll.

**Q: When do I need GSAP if Framer Motion is already installed?**
A: Only at intensity 3/3 with timeline scrub-driven choreography across multiple elements. If you only need single-property scroll-linked transforms, FM `useScroll` + `useTransform` (Tier 2) is enough — adding GSAP adds 50KB for one effect.

**Q: How does the motion intensity affect mobile?**
A: Auto-degrades by 1 step at <768px viewport (3/3 → 2/3, 2/3 → 1/3). Plus `prefers-reduced-motion` forces 0/3 regardless of locked intensity.

**Q: Can I import `three`, `@react-three/fiber`, `@react-three/drei`?**
A: Yes — but only as **shader/effect runners**, not 3D model viewers. Single `<Canvas>` with single `<mesh>` running custom shader = OK. `<GLTFLoader>` / `useGLTF` / `OrbitControls` = NO (unless user-GLB override).

---

## Contributing / Modifying

This is a personal skill. To extend:

1. **New vibe:** add palette + typography to `visual-direction-guide.md` + illustration style row to `2d-illustration-catalog.md` + effect layer pairing to visual-direction-guide
2. **New illustration style:** add to `2d-illustration-catalog.md` § Illustration Style Catalog + cross-reference vibe table
3. **New anti-slop pattern:** classify into Tier 1/2/3 in `anti-slop-rules.md`, add grep check to Final Audit
4. **New section archetype:** add ASCII layout to `section-archetypes.md` + vibe-mapping row
5. **New skill type (e.g., blog):** see deferred decision in `plans/260509-perfect-ui-multitype/brainstorm.md`

Validate after changes: `python ~/.claude/skills/skill-creator/scripts/quick_validate.py <skill-path>`

---

## Credits

- Original brainstorm: 2026-05-09 (`plans/260509-perfect-ui-multitype/brainstorm.md`)
- AI vs human evidence research: 2026-05-09 (`plans/260509-ai-vs-human-analysis/synthesis.md`)
- Vibe palettes adapted from contemporary editorial / branding references
- Typography recommendations from current premium foundries (Pangram Pangram, Klim, Grilli, Commercial Type)

Author: dris1153

---

## Related Workflows (Suggested Companions)

perfect-ui no longer refuses any page type, but for these specific deeper-architecture cases another workflow is a better fit. Companions, not replacements — perfect-ui still owns the visible page surface in each case.

| Need | Suggested approach |
|------|--------------------|
| Full app architecture, complex client-side state, deep multi-page IA | General frontend engineering workflow (state management, routing framework, type-safe API layer) |
| Full e-commerce backend (products, cart, checkout, inventory, payment integration) | Dedicated e-commerce platform workflow with backend orchestration |
| Exact design replication from screenshot / Figma reference | Vision-driven design-to-code workflow (multimodal model + visual diff loop) |
