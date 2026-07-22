# HabitCheck — MVP Specification (Implementation-Ready)

**Series:** AI in Action #4 · Better Living candidate  
**Status:** Discovery complete · ready for scaffold after owner go  
**Spec version:** v4 · July 2026  
**Parents:** [brief](./habitcheck-00-discovery-brief.md) · [product decisions](./habitcheck-01-product-decisions.md) · [architecture](../../apps/habitcheck-architecture.md) · [build spec](../../apps/habitcheck.md)

This document is the **implementation contract** for HabitCheck v1.0. Tracking math and AI boundaries here override earlier drafts that deferred AI or used daily/weekday schedule kinds.

---

## 0. One-liner

**HabitCheck** helps busy adults build healthier routines with flexible weekly targets, kind recovery after misses, and optional AI coaching — local-first, private by default.

**Promise:** Recover after missed days (without shame, without inflating completion).

**Differentiator vs siblings:** personal habit coach (comebacks · weekly insights · plan adjustments) on a deterministic weekly tracking core — not RetireCheck math, not SleepCheck sensory, not Readiness enterprise gates.

---

## 1. Locked decisions (normative)

| Area | Lock |
|------|------|
| Audience | Busy adults building healthier routines |
| Promise | Recover after missed days |
| Qualities | Private · Simple · Encouraging · Optional AI guidance |
| Active habits | **Up to 3** |
| Habit type (v1) | **Build only** (break-habits deferred) |
| Schedule | **Flexible weekly target** only (N of 7, N = 1–7) |
| Tracking week | **Monday–Sunday** (local timezone) |
| Formal miss | **Only when the week ends** without meeting target |
| Mid-week signal | Soft **at risk** when remaining days cannot meet target |
| Check-in | Status + optional difficulty (`easy` \| `manageable` \| `hard`) |
| Progress metrics | **Weekly consistency %** (primary) + **successful recoveries** (secondary) |
| Recovery UX | User chooses path: smaller version · reschedule in week · choose next restart day · Ask AI comeback |
| Successful recovery | User **followed the selected recovery path** (action completed) |
| Smaller version counting | **Recovery, not full completion** toward weekly target |
| Smaller version definition | **Preset at setup + customize** at recovery |
| Setup fields | Name · weekly target · motivation · smaller version |
| Target change trigger (down) | After **two consecutive difficult weeks** |
| Consistently easy | **Two consecutive easy weeks** → ask maintain or progress |
| Target change UX | **Accept · edit · dismiss** (never auto-apply); edits/suggestions take effect **next Monday** |
| Pause | **Either:** indefinite (no progress penalty) **or** until return date |
| Mid-week pause/resume | Week marked **`partially_paused`** (excluded from averages/triggers) |
| Pause end (dated) | **Resume automatically + reminder** |
| Reminders | Optional daily **in-app** at chosen time; system notification only when reliably supported |
| Weekly review content | Balanced: consistency · recoveries · difficulty → adjustments |
| Weekly review availability | After Sunday ends · **view anytime** (on-demand) |
| AI in v1.0 | Required: Weekly Review · personalized comebacks. Optional if time permits: Habit Starter. Target numbers remain deterministic; AI explanation may follow in v1.1. |
| AI data | **Selected summaries only** · opt-in **per AI action** |
| AI UI | **No chat** |
| Repo | Single Next.js app (no Turborepo day one) |
| Host | `habitcheck.weidong-shi.com` |

---

## 2. User flows

### 2.1 First-run onboarding

1. Welcome + wellness disclaimer (not medical advice).
2. Privacy posture: local-first; AI optional; summaries-only when used.
3. Optional: **Habit Starter** (AI) — plain-language goal → proposed habit (name, target, motivation, smaller version) → accept / edit / dismiss.
4. Or: manual create (same fields).
5. Land on **Today** with 1 habit (encourage staying ≤3).

### 2.2 Daily check-in (happy path)

1. Open Today → see up to 3 habits for the current week context.
2. Tap habit → mark **done** / **skipped** (or leave unset).
3. If done: optional difficulty chip (easy / manageable / hard); skip allowed.
4. Derived week progress updates (completions toward target; consistency preview).

### 2.3 Mid-week at risk

1. Tracking detects remaining calendar days in Mon–Sun week cannot reach `target` given current `done` count.
2. Soft banner: “This week is at risk” + CTA **Choose a recovery path** (does **not** mark formal miss).
3. User may dismiss; banner can return once per day max.

### 2.4 Missed week (Sunday ended)

1. After local Sunday 24:00 boundary: if `doneCount < target` → week status = **missed**.
2. Recovery sheet (choose one):
   - **Do a smaller version today** (preset; editable) → on complete → **successful recovery** (not full completion).
   - **Reschedule within the week** — N/A after week closed; after miss, interpret as **plan one catch-up completion in the new week** that counts as recovery action, not toward previous week.
   - **Choose my next restart day** — select a date in the current or following week; counts as recovery when the linked normal completion occurs on that date.
   - **Ask AI for a personalized comeback** — opt-in; summary payload; returns suggested micro-action → accept / edit / dismiss → complete → recovery.
3. Recording recovery increments `successfulRecoveries`; does not rewrite prior week’s consistency truth.

**Reschedule within week (while week still open):** user picks a future day in the current Mon–Sun week as intended catch-up; completing `done` that day counts as **full completion** toward target (normal). If they chose recovery *because of a daily slip* but week not missed yet, smaller-version still counts as recovery only.

### 2.5 Weekly review

1. Available anytime after prior week ends (Mon 00:00 onward for that closed week).
2. Screen shows deterministic stats: consistency %, recoveries, difficulty mix, at-risk events — as **three separate concepts**, never blended into one score.
3. Optional **AI Weekly Review** — opt-in → privacy gate → narrative balanced across consistency / recoveries / difficulty + one suggestion.
4. Offline / decline → stats-only view.

### 2.6 Target suggestion (down)

1. Two consecutive weeks classified **difficult** (see scoring).
2. Deterministic logic proposes `max(1, currentTarget - 1)`; AI may explain the recommendation but cannot choose an arbitrary target.
3. In-app prompt (not every review): suggested lower weekly target.
4. User: accept / edit / dismiss. Dismiss snoozes until the next qualifying pair (or manual ask from habit settings).
5. Accepted/edited target applies at the **next Monday** boundary; current week keeps its snapshot target.

### 2.7 Progression (up)

1. Two consecutive weeks classified **easy**.
2. Prompt: maintain or progress? If progress → deterministic `min(7, currentTarget + 1)`; AI may explain → accept / edit / dismiss.
3. Accepted change applies next Monday.

### 2.8 Pause / resume

1. Habit settings → Pause → indefinite **or** until date.
2. While paused: no expectation; full paused weeks are excluded from consistency.
3. A pause or resume during a week marks that week `partially_paused`; check-ins remain visible, but the week is excluded from consistency and two-week triggers.
4. Dated pause ends → habit active again + best-effort local reminder (if supported and enabled); otherwise show an in-app banner on next open.
5. Full scoring resumes the next Monday after a partial week.

### 2.9 Habit lifecycle

- Create / edit / archive (archive frees a slot toward the 3-active cap).
- Active cap enforced at create time.

---

## 3. Screens (IA)

| Route / surface | Purpose |
|-----------------|--------|
| `/` Today | Check-in, week progress rings, at-risk / recovery CTAs |
| `/habits/new` | Manual create or entry to Habit Starter |
| `/habits/[id]` | Detail: heatmap-lite, motivation, edit, pause, archive |
| `/habits/[id]/edit` | Edit fields including smaller version + target |
| `/review` | Closed-week picker + stats; AI review CTA |
| `/settings` | Theme, reminders master, export/import, about |
| `/privacy` | Privacy + wellness + AI disclosure |
| Modals | Recovery path sheet · AI consent · target change · Habit Starter result |

**Chrome:** skip link, mobile nav, theme toggle (parity with siblings). No dashboard clutter on first viewport — Today is one composition: habits + this week’s progress.

---

## 4. Data model

```ts
type Difficulty = "easy" | "manageable" | "hard";

type Habit = {
  id: string;
  name: string;
  motivation: string;
  weeklyTarget: number; // 1–7
  smallerVersion: string; // preset comeback text
  color?: string;
  icon?: string;
  status: "active" | "paused" | "archived";
  pause: null | { kind: "indefinite" } | { kind: "until"; untilDate: string }; // YYYY-MM-DD
  reminder?: { enabled: boolean; timeLocal: string }; // HH:mm
  /** Queued target after accept/edit; applied next Monday */
  pendingWeeklyTarget?: number;
  createdAt: string;
  archivedAt?: string;
};

type CheckInStatus = "done" | "skipped";

type CheckIn = {
  id: string;
  habitId: string;
  date: string; // YYYY-MM-DD local
  status: CheckInStatus;
  difficulty?: Difficulty; // optional; typically with done
  countsTowardTarget: boolean; // true for normal done; false for recovery-only action
  recoveryEventId?: string;
  loggedAt: string;
};

type RecoveryKind =
  | "smaller_version"
  | "reschedule_in_week"
  | "restart_next" // user-selected restart day (not a fixed schedule slot)
  | "ai_comeback";

type RecoveryEvent = {
  id: string;
  habitId: string;
  triggerWeekStart: string; // Monday YYYY-MM-DD of the week that triggered recovery
  kind: RecoveryKind;
  status: "selected" | "completed" | "dismissed" | "expired";
  actionText?: string;
  scheduledFor?: string; // YYYY-MM-DD for reschedule/restart path
  completedOn?: string;
  linkedCheckInId?: string;
  createdAt: string;
};

type WeekSnapshot = {
  habitId: string;
  weekStart: string; // Monday
  target: number; // snapshot target for that week
  doneCount: number; // full completions only
  skippedCount: number;
  status: "in_progress" | "met" | "missed" | "paused" | "partially_paused";
  difficultyCounts: { easy: number; manageable: number; hard: number };
  atRiskFired: boolean;
};

type Settings = {
  theme: "system" | "light" | "dark";
  remindersEnabled: boolean;
  aiEnabled: boolean; // master; each call still confirms
  onboardingCompleted: boolean;
};

type AiInvocationLog = {
  id: string;
  feature: "habit_starter" | "weekly_review" | "comeback" | "target_suggest";
  createdAt: string;
  // no prompt/response bodies persisted by default in v1
};
```

**Export:** `habitcheck-export@2` — `{ version, exportedAt, habits, checkIns, recoveryEvents, settings }`.  
(Bump from unused `@1` drafts; no production data yet.)

**Hard rule:** streaks, consistency %, week status, easy/difficult week labels, and at-risk are **derived** in `src/lib/tracking/` — never stored as source of truth (WeekSnapshot may be cached for UI performance but must be recomputable).

---

## 5. Scoring rules (deterministic)

### 5.1 Week boundaries

- Week = local Monday 00:00 → Sunday 24:00.
- `weekStart` = Monday `YYYY-MM-DD`.
- Formal evaluation of met/missed runs when `asOf` date is strictly after that week’s Sunday.

### 5.2 Full completion

- A `CheckIn` with `status: "done"` and `countsTowardTarget: true` on date D counts **+1** toward `doneCount` for that week.
- Smaller-version recovery completions are logged as recovery events (and may create a check-in tagged recovery-only) and **do not** increment `doneCount`.
- At most one target-counting completion exists per habit per local calendar date. Editing replaces that day's target-counting state instead of adding another completion.
- A recovery-only action may coexist on the same date but never increments `doneCount`.

### 5.3 Weekly consistency %

For a closed week with status neither `paused` nor `partially_paused`:

```
consistency = doneCount / weeklyTarget   // clamp display 0–100%+ optional cap at 100% for UI
```

Across weeks (habit progress): mean of closed non-paused / non-partially-paused weeks’ consistency (cap each week at 100% for averages).

Keep **consistency**, **successful recoveries**, and **difficulty pattern** visible as separate concepts — never merge into one score.

### 5.4 Met / missed / in progress

| Condition | Status |
|-----------|--------|
| Habit is paused for the entire week | `paused` (excluded from consistency averages) |
| Habit paused or resumed during week | `partially_paused` (excluded from averages and classification triggers) |
| Week still open | `in_progress` |
| Closed & `doneCount >= target` | `met` |
| Closed & `doneCount < target` | `missed` |

### 5.5 At risk (mid-week)

Assumption: at most one qualifying target-counting completion per habit per local day.

```
remainingDays = count of days from tomorrow through Sunday inclusive (local)
atRisk = week in_progress AND (doneCount + remainingDays) < target
```

Today can still be used: if including today as possible done:

```
possible = doneCount + (todayUnset ? 1 : 0) + daysAfterTodayThroughSunday
atRisk = possible < target
```

### 5.6 Successful recovery

Increment when `RecoveryEvent.status === "completed"` for a chosen path:

| Path | Completion criterion |
|------|----------------------|
| `smaller_version` | User logs recovery done (`countsTowardTarget: false`) for the agreed micro-action |
| `reschedule_in_week` | User completes a normal `done` on the chosen future day in an open week; **or** after missed week, completes the planned catch-up `done` in the new week (linked via `linkedCheckInId`) |
| `restart_next` | Linked normal completion (`countsTowardTarget: true`) occurs on the user-selected restart date (`scheduledFor`) in the current or following week |
| `ai_comeback` | User accepts (or edits) AI action and logs it complete (usually as recovery-only done) |

Abandoned paths use `dismissed` or `expired` — never count as successful recoveries.

### 5.7 Difficult week / easy week

Use this **single** authoritative classification algorithm for closed, non-paused, non-partially-paused weeks:

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

A week with no difficulty data is **neutral unless the weekly target was missed**. `paused` and `partially_paused` weeks are excluded.

**Down-suggest:** two consecutive closed weeks both `difficult` for same habit.  
**Up-ask:** two consecutive closed weeks both `easy`.

### 5.8 Active habit cap

`count(status === active || (status === paused)) ≤ 3`. Archived excluded. Creating the 4th active/paused is blocked.

### 5.9 Target change effective date

- Manual edits and accepted suggestions set `pendingWeeklyTarget`.
- On each local Monday, apply pending target to `weeklyTarget` and clear pending.
- Current open week always scores against `WeekSnapshot.target` captured at week start (or habit create if created mid-week).

---

## 6. AI boundaries

### 6.1 Features and release sequence

| Feature | Trigger | Input (after gate) | Output | User control |
|---------|---------|--------------------|--------|--------------|
| Habit Starter (v1.0 optional) | Onboarding / new habit | Goal text + optional constraints | name, target, motivation, smallerVersion | accept / edit / dismiss |
| Personalized comeback (v1.0 required) | Recovery path | Habit summary + week aggregates + smallerVersion preset | micro-action + short encouragement | accept / edit / dismiss |
| Weekly Review (v1.0 required) | `/review` CTA | Week aggregates for ≤3 habits | balanced narrative + one suggestion | display only; suggestions that change targets go through target UX |
| Target explanation (v1.1) | Two difficult or two easy weeks | Habit + two-week aggregates + deterministic allowed target | explanation of adjustment | accept / edit / dismiss |

**Target numbers:** deterministic only — `max(1, current - 1)` or `min(7, current + 1)`. The model may explain; it must not invent an unrestricted number.

Encouragement is **tone inside** these features — not a separate product surface.

### 6.2 Privacy gate

- Master `settings.aiEnabled` plus **confirm each invocation**.
- Payload whitelist only, e.g.:

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
  // no free-text check-in notes (none in v1); motivation allowed only for Habit Starter edit flows if user opts in
};
```

- Never send full history by default; Weekly Review sends **selected closed week(s)** summaries only (default: last 1–4 weeks aggregates).
- `privacyGate(feature, payload)` is the only browser→server path for model calls.
- Versioned prompts in-repo; cost caps; fail closed to non-AI UI.
- Offline: hide or disable AI CTAs; core tracking works.

### 6.3 Non-goals (AI)

- Chat / multi-turn coach
- On-device LLM requirement
- Auto-applying target or habit edits
- Allowing the model to choose an unrestricted numeric target
- Adaptive reminder ML
- Sending raw journal text (no journals in v1)

---

## 7. Local storage & platform

| Concern | Choice |
|---------|--------|
| DB | IndexedDB via Dexie |
| Derived logic | `src/lib/tracking/` pure functions + Vitest |
| PWA | Installable; offline check-in |
| Reminders | Optional daily **in-app** reminder at chosen local time; stop after weekly target met; pause suppresses; recovery date = one-time; system notification only when reliably supported |
| Analytics | Page views only if used; never habit payloads |
| CI | lint · typecheck · test · build |
| Host | Vercel + `habitcheck.weidong-shi.com` |

**Release note:** in-app reminders are required; background/system notification delivery is **not** a v1 release blocker (especially iOS PWA).

---

## 8. Edge cases

| Case | Behavior |
|------|----------|
| User in timezone crossing week boundary | All dates local; document that travel may shift week; no cloud reconcile |
| Pause or resume mid-week | Preserve check-ins; mark `partially_paused`; exclude week from averages/triggers; full scoring resumes next Monday |
| Archive mid-week | Preserve history; treat current week as `partially_paused` |
| Two recoveries same week | Allowed; each completed path counts; still no target inflation from smaller version |
| Edit past check-ins | Backfill last **7** local days only |
| Target edited mid-week | Queue change for next Monday; current week retains its snapshot target |
| AI returns invalid target | Ignore model number; keep deterministic suggestion; show error if needed |
| Reminder permission denied | In-app banners only; core OK |
| Fourth habit | Block with message to archive/pause one |
| Break-habit requests | Out of scope — copy points to build framing |
| Empty difficulty on all dones | Neutral unless the weekly target was missed |
| Sunday evening open app | Week still `in_progress` until local Monday |
| Daily reminder | Stop for the week after target is met; pause suppresses it |
| Recovery reminder | Separate one-time reminder for selected reschedule/restart date |
| Unsupported notifications | In-app reminders remain required; background delivery is not a release blocker |
| AI consent declined on AI recovery path | Fall back to non-AI paths (smaller version / restart day) without losing tracking |
| AI failure | Fail closed; tracking and stats remain fully usable |

### 8.1 Recovery-oriented language

Avoid: “failed,” “broke your streak,” “fell behind,” “try harder,” and “you only completed.”

Prefer: “This week didn’t go as planned,” “Choose a way to restart,” “A smaller action still matters,” “Your previous progress remains,” and “What feels realistic now?”

---

## 9. Acceptance criteria (v1.0 Done)

### Product

- [ ] Create up to 3 active habits with name, target, motivation, smaller version
- [ ] Daily done/skip + optional difficulty
- [ ] Enforce one target-counting completion per habit per local date
- [ ] Mon–Sun week progress; met/missed only after Sunday
- [ ] At-risk soft state mid-week
- [ ] Recovery sheet with 4 paths; smaller version = recovery not full completion
- [ ] Successful recovery counter increments on path completion
- [ ] Pause indefinite + until-date; dated end resumes + reminder/banner
- [ ] Mid-week pause/resume → `partially_paused` exclusion rules
- [ ] Weekly review stats after week ends; on-demand; metrics shown separately
- [ ] AI Comeback and Weekly Review behind per-action consent + summary-only gate
- [ ] AI Habit Starter may ship in v1.0 if time permits; AI target explanations may follow in v1.1
- [ ] Target changes never auto-apply
- [ ] Target edits and accepted suggestions take effect the next Monday
- [ ] Two difficult → down suggest; two easy → maintain/progress ask (deterministic ±1)
- [ ] Export/import `habitcheck-export@2`
- [ ] Privacy page + wellness disclaimer + AI disclosure
- [ ] Live on `habitcheck.weidong-shi.com`; CI green; PWA installable
- [ ] In-app reminders work; system notifications best-effort only (not a blocker)

### Engineering

- [ ] Tracking rules covered by unit tests (week status, at-risk, consistency, easy/difficult, recovery counting)
- [ ] Regression tests cover: duplicate same-day completion; recovery-only plus full completion; recovery early/on-time/late/never; cross-week restart; midweek pause/resume; next-Monday target change; missed weeks without ratings; easy week with one rated completion; daylight-saving/timezone boundaries; malformed/future imports; archive history; AI failure/declined consent; reminder suppression after target met
- [ ] No streak/consistency persisted as source of truth
- [ ] A11y: skip link, labels, focus, touch targets (sibling parity)

---

## 10. Phased implementation plan

| Phase | Goal | Exit |
|-------|------|------|
| **P0 — Scaffold** | Next.js + Tailwind v4 + Dexie + CI + `/privacy` stub | Deploy preview URL |
| **P1 — Tracking core** | Schema + pure tracking tests green (week, at-risk, consistency, recovery flags) | Tests are spec |
| **P2 — Today loop** | CRUD ≤3 habits, check-in, week ring, backfill 7d | Vertical slice usable offline |
| **P3 — Recovery & pause** | Recovery sheet, smaller-version rules, pause/resume + reminder hook | Promise visible in UI |
| **P4 — Review & progression** | `/review` stats; easy/difficult detection; deterministic target prompts accept/edit/dismiss | Non-AI coach loop complete |
| **P5 — AI** | privacyGate + required Comeback + Weekly Review; optional Habit Starter; deterministic target suggestion (AI explanation optional / v1.1) | Opt-in AI demos; fail closed |
| **P6 — Polish** | PWA, a11y, export/import, empty states, domain, hub case study draft | **v1.0 ship** |

**Indicative calendar:** ~4–6 weeks depending on AI provider reuse from Readiness.

**Post-v1.1 candidates:** AI-written target explanations, break-habits, specific weekdays schedules, user-chosen week start, chat-free deeper history insights, extract `@better-living/tracking`.

---

## 11. Content / portfolio notes

- **Thesis:** Recover without shame — weekly honesty + AI comebacks on a deterministic core.
- **Contrast chart:** RetireCheck (math) · SleepCheck (sensory) · Readiness (enterprise gates) · HabitCheck (personal coach + weekly grace).
- **Methodology:** Build → Validate → Improve → Document → Share.
- No monetization / pricing on public surfaces.

---

## 12. Open at scaffold (non-blocking)

- Exact GitHub repo name
- Visual identity (color/icon) within Better Living wellness tone — avoid generic purple-AI clichés
- Whether Habit Starter is offered before first manual create (recommend: yes, skippable)
