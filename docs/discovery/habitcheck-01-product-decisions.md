# HabitCheck — Product Decisions (v1.0)

**Status:** Locked for discovery · July 2026  
**Parent brief:** [habitcheck-00-discovery-brief.md](./habitcheck-00-discovery-brief.md)

These decisions are binding for the first implementation pass unless the owner explicitly revises them.

---

## 1. Series and positioning

| Decision | Value |
|----------|-------|
| Series number | AI in Action **#4** |
| Track | Better Living candidate (wellness / local-first) |
| App #3 | Remains **AI Production Readiness Advisor** |
| Public framing | Personal lab / educational showcase — not a commercial product |

---

## 2. Habit types

- **Build:** user wants to do the habit on scheduled days (e.g. stretch, read).
- **Break:** user wants to avoid the habit on scheduled days (e.g. no late coffee). Check-off means “I kept the break” (success), not “I did the bad habit.”

UI copy must make break-habit semantics obvious on create and on the home list.

---

## 3. Schedules

| Kind | Meaning |
|------|---------|
| `daily` | Expected every local calendar day |
| `weekly` | N successful days per week (`target` 1–7); which days are flexible |
| `weekdays` | Specific days of week (`days`: 0–6, local week start Monday for stats unless Settings later changes) |

Missed days are only evaluated for **scheduled** expectations. Unscheduled days do not break streaks.

---

## 4. Completions and backfill

- Statuses: `done` | `skipped` | `missed`
- Home: one-tap `done` / `skip` for today
- Backfill: allow editing completions for the last **7** local days only
- `missed` may be system-derived at end of day for scheduled days with no `done`/`skipped` (implementation detail — must be deterministic and tested)

---

## 5. Grace rules (streak)

**Intent:** One scheduled miss does not zero a long streak.

**v1.0 rule (normative):**

1. Streak counts consecutive **satisfied** scheduled periods (for `daily` / `weekdays`: consecutive expected days with `done`; for `weekly`: weeks meeting `target`).
2. A single scheduled day (or week) that is `missed` or empty-after-deadline **uses one grace token** if the streak length before that miss is ≥ 3 satisfied periods; the streak continues.
3. Grace does **not** apply to `skipped` (skip is intentional — streak pauses or holds per “skip does not extend, does not consume grace” — **skip neither extends nor breaks**; next success continues).
4. A second miss without an intervening satisfied period **resets** current streak to 0; best streak is retained separately.
5. Grace tokens: **at most one** outstanding; restored after the next satisfied period.

Exact edge cases must be encoded as unit tests in `src/lib/tracking/` — tests are the spec.

**UI:** Show “Grace used” affordance when applicable so the rule is honest, not hidden.

---

## 6. Progress views

- Per-habit **heatmap** (calendar cells for recent weeks)
- **Weekly completion %** for the current local week
- Simple **trend** (e.g. last 4–8 weeks completion %)

No social comparison, no global leaderboard.

---

## 7. Reminders

- Opt-in per habit; local notification via service worker when supported
- **Best-effort** on iOS PWA — in-app copy: reminders may not fire when the app is closed on some devices
- Core loop must work with reminders disabled

---

## 8. Export / import

- JSON document versioned (`habitcheck-export@1`)
- Includes habits, completions, settings (no secrets)
- Import replaces or merges — **v1.0: replace-with-confirm** (simpler, safer)
- Documented on Privacy page

---

## 9. Privacy and wellness copy

- No account; all habit data on-device (IndexedDB)
- Privacy page required (parity with sibling apps)
- If Vercel Analytics is used: disclose page views; habit data never sent as analytics events
- Wellness disclaimer: not medical advice; not treatment for addiction or clinical disorders
- v1.0: no model calls; Privacy page must not claim AI features until v1.1

---

## 10. Explicit non-decisions (deferred)

| Topic | When |
|-------|------|
| AI Weekly Review / Habit Starter | v1.1 |
| Turborepo / `@better-living/*` packages | After HabitCheck validates reuse |
| Accounts / sync | Engineering learning milestone later |
| Week-start locale / i18n | Post-v1 unless blocked |
| Native apps | Out of scope for educational PWA track |
