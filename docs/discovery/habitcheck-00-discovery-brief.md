# HabitCheck — Discovery Brief

**Series:** AI in Action #4 · Better Living candidate  
**Status:** Discovery complete — MVP spec ready; await owner go before app scaffold  
**Spec:** [apps/habitcheck.md](../../apps/habitcheck.md)  
**Decisions:** [habitcheck-01-product-decisions.md](./habitcheck-01-product-decisions.md)  
**MVP specification (v4):** [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md)  
**Architecture:** [apps/habitcheck-architecture.md](../../apps/habitcheck-architecture.md)

---

## 1. Problem

People start habits with good intent and quit after misses — apps punish streaks, hide recovery, demand accounts, or skip coaching. HabitCheck answers: **Can I keep a small set of weekly habits, recover kindly after slips, and optionally get AI coaching — fully on my device?**

## 2. Audience

| Audience | Why they care |
|----------|----------------|
| Busy adults | Flexible weekly targets, recovery paths, low shame |
| Engineers / hiring | Local-first PWA, derived domain logic, AI privacy gate, CI |
| Series readers | AI in Action #4 after Readiness — personal coach vs enterprise gates |

Not for: quantified-self power users, clinical therapy, or medical claims.

## 3. Why this app (portfolio)

- Complements RetireCheck (math), SleepCheck (sensory), Readiness (enterprise AI gates)
- Ships **optional AI in v1** as the differentiator (starter · comeback · weekly review · target suggest)
- Builds a reusable weekly **tracking** module for later Better Living apps — without Turborepo day one

## 4. MVP (v1.0) — locked

**One-liner:** Recover after missed days — local-first weekly habits with kind recovery and optional AI coaching.

**In:** ≤3 build habits · flexible weekly targets · Mon–Sun weeks · difficulty-aware check-ins · recovery paths · pause · weekly review · AI comeback + weekly review required (starter optional) · in-app reminders · export/import · PWA · Privacy page.

**Out:** break-habits · weekday-specific schedules · chat UI · accounts/sync · Turborepo · adaptive reminder ML.

Full contract: [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md).

## 5. Non-goals

- Not a medical device or clinical intervention
- Not a commercial catalog or monetization surface
- Not a shared Better Living monorepo in v1
- Not notification perfection on iOS PWA

## 6. Success metrics (post-launch)

1. 4-week retention of installed-PWA users (primary)
2. Share of active users who complete ≥1 recovery path
3. Opt-in AI feature usage (starter / review / comeback) among active users
4. Hub insight + LinkedIn reach vs prior series posts

## 7. Risks

| Risk | Mitigation |
|------|------------|
| AI feels gimmicky | Deterministic scoring owns truth; AI only proposes; accept/edit/dismiss |
| Privacy concern | Summaries-only gate; per-action consent; clear Privacy page |
| Scope creep (chat, unlimited habits) | Cap 3; no chat; MVP spec is gate |
| Reminder unreliability | Best-effort; banners on pause end |

## 8. Discovery exit criteria

Owner confirms:

- [x] Product questionnaire decisions locked
- [x] MVP specification (flows, screens, data, scoring, AI, acceptance, phases)
- [ ] Domain / branding: `habitcheck.weidong-shi.com`
- [ ] Go / no-go to scaffold public repo

## 9. Next step after approval

1. Create public GitHub repo under `weidong808`
2. Execute MVP phases P0→P6 in [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md)
3. Hub `/work` + `/insights` + LinkedIn when live
