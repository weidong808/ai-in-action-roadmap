# AI in Action — Roadmap

**Version:** 1.0  
**Owner:** Weidong Shi — Senior Technology Architect  
**Last updated:** July 31, 2026

---

## Guiding Principle

Build one useful application at a time. Validate it, improve it, document what you learned, and share the case study. Identify reusable capabilities only when duplication is real — then evolve those into shared technical foundations.

**Build → Validate → Improve → Document → Share**

Not: design everything first. Not: force a platform before reuse is proven. Not: build authentication from scratch.

---

## Current State

- [x] RetireCheck live — [retirecheck.weidong-shi.com](https://retirecheck.weidong-shi.com)
- [x] SleepCheck live — [sleepcheck.weidong-shi.com](https://sleepcheck.weidong-shi.com)
- [x] Cursor in Action / RetireCheck article published
- [x] AI in Action series launched
- [x] SleepCheck article published on hub ([/insights/ai-in-action-sleepcheck](https://weidong-shi.com/insights/ai-in-action-sleepcheck))
- [x] SleepCheck LinkedIn — [AI in Action #2 Pulse](https://www.linkedin.com/pulse/ai-action-2-from-idea-sleepcheck-weidong-shi-0fwrc) + Improve-loop feed post
- [x] AI Production Readiness Advisor live — [readiness.weidong-shi.com](https://readiness.weidong-shi.com) · hub + LinkedIn [#3](https://www.linkedin.com/posts/weidong-shi_ai-in-action-3-is-your-ai-system-ready-activity-7486042640698732544-43tn)
- [x] HabitCheck live — [habitcheck.weidong-shi.com](https://habitcheck.weidong-shi.com) · hub case study + LinkedIn [#4](https://www.linkedin.com/posts/weidong-shi_ai-in-action-4-i-used-to-lie-to-my-habit-activity-7486417146093137922-klvA)
- [x] AI in Action short videos / launch cards on hub ([weidong-shi.com](https://weidong-shi.com))
- [x] SleepCheck architecture documented ([SleepCheck/docs/architecture.md](https://github.com/weidong808/SleepCheck/blob/main/docs/architecture.md))
- [x] Public roadmap repository launched ([ai-in-action-roadmap](https://github.com/weidong808/ai-in-action-roadmap))
- [x] Cross-app design-system token sync (UI Round 2 Track A) across hub + four apps
- [ ] AI in Action retrospective article (hub insight + LinkedIn) — **next content milestone**
- [ ] Shared cross-app architecture synthesized beyond per-app docs
- [ ] Optional authentication introduced (engineering learning milestone)
- [ ] Capability maturity model reflected in app design (local-first → optional sync → advanced local insights)

---

## Phase 1 — Showcase and Validation

**Goal:** Credibility. Polish apps, publish content, gather feedback. Keep demos free and educational.

- [ ] Polish SleepCheck (UI, bugs, a11y, responsive, performance)
- [ ] Improve accessibility and responsiveness (both apps as needed)
- [x] Document SleepCheck architecture (`docs/architecture.md`)
- [ ] Document RetireCheck architecture gaps vs roadmap diagrams
- [ ] Collect user feedback
- [x] Publish AI in Action #2 on hub site
- [x] Publish AI in Action #2 on LinkedIn (Pulse + Improve-loop feed post)
- [x] Publish AI in Action #3 and #4 on hub + LinkedIn
- [ ] Publish AI in Action retrospective (four-app synthesis) on hub + LinkedIn
- [ ] Improve application READMEs (screenshots, known issues, future features)
- [x] Define capability maturity levels (see `docs/capability-maturity.md`)
- [ ] GitHub improvements (CI badges, screenshots gallery)
- [ ] Optional: per-app short videos (RetireCheck done; SleepCheck / others open)

---

## Phase 2 — Reusable Foundations

**Goal:** Extract what is genuinely shared. Nobody needs to “see” this work yet — future you will. Good portfolio signal: shared UI patterns, conventions, and deployment discipline.

- [ ] Identify genuinely shared components (only after duplication is real)
- [x] Define common design system / shared theme direction (tokens + `DESIGN.md`; Round 2 Track A shipped)
- [ ] UI Round 2 craft layer (skeletons, empty/error states, motion system) — in progress
- [ ] Define shared user model (conceptual; implement later with optional auth)
- [ ] Establish common telemetry / observability conventions
- [ ] Establish common deployment patterns
- [ ] Shared UI / layouts / utilities where reuse is clear
- [ ] Shared configuration and validation patterns

Do not force a monorepo unless operational benefit is clear.

---

## Phase 3 — Optional Identity and Persistence

**Goal:** Demonstrate authentication and cloud sync as an architecture skill — not as a product lock-in. Local-first remains the default experience.

- [ ] Evaluate authentication providers (Entra External ID, Auth0, Clerk, Firebase, Supabase, Cognito, etc.)
- [ ] Add optional registered-user accounts (social + email as justified)
- [ ] Add optional cloud history and synchronization
- [ ] Define privacy and retention policies (required before auth ships)
- [ ] Add capability policy design (feature flags / access policies for advanced features)
- [ ] Deeper local history / sessions first where useful (may start before full auth)

---

## Phase 4 — Advanced Capabilities (Engineering Learning)

**Goal:** Feature flags, deeper insights, testing, and observability as architecture practice — still framed as educational showcase work.

- [ ] Introduce feature flags for gradual rollout
- [ ] Map capability maturity levels to named entitlements / policies
- [ ] Deeper local insights and history (non-diagnostic for SleepCheck)
- [ ] Strengthen automated testing and observability
- [ ] Accessibility hardening as a first-class milestone

---

## Future Technical Themes

- [ ] Shared identity patterns across Check apps (optional)
- [ ] Shared reporting conventions
- [ ] Shared AI insight patterns (with human validation of critical outputs)
- [ ] Cross-application dashboard (when identity exists)
- [ ] Wearable integrations (educational experiment; wellness framing)
- [ ] Additional Check applications (FitnessCheck, NutritionCheck, MindCheck, HealthCheck, …)
- [ ] Private experiments may exist separately — out of scope for this public repo

---

## Near-term sprint focus (illustrative)

| Sprint | Focus |
|--------|--------|
| 1 | **Retrospective article** (hub insight + LinkedIn) — synthesize Apps #1–#4 |
| 2 | Phase 1 closeout: READMEs, feedback channel, remaining polish |
| 3 | UI Round 2 craft (skeletons, empty states) + shared architecture doc |
| 4 | Local user history / sessions (no login yet); auth evaluation prep |

Content cadence: quality LinkedIn posts over volume (aim ~2/week when sustainable).

---

## Related documents

- Vision: [VISION.md](./VISION.md)
- Scope: [docs/scope.md](./docs/scope.md)
- Current state detail: [docs/current-state.md](./docs/current-state.md)
- Capability maturity: [docs/capability-maturity.md](./docs/capability-maturity.md)
- Auth strategy: [docs/authentication-strategy.md](./docs/authentication-strategy.md)
- 30 / 60 / 90 day plans: [milestones/](./milestones/)
