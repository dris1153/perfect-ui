# Anti-Slop Rules — What to Avoid

The defaults LLMs gravitate to. Treat as forbidden unless user explicitly overrides twice (and log the override).

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

### Forbidden words / phrases (case-insensitive)
- Elevate, Seamless, Unleash, Empower, Unlock
- Game-changer, Next-gen, Cutting-edge, Revolutionary
- Delve, Tapestry, Embark, Leverage, Synergy
- Robust, Comprehensive, Holistic
- "Take your X to the next level"
- "Designed for the modern [audience]"
- "The future of [thing]"
- "Lorem ipsum"

### Forbidden placeholder data
- Names: John Doe, Jane Smith, Sarah Chan, Acme Corp, Globex, Initech
- Round fake numbers: 99.99%, 50% off, $100.00, 10x faster, 1M+ users
- Generic role + company combos that scream stock

### Approved
- Real specific numbers: 47.2%, $99, 3.4x, 12,400
- Realistic diverse names tied to actual demographics
- Specific outcome statements ("cut deploy time from 14min to 2min")
- Sentence case headers ("How it works" not "How It Works")
- Confident success messages ("Saved" not "Saved!")
- Direct error messages ("Connection failed. Try again." not "Oops!")

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

### Forbidden
- `MeshNormalMaterial` rainbow (default Three.js render)
- `OrbitControls` enabled by default — feels like a viewer demo
- Default Three.js lighting (`AmbientLight` only at 0.5)
- Stock physically-correct grass / water shaders
- Stats overlay shipped to production
- `frameloop="always"` on static scenes
- Generic "particle field with bloom" without vibe match

### Approved
- Custom-tuned material that matches palette
- No camera controls unless interactive-accent pattern requires
- Studio HDRI from `drei` for luxury / glass-tech vibe
- `frameloop="demand"` for static / scroll-only
- Lazy-loaded with `dynamic({ ssr: false })` + poster fallback

## Final Audit Checklist

Run BEFORE declaring complete. Each must PASS or be fixed.

### Source-code checks (grep)
```bash
# Emoji
grep -rE '[\x{1F300}-\x{1FAFF}]' app/  # must be empty

# Icon libraries
grep -rE 'lucide-react|@heroicons|@phosphor-icons|@tabler/icons|react-icons|font-awesome|material-icons' app/ package.json  # must be empty

# Forbidden fonts
grep -rE 'Inter|Roboto|"Open Sans"|Space Grotesk|Poppins|Montserrat|Lato|Nunito' app/ tailwind.config.* next.config.*  # must be empty (unless logged override)

# AI cliché copy
grep -rEi 'elevate|seamless|unleash|empower|unlock|game.?changer|next.?gen|cutting.?edge|delve|tapestry|leverage' app/lib/content.ts app/components  # must be empty

# Generic placeholder data
grep -rE 'John Doe|Jane Smith|Acme Corp|99\.99|Lorem ipsum' app/  # must be empty

# h-screen
grep -rE '\bh-screen\b' app/  # must be empty (must use min-h-[100dvh])

# Inline hex colors (should be Tailwind tokens)
grep -rE '#[0-9a-fA-F]{6}' app/components/ | grep -v 'tailwind.config' | grep -v 'globals.css'
# Should be empty or only inside SVG icon paths
```

### Visual checks
- [ ] Hero is NOT centered-H1-at-variance>4 (unless vibe = minimal)
- [ ] Single accent color enforced (count distinct accent values in render)
- [ ] No AI purple/blue hero gradient
- [ ] Custom icon set is consistent (same stroke weight, corner family, fill style)
- [ ] Testimonial avatars don't look like stock photos
- [ ] All text wrap balanced on H1/H2 (`text-wrap: balance`)

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
