# Phase 02 — Workflow phases update

## Context links
- [brainstorm.md](./brainstorm.md) § Phase 0.5 logic mới
- [brainstorm.md](./brainstorm.md) § Phase 0.5 expanded options (AskUserQuestion)
- [phase-01-foundation-files-and-anti-slop-matrix.md](./phase-01-foundation-files-and-anti-slop-matrix.md) — depends on
- [references/workflow-phases.md](../../references/workflow-phases.md) — file to modify (478 lines)
- [references/anti-slop-rules.md](../../references/anti-slop-rules.md) — for Phase 8 reference

## Overview
- **Priority:** High (defines runtime logic for scope-open behavior)
- **Status:** pending
- **Depends on:** Phase 01 (needs generic-page-anatomy.md + generic-page-skeleton.md paths)
- **Description:** Update workflow-phases.md to (a) replace Phase 0.5 detect-or-refuse with detect-or-ask-expanded-options, (b) add Phase 6 generic tier plan prompt template, (c) update Phase 8 to honor applicability matrix.

## Key insights
- Phase 0.5 is the central gate — its rewrite controls all downstream branching
- Existing Phase 0.5 logic has "off-scope refusal" prose that must be deleted; type detection keywords must expand
- Phase 6 has 2 prompts (landing-specific, portfolio-specific); must add 3rd (generic tier) without breaking the 2 existing ones
- Phase 8 audit currently runs "type-specific checks" — refactor to "applicability-tagged checks" referencing matrix from Phase 01

## Requirements

### Functional
- Phase 0.5 accepts any `--type` string (no validation against enum)
- Phase 0.5 auto-detect expanded keywords: blog, about, pricing, contact, coming-soon, waitlist, 404, legal, dashboard, admin, e-commerce, store
- Phase 0.5 AskUserQuestion fallback offers 8+ presets + "Other (free text)"
- Phase 0.5 NO refusal path — log "non-standard type, using generic tier" instead
- Phase 6 generic-tier prompt template defined (resolves brainstorm Q1)
- Phase 8 references applicability matrix from anti-slop-rules.md

### Non-functional
- Existing landing/portfolio flow text preserved word-for-word where possible (zero regression)
- Net line change ≤ +80 lines (additive, no major rewrites)

## Architecture

### Phase 0.5 new logic (replace § "Phase 0.5: Type Detection")
```markdown
### Phase 0.5 — Type Detection (no refusal)

**Step 1: Parse `--type` flag**
- If passed: accept any string, route to that type. No validation.

**Step 2: Auto-detect from input description**
Match keywords (case-insensitive):
- `landing|marketing|hero|sales|conversion|funnel` → `landing` (special tier)
- `portfolio|hire-me|work showcase|personal site|hire me` → `portfolio` (special tier)
- `blog|article|post` → `blog` (generic tier)
- `about|team|company info` → `about` (generic tier)
- `pricing|plans|tiers` → `pricing` (generic tier)
- `contact|reach out|get in touch` → `contact` (generic tier)
- `coming soon|waitlist|early access` → `coming-soon` (generic tier)
- `404|error page|not found` → `error-page` (generic tier)
- `legal|terms|privacy` → `legal` (generic tier)
- `dashboard|admin panel|admin dashboard` → `dashboard` (generic tier) — log warning: evidence base partial
- `e-commerce|storefront|product catalog|shop` → `e-commerce` (generic tier) — log warning
- Other matches → use detected keyword as type, generic tier

**Step 3: AskUserQuestion fallback**
If no detection possible, ask:
> Q: "What type of page are you designing?"
> Options:
>   - Landing page (marketing/conversion)
>   - Portfolio / personal site
>   - Blog / article
>   - About / team page
>   - Pricing page
>   - Contact / coming-soon / waitlist
>   - Dashboard / admin
>   - E-commerce / store
>   - Other (free text → generic tier)

**Step 4: Tier routing**
- Special tier (`landing` | `portfolio`) → use landing-anatomy.md / portfolio-anatomy.md + corresponding skeleton + section-archetypes.md
- Generic tier (any other) → use generic-page-anatomy.md + generic-page-skeleton.md

**Step 5: Honest disclosure for app-surface types**
If type ∈ {dashboard, admin, e-commerce}, log this notice to user:
> "Note: skill's evidence base (12 marketing landings analyzed) does NOT cover dashboard/admin/e-commerce patterns directly. Universal craft toolkit (vibe, custom icons, motion rules, anti-slop universal subset) still applies. Output quality is best-effort, not evidence-backed."

Type is carried in all downstream phase prompts.
```

### Phase 6 generic-tier prompt addition
Existing Phase 6 has subsections "Landing plan prompt" and "Portfolio plan prompt". Add 3rd subsection:

```markdown
**Generic tier plan prompt template (any type ≠ landing/portfolio):**

Pass to `ck:plan`:
- Brief locked at Phase 1 (page-purpose, audience, vibe, inspirations)
- Visual direction locked at Phase 2 (palette, typography, spatial, effect, motion)
- Custom icon set from Phase 3
- 2D illustrations from Phase 4
- Generic anatomy reference: `references/generic-page-anatomy.md`
- Generic skeleton reference: `assets/nextjs-skeleton/generic-page-skeleton.md`

Plan structure (per generic-anatomy):
1. Scaffold setup (Next.js + Tailwind tokens + fonts)
2. Page-purpose definition (driven by Phase 1 brief)
3. Section selection (pick from pattern library based on purpose — NOT a fixed stack)
4. Implement chosen sections in dependency order
5. Mobile responsive pass
6. Motion pass (respect locked intensity)
7. A11y + Lighthouse pass
8. Anti-slop audit (universal subset)

Note: section list is purpose-driven, not template-driven. If page is dashboard, sections may be: nav + sidebar + data-grid + filter-bar (no hero/CTA). If page is pricing, sections may be: hero + pricing-tiers + FAQ + CTA. Plan reflects user's page-purpose.
```

### Phase 8 audit update
Existing Phase 8 instructs running anti-slop grep checks. Update to:

```markdown
**Audit filter (Phase 8 — new logic):**

1. Read current session `--type`
2. Determine tier:
   - Special tier (`landing` | `portfolio`) → use full rule set
   - Generic tier → filter rules where tag = `[universal]` only
3. Run grep checks on filtered subset (see anti-slop-rules.md § Applicability Matrix for tag table)
4. Output PASS/FAIL with applicable rules count

Example for `--type dashboard`:
- Applicable: ~13 universal rules
- Skipped: ~12 marketing-only rules + portfolio-only rules
- Audit pass criteria: 0 universal rule violations OR ≥1 with logged override
```

## Related code files

**Modify:**
- `references/workflow-phases.md`
  - § Phase 0.5: full rewrite (~50 lines new, replaces ~30 lines existing refusal logic)
  - § Phase 6: add generic-tier subsection (~25 lines new)
  - § Phase 8: update audit filter logic (~20 lines new)

**Create:** None
**Delete:** Existing Phase 0.5 refusal prose paragraph(s)

## Implementation steps

1. **Read existing `references/workflow-phases.md`** to locate exact line ranges:
   - Phase 0.5 section start/end
   - Phase 6 section start/end
   - Phase 8 section start/end

2. **Rewrite Phase 0.5** — replace existing refusal-based logic with detect-or-ask flow:
   - Delete refusal prose ("If type ∈ {dashboard, admin, app, e-commerce} → refuse and redirect...")
   - Insert new 5-step logic as defined in Architecture above
   - Preserve existing section heading style

3. **Add Phase 6 generic-tier subsection** — after existing landing + portfolio prompt subsections:
   - Heading: `**Generic tier plan prompt template:**`
   - Body per Architecture above
   - Do NOT modify existing landing/portfolio prompt blocks

4. **Update Phase 8 audit logic** — locate existing audit instructions:
   - Replace "type-specific checks" prose with tier-filtered logic
   - Reference `anti-slop-rules.md § Applicability Matrix`
   - Add 1-2 example block (dashboard vs portfolio)

5. **Validation pass** — re-read entire workflow-phases.md:
   - Confirm landing/portfolio flow paragraphs unchanged
   - Confirm no leftover "refuse" / "off-scope" prose
   - Confirm Phase 6 has 3 prompt subsections
   - Confirm Phase 8 references the matrix

## Todo list
- [ ] Read workflow-phases.md, locate Phase 0.5/6/8 line ranges
- [ ] Rewrite Phase 0.5 section
- [ ] Add Phase 6 generic-tier subsection
- [ ] Update Phase 8 audit filter logic
- [ ] Final read-through: no leftover refusal prose

## Success criteria
- workflow-phases.md no longer contains "refuse" / "off-scope" instructions for dashboard/admin/e-commerce
- Phase 0.5 5-step logic present
- Phase 6 has 3 prompt subsections (landing / portfolio / generic)
- Phase 8 references § Applicability Matrix
- Existing landing/portfolio paragraphs unmodified (diff shows only additions + Phase 0.5 replacement)

## Risk assessment
- **Risk:** Accidentally modify existing landing/portfolio prose → Diff review before commit
- **Risk:** Phase 6 generic prompt too vague → include 2 concrete examples in template
- **Risk:** Phase 8 filter logic ambiguous → reference the matrix table directly with line/section anchors

## Security considerations
None.

## Next steps
- Phase 03 references workflow-phases.md updated logic in SKILL.md
