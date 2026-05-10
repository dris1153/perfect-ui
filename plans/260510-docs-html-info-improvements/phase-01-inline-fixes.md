# Phase 01 — Inline fixes

## Context links
- [brainstorm.md § Inline expansions](./brainstorm.md)
- Target: [index.html](../../index.html)

## Overview
- **Priority:** High (corrects documented inaccuracies + low risk, isolated edits)
- **Status:** pending
- **Effort:** XS (~15 minutes)
- **Description:** 4 isolated edits — version sync, file-name fix, splash criteria expansion, CLI flags table addition. No new sections.

## Key insights
- All 4 fixes are content-only, no CSS changes needed.
- CLI flags table can reuse `.tier li` or similar table patterns; if simpler, use a small `<dl>` or markdown-style table styled with mono font.
- Each edit is independent — can ship one without blocking others.

## Requirements
- Functional: every fix verifiable by grep/visual scan.
- Non-functional: zero impact on other sections, zero CSS additions (use existing tokens).

## Architecture
N/A — content edits only.

## Related code files
- **Modify:** `d:\Workspace\dris1153\Personal\claude-skills\perfect-ui\index.html`

## Implementation steps

### 1. Hero meta version sync
- **Location:** Line 376 (inside `.hero-head` → `.meta`)
- **Find:** `<span>v0.0.1</span>`
- **Replace:** `<span>v2.0.0</span>`
- **Verification:** grep `v0.0.1` returns zero hits in `index.html`.

### 2. Pipeline phase ∞ card body expansion
- **Location:** Lines 532-537 (the `.phase` block with `phase-num` "— ∞" / `h3` "Loading UI")
- **Find:** `<p>Default no splash. Earns place only when assets need masking or brand moment justifies.</p>`
- **Replace with structured content:**
```html
<p>Default no splash. Earns place only when:</p>
<ul style="font-size: 13px; color: var(--ink-muted); padding-left: 16px; margin: 0 0 16px;">
  <li>Heavy assets &gt;1.5s load</li>
  <li>Brand mark moment</li>
  <li>Curated narrative entrance</li>
</ul>
```
- **Note:** Inline styles match existing `.phase p` ink-muted color. Could also extract to class but inline keeps phase 01 isolated.
- **Verification:** Visual check — phase ∞ card now shows 3 bullet points, doesn't break grid alignment.

### 3. Getting Started → CLI flags table
- **Location:** After line 736 (after the trigger phrases paragraph, before closing `</div>` of `.start-col`)
- **Insert** new `<h3>` + table structure within the LEFT `.start-col` (Trigger phrases column), OR add separate column. Decision: append below trigger phrases in same col since right col (file structure) is already heavy.
- **Alternative (recommended):** Insert between the two existing `.start-col` divs as a third row spanning both cols, OR replace right column. Simpler: append within left `.start-col` after the existing `<p>` paragraph (line 735).

**Implementation (append to left col):**
```html
<h3 style="margin-top: 32px;">Flags</h3>
<div class="triggers" style="font-family: var(--font-mono); font-size: 12px; line-height: 1.7; color: var(--ink-muted);">
  <div><strong style="color: var(--ink);">--type</strong> &nbsp; landing | portfolio &nbsp; <span style="opacity: 0.7;">(asks if unspecified)</span></div>
  <div><strong style="color: var(--ink);">--new</strong> / <strong style="color: var(--ink);">--redesign</strong> &nbsp; <span style="opacity: 0.7;">(auto-detects from URL/screenshot)</span></div>
  <div><strong style="color: var(--ink);">--no-3d</strong> &nbsp; <span style="opacity: 0.7;">(skip Phase 5 entirely)</span></div>
  <div><strong style="color: var(--ink);">--stack</strong> &nbsp; nextjs | astro | vanilla &nbsp; <span style="opacity: 0.7;">(default: nextjs)</span></div>
</div>
```
- **Verification:** Flags section renders below trigger phrases, mono-styled, matches editorial restraint.

### 4. File structure block fix
- **Location:** Line 743 (inside `.files` block)
- **Find:** `├── docs.html (this file)`
- **Replace:** `├── index.html (this file)`
- **Verification:** grep `docs.html` returns zero hits in `index.html`.

## Todo list
- [ ] Edit 1 — version sync (line 376)
- [ ] Edit 2 — phase ∞ body expansion (lines 532-537)
- [ ] Edit 3 — CLI flags subsection (after line 735)
- [ ] Edit 4 — file structure name fix (line 743)
- [ ] Visual smoke test — open `index.html` in browser, check Hero / Pipeline / Getting Started render correctly
- [ ] grep verification — `v0.0.1` and `docs.html` both return 0 hits

## Success criteria
- [ ] grep `v0.0.1` → 0 hits
- [ ] grep `docs.html` → 0 hits (only `index.html` references remain)
- [ ] Phase ∞ card shows 3 bullet points
- [ ] Getting Started left col shows Flags subsection
- [ ] No CSS file changes
- [ ] No layout regressions

## Risk assessment
| Risk | Severity | Mitigation |
|---|---|---|
| Inline `<ul>` styling breaks `.phase` grid | Low | Use exact `padding-left` / `margin` values; smoke-test visually |
| CLI flags subsection visual weight unbalances 2-col layout | Low | Right col (file structure) already long; left col additions OK |
| Version field elsewhere also needs update | Low | grep reveals only line 376; verify before close |

## Security considerations
N/A — static content edits.

## Next steps
- Phase 02 — add "Why it exists" section (insertion point: after line 404, end of Hero).
