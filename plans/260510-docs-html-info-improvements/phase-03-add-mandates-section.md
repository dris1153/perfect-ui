# Phase 03 — Add "Mandates" section

## Context links
- [brainstorm.md § 06 Mandates](./brainstorm.md)
- Source: [SKILL.md § Hard Rules](../../SKILL.md), [README.md § Hard Rules](../../README.md)
- Target: [index.html](../../index.html)

## Overview
- **Priority:** High (clarifies doctrine vs audit-pattern distinction)
- **Status:** pending
- **Effort:** M (~30 minutes)
- **Description:** Insert new "Mandates" section after Anti-slop tiers (before Getting Started). 8 hard rules as 4×2 card grid.

## Key insights
- Mandates = doctrine (MUST/MUST NOT). Anti-slop tiers = audit patterns. Different abstraction levels.
- Card grid reuses `.tier` border treatment with smaller padding — minimal new CSS.
- Section becomes new "06" — Getting Started renumbers to "08" in phase 06.

## Requirements
- Functional: visually distinct from Anti-slop (denser grid, smaller cards) but use same border/background tokens.
- Non-functional: 4×2 grid → 2×4 at tablet → 1×8 at mobile.

## Architecture
**Insertion point:** After closing `</section>` of Anti-slop section (after line 710), before `<!-- GETTING STARTED -->` (line 712).

**Component breakdown:**
- `.sec-head` with subheading paragraph clarifying doctrine vs audit
- `.mandates` 4×2 grid container
- 8x `.mandate` cards — number / headline (italic display) / 1-line clarification

## Related code files
- **Modify:** `d:\Workspace\dris1153\Personal\claude-skills\perfect-ui\index.html`
  - Add ~100 lines HTML
  - Add ~30 lines CSS

## Implementation steps

### 1. Add CSS for mandates grid
**Location:** Inside `<style>` block, after `/* ANTI-SLOP TIERS */` rules (~line 300), before `/* GETTING STARTED */` (~line 302).

```css
/* MANDATES */
.mandates-intro { grid-column: 1 / span 12; max-width: 60ch; margin-bottom: 40px; font-size: 15px; color: var(--ink-muted); line-height: 1.6; }
.mandates-intro strong { color: var(--ink); font-weight: 500; }
.mandates { grid-column: 1 / span 12; display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; }
.mandate {
  border: 1px solid var(--rule);
  padding: 24px;
  background: var(--bg);
  position: relative;
  transition: border-color 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.mandate:hover { border-color: var(--accent); }
.mandate-num {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--accent);
  letter-spacing: 0.15em;
}
.mandate h3 {
  font-size: 19px;
  margin: 10px 0 12px;
  font-style: italic;
  line-height: 1.15;
}
.mandate p {
  font-size: 13px;
  color: var(--ink-muted);
  line-height: 1.5;
}
```

**Mobile (add to existing `@media (max-width: 900px)`):**
```css
.mandates { grid-template-columns: 1fr 1fr; }
```

**At <600px (additional breakpoint, optional):**
```css
@media (max-width: 600px) {
  .mandates { grid-template-columns: 1fr; }
}
```

### 2. Add HTML section
**Location:** After line 710 (end of Anti-slop section), before `<!-- GETTING STARTED -->` (line 712).

```html
  <!-- MANDATES -->
  <section aria-label="Hard rule mandates">
    <div class="grid-12">
      <div class="sec-head">
        <span class="label">— 06</span>
        <h2><em>Eight mandates.</em> Non-negotiable.</h2>
        <span class="sec-meta">SKILL.md § Hard Rules</span>
      </div>

      <p class="mandates-intro">
        <strong>Mandates</strong> are doctrine — what the skill MUST and MUST NOT do. <strong>Anti-slop tiers</strong> above are audit patterns the skill greps for. Mandates are the <em>why</em> behind tier-1 patterns.
      </p>

      <div class="mandates">

        <div class="mandate">
          <span class="mandate-num">— 01</span>
          <h3>NO emoji — anywhere</h3>
          <p>Not in copy, headings, or as icons. Use a custom SVG instead.</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 02</span>
          <h3>NO icon libraries</h3>
          <p>Lucide, Heroicons, Phosphor, Tabler, Font Awesome, Material, react-icons — all forbidden.</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 03</span>
          <h3>NO AI slop defaults</h3>
          <p>Inter alone, purple/blue gradient hero, two equal CTAs, "Elevate / Seamless / Unleash" copy.</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 04</span>
          <h3>NO 3D models as hero</h3>
          <p>Static render → PNG OK. Real-time GLB forbidden (user-product GLB needs override).</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 05</span>
          <h3>3D = effects only</h3>
          <p>Phase 5 = shaders, particles, atmosphere. CSS first; WebGL only when CSS can't.</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 06</span>
          <h3>Always propose effect layer</h3>
          <p>Every site gets the proposal. User accepts or declines. Default = decline.</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 07</span>
          <h3>Vibe before pixels</h3>
          <p>Never write code or generate assets before vibe + palette + typography are locked.</p>
        </div>

        <div class="mandate">
          <span class="mandate-num">— 08</span>
          <h3>Type-aware everything</h3>
          <p>Phase 1 brief, plan, anatomy, skeleton — all branch by <code>--type</code>.</p>
        </div>

      </div>
    </div>
  </section>
```

## Todo list
- [ ] Add CSS for `.mandates`, `.mandate`, `.mandate-num`, `.mandates-intro`
- [ ] Add mobile overrides (2-col + optional 1-col at <600px)
- [ ] Insert HTML section after Anti-slop, before Getting Started
- [ ] Verify visual differentiation from Anti-slop tiers (denser grid, smaller cards)
- [ ] Smoke test desktop 4×2 grid + tablet 2×4 + mobile 1×8

## Success criteria
- [ ] Section renders between Anti-slop and Getting Started
- [ ] 8 mandate cards visible, numbered 01-08
- [ ] Card hover triggers accent border (matches existing `.phase` hover)
- [ ] Intro paragraph clearly differentiates Mandates from Anti-slop
- [ ] No emoji, no icon library refs in new content (self-audit)
- [ ] All 4 forbidden-pattern names in mandate-03 content (Inter, gradient, CTAs, copy phrases) appear in QUOTED context — not actual stylesheet usage

## Risk assessment
| Risk | Severity | Mitigation |
|---|---|---|
| Overlap với Anti-slop tier-1 cards feels redundant | High | Intro paragraph explicitly differentiates; smaller cards (24px padding vs 32px), denser grid (4-col vs 3-col) |
| Card grid dày đặc trông SaaS-y | Medium | Reuse exact `.tier` / `.phase` border + bg pattern — already validated as editorial-restrained |
| Mandate 03 listing forbidden words triggers self grep audit | Medium | Acceptable — quoted/anti-pattern context. Same as Anti-slop section already does. |
| 4-col grid stacks awkwardly at tablet (700-900px) | Low | Mobile breakpoint kicks in at 900px → 2-col. Validated. |

## Security considerations
N/A.

## Next steps
- Phase 04 — In practice section + interactive tabs JS.
