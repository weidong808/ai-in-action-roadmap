# Application Roadmap

## Portfolio shape

```
AI in Action (educational portfolio)
│
├── RetireCheck                         ← live
├── SleepCheck                          ← live
├── AI Production Readiness Advisor     ← App #3 (local MVP; deploy TBD)
├── HabitCheck / other Check apps       ← backlog candidates
└── Future domain apps                  ← backlog
```

**Rule:** Build one useful application at a time. New apps enter active work only when prior apps are polished enough and capacity allows.

## Active applications

| App | Status | Primary lesson |
|-----|--------|----------------|
| [RetireCheck](../apps/retirecheck.md) | Live | End-to-end AI-assisted delivery with serious domain logic |
| [SleepCheck](../apps/sleepcheck.md) | Live | Idea → product thinking → maintainable wellness PWA |
| [AI Production Readiness Advisor](../apps/ai-production-readiness-advisor.md) | Live (Vercel; custom DNS pending) | Deterministic readiness gates + advisory LLM narrative / evals |

## Near-term app work (not new domains)

1. SleepCheck polish and documentation  
2. SleepCheck LinkedIn / optional AI in Action #2 video  
3. RetireCheck README / architecture improvements as needed  
4. Local history / sessions (especially SleepCheck) before optional auth  
5. Auth evaluation shared across apps (engineering learning)  

## Future applications

See [../apps/future-apps.md](../apps/future-apps.md). Candidate domains are placeholders for storytelling and technical planning — not commitments.

Admission criteria for starting a new Check app:

- Clear user problem and narrow v1 scope  
- Fits “demonstration + engineering lesson” content model  
- Does not require regulated medical claims for v1  
- Reuses existing patterns without blocking independent ship  
- Owner capacity after Phase 1 polish and content obligations  

## Platform coupling policy

- Apps may share **brand**, **docs conventions**, and eventually **optional identity patterns**  
- Apps must remain independently shippable until a deliberate shared-foundations cutover  
- Cross-app features (dashboard, unified insights) wait on shared identity  

## Related

- [../ROADMAP.md](../ROADMAP.md)
- [../apps/future-apps.md](../apps/future-apps.md)
- [../diagrams/platform-evolution.md](../diagrams/platform-evolution.md)
- [scope.md](./scope.md)
