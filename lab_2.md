### **Request 1: Marketing Campaign**

**Decision:** **Conditional Approval**

| Field | Details |
| :---- | :---- |
| **Lifecycle Stage** | **Use / Share** |
| **Justification** | Sarah’s request for "full student database" violates the **Principle of Minimality**. While she has a legitimate business goal, she does not need the entire raw database to launch a campaign. Since the email addresses are **CONFIDENTIAL**, we must ensure we have the data subjects' **Prior Consent** for direct marketing as required by Section 40 of the Ghana DPA. |
| **Action Steps** | 1\. **Data Minimization:** Export only First Name, Email, and Current Course (exclude phone numbers and full enrollment history if not vital). 2\. **Consent Check:** Run a query to filter only students who opted-in to marketing communications. 3\. **Secure Transfer:** Provide access via a password-protected, time-bound secure link rather than a CSV attachment in a ticket. 4\. **Consult:** Contact the **Data Protection Supervisor** to verify marketing consent logs. |

### **Request 2: Analytics Partnership**

**Decision:** **Deny** (Immediate Action Required)

| Field | Details |
| :---- | :---- |
| **Lifecycle Stage** | **Share / Store** |
| **Justification** | This request contains massive security and compliance failures. Providing "login credentials" to a third party violates basic **IAM (Identity & Access Management)** policies. Furthermore, transferring student PII (**CONFIDENTIAL**) to a US-based firm triggers **Cross-Border Transfer** restrictions. Under Ghana DPA, we must ensure the destination country has "adequate" protection or that a **Data Transfer Agreement (DTA)** is in place. |
| **Action Steps** | 1\. **Revoke Credentials:** Immediately reset the attached AWS credentials if they are active. 2\. **Anonymization:** Inform David that raw DB access is prohibited. Propose providing a **De-identified/Anonymized** dataset (removing names and profiles) for learning pattern analysis. 3\. **Legal Review:** Request a copy of the partnership contract to ensure it includes a "Data Processing Addendum" (DPA). 4\. **Consult:** **Legal Counsel** and the **CISO** regarding international data transfer compliance. |

### **Request 3: Archive & Deletion**

**Decision:** **Conditional Approval** (Partial Deletion)

| Field | Details |
| :---- | :---- |
| **Lifecycle Stage** | **Archive / Destroy** |
| **Justification** | While the student has the "Right to Erasure" (Section 44), this is not absolute. EduConnect must balance the "Right to be Forgotten" against **statutory retention obligations**. For example, financial records (payments) must often be kept for 6–7 years for tax/audit purposes under Ghana's financial laws. |
| **Action Steps** | 1\. **PII Scrubbing:** Delete the user's profile, contact info, and course progress data from active databases. 2\. **Hard Archiving:** Move payment records and certificates to a "Cold Storage" archive that is encrypted and accessible only by Finance/Legal. 3\. **Anonymize for Stats:** Retain "Course Completed" data but stripped of identity for internal historical analytics (permitted under Section 24). 4\. **Confirmation:** Issue a formal "Certificate of Deletion" to James Boateng stating which data was destroyed and what was retained for legal reasons. |

### **Summary of Principles Applied**

* **Least Privilege:** Users only get the data they *must* have to do their job, nothing more.  
* **Ghana DPA Compliance:** Prioritizing consent for marketing and adequacy for international transfers.  
* **Separation of Duties:** DevOps provides the technical pipe, but Legal/Compliance provides the permission.

