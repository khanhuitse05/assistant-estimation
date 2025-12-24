# Estimation Example: Hierarchical Table Format

## Scope Summary

- **Context:** Basic authentication system for a ride-sharing app with user and chauffeur roles
- **Goals:** Enable users and chauffeurs to register, login, and reset passwords
- **Out of scope:** Social login, two-factor authentication, password strength meter UI

## Assumptions

- Shared design system exists for UI components
- Email service configured and available
- Backend API framework already set up
- Mobile app uses responsive web views (not native)

## Estimation Table (person-days)

| Feature / Epic | User Story | Task | Platform | Difficulty | Core Feature | Min (PD) | Max (PD) | Avg (PD) | Milestone | Restriction |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Basic Sign Up / Login | As a user/chauffeur, I want to register with my email and password so that I can create an account and use the app. | Registration screen (shared design system, web + mobile layouts) | UI | Medium | FALSE | 1 | 1.25 | 1.125 | 1 | |
| | | Registration form + validation | FE - Web | Medium | FALSE | 1 | 1.5 | 1.25 | 1 | Max 1 email OR 1 phone per account. Don't support social login (Google/Apple). Password: min 8 chars, 1 uppercase, 1 number |
| | | Registration screen + validation (mobile optimized) | FE - Mobile | Medium | FALSE | 1 | 1.5 | 1.25 | 1 | |
| | | POST /auth/register → accept user role (user or chauffeur) | API | Medium | FALSE | 0.75 | 1 | 0.875 | 1 | |
| | As a user/chauffeur, I want to log in with my email and password so that I can access my account. | Login screen (shared design system) | UI | Medium | FALSE | 0.25 | 0.5 | 0.375 | 1 | |
| | | Login form + validation | FE - Web | Medium | FALSE | 0.75 | 1 | 0.875 | 1 | |
| | | Login form + validation | FE - Mobile | Medium | FALSE | 0.75 | 1 | 0.875 | 1 | |
| | | POST /auth/login → validate credentials | API | Medium | FALSE | 0.5 | 0.75 | 0.625 | 1 | Max 5 failed attempts → lock 30 min. Session timeout 30 min inactive |
| | As a user/chauffeur, I want to reset my password via email so that I can regain access if I forget it. | Reset password screen (new password) | UI | Medium | FALSE | 0.25 | 0.5 | 0.375 | 1 | |
| | | Forgot password form. Handle reset link page (token in URL) | FE - Web | Medium | FALSE | 0.5 | 0.75 | 0.625 | 1 | Max 3 reset requests/hour. Reset link valid 1 hour |
| | | Forgot password form. Open reset link in external browser or deep-link to app | FE - Mobile | Medium | FALSE | 0.5 | 0.75 | 0.625 | 1 | |
| | | POST /auth/reset-password → validate token & update password | API | Medium | FALSE | 0.25 | 0.5 | 0.375 | 1 | |

### Totals

- **Total Min:** 7.75 PD
- **Total Max:** 10.5 PD
- **Total Avg:** 9.125 PD
- **Total Final:** 10 PD
- **Critical path:** UI design → FE implementation → API endpoints (sequential dependencies)

**Team & Timeline:**

- Team composition: 1 UI designer, 2 FE developers (web + mobile), 1 BE developer
- Estimated velocity: 10 PD per week
- Estimated timeline: 1 week (10 PD ÷ 10 PD/week)

## Non-Functional & Compliance

- **Security:**
  - Password hashing (bcrypt/argon2)
  - Email verification tokens expire after 24 hours
  - Rate limiting on login attempts (5 attempts per 15 minutes)
  - HTTPS only for all auth endpoints

- **Performance/Availability:**
  - Login API response time: <200ms (p95)
  - Registration API response time: <500ms (p95)
  - Email delivery: async processing with retry logic

- **Observability:**
  - Log all authentication attempts (success/failure)
  - Track registration conversion rates
  - Monitor failed login attempts for security alerts

- **Compliance/Privacy:**
  - GDPR: User consent for account creation
  - Store only necessary user data
  - Password reset emails must not expose user information

## Open Questions

- Should password reset tokens be single-use or multi-use?
- What is the minimum password complexity requirement?
- Should we implement account lockout after failed attempts?
