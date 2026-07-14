# Vision — AI in Action

## One sentence

Build practical AI-assisted applications one at a time, document the engineering lessons, and share them as production-ready educational case studies — without designing everything first.

## Why this exists

**AI in Action** demonstrates how a Senior Technology Architect uses AI-assisted development to deliver production software end to end: product thinking, architecture, testing, CI/CD, cloud, feedback, and continuous improvement.

The series is a **public educational / showcase portfolio**. Audience: engineers, architects, hiring managers, and peers. Purpose: demonstrate engineering judgment, architecture, AI-assisted delivery, CI/CD, and cloud deploy.

The series is not about claiming AI replaces engineers. The central message is:

> **AI changes where engineers spend their time.**

Engineers who thrive will be strong architects of both software systems and AI behavior — directing, reviewing, and remaining accountable.

## What the product really is

| Surface | Role |
|---------|------|
| Each Check app | Live educational demonstration |
| Engineering process | The real lesson |
| Weidong Shi (architect) | The credibility people evaluate |

Every app should answer: **What engineering lesson did building this teach?**

Unusual combination to keep visible in public work:

- Senior Technology Architect
- Cloud & Azure experience
- Research background
- AI enthusiast building real applications
- Writing about engineering, not hype

## Operating loop

```
Build → Validate → Improve → Document → Share
```

| Step | Meaning |
|------|---------|
| **Build** | Ship one useful app |
| **Validate** | Real usage and feedback |
| **Improve** | Polish, a11y, performance, tests |
| **Document** | Architecture notes, READMEs, decision log |
| **Share** | Articles, diagrams, LinkedIn, open MIT showcases |

Anti-patterns: big-bang platform design, auth before privacy model, scattering capability checks in the UI, inventing private business strategy in this public repository.

## Portfolio north star (long term)

A coherent family of domain “Check” applications that share patterns when reuse is real:

```
AI in Action
├── RetireCheck
├── SleepCheck
├── FitnessCheck
├── NutritionCheck
├── MindCheck
├── HealthCheck
└── Future domain-specific apps
```

Shared technical themes over time (when reuse is real), framed as **engineering learning**:

- Optional authentication and profiles (architecture skill demo)
- Design system / shared UI patterns
- Reporting and analytics conventions
- AI insight patterns (with human validation of critical outputs)
- Notifications, feature flags, capability policies
- Deeper local history, accessibility, testing, observability
- Clear MIT educational licensing; private experiments stay private

## Constraints that do not change casually

1. **One app at a time** — avoid architectural choices that block integration later, but do not build the full shared stack now.
2. **Local-first by default** — optional accounts/cloud sync come later as an engineering milestone, with a privacy model first.
3. **MIT educational showcases** — apps stay free learning demos; future proprietary work may exist separately without turning this repo into a commercial roadmap.
4. **Wellness, not medicine** — SleepCheck (and similar apps) use non-diagnostic language unless a regulated path is intentionally pursued with legal support.
5. **Human accountability** — AI assists implementation; humans own product direction, architecture, security, and review.
6. **Public vs private** — this repository does not document private commercial strategy. See [docs/scope.md](./docs/scope.md).

## Success measures (practical)

Near term:

- Live apps people can use and learn from
- Credible public case studies and diagrams
- Feedback that informs which features matter
- Clear roadmap that prevents thrash

Later:

- Optional accounts that people actually create (if pursued)
- Shared patterns that reduce delivery cost across apps
- Stronger testing, accessibility, and observability
- A coherent multi-app engineering story that matches reality

## Related

- Checklist: [ROADMAP.md](./ROADMAP.md)
- Scope: [docs/scope.md](./docs/scope.md)
- Agent handoff: [AGENTS.md](./AGENTS.md)
- Product strategy: [docs/product-strategy.md](./docs/product-strategy.md)
