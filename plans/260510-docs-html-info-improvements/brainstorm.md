# Brainstorm — `index.html` (docs page) info improvements

**Date:** 2026-05-10
**Owner:** dris1153
**Target file:** `index.html` (single-page editorial-vibe docs for `perfect-ui` skill)
**Status:** Design approved by user. Ready for `/ck:plan`.

---

## Problem statement

`index.html` hiện 779 lines, 6 sections (Hero / Scope / Pipeline / Vibes / Anti-slop / Getting Started). Editorial vibe: cream `#F5F1E8` + ink `#1A1715` + dusk-rose `#B8635A`, Instrument Serif + Geist + Geist Mono, asymmetric 12-col grid. Đẹp nhưng **thiếu nhiều info load-bearing có trong README** — đặc biệt info bán-được-skill cho general visitors.

### Gaps identified

**Critical (mất motivation/credibility):**
- Why-it-exists story — 12 real landings analyzed (5 AI + 7 human), AI stack 10+ slop violations vì chọn ALL safe defaults. USP mạnh nhất nhưng absent.
- Worked examples — 3 cases (coffee landing, portfolio redesign, dashboard refused). Concrete demonstrations missing.
- Hard rules — 8 non-negotiable mandates (NO emoji, NO icon libs, NO 3D hero, vibe-before-pixels…). Anti-slop section chỉ show audit patterns, không show doctrine.

**Useful (hỗ trợ ra quyết định):**
- CLI flags & args (`--type`, `--new/--redesign`, `--no-3d`, `--stack`)
- Related skills compass (when to use this vs `ck:frontend-development` vs `ck:frontend-design` vs `ck:shopify`)
- Loading UI criteria (3 conditions splash earns place)

### Inconsistencies cần fix song song

- **Version mismatch** — Hero meta hiện `v0.0.1`, SKILL.md frontmatter có `version: "2.0.0"`, README ghi `Version 2.0.0`. → fix về `v2.0.0`.
- **File name mismatch** — File-structure block (line 743) ghi `docs.html (this file)` nhưng file thật là `index.html`. → fix về `index.html (this file)`.

---

## Constraints

- **Audience:** general visitor — phải bán được skill cho người chưa dùng VÀ serve as reference cho người đang dùng.
- **Page growth tolerance:** moderate — ~3-4 sections mới (page 779 → ~1200 lines OK).
- **Format mix:** flat + interactive (tabs) + visual-heavy (diagrams/swatches/grids) — open to all.
- **Cohesion mandate:** new sections KHÔNG được violate skill's own rules (no emoji, no icon libs, no AI slop). Reuse existing patterns (`sec-head`, `label`, `phase`, `tier`). No new fonts, no new accent colors.
- **Editorial restraint:** Tabs/interactivity dùng minimal styling (mono labels, accent bottom-rule on selected, no animation). Respect `prefers-reduced-motion`.

---

## Approaches evaluated

### Direction A — Evidence-first ("Why → Proof → How")
- Insert: Why-it-exists (sau Hero) → Examples (sau Pipeline) → Related skills (cuối). Hard rules merge vào anti-slop section.
- **Pros:** Strongest narrative arc cho người mới đánh giá skill.
- **Cons:** Push reference info xuống cuối. Power user phải scroll xa.

### Direction B — Reference-first ("How → Why")
- Insert: Hard rules ngay sau Hero → CLI flags trong Getting Started → Examples cuối → Why chỉ còn 1-2 callouts inline trong Hero.
- **Pros:** Tối ưu cho power user, scan nhanh, info-dense.
- **Cons:** General visitor thiếu motivation framing. "Buys-the-skill" story bị suy yếu.

### Direction C — Balanced (CHOSEN)
- 4 sections mới: Why → Mandates → Examples → Beyond. Plus inline expansions.
- **Pros:** Cân bằng narrative + reference. Mỗi section ngắn gọn, navigable. Phù hợp general visitor.
- **Cons:** Nhiều sections nhất (9 total). Risk feel cluttered nếu execute bad — mitigation: reuse existing patterns + generous whitespace.

**Decision:** Direction C — user approved.

---

## Final recommended solution

### Section structure (final order)

```
Hero
01  Why it exists       ← NEW   (~80 lines)
02  Scope               (existing, renumbered)
03  Pipeline            (existing — phase ∞ card expanded inline)
04  Vibes               (existing)
05  Anti-slop tiers     (existing)
06  Mandates            ← NEW   (~100 lines)
07  In practice         ← NEW   (~150 lines, interactive tabs)
08  Getting started     (existing — CLI flags table added inline)
09  Beyond perfect-ui   ← NEW   (~50 lines)
Footer
```

**Reasoning for order:**
- Why builds credibility BEFORE mechanics.
- Mandates flows naturally từ Anti-slop tiers (patterns → doctrine = audit signal → mandates).
- Examples sau cùng trong "how" cluster — đến lúc đó reader đã có vocab (phases, vibes, rules) để parse được examples.
- Beyond là natural exit ramp trước footer.

### Section specs

#### 01 — Why it exists (~80 lines)

Section header: `label: "— Why"` / heading: `<em>Made because</em> AI pages stack defaults.` / sec-meta: `plans/260509-ai-vs-human-analysis/synthesis.md`

**Stat row** (4 stats, reuse `stat-num` / `stat-label` from Hero):
- `12` Landings analyzed
- `5` AI-generated
- `7` Human-crafted
- `10+` Violations stacked per AI page

**Side-by-side comparison panel** (2-col, same gap as `scope-grid`):
- **Left col** — heading "AI defaults — stacked" (ink-muted color):
  - Inter font alone
  - Purple/blue gradient hero
  - `h-screen` everywhere
  - `lucide-react` icons
  - 3-col equal feature grid
  - "Get Started" CTAs
  - Round fake stats (10K+, 99.99%)
  - Fade-up on every element
- **Right col** — heading "Human commitment — singular" (full-ink color):
  - One vibe locked
  - Custom SVG icons
  - Asymmetric grid
  - Vibe-paired typography
  - Distinctive display fonts
  - Specific draft copy
  - Real evidence-based stats
  - Vibe-scaled motion
- Accent vertical rule between cols.

**Closing line:** "Cohesion is the multiplier on craft. This skill encodes that as enforceable rules."

#### 06 — Mandates (~100 lines)

Section header: `label: "— 06"` / heading: `<em>Eight mandates.</em> Non-negotiable.` / sec-meta: `SKILL.md § Hard Rules`

Subheading paragraph (1-2 sentences differentiating from Anti-slop):
> Mandates = doctrine (MUST / MUST NOT). Anti-slop tiers = audit patterns we grep for. Mandates exist as the WHY behind tier-1 patterns.

**4×2 card grid** (reuse `tier` border treatment, smaller padding):

| # | Headline | 1-line clarification |
|---|----------|----------------------|
| 01 | NO emoji — anywhere | Not in copy, headings, or as icons. Use custom SVG. |
| 02 | NO icon libraries | Lucide, Heroicons, Phosphor, Tabler, Font Awesome, Material, react-icons all forbidden. |
| 03 | NO AI slop defaults | Inter alone, purple/blue gradient, equal CTAs, "Elevate/Seamless/Unleash" copy. |
| 04 | NO 3D models as hero subject | Static render → PNG OK. Real-time GLB forbidden (user-product GLB needs override). |
| 05 | 3D = effects only | Phase 5 = shaders/particles/atmosphere. CSS first; WebGL only when CSS can't. |
| 06 | Always propose effect layer | Every site gets the proposal. User accepts or declines. |
| 07 | Vibe before pixels | Never write code or generate assets before vibe + palette + typography are locked. |
| 08 | Type-aware everything | Phase 1 brief, plan, anatomy, skeleton ALL branch by `--type`. |

Each card structure:
- Rule num (mono, accent color)
- Rule headline (Instrument Serif italic, ~22px)
- Clarification line (body font, ink-muted)

#### 07 — In practice (~150 lines)

Section header: `label: "— 07"` / heading: `<em>In practice.</em> Three real flows.` / sec-meta: `README.md § Examples`

**Tab implementation** — vanilla JS (~25 lines), proper ARIA:
- `role="tablist"` / `role="tab"` / `role="tabpanel"`
- `aria-selected` toggle on active tab
- Keyboard nav: Left/Right arrows + Home/End
- 3 tabs: "Coffee landing" / "Portfolio redesign" / "Dashboard refused"
- Active tab styling: monospace label + accent bottom-rule
- Mobile (<900px): tabs stack to vertical pill list, panels stack below
- No animation transitions (editorial-restrained)

**Per tab content shape:**
1. **Input quote** (italic display font, blockquote treatment) — verbatim user input
2. **Flow** (numbered list, mono-style refs to phases) — 5-7 steps
3. **Outcome** (1-2 sentence summary)

Tab 1 — Coffee landing:
> "Design a landing page for a new specialty coffee subscription service targeting home-brewing enthusiasts in Japan. Vibe should feel editorial and warm."
- Phase 0 detects `new` (no URL)
- Phase 0.5 detects `landing`
- Phase 1 → ck:brainstorm: editorial + agrarian (wildcard), 3 inspirations confirmed
- Phase 2 → palette `cream + ink + dusk-rose`, Migra + GT Sectra, asymmetric editorial spatial, 3D declined
- Phase 3 → 8 custom SVG icons (nav-mark, brewing steps, social marks)
- Phase 4 → silkscreen-style poster hero illustration via ck:ai-artist
- Phase 6-8 → ck:plan + ck:cook + Tier-1/2/3 audit passes

Tab 2 — Portfolio redesign:
> "Redesign this portfolio: https://my-old-site.com — I want it to feel more elegant and let my work speak. Currently has too many flashy hover effects."
- Phase 0 detects `redesign` (URL provided)
- Audit per `redesign-audit-checklist.md`: keep portfolio cover photo + monogram; kill hover-effect overload, skill-bar percentages, "Hi I'm passionate" opener
- Phase 0.5 detects `portfolio`
- Phase 1-2 → elegant vibe locked (PP Neue Montreal display, off-white, atmospheric)
- Phase 3-5 → minimal icon set (5 icons) + editorial portrait + 3D logo accent approved
- Phase 6-8 → Plan with `app/work/[slug]` case study route → audit catches "Welcome to my portfolio" leftover copy → ships

Tab 3 — Dashboard refused:
> "Build me an admin dashboard with a sidebar and analytics charts."
- **Refusal copy:** "perfect-ui scope = marketing-style sites only (landing/portfolio). For an admin dashboard with sidebar and charts, use `ck:frontend-development` instead — it has React/TypeScript patterns suited to app surfaces. If you need a marketing landing page FOR your admin tool, that's in scope — clarify and we'll proceed."
- Outcome: redirect, not refusal. Skill knows when to step aside.

#### 09 — Beyond perfect-ui (~50 lines)

Section header: `label: "— 09"` / heading: `<em>Beyond.</em> Where to go when this isn't the fit.` / sec-meta: `README.md § Related Skills`

**Flat 5-row table:**

| If you need… | Use instead |
|---|---|
| Full apps, dashboards, admin panels, complex multi-page IA | `ck:frontend-development` |
| Replicate exact design from screenshot/video | `ck:frontend-design` |
| Component-level UI work in existing apps | `ck:ui-ux-pro-max` |
| E-commerce stores | `ck:shopify` |
| Logo / CIP / banner / social-photo design (called by perfect-ui internally for icons) | `ckm:design` |

Mono-styled skill names (left-padded with leading rule). Generous row spacing.

### Inline expansions (no new section)

| Location | Change |
|---|---|
| Hero meta (line 376) | `v0.0.1` → `v2.0.0` |
| Pipeline phase ∞ card (~line 533) | Body expand: `Default no splash. Earns place only when assets need masking or brand moment justifies.` → `Default no splash. Earns place only when:` + bullet list (Heavy assets >1.5s · Brand mark moment · Curated narrative entrance) |
| Getting Started (~line 720) | Add CLI flags table dưới Trigger phrases — 4 rows: `--type`, `--new/--redesign`, `--no-3d`, `--stack` |
| File structure block (line 743) | `docs.html (this file)` → `index.html (this file)` |

### Cohesion guardrails

**Reuse existing CSS classes/patterns:**
- `sec-head` / `label` / `sec-meta` — section headers
- `stat-num` / `stat-label` — Why-section stats
- `tier` border treatment — Mandate cards (tighter padding)
- `phase` border treatment — alternative for Mandate cards if needed
- `grid-12` — outer grid
- `vibe-row` table styling — Beyond table can adapt

**No new tokens introduced:**
- Same palette (cream / ink / dusk-rose / accent-soft / rule)
- Same fonts (Instrument Serif / Geist / Geist Mono)
- Same spatial language (asymmetric 12-col, generous gaps)

**Tab styling — editorial-restrained:**
- Mono font labels, 12px, `letter-spacing: 0.15em`, uppercase
- Selected: accent bottom-rule (1px), full ink color
- Unselected: ink-muted, `border-bottom: 1px solid var(--rule)`
- No transitions on tab switch beyond color (already site default 0.3s cubic-bezier)
- Tab list: `display: flex; gap: 32px; border-bottom: 1px solid var(--rule)`

**Comparison panel styling (Why section):**
- 2 columns equal width, gap 64px
- Center vertical rule: `1px solid var(--rule)`, `accent` colored at midpoint dot
- Left col: heading `ink-muted`, list items `ink-muted`, mono items
- Right col: heading `ink`, list items `ink`, italic display heading
- Visual hierarchy: right col feels weightier (intentional — "human commitment wins")

---

## Implementation considerations

### Execution order (suggested phases)

1. **Phase 1 — Inline fixes** (low risk, isolated)
   - Hero meta version: `v0.0.1` → `v2.0.0`
   - File structure block: `docs.html` → `index.html`
   - Pipeline phase ∞ card: expand body
   - Getting Started: add CLI flags table

2. **Phase 2 — Why it exists section**
   - Insert after Hero (before existing Scope)
   - Stat block + comparison panel
   - Renumber existing Scope from "01" → "02"

3. **Phase 3 — Mandates section**
   - Insert after Anti-slop (before Getting Started)
   - 4×2 card grid
   - Renumber Getting Started "05" → "08"

4. **Phase 4 — In practice section + tabs JS**
   - Insert after Mandates (before Getting Started)
   - 3-tab interactive component
   - Add ~25 lines vanilla JS (ARIA + keyboard nav)

5. **Phase 5 — Beyond perfect-ui section**
   - Insert before footer
   - Flat 5-row table

6. **Phase 6 — Section number cascade**
   - Update all `label` numbers across sections to match new order
   - Verify mobile responsiveness for new sections
   - Run anti-slop self-audit

### Risks + mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| Page feels cluttered with 9 sections | Medium | Generous section padding (already 96px). Section dividers with `border-top: 1px solid var(--rule)`. Each new section ≤150 lines. |
| Mandate section overlaps với Anti-slop tier 1 patterns | Medium | Explicit subheading clarifying doctrine vs audit-pattern distinction. Different visual treatment (cards vs single tier blocks). |
| Tabs JS introduces SaaS-y feel | Medium | Editorial-restrained styling (mono labels, no transition animations, accent rule only). Plain HTML buttons + minimal JS. |
| Tabs accessibility broken | High | Full ARIA roles, keyboard nav (Arrow keys + Home/End), focus-visible styles. Test with keyboard-only nav. |
| Mobile responsiveness của new sections (especially comparison panel + tabs) | Medium | Comparison panel: stack to single column at <900px. Tabs: convert to vertical pill list at <900px. |
| Page weight tăng | Low | New content is mostly text + reused styles. Estimated +6-8KB unminified. No new fonts, no images. |
| Anti-slop self-violation | High | Mandatory pre-ship audit: grep for `lucide`, `purple-`, `h-screen`, emoji unicode ranges, `Get Started`. Verify zero hits. |
| User-provided URL placeholders break (Tab 2 has fake URL) | Low | Use clearly-fake `https://my-old-site.com` style, comment it as illustrative. |

### Out of scope (explicitly deferred)

- No new fonts, no new accent colors, no logo redesign.
- No interactive vibe-explorer (clicking a vibe → live palette preview). Could be future enhancement.
- No live demo embed of skill output. Out of scope for static docs page.
- No FAQ section — questions distributed inline where relevant. Full FAQ stays in README.
- No changelog / version history section. Version sync only.
- No internationalization. English-only as is.

---

## Success metrics + validation

**Content completeness:**
- [ ] All 8 hard rules listed in Mandate section match SKILL.md doctrine
- [ ] All 3 examples match README § Examples verbatim or near-verbatim
- [ ] All 5 related skills in Beyond table match README § Related Skills
- [ ] Stat numbers (12 / 5 / 7 / 10+) verified against `plans/260509-ai-vs-human-analysis/synthesis.md`

**Visual cohesion:**
- [ ] All new sections use existing CSS tokens (`--bg`, `--ink`, `--accent`, `--font-display`, `--font-body`, `--font-mono`, `--rule`)
- [ ] No new font imports added
- [ ] Section numbering sequential and matches new order
- [ ] Mobile (<900px): all new sections stack correctly, no horizontal scroll
- [ ] `prefers-reduced-motion` respected (already site-wide)

**Anti-slop self-audit:**
- [ ] Zero emoji in new content
- [ ] Zero icon library references in new content
- [ ] No "Elevate/Seamless/Unleash/Empower/Game-changer/Next-gen" in new copy
- [ ] No purple/blue gradient
- [ ] No 3-column equal feature grid (Mandate grid is 4×2 = OK, asymmetric)

**Functional:**
- [ ] Tabs keyboard navigable (Tab to focus, Arrow keys to switch, Enter/Space to activate)
- [ ] Tabs work without JS (graceful degradation: all panels visible if JS fails)
- [ ] All inline links resolve
- [ ] Page validates as HTML5

**Quantitative:**
- [ ] Page line count: 779 → ~1200 (target range 1100-1300)
- [ ] Page weight: < +10KB unminified
- [ ] No new external dependencies (no Google Fonts changes, no scripts loaded)

---

## Next steps + dependencies

**Immediate next step:** invoke `/ck:plan` with this brainstorm doc as context to produce phased implementation plan.

**Dependencies:**
- SKILL.md frontmatter (read-only — confirms `version: "2.0.0"`)
- README.md (read-only — source of truth for examples, related skills, hard rules)
- `plans/260509-ai-vs-human-analysis/synthesis.md` (read-only — source of truth for stat numbers + comparison content)
- `references/anti-slop-rules.md` (read-only — verify Mandate-vs-Anti-slop distinction copy)

**No external blockers.** Self-contained edit on `index.html`.

---

## Unresolved questions

None. All clarification points resolved during brainstorm:
- Audience: general visitor (both eval + active users) — confirmed
- Page growth: moderate (3-4 sections) — confirmed
- Format: open to flat + interactive + visual — confirmed
- Direction: C (Balanced) — confirmed
- Examples format: interactive tabs — confirmed
- Why visuals: stat block + comparison panel — confirmed
- Version source of truth: SKILL.md `2.0.0` — verified
