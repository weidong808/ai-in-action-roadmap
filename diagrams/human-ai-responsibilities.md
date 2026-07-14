# Diagram — Human and AI Responsibilities

AI changes where engineers spend time. Accountability stays human.

```mermaid
flowchart LR
  subgraph Human
    H1[Product direction]
    H2[Architecture]
    H3[Trade-offs]
    H4[Security]
    H5[Validation]
    H6[Review]
    H7[Accountability]
  end

  subgraph AI
    A1[Scaffolding]
    A2[Code generation]
    A3[Refactoring]
    A4[Test generation]
    A5[Documentation]
    A6[Debugging assistance]
    A7[UI exploration]
  end

  Human -->|directs and reviews| AI
  AI -->|accelerates| Human
```

## Workflow

```mermaid
flowchart TD
  I[Human Intent] --> R[Structured Requirements]
  R --> AR[Architecture and Rules]
  AR --> IMP[AI Implementation]
  IMP --> REV[Human Review]
  REV --> T[Automated Testing]
  T --> Q[Security and Quality Checks]
  Q --> D[Deployment]
  D --> F[Feedback]
  F --> I
```

## Guardrails (short)

- Do not trust AI output without review  
- Do not remove tests to make builds pass  
- Do not place domain logic in UI because generation was convenient  
- Do not invent APIs or weaken authorization  

Full agent brief: [../AGENTS.md](../AGENTS.md).
