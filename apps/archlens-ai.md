# ArchLens AI — AI in Action #5

**Status:** Live (verified evidence core)  
**Series role:** Enterprise architecture / evidence-first AI showcase  
**Repo:** https://github.com/weidong808/archlens-ai  
**Live demo:** https://archlens.weidong-shi.com  
**Vercel alias:** https://archlens-ai.vercel.app  
**Hub case study:** https://weidong-shi.com/work/archlens  

## Purpose

Turn architecture evidence into a **cited, human-approved modernization plan** — with a deterministic verifier gate that can refuse to advise when a claim is not proven.

Public demo mode uses **committed synthetic fixtures only**. No API key required for the current slice.

## Why this is App #5

Apps #1–#4 span decision support, wellness, production readiness gates, and local-first coaching. **ArchLens** is the enterprise architecture story: hybrid RAG and multi-agent orchestration *eventually* — but first, **evidence before recommendation** must be falsifiable.

Slice 1b makes that real: analysis re-reads and re-hashes fixtures on every click; citations resolve to `file:line`; unsupported claims render struck-through with **no recommended action**; tampering demotes findings to **stale**.

## Current milestone (slice 1b)

- Real SQL fixtures on disk (`fixtures/northstar/`)
- Verifier registry (`shared-write-target` SQL scan)
- Server action reads fixtures at runtime — not replayed prose
- Refusals are first-class UI
- 22 vitest tests + GitHub Actions CI
- Deployed on Vercel with fixture tracing in `next.config.ts`

## Next (slice 2)

Model as **proposer only** — every claim still adjudicated by the verifier before a human sees it.

## Related

- [BUILD-PLAN.md](https://github.com/weidong808/archlens-ai/blob/main/docs/BUILD-PLAN.md)  
- [SLICE-1B-REVISED.md](https://github.com/weidong808/archlens-ai/blob/main/docs/SLICE-1B-REVISED.md)  
- [PRIVACY-THREAT-MODEL.md](https://github.com/weidong808/archlens-ai/blob/main/docs/PRIVACY-THREAT-MODEL.md)  
- Public hub: [weidong-shi.com](https://weidong-shi.com)
