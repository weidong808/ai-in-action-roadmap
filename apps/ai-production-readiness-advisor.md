# AI Production Readiness Advisor — AI in Action #3

**Status:** Live  
**Series role:** Engineering / architecture showcase (not a Better Living “Check” wellness app)  
**Repo:** https://github.com/weidong808/ai-production-readiness-advisor  
**Live demo:** https://readiness.weidong-shi.com  
**Vercel alias:** https://ai-production-readiness-advisor.vercel.app

## Purpose

Help engineers and architects assess whether an AI feature is ready for production using:

1. Deterministic dimension scores + hard gates  
2. Schema-validated advisory narrative (OpenAI)  
3. Small curated reference corpus with citations  
4. Explicit “advisory only — not certification” framing  

## Why this is App #3

RetireCheck and SleepCheck demonstrated end-to-end product delivery in decision-support and local-first wellness. App #3 showcases **enterprise-relevant AI engineering judgment**: evaluation gates, prompt-injection posture, observability, cost controls, and structured outputs.

**HabitCheck** remains a Better Living candidate (see [habitcheck.md](./habitcheck.md)) and is **not replaced** — it is sequenced separately from this engineering showcase.

## Lessons intended for the case study

- Separate deterministic go/no-go logic from LLM narrative  
- Fail closed on malformed model output  
- Keep a reviewable in-repo corpus instead of open-ended web RAG for v1  
- Treat assessment free text as untrusted input  

## Related

- [future-apps.md](./future-apps.md)  
- [../docs/application-roadmap.md](../docs/application-roadmap.md)  
- Public hub: [weidong-shi.com](https://weidong-shi.com)  
