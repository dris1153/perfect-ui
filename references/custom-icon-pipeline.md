# Custom Icon Pipeline — Decision Tree & Recipes

How to produce a cohesive, bespoke icon set without ever touching emoji or icon libraries.

## Why Custom (Not Lucide / Heroicons)

A landing's icon set is a brand asset. Generic library icons leak the "made by AI" fingerprint and dilute the vibe. Custom icons:
- Match the locked stroke weight and corner family from visual direction
- Use the brand's metaphor language (organic for "wellness", angular for "fintech")
- Avoid clichés (rocket = launch, shield = security)

## Decision Tree

```
Need an icon?
├─ Is it a simple geometric form? (arrow, plus, dot, line, check)
│   └─ Direct SVG code (Claude writes inline)
├─ Is it symbolic but geometric? (clock, eye, lock, gear)
│   ├─ Can the metaphor be drawn with 1-3 paths?
│   │   ├─ Yes → Direct SVG code
│   │   └─ No → AI gen + trace
├─ Is it illustrative / handcrafted feeling? (mascot, character, scene)
│   └─ AI gen + trace
└─ Is it ornate / line-art / etched? (luxury, editorial)
    └─ AI gen + trace via ck:ai-artist with style prompt
```

## Method 1: Direct SVG Code

**When:** Simple geometric, symbolic, or vibe-matched stroke art.

### Process
1. Open `references/visual-direction.md` — note locked stroke weight and corner family.
2. Sketch in head: which 1-4 paths express the metaphor?
3. Write the SVG with viewBox `0 0 24 24` (system) or `0 0 48 48` (hero glyphs).
4. Use `currentColor` for fill/stroke so component inherits color from CSS.
5. Apply stroke-linecap: round/square/butt to match corner family.

### Template (outlined, 1.5px stroke, rounded caps)
```tsx
import { Icon, type IconProps } from './icon';

export const FeatureSpeed = (props: IconProps) => (
  <Icon {...props} viewBox="0 0 24 24">
    <path
      d="M4 12h12M12 4l8 8-8 8"
      fill="none"
      stroke="currentColor"
      strokeWidth="1.5"
      strokeLinecap="round"
      strokeLinejoin="round"
    />
  </Icon>
);
```

### Base Icon component
```tsx
// app/components/icons/icon.tsx
import { type SVGProps } from 'react';

export type IconProps = SVGProps<SVGSVGElement> & {
  size?: number;
};

export const Icon = ({ size = 24, children, ...props }: IconProps) => (
  <svg
    width={size}
    height={size}
    viewBox="0 0 24 24"
    aria-hidden="true"
    {...props}
  >
    {children}
  </svg>
);
```

## Method 2: AI Gen + Trace

**When:** Illustrative, ornate, mascot-like, or you can't draw it in 4 paths.

### Path A: ckm:design icon generator (preferred for production)
```bash
python3 ~/.claude/skills/design/scripts/icon/generate.py \
  --prompt "folded paper origami crane representing privacy" \
  --style outlined \
  --color "#1A1715" \
  --size 24 \
  --output app/components/icons/raw/feature-secure.svg
```

Match `--style` to the locked icon style from cohesion rules:
- `outlined` for stroke-only sets
- `filled` for solid sets
- `duotone` for two-tone sets
- `thin` for luxury / editorial vibe
- `bold` for brutalist / industrial vibe
- `hand-drawn` for organic / hand-crafted vibe

### Path B: ck:ai-artist (when style prompt matters more than category)
```bash
python3 ~/.claude/skills/ai-artist/scripts/generate.py \
  "minimalist line-art icon of a folded paper crane, single 1.5px stroke, no fill, on white" \
  -o icons/raw/feature-secure.png \
  --mode search
```

Then trace the PNG to SVG. Three options:
1. **Inkscape Trace Bitmap** (manual): user opens file, runs Path → Trace Bitmap.
2. **autotrace CLI** (automated): `autotrace -output-format svg input.png > output.svg`
3. **Re-write by hand**: best result for simple shapes — view AI image, write SVG manually.

### Path C: ck:ai-multimodal Imagen (highest quality realistic)
```bash
python3 ~/.claude/skills/ai-multimodal/scripts/gemini_batch_process.py \
  --task generate \
  --prompt "minimalist black ink icon, folded paper crane, white background, no shadows" \
  --output icons/raw/feature-secure.png
```

## Cohesion Rules (Apply to ENTIRE Set)

Pick ONE value per rule, apply to every icon. Document choices at top of `app/components/icons/index.ts`:

```ts
/**
 * Icon Set Cohesion Rules — DO NOT VIOLATE
 * - Stroke weight: 1.5px
 * - Corners: rounded (strokeLinecap="round", strokeLinejoin="round")
 * - Fill: none (outlined only)
 * - Metaphor language: organic, hand-drawn feel
 * - viewBox: 24×24 system, 48×48 hero
 */
```

### Rule 1: Single stroke weight
Pick: `1px` thin / `1.5px` default / `2px` bold / `3px` brutalist.

### Rule 2: Single corner philosophy
- **Sharp**: `strokeLinecap="butt" strokeLinejoin="miter"` — brutalist, industrial
- **Rounded**: `strokeLinecap="round" strokeLinejoin="round"` — playful, organic
- **Mixed-by-rule**: rounded caps, sharp joins — editorial

### Rule 3: Single fill style
- Outlined (stroke only)
- Filled (solid only)
- Duotone (two opacities) — only choose this if entire set can be drawn in 2 layers

NEVER mix. If one icon "needs" filled but the set is outlined, redesign the metaphor.

### Rule 4: Visual metaphor language
Tied to vibe:

| Vibe | Metaphor language |
|------|------------------|
| Minimal | Geometric primitives — circle, line, square. Avoid representational. |
| Editorial | Hand-drawn feel, organic curves, slightly imperfect |
| Brutalist | Pixel/blocky, aggressive geometry, no curves |
| Retro-futuristic | Wireframe, isometric, technical drawing |
| Organic | Flowing curves, leaf/water/wind metaphors |
| Luxury | Thin engraved lines, monogram-style |
| Playful | Slightly cartoonish, friendly proportions |
| Industrial | Mechanical, technical schematic feel |
| Art-deco | Symmetrical geometric, sunburst, fan |
| Glass-tech | Refractive shapes, layered transparency |
| Hand-crafted | Sketch lines, imperfect curves, dotted texture |

## Cliché Metaphors to Avoid

| Concept | Cliché icon | Better alternative |
|---------|-------------|-------------------|
| Launch | Rocketship | Arc (rising line), seedling, dawn sun |
| Security | Shield | Folded paper, vault door, woven knot |
| Speed | Lightning bolt | Arc with momentum dot, blur lines |
| Done | Check in circle | Underline mark, simple check (no circle) |
| Idea | Lightbulb | Sun-ray fragment, struck match |
| Settings | Gear | Slider track, dial face |
| Search | Magnifying glass | Open quote mark + dot |
| Email | Envelope | Diagonal paper fold |
| Cart | Shopping cart | Tagged item silhouette |
| User | Person silhouette | Initial monogram |

## File Structure (Next.js)

```
app/components/icons/
├── icon.tsx                  # Base wrapper component
├── index.ts                  # Re-exports + cohesion rules header
├── raw/                      # Source PNGs from AI gen (gitignored)
│   ├── feature-secure.png
│   └── ...
├── feature-speed.tsx         # Inline SVG components
├── feature-secure.tsx
├── feature-flow.tsx
├── nav-logo-mark.tsx
├── cta-arrow.tsx
├── social-twitter.tsx
└── testimonial-quote.tsx
```

`index.ts`:
```ts
/**
 * Icon Set Cohesion Rules — see custom-icon-pipeline.md
 * - Stroke weight: 1.5px
 * - Corners: round caps + round joins
 * - Fill: none (outlined only)
 * - Metaphor: organic / hand-drawn
 */
export { FeatureSpeed } from './feature-speed';
export { FeatureSecure } from './feature-secure';
export { FeatureFlow } from './feature-flow';
export { NavLogoMark } from './nav-logo-mark';
export { CtaArrow } from './cta-arrow';
export { SocialTwitter } from './social-twitter';
export { TestimonialQuote } from './testimonial-quote';
```

Usage in components:
```tsx
import { FeatureSpeed } from '@/components/icons';

<FeatureSpeed size={32} className="text-accent" />
```

## Validation Checklist

Before declaring icon set complete:

- [ ] Every icon imported from `app/components/icons/` (no library imports anywhere)
- [ ] Every icon has same stroke weight (grep `strokeWidth=` to verify)
- [ ] Every icon uses same `strokeLinecap` value
- [ ] Every icon uses `currentColor` (theme-able)
- [ ] No emoji in source files
- [ ] No clichéd metaphor (rocket / shield / lightning) unless vibe specifically calls for it
- [ ] Icons render at 16px / 24px / 48px without losing readability
- [ ] Documented cohesion rules in `index.ts` header

## Anti-Patterns

- ❌ Mixing outlined and filled icons in the same set
- ❌ One icon at 2px stroke when the rest are 1.5px
- ❌ Using a library icon "just for now" — it never gets replaced
- ❌ Auto-tracing AI output without cleanup (produces 200+ path nodes)
- ❌ Naming icons by what they look like (`circle-check`) instead of what they mean (`feature-verified`)
- ❌ Forcing a metaphor that doesn't fit cohesion (e.g., illustrative crane in a brutalist set)
