# Diagram — Target Architecture

Logical target for shared AI in Action technical foundations. **Not** a claim of current deployment topology.

```mermaid
flowchart TB
  subgraph Clients[Client Applications]
    RC[RetireCheck UI]
    SC[SleepCheck UI]
    FC[Future App UIs]
  end

  subgraph APIs[Application APIs]
    ID[Identity and Profile]
    Dom[Domain Services]
    Rep[Reporting]
    Cap[Capability Policies and Flags]
    N[Notifications]
    AI[AI Insight Services]
  end

  subgraph Data[Data Layer]
    UD[User Data]
    DD[Domain Data]
    AD[Audit Data]
    UsD[Usage Data]
    AnD[Analytics]
  end

  Clients --> APIs
  APIs --> Data
```

## Boundary rules

| Layer | Owns | Must not |
|-------|------|----------|
| UI | Presentation, local UX state | Critical domain rules, capability enforcement |
| Domain services | Business rules, calculations | Silent policy bypass |
| Capability policies | Access decisions | Hard-coded only in components |
| AI insights | Assistive outputs | Unvalidated control of critical logic |
| Data | Persistence, retention | Silent PII sprawl |

## Related

- [../docs/platform-architecture.md](../docs/platform-architecture.md)
- [platform-evolution.md](./platform-evolution.md)
- [../docs/scope.md](../docs/scope.md)
