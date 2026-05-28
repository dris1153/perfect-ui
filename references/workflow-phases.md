# Workflow Phases — Detailed Walkthrough

Complete phase-by-phase guidance with exact prompts to feed to delegated skills. Many phases branch by `--type` (landing | portfolio).

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

## Phase 1 — Discovery (delegate to ck:brainstorm, branched per type)

### If type = landing — Activation prompt
```
Task: Run a landing-page discovery brainstorm.
Mode: {new|redesign}
Type: landing
Audit context: {paste audit.md if redesign}

Output: plans/{date}-{slug}/brief.md with these exact sections:
1. Product (one sentence: what + who + why now)
2. Audience (specific role, e.g. "freelance designer earning $80k+ who codes side projects")
3. Conversion goal (single CTA — pick ONE: signup, demo, buy, waitlist, contact)
4. Vibe shortlist:
   - Pick 1 of: minimal | editorial | brutalist | retro-futuristic | organic |
     luxury | playful | industrial | art-deco | glass-tech | hand-crafted
   - Plus 1 wildcard adjective the brand owns
5. Inspirations (3 reference URLs)
6. Anti-references (2 landings to avoid)
7. Constraints (technical, deadline, budget)

DO NOT propose specific colors, fonts, or copy yet.
End with user approval of the brief before returning.
```

### If type = portfolio — Activation prompt
```
Task: Run a portfolio discovery brainstorm.
Mode: {new|redesign}
Type: portfolio
Audit context: {paste audit.md if redesign}

Output: plans/{date}-{slug}/brief.md with these exact sections:
1. Owner one-liner (you + craft, plainly stated — NOT cute)
2. Audience (specific: hiring managers at tech cos / agency clients /
   freelance leads / fellow craft community)
3. Single goal (hire me / book a call / freelance inquiry / "available from {date}")
4. Work focus (project types featured + count: 4 / 6 / 8 / 12)
5. Case study depth (gallery thumbnails | 1-2 deep dives | hybrid)
6. Vibe shortlist:
   - Pick 1 of: minimal | editorial | brutalist | retro-futuristic | organic |
     luxury | playful | industrial | art-deco | glass-tech | hand-crafted
   - Plus 1 wildcard adjective tied to your craft
7. Inspirations (3 portfolio URLs you admire)
8. Anti-references (2 portfolio styles to avoid — e.g., "no hover-overload bento grids")
9. Constraints

DO NOT propose specific colors, fonts, or copy yet.
End with user approval of the brief before returning.
```

### Quality bar (both types)
Brief is approved only when:
- [ ] Audience is specific (not "everyone", "users")
- [ ] Single goal locked (one CTA destination)
- [ ] Vibe is one anchor + one wildcard, not a list
- [ ] 3 inspirations are real URLs

### Portfolio-specific extra checks
- [ ] Work focus is specific ("brand identity for early-stage tech" not "design")
- [ ] Case study depth chosen (drives Phase 6 plan complexity)
- [ ] Anti-references include hover-overload / "Hi I'm passionate" if applicable

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
- **AI gen + trace:** invoke `ckm:design` icon CLI or `ck:ai-multimodal` Imagen. Then trace via Inkscape Trace Bitmap (mention to user; don't auto-trace) OR feed to a vectorizer.

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

### Tool routing (by style)
| Style | Primary tool | Notes |
|-------|--------------|-------|
| Silkscreen / hand-drawn / cut-paper / risograph / watercolor | `ck:ai-artist` --mode search | Best style match from 129 curated prompts |
| Engraved line-art / vintage patent | `ck:ai-artist` --mode wild | Random artistic transformation includes "vintage patent document" |
| Geometric flat (SVG) | Direct SVG code (Claude inline) | Preferred for production-quality vector |
| Architectural schematic | `ck:ai-artist` or vector tool | Technical aesthetic |
| Static 3D render → 2D | Blender / Spline / KeyShot manually OR `ck:ai-multimodal` Imagen Ultra with strict prompt | Output is PNG/WebP, NEVER `.glb` |
| Photographic | Real photos preferred for portfolios with real work; AI fallback only with anti-stock negative prompt | `ck:ai-multimodal` Nano Banana 2 |
| Synthwave gradient | `ck:ai-artist` --mode search "synthwave" | Retro-futuristic vibe ONLY |
| OG image | `ckm:design` social-photos | Manual composition fallback |

### Forbidden in this phase
- AI-generated 3D models (`.glb`/`.gltf`) — even if "for the hero"
- Stock illustrations from `unDraw` / `Storyset` libraries
- Default Octane render aesthetic outputs
- Style mixing across assets (silkscreen hero + synthwave dividers)
- Palette drift (using colors not in locked palette)

### Validation loop
After every generation:
1. View image with `ck:ai-multimodal` analyze
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
```bash
# Shader background patterns
python3 ~/.claude/skills/threejs/scripts/search.py "fragment shader noise" -n 5

# Particle systems
python3 ~/.claude/skills/threejs/scripts/search.py "particle field gpu compute" -n 5

# Scroll-driven shader effects
python3 ~/.claude/skills/threejs/scripts/search.py "scroll shader uniform" -n 5
```

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
3. Apply standard ck:threejs guardrails (Draco compression, Suspense fallback, dpr cap)

See `visual-effect-patterns.md` for full integration guide.

---

## Phase 6 — Plan (delegate to ck:plan)

### Activation prompt
```
Task: Plan a Next.js 14+ App Router landing page implementation.
Stack: Next.js, Tailwind, shadcn/ui, React Three Fiber {if 3D}.

Inputs (read these files):
- plans/{date}-{slug}/brief.md
- plans/{date}-{slug}/visual-direction.md
- app/components/icons/ (already populated)
- public/{landing|portfolio}/ (already populated)

### If type = landing — phase output
1. Project scaffold + Tailwind theme tokens from visual-direction.md
2. Font loading via next/font (display + body)
3. Layout primitives (Container, Section, Grid)
4. Hero section
5. Each content section (social-proof, features, how-it-works, testimonials, pricing?, FAQ, final-CTA, footer)
6. {if 3D} Three.js integration phase
7. Animations + scroll behavior
8. Responsive + a11y polish

### If type = portfolio — phase output
1. Project scaffold + Tailwind theme tokens
2. Font loading via next/font
3. Layout primitives (Container, Section, Grid)
4. Hero (intro) section
5. Selected Work Grid section
6. Featured Case Study section(s) — count from brief
7. About / Bio section
8. {if applicable} Process / Approach section
9. Contact / Availability CTA section
10. Footer
11. {if case studies have own pages} Per-project page template at `app/work/[slug]/page.tsx`
12. {if 3D} Three.js integration phase
13. Animations + scroll behavior
14. Responsive + a11y polish

### If tier = generic (any other type) — phase output
Sections are driven by the Page-Purpose Exercise (`generic-page-anatomy.md` § Page-Purpose Exercise), NOT a fixed template.

1. Project scaffold + Tailwind theme tokens from visual-direction.md
2. Font loading via next/font (display + body)
3. Layout primitives (Container, Section, Grid) — adjust to page chrome density
4. Page-purpose definition (consume Phase 1 brief answers)
5. Section selection — pick from `generic-page-anatomy.md` § Section Pattern Library based on purpose. Do NOT default to a hero+features+CTA stack.
6. Implement chosen sections in dependency order (e.g. dashboard: sidebar → topbar → data-grid → filter-bar; pricing: hero → tiers → FAQ → CTA; blog: hero → article-list → footer; 404: minimal banner + return-home link)
7. {if 3D} Visual effect layer integration
8. Animations + scroll behavior (respect locked motion intensity from Phase 2e)
9. Responsive + a11y polish
10. Phase 8 anti-slop audit — filtered subset per § Applicability Matrix

Example section stacks by type:
- `blog` → nav + hero + article-list + footer
- `pricing` → nav + hero + pricing-tiers + FAQ + final-CTA + footer
- `about` → nav + hero + team-grid + values + contact-cta + footer
- `contact` / `coming-soon` → minimal nav + hero + form + footer
- `dashboard` → app-shell (sidebar + topbar) + filter-bar + data-grid + empty-state
- `404` → minimal banner + return-home link
- `legal` → nav + long-form-prose + footer
- custom → user / page-purpose drives

### Hard constraints (all tiers) — call out in plan
- Custom icons only (NEVER lucide-react / heroicons / phosphor)
- Locked palette as Tailwind tokens — no inline hex
- Real draft copy, no Lorem, no AI clichés (per applicability matrix tier)
- min-h-[100dvh] not h-screen
- Type-specific anti-slop:
  - portfolio → no "Hi I'm passionate" opener, no skill bars
  - landing → no two equal-weight CTAs, no 3-col equal-feature-grid
  - generic with marketing intent → no AI gradient hero, no fake stats
  - generic without marketing intent (e.g. dashboard, 404, legal) → universal rules only
```

User reviews plan. Iterate until approved.

---

## Phase 7 — Implement (delegate to ck:cook)

### Activation prompt
```
/ck:cook plans/{date}-{slug}/plan.md

Constraints (enforce throughout):
- Import icons from app/components/icons — never npm install icon libraries
- Use Tailwind theme tokens for all colors — no inline hex
- All fonts via next/font — no <link> CDN
- 3D components: 'use client' + dynamic import with ssr:false
- Copy is real draft, not Lorem, not AI cliché vocabulary
- Hero composition follows visual-direction.md (no centered-H1 unless minimal vibe)

Motion constraints (per visual-direction.md § Motion Intensity, locked Phase 2e):
- Apply motion ONLY at locked intensity (0/3 → 3/3)
- Stack escalation: CSS → FM → Lenis → GSAP (only escalate if prior tier insufficient)
- NO generic fade-up on every element (≤30% sections at 2/3 intensity)
- NO motion on body <p> text
- Use vibe-paired cubic-bezier easing (see motion-patterns.md § Easing Library) — NOT ease-in-out
- prefers-reduced-motion MUST be respected (FM useReducedMotion or CSS @media)
- Mobile auto-degrades intensity by 1 step at <768px
- Total motion JS bundle ≤100KB gz
```

### Mid-implementation checks (run during ck:cook)
After each section completes, spot-check:
- Imports list — any forbidden library?
- Color values — any inline hex outside theme?
- Copy — any "Elevate / Seamless / Unleash"?

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

### Run as code-reviewer agent task
```
Task: Audit {type} for AI slop violations (tier-filtered).
Type: {type}
Tier: {special | generic}
Marketing intent: {true | false}     # generic tier only
Reference: references/anti-slop-rules.md § Applicability Matrix + § Final Audit
Source: app/ directory

[universal] grep checks — always run:
- Emoji: grep -rE '[\\x{1F300}-\\x{1FAFF}]' app/
- Icon libraries: grep -rE 'lucide-react|@heroicons|phosphor|@tabler|react-icons|font-awesome' app/
- Forbidden fonts alone: grep -rE 'Inter|Roboto|"Open Sans"|Space Grotesk|Poppins|Lato|Montserrat|Nunito' app/ tailwind.config.* (allow Inter when paired with distinctive display font)
- DM Sans + Space Grotesk pair (Tier 1): both present together = fail
- h-screen: grep -rE '\\bh-screen\\b' app/
- Inline hex outside tokens: grep -rE '#[0-9a-fA-F]{6}' app/components/ (exclude SVG paths)
- Generic ease-in-out / ease-out (Tier 2 motion): grep -rE '(ease-in-out|ease-out|"easeInOut"|"easeOut")' app/components/
- prefers-reduced-motion respect: grep -rE 'useReducedMotion|prefers-reduced-motion' app/ (required when motion library imported)
- Style mixing across illustrations: visual check via screenshot

[marketing-only] grep checks — run if tier = special OR (tier = generic AND marketing intent = true):
- AI clichés: grep -rEi 'elevate|seamless|unleash|empower|unlock|game.?changer|next.?gen|cutting.?edge|delve|tapestry|leverage' app/lib/content.ts app/components
- Round fake stats: grep -rE '10K\\+|99\\.99%|10x faster|1M\\+' app/
- Generic SaaS CTA: grep -rE '"Get Started"|"Sign In"|"Subscribe"|"Start Free"|"Sign Up Free"' app/
- AI purple/blue gradient: grep -rE 'from-purple-.*to-blue-|from-blue-.*to-purple-' app/
- Generic placeholders: grep -rE 'John Doe|Jane Smith|Acme Corp|Lorem ipsum' app/

[landing/portfolio-only] grep checks — run only if type = portfolio:
- Cliché openers: grep -rEi "hi,?\\s+i'?m\\s|hello,?\\s+world|welcome to my (portfolio|corner)|passionate (designer|developer|creative)" app/
- Skill bar / proficiency: grep -rEi 'proficiency|years of experience.{0,30}\\d+\\+|skill.bar' app/
- 4D framework: grep -rEi 'discover.{0,5}define.{0,5}develop.{0,5}deliver' app/
- Multi-disciplinary cliché: grep -rEi 'multi.?disciplinary creative|based in [a-z ]+' app/

Visual checks (screenshot-driven):
- Single accent color enforced (count distinct accents in render)
- Lighthouse mobile performance ≥ 90 (≥ 80 if 3D or data-heavy app surface)
- Tier-specific:
  - landing → hero NOT centered-H1 at variance > 4 (unless minimal vibe)
  - portfolio → actual work visible above the fold (not just bio)
  - generic (marketing intent) → no AI gradient hero, no fake stats, no two-equal-weight CTAs
  - generic (no marketing intent, e.g. dashboard) → vibe consistency + icon cohesion only

Output: plans/{date}-{slug}/anti-slop-report.md with
- Applicable rules: N
- Skipped rules: M
- Per-check PASS/FAIL
```

If any FAIL, return to Phase 7 to fix. Repeat until clean.
