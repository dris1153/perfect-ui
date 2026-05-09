# Section Archetypes

Reusable section layouts. Pick by vibe + section type. Adapt to locked palette/typography from `visual-direction.md`. Sections are organized by **type** (landing | portfolio).

---

# LANDING-TYPE ARCHETYPES

For landing pages. See `landing-anatomy.md` for which sections to include and in what order.

## Hero Archetypes (landing)

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

## Picking Landing Archetypes by Vibe

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

---

# PORTFOLIO-TYPE ARCHETYPES

For portfolios. See `portfolio-anatomy.md` for which sections to include and in what order.

## Hero Archetypes (portfolio)

### PA1. Display Name + Craft (asymmetric)
```
┌─────────────────────────────────────┐
│  [DISPLAY NAME                      │
│   line break possible]              │
│                                     │
│  [Subheadline: specific craft]      │
│                                     │
│  ─────────────────                  │
│  Brooklyn, NY                       │
│  ● Available from June 2026         │
└─────────────────────────────────────┘
```
Best for: editorial, hand-crafted, organic, luxury

### PA2. Featured-Project-as-Hero
```
┌─────────────────────────────────────┐
│  [LARGE FEATURED PROJECT IMAGE]     │
│  [full-bleed, 70-80% of viewport]   │
│                                     │
│  Name · Specific craft              │
│  Project title · Year · Client      │
└─────────────────────────────────────┘
```
Best for: photographers, brand designers, architects — when the work IS the intro
**Anti-pattern check:** Don't pick this if your strongest project is mediocre

### PA3. Monogram + Minimal Type
```
┌─────────────────────────────────────┐
│                                     │
│              [SC]                   │
│           [monogram]                │
│                                     │
│      [Display Name]                 │
│      [Specific craft]               │
│                                     │
└─────────────────────────────────────┘
```
Best for: minimal, luxury — only when DESIGN_VARIANCE ≤ 4

### PA4. Brutalist Type-First
```
┌─────────────────────────────────────┐
│ NAME                                │
│ ─────────────────────────────────── │
│ I {VERB} {SPECIFIC OUTCOME}.        │
│ {YEARS} YEARS · {CITY} · {STATUS}   │
│                                     │
│ ▌ View work  ▌ Email                │
└─────────────────────────────────────┘
```
Best for: brutalist, industrial, retro-futuristic

## Work Grid Archetypes (portfolio)

### PW1. Bento (mixed sizes, featured prominent)
```
┌─────────────────┬───────────────┐
│                 │               │
│  FEATURED       │   PROJECT     │
│  PROJECT        │               │
│  (large)        ├───────────────┤
│                 │   PROJECT     │
├─────────────────┴───────────────┤
│  PROJECT  │  PROJECT  │ PROJECT │
└───────────┴───────────┴─────────┘
```
Best for: editorial, hand-crafted, mixed-discipline portfolios

### PW2. Uniform Grid (process-led work)
```
┌─────────┬─────────┬─────────┐
│ project │ project │ project │
│ + meta  │ + meta  │ + meta  │
├─────────┼─────────┼─────────┤
│ project │ project │ project │
│ + meta  │ + meta  │ + meta  │
└─────────┴─────────┴─────────┘
```
Best for: product designers, UX — consistency conveys process

### PW3. Single Full-Width per Project (scroll reveal)
```
┌─────────────────────────────────────┐
│  [HUGE PROJECT IMAGE]               │
│  Title · Year · Client              │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│  [HUGE PROJECT IMAGE]               │
│  Title · Year · Client              │
└─────────────────────────────────────┘
```
Best for: photographers, architects, fine artists — work needs space

### PW4. List View (text-led)
```
─────────────────────────────────────
2025 │ Project Title           [thumb]
     │ Client · 1-line context        →
─────────────────────────────────────
2024 │ Project Title           [thumb]
     │ Client · 1-line context        →
─────────────────────────────────────
```
Best for: writers, strategists, hand-crafted, editorial

### PW5. Masonry (variable heights)
```
┌────────┐┌─────────┐┌──────┐
│ proj   ││ project ││ proj │
│ tall   ││ medium  ││ shrt │
│        │└─────────┘└──────┘
│        │┌──────┐┌──────────┐
└────────┘│ proj ││ project  │
          │ shrt ││ wide     │
          └──────┘└──────────┘
```
Best for: visual-led work — illustrators, graphic designers

## Featured Case Study Archetypes

### PC1. Magazine Long-Form
```
┌─────────────────────────────────────┐
│  [HERO IMAGE OF FINAL WORK]         │
│                                     │
│  Project Title (display, large)     │
│  Client · Year · Role · Duration    │
│                                     │
│  [Body text of context, 2 paragraphs│
│  in 65ch reading width]             │
│                                     │
│  [Image 1] caption                  │
│  [Image 2] caption                  │
│  [Image 3] caption                  │
│                                     │
│  [Outcome statement, large]         │
└─────────────────────────────────────┘
```
Best for: editorial, hand-crafted

### PC2. Embedded Inline (collapsible)
```
On main portfolio page:
┌─────────────────────────────────────┐
│  [Project tile]                     │
│  ▼ Read case study                  │
└─────────────────────────────────────┘
Expanded:
┌─────────────────────────────────────┐
│  [Tile + body + 3 process images]   │
└─────────────────────────────────────┘
```
Best for: when you only have 1-2 deep dives

### PC3. Standalone Page (own URL)
Separate route at `/work/[slug]`. Allows full magazine treatment, links from work-grid tiles.

## About / Bio Archetypes

### PB1. Editorial Bio + Portrait
```
┌─────────────────────┬───────────────┐
│  [BIO PARAGRAPH]    │  [PORTRAIT    │
│                     │   editorial   │
│  [Client list]      │   3:4]        │
│                     │               │
│  [Press list]       │               │
└─────────────────────┴───────────────┘
```
Portrait optional — only if matches vibe

### PB2. Text-Only Long Bio
```
─────────────────────────────────────
  About

  [Bio paragraph 1 — current focus]
  [Bio paragraph 2 — career path]
  [Bio paragraph 3 — what I'm into]

  Selected clients: Oscar, Forward, ...
  Press: NYT, AIGA, ...
─────────────────────────────────────
```
Best for: minimal, hand-crafted

### PB3. Brutalist Stat Block
```
┌─────────────────────────────────────┐
│ NAME                                │
│ ROLE / SPECIALTY                    │
│ BASED IN: {CITY}                    │
│ AT: {COMPANY}                       │
│ YEARS IN PRACTICE: 8                │
│ LANGUAGES: EN, VI                   │
│ ─────────────────                   │
│ [Bio paragraph]                     │
└─────────────────────────────────────┘
```
Best for: brutalist, industrial

## Process Archetypes (portfolio, optional)

### PP1. Numbered Steps (vertical)
```
01 │ Listen and observe
   │ I start by sitting with users in real workflows...
   │
02 │ Frame the actual problem
   │ ...
   │
03 │ Build, ship, learn
   │ ...
```

### PP2. Card Grid (horizontal)
```
┌──────────┬──────────┬──────────┐
│ 01       │ 02       │ 03       │
│ Listen   │ Frame    │ Build    │
│ Body     │ Body     │ Body     │
└──────────┴──────────┴──────────┘
```

**Forbidden process patterns:**
- "Discover · Define · Develop · Deliver" — every agency
- Stock illustrations next to each step
- Circular process diagram with arrows

## Contact CTA Archetypes (portfolio)

### PCT1. Centered Big Type + Email
```
─────────────────────────────────────
       [contact-mark icon]

       AVAILABLE FROM JUNE 2026

   Write me at sarah@chen.studio
─────────────────────────────────────
```

### PCT2. Inline-Calm
```
─────────────────────────────────────
  For project inquiries:
  sarah@chen.studio

  Currently booking projects starting June 2026.
─────────────────────────────────────
```

**Forbidden contact patterns:**
- "Let's create magic together!"
- "Drop a line!"
- Contact form with 8+ required fields
- Calendly embed without context

## Picking Portfolio Archetypes by Vibe

| Vibe | Hero | Work Grid | Case Study | About | Contact |
|------|------|-----------|------------|-------|---------|
| Minimal | PA3 | PW2 | PC3 | PB2 | PCT2 |
| Editorial | PA1 | PW1 | PC1 | PB1 | PCT1 |
| Brutalist | PA4 | PW2 | PC3 | PB3 | PCT2 |
| Retro-futuristic | PA4 | PW1 | PC3 | PB3 | PCT1 |
| Organic | PA1 | PW5 | PC1 | PB1 | PCT2 |
| Luxury | PA3 | PW3 | PC1 | PB1 | PCT1 |
| Playful | PA1 | PW1 | PC2 | PB1 | PCT1 |
| Industrial | PA4 | PW2 | PC3 | PB3 | PCT2 |
| Glass-tech | PA2 | PW1 | PC3 | PB1 | PCT1 |
| Hand-crafted | PA1 | PW5 | PC1 | PB2 | PCT2 |
