# TSE-X Backend Changelog

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
