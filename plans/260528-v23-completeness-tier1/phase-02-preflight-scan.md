# Phase 02 — Pre-flight scan (NEW file + workflow integration)

## Context links
- [brainstorm.md](./brainstorm.md) § Item C (Pre-flight scan)
- [references/workflow-phases.md](../../references/workflow-phases.md) — file to modify
- [references/preflight-scan.md] — file to CREATE
- [phase-01-anti-slop-updates.md](./phase-01-anti-slop-updates.md) — parallel-safe

## Overview
- **Priority:** High (new behavior — auto-detect existing tokens before designing)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 03, 04 (different files)
- **Description:** Create `references/preflight-scan.md` (~80 lines) with auto-detect logic + 6 signal sources + output format + persistence + edge cases. Add Phase 0.1 section to workflow-phases.md + Phase 7 honest copy constraint.

## Key insights
- Auto-detect mode: scan triggers when ANY of {package.json / tailwind.config / framework config / *.css in root / index.html} present; silent on empty repo
- Cache findings to `.perfect-ui/preflight.json` at project root; reuse unless mtime newer or user requests refresh
- 6 signal sources: font stack / palette / motion library / spacing scale / framework / icon library flag
- Icon library detection flags forbidden-by-Hard-Rule-#2 libraries (lucide-react, heroicons, phosphor) for replacement
- Output ≤6 lines preserve/introduce summary

## Requirements

### Functional
- NEW `references/preflight-scan.md` covers: detection trigger + signal sources + output format + persistence + edge cases
- workflow-phases.md gets new § Phase 0.1 (between current Phase 0 and Phase 0.5) referencing the new file
- workflow-phases.md Phase 7 § per-phase constraints gets new "Honest copy" line referencing `anti-slop-rules.md § Honest Copy Mandate`
- Cache file location: `.perfect-ui/preflight.json` at project root
- Default `.gitignore` suggestion in scaffold mentions `.perfect-ui/`

### Non-functional
- preflight-scan.md ~80 lines (target)
- workflow-phases.md grows ~+25 lines (Phase 0.1 + Phase 7 constraint)
- No regression to existing Phase 0 / Phase 0.5 / Phase 7 content

## Architecture

### NEW `references/preflight-scan.md` structure

Already spec'd in brainstorm.md § Item C. Recap structure (8 sections):

```
# Pre-flight Scan

[Intro paragraph — when this runs, why it matters]

## Detection trigger
[List of files/dirs that trigger scan; silent on empty]

## What to scan (6 signal sources)
1. Font stack
2. Palette
3. Motion library
4. Spacing scale
5. Framework
6. Icon library (flag for replacement)

## Output format
[code block — preserve/introduce summary template]

## Persistence
[.perfect-ui/preflight.json + cache rules]

## Edge cases
- Conflicting signals
- No signals found
- User said "ignore existing project"
- Cache corrupt

## Two sample outputs
[Vanilla HTML project, motion-cut]
[Astro + Tailwind + DTCG tokens]
```

### workflow-phases.md — Phase 0.1 insertion

Insert AFTER existing Phase 0, BEFORE Phase 0.5:

```markdown
---

## Phase 0.1 — Pre-flight scan (auto-detect)

See `preflight-scan.md` for full protocol. Auto-detect logic:

- If target directory has existing project files (package.json / tailwind.config / framework configs / *.css / index.html) → run scan, emit findings block
- If empty repo → silent, one-line note, proceed to Phase 0.5
- Cache findings in `.perfect-ui/preflight.json`; reuse unless user requests refresh OR config mtimes newer than cache

Preserved tokens / fonts / motion library are carried into Phase 2 visual direction dialog. perfect-ui only introduces what's missing. If user explicitly says "ignore existing project" / "fresh start", skip scan and proceed.

For redesign mode (Phase 0 set `redesign`), pre-flight runs IN ADDITION to redesign-audit-checklist.md — preflight scans tokens, audit assesses visual design.
```

### workflow-phases.md — Phase 7 constraint addition

In Phase 7 § per-phase constraints, add to existing list (after Copy section):

```markdown
- **Honest copy** — if metric / testimonial / logo / case-study count not supplied by user, use em-dash placeholder + label (`— metric to confirm`) rendered as visible grey block. Never invent. See `anti-slop-rules.md § Honest Copy Mandate` for 3 accepted paths.
```

## Related code files

**Create:** `references/preflight-scan.md` (NEW)

**Modify:** `references/workflow-phases.md` (2 surgical edits — Phase 0.1 + Phase 7 constraint)

## Implementation steps

1. **Write NEW `references/preflight-scan.md`** (~80 lines) following structure spec'd in brainstorm.md § Item C
2. **Read `references/workflow-phases.md`** to locate:
   - End of Phase 0 (mode detection) — insert Phase 0.1 after this
   - Phase 7 § per-phase constraints — append honest copy line
3. **Insert Phase 0.1 section** between Phase 0 and Phase 0.5 (use `---` separator + heading style consistent with existing)
4. **Append honest copy constraint** to Phase 7
5. **Verify cross-references** — workflow-phases.md Phase 0.1 must link to `preflight-scan.md`; Phase 7 must link to `anti-slop-rules.md § Honest Copy Mandate` (Phase 01 creates this section)

## Todo list
- [ ] Write `references/preflight-scan.md` (~80 lines)
- [ ] Read workflow-phases.md, locate Phase 0 end + Phase 7 constraints
- [ ] Insert Phase 0.1 section
- [ ] Append honest copy constraint to Phase 7
- [ ] Verify cross-references resolve (link targets exist or will exist after Phase 01)

## Success criteria
- `references/preflight-scan.md` exists, ~80 lines, all 8 sections present
- workflow-phases.md has new Phase 0.1 section (between Phase 0 and Phase 0.5)
- workflow-phases.md Phase 7 has honest copy constraint line
- File size workflow-phases.md ≤+30 lines net
- No regression to existing Phase 0 / Phase 0.5 / Phase 7 content
- Cross-refs (Phase 01 anti-slop-rules.md § Honest Copy Mandate) resolve after parallel completion

## Risk assessment
- **Risk:** Phase 0.1 disrupts existing Phase 0 / Phase 0.5 numbering or table-of-contents → verify section order intact after edit
- **Risk:** Preflight output format too verbose → cap at ≤6 bullet lines per brainstorm spec
- **Risk:** Cache invalidation race condition (user edits package.json between runs) → cache check on every run uses mtime comparison, not just existence
- **Risk:** Cross-ref to anti-slop-rules.md § Honest Copy Mandate fails if Phase 01 not complete → Phase 02 and 01 are parallel-safe; both phases must complete before Phase 05 validates references

## Security considerations
- `.perfect-ui/preflight.json` MAY contain detected font names / framework / motion lib — non-sensitive
- Recommend adding `.perfect-ui/` to default `.gitignore` suggestion (in preflight-scan.md or future scaffold)

## Next steps
- Phase 05 references Phase 0.1 in SKILL.md process flow diagram (+ Mermaid node)
- README.md FAQ entry for "what is pre-flight scan" (Phase 05)
- index.html Pipeline section may add Phase 0.1 card (defer — Phase 05 will decide whether to add or skip)
