# HabitCheck — MVP Specification (Implementation-Ready)

**Series:** AI in Action #4 · Better Living candidate  
**Status:** Discovery complete · **P0–P7 code complete** on [HabitCheck](https://github.com/weidong808/HabitCheck) · public deploy/domain pending 
**Spec version:** v5 · July 2026 (**AI-forward**)  
**Parents:** [brief](./habitcheck-00-discovery-brief.md) · [product decisions](./habitcheck-01-product-decisions.md) · [architecture](../../apps/habitcheck-architecture.md) · [build spec](../../apps/habitcheck.md)

This document is the **implementation contract** for HabitCheck v1.0. Tracking math remains deterministic; **AI coaching is a first-class product surface** (not optional polish). Overrides v3–v4 drafts that deferred or thinned AI.

---

## 0. One-liner

**HabitCheck** is a local-first weekly habit coach: flexible targets, kind recovery after misses, and AI guidance at every key moment — private by default, facts always honest.

**Promise:** Recover after missed days (without shame, without inflating completion).

**Differentiator vs siblings:** a **personal habit operating system** — AI in setup, recovery, review, and plan changes — on a deterministic weekly core. Not RetireCheck math, not SleepCheck sensory, not Readiness enterprise gates.

**AI weight (locked):** ~45–55% of product story and build. Tracking is the foundation; every key moment has a coach surface. Offline/declined AI → app still fully usable.

---

## 1. Locked decisions (normative)

| Area | Lock |
|------|------|
| Audience | Busy adults building healthier routines |
| Promise | Recover after missed days |
| Qualities | Private · Simple · Encouraging · **AI-powered coaching (first-class)** |
| Active habits | **Up to 3** |
| Habit type (v1) | **Build only** (break-habits deferred) |
| Schedule | **Flexible weekly target** only (N of 7, N = 1–7) |
| Tracking week | **Monday–Sunday** (local timezone) |
| Formal miss | **Only when the week ends** without meeting target |
| Mid-week signal | Soft **at risk** when remaining days cannot meet target |
| Check-in | Status + optional difficulty (`easy` \| `manageable` \| `hard`) |
| Progress metrics | **Weekly consistency %** · **successful recoveries** · **difficulty pattern** (three separate concepts) |
| Recovery UX | User chooses path: smaller version · reschedule in week · choose next restart day · **AI Comeback Coach** |
| Successful recovery | User **followed the selected recovery path** (action completed) |
| Smaller version counting | **Recovery, not full completion** toward weekly target |
| Smaller version definition | **AI-generated or preset at setup + customize** at recovery |
| Setup fields | Name · weekly target · motivation · smaller version · optional first-two-weeks ramp |
| Target change trigger (down) | After **two consecutive difficult weeks** |
| Consistently easy | **Two consecutive easy weeks** → ask maintain or progress |
| Target change UX | Deterministic ±1 + **AI Plan Adjuster explanation** · accept / edit / dismiss · **effective next Monday** |
| Pause | **Either:** indefinite **or** until return date |
| Mid-week pause/resume | Week marked **`partially_paused`** |
| Pause end (dated) | **Resume automatically + reminder** |
| Reminders | Optional daily **in-app** at chosen time; system notification best-effort |
| Weekly review | Deterministic stats + **required AI structured insight cards** |
| Weekly review availability | After Sunday ends · **view anytime** |
| AI in v1.0 | **All required:** Habit Starter · Comeback Coach · Weekly Review · Plan Adjuster · Smart smaller-version |
| AI data | **Selected summaries only** · opt-in **per AI action** |
| AI UI | **No free chat** — guided coach moments only; **Facts vs Coach** layout |
| Engineering shine | Privacy gate · versioned prompts · cost caps · streaming · eval fixtures · fail closed |
| Repo | Single Next.js app (no Turborepo day one) |
| Host | `habitcheck.weidong-shi.com` |

---

## 2. User flows

### 2.1 First-run onboarding

1. Welcome + wellness disclaimer (not medical advice).
2. Privacy posture: local-first; AI coaching available with summary-only sends; per-action consent.
3. **Habit Starter (AI, required path, skippable to manual):** plain-language goal → proposed habit (name, target, motivation, smaller version, first-two-weeks ramp) → accept / edit / dismiss.
4. Manual create remains available (same fields); **Smart smaller-version** can still generate/refine the micro-action.
5. Land on **Today** with 1 habit (encourage staying ≤3). UI shows **Facts** (week target) clearly; coach copy is secondary.

### 2.2 Daily check-in (happy path)

1. Open Today → see up to 3 habits for the current week context.
2. Tap habit → mark **done** / **skipped** (or leave unset).
3. If done: optional difficulty chip (easy / manageable / hard); skip allowed.
4. Derived week progress updates (completions toward target; consistency preview).

### 2.3 Mid-week at risk

1. Tracking detects remaining calendar days cannot reach `target`.
2. Soft banner (recovery language) + CTA **Choose a recovery path**.
3. Prefer opening **AI Comeback Coach** as the highlighted path (user can still pick non-AI paths).
4. User may dismiss; banner can return once per day max.

### 2.4 Missed week (Sunday ended)

1. After local Sunday 24:00: if `doneCount < target` → week status = **missed**.
2. Recovery sheet (choose one):
   - **Do a smaller version today** (AI-refined or preset; editable) → complete → **successful recovery** (not full completion).
   - **Reschedule within the week** — after miss: plan one catch-up in the **new** week (linked recovery).
   - **Choose my next restart day** — select date in current or following week; recovery when linked normal completion lands on that date.
   - **AI Comeback Coach** — opt-in → **2–3 micro-options** + short encouragement → pick / edit → complete → recovery.
3. Recovery never rewrites prior week’s consistency truth.

**Reschedule while week still open:** future day in current Mon–Sun; normal `done` counts toward target. Smaller-version remains recovery-only.

### 2.5 Weekly review

1. Available anytime after prior week ends.
2. **Facts panel:** consistency %, recoveries, difficulty mix, at-risk events (deterministic, separate metrics).
3. **Coach panel (required AI):** structured insight cards (one card per theme: consistency · recoveries · difficulty) + one next-week move → streaming OK.
4. Offline / decline → Facts-only view (still a complete review).

### 2.6 Plan Adjuster (down)

1. Two consecutive **difficult** weeks.
2. Deterministic proposal: `max(1, currentTarget - 1)`.
3. **AI Plan Adjuster** explains *why* this range helps (cannot invent another number).
4. Accept / edit / dismiss; apply **next Monday**.

### 2.7 Plan Adjuster (up)

1. Two consecutive **easy** weeks.
2. Maintain or progress? Progress → `min(7, currentTarget + 1)` + AI explanation → accept / edit / dismiss → next Monday.

### 2.8 Pause / resume

Unchanged from v4: indefinite or until-date; mid-week → `partially_paused`; dated end resumes + reminder/banner; full scoring next Monday.

### 2.9 Habit lifecycle

Create / edit / archive; active+paused cap ≤3.

---

## 3. Screens (IA)

| Route / surface | Purpose |
|-----------------|--------|
| `/` Today | Check-in, week rings, at-risk / recovery CTAs, coach entry points |
| `/habits/new` | Habit Starter (primary) + manual create |
| `/habits/[id]` | Detail: Facts + optional Coach actions; heatmap-lite; pause/archive |
| `/habits/[id]/edit` | Edit fields; Smart smaller-version regenerate |
| `/review` | Facts vs Coach weekly review |
| `/settings` | Theme, reminders, AI master toggle, export/import, about |
| `/privacy` | Privacy + wellness + AI disclosure |
| Modals | Recovery sheet · Comeback Coach (2–3 options) · Plan Adjuster · Starter result · AI consent |

**Chrome:** skip link, mobile nav, theme toggle. Today = one composition (habits + this week).  
**UI rule:** label **Facts** (code) vs **Coach** (AI) wherever both appear — portfolio-readable trust pattern.

---

## 4. Data model

```ts
type Difficulty = "easy" | "manageable" | "hard";

type Habit = {
  id: string;
  name: string;
  motivation: string;
  weeklyTarget: number; // 1–7
  smallerVersion: string;
  /** Optional AI Starter output; display-only guidance for first 14 days */
  firstTwoWeeksRamp?: string[];
  color?: string;
  icon?: string;
  status: "active" | "paused" | "archived";
  pause: null | { kind: "indefinite" } | { kind: "until"; untilDate: string };
  reminder?: { enabled: boolean; timeLocal: string };
  pendingWeeklyTarget?: number;
  createdAt: string;
  archivedAt?: string;
};

type CheckInStatus = "done" | "skipped";

type CheckIn = {
  id: string;
  habitId: string;
  date: string;
  status: CheckInStatus;
  difficulty?: Difficulty;
  countsTowardTarget: boolean;
  recoveryEventId?: string;
  loggedAt: string;
};

type RecoveryKind =
  | "smaller_version"
  | "reschedule_in_week"
  | "restart_next"
  | "ai_comeback";

type RecoveryEvent = {
  id: string;
  habitId: string;
  triggerWeekStart: string;
  kind: RecoveryKind;
  status: "selected" | "completed" | "dismissed" | "expired";
  actionText?: string;
  /** For ai_comeback: options shown before user picks */
  aiOptions?: string[];
  scheduledFor?: string;
  completedOn?: string;
  linkedCheckInId?: string;
  createdAt: string;
};

type WeekSnapshot = {
  habitId: string;
  weekStart: string;
  target: number;
  doneCount: number;
  skippedCount: number;
  status: "in_progress" | "met" | "missed" | "paused" | "partially_paused";
  difficultyCounts: { easy: number; manageable: number; hard: number };
  atRiskFired: boolean;
};

type Settings = {
  theme: "system" | "light" | "dark";
  remindersEnabled: boolean;
  aiEnabled: boolean;
  onboardingCompleted: boolean;
};

type AiInvocationLog = {
  id: string;
  feature:
    | "habit_starter"
    | "weekly_review"
    | "comeback"
    | "plan_adjuster"
    | "smaller_version";
  promptVersion: string;
  createdAt: string;
};
```

**Export:** `habitcheck-export@2` — `{ version, exportedAt, habits, checkIns, recoveryEvents, settings }`.

**Hard rule:** consistency %, week status, easy/difficult, at-risk are **derived** in `src/lib/tracking/` — never source-of-truth in storage.

---

## 5. Scoring rules (deterministic)

### 5.1–5.9

Same authoritative rules as v4:

- Mon–Sun weeks; miss only after Sunday
- `countsTowardTarget` + one target-counting done per habit per local day
- Recovery-only never inflates `doneCount`
- `classifyWeek` single algorithm (missed → difficult; no ratings → neutral unless missed)
- `partially_paused` excluded from averages/triggers
- Target changes via `pendingWeeklyTarget` apply **next Monday**
- At-risk assumes ≤1 full completion per day

See v4 text retained below for implementers.

### 5.1 Week boundaries

- Week = local Monday 00:00 → Sunday 24:00.
- Formal met/missed when `asOf` is strictly after that week’s Sunday.

### 5.2 Full completion

- `done` + `countsTowardTarget: true` → +1 `doneCount`.
- Recovery-only done → never +1.
- Edit replaces same-day target-counting state; recovery-only may coexist.

### 5.3 Weekly consistency %

```
consistency = doneCount / target  // UI may cap display at 100%
```

Exclude `paused` / `partially_paused` from averages. Never blend with recoveries into one score.

### 5.4 Week status

| Condition | Status |
|-----------|--------|
| Paused entire week | `paused` |
| Pause/resume mid-week | `partially_paused` |
| Open | `in_progress` |
| Closed & doneCount ≥ target | `met` |
| Closed & doneCount < target | `missed` |

### 5.5 At risk

```
possible = doneCount + (todayUnset ? 1 : 0) + daysAfterTodayThroughSunday
atRisk = in_progress && possible < target
```

### 5.6 Successful recovery

`RecoveryEvent.status === "completed"` per path rules (smaller_version / reschedule / restart_next / ai_comeback). `dismissed` / `expired` do not count.

For **ai_comeback:** user must pick (or edit) one of `aiOptions` (or equivalent single action) and complete it.

### 5.7 Easy / difficult

```ts
function classifyWeek(week: ClosedWeek): "easy" | "difficult" | "neutral" {
  const { easy, manageable, hard } = week.difficultyCounts;
  const ratedCount = easy + manageable + hard;
  if (week.status === "missed") return "difficult";
  if (ratedCount === 0) return "neutral";
  if (week.status === "met" && easy >= manageable + hard) return "easy";
  if (hard >= 2 && hard >= easy) return "difficult";
  return "neutral";
}
```

### 5.8 Cap

`active + paused ≤ 3`.

### 5.9 Target effective date

Pending target applies local Monday; open week uses snapshot target.

---

## 6. AI boundaries (first-class)

### 6.1 Required v1.0 features

| Feature | Trigger | Input (after gate) | Output | User control |
|---------|---------|--------------------|--------|--------------|
| **Habit Starter** | Onboarding / new habit | Goal text + constraints | name, target, motivation, smallerVersion, firstTwoWeeksRamp[] | accept / edit / dismiss |
| **Smart smaller-version** | Create/edit + recovery | Habit summary + optional goal | micro-action string | accept / edit / dismiss |
| **Comeback Coach** | At-risk / missed / recovery path | Habit + week aggregates + smallerVersion | **2–3** micro-options + short encouragement | pick / edit / dismiss |
| **Weekly Review** | `/review` | Aggregates for ≤3 habits (1–4 weeks) | **3 structured insight cards** + one next-week move | display; target changes via Plan Adjuster UX |
| **Plan Adjuster** | Two easy or two difficult weeks | Two-week aggregates + **deterministic allowed target** | Explanation only (number fixed by code) | accept / edit / dismiss |

**Target numbers:** code only — `max(1, current - 1)` or `min(7, current + 1)`. Model explains; never invents unrestricted N.

**No free chat** — guided coach moments only.

### 6.2 UX pattern: Facts vs Coach

Every AI-assisted screen must show:

1. **Facts** — numbers from `tracking` (consistency, done/target, recoveries, difficulty counts).
2. **Coach** — model narrative/options, clearly labeled, dismissible.

This is the portfolio trust signature (same spirit as Readiness hard gates + narrative).

### 6.3 Privacy gate

- `settings.aiEnabled` + **confirm each invocation**.
- Whitelist summaries only (`AiHabitSummary` + feature-specific fields such as `goalText` for Starter, `allowedTarget` for Plan Adjuster).
- Never send full history by default.
- `privacyGate(feature, payload)` sole browser→server path.
- Versioned prompts in-repo; cost caps; **streaming** supported for Review/Starter; fail closed.
- Offline: Facts work; Coach CTAs disabled or error with fallback copy.

```ts
type AiHabitSummary = {
  name: string;
  weeklyTarget: number;
  smallerVersion: string;
  week: {
    weekStart: string;
    doneCount: number;
    target: number;
    status: string;
    difficultyCounts: Record<Difficulty, number>;
    successfulRecoveriesInWeek: number;
    atRiskFired: boolean;
  };
};
```

### 6.4 Engineering shine (ship with v1.0)

| Capability | Requirement |
|------------|-------------|
| Prompt versions | `prompts/<feature>/vN.md` (or TS constants) referenced in logs |
| Cost caps | Per-day and per-invocation limits; friendly degrade |
| Streaming | Weekly Review + Habit Starter stream tokens into UI |
| Eval fixtures | Golden inputs → schema/shape checks for Starter, Comeback options (2–3), Review cards |
| Fail closed | Tracking never depends on model availability |
| Server validation | Reject non-whitelisted payload shapes |

### 6.5 Non-goals (AI)

- Free-form multi-turn chat inbox
- On-device LLM requirement
- Auto-applying target or habit edits
- Model-chosen unrestricted numeric targets
- Adaptive reminder ML
- Raw journals / full completion history uploads

---

## 7. Local storage & platform

| Concern | Choice |
|---------|--------|
| DB | IndexedDB via Dexie |
| Derived logic | `src/lib/tracking/` + Vitest |
| AI | `src/lib/ai/` privacyGate + prompts + clients; `src/app/api/ai/*` |
| PWA | Installable; offline Facts |
| Reminders | In-app daily; stop when target met; pause suppresses; recovery one-time; OS notify best-effort |
| CI | lint · typecheck · test · build (+ AI schema evals in test) |
| Host | Vercel + `habitcheck.weidong-shi.com` |

---

## 8. Edge cases

| Case | Behavior |
|------|----------|
| Timezone / travel | Local dates; document shift; no cloud reconcile |
| Mid-week pause/resume | `partially_paused`; scoring resumes next Monday |
| Archive mid-week | History kept; week `partially_paused` |
| Two recoveries same week | Allowed; no target inflation from mini actions |
| Backfill | Last 7 local days |
| Target mid-week | Queue for next Monday |
| Model invents target | Ignore; keep deterministic N |
| Comeback returns ≠2–3 options | Normalize/fail closed to preset smaller version |
| AI consent declined | Non-AI recovery paths; Facts intact |
| AI failure | Fail closed; tracking + Facts review OK |
| Reminder unsupported | In-app only; not a release blocker |
| Empty difficulty | Neutral unless missed |

### 8.1 Recovery-oriented language

Avoid: “failed,” “broke your streak,” “fell behind,” “try harder,” “you only completed.”

Prefer: “This week didn’t go as planned,” “Choose a way to restart,” “A smaller action still matters,” “Your previous progress remains,” “What feels realistic now?”

---

## 9. Acceptance criteria (v1.0 Done)

### Product

- [ ] ≤3 habits; setup fields + optional ramp from Starter
- [ ] Daily done/skip + difficulty; one target-counting done per habit/day
- [ ] Mon–Sun weeks; miss only after Sunday; at-risk mid-week
- [ ] Recovery paths including **AI Comeback Coach (2–3 options)**
- [ ] Smaller version = recovery, not full completion
- [ ] Pause + `partially_paused` rules
- [ ] Weekly review: **Facts + Coach cards** (Coach required when online/consenting)
- [ ] **Habit Starter** required in onboarding (skippable to manual)
- [ ] **Smart smaller-version** on create/recovery
- [ ] **Plan Adjuster**: deterministic ±1 + AI explanation; next Monday; never auto-apply
- [ ] Facts vs Coach labeling on AI surfaces
- [ ] Export/import `habitcheck-export@2`
- [ ] Privacy + wellness + AI disclosure
- [ ] Live domain; CI green; PWA installable
- [ ] In-app reminders; OS notify best-effort

### Engineering

- [ ] Tracking unit + regression tests (v4 suite)
- [ ] privacyGate + prompt versions + cost caps + fail closed
- [ ] Streaming for Starter and Weekly Review
- [ ] Eval fixtures for Starter / Comeback / Review card shape
- [ ] A11y parity with siblings

**v1.0 does not ship** without Habit Starter, Comeback Coach, Weekly Review Coach, and Plan Adjuster explanation — AI is a ship gate, not a stretch goal.

---

## 10. Phased implementation plan

| Phase | Goal | Exit |
|-------|------|------|
| **P0 — Scaffold** | Next.js + Tailwind v4 + Dexie + CI + `/privacy` + AI route stubs | Preview URL |
| **P1 — Tracking core** | Schema + pure tracking tests (v4 rules) | Tests are scoring spec |
| **P2 — Today loop** | CRUD ≤3, check-in, week ring, backfill | Offline Facts vertical slice |
| **P3 — Recovery & pause** | Recovery sheet, counting rules, pause/resume, reminders | Promise visible without AI |
| **P4 — Review & progression Facts** | `/review` Facts; easy/difficult; deterministic ±1 prompts | Non-AI coach loop |
| **P5 — AI platform** | privacyGate, prompts, caps, streaming, evals, Facts vs Coach chrome | AI substrate ready |
| **P6 — AI features** | Starter · Smart smaller-version · Comeback (2–3) · Review cards · Plan Adjuster | **All required AI live** |
| **P7 — Polish & ship** | PWA, a11y, export/import, domain, hub case study | **v1.0 ship** |

**Indicative calendar:** ~5–7 weeks (AI-forward adds platform + evals vs v4).

**Post-v1.1 candidates:** deeper multi-week Coach memory (still summary-only), break-habits, weekday schedules, user week-start, extract `@better-living/tracking` + `@better-living/ai`.

---

## 11. Content / portfolio notes

- **Thesis:** A personal habit OS — weekly honesty + AI coaching at every key moment, with Facts the model cannot rewrite.
- **Contrast:** RetireCheck (math) · SleepCheck (sensory) · Readiness (enterprise gates) · HabitCheck (**consumer coach OS**).
- **Demo script:** Starter → check-ins → at-risk Comeback (pick option) → missed week recovery → Weekly Review cards → Plan Adjuster.
- **Methodology:** Build → Validate → Improve → Document → Share.
- No monetization / pricing on public surfaces.

---

## 12. Open at scaffold (non-blocking)

- Exact GitHub repo name
- Visual identity (tech-forward wellness; avoid generic purple-AI clichés)
- Default model/provider env (reuse Readiness patterns where practical)
- Whether first-run forces Starter before manual (recommend: Starter primary, “enter manually” secondary)
