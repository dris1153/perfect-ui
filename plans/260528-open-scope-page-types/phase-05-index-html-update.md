# Phase 05 — index.html update

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Files modified > index.html
- [phase-03-skill-md-scope-update.md](./phase-03-skill-md-scope-update.md) — depends on (for scope consistency)
- [260510-docs-html-info-improvements/plan.md](../260510-docs-html-info-improvements/plan.md) — prior plan that built current index.html structure (completed)
- [index.html](../../index.html) — file to modify (1243 lines, 9 sections)
- [260510-docs-html-info-improvements/phase-04-add-examples-section-tabs.md](../260510-docs-html-info-improvements/phase-04-add-examples-section-tabs.md) — for tab structure pattern reference

## Overview
- **Priority:** Medium (published docs page — visual face of skill)
- **Status:** pending
- **Depends on:** Phase 03 (scope decisions locked in SKILL.md)
- **Parallel-safe with:** Phase 04 (README — different file)
- **Description:** Rewrite §02 Scope card content for 2-tier matrix; add 1 non-marketing tab to §07 In practice; reduce §09 Beyond to compact 3-row routing table; bump version 2.0.0 → 2.1.0 in hero + footer.

## Key insights
- index.html has editorial vibe + ARIA tabs + cream/ink/dusk-rose palette — preserve cohesion
- Anti-slop self-audit applies to this very file — no emoji, no Inter/Roboto, no purple gradient, no `h-screen`
- §07 tab structure uses `role="tab"` + `role="tabpanel"` + `aria-controls` + `aria-selected` + keyboard nav (Arrow/Home/End) — new tab must follow this contract
- §09 Beyond currently has 5 rows (after 260510 plan); will reduce to ~3 rows
- No new fonts, no new accent colors (per prior plan's cohesion guardrails)
- Version mentions: hero (likely h1 area) + footer (line ~1066 area per prior plan)

## Requirements

### Functional
- §02 Scope: replace refusal-style content with 2-tier matrix card (Special vs Generic)
- §07 In practice: add 1 new tab "Blog / non-marketing" demonstrating generic-tier example
- §09 Beyond: reduce to 3 routing cases where another skill is genuinely better (ck:frontend-development for deep app architecture, ck:shopify for full Shopify backend, ck:frontend-design for exact screenshot replication)
- Version bump 2.0.0 → 2.1.0 in 2 locations (hero + footer)

### Non-functional
- ARIA tab contract preserved (role, aria-selected, aria-controls, keyboard nav)
- No-JS fallback preserved (`.no-js` class strategy — all panels visible without JS)
- No new fonts (use existing Instrument Serif + Geist + Geist Mono)
- No new accent colors (cream + ink + dusk-rose only)
- Section count remains 9 (no add/remove sections, just internal content changes)
- File size change: net +50 to +100 lines (additive: +1 tab + tab panel; subtractive: §09 trimmed; rewrites neutral)

## Architecture

### §02 Scope — new card content
**Current** (per prior plan synthesis): Likely a card listing "What it handles" + "Explicit refusals"

**New structure:**
```html
<section id="scope" class="section">
  <div class="section-num">02</div>
  <h2>Scope</h2>
  <p>Applies to any web page output. Two tiers based on `--type`:</p>

  <div class="scope-tier-grid"> <!-- 2-col on desktop, stack on mobile -->
    <div class="scope-tier">
      <h3>Special tier</h3>
      <p><code>landing</code>, <code>portfolio</code></p>
      <ul>
        <li>Rich anatomy per type</li>
        <li>Section archetypes per vibe</li>
        <li>Full Tier 1/2/3 anti-slop audit</li>
        <li>Evidence-backed (12 landings analyzed)</li>
      </ul>
    </div>
    <div class="scope-tier">
      <h3>Generic tier</h3>
      <p>any other type — blog, about, pricing, contact, coming-soon, dashboard, admin, e-commerce, custom</p>
      <ul>
        <li>Generic anatomy + skeleton</li>
        <li>Page-purpose drives sections</li>
        <li>Universal anti-slop subset</li>
        <li>Best-effort craft (evidence base partial for app-surface types)</li>
      </ul>
    </div>
  </div>

  <p class="muted">No refusals. Universal toolkit (vibe + palette + typography + custom icons + 2D illustrations + motion) applies to both tiers.</p>
</section>
```

Use existing card class conventions (`.section`, `.section-num`, `<h2>`, `<h3>`). New CSS class `.scope-tier-grid` (2-col) and `.scope-tier` (card) — keep minimal, reuse existing color tokens.

### §07 In practice — add new tab
**Current:** 3 tabs (coffee landing, portfolio redesign, dashboard refused)

**Change:**
- Keep tab 1 (coffee landing)
- Keep tab 2 (portfolio redesign)
- **Rewrite tab 3:** Was "dashboard refused" — now "Blog page (generic tier)" — match README Example 3
- **Add tab 4:** "Dashboard (generic tier with disclosure)" — match README Example 4

**Tab list structure:**
```html
<div role="tablist" aria-label="Examples">
  <button role="tab" id="tab-1" aria-controls="panel-1" aria-selected="true">Coffee landing</button>
  <button role="tab" id="tab-2" aria-controls="panel-2" aria-selected="false">Portfolio redesign</button>
  <button role="tab" id="tab-3" aria-controls="panel-3" aria-selected="false">Blog page</button>
  <button role="tab" id="tab-4" aria-controls="panel-4" aria-selected="false">Dashboard</button>
</div>
```

Each panel uses existing `<article role="tabpanel" id="panel-N" aria-labelledby="tab-N">` structure.

Panel 3 (Blog) and Panel 4 (Dashboard) content: condensed version of README Example 3 + Example 4 — 8-10 line summary, not full numbered flow (per existing tab brevity).

### §09 Beyond perfect-ui — reduce
**Current** (per prior plan): 5-row routing table

**New: 3 rows max:**
```html
<section id="beyond" class="section">
  <div class="section-num">09</div>
  <h2>Beyond perfect-ui</h2>
  <p>For these specific cases, another skill is genuinely a better fit. perfect-ui doesn't refuse these — it suggests:</p>

  <table>
    <thead>
      <tr><th>Need</th><th>Better fit</th></tr>
    </thead>
    <tbody>
      <tr><td>Full app architecture, complex multi-page IA</td><td><code>ck:frontend-development</code></td></tr>
      <tr><td>Full Shopify backend (products, cart, checkout)</td><td><code>ck:shopify</code></td></tr>
      <tr><td>Exact design replication from screenshot</td><td><code>ck:frontend-design</code></td></tr>
    </tbody>
  </table>

  <p class="muted">perfect-ui still handles the visible page surface (landing for SaaS, storefront homepage, marketing pages of any app) — these are companion skills, not replacements.</p>
</section>
```

### Version bump
- Hero version (top of body, prob in header area): `v2.0.0` → `v2.1.0`
- Footer version (per prior plan, line ~1066): `v2.0.0` → `v2.1.0`

### Anti-slop self-audit (final check)
- grep `lucide`, `heroicons`, `phosphor` → 0 matches
- grep `Inter`, `Roboto`, `Arial` as font-family → 0 matches (Geist + Instrument Serif only)
- grep `h-screen` → 0 matches (use `min-h-[100dvh]` or similar)
- grep emoji unicode ranges → 0 matches
- grep `from-purple-` `to-blue-` → 0 matches
- grep raw hex colors outside CSS custom property defs → 0 matches

## Related code files

**Modify:**
- `index.html`
  - Hero version mention
  - §02 Scope — content rewrite
  - §07 In practice — replace tab 3 content + add tab 4 (tablist + tabpanel)
  - §09 Beyond — reduce to 3-row table
  - Footer version mention
  - (Optional) Add 2 new CSS classes `.scope-tier-grid` and `.scope-tier` if not reusing existing

**Create:** None
**Delete:** Existing §02 refusal content; existing §07 tab 3 (dashboard refused) content; §09 rows beyond top 3

## Implementation steps

1. **Read `index.html`** to locate exact line ranges:
   - Hero version
   - §02 Scope section
   - §07 In practice tablist + panels
   - §09 Beyond table
   - Footer version
   - Existing CSS classes used by scope card (for reuse)

2. **Bump hero version** → v2.1.0

3. **Rewrite §02 Scope** content per Architecture above
   - Add 2 new CSS classes if needed (`.scope-tier-grid` 2-col, `.scope-tier`)
   - Use existing color tokens (cream bg, ink text, dusk-rose accent)

4. **Update §07 In practice:**
   - Find existing 3 tabs (tablist + 3 panels)
   - Rewrite tab 3 button label: "Dashboard refused" → "Blog page"
   - Rewrite panel 3 content: README Example 3 (blog) condensed
   - Add 4th tab button: "Dashboard"
   - Add 4th panel: README Example 4 (dashboard) condensed
   - Verify ARIA: 4 tabs, 4 panels, aria-controls/aria-labelledby paired correctly
   - Verify keyboard nav JS handles 4 tabs (existing JS should — it loops over all `[role="tab"]`)

5. **Reduce §09 Beyond** to 3-row table per Architecture above

6. **Bump footer version** → v2.1.0

7. **Anti-slop self-audit** — run grep checks listed in Architecture; fix any violations

8. **No-JS validation** — confirm `.no-js` strategy still works (all 4 panels visible when class present)

9. **Section count check** — confirm 9 sections still (no add/remove)

## Todo list
- [ ] Read index.html, locate line ranges
- [ ] Bump hero version
- [ ] Rewrite §02 Scope content
- [ ] Add CSS for scope-tier-grid (if needed)
- [ ] Rewrite §07 tab 3 (Blog) panel content
- [ ] Add §07 tab 4 (Dashboard) button + panel
- [ ] Reduce §09 Beyond to 3 rows
- [ ] Bump footer version
- [ ] Run anti-slop self-audit greps
- [ ] No-JS strategy verify
- [ ] Final section count check (= 9)

## Success criteria
- Hero + footer version = v2.1.0
- §02 has 2-tier scope card (Special vs Generic); no refusal language
- §07 has 4 tabs (Coffee landing, Portfolio redesign, Blog page, Dashboard)
- §09 Beyond has exactly 3 rows
- All ARIA tab contracts intact (role, aria-selected, aria-controls, aria-labelledby)
- No-JS fallback: all 4 panels show when `.no-js` present
- Anti-slop self-audit: 0 violations (no lucide/heroicons/phosphor, no Inter/Roboto as font, no h-screen, no emoji, no purple-blue gradient, no inline hex outside CSS vars)
- Section count = 9 (unchanged)
- Net line change: +50 to +100 lines

## Risk assessment
- **Risk:** New tab CSS/JS breaks tab keyboard nav → existing JS loops `[role="tab"]` — 4 tabs auto-supported. Verify with Arrow keys.
- **Risk:** Scope tier card needs new CSS — add minimal classes, no new tokens
- **Risk:** Dashboard tab content includes "evidence base partial" disclosure → use existing typography styles for note (muted variant), no new color
- **Risk:** §09 reduction may strand orphan content → confirm 2 deleted rows didn't have unique info worth preserving elsewhere

## Security considerations
None — static HTML edits.

## Next steps
- After Phase 04 + 05 complete: final cross-file consistency check (SKILL.md ↔ README ↔ index.html scope language)
- Run `python ~/.claude/skills/skill-creator/scripts/quick_validate.py` per README contributing section
- Optional: visual diff index.html before/after to confirm layout integrity
