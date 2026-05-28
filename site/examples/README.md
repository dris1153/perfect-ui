# Examples

Real output samples from `perfect-ui` runs. Each file demonstrates a single skill output — vibe, palette, typography, custom icons, motion intensity locked end-to-end.

## Files

- [`coffee-landing.html`](coffee-landing.html) — landing page, **editorial vibe** + agrarian wildcard. Subscription coffee service in Kyoto. Custom SVG icons (chair / envelope / pot / clock), silkscreen-style hero illustration, motion intensity 2/3 (GSAP scroll reveals + masked-line hero entrance), **Tier 3-4 Lenis** (v2.5.1+ type-gate rule — landing/portfolio auto-Lenis regardless of vibe; editorial config lerp 0.1 for restrained-but-premium feel + GSAP ticker sync).

- [`luxury-landing.html`](luxury-landing.html) — landing page, **luxury vibe**. Heritage perfumery (Maison Lumière) with 12-year aging premise. Custom SVG icons (leaf / amphora / vial / envelope) + ornate bottle hero illustration with botanical filigree. Cormorant Garamond + Cormorant (Vietnamese subset). Dark theme (ink #0E0E0C + cream + gold accent). **Tier 3-4 Lenis demo** with verbose copy-paste setup (luxury config lerp 0.08 for ultra-premium; hard guards + Lenis init + GSAP ticker sync + anchor routing — all commented for skill users to learn the pattern).

Both examples now demonstrate the same smooth-scroll setup, tuned per vibe (editorial lerp 0.1, luxury lerp 0.08). This reflects v2.5.1+ rule: landing/portfolio always get Lenis regardless of vibe.

## How to add a new example

1. Create a new file `<vibe>-<type>.html`.
2. Link the project tokens via `<link rel="stylesheet" href="../css/tokens.css">` — every example shares the same token names but overrides palette per vibe.
3. Add a watermark banner at the top: `Example output · <vibe> vibe · <product>`.
4. Link back to `../index.html` in the banner.
5. Keep file under 600 lines. Examples are illustrative, not full production pages.
