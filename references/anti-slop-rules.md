# Anti-Slop Rules — What to Avoid

The defaults LLMs gravitate to. Treat as forbidden unless user explicitly overrides twice (and log the override).

## Tier System (Cumulative Detection)

Tells are CUMULATIVE — a single rule break is sometimes compensable, but stacked tells = AI fingerprint. This system was derived from direct comparison of 5 AI-generated landings vs 7 human-crafted landings (see `plans/260509-ai-vs-human-analysis/synthesis.md`).

| Tier | What it is | Enforcement |
|------|-----------|-------------|
| **Tier 1** | Strong, unambiguous AI tells. Each one is a serious flag. | ≥1 tier-1 hit = MUST FIX. ≥2 tier-1 hits = AI fingerprint, refuse to ship. |
| **Tier 2** | AI compositional tendencies. Common in AI work but not exclusive. | 1 tier-1 + 2+ tier-2 = drift toward AI; MUST FIX before ship. |
| **Tier 3** | Style preferences. Compensable with strong visual craft. | OK alone IF cohesion is high (see `visual-direction-guide.md` § Commitment Audit). |

**Strict default:** treat all tiers as MUST FIX. Only allow tier-3 break with logged override + visual proof of compensation.

### Tier 1 — Strong AI tells (MUST FIX, no compensation)

1. **DM Sans + Space Grotesk Google Fonts pairing** — direct evidence: present in 3/5 AI pages, 0/7 human. Forbidden combo even though individual fonts are softer flags.
2. **AI purple/blue gradient hero** (`from-purple-500 to-blue-500`, `from-purple-100 to-purple-200`, etc.) + **gradient highlight on H1 keyword** (e.g., "Confidence" highlighted in cyan-blue gradient).
3. **Icon library imports detected** (`lucide-react`, `@heroicons`, `@phosphor-icons`, `@tabler/icons`, `react-icons`, `font-awesome`). Confirmed in 2/5 AI pages.
4. **Two equal-weight CTAs in hero** (e.g., "Start Free" + "View Demo" both as primary buttons). Confirmed 5/5 AI pages.
5. **`h-screen` utility class** present (must use `min-h-[100dvh]`).
6. **3-column equal feature card grid** — confirmed 6 hits in single AI page; 0 in human.
7. **Heavy Tailwind utility class density (>200 in initial HTML)** — snapstory: 383, exgen: 379. Human max: 64. Indicator of utility-spam without committed CSS architecture.
8. **Generic SaaS CTA labels in hero**: "Get Started", "Sign In", "Subscribe", "Start Free", "Sign Up Free" — without product-specific framing.
9. **AI-generated 3D model as hero subject**. Default Octane render aesthetic — glossy plastic shading, balanced studio lighting, generic primitive arrangement. Includes `.glb`/`.gltf` imports rendered real-time + AI-generated 3D blobs/characters/scenes. **Use static 3D render → 2D image (Augen pattern) OR shader effect OR 2D illustration instead.** Direct evidence: 0/7 human-crafted landings used real-time AI-generated 3D models.
10. **OrbitControls enabled in landing/portfolio** — signals "viewer demo" not designed page. Visitor doesn't want to "explore 3D."

### Tier 2 — AI compositional tendencies (MUST FIX in combination)

11. **Generic browser-mockup as right-half of split hero** (laptop frame with fake UI inside). Confirmed pattern in snapstory + exgen.
12. **Friendly bullet checkbox reassurance row** under hero CTA: "✓ No credit card required ✓ 7-day free trial ✓ Cancel anytime" (or similar checkmark trio).
13. **Round fake stats** in hero: "10K+ users", "2M+ downloads", "1M+ stories", "99.99% uptime", "10x faster".
14. **AI-generated cute illustration** as hero subject (cartoon animal with laptop/coffee, generic 3D blob characters, "diverse team smiling at laptop").
15. **Centered hero with centered H1** at high DESIGN_VARIANCE. Compensable only when vibe is genuinely minimal AND visual carries the page.
16. **3D model used purely as decoration** without narrative purpose (e.g., rotating cube/torusKnot in middle of viewport). Even with user-provided GLB exception, model must serve the product story, not be eye-candy.
17. **Style mixing across 2D illustrations** in same site (silkscreen poster hero + synthwave gradient mid-section). All illustrations must share style language per `2d-illustration-catalog.md` § Asset Cohesion Rules.

### Tier 3 — Style preferences (compensable with visual craft)

14. Forbidden font names appearing alone: `Inter`, `Roboto`, `Open Sans`, `Helvetica`, `Poppins`, `Lato`, `Montserrat`, `Nunito` — *without* a distinctive paired display font.
   - **Compensable:** Inter as body text IS acceptable when paired with a distinctive display font (Instrument Serif, PP Neue Montreal, Greed, etc.). Confirmed in 3/7 human pages.
15. AI cliché phrases: Elevate / Seamless / Unleash / Empower / Unlock / Game-changer / Cutting-edge / Next-gen / Delve / Tapestry / Leverage. Confirmed 5/7 human pages contain at least one — but in non-load-bearing copy positions, with strong visual craft. Refuse them in headlines and primary CTAs unconditionally.
16. Generic startup names in placeholders: Acme, Globex, Initech.
17. Title Case Headers (sentence case is more contemporary).

### How to use these tiers

- During Phase 8 audit, classify each finding as Tier 1 / 2 / 3.
- Tier 1: ALWAYS fix.
- Tier 2: count alongside tier 1. ≥1 tier-1 + 2+ tier-2 = block ship.
- Tier 3: allow IF visual craft cohesion ≥ 8/10 (see `visual-direction-guide.md` § Commitment Audit).
- Override path: user must request twice + reason logged in `plans/{date}-{slug}/overrides.md`.


## Typography

### Forbidden fonts (default reject)
- `Inter` — the AI fingerprint
- `Roboto`, `Arial`, `Open Sans`, `Helvetica` — browser defaults
- `Space Grotesk` — overused tech-startup tell
- `Poppins`, `Lato`, `Montserrat`, `Nunito` — generic SaaS

### Forbidden patterns
- Only weights 400 + 700 (use 500/600 for subtler hierarchy)
- All-caps subheaders everywhere (try sentence case, italic, small-caps)
- Title Case On Every Header (sentence case is more contemporary)
- Orphaned words on H1 (always `text-wrap: balance`)
- Serif fonts on data UIs (reserve serif for editorial)

### Approved alternatives
| Need | Pick from |
|------|-----------|
| Clean grotesk | `Söhne`, `Geist`, `GT America`, `Neue Haas Unica` |
| Display character | `Cabinet Grotesk`, `PP Neue Machina`, `Migra`, `Editorial New` |
| Editorial serif | `Lyon Text`, `Reckless Neue`, `GT Sectra`, `Tobias` |
| Monospace | `JetBrains Mono`, `Geist Mono`, `Söhne Mono`, `IBM Plex Mono` |
| Variable fonts | `Outfit`, `Plus Jakarta Sans`, `General Sans` |

## Color

### Forbidden patterns
- AI purple/blue gradient hero (`from-purple-500 to-blue-500`) — THE most common AI fingerprint
- Pure `#000000` (use `#0a0a0a` or tinted dark)
- Pure `#FFFFFF` for backgrounds (use cream / off-white)
- Saturation > 80% on accents (desaturate to ≤80%)
- Gradient text on body copy or large headers
- Mixed warm + cool grays (pick one family, stick to it)
- More than one accent color (max 1)

### Approved patterns
- Single accent, used <10% of total surface area
- Tinted shadows (dark navy shadow on navy bg, not pure black)
- Subtle noise/grain over flat colors (not sterile flat)
- Off-blacks: `#0A0A0A`, `#111111`, `#1A1715`, Zinc-950
- Off-whites: `#FAFAF7`, `#F5F1E8`, `#F8F6F1`

## Layout

### Forbidden patterns
- 3-column equal-card feature row (THE generic AI layout)
- Centered hero with centered H1 at DESIGN_VARIANCE > 4
- `h-screen` (always `min-h-[100dvh]` — iOS Safari viewport bug)
- All sections centered and symmetrical
- Equal card heights forced by flexbox (allow variable or use masonry)
- Uniform border-radius everywhere (vary by hierarchy)
- Missing max-width (always constrain to ~1200-1440px)
- Hero with two equal-weight CTA buttons

### Approved patterns
- Asymmetric grid: `grid-cols-12` with deliberate offset placement
- 60/40 split heroes for editorial
- Zig-zag 2-col features (image left → image right alternating)
- Masonry for testimonials
- Variable border-radius: tighter on inner elements (4px), softer on containers (16px)
- Single primary CTA in hero, optional ghost button as secondary

## Icons

### Forbidden
- Any `npm install` of icon library (lucide-react, @heroicons/react, @phosphor-icons, @tabler/icons-react, react-icons, font-awesome, material-icons)
- Emoji as icons (`✨`, `🚀`, `🔒`, `⚡`)
- Mixed icon styles in the same set (some outlined, some filled)
- Cliché metaphors (rocket=launch, shield=security, lightning=speed, lightbulb=idea, gear=settings)
- Library icon "just for now" — never gets replaced

### Approved
- Custom SVG components in `app/components/icons/`
- Single stroke weight, single corner family, single fill style
- Fresh metaphors tied to product (folded paper for privacy, arc-with-momentum-dot for speed)
- AI-generated + traced for ornate icons
- Direct hand-written SVG for simple geometric icons

## Visual Effects

### Forbidden
- Neon outer glows (`box-shadow: 0 0 40px ...`) — "modern" cliché
- Custom mouse cursors (hurts a11y, dated)
- Standard `ease-in-out` / `linear` transitions everywhere
- `backdrop-blur` glassmorphism without inner border + refraction shadow
- Generic motion: fade-up + 0.3s + ease-in-out on every element
- Auto-playing video heros with loud audio

### Approved
- Spring physics motion (Framer Motion `spring` config)
- Custom cubic-beziers (`cubic-bezier(0.16, 1, 0.3, 1)` for elegant out)
- Inner-border + tinted shadow combos for elevation
- Subtle noise/grain layer over flat surfaces
- Orchestrated page-load sequence > scattered micro-interactions

## Copy

### Forbidden — landing-specific
- Elevate, Seamless, Unleash, Empower, Unlock
- Game-changer, Next-gen, Cutting-edge, Revolutionary
- Delve, Tapestry, Embark, Leverage, Synergy
- Robust, Comprehensive, Holistic
- "Take your X to the next level"
- "Designed for the modern [audience]"
- "The future of [thing]"
- "Lorem ipsum"

### Forbidden — portfolio-specific
- "Hi, I'm [Name], a passionate {designer | developer | creative}..."
- "Hello, world!" greeting
- "Welcome to my corner of the internet"
- "Welcome to my portfolio"
- "Multi-disciplinary creative based in {city}"
- "Crafting beautiful digital experiences"
- "Pixel-perfect" / "pixel pusher" self-descriptors
- "I love coffee and dogs" / personality-padding bio
- "Years of experience" prominent counter
- "Available for new opportunities" with no concrete date
- "Let's create magic together" / "Let's chat"
- "Drop a line"

### Forbidden placeholder data
- Names: John Doe, Jane Smith, Sarah Chan, Acme Corp, Globex, Initech
- Round fake numbers: 99.99%, 50% off, $100.00, 10x faster, 1M+ users
- Generic role + company combos that scream stock
- Portfolio: "Project 01", "Project 02" generic project titles
- Portfolio: testimonials from "Director of Awesome at Generic Studio"

### Approved (both types)
- Real specific numbers: 47.2%, $99, 3.4x, 12,400
- Realistic diverse names tied to actual demographics
- Specific outcome statements ("cut deploy time from 14min to 2min")
- Sentence case headers ("How it works" not "How It Works")
- Confident success messages ("Saved" not "Saved!")
- Direct error messages ("Connection failed. Try again." not "Oops!")

### Portfolio-approved
- "{Name} — {specific craft for specific audience}." Example: "Sarah Chen — Brand identity for early-stage tech."
- "I design healthcare apps. 6 years, 3 platforms, 12 launches." (concrete proof)
- "Available for projects starting June 2026." (concrete date)
- "Selectively booking design partnerships through Q3."
- Specific named process phases tied to your craft (NOT Discover-Define-Develop-Deliver)

## Components

### Forbidden
- Unstyled / default shadcn components (always customize)
- Generic card (white bg + border + shadow) at high VISUAL_DENSITY
- Pill "New" / "Beta" badges everywhere
- Avatar circles exclusively (try squircles, rounded squares)
- 3-card carousel testimonials with dots
- Newsletter footer takeover

### Approved
- Customized shadcn with palette tokens, custom radii, custom shadows
- Mixed shapes: avatar squircles for human, circles for icons
- Single rotating quote testimonial OR masonry wall
- Magazine-style spread testimonials for editorial vibe

## 3D-Specific Anti-Slop

### Forbidden — 3D models (Tier 1 escalation)
- **AI-generated `.glb` / `.gltf` as hero subject** — default Octane render aesthetic, generic plastic shading
- **Rotating product GLB at center of viewport** — "viewer demo" not landing
- **AI-generated 3D characters / blobs / mascots** — generic AI fingerprint
- **`OrbitControls` enabled** in landing/portfolio context

### Forbidden — Three.js defaults
- `MeshNormalMaterial` rainbow (default Three.js render)
- Default Three.js lighting (`AmbientLight` only at 0.5)
- Stock physically-correct grass / water shaders
- Stats overlay shipped to production
- `frameloop="always"` on static scenes
- Generic "particle field with bloom" without vibe match
- "Cube/sphere/torusKnot rotates in middle of viewport" stock demo

### Approved — visual effects only
- Custom-tuned shader material that matches locked palette
- Particle fields driven by shader uniforms (not CPU loop)
- Displacement plane shader (single plane, vertex displacement)
- Refractive shader for glass-tech vibe
- No camera controls (camera is fixed; user doesn't navigate scene)
- `frameloop="demand"` for static-state shaders
- Static 3D render exported as PNG → used as `<Image>` (handled in Phase 4, NOT Phase 5)

### User-provided real-product GLB exception
Only allowed when:
- User explicitly provides a GLB file
- Model shows a real shippable product (not generic shape)
- Override logged in `plans/{date}-{slug}/overrides.md` with reason
- All standard Three.js perf guardrails apply (Draco compression, dpr cap, Suspense fallback)
- Studio HDRI from `drei` for luxury / glass-tech vibe
- `frameloop="demand"` for static / scroll-only
- Lazy-loaded with `dynamic({ ssr: false })` + poster fallback

## Final Audit Checklist

Run BEFORE declaring complete. Each must PASS or be fixed.

### Source-code checks (grep) — universal (both types)
```bash
# Emoji
grep -rE '[\x{1F300}-\x{1FAFF}]' app/  # must be empty

# Icon libraries
grep -rE 'lucide-react|@heroicons|@phosphor-icons|@tabler/icons|react-icons|font-awesome|material-icons' app/ package.json  # must be empty

# Forbidden fonts
grep -rE 'Inter|Roboto|"Open Sans"|Space Grotesk|Poppins|Montserrat|Lato|Nunito' app/ tailwind.config.* next.config.*  # must be empty (unless logged override)

# h-screen
grep -rE '\bh-screen\b' app/  # must be empty (must use min-h-[100dvh])

# Inline hex colors (should be Tailwind tokens)
grep -rE '#[0-9a-fA-F]{6}' app/components/ | grep -v 'tailwind.config' | grep -v 'globals.css'
# Should be empty or only inside SVG icon paths

# 3D model imports (Tier 1 — must be empty unless user-GLB override logged)
grep -rE 'GLTFLoader|FBXLoader|OBJLoader|useGLTF|gltfjsx' app/  # must be empty unless override
find public/ -name '*.glb' -o -name '*.gltf' 2>/dev/null  # must be empty unless override

# OrbitControls in production (Tier 1)
grep -rE 'OrbitControls' app/  # must be empty for landing/portfolio

# Default Three.js material clichés
grep -rE 'MeshNormalMaterial' app/  # must be empty
```

### Source-code checks — if type = landing
```bash
# AI cliché copy
grep -rEi 'elevate|seamless|unleash|empower|unlock|game.?changer|next.?gen|cutting.?edge|delve|tapestry|leverage' app/lib/content.ts app/components  # must be empty

# Generic placeholder data
grep -rE 'John Doe|Jane Smith|Acme Corp|99\.99|Lorem ipsum' app/  # must be empty
```

### Source-code checks — if type = portfolio
```bash
# Cliché openers
grep -rEi "hi,?\s+i'?m\s+\w+|hello,?\s+world|welcome to my (portfolio|corner)" app/  # must be empty

# Personality padding
grep -rEi 'passionate (designer|developer|creative)|multi.?disciplinary creative|pixel.?perfect|crafting beautiful' app/  # must be empty

# Skill bars / proficiency
grep -rEi 'proficiency|skill.bar|years of experience.{0,30}\d+\+' app/  # must be empty

# 4D framework cliché
grep -rEi 'discover.{0,5}define.{0,5}develop.{0,5}deliver' app/  # must be empty

# Generic project titles
grep -rE 'Project 0?[1-9]|Project Title|Untitled Project' app/  # must be empty

# Vague availability
grep -rEi 'available for new opportunities|let’?s create magic|drop a line' app/  # must be empty
```

### Visual checks (both types)
- [ ] Single accent color enforced (count distinct accent values in render)
- [ ] No AI purple/blue hero gradient
- [ ] Custom icon set is consistent (same stroke weight, corner family, fill style)
- [ ] All text wrap balanced on H1/H2 (`text-wrap: balance`)

### Visual checks — if type = landing
- [ ] Hero is NOT centered-H1-at-variance>4 (unless vibe = minimal)
- [ ] Testimonial avatars don't look like stock photos
- [ ] Two equal-weight CTAs in hero — flag (single primary CTA only)

### Visual checks — if type = portfolio
- [ ] Actual work visible above the fold (not just bio / personality)
- [ ] Project tiles are NOT iPhone-mockup-holding-the-work
- [ ] Project tiles do NOT all force same aspect ratio
- [ ] Email + concrete availability date visible in contact section
- [ ] No hover-effect overload on work grid (max 1-2 hover changes)
- [ ] Skill bars / proficiency percentages absent

### Performance checks
- [ ] Lighthouse mobile performance ≥ 90 (≥ 80 if 3D layer)
- [ ] LCP ≤ 2.5s
- [ ] CLS ≤ 0.1
- [ ] Bundle size: JS ≤ 200KB gzipped (excluding 3D), 3D ≤ 200KB additional

### Accessibility checks
- [ ] Color contrast AA passes for all text
- [ ] All icons have `aria-hidden="true"` or `aria-label`
- [ ] Keyboard navigable (tab through all interactive elements)
- [ ] No motion-only state changes (always pair with color/text)
- [ ] `prefers-reduced-motion` respected on 3D and animations

### Override Logging
If ANY forbidden pattern is intentionally used (user requested twice):
- Add to `plans/{date}-{slug}/overrides.md`
- Format: `- {Forbidden pattern} — overridden because {user's reason}`
- This documents the deliberate violation so it doesn't look like an oversight

## How to Refuse Slop in the Moment

When during implementation Claude is tempted to:
- Reach for `lucide-react` → STOP. Open `references/custom-icon-pipeline.md`. Generate the icon.
- Use Inter "because it's installed" → STOP. Pick from `references/visual-direction-guide.md` typography pairs.
- Write "Elevate your workflow" → STOP. Open `lib/content.ts`. Write what the product actually does.
- Add a purple gradient — STOP. Use the locked accent at <10% surface area.
- Skip the 3D proposal — STOP. SKILL.md mandates always proposing.

**Refusal language:** When user requests a forbidden pattern, respond:
> I'm avoiding {pattern} because it's a known AI-default that breaks vibe cohesion. The locked direction calls for {alternative from visual-direction.md}. If you want to override, confirm twice and I'll log it.
