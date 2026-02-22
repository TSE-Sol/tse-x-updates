# 📱 TSE-X Mobile App Changelog

All notable changes to the TSE-X mobile application.

---

## [1.2.2] - 2026-02-21

### Added
- **Referral Code Input** — Enter a referral code during sign-up on the Create Account tab
- **Referral Validation** — Prevents self-referral, duplicate use, and invalid codes with colored snack bars
- **Referral Logs** — Permanent `referralLogs` Firestore collection prevents manipulation across account deletions
- **Email Verification** — New users must verify email before accessing the app (prevents fake referral abuse)
- **Verify Email Page** — Dedicated page with resend button, real-time verification check, and spam folder reminder
- **Forgot Password** — Reset password via email from the Log In tab with validation
- **Custom SMTP** — Password reset and verification emails sent from branded Gmail (no more spam folder)
- **Google Sheets Registry** — Automated user tracking with sign-up date, referral data, and active/deleted status
- **Cloud Functions** — Firestore triggers for user created, updated, and deleted events sync to Google Sheets
- **Live Profile Data** — Referral count streams in real-time from Firestore instead of cached auth data
- **Welcome Greeting** — Personalized "Welcome back, [Name]" on the Device Entry page
- **Account Deletion Cleanup** — Deleting account removes Firestore document and updates registry to "Deleted"

### Fixed
- **Display Name Save** — Profile save button was writing blank values; now correctly reads from text field
- **Navigation After Sign-Up** — Expired Firestore security rules blocked referral writes, killing the action flow
- **Referral Count Not Updating** — Firestore rules only allowed users to read/write their own document; updated to allow authenticated reads/writes for referral queries
- **Firestore Rules Expiration** — Updated security rules with no expiration date

### Changed
- Sign-up flow now routes through Email Verification page before wallet connection
- Referral code saved as `pendingReferralCode` during sign-up, applied after email verification
- Profile page referral count uses Firestore stream query instead of cached Authenticated User data
- Delete account action flow deletes Firestore document before Firebase Auth user

---

## [1.2.1] - 2026-02-15

### Added
- **Firebase Authentication** — Email/password, Google, and Apple sign-in fully integrated
- **Profile Page** — View and edit display name, email, profile avatar, referral code, and connected wallets
- **Avatar System** — 12 custom crypto-themed preset avatars hosted on GitHub Pages
- **Avatar Picker** — Bottom sheet with grid selection, saves to Firestore and persists across sessions
- **Referral System** — Auto-generated unique referral codes (TSE + 6 alphanumeric chars) on sign-up
- **Referral Tracking** — referralCode, referralCount, and referredBy fields stored in Firestore
- **Profile Image Upload** — Camera/gallery upload option with Firebase Storage integration
- **Copy to Clipboard** — One-tap copy for referral codes and wallet addresses
- **Save Profile Changes** — Updates display name and photo to Firestore with confirmation snack bar
- **Account Deletion** — Confirm dialog → delete Firebase auth user → navigate to sign-on (Apple App Store compliant)
- **Sign Out** — Clears wallet connections and navigates to sign-on with replacement

### Fixed
- **Auth Flow Security** — App no longer allows sign-in without an existing account
- **Sign-In Validation** — Conditional check on User ID before navigation, with error snack bar on failure
- **Google Sign-In (iOS)** — Added REVERSED_CLIENT_ID URL scheme to Info.plist for proper redirect
- **Google Sign-In Persistence** — Created automation script to restore GoogleService-Info.plist after FlutterFlow re-downloads

### Changed
- Social login (Google/Apple) on Log In tab uses Auth Log In instead of Auth Create Account
- Referral code generation added to both Create Account and Log In flows as safety net
- Wallet state variables cleared on sign out and account deletion

---

## [1.2.0] - 2026-02-07

### Added
- **Android Support** — App now builds and runs on Android devices alongside iOS
- **Android Deep Linking** — `tsex://` scheme for Phantom/MetaMask wallet callbacks on Android
- **Android NFC Support** — NFC tag reading for device discovery on Android
- **Android BLE Support** — Bluetooth Low Energy communication with TSE-X devices on Android

### Fixed
- Resolved Kotlin plugin compatibility issue blocking Android builds (nfc_manager + package_info_plus conflict)
- Android `MainActivity.kt` properly handles Phantom wallet deep link callbacks

---

## [1.1.3] - 2026-01-30

### Added
- **X402 Payment Protocol** — Full x402scan and ZauthX402 compatibility for standardized crypto payments
- **Dual Network Payments** — Pay with TSE tokens (Solana) or USDC (Base) from the same app
- **Public Stats Tracking** — Live transaction stats independent of x402scan, deployed to GitHub Pages
- **Transaction Logging** — All payments (including demo) logged with chain, token, amount, wallet, and device info

### Changed
- Backend compatibility layer supports both x402scan and Zauth payment header formats
- Payment verification handles X-PAYMENT headers from multiple facilitator platforms

---

## [1.1.2] - 2026-01-16

### Added
- **Dynamic TSE Pricing** — Live price fetched from GeckoTerminal with DexScreener and CoinGecko fallbacks
- **Price Display Widget** — Shows TSE cost, USD value, and countdown timer for price validity
- **Price Caching** — 5-minute cache to reduce API calls

### Fixed
- Price API reliability — switched primary source to GeckoTerminal (free, no API key required)
- Removed Jupiter and Birdeye price sources (now require paid API keys)

---

## [1.1.1] - 2026-01-14

### Added
- **Receipt Screen Email** — Send payment receipts via email with transaction details
- **Email Fallback** — Copies receipt to clipboard if email client fails to launch

### Fixed
- Email button on ReceiptScreen was non-functional — added proper url_launcher integration
- Removed conflicting custom url_launcher dependency (FlutterFlow has built-in 6.3.1)

---

## [1.1.0] - 2025-12-15

### Added
- **Wallet Persistence** — Phantom, MetaMask, and Base wallet connections survive app restarts
- **On Page Load Restore** — App checks for saved wallet data on startup and restores connected state
- **Persisted App State** — 14+ wallet-related fields now saved to local storage

### Changed
- On Page Load workflow updated: checks for existing wallet data before showing connect UI
- Wallet connection flow skips re-connect if session is still valid

---

## [1.0.0] - 2025-12-04

### Added
- **Phantom Wallet Integration** — Connect Solana wallet via deep linking
- **MetaMask Wallet Integration** — Connect Base/Ethereum wallet
- **NFC Device Discovery** — Tap NFC tags to find and connect to TSE-X devices
- **QR Code Scanning** — Scan QR codes for device discovery
- **BLE Communication** — Bluetooth Low Energy connection to Arduino-powered devices
- **Device Dashboard** — View device status, select payment method, and initiate payments
- **Coffee Machine UI** — Hot/Iced selection, brewing animation, and payment flow
- **Bike Lock UI** — Unlock, session timer, and lock controls
- **TSE Token Payments** — Pay with TSE on Solana network
- **USDC Payments** — Pay with USDC on Base network
- **iOS Deep Linking** — `tsex://` scheme for wallet callbacks
- **AppDelegate** — NFC + Phantom callback handling for iOS

---

## Links

- 🌐 [TSE-X Updates](https://github.com/TSE-Sol/tse-x-updates)
- 📊 [Live Stats](https://tse-sol.github.io/tse-assets/stats.html)
- 💬 [Discord](https://discord.gg/X9cTmzW2Gz)
- 🦅 [Twitter/X](https://x.com/T_S_E_Sol)
