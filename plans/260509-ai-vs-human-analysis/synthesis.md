---
title: AI vs Human Landing Page Analysis — Synthesis
date: 2026-05-09
type: research-synthesis
sources: 12 URLs (5 AI + 7 human), HTML inspection + screenshot analysis
---

# AI vs Human Landing Page Analysis

## Methodology

- **Direct evidence:** curl-fetched raw HTML for all 12 URLs, grep'd for: font-family, icon libraries, framework signals, Tailwind density, AI cliché phrases, h-screen vs dvh, animation libraries, 3-col grid patterns
- **Visual evidence:** Puppeteer screenshots (1440×900 viewport) of all 12 pages; visually analyzed 8 key pages
- **Limitation:** SPA pages (3 nextlevelbuilder demos, owo, marblex) had thin initial HTML — relied more on screenshots for those

## Pages Analyzed

### AI-generated (5)
1. `nextlevelbuilder.io/demo/educational-platform` — "LearnHub"
2. `nextlevelbuilder.io/demo/ai-chatbot-platform`
3. `nextlevelbuilder.io/demo/fintech-crypto` — "CryptoVault"
4. `snapstoryai.com`
5. `exgenai.com`

### Human-made (7)
1. `isadeburgh.com` (portfolio)
2. `overlay.com` (landing — beauty tech)
3. `paperclip.ing` (landing — open-source AI agents)
4. `gordensun.github.io/CuiMao` (portfolio)
5. `owo.app` (landing — fintech, WhatsApp payments)
6. `marblex.io` (landing — Web3 gaming, "funny")
7. `augen.pro` (landing — wearable tech, "elegant")

## Direct Evidence Table

| Signal | AI pages (5) | Human pages (7) |
|--------|--------------|-----------------|
| Forbidden Google Fonts (Inter / Space Grotesk / DM Sans / Roboto) | **3/5** (3 nextlevelbuilder = DM Sans + Space Grotesk) | 3/7 (paperclip+owo+marblex use Inter PAIRED with distinctive serif) |
| Distinctive paid display font detected | 0/5 | **6/7** (PP Neue Montreal, Instrument Serif, Greed, GT Maru Rounded, custom display, etc.) |
| Lucide / Heroicons / Phosphor library | **2/5** (snapstory, exgen) | **0/7** |
| AI purple/blue gradient detected | **2/5** (exgen, snapstory dark variant) | 0/7 |
| `h-screen` utility | **2/5** (snapstory, exgen) | **0/7** |
| Tailwind utility density (count) | 379, 383 (snapstory, exgen) | 0–64 (most 0–11) |
| `grid-cols-3` (3-col equal feature row) | **6 hits in exgen alone** | **0/7** |
| GSAP / Lenis / Theatre / WebGL detected | 0/5 | **4/7** (isadeburgh, overlay, augen, marblex implied) |
| Loading screen / preloader markup | 0/5 | **2/7** explicitly (cuimao 14 hits, isadeburgh 1 hit, marblex shows splash visually) |
| AI cliché copy (Elevate/Seamless/Unleash/Empower/Next-gen/etc.) | 5/5 hit | 5/7 hit (but contextually different — see notes) |
| Two equal-weight CTAs in hero | **5/5** (LearnHub, chatbot, fintech, snapstory, exgen all have dual CTAs) | 1/7 (overlay has subscribe form + "Get in touch" in nav) |
| Round fake numbers (10K+, 99.99%, 1M+) | **4/5** | 1/7 (owo "Works with banks" — real logos, not stat) |
| Centered hero + centered H1 | **5/5** | 2/7 (overlay, paperclip — both compensate with strong visuals) |
| Custom illustration / artwork in hero | 0/5 (snapstory has AI penguin) | **5/7** (paperclip flamingos, marblex logotype, cuimao zine, augen 3D head, isadeburgh portrait) |

## Key Insight: Tells are CUMULATIVE, not Disqualifying

Single rule violations don't prove AI. Multiple stacked tells do.

### Example — `overlay.com` (HUMAN)
Breaks several rules:
- ✗ Centered H1 ("The Future of Beauty is Automated")
- ✗ "Future of" forbidden phrase
- ✗ "cutting-edge", "unlock" cliché copy
- ✗ Hero composition centered

But COMPENSATES with:
- ✓ Custom photorealistic portrait with intentional light beam (premium)
- ✓ Lavender-peach-mint pastel gradient (NOT AI purple/blue)
- ✓ GSAP + Lenis + WebGL (animation craft)
- ✓ Single CTA only
- ✓ Off-white background, restrained palette

**Verdict:** High visual craft + commitment to aesthetic > rule compliance.

### Example — `exgenai.com` (AI)
Stacks 10+ tells:
- ✗ AI purple/blue gradient hero
- ✗ "Create Beautiful Landing Pages in Seconds" headline
- ✗ Cyan-gradient highlight on "Beautiful"
- ✗ Two CTAs ("Start Creating Free" + something)
- ✗ Generic browser mockup
- ✗ "No credit card • 7 free pages • 60 second setup" friendly bullets
- ✗ Centered hero
- ✗ Lucide-react detected
- ✗ Tailwind heavy density (379 utilities)
- ✗ "Game-changer" / "seamless" testimonial copy
- ✗ Generic CTA labels ("Get Started", "Sign In", "Subscribe")

**Verdict:** Density of tells = AI fingerprint.

## Refined Detection Rules (NEW patterns to add)

### Tier 1: Strong AI tells (each one is a serious flag)
1. **DM Sans + Space Grotesk pairing** (Google Fonts duo) — present in 3/5 AI pages, 0/7 human
2. **AI purple/blue gradient hero** + **gradient highlight on H1 keyword** (signature combo)
3. **Lucide-react / @heroicons / @tabler imports**
4. **Two equal-weight CTAs in hero** — was already on our list, confirmed AI-favored
5. **`h-screen` utility class** present
6. **3-column equal feature card grid** (exgen has 6 hits)

### Tier 2: AI compositional tendencies
7. **Generic browser mockup as right-half of split hero** (exgen, snapstory show this exact pattern)
8. **Friendly bullet-list reassurance row** ("No credit card • 7-day free trial • Cancel anytime")
9. **Round fake stats** (10K+, 2M+, 1M+, 99.99%) — 4/5 AI pages
10. **Generic SaaS CTA labels** ("Get Started", "Sign In", "Subscribe", "Start Free")
11. **AI-generated cute illustration** (cartoon animal with laptop, generic 3D character)
12. **Gradient text highlight on single hero keyword** (e.g., "Confidence" highlighted, "Beautiful" highlighted)

### Tier 3: AI copy fingerprints (already in our rules, confirmed)
13. "Create Beautiful X in Seconds" headline pattern
14. "Built for Serious X" / "Designed for the modern X" patterns
15. "Trust" / "Confidence" / "Power" as last word of H1

### Tier 4: Stacked-density indicator (META rule)
16. **Tailwind utility class count > 200** in initial HTML — strong AI signal (snapstory: 383, exgen: 379, vs human max: 64)

## Refined Human Craft Signals (NEW patterns to encode)

### Strong human tells
1. **Custom paid display font** — PP Neue Montreal, Instrument Serif, Greed, GT Maru Rounded, Migra, Cabinet Grotesk
2. **GSAP + Lenis combo** detected (smooth scroll + scroll-triggered animation)
3. **WebGL canvas** in hero
4. **Custom illustrated/photographed hero artwork** (not stock, not generic AI illustration)
5. **Single primary CTA in hero** (or zero CTAs — content invites, doesn't push)
6. **Real specific numbers** (paperclip 60.3k stars, real product names like A¹ Sense)

### Compositional human tells
7. **Loading screen as brand moment** — marblex shows giant logotype while loading, not spinner
8. **Lowercase / understated wordmark** (augen, owo) — confidence
9. **Period in declarative H1** ("Beyond Humanware.") rather than exclamation
10. **Off-black / off-white colors** instead of pure #000/#fff
11. **Asymmetric or boldly committed composition** — augen (head off-center), owo (ransom-note word blocks)
12. **Specific proprietary product names** — augen "A¹ Sense, B¹ Eye, A¹ Neuro"; paperclip "human control plane"

### Loading UI patterns observed
- **Marblex** (funny vibe): full-viewport custom logotype on light gray, masks complex Web3 site loading
- **Cuimao** (portfolio): 14 loader-related markers in HTML, custom spinner+label combo
- **Isadeburgh** (portfolio): scroll-triggered reveals with massive empty-space + bold display numerics ("99")
- **Other human pages**: NO splash — restraint when not needed (augen, paperclip, owo)

**Loading UI rule:** Only use a splash if it serves a function — masking heavy assets, brand-introduction moment, or expectation-setting. Never as decoration.

## Vibe-Specific Findings

### Funny vibe (Marblex)
What CREATES the funny:
- **Custom bubbly typography** (GT Maru Rounded — chunky, rounded, notched-white-openings)
- **Massive scale** of single brand mark
- **Restrained color** (light gray + black, not garish neons)
- **No exclamation marks** — humor through type, not punctuation
- Rumored mascot character (anime/manga goblin) seen in third-party reviews

### Elegant vibe (Augen)
What CREATES the elegance:
- **PP Neue Montreal** display font (premium tech serif)
- **Massive negative space** — 90%+ of viewport is breathing room
- **Single 3D-rendered head** as visual centerpiece
- **Lowercase wordmark** in lower-left corner (anti-branding)
- **Period in headline** ("Beyond Humanware.")
- **Floating pill nav** asymmetrically placed at top-center
- **Proprietary product naming** with subscript characters (A¹, B¹)
- **NO CTAs in hero** — chips invite discovery
- **Off-white background**, single muted blue-gray accent
- **Restraint in everything**

## Critical Synthesis: Why Human Pages "Read" Human

**The pattern:** Human-made pages exhibit COHESION and COMMITMENT.

| Cohesion check | What human pages do |
|----------------|---------------------|
| Type | Display font is distinctive AND paired with body type that complements (not random Google Fonts duo) |
| Color | One vibe direction committed (one accent, one neutral family) — not "minimal AI palette + purple gradient surprise" |
| Imagery | Custom or curated assets that match vibe — not stock or AI illustration |
| Copy | Specific to product/owner with proprietary terminology — not "Elevate your X" |
| Motion | Intentional — gsap/lenis only when reveals serve narrative, not decorative |
| Layout | Either follows convention well OR boldly subverts it — not "default centered" |

**The pattern of AI:** Tells stack because AI defaults to ALL safe options simultaneously. The result is a page that's "trying to look professional" without committing to any aesthetic direction.

## Recommended Updates to perfect-ui Skill

### Update 1: anti-slop-rules.md — Tier system
Replace flat list with cumulative tier system:
- **Tier 1 (auto-fail):** ≥2 tier-1 tells = AI fingerprint, must fix
- **Tier 2 (caution):** 1 tier-1 + 2+ tier-2 = drift, recommend fixing
- **Tier 3 (compensable):** 1-2 tier-3 alone is OK if visual craft compensates

### Update 2: anti-slop-rules.md — Add new patterns
- DM Sans + Space Grotesk pairing as forbidden font combo (new specific entry)
- Generic browser mockup as right-half hero (new layout anti-pattern)
- Friendly bullet checkbox reassurance row (new copy anti-pattern)
- Tailwind utility count > 200 (new density indicator)
- Gradient text highlight on single H1 word (new layout anti-pattern)

### Update 3: NEW reference file — `loading-ui-patterns.md`
- When to use a splash/loading screen (decision tree)
- Approved patterns: brand-moment, asset-masking, expectation-setting
- Forbidden patterns: generic spinner without context, fake progress bar
- Implementation patterns (Lenis splash, GSAP intro, simple opacity)

### Update 4: visual-direction-guide.md — Add cohesion check
After locking palette + typo + spatial, add a "commitment audit" — does every choice reinforce ONE direction?

### Update 5: anti-slop-rules.md — Add nuance footer
Document that single rule violations are COMPENSABLE with high visual craft (per overlay/paperclip examples). The skill should not refuse "centered hero" if vibe is genuinely minimal AND visual carries weight.

## Unresolved Questions

1. The skill recommends `min-h-[100dvh]` — confirmed AI pages use `h-screen`, but no human page uses either (most have viewport-relative section heights without forcing full-viewport). Should we soften the rule?
2. Inter is in 3/7 human pages (owo, paperclip, marblex use Inter for body) — should we allow Inter as body when paired with distinctive display? Probably yes.
3. The 3 nextlevelbuilder demos are intentionally generic AI demos — they may be the EXTREME case. Real AI-tool-generated pages might be subtler.
4. Should the skill expose a `--cohesion-audit` mode that scores against this tier system?
