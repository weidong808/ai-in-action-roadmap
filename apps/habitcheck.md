# HabitCheck — Build Spec (AI in Action #4)

**Build and break habits that stick — local-first PWA with kind streak rules and honest progress.**  
*AI in Action #4 · Better Living candidate · Spec v2 · July 2026*  
**Status:** Discovery (v1.0 scope locked: single app, AI deferred to v1.1)

Related:

- [Discovery brief](../docs/discovery/habitcheck-00-discovery-brief.md)
- [Product decisions](../docs/discovery/habitcheck-01-product-decisions.md)
- [Architecture notes](./habitcheck-architecture.md)
- [Future apps](./future-apps.md)

---

## 1. Why HabitCheck Next

Readiness (App #3) covered enterprise AI go/no-go judgment. HabitCheck returns to the Better Living track with a reusable **tracking engine**: streaks, schedules, check-offs, and progress views that FitnessCheck and siblings will need later.

Building HabitCheck first means:

- A clean internal `src/lib/tracking/` module that can later extract to `@better-living/tracking` when reuse is proven — **not** a Turborepo on day one.
- Strongest product thesis for the series: *"I built one app and got an engine for the next six."*
- Safest MVP: pure local-first, no hardware, no third-party API required for v1.0.

**Locked decisions (discovery):**

| Decision | Choice |
|----------|--------|
| Repo shape | Single Next.js app (SleepCheck / Readiness pattern) |
| AI in v1.0 | Deferred — Weekly Review + Habit Starter in **v1.1** |
| Series label | AI in Action **#4** (Readiness remains #3) |

---

## 2. Target User & Jobs to Be Done

Ordinary people (not quantified-self enthusiasts) who want to:

1. Start a small number of habits and actually keep them (build habits)
2. Cut down on something (break habits — often forgotten by competitors)
3. See honest progress without spreadsheet energy
4. Get reminders that feel helpful, not like a notification firehose

---

## 3. MVP Scope

### In (v1.0)

- **Habits:** create build-type and break-type habits; name, icon, color, motivation note
- **Schedules:** daily, N-days-per-week, specific weekdays
- **Check-off:** one-tap complete/skip from the home screen; backfill up to 7 days
- **Streaks:** current + best streak, with *grace rules* (one scheduled miss does not zero a long streak)
- **Progress views:** calendar heatmap per habit; weekly completion %; simple trend line
- **Reminders:** local notifications via service worker (opt-in, per habit; best-effort on iOS PWA)
- **Data:** export/import JSON; PWA installable; **fully offline**
- **Trust chrome:** Privacy page + wellness framing (not medical advice)

### Out (v1.0)

- Accounts, cloud sync, sharing/social, widgets, native apps
- **AI Weekly Review** and **AI Habit Starter** (planned **v1.1**)
- AI chat interface
- Turborepo / shared monorepo; migrating SleepCheck or RetireCheck

### Planned (v1.1)

- AI Weekly Review (on-demand; aggregated stats only leave the browser)
- AI Habit Starter (goal → structured habit proposal)
- Privacy gate + provider abstraction (previewed in architecture notes)

---

## 4. AI Design (v1.1 preview — not v1.0)

| Feature | Model use | Deterministic part | Privacy |
|---------|-----------|--------------------|---------|
| Weekly Review | Summarize + one recommendation from aggregates | Stats computed locally | Opt-in per invocation; aggregate JSON only |
| Habit Starter | Parse goal → structured habit proposal | Schedule validation, duplicate detection | Single prompt; no history |

When AI ships: versioned prompts, cost caps, and a single privacy-gate choke point. Offline always degrades to stats-only / non-AI flows.

---

## 5. Architecture (v1.0)

**Stack:** Next.js App Router + React + TypeScript + Tailwind v4, PWA, IndexedDB via Dexie, Vercel at `habitcheck.weidong-shi.com`, Cloudflare DNS, GitHub Actions CI (lint · typecheck · test · build).

**Module layout (single repo):**

```
habitcheck/
├── src/
│   ├── app/                 # routes, privacy, PWA
│   ├── components/
│   └── lib/
│       ├── tracking/        # schedules, streaks, grace rules, stats (unit-tested)
│       └── storage/         # Dexie schema, migrations, export/import
└── .github/workflows/ci.yml
```

Extract `@better-living/tracking` (and later `ai`) **after** HabitCheck validates the engine — do not block v1 on monorepo migration.

**Data model (IndexedDB):**

```ts
Habit      { id, name, type: 'build'|'break', icon, color, motivation,
             schedule: { kind: 'daily'|'weekly'|'weekdays', target?, days? },
             createdAt, archivedAt? }
Completion { id, habitId, date, status: 'done'|'skipped'|'missed', note?, loggedAt }
Settings   { reminders, theme, ... }
```

**Hard rule:** streaks and stats are **derived, never stored** — computed in `src/lib/tracking/` with unit tests as the module’s spec.

Full write-up: [habitcheck-architecture.md](./habitcheck-architecture.md).

---

## 6. Milestones (indicative)

| Phase | Deliverable |
|-------|-------------|
| Discovery | This pack — brief, decisions, architecture (current) |
| Week 1–2 | App scaffold; `tracking` tests; habit CRUD + check-off |
| Week 3 | Heatmap + trends; reminders; PWA/offline |
| Week 4 | Polish, a11y, export/import, Privacy page, deploy |
| Content | Hub `/work` + `/insights`, LinkedIn, diagrams |
| v1.1 | AI Weekly Review + Habit Starter behind privacy gate |

**Definition of done (v1.0):** live on subdomain; CI green; tracking module well covered by unit tests; Privacy page; hub case study draft ready.

---

## 7. AI in Action #4 — Content Plan

- **Article thesis:** *"One extra week on this app bought me an engine for the next six."* Spine: kind streak / grace-rule design + derived stats module (extract story continues in v1.1 / later packages).
- **Video (15s):** create habit → first check-off → streak animates → heatmap.
- **Lessons:** grace-rule product judgment; derived-vs-stored state; ship core before AI coach.
- **Consumer teaser:** "Most habit apps punish you for missing one day. HabitCheck doesn't."

---

## 8. Success Metrics (first 8 weeks post-launch)

1. 4-week retention of installed-PWA users (primary)
2. Median habits per active user (healthy range 2–5; >8 signals over-ambition churn)
3. (v1.1+) Weekly Review usage rate among active users
4. Article reads + repo stars vs prior AI in Action posts
5. Time-to-build for FitnessCheck afterward (reuse payoff — publish this number)

---

## 9. Risks

| Risk | Mitigation |
|------|------------|
| Over-engineering shared packages before feedback | Single app + internal `tracking` module only in v1 |
| Notification reliability on iOS PWA | Best-effort reminders; clear in-app expectations |
| Shipping AI too early feels gimmicky | AI deferred to v1.1 after core retention works |
| Scope creep into monorepo migration | Migrate SleepCheck/RetireCheck only after HabitCheck is live |
