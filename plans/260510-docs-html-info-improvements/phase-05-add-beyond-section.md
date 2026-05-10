# Phase 05 — Add "Beyond perfect-ui" section

## Context links
- [brainstorm.md § 09 Beyond perfect-ui](./brainstorm.md)
- Source: [README.md § Related Skills](../../README.md)
- Target: [index.html](../../index.html)

## Overview
- **Priority:** Medium (helps user self-route to right skill)
- **Status:** pending
- **Effort:** S (~20 minutes)
- **Description:** Insert new "Beyond perfect-ui" section before footer. 5-row table mapping needs → alternative skills.

## Key insights
- Last new section. Functions as exit ramp before footer.
- Flat table — no interactivity, no complex layout. Reuse table styling from `.vibe-row` if needed.
- Section becomes new "09".

## Requirements
- Functional: clearly maps "if you need X → use Y skill".
- Non-functional: scannable in <30 seconds; mono-styled skill names.

## Architecture
**Insertion point:** After closing `</section>` of Getting Started section (~line 765), before `<footer>` (~line 768).

**Component breakdown:**
- `.sec-head` — label / heading / sec-meta
- `.beyond-table` — 5 rows, 2 cols (need / skill)

## Related code files
- **Modify:** `d:\Workspace\dris1153\Personal\claude-skills\perfect-ui\index.html`
  - Add ~50 lines HTML
  - Add ~25 lines CSS

## Implementation steps

### 1. Add CSS for beyond table
**Location:** Inside `<style>` block, after `/* GETTING STARTED */` rules (~line 320), before `/* FOOTER */` (~line 322).

```css
/* BEYOND */
.beyond { grid-column: 1 / span 12; }
.beyond-row {
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 32px;
  padding: 24px 0;
  border-bottom: 1px solid var(--rule);
  align-items: baseline;
}
.beyond-row:first-child {
  border-top: 1px solid var(--ink);
  border-bottom: 1px solid var(--ink);
  font-family: var(--font-mono);
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  color: var(--ink-muted);
  padding: 12px 0;
}
.beyond-need { font-size: 16px; line-height: 1.4; }
.beyond-skill {
  font-family: var(--font-mono);
  font-size: 14px;
  color: var(--ink);
}
.beyond-skill code {
  background: var(--bg-muted);
  padding: 4px 10px;
  border-radius: 0;
  border-left: 2px solid var(--accent);
  font-size: 13px;
}
```

**Mobile (add to existing `@media (max-width: 900px)`):**
```css
.beyond-row { grid-template-columns: 1fr; gap: 8px; padding: 20px 0; }
.beyond-row:first-child { display: none; }
```

### 2. Add HTML section
**Location:** After Getting Started section (~line 765), before `<footer>` (~line 768).

```html
  <!-- BEYOND -->
  <section aria-label="Beyond perfect-ui — when to use other skills">
    <div class="grid-12">
      <div class="sec-head">
        <span class="label">— 09</span>
        <h2><em>Beyond.</em> Where to go when this isn't the fit.</h2>
        <span class="sec-meta">README.md § Related Skills</span>
      </div>

      <div class="beyond">
        <div class="beyond-row">
          <div>If you need</div>
          <div>Use instead</div>
        </div>

        <div class="beyond-row">
          <div class="beyond-need">Full apps, dashboards, admin panels, complex multi-page IA</div>
          <div class="beyond-skill"><code>ck:frontend-development</code></div>
        </div>

        <div class="beyond-row">
          <div class="beyond-need">Replicate exact design from screenshot or video</div>
          <div class="beyond-skill"><code>ck:frontend-design</code></div>
        </div>

        <div class="beyond-row">
          <div class="beyond-need">Component-level UI work in existing apps</div>
          <div class="beyond-skill"><code>ck:ui-ux-pro-max</code></div>
        </div>

        <div class="beyond-row">
          <div class="beyond-need">E-commerce stores</div>
          <div class="beyond-skill"><code>ck:shopify</code></div>
        </div>

        <div class="beyond-row">
          <div class="beyond-need">Logo / CIP / banner / social-photo design (called by perfect-ui internally for icons)</div>
          <div class="beyond-skill"><code>ckm:design</code></div>
        </div>
      </div>
    </div>
  </section>
```

## Todo list
- [ ] Add CSS for `.beyond`, `.beyond-row`, `.beyond-need`, `.beyond-skill`
- [ ] Add mobile overrides
- [ ] Insert HTML section after Getting Started, before Footer
- [ ] Smoke test desktop — 2-col table renders correctly
- [ ] Smoke test mobile — stacks to single column, header row hidden

## Success criteria
- [ ] Section renders between Getting Started and Footer
- [ ] All 5 rows visible with header row at top
- [ ] Skill names code-styled with accent left-rule
- [ ] Header row uses mono uppercase pattern (matches `.vibe-row:first-child`)
- [ ] Mobile: stacks cleanly, header row hidden
- [ ] No new fonts, no new tokens

## Risk assessment
| Risk | Severity | Mitigation |
|---|---|---|
| Visual similarity to Vibes table feels redundant | Low | Different content scope; positioned at end of page where Vibes is mid-page; intentional pattern reuse for cohesion |
| Skill names with `ck:` prefix break grep audits expecting bare imports | Low | These are skill INVOCATION names, not JS imports. Anti-slop audit greps for actual library imports (`from 'lucide-react'`), not text mentions. |
| Long need-text wraps awkwardly | Low | `line-height: 1.4` + `max-width` via grid col allocation handles wrap |

## Security considerations
N/A.

## Next steps
- Phase 06 — Section number cascade + final audit (last phase).
