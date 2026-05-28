# Phase 03 — NEW preemit-design-plan.md + workflow-implement.md Phase 7 gate

## Context links
- [brainstorm.md](./brainstorm.md) § Item Q (Structured `<design_plan>` block)
- gpt-taste reference (origin): `~/.claude/skills/gpt-taste/SKILL.md § 8. MANDATORY PRE-FLIGHT <design_plan>`

## Overview
- **Priority:** High (pre-emit gate — strongest quality enforcement v2.5.0 adds)
- **Status:** pending
- **Parallel-safe with:** Phase 01, 02 (distinct files)
- **Description:** CREATE `references/preemit-design-plan.md` (~80 lines). MODIFY `references/workflow-implement.md` (~+40 lines) — Phase 7 pre-emit gate + component-scope short-circuit.

## Key insights
- Pre-emit gate runs at Phase 7 entry, BEFORE any code emission
- 10 verification fields (full superset)
- Many fields auto-verifiable (no user prompt)
- Collect-all-errors approach: user fixes once, re-runs gate
- Component-scope runs MINIMAL subset (skip macrostructure / bento / label fields)
- Block emitted as CSS comment + plans/{slug}/plan.md § Pre-emit verification (BOTH placements per sub-decision 2)

## Requirements

### Functional
- preemit-design-plan.md has 5 sections: When applies / 10-field schema / Verification logic / Component-scope subset / Stamp placements
- 10 fields documented with example values + validation rules
- Verification logic: read block → check fields → collect errors → return to relevant phase if fail
- Component-scope subset (skip macrostructure / bento / label fields)
- Block placement BOTH: CSS comment (durable record) + plans/{slug}/plan.md § Pre-emit verification (audit trail)
- workflow-implement.md Phase 7 entry gate + component-scope short-circuit documented

### Non-functional
- preemit-design-plan.md ~80 lines
- workflow-implement.md grows ~+40 lines
- KISS — block format YAML-like for readability

## Architecture

### preemit-design-plan.md structure (~80 lines)

```markdown
# Pre-emit `<design_plan>` Block (v2.5.0+)

Mandatory pre-emit verification at Phase 7 entry. Forces structured plan output covering 10 verification fields. Catches drift between locked picks (Phases 1-6) and intended implementation (Phase 7) BEFORE code emission.

## When this applies

Phase 7 entry — before any code is written, before `phase-XX-*.md` files are populated.

Component-scope runs MINIMAL subset (skip macrostructure_diversification / bento_density / label_sweep fields — not applicable).

## 10-field block schema

```yaml
<design_plan>
  macrostructure_diversification:
    last_3: ["Marquee Hero", "Bento Grid", "Long Document"]
    pick: "Manifesto"
    differs_from_last_3: true
    diversification_rule_pass: true

  vibe_validity:
    anchor: "editorial"
    wildcard: "agrarian"
    contradiction: false
    valid: true

  dial_alignment:
    design_variance: 6
    visual_density: 4
    vibe_default_diff: 0
    macrostructure_within_pm_2: true

  motion_personality:
    name: "Premium"
    vibe_default_match: true
    override_logged: false

  hero_math:
    line_range_target: "1-3"
    container_class: "max-w-5xl"
    h1_font_class: "clamp(3rem, 5vw, 5.5rem)"
    projected_lines: 2
    universal_4plus_ban_pass: true

  bento_density:
    applicable: false
    # OR if Bento Grid macrostructure:
    # applicable: true
    # grid_flow_dense: true
    # span_interlock_verified: true

  label_sweep:
    meta_labels_found: 0
    long_document_exception: false
    pass: true

  button_contrast:
    eight_states_planned: ["default", "hover", "focus", "active", "disabled", "loading", "error", "success"]
    focus_ring_visible: true
    contrast_aa_pass: true

  honest_copy:
    fabricated_metrics: 0
    placeholders_required: 3
    em_dash_format: "— metric to confirm"

  gsap_decision:
    intensity: "2/3"
    gsap_needed: false
    skills_route: "n/a"
</design_plan>
```

## Verification logic

At Phase 7 entry:

1. Read locked picks from Phases 1-6 (brief.md, visual-direction.md, plan.md)
2. Populate 10 fields per schema above
3. Run validation per field (see field rules below)
4. **Collect all errors** (not fail-fast — user fixes once)
5. If any FAIL → return user to relevant phase to fix:
   - macrostructure_diversification fail → Phase 2.5
   - vibe_validity fail → Phase 1
   - dial_alignment fail → Phase 2
   - motion_personality fail → Phase 2.6
   - hero_math fail → Phase 2 + visual-direction-guide review
   - bento_density fail → Phase 2.5 or macrostructure-catalog § Bento Grid
   - label_sweep fail → anti-slop-rules § Tier 1 rule #12
   - button_contrast fail → component design (interaction-and-states)
   - honest_copy fail → anti-slop-rules § Honest Copy Mandate
   - gsap_decision fail → gsap-integration.md
6. If ALL PASS → block stamped, Phase 7 proceeds

## Field validation rules

- **macrostructure_diversification:** read `.perfect-ui/log.json` last 3 entries; pick must NOT match any
- **vibe_validity:** anchor + wildcard must not be obvious contradictions (e.g. "minimal + maximalist")
- **dial_alignment:** dials within ±2 of vibe defaults OR macrostructure adjustment within ±2 OR user override logged
- **motion_personality:** matches per-vibe default OR override logged
- **hero_math:** container max-w + H1 clamp() guarantees line_range_target; projected_lines ≤ vibe ceiling
- **bento_density:** if applicable, grid_flow_dense + span_interlock verified
- **label_sweep:** zero meta-labels OR Long Document macrostructure exception (≤5 ordinal)
- **button_contrast:** 8 states planned + focus ring visible + WCAG AA contrast
- **honest_copy:** zero fabricated metrics (placeholders match metric needs)
- **gsap_decision:** intensity 3/3 OR keyword → gsap_needed true; otherwise false

## Component-scope subset

Component-scope runs MINIMAL block (4 fields):
- vibe_validity
- motion_personality
- button_contrast (8 states applicable)
- honest_copy

Skip: macrostructure_diversification, dial_alignment, hero_math, bento_density, label_sweep, gsap_decision (none apply at component level).

## Stamp placements

Block stamped in TWO locations:

1. **CSS comment** at top of generated CSS file (durable record):
   ```css
   /* perfect-ui · <design_plan> v2.5.0
    * (all 10 fields verified — see plans/{slug}/plan.md § Pre-emit verification)
    */
   ```

2. **plans/{date}-{slug}/plan.md § Pre-emit verification** (audit trail):
   Full 10-field block embedded in plan.md as fenced YAML.

## Cross-references

- `workflow-implement.md § Phase 7 entry` — pre-emit gate runs here
- `workflow-brainstorm.md § Phase 1 brief` — vibe_validity sources
- `visual-direction-guide.md` — dial_alignment + hero_math fields source
- `motion-patterns.md § Motion Personalities` — motion_personality field source
- `macrostructure-catalog.md` — bento_density field source
- `anti-slop-rules.md § Honest Copy Mandate` + § Diversification Rule — honest_copy + macrostructure_diversification source
- `gsap-integration.md` — gsap_decision field source
- `component-scope.md` — subset block applies in component-scope runs
```

### workflow-implement.md — Phase 7 pre-emit gate + component-scope short-circuit

Insert NEW § Step 1.5 — Pre-emit design_plan verification AFTER existing Step 1 (Phase execution order), BEFORE Step 2 (Per-phase constraints):

```markdown
## Step 1.5 — Pre-emit `<design_plan>` verification (v2.5.0+)

At Phase 7 entry, BEFORE any code emission, run the pre-emit design_plan verification gate. See `preemit-design-plan.md` for full 10-field schema + validation rules.

1. Populate 10-field block from Phases 1-6 locked picks
2. Run validation; collect all errors
3. If any FAIL → return to relevant phase to fix; do NOT proceed to Step 2
4. If ALL PASS → block stamped in CSS + plans/{slug}/plan.md § Pre-emit verification; Step 2 proceeds

**Component-scope runs minimal subset (4 fields):** vibe_validity, motion_personality, button_contrast, honest_copy. See `preemit-design-plan.md § Component-scope subset`.
```

Insert NEW § Step 1.6 — Component-scope short-circuit AFTER Step 1.5:

```markdown
## Step 1.6 — Component-scope short-circuit (v2.5.0+)

If Phase 0.5 detected component-scope (see `component-scope.md`), Phase 7 collapses page-level emission:

- **Skip:** project scaffold (single component), macrostructure-driven section sequence, hero enrichment, multi-section composition
- **Emit:** 2 files — component artifact (Button.tsx / Card.vue / button.css+html / etc.) + `.preview.*` 8-state wrapper (extension auto-detected from framework, per `component-scope.md § What component-scope EMITS`)
- **Stamp:** component-scoped CSS comment (see `component-scope.md § Stamp format`)

Skip Step 6 (project memory log write) — component runs don't rotate.

After 2 files emitted, Phase 7 complete. Continue to Phase 8 audit (component-scope subset; see `workflow-audit.md`).
```

## Related code files

**Create:** `references/preemit-design-plan.md` (NEW, ~80 lines)

**Modify:** `references/workflow-implement.md` (+ Step 1.5 + Step 1.6, ~+40 lines)

## Implementation steps

1. Read gpt-taste `~/.claude/skills/gpt-taste/SKILL.md § 8. MANDATORY PRE-FLIGHT <design_plan>` for inspiration
2. Write `references/preemit-design-plan.md` with 5 sections + 10-field schema + validation logic
3. Read workflow-implement.md to identify insertion point (between Step 1 and Step 2)
4. Insert Step 1.5 (pre-emit gate) and Step 1.6 (component-scope short-circuit)
5. Verify cross-references

## Todo list
- [ ] Read gpt-taste design_plan reference
- [ ] Write preemit-design-plan.md with 5 sections
- [ ] 10-field schema with YAML format
- [ ] Field validation rules
- [ ] Component-scope subset (4 fields)
- [ ] Stamp placements (CSS + plan.md)
- [ ] Insert Step 1.5 in workflow-implement.md (pre-emit gate)
- [ ] Insert Step 1.6 in workflow-implement.md (component-scope short-circuit)
- [ ] Verify cross-references

## Success criteria
- preemit-design-plan.md exists, ~80 lines, 5 sections
- 10-field block schema documented with example values
- Validation rules + error routing documented
- Component-scope subset (4 fields) spec'd
- BOTH placements (CSS comment + plan.md section) documented
- workflow-implement.md has Step 1.5 + Step 1.6
- Cross-references to all 8 relevant files documented

## Risk assessment
- **Risk:** 10 fields = friction at every Phase 7 entry → many auto-verifiable (no prompt); collect-all-errors approach
- **Risk:** Component-scope subset confusion → explicit 4-field list in preemit-design-plan.md
- **Risk:** Stamp dual-placement diverges (CSS vs plan.md) → CSS is short summary, plan.md full block; explicit difference

## Security considerations
None — documentation only.

## Next steps
- Phase 04 routes Phase 0 / 0.5 mode detection
- Phase 05 SKILL.md References + Hard Rule #11 (pre-emit verification) reference this file
