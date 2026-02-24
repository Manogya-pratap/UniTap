# UniTap Platform Overview

## Project Identity
**UniTap** is a comprehensive campus fintech and identity platform designed for high-scale student environments. It integrates attendance, payments, and access control into a single unified system.

## Vision: "Use Everywhere"
While starting as a campus-focused solution, UniTap's vision is to become a student's primary financial and identity tool, usable both on-campus and with off-campus merchants (Phase 3).

## System Architecture
The platform follows a **3-layer microservices architecture**:
- **Edge Layer**: AWS WAF, CloudFront, ALB, and Spring Cloud Gateway for security and routing.
- **Service Layer**: Java Spring Boot 3.2 microservices (Auth, Wallet, NFC, Attendance, Campus, Admin, Analytics).
- **Data Layer**:
    - **PostgreSQL 15**: Primary transactional database with monthly partitioning.
    - **Redis 7**: Distributed locking (Redisson) and session caching.
    - **Kafka 3.6**: Event streaming for real-time notifications and audit trails.
    - **ClickHouse**: High-performance analytics and reporting.

## Core Features & Security
- **Triple-Locking Wallet**: Prevents race conditions and double charges using Idempotency checks, Redis Distributed Locks, and Database Pessimistic Locks.
- **NFC Anti-Replay**: Uses a 5-minute nonce window and SHA-256 hashing to prevent card cloning and replay attacks.
- **QR Code Payments**: Support for generating and scanning QR codes for payments, providing a flexible alternative to NFC.
- **Immutable Ledger**: Append-only transaction log for financial compliance.
- **Real-time Notifications**: Instant alerts to parents and students via Kafka and Firebase.

## Technology Stack
- **Backend**: Java 17, Spring Boot 3.2
- **Mobile**: Flutter 3.16, Dart 3.2
- **Web**: Next.js 14, React 18, TypeScript 5.3
- **Infrastructure**: AWS (EKS, RDS, MSK, ElastiCache), Terraform, Kubernetes

## Development Roadmap
1. **Infrastructure**: Provision AWS resources using Terraform.
2. **Database**: Initialize PostgreSQL with Flyway migrations and partitioning logic.
3. **Core Services**: Implement Auth and Wallet services with security-critical locking mechanisms.
4. **NFC & Attendance**: Setup hardware verification logic and event-driven attendance tracking.
5. **Frontend**: Build the Flutter mobile app (including QR scanner) and Next.js admin dashboards.
6. **Regulatory Expansion**: Partner with banks for PPI/Open-wallet status to enable off-campus usage.
