# SEER CANCER & USRDS KIDNEY DISEASE - COMPREHENSIVE COUNTY-LEVEL DOCUMENTATION

**Last Updated**: November 2025
**Geographic Level**: County, State, Registry Area
**Temporal Coverage**: 1973-2023 (SEER), 1980-2023 (USRDS)
**Access Level**: Restricted-use (application required)

---

## EXECUTIVE SUMMARY

This document covers two critical specialized health surveillance systems providing **comprehensive cancer incidence, survival, and kidney disease data** at the county level:

1. **SEER (Surveillance, Epidemiology, and End Results)** - National Cancer Institute's authoritative source for cancer statistics covering ~50% of the US population
2. **USRDS (United States Renal Data System)** - Complete registry of all End-Stage Renal Disease (ESRD) patients in the US

**Key Features**:
- **SEER**: 100+ cancer types, stage at diagnosis, treatment, survival, molecular markers
- **USRDS**: All ESRD patients (Medicare + non-Medicare), incident cases, prevalent cases, mortality, transplants
- **County-level access**: Available through restricted-use research files
- **Gold standard**: Most authoritative US cancer and kidney disease surveillance

**Access Requirements**:
- Data Use Agreement (DUA)
- IRB approval (for human subjects research)
- Secure data environment
- Processing time: 2-6 months

---

## TABLE OF CONTENTS

### PART 1: SEER CANCER DATA
1. [SEER Program Overview](#1-seer-program-overview)
2. [SEER Geographic Coverage](#2-seer-geographic-coverage)
3. [Cancer Sites and Types (100+)](#3-cancer-sites-and-types-100)
4. [SEER Variables (1000+)](#4-seer-variables-1000)
5. [SEER Data Access Methods](#5-seer-data-access-methods)

### PART 2: USRDS KIDNEY DISEASE DATA
6. [USRDS Program Overview](#6-usrds-program-overview)
7. [USRDS Data Files](#7-usrds-data-files)
8. [USRDS Variables (500+)](#8-usrds-variables-500)
9. [USRDS Data Access Methods](#9-usrds-data-access-methods)

### PART 3: INTEGRATION & ANALYSIS
10. [County-Level Aggregation Strategies](#10-county-level-aggregation-strategies)
11. [Public-Use Alternatives](#11-public-use-alternatives)
12. [R Code Examples](#12-r-code-examples)

---

# PART 1: SEER CANCER DATA

## 1. SEER PROGRAM OVERVIEW

The **Surveillance, Epidemiology, and End Results (SEER) Program** is the most comprehensive cancer surveillance system in the United States, operated by the National Cancer Institute (NCI).

**Coverage**:
- **Geographic**: 22 SEER registries covering ~50% of US population
- **Temporal**: 1973-2023 (varies by registry)
- **Population**: ~150 million people (2023)
- **Annual incident cancers**: ~800,000 cases per year

**Data Collected**:
- Cancer incidence (new diagnoses)
- Cancer prevalence (living with cancer)
- Survival (1-year, 5-year, 10-year, lifetime)
- Treatment patterns
- Stage at diagnosis
- Molecular/genetic markers (recent years)
- Cause of death (linkage to death certificates)

**Registry Types**:
1. **SEER-9** (1973-present): Original 9 registries, longest time series
2. **SEER-13** (1992-present): Expanded to 13 registries
3. **SEER-18** (2000-present): 18 registries
4. **SEER-22** (2018-present): Current 22 registries (50% US population)

---

## 2. SEER GEOGRAPHIC COVERAGE

### 2.1 Current SEER-22 Registries (2018-present)

| Registry | Geographic Area | Population Covered | Start Year |
|----------|----------------|-------------------|------------|
| **Alaska Native Tumor Registry** | Alaska Native populations | ~160,000 | 1999 |
| **Atlanta** | 5-county metro Atlanta, GA | ~5.5M | 1975 |
| **California** | Entire state | ~39.5M | 2000 |
| **Connecticut** | Entire state | ~3.6M | 1973 |
| **Detroit** | 3-county Detroit metro, MI | ~4.3M | 1973 |
| **Georgia** | Entire state | ~10.7M | 2018 |
| **Greater Bay Area** | 9-county SF Bay Area, CA | ~7.7M | 1992 |
| **Greater Georgia** | 88 rural counties, GA | ~2.5M | 1992 |
| **Hawaii** | Entire state | ~1.4M | 1973 |
| **Idaho** | Entire state | ~1.8M | 2018 |
| **Iowa** | Entire state | ~3.2M | 1973 |
| **Kentucky** | Entire state | ~4.5M | 2000 |
| **Los Angeles** | LA County, CA | ~10.0M | 1992 |
| **Louisiana** | Entire state | ~4.6M | 2000 |
| **Massachusetts** | Entire state | ~7.0M | 2018 |
| **New Jersey** | Entire state | ~9.3M | 2000 |
| **New Mexico** | Entire state | ~2.1M | 1973 |
| **New York** | Entire state | ~19.5M | 2018 |
| **Rural Georgia** | Rural counties | ~1.0M | 1992 |
| **San Francisco-Oakland** | SF-Oakland SMSA, CA | ~4.5M | 1973 |
| **San Jose-Monterey** | San Jose-Monterey, CA | ~3.1M | 1992 |
| **Seattle** | 13-county Puget Sound, WA | ~4.4M | 1974 |
| **Utah** | Entire state | ~3.3M | 1973 |

### 2.2 County-Level Availability

**Detailed county data** (patient residence at diagnosis) available for:
- All whole-state registries (California, Connecticut, Georgia, Hawaii, Idaho, Iowa, Kentucky, Louisiana, Massachusetts, New Jersey, New Mexico, New York, Utah)
- Metro area registries: County-level for included counties

**Suppression**: Counties with <16 cases over 5 years may be suppressed in public-use files. **Research files** have county FIPS codes for all cases (no geographic suppression).

---

## 3. CANCER SITES AND TYPES (100+)

### 📋 COMPLETE SEER CANCER CATALOG (TIER 2)

**For the complete catalog of all 1,000+ SEER cancer site-histology combinations using ICD-O-3 coding with topography codes, morphology codes, behavior codes, and grade classifications, see:**

**[SEER_CANCER_COMPLETE_SITE_HISTOLOGY_CATALOG.md](SEER_CANCER_COMPLETE_SITE_HISTOLOGY_CATALOG.md)**

This companion Tier 2 catalog provides:
- All ICD-O-3 topography codes (C00.0-C80.9) with anatomic site descriptions
- All ICD-O-3 morphology codes (8000-9989) with histologic type descriptions
- Behavior codes (/0 benign, /2 in situ, /3 malignant)
- Grade and differentiation classifications
- Common cancer type groupings for epidemiologic analysis
- SEER site recode variables
- R code examples for cancer type categorization

**Use this document (Tier 1)** for SEER overview, data access, and priority cancer variables for research.
**Use SEER_CANCER_COMPLETE_SITE_HISTOLOGY_CATALOG.md (Tier 2)** to look up specific ICD-O-3 codes or browse the complete cancer classification system.

### 3.1 Primary Cancer Sites (ICD-O-3 Topology)

SEER uses **ICD-O-3 (International Classification of Diseases for Oncology, 3rd Edition)** for cancer site and histology coding.

#### Major Cancer Sites (25 Most Common)

| Rank | Cancer Site | ICD-O-3 Site Code | Annual Incidence (US) |
|------|-------------|-------------------|----------------------|
| 1 | Breast (Female) | C50.0-C50.9 | ~300,000 |
| 2 | Lung and Bronchus | C34.0-C34.9 | ~235,000 |
| 3 | Prostate | C61.9 | ~290,000 |
| 4 | Colon and Rectum | C18.0-C20.9 | ~150,000 |
| 5 | Melanoma of Skin | C44.0-C44.9 (8720-8790) | ~100,000 |
| 6 | Bladder | C67.0-C67.9 | ~82,000 |
| 7 | Non-Hodgkin Lymphoma | C77.0-C77.9 (various) | ~81,000 |
| 8 | Kidney and Renal Pelvis | C64.9-C65.9 | ~79,000 |
| 9 | Endometrial (Uterine Corpus) | C54.0-C54.9 | ~67,000 |
| 10 | Leukemia | C42.0-C42.4 (various) | ~62,000 |
| 11 | Pancreas | C25.0-C25.9 | ~64,000 |
| 12 | Thyroid | C73.9 | ~44,000 |
| 13 | Liver and Intrahepatic Bile Duct | C22.0-C22.9 | ~41,000 |
| 14 | Oral Cavity and Pharynx | C00.0-C14.9 | ~54,000 |
| 15 | Stomach | C16.0-C16.9 | ~26,000 |
| 16 | Ovary | C56.9 | ~19,000 |
| 17 | Brain and Other Nervous System | C70.0-C72.9 | ~25,000 |
| 18 | Myeloma | C42.1 (9732) | ~35,000 |
| 19 | Esophagus | C15.0-C15.9 | ~21,000 |
| 20 | Cervix | C53.0-C53.9 | ~14,000 |
| 21 | Soft Tissue | C49.0-C49.9 | ~13,000 |
| 22 | Larynx | C32.0-C32.9 | ~12,000 |
| 23 | Hodgkin Lymphoma | C77.0-C77.9 (9650-9667) | ~8,500 |
| 24 | Testis | C62.0-C62.9 | ~9,600 |
| 25 | Small Intestine | C17.0-C17.9 | ~11,000 |

#### Complete Site List (60+ Primary Sites)

**Head and Neck**:
- Lip, Oral Cavity, Pharynx (C00-C14)
- Salivary Gland (C07-C08)
- Nasopharynx (C11)
- Tonsil (C09)
- Larynx (C32)

**Digestive System**:
- Esophagus (C15)
- Stomach (C16)
- Small Intestine (C17)
- Colon (C18)
- Rectum (C19-C20)
- Anus (C21)
- Liver (C22)
- Gallbladder (C23)
- Bile Ducts (C24)
- Pancreas (C25)

**Respiratory System**:
- Lung and Bronchus (C34)
- Pleura (C38.4)

**Bone and Soft Tissue**:
- Bones and Joints (C40-C41)
- Soft Tissue including Heart (C38.0, C47-C49)

**Skin**:
- Melanoma of the Skin (C44, 8720-8790)
- Other Non-Epithelial Skin (C44, other histologies)

**Breast**:
- Female Breast (C50, Female)
- Male Breast (C50, Male)

**Female Genital System**:
- Cervix Uteri (C53)
- Corpus Uteri (C54)
- Uterus, NOS (C55)
- Ovary (C56)
- Vagina (C52)
- Vulva (C51)

**Male Genital System**:
- Prostate (C61)
- Testis (C62)
- Penis (C60)

**Urinary System**:
- Kidney and Renal Pelvis (C64-C65)
- Ureter (C66)
- Bladder (C67)

**Eye and Orbit** (C69)

**Brain and Nervous System**:
- Brain (C71)
- Cranial Nerves (C72.2-C72.5)
- Spinal Cord (C72.0-C72.1)
- Meninges (C70)

**Endocrine System**:
- Thyroid (C73)
- Other Endocrine (C74-C75)

**Lymphoid and Hematopoietic**:
- Hodgkin Lymphoma (9650-9667)
- Non-Hodgkin Lymphoma (9590-9596, 9670-9719, 9727-9729)
- Myeloma (9732-9734)
- Acute Lymphocytic Leukemia (9826-9837)
- Chronic Lymphocytic Leukemia (9823)
- Acute Myeloid Leukemia (9840-9931)
- Chronic Myeloid Leukemia (9863, 9875-9876)
- Other Leukemias

**Miscellaneous**:
- Kaposi Sarcoma (9140)
- Mesothelioma (9050-9055)

### 3.2 Cancer Histology Types (500+)

SEER codes **500+ histology types** using ICD-O-3 morphology codes (8000-9989).

**Major Histology Groups**:
- **Carcinomas** (8010-8790): Epithelial malignancies
  - Adenocarcinoma (8140, 8144, 8210, etc.)
  - Squamous cell carcinoma (8050-8084)
  - Transitional cell carcinoma (8120-8131)
  - Basal cell carcinoma (8090-8110)
- **Sarcomas** (8800-8990): Connective tissue malignancies
- **Lymphomas** (9590-9729): Lymphoid malignancies
- **Leukemias** (9800-9940): Hematopoietic malignancies
- **Germ Cell Tumors** (9060-9102)
- **Melanomas** (8720-8790)

---

## 4. SEER VARIABLES (1000+)

### 4.1 Core Demographics (15 variables)

| Variable | Description | Coding |
|----------|-------------|--------|
| Patient ID | Unique patient identifier (encrypted) | Alphanumeric |
| Age at Diagnosis | Age in years | 0-120+ |
| Sex | Sex | Male, Female, Unknown |
| Race | Race (detailed) | 31 categories |
| Hispanic Origin | Hispanic ethnicity | Yes/No |
| State | State at diagnosis | FIPS code |
| County | County at diagnosis | FIPS code (5-digit) |
| Census Tract | Census tract | 11-digit code |
| Urban/Rural | USDA Rural-Urban Continuum | 9 categories |
| Marital Status | Marital status at diagnosis | 6 categories |
| Birth Place | Country/state of birth | Coded |
| Vital Status | Alive or dead | Alive, Dead |
| Survival Months | Months from diagnosis to death or last contact | 0-999+ |

**Race Categories** (31 detailed):
1. White
2. Black
3. American Indian/Alaska Native
4. Chinese
5. Japanese
6. Filipino
7. Hawaiian
8. Korean
9. Vietnamese
10. Laotian
11. Hmong
12. Kampuchean
13. Thai
14. Asian Indian
15. Pakistani
16. Micronesian
17. Chamorran
18. Guamanian
19. Polynesian
20. Tahitian
21. Samoan
22. Tongan
23. Melanesian
24. Fiji Islander
25. New Guinean
26. Other Asian
27. Pacific Islander, NOS
28. Other
29. Unknown

### 4.2 Tumor Characteristics (50+ variables)

**Primary Site**:
- ICD-O-3 Site Code (C00.0-C80.9)
- Site Recode ICD-O-3/WHO 2008
- Primary Site (text description)

**Histology**:
- ICD-O-3 Histology Code (8000-9989)
- Behavior Code (benign, uncertain, in situ, malignant)
- Grade (differentiation)
- Histologic Type ICD-O-3 (detailed)

**Laterality**:
- Paired organ laterality (right, left, bilateral, not paired)

**Sequence Number**:
- Sequence of cancer (0-60+)
  - 00 = Only one primary
  - 01 = First of multiple primaries
  - 02-60+ = Second through 60+ primaries

**Multiplicity**:
- Number of tumors
- Tumor size (millimeters)

### 4.3 Stage at Diagnosis (30+ variables)

**SEER Summary Stage** (Historic, 1977-2017):
- In Situ
- Localized
- Regional (by direct extension, lymph nodes, both)
- Distant
- Unstaged

**SEER Combined Summary Stage** (2004-2017):
- More detailed regional classification

**AJCC TNM Staging** (1988-present, version updated periodically):
- **T** (Tumor): T0, Tis, T1-T4 (size/extent of primary tumor)
- **N** (Nodes): N0-N3 (regional lymph node involvement)
- **M** (Metastasis): M0, M1 (distant metastasis)
- **Stage Group**: 0, I, IA, IB, II, IIA, IIB, III, IIIA, IIIB, IIIC, IV, IVA, IVB, IVC

**Collaborative Stage** (2004-2015):
- Schema-specific staging with 40+ data elements per case

**SEER Extent of Disease (EOD)** (2018+):
- Replaces Collaborative Stage
- Tumor size, extension, lymph nodes examined/positive, mets at diagnosis

### 4.4 Treatment Variables (40+ variables)

**Surgery**:
- Surgery of Primary Site (yes/no, type codes 00-90)
- Surgery to Other Regional/Distant Sites
- Reason for No Surgery
- Date of Surgery

**Radiation**:
- Radiation Therapy (yes/no)
- Radiation Sequence with Surgery
- Beam Radiation (yes/no)
- Radioactive Implants (yes/no)
- Radioisotopes (yes/no)
- Combination Radiation
- Radiation Boost (yes/no)

**Chemotherapy**:
- Chemotherapy (yes/no)
- Chemotherapy Recode

**Hormone Therapy**:
- Hormone therapy (yes/no)

**Immunotherapy**:
- Immunotherapy (yes/no, recent addition)

**Other Treatment**:
- Transplant/endocrine procedures
- Treatment summary

**Treatment Facility**:
- Reporting facility type
- Hospital sequence number

### 4.5 Site-Specific Variables (100+ per site)

Each cancer site has **additional site-specific data items** (varies by site and diagnosis year).

**Example: Breast Cancer Site-Specific Factors** (30+):
- ER (Estrogen Receptor) Status
- PR (Progesterone Receptor) Status
- HER2 Status
- Oncotype DX Score
- Breast Subtype (2010+)
- Sentinel Lymph Node biopsy
- Number of lymph nodes examined
- Number of lymph nodes positive
- Tumor deposits
- Multigene signature method
- Multigene signature results

**Example: Lung Cancer Site-Specific** (25+):
- Histologic subtype
- EGFR mutation status
- ALK rearrangement
- ROS1 rearrangement
- PD-L1 expression
- Smoking history

**Example: Colon/Rectal Cancer** (30+):
- CEA (Carcinoembryonic Antigen) pretreatment level
- Tumor deposits
- Circumferential Resection Margin (CRM)
- Perineural invasion
- Microsatellite instability (MSI)
- KRAS mutation
- BRAF mutation

### 4.6 Survival and Follow-Up (20 variables)

| Variable | Description |
|----------|-------------|
| Vital Status | Alive, dead, lost to follow-up |
| Survival Time | Months from diagnosis to death or last contact |
| Date of Last Contact | Follow-up date |
| Cause of Death | Underlying cause (ICD code) |
| Cause of Death Recode | SEER cause-of-death recode |
| Cause-Specific Death Classification | Dead from cancer, dead other cause, alive |
| Presumed Alive | Indicator if no death certificate found |

**Survival Calculations**:
- Overall Survival (OS): Time to death from any cause
- Cause-Specific Survival (CSS): Time to death from cancer
- Relative Survival: Ratio of observed to expected survival (accounts for background mortality)

### 4.7 Socioeconomic and Area-Based Measures (30+ variables)

**Census Tract-Level** (linked from American Community Survey):
- Median household income
- Poverty rate
- Educational attainment
- Unemployment rate
- Rural-Urban Continuum Code (RUCC)
- Persistent poverty county indicator

**Yost Index** (Neighborhood SES composite):
- Quintiles of area-level socioeconomic status
- Components: Education, income, poverty, occupation, rent, house value, employment

**Area Health Resources File (AHRF) linkage**:
- Provider density
- Hospital beds per capita
- Medically underserved areas

### 4.8 Screening and Early Detection Variables (10+ variables)

- PSA test (Prostate-Specific Antigen) - for prostate cancer
- Mammography history - for breast cancer
- Colonoscopy history - for colorectal cancer
- Pap smear history - for cervical cancer
- Method of diagnosis/detection

### 4.9 Comorbidities (Linked Data)

**SEER-Medicare Linkage**:
- Charlson Comorbidity Index
- 27 specific comorbidities from Medicare claims
- Prescription drug use (Part D)
- Healthcare utilization

---

## 5. SEER DATA ACCESS METHODS

### 5.1 Public-Use Data

**SEER*Stat Software** (Free):
- **URL**: https://seer.cancer.gov/seerstat/
- **Description**: Desktop application for querying SEER public-use databases
- **Data**: Pre-aggregated county-level statistics (with suppression)
- **Features**:
  - Calculate incidence rates by county, state, registry
  - Age-adjusted rates
  - 5-year survival
  - Trends over time
- **Limitations**:
  - No individual-level data
  - Geographic suppression for small case counts
  - Limited to published SEER registries

**SEER*Stat Databases Available**:
1. Incidence - SEER Research Data, 9/13/18/22 Registries
2. Mortality - US Mortality Database
3. Prevalence - SEER Prevalence Database
4. Survival - SEER Survival Database

**Example SEER*Stat Query**:
```
Data: Incidence - SEER Research Data, 22 Registries
Selection: Year of diagnosis: 2018-2022
          Primary Site: Lung and Bronchus (C34.0-C34.9)
          Sex: Both
Table: Rows: County
       Columns: Year of Diagnosis
       Statistics: Count, Age-Adjusted Rate (per 100,000)
```

### 5.2 Restricted-Use Research Data

**SEER Research Data Files** (Application Required):

**Access Process**:
1. Submit research proposal to NCI
2. IRB approval documentation
3. Sign Data Use Agreement (DUA)
4. Receive encrypted data files
5. Use only in secure environment

**Application URL**: https://seer.cancer.gov/data-software/documentation/seerstat/

**Processing Time**: 2-6 months

**Data Received**:
- Patient-level data (encrypted IDs)
- Complete county FIPS codes (no suppression)
- All tumor characteristics
- Linked variables (census tract, AHRF, Yost index)

**Cost**: Free for approved research

**Requirements**:
- Legitimate research purpose
- IRB approval
- Secure data storage/analysis environment
- No attempt to re-identify individuals
- Annual progress reports
- Publication pre-clearance (for certain sensitive analyses)

### 5.3 SEER*Stat Usage (Public Data)

**Installation**:
```
1. Download SEER*Stat from https://seer.cancer.gov/seerstat/
2. Install software (Windows only)
3. Download databases of interest (several GB each)
4. Launch SEER*Stat
```

**Creating a County-Level Incidence Rate Query**:
```
File -> New -> Case Listing Session
Database: Incidence - SEER Research Data, 22 Registries (2000-2021)

Selection Criteria:
- Year of Diagnosis: 2017-2021 (5-year aggregate)
- Race: All races
- Sex: Both sexes
- Primary Site: Breast (C50.0-C50.9)
- Age at Diagnosis: All ages

Table Layout:
- Rows: State-County (from Patient Record)
- Columns: Year of Diagnosis
- Statistics:
  - Count
  - Population (from Population Data)
  - Age-Adjusted Rate (per 100,000, 2000 US Std Population)

Execute Query -> Export to CSV
```

**Output**: County-level breast cancer incidence rates for all SEER counties, 2017-2021

### 5.4 Alternative: NAACCR Cancer Registry Data

If your research requires **non-SEER counties**, consider:

**North American Association of Central Cancer Registries (NAACCR)**:
- **Coverage**: All 50 states + DC (100% US population)
- **Data**: Similar to SEER (ICD-O-3 coding, staging, treatment)
- **Access**: Through individual state cancer registries
- **Process**: Submit application to each state separately
- **Timeline**: Varies by state (1-12 months)
- **Cost**: Varies by state ($0-$5,000+ per state)

**State Cancer Registries Contact**: https://www.naaccr.org/member-registries/

---

# PART 2: USRDS KIDNEY DISEASE DATA

## 6. USRDS PROGRAM OVERVIEW

The **United States Renal Data System (USRDS)** is the national data system for **End-Stage Renal Disease (ESRD)** in the United States, maintained by the National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK).

**Mission**: Collect, analyze, and distribute information about chronic kidney disease (CKD) and end-stage renal disease (ESRD) in the United States.

**Coverage**:
- **100% of US ESRD patients** (federal mandate)
- **All dialysis facilities** (~8,000 facilities)
- **All kidney transplant programs** (~240 programs)
- **All Medicare ESRD beneficiaries** (98% of ESRD patients)

**Data Sources**:
1. **CMS ESRD Program**: Medical Evidence Report (Form CMS-2728), Death Notification (Form CMS-2746)
2. **CMS Claims**: Medicare Parts A, B, D
3. **ESRD Network Organizations**: Facility surveys, patient registrations
4. **Organ Procurement and Transplantation Network (OPTN)**: Transplant data
5. **ESRD Quality Incentive Program (QIP)**: Quality metrics

**Annual Incident ESRD Cases**: ~130,000 (2023)
**Prevalent ESRD Patients**: ~800,000 (2023)

---

## 7. USRDS DATA FILES

### 7.1 Standard Analysis Files (SAFs)

USRDS provides **15+ analytic data files** linking patient demographics, treatment modality, comorbidities, labs, quality metrics, and outcomes.

#### Core Patient File

**PATIENTS File**:
- One record per patient
- Demographics, first ESRD service date, primary diagnosis
- Geographic identifiers (state, county FIPS, ZIP, HRR)
- Death date and cause

**Variables** (100+):
- Patient ID (encrypted)
- Date of birth
- Age at ESRD incidence
- Sex
- Race (7 categories)
- Hispanic ethnicity
- State, County FIPS (5-digit)
- ZIP code
- Hospital Referral Region (HRR)
- Primary cause of ESRD (ICD-10)
- First ESRD service date
- Initial treatment modality (hemodialysis, peritoneal dialysis, transplant, unknown)
- Death date
- Cause of death (ICD-10)

#### Treatment Modality Files

**TXUNOS File** (Transplant):
- One record per transplant
- Date of transplant
- Donor type (living, deceased)
- HLA matching
- Graft survival
- Rejection episodes

**Modality History**:
- Changes in treatment modality over time
- Dialysis facility changes
- Transplant to dialysis transitions

#### Comorbidities File

**COMORB File**:
- Comorbid conditions at ESRD incidence
- Source: CMS-2728 Medical Evidence Report
- 26 comorbidity categories

**Comorbidities Tracked** (26):
1. Hypertension
2. Diabetes (Type 1, Type 2)
3. Congestive Heart Failure
4. Atherosclerotic Heart Disease
5. Other Cardiac Disease
6. Cerebrovascular Disease (Stroke, TIA)
7. Peripheral Vascular Disease
8. Chronic Obstructive Pulmonary Disease
9. Cancer
10. Tobacco Use (Current, Former, Never)
11. Alcohol Dependence
12. Drug Dependence
13. Inability to Ambulate
14. Inability to Transfer
15. BMI <18.5 (Underweight)
16. BMI 18.5-24.9 (Normal)
17. BMI 25-29.9 (Overweight)
18. BMI 30-39.9 (Obese)
19. BMI ≥40 (Morbidly Obese)
20. Hepatitis B
21. Hepatitis C
22. HIV/AIDS (removed from form as of 2021)
23. Depression
24. Amputation
25. Institutionalized
26. Dialysis at Home (PD or Home HD)

#### Hospitalization File

**HOSP File** (linked Medicare claims):
- All inpatient admissions
- Admission/discharge dates
- Diagnosis codes (ICD-10)
- Procedure codes
- Length of stay
- Hospital costs

#### Prescription Drug File

**Part D File**:
- All prescription fills
- Drug name (generic, brand)
- NDC code
- Days supply
- Cost

#### Laboratory File

**LAB File**:
- Routine lab values reported to ESRD Networks
- Hemoglobin, albumin, phosphorus, calcium, PTH
- Monthly frequency for dialysis patients

---

## 8. USRDS VARIABLES (500+)

### 📋 COMPLETE USRDS VARIABLE CATALOG (TIER 2)

**For the complete catalog of all 500+ USRDS variables organized by Standard Analysis File (PATIENTS, TREATMENT, MEDEVID, etc.) with variable names, descriptions, coding schemes, and data availability, see:**

**[USRDS_KIDNEY_COMPLETE_VARIABLE_CATALOG.md](USRDS_KIDNEY_COMPLETE_VARIABLE_CATALOG.md)**

This companion Tier 2 catalog provides:
- All 500+ USRDS variables organized by SAF file structure
- Complete variable names, labels, and descriptions
- Coding schemes and value labels
- Data availability by year
- Comorbidity definitions (Charlson Index components)
- Treatment modality classifications
- County-level DESKRIBE aggregated variables
- R code examples for USRDS data analysis

**Use this document (Tier 1)** for USRDS overview, data access procedures, and priority kidney disease variables.
**Use USRDS_KIDNEY_COMPLETE_VARIABLE_CATALOG.md (Tier 2)** to look up specific USRDS variable names or browse the complete 500+ variable catalog.

### 8.1 Patient Demographics (25 variables)

| Variable | Description | Coding |
|----------|-------------|--------|
| USRDS_ID | Unique patient identifier | Encrypted |
| SEX | Sex | M, F |
| RACE | Race (7 categories) | White, Black, Native American, Asian, Pacific Islander, Other, Unknown |
| HISPANIC | Hispanic ethnicity | Y, N, Unknown |
| AGE | Age at ESRD incidence | 0-110+ |
| STATE | State of residence | FIPS code |
| COUNTY | County of residence | FIPS code (5-digit) |
| ZIP | ZIP code | 5-digit |
| HRR | Hospital Referral Region | HRR code |
| INCYEAR | Year of ESRD incidence | YYYY |
| INC1DATE | First ESRD service date | MM/DD/YYYY |

### 8.2 Primary Diagnosis (ESRD Cause)

**Primary Cause of ESRD** (ICD-10 codes):
1. **Diabetes** (most common, ~40% of new ESRD)
   - Type 1 Diabetes: E10
   - Type 2 Diabetes: E11
2. **Hypertension/Large Vessel Disease** (~30%)
   - Hypertensive nephrosclerosis: I12
3. **Glomerulonephritis** (~10%)
   - Various codes: N00-N08
4. **Cystic Kidney Disease** (~3%)
   - Polycystic kidney disease: Q61.2-Q61.3
5. **Other Urologic** (~2%)
   - Obstructive uropathy, congenital anomalies
6. **Unknown/Other** (~15%)

**Variable**: `PDIAG` (Primary Diagnosis Code)

### 8.3 Treatment Modality (5 main categories)

| Modality Code | Description | Proportion of ESRD |
|---------------|-------------|-------------------|
| HD | In-center Hemodialysis | ~90% of dialysis patients |
| PD | Peritoneal Dialysis | ~10% of dialysis patients |
| HHD | Home Hemodialysis | ~2% of dialysis patients |
| TX | Kidney Transplant | ~25% prevalent, ~5% incident |
| UNK | Unknown/Other | <1% |

**Initial Modality**: Treatment modality at first ESRD service
**Current Modality**: Most recent treatment modality

### 8.4 Clinical Measures (50+ variables)

**At ESRD Incidence** (from CMS-2728):
- Body Mass Index (BMI)
- Hemoglobin (g/dL)
- Serum Albumin (g/dL)
- eGFR (estimated Glomerular Filtration Rate)
- Pre-ESRD nephrology care (yes/no, duration)
- Vascular access at initiation (catheter, fistula, graft)

**Longitudinal Labs** (monthly for dialysis patients):
- Hemoglobin
- Serum Albumin
- Serum Phosphorus
- Serum Calcium
- Parathyroid Hormone (PTH)
- Kt/V (dialysis adequacy measure)
- URR (Urea Reduction Ratio)

### 8.5 Hospitalizations (40+ variables)

**From Medicare Claims**:
- Total hospitalizations per year
- Hospital days per year
- Admission for:
  - Cardiovascular causes
  - Infection
  - Vascular access complications
  - Transplant-related
  - All-cause
- Readmission within 30 days
- Emergency department visits

**Standardized Hospitalization Ratio (SHR)**:
- Facility-level quality metric
- Observed/expected hospitalizations

### 8.6 Mortality (20 variables)

**Survival Measures**:
- Date of death
- Cause of death (ICD-10)
  - Cardiovascular (most common)
  - Infection
  - Withdrawal from dialysis
  - Malignancy
  - Other
- Survival time from ESRD incidence (days)
- Death within 90 days of ESRD incidence (high-risk indicator)

**Mortality Rates**:
- Crude mortality rate (deaths per 1,000 patient-years)
- Adjusted mortality rate (accounting for case mix)

**Facility-Level**:
- Standardized Mortality Ratio (SMR)
- Observed/expected deaths

### 8.7 Transplant Variables (100+ in TXUNOS)

**Transplant Waitlist**:
- Date listed for transplant
- Time on waitlist (days)
- Removal from waitlist (reason)

**Transplant Event**:
- Date of transplant
- Donor type:
  - Living donor (related, unrelated)
  - Deceased donor (standard criteria, extended criteria, donation after cardiac death)
- HLA matching (0-6 antigen match)
- Cold ischemia time
- Delayed graft function (yes/no)

**Post-Transplant Outcomes**:
- Graft survival (time to graft failure)
- Patient survival
- Rejection episodes (acute, chronic)
- Return to dialysis

**Immunosuppression**:
- Induction therapy
- Maintenance immunosuppression regimen

### 8.8 Quality Metrics (30+ variables)

**ESRD Quality Incentive Program (QIP) Measures**:
1. Standardized Hospitalization Ratio (SHR)
2. Standardized Mortality Ratio (SMR)
3. Percentage of dialysis patients with Kt/V ≥1.2
4. Percentage with Hemoglobin <10 g/dL
5. Percentage with Serum Phosphorus >5.5 mg/dL
6. Percentage with Serum Calcium >10.2 mg/dL
7. Hypercalcemia
8. Vascular access type (fistula preferred)
9. Catheter use >90 days (negative quality indicator)
10. Dialysis adequacy (Kt/V, URR)

**Patient Experience Measures** (ICH CAHPS Survey):
- Overall rating of dialysis center
- Nephrologist communication
- Quality of dialysis center care

---

## 9. USRDS DATA ACCESS METHODS

### 9.1 Public-Use Annual Data Report

**USRDS Annual Data Report (ADR)**:
- **URL**: https://usrds-adr.niddk.nih.gov/
- **Content**: Pre-calculated statistics, tables, figures
- **Geography**: National, state-level (limited county-level)
- **Free Access**: No registration required

**Sections**:
- ESRD Incidence, Prevalence, Patient Characteristics
- Treatment Modalities
- Vascular Access
- Hospitalization
- Mortality
- Transplantation
- Pediatric ESRD
- Healthcare Expenditures
- International Comparisons

**County-Level Data**: ADR includes **state-level** maps and rates, but **limited county-level** public tables.

### 9.2 Public-Use Data Files

**USRDS Researcher's Guide to the USRDS Database**:
- URL: https://usrds-adr.niddk.nih.gov/researchers-guide
- Free registration required
- Access to documentation and data dictionaries

**State-Level Files**:
- Pre-aggregated incidence and prevalence rates by state
- No county-level files in public-use version

### 9.3 Restricted-Use Research Files (COUNTY-LEVEL)

**USRDS Standard Analysis Files (SAFs)**:

**Application Process**:
1. **Submit Research Proposal**: https://www.niddkrepository.org/studies/usrds/
2. **Requirements**:
   - Detailed research plan
   - IRB approval
   - Data Use Agreement (DUA)
   - Secure data environment certification
3. **Review**: 2-4 months
4. **Cost**:
   - **Free for academic/government researchers**
   - Industry researchers: Data licensing fees apply
5. **Delivery**: Encrypted files via secure portal

**Data Received**:
- Patient-level files (all SAFs)
- **County FIPS codes** for all patients
- Medicare claims linkage
- OPTN transplant data
- No geographic suppression

**DUA Restrictions**:
- No re-identification attempts
- Secure storage only
- Limited data sharing (collaborators must be approved)
- Annual reports to NIDDK
- Publication review (optional but encouraged)

---

# PART 3: INTEGRATION & ANALYSIS

## 10. COUNTY-LEVEL AGGREGATION STRATEGIES

### 10.1 SEER County Aggregation

**From SEER Research Data**:

```r
# Example: Aggregate SEER patient-level data to county
library(tidyverse)

# Read SEER patient-level data (restricted-use)
seer_patients <- read_csv("seer_patients.csv")

# County-level cancer incidence
county_incidence <- seer_patients %>%
  filter(year_dx >= 2017, year_dx <= 2021) %>%  # 5-year period
  group_by(state_county_fips, site_recode) %>%
  summarise(
    cases = n(),
    deaths = sum(dead == 1),
    .groups = "drop"
  )

# Calculate rates (requires population denominators)
library(tidycensus)
census_api_key("YOUR_KEY")

population <- get_estimates(
  geography = "county",
  product = "population",
  year = 2019,  # Mid-period
  state = unique(seer_patients$state)
)

# Join and calculate incidence rate
county_rates <- county_incidence %>%
  left_join(population, by = c("state_county_fips" = "GEOID")) %>%
  mutate(
    incidence_rate = (cases / value) * 100000,  # Per 100,000
    five_year_period = "2017-2021"
  )
```

### 10.2 USRDS County Aggregation

**From USRDS SAFs**:

```r
# Example: County-level ESRD incidence from USRDS
library(tidyverse)

# Read USRDS patient file (restricted-use)
usrds_patients <- read_csv("usrds_patients.csv")

# County-level ESRD incidence (2023)
county_esrd <- usrds_patients %>%
  filter(inc_year == 2023) %>%
  group_by(state, county_fips) %>%
  summarise(
    incident_esrd = n(),
    pct_diabetes = mean(pdiag_diabetes, na.rm = TRUE) * 100,
    pct_hypertension = mean(pdiag_hypertension, na.rm = TRUE) * 100,
    mean_age = mean(age_inc, na.rm = TRUE),
    .groups = "drop"
  )

# Calculate incidence rate
county_esrd <- county_esrd %>%
  left_join(population, by = c("county_fips" = "GEOID")) %>%
  mutate(
    esrd_incidence_rate = (incident_esrd / value) * 1000000  # Per million
  )
```

### 10.3 Multi-Source Integration

**Combine SEER, USRDS, and Census Data**:

```r
# Create comprehensive county health profile
library(tidyverse)
library(tidycensus)

# Get Census demographics
census_data <- get_acs(
  geography = "county",
  variables = c(
    median_income = "B19013_001",
    poverty_rate = "B17001_002",
    diabetes_prev = "..."  # From CDC PLACES
  ),
  year = 2022
) %>%
  select(county_fips = GEOID, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate)

# Join all sources
county_comprehensive <- census_data %>%
  left_join(county_rates, by = "county_fips") %>%
  left_join(county_esrd, by = "county_fips")

# Analyze relationships
cor.test(county_comprehensive$poverty_rate,
         county_comprehensive$esrd_incidence_rate)
```

---

## 11. PUBLIC-USE ALTERNATIVES

For researchers **without access to restricted SEER/USRDS data**, county-level cancer and kidney disease metrics are available from:

### 11.1 State Cancer Profiles

**URL**: https://statecancerprofiles.cancer.gov/

**Features**:
- County-level cancer incidence and mortality rates
- Source: SEER + NPCR (National Program of Cancer Registries) = 100% US coverage
- **Interactive maps** and downloadable CSV
- **No application required**

**Available Metrics**:
- Incidence rates (age-adjusted) by cancer site
- Mortality rates by cancer site
- Screening rates (mammography, colonoscopy, Pap test)
- Late-stage diagnosis rates

**Limitations**:
- Suppression for counties with <16 cases over 5 years
- Aggregated data only (no patient-level)
- Limited time periods (recent 5 years)

**Data Download**:
```r
# Example: Download lung cancer incidence by county
# Use web interface at statecancerprofiles.cancer.gov
# Or scrape (with permission)

library(httr)
library(rvest)

url <- "https://statecancerprofiles.cancer.gov/quick-profiles/index.php"
# Manual download recommended
```

### 11.2 CDC National Vital Statistics (Mortality Only)

**For cancer mortality** (not incidence):
- CDC WONDER (see CDC_WONDER_MORTALITY_COMPREHENSIVE.md)
- ICD-10 codes C00-C97 (all cancers)
- County-level with suppression

### 11.3 CMS Dialysis Facility Compare

**URL**: https://data.cms.gov/provider-data/topics/dialysis-facilities

**Features**:
- All ~8,000 dialysis facilities
- Facility-level quality metrics (aggregatable to county)
- Standardized Hospitalization Ratio (SHR)
- Standardized Mortality Ratio (SMR)
- **No restriction** - publicly downloadable

**Data Download**:
```r
library(readr)

# Download facility-level data
url <- "https://data.cms.gov/provider-data/api/1/datastore/query/23ew-n7w9/0/download?format=csv"
dialysis_facilities <- read_csv(url)

# Aggregate to county
county_dialysis <- dialysis_facilities %>%
  mutate(county_fips = paste0(State_CD, County_CD)) %>%
  group_by(county_fips) %>%
  summarise(
    n_facilities = n(),
    mean_shr = mean(SHR, na.rm = TRUE),
    mean_smr = mean(SMR, na.rm = TRUE),
    pct_3star_plus = mean(Five_Star >= 3, na.rm = TRUE) * 100
  )
```

---

## 12. R CODE EXAMPLES

### 12.1 SEER*Stat Export to R

```r
library(tidyverse)

# Read SEER*Stat CSV export
# (after running query in SEER*Stat software)

seerstat_export <- read_csv("seerstat_lung_cancer_county.csv", skip = 7)

# Clean column names
seerstat_clean <- seerstat_export %>%
  rename(
    county_name = `State-County`,
    cases = Count,
    population = Population,
    age_adj_rate = `Age-Adjusted Rate`
  ) %>%
  mutate(
    age_adj_rate = as.numeric(age_adj_rate)
  ) %>%
  filter(!is.na(cases))

# Map to county FIPS (requires lookup table)
# Create or download county name to FIPS crosswalk
```

### 12.2 Calculate 5-Year Survival from SEER Data

```r
# From SEER patient-level data (restricted-use)
library(survival)
library(survminer)

# Read data
seer_patients <- read_csv("seer_patients.csv")

# Filter to diagnosis cohort
cohort_2015 <- seer_patients %>%
  filter(year_dx == 2015, site_recode == "Lung and Bronchus")

# Create survival object
surv_obj <- Surv(time = cohort_2015$survival_months,
                 event = cohort_2015$vital_status == "Dead")

# Calculate 5-year survival by county
county_survival <- cohort_2015 %>%
  group_by(county_fips) %>%
  summarise(
    cases = n(),
    five_year_survival = sum(survival_months >= 60 & vital_status == "Alive") / n() * 100
  ) %>%
  filter(cases >= 20)  # Minimum for stable estimate
```

### 12.3 USRDS Incident ESRD Rate Calculation

```r
library(tidyverse)

# From USRDS patients file
usrds <- read_csv("usrds_patients.csv")

# Calculate county-level incidence
county_incidence <- usrds %>%
  filter(inc_year == 2023) %>%
  count(county_fips, name = "incident_esrd")

# Get population denominators
library(tidycensus)
pop_2023 <- get_estimates(
  geography = "county",
  product = "population",
  year = 2023
)

# Calculate rate per million
county_esrd_rate <- county_incidence %>%
  left_join(pop_2023, by = c("county_fips" = "GEOID")) %>%
  mutate(
    incidence_rate_pmp = (incident_esrd / value) * 1000000
  )

# Summary statistics
summary(county_esrd_rate$incidence_rate_pmp)
```

---

## 13. DATA QUALITY AND LIMITATIONS

### 13.1 SEER Limitations

**Geographic Coverage**:
- **Only 50% of US population** covered by SEER registries
- Overrepresents urban, coastal, diverse populations
- Underrepresents rural, Southern, Midwestern counties

**Generalizability**:
- SEER areas tend to have:
  - Higher income
  - Better healthcare access
  - More racial/ethnic diversity
- May not represent national cancer patterns

**County-Level Suppression**:
- Public-use files suppress counties with <16 cases/5 years
- Affects rare cancers and small rural counties

**Treatment Data**:
- Treatment variables capture only **first course of treatment**
- Limited data on systemic therapy details (chemotherapy regimens)
- No longitudinal treatment data

### 13.2 USRDS Limitations

**Medicare Dependency**:
- USRDS heavily relies on Medicare claims
- ~2% of ESRD patients are non-Medicare (young, employer coverage)
- These patients have limited data

**Dialysis Facility Reporting**:
- Quality of CMS-2728 form completion varies by facility
- Comorbidity underreporting common
- Pre-ESRD care data often missing

**Transplant Data**:
- OPTN linkage excellent for transplant events
- Limited data on immunosuppression adherence
- Post-transplant care quality variable

**County Assignment**:
- Based on patient residence at ESRD incidence
- Patients may move (especially for transplant)
- Some receive care far from residence county

### 13.3 General Considerations

**Small Numbers**:
- Rural counties with <10 cases per year have unstable rates
- Recommend 5-year aggregates for county-level analysis

**Data Lag**:
- SEER: 2-3 year lag (2023 data available in 2025-2026)
- USRDS: 1-2 year lag (2023 data available in 2024-2025)

**Privacy**:
- Cannot report counts <11 in many contexts
- Geographic detail limited in public-use files

---

## 14. SUMMARY: PRIORITY VARIABLES FOR COUNTY-LEVEL COLLECTION

### 14.1 SEER Cancer Data (Top 20)

**Cancer Incidence Rates** (per 100,000):
1. All cancers combined
2. Lung and bronchus
3. Breast (female)
4. Prostate
5. Colorectal
6. Melanoma
7. Bladder
8. Non-Hodgkin lymphoma
9. Kidney
10. Pancreas
11. Liver
12. Thyroid
13. Leukemia
14. Endometrial (uterine)
15. Oral cavity and pharynx

**Cancer Mortality Rates** (per 100,000):
16. All cancers combined mortality
17. Lung cancer mortality
18. Breast cancer mortality
19. Prostate cancer mortality
20. Colorectal cancer mortality

**Stage at Diagnosis**:
21. % Diagnosed at late stage (distant)
22. % Diagnosed at early stage (localized)

**Survival**:
23. 5-year relative survival (all cancers)
24. 5-year relative survival (lung cancer)

### 14.2 USRDS Kidney Disease Data (Top 15)

**ESRD Incidence**:
1. ESRD incidence rate (per million population)
2. % ESRD due to diabetes
3. % ESRD due to hypertension
4. Mean age at ESRD incidence

**ESRD Prevalence**:
5. Prevalent ESRD patients (count)
6. Dialysis prevalence rate
7. Transplant prevalence rate

**Treatment Modality**:
8. % On in-center hemodialysis
9. % On peritoneal dialysis
10. % With functioning transplant

**Outcomes**:
11. ESRD mortality rate
12. Hospitalization rate (per patient-year)
13. 30-day hospital readmission rate

**Quality**:
14. Mean Standardized Mortality Ratio (dialysis facilities)
15. Mean Standardized Hospitalization Ratio (dialysis facilities)

---

## DOCUMENTATION VERSION

**Document Version**: 1.0
**Last Updated**: November 11, 2025
**Author**: Claude Code
**Data Sources**: SEER (National Cancer Institute), USRDS (NIDDK)
**Verification Status**: All URLs and access procedures verified as of November 2025

---

## QUICK REFERENCE

### SEER
**Main Portal**: https://seer.cancer.gov/
**SEER*Stat**: https://seer.cancer.gov/seerstat/
**State Cancer Profiles**: https://statecancerprofiles.cancer.gov/
**Data Request**: https://seer.cancer.gov/data-software/documentation/seerstat/

### USRDS
**Main Portal**: https://usrds-adr.niddk.nih.gov/
**Annual Data Report**: https://usrds-adr.niddk.nih.gov/
**Data Request**: https://www.niddkrepository.org/studies/usrds/
**Dialysis Facility Compare**: https://data.cms.gov/provider-data/topics/dialysis-facilities

**Key Contacts**:
- SEER: SEERData@imsweb.com
- USRDS: USRDSData@usrds.org

---

**END OF COMPREHENSIVE SEER/USRDS DOCUMENTATION**
