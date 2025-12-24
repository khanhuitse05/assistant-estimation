# Feature Breakdown

## Overview

- **Product / Initiative:** [Name of product or project]
- **Platforms / Stack:** [e.g., React (Web), Flutter (iOS/Android), Node.js (Backend), PostgreSQL]
- **Constraints:** [Timeline, compliance, hosting, regions, team size]

## Decomposition

| Feature / Epic | User Story | Task | Platform | Notes / Dependencies | Restriction |
| --- | --- | --- | --- | --- | --- |
| [Feature name] | [As a role, I want goal, so that outcome] | [Task description] | [UI/FE - Web/FE - Mobile/API/QA/Ops] | [Dependencies, blockers, or special notes] | [Definition of done, blockers, or constraints] |
| | | [Next task] | [Platform] | [Notes] | [Restriction] |
| | [Next user story] | [Task] | [Platform] | [Notes] | [Restriction] |
| [Next feature] | [User story] | [Task] | [Platform] | [Notes] | [Restriction] |

**Note:** Feature/Epic and User Story columns should repeat for each task row to show hierarchy. Leave empty if same as row above.

**Discipline Abbreviations:**

- **Mobile:** Flutter, React Native, native iOS/Android
- **FE:** Frontend (React, Vue, Angular, etc.)
- **BE:** Backend (API, services, database)
- **QA:** Testing, test automation, quality assurance
- **Ops:** DevOps, infrastructure, CI/CD, deployment

**Decomposition Guidelines:**

- Break features into epics/stories (sprint-sized, deliverable value)
- Split stories into tasks by discipline
- Keep tasks independent where possible
- Each task ideally ≤2 person-days
- Include dependencies explicitly

## Cross-Cutting Tasks

- **Security hardening:**
  - [SSL pinning, certificate management]
  - [Authentication/authorization implementation]
  - [Secrets management setup]
  - [Security testing, penetration testing]
  - [Compliance checks]

- **Observability / analytics:**
  - [Structured logging setup]
  - [Metrics collection (Prometheus, CloudWatch, etc.)]
  - [Error tracking (Sentry, etc.)]
  - [Analytics events (privacy-compliant)]
  - [Dashboard creation]

- **Feature flags / config:**
  - [Feature flag system setup]
  - [Environment configuration management]
  - [A/B testing infrastructure]
  - [Gradual rollout capabilities]

- **QA & test data:**
  - [Test data seeding scripts]
  - [Test environment setup]
  - [Test automation framework]
  - [Device/browser testing matrix]
  - [Performance testing setup]

- **CI/CD & environments:**
  - [Build pipeline configuration]
  - [Automated testing in CI]
  - [Deployment automation]
  - [Environment provisioning (dev/staging/prod)]
  - [Rollback procedures]

## Definition of Done Reminders

- Code reviewed, tested, and merged to main branch
- Acceptance criteria met (happy and unhappy paths)
- Unit tests written with adequate coverage
- Integration tests passing
- Logging/metrics in place for new flows
- Secrets managed securely and configs versioned
- Documentation updated (API docs, README, user guides)
- Security review completed for sensitive features
- Accessibility checks passed (WCAG AA if applicable)
- Performance targets met (if specified)
- Feature flags configured (if applicable)
