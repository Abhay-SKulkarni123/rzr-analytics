# RZR Analytics Challenge - Lead Quality & Optimization Analysis

Analytics take-home assessment focused on lead quality, quality drivers, and opportunities to improve Closed Rate.

This README documents how to run the analysis, assessment coverage, analytical workflow, key outcomes, methodological decisions, limitations and submission contents.

---

## 1. How to Run

The notebooks are designed to be run sequentially from the repository root.

### Prerequisites

- Python 3.10+
- Jupyter Notebook or JupyterLab
- pandas
- numpy
- matplotlib
- seaborn
- scipy
- xlrd

### Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scipy xlrd jupyter
```

### Start Jupyter

```bash
jupyter notebook
```

Open the `notebooks/` directory and run the notebooks in the following order:

```text
01_data_foundation.ipynb
        ↓
02_quality_analysis.ipynb
        ↓
03_opportunity_analysis.ipynb
        ↓
04_final_case_study.ipynb
```

The notebooks use relative paths to the raw Excel dataset:

```text
data/raw/Analyst_case_study_dataset_1_.xls
```

The repository structure should therefore be preserved when running the notebooks.

---

## 2. Assessment Scope

The assessment asks three core business questions.

### Q1. Lead Quality Trend

- Determine whether lead quality is improving or declining over time.
- Quantify the observed trend in Closed Rate.
- Test whether the observed trend is statistically significant.

### Q2. Drivers of Lead Quality

- Identify segments with differing Closed Rates.
- Examine where the ad was shown.
- Examine form/ad configuration.
- Examine acquisition source and campaign dimensions.
- Examine consumer characteristics such as debt level and state.
- Distinguish descriptive associations from causal conclusions.

### Q3. Opportunity to Reach 9.6%

- Evaluate the stated move from 8.0% to 9.6% Closed Rate.
- Quantify the gap using the observed dataset baseline.
- Evaluate the $30 to $33 CPL scenario.
- Identify practical opportunities to improve lead quality.
- Translate the findings into testable actions.

---

## 3. Assessment Coverage

| Assessment Requirement | Status | Primary Notebook / Deliverable |
|---|---|---|
| Q1 - Lead quality trend over time | Complete | `02_quality_analysis.ipynb` + `04_final_case_study.ipynb` |
| Q1 - Statistical significance | Complete | `02_quality_analysis.ipynb` + `04_final_case_study.ipynb` |
| Q2 - Lead quality drivers / segmentation | Complete | `02_quality_analysis.ipynb` |
| Q2 - Widget / placement / campaign analysis | Complete | `02_quality_analysis.ipynb` |
| Q2 - Consumer / acquisition segmentation | Complete | `02_quality_analysis.ipynb` |
| Q3 - 9.6% opportunity analysis | Complete | `03_opportunity_analysis.ipynb` |
| Q3 - CPL scenario | Complete | `03_opportunity_analysis.ipynb` + `04_final_case_study.ipynb` |
| Q3 - Practical improvement opportunities | Complete | `03_opportunity_analysis.ipynb` + `04_final_case_study.ipynb` |
| Final case-study synthesis | Complete | `04_final_case_study.ipynb` |
| Executive summary | Complete | `reports/RZR_Final_2_Page_Summary.pdf` |

**Analytical coverage: 3/3 core business questions addressed.**

---

## 4. Analysis Workflow

### Notebook 01 - Data Foundation

`notebooks/01_data_foundation.ipynb`

- Loads and inspects the raw lead-level dataset.
- Establishes dataset dimensions and date coverage.
- Audits missing values and duplicate records.
- Checks `VendorLeadID` completeness and uniqueness.
- Reviews key categorical fields.
- Summarizes the available lead outcome structure.
- Documents important data-quality limitations before downstream analysis.

### Notebook 02 - Quality Analysis

`notebooks/02_quality_analysis.ipynb`

- Establishes the overall Closed Rate baseline.
- Reviews the distribution of `CallStatus`.
- Analyses monthly Closed Rate.
- Tests the observed time trend for statistical significance.
- Compares Closed Rate by:
  - Widget
  - Publisher placement
  - Publisher campaign
  - Advertiser campaign
  - Partner
  - Debt level
  - State
- Applies volume thresholds where appropriate to reduce overinterpretation of very small segments.

### Notebook 03 - Opportunity Analysis

`notebooks/03_opportunity_analysis.ipynb`

- Establishes the observed baseline versus the 9.6% target.
- Quantifies the required number of Closed leads.
- Evaluates the $30 to $33 CPL scenario.
- Identifies higher-performing partner, widget, and debt-level segments.
- Models simplified mix-shift scenarios.
- Translates historical segment differences into practical testing opportunities.
- Separates scenario analysis from causal claims.

### Notebook 04 - Final Case Study

`notebooks/04_final_case_study.ipynb`

- Consolidates the main findings from the preceding analysis.
- Answers the three core business questions directly.
- Summarizes the time trend and statistical significance.
- Highlights the most relevant quality drivers.
- Quantifies the opportunity to reach 9.6%.
- Documents recommended actions and the appropriate validation approach.

---

## 5. Key Analytical Outcomes

### Overall Lead Quality

The dataset contains **3,021 leads** and **245 Closed leads**, producing an observed Closed Rate of:

**8.11%**

The advertiser's stated target is:

**9.60%**

At the current lead volume:

- Target Closed leads: **291**
- Current Closed leads: **245**
- Additional Closed leads required: **46**
- Gap from observed rate to target: **1.49 percentage points**

### Lead Quality Trend

Monthly Closed Rate varies considerably:

| Month | Closed Rate |
|---|---:|
| April | 10.8% |
| May | 6.4% |
| June | 10.3% |
| July | 6.2% |
| August | 9.4% |
| September | 4.4% |

A simple linear trend produces:

- Slope: approximately **-0.78 percentage points/month**
- R²: approximately **0.31**
- p-value: approximately **0.248**

The observed direction is downward, but the trend is **not statistically significant at the 5% level**. With only six monthly observations, the result should be interpreted cautiously.

### Lead Quality Drivers

Several higher-volume segments show meaningfully different observed Closed Rates.

**Partner**

- AdKnowledge: approximately **12.3%**
- google: approximately **9.9%**
- yahoo: approximately **7.7%**
- Google: approximately **4.1%**

The separate `google` and `Google` categories should be investigated because inconsistent source naming can fragment acquisition reporting.

**Widget**

- `300250-CreditSolutions`: approximately **15.6%**
- `300250-BlueMeter`: approximately **14.1%**

These are potential candidates for controlled creative/form testing rather than evidence of causal performance.

**Debt Level**

- `70001-90000`: approximately **13.7%**
- `More_than_100000`: approximately **3.7%**

The relationship is not monotonic, so debt level is treated as a segmentation signal rather than a causal explanation.

### Opportunity

The historical data contains several potential avenues for improvement, but no single segment is sufficient on its current volume to be treated as a standalone solution to the 9.6% target.

The opportunity is therefore best viewed as an **incremental lead-mix and traffic-optimization problem**, supported by controlled testing.

---

## 6. Economic Scenario

The assessment specifies a quality improvement from:

**8.0% → 9.6%**

This is mathematically a **20% relative improvement**:

```text
8.0% × 1.20 = 9.6%
```

The assessment also specifies a CPL change from:

**$30 → $33**

This is mathematically a **10% increase**, not 20%:

```text
($33 - $30) / $30 = 10%
```

The analysis retains the explicit values supplied in the assessment and documents the discrepancy rather than silently changing the scenario.

---

## 7. Recommendations

### 1. Test Higher-Performing Widget Configurations

Use the higher-performing historical widgets as candidates for controlled creative/form experiments. Measure whether the observed Closed Rate difference persists prospectively.

### 2. Investigate Acquisition Partner Performance

Review higher-performing partners together with their traffic volume and composition. Resolve the `google` / `Google` naming issue before making detailed source-level allocation decisions.

### 3. Use Consumer Characteristics for Segmentation

Use debt level and other available lead characteristics to identify higher-quality profiles and generate targeting hypotheses. Do not treat these variables as standalone causal explanations.

### 4. Standardize Acquisition Reporting

Consistent partner, campaign, and source definitions will make future quality comparisons more reliable and reduce fragmented reporting.

### 5. Validate Through Controlled Testing

Historical segment differences are observational. Test promising widget and acquisition changes prospectively before scaling traffic allocation.

### 6. Monitor Rate and Absolute Conversions

The target requires approximately **46 additional Closed leads** at the current lead volume. Future experiments should therefore track both Closed Rate and the absolute number of Closed leads.

---

## 8. Key Methodological Decisions

### Primary Quality KPI

`Closed` is used as the primary lead-quality KPI because it represents the advertiser's ultimate measure of success.

### Missing Outcome Information

Missing `CallStatus` values are kept separate and are not automatically classified as either good or bad outcomes.

### Segment Volume

Segment comparisons use minimum-volume thresholds where appropriate to reduce the influence of unstable rates from very small samples.

### Trend Analysis

Monthly Closed Rate is evaluated using a simple linear trend across the six observed months. The result is treated as a concise diagnostic rather than a definitive time-series model.

### Observational Interpretation

Historical segment differences are treated as descriptive evidence. They do not establish that a widget, partner, debt level, or other variable causes higher lead quality.

### Scenario Analysis

Mix-shift calculations are sensitivity illustrations. They assume observed segment performance remains constant and therefore should not be interpreted as forecasts of future performance.

---

## 9. Data Quality & Validation

The initial audit identified:

- **3,021** lead records across **24 columns**
- **No completely duplicated rows**
- **8 missing `VendorLeadID` values**
- **3,012 unique non-null VendorLeadID values**
- `IP Address`: **100% missing**
- `CallStatus`: **70.84% missing**
- `Keyword`: **67.59% missing**
- `AddressScore`: **61.24% missing**
- `Referring Keyword String`: **58.13% missing**
- `PhoneScore`: **53.89% missing**

The data also contains:

- 14 widget variants
- 2 publisher placements
- 2 publisher campaign values
- 2 advertiser campaign values

Known limitations identified during the audit are carried into downstream interpretation rather than silently removed.

---

## 10. Limitations

The main analytical limitations are:

- A large proportion of `CallStatus` values are missing.
- Segment sizes vary considerably, making some observed rates less stable.
- The time trend is based on only six monthly observations.
- Historical segment comparisons are observational and do not establish causality.
- `PublisherZoneName` and `PublisherCampaignName` are closely aligned in this dataset and should not be interpreted as independent drivers.
- `google` and `Google` appear as separate partner categories and require source-definition clarification.
- The 9.6% opportunity analysis assumes the current total lead volume when calculating the required additional Closed leads.
- Mix-shift scenarios assume observed segment performance remains constant and therefore represent sensitivity analysis rather than forecasts.

These limitations are explicitly considered when interpreting the findings and recommendations.

---

## 11. Repository Structure

```text
rzr-analytics-challenge/
├── README.md
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── Analyst_case_study_dataset_1_.xls
│   └── processed/
│
├── notebooks/
│   ├── 01_data_foundation.ipynb
│   ├── 02_quality_analysis.ipynb
│   ├── 03_opportunity_analysis.ipynb
│   └── 04_final_case_study.ipynb
│
├── outputs/
│   ├── figures/
│   └── tables/
│
└── reports/
    └── RZR_Final_2_Page_Summary.pdf
```

---

## 12. Submission Contents

### 1. Executive Summary

A maximum 2-page summary containing:

- Key findings
- Opportunity to reach the 9.6% target
- Recommended actions
- Relevant assumptions
- Key limitations

### 2. Analytical Notebooks

Four notebooks containing the complete analytical workflow:

- Data foundation and quality audit
- Lead quality analysis
- Opportunity and scenario analysis
- Final case-study synthesis

### 3. README

This document provides:

- Run instructions
- Assessment coverage
- Analytical workflow
- Key outcomes
- Methodological decisions
- Data-quality considerations
- Limitations
- Repository structure

---

## 13. Analytical Principle

The analysis prioritizes actionable business decisions while explicitly distinguishing between:

- **Descriptive evidence**
- **Statistical evidence**
- **Scenario analysis**
- **Causal claims**

Where the available data does not support a causal conclusion, the finding is presented as a hypothesis or optimization signal and a controlled test is proposed as the next step.

The central conclusion is therefore not that one historical segment will automatically deliver the target. The data instead identifies **where to test, what to measure, and how to validate whether lead quality can be moved sustainably toward 9.6%**.
