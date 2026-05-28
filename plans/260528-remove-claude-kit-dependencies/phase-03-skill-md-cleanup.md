# Phase 03 — SKILL.md cleanup + version bump

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > § Beyond generic-ize
- [phase-01-workflow-phases-inline.md](./phase-01-workflow-phases-inline.md) — depends on (inline workflows referenced)
- [phase-02-reference-files-capability-cleanup.md](./phase-02-reference-files-capability-cleanup.md) — depends on (capability vocabulary)
- [SKILL.md](../../SKILL.md) — file to modify (~370 lines pre-edit, 22 ck: hits)

## Overview
- **Priority:** High (skill manifest — drives skill discovery + activation; orchestration definition)
- **Status:** pending
- **Depends on:** Phase 01 + Phase 02
- **Description:** Remove ck:/ckm: from SKILL.md (22 hits). Rewrite Skill Orchestration Map (no delegate-to-X). § Beyond generic-ize (3 rows). Update Hard Rules phrasing. References table cleanup. Anti-Rationalization rows update for v2.2.0 framing. Bump version 2.1.0 → 2.2.0.

## Key insights
- SKILL.md frontmatter `description` field has ck-related phrasing ("Orchestrates ck:brainstorm (vibe) → visual direction...") — must NOT lose activation keywords but remove ck-skill names
- § Skill Orchestration Map table (~6-8 rows) currently maps each phase to ck:X / ckm:X / agent — replace with capability descriptions or inline references
- § References table lists reference file paths (no ck mentions there) — likely OK; verify
- § Beyond perfect-ui (added in v2.1.0) lists ck:frontend-development / ck:shopify / ck:frontend-design — replace with generic capability descriptions

## Requirements

### Functional
- 0 ck:/ckm: matches in SKILL.md post-edit
- Frontmatter `description` keeps activation keywords (landing page, portfolio, design, etc.) but removes "Orchestrates ck:..." phrase
- Skill Orchestration Map → capability-based or inline-protocol references
- § Beyond → 3 generic capability rows
- Version 2.1.0 → 2.2.0 in frontmatter
- Anti-Rationalization rows updated (keep concept, remove ck delegation phrasing)
- Hard Rules phrasing — review any reference to ck-skill, update

### Non-functional
- Trigger phrases preserved (skill activation breadth unchanged)
- Hard Rules content intact (mandates unchanged)
- Process flow diagram (Mermaid) — check if any node label mentions ck-skill; update if so
- File size ± 30 lines net

## Architecture

### Frontmatter description rewrite

**Current** (line 3 approximate):
```
description: "Design and build cohesive web pages with custom visual identity — landing pages and portfolios get rich anatomy + section archetypes; any other page type ... Orchestrates ck:brainstorm (vibe) → visual direction (color/typography/mood) → custom icon set ... → ck:plan + ck:cook implementation on Next.js + Tailwind + shadcn. Always proposes 3D as optional. No refusals; outputs distinctive sites, not AI slop."
```

**New**:
```
description: "Design and build cohesive web pages with custom visual identity — landing pages and portfolios get rich anatomy + section archetypes; any other page type (blog, about, pricing, contact, coming-soon, dashboard, admin, e-commerce, custom) is supported through generic anatomy + skeleton. Use this skill whenever the user mentions: landing page, portfolio, personal site, hero section, marketing page, product page, sales page, splash page, blog page, about page, pricing page, contact page, coming-soon, waitlist, dashboard, admin panel, e-commerce store, redesign my site, design my portfolio, build a portfolio, work showcase, hire-me page, perfect-ui, perfect landing, or asks to create any web page surface. Two tiers: special (landing | portfolio — rich treatment) and generic (everything else — universal craft toolkit). Self-contained 8-phase pipeline: vibe discovery → visual direction (color/typography/mood) → custom icon set (NO emoji, NO icon library) → AI-generated visuals → optional shader effects layer → inline plan + implement on Next.js + Tailwind + shadcn. Always proposes effect layer as optional. No refusals; outputs distinctive sites, not AI slop."
```

Removed: "Orchestrates ck:brainstorm (vibe) → ... → ck:plan + ck:cook implementation"
Replaced with: "Self-contained 8-phase pipeline: vibe discovery → ... → inline plan + implement"

### Version bump

Frontmatter: `version: "2.1.0"` → `version: "2.2.0"`

### Skill Orchestration Map rewrite

**Current** (lines ~270-280 approximate):
```
| Phase | Skill / agent | Purpose |
|-------|---------------|---------|
| 1 | `ck:brainstorm` | Vibe + type-branched brief |
| 2 | inline + `AskUserQuestion` | Lock palette/typo/effect-layer |
| 3 | `ckm:design` icon gen and/or `ck:ai-multimodal` | Custom icons |
| 4 | `ck:ai-artist`, `ck:ai-multimodal`, `ck:media-processing` | 2D visual assets ... |
| 5 | `ck:threejs` (shaders only) OR CSS / Lottie | Visual Effect Layer ... |
| 6 | `ck:plan` | Type-aware implementation plan |
| 7 | `ck:cook` | Build the site |
| 8 | `code-reviewer` agent | Anti-slop audit |
```

**New**:
```
| Phase | Method | Purpose |
|-------|--------|---------|
| 1 | Inline brainstorm protocol (see workflow-phases.md § Phase 1) | Vibe + type-branched brief |
| 2 | Inline + `AskUserQuestion` | Lock palette/typo/effect-layer |
| 3 | Direct SVG OR vector icon design pipeline | Custom icons |
| 4 | Text-to-image (style control / photorealism) + image post-processing | 2D visual assets |
| 5 | React Three Fiber (shaders only) OR CSS / Lottie | Visual Effect Layer |
| 6 | Inline plan protocol (see workflow-phases.md § Phase 6) | Type-aware implementation plan |
| 7 | Inline implement protocol (see workflow-phases.md § Phase 7) | Build the site |
| 8 | Inline audit protocol (see workflow-phases.md § Phase 8) | Anti-slop audit |
```

### § Beyond perfect-ui generic-ize

**Current** (3 rows mention `ck:frontend-development`, `ck:shopify`, `ck:frontend-design`):

**New**:
```
| Need | Suggested approach |
|------|-------------------|
| Full app architecture, complex client-side state, deep multi-page IA | General frontend engineering workflow (state management, routing framework, type-safe API layer) |
| Full e-commerce backend (cart, checkout, inventory, payment integration) | Dedicated e-commerce platform workflow with backend orchestration |
| Exact design replication from screenshot / Figma reference | Vision-driven design-to-code workflow (multimodal model + visual diff loop) |
```

### Anti-Rationalization rows

Review existing rows. Update any that reference ck-skill delegation. Likely targets:
- Row mentioning "delegate to ck:brainstorm" → "skip the inline brainstorm protocol"
- Row mentioning "ck:plan handles structure" → "inline plan protocol structures phases"

Keep all existing concept rows intact; only update wording where ck-skill names appear.

### Process Flow diagram (Mermaid)

Check if any node label includes ck-skill names. If yes, update to method-neutral phrasing. Currently the diagram says:
- `M[Phase 0: Detect Mode: new vs redesign]`
- `T[Phase 0.5: Detect Type → tier route]`
- `B[Phase 1: Discovery via ck:brainstorm — branched per type]` ← UPDATE THIS
- `C[Phase 2: Visual Direction — palette/typo/spatial/effect/motion]`
- `H[Phase 6: Plan via ck:plan — type-aware]` ← UPDATE THIS
- `I[Phase 7: Implement via ck:cook — apply locked motion intensity]` ← UPDATE THIS

Update to:
- `B[Phase 1: Discovery — inline brainstorm protocol]`
- `H[Phase 6: Plan — inline plan protocol]`
- `I[Phase 7: Implement — apply locked motion intensity]`

### References table cleanup

Check for any ck-skill references; replace with file paths only (table currently lists file paths, likely already OK).

## Related code files

**Modify:** `SKILL.md` (single file, multiple sections)

**Create / Delete:** None

## Implementation steps

1. **Read SKILL.md** with grep for ck:/ckm: line numbers
2. **Update frontmatter description** — remove "Orchestrates ck:..." phrase, replace with "Self-contained 8-phase pipeline: ..." version
3. **Update frontmatter version** → "2.2.0"
4. **Rewrite Skill Orchestration Map table** (8 rows) per Architecture
5. **Rewrite § Beyond perfect-ui** (3 rows) per Architecture
6. **Update Mermaid diagram nodes B, H, I** per Architecture
7. **Update Anti-Rationalization rows** that mention ck-skill delegation
8. **Final grep** — `grep -E 'ck:|ckm:|code-reviewer' SKILL.md` returns 0 matches
9. **Verify** trigger phrases preserved in description (manual scan: "landing page", "portfolio", "blog page", "dashboard", etc. still present)

## Todo list
- [ ] Read SKILL.md, grep ck:/ckm: line numbers
- [ ] Update frontmatter description (preserve activation keywords)
- [ ] Bump version 2.1.0 → 2.2.0
- [ ] Rewrite Skill Orchestration Map
- [ ] Rewrite § Beyond perfect-ui
- [ ] Update Mermaid diagram (3 nodes)
- [ ] Update Anti-Rationalization rows
- [ ] Final grep verification (0 matches)
- [ ] Activation keyword preservation check

## Success criteria
- 0 ck:/ckm: matches in SKILL.md
- 0 `code-reviewer agent` mentions in SKILL.md
- Frontmatter version = "2.2.0"
- Frontmatter description retains activation keywords + describes self-contained pipeline
- Skill Orchestration Map uses inline-protocol or capability-based phrasing
- § Beyond has exactly 3 rows, no specific skill names
- Process flow diagram nodes B, H, I updated
- Trigger phrases preserved (manual scan confirms)

## Risk assessment
- **Risk:** Lose skill activation keywords in description rewrite → preserve all "design a landing page" / "design my portfolio" / "design a dashboard" / etc. phrases; only remove "Orchestrates ck:..." phrase
- **Risk:** Hard Rules wording weakens → only update where ck-skill names appear; mandate strength preserved
- **Risk:** References table accidentally modified → spot-check after edit
- **Risk:** Mermaid diagram syntax breaks → validate by re-reading diagram block

## Security considerations
None.

## Next steps
- Phase 04 (README) references SKILL.md scope decisions for consistency
- Phase 05 (index.html) references SKILL.md scope decisions for consistency
