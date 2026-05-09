# Visual Direction Guide

How to translate a vibe brief into locked color palette, typography, and spatial language. Use this in Phase 2.

## Vibe → Palette Mapping

11 anchor vibes with starter palette options. Each row = one candidate. Show user 3 from the matching vibe row.

### Minimal
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#FAFAF7` | `#F1F0EB` | `#181715` | `#2A4A3E` (forest) |
| `#FFFFFF` | `#F4F4F2` | `#0F0F0E` | `#5C5346` (taupe) |
| `#F8F6F1` | `#EFEAE0` | `#1A1A18` | `#A03B2A` (rust) |

### Editorial
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#F5F1E8` | `#EDE6D6` | `#1A1715` | `#B8635A` (dusk-rose) |
| `#EFEAD8` | `#E2DAB9` | `#221F1B` | `#7A8A4A` (olive) |
| `#F8F4E9` | `#E8E1CE` | `#0E1A2B` | `#C89A3A` (ochre) |

### Brutalist
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#E5E5E5` | `#FFFFFF` | `#000000` | `#FF3B00` (raw orange) |
| `#FFFF00` | `#000000` | `#000000` | `#FF00FF` (raw magenta) |
| `#D9D9D6` | `#FFFFFF` | `#0A0A0A` | `#0033FF` (raw blue) |

### Retro-Futuristic
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#0A0E27` | `#1A1F3A` | `#E8E6F0` | `#FF6B9D` (vapor pink) |
| `#1B1B2F` | `#16213E` | `#F0EFEA` | `#E94560` (synth red) |
| `#13111E` | `#241A3D` | `#F5F0FF` | `#7DF9FF` (electric cyan) |

### Organic
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#F4EFE6` | `#E8DCC4` | `#2C2418` | `#5C7A4A` (moss) |
| `#FAF6EE` | `#E5D9C0` | `#1F1A12` | `#A8693A` (clay) |
| `#EFEAE0` | `#D8C9B0` | `#3A2F1F` | `#7A6F4F` (linen) |

### Luxury
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#0E0E0C` | `#1A1A17` | `#F0EBE0` | `#C9A961` (champagne gold) |
| `#1A1715` | `#2A2521` | `#F5F0E8` | `#8B6F47` (bronze) |
| `#0F1216` | `#1A1F26` | `#E8E5DD` | `#A89968` (oxidized brass) |

### Playful
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#FFF8E7` | `#FFE8C2` | `#2D1F12` | `#FF6B4A` (coral) |
| `#FCE4EC` | `#F8BBD0` | `#3D1F2C` | `#5A3FCC` (grape) |
| `#E0F4F4` | `#B8E0E0` | `#1F3A3D` | `#F4A742` (marigold) |

### Industrial
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#1F1E1B` | `#2D2C28` | `#E5E2DC` | `#D45A1A` (rust orange) |
| `#262524` | `#36342F` | `#EFECE5` | `#A09480` (cement) |
| `#1A1A1A` | `#2A2A2A` | `#E0DDD6` | `#7A6F5F` (steel) |

### Art-Deco
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#1A1614` | `#2A211C` | `#E8DCC4` | `#C9A961` (gold) |
| `#0E1A2B` | `#1A2840` | `#E5DCC4` | `#B8954A` (brass) |
| `#1F0E18` | `#2D1825` | `#F0E5D5` | `#D4A04F` (champagne) |

### Glass-Tech
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#0A0F1F` | `#141B33` (glass tint) | `#E8EAF0` | `#5EE7DF` (glacier) |
| `#0E1117` | `#1A1F2E` | `#F0F2F7` | `#7C9CFF` (azure) |
| `#0C1019` | `#171D2E` | `#E5E8F0` | `#A2D8F0` (ice) |

### Hand-Crafted
| Bg | Surface | Ink | Accent |
|----|---------|-----|--------|
| `#F4ECD8` | `#E5D6B5` | `#2C1F0F` | `#8B4A2A` (terracotta) |
| `#EFE4D2` | `#D8C5A5` | `#1F1810` | `#5C7A3A` (sage) |
| `#F8F0DC` | `#E2D0AD` | `#2A1F12` | `#B8682F` (caramel) |

## Tailwind Token Output Pattern

After lock, generate this snippet for `tailwind.config.ts`:

```ts
theme: {
  extend: {
    colors: {
      bg: { DEFAULT: '#F5F1E8', muted: '#EDE6D6' },
      ink: { DEFAULT: '#1A1715', muted: '#5A5247' },
      accent: { DEFAULT: '#B8635A', soft: '#E5C4BF' },
    },
    fontFamily: {
      display: ['var(--font-display)', 'serif'],
      sans: ['var(--font-body)', 'sans-serif'],
    },
  },
}
```

## Vibe → Typography Pairs

### Minimal
- `Söhne` + `Söhne Mono` (numerics)
- `Neue Haas Grotesk` + `Neue Haas Unica`
- `GT America` + `GT America Mono`

### Editorial
- `Migra` (display) + `GT Sectra` (body)
- `Editorial New` (display) + `Lyon Text` (body)
- `Canela` (display) + `Söhne` (body)

### Brutalist
- `PP Neue Machina Inktrap` + `PP Neue Montreal`
- `Migra` + `GT America Mono`
- `Hubot Sans` + `Söhne`

### Retro-Futuristic
- `PP Neue Machina` + `JetBrains Mono`
- `Cabinet Grotesk` + `IBM Plex Mono`
- `Space Mono` + `Space Mono` (mono everywhere — done well)

### Organic
- `Tobias` (display) + `Lyon Text` (body)
- `Migra` + `Reckless Neue`
- `IvyMode` + `IvyJournal`

### Luxury
- `PP Editorial New Ultralight` + `Reckless Neue`
- `Canela Light` + `Söhne Buch`
- `Editorial Old` + `Söhne Mono` (numerics)

### Playful
- `Boing` + `Plus Jakarta Sans`
- `Cabinet Grotesk` (heavy weights) + `General Sans`
- `Sharpie` + `General Sans`

### Industrial
- `Söhne Breit` + `Söhne Mono`
- `Founders Grotesk Condensed` + `Founders Grotesk`
- `Apercu Condensed` + `Apercu Mono`

### Art-Deco
- `Migra` + `Reckless Neue`
- `Mostra Nuova` (specifically deco) + `Söhne`
- `Cinzel Display` + `Lyon Text`

### Glass-Tech
- `PP Neue Montreal` + `JetBrains Mono`
- `Geist` + `Geist Mono`
- `Söhne` + `Söhne Mono`

### Hand-Crafted
- `Tobias` + `Reckless Neue`
- `Caslon Doric` + `Lyon Text`
- `Migra` + `Söhne`

## Forbidden Fonts (Reject Without Override)

`Inter`, `Roboto`, `Arial`, `Open Sans`, `Space Grotesk`, `Poppins`, `Lato`, `Montserrat`, `Nunito`.

If user explicitly requests one of these twice, allow but log: "User-overridden anti-slop violation: Inter".

## Spatial Language Rules

### Asymmetric Editorial
- Hero: split 60/40 or 70/30, NOT 50/50
- H1 left-aligned, sized 7xl–9xl, line-height tight
- Negative space anchored to one corner (top-left typically)
- Use `text-wrap: balance` on H1
- Section grids vary: 12-col with offset placement

### Minimal Grid
- Container max-width 1280px, generous py-32 between sections
- 12-col grid, components span 4-6-8 cols
- Padding hierarchy: section py-32, container px-8, component p-12
- Single horizontal divider between sections (1px, ink-muted at 20%)

### Brutalist Density
- No max-width — components span viewport
- Tight padding (p-2 to p-4)
- Visible borders (2px solid ink) on every box
- Monospace numerics
- Asymmetric cramped grids (3-col with 1-2-1 fr)

### Atmospheric
- Layered backgrounds: gradient + noise PNG + soft-blur shadows
- `backdrop-filter` glass surfaces with inner border
- Generous py-40+ between sections
- Type sits on atmosphere, not on flat color

## 3D Layer Pairings (when Phase 2d = yes)

| Vibe | Best 3D layer type | Avoid |
|------|---------------------|-------|
| Minimal | interactive-accent (small widget) | hero-scene (clutters) |
| Editorial | scroll-triggered (subtle) | hero-scene |
| Brutalist | hero-scene (raw geometry) | scroll-triggered |
| Retro-futuristic | hero-scene (particles, grids) | flat |
| Organic | scroll-triggered (camera flow) | hero-scene |
| Luxury | hero-scene (rotating product) | brutalist geometry |
| Playful | interactive-accent (toy-like) | static hero |
| Industrial | hero-scene (mechanical) | organic flow |
| Art-deco | scroll-triggered (geometric reveal) | particles |
| Glass-tech | hero-scene (volumetric glass) | flat |
| Hand-crafted | none (3D fights vibe) | hero-scene |

## Output Artifact Template

Save to `plans/{date}-{slug}/visual-direction.md`:

```markdown
# Visual Direction — {Project Name}

## Vibe
- Anchor: {one of 11}
- Wildcard: {brand-owned adjective}

## Palette (LOCKED)
- Background: `#XXXXXX`
- Surface: `#XXXXXX`
- Ink: `#XXXXXX`
- Accent: `#XXXXXX` (single)

## Typography (LOCKED)
- Display: `{Font Name}` weights [400, 500, 700]
- Body: `{Font Name}` weights [400, 500, 600]

## Spatial Language
{Asymmetric Editorial | Minimal Grid | Brutalist Density | Atmospheric}

## 3D Layer
{none | hero-scene | scroll-triggered | interactive-accent}

## Forbidden (apply throughout build)
- No Inter / Roboto / AI purple gradient
- No emoji
- No icon libraries
- No `h-screen`
- No "Elevate / Seamless / Unleash" copy
- No centered H1 (unless vibe = minimal)
```

## Commitment Audit (REQUIRED before Phase 3)

After locking palette + typography + spatial language, run a commitment audit. The single biggest distinguisher between AI and human pages is **cohesion** — every choice reinforces ONE direction (see `plans/260509-ai-vs-human-analysis/synthesis.md` for evidence).

### The audit (six questions)

For each question, give a 1-10 score. **Total ≥ 48/60 = pass; <48 = revisit visual direction.**

1. **Type → vibe alignment**: does the locked display font's character match the vibe anchor? (e.g., GT Maru Rounded for funny, PP Neue Montreal for elegant — not Inter for both)
2. **Palette → vibe alignment**: do the locked colors evoke the vibe word without hedging? (luxury palette has gold/champagne, NOT teal AI-startup gradient)
3. **Spatial → vibe alignment**: does the spatial language reinforce vibe? (atmospheric vibes need generous padding + grain; brutalist needs cramped, hard borders)
4. **Internal palette consistency**: single accent, single neutral family, no surprise rogue colors planned
5. **Typography pair tension**: display + body create deliberate contrast OR deliberate harmony (NOT "we picked two random Google Fonts that go OK together")
6. **Vibe-anchor commitment**: would a designer recognize this anchor in 2 seconds from a screenshot? (if vibe is "luxury" but palette could pass for SaaS, commitment is weak)

### Scoring template

```
Visual Direction Commitment Audit — {Project}

1. Type → vibe: {N}/10  ({reason})
2. Palette → vibe: {N}/10  ({reason})
3. Spatial → vibe: {N}/10  ({reason})
4. Palette consistency: {N}/10  ({reason})
5. Typography pair: {N}/10  ({reason})
6. Vibe commitment: {N}/10  ({reason})

TOTAL: {sum}/60  →  {PASS if ≥48 / REVISIT if <48}
```

### What "revisit" means

If score < 48, return to one of:
- **2a**: re-pick palette
- **2b**: re-pick typography
- **2c**: re-pick spatial language

Do NOT proceed to Phase 3 with a score below 48 — every downstream phase (icons, assets, plan, code) inherits the commitment level. A weak direction = AI-fingerprint output regardless of execution.

### Why this matters (data)

Direct comparison of 12 real landings showed: AI pages stack 10+ anti-slop violations because they default to ALL safe choices simultaneously without committing to any vibe. Human pages with strong commitment scores can break 1-2 individual rules and still read as human-crafted (overlay.com breaks 4 anti-slop rules but commits hard to "premium beauty tech" via custom photo + GSAP + WebGL + restrained palette).

**Commitment is the multiplier on craft.**
