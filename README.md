## Executive Summary: Retention Collapse Analysis
The March 2025 cohort experienced a critical structural retention failure. Month 1 to Month 2 user retention collapsed from 45% to just 13%—a drop roughly twice as steep as any other historical cohort in the dataset.  
Unknown
+ 2
The problem was not isolated to March; the April 2025 cohort, which onboarded while this issue was still ongoing in the product, shows an identical, highly depressed retention profile (42% to 14%).  
Unknown
### Likely Root Cause: Core Software Anomaly
The precise timing of this collapse strongly points to the app update pushed in early March 2025.  
Unknown
Pre-Update Baseline: Cohorts that signed up before the release (January and February 2025) stabilized at standard benchmarks.  
Unknown
Post-Fix Recovery: Cohorts that onboarded after a hotfix or resolution was deployed (May and June 2025) instantly showed a 2x to 3x improvement in Month 2 retention compared to the infected March/April window.  
Unknown
### Key Dashboard Components & Configurations
The workbook is built to explicitly visualize and highlight this specific software defect using two primary views:  
Unknown
Retention Curve (Line Chart):
Maps out Months Since Signup on the X-axis against the calculated Retention % on the Y-axis.  
Unknown
An explicitly programmed Point Annotation maps to this exact breakdown point to call out the high-priority app bug to stakeholders.  
Unknown
Retention HeatMap (Matrix Grid):
Displays the drop-off dynamically over a diverging color palette (red_green_white_diverging_10_0), explicitly formatted to color-code the percentage drop-offs to make visual scanning of core anomalies instantaneous.  
Unknown
### Data Schema & Calculated Logic
The underlying dataset (nua_cohort_data.csv) tracks metrics on a transactional user level, which the dashboard translates using specific structural logic:  
Unknown
Cohort Size Formulation: Determined using a fixed Level of Detail (LOD) expression:
{FIXED [cohort_month] : COUNTD(IF [months_since_signup] = 0 THEN [user_id] END)}
Is Active Flag: Pushed via a standard boolean check:
IIF(ISNULL([activity_date]), 0, 1)
### Strategic Recommendations
Changelog Audit: Immediately audit the early March 2025 release logs against engineering crash/error-rate logs to pinpoint exactly which breaking change caused the user fallout.  
Unknown
Implementation of Staged Rollouts: Use this specific event as a business case to shift development operations toward a staged-rollout policy (e.g., 5% → 20% → 100%).  
Unknown
Automated Anomaly Alerts: Build real-time, automated threshold alerts on the cohort tracking data to notify product teams immediately if Month 1 or Month 2 metric boundaries dip below normal variance lines again.
