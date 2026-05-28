# Phase 02 — NEW component-scope.md + workflow-brainstorm.md studied-DNA mode

## Context links
- [brainstorm.md](./brainstorm.md) § Item H (Component-scope branch)
- Hallmark reference: `~/.claude/skills/hallmark/SKILL.md § When the brief is a component, not a page`

## Overview
- **Priority:** High (NEW mode + workflow-brainstorm.md integration)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 03 (distinct files)
- **Description:** CREATE `references/component-scope.md` (~100 lines). MODIFY `references/workflow-brainstorm.md` (~+30 lines) — add Studied-DNA input mode for Study verb.

## Key insights
- Component-scope multi-signal detection — needs ≥2 signals to confirm (default page-scope)
- Skipped phases: macrostructure, spatial language, nav/footer archetypes, hero enrichment, log.json write, Phase 8 visual checks
- Kept phases: pre-flight, vibe, palette, typography, Brand Motion Identity, anti-slop universal subset
- Output 2 files: component artifact + `.preview.*` 8-state wrapper
- Framework-aware preview file extension (React → `.preview.tsx`, Vue → `.preview.vue`, etc.)
- workflow-brainstorm.md needs new "Studied-DNA input mode" — Phase 1 brief uses extracted DNA as locked inputs

## Requirements

### Functional
- component-scope.md has 7 sections: When applies / Detection signals / Routing rule / Kept phases / Skipped phases / Output format (2 files) / Stamp format
- Detection multi-signal (2+ signals confirm): brief ≤30 words + UI element keyword + `--component` flag
- Skip rules clear (5 items)
- 8-state preview wrapper format spec'd (default · hover · focus · active · disabled · loading · error · success)
- Framework auto-detection for preview file extension
- workflow-brainstorm.md adds § "Studied-DNA input mode" — Phase 1 brief uses extracted DNA as locked inputs

### Non-functional
- component-scope.md ~100 lines
- workflow-brainstorm.md grows ~+30 lines
- KISS — preview wrapper minimal, defer Storybook integration

## Architecture

### component-scope.md structure (~100 lines)

```markdown
# Component Scope

When user brief = 1 UI element (button / card / modal / dropdown / etc.), perfect-ui collapses page-level apparatus and emits a self-contained component + 8-state preview wrapper. NOT for full pages — those stay in page-scope.

## When this applies (auto-detect at Phase 0.5)

Multi-signal detection. 2+ signals → component scope confirmed.

### Component-scope signals

- **Brief mentions single UI element:** button · input · card · modal · dropdown · tooltip · select · checkbox · switch · tab strip · chip · badge · banner · snackbar · popover · slider · date picker · avatar
- **Brief is short (≤30 words)** and refers to one element
- **Target file is single component** (e.g. `./Button.tsx`, `app/components/Card.vue`)
- **User says** *"just the X"*, *"only the Y"*, *"this one element"*, *"a single ___"*
- **Explicit `--component` flag** passed

### Routing rule

- If 2+ signals fire → component scope. Confirm with one-line note to user.
- If only page-flow signals fire (multi-section brief, "build me a landing page") → stay in page scope.
- If exactly 1 component signal fires (ambiguous) → ask via `AskUserQuestion`: *"One component or whole page?"*
- Default if user doesn't engage → component (single-artifact output is cheaper to redirect than multi-section page).

## What component-scope KEEPS from page flow

- **Phase 0 pre-flight scan** — read existing tokens, fonts, framework, microinteraction stance (same)
- **Phase 1 genre detection** — editorial / modern-minimal / atmospheric / playful (same)
- **Phase 2 vibe + palette + typography** — if `tokens.css` or `design.md` exists, use those; else ask user
- **Phase 2.6 Brand Motion Identity** — personality + 3 constants apply to component
- **2+1 font discipline** — same
- **State discipline — STRICTER.** Every interactive component MUST ship code for **all 8 states**
- **Anti-slop universal subset** — visual / microinteraction / contrast (gates 46-50) / a11y / typography gates

## What component-scope SKIPS

- **Phase 2.5 Macrostructure pick** — components don't have macrostructures. State explicitly: *"Component-scope: skipping macrostructure."*
- **Phase 2c Spatial language** — single element; no page-level spatial
- **Nav + footer archetypes** — page-scope only. A component is one element; it has no nav, no footer
- **Hero enrichment patterns** — page-scope only. A button or card has no hero
- **Phase 8 visual checks** — no full page to render
- **`.perfect-ui/log.json` write** — component runs don't rotate; diversification rule doesn't apply

## What component-scope EMITS

**Two files, side by side:**

### 1. Component artifact

Single self-contained file matching project conventions:

- **React / Next.js:** `Button.tsx`
- **Vue / Nuxt:** `Button.vue`
- **Svelte / SvelteKit:** `Button.svelte`
- **Vanilla web:** `button.css` + `button.html`
- **Tailwind project:** a `.tsx` with `className` chains AND a `tokens.css` if missing

Component consumes perfect-ui tokens by name (`var(--color-accent)`), never inlines OKLCH values.

### 2. 8-state preview wrapper

Auto-detect framework from pre-flight scan; emit matching preview file:

- React → `<ComponentName>.preview.tsx`
- Vue → `<ComponentName>.preview.vue`
- Svelte → `<ComponentName>.preview.svelte`
- Vanilla → `<ComponentName>.preview.html`

A standalone page rendering the component in **all 8 states** stacked vertically with labels:

```
┌──── Button — 8 states ────────────────────────┐
│                                                │
│ default       [ Click me                  ]    │
│ hover         [ Click me                  ]    │  ← .is-hover forces :hover styling
│ focus         [ Click me                  ]    │  ← .is-focus forces :focus-visible
│ active        [ Click me                  ]    │  ← .is-active forces :active
│ disabled      [ Click me                  ]    │  ← disabled attr
│ loading       [ ⌛ Working…                ]    │  ← data-state="loading"
│ error         [ ⚠ Try again               ]    │  ← data-state="error"
│ success       [ ✓ Saved                   ]    │  ← data-state="success"
│                                                │
└────────────────────────────────────────────────┘
```

Each labelled row uses a class (e.g. `.is-hover`) that the component's CSS targets in addition to the real pseudo-class, so all 8 states render at once on the demo page:

```css
.btn:hover, .btn.is-hover { background: var(--color-paper-3); }
.btn:focus-visible, .btn.is-focus { outline: 2px solid var(--color-focus); }
.btn:active, .btn.is-active { transform: translateY(1px); }
```

User opens preview once, sees the component working, then deletes it. The wrapper is NOT part of production code.

## Stamp format for component output

Components stamp differently from pages:

```css
/* perfect-ui · component: <type> · genre: <genre> · vibe: <vibe>
 * states: default · hover · focus · active · disabled · loading · error · success
 * contrast: pass
 */
```

The `component:` prefix tells future perfect-ui runs this artifact is component-scoped — won't trigger page-level diversification rules. The `states:` line is a checklist — every state listed must have actual styling in the file.

## Cross-references

- `workflow-phases.md § Phase 0.5` — component-scope detection routes here
- `workflow-implement.md § Component-scope short-circuit` — Phase 7 collapsed flow
- `workflow-audit.md § Component-scope subset` — Phase 8 filtered checks
- `preflight-scan.md` — framework detection feeds preview file extension
- `motion-patterns.md § Motion Personalities` — Brand Motion Identity applies to component
```

### workflow-brainstorm.md — Studied-DNA input mode section

Insert AFTER existing § Phase 0.5 (Read project memory), BEFORE Step 1 (Scope sanity check):

```markdown
## Studied-DNA input mode (NEW v2.5.0)

When `--study <URL>` ran and produced extracted DNA (see `study-mode.md`), Phase 1 brief uses extracted DNA as LOCKED inputs — skip vibe / palette / typography questions (already extracted). User still answers:

- Audience
- Use case
- Tone
- Macrostructure pick uses extracted macrostructure as default (can override)

Diversification rule SUSPENDED for studied-DNA runs (`.perfect-ui/log.json` entry records `theme: studied-DNA`).

If user pivots ("use Linen theme instead" / "ignore the DNA"), route back to normal Phase 1 questions; diversification resumes.
```

## Related code files

**Create:** `references/component-scope.md` (NEW, ~100 lines)

**Modify:** `references/workflow-brainstorm.md` (+ § Studied-DNA input mode, ~+30 lines)

## Implementation steps

1. Read Hallmark `~/.claude/skills/hallmark/SKILL.md § When the brief is a component` for protocol reference
2. Write `references/component-scope.md` adapting Hallmark protocol with perfect-ui vocabulary
3. Read workflow-brainstorm.md to find insertion point (after Phase 0.5 log read, before Step 1)
4. Insert § Studied-DNA input mode section
5. Verify cross-references

## Todo list
- [ ] Read Hallmark component-scope reference
- [ ] Write component-scope.md with 7 sections
- [ ] Detection multi-signal logic
- [ ] Routing rule documented
- [ ] Kept vs skipped phases
- [ ] 8-state preview wrapper format
- [ ] Framework auto-detection
- [ ] Stamp format
- [ ] Insert studied-DNA input mode in workflow-brainstorm.md
- [ ] Verify cross-references

## Success criteria
- component-scope.md exists, ~100 lines, 7 sections
- Multi-signal detection documented (2+ signals confirm)
- 8-state preview wrapper format spec'd
- Framework auto-detection rules clear
- workflow-brainstorm.md has Studied-DNA input mode section
- Cross-references to Phase 03/04 outputs documented

## Risk assessment
- **Risk:** Component-scope auto-detect false positive (whole page brief mistaken as component) → default page-scope; require 2+ signals
- **Risk:** Preview file extension drift (project has unusual framework) → fallback to `.preview.html` for vanilla
- **Risk:** Studied-DNA + diversification interaction confusing → explicit "diversification suspended" note

## Security considerations
None — documentation only.

## Next steps
- Phase 04 wires Phase 0.5 component-scope detection in workflow-phases.md
- Phase 03 workflow-implement.md handles component-scope short-circuit at Phase 7
- Phase 05 SKILL.md References + Mermaid + Pipeline reference these files
