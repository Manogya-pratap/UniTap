# QR Code Payment Specification

## 1. Overview
QR Code payments provide an alternative to NFC for both on-campus and off-campus transactions. The system supports two modes:
- **Merchant-Presented Mode (MPM)**: Merchant displays a QR code, student scans it with the mobile app.
- **Consumer-Presented Mode (CPM)**: Student displays a QR code, merchant scans it (useful for offline scenarios).

## 2. Secure QR Generation
- **Payload**: Encrypted JSON containing `merchant_id`, `amount` (optional), `timestamp`, and a `hmac` signature.
- **TTL**: Payment QRs should have a short TTL (e.g., 60-120 seconds) to prevent replay attacks.
- **Encryption**: AES-256-GCM using keys managed by AWS KMS.

## 3. Transaction Flow (MPM)
1. **Merchant** generates a QR code for a specific amount.
2. **Student** scans the QR code using the Flutter app.
3. **App** decrypts and validates the QR signature.
4. **App** sends a `debit` request to the **Wallet Service** with the merchant's details and an idempotency key.
5. **Wallet Service** executes the **Triple-Locking** flow.
6. **Success**: Notification sent to both student and merchant (via WebSocket).

## 4. Mobile App Requirements (Flutter)
- **Library**: `mobile_scanner` for scanning.
- **Library**: `qr_flutter` for generating (CPM mode).
- **UX**: Immediate feedback on scan, biometric confirmation for high-value transactions.

## 5. Backend Requirements (Spring Boot)
- **Endpoint**: `POST /api/v1/payments/qr/verify`
- **Logic**: Validate QR signature, check TTL, and initiate the standard wallet debit flow.
