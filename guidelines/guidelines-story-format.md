# Story Format

## User Story Format

**Standard Format:**

- As a `<role>`, I want `<goal>`, so that `<outcome>`.

**Guidelines:**

- Use specific roles (e.g., "merchant", "end user", "admin", "payment processor")
- State clear, measurable goals
- Explain the business value/outcome
- Include context or preconditions when non-obvious
- Keep stories sprint-sized (typically 1-5 person-days)

## Acceptance Criteria (AC)

**Format:** Use Given / When / Then structure

**Coverage:**

- **Happy path**: Primary success scenario
- **Failure paths**: Main error cases and edge cases
- **Validation**: Input validation, business rules
- **Error handling**: User-friendly error messages and recovery
- **Non-functional**: Performance, security, accessibility when critical

**Best Practices:**

- Each AC should be independently testable
- Include data/state preconditions explicitly
- Specify expected outcomes clearly
- Add performance targets when relevant (e.g., "within 1s", "supports 1000 concurrent users")

## Additional Fields

**Dependencies:**

- Upstream APIs or services
- Credentials, SDKs, or libraries
- Environments (dev/staging/prod)
- Other stories or features

**Definition of Done Reminders:**

- Tests: unit, integration, E2E
- Logging/metrics for observability
- Feature flags for gradual rollout
- Accessibility checks (WCAG compliance)
- Security: authentication, authorization, secrets management
- Documentation: API docs, user guides

## Examples

### Example 1: Mobile Feature

**Story:** As a merchant, I want to scan a customer QR code to initiate payment so that I can collect funds quickly.

**Context:** The app uses native camera APIs via Flutter plugins. QR codes contain payment initiation data (amount, payer ID, transaction reference).

**Acceptance Criteria:**

1. **Happy Path:**
   - Given camera permission is granted, when I tap "Scan QR", then the native scanner opens within 1s and displays camera view
   - Given a valid QR payload is scanned, when the scanner detects it, then payment initiation screen pre-fills amount and payer ID, and I can review before confirming

2. **Error Handling:**
   - Given an invalid/expired QR code, when scanned, then I see an error message "Invalid QR code. Please try again." with a retry button
   - Given no camera permission, when I tap "Scan QR", then I am prompted to allow access with explanation, or guided to Settings if previously denied
   - Given camera hardware is unavailable, when I tap "Scan QR", then I see "Camera not available" message

3. **Non-Functional:**
   - Scanner opens within 1s on devices with camera access
   - QR detection works in normal indoor lighting conditions
   - Scanner respects app security policy (no screenshots during scan)

**Dependencies:**

- Native camera plugin (camera package)
- QR code parsing library
- Payment initiation API endpoint

**Tests:**

- Unit: QR parsing logic, validation rules
- Integration: Camera plugin integration, API call with parsed data
- Manual: Various QR formats, lighting conditions, permission flows

---

### Example 2: Backend API Feature

**Story:** As a payment processor, I want to receive webhook notifications from Open Banking providers so that I can update transaction status automatically.

**Context:** Webhooks arrive from TrueLayer, Token.io, and Yapily. Each provider uses HMAC signatures for verification.

**Acceptance Criteria:**

1. **Happy Path:**
   - Given a valid webhook with correct HMAC signature, when received, then transaction status is updated in database and confirmation response (200 OK) is returned within 500ms
   - Given webhook contains payment completion event, when processed, then merchant is notified via push notification

2. **Error Handling:**
   - Given invalid HMAC signature, when webhook received, then request is rejected (401 Unauthorized) and logged as security event
   - Given duplicate webhook (same event ID processed), when received, then idempotent handling returns 200 OK without duplicate processing
   - Given webhook payload is malformed, when received, then 400 Bad Request is returned and error is logged

3. **Non-Functional:**
   - Webhook endpoint responds within 500ms (p95)
   - Supports 100 webhooks/minute per provider
   - All webhook events are logged with correlation IDs
   - Failed webhooks are retried with exponential backoff (max 3 retries)

**Dependencies:**

- HMAC verification libraries for each provider
- Transaction database
- Push notification service
- Webhook endpoint infrastructure

**Tests:**

- Unit: HMAC verification, payload parsing, idempotency checks
- Integration: End-to-end webhook processing with test providers
- Security: Signature validation, replay attack prevention

---

### Example 3: Frontend Feature

**Story:** As an end user, I want to view my transaction history with filters so that I can quickly find specific payments.

**Context:** Transaction list displays last 30 days by default. Supports filtering by date range, amount, status, and search by merchant name.

**Acceptance Criteria:**

1. **Happy Path:**
   - Given I am logged in, when I navigate to Transaction History, then I see list of transactions from last 30 days sorted by date (newest first)
   - Given I apply date range filter (e.g., last 7 days), when I confirm, then list updates to show only transactions in that range
   - Given I search by merchant name "Coffee Shop", when I submit, then list shows only transactions matching that merchant

2. **Error Handling:**
   - Given API returns error, when loading transactions, then I see "Unable to load transactions. Please try again." with retry button
   - Given no transactions match filters, when I apply filters, then I see "No transactions found" message with option to clear filters

3. **Non-Functional:**
   - Transaction list loads within 2s on 3G connection
   - Supports pagination for lists >50 items
   - Filters persist in URL query params (shareable/bookmarkable)
   - Accessible: keyboard navigation, screen reader support, WCAG AA compliant

**Dependencies:**

- Transaction history API endpoint
- Date picker component library
- Search/filter state management

**Tests:**

- Unit: Filter logic, date range calculations
- Integration: API calls with various filter combinations
- E2E: Complete user flow with filters and search
- Accessibility: Screen reader testing, keyboard navigation
