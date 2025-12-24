# Estimation Method

## Purpose

Consistent, lightweight effort estimation for product features using Scrum or Kanban practices, with outputs ready to populate the provided templates.

## Inputs Required

- Product brief or requirements list
- Target platforms and tech stack
- Constraints: timeline, compliance, hosting, regions
- Team composition and velocity assumptions (if known)
- Definition of Done (DoD) and Acceptance Criteria (AC) expectations

## Units and Scales

- Use person-days (PD) at 6 focused hours per day; when finer granularity helps, use hours.
- Label confidence: High (≥70% knowns), Medium (some unknowns), Low (many unknowns/new tech).
- Apply risk buffer after sizing: Low risk +10%, Medium +20%, High +35%.

## Estimation Steps

1) Clarify scope: list key features and constraints; note exclusions.
2) Decompose: feature → epic/user story → tasks (FE, Mobile, BE, QA, Ops as needed).
3) Assumptions: document environment, tools, integrations, data availability.
4) Size tasks: base effort (PD) with rationale; consider complexity drivers (new tech, integrations, security, performance, data migration, environments).
5) Add buffer: apply risk multiplier per feature/epic based on unknowns.
6) Summarize: totals per feature and overall; call out critical path and dependencies.

## Complexity Heuristics

- Open Banking/payment integrations: +30–60% per provider if brand-new; reuse reduces to +10–20%.
- Security hardening (cert pinning, jailbreak/root detection, HMAC/JWT webhook verification): add 0.5–1.5 PD per platform/service.
- Mobile native bridges (camera/biometric/deep link): 0.5–1 PD each if standard libraries; more if custom UX flows.
- Cloud infra baseline (single region): 2–4 PD for IaC, CI/CD, secrets, observability skeleton.
- QA: functional + regression + basic security checks; add 20–30% of build effort unless already included per task.

## Output Expectations

- Deliver feature breakdown and estimation tables using the templates in /templates.
- Keep language concise and actionable; highlight blockers, dependencies, and assumptions.
