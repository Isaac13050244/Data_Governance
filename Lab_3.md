### **Compliance Response Matrix**

| Element | Ghana DPA (Act 843\) | EU GDPR | CCPA / CPRA |
| :---- | :---- | :---- | :---- |
| **Right to Deletion Exists?** | **Yes** (Section 33\) | **Yes** (Article 17\) | **Yes** (Section 1798.105) |
| **Exemptions / Conditions** | Retention required by law, contract, or for a lawful purpose related to the entity’s function. | Legal obligation (e.g., tax/audit), establishment of legal claims, or public interest. | Completing a transaction, active disputes, security, or complying with legal obligations. |
| **Response Deadline** | **21 Working Days** | **1 Month** (30 Days) | **45 Days** (Confirm receipt in 10\) |
| **Penalties** | Up to 2,500 penalty units or 2 years imprisonment (approx GHS 30,000). | Up to €20M or 4% of global annual turnover. | $2,500 (unintentional) to $7,500 (intentional) per violation. |
| **Consent Model** | **Opt-In** (Explicit) | **Opt-In** (Explicit/Freely given) | **Opt-Out** (Notice at collection) |

### **Customer Analysis & Action Plans**

#### **Customer A: Abena (Accra)**

* **Legal Right:** Yes, but qualified. Under Section 33, she can request deletion if the data is no longer necessary.  
* **ShopGhana’s Obligations:** We must act within **21 working days**.  
* **Data Retention:** We **must** retain financial records of her purchases (from 8 months ago) for tax audit purposes as required by Ghana Revenue Authority (GRA) guidelines (typically 6 years).  
* **Draft Response:** "Hello Abena, we have received your request. We will delete your account profile and marketing data within 21 days. Please note we are legally required to retain your transaction history for tax purposes."

#### 

#### **Customer B: Lukas (Berlin)**

* **Legal Right:** Yes. Lukas has the "Right to be Forgotten" since his delivery is complete and there is no longer a contractual necessity to hold his profile.  
* **Exemptions:** Only the retention of the invoice for EU VAT compliance (10 years in Germany).  
* **ShopGhana’s Obligations:** Erase PII from active databases and notify any third-party processors (like DHL or Mailchimp) to do the same.  
* **Draft Response:** "Guten Tag Lukas, your request under GDPR Art. 17 is being processed. Your profile will be erased within 30 days. Statutory tax records will be moved to a restricted archive."

#### 

#### **Customer C: Maria (Los Angeles)**

* **Legal Right:** Yes, but **deletion is deferred** due to the "Active Return Dispute."  
* **ShopGhana’s Obligations:** We must confirm receipt within **10 days**. We cannot delete the data necessary to resolve her return, but we **must** immediately honor her "Stop Selling" (Do Not Sell My Info) request.  
* **Retention Justification:** Data is needed to "complete the transaction" (the return/refund) per CCPA exceptions.  
* **Draft Response:** "Hi Maria, we’ve updated your account to 'Do Not Sell or Share.' Regarding deletion, we cannot erase your data yet due to your active return dispute. Once resolved, we will proceed with the deletion."

### **The Cybersecurity Risk of Inconsistency**

From a **Security Engineering** perspective, the greatest threat is **The "Audit Trail Blind Spot."** When deletion processes are manual or inconsistent across regions, we lose the ability to perform accurate **Forensics**. If a breach occurs, and our logs show activity from "Customer A" (who was supposed to be deleted), we cannot distinguish between a legitimate system error and a **Malicious Insider** or an **External Attacker** exploiting a deactivated account.

**Zero-Trust Rule:** A user is either fully authenticated or fully erased. "Partial deletion" is a vulnerability.

