# 2️⃣ BANK–UNITAP–COLLEGE RACI MATRIX

*(Who is responsible for what)*

## 🎯 Purpose
Avoid **liability confusion** (this kills partnerships).

---

## 🧾 Responsibility Matrix

| Function               | Bank  | UniTap | College |
| ---------------------- | ----- | ------ | ------- |
| Wallet funds custody   | **R** | I      | I       |
| Transaction processing | **R** | **A**  | I       |
| Ledger correctness     | **R** | **A**  | I       |
| Card issuance          | I     | **R**  | **A**   |
| Attendance accuracy    | I     | **A**  | **R**   |
| Device installation    | I     | **A**  | **R**   |
| AML monitoring         | **R** | **A**  | I       |
| Fraud alerts           | **R** | **A**  | I       |
| Student KYC            | **R** | **A**  | I       |
| Data privacy           | **A** | **R**  | **R**   |
| **Gateway Security (mTLS)** | **R/A** | **R/A** | I       |

**Legend**
* **R** = Responsible
* **A** = Accountable
* **I** = Informed

---

## 🔑 Critical Line (for contracts)
> “UniTap does not hold customer funds. All regulated financial responsibilities are executed by the banking partner.”
