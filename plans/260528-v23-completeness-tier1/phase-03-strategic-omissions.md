# Phase 03 — Strategic Omissions checklists (3 anatomy files)

## Context links
- [brainstorm.md](./brainstorm.md) § Item A (Strategic Omissions)
- [references/landing-anatomy.md](../../references/landing-anatomy.md)
- [references/portfolio-anatomy.md](../../references/portfolio-anatomy.md)
- [references/generic-page-anatomy.md](../../references/generic-page-anatomy.md)
- [phase-01-anti-slop-updates.md](./phase-01-anti-slop-updates.md) — parallel-safe (optional cross-link)

## Overview
- **Priority:** Medium-high (visible audit improvement; covers known AI omissions)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 02, 04 (different files)
- **Description:** Add § Strategic Omissions to 3 anatomy files. Inline `[condition]` tags express applicability per item.

## Key insights
- Same item list across 3 files but tags differ slightly per anatomy context
- Landing has all 9 items (full set); portfolio prunes ~2 (cookie + sitemap rarely needed); generic-page tags vary per Page-Purpose Exercise answer
- Tag vocabulary must be CONSISTENT across 3 files (defined once, used everywhere)
- Phase 8 audit will flag missing items (already in anti-slop-rules.md tag matrix from Phase 01? No — anti-slop matrix doesn't track Strategic Omissions; this is a separate audit class. Document as such.)

## Requirements

### Functional
- § Strategic Omissions added to landing-anatomy.md (~30 lines, 9 items full set)
- § Strategic Omissions added to portfolio-anatomy.md (~25 lines, ~7 items pruned)
- § Strategic Omissions added to generic-page-anatomy.md (~30 lines, conditional per Page-Purpose Exercise)
- Tag vocabulary consistent: `[always]`, `[EU jurisdiction]`, `[when form present]`, `[when multi-page site]`, `[when email capture]`, `[when contact form]`, `[when data persistence]`, `[when multi-step flow]`
- Cross-reference Phase 01 § Honest Copy Mandate (item: "fabricated metrics" → see § Honest Copy)

### Non-functional
- New § placed AFTER existing § Mobile/A11y (or equivalent location near end of file), BEFORE § Validation/Anti-patterns
- Section heading consistent across 3 files: `## Strategic Omissions — what AI typically forgets`
- Tag vocabulary defined inline in each file (no eager-load dependency)

## Architecture

### landing-anatomy.md § Strategic Omissions

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
- Honest copy — no fabricated metrics; see `anti-slop-rules.md § Honest Copy Mandate` `[always]`

If item applies (per its tag condition) but is missing from output, flag in Phase 8 audit as Tier 2 violation (categorized as Strategic Omission).

Tag vocabulary:
- `[always]` — applies to every landing regardless of context
- `[EU/UK/EEA jurisdiction]` — applies when site serves users in those jurisdictions
- `[when form present]` — applies when page contains any form (signup, contact, etc.)
- `[when multi-page site]` — applies when site has >1 indexed page
- `[when multi-step flow]` — applies for funnels, signup wizards, multi-step CTAs
- `[when email capture]` — applies when page captures email addresses
```

### portfolio-anatomy.md § Strategic Omissions

```markdown
## Strategic Omissions — what AI typically forgets

Audit before ship. Each item tagged with applicability condition.

- Privacy policy + terms-of-service links in footer `[always]`
- Custom 404 page `[when multi-page site]` (portfolios with per-project subpages)
- Form validation (client-side, inline) `[when contact form]`
- "Skip to main content" a11y link `[always]`
- "Back" navigation in case-study subpages `[when case studies have own pages]`
- Page metadata (`<title>`, description, OG image, social cards) `[always]`
- Working contact mechanism that actually mailtos / submits — not a dead form `[always]`
- Honest copy — no fabricated work / clients / awards; see `anti-slop-rules.md § Honest Copy Mandate` `[always]`

Cookie consent + sitemap typically skipped for single-page portfolios; revisit if multi-page or analytics-heavy.

Tag vocabulary: see landing-anatomy.md § Strategic Omissions (same vocabulary).
```

### generic-page-anatomy.md § Strategic Omissions

```markdown
## Strategic Omissions — what AI typically forgets

Audit before ship. Items conditional on Page-Purpose Exercise answer.

Universal (any page type):
- Privacy policy + terms-of-service links in footer `[always]` (skip on legal pages — they ARE the policy)
- Page metadata (`<title>`, description, OG image, social cards) `[always]`
- "Skip to main content" a11y link `[always]`
- Honest copy — no fabricated metrics / testimonials; see `anti-slop-rules.md § Honest Copy Mandate` `[always]`

Conditional on page-purpose:

- **Purpose = convert / collect:** Form validation `[when form present]` · Cookie consent `[EU jurisdiction + data persistence]` · Working unsubscribe `[when email capture]`
- **Purpose = display data (dashboard, admin):** Empty / loading / error states `[always for data UI]` · Keyboard nav for grids / tables `[always]`
- **Purpose = navigate (index, hub):** Sitemap visible OR clean hierarchical IA `[when multi-page]`
- **Purpose = tell a story (case-study standalone, manifesto):** Reading progress indicator OR clear section navigation `[when long-form]`
- **Purpose = inform (blog, about, legal):** Last-updated date `[always for time-sensitive content]` · Author + bio `[when blog]`

Tag vocabulary: see landing-anatomy.md § Strategic Omissions.
```

## Related code files

**Modify (3 files):**
- `references/landing-anatomy.md` — add § Strategic Omissions (~30 lines)
- `references/portfolio-anatomy.md` — add § Strategic Omissions (~25 lines)
- `references/generic-page-anatomy.md` — add § Strategic Omissions (~30 lines, conditional structure)

**Create / Delete:** None

## Implementation steps

1. **Read each anatomy file** to identify insertion point (after § Mobile/A11y or equivalent, before § Validation/Anti-patterns)
2. **Insert landing-anatomy.md § Strategic Omissions** (~30 lines, full 10-item list + tag vocabulary definition)
3. **Insert portfolio-anatomy.md § Strategic Omissions** (~25 lines, 8-item pruned list + reference to landing for vocab)
4. **Insert generic-page-anatomy.md § Strategic Omissions** (~30 lines, conditional structure by page-purpose)
5. **Verify cross-references** — Honest Copy Mandate link to `anti-slop-rules.md § Honest Copy Mandate` (Phase 01 creates this)

## Todo list
- [ ] Read 3 anatomy files, identify insertion points
- [ ] Insert § Strategic Omissions in landing-anatomy.md
- [ ] Insert § Strategic Omissions in portfolio-anatomy.md
- [ ] Insert § Strategic Omissions in generic-page-anatomy.md
- [ ] Verify cross-references to anti-slop-rules.md § Honest Copy Mandate
- [ ] Final read-through — tag vocabulary consistent across 3 files

## Success criteria
- All 3 anatomy files have § Strategic Omissions section
- Tag vocabulary identical (8 tags) across files
- Honest copy cross-reference present in all 3
- File size growth: landing ~+30, portfolio ~+25, generic ~+30 (total ~+85)
- Existing content untouched

## Risk assessment
- **Risk:** Tag vocabulary drifts across 3 files (synonyms creep in) → define once in landing, reference from others
- **Risk:** generic-page-anatomy.md conditional structure too complex → keep flat: universal items first, conditional grouped by purpose
- **Risk:** Section heading naming conflicts with future v2.4 / v2.5 additions → "Strategic Omissions" is unique; safe
- **Risk:** Phase 8 audit doesn't know about Strategic Omissions → document inline: "flag missing applicable items as Tier 2 violation"

## Security considerations
None.

## Next steps
- Phase 05 SKILL.md Anti-Rationalization may add row about Strategic Omissions
- Phase 05 README.md FAQ may add entry "what does Strategic Omissions audit catch"
