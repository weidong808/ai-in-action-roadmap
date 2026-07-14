# Diagram — Capability Levels

Conceptual capability model. Today’s live apps are primarily **local-first**.

```mermaid
flowchart TB
  subgraph LocalFirst[Local-first]
    G1[Try core features]
    G2[No sign-up]
    G3[Limited local history]
  end

  subgraph OptionalSync[Optional sync]
    F1[Saved history]
    F2[Cloud sync]
    F3[Basic reports]
    F4[Personal settings]
  end

  subgraph AdvancedInsights[Advanced local insights]
    P1[Deeper insights]
    P2[AI-assisted recommendations]
    P3[Exports]
    P4[Integrations]
    P5[Extended history]
  end

  LocalFirst --> OptionalSync --> AdvancedInsights
```

## Notes

- Optional identity is an engineering learning milestone, not a commercial gate.  
- Advanced insights are learning themes after feedback shows they matter.  
- Detailed matrices: [../docs/capability-maturity.md](../docs/capability-maturity.md).

## Related

- [../docs/authentication-strategy.md](../docs/authentication-strategy.md)
- [../docs/scope.md](../docs/scope.md)
