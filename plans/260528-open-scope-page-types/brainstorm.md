# Open scope — page types beyond landing/portfolio

**Date:** 2026-05-28
**Status:** Brainstorm complete, awaiting plan approval
**Skill version impact:** v2.0.0 → v2.1.0 (minor, additive + scope softening)

---

## Problem statement

Skill hiện tại block hoàn toàn type khác landing/portfolio: Phase 0.5 refuses dashboard/admin/full-app/e-commerce; SKILL.md liệt kê "Off-scope (refused, redirected)"; Hard Rule #1 ngầm define scope = "marketing-style sites only". User muốn skill áp dụng cho **mọi page type**, landing/portfolio chỉ là 2 case được improve đặc biệt hơn (giữ anatomy + skeleton riêng), còn lại dùng generic toolkit.

## Requirements

| ID | Requirement | Source |
|----|-------------|--------|
| R1 | Skill không refuse type nào | User explicit |
| R2 | `--type` accept bất kỳ giá trị | User explicit |
| R3 | Landing/portfolio giữ quality bar hiện tại (zero regression) | KISS + safety |
| R4 | Type khác vẫn nhận universal toolkit (vibe, anti-slop, motion, icons, illustrations) | User explicit |
| R5 | Anti-slop audit không raise false positive cho non-marketing type | Anti-slop applicability decision |
| R6 | Default behavior khi không pass `--type` = ask user with expanded options | User pick |
| R7 | Footprint minimal — 2 file mới, không refactor lớn | KISS |

## Evaluated approaches

### Approach A — Universal skill + type modifiers (CHOSEN)
- Core skill universal; landing/portfolio = special anatomy + skeleton; others = 1 generic file chung
- **Pros:** Min footprint (2 file mới + 5 sửa); zero regression cho landing/portfolio; áp dụng KISS
- **Cons:** Generic anatomy fuzzy by design; quality non-marketing phụ thuộc commitment audit
- **Verdict:** Selected

### Approach B — Tiered system (A/B/C)
- Tier A landing/portfolio (rich), Tier B blog/about/pricing/contact (templated, ~5 file mới), Tier C generic
- **Pros:** Coverage tốt hơn cho common type
- **Cons:** ~7 file mới; maintenance overhead
- **Verdict:** Rejected (user pick KISS)

### Approach C — Per-type anatomy
- Mỗi type phổ biến có anatomy nhẹ riêng
- **Pros:** Guidance đầy đủ
- **Cons:** Nhiều file, dễ inconsistent
- **Verdict:** Rejected (user pick KISS)

## Final design

### 1. Architecture

```
Phase 0.5 (NEW LOGIC):
  if --type passed: route to that type (any string accepted)
  else if description detectable: auto-detect (landing | portfolio | blog | about | pricing | contact | dashboard | admin | e-commerce | ...)
  else: AskUserQuestion với expanded options
  → SPECIAL tier (landing | portfolio): existing rich flow
  → GENERIC tier (anything else): use generic-page-anatomy + generic-page-skeleton
  NO REFUSALS
```

### 2. Files

**New (2):**
- `references/generic-page-anatomy.md` (~120 lines)
  - § Page-purpose exercise (what's the page's job? success criteria? primary action?)
  - § Section pattern library (header, hero?, content, CTA?, footer, nav?)
  - § Universal anti-patterns (link to applicability matrix)
  - § Mobile + a11y reminders
  - § Note: evidence base (12 landings) không cover dashboard/admin/e-commerce — output là best-effort universal craft, không phải evidence-backed
- `assets/nextjs-skeleton/generic-page-skeleton.md` (~80 lines)
  - Minimal Next.js scaffold: `app/layout.tsx`, `app/page.tsx`, `app/globals.css`
  - Custom icons folder mandate (`app/components/icons/`)
  - Centralized copy mandate (`app/lib/content.ts`)
  - Tailwind HSL tokens + theme config
  - Optional sections: nav, footer (skeleton commented out, uncomment as needed)

**Modified (5):**
- `SKILL.md`
  - Rewrite § Scope: bỏ refusal list; thêm 2-tier matrix
  - Hard Rule #1 reworded — vẫn NO emoji nhưng bỏ "marketing-style only" framing
  - Hard Rule #8 → "Type-aware where it matters": landing/portfolio có anatomy + audit riêng; others dùng generic anatomy + universal audit subset
- `references/workflow-phases.md`
  - Phase 0.5 update theo logic mới ở trên
  - Phase 6 (plan generation) — landing/portfolio invoke existing prompt; others invoke generic prompt (sections do user/page-purpose drive, không prescribed)
- `references/anti-slop-rules.md`
  - Thêm § Applicability Matrix ở đầu file
  - Tag mỗi rule với `[universal]`, `[marketing-only]`, hoặc `[landing/portfolio-only]`
  - Nội dung rules không đổi
  - Phase 8 audit chạy filtered subset theo type
- `README.md`
  - § What it does — thêm câu "applies to any page; landing/portfolio get special treatment"
  - § Examples — bỏ Example 3 (dashboard refused); thêm Example 4 (blog/about) + Example 5 (dashboard với warning)
  - § FAQ — cập nhật câu hỏi "What about blog sites?"
- `index.html`
  - § 02 Scope rewrite: bỏ refusal list, thêm 2-tier card
  - § 07 In practice — thêm 1 tab non-marketing example
  - § 09 Beyond — thu nhỏ; chỉ giữ skill routing khi có skill thực sự tốt hơn (vd. e-commerce → shopify nếu user muốn full Shopify backend, không phải vì refuse e-commerce)

**Untouched:**
- `references/visual-direction-guide.md` (11 vibes vẫn áp dụng universal)
- `references/2d-illustration-catalog.md`
- `references/visual-asset-prompt-library.md`
- `references/visual-effect-patterns.md`
- `references/motion-patterns.md`
- `references/custom-icon-pipeline.md`
- `references/loading-ui-patterns.md`
- `references/redesign-audit-checklist.md`
- `references/landing-anatomy.md`
- `references/portfolio-anatomy.md`
- `assets/nextjs-skeleton/section-archetypes.md` (still landing/portfolio only)
- `assets/nextjs-skeleton/landing-skeleton.md`
- `assets/nextjs-skeleton/portfolio-skeleton.md`

### 3. Anti-slop Applicability Matrix (preview)

Audit rules từ `anti-slop-rules.md` được tag:

| Rule | Tag | Lý do |
|------|-----|-------|
| No emoji anywhere | universal | Brand hygiene |
| No icon libraries | universal | Custom craft principle |
| No Inter/Roboto/Arial alone | universal | Font fingerprint |
| No DM Sans + Space Grotesk pair | universal | AI-default pair |
| Custom SVG cohesion | universal | Icon discipline |
| `h-screen` banned (use min-h-[100dvh]) | universal | Mobile correctness |
| No AI 3D models as hero | marketing-only | Hero concept only applies |
| No purple-blue gradient hero | marketing-only | Hero concept only applies |
| No 3-col equal feature grid | marketing-only | Features section concept |
| Two equal CTAs in hero | marketing-only | Hero CTA pattern |
| Generic CTA labels (Get Started/Sign In) | marketing-only | Conversion context |
| Browser-mockup hero | marketing-only | Hero pattern |
| Friendly bullet checklist | marketing-only | Features section |
| Fake stats (99.99%, 10x faster) | marketing-only | Social proof context |
| Centered H1 at high variance | marketing-only | Hero layout |
| "Elevate/Seamless/Unleash" copy | marketing-only | Marketing copy |
| "Hi I'm X passionate designer" | landing/portfolio-only (portfolio) | Portfolio-specific |
| Skill bars / tool clouds | landing/portfolio-only (portfolio) | Portfolio-specific |

→ Phase 8 audit cho dashboard sẽ skip ~12/18 rules; cho landing/portfolio chạy full.

### 4. Phase 0.5 expanded options (AskUserQuestion)

```
Q: "Bạn đang design loại page gì?"
Options:
  - Landing page (marketing/conversion)
  - Portfolio / personal site
  - Blog / article
  - About / team page
  - Pricing page
  - Contact / coming-soon / waitlist
  - Dashboard / admin
  - E-commerce / store
  - Other (free text → generic tier)
```

## Implementation considerations

### Migration safety
- Existing landing/portfolio flows: 0 thay đổi behavior
- Existing `--type landing|portfolio` flag: backward compat 100%
- Anti-slop audit: cho landing/portfolio chạy full = identical to current; cho new types chạy filtered subset
- README + index.html: visible changes nhưng không break URL/anchor existing

### Honest limitations to document
- Generic anatomy KHÔNG prescribe sections — user/page-purpose drive
- Evidence base (12 landings) không cover non-marketing types — note rõ trong generic-page-anatomy
- Một số vibe (Editorial, Organic, Hand-crafted) có thể không hợp dashboard; commitment audit (≥48/60) handle case-by-case
- Section archetypes không expand cho type mới (KISS) — user tự design sections từ pattern library

## Success criteria

1. `--type pricing` (hoặc bất kỳ string khác landing/portfolio) chạy được, không bị refuse
2. `--type landing` và `--type portfolio` output identical với behavior hiện tại
3. Phase 8 audit cho `--type dashboard` không raise false positive (skip "no hero CTA", "no 3-col grid", etc.)
4. README + index.html có 2 example non-marketing
5. SKILL.md, anti-slop-rules.md có applicability tag
6. Backward compat: existing tests/examples không break

## Risks & mitigations

| Risk | Likelihood | Mitigation |
|------|-----------|------------|
| Output cho dashboard/admin tệ hơn expectation | High | Note rõ "best-effort, not evidence-backed" trong generic-anatomy + scope card |
| Applicability matrix bị maintain sai (rule mới quên tag) | Medium | Audit checklist Phase 8 phải check rule có tag chưa |
| User confused về tier (special vs generic) | Low | Scope card trong index.html + README explain rõ |
| Generic anatomy quá fuzzy → AI produces slop | Medium | Universal anti-slop rules + commitment audit ≥48/60 vẫn enforce |
| Phase 0.5 detection sai (vd. "about my product" → about page thay vì landing) | Low | Fallback: detection ambiguous → AskUserQuestion |

## Out of scope (defer)

- Per-type anatomy cho blog/about/pricing (Approach C) — defer cho v2.2 nếu user feedback cần
- Section archetypes cho non-marketing type — defer
- Evidence research cho dashboard/admin pattern — defer (different problem class, possibly different skill)
- Multi-page marketing site orchestration — defer (current scope = single page output; multi-page = compose multiple type invocations)
- Vibe filtering by type (vd. dashboard không cho Editorial) — defer; commitment audit handles

## Next steps

1. User approve design này → proceed `/ck:plan` để phân rã phase
2. Plan dự kiến ~3-4 phase: (a) anti-slop matrix + workflow update, (b) generic anatomy + skeleton, (c) SKILL.md + README, (d) index.html
3. Implementation parallel-safe theo file boundaries

## Unresolved questions

- Phase 6 plan generation cho generic tier: prompt template như thế nào cho `ck:plan`? Có thể cần section "Generic plan prompt" trong workflow-phases.md — sẽ define trong /ck:plan phase
- Có cần version bump SKILL.md `v2.0.0` → `v2.1.0`? README hiện ghi v2.0.0; index.html hero hiện ghi v2.0.0 — convention dự án chưa rõ, để user quyết khi plan
- `index.html` "Beyond" section: giữ Shopify routing không? Hay xóa hoàn toàn vì giờ skill không refuse e-commerce nữa? Tôi propose giữ với câu "use this skill cho storefront landing; dùng shopify cho full backend" — confirm khi plan
