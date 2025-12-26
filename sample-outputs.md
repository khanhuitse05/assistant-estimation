# Estimation Example

## Scope Summary

* **Context:** Core authentication and onboarding features for a mobile payment application, supporting end users and merchants.
* **Goals:**

  * Enable account registration, login, logout, and password recovery
  * Support secure authentication flows (OTP, biometric login)
  * Allow merchants to complete onboarding and access QR payment features
* **Out of scope:**

  * Social login (Google, Apple, etc.)
  * Advanced fraud detection or risk scoring
  * Multi-device session management
  * Complex role-based permission management beyond current scope

## Assumptions

* A shared design system and UI guidelines are available
* Email/SMS services for OTP and password reset are configured and accessible
* Backend API infrastructure and authentication framework are already in place
* Mobile application is built using Flutter (mobile-first), not responsive web
* Open Banking providers (e.g. TrueLayer / Token.io / Yapily) are available for integration

## Estimation Table

| No | Features / Modules   | User stories                                                         | **Task**                                                      | Type        | Complexity | Core feature | Optimistic | Pessimistic | Average | Milestone | Restriction        | Note                                   |
| -- | -------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------- | ----------- | ---------- | ------------ | ---------- | ----------- | ------- | --------- | ------------------ | -------------------------------------- |
| 1  | Kick off             | As a developer I want to setup a Flutter project                     | Initialize Flutter project structure, environments, CI basics | FE - Mobile | Low        | FALSE        | 0.5        | 1           | 0.75    | 1         |                    |                                        |
| 2  |                      | As a developer I want to setup a BE project                          | Setup backend project, base architecture, env configs         | API         | Low        | FALSE        | 0.5        | 1           | 0.75    | 1         |                    |                                        |
| 3  | Splash screen        | As a user, I want to see a splash screen when the app is launched    | Implement splash screen with branding and loading logic       | FE - Mobile | Low        | FALSE        | 0.25       | 0.5         | 0.375   | 1         |                    |                                        |
| 4  |                      | UI                                                                   | Design and implement splash screen UI                         | UI          | Low        | FALSE        | 0.25       | 0.5         | 0.375   | 1         |                    |                                        |
| 5  | Registration & login | As a user, I want to register an account using my email/phone number | Implement registration flow, form validation, API integration | FE - Mobile | Medium     | TRUE         | 0.5        | 1           | 0.75    | 1         | No social login    | Extra estimation if Google/Apple added |
| 6  |                      | API                                                                  | Implement registration APIs, validation, persistence          | API         | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 7  |                      | UI                                                                   | Build registration screens and input components               | UI          | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 8  |                      | As a user, I want to verify my identity via OTP                      | Implement OTP input, resend logic, error handling             | FE - Mobile | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 1         | OTP rules          | Lock after invalid attempts            |
| 9  |                      | API                                                                  | Implement OTP generation, validation, rate limiting           | API         | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 10 |                      | UI                                                                   | Design OTP input UI and error states                          | UI          | Medium     | FALSE        | 0.25       | 0.5         | 0.375   | 1         |                    |                                        |
| 11 |                      | As a user, I want to log in using email/phone & password             | Implement login flow, session handling, error cases           | FE - Mobile | Medium     | TRUE         | 0.5        | 0.75        | 0.625   | 1         | Security rules     | Lock, session timeout                  |
| 12 |                      | API                                                                  | Implement login API, auth token, lock logic                   | API         | Medium     | TRUE         | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 13 |                      | UI                                                                   | Build login screen and validation UI                          | UI          | Medium     | FALSE        | 0.25       | 0.5         | 0.375   | 1         |                    |                                        |
| 14 |                      | As a user, I want to log in using biometrics                         | Integrate FaceID / TouchID / Android biometrics               | FE - Mobile | High       | FALSE        | 0.75       | 1.25        | 1       | 1         | Enable after login | Follow native APIs                     |
| 15 |                      | UI                                                                   | Add biometric toggle and status UI                            | UI          | Medium     | FALSE        | 0.25       | 0.75        | 0.5     | 1         |                    | Use `local_auth`                       |
| 16 |                      | As a user, I want to reset my password                               | Implement forgot-password flow                                | FE - Mobile | Medium     | TRUE         | 0.25       | 0.5         | 0.375   | 1         | Rate limit         | Link expiry                            |
| 17 |                      | API                                                                  | Implement password reset APIs and token validation            | API         | Medium     | TRUE         | 0.25       | 0.5         | 0.375   | 1         |                    |                                        |
| 18 |                      | UI                                                                   | Build reset password screens                                  | UI          | Low        | FALSE        | 0.25       | 0.5         | 0.375   | 1         |                    |                                        |
| 19 |                      | As a user, I want to log out                                         | Implement logout and token cleanup                            | FE - Mobile | Low        | FALSE        | 0.25       | 0.25        | 0.25    | 1         | Single device      |                                        |
| 20 |                      | API                                                                  | Invalidate session/token on logout                            | API         | Low        | FALSE        | 0.25       | 0.25        | 0.25    | 1         |                    |                                        |
| 21 | Merchant Onboarding  | As a merchant, I want to submit my business info                     | Implement onboarding form and submission flow                 | FE - Mobile | Medium     | TRUE         | 0.75       | 1           | 0.875   | 1         | Business rules     | Category predefined                    |
| 22 |                      | API                                                                  | Store and validate merchant business data                     | API         | Medium     | TRUE         | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 23 |                      | UI                                                                   | Design onboarding forms and review screens                    | UI          | Medium     | FALSE        | 0.75       | 1           | 0.875   | 1         |                    |                                        |
| 24 |                      | As a merchant, I want to upload documents                            | Implement document upload & preview                           | FE - Mobile | High       | FALSE        | 0.75       | 1           | 0.875   | 1         | File limits        | PDF/JPG/PNG                            |
| 25 |                      | API                                                                  | Handle file upload, validation, storage                       | API         | High       | FALSE        | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 26 |                      | UI                                                                   | Build document upload UI                                      | UI          | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 1         |                    |                                        |
| 36 | QR Payments          | As a merchant, I want to generate a QR code                          | Generate dynamic QR and display for payment                   | FE - Mobile | Medium     | TRUE         | 0.5        | 0.75        | 0.625   | 2         | Amount rules       | Open Banking                           |
| 37 |                      | API                                                                  | Generate QR payload and payment intent                        | API         | High       | TRUE         | 1          | 1.5         | 1.25    | 2         |                    |                                        |
| 38 |                      | UI                                                                   | Display QR code and expiry status                             | UI          | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 2         |                    |                                        |
| 39 |                      | As a user, I want to scan a QR code                                  | Implement QR scanning via camera                              | FE - Mobile | High       | TRUE         | 1          | 1.5         | 1.25    | 2         | iPay only          | Camera permission                      |
| 46 | Push notifications   | As a user, I want to receive notifications                           | Integrate FCM and handle notification events                  | FE - Mobile | Medium     | FALSE        | 0.5        | 0.75        | 0.625   | 2         | Rate limit         | Store token                            |
| 53 | Setting              | As a user, I want to delete my account                               | Implement account deletion flow                               | FE - Mobile | Medium     | FALSE        | 0.25       | 0.75        | 0.5     | 2         | Soft delete        | App Store requirement                  |
| 58 | Deep Linking         | As a developer, I need deep links                                    | Configure deep links for Open Banking callbacks               | FE - Mobile | Medium     | TRUE         | 0.5        | 1           | 0.75    | 2         | 2 patterns         |                                        |
| 59 | Deploying            | As a developer, I want to submit the app                             | Prepare builds & submit to stores                             | FE - Mobile | Medium     | TRUE         | 0.75       | 1.5         | 1.125   | 2         |                    |                                        |
| 60 |                      | As a developer, I need to deploy backend                             | Deploy backend to UK/EU region                                | API         | Medium     | TRUE         | 0.75       | 1.5         | 1.125   | 2         | GDPR               | Single AZ                              |
