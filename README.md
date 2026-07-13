## Executive Summary: Retention Collapse Analysis
The **March 2025 cohort** experienced a critical structural retention failure. Month 1 to Month 2 user retention **collapsed from 45% to just 13%**—a drop roughly **twice as steep** as any other historical cohort in the dataset. 

The problem was not isolated to March; the **April 2025 cohort**, which onboarded while this issue was still ongoing in the product, shows an identical, highly depressed retention profile (**42% to 14%**). 

---

### Likely Root Cause: Core Software Anomaly
The precise timing of this collapse strongly points to the **app update pushed in early March 2025**. 
* **Pre-Update Baseline:** Cohorts that signed up before the release (January and February 2025) stabilized at standard benchmarks.
* **Post-Fix Recovery:** Cohorts that onboarded after a hotfix or resolution was deployed (May and June 2025) instantly showed a **2x to 3x improvement** in Month 2 retention compared to the infected March/April window.

---

### Key Dashboard Components & Configurations
The workbook is built to explicitly visualize and highlight this specific software defect using two primary views:

1. **Retention Curve (Line Chart):** 
   * Maps out `Months Since Signup` on the X-axis against the calculated `Retention %` on the Y-axis.
   * An explicitly programmed **Point Annotation** maps to this exact breakdown point to call out the high-priority app bug to stakeholders.
2. **Retention HeatMap (Matrix Grid):**
   * Displays the drop-off dynamically over a diverging color palette (`red_green_white_diverging_10_0`), explicitly formatted to color-code the percentage drop-offs to make visual scanning of core anomalies instantaneous.

---

### Data Schema & Calculated Logic
The underlying dataset (`nua_cohort_data.csv`) tracks metrics on a transactional user level, which the dashboard translates using specific structural logic:
* **`Cohort Size` Formulation:** Determined using a fixed Level of Detail (LOD) expression: 
  $$\{FIXED\ [cohort\_month]\ :\ COUNTD(IF\ [months\_since\_signup]\ =\ 0\ THEN\ [user\_id]\ END)\}$$
* **`Is Active` Flag:** Pushed via a standard boolean check: 
  $$\text{IIF(ISNULL([activity\_date]), 0, 1)}$$

---

### Strategic Recommendations
* **Changelog Audit:** Immediately audit the early March 2025 release logs against engineering crash/error-rate logs to pinpoint exactly which breaking change caused the user fallout.
* **Implementation of Staged Rollouts:** Use this specific event as a business case to shift development operations toward a **staged-rollout policy** (e.g., 5% $\rightarrow$ 20% $\rightarrow$ 100%).
* **Automated Anomaly Alerts:** Build real-time, automated threshold alerts on the cohort tracking data to notify product teams immediately if Month 1 or Month 2 metric boundaries dip below normal variance lines again.
