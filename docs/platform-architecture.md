# Platform Architecture

## Intent

Describe a **target logical architecture** for shared AI in Action technical foundations. Today’s apps are mostly independent. Shared services appear when reuse justifies them.

This is planning documentation — not a claim that shared services already exist. Framing: educational portfolio and engineering learning, not a commercial platform pitch.

## Current architecture (today)

```
RetireCheck (independent deployable)
├── Next.js UI
└── ASP.NET Core API + C# domain

SleepCheck (independent deployable)
└── Next.js / PWA (local-first; no accounts)

Hub (weidong-shi.com)
└── Case studies, articles, links
```

No shared identity. No shared capability-policy service. No cross-app data plane.

## Target logical architecture (future)

```
Client Applications
│
├── RetireCheck UI
├── SleepCheck UI
└── Future App UIs
        │
        ▼
Application APIs / BFF as needed
        │
├── Identity and Profile (optional)
├── Domain Services (per app)
├── Reporting
├── Capability Policies + Feature Flags
├── Notifications
└── AI Insight Services
        │
        ▼
Data Layer
├── User data
├── Domain data
├── Audit data
├── Usage data
└── Analytics
```

See Mermaid: [../diagrams/target-architecture.md](../diagrams/target-architecture.md).

## Design principles

1. **Domain logic outside the UI** — calculators, rules, and critical decisions live in testable layers.
2. **Explicit boundaries** — presentation / application / domain / persistence / external / AI.
3. **Centralized capability policies** — no scattered checks; backend enforces when accounts exist.
4. **Managed identity** — do not build authentication from scratch.
5. **AI outputs are advisory** — never drive critical business logic without validation.
6. **Incremental extraction** — shared packages/services only after duplication is proven.
7. **Deploy independence** — prefer separate app deploys until a monorepo clearly helps.

## Shared capabilities (order of introduction)

| Capability | When | Notes |
|------------|------|-------|
| Conventions (telemetry, config, docs) | Phase 2 | Low risk |
| Design tokens / UI primitives | Phase 2 | Extract when both apps share patterns |
| User model (schema) | Phase 2–3 | Conceptual before implementation |
| Optional authentication | Phase 3 | After privacy/retention model |
| Cloud history / sync | Phase 3 | Optional registered users |
| Feature flags + capability policies | Phase 4 | Engineering maturity |
| Shared AI insight patterns | Later | Human-validated outputs |
| Cross-app dashboard | Later | Needs shared identity |
| Testing, a11y, observability hardening | Ongoing | Portfolio-quality engineering |

## Repository mapping

| Concern | Repository type |
|---------|-----------------|
| Planning / ADRs | `ai-in-action-roadmap` (this repo) |
| Showcase apps | Public MIT educational app repos |
| Private experiments | Out of scope for this public repo |

## Non-goals (near term)

- Premature microservices mesh
- Homegrown IdP
- Forcing both apps into one codebase immediately
- Claiming HIPAA or medical-device readiness
- Documenting private commercial systems here

## Related

- [authentication-strategy.md](./authentication-strategy.md)
- [capability-maturity.md](./capability-maturity.md)
- [scope.md](./scope.md)
- [../diagrams/platform-evolution.md](../diagrams/platform-evolution.md)
