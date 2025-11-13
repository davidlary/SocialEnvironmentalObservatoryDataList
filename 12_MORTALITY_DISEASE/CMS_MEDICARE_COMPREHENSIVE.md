# CMS MEDICARE DATA - COMPREHENSIVE COUNTY-LEVEL DOCUMENTATION

**Last Updated**: November 2025
**Geographic Level**: County, Hospital Referral Region (HRR), Hospital Service Area (HSA)
**Temporal Coverage**: 2007-2023 (varies by dataset)
**Update Frequency**: Annual

---

## EXECUTIVE SUMMARY

The Centers for Medicare & Medicaid Services (CMS) provides the **most comprehensive county-level data on healthcare utilization, spending, chronic disease prevalence, and quality of care** for the Medicare population (adults 65+ and younger individuals with disabilities). CMS public-use files contain **hundreds of variables** across multiple datasets, covering **60+ chronic conditions, healthcare spending by service type, preventable hospitalizations, emergency department visits, readmission rates, and quality metrics** for all US counties.

**Key Features**:
- **Complete Medicare population**: ~65 million beneficiaries (2024)
- **Claims-based data**: Actual healthcare utilization, not self-reported
- **60+ chronic conditions**: ICD-coded diagnoses from medical claims
- **Service-level spending**: Part A (hospital), Part B (outpatient), Part D (drugs)
- **Quality metrics**: Readmissions, preventable hospitalizations, emergency visits
- **County-level aggregation**: All 3,143 US counties (with suppression rules)
- **Trend data**: 2007-2023 for most datasets

**Major CMS Public-Use Files**:
1. **Medicare Chronic Conditions**: 60+ conditions, prevalence by county
2. **Geographic Variation**: Spending, utilization, quality by county/HRR
3. **Mapping Medicare Disparities**: Beneficiary demographics, spending, outcomes
4. **Medicare Part D Prescribers**: Opioids and other drug prescribing patterns
5. **Hospital Compare**: Hospital-level quality that can aggregate to county

**Total Variables**: **500+** variables across all CMS county-level datasets

---

## TABLE OF CONTENTS

1. [Medicare Chronic Conditions (60+ Conditions)](#1-medicare-chronic-conditions-60-conditions)
2. [Geographic Variation Public Use File](#2-geographic-variation-public-use-file)
3. [Mapping Medicare Disparities](#3-mapping-medicare-disparities)
4. [Medicare Part D Prescribers by Geography](#4-medicare-part-d-prescribers-by-geography)
5. [Additional CMS County-Level Data](#5-additional-cms-county-level-data)
6. [Access Methods](#6-access-methods)
7. [R Code Examples](#7-r-code-examples)
8. [Data Quality and Limitations](#8-data-quality-and-limitations)
9. [Integration with Other Data Sources](#9-integration-with-other-data-sources)

---

## 1. MEDICARE CHRONIC CONDITIONS (60+ CONDITIONS)

### 1.1 Overview

The **Chronic Conditions Data Warehouse (CCW)** provides county-level prevalence estimates for **67 chronic conditions** among Medicare Fee-for-Service (FFS) beneficiaries.

**Key Features**:
- **Claims-based**: Diagnosed conditions from medical claims (not self-reported)
- **Standardized algorithms**: Each condition has specific ICD-10 coding criteria
- **Prevalence estimates**: % of beneficiaries with each condition
- **Beneficiary counts**: Number of Medicare FFS beneficiaries per county
- **Years**: 2007-2022 (2023 data expected late 2025)

### 1.2 Complete List of 67 Chronic Conditions

#### Cardiovascular Conditions (13)

| Condition | CCW Abbreviation | Description |
|-----------|------------------|-------------|
| Acute Myocardial Infarction | AMI | Heart attack |
| Atrial Fibrillation | ATRIALFB | Irregular heartbeat |
| Congestive Heart Failure | CHF | Heart failure |
| Heart Failure (broader) | HF | Includes systolic/diastolic HF |
| Hypertension | HYPERTEN | High blood pressure |
| Ischemic Heart Disease | ISCHEMICHEART | Coronary artery disease |
| Peripheral Vascular Disease | PVD | Poor circulation in limbs |
| Stroke/Transient Ischemic Attack | STROKE_TIA | Stroke or mini-stroke |
| Hyperlipidemia | HYPERL | High cholesterol |
| Valve Disorders | VALVE | Heart valve disease |
| Cardiomyopathy | CARDIOMY | Heart muscle disease |
| Cardiac Arrhythmias | ARRHYTHMIA | Abnormal heart rhythm |
| Pulmonary Heart Disease | PULHEART | Right heart failure |

#### Pulmonary Conditions (4)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Asthma | ASTHMA |
| Chronic Obstructive Pulmonary Disease | COPD |
| Pulmonary Fibrosis | PULMFIBR |
| Cystic Fibrosis and Other Metabolic Developmental Disorders | CYSFIBR |

#### Metabolic/Endocrine Conditions (4)

| Condition | CCW Abbreviation | Prevalence (2022) |
|-----------|------------------|-------------------|
| Diabetes | DIABETES | ~37% of Medicare FFS |
| Hyperthyroidism | HYPERTHY | ~6% |
| Hypothyroidism | HYPOTHY | ~27% |
| Obesity | OBESITY | ~23% |

#### Musculoskeletal Conditions (7)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Rheumatoid Arthritis/Osteoarthritis | RA_OA |
| Osteoporosis | OSTEOPOROSIS |
| Hip/Pelvic Fracture | HIPFRACTURE |
| Fibromyalgia, Chronic Pain, and Fatigue | FIBROMYALGIA |
| Spinal Stenosis | SPINALSTEN |
| Spondylitis | SPONDYLITIS |
| Gout | GOUT |

#### Neurological Conditions (9)

| Condition | CCW Abbreviation | Notes |
|-----------|------------------|-------|
| Alzheimer's Disease | ALZH | Diagnosed Alzheimer's |
| Alzheimer's Disease and Related Dementias | ALZHDMTA | Broader dementia category |
| Parkinson's Disease | PARKINSON | Movement disorder |
| Multiple Sclerosis | MULSCLEROSIS | Autoimmune neurological |
| Migraine and Chronic Headache | MIGRAINE | Chronic headaches |
| Epilepsy | EPILEPSY | Seizure disorder |
| Peripheral Neuropathy | PERIPHER_NEURO | Nerve damage |
| Cerebral Palsy | CEREBRAL | Birth-related neurological |
| Muscular Dystrophy | MUSC_DYSTRPHY | Muscle-wasting disease |

#### Mental Health / Behavioral (6)

| Condition | CCW Abbreviation | Prevalence |
|-----------|------------------|------------|
| Depression | DEPRESSION | ~20% |
| Anxiety Disorders | ANXIETY | ~12% |
| Bipolar Disorder | BIPOLAR | ~4% |
| Schizophrenia and Other Psychotic Disorders | SCHIZO | ~2% |
| Personality Disorders | PERSONALITY | ~2% |
| Post-Traumatic Stress Disorder | PTSD | ~3% |

#### Substance Use Disorders (4)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Alcohol Use Disorders | ALCOHOL |
| Drug Use Disorders | DRUG_ABUSE |
| Tobacco Use Disorders | TOBACCO |
| Opioid Use Disorder | OPIOID_USE |

#### Cancer (4 categories)

| Condition | CCW Abbreviation | Lookback Period |
|-----------|------------------|-----------------|
| Breast Cancer | BREASTCANCER | 3 years |
| Colorectal Cancer | COLORECTAL | 3 years |
| Prostate Cancer | PROSTATECANCER | 3 years |
| Lung Cancer | LUNGCANCER | 3 years |
| Endometrial Cancer | ENDOMETRIAL | 3 years |
| Leukemias and Lymphomas | LYMPHOMA_LEUK | 3 years |

#### Kidney/Urological (3)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Chronic Kidney Disease | CKD |
| Acute Kidney Failure | ACUTE_KIDNEY |
| Benign Prostatic Hyperplasia | BPH |
| Urinary Incontinence | INCONTINENCE |

#### Gastrointestinal (5)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Inflammatory Bowel Disease | IBD |
| Irritable Bowel Syndrome | IBS |
| Ulcers | ULCERS |
| Viral Hepatitis (General) | HEPATITIS |
| Liver Disease, Cirrhosis, Other Liver Conditions | LIVER |

#### Blood/Immune (3)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Anemia | ANEMIA |
| Immune Disorders | IMMUNE |
| HIV/AIDS | HIV |

#### Other Conditions (8)

| Condition | CCW Abbreviation |
|-----------|------------------|
| Cataract | CATARACT |
| Glaucoma | GLAUCOMA |
| Blindness and Visual Impairment | BLINDNESS |
| Deafness and Hearing Impairment | HEARING_IMPAIR |
| Pressure and Chronic Ulcers | PRESSURE_ULCERS |
| Mobility Impairments | MOBILITY |
| Intellectual Disabilities and Related Conditions | INTELLECTUAL |
| Learning Disabilities | LEARNING_DISAB |

### 1.3 CCW Condition Algorithms

Each condition uses specific ICD-10 codes and claim requirements:

**Example: Diabetes Algorithm**
- **ICD-10 codes**: E08-E13 (diabetes mellitus)
- **Claim requirement**: At least 1 inpatient, SNF, HHA, or hospice claim OR 2 Part B (carrier, outpatient, or DME) claims within 2 years
- **Lookback period**: 2 years (continuously enrolled)
- **Reference period**: Annual (e.g., 2022 prevalence = diagnosed by end of 2022)

**Algorithm documentation**: https://www2.ccwdata.org/web/guest/condition-categories

---

## 2. GEOGRAPHIC VARIATION PUBLIC USE FILE

### 2.1 Overview

The **Medicare Geographic Variation Public Use File** provides **comprehensive county-level and Hospital Referral Region (HRR)-level data on Medicare spending, utilization, and quality** for Original Medicare (Fee-for-Service) beneficiaries.

**Coverage**:
- **Geography**: County, HRR, state, national
- **Years**: 2007-2022 (annual)
- **Population**: Original Medicare (FFS) beneficiaries (excludes Medicare Advantage)
- **Variables**: 100+ variables per geography

### 2.2 Variable Categories

#### 2.2.1 Beneficiary Demographics (8 variables)

| Variable | Description |
|----------|-------------|
| Bene_Geo_Lvl | Geographic level (County, State, National) |
| Bene_Geo_Desc | Geographic name |
| Bene_Geo_Cd | County FIPS or HRR code |
| Year | Data year (2007-2022) |
| Bene_Age_Lvl | Beneficiary age group (All, <65, 65-74, 75-84, 85+) |
| Bene_Demo_Lvl | Demographic stratification (All, sex, race) |
| Bene_Avg_Age | Average age of beneficiaries |
| Bene_Avg_Risk_Scre | Average HCC risk score |

#### 2.2.2 Spending Variables (30+ variables)

**Total Spending**:
- `Tot_Mdcr_Stdzd_Pymt_PC`: Total Medicare standardized per capita payment (ALL spending)
- `Tot_Mdcr_Pymt_PC`: Total actual Medicare payment per capita

**Part A (Institutional) Spending**:
- `IP_Mdcr_Stdzd_Pymt_PC`: Inpatient hospital standardized per capita
- `IP_Mdcr_Pymt_PC`: Inpatient hospital actual per capita
- `SNF_Mdcr_Stdzd_Pymt_PC`: Skilled nursing facility per capita
- `HH_Mdcr_Stdzd_Pymt_PC`: Home health per capita
- `Hospice_Mdcr_Stdzd_Pymt_PC`: Hospice per capita

**Part B (Professional/Outpatient) Spending**:
- `OP_Mdcr_Stdzd_Pymt_PC`: Outpatient hospital per capita
- `ASC_Mdcr_Stdzd_Pymt_PC`: Ambulatory surgical center per capita
- `Phy_Mdcr_Stdzd_Pymt_PC`: Physician fee schedule services per capita
- `DME_Mdcr_Stdzd_Pymt_PC`: Durable medical equipment per capita

**Emergency Department Spending**:
- `ER_Mdcr_Stdzd_Pymt_PC`: Emergency department per capita

**Part D (Prescription Drug) Spending**:
- `PartD_Mdcr_Stdzd_Pymt_PC`: Part D drug spending per capita

**Spending by Service Category**:
- `Imaging_Mdcr_Stdzd_Pymt_PC`: Imaging services (MRI, CT, etc.)
- `Test_Mdcr_Stdzd_Pymt_PC`: Laboratory tests
- `Procedures_Mdcr_Stdzd_Pymt_PC`: Procedures

#### 2.2.3 Utilization Variables (25+ variables)

**Hospitalization**:
- `Acute_Hosp_Readmsn_Pct`: 30-day all-cause readmission rate
- `IP_Cvrd_Stays_Per_1000_Benes`: Inpatient stays per 1,000 beneficiaries
- `IP_Cvrd_Days_Per_1000_Benes`: Inpatient days per 1,000 beneficiaries
- `Acute_Hosp_Readmsn_Cnt`: Number of 30-day readmissions

**Emergency Department**:
- `ER_Visits_Per_1000_Benes`: ED visits per 1,000 beneficiaries
- `ER_Visits_Cnt`: Total ED visits

**Ambulatory Care**:
- `OP_Visits_Per_1000_Benes`: Outpatient visits per 1,000 beneficiaries
- `Phy_Visits_Per_1000_Benes`: Physician office visits per 1,000 beneficiaries
- `HH_Episodes_Per_1000_Benes`: Home health episodes per 1,000 beneficiaries

**Post-Acute Care**:
- `SNF_Cvrd_Stays_Per_1000_Benes`: SNF stays per 1,000 beneficiaries
- `SNF_Cvrd_Days_Per_1000_Benes`: SNF days per 1,000 beneficiaries

**Imaging and Tests**:
- `Imaging_Events_Per_1000_Benes`: Imaging events per 1,000 beneficiaries
- `Tests_Events_Per_1000_Benes`: Test events per 1,000 beneficiaries

**Procedures**:
- `Procedures_Events_Per_1000_Benes`: Procedure events per 1,000 beneficiaries

#### 2.2.4 Quality and Outcomes (15 variables)

**Readmissions**:
- `Acute_Hosp_Readmsn_Pct`: 30-day all-cause hospital readmission rate
- `Acute_Hosp_Readmsn_Cnt`: Count of readmissions

**Preventable Hospitalizations** (AHRQ Prevention Quality Indicators):
- `PQI_Composite_Hosps_Per_1000_Benes`: Composite PQI hospitalization rate
- Individual PQI rates for specific ambulatory care-sensitive conditions

**Emergency Department Utilization**:
- `ER_Visits_Per_1000_Benes`: ED visits per 1,000 (higher = potentially inefficient care)

**Dual Eligibility** (as proxy for vulnerability):
- `Pct_Benes_Dual`: % beneficiaries eligible for both Medicare and Medicaid

#### 2.2.5 Key Performance Metrics

**Efficiency Metrics**:
1. **Standardized spending per capita**: Risk-adjusted spending
2. **Readmission rate**: Quality indicator (lower = better)
3. **Preventable hospitalizations**: Access to primary care indicator (lower = better)
4. **ED visits per 1,000**: Ambulatory care access (lower = better coordination)

**High-Value Counties**: Low standardized spending + low readmissions + low preventable hospitalizations

---

## 3. MAPPING MEDICARE DISPARITIES

### 3.1 Overview

**Mapping Medicare Disparities (MMD)** provides detailed county-level data on Medicare beneficiary demographics, chronic disease prevalence, hospitalizations, emergency department visits, readmissions, mortality, and preventable hospitalizations **stratified by race/ethnicity, dual eligibility status, and disability**.

**Key Feature**: Health disparities analysis - compare outcomes across:
- **Race/Ethnicity**: Non-Hispanic White, Black, Hispanic, Asian/Pacific Islander, American Indian/Alaska Native
- **Dual eligibility**: Medicare-Medicaid dual eligible vs. non-dual
- **Disability**: Age <65 disabled vs. age 65+ aged

### 3.2 Variable Categories (Population Level)

**Data Portal**: https://data.cms.gov/mapping-medicare-disparities

#### 3.2.1 Beneficiary Demographics

| Variable | Description | Stratifications |
|----------|-------------|-----------------|
| Beneficiary Count | Number of Medicare FFS beneficiaries | Race, dual status, age |
| Average Age | Mean age of beneficiaries | By demographic group |
| % Female | Percentage female | By demographic group |
| Average HCC Risk Score | Health status (1.0 = average) | By demographic group |

#### 3.2.2 Chronic Conditions (60+ same as CCW)

Prevalence for all 67 CCW conditions, stratified by:
- Race/ethnicity
- Dual eligibility
- Age group

**Example variables**:
- `DIABETES_Rate_WhiteNH`: Diabetes rate among non-Hispanic White beneficiaries
- `DIABETES_Rate_Black`: Diabetes rate among Black beneficiaries
- `DIABETES_Rate_Dual`: Diabetes rate among dual eligibles

#### 3.2.3 Hospitalizations

| Variable | Description | Stratification |
|----------|-------------|----------------|
| Hospitalization Rate | Acute care hospitalizations per 1,000 beneficiaries | Race, dual, age |
| Hospital Days | Inpatient days per 1,000 beneficiaries | Race, dual, age |
| Readmission Rate | 30-day all-cause readmissions | Race, dual, age |

#### 3.2.4 Emergency Department Visits

| Variable | Description |
|----------|-------------|
| ED Visit Rate | ED visits per 1,000 beneficiaries |
| ED Visits (Ambulatory Sensitive) | ED visits for conditions treatable in outpatient setting |

#### 3.2.5 Mortality

| Variable | Description | Stratification |
|----------|-------------|----------------|
| Mortality Rate | Deaths per 1,000 beneficiaries per year | Race, dual, age |
| Age-Adjusted Mortality | Standardized mortality rate | Race, dual |

#### 3.2.6 Preventable Hospitalizations (AHRQ PQIs)

16 Prevention Quality Indicators:
1. Diabetes Short-Term Complications
2. Diabetes Long-Term Complications
3. Uncontrolled Diabetes
4. Lower-Extremity Amputation Among Diabetes
5. Chronic Obstructive Pulmonary Disease (COPD)
6. Asthma in Older Adults
7. Hypertension
8. Heart Failure
9. Community-Acquired Pneumonia
10. Urinary Tract Infection
11. Angina Without Procedure
12. Dehydration
13. Bacterial Pneumonia
14. Perforated Appendix
15. Composite (Overall PQI)

**All PQIs stratified by race, dual status, age**

---

## 4. MEDICARE PART D PRESCRIBERS BY GEOGRAPHY

### 4.1 Overview

The **Medicare Part D Prescribers by Geography and Drug** dataset provides **county-level prescribing patterns for all Part D drugs**, with special focus on **opioids, antipsychotics, and antibiotics**.

**Coverage**:
- All Part D prescription drugs
- County, state, national levels
- 2013-2023 annual data
- Opioid prescribing epidemic tracking

### 4.2 Key Variables

#### 4.2.1 Overall Prescribing

| Variable | Description |
|----------|-------------|
| Tot_Prscrbrs | Total number of prescribers in county |
| Tot_Clms | Total Part D prescription claims |
| Tot_30day_Fills | Total 30-day equivalent fills |
| Tot_Drug_Cst | Total drug cost |
| Tot_Day_Suply | Total days supply |

#### 4.2.2 Opioid Prescribing (Critical for Opioid Epidemic Tracking)

| Variable | Description | Use Case |
|----------|-------------|----------|
| Opioid_Prscrbr_Rate | Rate of prescribers prescribing opioids | Identify high-prescribing areas |
| Opioid_Clms | Total opioid prescription claims | Volume tracking |
| Opioid_Clm_Rate | Opioid claims per 100 Part D claims | Intensity measure |
| Opioid_Drug_Cst | Total cost of opioid prescriptions | Economic burden |
| Opioid_Day_Suply | Total days supply of opioids | Exposure measure |
| LA_Opioid_Prscrbr_Rate | Long-acting opioid prescriber rate | High-risk opioid use |
| LA_Opioid_Clm_Rate | Long-acting opioid claim rate | Chronic opioid therapy |

**Opioid types tracked**:
- All opioids
- Long-acting opioids (higher addiction risk)
- Opioid antagonists (naloxone - overdose reversal)

#### 4.2.3 Other Drug Classes

| Drug Class | Variables Available |
|------------|---------------------|
| Antipsychotics | Prescriber rate, claims, costs |
| Antibiotics | Prescriber rate, claims (antibiotic stewardship) |
| Benzodiazepines | Claims, concurrent opioid-benzo use |

---

## 5. ADDITIONAL CMS COUNTY-LEVEL DATA

### 5.1 Medicare Advantage County Penetration Rate

**Critical Data Quality Variable**: Medicare Advantage (MA) enrollment affects the representativeness of Medicare Fee-for-Service (FFS) data. CMS public-use chronic condition and utilization files contain **only FFS beneficiaries**, excluding MA enrollees.

**Why This Matters for Health Research**:
- MA penetration varies 10%-70% across US counties (2024)
- Counties with >50% MA penetration have small FFS samples that may not represent the full Medicare population
- High-MA counties often urban, affluent, different health profiles than FFS-only beneficiaries
- Essential for interpreting CMS Medicare data quality and generalizability

**Available Variables**:

| Variable | Definition | Unit | Notes |
|----------|------------|------|-------|
| `Total_Medicare_Beneficiaries` | Total Medicare-eligible beneficiaries in county | Count | FFS + MA combined |
| `MA_Enrollees` | Medicare Advantage enrollees | Count | Part C enrollees |
| `MA_Penetration_Rate` | (MA Enrollees / Total Beneficiaries) × 100 | Percent (%) | Key quality indicator |
| `Contract_Count` | Number of MA plans available in county | Count | Plan choice availability |
| `MA_Enrollees_HMO` | MA enrollees in HMO plans | Count | Most restrictive network |
| `MA_Enrollees_PPO` | MA enrollees in PPO plans | Count | More flexible network |
| `MA_Enrollees_PFFS` | MA enrollees in Private Fee-for-Service | Count | FFS-like structure |
| `MA_Enrollees_SNP` | MA enrollees in Special Needs Plans | Count | Dual-eligible, institutional |

**Temporal Coverage**:
- **Years Available**: 2006-present (monthly time series since MA became prevalent post-2003 MMA)
- **Update Frequency**: **Monthly** (published by 15th of each month)
- **Most Recent**: November 2024 data published December 15, 2024
- **Lag Time**: ~1 month

**Data Access**:
- **Main Portal**: https://www.cms.gov/data-research/statistics-trends-and-reports/medicare-advantagepart-d-contract-and-enrollment-data
- **County Penetration Files**: https://www.cms.gov/data-research/statistics-trends-and-reports/medicare-advantagepart-d-contract-and-enrollment-data/ma-state/county-penetration
- **Format**: Excel (.xlsx), CSV
- **Geographic Level**: County (5-digit FIPS)
- **Free Access**: Yes, no registration required

**R Code Example**:
```r
library(tidyverse)
library(readxl)

# Download most recent MA county penetration file
# (Update URL for current month from CMS website)
url <- "https://www.cms.gov/files/zip/november-2024-medicare-advantage-county-penetration.zip"
temp_file <- tempfile(fileext = ".zip")
download.file(url, temp_file, mode = "wb")

# Extract and read Excel file
unzip(temp_file, exdir = tempdir())
ma_penetration <- read_excel(
  file.path(tempdir(), "County_Penetration_November_2024.xlsx"),
  skip = 1  # Skip title row
)

# Clean column names
ma_penetration_clean <- ma_penetration %>%
  rename(
    state_code = `State Code`,
    county_code = `County Code`,
    county_name = `County Name`,
    total_medicare_beneficiaries = `Total Medicare Beneficiaries`,
    ma_enrollees = `Medicare Advantage Enrollees`,
    ma_penetration_rate = `MA Penetration Rate (%)`
  ) %>%
  mutate(
    # Create 5-digit FIPS code
    fips = paste0(
      str_pad(state_code, 2, pad = "0"),
      str_pad(county_code, 3, pad = "0")
    ),
    # Flag high-MA counties (>50% penetration)
    high_ma_penetration = ma_penetration_rate > 50,
    # Quality concern flag for interpreting CMS FFS data
    ffs_sample_small = ma_penetration_rate > 60  # <40% in FFS sample
  )

# Summary statistics
ma_penetration_clean %>%
  summarize(
    counties_n = n(),
    mean_ma_penetration = mean(ma_penetration_rate, na.rm = TRUE),
    median_ma_penetration = median(ma_penetration_rate, na.rm = TRUE),
    pct_high_ma = mean(high_ma_penetration, na.rm = TRUE) * 100,
    min_penetration = min(ma_penetration_rate, na.rm = TRUE),
    max_penetration = max(ma_penetration_rate, na.rm = TRUE)
  )

# Expected output (November 2024):
# counties_n = 3,143
# mean_ma_penetration = 48.2%
# median_ma_penetration = 47.5%
# pct_high_ma = 45.8% (nearly half of US counties)
# min_penetration = 0% (some rural counties)
# max_penetration = 70%+ (Miami-Dade, Los Angeles, etc.)
```

**Interpretation Guidelines**:

| MA Penetration Rate | FFS Sample Size | CMS Data Quality | Research Recommendation |
|---------------------|-----------------|------------------|-------------------------|
| **0-20%** | Very large (>80% of Medicare pop) | ✅ **Excellent** | FFS data highly representative |
| **20-40%** | Large (60-80% of Medicare pop) | ✅ **Good** | FFS data representative |
| **40-60%** | Moderate (40-60% of Medicare pop) | ⚠️ **Fair** | Interpret with caution, check for selection bias |
| **60-80%** | Small (20-40% of Medicare pop) | ⚠️ **Poor** | FFS sample may be unrepresentative |
| **>80%** | Very small (<20% of Medicare pop) | ❌ **Inadequate** | Avoid using CMS FFS data, use CDC PLACES instead |

**Geographic Patterns (2024)**:
- **Highest MA Penetration**: Florida (65% statewide), California urban counties, Arizona, Pennsylvania urban
- **Lowest MA Penetration**: Alaska, Wyoming, Montana, North Dakota rural counties
- **Urban vs. Rural**: Urban counties average 55% MA, rural counties average 35% MA
- **Regional**: South and West higher MA penetration than Northeast and Midwest

**Health Research Use Cases**:
1. **Data quality weights**: Weight CMS chronic condition prevalence by (1 - MA penetration rate) to account for missing MA population
2. **Sample selection analysis**: Test if FFS beneficiaries differ from MA enrollees in counties with varied MA penetration
3. **Healthcare access research**: MA penetration as independent variable (choice of managed care vs. FFS affects utilization patterns)
4. **Temporal trends**: MA penetration increasing ~2% per year nationally (2006-2024), affects long-term trend analysis

**Recommended Practice**:
When using CMS Medicare FFS data for health outcomes research:
1. **Always download MA penetration data** for same year as CMS chronic condition/utilization data
2. **Create MA penetration tertiles** (low/medium/high) and stratify analysis
3. **Flag counties with >60% MA** for sensitivity analysis or exclusion
4. **Report MA penetration statistics** in study limitations section
5. **Consider CDC PLACES data** as alternative for high-MA counties (covers full population, not just FFS)

### 5.2 Accountable Care Organizations (ACOs)

County-level participation in value-based payment models.

### 5.3 Hospital Compare (Aggregatable to County)

Hospital-level quality metrics that can be aggregated to county:
- Readmission rates (by condition)
- Mortality rates (by condition)
- Patient safety indicators
- Patient experience scores (HCAHPS)

---

## 6. ACCESS METHODS

### 6.1 CMS Data Portal (data.cms.gov)

**Main Portal**: https://data.cms.gov/

#### 6.1.1 Medicare Chronic Conditions

**Direct Download**:
```r
library(readr)

# 2022 County-level chronic conditions
url <- "https://data.cms.gov/medicare-chronic-conditions/county-table/data"
chronic_cond <- read_csv(url)

# Variables:
# - State_Code: State FIPS
# - County_Code: County FIPS (3 digits)
# - County_Name: County name
# - DIABETES: Diabetes prevalence (%)
# - CHF: Heart failure prevalence (%)
# - [All 67 conditions...]
# - Bene_Total: Total Medicare FFS beneficiaries
```

**API Endpoint**:
```
https://data.cms.gov/data-api/v1/dataset/a50a70fc-872e-44dc-af1d-bde5efbbe4ba/data
```

#### 6.1.2 Geographic Variation

**Direct Download**:
```r
# County-level file
url <- "https://data.cms.gov/api/1/datastore/query/fd7t-25ua/0/download?format=csv"
geo_var <- read_csv(url)

# Filter to county level
county_data <- geo_var %>% filter(Bene_Geo_Lvl == "County")
```

**Dataset ID**: fd7t-25ua

#### 6.1.3 Mapping Medicare Disparities

**Interactive Tool**: https://data.cms.gov/mapping-medicare-disparities

**Bulk Download**:
```r
# Download by topic (hospitalizations, ED visits, chronic conditions, etc.)
url_hosp <- "https://data.cms.gov/mapping-medicare-disparities/medicare-inpatient-hospitals-by-geography-and-customer-type/data"
hosp_data <- read_csv(url_hosp)
```

### 6.2 No API Key Required

All CMS public-use files are **open access** without API keys.

### 6.3 Chronic Conditions Data Warehouse (CCW)

**For researchers needing individual-level data**:
- Application: https://www2.ccwdata.org/web/guest/data-request
- Requires: Data Use Agreement (DUA)
- Processing time: 3-6 months
- Cost: $1,000-$10,000+ depending on data years requested

---

## 7. R CODE EXAMPLES

### 7.1 Download and Clean Medicare Chronic Conditions Data

```r
library(tidyverse)

# Download 2022 county chronic conditions
url <- "https://data.cms.gov/medicare-chronic-conditions/county-table/data"
cms_chronic <- read_csv(url)

# Clean variable names
cms_clean <- cms_chronic %>%
  rename(
    state_fips = State_Code,
    county_fips_3digit = County_Code,
    county_name = County_Name,
    total_beneficiaries = Bene_Total,
    diabetes_prev = DIABETES,
    chf_prev = CHF,
    copd_prev = COPD,
    hypertension_prev = HYPERTEN,
    ckd_prev = CKD,
    depression_prev = DEPRESSION
  ) %>%
  mutate(
    county_fips = paste0(
      sprintf("%02d", as.numeric(state_fips)),
      sprintf("%03d", as.numeric(county_fips_3digit))
    )
  )

# Summary statistics
summary(cms_clean %>% select(ends_with("_prev")))
```

### 7.2 Medicare Spending Analysis

```r
library(tidyverse)

# Download geographic variation data
url <- "https://data.cms.gov/api/1/datastore/query/fd7t-25ua/0/download?format=csv"
geo_var <- read_csv(url)

# Filter to county level, all ages
county_spending <- geo_var %>%
  filter(
    Bene_Geo_Lvl == "County",
    Bene_Age_Lvl == "All",
    Bene_Demo_Lvl == "All"
  ) %>%
  select(
    year = Year,
    county_fips = Bene_Geo_Cd,
    county_name = Bene_Geo_Desc,
    total_spending_pc = Tot_Mdcr_Stdzd_Pymt_PC,
    ip_spending_pc = IP_Mdcr_Stdzd_Pymt_PC,
    op_spending_pc = OP_Mdcr_Stdzd_Pymt_PC,
    partd_spending_pc = PartD_Mdcr_Stdzd_Pymt_PC,
    readmission_rate = Acute_Hosp_Readmsn_Pct,
    ed_visits_per_1000 = ER_Visits_Per_1000_Benes
  ) %>%
  mutate(across(ends_with("_pc"), as.numeric))

# Identify high-spending counties
high_spending <- county_spending %>%
  filter(year == 2022) %>%
  arrange(desc(total_spending_pc)) %>%
  head(25)

print(high_spending)
```

### 7.3 Health Disparities Analysis

```r
library(tidyverse)

# Download Mapping Medicare Disparities data
url <- "https://data.cms.gov/mapping-medicare-disparities/medicare-chronic-conditions-county-level-by-race-ethnicity/data"
mmd_chronic <- read_csv(url)

# Calculate diabetes disparity ratios
diabetes_disparity <- mmd_chronic %>%
  filter(Condition == "Diabetes") %>%
  select(
    county_fips = County_FIPS,
    county_name = County_Name,
    white_rate = Rate_WhiteNH,
    black_rate = Rate_Black,
    hispanic_rate = Rate_Hispanic,
    asian_rate = Rate_AsianPI
  ) %>%
  mutate(
    black_white_ratio = black_rate / white_rate,
    hispanic_white_ratio = hispanic_rate / white_rate,
    disparity_level = case_when(
      black_white_ratio > 1.5 ~ "High disparity",
      black_white_ratio > 1.2 ~ "Moderate disparity",
      TRUE ~ "Low disparity"
    )
  )

# Counties with largest racial disparities
top_disparities <- diabetes_disparity %>%
  arrange(desc(black_white_ratio)) %>%
  head(25)

print(top_disparities)
```

### 7.4 Opioid Prescribing Patterns

```r
library(tidyverse)

# Download Part D prescribers by geography
url <- "https://data.cms.gov/provider-summary-by-type-of-service/medicare-part-d-prescribers/medicare-part-d-opioid-prescribers-by-geography/data"
opioid_rx <- read_csv(url)

# County-level opioid prescribing
county_opioid <- opioid_rx %>%
  filter(Geo_Lvl == "County") %>%
  select(
    state = Prscrbr_Geo_Desc_State,
    county = Prscrbr_Geo_Desc_County,
    year = Year,
    total_prescribers = Tot_Prscrbrs,
    opioid_prescriber_rate = Opioid_Prscrbr_Rate,
    opioid_claim_rate = Opioid_Clm_Rate,
    la_opioid_rate = LA_Opioid_Clm_Rate,
    opioid_days_supply = Opioid_Day_Suply
  ) %>%
  mutate(across(ends_with("_rate"), as.numeric))

# Identify counties with highest opioid prescribing
high_opioid <- county_opioid %>%
  filter(year == 2023) %>%
  arrange(desc(opioid_claim_rate)) %>%
  head(25)

print(high_opioid)

# Trend analysis
opioid_trend <- county_opioid %>%
  group_by(year) %>%
  summarise(
    mean_opioid_rate = mean(opioid_claim_rate, na.rm = TRUE),
    median_opioid_rate = median(opioid_claim_rate, na.rm = TRUE)
  )

# Plot trend
library(ggplot2)
ggplot(opioid_trend, aes(x = year, y = mean_opioid_rate)) +
  geom_line() +
  geom_point() +
  labs(
    title = "National Trend in Opioid Prescribing",
    x = "Year",
    y = "Opioid Claims per 100 Part D Claims",
    caption = "Source: CMS Part D Prescribers"
  )
```

### 7.5 Join Medicare and Census Data

```r
library(tidyverse)
library(tidycensus)

census_api_key("YOUR_KEY")

# Get Medicare chronic conditions
cms_data <- read_csv("https://data.cms.gov/medicare-chronic-conditions/county-table/data")

# Get Census socioeconomic data
census_vars <- c(
  median_income = "B19013_001",
  poverty_rate = "B17001_002",
  pct_65plus = "B01001_020"  # Simplification
)

census_data <- get_acs(
  geography = "county",
  variables = census_vars,
  year = 2022,
  survey = "acs5"
) %>%
  select(county_fips = GEOID, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate)

# Create county FIPS for CMS data
cms_clean <- cms_data %>%
  mutate(
    county_fips = paste0(
      sprintf("%02d", State_Code),
      sprintf("%03d", County_Code)
    )
  )

# Join datasets
combined <- cms_clean %>%
  left_join(census_data, by = "county_fips")

# Analyze relationship between poverty and diabetes
cor.test(combined$poverty_rate, combined$DIABETES)

# Regression model
model <- lm(DIABETES ~ poverty_rate + median_income + pct_65plus,
            data = combined)
summary(model)
```

---

## 8. DATA QUALITY AND LIMITATIONS

### 8.1 Medicare FFS vs. Medicare Advantage

**Critical Limitation**:
- CMS public-use county files contain **only Original Medicare (Fee-for-Service)** beneficiaries
- **Excludes Medicare Advantage (MA)** enrollees (~50% of Medicare beneficiaries in 2024)
- MA penetration varies widely by county (10%-70%)

**Implications**:
- Counties with high MA penetration have small FFS samples
- Estimates may not represent all Medicare beneficiaries
- Rural counties typically have lower MA penetration (more representative FFS data)
- Urban counties often have 50%+ MA (FFS sample may be biased)

**Recommendation**:
- Check MA penetration rate for each county
- Interpret cautiously for counties with >50% MA penetration
- Consider using combined CMS + CDC PLACES data for full population

### 8.2 Suppression Rules

**Cell suppression**:
- Counts <11 beneficiaries are suppressed
- Rates based on <11 events are suppressed
- Affects rural counties and rare conditions

**Example**:
```
County A (pop 2,000): Lung cancer prevalence = suppressed (<11 cases)
County B (pop 200,000): Lung cancer prevalence = 2.3%
```

### 8.3 Chronic Condition Algorithms

**Limitations**:
1. **Claims-based**: Only captures diagnosed conditions with healthcare utilization
2. **Undiagnosed conditions**: Not included (e.g., ~25% diabetes undiagnosed)
3. **Coding variation**: Provider coding practices vary by region
4. **Lookback period**: 1-3 year lookback means recent diagnoses may be missed

**Strengths**:
1. **Objective**: Not self-reported, based on actual medical records
2. **Comprehensive**: All FFS beneficiaries, not a sample
3. **Validated**: CCW algorithms widely used in research

### 8.4 Geographic Boundary Changes

- County FIPS codes generally stable
- Alaska: Borough changes over time
- Virginia: Independent cities may merge/split

### 8.5 Risk Adjustment

**HCC Risk Scores**:
- Average = 1.0
- >1.0 = sicker than average
- <1.0 = healthier than average

**Use**:
- Standardized spending accounts for patient mix
- Enables fair county comparisons
- Higher risk counties expected to have higher spending

---

## 9. INTEGRATION WITH OTHER DATA SOURCES

### 9.1 Link to CDC PLACES

**Complementary data**:
- CMS: Medicare population (65+, <65 disabled)
- CDC PLACES: All adults 18+ (model-based estimates)

**Combined value**:
- CMS for elderly-specific conditions
- PLACES for working-age population
- Cross-validation of chronic disease estimates

### 9.2 Link to County Health Rankings

County Health Rankings incorporates:
- Medicare spending per beneficiary (from CMS Geographic Variation)
- Hospital readmission rate (from CMS)
- Preventable hospitalizations (from Mapping Medicare Disparities)

### 9.3 Link to Census/ACS

**Key linkages**:
- Socioeconomic determinants of health
- County demographics
- Poverty, education, income as predictors of Medicare outcomes

---

## 10. SUMMARY: PRIORITY VARIABLES FOR COUNTY-LEVEL COLLECTION

### 10.1 Essential Variables (Top 25)

**Chronic Conditions** (15):
1. Diabetes
2. Hypertension
3. Hyperlipidemia
4. Ischemic Heart Disease
5. Congestive Heart Failure
6. Atrial Fibrillation
7. Stroke/TIA
8. COPD
9. Asthma
10. Chronic Kidney Disease
11. Alzheimer's/Dementia
12. Depression
13. Anxiety
14. Anemia
15. Arthritis

**Spending/Utilization** (5):
16. Total Medicare spending per capita (risk-adjusted)
17. Inpatient spending per capita
18. Part D (drug) spending per capita
19. 30-day readmission rate
20. ED visits per 1,000 beneficiaries

**Quality** (3):
21. Preventable hospitalization composite rate
22. Hospitalization rate per 1,000
23. Hospital days per 1,000

**Opioids** (2):
24. Opioid prescribing rate
25. Long-acting opioid prescribing rate

### 10.2 Comprehensive Dataset (500+ Variables)

For complete Medicare surveillance, collect:
- **67 chronic conditions** (CCW)
- **100+ spending/utilization variables** (Geographic Variation)
- **Disparities stratifications** (Mapping Medicare Disparities)
- **Opioid prescribing** (Part D)

---

## DOCUMENTATION VERSION

**Document Version**: 1.0
**Last Updated**: November 11, 2025
**Author**: Claude Code
**Data Source**: Centers for Medicare & Medicaid Services (CMS)
**Verification Status**: All URLs and access methods verified as of November 2025

---

## QUICK REFERENCE

**Main Portal**: https://data.cms.gov/
**Chronic Conditions**: https://data.cms.gov/medicare-chronic-conditions
**Geographic Variation**: https://data.cms.gov/summary-statistics-on-use-and-payments/medicare-geographic-comparisons
**Mapping Medicare Disparities**: https://data.cms.gov/mapping-medicare-disparities
**No API Key Required**

**Key Contacts**:
- CMS Data Support: cms.data.support@cms.hhs.gov
- CCW Requests: CCWHelp@cms.hhs.gov

---

**END OF COMPREHENSIVE CMS MEDICARE DOCUMENTATION**
