# User Story

- As a **`<role>`**, I want **`<goal>`**, so that **`<outcome>`**.

## Context / Preconditions

- [Background information, user state, or system conditions required]
- [Example: User is logged in and authenticated]
- [Example: Payment provider account is configured]

## Acceptance Criteria (Given / When / Then)

**Happy Path:**

1. Given [precondition], when [action], then [expected outcome]
2. Given [precondition], when [action], then [expected outcome]

**Error Handling:**
3. Given [error condition], when [action], then [error message/behavior]
4. Given [edge case], when [action], then [handling]

**Validation:**
5. Given [invalid input], when [action], then [validation error]

**Format Guidelines:**

- Use Given/When/Then structure
- Each AC should be independently testable
- Cover happy path, main error cases, and edge cases
- Be specific about expected outcomes

## Non-Functional

- **Performance/availability:**
  - [Response time targets, e.g., "Loads within 2s"]
  - [Throughput requirements, e.g., "Supports 100 concurrent users"]
  - [Availability targets, if applicable]

- **Security/privacy:**
  - [Authentication/authorization requirements]
  - [Data protection measures]
  - [Input validation and sanitization]
  - [Privacy considerations]

- **Accessibility:**
  - [WCAG compliance level, e.g., "WCAG AA"]
  - [Screen reader support]
  - [Keyboard navigation]
  - [Color contrast requirements]

## Dependencies

- **Upstream:**
  - [APIs, services, or features that must be ready first]
  - [Example: Payment API endpoint must be implemented]

- **Credentials/Environments:**
  - [Required credentials, SDKs, or environment setup]
  - [Example: Test API keys, sandbox accounts]

- **Other Stories:**
  - [Related stories that should be completed first]
  - [Example: Authentication flow must be complete]

## Definition of Done Checklist

- [ ] Story meets all acceptance criteria
- [ ] Documentation updated (if applicable)
- [ ] Non-functional requirements verified
- [ ] Accessibility checks passed (if applicable)
