# Authentication Strategy

## Principle

**Optional identity as an engineering learning milestone.** Local-first users can try the full core experience without friction. Registered users unlock persistence and personalization when that architecture is worth demonstrating. Advanced insights are a later capability layer — not a commercial gate.

Do **not** build authentication from scratch. Prefer a managed identity provider.

## Conceptual user journey

```
Local-first → Optional sync (registered) → Advanced insights (later)
```

| Level | Auth | Persistence | Goal |
|-------|------|-------------|------|
| Local-first | None | Local / temporary | Try everything useful without friction |
| Optional sync | Managed IdP | Cloud sync + history | Return users, cross-device; architecture demo |
| Advanced insights | Same identity + policies | Extended data + insights | Deeper learning themes after validation |

Leave capability **hooks** early; do not invent commercial packaging in the auth phase.

## Decision framework (evaluate before choosing)

Score candidates against:

1. Ops and learning cost at expected scale  
2. Custom domain / branded login  
3. Social login (Google, GitHub, Apple, Microsoft) + email  
4. Data residency / region options  
5. Developer experience and Next.js fit  
6. Vendor lock-in and exit path  
7. Future mobile support  
8. Roles, claims, and capability-policy integration  
9. Compliance posture relevant to stored data (not assumed HIPAA)

### Candidates to evaluate later

| Provider | Notes |
|----------|--------|
| Microsoft Entra External ID | Strong if Azure-centric |
| Auth0 | Mature; watch complexity/cost |
| Clerk | Fast DX for Next.js; evaluate lock-in |
| Firebase Authentication | Familiar; Google ecosystem |
| Supabase Auth | Good if Postgres already chosen |
| Amazon Cognito | AWS-centric; more ops complexity |

**Decision status:** Not selected. Record the choice in [decision-log.md](./decision-log.md) when made.

## Prerequisites before shipping auth

- [ ] Privacy policy and terms covering account data  
- [ ] Data retention and deletion model  
- [ ] Account export approach (at least planned)  
- [ ] Encryption in transit (and at rest for stored PII)  
- [ ] Clear Local-first vs Optional-sync capability matrix  
- [ ] Capability policy design (even if advanced features are empty)  
- [ ] No secrets in client bundles  

## Recommended rollout

1. **Local history / sessions** (no login) — reduce data loss for local-first users  
2. **IdP spike** — one app, limited surface  
3. **Optional registered accounts** on SleepCheck or RetireCheck (pick based on feedback)  
4. **Cloud sync** for saved settings/history  
5. **Shared identity patterns** across apps only after one app is stable  
6. **Advanced capability policies** via feature flags  
7. Keep the public story educational — see [scope.md](./scope.md)  

## Social providers (target set)

Evaluate enabling: Google, Microsoft, Apple, GitHub, and email magic-link or OTP as needed. Ship the minimum set that covers primary audiences.

## Anti-patterns

- Rolling a custom password database “just for now”  
- Treating accounts as a commercial gate in public docs  
- Storing health-adjacent journal content without retention/consent design  
- Hard-coding role checks in dozens of UI components  

## Related

- [capability-maturity.md](./capability-maturity.md)
- [privacy-and-security.md](./privacy-and-security.md)
- [scope.md](./scope.md)
- [../diagrams/capability-levels.md](../diagrams/capability-levels.md)
