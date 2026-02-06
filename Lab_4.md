## 

## 

## **Bias Investigation Report: TalentMatch AI (HireScore)**

**By:** Isaac Martey

**Date:** February 6, 2026

**Subject:** Investigation into Algorithmic Bias in the HireScore Ranking System

### **Executive Summary**

* **Overall Bias Severity:** **High**. The system exhibits significant disparate impact across gender, regional origin, and educational background.  
* **Primary Affected Groups:** Female applicants, candidates from Northern and other non-coastal regions, and graduates from "non-tier 1" (outside UG/KNUST/Ashesi) universities.  
* **Top 3 Recommended Actions:**  
  1. **Immediate Feature Removal:** Remove "LinkedIn Connections" and "Graduation Year" (Age proxy).  
  2. **Model Retraining:** Implement **re-weighting** techniques on the training data to balance successful hire ratios.  
  3. **Governance:** Implement a "Human-in-the-Loop" review for any candidate scoring in the 60th–80th percentile to prevent "Automation Bias.

###  **Identify Bias Types**

| Bias Type | Present? | Evidence & Disadvantaged Groups |
| :---- | :---- | :---- |
| **Historical Bias** | **Yes** | **Evidence:** Training data shows 72% of successful hires were Male. The AI has "learned" that being male is a predictor of success. **Disadvantaged:** Female applicants (only 11% of Top 100 despite 28% success rate in history). |
| **Sampling Bias** | **Yes** | **Evidence:** 60% of training data comes from Greater Accra. Regional representation is severely skewed (Accra/Ashanti \= 85%). **Disadvantaged:** Candidates from the Northern, Upper East/West, and Volta regions. |
| **Measurement Bias** | **Yes** | **Evidence:** Features like "LinkedIn connections count" measure networking privilege, not job competency. This unfairly rewards candidates from affluent backgrounds. **Disadvantaged:** Low-income students and those with limited access to professional digital networks. |
| **Proxy Bias** | **Yes** | **Evidence:** "University attended" and "Location of previous employment" act as proxies for socio-economic status and regional origin. **Disadvantaged:** Students from regional technical universities (e.g., Tamale or Ho TU) who may have identical skills but lower "prestige" scores. |

### **Trace the Bias Pipeline**

**\[Historical Hiring Decisions\]** ↓

**\[Training Data Collection\]** ➙ **Bias Point \#1:** **Data Imbalance.** 72% male success rate reinforces a "male-standard" for success.

↓

**\[Feature Selection\]** ➙ **Bias Point \#2:** **Proxy Features.** Including "LinkedIn connections" and "University" correlates with wealth and geography.

↓

**\[Model Training\]**➙ **Bias Point \#3:** **Objective Function.** The model optimizes for "accuracy" relative to historical hires, entrenching past inequalities.

↓

**\[Deployment & Scoring\]** ➙**Bias Point \#4:** **Thresholding.** Setting a high score cutoff (Top 100\) amplifies small differences into total exclusion.

↓

**\[Biased Outcomes\]**

### 

### **Propose Mitigation Strategies**

#### **Immediate Actions (This Week)**

* Feature Removal: Remove LinkedIn Connection Count (wealth proxy) and Age/Graduation Year (ageism risk). These add more noise/bias than true predictive value for skill.  
* Threshold Adjustments: Shift from a "Top 100" list to "Demographic Buckets" (e.g., ensuring Top 20 from each region are visible to recruiters).  
* Output Monitoring: Track the Disparate Impact Ratio (DIR). If the selection rate for women is $\< 80\\%$ of the rate for men, the system should trigger a "Bias Alert."

#### **Short-Term Actions (1-3 Months)**

* Data Collection: Gather "Negative Samples"—data on qualified candidates who were *rejected* in the past but succeeded elsewhere—to fix the "survivorship bias" in the data.  
* Model Retraining: Use Adversarial Debiasng. Train a second model to "guess" the gender/region; the main HireScore model is then penalized if the second model can succeed, forcing it to ignore those traits.  
* Human Oversight: Implement a mandatory audit by a diverse HR panel for any job category where female representation in the Top 10% falls below 40%.

#### **Long-Term Actions (6-12 Months)**

* Fairness Metric: Adopt Equal Opportunity. This ensures that *if* a candidate is qualified, they have an equal chance of being ranked highly, regardless of their university or gender.  
* Process Changes: Move to Blind Ranking for the first stage. Hide names, universities, and locations from recruiters until the interview stage is reached.  
* Transparency: Provide applicants with a "Reasoning Code" (e.g., "Ranked high for Python skills") to comply with Ghana DPA (Section 42\) regarding automated decision-making.

