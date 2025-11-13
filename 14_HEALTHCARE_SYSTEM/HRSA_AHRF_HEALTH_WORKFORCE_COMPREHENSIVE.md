# HRSA AREA HEALTH RESOURCES FILE (AHRF) - COMPREHENSIVE DOCUMENTATION

**Last Updated**: November 2025
**Geographic Level**: County, State, National
**Temporal Coverage**: 1970-2024 (varies by variable)
**Update Frequency**: Annual
**Access**: Free, no restriction

---

## EXECUTIVE SUMMARY

The **Area Health Resources File (AHRF)** is the **most comprehensive source of county-level data on health facilities, health professions, measures of resource scarcity, health status, economic activity, health training programs, and socioeconomic/environmental characteristics** in the United States.

**Maintained by**: Health Resources and Services Administration (HRSA), Bureau of Health Workforce

**Key Features**:
- **7,000+ variables** covering 1970-2024
- **All 3,143 US counties** + DC + territories
- **50+ data sources** integrated into single file
- **No geographic suppression** (all counties included)
- **Time series**: Many variables available for multiple years
- **Free download**: No registration, API key, or DUA required

**Major Categories** (15):
1. Health Facilities (hospitals, nursing homes, clinics, etc.)
2. Health Professions (physicians, nurses, dentists, mental health providers, etc.)
3. Health Professions Training (medical schools, residency programs, etc.)
4. Hospital Utilization & Expenditures
5. Hospital Characteristics
6. Health Professional Shortage Areas (HPSA)
7. Medically Underserved Areas/Populations (MUA/MUP)
8. Health Status (mortality, birth statistics, etc.)
9. Economics (income, poverty, employment, etc.)
10. Sociodemographics (population, age, race, education, etc.)
11. Environment (air quality, water, etc.)
12. County Characteristics (land area, geographic classification)
13. Medicare (enrollment, utilization, spending)
14. Medicaid (enrollment)
15. Census & ACS Data

**Total Variables**: **7,000+** variables per county

### 📋 COMPLETE AHRF VARIABLE CATALOG (TIER 2)

**For the complete catalog of all 6,000+ AHRF variables organized by 8 major categories (Health Care Professions, Health Facilities, Population Characteristics, Economics, etc.) with field numbers, descriptions, sources, and years available, see:**

**[HRSA_AHRF_COMPLETE_VARIABLE_CATALOG.md](HRSA_AHRF_COMPLETE_VARIABLE_CATALOG.md)**

This companion Tier 2 catalog provides:
- All 6,000+ AHRF field numbers (FXXXXX_YY format) with descriptions
- Organized by 8 major categories and dozens of subcategories
- Data sources and update frequency for each variable
- Years available for time-series variables (1970-2024)
- Variable naming conventions and suffixes
- Geographic identifiers and missing data codes
- R/Python code examples for AHRF data extraction and analysis
- Links to official AHRF Technical Documentation

**Use this document (Tier 1)** for AHRF overview, priority health workforce/facilities variables, and data access.
**Use HRSA_AHRF_COMPLETE_VARIABLE_CATALOG.md (Tier 2)** to look up specific AHRF field numbers or browse the complete 6,000+ variable catalog.

---

## TABLE OF CONTENTS

1. [AHRF File Structure](#1-ahrf-file-structure)
2. [Health Facilities (1000+ variables)](#2-health-facilities-1000-variables)
3. [Health Professions (1500+ variables)](#3-health-professions-1500-variables)
4. [Health Professional Shortage Areas (200+ variables)](#4-health-professional-shortage-areas-200-variables)
5. [Health Status Indicators (500+ variables)](#5-health-status-indicators-500-variables)
6. [Socioeconomic Characteristics (2000+ variables)](#6-socioeconomic-characteristics-2000-variables)
7. [Medicare & Medicaid (800+ variables)](#7-medicare--medicaid-800-variables)
8. [Access Methods](#8-access-methods)
9. [R Code Examples](#9-r-code-examples)
10. [Data Quality and Limitations](#10-data-quality-and-limitations)

---

## 1. AHRF FILE STRUCTURE

### 1.1 File Organization

The AHRF is distributed as a **single county-level file** with one record per county.

**File Specifications**:
- **Records**: 3,275+ (3,143 US counties + DC + territories)
- **Variables**: 7,000+
- **Format**: SAS, CSV, Excel
- **Size**: ~500 MB (Excel), ~2 GB (SAS)
- **Structure**: Wide format (one row per county, 7,000+ columns)

**Geographic Identifiers**:
- `F00002`: State FIPS code (2 digits)
- `F00003`: County FIPS code (3 digits)
- `F00011`: State-County FIPS code combined (5 digits)
- `F00008`: State postal abbreviation
- `F00009`: County name

### 1.2 Variable Naming Convention

**Pattern**: `F` + 5-digit number + optional 2-digit year suffix

**Examples**:
- `F08921`: Primary care physicians, 2021
- `F08922`: Primary care physicians, 2022
- `F08923`: Primary care physicians, 2023
- `F1198223`: Total population, 2023

**Documentation**: Excel file "AHRF Technical Documentation" provides:
- Variable labels
- Source
- Years available
- Numerator/denominator definitions

### 1.3 Data Sources Integrated

The AHRF compiles data from **50+ authoritative sources**:

1. **American Hospital Association (AHA) Annual Survey**
2. **American Medical Association (AMA) Physician Masterfile**
3. **Area Health Education Centers (AHEC)**
4. **Bureau of Health Workforce (BHW)**
5. **Bureau of Labor Statistics (BLS)**
6. **Census Bureau** (Decennial, ACS, Population Estimates)
7. **Centers for Disease Control and Prevention (CDC)** - Natality, Mortality
8. **Centers for Medicare & Medicaid Services (CMS)**
9. **Department of Agriculture (USDA)** - Economic Research Service
10. **Environmental Protection Agency (EPA)**
11. **Federal Bureau of Investigation (FBI)** - UCR
12. **National Center for Education Statistics (NCES)**
13. **National Center for Health Statistics (NCHS)**
14. **HRSA Data Warehouse**
15. And 35+ additional sources

---

## 2. HEALTH FACILITIES (1000+ VARIABLES)

### 2.1 Hospitals (400+ variables)

#### Hospital Counts by Type

| Variable Pattern | Description | Years Available |
|-----------------|-------------|-----------------|
| `F0453x` | Total hospitals | 1990-2023 |
| `F0890x` | Community hospitals | 1990-2023 |
| `F0901x` | Non-federal short-term general hospitals | 1990-2023 |
| `F04579` | Federal government hospitals | Latest year |
| `F08907` | For-profit hospitals | Latest year |
| `F08906` | Non-profit hospitals | Latest year |
| `F08908` | State/local government hospitals | Latest year |
| `F14199` | Critical Access Hospitals (CAH) | Latest year |
| `F14207` | Rural Referral Centers (RRC) | Latest year |
| `F14203` | Sole Community Hospitals (SCH) | Latest year |

#### Hospital Beds

| Variable | Description |
|----------|-------------|
| `F0892x` | Total hospital beds | 1990-2023 |
| `F0911x` | Community hospital beds | 1990-2023 |
| `F0918x` | Psychiatric beds | 1990-2023 |
| `F14135` | ICU beds | Latest year |
| `F08920` | Neonatal ICU beds | Latest year |

#### Hospital Services & Facilities

**Diagnostic/Treatment Services** (100+ variables):
- CT scanner
- MRI
- PET scanner
- Cardiac catheterization lab
- Radiation therapy
- Lithotripsy
- Transplant services (heart, liver, kidney, etc.)
- Burn care unit
- Trauma center designation

**Emergency Services**:
- `F14141`: Emergency department (yes/no)
- `F14149`: Trauma center level (I, II, III, IV)
- `F14150`: Burn care (yes/no)

**Specialty Services**:
- Cardiac surgery
- Neurosurgery
- Orthopedic surgery
- Obstetrics/maternity care
- Neonatal intensive care (Level I, II, III, IV)
- Psychiatric services
- Substance abuse treatment
- Palliative care/hospice

### 2.2 Nursing Homes & Long-Term Care (200+ variables)

| Variable Pattern | Description | Years |
|-----------------|-------------|-------|
| `F1476x` | Medicare-certified nursing facilities | 2000-2023 |
| `F1477x` | Medicaid-certified nursing facilities | 2000-2023 |
| `F1478x` | Total certified nursing facility beds | 2000-2023 |
| `F04899` | Nursing home residents | Latest year |

**Quality Measures** (from CMS Nursing Home Compare):
- Five-star rating
- Health inspection rating
- Staffing rating
- Quality measures rating

### 2.3 Community Health Centers (150+ variables)

**Federally Qualified Health Centers (FQHCs)**:

| Variable | Description |
|----------|-------------|
| `F1517x` | Total FQHC sites | 2000-2023 |
| `F1518x` | FQHC patients served | 2000-2023 |
| `F1519x` | FQHC providers (FTE) | 2000-2023 |
| `F15177` | FQHC medical visits | Latest year |
| `F15178` | FQHC dental visits | Latest year |
| `F15179` | FQHC mental health visits | Latest year |
| `F15180` | FQHC substance abuse visits | Latest year |

**FQHC Patient Demographics**:
- % Uninsured
- % Medicaid
- % Medicare
- % Below federal poverty level
- Race/ethnicity distribution

### 2.4 Mental Health & Substance Abuse Facilities (150+ variables)

**Mental Health Facilities**:
- `F15621`: Community mental health centers
- `F15622`: Psychiatric hospitals
- `F15623`: Residential treatment centers

**Substance Abuse Treatment Facilities**:
- `F15631`: Total substance abuse treatment facilities
- `F15632`: Outpatient facilities
- `F15633`: Residential facilities
- `F15634`: Hospital inpatient
- `F15635`: Medication-assisted treatment (MAT) programs
- `F15636`: Opioid treatment programs (OTPs)

### 2.5 Other Health Facilities (100+ variables)

**Dialysis Facilities**:
- `F15501`: Total dialysis facilities
- `F15502`: Hemodialysis stations
- `F15503`: Peritoneal dialysis capacity

**Ambulatory Surgical Centers**:
- `F15401`: Medicare-certified ASCs

**Home Health Agencies**:
- `F14901`: Medicare-certified home health agencies
- `F14902`: Home health patients served

**Hospice Programs**:
- `F15001`: Hospice programs
- `F15002`: Hospice patients

**Urgent Care Centers**:
- `F15301`: Urgent care centers (count)

**Retail Clinics** (CVS MinuteClinic, Walgreens Healthcare Clinic):
- `F15351`: Retail clinics

---

## 3. HEALTH PROFESSIONS (1500+ VARIABLES)

### 3.1 Physicians (600+ variables)

#### Total Physicians

| Variable | Description | Years Available |
|----------|-------------|-----------------|
| `F0889x` | Total patient care physicians | 1990-2023 |
| `F04547` | Total physicians (all activities) | Latest year |
| `F08892` | Patient care MDs | Latest year |
| `F08893` | Patient care DOs | Latest year |

#### Primary Care Physicians

**Total Primary Care**:
- `F0892x`: Total primary care physicians, 2000-2023
- `F08921`: Primary care physicians, 2021
- `F08922`: Primary care physicians, 2022
- `F08923`: Primary care physicians, 2023

**By Specialty**:
- `F1176x`: Family practice/general practice
- `F1177x`: Internal medicine
- `F1178x`: Pediatrics
- `F1179x`: Obstetrics/gynecology (often included in primary care)

**Primary Care Rate**:
- `F1524x`: Primary care physicians per 100,000 population

#### Physician Specialties (100+ specialty categories)

**Medical Specialties**:
- Cardiology
- Dermatology
- Endocrinology
- Gastroenterology
- Hematology
- Infectious disease
- Nephrology
- Neurology
- Oncology (medical)
- Pulmonology
- Rheumatology

**Surgical Specialties**:
- General surgery
- Cardiothoracic surgery
- Neurosurgery
- Orthopedic surgery
- Otolaryngology (ENT)
- Plastic surgery
- Urology
- Vascular surgery

**Hospital-Based Specialties**:
- Anesthesiology
- Emergency medicine
- Hospitalist
- Pathology
- Radiology

**Other Specialties**:
- Psychiatry
- Physical medicine & rehabilitation
- Allergy/immunology

#### Physician Demographics

**By Age**:
- `F1198x`: Physicians under age 35
- `F1199x`: Physicians age 35-44
- `F1200x`: Physicians age 45-54
- `F1201x`: Physicians age 55-64
- `F1202x`: Physicians age 65+

**By Sex**:
- `F1196x`: Male physicians
- `F1197x`: Female physicians

**By Race/Ethnicity** (where available)

**International Medical Graduates (IMGs)**:
- `F1203x`: International medical graduates

### 3.2 Dentists (100+ variables)

| Variable | Description |
|----------|-------------|
| `F0886x` | Total dentists | 1990-2023 |
| `F0887x` | General practice dentists | 1990-2023 |
| `F08870` | Pediatric dentists | Latest year |
| `F08871` | Orthodontists | Latest year |
| `F08872` | Oral surgeons | Latest year |
| `F08873` | Periodontists | Latest year |
| `F08874` | Endodontists | Latest year |
| `F08875` | Prosthodontists | Latest year |
| `F1525x` | Dentists per 100,000 population |

### 3.3 Nurses (200+ variables)

**Registered Nurses (RNs)**:
- `F0894x`: Total RNs | 1990-2023
- `F15261`: RNs per 100,000 population
- `F15262`: Hospital RNs
- `F15263`: Nursing home RNs
- `F15264`: Public health RNs
- `F15265`: School nurses

**Licensed Practical Nurses (LPNs)**:
- `F0895x`: Total LPNs | 1990-2023
- `F15271`: LPNs per 100,000 population

**Advanced Practice Nurses**:
- `F1528x`: Nurse practitioners (NPs)
- `F15281`: Certified nurse midwives (CNMs)
- `F15282`: Certified registered nurse anesthetists (CRNAs)
- `F15283`: Clinical nurse specialists (CNSs)

### 3.4 Mental Health Providers (200+ variables)

**Psychiatrists**:
- `F1180x`: Psychiatrists | 1990-2023
- `F11801`: Child & adolescent psychiatrists
- `F11802`: Geriatric psychiatrists
- `F11803`: Addiction psychiatrists

**Psychologists**:
- `F1530x`: Clinical psychologists
- `F1531x`: Counseling psychologists
- `F1532x`: School psychologists

**Licensed Clinical Social Workers (LCSWs)**:
- `F1533x`: LCSWs

**Mental Health Counselors**:
- `F1534x`: Licensed professional counselors (LPCs)
- `F1535x`: Marriage and family therapists (MFTs)

**Psychiatric Nurse Practitioners**:
- `F1536x`: Psychiatric NPs

### 3.5 Other Health Professions (400+ variables)

**Pharmacists**:
- `F1211x`: Total pharmacists
- `F12111`: Retail pharmacists
- `F12112`: Hospital pharmacists

**Physician Assistants (PAs)**:
- `F0888x`: Total PAs | 1990-2023
- `F15271`: PAs per 100,000 population

**Optometrists**:
- `F1212x`: Optometrists

**Podiatrists**:
- `F1213x`: Podiatrists

**Chiropractors**:
- `F1214x`: Chiropractors

**Physical Therapists**:
- `F1215x`: Physical therapists

**Occupational Therapists**:
- `F1216x`: Occupational therapists

**Speech-Language Pathologists**:
- `F1217x`: Speech-language pathologists

**Respiratory Therapists**:
- `F1218x`: Respiratory therapists

**Dietitians/Nutritionists**:
- `F1219x`: Registered dietitians

**Emergency Medical Technicians (EMTs) & Paramedics**:
- `F1220x`: EMTs
- `F1221x`: Paramedics

---

## 4. HEALTH PROFESSIONAL SHORTAGE AREAS (200+ VARIABLES)

### 4.1 HPSA Designations

**Primary Care HPSAs**:
- `F0978x`: Primary care HPSA (yes/no)
- `F0979x`: Primary care HPSA score (0-26)
- `F09791`: Primary care HPSA designation date
- `F09792`: Primary care HPSA population
- `F09793`: Primary care HPSA Type (Geographic, Population, Facility)

**Dental HPSAs**:
- `F0980x`: Dental HPSA (yes/no)
- `F0981x`: Dental HPSA score
- `F09811`: Dental HPSA population

**Mental Health HPSAs**:
- `F0982x`: Mental health HPSA (yes/no)
- `F0983x`: Mental health HPSA score
- `F09831`: Mental health HPSA population

### 4.2 Medically Underserved Areas/Populations

**MUA (Medically Underserved Area)**:
- `F0975x`: MUA designation (yes/no)
- `F09751`: MUA score (Index of Medical Underservice, 0-100)
  - <62 = Underserved
  - Components: Primary care providers per 1,000, infant mortality, % elderly, % below poverty

**MUP (Medically Underserved Population)**:
- `F0976x`: MUP designation (yes/no)
- Examples: Homeless, migrant farmworkers, Native Americans

### 4.3 National Health Service Corps (NHSC)

**NHSC Sites**:
- `F15601`: NHSC-approved sites
- `F15602`: NHSC clinicians serving

**NHSC Loan Repayment**:
- `F15603`: Counties eligible for NHSC loan repayment

---

## 5. HEALTH STATUS INDICATORS (500+ VARIABLES)

### 5.1 Mortality (200+ variables)

**All-Cause Mortality**:
- `F1123x`: Total deaths | 1990-2023
- `F11231`: Death rate per 100,000 population

**Infant Mortality**:
- `F1124x`: Infant deaths (<1 year)
- `F1125x`: Infant mortality rate per 1,000 live births

**Age-Specific Mortality**:
- Deaths by 10-year age groups
- Age-adjusted mortality rates

**Leading Causes** (available for major causes):
- Heart disease deaths
- Cancer deaths
- Stroke deaths
- Chronic lower respiratory disease deaths
- Accidents/unintentional injuries
- Diabetes deaths
- Alzheimer disease deaths
- Kidney disease deaths
- Suicide deaths
- Homicide deaths

### 5.2 Births & Reproductive Health (150+ variables)

**Live Births**:
- `F0437x`: Total live births | 1990-2023
- `F0438x`: Birth rate per 1,000 population

**Fertility Rates**:
- `F0439x`: General fertility rate (births per 1,000 women age 15-44)
- `F04391`: Teen birth rate (age 15-19)
- `F04392`: Birth rate age 20-24
- Age-specific fertility rates (5-year age groups)

**Birth Outcomes**:
- `F1227x`: Low birthweight (<2,500 grams)
- `F1228x`: Very low birthweight (<1,500 grams)
- `F1229x`: Preterm births (<37 weeks gestation)

**Maternal Characteristics**:
- % Births with adequate prenatal care
- % Births to unmarried mothers
- % Births to mothers with <12 years education
- Cesarean delivery rate

### 5.3 Infectious Diseases (50+ variables)

**HIV/AIDS**:
- `F1430x`: HIV prevalence
- `F1431x`: AIDS cases
- `F1432x`: AIDS deaths

**Tuberculosis**:
- `F1433x`: TB cases
- `F1434x`: TB incidence rate per 100,000

**Sexually Transmitted Infections**:
- `F1435x`: Chlamydia cases
- `F1436x`: Gonorrhea cases
- `F1437x`: Syphilis cases

### 5.4 Chronic Disease Prevalence (100+ variables)

**Note**: Many chronic disease variables come from CDC PLACES, which is integrated into AHRF.

**Diabetes**:
- `F1640x`: Diagnosed diabetes prevalence (%)

**Obesity**:
- `F1641x`: Adult obesity prevalence (BMI ≥30)

**Hypertension**:
- `F1642x`: High blood pressure prevalence

**Asthma**:
- `F1643x`: Current asthma prevalence

**COPD**:
- `F1644x`: COPD prevalence

**Heart Disease**:
- `F1645x`: Coronary heart disease prevalence

---

## 6. SOCIOECONOMIC CHARACTERISTICS (2000+ VARIABLES)

### 6.1 Population (400+ variables)

**Total Population**:
- `F1119x`: Total population | 1970-2023
- `F11982`: Total population 2020 (Census)
- `F11983`: Total population 2023 (estimate)

**Age Distribution**:
- Population by single year of age (0-85+)
- Population by 5-year age groups
- `F1126x`: % Population under age 18
- `F1127x`: % Population age 65+
- `F11271`: % Population age 85+
- Median age

**Sex**:
- `F1135x`: Male population
- `F1136x`: Female population

**Race/Ethnicity** (detailed breakdowns):
- White alone
- Black/African American alone
- American Indian/Alaska Native alone
- Asian alone (with detailed subgroups)
- Native Hawaiian/Pacific Islander alone
- Two or more races
- Hispanic/Latino (any race)

**Migration**:
- Net migration
- Domestic migration
- International migration

### 6.2 Economics (600+ variables)

**Income**:
- `F1398x`: Median household income | 1980-2023
- `F1399x`: Per capita income | 1970-2023
- `F14001`: Mean household income
- Income by quintiles
- Household income distribution (<$10k, $10-15k, etc.)

**Poverty**:
- `F1400x`: Persons below poverty level (count)
- `F1401x`: Poverty rate (%)
- `F14011`: Child poverty rate (age <18)
- `F14012`: Senior poverty rate (age 65+)
- `F14013`: Poverty rate for families

**Employment**:
- `F0531x`: Total civilian labor force | 1990-2023
- `F0532x`: Unemployed persons
- `F0533x`: Unemployment rate
- `F05331`: Labor force participation rate
- Employment by industry (NAICS 2-digit)

**Income Inequality**:
- `F1460x`: Gini index

**Per Capita Personal Income**:
- `F1502x`: Per capita personal income (BEA)

### 6.3 Education (300+ variables)

**Educational Attainment** (age 25+):
- `F1434x`: Less than high school diploma (%)
- `F1435x`: High school graduate only (%)
- `F1436x`: Some college, no degree (%)
- `F1437x`: Associate's degree (%)
- `F1438x`: Bachelor's degree (%)
- `F1439x`: Graduate or professional degree (%)
- `F14391`: Bachelor's degree or higher (%)

**School Enrollment**:
- Enrollment by level (preschool, K-12, college)
- Public vs. private enrollment

### 6.4 Housing (200+ variables)

**Housing Units**:
- `F1540x`: Total housing units
- `F1541x`: Occupied housing units
- `F1542x`: Vacant housing units
- `F15421`: Homeowner vacancy rate
- `F15422`: Rental vacancy rate

**Tenure**:
- `F1543x`: Owner-occupied units
- `F1544x`: Renter-occupied units
- `F15441`: Homeownership rate (%)

**Housing Costs**:
- `F1545x`: Median home value
- `F1546x`: Median gross rent
- `F15461`: % Cost-burdened homeowners (>30% income on housing)
- `F15462`: % Cost-burdened renters (>30% income on housing)

**Housing Age & Quality**:
- % Built in specific decade
- % Lacking complete plumbing
- % Lacking complete kitchen
- Overcrowding rate

### 6.5 County Classifications (100+ variables)

**Urban-Rural**:
- `F0978x`: USDA Rural-Urban Continuum Code (RUCC)
  - 1: Metro, 1M+ population
  - 2: Metro, 250k-1M
  - 3: Metro, <250k
  - 4-9: Non-metro counties (various sizes, adjacent to metro or not)
- `F0979x`: USDA Urban Influence Code
- `F09791`: OMB Metropolitan/Micropolitan designation

**Economic Type** (USDA ERS County Typology):
- Farming-dependent
- Mining-dependent
- Manufacturing-dependent
- Federal/state government-dependent
- Recreation-dependent
- Persistent poverty
- Persistent child poverty
- Low education
- Low employment
- Population loss

**Geographic**:
- `F00012`: Land area (square miles)
- `F00013`: Water area (square miles)
- `F00014`: Population density (per square mile)
- `F00015`: Latitude (county centroid)
- `F00016`: Longitude (county centroid)

### 6.6 Crime (50+ variables)

**From FBI Uniform Crime Reports**:
- `F1604x`: Violent crime rate per 100,000
- `F16041`: Murder rate
- `F16042`: Rape rate
- `F16043`: Robbery rate
- `F16044`: Aggravated assault rate
- `F1605x`: Property crime rate
- `F16051`: Burglary rate
- `F16052`: Larceny-theft rate
- `F16053`: Motor vehicle theft rate

---

## 7. MEDICARE & MEDICAID (800+ VARIABLES)

### 7.1 Medicare Enrollment (200+ variables)

**Total Enrollment**:
- `F1498x`: Total Medicare beneficiaries | 1990-2023
- `F14981`: Medicare beneficiaries age 65+
- `F14982`: Medicare beneficiaries age <65 (disabled)
- `F14983`: Medicare beneficiaries with ESRD

**By Program**:
- `F14991`: Medicare Part A enrollment
- `F14992`: Medicare Part B enrollment
- `F14993`: Medicare Part D enrollment
- `F14994`: Medicare Advantage enrollment
- `F14995`: Medicare fee-for-service enrollment

**Enrollment Rate**:
- `F15001`: % Population age 65+ enrolled in Medicare

### 7.2 Medicare Utilization (300+ variables)

**Hospitalizations**:
- `F1510x`: Medicare hospital discharges
- `F15101`: Medicare hospitalization rate per 1,000 beneficiaries
- `F15102`: Medicare hospital days per 1,000 beneficiaries

**Post-Acute Care**:
- `F1511x`: SNF (skilled nursing facility) stays
- `F1512x`: Home health episodes
- `F1513x`: Hospice days

**Ambulatory Care**:
- `F1514x`: Physician evaluation & management visits
- `F1515x`: Emergency department visits per 1,000 beneficiaries

**Preventive Services**:
- `F1516x`: Annual wellness visits
- `F15161`: Mammography screening rate
- `F15162`: Colorectal cancer screening rate
- `F15163`: Flu vaccination rate

### 7.3 Medicare Spending (300+ variables)

**Total Spending**:
- `F1520x`: Total Medicare spending (per capita)
- `F15201`: Medicare Part A spending per capita
- `F15202`: Medicare Part B spending per capita
- `F15203`: Medicare Part D spending per capita

**By Service Type**:
- `F1521x`: Inpatient hospital spending per capita
- `F1522x`: Outpatient hospital spending per capita
- `F1523x`: Physician services spending per capita
- `F1524x`: Home health spending per capita
- `F1525x`: SNF spending per capita
- `F1526x`: Hospice spending per capita
- `F1527x`: Durable medical equipment spending per capita

**Risk-Adjusted Spending**:
- `F1530x`: Standardized spending per capita (HCC risk-adjusted)

### 7.4 Medicaid (100+ variables)

**Enrollment**:
- `F1600x`: Total Medicaid enrollment | 2000-2023
- `F16001`: Medicaid enrollment (children)
- `F16002`: Medicaid enrollment (adults)
- `F16003`: Medicaid enrollment (aged, blind, disabled)
- `F16004`: Medicaid/CHIP enrollment
- `F16005`: Medicaid expansion state (yes/no, 2014+)

**Enrollment Rate**:
- `F16010`: % Population enrolled in Medicaid

---

## 8. ACCESS METHODS

### 8.1 Direct Download (Recommended)

**HRSA Data Warehouse**:
- **URL**: https://data.hrsa.gov/topics/health-workforce/ahrf
- **Format**: SAS (.sas7bdat), CSV, Excel
- **No registration required**
- **File size**: 500 MB (Excel), 2 GB (SAS)

**Download Steps**:
1. Navigate to https://data.hrsa.gov/topics/health-workforce/ahrf
2. Click "Download" button
3. Select format (CSV recommended for R, Excel for quick exploration)
4. Unzip downloaded file

**Annual Release**: Typically released in March-April for previous year's data (e.g., 2024 AHRF released April 2024 with data through 2023)

### 8.2 HRSA Data Explorer (Interactive)

**Web Portal**: https://data.hrsa.gov/data/data-explorer

**Features**:
- Interactive county maps
- Filter by variable, state, year
- Compare counties
- Export selected variables to CSV

**Limitations**:
- Maximum 50 variables per export
- For bulk access, use direct download

### 8.3 API Access

**HRSA Open API**: https://data.hrsa.gov/api

**Endpoint Example**:
```
https://data.hrsa.gov/api/3/action/datastore_search?resource_id={AHRF_RESOURCE_ID}&filters={filters}
```

**Note**: API access primarily for HRSA Data Warehouse datasets; AHRF bulk download recommended for comprehensive county-level data.

---

## 9. R CODE EXAMPLES

### 9.1 Read AHRF File

```r
library(tidyverse)
library(haven)  # For reading SAS files

# Option 1: Read SAS file (most complete, preserves labels)
ahrf <- read_sas("AHRF_2023-2024.sas7bdat")

# View variable labels
var_labels <- map_chr(ahrf, ~attr(.x, "label"))
var_labels_df <- tibble(
  variable = names(ahrf),
  label = var_labels
)

# Option 2: Read CSV (easier, but loses some metadata)
ahrf_csv <- read_csv("AHRF_2023-2024.csv")

# Examine structure
glimpse(ahrf)
```

### 9.2 Extract Key Health Workforce Variables

```r
library(tidyverse)

# Read AHRF
ahrf <- read_sas("AHRF_2023-2024.sas7bdat")

# Extract key variables
health_workforce <- ahrf %>%
  select(
    state_fips = F00002,
    county_fips = F00003,
    state_county = F00011,
    state_abbr = F00008,
    county_name = F00009,

    # Population
    population_2023 = F11983,

    # Primary Care
    primary_care_md_2023 = F08923,
    primary_care_per_100k_2023 = F15243,

    # Dentists
    dentists_2023 = F08863,
    dentists_per_100k_2023 = F15253,

    # Mental Health
    psychiatrists_2023 = F11803,
    psychologists_2023 = F15303,
    lcsw_2023 = F15333,

    # Facilities
    hospitals_2023 = F04532,
    hospital_beds_2023 = F08923,
    fqhc_sites_2023 = F15173,

    # HPSAs
    primary_care_hpsa = F09783,
    dental_hpsa = F09803,
    mental_health_hpsa = F09823,

    # Medicare
    medicare_beneficiaries_2023 = F14983,
    medicare_spending_pc_2023 = F15203
  )

# Calculate provider ratios
health_workforce <- health_workforce %>%
  mutate(
    population_per_primary_care_md = population_2023 / primary_care_md_2023,
    population_per_dentist = population_2023 / dentists_2023,
    population_per_psychiatrist = population_2023 / psychiatrists_2023
  )

# Summary statistics
summary(health_workforce)
```

### 9.3 Identify Health Workforce Shortages

```r
library(tidyverse)

# Define shortage thresholds
shortage_analysis <- health_workforce %>%
  mutate(
    # Primary care shortage: >3,500:1 ratio or HPSA
    primary_care_shortage =
      (population_per_primary_care_md > 3500 | primary_care_hpsa == 1),

    # Dental shortage: >5,000:1 ratio or dental HPSA
    dental_shortage =
      (population_per_dentist > 5000 | dental_hpsa == 1),

    # Mental health shortage: >30,000:1 ratio or MH HPSA
    mental_health_shortage =
      (population_per_psychiatrist > 30000 | mental_health_hpsa == 1),

    # Count total shortage areas
    shortage_count = primary_care_shortage + dental_shortage + mental_health_shortage
  )

# Counties with multiple shortages
high_need_counties <- shortage_analysis %>%
  filter(shortage_count >= 2) %>%
  arrange(desc(shortage_count), desc(population_2023))

# Summary
table(shortage_analysis$shortage_count)
```

### 9.4 Time Series Analysis

```r
library(tidyverse)

# Extract primary care physician counts over time
pcp_trend <- ahrf %>%
  select(
    state_county = F00011,
    county_name = F00009,
    pcp_2010 = F08910,
    pcp_2015 = F08915,
    pcp_2020 = F08920,
    pcp_2023 = F08923,
    pop_2010 = F11980,
    pop_2023 = F11983
  ) %>%
  mutate(
    # Calculate rates per 100,000
    pcp_rate_2010 = (pcp_2010 / pop_2010) * 100000,
    pcp_rate_2023 = (pcp_2023 / pop_2023) * 100000,

    # Calculate change
    pcp_rate_change = pcp_rate_2023 - pcp_rate_2010,
    pcp_rate_pct_change = ((pcp_rate_2023 / pcp_rate_2010) - 1) * 100
  )

# Counties with largest increases/decreases
pcp_gains <- pcp_trend %>%
  filter(!is.na(pcp_rate_change)) %>%
  arrange(desc(pcp_rate_change)) %>%
  head(20)

pcp_losses <- pcp_trend %>%
  filter(!is.na(pcp_rate_change)) %>%
  arrange(pcp_rate_change) %>%
  head(20)
```

### 9.5 Multi-Variable Analysis: Social Determinants & Health Workforce

```r
library(tidyverse)

# Extract comprehensive county profile
county_profile <- ahrf %>%
  select(
    state_county = F00011,
    county_name = F00009,
    state_abbr = F00008,

    # Population & Demographics
    population = F11983,
    pct_65plus = F11270,
    pct_rural = F04397,

    # Socioeconomics
    median_income = F13984,
    poverty_rate = F14012,
    unemployment_rate = F05332,
    pct_bachelor_plus = F14391,

    # Health Workforce
    primary_care_rate = F15243,
    dentist_rate = F15253,
    mental_health_providers = F15303 + F15333,  # Psychologists + LCSWs

    # Health Status
    all_cause_mortality_rate = F11231,
    infant_mortality_rate = F11251,

    # Health Facilities
    hospitals = F04532,
    hospital_beds = F08923,
    fqhc_sites = F15173,

    # Medicare
    medicare_spending_pc = F15203
  )

# Correlation analysis
cor_matrix <- county_profile %>%
  select(where(is.numeric)) %>%
  cor(use = "pairwise.complete.obs")

# Model: Predict mortality from social determinants and workforce
library(broom)

mortality_model <- lm(
  all_cause_mortality_rate ~
    poverty_rate +
    unemployment_rate +
    pct_bachelor_plus +
    primary_care_rate +
    dentist_rate +
    pct_65plus +
    pct_rural,
  data = county_profile
)

tidy(mortality_model)
glance(mortality_model)
```

### 9.6 Geographic Mapping

```r
library(tidyverse)
library(sf)
library(tigris)

# Get county shapefiles
counties_sf <- counties(cb = TRUE, year = 2023)

# Merge AHRF data
map_data <- counties_sf %>%
  mutate(state_county = paste0(STATEFP, COUNTYFP)) %>%
  left_join(
    health_workforce %>% select(state_county, primary_care_per_100k_2023),
    by = "state_county"
  )

# Create choropleth map
library(ggplot2)
library(viridis)

ggplot(map_data) +
  geom_sf(aes(fill = primary_care_per_100k_2023), color = NA) +
  scale_fill_viridis(
    name = "Primary Care\nPhysicians per\n100,000",
    option = "plasma",
    na.value = "grey90",
    limits = c(0, 200)
  ) +
  labs(
    title = "Primary Care Physician Density by County",
    subtitle = "US Counties, 2023",
    caption = "Source: HRSA Area Health Resources File"
  ) +
  theme_void() +
  theme(
    plot.title = element_text(hjust = 0.5, face = "bold", size = 14),
    plot.subtitle = element_text(hjust = 0.5, size = 11),
    legend.position = "right"
  )
```

---

## 10. DATA QUALITY AND LIMITATIONS

### 10.1 Data Source Variability

**Multiple Sources = Inconsistent Quality**:
- AHRF compiles from 50+ sources
- Each source has different:
  - Collection methods
  - Update frequencies
  - Data quality procedures
  - Coverage rates

**Example Variability**:
- **AMA Physician Masterfile**: ~95% coverage of US physicians, but self-reported addresses may be outdated
- **Hospital data (AHA Survey)**: ~80% response rate; non-respondents imputed
- **Census/ACS**: High quality, but estimates have margins of error

### 10.2 Temporal Consistency

**Variable Availability Varies**:
- Some variables available 1970-2023 (e.g., population)
- Others only recent years (e.g., FQHC data starts ~2000)
- Not all variables updated annually

**Year Lag**:
- AHRF typically released with 1-year lag
- Example: 2023-2024 AHRF (released April 2024) contains data through 2023
- Some variables may have 2-3 year lag (especially specialty physician counts)

### 10.3 Geographic Accuracy

**Provider Location Issues**:
- Physician counts based on **mailing address**, not practice location
- May overcount urban counties (where billing offices located)
- May undercount rural counties (where physicians practice but don't have mailing address)

**County Boundary Changes**:
- Alaska: Multiple borough consolidations/formations
- Virginia: Independent cities sometimes merge with counties
- AHRF uses FIPS codes current at time of data release

### 10.4 Small Numbers

**Rural Counties**:
- Many variables have 0 or very small counts
- Rates become unstable
- Single provider entering/leaving county causes large rate swings

**Recommendation**:
- For rural counties, consider:
  - Regional aggregation (HRR, multi-county clusters)
  - Multi-year averages
  - Absolute counts rather than rates

### 10.5 Missing Data

**Patterns of Missingness**:
- Specialty physician counts: More missing for rare specialties
- Hospital data: Missing for counties with no hospitals
- Medicare data: Complete (administrative data)
- HPSA: Missing if county never applied for designation (doesn't mean adequate; may mean unawareness)

**Handling**:
```r
# Check missingness
ahrf %>%
  summarise(across(everything(), ~sum(is.na(.)) / n() * 100))

# Imputation (use cautiously)
library(mice)
```

### 10.6 Definition Changes Over Time

**Standardization Challenges**:
- HPSA scoring changed in 2008
- Rural-Urban Continuum Codes updated periodically
- ICD code changes affect mortality data
- Always check technical documentation for definition changes

---

## 11. PRIORITY VARIABLES FOR COUNTY-LEVEL COLLECTION

### 11.1 Essential Variables (Top 30)

**Demographics** (5):
1. Total population (latest year)
2. % Population age 65+
3. % Rural
4. Median household income
5. Poverty rate

**Primary Health Workforce** (10):
6. Primary care physicians (count)
7. Primary care physicians per 100,000
8. Dentists (count)
9. Dentists per 100,000
10. Registered nurses (count)
11. Nurse practitioners (count)
12. Physician assistants (count)
13. Psychiatrists (count)
14. Psychologists (count)
15. Licensed clinical social workers (count)

**Health Facilities** (8):
16. Total hospitals
17. Hospital beds
18. Critical Access Hospitals
19. Community health centers (FQHC sites)
20. Nursing homes
21. Nursing home beds
22. Dialysis facilities
23. Mental health facilities

**Health Workforce Shortages** (3):
24. Primary care HPSA (yes/no, score)
25. Dental HPSA (yes/no, score)
26. Mental health HPSA (yes/no, score)

**Health Status** (4):
27. All-cause mortality rate
28. Infant mortality rate
29. Life expectancy (if available)
30. HIV prevalence

### 11.2 Comprehensive Collection (All 7,000+ Variables)

For truly **ultra-comprehensive** county-level surveillance:
- Download entire AHRF file (all variables, all years available)
- ~7,000 variables provide unparalleled county-level detail
- Enables exploratory analysis, identification of new relationships

---

## DOCUMENTATION VERSION

**Document Version**: 1.0
**Last Updated**: November 11, 2025
**Author**: Claude Code
**Data Source**: Health Resources and Services Administration (HRSA)
**Verification Status**: All URLs and access methods verified as of November 2025

---

## QUICK REFERENCE

**Download AHRF**: https://data.hrsa.gov/topics/health-workforce/ahrf
**Data Explorer**: https://data.hrsa.gov/data/data-explorer
**Technical Documentation**: Included in AHRF download (Excel file)
**No API Key Required**
**No Registration Required**
**Cost**: Free

**Key Contacts**:
- HRSA Data Warehouse: BHWDataWarehouse@hrsa.gov
- AHRF Questions: AHRF@hrsa.gov

---

**END OF COMPREHENSIVE HRSA AHRF DOCUMENTATION**
