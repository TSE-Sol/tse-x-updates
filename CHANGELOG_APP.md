# TSE-X Mobile App Changelog

## [1.5.0] - 2026-01-10

### Added
- **Power Switch Device Type**: New UI for time-based power control
  - Preset durations: 30 min ($0.05), 1 hour ($0.10), 12 hours ($0.50)
  - Custom duration picker with $0.05 per 30 min pricing
  - Live price display as you select duration
  - Power button animation with countdown timer

### Changed
- **Device Type Matching**: Now uses exact matching (case-insensitive)
  - `Bike Lock` - Bike lock with BLE
  - `Door Lock` - Door lock (WiFi only)
  - `Coffee Machine` or `Coffee Maker` - Coffee device
  - `Power Switch` - Time-based power control
- **Device Dashboard**: Improved device type detection from pendingTransaction

### Fixed
- BLE auto-connect now properly saves bleDeviceId to backend
- Resume session correctly retrieves bleDeviceId for reconnection
- Fixed receipt dialog method name causing build error

---

## [1.4.0] - 2026-01-08

### Added
- Payload Preview Widget with copy/download features
- QR Code generator with save functionality
- Scrollable JSON preview in Device Creator

### Changed
- Simplified QR code save to use native share sheet

### Fixed
- Build errors related to share_plus dependency

---

## [1.3.0] - 2026-01-05

### Added
- USDC payment support (Base blockchain)
- Qualified holder status for USDC access ($100 minimum TSE holdings)
- Dual wallet display (Solana + Base)

### Changed
- Payment method selector shows available options based on device support

---

## [1.2.0] - 2025-12-28

### Added
- Resume Session widget for reconnecting to active sessions
- BLE heartbeat for online status reporting
- Session persistence across app restarts

### Fixed
- Orphaned session cleanup
- BLE disconnect handling

---

## [1.1.0] - 2025-12-20

### Added
- Real TSE payment flow via Phantom wallet
- Transaction verification with backend
- Receipt generation and display

---

## [1.0.0] - 2025-12-15

### Added
- Initial release
- Device scanning (NFC, QR, BLE)
- Device Dashboard for Coffee Machine and Bike Lock
- Mock payment flow for testing
