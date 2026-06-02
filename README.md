## Disclaimer

This project is intended for **educational and research purposes only**.

I am a student and an active user of the MyNIAT platform. This repository does not contain any proprietary source code, sensitive information, or confidential data from the original application.

All analysis is based on publicly accessible application binaries and is shared solely to demonstrate learning in:
- Reverse engineering techniques
- Mobile app architecture
- Security analysis and concepts

**This project is not affiliated with, endorsed by, or associated with NxtWave or MyNIAT.**

**WARNING**: This content is for **educational purposes only**. Do not use this information for any unauthorized activities. Use at your own risk.
---

<div align="center">

![jadx](https://img.shields.io/badge/jadx-1.5.5-blue?style=flat-square)
![React Native](https://img.shields.io/badge/React_Native-0.76-black?style=flat-square&logo=react)
![Expo](https://img.shields.io/badge/Expo-52-white?style=flat-square&logo=expo)
![Firebase](https://img.shields.io/badge/Firebase-Console-orange?style=flat-square&logo=firebase)
![Android](https://img.shields.io/badge/Android-SDK_35-green?style=flat-square&logo=android)
![AWS](https://img.shields.io/badge/AWS-S3-orange?style=flat-square&logo=amazon-aws)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=flat-square&logo=typescript)
![Hermes](https://img.shields.io/badge/Hermes-Engine-blueviolet?style=flat-square)
![Visitors](https://visitor-badge.laobi.icu/badge?page_id=Yashwanth-Kumar-26.myniat-reverse-engineering)
</div>

---
## Contributors

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/Yashwanth-Kumar-26">
        <img src="https://github.com/Yashwanth-Kumar-26.png" width="100px;" alt="Yashwanth Kumar"/><br />
        <sub><b>Yashwanth Kumar</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/saiadarsh-03">
        <img src="https://github.com/saiadarsh-03.png" width="100px;" alt="Sai Adarsh"/><br />
        <sub><b>Sai Adarsh</b></sub>
      </a>
    </td>
  </tr>
</table>

## Table of Contents

1. [App Overview](#app-overview)
2. [Key API Endpoints Discovered](#key-api-endpoints-discovered)
3. [Architecture & Technologies](#architecture--technologies)
4. [Security & Permissions](#security--permissions)
5. [File Structure](#file-structure)
6. [Security Observations](#security-observations)
7. [API Call Flow Examples](#api-call-flow-examples)
8. [Dependencies](#dependencies)
9. [Network Configuration](#network-configuration)
10. [Decompilation Notes](#decompilation-notes)
11. [Troubleshooting](#troubleshooting)
12. [Conclusion](#conclusion)

---

# MyNIAT Android App - Reverse Engineering Analysis

## App Overview

**MyNIAT** (NxtWave Student App) - Version 1.0.37
- **Package**: `tech.nxtwave.myniat` (Beta: `tech.nxtwave.myniat_beta`)
- **Architecture**: React Native with Expo
- **Platform**: Android (min SDK 24, target SDK 35)
- **Decompilation Date**: 2026-04-26
- **File**: `nxt.xapk`

## Key API Endpoints Discovered

### Main Backend APIs

#### Student Backend
**Base URL**: `https://niat-student-backend-prod-apis.ccbp.in/api/v1/`

- **Activities by Month**: `/api/v1/activitiesByMonthActivitiesWrapper`
- **Calendar Attendance**: `/calendar/attendance/details`
- **Academic Calendar**: `/academic_calendar/v1/get-ice-server-config`

#### User Account APIs
**Base URL**: `https://ib-user-accounts-backend-prod-apis.ccbp.in/api/`

- **Login**: `POST /user/login/phone_number/v1`
- **Logout**: `POST /user/logout/v1`
- **Profile**: `GET /user/profile/v1`
- **Device Registration**: `POST /user/register_device`
- **Mark Attendance**: `POST /user/mark_attendance`
- **Monthly Attendance**: `GET /user/month/attendance`
- **Attendance Slots**: `GET /user/attendance_slots`

### Support & Features APIs

- **Support Assistant**: `POST /support/assistant/query`
- **Support Ticket Details**: `GET /support/support_ticket/details`
- **Ticket Categories**: `GET /support/support_tickets/categories`
- **Create Ticket**: `POST /support/user/create_ticket/v1`
- **Mark All Read**: `POST /notifications/mark_all_as_read/v1`
- **Unread Count**: `GET /notifications/unread/count/v1`

### Additional Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/user/dashboard/v1` | User dashboard data |
| GET | `/user/courses/v1` | Enrolled courses list |
| POST | `/user/fcm_token/update` | Update FCM token |
| GET | `/academics/grades/v1` | Academic grades |
| GET | `/attendance/history` | Attendance history |
| POST | `/user/logout/all` | Logout all devices |
| GET | `/announcements/v1` | System announcements |

### Media & Static Content

**S3 Media Base**: `https://niat-core-backend-media-static.s3.ap-south-1.amazonaws.com/`

- **Android App Version**: `/beta/student_platform_static/appversion/prod/android/app_version.json`
- **iOS App Version**: `/beta/student_platform_static/appversion/prod/ios/app_version.json`
- **Invite & Earn**: `/prod/student_platform_static/invite_and_earn.json`
- **Student Events**: `/prod/student_platform_static/student_event.json`

### Other Services

- **Rewards Program**: `https://nxtrewards.ccbp.in/invite-and-earn?source_program=niat`
- **Learning Platform**: `https://learning.ccbp.in/edit-profile`
- **Privacy Policy**: `https://www.ccbp.in/privacy-policy`
- **Terms of Use**: `https://www.niatindia.com/terms-of-use`

## Architecture & Technologies

### Core Framework
- **React Native** with Expo Router
- **New Architecture** enabled (Fabric/TurboModules)
- **Hermes** JavaScript engine
- **TypeScript** support

### Third-Party Services

#### Firebase Integration
- Firebase Messaging (Push Notifications)
- Firebase Analytics
- Firebase Installations
- Project ID: `niat-student-platform-prod`

#### Analytics & Monitoring
- **WebEngage**: User engagement and analytics
  - License Key: `EXPO_PUBLIC_WEBENGAGE_LICENCE_KEY`
- **Sentry**: Error tracking and performance monitoring
  - DSN: `https://1155ed95f40782019edf777d5a28fc58@o1177444.ingest.us.sentry.io/4509665171537920`
  - Project: `niat-student-platform-prod`
- **Microsoft Clarity**: User behavior analytics

#### Cloud Services
- **AWS S3**: Static content hosting (ap-south-1 region)
- **CloudFront**: CDN distribution

### Key Features

#### 1. Attendance Tracking
- GPS-based attendance marking
- Location services integration
- Monthly attendance reports
- Attendance slot management

#### 2. AI Assistant
- Speech recognition for voice queries
- Natural language processing
- Context-aware responses for academics, attendance, and schedule
- Uses Google's speech recognition service

#### 3. Academic Calendar
- Backend calendar integration
- ICE server configuration for WebRTC
- Activity tracking by month
- Academic event management

#### 4. Support System
- Ticket-based support system
- Categorized support tickets
- AI-powered support assistant
- Real-time notifications

#### 5. Profile Management
- User profile management
- Device registration and management
- Biometric authentication support
- Multi-device support

#### 6. Notifications
- Firebase Cloud Messaging
- Push notification support
- Notification categories
- Read/unread status tracking

#### 7. Rewards Program
- Invite and earn functionality
- Referral tracking
- Source program attribution

## Security & Permissions

### Required Permissions

#### Network & Connectivity
- `INTERNET` - Required for API calls
- `ACCESS_NETWORK_STATE` - Network status monitoring
- `ACCESS_WIFI_STATE` - WiFi connectivity

#### Location Services
- `ACCESS_FINE_LOCATION` - Precise location for attendance
- `ACCESS_COARSE_LOCATION` - Approximate location
- `NEARBY_WIFI_DEVICES` - WiFi-based location

#### Audio & Speech
- `RECORD_AUDIO` - Voice input for AI assistant

#### Storage
- `READ_EXTERNAL_STORAGE` - File access (max SDK 32)
- `WRITE_EXTERNAL_STORAGE` - File storage

#### Biometrics
- `USE_BIOMETRIC` - Biometric authentication
- `USE_FINGERPRINT` - Fingerprint authentication

#### System
- `POST_NOTIFICATIONS` - Push notifications
- `VIBRATE` - Haptic feedback
- `WAKE_LOCK` - Background operations
- `FOREGROUND_SERVICE` - Background services
- `SYSTEM_ALERT_WINDOW` - Overlay permissions
- `RECEIVE_BOOT_COMPLETED` - Auto-start on boot

### Security Features

#### Authentication
- Firebase token-based authentication
- Phone number verification
- OTP-based login system
- Session management

#### Data Protection
- Network security configuration
- SSL/TLS encryption
- Biometric authentication support
- Secure token storage

#### License Verification
- PairIP license checking system
- License activity and content provider
- Anti-piracy measures

## File Structure

### Native Components

#### Main Activity
- **File**: `MainActivity.java`
- **Package**: `tech.nxtwave.myniat_beta`
- **Purpose**: React Native bridge and splash screen management
- **Features**:
  - Splash screen integration
  - React Native host configuration
  - Back button handling

#### Application Class
- **File**: `MainApplication.java`
- **Package**: `tech.nxtwave.myniat_beta`
- **Purpose**: Application initialization and service setup
- **Features**:
  - Firebase initialization
  - WebEngage integration
  - React Native host configuration
  - Package list management

#### Build Configuration
- **File**: `BuildConfig.java`
- **Package**: `tech.nxtwave.myniat_beta`
- **Version**: 1.0.37 (version code 37)
- **Build Type**: Production release

### JavaScript Bundle

#### Main Bundle
- **File**: `index.android.bundle`
- **Size**: Large minified React Native bundle
- **Purpose**: Contains all application logic
- **Features**:
  - React components
  - API integration
  - State management
  - Navigation logic

#### Configuration Files
- **app.config**: Expo configuration
- **app.manifest**: App manifest
- **clarity.js**: Microsoft Clarity analytics

### Resources

#### Android Manifest
- **Package**: `tech.nxtwave.myniat`
- **Activities**: MainActivity, FullscreenPlayerActivity
- **Services**: Multiple Firebase and background services
- **Receivers**: Firebase messaging receiver
- **Providers**: File providers, Firebase providers

#### Assets
- **Images**: Adaptive icons, splash screens
- **Certificates**: Expo root certificate
- **Fonts**: Roboto font family
- **Profiling**: Baseline profiles for optimization

## Security Observations

### 1. Multi-Environment Support
- Production and beta environments
- Separate Google Services configuration
- Environment-specific API endpoints
- Feature flag support

### 2. Speech Recognition
- Uses Google's speech recognition service
- Package: `com.google.android.googlequicksearchbox`
- Permission: `android.permission.RECORD_AUDIO`
- Purpose: AI assistant voice input

### 3. Location-Based Attendance
- Requires precise location permissions
- GPS and WiFi-based location
- Attendance slot management
- Monthly attendance tracking

### 4. Comprehensive Analytics
- Multiple analytics platforms integrated
- Firebase Analytics for user behavior
- WebEngage for engagement tracking
- Sentry for error monitoring
- Microsoft Clarity for user sessions

### 5. Modular Architecture
- Split APKs for different architectures
- Separate APKs for:
  - `config.arm64_v8a.apk` - 64-bit ARM
  - `config.armeabi_v7a.apk` - 32-bit ARM
  - `config.en.apk` - English resources
  - `config.xxhdpi.apk` - High-density screens
  - `tech.nxtwave.myniat.apk` - Main application

### 6. Performance Optimization
- Hermes JavaScript engine
- New Architecture (Fabric/TurboModules)
- Baseline profiles for faster startup
- Code splitting and lazy loading

### 7. Security Measures
- Network security configuration
- Biometric authentication
- License verification system
- Secure token management
- SSL pinning support
## Security Vulnerabilities Found
### 1. AndroidManifest Security Issues
- `allowBackup="true"` - Enables data extraction via ADB backup
- Deep link schemes (`my-niat`, `exp+my-niat`) exported without protection
- No root/jailbreak detection implemented
- SSL certificate pinning not visible in manifest
### 2. React Native Specific Vulnerabilities
- **JS Bundle Exposure**: `index.android.bundle` easily extracted (7.6 MB)
- **No Code Obfuscation**: Business logic fully visible in JavaScript
- **AsyncStorage Risk**: Sensitive data often stored in plaintext
- **Remote Updates**: `expo.modules.updates` could allow code injection
### 3. Third-Party SDK Risks
- **WebEngage SDK**: Known vulnerabilities in older versions
- **Firebase Services**: Multiple entry points increase attack surface
- **Sentry**: Debug mode may expose sensitive data
### 4. API Security Concerns
- Endpoints visible in JS bundle
- No visible rate limiting implementation
- Token storage mechanism unknown
- GPS spoofing possible for attendance
---
> **Note**: These are common patterns in React Native apps. For production hardening: implement root detection, disable backup, add SSL pinning, enable code obfuscation, and restrict exported components.

## API Call Flow Examples

### Authentication Flow
1. User enters phone number → POST /user/login/phone_number/v1 → OTP sent
2. User enters OTP → POST /user/login/phone_number/v1 (with OTP) → Auth token received
3. Token stored locally and services registered

### Attendance Marking Flow
1. User requests attendance marking
2. App gets GPS location → ACCESS_FINE_LOCATION permission
3. POST /user/mark_attendance with location data → Confirmed
4. GET /user/month/attendance → Monthly status updated

### Support Ticket Flow
1. User selects category → GET /support/support_tickets/categories
2. POST /support/user/create_ticket/v1 with details → Ticket ID received
3. User checks status → GET /support/support_ticket/details/{id} → Status displayed

## Dependencies

### React Native Libraries
- `@react-navigation/native` - Navigation
- `expo-router` - File-based routing
- `react-native-paper` - Material Design components
- `react-native-reanimated` - Animations
- `react-native-gesture-handler` - Gesture handling
- `react-native-screens` - Native screen optimization

### Firebase Libraries
- `@react-native-firebase/app` - Firebase core
- `@react-native-firebase/messaging` - Push notifications
- `@react-native-firebase/analytics` - Analytics
- `@react-native-firebase/installations` - App installations

### Expo Modules
- `expo-splash-screen` - Splash screen
- `expo-speech-recognition` - Speech recognition
- `expo-font` - Font loading
- `expo-video` - Video playback
- `expo-document-picker` - File selection
- `expo-web-browser` - In-app browser
- `expo-location` - Location services

### Third-Party Libraries
- `@sentry/react-native` - Error tracking
- `@microsoft/react-native-clarity` - Analytics
- `react-native-toast-message` - Toast notifications
- `react-native-webview` - Web content display

## Network Configuration

### Base URLs
- **Production**: `https://niat-student-backend-prod-apis.ccbp.in`
- **User Accounts**: `https://ib-user-accounts-backend-prod-apis.ccbp.in`
- **Media**: `https://niat-core-backend-media-static.s3.ap-south-1.amazonaws.com`

### Network Security
- SSL/TLS encryption
- Certificate pinning support
- Network security config in AndroidManifest
- HTTP/2 support

## Decompilation Notes

### Decompilation Tool
- **Tool**: jadx (Java Decompiler)
- **Version**: 1.5.5
- **Engine**: jadx with deobfuscation enabled

### Decompilation Results
- **Status**: Successful with minor issues
- **Output**: Complete source code and resources

### Split APK Analysis
The XAPK file contained 5 separate APKs:
1. **Main APK**: `tech.nxtwave.myniat.apk` (58.3 MB)
2. **ARM64**: `config.arm64_v8a.apk` (21.3 MB)
3. **ARMv7**: `config.armeabi_v7a.apk` (14.9 MB)
4. **English**: `config.en.apk` (78 KB)
5. **XXHDPI**: `config.xxhdpi.apk` (248 KB)

## Troubleshooting

### Common Issues

#### 1. APK Installation Failed
- **Issue**: "App not installed" error
- **Solution**: Enable "Install unknown apps" in Android settings, uninstall previous version first

#### 2. Decompilation Errors
- **Issue**: jadx crashes or produces incomplete output
- **Solution**: Use `--no-res` flag to skip resources, increase heap size with `-Xmx4g`

#### 3. JS Bundle Extraction
- **Issue**: Bundle is minified and hard to read
- **Solution**: Use `bundler` tool to reconstruct source maps, or use decompiler with source map support

#### 4. SSL Pinning Bypass
- **Issue**: Network requests fail with SSL errors
- **Solution**: Use Frida scripts to bypass SSL pinning, or modify network security config

#### 5. Firebase Configuration Missing
- **Issue**: Push notifications not working after rebuild
- **Solution**: Add valid `google-services.json` from Firebase console

### Tools Used

| Tool | Purpose | Version |
|------|---------|---------|
| jadx | Java decompilation | 1.5.5 |
| APK Tool | APK extraction/repacking | 2.7.0 |
| Frida | Runtime instrumentation | Latest |
| Burp Suite | Network interception | 2024.x |

## Conclusion

The MyNIAT app is a well-architected React Native application with comprehensive features for student management, attendance tracking, and academic support. It leverages modern technologies including Firebase, AWS services, and multiple analytics platforms. The app follows security best practices with biometric authentication, location-based services, and proper permission handling.

The decompilation revealed a clean separation between native Android code and React Native JavaScript, with most business logic residing in the JavaScript bundle. The app uses industry-standard libraries and follows React Native best practices for performance and user experience.

---

## Analysis Summary

| Metric | Value |
|---------|---------|
| **Analyst(s)** | [Yashwanth Kumar Gummadavelli](https://github.com/Yashwanth-Kumar-26) & [Sai Adarsh Kala](https://github.com/saiadarsh-03) |
| **Decompilation Tool** | jadx 1.5.5 |
| **Total Analysis Time** | ~3 days |

---

## Resources

- **Repository**: MyNIAT Reverse Engineering Analysis
- **File**: `nxt.xapk` (v1.0.37)
- **Platform**: Android
- **Status**:Complete Analysis

---

>**Note**: This analysis demonstrates reverse engineering skills and mobile security knowledge. For questions or feedback, feel free to reach out!

---

## Learning Outcomes

This reverse engineering analysis demonstrates the following skills:

- **Static Analysis**: Decompiling Android APKs using jadx
- **Network Analysis**: Identifying API endpoints and request/response patterns
- **Code Analysis**: Understanding React Native app architecture
- **Security Assessment**: Evaluating app permissions and security measures
- **Mobile Forensics**: Extracting and analyzing app resources

### Skills Acquired

1. Android APK structure and decomposition
2. React Native application analysis
3. API endpoint identification
4. Security vulnerability assessment
5. Documentation and reporting

---

## License

MIT License


**© 2026 - Yashwanth Kumar Gummadavelli**  
