# perfect-ui v2.3.0 — Completeness (Tier 1)

**Date:** 2026-05-28
**Status:** Brainstorm complete, awaiting plan approval
**Skill version impact:** v2.2.0 → v2.3.0 (minor — additive, backward-compatible)
**Parent roadmap:** [260528-taste-skill-research-upgrades/brainstorm.md](../260528-taste-skill-research-upgrades/brainstorm.md)

---

## Problem statement

Per roadmap brainstorm: perfect-ui anatomies + anti-slop don't enforce **what AI typically forgets** (legal/404/back-nav/form-validation/skip-link/cookie-consent), don't prevent **fabricated metrics** (current "no fake stats" rule is negative-only, lacks positive guidance), don't **scan existing tokens** before designing in new mode (only redesign mode does this), and don't enforce **hero discipline** (line count, meta-labels, filler text — concrete patterns identified from gpt-taste + stitch-design-taste).

v2.3.0 closes these 6 gaps. Theme: "Completeness — fewer AI omissions."

## Requirements (locked from user decisions Q1–Q7)

| ID | Decision | Source Q |
|----|----------|----------|
| R1 | Strategic Omissions tagged inline `[condition]` (e.g., `[EU only]`, `[always]`, `[when form present]`) | Q1 |
| R2 | Honest copy placeholder = em-dash + label (Hallmark-style): `— metric to confirm` plus visual grey block | Q2 |
| R3 | Pre-flight scan auto-detect: eager when existing files (package.json/tailwind.config/*.css), silent on empty repo | Q3 |
| R4 | Hero line-count rule = vibe-specific defaults (per-vibe recommended range; universal ban on 4+ lines) | Q4 |
| R5 | Meta-label ban = universal (no exception, even ordinal content) | Q5 |
| R6 | Hero filler-text ban = TEXT only ("Scroll to explore" / "Swipe down" banned); icons allowed (static or animated) | Q6 |
| R7 | No attribution in references — perfect-ui authoritative voice; general "taste-skill ecosystem" mention in README v2.3 changelog only | Q7 |

## Evaluated approaches (selected per Q&A)

No alternative approaches at architecture level — v2.3 is purely additive across 6 known items. Selection happened at the conditionality / format / scope dial level via Q1–Q7.

## Final design — per-item specifications

### Item A — Strategic Omissions checklist

**Anatomy file additions** (3 files: landing/portfolio/generic):
Add new section `## Strategic Omissions` (after § Mobile/A11y, before § Validation), tagged inline per R1:

**Landing-anatomy.md insertion (~30 lines):**
```markdown
## Strategic Omissions — what AI typically forgets

Audit before ship. Each item tagged with applicability condition.

- Privacy policy + terms-of-service links in footer `[always]`
- Custom 404 page `[when multi-page site]`
- Form validation (client-side, inline) `[when form present]`
- "Skip to main content" a11y link (visually-hidden, focus-visible) `[always]`
- Cookie consent banner `[EU/UK/EEA jurisdiction]`
- "Back" navigation in any flow >1 step `[when multi-step flow]`
- Page metadata (`<title>`, description, OG image, social cards) `[always]`
- Sitemap link or visible site index `[when multi-page site]`
- Working unsubscribe link in email-capture flows `[when email capture]`

If item applies but is missing from output, flag in Phase 8 audit as Tier 2 violation.
```

**Portfolio-anatomy.md insertion (~25 lines):** Same structure, slight pruning — most portfolios skip cookie consent + sitemap; add `[when contact form]` for form validation tag.

**Generic-page-anatomy.md insertion (~30 lines):** Full list + condition tags driven by Page-Purpose Exercise answer (when purpose=convert/collect, form validation `[always]`; when purpose=display data, skip-link still `[always]` but cookie banner `[EU jurisdiction + data persistence]`).

### Item B — Honest copy mandate

**anti-slop-rules.md addition** (~20 lines, new § after Applicability Matrix):

```markdown
## Honest Copy Mandate (universal)

If the user did not supply a metric / testimonial / logo / case-study count, the skill does NOT invent one. Three accepted paths:

1. **Em-dash placeholder + label** — `— metric to confirm` rendered as visible grey block. Layout reserves space; user fills in later. **Default — use this.**
2. **Pick a different macrostructure** — if a stat-led hero requires N metrics and only M < N are available, switch to a non-stat hero (typography-led, image-led).
3. **Refuse the section entirely** — if a "trusted by 50,000+ teams" logo bar has 0 real logos to show, do not include the logo bar. Honest absence beats fabricated presence.

Forbidden:
- "+47% conversion", "trusted by 50,000+ teams", "10× faster" with no source
- John Doe / Jane Smith testimonials with realistic-looking avatars
- Generic startup logos (Acme / Globex / Initech / Nexus)
- "1M+ users", "99.99% uptime", round-fake numbers
- Fabricated case-study counts (8 case studies displayed when user has 2)

Phase 7 implementation must use placeholder rendering; Phase 8 audit greps for forbidden patterns (already covered by `[marketing-only]` rules).
```

**workflow-phases.md Phase 7 update** (~10 lines): Add to per-phase constraints:
- **Honest copy** — if metric/logo/testimonial not supplied by user, use em-dash placeholder + label. Never invent. See `anti-slop-rules.md § Honest Copy Mandate`.

### Item C — Pre-flight scan (auto-detect)

**NEW file `references/preflight-scan.md`** (~80 lines):

```markdown
# Pre-flight Scan

Run BEFORE Phase 2 (Visual Direction) on every new build. Auto-detect mode: scans for existing project files; emits findings block when signals detected, silent when truly empty repo.

## Detection trigger

Run scan if ANY of these exist in target directory:
- `package.json` (Node project)
- `tailwind.config.{js,ts,mjs}` (Tailwind project)
- `next.config.{js,ts,mjs}`, `astro.config.{js,ts,mjs}`, `vite.config.{js,ts,mjs}`
- `app/`, `src/`, or `pages/` directory with any TS/JS/CSS files
- `index.html` with `<link rel="stylesheet">` or inline `<style>`
- `*.css` files in repo root

If none detected: silent. Emit single line `Pre-flight: no signals — proceeding with full perfect-ui stack.`

## What to scan (6 signal sources)

1. **Font stack** — `package.json` for `next/font`, `@fontsource/*`, `geist`; `<link href="...fonts.googleapis.com/...">`; `tailwind.config` `fontFamily`; `@import url("fonts.googleapis.com/...")`
2. **Palette** — OKLCH / HSL / hex in `:root`; `tailwind.config` `theme.extend.colors`; `tokens.json` / `design-tokens.{json,yaml}`
3. **Motion library** — `package.json` deps for `framer-motion`, `gsap`, `motion`, `lenis`, `lottie-react`, `@react-spring/*`
4. **Spacing scale** — Tailwind `theme.extend.spacing`; `--space-*` custom properties; 4pt/8pt scale presence
5. **Framework** — Next.js / Astro / Vue / Svelte / Remix / vanilla HTML
6. **Existing icon library** — `package.json` for lucide-react / @heroicons / phosphor (FLAG — perfect-ui will replace per Hard Rule #2)

## Output format

Emit before Phase 2 dialog:

```
Pre-flight findings:
· Font stack: {detected fonts} ({source file:line})
· Palette: {OKLCH | HSL | hex | DTCG tokens} ({source})
· Motion: {framer-motion 11 | gsap | none} ({source})
· Spacing: {Tailwind extend | 4-pt scale | none}
· Framework: {detected framework}
· Icon library FLAG: {lucide-react detected — will replace per Hard Rule #2}

perfect-ui will preserve: {list — fonts, palette, spacing}.
perfect-ui will introduce: {list — vibe + custom icons + anti-slop + motion intensity + Tier 1/2/3 audit}.

If you want perfect-ui to override any preserved item, say so before Phase 2 locks.
```

## Persistence

Write findings to `.perfect-ui/preflight.json` once. Subsequent runs reuse cache unless:
- User says "refresh pre-flight" / "scan again" / "re-scan"
- `package.json` / `tailwind.config.*` mtime newer than cache

If cached, emit one-line note: `Pre-flight cached (last scan: {date}). Say "refresh pre-flight" to re-scan.`

## Edge cases

- **Conflicting signals** (e.g. Geist imported in `package.json` but hard-coded `font-family: Inter` in CSS) → flag conflict explicitly, ask user to confirm or remove conflict
- **No signals found** → one-line silent note, proceed normally
- **User said "ignore existing project" / "fresh start"** → skip scan entirely, emit `Pre-flight skipped at user request.`
- **`.perfect-ui/preflight.json` corrupt** → regenerate silently

Pre-flight scan is the user's accountability line — "here's what perfect-ui noticed before touching anything." Skipping it on a populated repo = fastest way to lose user trust.
```

**workflow-phases.md Phase 0 update** (~15 lines): Add new step before Phase 0.5 mode detection:
```markdown
### Phase 0.1 — Pre-flight scan (auto-detect)

See `preflight-scan.md` for full protocol. Auto-detect:
- If existing project files detected (package.json / tailwind.config / *.css / framework configs) → run scan, emit findings block
- If empty repo → silent, proceed to Phase 0
- Cache in `.perfect-ui/preflight.json`; reuse unless user requests refresh

Preserved tokens / fonts / motion lib are carried into Phase 2 visual direction dialog. perfect-ui only introduces what's missing.
```

### Item N — Hero 2-line iron rule (vibe-specific)

**anti-slop-rules.md addition** (~10 lines, in § Layout section + tag matrix):
```markdown
- Hero H1 exceeds vibe-specific line count → Tier 1 violation. Universal ceiling: 4+ lines never allowed.
- Per-vibe recommended H1 line range (from visual-direction-guide.md):
  - Minimal: 1-2 lines
  - Editorial: 1-3 lines
  - Brutalist: 1 line (declarative)
  - Retro-futuristic: 1-2 lines
  - Organic: 2-3 lines
  - Luxury: 1-2 lines
  - Playful: 2-3 lines
  - Industrial: 1-2 lines
  - Art-deco: 1-2 lines
  - Glass-tech: 1-2 lines
  - Hand-crafted: 2-3 lines

Enforce in Phase 7 via `max-w-5xl` / `max-w-6xl` containers + `clamp(3rem, 5vw, 5.5rem)` H1 sizing. If headline copy exceeds 90 chars, rewrite shorter; never break the line cap by reducing font size below `--text-display-s`.
```

**visual-direction-guide.md update** (~15 lines): Add `Hero H1 line range` column to vibe matrix at top of file.

### Item S — Meta-label ban (universal)

**anti-slop-rules.md addition** (~5 lines, in § Layout section):
```markdown
- Meta-label headers banned universally: "SECTION 01" / "QUESTION 05" / "ABOUT US" / "CHAPTER THREE" / numbered eyebrows / uppercase mono-cap section numbers — Tier 1 violation. No exception even for ordinal content.
- If section identity matters, communicate via vibe-paired typography hierarchy (display vs body weight differences), NOT mono-cap kicker labels.
- Exception: vibe = brutalist AND content is genuinely declarative (e.g., "01. MANIFESTO") allowed iff ≤1 occurrence on page. Even then, prefer no label.
```

### Item V — Hero filler-text ban (text only, icons OK)

**anti-slop-rules.md addition** (~5 lines):
```markdown
- Hero filler text banned: "Scroll to explore" / "Swipe down" / "Continue below" / similar prompt-text — Tier 2 violation. The hero composition must communicate "more below" without typed instructions.
- Icons (↓, chevron, bouncing arrow) allowed — they're visual hints, not text filler. If used, keep subtle (small size, low contrast); aggressive bouncing animation = Tier 2 violation per generic motion-on-everything rule.
```

## File-level impact summary

**New files (1):**
- `references/preflight-scan.md` (~80 lines)

**Modified files (8):**
| File | Edit | Lines |
|------|------|-------|
| `references/anti-slop-rules.md` | + § Honest Copy Mandate + Hero line / meta-label / filler-text rules + tag matrix updates | ~+50 |
| `references/landing-anatomy.md` | + § Strategic Omissions | ~+30 |
| `references/portfolio-anatomy.md` | + § Strategic Omissions | ~+25 |
| `references/generic-page-anatomy.md` | + § Strategic Omissions | ~+30 |
| `references/workflow-phases.md` | + Phase 0.1 pre-flight ref + Phase 7 honest copy constraint | ~+25 |
| `references/visual-direction-guide.md` | + Hero H1 line range column in vibe matrix | ~+15 |
| `SKILL.md` | + version 2.3.0 + Hard Rule update (mention honest copy) + Phase 0.1 reference | ~+15 |
| `README.md` | + v2.3.0 update paragraph + 1 new FAQ entry ("what's new") | ~+20 |
| `index.html` | + Mandates section update (hero discipline + honest copy) + version 2.3.0 hero + footer | ~+20 |

**Total:** 1 new file (~80 lines) + 8 modified files (~+230 lines) = ~310 new lines net.

## Success criteria (overall)

1. Strategic Omissions section present in all 3 anatomy files, inline `[condition]` tags
2. Honest Copy Mandate section in anti-slop-rules.md with em-dash placeholder spec
3. Pre-flight scan auto-detect logic in workflow-phases.md Phase 0.1 + reference file
4. Hero H1 line range column in visual-direction-guide.md vibe matrix (11 vibes)
5. Meta-label + filler-text rules added to anti-slop-rules.md Tier classification
6. Version 2.3.0 in SKILL.md frontmatter + README L5 + index.html hero + footer
7. No anti-slop self-violations in new content (existing v2.2.0 audit still passes on this file)
8. Backward compat: landing/portfolio v2.2.0 examples produce same output skeleton

## Implementation considerations

- **Cross-file consistency:** Strategic Omissions list per anatomy file must reference SAME items but with anatomy-specific tag conditions
- **Tag vocabulary:** `[always]`, `[EU jurisdiction]`, `[when form present]`, `[when multi-page site]`, `[when email capture]`, `[when contact form]`, `[when data persistence]`, `[when multi-step flow]` — keep stable across files
- **Pre-flight cache file `.perfect-ui/preflight.json`:** add to `.gitignore` default suggestion in scaffold; respect user's existing `.gitignore`
- **Hero line range column in visual-direction-guide.md:** must be visible at first glance (not buried in per-vibe deep section)
- **README v2.3.0 attribution:** general "Inspired by patterns from taste-skill ecosystem (Hallmark, gpt-taste, stitch-design-taste, motion-design, et al.)" in changelog only — per R7, no inline attribution in reference content

## Risks

| Risk | Mitigation |
|------|------------|
| Pre-flight findings block too noisy on partially-populated repos | Limit to ≤6 lines; only flag what perfect-ui will actually preserve OR replace |
| Strategic Omissions tag vocabulary inconsistent across 3 anatomy files | Define vocabulary in one place (anti-slop-rules.md or new tag glossary); cross-reference |
| Hero line range column makes visual-direction-guide.md too wide for readable rendering | Use compact format ("1-2" / "2-3" / "1") not verbose |
| Em-dash placeholder rendering needs concrete CSS pattern | Define inline in honest-copy section: `<span class="placeholder">— metric to confirm</span>` with `bg-bg-muted px-2 rounded text-ink-muted` |
| Conflict with v2.4 macrostructure layer (Long Document MAY want ordinal labels) | v2.5 will revisit meta-label exception when Long Document ships. v2.3 enforces strict ban as baseline. |
| Pre-flight scan might miss exotic frameworks (Solid, Qwik, etc.) | Acceptable for v2.3; expand detection in later versions if users report |

## Out of scope (defer)

- v2.4 items (D project memory, E macrostructure layer, F dials, K motion personalities, T atmosphere spectrum, O hero compositions, R gapless bento)
- v2.5 items (G study verb, H component-scope, Q design_plan block)
- Vibe-specific hero composition recipes (defer to v2.4 § E macrostructure layer + § O hero composition catalog)
- Pre-flight scan for exotic frameworks (Solid, Qwik, Lit)
- Cookie consent component implementation details (Phase 7 generates per project; v2.3 just flags requirement)
- Form validation library prescription (perfect-ui doesn't recommend libraries; Phase 7 implements inline JS)

## Next steps

1. User approve this brainstorm → proceed to `/ck:plan`
2. Plan dự kiến: ~4-5 phase files
   - Phase 01: Foundation rules — anti-slop-rules.md updates (honest copy + hero line + meta-label + filler-text) + new tag matrix entries
   - Phase 02: Pre-flight scan — NEW references/preflight-scan.md + workflow-phases.md Phase 0.1
   - Phase 03: Strategic Omissions checklists — landing/portfolio/generic anatomy files
   - Phase 04: Visual direction matrix — hero line range column
   - Phase 05: SKILL.md + README.md + index.html — version + Mandates + changelog
3. Each phase parallel-safe by file ownership
4. Final verification: grep zero stale references; version 2.3.0 in 4 locations; backward compat smoke test

## Unresolved questions (resolve in /ck:plan or execution)

- Pre-flight scan: `.perfect-ui/preflight.json` location — root vs `.perfect-ui/` folder? Should it be gitignored by default in scaffold?
- index.html version 2.3.0 update: add new "Completeness" tab in In Practice section? Or skip In Practice update until v2.4 brings substantial new examples?
- visual-direction-guide.md Hero H1 line range — add as new column in existing vibe matrix OR new sub-section? Existing matrix already has 5+ columns; adding 6th might cramp.
- SKILL.md Hard Rules — add NEW Hard Rule #10 for honest copy OR fold into existing #3 anti-slop defaults? Adding #10 = first new Hard Rule since v2.0.0.
