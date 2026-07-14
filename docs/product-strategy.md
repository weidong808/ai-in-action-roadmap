# Product Strategy

## Thesis

Ship one credible application at a time. Use each app as a public demonstration of AI-assisted engineering. Document lessons and share case studies. Evolve shared capabilities only when reuse is real.

## Brand

- **Series brand:** AI in Action (not permanently “Cursor in Action”)
- **App family:** “Check” applications under optional shared technical foundations
- **Personal brand:** Senior Technology Architect who builds and writes about real systems
- **Audience:** engineers, architects, hiring managers, peers

## Strategic sequence

```
Build → Validate → Improve → Document → Share
```

| Phase | Focus | Success signal |
|-------|-------|----------------|
| Showcase | Live apps + articles | Credibility, traffic, feedback |
| Foundations | Shared patterns without forcing platform | Less duplication, clearer conventions |
| Optional identity | Accounts + sync + privacy model | People create accounts and return (if pursued) |
| Advanced capabilities | Flags + deeper insights + testing/a11y/observability | Clear engineering maturity |
| Shared foundations | Cross-app patterns, reporting, AI insight conventions | Multi-app coherence that matches reality |

## What we optimize for now

1. **Credibility** — polished apps and honest case studies  
2. **Learning** — which features matter  
3. **Clarity** — this roadmap as north star  
4. **Optionality** — architecture that allows private experiments later without documenting them here  

## What we defer

- Full multi-tenant SaaS platform
- Building auth from scratch
- Health claims or regulated medical product path (unless intentionally pursued later)
- Monorepo / microservices without operational need
- Private commercial strategy in this public repo (see [scope.md](./scope.md))

## Biggest portfolio asset

Not RetireCheck or SleepCheck alone — **the architect**. Each release should teach an engineering lesson people can follow.

## Risks and mitigations

| Risk | Mitigation |
|------|------------|
| Overbuilding the platform early | Phase checkboxes; extract only proven shared pieces |
| Scope creep into private commercial docs | Keep [scope.md](./scope.md); agents refuse monetization content here |
| MIT vs private-work confusion | Clear educational licensing; private work stays private |
| Wellness → medical mispositioning | Explicit non-diagnostic language; legal review before health claims |
| Content without substance | Always pair articles with live apps and architecture docs |
| Scope creep across too many Check apps | One app at a time; future apps stay in backlog until capacity |

## Related

- [application-roadmap.md](./application-roadmap.md)
- [capability-maturity.md](./capability-maturity.md)
- [scope.md](./scope.md)
- [../milestones/30-day-plan.md](../milestones/30-day-plan.md)
