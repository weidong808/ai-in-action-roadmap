# HabitCheck — Build Spec (AI in Action #3)

**Build habits that stick, with an AI coach that spots your patterns.**
*Better Living product #3 · Spec v1 · July 2026*

---

## 1. Why HabitCheck Next

The handoff doc suggested FitnessCheck; this spec flips the order for one reason: **HabitCheck's core is the shared engine for the rest of the family.** Streaks, recurring schedules, reminders, completion tracking, and trend charts are exactly what FitnessCheck, WalkCheck, HydrationCheck, GratitudeCheck, and PrayerCheck all need. Building it first means:

- FitnessCheck becomes a ~2-week build on top of `@better-living/tracking` instead of another 6-week from-scratch app.
- It kicks off the monorepo + shared-packages migration (handoff action items #2 and #3) with a concrete driver, not speculative architecture.
- It's the strongest AI in Action article of the three: *"I built one app and got an engine for the next six."*

It's also the safest MVP in the catalog: pure local-first, zero hardware or third-party API dependencies, and the highest built-in retention mechanic (streaks) in the family.

## 2. Target User & Jobs to Be Done

Ordinary people (not quantified-self enthusiasts) who want to:

1. Start a small number of habits and actually keep them (build habits)
2. Cut down on something (break habits — often forgotten by competitors)
3. See honest progress without spreadsheet energy
4. Get a nudge that feels like a coach, not a notification firehose

## 3. MVP Scope

### In (v1.0)

- **Habits:** create build-type and break-type habits; name, icon, color, motivation note
- **Schedules:** daily, N-days-per-week, specific weekdays
- **Check-off:** one-tap complete/skip from the home screen; backfill up to 7 days
- **Streaks:** current + best streak, with *grace rules* (one scheduled miss doesn't zero a long streak — kinder than competitors, on-brand for Better Living)
- **Progress views:** calendar heatmap per habit; weekly completion %; simple trend line
- **Reminders:** local notifications via service worker (opt-in, per habit)
- **AI Weekly Review (the differentiator):** on-demand summary — what's working, what's slipping, one concrete suggestion. Runs only when the user taps it; only aggregated stats leave the browser, never raw logs
- **AI habit starter:** describe a goal in plain language → suggested habit + schedule + realistic first-two-weeks plan
- **Data:** export/import JSON; PWA installable; fully offline except the two AI features

### Out (v1.x / later engineering themes)

- Accounts, cloud sync, sharing/social, widgets, native apps (optional later capability work — framed as engineering learning, not commercial packaging)
- Habit categories/tags beyond icon+color
- AI chat interface (deliberately — "AI where it creates value, not a chatbot everywhere")

## 4. AI Design

| Feature | Model use | Deterministic part | Privacy |
|---|---|---|---|
| Weekly Review | Summarize + one recommendation from aggregated stats | Stats computed locally (completion %, streaks, day-of-week patterns, time-of-day patterns) | Only the aggregate JSON is sent; opt-in per invocation; works never→always offline degrades to stats-only view |
| Habit Starter | Parse goal → structured habit proposal | Schedule validation, duplicate detection | Single prompt, no history sent |

Implementation via `@better-living/ai` (new shared package):

- **Provider abstraction:** one interface, adapters for Anthropic/OpenAI/local; model choice per feature via config
- **Prompt registry:** versioned prompts in-repo, testable with fixture inputs
- **Cost guards:** per-user daily invocation cap, response caching keyed on the stats hash (same week's data → cached review)
- **Privacy gate:** a single choke-point function that whitelists exactly which fields may leave the device

## 5. Architecture

**Stack (per Better Living standard):** Next.js + React + TypeScript + Tailwind, PWA, IndexedDB via Dexie, deployed on Vercel at `habitcheck.weidong-shi.com`, Cloudflare DNS, GitHub Actions CI/CD.

**Monorepo kickoff (Turborepo):**

```
better-living/
├── apps/
│   └── habitcheck/          # this build
├── packages/
│   ├── ui/                  # extracted from SleepCheck/RetireCheck patterns
│   ├── storage/             # Dexie wrapper, migrations, export/import
│   ├── ai/                  # provider abstraction, prompts, privacy gate
│   └── tracking/            # THE engine: habits, schedules, streaks, stats
└── .github/workflows/       # shared CI, per-app deploy
```

RetireCheck and SleepCheck migrate into `apps/` *after* HabitCheck ships — don't block the new build on migration.

**Data model (IndexedDB):**

```ts
Habit      { id, name, type: 'build'|'break', icon, color, motivation,
             schedule: { kind: 'daily'|'weekly'|'weekdays', target?, days? },
             createdAt, archivedAt? }
Completion { id, habitId, date, status: 'done'|'skipped'|'missed', note?, loggedAt }
Settings   { reminders, aiOptIn, theme, ... }
```

Streaks and stats are **derived, never stored** — computed in `@better-living/tracking` with unit tests as the package's spec.

## 6. Milestones (6 weeks)

| Week | Deliverable |
|---|---|
| 1 | Monorepo scaffold; `tracking` package with full unit-test suite (schedules, streaks, grace rules); data model + storage |
| 2 | Core UI: habit CRUD, home screen check-off, onboarding |
| 3 | Heatmap + trends; reminders; PWA/offline hardening |
| 4 | `ai` package: provider abstraction, privacy gate; Weekly Review + Habit Starter |
| 5 | Polish: theming, accessibility pass, empty states, export/import; beta with a handful of real users |
| 6 | Fix, deploy to production, then content week: article, video, diagram, portfolio update |

**Definition of done:** app live on subdomain, Lighthouse PWA + a11y ≥ 90, tracking package ≥ 90% test coverage, full 8-asset content stack published.

## 7. AI in Action #3 — Content Plan

- **Article thesis:** *"One extra week on this app bought me an engine for the next six."* Spine: the decision to extract `@better-living/tracking`, with the monorepo before/after diagram.
- **Video (15s):** goal typed in plain English → AI proposes habit → first check-off → streak animates.
- **Lessons section candidates:** grace-rule design (product judgment vs. copying competitors), privacy gate pattern, derived-vs-stored state, what AI wrote vs. what required engineering judgment.
- **Consumer teaser:** "Most habit apps punish you for missing one day. HabitCheck doesn't." 

## 8. Success Metrics (first 8 weeks post-launch)

1. 4-week retention of installed-PWA users (primary)
2. Median habits per active user (healthy range 2–5; >8 signals over-ambition churn)
3. Weekly Review usage rate among active users (validates the AI investment)
4. Article reads + repo stars vs. AI in Action #2 (content trajectory)
5. Time-to-build for FitnessCheck afterward (the reuse payoff — publish this number)

## 9. Risks

| Risk | Mitigation |
|---|---|
| Over-engineering the shared packages before real user feedback | Extract only what HabitCheck itself needs; no speculative APIs |
| Notification reliability on iOS PWA | Ship reminders as best-effort; set expectations in-app; native apps fix this in Phase 3 |
| AI features feel gimmicky | Both features must pass the "would a good human coach say this?" bar in beta, or ship stats-only and add AI in v1.1 |
| Monorepo migration stalls the build | New app first; migrate the old two apps after launch |
