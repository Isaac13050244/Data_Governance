

## **Data Quality Assessment Report: MedTrack Ghana**

**By:** Isaac Martey

**Date:** February 6, 2026

**Subject:** Investigation into Patient Appointment Database Integrity

**Quality Issues and Business Impact**

| Dimension | Violation Example | Operational Problem | Affected Function |
| :---: | :---: | :---: | :---: |
| **Accuracy** | **P002 (Ama Serwa):** Phonenumber 244789012 is missing a digit. | SMS reminders fail; unauthorized parties could receive sensitive info if a digit is wrong. | Operations / Privacy |
| **Completeness** | **P004:** The PatientName field is empty. | Missing identity data makes it impossible to verify the user during a Subject Access Request (SAR). | Clinical / Compliance |
| **Consistency** | **Dr. Osei vs dr. osei:** Case sensitivity variations. | Logs become fragmented; difficult to track which account actually accessed a record during an audit. | IT / Audit |
| **Timeliness** | **P003:** Date format 10/16/2025 mixed with 15/10/2025. | Sorting fails; prevents accurate "Time of Flight" analysis during a security incident. | Operations / Security |
| **Validity** | **P002:** Date formatted as 15/10/2025 instead of 2025-10-15. | Backend validation scripts fail, potentially allowing **SQL Injection** or buffer overflows if input isn't sanitized. | Finance / Security |
| **Uniqueness** | **P001/P002:** Duplicate entries for the same patient/visit. | Skews behavioral analytics used to detect "Insider Threats" or fraudulent billing patterns. | Finance / Security |

**Recommended Solutions**

#### **1\. Input Sanitization & Regex (Validity & Accuracy)**

* **Technical Solution:** Implement strict **Server-Side Validation** using Regular Expressions (Regex). For Ghana numbers: `^\+233(24|54|55|20|50|27|57|26|56)[0-9]{7}$`. This ensures only valid, reachable numbers enter the system.  
* **Responsibility:** Security Engineer / Backend Developer.  
* **Verification:** Penetration testing via "Fuzzing"—attempting to inject symbols or short strings into the phone field to see if the system rejects them.

#### **2\. Canonicalization via Dropdowns (Consistency)**

* **Technical Solution:** Move away from free-text fields for "DoctorName" and "PaymentStatus." Use **Canonicalization**—storing a single, authorized version of a data element. Implement restricted dropdown menus sourced from a master "Provider Table."  
* **Responsibility:** Database Administrator (DBA).  
* **Verification:** Audit the database logs to ensure no new variations of "Dr. Osei" appear over a 30-day period.

#### **3\. Database Constraints (Uniqueness)**

* **Technical Solution:** Apply a **Unique Constraint** on the `PatientID` \+ `AppointmentDate` combination. This prevents "Double-Entry" attacks or accidental data bloat at the structural level.  
* **Responsibility:** Database Architect.  
* **Verification:** Attempting to manually insert a duplicate record should trigger a `409 Conflict` or `SQL Constraint Violation` error.

### **The Cybersecurity Perspective**

**The Biggest Risk of Poor Data Consistency: The "Audit Trail Blind Spot" and Identity Logic Flaws.**

From a security standpoint, inconsistent data is a gift to an attacker. If `PatientName` or `DoctorName` isn't consistent, our **Identity and Access Management (IAM)** systems fail.

1. **Log Evasion:** If an attacker modifies a record using a variation of a name (e.g., `dr. osei` instead of `Dr. Osei`), security automated alerts (SIEM) might treat them as two different entities, failing to trigger a "Multiple Access" alert.  
2. **Authorization Bypass:** If our system grants permissions based on a string match (e.g., `IF user.role == 'Doctor'`), a typo in the database could accidentally lock a doctor out during an emergency or, worse, grant "Admin" privileges to a "dr." entry that hasn't been properly vetted.

In short, **Consistency is the foundation of Integrity.** Without it, we cannot prove who did what, when they did it, or if the data we are protecting is even real.

