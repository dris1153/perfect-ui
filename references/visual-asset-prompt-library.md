# Visual Asset Prompt Library

Battle-tested prompt templates for hero illustrations, backgrounds, OG images, and avatars. Always inject the locked palette and vibe from `visual-direction.md`.

## Prompt Anatomy (apply to ALL)

```
{SUBJECT}
{VIBE_ANCHOR} + {WILDCARD_ADJECTIVE}
Palette: {3 hex codes with role descriptions}
Lighting: {atmospheric keyword}
Composition: {asymmetric | rule-of-thirds | center}
Negative space: {top-left | bottom-right | empty corner}
Style references: {2-3 artists / movements}
Forbidden: AI purple/blue gradient, neon glow, generic tech illustration,
  Microsoft clip-art aesthetic, gradient mesh, default Octane render,
  cyberpunk hologram unless vibe explicitly requests
Aspect ratio: {1:1 | 16:9 | 9:16 | 21:9}
```

## Hero Illustration Templates

### Template: Editorial Hero (asymmetric, organic warmth)
```
A single hand-pulled silkscreen poster of {product metaphor — e.g., "a folded
letter releasing seeds"}, editorial and luxury vibe with hand-crafted wildcard.
Palette: cream background #F5F1E8, deep ink #1A1715, single dusk-rose accent
#B8635A. Lighting: late-afternoon side light from window, soft and dimensional.
Composition: subject anchored to right third, large empty space top-left for
copy overlay. Style references: Saul Bass posters, Dieter Rams product
photography, editorial print of the 1960s. Forbidden: AI purple/blue gradient,
neon, generic tech illustration, gradient mesh, "modern" digital art aesthetic.
Aspect ratio: 16:9.
```

### Template: Brutalist Hero (raw geometry)
```
A photograph-style image of three primitive geometric forms (cube, cone,
cylinder) arranged in deliberate misalignment on raw concrete. Brutalist vibe
with industrial wildcard. Palette: cement #E5E5E5, raw orange accent #FF3B00,
hard black #000000. Lighting: single harsh studio flash from upper-left,
sharp-edged shadows. Composition: forms cluster in lower-right, large empty
sky-like negative space upper-left and right. Style references: Tadao Ando
architecture photography, Wolfgang Tillmans, post-Bauhaus product. Forbidden:
soft gradients, glow, glassmorphism, AI rendering. Aspect ratio: 16:9.
```

### Template: Retro-Futuristic Hero (synth particles)
```
An abstract scene of a particle grid receding to a vanishing point in a deep
twilight space, retro-futuristic vibe with cinematic wildcard. Palette: deep
navy #0A0E27, vapor pink accent #FF6B9D, electric cyan accent #7DF9FF (use
sparingly). Lighting: single backlight casting volumetric rays through
particles, soft fog. Composition: vanishing point at lower-third intersection,
horizon implied not drawn. Style references: TRON 1982, early synthwave album
art, Syd Mead concept paintings. Forbidden: modern AI cyberpunk hologram
aesthetic, neon overload, generic grid wireframe, character figures. Aspect
ratio: 21:9.
```

### Template: Luxury Hero (product on glass)
```
A photorealistic product shot of {product} on a brushed brass podium against
a softly lit dark backdrop, luxury vibe with editorial wildcard. Palette:
near-black #0E0E0C, warm cream highlight #F0EBE0, champagne gold accent
#C9A961. Lighting: two-light setup — soft key from upper-right, rim from
behind for separation. Composition: product centered with deliberate symmetry,
horizon line at lower-third. Style references: Apple keynote photography,
Hermès editorial, Vogue product styling. Forbidden: AI render aesthetic,
purple/blue tint, glow halos, dramatic blur, faux bokeh. Aspect ratio: 1:1.
```

### Template: Organic Hero (natural materials)
```
A still-life photograph of {product metaphor — e.g., "a clay cup of warm
liquid beside dried herbs"} on a linen surface, organic vibe with hand-crafted
wildcard. Palette: linen cream #F4EFE6, moss green #5C7A4A, terracotta accent
#A8693A. Lighting: morning window light, soft diffuse, warm temperature.
Composition: rule-of-thirds with subject in lower-left, sprig of herb leading
eye to upper-right. Style references: Vincent Van Gogh interior paintings,
Kinfolk magazine, contemporary cookbook photography. Forbidden: tech
aesthetic, digital glow, AI gradient, plastic/synthetic materials. Aspect
ratio: 16:9.
```

### Template: Playful Hero (toy-like primitives)
```
A 3D scene of soft-edged primitive shapes (sphere, capsule, torus) in a
deliberately playful arrangement, playful vibe with handmade wildcard.
Palette: cream-yellow background #FFF8E7, coral accent #FF6B4A, deep brown
ink #2D1F12. Lighting: warm soft three-point setup, gentle shadows. Style
references: Memphis Group 1980s, claymation, Bruno Munari toys. Forbidden:
chrome material, neon, AI default 3D render aesthetic, MeshNormalMaterial
rainbow. Aspect ratio: 1:1.
```

## Background Texture Templates

### Subtle grain / noise (tileable, all vibes)
```
A seamless tileable grain texture, very subtle, suitable as overlay on flat
color backgrounds. Color: warm gray on transparent. No discernible pattern,
just organic noise. Aspect ratio: 1:1, optimized for tiling.
```

### Editorial paper texture
```
A high-resolution scan of cream-colored uncoated paper with subtle fiber
texture, no folds, no marks. Color: #F5F1E8 cream with warm gray fibers.
Aspect ratio: 1:1, edges should tile seamlessly.
```

### Brutalist concrete
```
A photograph of raw poured concrete surface, harsh side-lighting revealing
texture. Color: cement gray. No pattern, just stochastic surface. Aspect
ratio: 16:9, edges should tile.
```

## Section Divider Templates

### Editorial: hand-drawn line
```
A single hand-drawn ink line on cream paper, slight imperfection, expressive
weight variation. Color: #1A1715 ink. Length: full width. Style: thin
calligraphy line, single stroke. Aspect ratio: 21:9.
```

### Brutalist: raw block
```
A solid black rectangle with hand-stamped texture, slight ink bleeds at
edges. Color: #000000 on transparent. Aspect ratio: 21:1, full-width
divider strip.
```

## OG Image Templates

OG images are 1200×630, render-safe (no thin text, no off-canvas elements).

### Template: typographic OG
```
A typography-driven Open Graph image, 1200×630px. Headline "{H1 from hero}"
in {display font from visual-direction} at 96px, color {ink from palette},
left-aligned with negative space on right third. Background: {background from
palette} with subtle paper texture. Brand mark in upper-right corner at 40px.
No imagery — pure typography and texture. Forbidden: gradients, generic stock
photo, AI template aesthetic.
```

### Template: hero-image OG
```
A 1200×630px composition combining the hero illustration (cropped to focus on
subject) on left 60%, with bold display typography on right 40% containing
"{H1}" and "{tagline}". Match all colors and lighting from hero illustration.
Brand mark bottom-right.
```

## Avatar Templates (testimonials)

Avatars must feel real, diverse, contextual to product.

### Template: editorial avatar
```
A natural portrait photograph of {role description — e.g., "a 40s freelance
designer in their home studio"}, looking slightly off-camera, soft editorial
lighting. Color treatment: {tinted to match palette accent}. Style references:
August Sander portraits, contemporary editorial. Forbidden: stock photo
aesthetic, fake smile, generic office background, perfect symmetry, AI face
artifacts. Aspect ratio: 1:1.
```

### Template: hand-illustrated avatar
```
A loose ink-and-watercolor portrait of {role description}, single sitting,
expressive line, not overly polished. Palette: ink lines + single accent wash
matching {accent color}. Style references: Alvin Lustig, Saul Bass character
work, mid-century editorial illustration. Aspect ratio: 1:1.
```

## Tool Routing

| Asset type | Recommended tool | Command |
|-----------|------------------|---------|
| Hero illustration (artistic) | `ck:ai-artist` | `python3 ~/.claude/skills/ai-artist/scripts/generate.py "{prompt}" -o hero.png --mode search` |
| Hero photo (realistic) | `ck:ai-multimodal` Imagen Ultra | `python3 ~/.claude/skills/ai-multimodal/scripts/gemini_batch_process.py --task generate --model imagen-4.0-ultra-generate-001 --prompt "{prompt}" --output hero.png` |
| Background texture | `ck:ai-multimodal` Imagen Fast | `--model imagen-4.0-fast-generate-001` |
| OG image | `ckm:design` social-photos | per `~/.claude/skills/design/references/social-photos-design.md` |
| Avatar | `ck:ai-multimodal` Nano Banana 2 | `--model gemini-3.1-flash-image-preview` |

## Validation

After every generation:
1. Open via `ck:ai-multimodal` analyze: `gemini -y -m gemini-2.5-flash <"image-path"`
2. Ask Claude: "Does this image match {palette hex codes} and feel like {vibe}? Score 1-10. List drift."
3. If score < 7 OR palette drift > 30%, regenerate with stronger negative prompt.
4. If score ≥ 8, save to `public/landing/`.

## Negative Prompt Library

Reuse these to suppress common AI defaults:

```
no AI purple/blue gradient
no neon glow, no outer glow on text
no generic tech illustration with circuits/data-flow lines
no Microsoft clip-art aesthetic
no gradient mesh background
no default Octane / Cycles render aesthetic
no cyberpunk hologram unless explicitly requested
no character figures unless explicitly requested
no stock-photo "diverse team smiling at laptop"
no isometric 3D illustration of "abstract concepts"
no chrome / liquid metal material unless vibe is glass-tech
no MeshNormalMaterial rainbow (3D)
no cliché icons inside illustrations (no rocket, no shield, no lightbulb)
```
