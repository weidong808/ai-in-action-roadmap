# AI in Action — Public Roadmap

Public architecture and delivery roadmap for the **AI in Action** series — production-ready personal case studies including RetireCheck, SleepCheck, and optional shared technical foundations.

This repository is documentation only. It is the educational and architectural source of truth. Application source code lives in separate repositories.

| | |
|---|---|
| **Owner** | Weidong Shi — Senior Technology Architect |
| **Hub** | [weidong-shi.com](https://weidong-shi.com) |
| **Roadmap repo** | [weidong808/ai-in-action-roadmap](https://github.com/weidong808/ai-in-action-roadmap) |

---

## What is AI in Action?

**AI in Action** is a public educational series that shows how experienced engineers and architects can use AI-assisted development to ship real, production-ready applications — not demos or hype.

Each application is a case study. The deeper product is the engineering process: product thinking, architecture, testing, CI/CD, cloud deployment, and human judgment.

**Audience:** engineers, architects, hiring managers, and peers evaluating engineering credibility.

Apps remain free educational showcases under MIT. Live demos exist so others can learn from working software.

## Guiding philosophy

**Build → Validate → Improve → Document → Share**

Not:

**Design everything first.**

Working principles:

- Build one useful application at a time
- Work incrementally; avoid premature platform complexity
- The app is the demonstration; the architect is the product
- AI changes where engineers spend their time — it does not remove accountability
- Prefer local-first experiences; add optional identity/sync only as an engineering learning milestone
- Keep MIT educational case studies open and useful
- SleepCheck is a wellness companion, not a medical device

See [VISION.md](./VISION.md) for the full statement. Scope boundary: [docs/scope.md](./docs/scope.md).

## Live applications

| App | Status | Live URL | Source |
|-----|--------|----------|--------|
| **RetireCheck** | Live | [retirecheck.weidong-shi.com](https://retirecheck.weidong-shi.com) | [Retirement-Calculator](https://github.com/weidong808/Retirement-Calculator) |
| **SleepCheck** | Live | [sleepcheck.weidong-shi.com](https://sleepcheck.weidong-shi.com) | [SleepCheck](https://github.com/weidong808/SleepCheck) |
| **AI Production Readiness Advisor** | Live (Vercel) | [ai-production-readiness-advisor.vercel.app](https://ai-production-readiness-advisor.vercel.app) · `readiness.weidong-shi.com` (DNS pending) | [ai-production-readiness-advisor](https://github.com/weidong808/ai-production-readiness-advisor) |
| **Personal hub** | Live | [weidong-shi.com](https://weidong-shi.com) | Personal site (case studies & articles) |

App notes: [apps/retirecheck.md](./apps/retirecheck.md) · [apps/sleepcheck.md](./apps/sleepcheck.md) · [apps/ai-production-readiness-advisor.md](./apps/ai-production-readiness-advisor.md) (#3 engineering showcase) · [apps/habitcheck.md](./apps/habitcheck.md) (Better Living candidate) · [apps/future-apps.md](./apps/future-apps.md)

## Current state (summary)

- RetireCheck and SleepCheck are live educational demos
- AI in Action content series is active (RetireCheck and SleepCheck hub + LinkedIn articles published; short videos live)
- No authentication yet; apps are local-first
- Shared technical capabilities are planned as learning milestones, not a product platform pitch
- Early feedback stage

Full checklist: [ROADMAP.md](./ROADMAP.md) · Current snapshot: [docs/current-state.md](./docs/current-state.md)

## Path toward shared technical foundations

Do not treat RetireCheck and SleepCheck as isolated forever — but do not force a shared platform before reuse is real.

```
AI in Action (educational portfolio)
│
├── RetireCheck
├── SleepCheck
├── Future Check apps (optional)
└── Shared capabilities when reuse is proven
    (UI patterns, optional identity/sync, reporting conventions, AI insight patterns)
```

Sequence: polish and validate apps → document and share → extract shared patterns → optional identity as an architecture skill demo → deeper local insights and observability.

## Repository map

```
weidong808/
├── Retirement-Calculator     # RetireCheck (public MIT educational showcase)
├── SleepCheck                # SleepCheck (public MIT educational showcase)
└── ai-in-action-roadmap      # this repo — public planning & education only
```

Private experiments may exist elsewhere. They are out of scope for this public repository. See [docs/scope.md](./docs/scope.md) and [docs/licensing-strategy.md](./docs/licensing-strategy.md).

## Documentation index

| Document | Purpose |
|----------|---------|
| [ROADMAP.md](./ROADMAP.md) | Phased checklist (v1.0) |
| [VISION.md](./VISION.md) | North-star vision and principles |
| [AGENTS.md](./AGENTS.md) | Handoff brief for AI agents |
| [CONTRIBUTING.md](./CONTRIBUTING.md) | How to contribute to this roadmap |
| [docs/scope.md](./docs/scope.md) | Public education/showcase boundary |
| [docs/current-state.md](./docs/current-state.md) | What exists today |
| [docs/product-strategy.md](./docs/product-strategy.md) | Product / portfolio direction |
| [docs/platform-architecture.md](./docs/platform-architecture.md) | Target architecture |
| [docs/application-roadmap.md](./docs/application-roadmap.md) | App portfolio plan |
| [docs/authentication-strategy.md](./docs/authentication-strategy.md) | Optional identity as engineering milestone |
| [docs/capability-maturity.md](./docs/capability-maturity.md) | Local-first → optional sync → advanced insights |
| [docs/licensing-strategy.md](./docs/licensing-strategy.md) | MIT educational licensing |
| [docs/privacy-and-security.md](./docs/privacy-and-security.md) | Privacy, wellness positioning |
| [docs/content-strategy.md](./docs/content-strategy.md) | Articles, diagrams, LinkedIn |
| [docs/decision-log.md](./docs/decision-log.md) | Recorded decisions |

### Diagrams

- [Product journey](./diagrams/product-journey.md)
- [Platform evolution](./diagrams/platform-evolution.md)
- [Capability levels](./diagrams/capability-levels.md)
- [Human vs AI responsibilities](./diagrams/human-ai-responsibilities.md)
- [Target architecture](./diagrams/target-architecture.md)

### Milestones

- [30-day plan](./milestones/30-day-plan.md)
- [60-day plan](./milestones/60-day-plan.md)
- [90-day plan](./milestones/90-day-plan.md)
- [Future backlog](./milestones/future-backlog.md)

## License

Documentation in this repository is released under the [MIT License](./LICENSE).

Application repositories remain separately licensed (currently MIT educational showcases). Future proprietary work may exist separately and is not covered by those showcase licenses. See [docs/licensing-strategy.md](./docs/licensing-strategy.md).
