# Phase 01 — Foundation files + anti-slop matrix

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Files (new)
- [brainstorm.md](./brainstorm.md) § Anti-slop Applicability Matrix (preview)
- [references/anti-slop-rules.md](../../references/anti-slop-rules.md) — file to modify
- [references/landing-anatomy.md](../../references/landing-anatomy.md), [references/portfolio-anatomy.md](../../references/portfolio-anatomy.md) — anatomy file style reference
- [assets/nextjs-skeleton/landing-skeleton.md](../../assets/nextjs-skeleton/landing-skeleton.md) — skeleton file style reference

## Overview
- **Priority:** High (foundation for all downstream phases)
- **Status:** pending
- **Description:** Create 2 new foundation files (generic-page-anatomy + generic-page-skeleton) and add Applicability Matrix to anti-slop-rules.md. All 3 files have independent ownership and can be edited in parallel sub-tasks within this phase.

## Key insights
- Generic anatomy phải FUZZY by design — không prescribe sections vì pricing ≠ 404 ≠ blog
- Skeleton phải KEEP mandate cốt lõi (custom icons, HSL tokens, centralized copy) nhưng KHÔNG prescribe sections
- Applicability matrix critical — không có nó, dashboard audit raise false positive (rule "no two equal CTAs in hero" vô nghĩa cho dashboard)

## Requirements

### Functional
- `references/generic-page-anatomy.md` cung cấp page-purpose exercise + section pattern library + universal anti-pattern reminders
- `assets/nextjs-skeleton/generic-page-skeleton.md` cung cấp minimal Next.js scaffold giữ mandate
- `references/anti-slop-rules.md` có § Applicability Matrix tag mỗi rule là `[universal]` | `[marketing-only]` | `[landing/portfolio-only]`

### Non-functional
- Tone matches existing reference style (sacrifice grammar for concision)
- Cross-references functional (no broken markdown links)
- File size <200 lines each new file

## Architecture

### `references/generic-page-anatomy.md` structure (~120 lines)
```
# Generic page anatomy

## Scope
- For any page type NOT landing/portfolio
- Examples: blog, about, pricing, contact, coming-soon, 404, dashboard, admin, e-commerce, legal
- Note: evidence base (12 landings) covers marketing patterns only — output for app-surface types is best-effort universal craft

## Page-purpose exercise (before designing)
- What's this page's ONE job? (inform | convert | navigate | display data | collect input | tell a story)
- Who lands here and from where?
- What's the primary action (if any)? Secondary actions?
- What success looks like (metric or qualitative)?

## Section pattern library (pick what fits purpose; do NOT prescribe order)
- Nav / header (when site has multiple pages)
- Hero (when page needs a strong opener — most content pages do; 404/error pages don't)
- Content block (long-form prose, data table, form, feature list, FAQ, image gallery — purpose-driven)
- CTA block (when conversion is goal; skip for purely informational pages)
- Footer (always for marketing-style site; skip for app surface)

## Universal anti-patterns (always avoid; references anti-slop-rules.md universal subset)
- No emoji as icons
- No icon library imports
- No Inter/Roboto/Arial alone
- No DM Sans + Space Grotesk pairing
- No `h-screen` (use `min-h-[100dvh]`)
- No hex colors inline (use Tailwind tokens)
- No `ease-in-out 0.3s` default; use vibe-paired cubic-bezier
- Always respect `prefers-reduced-motion`

## Marketing anti-patterns (apply only when page has marketing intent)
- Pricing page: still avoid fake stats, "Elevate/Seamless/Unleash" copy, browser-mockup
- Blog: still avoid fake testimonials, generic stock photos
- For non-marketing pages (dashboard, admin): these don't apply

## Mobile + a11y reminders
- Viewport: design for 390×844 baseline
- Tap target ≥44px
- Color contrast WCAG AA
- Reduced motion: auto-degrade motion intensity to 0/3

## Validation
- Commitment audit (≥48/60) still required — vibe must be locked before code
- Phase 8 audit runs filtered subset per applicability matrix
```

### `assets/nextjs-skeleton/generic-page-skeleton.md` structure (~80 lines)
```
# Generic page skeleton (Next.js)

## Scope
- For `--type` ≠ landing/portfolio
- Minimal scaffold; user/page-purpose decides sections

## File tree
app/
├── layout.tsx          (fonts, metadata, html/body)
├── page.tsx            (compose page sections — start empty, build per page-purpose)
├── globals.css         (Tailwind + text-wrap balance + off-black/off-white defaults)
├── components/
│   ├── icons/          (custom SVG only — see custom-icon-pipeline.md)
│   ├── ui/             (primitives — Button, Card)
│   └── sections/       (created per page-purpose)
└── lib/
    └── content.ts      (all copy in one file)

public/
└── {type}/             (assets folder named per page-type)

## Tailwind config (essential)
- HSL tokens (--bg, --ink, --accent) — never hex inline
- fontFamily mapped to --font-display, --font-body via next/font
- maxWidth container 1280px

## globals.css (essential)
- text-wrap: balance on h1/h2/h3
- text-wrap: pretty on <p>
- Off-black ink (#1A1715 or equivalent), off-white bg (not pure #FFF/#000)

## Bundle targets
- JS ≤200KB gzipped
- LCP ≤2.5s
- CLS ≤0.1
- Lighthouse mobile ≥90 (relaxed for app surfaces if data-heavy)

## Optional sections (uncomment in page.tsx as needed)
- Nav (when multi-page site)
- Footer (when marketing-style)

## What this skeleton does NOT prescribe
- Section order
- Hero presence
- CTA layout
- Page chrome density
→ All driven by page-purpose from generic-page-anatomy.md
```

### `references/anti-slop-rules.md` — § Applicability Matrix (add at top, after intro)
```markdown
## § Applicability Matrix

Each rule below tagged with applicability scope. Phase 8 audit filters rules by `--type` tier:
- **Special tier** (`landing`, `portfolio`) → all rules apply
- **Generic tier** (any other type) → only `[universal]` rules apply; `[marketing-only]` skipped unless page has explicit marketing intent

| Rule | Tag |
|------|-----|
| No emoji anywhere | `[universal]` |
| No icon libraries (lucide/heroicons/phosphor) | `[universal]` |
| No Inter/Roboto/Arial/Open Sans alone | `[universal]` |
| No DM Sans + Space Grotesk pairing | `[universal]` |
| Custom SVG cohesion (single stroke weight, etc.) | `[universal]` |
| `h-screen` banned (use min-h-[100dvh]) | `[universal]` |
| No inline hex colors (use tokens) | `[universal]` |
| Respect prefers-reduced-motion | `[universal]` |
| No `ease-in-out 0.3s` default | `[universal]` |
| AI cute illustration as decoration | `[universal]` |
| Inter alone (no display pair) | `[universal]` Tier 3 |
| Title Case headers | `[universal]` Tier 3 |
| AI cliché copy ("Elevate/Seamless/Unleash") | `[universal]` Tier 3 (load-bearing positions) |
| No AI 3D model as hero subject | `[marketing-only]` |
| No purple-blue gradient hero | `[marketing-only]` |
| No 3-col equal feature grid | `[marketing-only]` |
| No two equal-weight CTAs in hero | `[marketing-only]` |
| Generic CTA labels ("Get Started"/"Sign In") | `[marketing-only]` |
| No browser-mockup hero | `[marketing-only]` Tier 2 |
| Friendly bullet checklist with green checks | `[marketing-only]` Tier 2 |
| Round fake stats (99.99%, 10x) | `[marketing-only]` Tier 2 |
| Centered H1 at high variance | `[marketing-only]` Tier 2 |
| "Hi I'm X passionate designer" | `[landing/portfolio-only]` (portfolio) |
| Skill bars / tool clouds | `[landing/portfolio-only]` (portfolio) |
| iPhone-mockup holding work | `[landing/portfolio-only]` (portfolio) |
| 30+ projects shown | `[landing/portfolio-only]` (portfolio) |

**Audit logic (Phase 8):**
- Read `--type` from session context
- Filter rule set: special tier = all, generic tier = `[universal]` only
- Run grep checks on filtered subset
- Output PASS/FAIL with applicable rules count
```

## Related code files

**Modify:**
- `references/anti-slop-rules.md` — add § Applicability Matrix after intro/preface, before § Tier 1 section

**Create:**
- `references/generic-page-anatomy.md`
- `assets/nextjs-skeleton/generic-page-skeleton.md`

**Delete:** None

## Implementation steps

1. **Create `references/generic-page-anatomy.md`**
   - Use structure above (~120 lines)
   - Sections: Scope, Page-purpose exercise, Section pattern library, Universal anti-patterns, Marketing anti-patterns conditional, Mobile + a11y, Validation
   - Cross-link to anti-slop-rules.md applicability matrix
   - Cross-link to visual-direction-guide.md commitment audit

2. **Create `assets/nextjs-skeleton/generic-page-skeleton.md`**
   - Use structure above (~80 lines)
   - Sections: Scope, File tree, Tailwind config, globals.css, Bundle targets, Optional sections, What it does NOT prescribe
   - Cross-link to custom-icon-pipeline.md
   - Cross-link to visual-direction-guide.md for vibe tokens

3. **Modify `references/anti-slop-rules.md`** — add § Applicability Matrix section
   - Insert after file intro/preface, before existing § Tier 1 section
   - Build table tagging every existing rule (see preview structure above)
   - Add audit logic paragraph at end of § explaining filter behavior
   - Do NOT change existing rule content — only add the matrix section

4. **Validation** — verify every existing rule in anti-slop-rules.md has a row in the matrix (no untagged rules)

## Todo list
- [ ] Create `references/generic-page-anatomy.md`
- [ ] Create `assets/nextjs-skeleton/generic-page-skeleton.md`
- [ ] Add § Applicability Matrix to `references/anti-slop-rules.md`
- [ ] Verify every rule has tag (no untagged)
- [ ] Verify all cross-references resolve (markdown link check)

## Success criteria
- `references/generic-page-anatomy.md` exists, <200 lines, all sections present
- `assets/nextjs-skeleton/generic-page-skeleton.md` exists, <100 lines, all sections present
- `references/anti-slop-rules.md` has § Applicability Matrix; every existing rule tagged
- No regression: existing landing/portfolio rules read identically
- Markdown links from new files resolve

## Risk assessment
- **Risk:** Forgot to tag a rule → Phase 8 audit treats untagged as `[universal]` (safe default)
- **Risk:** Generic-anatomy too prescriptive defeats purpose → keep section list "pattern library" not "stack"
- **Risk:** Skeleton drift from landing/portfolio skeleton conventions → mirror their structure exactly

## Security considerations
None — documentation-only changes.

## Next steps
- Phase 02 references the new files in workflow-phases.md updates
- Phase 03 references new files in SKILL.md
