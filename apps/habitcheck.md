# HabitCheck — Build Spec (AI in Action #4)

**Recover after missed days — local-first weekly habits with kind recovery and optional AI coaching.**  
*AI in Action #4 · Better Living candidate · Spec v4 · July 2026*  
**Status:** Discovery complete — implementation-ready MVP spec locked (v4)

Related:

- [Discovery brief](../docs/discovery/habitcheck-00-discovery-brief.md)
- [Product decisions](../docs/discovery/habitcheck-01-product-decisions.md)
- [MVP specification](../docs/discovery/habitcheck-02-mvp-specification.md) ← **implementation contract**
- [Architecture notes](./habitcheck-architecture.md)
- [Future apps](./future-apps.md)

---

## 1. Why HabitCheck Next

Readiness (App #3) covered enterprise AI go/no-go judgment. HabitCheck returns to Better Living with:

1. A reusable **weekly tracking** engine (targets, miss/at-risk, recoveries, easy/difficult weeks).
2. A **personal coach** AI layer that is clearly different from Readiness — comebacks, weekly insights, plan adjustments — without chat.

**Locked decisions:**

| Decision | Choice |
|----------|--------|
| Repo shape | Single Next.js app (SleepCheck / Readiness pattern) |
| AI in v1.0 | **In scope** — Starter · Comeback · Weekly Review · Target suggest |
| Series label | AI in Action **#4** |
| Habit cap | ≤ 3 active/paused |
| Schedule | Flexible weekly target · Mon–Sun |

---

## 2. Target user & JTBD

Busy adults who want to:

1. Keep a small number of healthier routines with flexible weekly targets
2. Recover after misses without streak shame
3. Optionally use AI for plans, comebacks, and weekly pattern language
4. Stay private / local-first

---

## 3. MVP scope

### In (v1.0)

- ≤3 **build** habits: name, weekly target, motivation, smaller-version preset
- Check-in: done/skip + optional difficulty (easy / manageable / hard)
- Week model: Mon–Sun; miss only at week end; mid-week at-risk
- Recovery paths (user chooses): smaller version · reschedule · **choose next restart day** · Ask AI
- Smaller version = **successful recovery, not full completion**
- Pause: indefinite or until date; mid-week → `partially_paused`; dated end resumes + reminder
- Progression: two easy/difficult weeks → deterministic ±1 target (accept/edit/dismiss; **effective next Monday**)
- Weekly review: balanced stats (separate metrics) + optional AI narrative (after Sunday, anytime)
- Opt-in in-app reminders; export/import; PWA; Privacy + wellness + AI disclosure

### Out (v1.0)

- Break-habits, weekday-specific schedules, chat UI
- Accounts, cloud sync, social, native apps, Turborepo
- Adaptive reminder ML; auto-applied target changes; model-chosen unrestricted targets

---

## 4. AI design (v1.0)

| Feature | Priority | Model use | Deterministic part | Privacy |
|---------|----------|-----------|--------------------|---------|
| Comeback | **Required** | Personalized micro-action | Recovery completion rules | Opt-in; week/habit summary |
| Weekly Review | **Required** | Balanced narrative + one suggestion | Stats computed locally | Opt-in; aggregates only |
| Habit Starter | Optional if time | Goal → structured habit fields | Validation, cap ≤3 | Opt-in; single prompt |
| Target explanation | v1.1 | Explain ±1 suggestion | Easy/difficult + `max/min` clamp | Opt-in; two-week summary |

Same discipline as Readiness: versioned prompts, cost caps, privacy-gate choke point, fail closed. Details: [MVP spec v4 §6](../docs/discovery/habitcheck-02-mvp-specification.md).

---

## 5. Architecture (summary)

**Stack:** Next.js App Router + TypeScript + Tailwind v4 + Dexie + PWA · Vercel `habitcheck.weidong-shi.com` · GitHub Actions CI.

```
habitcheck/
├── src/
│   ├── app/
│   ├── components/
│   └── lib/
│       ├── tracking/     # week status, at-risk, consistency, easy/difficult, recovery rules
│       ├── storage/      # Dexie, export/import
│       └── ai/           # privacyGate, prompts, client helpers
└── .github/workflows/ci.yml
```

Full notes: [habitcheck-architecture.md](./habitcheck-architecture.md).

---

## 6. Milestones

| Phase | Deliverable |
|-------|-------------|
| Discovery | Brief · decisions · **MVP spec** · architecture (current) |
| P0–P2 | Scaffold · tracking tests · Today loop |
| P3–P4 | Recovery, pause, review, progression prompts |
| P5–P6 | AI gate + features · polish · ship |
| Content | Hub `/work` + `/insights`, LinkedIn |

Definition of done: [MVP acceptance criteria](../docs/discovery/habitcheck-02-mvp-specification.md).

---

## 7. AI in Action #4 — content plan

- **Article thesis:** Recover without shame — weekly honesty + AI comebacks on a deterministic core.
- **Contrast:** four apps, four AI postures (none / none / enterprise gates / personal coach).
- **Consumer teaser:** “Miss a day? HabitCheck helps you come back — without fake completion.”

---

## 8. Success metrics (first 8 weeks)

1. 4-week retention of installed-PWA users
2. Recovery-path completion rate among users who miss a week
3. AI opt-in usage (starter / review / comeback)
4. Article reads + engagement vs prior series posts

---

## 9. Risks

| Risk | Mitigation |
|------|------------|
| AI gimmick | Code owns scores; model proposes only |
| Inflated completion via mini habits | Smaller version ≠ full completion |
| Scope creep | MVP spec + ≤3 habits + no chat |
| iOS reminders | Best-effort + in-app banners |
