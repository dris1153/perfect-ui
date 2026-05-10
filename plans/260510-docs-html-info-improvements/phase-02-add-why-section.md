# Phase 02 — Add "Why it exists" section

## Context links
- [brainstorm.md § 01 Why it exists](./brainstorm.md)
- Source data: [synthesis.md](../260509-ai-vs-human-analysis/synthesis.md)
- Target: [index.html](../../index.html)

## Overview
- **Priority:** High (most load-bearing addition for general-visitor audience)
- **Status:** pending
- **Effort:** M (~30 minutes)
- **Description:** Insert new "Why it exists" section after Hero (before existing Scope section). Contains 4-stat row + side-by-side AI-vs-human comparison panel.

## Key insights
- Stats row reuses Hero `.stat-num` / `.stat-label` styles — NO new CSS for stats.
- Comparison panel follows existing `.scope-grid` 2-col pattern — minimal new CSS.
- Section becomes new "01" — Scope renumbers to "02" in phase 06.

## Requirements
- Functional: visually distinct from Hero (border-top divider) but cohesive (same palette, type, spatial language).
- Non-functional: no new font imports, no new accent tokens, mobile-stacks at <900px.

## Architecture
**Insertion point:** Immediately after closing `</section>` of `.hero` (after line 404), before opening `<section aria-label="Scope">` (line 407).

**Component breakdown:**
- `.sec-head` block — label / heading / sec-meta (existing pattern)
- `.why-stats` row (4 stats) — reuse Hero stat styling
- `.why-compare` panel (2 cols) — new minimal CSS

## Related code files
- **Modify:** `d:\Workspace\dris1153\Personal\claude-skills\perfect-ui\index.html`
  - Add ~80 lines HTML inside `<div class="container">`
  - Add ~30 lines CSS inside existing `<style>` block (just for `.why-compare`)

## Implementation steps

### 1. Add CSS for comparison panel
**Location:** Inside `<style>` block, after `/* SCOPE */` rules (~line 184), before `/* PIPELINE */` (~line 185).

```css
/* WHY (comparison) */
.why-stats { grid-column: 1 / span 12; display: grid; grid-template-columns: repeat(4, 1fr); gap: 32px; border-top: 1px solid var(--rule); border-bottom: 1px solid var(--rule); padding: 32px 0; margin-bottom: 56px; }
.why-stats .stat-num { font-size: 48px; }
.why-compare { grid-column: 1 / span 12; display: grid; grid-template-columns: 1fr 1px 1fr; gap: 0 64px; align-items: start; }
.why-compare-rule { background: var(--rule); width: 1px; align-self: stretch; position: relative; }
.why-compare-rule::before { content: ''; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); width: 6px; height: 6px; background: var(--accent); border-radius: 50%; }
.why-col h3 { font-size: 20px; margin-bottom: 20px; font-style: italic; }
.why-col-ai h3 { color: var(--ink-muted); }
.why-col ul { list-style: none; padding: 0; margin: 0; }
.why-col li { padding: 10px 0; border-bottom: 1px solid var(--rule); font-size: 14px; line-height: 1.5; }
.why-col li:last-child { border-bottom: none; }
.why-col-ai li { color: var(--ink-muted); font-family: var(--font-mono); font-size: 13px; }
.why-col-human li { color: var(--ink); }
.why-close { grid-column: 1 / span 12; margin-top: 48px; font-size: 16px; color: var(--ink-muted); font-style: italic; max-width: 60ch; }
```

**Mobile (add to existing `@media (max-width: 900px)` block ~line 343):**
```css
.why-stats { grid-template-columns: repeat(2, 1fr); }
.why-compare { grid-template-columns: 1fr; }
.why-compare-rule { display: none; }
```

### 2. Add HTML section
**Location:** After line 404 (end of `.hero` section), before `<!-- SCOPE -->` (line 406).

```html
  <!-- WHY -->
  <section aria-label="Why it exists">
    <div class="grid-12">
      <div class="sec-head">
        <span class="label">— Why</span>
        <h2><em>Made because</em> AI pages stack defaults.</h2>
        <span class="sec-meta">plans/260509-ai-vs-human-analysis/synthesis.md</span>
      </div>

      <div class="why-stats">
        <div>
          <div class="stat-num">12</div>
          <div class="stat-label">Landings analyzed</div>
        </div>
        <div>
          <div class="stat-num">5</div>
          <div class="stat-label">AI-generated</div>
        </div>
        <div>
          <div class="stat-num">7</div>
          <div class="stat-label">Human-crafted</div>
        </div>
        <div>
          <div class="stat-num">10+</div>
          <div class="stat-label">Violations stacked / AI page</div>
        </div>
      </div>

      <div class="why-compare">
        <div class="why-col why-col-ai">
          <h3>AI defaults — stacked</h3>
          <ul>
            <li>Inter font alone</li>
            <li>Purple/blue gradient hero</li>
            <li><code>h-screen</code> everywhere</li>
            <li><code>lucide-react</code> icons</li>
            <li>3-col equal feature grid</li>
            <li>"Get Started" CTAs</li>
            <li>Round fake stats (10K+, 99.99%)</li>
            <li>Fade-up on every element</li>
          </ul>
        </div>

        <div class="why-compare-rule" aria-hidden="true"></div>

        <div class="why-col why-col-human">
          <h3>Human commitment — singular</h3>
          <ul>
            <li>One vibe locked end-to-end</li>
            <li>Custom SVG icon set</li>
            <li>Asymmetric editorial grid</li>
            <li>Vibe-paired typography</li>
            <li>Distinctive display fonts</li>
            <li>Specific draft copy</li>
            <li>Real evidence-based stats</li>
            <li>Vibe-scaled motion intensity</li>
          </ul>
        </div>
      </div>

      <p class="why-close">Cohesion is the multiplier on craft. This skill encodes that as enforceable rules.</p>
    </div>
  </section>
```

## Todo list
- [ ] Add CSS rules for `.why-stats`, `.why-compare`, `.why-compare-rule`, `.why-col`, `.why-close`
- [ ] Add mobile overrides in existing media query
- [ ] Insert HTML section after Hero
- [ ] Smoke test desktop — stats row + 2-col comparison render correctly
- [ ] Smoke test mobile (<900px) — stacks to single col, accent dot hidden
- [ ] Verify no AI-slop self-violation (the listed AI defaults are RECEPTION of patterns, not USE — OK)

## Success criteria
- [ ] Section renders between Hero and Scope
- [ ] Stat numbers `12 / 5 / 7 / 10+` visible at desktop + mobile
- [ ] Right column (Human) feels visually weightier than Left (AI) — intentional hierarchy
- [ ] Vertical accent rule between columns (desktop only)
- [ ] Closing line italic, ink-muted
- [ ] No new fonts loaded, no new color tokens introduced
- [ ] Mobile renders without horizontal scroll

## Risk assessment
| Risk | Severity | Mitigation |
|---|---|---|
| AI-defaults list reads as endorsement | Medium | Section heading "Made because AI pages stack defaults" + ink-muted styling clearly mark these as anti-patterns |
| `<code>` inside `.why-col-ai li` triggers grep audit (e.g., `lucide-react` literal in source) | Medium | Acceptable — appears in QUOTED context (anti-pattern listing). Anti-slop audit is for IMPORTED libs, not documented forbidden patterns. Brainstorm self-document section already has same content pattern. |
| Comparison panel breaks on tablet 700-900px | Low | Existing `.scope-grid` uses same breakpoint, validated pattern |
| Section number "Why" non-numeric breaks visual rhythm | Low | Intentional — narrative section vs mechanical sections. Other approach: number it "00" but breaks Pipeline's "00" phase already used. Keep "— Why" |

## Security considerations
N/A — static content.

## Next steps
- Phase 03 — Mandates section (after Anti-slop tier section, before Getting Started).
