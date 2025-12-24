# Feature Breakdown: iPay QR App MVP

## Overview

- **Product / Initiative:** iPay QR App MVP - Cross-platform mobile app for Open Banking payments
- **Platforms / Stack:** Flutter (iOS & Android), NestJS backend, PostgreSQL, Redis
- **Constraints:**
  - UK/EU hosting (AWS London or Azure UK)
  - GDPR compliance required
  - MVP launch timeline: 12 weeks
  - Must support TrueLayer, Token.io, Yapily integrations

## Decomposition

| Feature | Epic / Story | Task (discipline) | Notes / Dependencies | Restriction |
| --- | --- | --- | --- | --- |
| **App Foundation** | App shell & setup | Flutter project setup with iOS/Android configs (Mobile) | Base project structure, dependencies | Project structure must be approved; all dependencies locked |
| | | CI/CD pipeline setup (DevOps) | GitHub Actions / GitLab CI for build & test | Build artifacts must pass security scans before deployment |
| | | Development environment setup (DevOps) | Local dev setup, emulator configs | All team members must complete setup successfully |
| **Security & Native Features** | Secure container | SSL pinning implementation (Mobile) | Certificate management, pinning config | Certificates must be managed via secure storage; security review required |
| | | Jailbreak/root detection (Mobile) | Native plugins for iOS/Android | Must work on iOS 13+ and Android 8+ |
| | | Screenshot prevention (Mobile) | Native security features | Must prevent screenshots in payment flows only |
| | Biometric auth | FaceID/TouchID integration (Mobile) | Flutter biometric plugin, error handling | Must fallback to PIN if biometric unavailable |
| | | Biometric fallback to PIN (Mobile) | PIN entry UI, secure storage | PIN must be stored securely; max 3 failed attempts before lockout |
| | QR Scanner | Native camera integration (Mobile) | Camera permissions, QR parsing library | Must handle camera permission denial gracefully |
| | | QR code generation (Mobile) | QR library, payment data encoding | QR must be readable by standard scanners from 30cm distance |
| | Deep linking | Open Banking redirect handling (Mobile) | URL scheme config, deep link routing | URL schemes must be registered with app stores |
| | | Deep link validation & security (Mobile) | URL validation, signature checks | All deep links must be validated before processing |
| **Authentication & Onboarding** | User registration | Registration API endpoint (Backend) | User model, validation, password hashing | Max 1 email OR 1 phone per account. Don't support social login (Google/Apple). Password: min 8 chars, 1 uppercase, 1 number |
| | | Registration UI (Mobile) | Form validation, error handling | |
| | | Email verification flow (Backend + Mobile) | Email service, verification tokens | OTP valid 5 minutes. Max 3 resend/hour. Max 5 wrong attempts → lock 15 min |
| | User login | Login API endpoint (Backend) | JWT generation, session management | Max 5 failed attempts → lock 30 min. Session timeout 30 min inactive |
| | | Login UI with biometric option (Mobile) | Login form, biometric prompt | Only enable after 1 successful login. User can disable in Settings |
| | Merchant onboarding | Merchant registration API (Backend) | Merchant model, KYC data collection | Max 1 business per merchant account. Required fields: business name, address, contact, category. Category: predefined list (max 20 options). No edit after submit. Must contact support to change. 3 statuses: pending, approved, rejected. No detailed rejection reason displayed (generic message only) |
| | | Merchant onboarding UI (Mobile) | Multi-step form, document upload | Max 3 documents. Max 10MB/file. Formats: PDF, JPG, PNG only |
| | Bank account linking | Bank account linking API (Backend) | OB provider integration, account verification | Only support UK bank accounts. Max 1 bank account per merchant |
| | | Bank selection API (Backend) | Provider aggregation, bank list management | Aggregate from all configured providers. Cache in Redis (TTL 24h). Filter UK payment-enabled banks only. Include provider mapping per bank |
| | | Bank selection UI (Mobile) | Bank list display, search | Top 20 UK retail banks initially. Bank list cached 24h locally. Search by bank name only. Must display bank logo and name. Grid layout (2-3 columns). Loading skeleton while fetching. Include "Can't find your bank?" help link |
| **Payment Flows** | QR Payment Initiation | Generate QR code API (Backend) | Payment session creation, QR data | Dynamic QR only (amount included). QR valid 15 minutes. Max amount: £10,000. Min amount: £0.01 |
| | | QR display UI (Mobile) | QR code rendering, amount display | |
| | | Scan QR & parse (Mobile) | Camera integration, QR parsing | Only scan iPay QR format. No support for scanning QR from other payment providers. 4 error types: expired, invalid_format, invalid_signature, merchant_inactive |
| | Open Banking Integration | TrueLayer integration (Backend) | API client, webhook handler | |
| | | Token.io integration (Backend) | API client, webhook handler | |
| | | Yapily integration (Backend) | API client, webhook handler | |
| | | Payment initiation API (Backend) | Provider routing, payment session | Single payment only (no recurring). GBP only. UK banks only. Max £10,000, Min £0.01. Payment session expires 15 minutes after QR scan. Idempotency required (use QR reference). Request timeout 30s. Must validate QR HMAC signature. Only approved merchants can receive payments |
| | | Payment status polling (Backend) | Status check endpoints, provider APIs | |
| | Payment UI | Payment initiation screen (Mobile) | Amount confirmation, provider selection | Must display regulatory disclaimer for PISPs. Show "Powered by [Provider]" badge. Amount not editable after QR scan |
| | | Payment status screen (Mobile) | Real-time status updates, success/failure | WebSocket preferred, polling fallback (every 5s). Play sound/vibration on new payment. Show in-app notification banner |
| | | Redirect handling for OB flows (Mobile) | Deep link handling, WebView for OB | CRITICAL: Must open in external browser, NOT WebView (banks block WebView for security). Redirect timeout: 30 seconds. If user doesn't complete → auto cancel. Show interstitial before redirect. Show bank logo on interstitial. Include security message. Auto-redirect after 2-3 seconds or on tap. Support success/cancel/error scenarios. Handle app killed during redirect. Requires Universal Links (iOS) + App Links (Android) |
| **Transaction Management** | Transaction History | Transaction list API (Backend) | Pagination, filtering, sorting | Must support pagination (20 items per page) and date filtering |
| | | Transaction history UI (Mobile) | List view, pull-to-refresh, filters | Must support pull-to-refresh and infinite scroll |
| | | Transaction detail API (Backend) | Single transaction retrieval | Must return full transaction details including status |
| | | Transaction detail UI (Mobile) | Detail view, receipt generation | Show loading while verifying. Clearly distinguish success/failure/cancelled states. Success: show amount, merchant, reference, timestamp. Failure: generic error only (no technical details). Include support contact on failure. Animation for success. User-friendly error messages. Include share/screenshot option |
| **Merchant Dashboard** | Dashboard overview | Dashboard API (Backend) | Aggregated stats, recent transactions | API response must be <500ms; cache for 5 minutes |
| | | Dashboard UI (Mobile) | Charts, summary cards, navigation | Charts must be accessible (WCAG AA) |
| | Settings | Settings API (Backend) | User preferences, notification settings | Settings must persist across app restarts |
| | | Settings UI (Mobile) | Settings screens, preference toggles | Logout single device only (not logout all devices) |
| **Backend Infrastructure** | Database setup | PostgreSQL schema design (Backend) | Tables, indexes, migrations | Schema must support GDPR deletion requests |
| | | Database migrations (Backend) | Migration scripts, seed data | All migrations must be reversible |
| | Caching & Sessions | Redis setup (DevOps) | Redis configuration, connection pooling | Redis must be configured for persistence |
| | | Session management (Backend) | Redis session store, TTL management | Sessions must expire after 24h inactivity |
| | API Security | JWT authentication middleware (Backend) | Token validation, refresh logic | Refresh tokens must expire after 30 days |
| | | Webhook HMAC verification (Backend) | Provider-specific signature validation | Webhook processing <5 seconds. Idempotency using event ID (Redis TTL 24h). Must verify signature per provider |
| | | Secrets management (DevOps) | AWS Secrets Manager / Azure Key Vault | All secrets must be stored in cloud secret manager |
| **Observability & QA** | Logging | Structured logging (Backend) | Log levels, correlation IDs | All logs must include correlation IDs for tracing |
| | | Error tracking (Backend) | Sentry/error monitoring integration | Critical errors must trigger alerts |
| | Monitoring | Metrics collection (Backend) | Prometheus/Grafana or cloud metrics | Metrics dashboard must be accessible to team |
| | | Health check endpoints (Backend) | /health, /ready endpoints | Health check must verify DB and Redis connectivity |
| | Testing | Unit tests (Backend + Mobile) | Test coverage for critical paths | Minimum 80% code coverage for backend, 70% for mobile |
| | | Integration tests (Backend) | API tests, provider sandbox tests | All payment flows must have integration tests |
| | | E2E tests (QA) | Critical user journeys | Must test on iOS 13+ and Android 8+ |
| | QA | Test plan creation (QA) | Test cases, regression suite | Test plan must cover all user stories |
| | | Manual testing (QA) | Exploratory testing, device testing | Must test on at least 3 iOS and 3 Android devices |

## Cross-Cutting Tasks

- **Security hardening:**
  - SSL pinning configuration and certificate management
  - Jailbreak/root detection implementation
  - Webhook HMAC/JWT verification for all providers
  - Secrets management (AWS Secrets Manager / Azure Key Vault)
  - GDPR compliance: data retention policies, user data export/deletion

- **Observability / analytics:**
  - Structured logging with correlation IDs
  - Metrics: API response times, error rates, payment success rates
  - Error tracking (Sentry or similar)
  - Analytics events for key user actions (privacy-compliant)

- **Feature flags / config:**
  - Feature flag system for gradual rollout
  - Environment-based configuration (dev/staging/prod)
  - Provider enable/disable flags

- **QA & test data:**
  - Test data seeding scripts
  - Sandbox account setup for each OB provider
  - Test QR codes for various scenarios
  - Device testing matrix (iOS/Android versions)

- **CI/CD & environments:**
  - Build pipelines for iOS/Android apps
  - Automated testing in CI
  - Staging environment setup
  - Production deployment process
  - App Store / Play Store submission process

## Definition of Done Reminders

- Code reviewed, tested, and merged
- AC met (happy/unhappy paths)
- Logging/metrics in place for new flows
- Secrets managed and configs versioned
- Security review completed for sensitive features
- Accessibility checks passed (WCAG AA)
- Documentation updated (API docs, user guides)
