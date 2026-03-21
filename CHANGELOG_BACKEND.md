# TSE-X Backend Changelog

## [1.2.0] - 2026-03-20

### Added
- **Device Pricing Module (`deviceprices.js`)** — New module with full REST API for managing multiple prices per device
  - `GET /api/device-prices/:deviceId` — public, returns prices + wallet addresses + bleDeviceId
  - `POST /api/device-prices/:deviceId` — set prices at registration (requires deviceSecret)
  - `PUT /api/device-prices/:deviceId` — update prices (requires deviceSecret)
  - `DELETE /api/device-prices/:deviceId/price/:index` — remove single price item
  - `DELETE /api/device-prices/:deviceId/device` — delete entire device (requires deviceSecret)
  - `POST /api/device-prices/:deviceId/ble-device-id` — save BLE MAC address after app connects
- **TSE-X Device Registry** — Web-based operator dashboard with Firebase Auth, QR code generation, and full Arduino file download pre-filled with device credentials
- **Multi-Price Support** — Each price item supports: name, description, priceUsd (min $0.01), duration (minutes), image URL
- **BLE Device ID Auto-Save** — App reports BLE MAC after first connection; backend stores and returns it for direct reconnect

### Fixed
- **Device Registration** — `/devices/register` now properly saves all fields: `deviceName`, `deviceType`, `model`, `firmwareVersion`, `solanaWalletAddress`, `baseWalletAddress`
- **Payment Routing** — All 3 challenge endpoints (TSE Solana, USDC Base, USDC Solana) now route payments to device operator's registered wallet, falling back to platform wallet only if none set
- **BLE Heartbeat for BLE-Only Devices** — App-sourced heartbeats (`source: 'app'`) bypass Arduino secret requirement, allowing claimed BLE-only devices to be verified and accept payments without WiFi

---

## [1.1.2] - 2026-03-14

### Added
- **Prize Draw System** — Automatic weekly draw every Saturday midnight UTC via `prizedraw.js`
- **Winner Logging** — Winners recorded to Google Sheets with wallet, amount, and timestamp
- **Public Winners Ledger** — Separate "Public Winners" tab with ARRAYFORMULA auto-pull, published via Google Sheets publish-to-web
- **Catch-up Draw** — On server startup, detects and runs any overdue weekly draws
- **Manual Draw Endpoint** — `POST /api/prize-draw/draw` for admin-triggered draws
- **Stored Winner Amount** — `/pot` endpoint returns `winnerAmount` from Firestore so pot refills don't affect displayed prize
- **Prize Pool Firestore Sync** — Winner amount written to Firestore on each draw for app widget consumption

### Changed
- `/pot` endpoint now returns stored `winnerAmount` field from Firestore instead of calculating from live balance

---

## [1.1.1] - 2026-02-21

### Added
- **Firebase Cloud Functions** — Sync user data (create, update, delete) to Google Sheets via Firestore triggers
- **User Registry Sheet** — Tracks sign-up date, referral data, email, display name, and deleted status

---

## [1.1.0] - 2026-02-07

### Added
- **Public Stats API** — `/api/stats`, `/api/transactions`, `/api/leaderboard` endpoints
- **Transaction Logging** — All payments logged with chain, token, amount, and wallet
- **Stats Widget** — Embeddable HTML widget for live payment stats

---

## [1.0.1] - 2026-02-07

### Fixed
- **Payment Flow Hanging** — Transaction submit no longer blocks waiting for Solana confirmation (5-30+ sec)
- **Non-blocking Confirmation** — Returns immediately after submit; confirmation runs in background via `process.nextTick`

### Changed
- Solana verification retries increased from 3→5 with 3s delay for better reliability

---

## [1.0.0] - 2026-01-30

### Added
- **x402scan Integration** — Full compatibility with x402scan.com payment aggregator
- **Custom Facilitator** — Server submits signed payment authorizations on behalf of users
  - Base: EIP-3009 `transferWithAuthorization` for USDC payments
  - Solana: Versioned transaction support with feePayer signature
- **Ownership Proofs** — Cryptographic signatures proving control of payment addresses
  - Added to `/.well-known/x402` discovery endpoint
  - Added to all 402 Payment Required responses
- **Solana USDC** — Added as payment option alongside Base USDC and Solana TSE
- **feePayer field** — Solana accepts now include feePayer for x402scan compatibility

### Changed
- Payment-Required header now includes `ownershipProofs` array
- `buildAcceptsArray()` returns both Solana and Base payment options
- Versioned transactions (v0) supported for Solana payments

### Environment Variables
- `X402_SERVER_PRIVATE_KEY` — Base wallet for submitting EIP-3009 transfers
- `SOLANA_SUBMITTER_PRIVATE_KEY` — Solana wallet for paying fees and submitting SPL transfers

---

## [0.9.0] - 2026-01-10 (Beta)

### Added
- `brewing` and `brewType` fields at top level of status response (for easier Arduino parsing)
- Power Switch support with variable duration pricing

### Changed
- Status endpoint now returns brewing info at root level, not just nested in session

### Fixed
- BLE device ID now saved when app first connects (`/x402/:deviceId/ble-connect`)

---

## [0.8.0] - 2026-01-08

### Added
- Device secret validation on poll endpoints
- Auto-registration for new devices on first contact
- `bleDeviceId` storage for BLE devices

### Changed
- Improved session cleanup for orphaned sessions

---

## [0.7.0] - 2026-01-05

### Added
- USDC payment verification (Base blockchain)
- Holder status endpoint (`/tse/holder-status/:walletAddress`)
- Multi-currency challenge creation

### Changed
- Challenge endpoint accepts `amountUsd` for variable pricing
- Payment info includes both TSE and USDC options

---

## [0.6.0] - 2025-12-28

### Added
- X.402 protocol implementation
- Session-based access control
- Receipt generation with unique IDs
- File-based data persistence

### Changed
- Complete API restructure for X.402 compliance
- JWT-based session tokens

---

## [0.1.0] - 2025-12-15

### Added
- Initial backend release
- Device registration endpoints
- Basic payment flow
- Challenge/verify system

---

## API Endpoints

### Device Status
```
GET /x402/:deviceId/status
Query: ?deviceSecret=XXX&wallet=XXX&source=app
```

### Payment Challenge
```
POST /x402/:deviceId/challenge
Body: { wallet, chain, amountUsd }
```

### Payment Verification
```
POST /x402/:deviceId/verify
Body: { challengeId, txHash, wallet }
```

### Session Control
```
POST /x402/:deviceId/brew    # Start brewing/power
POST /x402/:deviceId/complete # End session
POST /x402/:deviceId/stop    # Cancel early
```

### BLE Connection
```
POST /x402/:deviceId/ble-connect
Body: { bleDeviceId, wallet }
```

### x402 Discovery
```
GET /.well-known/x402
Returns: Server info, payment options, ownership proofs
```

### Prize Draw
```
POST /api/prize-draw/draw    # Manual draw trigger
GET  /api/prize-draw/pot     # Current pot + stored winner amount
```
