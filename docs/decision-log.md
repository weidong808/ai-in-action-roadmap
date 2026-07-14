# Decision Log

Record significant product and architecture decisions here. Newest first.

Format: **ADR-lite** — context, decision, consequences.

---

## D-007 — Public repo excludes private commercial strategy

- **Date:** 2026-07  
- **Status:** Accepted  
- **Context:** This repository is a public educational / showcase portfolio for professional credibility. Private commercial plans must not appear here.  
- **Decision:** Document only education, architecture, delivery, and engineering-learning themes. Replace monetization docs with [scope.md](./scope.md). Agents must refuse to add pricing, payment providers, or private business strategy.  
- **Consequences:** Public philosophy loop is Build → Validate → Improve → Document → Share. Capability maturity replaces Guest/Free/Premium commercial framing.

---

## D-001 — Dedicated public roadmap repository

- **Date:** 2026-07  
- **Status:** Accepted  
- **Context:** Need a durable north star for phased work without mixing planning into app repos.  
- **Decision:** Create public repo `weidong808/ai-in-action-roadmap` for vision, roadmap checklists, docs, diagrams, and milestones only.  
- **Consequences:** App repos stay focused on code; strategy changes are reviewable in one place; no application source code in the roadmap repo.

---

## D-002 — Operating philosophy: build → validate → improve → document → share

- **Date:** 2026-07  
- **Status:** Accepted (updated)  
- **Context:** Risk of overdesigning a multi-app platform before validation; public portfolio must not read as a commercial roadmap.  
- **Decision:** Follow Build → Validate → Improve → Document → Share. Build one app at a time. Local-first by default; optional auth later as an engineering milestone.  
- **Consequences:** Near-term work prioritizes SleepCheck polish, content, and feedback over big-bang shared platform work.

---

## D-003 — Showcase MIT educational case studies; private work stays private

- **Date:** 2026-07  
- **Status:** Accepted (pending legal review of public wording)  
- **Context:** Public apps are educational showcases. Future proprietary work may exist separately.  
- **Decision:** Keep current showcase repos MIT; do not invent open-core commercialization plans in this public repo; do not impulsively relicense.  
- **Consequences:** Clear educational licensing note; private experiments stay out of this tree.

---

## D-004 — SleepCheck wellness positioning

- **Date:** 2026-07  
- **Status:** Accepted  
- **Context:** Sleep-related products invite medical-device / diagnostic interpretation.  
- **Decision:** Position SleepCheck as wellness / educational / habit support; avoid diagnostic claims.  
- **Consequences:** Content, UI copy, and “insights” language must stay non-diagnostic; regulatory paths only with deliberate legal support.

---

## D-005 — Authentication provider

- **Date:** —  
- **Status:** Proposed / not decided  
- **Context:** Phase 3 may introduce optional managed IdP as an architecture skill demo.  
- **Decision:** TBD among Entra External ID, Auth0, Clerk, Firebase Auth, Supabase Auth, Cognito, etc.  
- **Consequences:** Spike and score against authentication-strategy criteria before committing.

---

## Top risks (living)

| Risk | Mitigation | Owner focus |
|------|------------|-------------|
| Platform overbuild | Phase checkboxes; extract on proven duplication | Architect |
| Private strategy leaking into public docs | [scope.md](./scope.md); agent refusal rule | Architect |
| License confusion | MIT educational stance; private work separate | Architect + counsel |
| Medical mispositioning | Wellness language; content review | Product + content |
| Privacy debt at auth time | Privacy/retention before accounts | Architect |
| Content without shipping | Pair every article with live URL + diagrams | Content |

When a risk becomes a decision, promote it to a dated entry above.
