# Phase 04 — Add "In practice" section + tabs JS

## Context links
- [brainstorm.md § 07 In practice](./brainstorm.md)
- Source: [README.md § Examples](../../README.md)
- Target: [index.html](../../index.html)

## Overview
- **Priority:** Medium-High (concrete demonstrations of skill flow)
- **Status:** pending
- **Effort:** L (~60 minutes — most complex phase due to tabs JS + ARIA)
- **Description:** Insert new "In practice" section after Mandates. 3 worked examples in interactive tabs (vanilla JS, ARIA-compliant).

## Key insights
- Tabs MUST work without JS (graceful degradation: all 3 panels visible if JS fails).
- Editorial-restrained tab styling: monospace labels, accent bottom-rule on selected, no transitions on switch.
- Mobile: tabs stack to vertical pill list, panels stack below.
- Section becomes new "07" — Getting Started renumbers to "08", Beyond becomes "09" (in phase 06).

## Requirements
- Functional: tab switching via click + keyboard (Arrow Left/Right, Home, End).
- Functional: ARIA roles (`tablist`, `tab`, `tabpanel`, `aria-selected`, `aria-controls`).
- Non-functional: ~25 lines vanilla JS, no external libs.
- Non-functional: graceful no-JS fallback.

## Architecture
**Insertion point:** After closing `</section>` of Mandates section (added in phase 03), before `<!-- GETTING STARTED -->`.

**Component breakdown:**
- `.sec-head` — label / heading / sec-meta
- `.tabs-list` (role=tablist) — 3 tab buttons
- `.tabs-panels` — 3 tabpanel divs (1 visible at a time)
- `<script>` block at end of `<body>` — tab switching logic

## Related code files
- **Modify:** `d:\Workspace\dris1153\Personal\claude-skills\perfect-ui\index.html`
  - Add ~150 lines HTML
  - Add ~40 lines CSS
  - Add ~30 lines vanilla JS

## Implementation steps

### 1. Add CSS for tabs
**Location:** Inside `<style>` block, after `/* MANDATES */` (added in phase 03), before `/* GETTING STARTED */`.

```css
/* IN PRACTICE (tabs) */
.tabs { grid-column: 1 / span 12; }
.tabs-list {
  display: flex;
  gap: 32px;
  border-bottom: 1px solid var(--rule);
  margin-bottom: 40px;
  padding: 0;
  list-style: none;
  flex-wrap: wrap;
}
.tabs-list button {
  font-family: var(--font-mono);
  font-size: 12px;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  background: none;
  border: none;
  padding: 16px 0;
  cursor: pointer;
  color: var(--ink-muted);
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  transition: color 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.tabs-list button:hover { color: var(--ink); }
.tabs-list button[aria-selected="true"] {
  color: var(--ink);
  border-bottom-color: var(--accent);
}
.tabs-list button:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 4px;
}
.tab-panel { display: none; }
.tab-panel[data-active="true"] { display: block; }
.tab-quote {
  font-family: var(--font-display);
  font-style: italic;
  font-size: 22px;
  line-height: 1.4;
  color: var(--ink);
  border-left: 2px solid var(--accent);
  padding: 8px 0 8px 24px;
  margin: 0 0 32px;
  max-width: 70ch;
}
.tab-flow {
  list-style: none;
  padding: 0;
  margin: 0 0 32px;
  counter-reset: flow-step;
}
.tab-flow li {
  counter-increment: flow-step;
  padding: 12px 0 12px 56px;
  border-bottom: 1px solid var(--rule);
  position: relative;
  font-size: 14px;
  line-height: 1.55;
}
.tab-flow li::before {
  content: counter(flow-step, decimal-leading-zero);
  position: absolute;
  left: 0;
  top: 14px;
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--accent);
  letter-spacing: 0.1em;
}
.tab-flow li:last-child { border-bottom: none; }
.tab-flow code {
  font-size: 12px;
}
.tab-outcome {
  font-size: 15px;
  color: var(--ink-muted);
  font-style: italic;
  max-width: 60ch;
  border-top: 1px solid var(--ink);
  padding-top: 16px;
}
.tab-refusal {
  background: var(--bg-muted);
  padding: 24px;
  margin-bottom: 32px;
  border-left: 2px solid var(--accent);
  font-size: 15px;
  line-height: 1.6;
  color: var(--ink);
}
```

**Mobile (add to existing `@media (max-width: 900px)`):**
```css
.tabs-list { gap: 0; flex-direction: column; border-bottom: none; }
.tabs-list button { text-align: left; padding: 16px 0; border-bottom: 1px solid var(--rule); }
.tabs-list button[aria-selected="true"] { border-bottom-color: var(--accent); border-bottom-width: 2px; }
.tab-quote { font-size: 18px; padding-left: 16px; }
```

**No-JS fallback (add to `<style>` end):**
```css
/* No-JS fallback: show all panels */
.no-js .tab-panel { display: block; border-top: 1px solid var(--rule); padding-top: 32px; margin-top: 32px; }
.no-js .tabs-list { display: none; }
```

### 2. Add HTML section
**Location:** After Mandates section (added in phase 03), before `<!-- GETTING STARTED -->`.

```html
  <!-- IN PRACTICE -->
  <section aria-label="In practice — three example flows">
    <div class="grid-12">
      <div class="sec-head">
        <span class="label">— 07</span>
        <h2><em>In practice.</em> Three real flows.</h2>
        <span class="sec-meta">README.md § Examples</span>
      </div>

      <div class="tabs">
        <div class="tabs-list" role="tablist" aria-label="Example flows">
          <button role="tab" id="tab-coffee" aria-controls="panel-coffee" aria-selected="true" tabindex="0">Coffee landing</button>
          <button role="tab" id="tab-portfolio" aria-controls="panel-portfolio" aria-selected="false" tabindex="-1">Portfolio redesign</button>
          <button role="tab" id="tab-refused" aria-controls="panel-refused" aria-selected="false" tabindex="-1">Dashboard refused</button>
        </div>

        <div class="tabs-panels">

          <div class="tab-panel" id="panel-coffee" role="tabpanel" aria-labelledby="tab-coffee" data-active="true">
            <p class="tab-quote">"Design a landing page for a new specialty coffee subscription service targeting home-brewing enthusiasts in Japan. Vibe should feel editorial and warm."</p>
            <ol class="tab-flow">
              <li>Phase 0 detects <code>--new</code> (no URL provided)</li>
              <li>Phase 0.5 detects <code>landing</code> from "landing page"</li>
              <li>Phase 1 → <code>ck:brainstorm</code> locks vibe = editorial + agrarian (wildcard), 3 inspirations confirmed</li>
              <li>Phase 2 → palette cream <code>#F5F1E8</code> + ink + dusk-rose accent · Migra + GT Sectra · asymmetric editorial · 3D declined</li>
              <li>Phase 3 → 8 custom SVG icons designed (nav-mark, brewing-step icons, social marks)</li>
              <li>Phase 4 → silkscreen-style poster hero illustration via <code>ck:ai-artist</code></li>
              <li>Phase 6-8 → <code>ck:plan</code> + <code>ck:cook</code> + Tier 1/2/3 audit passes; ships</li>
            </ol>
            <p class="tab-outcome">Editorial coffee landing with custom assets, vibe-paired type, zero AI slop. No 3D, no icon library, no purple gradient anywhere.</p>
          </div>

          <div class="tab-panel" id="panel-portfolio" role="tabpanel" aria-labelledby="tab-portfolio" data-active="false">
            <p class="tab-quote">"Redesign this portfolio: https://my-old-site.com — I want it to feel more elegant and let my work speak. Currently has too many flashy hover effects."</p>
            <ol class="tab-flow">
              <li>Phase 0 detects <code>--redesign</code> (URL provided)</li>
              <li>Audit per <code>redesign-audit-checklist.md</code> — keep portfolio cover photo + custom monogram; kill hover-effect overload, skill-bar percentages, "Hi I'm passionate" opener</li>
              <li>Phase 0.5 detects <code>portfolio</code></li>
              <li>Phase 1-2 → elegant vibe locked · PP Neue Montreal display · off-white palette · atmospheric spatial</li>
              <li>Phase 3-5 → minimal icon set (5 icons) · editorial environmental portrait · 3D logo accent approved</li>
              <li>Phase 6-8 → Plan with <code>app/work/[slug]</code> case study route → audit catches "Welcome to my portfolio" leftover copy → fixes → ships</li>
            </ol>
            <p class="tab-outcome">Restrained portfolio that lets the work breathe. Atmospheric, not flashy. Audit-caught copy leftover prevented a slop-shipped redesign.</p>
          </div>

          <div class="tab-panel" id="panel-refused" role="tabpanel" aria-labelledby="tab-refused" data-active="false">
            <p class="tab-quote">"Build me an admin dashboard with a sidebar and analytics charts."</p>
            <div class="tab-refusal">
              perfect-ui scope = marketing-style sites only (landing / portfolio). For an admin dashboard with sidebar and charts, use <code>ck:frontend-development</code> instead — it has React/TypeScript patterns suited to app surfaces. If you need a marketing landing page <em>for</em> your admin tool, that's in scope — clarify and we'll proceed.
            </div>
            <p class="tab-outcome">Skill knows when to step aside. Refusal is a redirect, not a block. Off-scope work goes to skills built for it.</p>
          </div>

        </div>
      </div>
    </div>
  </section>
```

### 3. Add tabs JS
**Location:** Just before closing `</body>` (line 778).

```html
<script>
  (function () {
    var tabs = document.querySelectorAll('[role="tab"]');
    if (!tabs.length) return;

    function activate(tab) {
      tabs.forEach(function (t) {
        var panel = document.getElementById(t.getAttribute('aria-controls'));
        var isActive = t === tab;
        t.setAttribute('aria-selected', isActive ? 'true' : 'false');
        t.setAttribute('tabindex', isActive ? '0' : '-1');
        if (panel) panel.setAttribute('data-active', isActive ? 'true' : 'false');
      });
      tab.focus();
    }

    tabs.forEach(function (tab, idx) {
      tab.addEventListener('click', function () { activate(tab); });
      tab.addEventListener('keydown', function (e) {
        var key = e.key;
        var next;
        if (key === 'ArrowRight') next = tabs[(idx + 1) % tabs.length];
        else if (key === 'ArrowLeft') next = tabs[(idx - 1 + tabs.length) % tabs.length];
        else if (key === 'Home') next = tabs[0];
        else if (key === 'End') next = tabs[tabs.length - 1];
        if (next) { e.preventDefault(); activate(next); }
      });
    });
  })();
</script>
```

### 4. Add no-JS fallback class
**Location:** `<html>` tag (line 2).

**Find:** `<html lang="en">`
**Replace:** `<html lang="en" class="no-js">`

**Add inline script in `<head>`** (immediately after `<title>`, line 6):
```html
<script>document.documentElement.classList.remove('no-js');</script>
```

This way: JS-enabled clients remove `.no-js` instantly (before render); JS-disabled clients keep `.no-js` and CSS shows all panels.

## Todo list
- [ ] Add CSS for `.tabs`, `.tabs-list`, `.tab-panel`, `.tab-quote`, `.tab-flow`, `.tab-outcome`, `.tab-refusal`
- [ ] Add no-JS fallback CSS
- [ ] Add mobile overrides (vertical tab list)
- [ ] Insert HTML section after Mandates
- [ ] Add no-js class to `<html>` + inline removal script in `<head>`
- [ ] Add tabs JS at end of `<body>`
- [ ] Smoke test: click each tab → correct panel shows
- [ ] Smoke test: keyboard nav (Tab to focus, Arrow keys to switch, Home/End)
- [ ] Smoke test: disable JS in DevTools → all 3 panels visible, tab list hidden
- [ ] Smoke test: mobile (<900px) → vertical tab pills

## Success criteria
- [ ] Section renders between Mandates and Getting Started
- [ ] Default active tab: "Coffee landing"
- [ ] Click switches active tab + panel correctly
- [ ] Arrow Left/Right cycles through tabs
- [ ] Home jumps to first, End to last
- [ ] Focus visible on tab buttons (accent outline)
- [ ] No-JS fallback shows all 3 panels stacked
- [ ] Mobile: tabs become vertical pill list, panels render correctly
- [ ] All 3 example contents match brainstorm verbatim
- [ ] Tab `<button>` not `<a>` — proper semantic element
- [ ] No animation transitions on tab switch (per editorial-restrained mandate)

## Risk assessment
| Risk | Severity | Mitigation |
|---|---|---|
| Tabs JS breaks if minimal browser doesn't support `Element.classList` / `forEach` on NodeList | Low | Target modern browsers; vanilla pattern is widely compatible. IE11 not supported (acceptable). |
| ARIA setup wrong → screen readers announce incorrectly | High | Follow WAI-ARIA Authoring Practices for tabs. Test with VoiceOver / NVDA after build. |
| Initial render flicker from no-js fallback removing class | Low | Inline `<script>` runs synchronously in `<head>` BEFORE body renders → no flash. |
| Tab content too long for mobile, becomes scroll-heavy | Medium | Coffee tab has 7 flow steps — at mobile that's reasonable. If feels long, can shorten flow descriptions in implementation. |
| Tab switching focus jump confuses keyboard users | Low | Standard ARIA pattern. `tab.focus()` after activate() is expected. |
| `'use strict'` not declared — IIFE pattern | Low | Pattern is standard, scoped to IIFE. No globals leaked. Adding `'use strict'` is optional cleanup. |

## Security considerations
- Inline script in `<head>` triggers CSP issues if strict CSP applied. Current docs page has no CSP meta tag → OK. If CSP added later, move no-js removal to nonce-based or external file.
- Tabs JS uses `document.getElementById` and event listeners on existing DOM — no innerHTML, no eval, no XSS surface.

## Next steps
- Phase 05 — Beyond perfect-ui section (related skills compass, before footer).
