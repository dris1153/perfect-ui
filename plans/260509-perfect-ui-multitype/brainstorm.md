---
title: perfect-landing → perfect-ui multi-type expansion
date: 2026-05-09
status: approved
type: brainstorm
---

# Brainstorm — perfect-ui Multi-Type Expansion

## Problem Statement

Current `perfect-landing` skill is locked to landing pages only. User wants to add `--type` arg for portfolio + landing. (Blog deferred to later phase.)

## Approved Decisions

| Item | Decision |
|------|----------|
| Skill rename | `perfect-landing` → `perfect-ui` |
| Types supported | `landing` \| `portfolio` (blog deferred) |
| Default behavior | `AskUserQuestion` if `--type` not passed |
| Workflow sharing | All 8 phases shared, only Phase 1 brief + Phase 6 plan + anatomy reference differ |
| Off-scope refusal | Explicit refuse for: dashboards, full apps, admin panels, e-commerce, SaaS internals |

## Approaches Evaluated

### A. Single skill `perfect-ui` with `--type` flag (CHOSEN)
- Pros: Single entry, shared pipeline (vibe/icons/3D/build identical), low duplication
- Cons: Name "ui" generic — risk of triggering for dashboard work
- Mitigation: Hard scope declaration + refuse logic

### B. Keep `perfect-landing`, add `--type`
- Rejected: Skill name no longer matches scope, confusing for future invocations

### C. Separate sibling skills (perfect-landing + perfect-portfolio)
- Rejected: Duplicates 80% of references; user explicitly chose unified

### D. Parent-router (`perfect-ui` delegates to sub-skills)
- Rejected: Over-engineered for 2 types; orchestration overhead > benefit

## Final Architecture

### File migration

```
perfect-landing/                     →  perfect-ui/
  SKILL.md                              SKILL.md                            (rename + expand desc + Phase 0.5)
  references/
    workflow-phases.md                  workflow-phases.md                   (Phase 1 branches per type)
    visual-direction-guide.md           visual-direction-guide.md            (unchanged)
    custom-icon-pipeline.md             custom-icon-pipeline.md              (add portfolio icon inventory)
    threejs-integration-patterns.md     threejs-integration-patterns.md      (unchanged)
    visual-asset-prompt-library.md      visual-asset-prompt-library.md       (add portfolio hero prompts)
    landing-page-anatomy.md             landing-anatomy.md                   (rename)
                                        portfolio-anatomy.md                 (NEW)
    anti-slop-rules.md                  anti-slop-rules.md                   (add portfolio clichés)
    redesign-audit-checklist.md         redesign-audit-checklist.md          (mention type detection)
  assets/landing-templates/             assets/nextjs-skeleton/
    nextjs-skeleton.md                    landing-skeleton.md                (rename)
                                          portfolio-skeleton.md              (NEW)
    section-archetypes.md                 section-archetypes.md              (add portfolio archetypes)
```

### SKILL.md frontmatter

```yaml
name: perfect-ui
description: "Design and build cohesive marketing-style websites — landing pages and portfolios — with custom visual identity. Use whenever user mentions: landing page, portfolio, personal site, hero section, marketing page, product page, sales page, redesign my site, design my portfolio, build a portfolio, work showcase, hire-me page, perfect-ui, perfect landing. Types: landing | portfolio (asks if unspecified). Orchestrates ck:brainstorm (vibe) → visual direction → custom icon set (NO emoji, NO library) → AI visuals → optional Three.js 3D → ck:plan + ck:cook on Next.js + Tailwind + shadcn. Outputs distinctive sites, not AI slop. Does NOT handle: full apps, dashboards, admin panels, e-commerce, SaaS internals."
argument-hint: "[description OR site URL] [--type landing|portfolio] [--new|--redesign] [--no-3d]"
```

### New: Phase 0.5 — Type Detection (between Mode and Discovery)

```
- If --type flag passed → use it
- If user explicitly mentions "portfolio" or "landing" → infer
- Else AskUserQuestion("Type site?", [Landing, Portfolio])
- Carry type into all downstream phases
- Refuse if user requests dashboard / full app / e-commerce
```

### Phase 1 brief — branches per type

**Landing brief** (existing):
1. Product / 2. Audience / 3. Conversion goal / 4. Vibe + wildcard / 5. Inspirations / 6. Anti-refs / 7. Constraints

**Portfolio brief** (new):
1. Owner one-liner (you + craft)
2. Audience (hiring managers / agency clients / freelance leads)
3. Single goal (hire me / book call / freelance inquiry)
4. Work focus (project types featured, count: 4 / 6 / 8 / 12)
5. Case study depth (deep dives vs gallery thumbnails)
6. Vibe + wildcard
7. Inspirations / Anti-references / Constraints

### portfolio-anatomy.md (new) — section stack

1. Hero (intro: who you are + craft)
2. Selected Work Grid
3. Featured Case Study (1-2 deep)
4. About / Bio
5. Process / Approach (optional)
6. Contact CTA
7. Footer

**Anti-patterns specific to portfolio:**
- "Hi, I'm [Name], a passionate designer who loves coffee" cliché → refuse
- Generic "View my work" CTA → use specific outcome ("Available for freelance from June")
- Hover-effect overload on work grid → keep grid calm, let work speak
- Project cards with same-aspect-ratio masonry-fail → use real project covers

## Implementation Considerations

### Risks
- `perfect-ui` name is generic — hard scope declaration + refuse logic critical
- Description char count ~1000 — close to 1024 limit, monitor
- workflow-phases.md branching may increase length — mitigate with sub-sections per type

### Estimated effort
~2 hours of writing (skipping blog cuts ~45 min)

### Validation
- Run `quick_validate.py` after rename
- Manually test trigger phrases for both types

## Success Criteria

- [ ] Folder renamed `perfect-landing/` → `perfect-ui/`
- [ ] SKILL.md frontmatter updated, description ≤1024 char
- [ ] Phase 0.5 type detection added
- [ ] Phase 1 brief has 2 branches (landing, portfolio)
- [ ] `portfolio-anatomy.md` exists with 7 sections + anti-patterns
- [ ] `portfolio-skeleton.md` exists with Next.js scaffold
- [ ] `section-archetypes.md` adds portfolio archetypes
- [ ] `anti-slop-rules.md` adds portfolio clichés
- [ ] `quick_validate.py` passes
- [ ] Trigger test: "design my portfolio" activates skill

## Next Steps

User decides: /ck:plan formal plan, OR direct implementation, OR skip.
