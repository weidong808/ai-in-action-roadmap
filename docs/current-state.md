# Current State

**As of:** July 2026  
**Owner:** Weidong Shi — Senior Technology Architect

## What exists today

| Asset | Status | URL / location |
|-------|--------|----------------|
| RetireCheck | Live educational demo | https://retirecheck.weidong-shi.com |
| RetireCheck source | Public MIT | https://github.com/weidong808/Retirement-Calculator |
| SleepCheck | Live educational demo | https://sleepcheck.weidong-shi.com |
| SleepCheck source | Public MIT | https://github.com/weidong808/SleepCheck |
| Personal hub | Live | https://weidong-shi.com |
| AI in Action #1 (RetireCheck) | Published | Hub articles + LinkedIn (“Cursor in Action”) |
| AI in Action #2 (SleepCheck) | Hub published; LinkedIn / video optional | https://weidong-shi.com/articles/ai-in-action-sleepcheck |
| This roadmap repo | Active | https://github.com/weidong808/ai-in-action-roadmap |

## What is intentionally not built yet

- Shared authentication / SSO across apps
- Cloud user accounts or cross-device sync
- Feature flags / capability-policy enforcement
- Shared design-system package extracted from both apps
- Multi-app dashboard
- Private experiments (out of scope for this public repo)

## Product posture by app

### RetireCheck

- Production retirement planning calculator (wizard, Monte Carlo, SSA-related modeling, shareable results)
- Stack direction: Next.js frontend + ASP.NET Core API + C# domain engine
- Role: first end-to-end AI-assisted delivery case study
- Live demo for learning

### SleepCheck

- Player-first sleep / wellness companion: soundscapes, stories/TTS, breathing, streaks, PWA
- Local-first preferences today — no accounts, no tracking-as-product
- Role: second case study; product-thinking and maintainable delivery narrative
- Positioning: **wellness, not medical device**
- Live demo for learning

## Feedback and validation stage

Early. Priorities are polish, documentation, content, and learning which features people actually use.

## Source of truth

Checkboxes and phases: [../ROADMAP.md](../ROADMAP.md)  
Philosophy: [../VISION.md](../VISION.md)  
Public boundary: [scope.md](./scope.md)
