# Section Archetypes

Reusable section layouts. Pick by vibe + section type. Adapt to locked palette/typography from `visual-direction.md`.

## Hero Archetypes

### A1. Editorial Asymmetric (60/40 split)
```
┌─────────────────────────────────────┐
│  [Display H1                        │
│   spans 3 lines                     │
│   weight 500]            [HERO IMG] │
│                          [   3:4   ]│
│  Subheadline 1-2 lines              │
│                                     │
│  [CTA →]                            │
└─────────────────────────────────────┘
```
Best for: editorial, organic, hand-crafted

### A2. Minimal Centered (low VARIANCE only)
```
┌─────────────────────────────────────┐
│                                     │
│         [Logo mark, small]          │
│                                     │
│      [H1 centered, 2 lines]         │
│                                     │
│       [Sub, single line]            │
│                                     │
│            [CTA →]                  │
│                                     │
│      [Single hero element]          │
│                                     │
└─────────────────────────────────────┘
```
Best for: minimal — only when DESIGN_VARIANCE ≤ 3

### A3. Brutalist Full-Bleed
```
┌─────────────────────────────────────┐
│ [HERO 3D / LARGE IMAGE - full bleed]│
│                                     │
│  [H1 RAW DISPLAY                    │
│   OVERLAID, BLOCK SHADOW]           │
│                                     │
│  [▌ CTA]                            │
└─────────────────────────────────────┘
```
Best for: brutalist, industrial, retro-futuristic

### A4. Atmospheric Layered
```
┌─────────────────────────────────────┐
│ [GRADIENT + GRAIN BACKGROUND]       │
│                                     │
│      [Display H1 floating           │
│       with soft shadow]             │
│                                     │
│       [3D element behind]           │
│       [Sub] [CTA]                   │
└─────────────────────────────────────┘
```
Best for: glass-tech, retro-futuristic, luxury

## Social Proof Archetypes

### S1. Single Row Logo Bar
```
─────────────────────────────────────
  Trusted by teams at
  [logo] [logo] [logo] [logo] [logo]
─────────────────────────────────────
```
All logos same size, grayscale or single-tint.

### S2. Stat Row (no logos)
```
─────────────────────────────────────
  47.2%        12,400        $99
  faster       teams         /month
─────────────────────────────────────
```
Real numbers (no 99.99% / 10x / 1M+).

## Features Archetypes

### F1. Zig-Zag (asymmetric editorial)
```
[ICON] Headline               [IMAGE]
       Body text 2-3 lines

[IMAGE]               [ICON] Headline
                             Body

[ICON] Headline               [IMAGE]
       Body
```
Best for: editorial, organic, hand-crafted

### F2. Bento Grid (3-2 mix)
```
┌──────────┬───────────┬──────────┐
│ Big      │ Med       │ Med      │
│ feature  │ feature   │ feature  │
│ tile     │ tile      │ tile     │
├──────────┴─────┬─────┴──────────┤
│ Wide feature   │ Tall feature   │
│ tile           │ tile           │
└────────────────┴────────────────┘
```
Best for: minimal, glass-tech (with translucent surfaces)

### F3. Single-Feature Scroll Stops
```
┌─────────────────────────────────────┐
│  [Feature 1 — full viewport]        │
│  Big visual + headline + body       │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│  [Feature 2 — full viewport]        │
│  ...                                │
└─────────────────────────────────────┘
```
Best for: atmospheric, luxury, retro-futuristic

### F4. Brutalist Stacked Cards
```
┌─────────┬─────────┬─────────┬─────────┐
│ [icon]  │ [icon]  │ [icon]  │ [icon]  │
│ Head    │ Head    │ Head    │ Head    │
│ ─────   │ ─────   │ ─────   │ ─────   │
│ Body    │ Body    │ Body    │ Body    │
└─────────┴─────────┴─────────┴─────────┘
```
2px borders, no shadows, monospace numerics.

## How It Works Archetypes

### H1. Horizontal 3-Step
```
[01]──→──[02]──→──[03]
Title    Title    Title
Body     Body     Body
```
Custom connectors (NOT generic arrows).

### H2. Vertical Numbered
```
01 │ Headline of step
   │ Body text
   │
02 │ Headline
   │ Body
   │
03 │ Headline
   │ Body
```
Best for: editorial, hand-crafted

### H3. Animated Diagram
```
[Visual flow diagram showing user path]
[Animates on scroll into view]
```
Best for: glass-tech, retro-futuristic

## Testimonials Archetypes

### T1. Single Rotating Pull-Quote
```
"           [Avatar]
  Specific outcome quote
  in 2-3 lines, generous size.
                               "
                — Name, Role @ Company
```
Best for: editorial, luxury, atmospheric

### T2. Masonry Wall
```
┌───────┐ ┌─────┐ ┌──────────┐
│ Quote │ │Quote│ │  Quote   │
│       │ │     │ │          │
└───────┘ │     │ └──────────┘
┌──────┐  │     │  ┌─────┐
│Quote │  └─────┘  │Quote│
└──────┘           └─────┘
```
Variable card heights. Best for: minimal, brutalist.

### T3. Magazine Spread
```
┌──────────────────┬──────────────────┐
│ "Pull quote in   │  [Portrait       │
│  large display    │   photograph]    │
│  type"            │                  │
│                  │                  │
│  Body of testimonial             │  │
│  with specific outcome.            │ │
│                                    │ │
│  — Name                            │ │
│    Role @ Company                  │ │
└──────────────────┴──────────────────┘
```
Best for: editorial, hand-crafted

## FAQ Archetypes

### Q1. Single-Open Accordion
```
▼ Real question someone asked?
  Direct answer in 2-3 sentences.

▶ Another question?

▶ Another question?
```

### Q2. Static 2-Col (no accordion)
```
Q: Question?              Q: Question?
A: Answer.                A: Answer.

Q: Question?              Q: Question?
A: Answer.                A: Answer.
```
Best for: minimal vibe (avoids interaction overhead).

## CTA Archetypes

### C1. Bold Restatement
```
─────────────────────────────────────
   Restated value proposition,
   slightly different wording from H1.

   [Primary CTA]        [Secondary]
─────────────────────────────────────
```

### C2. Form-Inline (Waitlist / Newsletter)
```
   Get notified when we launch.
   ┌─────────────────────────┐
   │ email@example.com       │  [Submit]
   └─────────────────────────┘
   No spam. Unsubscribe anytime.
```

### C3. Visual Echo of Hero
```
[Same hero composition, simplified]
  [H2 echoing hero promise]
  [CTA (same as hero CTA)]
```
Best for: atmospheric, luxury — creates visual bookend.

## Footer Archetypes

### F1. Generous Editorial Footer
```
─────────────────────────────────────
  [Logo + tagline]

  Product       Company       Legal
  ─────         ─────         ─────
  Features      About         Terms
  Pricing       Blog          Privacy
  Docs          Careers
                Contact

  [Social: 3-5 custom icons]
  © 2026 — All rights reserved
─────────────────────────────────────
```

### F2. Minimal Footer
```
─────────────────────────────────────
  © 2026 ProductName     Privacy · Terms
─────────────────────────────────────
```
For when legal nav lives in /legal.

## Picking Archetypes by Vibe

| Vibe | Hero | Features | Testimonials | Footer |
|------|------|----------|--------------|--------|
| Minimal | A2 | F2 (Bento) | T2 (Masonry) | F2 |
| Editorial | A1 | F1 (Zig-zag) | T3 (Spread) | F1 |
| Brutalist | A3 | F4 (Stacked) | T2 (Masonry) | F1 |
| Retro-futuristic | A4 | F3 (Scroll) | T1 (Rotating) | F1 |
| Organic | A1 | F1 (Zig-zag) | T1 (Rotating) | F1 |
| Luxury | A4 | F3 (Scroll) | T3 (Spread) | F1 |
| Playful | A1 | F2 (Bento) | T2 (Masonry) | F1 |
| Industrial | A3 | F4 (Stacked) | T2 (Masonry) | F1 |
| Glass-tech | A4 | F2 (Bento) | T1 (Rotating) | F1 |
| Hand-crafted | A1 | F1 (Zig-zag) | T3 (Spread) | F1 |
