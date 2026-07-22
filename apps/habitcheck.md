# HabitCheck — Build Spec (AI in Action #4)

**Recover after missed days — local-first weekly habit OS with kind recovery and first-class AI coaching.**  
*AI in Action #4 · Better Living candidate · Spec v5 · July 2026*  
**Status:** Discovery complete — implementation-ready MVP spec locked (**v5 AI-forward**)

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
2. A **first-class AI coach platform** (~45–55% of story/build): Starter, Comeback Coach, Weekly Review cards, Plan Adjuster, Smart smaller-version — Facts vs Coach, no free chat.

**Locked decisions:**

| Decision | Choice |
|----------|--------|
| Repo shape | Single Next.js app (SleepCheck / Readiness pattern) |
| AI in v1.0 | **Ship gate** — all five coach surfaces required |
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
- Weekly review: **Facts + Coach insight cards** (after Sunday, anytime)
- AI: Habit Starter · Comeback Coach (2–3 options) · Smart smaller-version · Plan Adjuster
- Engineering shine: privacy gate, streaming, prompt versions, eval fixtures
- Opt-in in-app reminders; export/import; PWA; Privacy + wellness + AI disclosure

### Out (v1.0)

- Break-habits, weekday-specific schedules, free-form chat
- Accounts, cloud sync, social, native apps, Turborepo
- Adaptive reminder ML; auto-applied target changes; model-chosen unrestricted targets

---

## 4. AI design (v1.0 — ship gate)

| Feature | Model use | Deterministic part | Privacy |
|---------|-----------|--------------------|---------|
| Habit Starter | Goal → plan + 2-week ramp | Validation, cap ≤3 | Opt-in; goal + constraints |
| Smart smaller-version | Micro-action string | Recovery counting rules | Opt-in; habit summary |
| Comeback Coach | **2–3** micro-options + encouragement | Path completion rules | Opt-in; week/habit summary |
| Weekly Review Coach | 3 insight cards + next move | Stats computed locally | Opt-in; aggregates only |
| Plan Adjuster | Explains ±1 only | Easy/difficult + `max/min` clamp | Opt-in; two-week summary |

**UX:** Facts (code) vs Coach (AI) on every assisted surface.  
Same discipline as Readiness: versioned prompts, cost caps, privacy gate, streaming, fail closed, evals. Details: [MVP spec v5 §6](../docs/discovery/habitcheck-02-mvp-specification.md).

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
| Discovery | Brief · decisions · **MVP spec v5** · architecture (current) |
| P0–P2 | Scaffold · tracking tests · Today loop |
| P3–P4 | Recovery, pause, Facts review, deterministic ±1 |
| P5–P6 | AI platform + all required coach features |
| P7 | Polish · ship |
| Content | Hub `/work` + `/insights`, LinkedIn |

Definition of done: [MVP acceptance criteria](../docs/discovery/habitcheck-02-mvp-specification.md) — **AI is a ship gate**.

---

## 7. AI in Action #4 — content plan

- **Article thesis:** A personal habit OS — weekly honesty + AI at every key moment, with Facts the model cannot rewrite.
- **Contrast:** four apps, four AI postures (none / none / enterprise gates / **consumer coach OS**).
- **Demo:** Starter → Comeback options → Review cards → Plan Adjuster.
- **Consumer teaser:** “Miss a day? HabitCheck coaches you back — without fake completion.”

---

## 8. Success metrics (first 8 weeks)

1. 4-week retention of installed-PWA users
2. Recovery-path completion rate among users who miss a week
3. AI adoption across Starter / Comeback / Review / Plan Adjuster
4. Article reads + engagement vs prior series posts

---

## 9. Risks

| Risk | Mitigation |
|------|------------|
| AI gimmick | Facts vs Coach; code owns scores |
| Inflated completion via mini habits | Smaller version ≠ full completion |
| Scope creep | MVP v5 + ≤3 habits + no free chat |
| AI schedule slip | P5/P6 are ship gates, not stretch |
| iOS reminders | Best-effort + in-app banners |
