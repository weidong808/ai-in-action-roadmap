# Capability Maturity — Local-first → Optional Sync → Advanced Insights

Conceptual capability model for the AI in Action apps. **Not all rows are implemented today.** Today both apps are effectively **local-first**.

Use this matrix to design feature flags and policies later. UI may hide features; **enforcement belongs in policy/backend** when accounts exist.

This is an **engineering maturity** model for educational showcases — not a commercial packaging matrix.

## Level definitions

| Level | Description |
|-------|-------------|
| **Local-first** | No login. Try core experience. Local or temporary session. Limited history. No cloud sync. |
| **Optional sync** | Optional account via managed IdP. Saved history, settings, cross-device sync, basic reports. Architecture skill demo. |
| **Advanced local insights** | Deeper history, AI-assisted insights (non-diagnostic), exports, integrations. Learning themes — not paid gates. |

---

## SleepCheck (conceptual)

| Capability | Local-first | Optional sync | Advanced insights |
|------------|:-----------:|:-------------:|:-----------------:|
| Browse / play soundscapes | ✓ | ✓ | ✓ |
| Bedtime stories / narrator voices | ✓ | ✓ | ✓ |
| Breathing / wind-down flows | ✓ | ✓ | ✓ |
| Sleep timer | ✓ | ✓ | ✓ |
| Streaks (local) | ✓ | ✓ | ✓ |
| PWA install / offline-friendly core | ✓ | ✓ | ✓ |
| Local preferences | ✓ | ✓ | ✓ |
| Local session / mix history (limited) | ✓ | ✓ | ✓ |
| Cloud sync of preferences & history | — | ✓ | ✓ |
| Cross-device continue | — | ✓ | ✓ |
| Basic weekly summary (non-diagnostic) | — | ✓ | ✓ |
| Personalized goals (simple) | — | ✓ | ✓ |
| AI sleep insights / recommendations | — | limited / — | ✓ |
| Longitudinal trends (weekly/monthly) | — | basic | ✓ |
| Sleep journal analysis | — | — | ✓ |
| Wearable integrations | — | — | ✓ |
| Downloadable / shareable detailed reports | — | — | ✓ |
| Smart alerts / advanced correlations | — | — | ✓ |
| Family profiles | — | — | ✓ |
| Cross-app wellness insights | — | — | ✓ |

**Positioning reminder:** All SleepCheck insights are wellness / educational / habit-support — **not** diagnosis, disorder detection, or medical validation.

---

## RetireCheck (conceptual)

| Capability | Local-first | Optional sync | Advanced insights |
|------------|:-----------:|:-------------:|:-----------------:|
| Core retirement wizard / calculator | ✓ | ✓ | ✓ |
| Monte Carlo / projection charts | ✓ | ✓ | ✓ |
| SSA FRA / core modeling features | ✓ | ✓ | ✓ |
| Shareable results (link/export light) | ✓ | ✓ | ✓ |
| Local save of last scenario | ✓ | ✓ | ✓ |
| Cloud-saved scenarios | — | ✓ | ✓ |
| Scenario history / compare (basic) | — | ✓ | ✓ |
| Cross-device access | — | ✓ | ✓ |
| Basic saved reports | — | ✓ | ✓ |
| Advanced scenario packs / stress tests | — | limited | ✓ |
| AI planning insights / explanations | — | limited / — | ✓ |
| Detailed export packs | — | — | ✓ |
| Household / multi-profile planning | — | — | ✓ |

RetireCheck remains an educational / planning tool — not personalized financial advice unless explicitly productized with appropriate disclaimers and review.

---

## Policy design notes

```
User
├── Identity (optional)
├── Capability Level
├── Entitlements / Policies
├── Feature Flags
└── Usage Limits (technical)
```

- Prefer named capabilities (`sleep.insights.ai`, `retire.scenarios.cloud`) over string compares in UI  
- Feature flags allow gradual rollout without redeploying policy forever  
- Advanced rows are **hypotheses** until feedback shows they matter for learning and usefulness  

## Related

- [authentication-strategy.md](./authentication-strategy.md)
- [scope.md](./scope.md)
- [../diagrams/capability-levels.md](../diagrams/capability-levels.md)
