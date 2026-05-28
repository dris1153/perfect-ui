# Phase 01 — workflow-phases.md heavy inline expansion

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Workflow inline replacements
- [references/workflow-phases.md](../../references/workflow-phases.md) — file to modify (~485 lines pre-edit)

## Overview
- **Priority:** High (foundation for all downstream phases)
- **Status:** pending
- **Description:** Massive inline expansion of Phase 1 (brainstorm protocol), Phase 6 (plan protocol), Phase 7 (implement protocol), Phase 8 (inline audit). Also Phase 4 tool-routing table → capability table. Target growth: ~+270 lines → final ~755 lines.

## Key insights
- Phase 1/6/7/8 are the orchestration entry points currently delegating to ck:brainstorm / ck:plan / ck:cook / code-reviewer
- Inline workflows must be tailored for perfect-ui (NOT generic copies) — questions branched by type, plan templates aware of vibe/palette/icon/asset artifacts, implement checklist aware of locked motion intensity etc.
- Phase 4 tool routing table mentions ck:ai-artist / ck:ai-multimodal — replace with capability descriptions

## Requirements

### Functional
- Phase 1 contains inline brainstorm protocol with: question scripts (branched landing/portfolio/generic), brief.md schema, approval gate, scope-decomposition trigger
- Phase 6 contains inline plan protocol with: plan.md frontmatter spec, phase-XX.md naming + structure, dependency analysis rules, parallel-safe file ownership conventions
- Phase 7 contains inline implement protocol with: atomic commit pattern (one phase → one commit; user reviews manually per CLAUDE.md no-auto-commit), file ownership enforcement, constraint check per phase
- Phase 8 contains inline audit protocol with: grep runner scripts (from existing § Final Audit), visual check via vision-capable model, tier-filtered output template
- Phase 4 tool routing table replaced with capability table

### Non-functional
- Existing landing/portfolio detection / branching logic preserved word-for-word
- File ≤ 800 lines (split if exceeds 1200)
- No ck:/ckm: references remain in this file after edit
- code-reviewer agent reference removed (replaced with inline audit)

## Architecture

### Phase 1 inline protocol (replace `delegate to ck:brainstorm` block)

Structure (~80 lines):
```
### Phase 1 — Discovery (inline brainstorm protocol)

Skill conducts brainstorm directly via AskUserQuestion. Output: plans/{date}-{slug}/brief.md.

#### Step 1 — Scope sanity check
- If user request describes 3+ independent concerns → flag for decomposition before continuing
- If trivial (single section update) → produce 5-line brief inline, skip approval gate

#### Step 2 — Question script (branched per type)

If type = landing — ask in this order via AskUserQuestion:
1. Product (one sentence: what + who + why now)
2. Primary audience (specific role)
3. Single conversion goal (signup / demo / buy / waitlist)
4. Vibe shortlist (1 anchor + 1 wildcard)
5. Inspirations (3 reference URLs)
6. Anti-references (2 to avoid)
7. Constraints (technical, deadline, budget)

If type = portfolio — ask in this order:
[7-question portfolio script - mirrors existing]

If type = generic — ask:
1. Page-purpose (which of inform / convert / navigate / display data / collect input / story)
2. Marketing intent flag (true / false)
3. Audience + primary action
4. Vibe + wildcard
5. Inspirations + anti-references
6. Constraints

#### Step 3 — brief.md schema

Write plans/{date}-{slug}/brief.md with sections:
- Type + tier
- Product/owner one-liner
- Audience
- Primary action / conversion goal
- Vibe anchor + wildcard
- Inspirations (URLs)
- Anti-references (URLs)
- Constraints
- (generic tier) Page-Purpose Exercise answers

#### Step 4 — Approval gate
User reviews brief. Only proceed to Phase 2 once approved.

#### Step 5 — Forbidden brief patterns (auto-refuse)
- "Build a website" without audience or conversion goal → push back, ask for specifics
- Generic vibe ("modern", "clean", "professional") without anchor → push back
- 3+ inspirations all from same era / aesthetic → ask for variety
```

### Phase 6 inline protocol (replace `delegate to ck:plan`)

Structure (~80 lines):
```
### Phase 6 — Plan (inline plan protocol)

Skill writes plan files directly. Output: plans/{date}-{slug}/plan.md + phase-XX-*.md files.

#### Step 1 — plan.md template

```yaml
---
name: {slug}
status: pending
priority: {high|medium|low}
created: {date}
target: {type} {new|redesign}
blockedBy: []
blocks: []
---
```

Body sections: Source of truth · Context links · Goal · Phases table · Key dependencies · File ownership · Success criteria · Risks.

#### Step 2 — Phase decomposition rules

Each phase = one logical concern:
- Tier A (landing): scaffold/tokens → primitives → hero → social-proof → features → ... → final-cta → footer
- Tier B (portfolio): scaffold → primitives → hero-intro → work-grid → case-study(s) → about → ... → contact
- Tier C (generic): scaffold → primitives → sections (from Page-Purpose Exercise — pick from pattern library)

Append: 3D phase (if Phase 2d ≠ none), Animations pass, Responsive/a11y polish, Final audit.

#### Step 3 — Dependency analysis

For each phase, identify:
- Inputs (which files produced by previous phases)
- Outputs (which files/components produced)
- Blockers (must wait for which phases)
- Parallel candidates (can run alongside which other phases)

Default rule: Layout primitives → Sections (sections depend on primitives). Sections within same depth are parallel-safe.

#### Step 4 — File ownership contracts

For each phase, declare exact file paths owned (no other phase may write to these files). Use file-level granularity, not function-level.

#### Step 5 — Success criteria + Risks per phase

Each phase-XX.md must include explicit checkable success criteria and ≥2 identified risks with mitigations.

#### Step 6 — Approval gate
User reviews plan. Only proceed to Phase 7 once approved.
```

### Phase 7 inline protocol (replace `delegate to ck:cook`)

Structure (~60 lines):
```
### Phase 7 — Implement (inline implement protocol)

Skill implements directly from plan. Per CLAUDE.md: NO auto-commit — user reviews + commits manually.

#### Step 1 — Phase execution order
Follow plan.md dependency graph. Default sequential unless plan marks phases parallel-safe.

#### Step 2 — Per-phase constraints (enforce throughout)
- Custom icons only — NEVER `import` any icon library (zero npm install)
- Locked palette as Tailwind tokens — no inline hex outside SVG icon paths
- All fonts via next/font — no <link> CDN
- 3D components: 'use client' + dynamic import with ssr:false
- Copy is real draft, not Lorem, not AI cliché vocabulary (apply applicability matrix)
- Hero composition follows visual-direction.md (no centered-H1 unless minimal vibe)
- Motion respects locked Phase 2e intensity; `prefers-reduced-motion` honored
- Total motion JS bundle ≤100KB gzipped

#### Step 3 — Mid-implementation checks
After each section completes, spot-check:
- Imports list — any forbidden library?
- Color values — any inline hex outside theme?
- Copy — any "Elevate / Seamless / Unleash"?
- Motion — any `ease-in-out 0.3s` default?
- Icons — any emoji?

#### Step 4 — Commit pattern (when user commits manually)
- One phase = one focused commit
- Commit message: conventional commits format (feat: / fix: / refactor: / docs:)
- No AI-tool references in commit messages
- Stage files explicitly (no `git add .`)
- pre-commit hooks pass (lint, type-check)

#### Step 5 — Phase completion check
- Mark phase status: completed in phase-XX.md
- Update plan.md phase table
- Update plan.md success criteria checkboxes
```

### Phase 8 inline protocol (replace `delegate to code-reviewer`)

Structure (~50 lines):
```
### Phase 8 — Anti-Slop Review (inline audit protocol)

Skill runs audit directly. No external agent delegation. Output: plans/{date}-{slug}/anti-slop-report.md.

#### Step 1 — Determine tier + applicable rules
From session: --type, tier (special/generic), marketing-intent flag.
Filter rules per `anti-slop-rules.md` § Applicability Matrix.

#### Step 2 — Run grep checks (consolidated bash block)

Universal grep checks:
```bash
grep -rE '[\x{1F300}-\x{1FAFF}]' app/                           # Emoji
grep -rE 'lucide-react|@heroicons|phosphor|@tabler' app/        # Icon libraries
grep -rE 'Inter|Roboto|"Open Sans"|Space Grotesk' app/          # Forbidden fonts
grep -rE '\bh-screen\b' app/                                    # h-screen
grep -rE '#[0-9a-fA-F]{6}' app/components/                      # Inline hex
grep -rE '(ease-in-out|ease-out|"easeInOut")' app/components/   # Generic easing
grep -rE 'useReducedMotion|prefers-reduced-motion' app/         # Motion respect
```

Marketing-only grep checks (only if tier=special OR marketing-intent=true):
```bash
grep -rEi 'elevate|seamless|unleash|empower|game.?changer|next.?gen' app/
grep -rE '"Get Started"|"Sign In"|"Subscribe"' app/
grep -rE 'from-purple-.*to-blue-' app/
```

Portfolio-only grep checks (only if --type=portfolio):
```bash
grep -rEi "hi,?\\s+i'?m\\s|hello,?\\s+world|passionate (designer|developer)" app/
grep -rEi 'proficiency|years of experience' app/
```

#### Step 3 — Visual checks (via vision-capable model)
- Render screenshot of key sections (hero, mid, footer)
- Send to vision-capable model with prompt: "Extract dominant colors. Count distinct accent values. Describe vibe in 3 words. Score vibe-match against locked direction."
- Compare against visual-direction.md locked values

#### Step 4 — Output report
Write plans/{date}-{slug}/anti-slop-report.md:
- Applicable rules count + skipped count
- Per-grep PASS/FAIL
- Visual check scores
- Recommendations for FAIL items

If any FAIL → return to Phase 7 to fix. Repeat until clean.
```

### Phase 4 tool routing → capability table

Replace existing "Tool routing (by style)" table:

```
| Style | Capability needed |
|-------|-------------------|
| Silkscreen / hand-drawn / cut-paper / risograph / watercolor | Text-to-image with style control + curated style prompt library |
| Engraved line-art / vintage patent | Text-to-image with creative direction freedom (wild mode) |
| Geometric flat (SVG) | Direct SVG generation by LLM (inline code) |
| Architectural schematic | Text-to-image with technical aesthetic + vector trace if SVG needed |
| Static 3D render → 2D | 3D modeling tool (Blender / Spline / KeyShot) exporting PNG/WebP — never .glb |
| Photographic | Real photos preferred; AI fallback with photorealism + anti-stock negatives |
| Synthwave gradient | Text-to-image with style control (retro-futuristic vibe only) |
| OG image | Multi-platform social image composition (HTML→screenshot or text-to-image) |
```

## Related code files

**Modify:** `references/workflow-phases.md` (single file, multiple sections)

**Create / Delete:** None

## Implementation steps

1. **Read full workflow-phases.md** to identify exact line ranges for: Phase 1 (lines ~62-125), Phase 4 tool routing table (~283-292), Phase 6 (~357-405), Phase 7 (~408-440), Phase 8 (~441-end)
2. **Rewrite Phase 1** with inline brainstorm protocol per Architecture above
3. **Rewrite Phase 6** with inline plan protocol per Architecture above
4. **Rewrite Phase 7** with inline implement protocol per Architecture above
5. **Rewrite Phase 8** with inline audit protocol per Architecture above
6. **Replace Phase 4 tool routing table** with capability table per Architecture above
7. **Final scan** — `grep -E 'ck:|ckm:|code-reviewer' workflow-phases.md` → 0 matches

## Todo list
- [ ] Read workflow-phases.md, locate Phase 1/4/6/7/8 line ranges
- [ ] Rewrite Phase 1 with inline brainstorm protocol
- [ ] Rewrite Phase 6 with inline plan protocol
- [ ] Rewrite Phase 7 with inline implement protocol
- [ ] Rewrite Phase 8 with inline audit protocol
- [ ] Replace Phase 4 tool routing table with capability table
- [ ] Verify 0 matches for ck:/ckm:/code-reviewer in workflow-phases.md
- [ ] Verify file size <800 lines (target) or <1200 (hard limit)

## Success criteria
- workflow-phases.md contains 4 inline protocols (Phase 1/6/7/8)
- workflow-phases.md Phase 4 has capability table (no specific tool names)
- 0 ck:/ckm: matches in workflow-phases.md
- 0 "code-reviewer agent" / "code-reviewer subagent" matches in workflow-phases.md
- File size ≤ 800 lines (target) or ≤ 1200 (hard limit)
- Existing landing/portfolio Phase 0/0.5/2/3/5 sections untouched

## Risk assessment
- **Risk:** File exceeds 1200 lines → split into sub-references (workflow-brainstorm.md, workflow-plan.md). Mitigation: keep protocols concise — essence only, not implementation details
- **Risk:** Inline protocols differ from existing ck-skill behaviors → user accepts (NOT copy 100%; adapt for perfect-ui)
- **Risk:** Phase 2 / Phase 5 sections accidentally modified → diff review before commit

## Security considerations
None — documentation-only changes.

## Next steps
- Phase 02 references this file's capability table mapping
- Phase 03 SKILL.md references this file's inline protocols
