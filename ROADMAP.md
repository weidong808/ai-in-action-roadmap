# AI in Action — Roadmap

**Version:** 1.0  
**Owner:** Weidong Shi — Senior Technology Architect  
**Last updated:** July 2026

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
- [x] SleepCheck article published on hub ([weidong-shi.com/articles/ai-in-action-sleepcheck](https://weidong-shi.com/articles/ai-in-action-sleepcheck))
- [ ] SleepCheck LinkedIn pulse / AI in Action #2 video
- [x] SleepCheck architecture documented ([SleepCheck/docs/architecture.md](https://github.com/weidong808/SleepCheck/blob/main/docs/architecture.md))
- [x] Public roadmap repository launched ([ai-in-action-roadmap](https://github.com/weidong808/ai-in-action-roadmap))
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
- [ ] Publish AI in Action #2 on LinkedIn (+ optional short video)
- [ ] Improve application READMEs (screenshots, known issues, future features)
- [x] Define capability maturity levels (see `docs/capability-maturity.md`)
- [ ] GitHub improvements (CI badges, screenshots gallery)
- [ ] Optional: AI in Action #2 short video

---

## Phase 2 — Reusable Foundations

**Goal:** Extract what is genuinely shared. Nobody needs to “see” this work yet — future you will. Good portfolio signal: shared UI patterns, conventions, and deployment discipline.

- [ ] Identify genuinely shared components (only after duplication is real)
- [ ] Define common design system / shared theme direction
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
| 1 | SleepCheck polish (UI, bugs, a11y, responsive, performance) |
| 2 | AI in Action #2 LinkedIn / optional video; architecture diagrams |
| 3 | Local user history / sessions (no login yet) |
| 4 | Move toward authentication evaluation and design |

Content cadence: quality LinkedIn posts over volume (aim ~2/week when sustainable).

---

## Related documents

- Vision: [VISION.md](./VISION.md)
- Scope: [docs/scope.md](./docs/scope.md)
- Current state detail: [docs/current-state.md](./docs/current-state.md)
- Capability maturity: [docs/capability-maturity.md](./docs/capability-maturity.md)
- Auth strategy: [docs/authentication-strategy.md](./docs/authentication-strategy.md)
- 30 / 60 / 90 day plans: [milestones/](./milestones/)
