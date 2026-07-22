# HabitCheck — Discovery Brief

**Series:** AI in Action #4 · Better Living candidate  
**Status:** Discovery complete for planning — await owner approval before app scaffold  
**Spec:** [apps/habitcheck.md](../../apps/habitcheck.md)  
**Decisions:** [habitcheck-01-product-decisions.md](./habitcheck-01-product-decisions.md)  
**Architecture:** [apps/habitcheck-architecture.md](../../apps/habitcheck-architecture.md)

---

## 1. Problem

People start habits with good intent and fail for predictable reasons: apps punish a single miss, hide break-habits, demand accounts before value, or bury progress in spreadsheets. Competitors optimize for streaks-as-shame rather than streaks-as-momentum.

HabitCheck answers: **Can I build or break a small set of habits with kind rules and honest progress — fully on my device?**

## 2. Audience

| Audience | Why they care |
|----------|----------------|
| Everyday users | Simple check-off, grace, local privacy |
| Engineers / hiring | Local-first PWA, derived domain logic, CI, case study |
| Series readers | Continues AI in Action after Readiness (#3) on a wellness track |

Not for: quantified-self power users, clinical habit therapy, or medical claims.

## 3. Why this app (portfolio)

- Complements RetireCheck (decision math), SleepCheck (sensory PWA), Readiness (AI gates)
- Teaches **product judgment** (grace rules) + **domain isolation** (tracking module)
- Sets up later Better Living reuse without requiring a platform on day one

## 4. MVP (v1.0) — locked

**One-liner:** Build and break habits that stick — local-first PWA with kind streak rules and honest progress views.

**In:** habits (build/break), schedules, check-off/skip, 7-day backfill, grace streaks, heatmap + weekly %, opt-in local reminders, export/import, PWA, Privacy page, wellness disclaimer.

**Out:** accounts/sync/social, AI Weekly Review / Habit Starter (v1.1), chat UI, Turborepo, migrating sibling apps.

## 5. Non-goals

- Not a medical device or clinical intervention
- Not a commercial product catalog or monetization surface
- Not a shared Better Living monorepo in v1
- Not notification perfection on iOS PWA

## 6. Success metrics (post-launch)

1. 4-week retention of installed-PWA users (primary)
2. Median habits per active user in 2–5 range
3. Content: hub insight + LinkedIn reach vs prior series posts
4. Later: FitnessCheck time-to-build after extracting tracking (publish the number)

## 7. Risks

| Risk | Mitigation |
|------|------------|
| Grace rules feel “cheating” | Document rule clearly in UI and case study |
| Reminder unreliability | Best-effort copy; never block core loop |
| Scope creep into AI or monorepo | v1.0 gate: no AI, no Turborepo |
| Empty-state churn | Strong onboarding: suggest 1–3 starter habits without AI |

## 8. Discovery exit criteria

Owner confirms:

- [ ] v1.0 scope (this brief + product decisions)
- [ ] Architecture notes (single app + `src/lib/tracking`)
- [ ] Domain / branding: `habitcheck.weidong-shi.com`
- [ ] Go / no-go to scaffold public repo

## 9. Next step after approval

1. Create public GitHub repo under `weidong808`
2. Scaffold Next.js + Dexie + tracking unit tests
3. Vertical slice: create habit → check-off → streak → heatmap
4. PWA, Privacy, CI, custom domain → hub `/work` + `/insights`
