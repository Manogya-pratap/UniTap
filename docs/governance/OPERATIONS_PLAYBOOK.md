# 1️⃣ OPERATIONS & INCIDENT PLAYBOOK

*(“What happens when things go wrong?”)*

## 🎯 Purpose
Ensure **predictable behavior under failure** so:
* colleges don’t panic
* banks trust you
* users don’t lose confidence

---

## 🧩 Incident Categories

### A. Platform Incidents
| Incident        | Example                       |
| --------------- | ----------------------------- |
| Partial outage  | Attendance works, wallet slow |
| Full outage     | Backend unavailable           |
| Device outage   | NFC reader down               |
| Data sync delay | Offline attendance pending    |

### B. Financial Incidents
| Incident          | Example                   |
| ----------------- | ------------------------- |
| Duplicate debit   | Retry without idempotency |
| Wallet mismatch   | Ledger vs balance         |
| Failed settlement | Bank delay                |
| Refund stuck      | Merchant error            |

### C. Security Incidents
| Incident               | Example              |
| ---------------------- | -------------------- |
| Card cloning suspicion | Repeated UID pattern |
| Device compromise      | Unregistered reader  |
| Account takeover       | Suspicious login     |

---

## 🧭 Incident Response Flow (MANDATORY)
```
Detect → Classify → Contain → Communicate → Resolve → Review
```

---

## ⏱ SLA Matrix
| Severity | Example            | Response | Resolution |
| -------- | ------------------ | -------- | ---------- |
| SEV-1    | Wallet debit wrong | 15 min   | 4 hrs      |
| SEV-2    | Attendance outage  | 30 min   | 24 hrs     |
| SEV-3    | Report delay       | 24 hrs   | 72 hrs     |

---

## 📣 Communication Rules

### Student App
* Clear message
* No technical jargon
  Example:
> “Payments are temporarily unavailable. Your balance is safe.”

### College Admin
* Dashboard banner
* ETA
* Manual fallback instructions

### Bank
* Formal incident email
* Timeline
* Impact analysis

---

## 🔁 Post-Incident Review (NON-NEGOTIABLE)
Every SEV-1 or SEV-2 incident must produce:
* Root cause
* Timeline
* Preventive action
* Owner assigned
