# 📱 TSE-X Mobile App Changelog

All notable changes to the TSE-X mobile application.

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
- 🐦 [Twitter/X](https://x.com/T_S_E_Sol)
