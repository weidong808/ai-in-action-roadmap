# Update — AI feature additions across the series

**Date:** 2026-07-23
**Owner:** Weidong Shi — Senior Technology Architect
**Status:** Implemented on feature branches, pending review / release.

This entry records a round of AI and UX additions made across the AI in
Action apps, so the roadmap reflects what now exists in code (not just what is
deployed). Each change lives on its own feature branch and does not alter
`main` until reviewed.

## What changed

| App | Branch | Change |
|-----|--------|--------|
| SleepCheck | `feat/ai-bedtime-stories` | New optional AI bedtime-story generator: a Node API route composes a calm, second-person story via OpenAI, validated by dependency-free type guards with an injection-resistant prompt and per-IP rate limiting. Reuses the existing narrator engine. Hidden unless `OPENAI_API_KEY` is set. |
| RetireCheck | `feat/ai-plan-explainer` | New optional "Explain my plan in plain English" panel. Sends only a PII-free numeric summary to OpenAI; the prompt forbids the model from changing any number and frames output as educational, not advice. Deterministic engine remains authoritative. |
| HabitCheck | `feat/toast-feedback` | Accessible, reduced-motion-aware toast feedback wired into check-in, skip, create, archive, and recovery actions. |
| AI Production Readiness Advisor | `feat/report-copy-markdown` | "Copy Markdown" report action (paste a readiness summary into Slack / a PR / a doc) with clipboard fallback to download. |
| Personal hub | `feat/live-app-status` | App tiles show a best-effort liveness indicator (CORS-safe reachability probe) instead of a static "Live" badge. |

## Alignment notes

- SleepCheck and RetireCheck now have working AI capabilities. Previously the
  commercial/monetization docs assumed premium AI features that were not yet
  built; those assumptions are now backed by real implementations (see the
  business roadmap update of the same date).
- All AI features are **opt-in and privacy-preserving**: they are disabled and
  their entry points hidden unless an API key is configured, and they send
  only aggregate / non-PII data. This is consistent with
  [privacy-and-security.md](../privacy-and-security.md).
- No new runtime dependencies were added to any app; AI calls use `fetch` and
  responses are validated with hand-written type guards.

## Follow-ups

- Consider a shared provider abstraction (OpenAI + a fallback) across apps.
- Consider streaming responses for the SleepCheck story and RetireCheck
  explainer to improve perceived latency.
