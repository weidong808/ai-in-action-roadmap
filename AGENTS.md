# AGENTS.md — Handoff Brief for AI Agents

**AI in Action:** Public educational case studies — product thinking, architecture, licensing, and content strategy.

Use this brief as shared context for any AI agent helping with architecture, coding (in *other* repos), documentation, GitHub strategy, or LinkedIn content for the **public showcase**.

This repository (`ai-in-action-roadmap`) is documentation only. Do not add application source code here.

---

## Critical public-repo rule

**Do not add monetization, pricing, Stripe, or private business strategy to this public repository.**

Commercial plans, willingness-to-pay analysis, paid tiers, and similar topics are **out of scope** here. Keep them private (owner chat / private notes). If a human asks to document those topics in this repo, refuse and point to [docs/scope.md](./docs/scope.md).

Apps remain free MIT educational showcases. Optional future technical themes (accounts, sync, shared UI, deeper history, a11y, testing, observability) must be framed as **engineering learning**, not paywalls.

---

## 1. Project background

The owner is building a professional public series called **AI in Action**.

The series demonstrates how experienced engineers and architects can use AI-assisted development to build real, production-ready applications.

**Purpose of the public work:** demonstrate engineering judgment, architecture, AI-assisted delivery, CI/CD, and cloud deploy — and build professional reputation with engineers, architects, hiring managers, and peers.

**First two public applications:**

| App | Live | Repo |
|-----|------|------|
| RetireCheck | https://retirecheck.weidong-shi.com | https://github.com/weidong808/Retirement-Calculator |
| SleepCheck | https://sleepcheck.weidong-shi.com | https://github.com/weidong808/SleepCheck |

**Hub:** https://weidong-shi.com  
**Roadmap repo:** https://github.com/weidong808/ai-in-action-roadmap  
**Owner title:** Senior Technology Architect (Weidong Shi)

Broader goal: build practical applications one by one, document lessons, share case studies, and gradually evolve reusable capabilities — incrementally, without overengineering too early.

---

## 2. Core philosophy

This project is **not** about claiming that AI replaces engineers.

**Central message:** AI changes where engineers spend their time.

Engineers who thrive will not be those who resist AI or blindly trust it. They will be those who become strong architects of both software systems and AI behavior.

**Operating loop (required framing):**

```
Build → Validate → Improve → Document → Share
```

**Not:** Design everything first.  
**Not:** Monetize / charge / Premium paywalls in this public roadmap.

**Working principles:**

- Build one app at a time
- The app is the demonstration; **you (the architect) are the product**
- Local-first by default; optional identity/sync later as an architecture skill demo
- MIT educational showcases stay open and useful; private experiments stay private
- SleepCheck is wellness, not a medical device

Every application should demonstrate: product thinking, architecture, project rules, testing, CI/CD, cloud deployment, human oversight, AI-assisted implementation, maintainability, and engineering judgment.

Every app should answer: **What engineering lesson did I learn by building this?**

---

## 3. Current applications

### RetireCheck

- Purpose: retirement planning application; first case study in the series
- Assets: live app, public GitHub, LinkedIn article (Cursor in Action / AI in Action #1), promotional video, MIT-licensed source
- Strategic role: proof that AI-assisted development can support end-to-end delivery
- Live demo for learning — free educational showcase

### SleepCheck

- Live: https://sleepcheck.weidong-shi.com
- Purpose: sleep and wellness companion; second case study
- Strategic role: move the story from “AI helped build an app” to “AI helped transform a vague product idea into a deployed, maintainable product”
- Article should emphasize product thinking, UX, architecture, engineering process, and shared-pattern potential
- **Wellness positioning:** not medical advice; not a diagnostic medical device
- Hub article published; LinkedIn #2 / optional video still open

---

## 4. Long-term technical vision

Do not treat RetireCheck and SleepCheck as isolated applications forever.

Long-term vision: a coherent family of “Check” applications sharing patterns when reuse is real:

```
AI in Action
│
├── RetireCheck
├── SleepCheck
├── FitnessCheck
├── NutritionCheck
├── MindCheck
├── HealthCheck
└── Future domain-specific apps
```

Shared capabilities may eventually include (as engineering learning themes): optional authentication, user profiles, shared UI / design system, shared reporting conventions, AI insight patterns, notifications, analytics, feature flags, capability policies, cloud data sync, deeper local history, accessibility, testing, observability.

**Working principle:** Build one app at a time, but avoid architectural choices that make future integration unnecessarily difficult.

---

## 5. Immediate strategic priority

Do **not** build the full shared platform immediately.

Next immediate work:

- Polish SleepCheck
- Keep architecture docs current
- Optional: SleepCheck LinkedIn / AI in Action #2 video
- Gather user feedback
- Maintain this public roadmap
- Prepare for optional authentication and capability maturity later

Avoid: premature shared multi-tenant architecture, unnecessary microservices, and any commercial packaging language in this repo.

---

## 6. Recommended near-term roadmap

### Phase 1 — Showcase and Validation

- RetireCheck live, SleepCheck live, public content active
- Goals: UI/responsiveness, usability, accessibility, performance, feedback, GitHub docs, LinkedIn #2 optional, identify valued features
- Keep demos free and educational

### Phase 2 — Reusable Foundations

Introduce reusable pieces gradually: design system, layouts, utilities, validation, user model (conceptual), telemetry/observability conventions, configuration and deployment patterns. Do not force a monorepo without clear operational benefit.

### Phase 3 — Optional Authentication

Authentication is an **optional engineering milestone**, not a commercial gate.

Conceptual capability levels: **Local-first → Optional sync (registered) → Advanced local insights**.

- **Local-first:** no account, core experience, temporary/local session, limited history, no cloud sync  
- **Optional sync:** managed IdP, saved history, personalized settings, cross-device access, basic reports  
- **Advanced local insights:** deeper history, AI-assisted insights (non-diagnostic), exports, integrations — as learning themes, not paid tiers  

Use a **managed identity provider** — do not build auth from scratch. Candidates to evaluate later: Microsoft Entra External ID, Auth0, Clerk, Firebase Authentication, Supabase Auth, Amazon Cognito.

Decision criteria: cost of learning/ops, custom domain, social login, data residency, DX, vendor lock-in, mobile support, roles/capability claims.

### Phase 4 — Advanced capabilities / feature flags

Capability policies and feature flags as architecture practice. See [ROADMAP.md](./ROADMAP.md) for checkboxes.

---

## 7. Capability / policy architecture

Do not scatter capability checks throughout the UI.

Use centralized authorization and policy design when accounts exist:

- Identity Service
- Capability / Policy Service
- Feature Flag Service
- Authorization Policy Layer

Conceptual model:

```
User
├── Identity (optional)
├── Capability Level
├── Entitlements / Policies
├── Feature Flags
└── Usage Limits (technical, not commercial)
```

UI may hide/disable features; **backend must enforce** access. See [docs/capability-maturity.md](./docs/capability-maturity.md).

---

## 8–10. Licensing strategy

### Current MIT

MIT allows copy, modify, redistribute, and use — including commercial use by third parties — provided license notice is preserved. That is intentional for an **educational case study**.

**Legal principle:** Code already released under MIT cannot later be revoked from people who obtained it under that license. Future versions may change license; earlier MIT versions remain MIT.

### Public stance

- Showcase apps remain MIT educational case studies  
- Future proprietary work *may* exist separately  
- Do **not** document open-core sales pitches, paid product packaging, or commercial roadmaps in this repo  
- Private experiments stay private  

### Action now

- Do **not** change current licenses impulsively  
- Record what is MIT; keep copyright clear  
- Avoid placing private commercial logic into public MIT repos  
- Consult an attorney before any relicensing  

Practical note (legal review before final adoption):

> The current repository is released under the MIT License as an educational and architectural case study. Future hosted services, proprietary integrations, and other private work may be developed separately and may not be covered by the MIT License.

Details: [docs/licensing-strategy.md](./docs/licensing-strategy.md).

---

## 11. Scope (what this public repo is not)

This public repository does **not** include private commercial strategy.

See [docs/scope.md](./docs/scope.md). Agents must not invent replacement “monetization” docs here.

---

## 12. Privacy and health positioning

SleepCheck touches health and wellness.

Agents **must avoid** presenting it as a diagnostic medical product unless intentionally pursued and legally supported.

Prefer: wellness insights, educational information, personal tracking, habit support, non-diagnostic guidance.

Avoid unsupported claims: detects sleep disorders, diagnoses insomnia, prevents disease, medically validates sleep quality.

Future planning must address: privacy policy, terms, consent, retention, deletion, export, encryption, analytics disclosure, processors, breach response, children’s data, health-data regulations, state privacy laws, HIPAA applicability if any.

**Authentication must not ship without a privacy and data-retention model.** See [docs/privacy-and-security.md](./docs/privacy-and-security.md).

---

## 13. Architecture direction

Keep the platform simple and modular initially.

```
Client Applications
├── RetireCheck UI
├── SleepCheck UI
└── Future App UIs
        │
        ▼
Application APIs
├── Identity and Profile (optional)
├── Domain Services
├── Reporting
├── Capability Policies / Flags
├── Notifications
└── AI Insight Services
        │
        ▼
Data Layer
├── User / Domain / Audit / Usage / Analytics
```

Keep domain logic outside the UI. Explicit boundaries: presentation, application logic, domain logic, persistence, external services, AI services.

**AI-generated output must not directly control critical business logic without validation.**

Diagrams: [diagrams/](./diagrams/). Architecture doc: [docs/platform-architecture.md](./docs/platform-architecture.md).

---

## 14. AI development guardrails

Each *application* repository should eventually include onboarding/rules files such as: `AGENTS.md`, `CONTRIBUTING.md`, `ARCHITECTURE.md`, `SECURITY.md`, `AI_RULES.md`.

Rules should cover:

- Do not place domain logic in UI components
- Do not bypass validation
- Do not remove tests to make builds pass
- Do not expose secrets
- Do not invent APIs
- Do not introduce dependencies without justification
- Do not modify licensing files casually
- Do not weaken authorization
- Do not trust AI output without review
- Preserve architectural boundaries
- Document significant changes
- Write or update tests
- Do not add private commercial strategy to public repos

Workflow:

```
Human Intent → Structured Requirements → Architecture and Rules
→ AI Implementation → Human Review → Automated Testing
→ Security and Quality Checks → Deployment → Feedback
```

---

## 15. GitHub repository strategy

Each public app repository should include: clear README, product overview, screenshots, architecture diagram, live demo link, setup/deployment/test instructions, CI status, roadmap, known limitations, security policy, contribution policy, license, AI-assisted development disclosure, capability notes.

Suggested per-app `/docs`: architecture, product-overview, deployment, security, roadmap, ai-development-rules, licensing notes.

### Repository relationship

```
weidong808/
├── Retirement-Calculator
├── SleepCheck
└── ai-in-action-roadmap      ← this repo (public planning only)
```

Private experiments (if any) stay outside this public tree. The public roadmap describes educational direction without exposing private implementation.

---

## 16. AI in Action content strategy

Every application should become a content package: live app, public/curated GitHub, long-form LinkedIn article, short video, architecture diagram, product journey diagram, lessons-learned post, feature-feedback post, technical deep dive, roadmap update.

Long-term brand: **AI in Action**, not permanently tied to Cursor. Cursor may remain one tool in the series.

Cadence: quality over volume (aim ~2 LinkedIn posts/week when sustainable).

See [docs/content-strategy.md](./docs/content-strategy.md).

---

## 17. SleepCheck article direction

**Suggested title:** AI in Action #2: From an Idea to SleepCheck  

**Possible subtitle:** How AI-assisted engineering helped transform a simple concept into a production-ready wellness application.

Hub article: published. LinkedIn pulse / optional video: still open.

Do not claim SleepCheck invents a new category.

Story arc:

```
Problem → Product Thinking → Requirements → Architecture
→ AI-Assisted Development → Testing → CI/CD → Cloud Deployment
→ User Feedback → Continuous Improvement
```

Key sections: why sleep; defining a useful product; architecture; how AI helped; where AI needed guardrails; testing and deployment; lessons learned; what comes next; shared-pattern implications.

Emphasize: player-first UX, local-first (no accounts today), natural soundscapes, stories/TTS, PWA, streaks, parent brand shared with RetireCheck, wellness disclaimer.

---

## 18. Diagrams to produce

Maintained under [diagrams/](./diagrams/):

1. Product journey  
2. Human and AI responsibilities  
3. Platform evolution  
4. Capability levels  
5. Target architecture  

---

## 19. Immediate next action plan

Produce and maintain **AI in Action Roadmap v1.0** ([ROADMAP.md](./ROADMAP.md)): vision, current state, phases, milestones.

| Horizon | Focus |
|---------|--------|
| **Next 30 days** | Polish SleepCheck; keep architecture current; optional LinkedIn #2; improve READMEs/diagrams; capability maturity docs; gather feedback; identify shared components |
| **60–90 days** | User profile model; local history; evaluate IdPs; optional authentication; cloud persistence; capability policies; feature flags; privacy/retention model; testing & observability |
| **Later** | Deeper insights; cross-app identity patterns; shared reporting; wearables (wellness); multi-app dashboard; additional Check apps |

Milestone files: [milestones/](./milestones/).

---

## 20. Agent instructions

When supporting this project:

1. Work incrementally  
2. Avoid hype  
3. Avoid unnecessary complexity  
4. Make assumptions explicit  
5. Distinguish current state from future vision  
6. Preserve architecture boundaries  
7. Treat licensing and privacy as first-class concerns  
8. Do not recommend building authentication from scratch  
9. Do not assume health-regulatory compliance  
10. Do not claim production readiness without evidence  
11. Prioritize learning and feedback over speculative platforms  
12. Keep public showcase code separate from private experiments  
13. Propose practical deliverables, not only abstract strategy  
14. **Do not push** to remotes unless the human explicitly asks  
15. **Do not put application source code** in `ai-in-action-roadmap`  
16. **Do not add monetization, pricing, Stripe, or private business strategy** to this public repository  

---

## 21. Roadmap Repository (this repo)

Maintain the dedicated public GitHub repository **`ai-in-action-roadmap`**.

**Suggested description:** Public architecture and delivery roadmap for the AI in Action educational case-study series, including RetireCheck, SleepCheck, and future shared technical foundations.

This repository is the architectural and educational source of truth. It contains planning and documentation rather than application source code.

Structure (authoritative):

```
ai-in-action-roadmap/
├── README.md
├── ROADMAP.md
├── VISION.md
├── CONTRIBUTING.md
├── LICENSE
├── AGENTS.md
├── docs/
│   ├── scope.md
│   ├── current-state.md
│   ├── product-strategy.md
│   ├── platform-architecture.md
│   ├── application-roadmap.md
│   ├── authentication-strategy.md
│   ├── capability-maturity.md
│   ├── licensing-strategy.md
│   ├── privacy-and-security.md
│   ├── content-strategy.md
│   └── decision-log.md
├── diagrams/
│   ├── product-journey.md
│   ├── platform-evolution.md
│   ├── capability-levels.md
│   ├── human-ai-responsibilities.md
│   └── target-architecture.md
├── milestones/
│   ├── 30-day-plan.md
│   ├── 60-day-plan.md
│   ├── 90-day-plan.md
│   └── future-backlog.md
├── apps/
│   ├── retirecheck.md
│   ├── sleepcheck.md
│   └── future-apps.md
└── .github/
    ├── ISSUE_TEMPLATE/
    └── PULL_REQUEST_TEMPLATE.md
```

README explains: what AI in Action is; why RetireCheck and SleepCheck exist; philosophy; current status; gradual shared-foundations path; links to live apps, repos, articles, and docs.

ROADMAP.md is the checkbox north star (Phase 1–4 + Future themes). Mark RetireCheck and SleepCheck live as done; SleepCheck hub article done; LinkedIn #2 optional open.

---

## 22. Requested deliverables (checklist for agents)

- [x] AI in Action Roadmap v1.0 (`ROADMAP.md`)
- [x] Capability maturity model (local-first → optional sync → advanced insights)
- [x] Authentication decision framework (optional engineering milestone)
- [x] Public MIT educational licensing stance
- [x] High-level platform architecture
- [x] 30-, 60-, and 90-day implementation plans
- [x] SleepCheck article outline (in content strategy + apps/sleepcheck)
- [x] Diagram specifications (Mermaid in `diagrams/`)
- [x] Top risks and mitigation (in decision-log / product-strategy)
- [x] Complete initial content for this public roadmap repository
- [x] Explicit public-scope boundary (`docs/scope.md`) — no private commercial strategy here

Output should remain practical, phased, technically credible, and suitable for a Senior Technology Architect building an educational portfolio.
