# **iPay QR App Shell MVP**

The client requires a **lightweight App (hybrid app, Flutter app)** for both iOS and Android to enable rapid market launch of iPay QR. The app will serve primarily as a secure container enabling **store presence, device-level features**, and **Open Banking payment flows**.

## Tech stack

- Mobile: Flutter  
- BE: NestJS

### **Key Requirements**

### **1. App & Service**

- Create a Flutter app for iOS & Android.
- Include:  
  - Permissions manager (camera, notifications)  
  - QR code scanning via native camera  
  - Biometric login (FaceID/TouchID/Android Biometrics)  
  - Deep linking for Open Banking redirects  
  - Security features (SSL pinning, disable screenshots, jailbreak/root detection)

### **2. Main Product UI**

- User onboarding & authentication  
- QR payment page  
- Merchant dashboard  
- Transaction history  
- Settings & support  
- Must be mobile-responsive and optimized.

### **3. Backend & Integrations**

- Hosted in UK/EU region (AWS London or Azure UK)  
- Integrate with Open Banking providers:  
  - TrueLayer  
  - Token.io  
  - Yapily  
- Database: PostgreSQL  
- Caching/Sessions: Redis

### **4. MVP Features**

#### **Native:**

- Splash screen  
- Secure container  
- QR scanner  
- Biometric authentication  
- Deep linking  
- Push notifications (later phase)

#### **Flutter App:**

- Registration & login  
- Merchant onboarding  
- Generate and scan QR codes for payments  
- Payment initiation via Open Banking  
- Transaction history  
- Merchant portal

### **5. Security & Compliance**

- TLS 1.2+, HSTS  
- SSL certificate pinning  
- WebView file access disabled  
- Jailbreak/root detection  
- GDPR compliance  
- Secure secrets management (AWS Secret Manager / Azure Key Vault)  
- Webhook verification (HMAC/JWT)

### **8. Client’s Preferred Strategy**

**Cross-platform App, MVP Backend**  
→ Faster launch, lower cost, strong marketing presence, easy updates, and full App Store/Play Store visibility.
