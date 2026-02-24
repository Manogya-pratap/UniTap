# Kong API Gateway Security Specification

## 1. Overview
UniTap uses **Kong API Gateway** as the primary perimeter for all external and internal traffic. For bank-level transactions and third-party integrations, Kong enforces strict security policies to ensure data integrity and authenticity.

## 2. Core Security Plugins & Policies

### A. Mutual TLS (mTLS)
- **Use Case**: Direct integrations between UniTap and Banking Partners.
- **Requirement**: Both the client (Bank) and the server (UniTap Gateway) must present valid certificates issued by a trusted CA.
- **Implementation**: Kong `mtls-auth` plugin configured on bank-specific routes.

### B. HMAC Signature Verification
- **Use Case**: Securing financial debit/credit requests from the mobile app and POS.
- **Requirement**: Every financial request must include an `X-UniTap-Signature` header.
- **Implementation**: Kong `hmac-auth` plugin. Kong validates the signature using a shared secret before the request ever reaches the microservices.

### C. IP Restriction & Whitelisting
- **Use Case**: Restricting access to internal Admin dashboards and Bank callback webhooks.
- **Requirement**: Requests are rejected unless they originate from a known, whitelisted IP address (e.g., Office VPN, Bank Gateway).
- **Implementation**: Kong `ip-restriction` plugin.

### D. Rate Limiting (Token Bucket)
- **Use Case**: Preventing brute-force attacks on Auth endpoints and API abuse on the Wallet.
- **Requirement**:
    - Auth: 5 OTP requests per hour per user.
    - Wallet: 20 payment attempts per minute per user.
- **Implementation**: Kong `rate-limiting` plugin with Redis as the data store.

## 3. Bank Approval Flow Security
1. **Request**: Bank sends an approval/webhook to `https://api.unitap.in/v1/bank/callback`.
2. **Layer 1 (WAF)**: Checks for DDoS and common SQLi/XSS patterns.
3. **Layer 2 (mTLS)**: Kong validates the Bank's client certificate.
4. **Layer 3 (HMAC)**: Kong validates the payload signature.
5. **Layer 4 (IP)**: Kong verifies the request is from the Bank's known IP range.
6. **Delivery**: Request forwarded to the internal **Payment/Settlement Service**.

## 4. Key Management
- Secrets used for HMAC and mTLS certificates are stored in **AWS Secrets Manager** and injected into Kong via the **Kong Konnect** secret management interface or Kubernetes Secrets.
- Auto-rotation is enabled for all API keys every 90 days.
