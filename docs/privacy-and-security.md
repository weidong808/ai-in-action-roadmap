# Privacy and Security

## Positioning (non-negotiable for SleepCheck)

SleepCheck is a **wellness** companion: educational information, personal tracking, and habit support.

It is **not** a diagnostic medical product unless that path is intentionally pursued with legal and regulatory support.

### Preferred language

- Wellness insights  
- Educational information  
- Personal tracking  
- Habit support  
- Non-diagnostic guidance  

### Avoid unsupported claims

- Detects sleep disorders  
- Diagnoses insomnia  
- Prevents disease  
- Medically validates sleep quality  

RetireCheck similarly must avoid implying personalized financial, tax, or legal advice unless explicitly scoped and reviewed.

## Privacy program (build before auth)

Before shipping accounts or cloud sync, plan:

| Topic | Status target |
|-------|----------------|
| Privacy policy | Required before auth |
| Terms of use | Required before auth |
| Consent for stored data | Required |
| Data retention schedule | Required |
| Account deletion | Required |
| Data export | Planned at minimum |
| Encryption in transit | Required |
| Encryption at rest (PII) | Required for cloud stores |
| Analytics disclosure | Required if analytics on |
| Third-party processors list | Required |
| Breach response outline | Required before sensitive data |
| Children’s data | Decide age gates; default conservative |
| Health-data / HIPAA applicability | **Do not assume**; evaluate with counsel if claims or covered entities appear |
| State privacy laws (e.g. CCPA-like) | Track as user base grows |

**Rule:** Authentication should not be added without a privacy and data-retention model.

## Current-state posture (today)

- SleepCheck: local-first preferences; no accounts  
- RetireCheck: calculation-focused; treat any future saved scenarios as sensitive personal financial context  
- Minimize collection until sync is intentional  

## Security engineering expectations

- No secrets in client code or public repos  
- Dependency and CI hygiene on app repos  
- Least privilege for cloud credentials  
- Authorization enforced server-side when accounts exist  
- Do not weaken authz to “make the demo work”  
- AI tools must not invent security controls that are not implemented  

## AI and sensitive data

- Do not send unnecessary PII to third-party AI APIs  
- Document any model providers used for product features  
- Human review for security-sensitive changes  

## Related

- [authentication-strategy.md](./authentication-strategy.md)
- [scope.md](./scope.md)
- [../AGENTS.md](../AGENTS.md)
- [decision-log.md](./decision-log.md)
