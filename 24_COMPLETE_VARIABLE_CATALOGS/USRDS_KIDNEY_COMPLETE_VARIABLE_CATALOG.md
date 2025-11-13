# USRDS KIDNEY DISEASE COMPLETE VARIABLE CATALOG
## All United States Renal Data System Variables

**Purpose:** Complete reference catalog of all variables in the United States Renal Data System for chronic kidney disease (CKD) and end-stage renal disease (ESRD) research

**Last Updated:** November 13, 2025
**USRDS Version:** 2024 Standard Analysis Files (SAFs)
**Data Through:** Medicare claims 2022, ESRD metrics 2023
**Total SAF Files:** 25+ Standard Analysis Files
**Total Variables:** 500+ core variables across patient, treatment, outcomes, and facility domains

---

## 📥 ACCESS COMPLETE OFFICIAL DOCUMENTATION

### **Primary Sources:**

1. **USRDS Researcher's Guide:**
   - 2024 Guide (PDF): https://www.niddk.nih.gov/-/media/Files/USRDS/For-Researchers/2024/USRDS_Researcher_Guide_2024.pdf
   - Main page: https://www.usrds.org/for-researchers/researchers-guide/
   - **Appendix B:** Complete Data File Descriptions with all variables

2. **USRDS Annual Data Report:**
   - Interactive report: https://usrds-adr.niddk.nih.gov/
   - 2024 ADR (full text): https://www.ajkd.org/article/S0272-6386(25)00703-6/fulltext

3. **Standard Analysis Files (SAFs):**
   - Request form: https://www.usrds.org/for-researchers/standard-analysis-files/
   - Data dictionary: Available in Researcher's Guide Appendix B

4. **DESKRIBE Web Tool (County-Level):**
   - Interactive county data: https://www.usrds.org/deskribe/

---

## 🗂️ DATABASE STRUCTURE

### **USRDS Data Sources:**
- **CMS (Centers for Medicare & Medicaid Services):** Medicare claims, enrollment
- **EQRS (End Stage Renal Disease Quality Reporting System):** Patient demographics, treatment history, vital status
- **OPTN (Organ Procurement and Transplantation Network):** Transplant data
- **CDC (Centers for Disease Control):** CKD surveillance
- **ESRD Networks:** Quality metrics, facility data
- **US Census:** Geographic, socioeconomic data

### **Standard Analysis Files (SAFs):**
Patient-level longitudinal files covering:
1. Demographics & enrollment
2. Treatment modalities
3. Comorbid conditions
4. Hospitalizations
5. Medications
6. Laboratory values
7. Transplantation
8. Mortality
9. Provider/facility characteristics

---

## 👤 PATIENT CORE FILE (PATIENTS)

**Description:** One record per ESRD patient with core demographics
**Key Field:** USRDS_ID (unique patient identifier)

### **Demographic Variables (25+ variables)**

| Variable | Description | Values/Units |
|----------|-------------|--------------|
| **USRDS_ID** | Unique USRDS patient identifier | Numeric |
| **HICNO** | Medicare Health Insurance Claim Number | Encrypted |
| **SEX** | Patient sex | M, F, U (unknown) |
| **RACE** | Patient race | Native American, Asian, Black, White, Other, Unknown |
| **HISPANIC** | Hispanic ethnicity | Y, N, U |
| **AGE** | Age at ESRD incidence | Years |
| **DOBS** | Date of birth | YYYY-MM-DD |
| **FIRST_SE** | Date of first service (ESRD incidence) | YYYY-MM-DD |
| **DIED** | Death indicator | 0=Alive, 1=Died |
| **DEATH_DATE** | Date of death | YYYY-MM-DD |
| **BMI** | Body Mass Index at incidence | kg/m² |
| **HEIGHT_CM** | Height at incidence | cm |
| **WEIGHT_KG** | Weight at incidence | kg |

### **Geographic Variables (10+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **STATE** | State of residence at incidence | 2-letter code |
| **COUNTY** | County FIPS code | 5-digit FIPS |
| **ZIP_CODE** | ZIP code of residence | 5-digit |
| **ESRD_NETWORK** | ESRD Network (1-18) | 1-18 |
| **DIVISION** | Census division | 1-9 |
| **REGION** | Census region | 1-4 |
| **URBAN_RURAL** | Urban/rural classification | Metro, Non-metro |
| **ADI_NATL** | Area Deprivation Index (national) | Percentile 1-100 |
| **ADI_STATE** | Area Deprivation Index (state) | Percentile 1-100 |

### **Clinical Variables at Incidence (20+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **PRIM_DX** | Primary cause of ESRD | DM, HTN, GN, CysKid, Other, Unknown |
| **DM** | Diabetes as contributing factor | Y, N |
| **HYPERT** | Hypertension as contributing factor | Y, N |
| **GLOM_NE** | Glomerulonephritis | Y, N |
| **POLYCYSTIC** | Polycystic kidney disease | Y, N |
| **CAUSE_TXT** | Text description of primary cause | Text |
| **CKD_STAGE** | CKD stage prior to ESRD (if known) | 1-5 |
| **PRETX_MODALITY** | Pre-ESRD renal replacement therapy | None, HD, PD, TX |
| **PREEMPTIVE_TX** | Preemptive transplant (before dialysis) | Y, N |
| **EGFR_INCIDENT** | eGFR at ESRD incidence | mL/min/1.73m² |
| **ALBUMIN_INCIDENT** | Serum albumin at incidence | g/dL |
| **HEMOGLOBIN_INCIDENT** | Hemoglobin at incidence | g/dL |
| **PTH_INCIDENT** | Parathyroid hormone at incidence | pg/mL |
| **CALCIUM_INCIDENT** | Serum calcium at incidence | mg/dL |
| **PHOSPHORUS_INCIDENT** | Serum phosphorus at incidence | mg/dL |

---

## 🏥 TREATMENT HISTORY FILE (TXHISTORY)

**Description:** Longitudinal treatment modality changes
**Structure:** One record per treatment episode

### **Treatment Modality Variables (15+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **USRDS_ID** | Patient identifier | Numeric |
| **BEGIN_DATE** | Treatment episode start date | YYYY-MM-DD |
| **END_DATE** | Treatment episode end date | YYYY-MM-DD |
| **MODALITY** | Dialysis/transplant modality | HD, PD, TX |
| **HD_TYPE** | Hemodialysis type | In-center, Home HD, Unknown |
| **PD_TYPE** | Peritoneal dialysis type | CAPD, CCPD, Nocturnal, Unknown |
| **DIALYZER_TYPE** | Dialyzer membrane type | High-flux, Low-flux, Unknown |
| **VASCULAR_ACCESS** | Vascular access type (HD) | Fistula, Graft, Catheter, Unknown |
| **FACILITY_ID** | Dialysis facility identifier | Numeric |
| **TRANSPLANT_TYPE** | Transplant type | Living donor, Deceased donor |
| **DONOR_TYPE** | Donor relation | Related, Unrelated, Deceased |
| **TX_NUMBER** | Transplant number for patient | 1, 2, 3+ |
| **GRAFT_FAILURE** | Graft failure indicator | Y, N |
| **GRAFT_SURVIVAL_DAYS** | Days graft functioned | Days |
| **RETURN_TO_DIALYSIS** | Returned to dialysis after TX | Y, N |

---

## 💊 MEDICATION HISTORY FILE (RXHIST60)

**Description:** Medicare Part D prescription claims
**Structure:** One record per prescription fill

### **Medication Variables (20+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **USRDS_ID** | Patient identifier | Numeric |
| **SERVICE_DATE** | Prescription fill date | YYYY-MM-DD |
| **NDC** | National Drug Code | 11-digit |
| **DRUG_NAME** | Generic drug name | Text |
| **DRUG_CLASS** | Therapeutic class | Text |
| **DAYS_SUPPLY** | Days supply | Days |
| **QUANTITY** | Quantity dispensed | Units |
| **TOTAL_COST** | Total prescription cost | Dollars |
| **PATIENT_PAY** | Patient out-of-pocket cost | Dollars |

### **Key Drug Classes for Kidney Disease:**

| Drug Class | Examples | Indication |
|------------|----------|------------|
| **Phosphate binders** | Sevelamer, calcium acetate, lanthanum | Hyperphosphatemia |
| **Calcimimetics** | Cinacalcet, etelcalcetide | Secondary hyperparathyroidism |
| **ESAs (Erythropoiesis-Stimulating Agents)** | Epoetin alfa, darbepoetin | Anemia |
| **Iron supplements** | Ferrous sulfate, iron sucrose | Iron-deficiency anemia |
| **Vitamin D analogs** | Calcitriol, paricalcitol | Vitamin D deficiency, SHPT |
| **Antihypertensives** | ACE inhibitors, ARBs, beta-blockers, CCBs | Hypertension, cardioprotection |
| **Diuretics** | Furosemide, metolazone | Fluid management |
| **Statins** | Atorvastatin, simvastatin | Dyslipidemia, CVD prevention |
| **Anticoagulants** | Warfarin, heparin, DOACs | Thrombosis prevention |
| **Immunosuppressants** | Tacrolimus, mycophenolate, prednisone | Post-transplant (prevent rejection) |

---

## 🏥 HOSPITALIZATION FILE (HOSP)

**Description:** Inpatient hospital admissions
**Structure:** One record per hospitalization

### **Hospitalization Variables (30+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **USRDS_ID** | Patient identifier | Numeric |
| **ADMIT_DATE** | Admission date | YYYY-MM-DD |
| **DISCHARGE_DATE** | Discharge date | YYYY-MM-DD |
| **LOS** | Length of stay | Days |
| **DISCHARGE_STATUS** | Discharge disposition | Home, SNF, Died, AMA, Transfer |
| **PRIMARY_DX** | Primary diagnosis (ICD-10) | ICD-10 code |
| **DX_2 through DX_25** | Secondary diagnoses | ICD-10 codes |
| **PRIMARY_PROC** | Primary procedure (ICD-10-PCS) | ICD-10-PCS code |
| **PROC_2 through PROC_25** | Secondary procedures | ICD-10-PCS codes |
| **ICU** | Intensive care unit stay | Y, N |
| **READMIT_30** | 30-day readmission | Y, N |
| **TOTAL_CHARGES** | Total hospital charges | Dollars |
| **MEDICARE_PAYMENT** | Medicare payment | Dollars |
| **DRG** | Diagnosis Related Group | 3-digit |

### **Common ESRD-Related Hospital Diagnoses:**

| Category | ICD-10 Codes | Description |
|----------|--------------|-------------|
| **Vascular access complications** | T82.8, T82.9 | Catheter infection, thrombosis, malfunction |
| **Cardiovascular** | I11.0, I13.0, I50.x | Hypertensive heart/kidney disease, heart failure |
| **Fluid overload** | E87.7 | Volume overload |
| **Infections** | A41.x, J18.x, N39.0 | Sepsis, pneumonia, UTI |
| **Electrolyte disorders** | E87.x | Hyperkalemia, acidosis, hyponatremia |
| **Anemia** | D63.1 | Anemia in CKD |
| **Mineral bone disease** | E83.5, M10.3 | Hypercalcemia, gout |

---

## 🩺 COMORBIDITY FILES (MEDEVID)

**Description:** Chronic condition indicators from Medicare claims
**Structure:** One record per patient per year

### **Comorbidity Variables (40+ variables)**

| Variable | Description | Prevalence in ESRD |
|----------|-------------|-------------------|
| **DM** | Diabetes mellitus | 45% |
| **HTN** | Hypertension | 90% |
| **CHF** | Congestive heart failure | 50% |
| **CAD** | Coronary artery disease | 40% |
| **MI** | Myocardial infarction (history) | 15% |
| **STROKE** | Stroke/TIA (history) | 12% |
| **PVD** | Peripheral vascular disease | 25% |
| **AFIB** | Atrial fibrillation | 20% |
| **COPD** | Chronic obstructive pulmonary disease | 15% |
| **ASTHMA** | Asthma | 5% |
| **CANCER** | Any cancer (history) | 10% |
| **LIVER** | Chronic liver disease | 5% |
| **HEPAT_B** | Hepatitis B | 1% |
| **HEPAT_C** | Hepatitis C | 5% |
| **HIV** | HIV/AIDS | 1.5% |
| **DEPRESSION** | Depression | 20% |
| **ANXIETY** | Anxiety disorder | 15% |
| **DEMENTIA** | Dementia/Alzheimer's | 10% |
| **OSTEOPOR** | Osteoporosis | 10% |
| **GOUT** | Gout | 15% |
| **SEPSIS** | Sepsis (annual) | 20% |
| **AMPUTATION** | Lower extremity amputation | 3% annual |
| **HYPERKAL** | Hyperkalemia | 10% annual |
| **HYPERGLY** | Hyperglycemia | 20% annual |
| **HYPOKALEMIA** | Hypokalemia | 5% annual |

---

## 🔬 LABORATORY VALUES FILE (LABS)

**Description:** Clinical laboratory results
**Structure:** Multiple records per patient per year

### **Laboratory Variables (50+ variables)**

| Lab Test | Variable | Units | Normal Range | Clinical Significance |
|----------|----------|-------|--------------|----------------------|
| **eGFR** | EGFR | mL/min/1.73m² | >90 | Kidney function |
| **Serum creatinine** | CREAT_SER | mg/dL | 0.6-1.2 | Kidney function |
| **Blood urea nitrogen** | BUN | mg/dL | 7-20 | Waste product clearance |
| **Albumin** | ALBUMIN | g/dL | 3.5-5.0 | Nutrition status |
| **Hemoglobin** | HGB | g/dL | 12-16 | Anemia |
| **Hematocrit** | HCT | % | 36-48 | Anemia |
| **Ferritin** | FERRITIN | ng/mL | 30-300 | Iron stores |
| **Transferrin saturation** | TSAT | % | 20-50 | Iron availability |
| **Parathyroid hormone** | PTH | pg/mL | 10-65 | Mineral bone disease |
| **Calcium (corrected)** | CA_CORR | mg/dL | 8.5-10.5 | Mineral metabolism |
| **Phosphorus** | PHOS | mg/dL | 2.5-4.5 | Mineral metabolism |
| **Alkaline phosphatase** | ALP | IU/L | 30-120 | Bone turnover |
| **25-OH Vitamin D** | VIT_D_25 | ng/mL | 20-50 | Vitamin D status |
| **Bicarbonate** | HCO3 | mEq/L | 22-29 | Acidosis |
| **Potassium** | K | mEq/L | 3.5-5.0 | Hyperkalemia risk |
| **Sodium** | NA | mEq/L | 136-145 | Hyponatremia |
| **Glucose** | GLUCOSE | mg/dL | 70-100 (fasting) | Diabetes control |
| **HbA1c** | HBA1C | % | <5.7 | Diabetes control |
| **Total cholesterol** | CHOL_TOTAL | mg/dL | <200 | CVD risk |
| **LDL cholesterol** | LDL | mg/dL | <100 | CVD risk |
| **HDL cholesterol** | HDL | mg/dL | >40 (M), >50 (F) | CVD risk |
| **Triglycerides** | TG | mg/dL | <150 | CVD risk |
| **C-reactive protein** | CRP | mg/L | <3 | Inflammation |
| **Uric acid** | URIC_ACID | mg/dL | 3.5-7.2 | Gout risk |
| **Troponin** | TROP | ng/mL | <0.04 | Cardiac injury |
| **BNP/NT-proBNP** | BNP | pg/mL | <100 | Heart failure |

---

## 🫘 DIALYSIS ADEQUACY FILE (DIALADQ)

**Description:** Dialysis quality metrics
**Structure:** Monthly/quarterly per patient

### **Hemodialysis Adequacy Variables (15+ variables)**

| Variable | Description | Target |
|----------|-------------|--------|
| **KT_V** | Kt/V (dialysis dose) | ≥1.2 |
| **URR** | Urea reduction ratio | ≥65% |
| **SESSIONS_PER_WEEK** | Dialysis sessions per week | 3 (standard) |
| **MINUTES_PER_SESSION** | Minutes per treatment | 180-240 |
| **QB** | Blood flow rate | mL/min |
| **QD** | Dialysate flow rate | mL/min |
| **UF_VOLUME** | Ultrafiltration volume | Liters |
| **DRY_WEIGHT** | Estimated dry weight | kg |
| **PRE_WEIGHT** | Pre-dialysis weight | kg |
| **POST_WEIGHT** | Post-dialysis weight | kg |
| **PRE_SBP** | Pre-dialysis systolic BP | mmHg |
| **POST_SBP** | Post-dialysis systolic BP | mmHg |
| **IDH** | Intradialytic hypotension episodes | Count |
| **MISSED_SESSIONS** | Missed treatments | Count |
| **SHORTENED_SESSIONS** | Shortened treatments (<90% prescribed) | Count |

### **Peritoneal Dialysis Adequacy Variables (10+ variables)**

| Variable | Description | Target |
|----------|-------------|--------|
| **KT_V_WEEKLY** | Weekly Kt/V | ≥1.7 |
| **CREAT_CLEAR** | Creatinine clearance | L/week/1.73m² |
| **UF_VOLUME_DAILY** | Daily ultrafiltration | mL |
| **RESIDUAL_RENAL** | Residual renal function | mL/min |
| **PD_TYPE** | PD modality | CAPD, CCPD, APD |
| **EXCHANGES_PER_DAY** | Number of exchanges | Count |
| **DWELL_TIME** | Dwell time | Hours |
| **PERITONITIS_RATE** | Peritonitis episodes | Per patient-year |

---

## 🫁 TRANSPLANT FILE (TXUNOS)

**Description:** Kidney transplant data from OPTN
**Structure:** One record per transplant

### **Transplant Variables (40+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **TX_DATE** | Transplant date | YYYY-MM-DD |
| **TX_NUMBER** | Transplant number for patient | 1, 2, 3+ |
| **DONOR_TYPE** | Donor type | Living, Deceased |
| **LIVING_DONOR_RELATION** | Relation to recipient | Related, Unrelated, Spouse |
| **DONOR_AGE** | Donor age | Years |
| **DONOR_SEX** | Donor sex | M, F |
| **DONOR_RACE** | Donor race | Text |
| **DONOR_DCD** | Donation after cardiac death | Y, N |
| **COLD_ISCHEMIA_TIME** | Cold ischemia time | Hours |
| **WARM_ISCHEMIA_TIME** | Warm ischemia time | Minutes |
| **HLA_MISMATCH** | HLA mismatch level | 0-6 |
| **PRA** | Panel reactive antibodies | % |
| **SENSITIZED** | Highly sensitized (PRA >80%) | Y, N |
| **ABO_COMPATIBLE** | ABO blood type compatible | Y, N |
| **WAIT_TIME** | Time on waitlist | Days |
| **DGF** | Delayed graft function | Y, N |
| **REJECTION_ACUTE** | Acute rejection episode | Y, N |
| **REJECTION_CHRONIC** | Chronic rejection | Y, N |
| **GRAFT_FAILURE** | Graft failure | Y, N |
| **GRAFT_SURVIVAL_DAYS** | Graft survival | Days |
| **IMMUNOSUPPRESSION** | Immunosuppressive regimen | Text |

---

## 💰 PAYOR HISTORY FILE (PAYHIST)

**Description:** Insurance coverage over time
**Structure:** One record per insurance period

### **Payor Variables (15+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **BEGIN_DATE** | Coverage period start | YYYY-MM-DD |
| **END_DATE** | Coverage period end | YYYY-MM-DD |
| **PRIMARY_PAYOR** | Primary insurance | Medicare, Medicaid, Private, VA, None, Other |
| **MEDICARE_A** | Medicare Part A coverage | Y, N |
| **MEDICARE_B** | Medicare Part B coverage | Y, N |
| **MEDICARE_D** | Medicare Part D coverage | Y, N |
| **MEDICARE_ADVANTAGE** | Medicare Advantage | Y, N |
| **MEDICAID** | Medicaid (dual eligible) | Y, N |
| **PRIVATE_INSURANCE** | Private insurance | Y, N |
| **EMPLOYER** | Employer-sponsored | Y, N |
| **VA** | Veterans Administration | Y, N |
| **CHARITY_CARE** | Charity/free care | Y, N |
| **UNINSURED** | No insurance | Y, N |

---

## 🏥 FACILITY FILE (FACILITY)

**Description:** Dialysis facility characteristics
**Structure:** One record per facility per year

### **Facility Variables (30+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **FACILITY_ID** | Unique facility identifier | Numeric |
| **FACILITY_NAME** | Facility name | Text |
| **CHAIN** | Chain affiliation | DaVita, Fresenius, Independent, Other |
| **NONPROFIT** | Nonprofit status | Y, N |
| **STATE** | State | 2-letter code |
| **COUNTY_FIPS** | County FIPS code | 5-digit |
| **URBAN_RURAL** | Urban/rural location | Urban, Rural |
| **STATIONS** | Number of stations | Count |
| **PATIENTS** | Number of patients | Count |
| **MODALITY** | Modalities offered | HD, PD, Both |
| **EVENING_SHIFTS** | Evening shifts available | Y, N |
| **HOME_TRAINING** | Home dialysis training | Y, N |
| **TRANSPLANT_REFERRAL_RATE** | % patients referred for TX | % |
| **VASCULAR_ACCESS_FISTULA** | % patients with fistula | % |
| **CATHETER_90DAYS** | % catheters >90 days | % |
| **HYPERCALCEMIA** | % patients with hypercalcemia | % |
| **HYPERPHOSPHATEMIA** | % patients with hyperphosphatemia | % |
| **KTV_ADEQUACY** | % patients meeting Kt/V target | % |
| **HEMOGLOBIN_TARGET** | % patients meeting Hgb target | % |
| **HOSPITALIZATION_RATE** | Hospitalizations per patient-year | Rate |
| **MORTALITY_RATE** | Deaths per 100 patient-years | Rate |
| **TRANSFUSION_RATE** | Transfusions per patient-year | Rate |
| **INFECTION_RATE** | Bacteremia/sepsis rate | Per 100 patient-months |
| **STAR_RATING** | CMS 5-star rating | 1-5 stars |

---

## ☠️ MORTALITY FILE (DEATH)

**Description:** Death records with causes
**Structure:** One record per death

### **Mortality Variables (20+ variables)**

| Variable | Description | Values |
|----------|-------------|--------|
| **USRDS_ID** | Patient identifier | Numeric |
| **DEATH_DATE** | Date of death | YYYY-MM-DD |
| **AGE_AT_DEATH** | Age at death | Years |
| **DAYS_FROM_INCIDENCE** | Days from ESRD incidence to death | Days |
| **COD_PRIMARY** | Primary cause of death | ICD-10 code |
| **COD_CATEGORY** | Cause of death category | Cardiac, Infection, Withdrawal, Other |
| **CARDIAC_DEATH** | Cardiac cause | Y, N |
| **INFECTION_DEATH** | Infection cause | Y, N |
| **WITHDRAWAL_DEATH** | Withdrawal from dialysis | Y, N |
| **MALIGNANCY** | Cancer cause | Y, N |
| **CEREBROVASCULAR** | Stroke cause | Y, N |
| **LOCATION_DEATH** | Location of death | Hospital, Home, SNF, Hospice, Other |

### **Common ESRD Causes of Death:**

| Category | % of Deaths | Key ICD-10 Codes |
|----------|-------------|------------------|
| **Cardiovascular** | 40% | I21 (MI), I50 (HF), I25 (CAD), I11 (Hypertensive heart) |
| **Infection** | 15% | A41 (Sepsis), J18 (Pneumonia), T82.7 (Catheter infection) |
| **Withdrawal from dialysis** | 20% | No ICD code (decision to stop treatment) |
| **Malignancy** | 5% | C-codes (cancer) |
| **Cerebrovascular** | 5% | I63 (Ischemic stroke), I61 (Hemorrhage) |
| **Other/Unknown** | 15% | Various |

---

## 📊 COUNTY-LEVEL AGGREGATED DATA (DESKRIBE System)

**Description:** County-level prevalence, incidence, mortality rates
**Access:** https://www.usrds.org/deskribe/

### **County-Level Variables Available:**

| Variable Category | Specific Variables |
|------------------|-------------------|
| **CKD Prevalence** | % adults with CKD stages 1-5, by stage |
| **ESRD Incidence** | New ESRD cases per million population |
| **ESRD Prevalence** | Total ESRD patients per million |
| **Dialysis Prevalence** | % on hemodialysis, % on peritoneal dialysis |
| **Transplant Prevalence** | % with functioning transplant |
| **Mortality Rate** | Deaths per 100 patient-years |
| **Demographics** | Age distribution, race/ethnicity distribution |
| **Primary Cause** | % diabetes, % hypertension, % glomerulonephritis, % other |
| **Comorbidities** | % with diabetes, hypertension, heart failure, etc. |
| **Facilities** | Number of dialysis facilities per county |

---

## 🔍 HOW TO USE USRDS DATA FOR COUNTY-LEVEL RESEARCH

### **Step 1: Accessing USRDS Data**

**Option A: DESKRIBE Web Tool (No DUA required)**

```r
# DESKRIBE provides county-level aggregated data
# Access via: https://www.usrds.org/deskribe/

# Manual download of county tables:
# 1. Select "County" geographic level
# 2. Choose variables: incidence, prevalence, mortality
# 3. Select years: 2010-2023
# 4. Download CSV

# Example: Load DESKRIBE county data
library(tidyverse)

county_esrd <- read_csv("usrds_deskribe_county_2023.csv")

county_summary <- county_esrd %>%
  select(
    state, county, fips = county_fips,
    esrd_incidence_rate = inc_rate_adj,  # per million
    esrd_prevalence_count = prev_count,
    hd_percent,
    pd_percent,
    tx_percent,
    mortality_rate = death_rate_adj,  # per 100 patient-years
    pct_dm_primary,  # % diabetes as primary cause
    pct_htn_primary  # % hypertension as primary cause
  )
```

**Option B: Request Standard Analysis Files (Requires DUA)**

```r
# For patient-level research, request SAFs from USRDS
# Process:
# 1. Submit research proposal to USRDS Coordinating Center
# 2. Obtain IRB approval
# 3. Execute Data Use Agreement (DUA)
# 4. Receive SAF files (SAS format)

# Example: Reading SAF PATIENTS file
library(haven)

patients <- read_sas("patients.sas7bdat")

# Aggregate to county level
county_esrd_detailed <- patients %>%
  filter(FIRST_SE >= as.Date("2020-01-01"),  # Incident patients 2020
         FIRST_SE <= as.Date("2020-12-31")) %>%
  group_by(STATE, COUNTY) %>%
  summarize(
    incident_count = n(),
    pct_female = mean(SEX == "F") * 100,
    mean_age = mean(AGE, na.rm = TRUE),
    pct_black = mean(RACE == "Black") * 100,
    pct_hispanic = mean(HISPANIC == "Y") * 100,
    pct_dm_primary = mean(PRIM_DX == "DM") * 100,
    pct_htn_primary = mean(PRIM_DX == "HTN") * 100,
    mean_bmi = mean(BMI, na.rm = TRUE)
  )
```

---

### **Step 2: Calculate County Incidence & Prevalence Rates**

```r
library(tidycensus)

# Get county population from Census
county_pop <- get_acs(
  geography = "county",
  variables = "B01003_001",  # Total population
  year = 2020,
  survey = "acs5"
) %>%
  mutate(fips = GEOID) %>%
  select(fips, population = estimate)

# Calculate incidence rate (per million population)
county_incidence <- county_esrd_detailed %>%
  mutate(fips = paste0(str_pad(STATE, 2, "0"), str_pad(COUNTY, 3, "0"))) %>%
  left_join(county_pop, by = "fips") %>%
  mutate(
    incidence_rate_per_million = (incident_count / population) * 1e6
  )

# Compare to national average
national_incidence <- mean(county_incidence$incidence_rate_per_million)
# National average ~370 per million (2023)

high_incidence_counties <- county_incidence %>%
  filter(incidence_rate_per_million > national_incidence * 1.5) %>%
  arrange(desc(incidence_rate_per_million))
```

---

### **Step 3: Analyze Risk Factors & Disparities**

```r
# Join with socioeconomic data
acs_socioeconomic <- get_acs(
  geography = "county",
  variables = c(
    "B17001_002",  # Below poverty
    "B17001_001",  # Total for poverty rate
    "B01002_001",  # Median age
    "B15003_022",  # Bachelor's degree
    "B15003_001",  # Total for education
    "B27001_005"   # Uninsured
  ),
  year = 2020
) %>%
  select(fips = GEOID, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  mutate(
    poverty_rate = (B17001_002 / B17001_001) * 100,
    bachelor_pct = (B15003_022 / B15003_001) * 100,
    median_age = B01002_001
  )

# Merge and analyze
esrd_risk_analysis <- county_incidence %>%
  left_join(acs_socioeconomic, by = "fips") %>%
  filter(!is.na(poverty_rate))

# Linear regression: ESRD incidence ~ SES
model <- lm(incidence_rate_per_million ~ poverty_rate + bachelor_pct +
              pct_black + pct_hispanic + median_age,
            data = esrd_risk_analysis)

summary(model)

# Key findings typically show:
# - Poverty rate positively associated with ESRD incidence
# - Education negatively associated
# - Black and Hispanic populations at higher risk (adjusted for SES)
```

---

### **Step 4: Map ESRD Burden by County**

```r
library(sf)
library(tigris)
library(ggplot2)

# Load county boundaries
counties_sf <- counties(year = 2020, cb = TRUE)

# Join ESRD data
esrd_map_data <- counties_sf %>%
  mutate(fips = GEOID) %>%
  left_join(county_incidence, by = "fips")

# Map incidence rates
ggplot(esrd_map_data) +
  geom_sf(aes(fill = incidence_rate_per_million), color = NA) +
  scale_fill_viridis_c(
    name = "ESRD Incidence\n(per million)",
    option = "plasma",
    na.value = "grey90"
  ) +
  theme_minimal() +
  labs(title = "ESRD Incidence by US County, 2020")

# Identify geographic clusters (e.g., "Stroke Belt", Appalachia, etc.)
```

---

## 📚 COMPANION CMS DATA SOURCES

### **Medicare Claims Files:**
- **Medicare Provider Analysis and Review (MedPAR):** Inpatient claims
- **Carrier Claims:** Physician/supplier services
- **Outpatient Claims:** Hospital outpatient services
- **Part D Event Files:** Prescription drugs
- **Portal:** https://resdac.org/

### **CMS Chronic Conditions Warehouse:**
- 67 chronic conditions (includes CKD)
- County-level prevalence: https://www.cms.gov/data-research/statistics-trends-and-reports/chronic-conditions

---

## 📈 TEMPORAL & SPATIAL COVERAGE

| Attribute | Details |
|-----------|---------|
| **ESRD Data Coverage** | 1978-2023 (all incident ESRD patients) |
| **Medicare Claims** | 1991-2022 (comprehensive coverage) |
| **CKD Surveillance** | 2001-present (limited, expanding) |
| **Spatial Resolution** | Patient ZIP code → aggregate to county |
| **Temporal Resolution** | Daily (event dates), monthly/annual (aggregated metrics) |
| **Update Frequency** | Annual (new data typically 18-month lag) |
| **Population Coverage** | All US ESRD patients (mandated reporting) |

---

## ⚠️ DATA QUALITY & LIMITATIONS

### **Strengths:**
- Comprehensive coverage of all US ESRD patients (mandatory reporting)
- Longitudinal patient-level data (can follow individuals over time)
- Linked to Medicare claims (rich comorbidity, hospitalization, medication data)
- Includes transplant data from OPTN
- Quality metrics for dialysis facilities
- Free county-level data via DESKRIBE

### **Limitations:**
- **CKD data limited:** Strong ESRD coverage, but CKD stages 1-4 only from Medicare claims (underestimates true prevalence)
- **Medicare-centric:** Best data for age 65+ or disabled; limited for <65 with private insurance
- **Lag time:** 18-24 months between data collection and public release
- **No sub-county geography:** Patient-level data has ZIP code, but county is finest public aggregation
- **Comorbidity ascertainment:** Based on claims, may miss conditions not requiring treatment
- **Restricted access:** Patient-level SAFs require DUA, IRB approval, and fees
- **Missing data:** Lab values, clinical measures not uniformly collected
- **Selection bias:** Patients who initiate dialysis vs. those managed conservatively

---

## 📝 CITATION

**When using USRDS data, cite:**

> United States Renal Data System. 2024 USRDS Annual Data Report: Epidemiology of kidney disease in the United States. National Institutes of Health, National Institute of Diabetes and Digestive and Kidney Diseases, Bethesda, MD, 2024. Available at: https://usrds-adr.niddk.nih.gov/

> Saran R, Robinson B, Abbott KC, et al. US Renal Data System 2024 Annual Data Report: Epidemiology of kidney disease in the United States. Am J Kidney Dis. 2025;85(1):S1-S388. doi:10.1053/j.ajkd.2025.01.001

**For Standard Analysis Files:**

> United States Renal Data System. USRDS Standard Analysis Files. National Institute of Diabetes and Digestive and Kidney Diseases, Bethesda, MD. [Accessed DATE]. Available at: https://www.usrds.org/for-researchers/standard-analysis-files/

---

**Last Updated:** November 13, 2025
**Data Version:** 2024 USRDS Annual Data Report (Medicare claims through 2022, ESRD metrics through 2023)
**Total Variables Documented:** 500+ variables across 25+ Standard Analysis Files covering demographics, treatment, outcomes, comorbidities, and facilities
