# Breakdown Rules

## Goal

Consistent decomposition to task-level items that are estimable and testable within Scrum or Kanban.

## Levels

- Feature: user-facing capability or major service area.
- Epic / User Story: coherent slice delivering value; small enough for a sprint.
- Task: single-discipline unit of work (Mobile, FE, BE, QA, Ops) ideally ≤2 PD.

## Decomposition Rules

1) Start from feature list; for each, enumerate user journeys and system interactions.
2) Derive epics/stories per journey or subsystem; include unhappy paths and security flows.
3) Split stories into tasks by concern:

   - Mobile (Flutter + native bridges), Web/FE, BE/API, Data/DB, QA, DevOps/SRE.

4) Keep tasks independent where possible; express clear outcome and AC hints.
5) Note dependencies (e.g., API contract before UI wiring, SDK availability, credentials).
6) Include cross-cutting tasks: instrumentation/analytics, feature flags, accessibility, security hardening, CI/CD adjustments.
7) If a task exceeds 2 PD or spans multiple concerns, split further.

## Definition of Ready (DoR) for Estimation

- Clear goal and scope
- Known integrations/providers
- Acceptance criteria drafted (happy and main unhappy paths)
- Non-functional needs captured (performance, security, compliance)
- Environment assumptions noted (dev/stage/prod, regions)

## Definition of Done (DoD) Hints

- Code merged, reviewed, linted, and unit-tested
- Integration tested against sandbox or mocked providers
- QA sign-off for main paths; regression updated
- Observability: logs/metrics for new flows; alerts for critical failures
- Security: secrets managed, least-privileged access, transport security validated
