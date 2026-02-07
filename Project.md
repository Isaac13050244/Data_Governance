# **QuickLoan Governance Review Card**

| Section | Issue / Definition | Impact | Suggested Fix / Mitigation |
| :---- | :---- | :---- | :---- |
| **1\. Data Quality Risk** | Inaccurate and irregularly structured client information employed in machine learning assessment | Results in flawed loan approval outcomes and compromised analytical insights | Apply data entry verification at application interface, structural validation at API entry point, and systematic quality assurance protocols |
| **2\. Legal & Compliance Risk** | Over-gathering of personally identifiable information lacking direct user authorization | Breaches Ghana's Data Protection Act (Act 843\) and subjects the organization to regulatory sanctions | Deploy clear consent mechanisms, adopt data collection minimization strategies, and maintain documentation of legitimate processing justifications |
| **Data Classification** | **Sensitive** | Confidential monetary and individual information demands the highest level of safeguarding | Implement cryptographic protection, rigorous authorization controls, and specified data preservation and removal protocols |
| **3\. Bias & Fairness Risk** | Past training datasets could contain embedded economic or population-based prejudices | System-driven determinations may unjustly penalize specific customer segments | Execute prejudice assessment procedures and track authorization results across different populations |
| **Source of Bias** | Legacy lending records and indirect indicators (such as geographic area, mobile device behavior) | Prejudice may be magnified through algorithmic processing systems | Eliminate problematic proxy attributes and establish periodic equity evaluations |
| **4\. Storytelling / Reporting Recommendation** | **Metric:**  Loan Approval Rate Parity | Facilitates openness regarding equitable treatment in algorithmic determinations | Monitor authorization percentage variations among population categories or substitute variables |
| **Visualization Type** | Clustered Column Chart or Trend Line Graph | Renders inequalities readily identifiable across temporal periods | Employ visual analytics platforms for ongoing surveillance |
| **Why It Matters** | Exhibits responsible artificial intelligence deployment and cultivates partner confidence | Reinforces organizational responsibility and adherence to legal mandates | Guarantees equitable treatment remains a tracked governance priority |

## **Corrected Data Flow Diagram**

Below are the critical corrections required for QuickLoan Mobile's data pipeline, with annotations explaining each change and its necessity.

### **Required Data Flow Corrections**

1. **Correction at Step 1 (User Mobile App): Implement Data Minimization**

**Current Issue:** The app collects excessive personal data including the user's entire contact list, which is not necessary for loan decisioning.

**Required Change:** Remove contact list collection entirely. Limit data collection to only what is necessary for loan assessment: name, phone number, ID number, income verification, loan amount requested, and repayment history.

**Why Necessary:** Complies with Data Minimization principle in Ghana's DPA (Act 843\) and reduces privacy risk exposure. Collecting unnecessary data increases liability and violates the principle that data collection must be adequate, relevant, and limited to what is necessary.

2. **Correction between Steps 2-3 (API Gateway → Raw Data DB): Implement Consent Verification Layer**

**Current Issue:** No consent capture or verification mechanism exists before data enters the database.

**Required Change:** Add a Consent Management Service between API Gateway and Raw Data DB that: (a) Verifies explicit consent was obtained, (b) Logs consent timestamp and scope, (c) Blocks data processing if consent is missing, (d) Enables consent withdrawal requests.

**Why Necessary:** Ghana's DPA requires explicit, informed consent for personal data processing. Without this layer, QuickLoan violates Section 28 of Act 843 and faces regulatory penalties. This creates an audit trail demonstrating compliance.

3. **Correction at Step 3 (Raw Data DB): Implement Data Classification and Retention Policies**

**Current Issue:** No data classification system or retention policies are in place.

**Required Change:** Tag all data with classification labels (Public/Internal/Confidential/Sensitive) upon storage. Implement automated retention policies: delete raw application data after 7 years (regulatory requirement), delete rejected applications after 2 years, and flag Sensitive PII for enhanced protection.

**Why Necessary:** Prevents indefinite data accumulation (violates storage limitation principle), enables appropriate security controls based on data sensitivity, and ensures compliance with data retention requirements under Ghana's DPA.

4. **Correction at Step 4 (Preprocessing Service): Add Data Quality Validation and Bias Detection**

**Current Issue:** No defined data quality checks or bias detection mechanisms.

**Required Change:** Implement validation checks: format standardization (phone numbers, names), completeness scoring, outlier detection, and duplicate detection. Add bias detection to identify proxy variables that correlate with protected demographic attributes.

**Why Necessary:** Poor data quality leads to inaccurate loan decisions. Undetected proxy variables can introduce discriminatory bias. This step ensures data reliability and fairness before model training/inference.

5. **Correction at Step 7 (Decision Service): Implement Decision Logging and Transparency**

**Current Issue:** No logging of automated decisions or explainability features.

**Required Change:** Log every automated decision with: model version, input features used, confidence score, decision outcome, and timestamp. Implement explainability features showing key factors influencing each decision. Add human review queue for borderline cases.

**Why Necessary:** Ghana's DPA grants individuals the right to explanation for automated decisions (Section 37). Logging enables compliance with this right, supports bias audits, and provides accountability for model decisions.

6. **Correction at Steps 9-10 (Analytics DB and 3rd-Party Partner): Implement Data Masking and Anonymization**

**Current Issue:** Raw PII is accessible in analytics databases and shared with third-party partners without protection.

**Required Change:** Apply data masking before loading into Analytics DB: hash customer IDs, aggregate geographic data to region level, and remove direct identifiers. For 3rd-party sharing: use anonymization techniques, conduct Data Protection Impact Assessments (DPIAs), and require data processing agreements.

**Why Necessary:** Protects PII from misuse by internal analysts and external partners. Reduces breach impact. Third-party data sharing without adequate protection violates Ghana's DPA transfer requirements and increases privacy risk.

## **Summary of Review Process**

### **Governance Review Methodology**

My review process applied data lifecycle and classification principles systematically to identify risks at each stage of QuickLoan's data pipeline. I began by mapping the data lifecycle from collection through storage, processing, usage, and sharing. At each stage, I asked critical questions: Is data collection proportionate and lawful? Is consent properly obtained? How is data classified and protected? Are quality controls in place? Is processing transparent and fair?

Using data classification principles, I categorized QuickLoan's data as 'Sensitive' due to its inclusion of financial information and PII subject to regulatory protection. This classification revealed gaps in protection mechanisms, particularly the absence of masking in analytics databases and inadequate controls for third-party sharing. The lifecycle lens exposed three critical failure points: lack of consent verification at ingestion, missing data quality controls during preprocessing, and insufficient transparency in automated decision-making.

The Demographic Parity Ratio metric I proposed ensures ethical governance by providing quantifiable, ongoing evidence of fairness in automated lending decisions. Unlike one-time audits, this metric enables continuous monitoring of approval rate disparities across demographic groups. When DPR values fall outside the 0.80-1.25 acceptable range, it triggers immediate investigation and remediation. This metric operationalizes fairness as a measurable business objective rather than an aspirational principle.

The grouped bar chart visualization makes fairness accessible to non-technical stakeholders, including regulators and executive leadership. By tracking DPR monthly, QuickLoan can detect bias drift as the model evolves, demonstrate proactive fairness management to regulators, and build customer trust through transparent reporting. This approach transforms algorithmic fairness from a compliance checkbox into a core operational metric that protects both customers and the business from discriminatory outcomes.

