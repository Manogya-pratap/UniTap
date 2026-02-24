# UniTap Master Build Specification & Prompts

This document contains the consolidated technical specifications and AI generation prompts for the UniTap platform.

## 1. Project Context
UniTap is a campus fintech platform designed for 100,000 users. It provides integrated wallet payments, NFC-based attendance tracking, and campus access control.

## 2. System Architecture
- **Backend**: Spring Boot 3.2, Java 17, Microservices.
- **Frontend**: Flutter 3.16 (Mobile), Next.js 14 (Dashboards).
- **Data**: PostgreSQL 15 (ACID), Redis 7 (Locking/Cache), Kafka 3.6 (Events), ClickHouse (Analytics).

## 3. Core Security Mechanisms
- **Triple-Locking Wallet**: Idempotency Key -> Redis Distributed Lock -> DB Pessimistic Lock (Serializable).
- **NFC Anti-Replay**: 5-minute nonce window + SHA-256 hashing of card tokens.
- **QR Secure Session**: Time-limited, encrypted QR codes for off-campus payments and fallback.

## 4. Services Overview
- **Auth Service**: JWT/OTP/Refresh tokens.
- **Wallet Service**: Ledger-based transactions with strong consistency. Support for QR-based debit requests.
- **NFC Service**: Secure card verification and device management.
- **Attendance Service**: Event-driven tracking with fraud detection.
- **Payment/QR Service**: Generation and validation of secure payment QR codes.

## 5. Development Prompts
Refer to the provided documentation to generate:
- Terraform infrastructure for AWS ap-south-1.
- Flyway SQL migrations with monthly partitioning for the ledger.
- Wallet Service implementation with the 9-step debit flow and QR support.
- Flutter Student App with Clean Architecture, Riverpod, and **QR Payment Scanner**.
- React Admin Dashboards with Next.js and Ant Design.
- Merchant POS app with **QR Code Generator** for receiving payments.
