# Phase 04 — README.md update

## Context links
- [brainstorm.md](./brainstorm.md) § Final design > Files modified > README.md
- [phase-03-skill-md-scope-update.md](./phase-03-skill-md-scope-update.md) — depends on (for scope consistency)
- [README.md](../../README.md) — file to modify (363 lines)

## Overview
- **Priority:** Medium (public-facing docs — drift from SKILL.md confuses users)
- **Status:** pending
- **Depends on:** Phase 03 (scope decisions locked in SKILL.md)
- **Parallel-safe with:** Phase 05 (index.html — different file, different content)
- **Description:** Remove Example 3 (dashboard refusal), add 2 non-marketing examples (blog/about + dashboard), update FAQ "Can I use this for blog sites?", bump version 2.0.0 → 2.1.0.

## Key insights
- README is public-first content — must read naturally, not feel like changelog
- Example 3 (dashboard refusal) currently exists at lines ~127-135; entire block must be replaced
- FAQ entry "Q: Can I use this for blog sites?" currently says "Not yet" — must update
- Version mention at line 5: `**Version:** 2.0.0` — bump

## Requirements

### Functional
- Replace Example 3 (refusal) with 2 new examples:
  - **New Example 3:** Blog or about page — demonstrates generic-tier flow
  - **New Example 4:** Dashboard — demonstrates generic-tier with evidence-base disclosure
- Update FAQ:
  - "Q: Can I use this for blog sites?" → answer: "Yes — generic tier supports any page type. Landing/portfolio get rich anatomy; everything else uses generic anatomy."
  - Add new Q: "What about dashboards/admin/e-commerce?" → answer with evidence-base honesty
- Update intro § What it does to mention scope is now any page (not landing/portfolio only)
- Update § Usage > Trigger phrases — keep landing/portfolio sections, add general "design a [page type]" section, remove "Off-scope (refused, redirected)" subsection
- Version bump 2.0.0 → 2.1.0

### Non-functional
- Tone matches existing README (casual but technical)
- Examples follow existing format (Input quote + numbered skill-flow steps)
- Keep file size <500 lines (currently 363)

## Architecture

### Example 3 replacement
**Current location:** Roughly lines 127-135 (Example 3 — dashboard refusal)

**Delete this block:**
```markdown
### Example 3 — User request that gets refused

**Input:**
> Build me an admin dashboard with a sidebar and analytics charts.

**Skill response:**
> perfect-ui scope = marketing-style sites only (landing/portfolio).
> For an admin dashboard with sidebar and charts, use `ck:frontend-development` instead — it has React/TypeScript patterns suited to app surfaces.
> If you need a marketing landing page FOR your admin tool, that's in scope — clarify and we'll proceed.
```

**Replace with:**
```markdown
### Example 3 — Blog page (generic tier)

**Input:**
> Design a blog landing for a typography studio's writing. Editorial vibe, long-form serif.

**Skill flow:**
1. Phase 0 — detects `new`
2. Phase 0.5 — detects `blog` keyword → generic tier
3. Phase 1 — `ck:brainstorm` runs page-purpose brief (audience, content type, primary action)
4. Phase 2 — locks editorial vibe (PP Editorial Old + Söhne, cream + ink palette)
5. Phase 3 — minimal icon set (3 icons: tag-glyph, link-arrow, social)
6. Phase 4 — letter-form illustration as hero accent
7. Phase 5 — skipped
8. Phase 6 — `ck:plan` outputs generic-tier plan: scaffold + hero + article-list + footer (sections driven by page-purpose, not template)
9. Phase 7 — `ck:cook` builds it
10. Phase 8 — audit runs universal anti-slop subset (no marketing-only rules triggered) — passes

### Example 4 — Dashboard (generic tier with evidence disclosure)

**Input:**
> Design a dashboard for a self-hosted analytics tool. Brutalist vibe, dense info, dark mode.

**Skill response:**
> Note: skill's evidence base (12 marketing landings analyzed) does NOT cover dashboard patterns directly. Universal craft toolkit (vibe lock, custom icons, motion rules, anti-slop universal subset) applies. Output quality is best-effort, not evidence-backed. Proceeding.

**Skill flow:**
1. Phase 0 — detects `new`
2. Phase 0.5 — detects `dashboard` keyword → generic tier (warning logged)
3. Phase 1 — `ck:brainstorm` runs page-purpose brief (data being shown, user role, primary action)
4. Phase 2 — locks brutalist vibe (Söhne Mono + Söhne Breit, hi-contrast b/w + electric-yellow accent)
5. Phase 3 — 6 custom icons (data-source markers, filter glyphs)
6. Phase 4 — schematic illustration for empty-states
7. Phase 5 — skipped (data-heavy, no atmosphere needed)
8. Phase 6 — generic plan: sidebar + top-bar + chart-grid + data-table (sections driven by data hierarchy)
9. Phase 7 — `ck:cook` builds it
10. Phase 8 — audit skips marketing-only rules (no hero, no CTA, no feature-grid concept); universal rules pass
```

### FAQ update
Locate existing entries near end of README. Modify and add:

**Modify:**
```markdown
**Q: Can I use this for blog sites?**
A: Yes — blog is supported via generic tier. Skill applies vibe lock + custom icons + motion + universal anti-slop. Generic anatomy lets page-purpose drive sections rather than prescribing a template. Landing/portfolio remain the only types with full rich anatomy + section archetypes.
```

**Add (after blog FAQ):**
```markdown
**Q: Does this skill work for dashboards / admin / e-commerce?**
A: Yes — generic tier accepts any type. Skill logs a notice that the evidence base (12 marketing landings) doesn't cover app-surface patterns directly; output is best-effort universal craft. Vibe lock, custom icons, motion rules, and universal anti-slop still apply. For full Shopify backend, `ck:shopify` covers commerce internals; for deep app-surface work, `ck:frontend-development` covers app architecture — but perfect-ui isn't a refusal for these.
```

### Intro § What it does — append paragraph
After existing "What it does" prose, add:
```markdown
**v2.1.0 update:** Skill scope opens beyond landing/portfolio. `--type` now accepts any page type. Landing and portfolio keep rich anatomy + skeleton + section archetypes. All other types (blog, about, pricing, contact, coming-soon, dashboard, admin, e-commerce, custom) use generic anatomy + skeleton with the same universal toolkit. No refusals.
```

### § Usage > Trigger phrases update
**Current structure:**
- Landing page (list of phrases)
- Portfolio (list of phrases)
- Off-scope (refused, redirected) — DELETE this subsection

**New structure (after deleting refusal):**
- Landing page (list of phrases — unchanged)
- Portfolio (list of phrases — unchanged)
- **Generic (any other type):** add example phrases:
  - "design my pricing page"
  - "build a blog landing"
  - "create an about page"
  - "design a dashboard for my analytics tool"
  - "make a contact page"

### Version bump
Line 5: `**Version:** 2.0.0` → `**Version:** 2.1.0`

## Related code files

**Modify:**
- `README.md`
  - Line 5 version
  - § What it does append
  - § Examples block (Example 3 replace, Example 4 add)
  - § Usage > Trigger phrases (delete off-scope, add generic)
  - § FAQ (modify blog Q, add dashboard Q)

**Create:** None
**Delete:** Off-scope subsection within Trigger phrases; Example 3 refusal block

## Implementation steps

1. **Read `README.md`** to locate exact line ranges:
   - Line 5: version
   - § What it does section
   - § Examples (specifically Example 3)
   - § Usage > Trigger phrases (Off-scope subsection)
   - § FAQ (blog Q, anywhere reasonable to add dashboard Q)

2. **Update version** line 5 → `2.1.0`

3. **Append v2.1.0 update paragraph** at end of § What it does

4. **Replace Example 3** with new Example 3 (blog) and add Example 4 (dashboard)

5. **Update § Usage > Trigger phrases:**
   - Delete "Off-scope (refused, redirected)" subsection
   - Add "Generic (any other type)" subsection with example phrases

6. **Update FAQ:**
   - Find existing "Q: Can I use this for blog sites?" → replace answer
   - Add new entry "Q: Does this skill work for dashboards/admin/e-commerce?" after blog entry

7. **Validation pass:**
   - Re-read README.md
   - Confirm no "refuse" / "refused" / "off-scope" language remains
   - Confirm version is 2.1.0
   - Confirm 4 examples now (was 3), 1 more FAQ entry

## Todo list
- [ ] Read README.md, locate line ranges
- [ ] Update version 2.0.0 → 2.1.0
- [ ] Append v2.1.0 update paragraph to § What it does
- [ ] Replace Example 3 with blog example
- [ ] Add Example 4 (dashboard)
- [ ] Update Trigger phrases (delete off-scope, add generic)
- [ ] Update blog FAQ entry
- [ ] Add dashboard FAQ entry
- [ ] Final read-through

## Success criteria
- README version = 2.1.0
- 4 examples (was 3); Example 3 = blog, Example 4 = dashboard
- No "off-scope" / "refused" language anywhere
- Blog FAQ answer changed from "Not yet" to affirmative
- Dashboard FAQ entry added
- Generic trigger phrases listed under § Usage

## Risk assessment
- **Risk:** Lose tonal consistency with existing examples → mirror format exactly (Input quote + numbered Skill flow)
- **Risk:** FAQ contradicts SKILL.md scope → cross-check Phase 03 SKILL.md output before finalizing answers
- **Risk:** Generic trigger phrases too broad → keep them specific (page types, not "anything web")

## Security considerations
None.

## Next steps
- Phase 05 (index.html) updates separately — parallel-safe
- Final check: README + index.html scope language matches SKILL.md
