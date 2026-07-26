# Codebase Maintenance Guide

**Updated:** July 26, 2026

This page is the cross-repository handoff for maintaining the public AI in
Action applications. Product and architecture decisions remain in each
application repository.

## Repositories and verification

| Repository | Primary verification | Current focus |
|---|---|---|
| RetireCheck | Frontend: `npm run lint`, `npm run typecheck`, `npm run build`; backend: `dotnet test` | Financial-domain regression coverage, accessibility, API/client contract generation |
| SleepCheck | `npm run lint`, `npm run typecheck`, `npm test`, `npm run build` | Audio/PWA regression coverage, accessibility, browser compatibility |
| AI Production Readiness Advisor | `npm run lint`, `npm run typecheck`, `npm test`, `npm run build` | Evaluation depth, corpus freshness, narrative safety, operational telemetry |
| HabitCheck | `npm run lint`, `npm run typecheck`, `npm test`, `npm run build` | IndexedDB migration safety, accessibility, recovery-loop feedback |
| AI in Action roadmap | Review internal links, dates, app status, and public/private scope before merge | Keep cross-repository status and decisions aligned |

Use the lockfile-preserving install command (`npm ci`) for verification. Do not
mix dependency upgrades with unrelated features.

## Maintenance rules

1. Keep domain logic out of UI components.
2. Add or update tests when changing scoring, financial calculations, tracking,
   storage migrations, privacy gates, or date boundaries.
3. Treat all AI input as untrusted and potentially sensitive.
4. Keep deterministic decisions outside the model.
5. Preserve the local-first boundary in SleepCheck and HabitCheck unless a
   documented product decision changes it.
6. Update the application README, architecture notes, and this page when a
   release changes commands, routes, deployment, or status.
7. Prefer small, independently verifiable pull requests.

## Recommended next sequence

1. Add browser-level smoke tests for each live application's critical path.
2. Add accessibility checks to CI.
3. Expand SleepCheck tests around storage, streaks, and timer behavior.
4. Expand RetireCheck domain tests around tax/RMD boundary cases.
5. Add dependency-update automation with grouped, reviewed updates.
6. Reassess shared components only after two or more applications repeatedly
   require the same change.

## Definition of done

A change is ready when its relevant lint, type, test, and build checks pass;
privacy and product boundaries remain intact; documentation reflects user-visible
or operational changes; and no generated files, secrets, or obsolete scaffold
assets are included.
