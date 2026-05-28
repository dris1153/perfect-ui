---
name: v23-completeness-tier1
status: completed
priority: medium
mode: auto
created: 2026-05-28
completed: 2026-05-28
target: SKILL.md, README.md, index.html, references/, anatomy files
blockedBy: []
blocks: []
---

# Plan — perfect-ui v2.3.0 Completeness (Tier 1)

6 items from roadmap Tier 1 (A+B+C+N+S+V): Strategic Omissions checklist + Honest copy mandate + Pre-flight scan + Hero 2-line iron rule (vibe-specific) + Meta-label ban + Hero filler-text ban.

## Source of truth
[brainstorm.md](./brainstorm.md) — full design, Q1-Q7 locked decisions, per-item specifications.
[roadmap brainstorm](../260528-taste-skill-research-upgrades/brainstorm.md) — parent v2.3 → v2.4 → v2.5 strategy.

## Context links
- Skill manifest: [SKILL.md](../../SKILL.md) (`version: "2.2.0"`)
- Public docs: [README.md](../../README.md), [index.html](../../index.html)
- Anti-slop rules: [references/anti-slop-rules.md](../../references/anti-slop-rules.md)
- Workflow: [references/workflow-phases.md](../../references/workflow-phases.md)
- Anatomy files: [landing](../../references/landing-anatomy.md) · [portfolio](../../references/portfolio-anatomy.md) · [generic-page](../../references/generic-page-anatomy.md)
- Visual direction: [references/visual-direction-guide.md](../../references/visual-direction-guide.md)
- Prior completed plans: [260528-open-scope-page-types](../260528-open-scope-page-types/plan.md), [260528-remove-claude-kit-dependencies](../260528-remove-claude-kit-dependencies/plan.md)

## Resolved decisions (from brainstorm Q-section)

| # | Decision |
|---|----------|
| Q1 | Strategic Omissions inline `[condition]` tags |
| Q2 | Honest copy placeholder = em-dash + label (`— metric to confirm`) |
| Q3 | Pre-flight auto-detect (eager when existing files; silent on empty repo) |
| Q4 | Hero line rule vibe-specific (per-vibe range; universal 4+ ban) |
| Q5 | Meta-label universal ban (even ordinal content) |
| Q6 | Filler-text ban TEXT only; icons (static + animated) allowed |
| Q7 | No attribution in references; general "taste-skill ecosystem inspiration" mention in README v2.3 changelog only |

## Resolved sub-decisions (from plan args defaults)

1. `.perfect-ui/preflight.json` at project root + add to `.gitignore` suggestion in scaffold
2. Skip In Practice tab update in v2.3 — defer to v2.5 when study + component modes ship
3. Hero H1 line range = compact new column in vibe matrix (format: "1-2" / "2-3" / "1")
4. Honest copy → fold into existing Hard Rule #3 anti-slop defaults (no new Hard Rule #10)

## Goal

1. Strategic Omissions section present in all 3 anatomy files with `[condition]` inline tags
2. Honest Copy Mandate § in anti-slop-rules.md with em-dash placeholder spec
3. Pre-flight scan auto-detect in workflow-phases.md Phase 0.1 + new reference file
4. Hero H1 line range column in visual-direction-guide.md vibe matrix (11 vibes)
5. Meta-label + filler-text rules added to anti-slop-rules.md Tier classification
6. Version 2.3.0 in SKILL.md frontmatter + README L5 + index.html hero + footer
7. Backward compat: landing/portfolio v2.2.0 examples render identically

## Phases

| # | Phase | Files | Status | Effort |
|---|-------|-------|--------|--------|
| 01 | Anti-slop rules — 4 new patterns + tag matrix | [phase-01-anti-slop-updates.md](./phase-01-anti-slop-updates.md) | completed | M |
| 02 | Pre-flight scan — new file + workflow Phase 0.1 + Phase 7 | [phase-02-preflight-scan.md](./phase-02-preflight-scan.md) | completed | M |
| 03 | Strategic Omissions — 3 anatomy files | [phase-03-strategic-omissions.md](./phase-03-strategic-omissions.md) | completed | M |
| 04 | Hero H1 line range — visual-direction-guide.md | [phase-04-hero-line-matrix.md](./phase-04-hero-line-matrix.md) | completed | S |
| 05 | Public surfaces — SKILL.md + README.md + index.html + version | [phase-05-public-surfaces.md](./phase-05-public-surfaces.md) | completed | M |

## Key dependencies

```
Phase 01 ⊥ Phase 02 ⊥ Phase 03 ⊥ Phase 04   (4 phases parallel-safe — distinct file ownership)
              ↓
Phase 05 (depends on 01-04 to summarize + version bump correctly)
```

- Phase 01-04 each own distinct files — can run in parallel
- Phase 05 references all above outputs (Mandates section + version + FAQ + index.html)
- Phase 03's Strategic Omissions can cross-reference Phase 01's Honest Copy Mandate (link via markdown) but doesn't block

## File ownership (parallel-safe contracts)

| File | Owner phase | Action | Approx. lines |
|------|-------------|--------|---------------|
| `references/anti-slop-rules.md` | 01 | MODIFY (+§ Honest Copy, + hero line / meta-label / filler-text rules, + tag matrix updates) | +50 |
| `references/preflight-scan.md` | 02 | CREATE | +80 |
| `references/workflow-phases.md` | 02 | MODIFY (+ Phase 0.1, + Phase 7 honest copy constraint) | +25 |
| `references/landing-anatomy.md` | 03 | MODIFY (+ § Strategic Omissions) | +30 |
| `references/portfolio-anatomy.md` | 03 | MODIFY (+ § Strategic Omissions) | +25 |
| `references/generic-page-anatomy.md` | 03 | MODIFY (+ § Strategic Omissions) | +30 |
| `references/visual-direction-guide.md` | 04 | MODIFY (+ Hero H1 line range column) | +15 |
| `SKILL.md` | 05 | MODIFY (frontmatter version 2.3.0 + Hard Rule #3 update + Phase 0.1 reference) | +15 |
| `README.md` | 05 | MODIFY (L5 version 2.3.0 + v2.3.0 update paragraph + 1 new FAQ + changelog mention) | +20 |
| `index.html` | 05 | MODIFY (Mandates section + hero version + footer version) | +20 |

**Total:** 1 new file (~80 lines) + 9 modified files (~+230 lines) = ~310 net new lines.

## Success criteria (overall)

- [ ] anti-slop-rules.md has § Honest Copy Mandate + 3 new tier-classified rules (hero line, meta-label, filler-text) + tag matrix updates
- [ ] preflight-scan.md exists (~80 lines) covering detection + 6 signal sources + output format + persistence + edge cases
- [ ] workflow-phases.md has new Phase 0.1 section + Phase 7 honest copy constraint
- [ ] 3 anatomy files have § Strategic Omissions with consistent `[condition]` tag vocabulary
- [ ] visual-direction-guide.md vibe matrix has Hero H1 line range column for all 11 vibes
- [ ] SKILL.md frontmatter `version: "2.3.0"` + Hard Rule #3 updated + Phase 0.1 reference
- [ ] README.md L5 version 2.3.0 + v2.3.0 update paragraph + new FAQ + changelog with "taste-skill ecosystem inspiration" mention
- [ ] index.html hero version 2.3.0 + footer version 2.3.0 + Mandates section updated
- [ ] Final grep: 0 stale "v2.2.0" references in active files
- [ ] Backward compat: landing/portfolio Phase 1/6/7/8 outputs schema-identical to v2.2.0

## Out of scope

- v2.4 items (project memory, macrostructure layer, dials, motion personalities, hero composition catalog, gapless bento)
- v2.5 items (study verb, component-scope, design_plan block)
- Vibe-specific hero composition recipes (defer to v2.4 macrostructure layer)
- Pre-flight scan for exotic frameworks (Solid, Qwik, Lit)
- Cookie consent component implementation details
- Form validation library prescription
- In Practice tab update in index.html (defer to v2.5)
- New Hard Rule #10 (honest copy folded into #3 instead)

## Risks

| Risk | Mitigation |
|------|------------|
| Pre-flight findings block too noisy on partially-populated repos | Limit to ≤6 lines; only flag what perfect-ui preserves OR replaces |
| Strategic Omissions tag vocabulary inconsistent across 3 anatomy files | Define vocabulary in one place (anti-slop-rules.md § Tag glossary or top of brainstorm); cross-reference in each anatomy file |
| Hero H1 line range column makes visual-direction-guide.md vibe matrix too wide | Use compact format ("1-2" / "1") — not verbose; ≤6 chars per cell |
| Em-dash placeholder rendering needs concrete CSS pattern | Define inline: `<span class="placeholder">— metric to confirm</span>` with Tailwind classes (`bg-bg-muted px-2 rounded text-ink-muted`) |
| v2.4 macrostructures (Long Document) may want ordinal labels conflicting with universal meta-label ban | Document as known conflict in roadmap; v2.4 brainstorm will revisit |
| Backward compat regression (landing/portfolio v2.2.0 outputs change) | Phase 05 includes smoke test step + diff review |

## Final verification (last task before plan.md status → completed)

1. Run grep: `grep -rE 'v?2\.2\.0' SKILL.md README.md index.html` → 0 matches (excluding historical context in Anti-Rationalization rows or footer)
2. Run grep: `grep -rE 'v?2\.3\.0' SKILL.md README.md index.html` → ≥4 matches (frontmatter + L5 + hero + footer)
3. Verify `references/preflight-scan.md` exists + file size ~80 lines
4. Verify anti-slop-rules.md § Applicability Matrix has 4 new tagged rules
5. Verify all 3 anatomy files have § Strategic Omissions section
6. Verify visual-direction-guide.md vibe matrix has Hero H1 line range column for all 11 vibes
7. Backward compat smoke test: read existing landing/portfolio example in README — confirm no breaking change in Phase outputs
