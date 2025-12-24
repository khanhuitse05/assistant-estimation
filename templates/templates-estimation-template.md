# Estimation

## Scope Summary

- **Context:** [Brief description of the product/project and its purpose]
- **Goals:** [Key objectives and success criteria]
- **Out of scope:** [Explicitly excluded features or requirements]

## Assumptions

- [List assumptions about requirements, technology, team, or environment]
- [Example: Team has experience with React and Node.js]
- [Example: Third-party API sandbox available for testing]

## Estimation Table (person-days)

| Feature / Epic | User Story | Task | Platform | Difficulty | Core Feature | Min (PD) | Max (PD) | Avg (PD) | Milestone | Restriction |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [Feature name] | [As a role, I want goal, so that outcome] | [Task description] | [UI/FE - Web/FE - Mobile/API/QA/Ops] | [High/Medium/Low] | [TRUE/FALSE] | [Min estimate] | [Max estimate] | [Average] | [Final estimate] | [Definition of done, blockers, or constraints] |
| | | [Next task] | [Platform] | [Difficulty] | [TRUE/FALSE] | [Min] | [Max] | [Avg] | [Final] | [Restriction] |
| | [Next user story] | [Task] | [Platform] | [Difficulty] | [TRUE/FALSE] | [Min] | [Max] | [Avg] | [Final] | [Restriction] |
| [Next feature] | [User story] | [Task] | [Platform] | [Difficulty] | [TRUE/FALSE] | [Min] | [Max] | [Avg] | [Final] | [Restriction] |

**Estimation Guidelines:**

- **Feature / Epic:** High-level feature or epic name
- **User Story:** Full user story text (repeat for each task under that story)
- **Task:** Specific task description broken down by platform/discipline
- **Platform:** UI, FE - Web, FE - Mobile, API, QA, Ops, etc.
- **Difficulty:** High, Medium, or Low complexity
- **Core Feature:** TRUE if Core Feature
- **Min (PD):** Minimum estimate in person-days
- **Max (PD):** Maximum estimate in person-days
- **Avg (PD):** Average of min and max: (Min + Max) / 2
- **Milestone:** It will be divided into 1, 2, or 3 phases, depending on the size of the project.
- **Restriction:** Definition of "done" for this task, potential blockers, or constraints that affect completion

**Note:** Feature/Epic and User Story columns should repeat for each task row to show hierarchy. Leave empty if same as row above.

### Totals

- **Total Min:** [Sum of all min estimates]
- **Total Max:** [Sum of all max estimates]
- **Total Avg:** [Sum of all avg estimates]
- **Total Final:** [Sum of all final estimates]
- **Critical path:** [List features/tasks that must complete sequentially and are on the longest path]

**Team & Timeline:**

- Team composition: [e.g., 2 FE, 2 BE, 1 QA]
- Estimated velocity: [PD per week]
- Estimated timeline: [Total Final ÷ velocity]

## Non-Functional & Compliance

- **Security:**
  - [Authentication/authorization requirements]
  - [Data encryption, transport security]
  - [Secrets management]
  - [Security testing requirements]

- **Performance/Availability:**
  - [Response time targets, e.g., API <500ms p95]
  - [Throughput requirements, e.g., 1000 req/min]
  - [Uptime targets, e.g., 99.5%]
  - [Scalability considerations]

- **Observability:**
  - [Logging requirements: structured logs, correlation IDs]
  - [Metrics: what to track, alert thresholds]
  - [Error tracking: Sentry, error monitoring]
  - [Health checks: endpoints, monitoring]

- **Compliance/Privacy:**
  - [GDPR, PCI-DSS, HIPAA, etc.]
  - [Data retention policies]
  - [User consent management]
  - [Audit logging requirements]

## Open Questions

- [Unanswered questions that affect estimation accuracy]
- [Clarifications needed from stakeholders]
- [Technical decisions pending]
