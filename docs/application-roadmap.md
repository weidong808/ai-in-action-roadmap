# Application Roadmap

## Portfolio shape

```
AI in Action (educational portfolio)
│
├── RetireCheck                         ← live
├── SleepCheck                          ← live
├── AI Production Readiness Advisor     ← App #3 live (readiness.weidong-shi.com)
├── HabitCheck                          ← App #4 P0–P7 code complete (deploy pending)
└── Future Check / domain apps          ← backlog
```

**Rule:** Build one useful application at a time. New apps enter active work only when prior apps are polished enough and capacity allows.

## Active applications

| App | Status | Primary lesson |
|-----|--------|----------------|
| [RetireCheck](../apps/retirecheck.md) | Live | End-to-end AI-assisted delivery with serious domain logic |
| [SleepCheck](../apps/sleepcheck.md) | Live | Idea → product thinking → maintainable wellness PWA |
| [AI Production Readiness Advisor](../apps/ai-production-readiness-advisor.md) | Live | Deterministic readiness gates + advisory LLM narrative / evals |
| [HabitCheck](../apps/habitcheck.md) | P0–P7 code complete | Weekly recovery + AI-forward coach OS · [repo](https://github.com/weidong808/HabitCheck) · public deploy pending |

## Near-term app work

1. HabitCheck public ship — Vercel + DNS + `OPENAI_API_KEY` + hub case study  
2. LinkedIn cadence for live apps (Readiness / HabitCheck)  
3. Extract shared tracking only after HabitCheck validates reuse  
4. Auth evaluation across apps remains a later engineering learning milestone

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
