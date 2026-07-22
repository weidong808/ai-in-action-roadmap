# HabitCheck — Product Decisions (v1.0)

**Status:** Locked · July 2026 · aligned to MVP **v5 AI-forward**  
**Parent brief:** [habitcheck-00-discovery-brief.md](./habitcheck-00-discovery-brief.md)  
**MVP spec (implementation contract):** [habitcheck-02-mvp-specification.md](./habitcheck-02-mvp-specification.md)

These decisions are binding for the first implementation pass unless the owner explicitly revises them.

---

## 1. Series and positioning

| Decision | Value |
|----------|-------|
| Series number | AI in Action **#4** |
| Track | Better Living candidate (wellness / local-first) |
| App #3 | Remains **AI Production Readiness Advisor** |
| Audience | Busy adults building healthier routines |
| Promise | **Recover after missed days** |
| Qualities | Private · Simple · Encouraging · **AI-powered coaching (first-class)** |
| AI weight | ~45–55% of product story and build |
| Public framing | Personal lab / educational showcase — not a commercial product |

**Differentiation:** personal habit **OS** — AI in setup, recovery, review, and plan changes — on a deterministic weekly core. Distinct from RetireCheck, SleepCheck, and Readiness.

---

## 2. Habits

- **v1 type:** **Build only** (do the habit N times per week). Break-habits deferred.
- **Active cap:** **≤ 3** (active + paused). Archive to free a slot.
- **Setup requires:** name, weekly target (1–7), motivation, smaller version (AI-generated or manual); optional first-two-weeks ramp from Starter.

---

## 3. Scheduling and weeks

| Decision | Value |
|----------|-------|
| Schedule kind | **Flexible weekly target only** (no specific-weekdays mode in v1) |
| Week definition | **Monday–Sunday** local |
| Formal miss | **Only when the week ends** without meeting target |
| Mid-week | Soft **at risk** when target becomes unreachable — not a formal miss |

---

## 4. Check-ins

- Statuses: `done` | `skipped` (unset = not logged yet).
- Optional difficulty on done: **easy · manageable · hard** (skippable).
- Backfill: last **7** local days only.
- Home: one-tap done/skip for today.

---

## 5. Progress and recovery

| Decision | Value |
|----------|-------|
| Primary metric | Weekly consistency % (`doneCount / target`) |
| Secondary metric | Successful recoveries |
| Recovery UX | User **chooses** a path |
| Recovery paths | Smaller version · Reschedule in week · **Choose next restart day** · Ask AI comeback |
| Successful recovery | **Following the selected path** (action completed) |
| Smaller version | AI-generated or preset at setup + customize at recovery |
| Smaller version scoring | **Recovery, not full completion** |

Grace-as-daily-streak from earlier drafts is **replaced** by this weekly + recovery model for v1. Full scoring contract: [MVP spec v4](./habitcheck-02-mvp-specification.md).

---

## 6. Target changes and progression

| Trigger | Behavior |
|---------|----------|
| Two consecutive **difficult** weeks | Deterministic `max(1, target - 1)` + **AI Plan Adjuster** explanation |
| Two consecutive **easy** weeks (“consistently easy”) | Ask maintain **or** progress (`min(7, target + 1)`) + AI explanation |
| Suggestion UX | **Accept · edit · dismiss** — never auto-apply; model cannot invent unrestricted N |
| Effective date | **Next Monday** (current week keeps snapshot target) |
| Manual | User may always queue a target change in habit edit |

Definitions of easy/difficult weeks: MVP spec §5.7 (single authoritative algorithm).

---

## 7. Pause

- Allow **either:** indefinite pause (no progress penalty) **or** pause until a return date.
- Mid-week pause/resume → week status **`partially_paused`** (check-ins visible; excluded from averages/triggers); full scoring resumes next Monday.
- Dated pause end: **resume automatically with a reminder** (fallback in-app banner if notifications blocked).

---

## 8. Reminders

- Optional daily **in-app** reminder at chosen local time; stop after weekly target met; pause suppresses; recovery dates are one-time.
- System/OS notifications only when reliably supported — **not** a v1 release blocker.
- No adaptive/ML reminders in v1.

---

## 9. Weekly review

- **Facts** panel: consistency, recoveries, difficulty (separate metrics).
- **Coach** panel: required AI structured insight cards + one next-week move.
- Available **after Sunday ends**, viewed **anytime** (on-demand).
- Offline/decline → Facts-only (still complete).

---

## 10. AI (v1.0 — first-class ship gate)

| Feature | Role |
|---------|------|
| Habit Starter | **Required** — goal → plan + first-two-weeks ramp |
| Smart smaller-version | **Required** — create/recovery micro-action |
| Comeback Coach | **Required** — 2–3 micro-options at at-risk/miss |
| Weekly Review Coach | **Required** — structured insight cards |
| Plan Adjuster | **Required** — explains deterministic ±1 |

**Rules:** summaries only; per-action consent; **no free chat**; Facts vs Coach UI; streaming for Starter/Review; versioned prompts; cost caps; eval fixtures; fail closed; model must not invent unrestricted targets.

**v1.0 does not ship** without the five AI surfaces above.

---

## 11. Export / privacy / wellness

- Export `habitcheck-export@2` (habits, check-ins, recovery events, settings); import replace-with-confirm.
- No accounts; data on-device; Privacy page required.
- Analytics (if any): page views only — never habit payloads.
- Wellness: not medical advice; not clinical treatment.
- Privacy page **must** disclose AI coach summary sends (per-action consent) in v1.

---

## 12. Explicit non-goals (deferred)

| Topic | When |
|-------|------|
| Break-habits | Post-v1 |
| Specific weekdays schedules / user-chosen week start | Post-v1 |
| Chat coach / full-history AI | Out unless explicitly reopened |
| Turborepo / `@better-living/*` | After HabitCheck validates reuse |
| Accounts / sync | Later engineering milestone |
| Native apps | Out of scope for educational PWA track |
