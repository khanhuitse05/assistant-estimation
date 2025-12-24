# Estimation: iPay QR App MVP

## Scope Summary

- **Context:** Cross-platform mobile app (Flutter) for Open Banking payments with NestJS backend. MVP launch target: 12 weeks.
- **Goals:**
  - Enable merchants to generate and scan QR codes for payments
  - Integrate with 3 Open Banking providers (TrueLayer, Token.io, Yapily)
  - Secure, GDPR-compliant payment processing
  - Merchant dashboard and transaction history
- **Out of scope:**
  - Push notifications (later phase)
  - Multi-currency support
  - Advanced analytics/reporting
  - Merchant admin web portal

## Assumptions

- Team has Flutter and NestJS experience
- Open Banking provider sandboxes available for testing
- AWS/Azure accounts provisioned
- Design assets and brand guidelines provided
- App Store/Play Store developer accounts ready
- Third-party libraries available: camera, biometric, QR code libraries
- Existing authentication patterns can be reused

## Estimation Table (person-days, 6h/PD)

| Feature / Epic | Task | Base Effort (PD) | Buffer % | Buffered Effort (PD) | Confidence | Dependencies / Risks | Notes | Restriction |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **App Foundation** | Flutter project setup | 1.0 | 10% | 1.1 | High | - | Standard setup | |
| | CI/CD pipeline | 2.0 | 20% | 2.4 | Medium | DevOps expertise | GitHub Actions setup | |
| | Dev environment setup | 0.5 | 10% | 0.6 | High | - | Documentation | |
| **Security & Native** | SSL pinning | 1.5 | 35% | 2.0 | Low | Certificate management complexity | New security requirement | |
| | Jailbreak/root detection | 1.0 | 20% | 1.2 | Medium | Plugin availability | May need custom native code | |
| | Screenshot prevention | 0.5 | 10% | 0.6 | High | Native APIs | Standard implementation | |
| | Biometric auth | 1.5 | 20% | 1.8 | Medium | Plugin integration | Fallback handling adds complexity | Only enable after 1 successful login. User can disable in Settings |
| | QR Scanner | 2.0 | 20% | 2.4 | Medium | Camera permissions, QR library | Edge cases in parsing | Only scan iPay QR format. No support for scanning QR from other payment providers |
| | QR generation | 0.5 | 10% | 0.6 | High | QR library | Straightforward | |
| | Deep linking setup | 1.0 | 20% | 1.2 | Medium | URL schemes, routing | Provider-specific handling | |
| | Deep link security | 1.0 | 20% | 1.2 | Medium | Signature validation | Security-critical | |
| **Auth & Onboarding** | Registration API | 2.0 | 20% | 2.4 | Medium | User model design | Standard CRUD | Max 1 email OR 1 phone per account. Don't support social login (Google/Apple). Password: min 8 chars, 1 uppercase, 1 number |
| | Registration UI | 1.5 | 20% | 1.8 | Medium | Design assets | Form validation | |
| | Email verification | 1.5 | 20% | 1.8 | Medium | Email service setup | Provider integration | OTP valid 5 minutes. Max 3 resend/hour. Max 5 wrong attempts → lock 15 min |
| | Login API | 1.5 | 20% | 1.8 | Medium | JWT setup | Session management | Max 5 failed attempts → lock 30 min. Session timeout 30 min inactive |
| | Login UI | 1.0 | 20% | 1.2 | Medium | Design assets | Biometric integration | |
| | Merchant onboarding API | 3.0 | 30% | 3.9 | Low | KYC requirements unclear | Complex data model | Max 1 business per merchant account. Required fields: business name, address, contact, category. Category: predefined list (max 20 options). No edit after submit. Must contact support to change. 3 statuses: pending, approved, rejected. No detailed rejection reason displayed (generic message only) |
| | Merchant onboarding UI | 2.5 | 30% | 3.3 | Low | Multi-step form complexity | Document upload | Max 3 documents. Max 10MB/file. Formats: PDF, JPG, PNG only |
| | Bank account linking API | 2.0 | 20% | 2.4 | Medium | OB provider integration | Account verification | Only support UK bank accounts. Max 1 bank account per merchant |
| | Bank selection API | 1.5 | 20% | 1.8 | Medium | Provider aggregation | Bank list management | Aggregate from all configured providers. Cache in Redis (TTL 24h). Filter UK payment-enabled banks only. Include provider mapping per bank |
| | Bank selection UI | 2.0 | 20% | 2.4 | Medium | Design assets | Bank list display | Top 20 UK retail banks initially. Bank list cached 24h locally. Search by bank name only. Must display bank logo and name. Grid layout (2-3 columns). Loading skeleton while fetching. Include "Can't find your bank?" help link |
| **Payment Flows** | QR generation API | 1.0 | 20% | 1.2 | Medium | Payment session model | Standard API | Dynamic QR only (amount included). QR valid 15 minutes. Max amount: £10,000. Min amount: £0.01 |
| | QR display UI | 0.5 | 10% | 0.6 | High | QR library | Simple display | |
| | Scan QR & parse | 1.5 | 20% | 1.8 | Medium | Camera integration | Error handling | 4 error types: expired, invalid_format, invalid_signature, merchant_inactive |
| | TrueLayer integration | 4.0 | 40% | 5.6 | Low | New integration | API learning curve | |
| | Token.io integration | 4.0 | 40% | 5.6 | Low | New integration | API learning curve | |
| | Yapily integration | 4.0 | 40% | 5.6 | Low | New integration | API learning curve | |
| | Payment initiation API | 2.0 | 30% | 2.6 | Low | Provider routing logic | Complex error handling | Single payment only (no recurring). GBP only. UK banks only. Max £10,000, Min £0.01. Payment session expires 15 minutes after QR scan. Idempotency required (use QR reference). Request timeout 30s. Must validate QR HMAC signature. Only approved merchants can receive payments |
| | Payment status polling | 2.0 | 30% | 2.6 | Low | Provider APIs vary | Polling strategy | |
| | Payment initiation UI | 2.0 | 20% | 2.4 | Medium | Design, provider selection | User flow complexity | Must display regulatory disclaimer for PISPs. Show "Powered by [Provider]" badge. Amount not editable after QR scan |
| | Payment status UI | 1.5 | 20% | 1.8 | Medium | Real-time updates | WebSocket or polling | WebSocket preferred, polling fallback (every 5s). Play sound/vibration on new payment. Show in-app notification banner |
| | OB redirect handling | 2.0 | 30% | 2.6 | Low | Deep links, WebView | Provider-specific flows | CRITICAL: Must open in external browser, NOT WebView (banks block WebView for security). Redirect timeout: 30 seconds. If user doesn't complete → auto cancel. Show interstitial before redirect. Show bank logo on interstitial. Include security message. Auto-redirect after 2-3 seconds or on tap. Support success/cancel/error scenarios. Handle app killed during redirect. Requires Universal Links (iOS) + App Links (Android) |
| **Transaction Management** | Transaction list API | 2.0 | 20% | 2.4 | Medium | Pagination, filtering | Standard API | |
| | Transaction history UI | 2.5 | 20% | 3.0 | Medium | Design, filters | List complexity | |
| | Transaction detail API | 1.0 | 10% | 1.1 | High | Simple retrieval | Standard API | |
| | Transaction detail UI | 1.0 | 20% | 1.2 | Medium | Design assets | Receipt generation | Show loading while verifying. Clearly distinguish success/failure/cancelled states. Success: show amount, merchant, reference, timestamp. Failure: generic error only (no technical details). Include support contact on failure. Animation for success. User-friendly error messages. Include share/screenshot option |
| **Merchant Dashboard** | Dashboard API | 2.0 | 30% | 2.6 | Low | Aggregation logic | Performance considerations | |
| | Dashboard UI | 3.0 | 30% | 3.9 | Low | Charts, design | Complex UI | |
| | Settings API | 1.0 | 20% | 1.2 | Medium | Preference model | Standard CRUD | |
| | Settings UI | 1.5 | 20% | 1.8 | Medium | Design assets | Multiple screens | Logout single device only (not logout all devices) |
| **Backend Infrastructure** | PostgreSQL schema | 2.0 | 20% | 2.4 | Medium | Data modeling | Index optimization | |
| | Database migrations | 1.0 | 20% | 1.2 | Medium | Migration tools | Version control | |
| | Redis setup | 1.0 | 20% | 1.2 | Medium | Infrastructure | Configuration | |
| | Session management | 1.5 | 20% | 1.8 | Medium | Redis integration | TTL management | |
| | JWT middleware | 1.5 | 20% | 1.8 | Medium | Auth library | Token refresh | |
| | Webhook HMAC verification | 2.0 | 30% | 2.6 | Low | Provider-specific | Security-critical | Webhook processing <5 seconds. Idempotency using event ID (Redis TTL 24h). Must verify signature per provider |
| | Secrets management | 1.0 | 20% | 1.2 | Medium | Cloud provider | Setup complexity | |
| **Observability & QA** | Structured logging | 1.0 | 20% | 1.2 | Medium | Logging library | Correlation IDs | |
| | Error tracking | 1.0 | 20% | 1.2 | Medium | Sentry setup | Integration | |
| | Metrics collection | 1.5 | 30% | 2.0 | Low | Monitoring setup | Cloud provider | |
| | Health checks | 0.5 | 10% | 0.6 | High | Standard endpoints | Simple | |
| | Unit tests (Backend) | 4.0 | 20% | 4.8 | Medium | Test coverage target | Critical paths | |
| | Unit tests (Mobile) | 3.0 | 20% | 3.6 | Medium | Test coverage target | Critical paths | |
| | Integration tests | 3.0 | 30% | 3.9 | Low | Provider sandboxes | Test data setup | |
| | E2E tests | 3.0 | 30% | 3.9 | Low | Test framework | Device testing | |
| | Test plan creation | 2.0 | 20% | 2.4 | Medium | Requirements | Documentation | |
| | Manual testing | 4.0 | 20% | 4.8 | Medium | Device matrix | Exploratory | |

### Totals

- **Base total:** 85.5 PD
- **Buffer total:** 19.0 PD (average ~22%)
- **Buffered total:** 104.5 PD
- **Critical path:**
  1. App foundation → Security setup → Auth flows
  2. Open Banking integrations (longest, highest risk)
  3. Payment flows → Transaction management
  4. Backend infrastructure (parallel with frontend)
  5. QA/testing (ongoing, but final E2E critical)

**Team Assumptions:**

- 2 Mobile developers (Flutter)
- 2 Backend developers (NestJS)
- 1 DevOps engineer
- 1 QA engineer
- Estimated velocity: ~20 PD/week across team
- **Timeline:** ~5-6 weeks with full team (104.5 PD ÷ 20 PD/week)

## Risks & Mitigations

1. **Open Banking Integration Complexity (High Risk)**
   - **Risk:** Each provider has different APIs, webhook formats, error handling
   - **Mitigation:** Start with one provider (TrueLayer), establish patterns, then replicate. Use provider sandboxes early. Buffer applied (40%)

2. **Security Requirements (Medium-High Risk)**
   - **Risk:** SSL pinning, jailbreak detection may require custom native code
   - **Mitigation:** Research plugins early, allocate time for custom implementation if needed. Security review checkpoint.

3. **Merchant Onboarding Complexity (Medium Risk)**
   - **Risk:** KYC requirements may be unclear, document upload complexity
   - **Mitigation:** Clarify requirements early, design flexible data model, use file storage service (S3/Azure Blob)

4. **Provider API Changes (Medium Risk)**
   - **Risk:** OB providers may update APIs during development
   - **Mitigation:** Version API clients, monitor provider changelogs, abstract provider differences

5. **App Store Review (Medium Risk)**
   - **Risk:** First submission may face review delays or rejections
   - **Mitigation:** Follow guidelines strictly, submit early for review, have fallback plan

6. **Performance at Scale (Low-Medium Risk)**
   - **Risk:** Payment status polling may not scale
   - **Mitigation:** Design for WebSocket/SSE if needed, load test early

## Non-Functional & Compliance

- **Security:**
  - SSL pinning on mobile apps
  - Jailbreak/root detection
  - Webhook HMAC/JWT verification
  - Secrets in AWS Secrets Manager / Azure Key Vault
  - JWT with refresh tokens
  - TLS 1.2+ for all API calls
  - Secure storage for biometric data

- **Performance/Availability:**
  - API response time: <500ms (p95)
  - Mobile app startup: <2s
  - QR scanner opens: <1s
  - Payment status updates: Real-time (polling or WebSocket)
  - Uptime target: 99.5% (SLA with providers)
  - Database connection pooling
  - Redis caching for session data

- **Observability:**
  - Structured logging with correlation IDs
  - Metrics: API latency, error rates, payment success rates
  - Error tracking (Sentry)
  - Health check endpoints
  - Alerting for critical failures (payment failures, API errors)

- **Compliance/Privacy:**
  - GDPR: User data export, deletion, consent management
  - Data retention policies (transaction data: 7 years for tax)
  - Privacy policy and terms of service
  - Cookie consent (if web components)
  - PCI-DSS considerations (if storing card data - not applicable for OB)

## Open Questions

1. **KYC Requirements:** What level of KYC is required for merchants? Document types?
2. **Payment Limits:** Are there transaction limits per merchant/user?
3. **Refund Policy:** How are refunds handled? Manual or automated?
4. **Multi-Provider Selection:** Can users choose OB provider, or auto-select?
5. **Offline Mode:** Should app work offline (view history) or require connectivity?
6. **Analytics:** What user analytics are needed? Privacy-compliant tracking?
7. **Support:** In-app support chat or email only?
8. **Localization:** English only for MVP, or multiple languages?
