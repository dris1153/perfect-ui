---
name: open-scope-page-types
status: completed
priority: medium
mode: auto
created: 2026-05-28
completed: 2026-05-28
target: SKILL.md, references/, README.md, index.html
blockedBy: []
blocks: []
---

# Plan — Open scope beyond landing/portfolio

Soften skill scope so `--type` accepts any string. Landing/portfolio keep current rich treatment (anatomy + skeleton + section-archetypes); all other types get a generic anatomy + skeleton. Anti-slop audit gains an applicability matrix so dashboard/admin/e-commerce don't raise false positives.

## Source of truth
[brainstorm.md](./brainstorm.md) — full design, evaluated approaches, trade-offs, applicability matrix preview.

## Context links
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.0.0"`)
- Workflow detail: [references/workflow-phases.md](../../references/workflow-phases.md)
- Anti-slop rules: [references/anti-slop-rules.md](../../references/anti-slop-rules.md)
- Existing anatomy: [references/landing-anatomy.md](../../references/landing-anatomy.md), [references/portfolio-anatomy.md](../../references/portfolio-anatomy.md)
- Public docs: [README.md](../../README.md), [index.html](../../index.html)
- Related prior plan: [260510-docs-html-info-improvements/plan.md](../260510-docs-html-info-improvements/plan.md) (completed; informs index.html structure)

## Resolved decisions (from brainstorm Q-section)
1. **Phase 6 generic tier prompt** → template defined in workflow-phases.md (Phase 02 of this plan)
2. **Version bump** → 2.0.0 → 2.1.0 (additive scope softening = minor bump). Apply in Phase 03 (SKILL.md), Phase 04 (README), Phase 05 (index.html hero + footer)
3. **§09 Beyond** → thu nhỏ (giữ ~3 routing case khi skill khác thực sự tốt hơn: ck:frontend-development cho full app surfaces, ck:shopify cho Shopify backend, ck:frontend-design cho exact replication từ screenshot)

## Goal
1. Skill applies to any web page type, no refusals
2. Landing/portfolio behavior identical post-change (zero regression)
3. Phase 8 audit không raise false positive cho non-marketing type
4. Footprint: 2 new file + 5 modified file
5. Public docs (README + index.html) consistent với SKILL.md scope

## Phases

| # | Phase | Files | Status | Effort |
|---|-------|-------|--------|--------|
| 01 | Foundation files + anti-slop matrix | [phase-01-foundation-files-and-anti-slop-matrix.md](./phase-01-foundation-files-and-anti-slop-matrix.md) | completed | M |
| 02 | Workflow phases update | [phase-02-workflow-phases-update.md](./phase-02-workflow-phases-update.md) | completed | M |
| 03 | SKILL.md scope update | [phase-03-skill-md-scope-update.md](./phase-03-skill-md-scope-update.md) | completed | M |
| 04 | README.md update | [phase-04-readme-update.md](./phase-04-readme-update.md) | completed | M |
| 05 | index.html update | [phase-05-index-html-update.md](./phase-05-index-html-update.md) | completed | M |

## Key dependencies

```
Phase 01 (foundation, parallel-safe internal files)
   ↓
Phase 02 (workflow logic — references new files)
   ↓
Phase 03 (SKILL.md — references all above)
   ↓
Phase 04 + Phase 05 (parallel-safe: different files, no shared content)
```

- Phase 01 → Phase 02: workflow-phases.md references `generic-page-anatomy.md` and `generic-page-skeleton.md` paths
- Phase 02 → Phase 03: SKILL.md scope section references workflow logic
- Phase 03 → Phase 04, 05: README + index.html consistency với SKILL.md decisions
- Phase 04 ⊥ Phase 05: independent file ownership, can run in parallel

## File ownership (parallel-safe contracts)

| File | Owner phase | Action |
|------|-------------|--------|
| `references/generic-page-anatomy.md` | 01 | CREATE |
| `assets/nextjs-skeleton/generic-page-skeleton.md` | 01 | CREATE |
| `references/anti-slop-rules.md` | 01 | MODIFY (add Applicability Matrix § + tag rules) |
| `references/workflow-phases.md` | 02 | MODIFY (Phase 0.5 + Phase 6 + Phase 8) |
| `SKILL.md` | 03 | MODIFY (scope + Hard Rule #1 #8 + version) |
| `README.md` | 04 | MODIFY (examples + FAQ + version) |
| `index.html` | 05 | MODIFY (§02 + §07 tab + §09 + version) |

## Success criteria (overall)

- [x] `--type pricing` (or any non-landing/portfolio string) executes without refusal — Phase 0.5 rewrite + scope rewrite
- [x] `--type landing` / `--type portfolio` behavior identical pre/post change — special-tier prompts and flows untouched
- [x] Anti-slop applicability matrix tags every rule; Phase 8 audit honors tags — `references/anti-slop-rules.md` § Applicability Matrix added
- [x] Phase 0.5 expanded options work (8+ presets + free text) — workflow-phases.md Phase 0.5 Step 3
- [x] All 7 files in scope updated; untouched files stay untouched — verified
- [x] Version 2.1.0 in SKILL.md, README, index.html (hero + footer) — grep confirms 0 hits for v2.0.0, multiple hits for v2.1.0
- [x] No anti-slop self-violations in new content — grep confirms forbidden names appear only in "do NOT" contexts; 0 emoji
- [x] Cross-references between files resolve (no broken links) — new files cross-link to existing references

## Outcome

- 2 new files created: `references/generic-page-anatomy.md` (~120 lines), `assets/nextjs-skeleton/generic-page-skeleton.md` (~90 lines)
- 5 files modified: `references/anti-slop-rules.md` (+ § Applicability Matrix, ~70 lines), `references/workflow-phases.md` (Phase 0.5 rewrite + Phase 6 generic tier + Phase 8 tier filter), `SKILL.md` (Scope + Hard Rules + Phase 0.5 table + Phase 6 + Phase 7 + Phase 8 + References + Beyond + Security + Anti-Rationalization + final paragraph + version), `README.md` (Examples + Trigger phrases + Flags + FAQ + version), `index.html` (hero version + hero stat + § Scope + phase 0.5 card + § In Practice tabs + Getting Started + § Beyond + footer + Mandate #8)
- 14 untouched files: visual-direction-guide, 2d-illustration-catalog, visual-asset-prompt-library, visual-effect-patterns, motion-patterns, custom-icon-pipeline, loading-ui-patterns, redesign-audit-checklist, landing-anatomy, portfolio-anatomy, section-archetypes, landing-skeleton, portfolio-skeleton, plus existing plans
- No commits created — per user CLAUDE.md "No auto-commit" preference. User reviews and commits manually.

## Out of scope

- Per-type anatomy cho blog/about/pricing (defer to v2.2 nếu cần)
- Section archetypes mở rộng cho non-marketing type (defer)
- Multi-page site orchestration (defer)
- Evidence research cho dashboard/admin pattern (different problem class)

## Risks

| Risk | Mitigation |
|------|------------|
| Anti-slop applicability tag sai cho 1 rule | Phase 01 includes audit checklist verifying every rule has tag |
| SKILL.md scope rewrite gây confusion về tier | Phase 03 includes 2-tier comparison table |
| README/index.html drift khỏi SKILL.md | Phase 04, 05 explicitly cross-check against Phase 03 output |
| Backward compat break cho landing/portfolio | Phase 02 keeps existing flows literally identical, only adds branches |
