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

   - Mobile (Flutter/RN), Web/FE, BE/API, Data/DB, QA, DevOps/SRE.

4) Keep tasks independent where possible; express clear outcome and AC hints.
5) Note dependencies (e.g., API contract before UI wiring, SDK availability, credentials).
6) Include cross-cutting tasks: instrumentation/analytics, feature flags, accessibility, security hardening, CI/CD adjustments.
7) If a task exceeds 2 PD or spans multiple concerns, split further.

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

- Use person-days (PD) at 8 hours per day; when finer granularity helps, use hours.
- Platform/Type**: Mobile, Web, API, AI, Design, Admin ...
- Task Complexity: Low, Medium, High, Very High

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

# Story Format

## User Story Format

**Standard Format:**

- As a `<role>`, I want `<goal>`, so that `<outcome>`.

**Guidelines:**

- Use specific roles (e.g., "merchant", "end user", "admin", "payment processor", "developer")
- State clear, measurable goals
- Explain the business value/outcome
- Include context or preconditions when non-obvious
- Keep stories sprint-sized (typically 1-5 person-days)

## Examples

### Example 1: Mobile Chat Feature

- As a user, I want to see my chat history so that I can see conversations and go to chatDetail to start conversations.
- As a user, I want to see list message history of conversation and receive new message incoming.
- As a user, I want to send messages so that I can communicate with others.
- As a user, I want to send images so that I can share multimedia content.
  - Note: not support , videos, and other files type yet. Need more time if have
- As a user, I want to receive push notifications for new messages so that I stay updated even when the app is closed.

## Example 2: Subscription

- As a user, I want to view subscription plans, so that I can understand available pricing and benefits.
- As a user, I want to start a 7-day free trial for either the yearly or monthly plan, so that I can explore premium features without immediate payment.
- As a user, I want to purchase a subscription using in-app purchase, so that I can unlock premium content (e.g., exclusive recipes).
- As a user, I want to see my current subscription status, so that I know if I have access to premium features.
- As a developer, I want to integrate IAP for iOS, so that users can purchase subscriptions through the appropriate store.
- As a developer, I want to integrate IAP for Android, so that users can purchase subscriptions through the appropriate store.
- As a developer, I want to securely validate and sync subscription status with backend, so that premium access is consistently managed.
- As a premium user, I want to access all features, so that I get full value for my subscription.
- As a free user, I want to see which features or content are locked, so that I understand what I’m missing as a non-subscriber.

## Example 3: Deploy

As a developer, I want to deploy the app to the App Store and Google Play, so that users can download and use it on their devices.
    - Setup metadata (app name, description, screenshots, categories, etc.)
    - Configure beta testing
    - Handle review - fix any rejection issues from the App Store or Play Store
