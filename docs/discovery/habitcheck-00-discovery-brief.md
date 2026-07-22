# HabitCheck — Discovery Brief

**Series:** AI in Action #4 · Better Living candidate  
**Status:** Discovery complete — MVP spec v5 (AI-forward); await owner go before app scaffold  
**Spec:** [apps/habitcheck.md](../../apps/habitcheck.md)  
**Decisions:** [habitcheck-01-product-decisions.md](./habitcheck-01-product-decisions.md)  
**MVP specification (v5):** [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md)  
**Architecture:** [apps/habitcheck-architecture.md](../../apps/habitcheck-architecture.md)

---

## 1. Problem

People start habits with good intent and quit after misses — apps punish streaks, hide recovery, demand accounts, or offer thin “AI” gimmicks. HabitCheck answers: **Can I keep a small set of weekly habits, recover kindly after slips, and get serious AI coaching at every key moment — fully on my device for Facts?**

## 2. Audience

| Audience | Why they care |
|----------|----------------|
| Busy adults | Flexible weekly targets, recovery paths, encouraging coach |
| Engineers / hiring | Local-first PWA, derived domain logic, privacy-gated AI platform, evals, CI |
| Series readers | AI in Action #4 — consumer coach OS vs Readiness enterprise gates |

Not for: quantified-self power users, clinical therapy, or medical claims.

## 3. Why this app (portfolio)

- Complements RetireCheck (math), SleepCheck (sensory), Readiness (enterprise AI gates)
- **AI-forward v1:** Starter · Comeback Coach · Weekly Review cards · Plan Adjuster · Smart smaller-version (~45–55% of story/build)
- Reusable weekly **tracking** + **AI gate** patterns for later Better Living apps — without Turborepo day one

## 4. MVP (v1.0) — locked

**One-liner:** A local-first weekly habit OS — kind recovery + AI coaching at every key moment.

**In:** ≤3 build habits · flexible weekly targets · Mon–Sun · difficulty check-ins · recovery paths · pause · Facts vs Coach review · **all required AI surfaces** · in-app reminders · export/import · PWA · Privacy page · prompt versions / caps / streaming / evals.

**Out:** break-habits · weekday schedules · free chat · accounts/sync · Turborepo · adaptive reminder ML · model-chosen unrestricted targets.

Full contract: [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md).

## 5. Non-goals

- Not a medical device or clinical intervention
- Not a commercial catalog or monetization surface
- Not a shared Better Living monorepo in v1
- Not notification perfection on iOS PWA

## 6. Success metrics (post-launch)

1. 4-week retention of installed-PWA users (primary)
2. Share of active users who complete ≥1 recovery path
3. AI feature adoption (Starter / Comeback / Review / Plan Adjuster) among active users
4. Hub insight + LinkedIn reach vs prior series posts

## 7. Risks

| Risk | Mitigation |
|------|------------|
| AI feels gimmicky | Facts vs Coach; code owns scores; accept/edit/dismiss |
| AI scope slips schedule | AI is ship gate — sequence P5 platform then P6 features; no silent cuts |
| Privacy concern | Summaries-only gate; per-action consent; clear Privacy page |
| Reminder unreliability | Best-effort OS; in-app required |

## 8. Discovery exit criteria

Owner confirms:

- [x] Product questionnaire decisions locked
- [x] MVP specification v4 review fixes
- [x] MVP specification **v5 AI-forward** locked
- [ ] Domain / branding: `habitcheck.weidong-shi.com`
- [ ] Go / no-go to scaffold public repo

## 9. Next step after approval

1. Create public GitHub repo under `weidong808`
2. Execute MVP phases P0→P7 in [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md)
3. Hub `/work` + `/insights` + LinkedIn when live
