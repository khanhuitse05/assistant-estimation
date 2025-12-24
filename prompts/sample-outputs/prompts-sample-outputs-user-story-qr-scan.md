# User Story: QR Code Scanning for Payment Initiation

- As a **merchant**, I want to **scan a customer's QR code to initiate a payment**, so that **I can collect funds quickly without manual data entry**.

## Context / Preconditions

- The app uses native camera APIs via Flutter plugins (camera package)
- QR codes contain payment initiation data: amount, payer ID, transaction reference, merchant ID
- Camera permissions must be requested at runtime (iOS/Android)
- QR codes follow a standardized format (JSON payload with signature)
- User is logged in and authenticated

## Acceptance Criteria (Given / When / Then)

1. **Happy Path - Successful Scan:**
   - Given camera permission is granted, when I tap "Scan QR Code", then the native camera scanner opens within 1s and displays the camera viewfinder
   - Given a valid QR code is scanned with correct format, when the scanner detects it, then the payment initiation screen opens with pre-filled amount, payer ID, and transaction reference, and I can review details before confirming

2. **Error Handling - Invalid QR:**
   - Given an invalid QR code format is scanned, when detected, then I see error message "Invalid QR code format. Please try again." with a "Retry" button that reopens the scanner
   - Given an expired QR code (timestamp > 5 minutes old) is scanned, when detected, then I see error message "This QR code has expired. Please request a new one." with option to retry
   - Given a QR code with invalid signature is scanned, when detected, then I see error message "QR code verification failed. Please try again." with retry option

3. **Permission Handling:**
   - Given camera permission is not yet granted, when I tap "Scan QR Code", then I see a permission request dialog explaining why camera access is needed, with "Allow" and "Not Now" options
   - Given camera permission was previously denied, when I tap "Scan QR Code", then I see a message "Camera access is required. Please enable it in Settings." with a button that opens device Settings to the app's permission page

4. **Hardware/Environment Errors:**
   - Given camera hardware is unavailable (device has no camera), when I tap "Scan QR Code", then I see error message "Camera not available on this device" and the option is disabled
   - Given camera is already in use by another app, when I tap "Scan QR Code", then I see error message "Camera is in use. Please close other apps using the camera." with retry option
   - Given low lighting conditions prevent QR detection, when scanning, then I see a hint "Move to better lighting" and the scanner continues attempting to detect

5. **Navigation & UX:**
   - Given I am on the payment initiation screen from QR scan, when I tap "Cancel", then I return to the previous screen without initiating payment
   - Given I successfully scan a QR code, when the payment initiation screen opens, then I can see all payment details clearly and modify amount if needed (if merchant allows amount override)

## Non-Functional

- **Performance/availability:**
  - Scanner opens within 1s on devices with camera access (p95)
  - QR detection works in normal indoor lighting conditions (≥200 lux)
  - Scanner processes QR codes up to 2MB in size
  - App remains responsive during scanning (no UI freezing)

- **Security/privacy:**
  - Scanner respects app security policy: screenshots disabled during active scanning
  - QR code data is validated before processing (signature verification)
  - No QR code data is stored locally after successful payment initiation
  - Camera feed is not recorded or transmitted

- **Accessibility:**
  - Scanner screen is accessible via screen readers (announces "Camera viewfinder active")
  - Error messages are announced to screen readers
  - High contrast mode supported for camera overlay UI
  - Supports system font scaling

## Dependencies

- **Upstream:**
  - Camera plugin (camera package) - Flutter plugin for native camera access
  - QR code parsing library (qr_code_scanner or mobile_scanner)
  - Payment initiation API endpoint (must be ready before UI integration)
  - QR code format specification document

- **Credentials/Environments:**
  - Camera permissions configured in iOS Info.plist and Android AndroidManifest.xml
  - Test QR codes for various scenarios (valid, invalid, expired)

- **Other Stories:**
  - Payment initiation screen must be implemented first
  - Authentication/login flow must be complete

## Tests

- **Unit:**
  - QR code parsing logic with various payload formats
  - Signature validation algorithm
  - Expiration timestamp checking
  - Error message generation for different error types

- **Integration:**
  - Camera plugin integration (mock camera for CI)
  - API call with parsed QR data to payment initiation endpoint
  - Permission flow handling (mock permission responses)
  - Deep link handling if QR contains deep link URL

- **Manual/Exploratory:**
  - Test on physical devices (iOS and Android)
  - Various lighting conditions (bright, dim, outdoor)
  - Different QR code sizes and distances
  - Permission denial scenarios
  - Network interruption during scan
  - Multiple rapid scans
  - QR codes with special characters in payload
