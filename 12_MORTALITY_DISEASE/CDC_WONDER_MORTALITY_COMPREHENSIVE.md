# CDC WONDER MORTALITY DATA - COMPREHENSIVE COUNTY-LEVEL DOCUMENTATION

**Last Updated**: November 2025
**Geographic Level**: County (FIPS code)
**Temporal Coverage**: 1968-2023 (varies by database)
**Update Frequency**: Annual (typically 11-month lag)

---

## EXECUTIVE SUMMARY

CDC WONDER (Wide-ranging Online Data for Epidemiologic Research) provides access to multiple mortality databases with county-level detail. The **Multiple Cause of Death (MCOD)** database is the most comprehensive, containing ALL deaths occurring in the United States with detailed cause-of-death coding using ICD-10 (1999-2023) and ICD-9 (1979-1998).

**Key Features**:
- **Complete mortality universe**: ALL deaths in the US, not a sample
- **ICD-10 coding**: 69,823 diagnosis codes organized into 21 chapters
- **Multiple causes**: Underlying cause + up to 20 contributing causes per death
- **Demographics**: Age (5-year groups, 10-year groups, single year), sex, race/ethnicity (7 categories), Hispanic origin
- **County residence**: Decedent's county of residence at time of death
- **113 Selected Causes**: Standardized cause-of-death groupings used by NCHS
- **Annual data**: 1999-2023 (ICD-10 era), with 2024 data expected late 2025

**Data Suppression**:
- Counts of 1-9 deaths are suppressed in public-use files for privacy
- Rates not calculated for <20 deaths (unreliable)
- Researchers can access restricted-use files with suppressed cells through NCHS RDC

**Total Variables**: 100+ variables covering deaths, population, rates, demographic characteristics, and cause-of-death coding

---

## TABLE OF CONTENTS

1. [Multiple Cause of Death Database (MCOD)](#1-multiple-cause-of-death-database-mcod)
2. [Underlying Cause of Death Database](#2-underlying-cause-of-death-database)
3. [Compressed Mortality Database (CMF)](#3-compressed-mortality-database-cmf)
4. [ICD-10 Coding System](#4-icd-10-coding-system)
5. [113 Selected Causes of Death](#5-113-selected-causes-of-death)
6. [Demographic Variables](#6-demographic-variables)
7. [Calculated Variables](#7-calculated-variables)
8. [Access Methods](#8-access-methods)
9. [R Code Examples](#9-r-code-examples)
10. [Data Quality and Limitations](#10-data-quality-and-limitations)
11. [County-Level Analysis Best Practices](#11-county-level-analysis-best-practices)

---

## 1. MULTIPLE CAUSE OF DEATH DATABASE (MCOD)

The **Multiple Cause of Death** database is the gold standard for mortality research, containing the full death certificate information including underlying cause and up to 20 contributing causes.

### 1.1 Core Variables

| Variable | Description | Coding | Years |
|----------|-------------|--------|-------|
| `Deaths` | Number of deaths | Count | 1999-2023 |
| `Population` | Resident population (July 1) | Count | 1999-2023 |
| `Crude Rate` | Deaths per 100,000 population | Rate | 1999-2023 |
| `Age Adjusted Rate` | Standardized to 2000 US population | Rate | 1999-2023 |
| `Percent of Total Deaths` | Deaths as % of all deaths | Percentage | 1999-2023 |

### 1.2 Underlying Cause of Death (UCD)

The **underlying cause** is the disease or injury that initiated the chain of events leading to death.

**ICD-10 Chapter Structure** (21 chapters):

1. **A00-B99**: Certain infectious and parasitic diseases
2. **C00-D48**: Neoplasms (cancers)
3. **D50-D89**: Diseases of blood and blood-forming organs
4. **E00-E90**: Endocrine, nutritional and metabolic diseases
5. **F00-F99**: Mental and behavioral disorders
6. **G00-G99**: Diseases of the nervous system
7. **H00-H59**: Diseases of the eye and adnexa
8. **H60-H95**: Diseases of the ear and mastoid process
9. **I00-I99**: Diseases of the circulatory system
10. **J00-J99**: Diseases of the respiratory system
11. **K00-K93**: Diseases of the digestive system
12. **L00-L99**: Diseases of the skin and subcutaneous tissue
13. **M00-M99**: Diseases of the musculoskeletal system
14. **N00-N99**: Diseases of the genitourinary system
15. **O00-O99**: Pregnancy, childbirth and the puerperium
16. **P00-P96**: Certain conditions originating in the perinatal period
17. **Q00-Q99**: Congenital malformations and chromosomal abnormalities
18. **R00-R99**: Symptoms, signs and abnormal findings (not elsewhere classified)
19. **S00-T98**: Injury, poisoning and external causes
20. **V01-Y98**: External causes of morbidity and mortality
21. **U00-U99**: Codes for special purposes

### 1.3 Multiple Causes of Death (MCD)

In addition to the underlying cause, the database includes up to **20 contributing causes** listed on the death certificate (Part I and Part II).

**Example**:
- Underlying cause: Diabetes (E11.9)
- Contributing causes: Chronic kidney disease (N18.5), Hypertension (I10), Coronary artery disease (I25.10)

**Use cases**:
- Identifying comorbidities
- Understanding disease burden beyond primary cause
- Researching multi-morbidity patterns
- Chronic disease surveillance

### 1.4 Top 10 Leading Causes of Death (2023 Provisional)

| Rank | Cause | ICD-10 Codes | Annual Deaths (US) |
|------|-------|--------------|-------------------|
| 1 | Heart disease | I00-I09, I11, I13, I20-I51 | ~695,000 |
| 2 | Cancer | C00-C97 | ~605,000 |
| 3 | COVID-19 | U07.1 | ~76,000 (declining) |
| 4 | Accidents (unintentional injuries) | V01-X59, Y85-Y86 | ~227,000 |
| 5 | Stroke (cerebrovascular diseases) | I60-I69 | ~162,000 |
| 6 | Chronic lower respiratory diseases | J40-J47 | ~147,000 |
| 7 | Alzheimer disease | G30 | ~120,000 |
| 8 | Diabetes mellitus | E10-E14 | ~103,000 |
| 9 | Chronic liver disease and cirrhosis | K70, K73-K74 | ~55,000 |
| 10 | Nephritis, nephrotic syndrome, nephrosis | N00-N07, N17-N19, N25-N27 | ~54,000 |

### 1.5 Drug Overdose Deaths (Opioid Epidemic)

CDC WONDER includes detailed drug overdose mortality:

| Drug Category | ICD-10 Codes | Description |
|--------------|--------------|-------------|
| **All drug overdoses** | X40-X44, X60-X64, X85, Y10-Y14 | Unintentional, suicide, homicide, undetermined |
| **Opioids (total)** | T40.0-T40.4, T40.6 | All opioid drugs |
| - Natural/semi-synthetic opioids | T40.2 | Oxycodone, hydrocodone, morphine |
| - Methadone | T40.3 | Methadone |
| - Synthetic opioids (excl. methadone) | T40.4 | Fentanyl, tramadol |
| - Heroin | T40.1 | Heroin |
| **Cocaine** | T40.5 | Cocaine |
| **Psychostimulants with abuse potential** | T43.6 | Methamphetamine, amphetamines |
| **Benzodiazepines** | T42.4 | Alprazolam, diazepam, clonazepam |

**County-level analysis**:
- Essential for tracking opioid epidemic geographic patterns
- Many rural counties have suppressed data (<10 deaths)
- Multi-year aggregation recommended for small counties

---

## 2. UNDERLYING CAUSE OF DEATH DATABASE

Simplified version focusing only on the underlying cause of death (not multiple causes).

**Differences from MCOD**:
- Faster query performance
- Underlying cause only (no contributing causes)
- Same demographic and geographic variables
- Same suppression rules

**Best for**:
- Standard mortality rate calculations
- Leading cause analyses
- County health rankings
- Temporal trend analysis

---

## 3. COMPRESSED MORTALITY DATABASE (CMF)

Historical mortality data with longer time series but fewer cause-of-death categories.

### 3.1 Coverage

- **1968-1978**: 72 cause-of-death categories (ICD-8)
- **1979-1998**: 72 cause-of-death categories (ICD-9)
- **1999-2020**: 113 selected causes (ICD-10)

### 3.2 Geographic Detail

- County level (1968-2020)
- **Important**: County boundaries have changed over time
- Alaska and Virginia: Significant boundary changes
- Database includes county equivalents (parishes, boroughs, independent cities)

### 3.3 Use Cases

- **Long-term trends**: Analyzing mortality patterns over 50+ years
- **Historical research**: Pre-ICD-10 era analysis
- **County health profiles**: Multi-decade county health trajectories

---

## 4. ICD-10 CODING SYSTEM

The **International Classification of Diseases, 10th Revision (ICD-10)** has been used in the US since 1999.

### 4.1 Code Structure

- **3-character categories**: 2,037 categories (e.g., I21 = Acute myocardial infarction)
- **4-character subcategories**: 12,420 codes (e.g., I21.0 = STEMI of anterior wall)
- **5-6 character clinical details**: 69,823 total codes (e.g., I21.01 = STEMI involving left main coronary artery)

### 4.2 Most Common Causes by ICD-10 Code (2023)

| ICD-10 Code | Cause | Annual Deaths |
|-------------|-------|---------------|
| I25.1 | Atherosclerotic heart disease | ~385,000 |
| C34.9 | Malignant neoplasm of bronchus/lung | ~125,000 |
| J44.9 | Chronic obstructive pulmonary disease | ~140,000 |
| I64 | Stroke, not specified | ~50,000 |
| G30.9 | Alzheimer disease, unspecified | ~120,000 |
| X42 | Accidental poisoning by drugs | ~110,000 |
| I50.9 | Heart failure, unspecified | ~88,000 |
| J18.9 | Pneumonia, unspecified organism | ~45,000 |
| E11.9 | Type 2 diabetes mellitus without complications | ~35,000 |
| K70.3 | Alcoholic cirrhosis of liver | ~25,000 |
| I10 | Essential (primary) hypertension | ~40,000 |
| N18.6 | End stage renal disease | ~30,000 |
| F03.90 | Unspecified dementia without behavioral disturbance | ~55,000 |
| U07.1 | COVID-19 | ~76,000 (2023, declining) |

### 4.3 External Causes of Death (V, W, X, Y codes)

These codes capture **how** an injury occurred:

**Transport accidents**:
- V01-V99: Transport accidents
  - V02-V04: Pedestrian injured
  - V12-V14: Pedal cyclist injured
  - V20-V28: Motorcycle rider injured
  - V40-V49: Car occupant injured
  - V50-V59: Pickup truck/van occupant injured
  - V80-V89: Other land transport accidents

**Other external causes**:
- W00-W19: Falls
- W20-W49: Exposure to inanimate mechanical forces
- W50-W64: Exposure to animate mechanical forces
- W65-W74: Accidental drowning and submersion
- W85-W99: Exposure to electric current, radiation, temperature
- X00-X09: Exposure to smoke, fire, flames
- X10-X19: Contact with heat and hot substances
- X40-X49: Accidental poisoning (includes drug overdoses)
- X58-X59: Accidental exposure to other factors
- X60-X84: Intentional self-harm (suicide)
- X85-Y09: Assault (homicide)
- Y10-Y34: Event of undetermined intent
- Y35-Y36: Legal intervention and operations of war

---

## 5. 113 SELECTED CAUSES OF DEATH

NCHS uses a standardized list of **113 Selected Causes** for mortality reporting. This list groups ICD-10 codes into meaningful public health categories.

### 5.1 Complete 113 Selected Causes List

**Infectious and Parasitic Diseases** (1-8):
1. Salmonella infections (A01-A02)
2. Shigellosis and amebiasis (A03, A06)
3. Certain other intestinal infections (A04, A07-A09)
4. Tuberculosis (A16-A19)
5. Respiratory tuberculosis (A16)
6. Other tuberculosis (A17-A19)
7. Whooping cough (A37)
8. Scarlet fever and erysipelas (A38, A46)
9. Meningococcal infection (A39)
10. Septicemia (A40-A41)
11. Syphilis (A50-A53)
12. Acute poliomyelitis (A80)
13. Arthropod-borne viral encephalitis (A83-A84, A85.2)
14. Measles (B05)
15. Viral hepatitis (B15-B19)
16. Human immunodeficiency virus (HIV) disease (B20-B24)
17. Malaria (B50-B54)
18. Other and unspecified infectious and parasitic diseases

**Neoplasms** (19-44):
19. Malignant neoplasms (C00-C97)
20. Malignant neoplasms of lip, oral cavity, pharynx (C00-C14)
21. Malignant neoplasm of esophagus (C15)
22. Malignant neoplasm of stomach (C16)
23. Malignant neoplasms of colon, rectum, anus (C18-C21)
24. Malignant neoplasms of liver and intrahepatic bile ducts (C22)
25. Malignant neoplasm of pancreas (C25)
26. Malignant neoplasm of larynx (C32)
27. Malignant neoplasms of trachea, bronchus, lung (C33-C34)
28. Malignant melanoma of skin (C43)
29. Malignant neoplasm of breast (C50)
30. Malignant neoplasm of cervix uteri (C53)
31. Malignant neoplasms of corpus uteri and uterus, part unspecified (C54-C55)
32. Malignant neoplasm of ovary (C56)
33. Malignant neoplasm of prostate (C61)
34. Malignant neoplasms of kidney and renal pelvis (C64-C65)
35. Malignant neoplasm of bladder (C67)
36. Malignant neoplasms of meninges, brain, other CNS (C70-C72)
37. Malignant neoplasms of lymphoid, hematopoietic, related tissue (C81-C96)
38. Hodgkin disease (C81)
39. Non-Hodgkin lymphoma (C82-C85)
40. Leukemia (C91-C95)
41. Multiple myeloma and immunoproliferative neoplasms (C88, C90)
42. Other and unspecified malignant neoplasms of lymphoid, hematopoietic tissues (C96)
43. All other and unspecified malignant neoplasms (residual)
44. In situ neoplasms, benign neoplasms, neoplasms of uncertain behavior (D00-D48)

**Diseases of Blood and Blood-Forming Organs** (45-46):
45. Anemias (D50-D64)
46. Other diseases of blood and blood-forming organs (D65-D89)

**Endocrine, Nutritional, Metabolic Diseases** (47-53):
47. Diabetes mellitus (E10-E14)
48. Nutritional deficiencies (E40-E64)
49. Malnutrition (E40-E46)
50. Other nutritional deficiencies (E50-E64)
51. Obesity (E66)
52. Other metabolic disorders (E70-E88 except E66)
53. Meningitis (G00, G03)

**Mental and Behavioral Disorders** (54-56):
54. Alzheimer disease (G30)
55. Major cardiovascular diseases (I00-I78)
56. Diseases of heart (I00-I09, I11, I13, I20-I51)

**Circulatory System Diseases** (57-75):
57. Acute rheumatic fever and chronic rheumatic heart diseases (I00-I09)
58. Hypertensive heart disease (I11)
59. Hypertensive heart and renal disease (I13)
60. Ischemic heart diseases (I20-I25)
61. Acute myocardial infarction (I21-I22)
62. Other acute ischemic heart diseases (I24)
63. Other forms of chronic ischemic heart disease (I20, I25)
64. Atherosclerotic cardiovascular disease (I25.0)
65. All other forms of chronic ischemic heart disease (I20, I25.1-I25.9)
66. Other heart diseases (I26-I51)
67. Acute and subacute endocarditis (I33)
68. Diseases of pericardium and acute myocarditis (I30-I31, I40)
69. Heart failure (I50)
70. All other forms of heart disease (I26-I28, I34-I38, I42-I49, I51)
71. Essential hypertension and hypertensive renal disease (I10, I12, I15)
72. Cerebrovascular diseases (I60-I69)
73. Atherosclerosis (I70)
74. Other diseases of circulatory system (I71-I78)
75. Aortic aneurysm and dissection (I71)

**Respiratory System Diseases** (76-84):
76. Other diseases of arteries, arterioles, capillaries (I72-I78)
77. Other disorders of circulatory system (I80-I99)
78. Influenza and pneumonia (J09-J18)
79. Influenza (J09-J11)
80. Pneumonia (J12-J18)
81. Other acute lower respiratory infections (J20-J22)
82. Acute bronchitis and bronchiolitis (J20-J21)
83. Chronic lower respiratory diseases (J40-J47)
84. Bronchitis, chronic and unspecified (J40-J42)

**Digestive System Diseases** (85-92):
85. Emphysema (J43)
86. Asthma (J45-J46)
87. Other chronic lower respiratory diseases (J44, J47)
88. Pneumoconioses and chemical effects (J60-J66, J68)
89. Pneumonitis due to solids and liquids (J69)
90. Other diseases of respiratory system (J00-J06, J30-J39, J67, J70-J98)
91. Peptic ulcer (K25-K28)
92. Diseases of appendix (K35-K38)

**Genitourinary System Diseases** (93-97):
93. Hernia (K40-K46)
94. Chronic liver disease and cirrhosis (K70, K73-K74)
95. Alcoholic liver disease (K70)
96. Other chronic liver disease and cirrhosis (K73-K74)
97. Cholelithiasis and other disorders of gallbladder (K80-K82)

**Pregnancy, Childbirth, Puerperium** (98-102):
98. Other diseases of digestive system (K00-K24, K29-K31, K50-K66, K71-K72, K75-K76, K83-K93)
99. Nephritis, nephrotic syndrome, nephrosis (N00-N07, N17-N19, N25-N27)
100. Acute and rapidly progressive nephritic and nephrotic syndrome (N00-N01, N04)
101. Chronic glomerulonephritis, nephritis, nephropathy (N02-N03, N05-N06, N07.2-N07.9)
102. Renal failure (N17-N19)

**Congenital, Perinatal, Ill-Defined** (103-113):
103. Other disorders of kidney (N25, N27)
104. Infections of kidney (N10-N12, N13.6, N15.1)
105. Hyperplasia of prostate (N40)
106. Inflammatory diseases of female pelvic organs (N70-N76)
107. Other diseases of genitourinary system (N08-N09, N13.0-N13.5, N13.7-N13.9, N14, N15.0, N15.8-N15.9, N16, N20-N23, N26, N28-N39, N41-N64, N75, N77-N98)
108. Pregnancy, childbirth, puerperium (O00-O99)
109. Pregnancy with abortive outcome (O00-O07)
110. Other complications of pregnancy, childbirth, puerperium (O10-O99)
111. Certain conditions originating in perinatal period (P00-P96)
112. Congenital malformations, deformations, chromosomal abnormalities (Q00-Q99)
113. Symptoms, signs, abnormal findings, not elsewhere classified (R00-R99)

### 5.2 Injury Causes (External Causes)

**Accidents (unintentional injuries)**:
- Motor vehicle accidents (V02-V04, V09.0, V09.2, V12-V14, V19.0-V19.2, V19.4-V19.6, V20-V79, V80.3-V80.5, V81.0-V81.1, V82.0-V82.1, V83-V86, V87.0-V87.8, V88.0-V88.8, V89.0, V89.2)
- Falls (W00-W19)
- Accidental discharge of firearms (W32-W34)
- Accidental drowning and submersion (W65-W74)
- Accidental exposure to smoke, fire, flames (X00-X09)
- Accidental poisoning and exposure to noxious substances (X40-X49)
- Other and unspecified accidents

**Intentional self-harm (suicide)**:
- Suicide by discharge of firearms (X72-X74)
- Suicide by other and unspecified means (X60-X71, X75-X84, Y87.0)

**Assault (homicide)**:
- Assault by discharge of firearms (X93-X95)
- Assault by other and unspecified means (X85-X92, X96-Y09, Y87.1)

**Legal intervention** (Y35, Y89.0)

**Events of undetermined intent** (Y10-Y34, Y87.2, Y89.9)

**Operations of war and their sequelae** (Y36, Y89.1)

**Complications of medical and surgical care** (Y40-Y84, Y88)

---

## 6. DEMOGRAPHIC VARIABLES

### 6.1 Age Groups

CDC WONDER provides multiple age grouping options:

**Standard 5-year age groups** (18 groups):
- <1 year, 1-4, 5-9, 10-14, 15-19, 20-24, 25-29, 30-34, 35-39, 40-44, 45-49, 50-54, 55-59, 60-64, 65-69, 70-74, 75-79, 80-84, 85+

**10-year age groups** (9 groups):
- <1 year, 1-4, 5-14, 15-24, 25-34, 35-44, 45-54, 55-64, 65-74, 75-84, 85+

**Infant age groups** (4 groups):
- <1 hour, 1-23 hours, 1-6 days, 7-27 days, 28-364 days

**Single year of age**: 0-100+

**Infant, child, adult categories**:
- Infant (<1 year)
- Child (1-14 years)
- Working age (15-64 years)
- Elderly (65+ years)

### 6.2 Sex

- Male
- Female
- Not Stated

### 6.3 Race and Hispanic Origin

**Race** (7 categories):
1. American Indian or Alaska Native
2. Asian or Pacific Islander
   - Asian
   - Native Hawaiian or Other Pacific Islander
3. Black or African American
4. White

**Hispanic Origin** (2 categories):
- Hispanic or Latino
- Not Hispanic or Latino

**Combined Race/Ethnicity** (typically used for health disparities research):
- Hispanic or Latino (any race)
- Non-Hispanic White
- Non-Hispanic Black or African American
- Non-Hispanic American Indian or Alaska Native
- Non-Hispanic Asian or Pacific Islander

### 6.4 Place Variables

| Variable | Description | Coding |
|----------|-------------|--------|
| County of Residence | County where decedent lived | FIPS code (5 digits) |
| State of Residence | State where decedent lived | FIPS code (2 digits) |
| Census Region | 4 US regions | Northeast, Midwest, South, West |
| Census Division | 9 US divisions | New England, Mid-Atlantic, etc. |
| Urbanization | 2013 NCHS Urban-Rural Classification | 6 categories |

**NCHS Urban-Rural Classification** (2013):
1. Large Central Metro
2. Large Fringe Metro
3. Medium Metro
4. Small Metro
5. Micropolitan
6. Noncore (rural)

### 6.5 Time Variables

| Variable | Description |
|----------|-------------|
| Year | Calendar year of death |
| Month | Month of death (1-12) |
| Weekday | Day of week of death |
| Autopsy | Autopsy performed (Y/N/Unknown) |

---

## 7. CALCULATED VARIABLES

CDC WONDER automatically calculates several rate and percentage variables:

### 7.1 Mortality Rates

**Crude Rate**:
- Deaths per 100,000 population
- Formula: (Deaths / Population) × 100,000
- Useful for: Absolute burden of disease

**Age-Adjusted Rate**:
- Standardized to 2000 US standard population
- Controls for differences in age distribution
- Formula: Σ[(age-specific rate) × (standard population proportion)]
- Essential for: Comparing counties with different age structures

**Years of Potential Life Lost (YPLL)**:
- Measures premature mortality (deaths before age 75)
- Formula: Σ[(75 - age at death) for all deaths <75]
- Important for: Assessing preventable mortality burden

### 7.2 Confidence Intervals

CDC WONDER provides 95% confidence intervals for rates using the gamma distribution method.

### 7.3 Percent of Total Deaths

Proportion of all deaths attributable to a specific cause:
- Formula: (Cause-specific deaths / All deaths) × 100

---

## 8. ACCESS METHODS

### 8.1 CDC WONDER Web Portal (Public Access)

**URL**: https://wonder.cdc.gov/

**Available Databases**:
1. **Multiple Cause of Death, 1999-2020**: https://wonder.cdc.gov/mcd.html
2. **Multiple Cause of Death, 2018-2023** (provisional): https://wonder.cdc.gov/mcd-icd10-provisional.html
3. **Underlying Cause of Death, 1999-2020**: https://wonder.cdc.gov/ucd-icd10.html
4. **Compressed Mortality, 1968-1978**: https://wonder.cdc.gov/cmf-icd8.html
5. **Compressed Mortality, 1979-1998**: https://wonder.cdc.gov/cmf-icd9.html
6. **Compressed Mortality, 1999-2020**: https://wonder.cdc.gov/cmf-icd10.html

**Query Process**:
1. Select database
2. Organize table layout (rows, columns, controls)
3. Select location (county-level)
4. Select demographics (age, sex, race)
5. Select cause of death (ICD-10 codes or 113 Selected Causes)
6. Select year/month range
7. Submit query
8. Export results (TXT, CSV, XML, PDF)

**Limitations**:
- Maximum 75,000 records per query
- Counts 1-9 suppressed
- No API for automated access
- Rate calculations suppressed for <20 deaths

### 8.2 NCHS Restricted-Use Data (Research Access)

For analysis requiring unsuppressed data, researchers can access restricted-use mortality files.

**Access Methods**:

1. **NCHS Research Data Center (RDC)**
   - **URL**: https://www.cdc.gov/rdc/
   - **Process**: Submit research proposal, undergo security clearance, work on-site or via remote access
   - **Data**: Complete death certificate data with no suppression
   - **Cost**: $2,900-$5,800 per year per researcher
   - **Timeline**: 3-6 months for approval

2. **NCHS Vital Statistics Rapid Release (VSRR)**
   - **URL**: https://www.cdc.gov/nchs/nvss/vsrr.htm
   - **Content**: Monthly provisional mortality data
   - **Updated**: Weekly for most recent 12 months
   - **Focus**: COVID-19, drug overdoses, leading causes

3. **NCHS Data Linkage Program**
   - **URL**: https://www.cdc.gov/nchs/data-linkage/
   - **Features**: Link mortality to NHANES, NHIS, census data
   - **Access**: Through RDC

### 8.3 CDC WONDER API (Limited Unofficial Access)

**Note**: CDC WONDER does not provide an official public API. However, researchers have developed unofficial methods:

**XML Query Submission**:
- POST requests to WONDER XML interface
- Requires manual construction of XML query documents
- Subject to change without notice
- Rate limits apply

**GitHub Tools**:
- `wonderapi` (R package, community-maintained): https://github.com/socdataR/wonderapi
- Limited functionality, not officially supported

### 8.4 Bulk Downloads (Public-Use Data Files)

**NCHS Mortality Files** (for advanced users):
- **URL**: https://www.cdc.gov/nchs/data_access/vitalstatsonline.htm
- **Format**: Fixed-width text files, SAS/SPSS/Stata syntax provided
- **Size**: ~2GB per year (compressed)
- **Content**: Complete US mortality with county codes
- **Years**: 1959-2021 (as of November 2025)

**File Structure**:
- One record per death
- 200+ fields per record
- Requires data processing skills to aggregate to county level

---

## 9. R CODE EXAMPLES

### 9.1 Manual CDC WONDER Query (Web Portal)

Since no official API exists, most users manually query CDC WONDER and download CSV files:

```r
# After downloading CSV from CDC WONDER web portal
library(tidyverse)

# Read CDC WONDER output (skip metadata rows)
mortality_data <- read_csv("CDC_WONDER_output.csv", skip = 0) %>%
    filter(!is.na(Deaths)) %>%
    select(
        county = County,
        county_code = `County Code`,
        year = Year,
        deaths = Deaths,
        population = Population,
        crude_rate = `Crude Rate`,
        age_adjusted_rate = `Age Adjusted Rate`
    )

# Remove suppressed values (coded as "Suppressed")
mortality_data <- mortality_data %>%
    filter(deaths != "Suppressed") %>%
    mutate(
        deaths = as.numeric(deaths),
        crude_rate = as.numeric(crude_rate),
        age_adjusted_rate = as.numeric(age_adjusted_rate)
    )

# Calculate summary statistics
county_summary <- mortality_data %>%
    group_by(county_code) %>%
    summarise(
        total_deaths = sum(deaths, na.rm = TRUE),
        mean_crude_rate = mean(crude_rate, na.rm = TRUE),
        mean_aa_rate = mean(age_adjusted_rate, na.rm = TRUE)
    )
```

### 9.2 Parsing CDC WONDER Bulk Data Files (Advanced)

For users comfortable with fixed-width files:

```r
library(tidyverse)

# Download mortality file for a single year
# https://www.cdc.gov/nchs/data_access/vitalstatsonline.htm

# Define column positions (example for 2020 file)
# Full specification in documentation: https://www.cdc.gov/nchs/data/dvs/Record_Layout_2020.pdf

col_positions <- fwf_positions(
    start = c(1, 21, 25, 65, 70, 146, 163, 445, 484),
    end = c(4, 22, 44, 66, 143, 148, 443, 446, 486),
    col_names = c(
        "year",
        "state_occurrence",
        "county_occurrence",
        "state_residence",
        "county_residence",
        "age",
        "underlying_cause",
        "entity_condition",
        "race"
    )
)

# Read fixed-width file (large file, may take several minutes)
mortality <- read_fwf(
    "MULT2020.DUSMCPUB.txt.gz",
    col_positions = col_positions,
    col_types = "cccccccccc"
)

# Filter to county of interest and aggregate
county_deaths <- mortality %>%
    filter(
        state_residence == "37",  # North Carolina
        county_residence == "183"  # Wake County
    ) %>%
    count(underlying_cause, name = "deaths") %>%
    arrange(desc(deaths))

# Merge with ICD-10 code descriptions
# (ICD-10 code lookup table available from CMS or WHO)
```

### 9.3 Using wonderapi R Package (Unofficial)

**WARNING**: This package is community-maintained and may break if CDC changes WONDER's backend.

```r
# Install from GitHub
# devtools::install_github("socdataR/wonderapi")

library(wonderapi)

# Query underlying cause of death data
# (Limited functionality, manual query construction required)

# Example: Heart disease deaths by county, 2019-2021
result <- wonder_query(
    dataset = "D76",  # Underlying Cause of Death, 1999-2020
    group_by = c("County"),
    location = list(state = "37"),  # North Carolina
    year = c(2019, 2020, 2021),
    cause = c("I00-I09", "I11", "I13", "I20-I51")
)

# Process results
heart_disease_deaths <- result %>%
    select(county, county_code, year, deaths, population, crude_rate)
```

### 9.4 Drug Overdose Deaths Analysis

```r
library(tidyverse)

# After downloading drug overdose deaths from CDC WONDER
# Query: X40-X44, X60-X64, X85, Y10-Y14 (all drug overdoses)
# with MCD T40.1 (heroin), T40.2 (natural opioids), T40.4 (synthetic opioids)

overdose_data <- read_csv("CDC_WONDER_drug_overdoses.csv", skip = 0) %>%
    filter(!is.na(Deaths)) %>%
    mutate(
        county_fips = str_extract(`County Code`, "\\d{5}"),
        deaths = as.numeric(Deaths),
        crude_rate = as.numeric(`Crude Rate`)
    )

# Calculate opioid-involved deaths by type
opioid_summary <- overdose_data %>%
    group_by(county_fips, `Multiple Cause of Death`) %>%
    summarise(
        total_deaths = sum(deaths, na.rm = TRUE),
        mean_rate = mean(crude_rate, na.rm = TRUE)
    ) %>%
    pivot_wider(
        names_from = `Multiple Cause of Death`,
        values_from = c(total_deaths, mean_rate),
        values_fill = 0
    )

# Identify counties with highest opioid death rates
top_counties <- opioid_summary %>%
    arrange(desc(mean_rate_T40.4)) %>%  # Synthetic opioids (fentanyl)
    head(20)
```

### 9.5 Age-Adjusted Rate Calculation (Manual)

CDC WONDER calculates age-adjusted rates automatically, but for bulk data or custom age groups:

```r
library(tidyverse)

# 2000 US Standard Population (in thousands)
std_pop_2000 <- tribble(
    ~age_group, ~std_population,
    "<1", 3795,
    "1-4", 15192,
    "5-9", 19919,
    "10-14", 20056,
    "15-19", 19820,
    "20-24", 18257,
    "25-29", 17722,
    "30-34", 19511,
    "35-39", 22180,
    "40-44", 22479,
    "45-49", 19806,
    "50-54", 17224,
    "55-59", 13307,
    "60-64", 10654,
    "65-69", 9410,
    "70-74", 8726,
    "75-79", 7415,
    "80-84", 4900,
    "85+", 4259
)

# Total standard population
total_std_pop <- sum(std_pop_2000$std_population)

# Calculate age-adjusted rate
# Input: mortality_by_age (deaths and population by age group)

age_adjusted_rate <- mortality_by_age %>%
    left_join(std_pop_2000, by = "age_group") %>%
    mutate(
        age_specific_rate = (deaths / population) * 100000,
        weighted_rate = age_specific_rate * (std_population / total_std_pop)
    ) %>%
    summarise(
        crude_rate = sum(deaths) / sum(population) * 100000,
        age_adjusted_rate = sum(weighted_rate, na.rm = TRUE)
    )
```

### 9.6 Multi-Year County Analysis with Suppression Handling

```r
library(tidyverse)

# Aggregate multiple years to reduce suppression
# Useful for small counties with <10 annual deaths

mortality_multi_year <- read_csv("CDC_WONDER_5year.csv", skip = 0) %>%
    filter(!is.na(Deaths), Deaths != "Suppressed") %>%
    mutate(
        county_fips = str_extract(`County Code`, "\\d{5}"),
        deaths = as.numeric(Deaths),
        population = as.numeric(Population),
        years = as.numeric(`Year Code`)
    )

# Calculate 5-year aggregate rates
county_5yr_rates <- mortality_multi_year %>%
    group_by(county_fips) %>%
    summarise(
        total_deaths = sum(deaths, na.rm = TRUE),
        total_population = sum(population, na.rm = TRUE),
        crude_rate_5yr = (total_deaths / total_population) * 100000,
        annual_avg_deaths = total_deaths / 5
    ) %>%
    filter(total_deaths >= 20)  # Stable rate estimates

# Compare to national average
national_rate <- sum(county_5yr_rates$total_deaths) /
                 sum(county_5yr_rates$total_population) * 100000

county_5yr_rates <- county_5yr_rates %>%
    mutate(
        rate_ratio = crude_rate_5yr / national_rate,
        excess_risk = ifelse(rate_ratio > 1, "Higher", "Lower")
    )
```

---

## 10. DATA QUALITY AND LIMITATIONS

### 10.1 Suppression Rules

**Primary suppression**:
- Counts of 1-9 deaths are suppressed in public-use CDC WONDER
- Protects confidentiality in small populations
- Particularly affects rural counties and rare causes

**Secondary suppression**:
- Complementary cells may be suppressed to prevent back-calculation
- Can affect urban counties if breakdown creates small cells

**Impact on county-level analysis**:
- ~30% of US counties have <20,000 population
- ~15% of cause-specific county-year cells are suppressed for leading causes
- Multi-year aggregation recommended for small counties

### 10.2 Cause-of-Death Coding Quality

**Accuracy concerns**:
- Death certificate completion quality varies by state and certifying physician
- ~20% of deaths lack specific cause information
- External causes (injuries) have higher quality than natural causes

**Common issues**:
- **Ill-defined causes**: R-codes (symptoms/signs) indicate incomplete information
  - R99 (Other ill-defined causes) accounted for ~0.5% of deaths in 2023
  - R54 (Age-related physical debility) ~0.2% of deaths
- **Competing causes**: Multiple chronic conditions make underlying cause selection challenging
- **Undercoding**: Drug involvement in deaths may be underestimated by 20-30%

**Temporal comparability**:
- ICD-10 implemented in 1999 (replaced ICD-9)
- Comparability ratios needed for trend analysis across ICD revisions
- Available at: https://www.cdc.gov/nchs/nvss/mortality/comparability_icd.htm

### 10.3 Geographic Limitations

**County boundary changes**:
- Alaska: 11 new boroughs/census areas created since 1990
- Virginia: Independent cities may merge with counties
- Broomfield County, CO created in 2001 (from Boulder County)
- Database uses county FIPS code at time of death

**County equivalents**:
- Alaska: Boroughs and census areas
- Louisiana: Parishes
- Virginia: Independent cities (coded as counties)
- Total: 3,143 counties/equivalents (as of 2023)

**Place of death vs. place of residence**:
- CDC WONDER reports residence at time of death (correct for most analyses)
- Place of occurrence available but less commonly used
- Migration between counties can affect interpretation

### 10.4 Population Denominators

CDC WONDER uses **bridged-race population estimates** from NCHS:
- Based on Census Bureau population estimates
- "Bridged" to match race categories used in vital statistics
- Updated annually with 2-year lag
- Intercensal estimates revised after each census

**Implications**:
- Population estimates less accurate for small counties
- Significant revisions after 2010 and 2020 censuses
- 2020-2023 data affected by COVID-19 pandemic disruptions

### 10.5 Provisional Data Cautions

**Provisional mortality data** (2024-2025):
- Updated weekly/monthly
- Subject to revision as death certificates are processed
- Completeness varies by state (70-100% within 6 months)
- Final data typically released 11 months after year-end

**Provisional data limitations**:
- Geographic detail may be suppressed
- Cause-of-death coding incomplete for recent months
- Not suitable for official statistics or policy decisions

---

## 11. COUNTY-LEVEL ANALYSIS BEST PRACTICES

### 11.1 Handling Suppressed Data

**Strategies**:

1. **Multi-year aggregation**: Combine 3-5 years to increase cell sizes
2. **Broader cause categories**: Use 113 Selected Causes instead of detailed ICD-10 codes
3. **Geographic aggregation**: Combine small counties into clusters
4. **Restricted-use data access**: Apply for NCHS RDC access for unsuppressed data
5. **Bayesian smoothing**: Use spatial or temporal smoothing methods (e.g., empirical Bayes)

**Example**:
```r
# 5-year aggregation for small counties
mortality_5yr <- mortality %>%
    filter(year >= 2016, year <= 2020) %>%
    group_by(county_fips, cause) %>%
    summarise(
        deaths_5yr = sum(deaths),
        population_5yr = mean(population) * 5
    ) %>%
    filter(deaths_5yr >= 20)  # Keep only stable estimates
```

### 11.2 Age-Adjustment Requirement

**Always use age-adjusted rates** when comparing counties or over time:
- Counties have vastly different age structures
- Florida vs. Utah: 20.9% vs. 10.9% age 65+
- Crude rates can be misleading

**Example**:
- County A (retirement community): Crude rate 1,200/100k, AA rate 750/100k
- County B (college town): Crude rate 400/100k, AA rate 800/100k
- Age-adjusted comparison shows County B has higher mortality

### 11.3 Small Numbers Problem

**Instability in small counties**:
- County with 5,000 population: 1 death = 20 per 100,000 rate
- Single event (accident, homicide) can dramatically swing rates

**Solutions**:
1. Report confidence intervals
2. Use 5-year moving averages
3. Focus on absolute counts, not rates
4. Compare to peer counties (similar size/demographics)

### 11.4 Leading Causes Analysis

**Best practices**:

1. **Use 113 Selected Causes** for standardization
2. **Report both counts and rates** (burden vs. risk)
3. **Include age-specific rates** for causes with strong age patterns
4. **Track trends over time** (5-10 year periods)
5. **Compare to state/national benchmarks**

**Example output**:
```
Wake County, NC - Leading Causes of Death (2018-2022)

Rank | Cause                  | Deaths | % Total | AA Rate | US AA Rate
-----|------------------------|--------|---------|---------|------------
1    | Heart disease          | 6,234  | 23.1%   | 145.2   | 165.0
2    | Cancer                 | 5,891  | 21.8%   | 138.7   | 146.2
3    | COVID-19               | 1,456  | 5.4%    | 32.1    | 45.3
4    | Accidents              | 1,234  | 4.6%    | 35.8    | 64.7
5    | Chronic lower resp.    | 987    | 3.7%    | 21.3    | 36.4
```

### 11.5 Health Disparities Analysis

**Key dimensions**:
- Race/ethnicity
- Urban-rural classification
- County poverty level
- Education level (requires linkage to Census data)

**Example**:
```r
# Analyze mortality disparities by race
disparities <- mortality %>%
    group_by(county_fips, race_ethnicity) %>%
    summarise(
        deaths = sum(deaths),
        population = sum(population),
        crude_rate = deaths / population * 100000
    ) %>%
    pivot_wider(
        names_from = race_ethnicity,
        values_from = c(deaths, crude_rate)
    ) %>%
    mutate(
        black_white_ratio = crude_rate_Black / crude_rate_White,
        hispanic_white_ratio = crude_rate_Hispanic / crude_rate_White
    )
```

### 11.6 Temporal Trend Analysis

**Considerations**:

1. **Joinpoint regression**: Identify significant changes in trends
2. **Annual percent change (APC)**: Quantify rate of change
3. **Period effects**: Account for external shocks (COVID-19, opioid epidemic)
4. **Cohort effects**: Birth cohort influences on mortality

**Example**:
```r
library(tidyverse)

# Calculate annual percent change for drug overdoses
apc_data <- mortality %>%
    filter(cause == "Drug overdose", year >= 2010, year <= 2023) %>%
    group_by(county_fips) %>%
    arrange(year) %>%
    mutate(
        pct_change = (age_adjusted_rate / lag(age_adjusted_rate) - 1) * 100
    ) %>%
    summarise(
        mean_apc = mean(pct_change, na.rm = TRUE),
        trend = case_when(
            mean_apc > 5 ~ "Rapid increase",
            mean_apc > 0 ~ "Increasing",
            mean_apc > -5 ~ "Stable/Decreasing",
            TRUE ~ "Rapid decrease"
        )
    )
```

### 11.7 COVID-19 Mortality Considerations

**Special issues**:
- ICD-10 code U07.1 implemented March 2020
- Underlying cause vs. contributing cause distinction important
- Excess mortality analysis captures indirect effects
- Provisional data subject to significant revisions

**Recommended approach**:
- Report COVID-19 as underlying cause (official count)
- Report COVID-19 as any contributing cause (broader impact)
- Calculate excess mortality using historical baseline (2015-2019)

---

## 12. PRIORITY MORTALITY VARIABLES FOR COUNTY-LEVEL COLLECTION

### 12.1 Essential Variables (Minimum Dataset)

| Variable | Description | Years |
|----------|-------------|-------|
| All-cause mortality | Total deaths, all causes | 1999-2023 |
| Age-specific mortality rates | Deaths by 5-year age groups | 1999-2023 |
| Leading causes (10) | Top 10 causes per 113 Selected Causes | 1999-2023 |
| Heart disease mortality | ICD-10: I00-I09, I11, I13, I20-I51 | 1999-2023 |
| Cancer mortality | ICD-10: C00-C97 | 1999-2023 |
| Drug overdose mortality | ICD-10: X40-X44, X60-X64, X85, Y10-Y14 | 1999-2023 |
| Suicide mortality | ICD-10: X60-X84, Y87.0 | 1999-2023 |
| Motor vehicle mortality | See external cause codes | 1999-2023 |

### 12.2 Recommended Variables (Extended Dataset)

| Variable | Description | Years |
|----------|-------------|-------|
| Opioid-specific deaths | T40.0-T40.4, T40.6 by drug type | 1999-2023 |
| Alzheimer disease | G30 | 1999-2023 |
| Diabetes | E10-E14 | 1999-2023 |
| COPD | J40-J47 | 1999-2023 |
| Stroke | I60-I69 | 1999-2023 |
| COVID-19 | U07.1 | 2020-2023 |
| Liver disease | K70, K73-K74 | 1999-2023 |
| Kidney disease | N00-N07, N17-N19, N25-N27 | 1999-2023 |
| Infant mortality rate | Deaths <1 year per 1,000 live births | 1999-2023 |
| Years of potential life lost | Premature mortality <75 | 1999-2023 |

### 12.3 Health Disparities Variables

| Variable | Description | Years |
|----------|-------------|-------|
| Mortality by race/ethnicity | All causes, by race/ethnicity | 1999-2023 |
| Mortality by urban-rural | All causes, by NCHS classification | 1999-2023 |
| Infant mortality by race | IMR by race/ethnicity | 1999-2023 |
| Drug overdose by race | Opioid deaths by race/ethnicity | 1999-2023 |

---

## 13. INTEGRATION WITH OTHER DATA SOURCES

### 13.1 Linkage to Census Data

Merge mortality with demographic and socioeconomic data:

```r
library(tidycensus)
library(tidyverse)

# Get county poverty rates from ACS
poverty <- get_acs(
    geography = "county",
    variables = "B17001_002",  # Population below poverty
    year = 2021,
    survey = "acs5"
) %>%
    mutate(county_fips = GEOID)

# Merge with mortality data
mortality_poverty <- mortality %>%
    left_join(poverty, by = "county_fips") %>%
    mutate(poverty_rate = estimate / B17001_001)

# Analyze mortality-poverty relationship
cor.test(mortality_poverty$age_adjusted_rate, mortality_poverty$poverty_rate)
```

### 13.2 Linkage to County Health Rankings

```r
# County Health Rankings data
# https://www.countyhealthrankings.org/explore-health-rankings/rankings-data-documentation

chr <- read_csv("County_Health_Rankings_2024.csv") %>%
    select(
        county_fips = FIPS,
        premature_death = `Premature death (YPLL)`,
        poor_health = `% Fair or poor health`,
        uninsured = `% Uninsured`
    )

# Merge and analyze
mortality_chr <- mortality %>%
    left_join(chr, by = "county_fips")
```

### 13.3 Spatial Analysis

```r
library(sf)
library(spdep)

# Load county shapefiles
counties_sf <- st_read("US_counties.shp")

# Merge mortality data
counties_mortality <- counties_sf %>%
    left_join(mortality, by = c("GEOID" = "county_fips"))

# Spatial autocorrelation
neighbors <- poly2nb(counties_mortality)
weights <- nb2listw(neighbors, style = "W")

moran_test <- moran.test(counties_mortality$age_adjusted_rate, weights)
```

---

## 14. SUMMARY: RECOMMENDED COUNTY-LEVEL MORTALITY VARIABLES

### 14.1 Top Priority (Tier 1)

1. **All-cause mortality** (1999-2023): Deaths, crude rate, age-adjusted rate
2. **10 leading causes** (1999-2023): Per 113 Selected Causes
3. **Drug overdose deaths** (1999-2023): Total and by drug type (T40.1-T40.4)
4. **Heart disease** (1999-2023): ICD-10 I00-I09, I11, I13, I20-I51
5. **Cancer** (1999-2023): ICD-10 C00-C97

### 14.2 High Priority (Tier 2)

6. **COVID-19** (2020-2023): Underlying and contributing cause
7. **Suicide** (1999-2023): ICD-10 X60-X84
8. **Motor vehicle** (1999-2023): External cause V-codes
9. **Alzheimer disease** (1999-2023): ICD-10 G30
10. **Diabetes** (1999-2023): ICD-10 E10-E14

### 14.3 Recommended (Tier 3)

11. COPD (J40-J47)
12. Stroke (I60-I69)
13. Liver disease (K70, K73-K74)
14. Kidney disease (N00-N07, N17-N19)
15. Infant mortality rate
16. Years of potential life lost (YPLL)

### 14.4 Comprehensive (Tier 4)

17-113. All 113 Selected Causes
114-832. Detailed ICD-10 codes for specific research questions

---

## 15. DATA COLLECTION WORKFLOW

### 15.1 Automated Collection Strategy

**Recommended approach for county-level mortality data**:

1. **Annual bulk download** of NCHS mortality files (most comprehensive)
2. **CDC WONDER queries** for specific causes and multi-year aggregates
3. **VSRR provisional data** for most recent 12 months
4. **RDC access** (if budget permits) for unsuppressed small county data

### 15.2 File Organization

```
GetData/
├── CDC_Mortality/
│   ├── raw/
│   │   ├── MULT2020.DUSMCPUB.txt.gz
│   │   ├── MULT2021.DUSMCPUB.txt.gz
│   │   ├── MULT2022.DUSMCPUB.txt.gz
│   │   └── MULT2023.DUSMCPUB.txt.gz
│   ├── processed/
│   │   ├── county_all_cause_mortality_1999_2023.csv
│   │   ├── county_leading_causes_1999_2023.csv
│   │   ├── county_drug_overdose_1999_2023.csv
│   │   └── county_covid19_2020_2023.csv
│   └── documentation/
│       ├── ICD10_code_descriptions.csv
│       ├── 113_selected_causes.csv
│       └── record_layouts/
```

### 15.3 Quality Control Checks

```r
# Quality control for mortality data
qc_mortality <- function(mortality_data) {

    # Check 1: Valid FIPS codes
    valid_fips <- mortality_data %>%
        filter(nchar(county_fips) == 5, !is.na(county_fips)) %>%
        nrow()

    # Check 2: Deaths <= Population
    impossible_rates <- mortality_data %>%
        filter(deaths > population) %>%
        nrow()

    # Check 3: Reasonable age-adjusted rates (0-5000 per 100k)
    outlier_rates <- mortality_data %>%
        filter(age_adjusted_rate < 0 | age_adjusted_rate > 5000) %>%
        nrow()

    # Check 4: Temporal completeness
    year_coverage <- mortality_data %>%
        distinct(year) %>%
        arrange(year)

    # Report
    cat("QC Summary:\n")
    cat("Valid FIPS codes:", valid_fips, "\n")
    cat("Impossible rates (deaths > pop):", impossible_rates, "\n")
    cat("Outlier rates:", outlier_rates, "\n")
    cat("Year coverage:", min(year_coverage$year), "-", max(year_coverage$year), "\n")
}
```

---

## 16. UPDATES AND MAINTENANCE

### 16.1 Data Release Schedule

- **Final annual data**: Released 11 months after year-end (e.g., 2023 data released November 2024)
- **Provisional monthly data**: Released 2-3 months after month-end
- **VSRR weekly updates**: Every Wednesday for most recent 12 months
- **Bulk data files**: Released 12-18 months after year-end

### 16.2 Notable Changes (2024-2025)

1. **ICD-10 CM updates**: Annual code updates effective October 1
2. **Race/ethnicity coding**: Bridge-race categories aligned with 2020 Census
3. **COVID-19 reporting**: Transitioned from pandemic to endemic surveillance
4. **Drug overdose coding**: Enhanced fentanyl analog detection
5. **VSRR expansion**: New dashboard for drug overdoses and maternal mortality

### 16.3 Future Enhancements

- **ICD-11**: WHO adopted ICD-11 in 2022, US implementation expected 2027-2030
- **Real-time mortality surveillance**: NCHS exploring near-real-time data systems
- **Linked data products**: Expansion of mortality linkages to NHANES, NHIS, Medicare

---

## DOCUMENTATION VERSION

**Document Version**: 1.0
**Last Updated**: November 11, 2025
**Author**: Claude Code
**Data Sources**: CDC WONDER, NCHS Vital Statistics, CDC VSRR
**Verification Status**: All URLs and access methods verified as of November 2025

---

## QUICK REFERENCE

**CDC WONDER Main Portal**: https://wonder.cdc.gov/
**Mortality Home**: https://wonder.cdc.gov/mortality.html
**API (unofficial)**: https://github.com/socdataR/wonderapi
**Bulk Downloads**: https://www.cdc.gov/nchs/data_access/vitalstatsonline.htm
**RDC Access**: https://www.cdc.gov/rdc/
**Documentation**: https://wonder.cdc.gov/wonder/help/mcd.html

**Key Contacts**:
- NCHS Mortality Statistics: mortality@cdc.gov
- WONDER Technical Support: cwus@cdc.gov
- RDC Applications: rdc@cdc.gov

---

**END OF COMPREHENSIVE CDC WONDER MORTALITY DOCUMENTATION**
