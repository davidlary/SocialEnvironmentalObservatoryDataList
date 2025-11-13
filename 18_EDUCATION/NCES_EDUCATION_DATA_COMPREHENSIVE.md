# NCES Education Data - Comprehensive County-Level Documentation

## Executive Summary

The **National Center for Education Statistics (NCES)** is the primary federal entity for collecting and analyzing education data in the United States. This documentation provides complete access to county-level education variables covering K-12 schools, school districts, postsecondary institutions, educational outcomes, and workforce characteristics.

### Key Features

- **🏫 Schools & Districts**: 130,000+ public schools, 18,000+ school districts, 6,700+ private schools
- **📊 Core Variables**: Enrollment, demographics, staffing, finances, performance, facilities
- **🎓 Outcomes**: Graduation rates, test scores, achievement gaps, college readiness
- **💰 Finances**: Revenue by source, expenditures by function, per-pupil spending
- **👥 Demographics**: Student race/ethnicity, poverty (free/reduced lunch), ELL, special ed, homeless
- **📈 Time Coverage**: 1986-present (Common Core of Data); earlier for some series
- **🔑 Access**: Free, no restrictions, multiple APIs, bulk downloads, R packages
- **🌎 Geography**: School-level (geocoded), district-level (mapped to counties), county aggregation

---

## Table of Contents

1. [Data Systems & Sources](#data-systems--sources)
2. [Common Core of Data (CCD) - Public Schools](#common-core-of-data-ccd---public-schools)
3. [Private School Universe Survey (PSS)](#private-school-universe-survey-pss)
4. [EDFacts - Performance & Accountability](#edfacts---performance--accountability)
5. [School District Finance Survey (F-33)](#school-district-finance-survey-f-33)
6. [Postsecondary Education (IPEDS)](#postsecondary-education-ipeds)
7. [Stanford Education Data Archive (SEDA)](#stanford-education-data-archive-seda)
8. [County-Level Aggregation Strategies](#county-level-aggregation-strategies)
9. [Access Methods & APIs](#access-methods--apis)
10. [R Packages & Code Examples](#r-packages--code-examples)
11. [Data Quality & Limitations](#data-quality--limitations)
12. [Priority Variables for Collection](#priority-variables-for-collection)
13. [Quick Reference](#quick-reference)

---

## Data Systems & Sources

### 1. Common Core of Data (CCD)
**Universe:** All public elementary and secondary schools and school districts
**Coverage:** 130,000+ schools, 18,000+ districts, 50 states + DC, territories
**Years:** 1986-present (comprehensive); selected series to 1967
**Update Frequency:** Annual (released ~18 months after school year end)
**Restriction:** Public use, no restrictions

### 2. Private School Universe Survey (PSS)
**Universe:** All private elementary and secondary schools
**Coverage:** ~30,000-35,000 private schools (varies by year)
**Years:** Biennial 1989-2018; annual 2019-present
**Update Frequency:** Annual or biennial
**Restriction:** Public use, no restrictions

### 3. EDFacts
**Universe:** Public schools and districts (state-reported accountability data)
**Coverage:** All states required to report under ESSA
**Years:** 2006-present (varies by metric)
**Update Frequency:** Annual
**Restriction:** Public use, aggregated to protect student privacy

### 4. School District Finance Survey (F-33)
**Universe:** All school districts with fiscal autonomy (~13,000 districts)
**Coverage:** Revenue, expenditures, debt, assets
**Years:** 1992-present (comprehensive); earlier years available
**Update Frequency:** Annual (released ~18 months after fiscal year)
**Restriction:** Public use, no restrictions

### 5. Integrated Postsecondary Education Data System (IPEDS)
**Universe:** All postsecondary institutions participating in Title IV federal aid
**Coverage:** 6,700+ institutions (2- and 4-year, public and private)
**Years:** 1980-present (comprehensive); earlier years available
**Update Frequency:** Annual
**Restriction:** Public use, no restrictions

### 6. Stanford Education Data Archive (SEDA)
**Universe:** Public schools and districts with state assessment data
**Coverage:** Test score data linked to covariates, standardized across states
**Years:** 2009-2018 (version 4.1); updates planned
**Update Frequency:** Periodic research releases
**Restriction:** Public use for research, registration required

---

## Common Core of Data (CCD) - Public Schools

The CCD is the NCES annual census of all public elementary and secondary schools and school districts in the US.

### School-Level Variables (~150 variables)

#### A. Identification & Geographic
- `NCESSCH` - 12-digit NCES school ID (unique persistent identifier)
- `SEASCH` - State-assigned school ID
- `LEAID` - 7-digit NCES district ID
- `SEADIR` - State-assigned district ID
- `FIPST` - State FIPS code (2-digit)
- `STABBR` - State abbreviation
- `LEANM` - District name
- `SCH_NAME` - School name
- `LCITY` - City location
- `LSTATE` - State location
- `LZIP` - ZIP code
- `LZIP4` - ZIP+4
- `MZIP` - Mailing ZIP
- `PHONE` - School phone number
- `LATCOD` - Latitude
- `LONCOD` - Longitude
- `COUNTYCD` - County FIPS code (3-digit, state-specific)
- `CONUM` - County number
- `CONAME` - County name
- `NMCNTY` - Number of counties school serves
- `CBSA` - Core-Based Statistical Area code

#### B. School Characteristics
- `TYPE` - School type (1=Regular, 2=Special education, 3=Vocational, 4=Alternative/other)
- `STATUS` - School status (1=Open, 2=Closed, 3=Future, 4=Inactive, 5=Future, 6-8=Other)
- `ULOCALE` - Urban-centric locale code (12 categories from large city to rural remote)
- `LEVEL` - School level (1=Primary, 2=Middle, 3=High, 4=Other)
- `TITLEI` - Title I school status (1-6, indicating eligibility and participation)
- `STITLI` - Title I schoolwide status (1-9, indicating program type)
- `MAGNET` - Magnet school (1=Yes, 2=No, -1=Missing)
- `CHARTR` - Charter school (1=Yes, 2=No, -1=Missing)
- `SHARED` - Shared-time school (1=Yes, 2=No, -1=Missing)
- `GSLO` - Lowest grade (PK-12)
- `GSHI` - Highest grade (PK-12)
- `G_PK_OFFERED` - Prekindergarten offered (1=Yes, 2=No, -1=Missing)

#### C. Enrollment by Grade (~20 variables)
- `MEMBER` - Total students (October 1 count)
- `G_PK_FT` - Prekindergarten full-time enrollment
- `G_PK_PT` - Prekindergarten part-time enrollment
- `G_KG_FT` - Kindergarten full-time enrollment
- `G_KG_PT` - Kindergarten part-time enrollment
- `G_1` - Grade 1 enrollment
- `G_2` - Grade 2 enrollment
- ...
- `G_12` - Grade 12 enrollment
- `G_13` - Grade 13 enrollment (rare)
- `G_UG` - Ungraded enrollment
- `G_AE` - Adult education enrollment

#### D. Enrollment by Race/Ethnicity (~8 variables)
- `AM` - American Indian/Alaska Native students
- `AS` - Asian students
- `HI` - Hispanic students
- `BL` - Black or African American students
- `WH` - White students
- `HP` - Native Hawaiian/Pacific Islander students
- `TR` - Two or more races students
- `TOTETH` - Total students (race/ethnicity sum, for verification)

#### E. Enrollment by Gender
- `FTE` - Full-time equivalent enrollment
- `TOTFRL` - Total free and reduced-price lunch eligible (proxy for poverty)
- `FRELCH` - Free lunch eligible
- `REDLCH` - Reduced-price lunch eligible

#### F. Teachers & Staff (~10 variables)
- `FTE_TEACHERS` - Full-time equivalent teachers
- `FTE_TEACH_SEC` - FTE secondary teachers
- `FTE_TEACH_ELE` - FTE elementary teachers
- `FTE_TEACH_UG` - FTE ungraded teachers
- `AIDES` - Instructional aides (FTE)
- `GUID` - Guidance counselors (FTE)
- `LIBSPE` - Librarians/media specialists (FTE)
- `ELMGUI` - Elementary guidance counselors (FTE)
- `SECGUI` - Secondary guidance counselors (FTE)

#### G. Pupil/Teacher Ratio
- `PUPIL_TEACHER_RATIO` - Calculated as MEMBER / FTE_TEACHERS

### District-Level Variables (~200 variables)

#### A. Identification & Geographic
- `LEAID` - 7-digit NCES district ID
- `LEA_NAME` - District name
- `PHONE` - District phone
- `MAIL_ADDRESS` - Mailing address
- `MAIL_CITY`, `MAIL_STATE`, `MAIL_ZIP`, `MAIL_ZIP4`
- `LOCATION_ADDRESS` - Physical address
- `LOCATION_CITY`, `LOCATION_STATE`, `LOCATION_ZIP`
- `LATCOD`, `LONCOD` - Lat/long of district administrative office
- `COUNTY_NUMBER` - County FIPS code
- `COUNTY_NAME` - County name
- `CBSA` - Core-Based Statistical Area
- `CSA` - Combined Statistical Area

#### B. District Characteristics
- `TYPE` - District type (1-7, regular/specialized)
- `UNION` - Supervisory union number (New England states)
- `LEA_STATUS` - Operational status
- `UPDATED_STATUS` - Most recent update to operational status
- `ULOCALE` - Urban-centric locale (based on enrollment-weighted schools)
- `LOWEST_GRADE`, `HIGHEST_GRADE` - Grade span
- `CHARTER_TEXT` - Charter status description

#### C. Enrollment Counts
All grade-by-grade enrollment variables as in school-level data, district totals
- `TOTALT` - Total K-12 membership
- `PREKINDT` - Prekindergarten total
- `KINDT` - Kindergarten total
- `G01T` - Grade 1 total
- ...
- `G12T` - Grade 12 total
- `UNGRT` - Ungraded total

#### D. Enrollment by Demographics
- `AM` - American Indian/Alaska Native
- `AS` - Asian
- `HI` - Hispanic
- `BL` - Black or African American
- `WH` - White
- `HP` - Native Hawaiian/Pacific Islander
- `TR` - Two or more races

#### E. Special Populations
- `TOTFRL` - Free/reduced lunch eligible (all schools)
- `FRELCH` - Free lunch eligible
- `REDLCH` - Reduced lunch eligible
- `SPECED` - Special education students (from EDFacts)
- `LEP` - Limited English proficient students (from EDFacts)

#### F. Staff Counts (~30 variables)
- `TEACHERS` - Total teachers (FTE)
- `SUPPORT` - Support staff (FTE)
- `ADMIN` - Administrators (FTE)
- `GUIDANCE` - Guidance counselors (FTE)
- `LIBRARIANS` - Librarians (FTE)
- `INSTRUCT_COORD` - Instructional coordinators (FTE)
- `INSTRUCT_AIDES` - Instructional aides (FTE)
- `LEA_ADMIN` - District administrators (FTE)
- `SCHOOL_ADMIN` - School administrators (FTE)
- `STUDENT_SUPPORT` - Student support services staff (FTE)
- `OTHER_SUPPORT` - Other support services staff (FTE)

#### G. District Operations
- `SCH_COUNT` - Number of schools
- `SCH_REGULAR` - Number of regular schools
- `SCH_SPECIAL` - Number of special education schools
- `SCH_VOC` - Number of vocational schools
- `SCH_ALT` - Number of alternative schools
- `SCH_CLOSED` - Number of recently closed schools

---

## Private School Universe Survey (PSS)

### School-Level Variables (~130 variables)

#### A. Identification & Location
- `PPIN` - Private school unique identifier
- `SCHOOL_NAME` - School name
- `ADDRESS`, `CITY`, `STATE`, `ZIP`
- `COUNTY_FIPS` - County FIPS code
- `LATITUDE`, `LONGITUDE`
- `ULOCALE` - Urban-centric locale
- `CBSA` - Core-Based Statistical Area

#### B. School Characteristics
- `SCHOOL_TYPE` - Catholic, other religious, nonsectarian
- `RELIGIOUS_AFFILIATION` - Detailed affiliation (30+ categories)
- `LEVEL` - Elementary, secondary, combined
- `ORIENTATION` - Regular, special program emphasis, special ed, alternative, early childhood
- `GSLO`, `GSHI` - Lowest and highest grades
- `HOURS_PER_DAY` - Instructional hours
- `DAYS_PER_YEAR` - Days in school year

#### C. Enrollment
- `TOTAL_STUDENTS` - Total K-12 enrollment
- `PK_ENROLL` - Prekindergarten
- `KG_ENROLL` - Kindergarten
- `G01_ENROLL` - Grade 1
- ...
- `G12_ENROLL` - Grade 12
- `UG_ENROLL` - Ungraded

#### D. Demographics
- `AM` - American Indian/Alaska Native
- `AS` - Asian
- `HI` - Hispanic
- `BL` - Black or African American
- `WH` - White
- `HP` - Native Hawaiian/Pacific Islander
- `TR` - Two or more races

#### E. Teachers & Staff
- `NUM_TEACHERS` - Number of teachers (FTE)
- `PUPIL_TEACHER_RATIO`
- `LIBRARIANS`, `GUIDANCE`, `AIDES`

#### F. Tuition & Finances
- `TUITION_1` - Elementary tuition (median or typical)
- `TUITION_2` - Secondary tuition
- `FINANCIAL_AID_AMT` - Total financial aid awarded
- `PERCENT_RECEIVING_AID` - Percent students receiving aid

---

## EDFacts - Performance & Accountability

EDFacts collects state-reported data on assessments, accountability, and performance under the Every Student Succeeds Act (ESSA).

### Key Variable Categories (~80 EDFacts files)

#### A. Assessment Participation & Performance
**Files:** Assessment Participation, Assessment Performance

**Breakdowns:**
- Grade level (3-8, high school)
- Subject (mathematics, reading/language arts, science)
- Subgroups:
  - Race/ethnicity (7 categories)
  - Economically disadvantaged (Y/N)
  - Students with disabilities (Y/N)
  - English learners (Y/N)
  - Gender (M/F)
  - Homeless (Y/N)
  - Foster care (Y/N)
  - Military-connected (Y/N)

**Variables (per file × subject × grade × subgroup):**
- Number tested
- Number proficient or above
- Percent proficient or above
- Number at each achievement level (1-5)

**Coverage:** 2006-present
**Aggregation:** School and district level

#### B. Graduation Rates
**Files:** Four-year adjusted cohort graduation rate, Five-year ACGR, Six-year ACGR

**Variables:**
- Cohort count
- Number graduated
- Graduation rate
- Breakdowns by all subgroups above

**Years:** 2011-present (ACGR became mandatory)
**Note:** Prior to ACGR, states used varied methods

#### C. Chronic Absenteeism
**File:** Chronic Absenteeism

**Variables:**
- Number of students
- Number chronically absent (typically ≥10% days missed)
- Chronic absenteeism rate
- Breakdowns by subgroups

**Years:** 2016-present

#### D. Discipline
**Files:** Disciplinary removals, Corporal punishment, Restraint and seclusion

**Variables:**
- Number of students with incidents
- Number of incidents
- Rates by subgroup

**Years:** Varies by file, mostly 2006-present

#### E. Teachers
**Files:** Teacher experience, Teacher qualifications

**Variables:**
- Number of teachers
- Number of inexperienced teachers (<3 years)
- Number teaching out of field
- Breakdowns by high-poverty/low-poverty schools

**Years:** 2011-present

---

## School District Finance Survey (F-33)

Comprehensive revenue, expenditure, and debt data for all school districts with fiscal autonomy (~13,000 districts).

### Revenue Variables (~40 variables)

#### A. Total Revenue
- `TOTALREV` - Total revenue from all sources
- `TFEDREV` - Total federal revenue
- `TSTREV` - Total state revenue
- `TLOCREV` - Total local revenue

#### B. Federal Revenue by Program
- `FEDREV` - Total federal revenue (detailed)
- `C01` - Title I (ESEA)
- `C03` - Child nutrition
- `C06` - IDEA Part B (special education)
- `C09` - Career and technical education
- `C10` - Impact aid
- `C14` - Other federal revenue

#### C. State Revenue by Source
- `TSTREV` - Total state revenue
- `C23` - General formula assistance
- `C25` - Special education
- `C27` - Transportation
- `C28` - Staff compensation
- `C29` - Capital outlay and debt
- `C30` - Other state revenue

#### D. Local Revenue by Source
- `TLOCREV` - Total local revenue
- `T06` - Local taxes
- `A11` - Local property taxes
- `A12` - Local sales taxes
- `A13` - Other local taxes
- `T09` - Parent government contributions
- `T15` - Other local revenues

### Expenditure Variables (~60 variables)

#### A. Current Spending by Function
- `TCURELSC` - Total current expenditures for elementary/secondary education
- `V33` - Instruction
- `V34` - Support services
- `V35` - Student support services
- `V36` - Instructional staff support
- `V37` - General administration
- `V38` - School administration
- `V39` - Operations and maintenance
- `V40` - Student transportation
- `V41` - Other support services
- `V44` - Food services
- `V45` - Enterprise operations

#### B. Current Spending by Object
- `Z32` - Salaries and wages
- `Z33` - Employee benefits
- `Z34` - Purchased services
- `Z35` - Tuition and other local education agencies
- `Z36` - Supplies
- `Z37` - Property (equipment, land)
- `Z38` - Other

#### C. Capital Outlay
- `TCAPOUT` - Total capital outlay
- `K06` - Construction
- `K10` - Instructional equipment
- `K12` - Other equipment
- `K13` - Land acquisition

#### D. Debt Service
- `I86` - Interest on debt
- `I88` - Principal on debt

#### E. Per-Pupil Calculations
- `TOTALEXP` - Total expenditures
- `CURRENTEXP_PP` - Current expenditures per pupil
- `INSTRUCTION_PP` - Instruction expenditures per pupil
- `SUPPORT_PP` - Support services expenditures per pupil

### Debt & Assets (~20 variables)

- `LONGTERM_DEBT` - Long-term debt outstanding
- `SHORTTERM_DEBT` - Short-term debt outstanding
- `CASH_SECURITIES` - Cash and investments
- `TOTAL_ASSETS` - Total assets

### Staffing & Enrollment (for per-pupil calculations)
- `MEMBER` - Student membership (October 1)
- `V11` - Full-time equivalent staff count

---

## Postsecondary Education (IPEDS)

IPEDS collects data from all postsecondary institutions participating in Title IV federal student aid programs.

### Institution-Level Variables (~1,000 variables across multiple files)

#### A. Institutional Characteristics
**File:** HD (Directory Information)

- `UNITID` - Unique institution identifier
- `INSTNM` - Institution name
- `ADDR`, `CITY`, `STABBR`, `ZIP`, `FIPS` - Address and location
- `OBEREG` - Census region
- `COUNTYNM`, `COUNTYCD` - County name and FIPS
- `LONGITUD`, `LATITUDE`
- `SECTOR` - Institutional sector (public 4-year, private nonprofit 4-year, for-profit 2-year, etc.)
- `ICLEVEL` - Level of institution (4-year, 2-year, <2-year)
- `CONTROL` - Control (public, private nonprofit, private for-profit)
- `HLOFFER` - Highest degree offered
- `UGOFFER`, `GROFFER` - Undergraduate/graduate offering
- `HDEGOFR1` - Highest degree offered (detailed)
- `DEGGRANT` - Degree-granting status
- `HBCU` - Historically Black College/University
- `HOSPITAL` - Institution has hospital
- `MEDICAL` - Grants medical degree
- `TRIBAL` - Tribal college
- `LOCALE` - Degree of urbanization
- `OPENPUBL` - Open admissions policy
- `ACT` - Status of institution (active, inactive)
- `NEWID` - Institution ID to which merged
- `DEATHYR` - Year institution closed
- `CLOSEDAT` - Date institution closed
- `CYACTIVE` - Institution active in current year
- `CARNEGIE` - Carnegie classification
- `LANDGRNT` - Land-grant institution
- `INSTSIZE` - Institution size category
- `F1SYSTYP` - Multi or single institution or system
- `F1SYSNAM` - Name of system

#### B. Admissions & Test Scores
**File:** ADM (Admissions)

- `APPLCN`, `APPLCNM`, `APPLCNW` - Applications received (total, men, women)
- `ADMSSN`, `ADMSSNM`, `ADMSSNW` - Admissions total (total, men, women)
- `ENRLT`, `ENRLM`, `ENRLW` - Enrolled total (total, men, women)
- `SATNUM` - Number of first-time students submitting SAT
- `SATPCT` - Percent submitting SAT
- `ACTNUM`, `ACTPCT` - ACT submissions
- `SATVR25`, `SATVR75` - SAT verbal 25th/75th percentile
- `SATMT25`, `SATMT75` - SAT math 25th/75th percentile
- `SATWR25`, `SATWR75` - SAT writing 25th/75th percentile
- `ACTCM25`, `ACTCM75` - ACT composite 25th/75th percentile
- `ACTEN25`, `ACTEN75` - ACT English 25th/75th percentile
- `ACTMT25`, `ACTMT75` - ACT math 25th/75th percentile

#### C. Enrollment
**File:** EF (Fall Enrollment)

- `EFDETOT` - Grand total, all students
- By level: undergraduate, graduate, first-professional
- By attendance status: full-time, part-time
- By gender: men, women
- By race/ethnicity: 9 categories
- By age: 7 age groups
- By residence: in-state, out-of-state, foreign

**File:** EFFY (12-month enrollment)
- Total unduplicated headcount over 12 months
- By instructional activity (credit, non-credit)

#### D. Completions (Degrees Awarded)
**File:** C (Completions)

- `CTOTALT` - Grand total awards/degrees conferred
- By award level:
  - `AWLEVEL` - Certificate/diploma, associate, bachelor, master, doctoral, professional
- By CIP code (Classification of Instructional Programs):
  - 2-digit: 50 broad fields
  - 4-digit: 350+ intermediate fields
  - 6-digit: 2,000+ detailed programs
- By race/ethnicity and gender (for each program × level)

**Example CIP codes:**
- 01 - Agriculture
- 09 - Communication
- 11 - Computer and Information Sciences
- 13 - Education
- 14 - Engineering
- 26 - Biological/Biomedical Sciences
- 45 - Social Sciences
- 51 - Health Professions
- 52 - Business

#### E. Student Financial Aid
**File:** SFA (Student Financial Aid)

- `SCUGFFN` - Number of undergrads receiving federal grant aid
- `SCFA2` - Total amount of federal grant aid
- `SCUGRF` - Undergrads receiving institutional grants
- `GIS4` - Institutional grant aid amount
- `SCUGLOAN` - Undergrads receiving federal loans
- `LOAN4` - Total federal loan amount
- `NPIST2` - Net price (cost minus grant aid) for income quintiles 1-5

#### F. Graduation Rates
**File:** GR (Graduation Rates)

- `CHRTSTAT` - Cohort status (full-time first-time cohort)
- `GRTYPE` - Graduation rate type
- `GRRACE` - Race/ethnicity of cohort
- `GR150RT` - Graduation rate at 150% of normal time (6 years for bachelor's, 3 years for associate)
- `GR100RT` - 100% of normal time
- `GR200RT` - 200% of normal time
- Breakdowns by gender, race/ethnicity, Pell status

#### G. Retention Rates
**File:** EF (Fall Enrollment)

- `RET_PCF` - Full-time retention rate (% returning year 2)
- `RET_PCP` - Part-time retention rate

#### H. Finance
**File:** F (Finance)

For public institutions:
- `F1C01` - Total revenues
- `F1C02` - Tuition and fees
- `F1C03` - Federal appropriations
- `F1C04` - State appropriations
- `F1C05` - Local appropriations
- `F1C06` - Federal grants and contracts
- `F1C07` - State grants and contracts
- `F1C08` - Local grants and contracts
- `F1C09` - Private gifts, grants, contracts
- `F1C10` - Investment return
- `F1C11` - Other revenues
- `F1D01` - Total expenses
- `F1D02` - Instruction
- `F1D03` - Research
- `F1D04` - Public service
- `F1D05` - Academic support
- `F1D06` - Student services
- `F1D07` - Institutional support
- `F1D08` - Auxiliary enterprises
- `F1D09` - Net grant aid to students
- `F1D10` - Other expenses

For private institutions: Similar structure with FASB accounting categories

#### I. Human Resources
**File:** S (Staff)

- Instructional staff: by employment status (full-time, part-time), by rank (professor, associate, assistant, instructor, lecturer)
- Non-instructional staff: by occupational category (25 categories)
- Salaries: average/median by rank, gender, contract length
- Benefits: total fringe benefits expenditures

---

## Stanford Education Data Archive (SEDA)

SEDA harmonizes state assessment data to enable cross-state and cross-district comparisons of student achievement and achievement gaps.

### Key Features

- **Standardized Test Scores**: Mean scale scores in math and reading/language arts standardized to the National Assessment of Educational Progress (NAEP) scale
- **Achievement Gaps**: Black-white, Hispanic-white, female-male, economically disadvantaged gaps
- **Growth**: Learning rates (grades of growth per year)
- **Cohorts**: Grade 3-8 cohort means
- **Time:** 2009-2018 (version 4.1)

### District-Level Variables (~50 variables)

#### A. Test Score Levels (Grade × Subject)
- `cs_mn_avg_ol` - Average standardized test score (all students)
- `cs_mn_grd_03` - Grade 3 mean score
- ...
- `cs_mn_grd_08` - Grade 8 mean score
- By subject: `_rdg` (reading), `_mth` (math)

#### B. Test Score Gaps
- `cs_mn_bw_ol` - Black-white achievement gap (all grades)
- `cs_mn_hw_ol` - Hispanic-white achievement gap
- `cs_mn_np_ol` - Not economically disadvantaged - economically disadvantaged gap
- `cs_mn_mf_ol` - Male-female achievement gap (negative = female advantage)

#### C. Learning Rates (Growth)
- `gcs_mn_avg_ol` - Average learning rate (grades of growth per year, all students)
- `gcs_mn_bw_ol` - Black-white learning rate gap
- `gcs_mn_hw_ol` - Hispanic-white learning rate gap
- `gcs_mn_np_ol` - Not poor - poor learning rate gap

#### D. Sociodemographic Covariates (linked from other sources)
- Percent of students by race/ethnicity
- Percent economically disadvantaged
- Per-pupil expenditures
- Pupil-teacher ratio
- Median household income (from ACS)
- Adult education levels (from ACS)
- Unemployment rate (from BLS)

#### E. Geographic & Crosswalk
- `sedalea` - SEDA district ID
- `leaidC` - NCES district ID (for crosswalk to other NCES data)
- `stateabb` - State abbreviation
- `county_name` - County name(s)
- `county_fips` - County FIPS code(s) (semicolon-separated if multi-county)

### School-Level Variables
SEDA 4.1 includes school-level data with similar structure to district level.

---

## County-Level Aggregation Strategies

Most NCES data are at the **school** or **school district** level. To aggregate to **county** level:

### Strategy 1: Direct County Assignment (Schools & Districts)
Many schools and districts are coded with county FIPS in CCD and PSS.

**Steps:**
1. Filter to target school year
2. Group by `FIPST` (state FIPS) and `COUNTYCD` or `COUNTY_FIPS`
3. Aggregate:
   - **Counts**: Sum (e.g., total students = sum of all school enrollments in county)
   - **Means**: Enrollment-weighted (e.g., county mean pupil-teacher ratio)
   - **Compositions**: Sum numerator and denominator separately (e.g., % free lunch = sum(TOTFRL) / sum(MEMBER))

**Example:**
```r
county_enrollment <- ccd_schools %>%
  filter(!is.na(COUNTYCD), STATUS == "Open") %>%
  mutate(county_fips = paste0(FIPST, str_pad(COUNTYCD, 3, pad = "0"))) %>%
  group_by(county_fips) %>%
  summarise(
    schools = n(),
    total_students = sum(MEMBER, na.rm = TRUE),
    pct_free_lunch = sum(TOTFRL, na.rm = TRUE) / sum(MEMBER, na.rm = TRUE) * 100,
    pct_black = sum(BL, na.rm = TRUE) / sum(MEMBER, na.rm = TRUE) * 100,
    mean_ptr = weighted.mean(PUPIL_TEACHER_RATIO, w = MEMBER, na.rm = TRUE)
  )
```

### Strategy 2: Geocoded Aggregation (Schools with Lat/Long)
For more precise county assignment or when county code is missing:

**Steps:**
1. Use latitude/longitude to spatially join schools to county polygons
2. Requires spatial data (e.g., `tigris` package for county boundaries)
3. Aggregate as in Strategy 1

**Example:**
```r
library(sf)
library(tigris)

# Get county boundaries
counties <- counties(cb = TRUE, year = 2022)

# Convert schools to spatial points
schools_sf <- ccd_schools %>%
  filter(!is.na(LATCOD), !is.na(LONCOD)) %>%
  st_as_sf(coords = c("LONCOD", "LATCOD"), crs = 4269)

# Spatial join
schools_with_county <- st_join(schools_sf, counties)

# Aggregate
county_data <- schools_with_county %>%
  st_drop_geometry() %>%
  group_by(GEOID) %>%
  summarise(...)
```

### Strategy 3: District-to-County Crosswalk
Some districts span multiple counties. Use enrollment-weighted allocation or assign to county with plurality of enrollment.

**NCES provides:** Geographic Edge files linking districts to counties with enrollment shares.

**Example:**
```r
# Load district-county crosswalk (from NCES Edge files)
dist_county_xwalk <- read_csv("path/to/edge_file.csv")

# Join district-level data to crosswalk
district_data_by_county <- district_finance %>%
  left_join(dist_county_xwalk, by = "LEAID") %>%
  mutate(
    revenue_allocated = TOTALREV * enrollment_share,
    exp_allocated = TOTALEXP * enrollment_share
  ) %>%
  group_by(county_fips) %>%
  summarise(
    total_revenue = sum(revenue_allocated, na.rm = TRUE),
    total_expenditure = sum(exp_allocated, na.rm = TRUE)
  )
```

### Strategy 4: IPEDS County Aggregation
IPEDS institutions are already county-coded.

**Steps:**
1. Filter to relevant institution types (e.g., 2-year colleges, 4-year colleges)
2. Group by `COUNTYCD` or derived county FIPS
3. Aggregate:
   - Number of institutions
   - Total enrollment
   - Total completions by field
   - Average/median tuition, test scores, graduation rates

---

## Access Methods & APIs

### 1. NCES Data Explorer (Primary Portal)
**URL:** https://nces.ed.gov/ccd/elsi/

**Features:**
- Interactive query builder
- Select variables, filters, aggregations
- Export to CSV, Excel, SAS
- No API key required

**Coverage:** CCD (schools, districts, membership, staff), EDFacts (performance, accountability)

**Use Case:** Exploratory analysis, custom queries, one-time exports

### 2. NCES Data Downloads (Bulk Files)
**URL:** https://nces.ed.gov/ccd/files.asp

**Files:**
- CCD: Separate files for schools, districts, membership, staff (annual)
- PSS: School and data files (biennial/annual)
- F-33: District finance (annual)
- IPEDS: Annual data files (multiple tables per year)

**Format:** CSV, SAS, SPSS, Stata

**Access:** Direct download, no registration

### 3. Urban Institute Education Data Portal API
**URL:** https://educationdata.urban.org/documentation/

**Features:**
- RESTful API for NCES data (CCD, IPEDS, some EDFacts)
- JSON responses
- Endpoints by data category (schools, districts, college-university)
- Query parameters for filtering, sorting, pagination
- No API key required
- **Rate Limit:** 1,000 requests/day per IP

**Example Endpoints:**
- Schools: `GET https://educationdata.urban.org/api/v1/schools/ccd/directory/{year}/`
- Districts: `GET https://educationdata.urban.org/api/v1/schools/ccd/district/{year}/`
- IPEDS: `GET https://educationdata.urban.org/api/v1/college-university/ipeds/directory/{year}/`

**Query Example:**
```
GET https://educationdata.urban.org/api/v1/schools/ccd/directory/2021/?fips=6&county_code=075
```
(Returns all schools in San Francisco County, CA in 2021)

### 4. Census Bureau Education APIs
The Census Bureau American Community Survey (ACS) provides county-level education attainment data (not school-level).

**URL:** https://api.census.gov/data.html

**Variables:**
- `B15003_*` - Educational attainment (detailed)
- `S1501_*` - Educational attainment (summary)
- `B14001_*` - School enrollment by level

**Access:** Requires free API key from https://api.census.gov/data/key_signup.html

### 5. SEDA Data Access
**URL:** https://edopportunity.org/get-the-data/

**Access:**
- Free registration required
- Bulk download (CSV, Stata, R data files)
- No API

**Files:**
- District-level: `seda_geodist_long_4.1.csv`
- School-level: `seda_school_long_4.1.csv`
- Crosswalks: `seda_cov_geodist_4.1.csv`

---

## R Packages & Code Examples

### 1. `educationdata` Package (Urban Institute)

**Installation:**
```r
install.packages("educationdata")
library(educationdata)
```

**Get all schools in a state for a given year:**
```r
# All schools in Iowa, 2021
iowa_schools_2021 <- get_education_data(
  level = "schools",
  source = "ccd",
  topic = "directory",
  filters = list(year = 2021, fips = 19)
)

# View structure
glimpse(iowa_schools_2021)
```

**Get enrollment by race/ethnicity:**
```r
iowa_enrollment <- get_education_data(
  level = "schools",
  source = "ccd",
  topic = "enrollment",
  subtopic = list("race"),
  filters = list(year = 2021, fips = 19)
)
```

**Get district finance data:**
```r
# All districts, 2019 (most recent available)
district_finance <- get_education_data(
  level = "school-districts",
  source = "ccd",
  topic = "finance",
  filters = list(year = 2019)
)

# Per-pupil spending
district_spending <- district_finance %>%
  select(leaid, year, state_location, name,
         totalrev, totalexp, enroll,
         tfedrev, tstrev, tlocrev) %>%
  mutate(
    exp_per_pupil = totalexp / enroll,
    fed_pct = tfedrev / totalrev * 100,
    state_pct = tstrev / totalrev * 100,
    local_pct = tlocrev / totalrev * 100
  )
```

**Get IPEDS data (colleges):**
```r
# All 4-year colleges, 2021
colleges_2021 <- get_education_data(
  level = "college-university",
  source = "ipeds",
  topic = "directory",
  filters = list(year = 2021, inst_level = 1)  # 1 = 4-year
)

# Enrollment by race/ethnicity
college_enrollment <- get_education_data(
  level = "college-university",
  source = "ipeds",
  topic = "enrollment-full-time-equivalent",
  filters = list(year = 2021)
)
```

### 2. Direct Download & Processing

**Download CCD School Directory:**
```r
library(tidyverse)

# URL for 2021-22 school year
url <- "https://nces.ed.gov/ccd/Data/zip/ccd_sch_029_2122_w_0a_091422.zip"

# Download and unzip
temp <- tempfile()
download.file(url, temp)
ccd_schools <- read_csv(unz(temp, "ccd_sch_029_2122_w_0a_091422.csv"))
unlink(temp)
```

**Aggregate to county level:**
```r
county_schools <- ccd_schools %>%
  filter(SCH_STATUS_TEXT == "Open") %>%
  mutate(
    county_fips = paste0(str_pad(FIPST, 2, pad = "0"),
                         str_pad(COUNTYCD, 3, pad = "0"))
  ) %>%
  group_by(county_fips, ST) %>%
  summarise(
    num_schools = n(),
    total_students = sum(MEMBER, na.rm = TRUE),
    num_charter = sum(CHARTR == 1, na.rm = TRUE),
    pct_charter = num_charter / num_schools * 100,
    num_title1 = sum(TITLEI %in% c(1, 3, 5, 7), na.rm = TRUE),
    pct_frl = sum(TOTFRL, na.rm = TRUE) / sum(MEMBER, na.rm = TRUE) * 100,
    pct_black = sum(BL, na.rm = TRUE) / sum(MEMBER, na.rm = TRUE) * 100,
    pct_hispanic = sum(HI, na.rm = TRUE) / sum(MEMBER, na.rm = TRUE) * 100,
    pct_white = sum(WH, na.rm = TRUE) / sum(MEMBER, na.rm = TRUE) * 100,
    mean_ptr = weighted.mean(PUPIL_TEACHER_RATIO, w = MEMBER, na.rm = TRUE),
    .groups = "drop"
  )
```

### 3. SEDA Data Processing

**Load SEDA district data:**
```r
# Download from https://edopportunity.org/get-the-data/
# Assuming file is in working directory

seda_districts <- read_csv("seda_geodist_long_4.1.csv")

# Average test scores by district, 2018
seda_2018 <- seda_districts %>%
  filter(year == 2018, grade == "all") %>%
  select(
    sedalea, leaidC, leaname, stateabb,
    subject,
    cs_mn_all,      # Mean test score (all students)
    cs_mn_wht,      # Mean for white students
    cs_mn_blk,      # Mean for Black students
    cs_mn_hsp,      # Mean for Hispanic students
    cs_mn_asn,      # Mean for Asian students
    cs_mn_ecd,      # Economically disadvantaged
    cs_mn_ned,      # Not economically disadvantaged
    gcs_mn_all      # Learning rate (growth)
  ) %>%
  pivot_wider(names_from = subject, values_from = c(cs_mn_all, gcs_mn_all))

# Calculate achievement gaps
seda_gaps <- seda_districts %>%
  filter(year == 2018, grade == "all") %>%
  select(sedalea, leaname, stateabb, subject,
         cs_mn_bw, cs_mn_hw, cs_mn_np, cs_mn_mf) %>%
  pivot_wider(names_from = subject, values_from = cs_mn_bw:cs_mn_mf)
```

**Link SEDA to county FIPS:**
```r
# SEDA provides county name(s); need to map to FIPS
# Use tidycensus fips_codes or tigris counties()

library(tidycensus)
data("fips_codes")

county_fips_lookup <- fips_codes %>%
  mutate(county_fips = paste0(state_code, county_code)) %>%
  select(state_abb = state, county_name = county, county_fips)

# SEDA county_fips field may have multiple semicolon-separated values
# For simplicity, assign to first county or handle multi-county districts
seda_with_fips <- seda_2018 %>%
  mutate(
    county_fips_first = str_split(county_fips, ";") %>% map_chr(1)
  )
```

### 4. IPEDS Data Processing

**Download IPEDS directory file:**
```r
# IPEDS files are posted annually at https://nces.ed.gov/ipeds/datacenter/DataFiles.aspx

# Example: 2021 directory
url_ipeds <- "https://nces.ed.gov/ipeds/datacenter/data/HD2021.zip"
temp <- tempfile()
download.file(url_ipeds, temp)
ipeds_hd <- read_csv(unz(temp, "hd2021.csv"))
unlink(temp)

# Aggregate to county level
county_colleges <- ipeds_hd %>%
  filter(CYACTIVE == 1) %>%  # Active institutions
  group_by(COUNTYCD, STABBR) %>%
  summarise(
    num_institutions = n(),
    num_public = sum(CONTROL == 1),
    num_private_np = sum(CONTROL == 2),
    num_private_fp = sum(CONTROL == 3),
    num_4year = sum(ICLEVEL == 1),
    num_2year = sum(ICLEVEL == 2),
    .groups = "drop"
  )
```

**Get enrollment and completion data:**
```r
# Enrollment (EF file)
url_ef <- "https://nces.ed.gov/ipeds/datacenter/data/EF2021A.zip"
temp <- tempfile()
download.file(url_ef, temp)
ipeds_ef <- read_csv(unz(temp, "ef2021a.csv"))
unlink(temp)

# County total enrollment
county_enroll <- ipeds_hd %>%
  select(UNITID, COUNTYCD, STABBR) %>%
  left_join(ipeds_ef %>% filter(EFALEVEL == 1), by = "UNITID") %>%  # Undergrad
  group_by(COUNTYCD, STABBR) %>%
  summarise(
    undergrad_total = sum(EFDETOT, na.rm = TRUE),
    .groups = "drop"
  )
```

---

## Data Quality & Limitations

### Common Core of Data (CCD)

**Strengths:**
- Comprehensive universe (all public schools and districts)
- Long time series (1986-present for comprehensive data)
- Consistent definitions across states
- High response rates (mandatory reporting)

**Limitations:**
- **Lag time**: Data released 18-24 months after school year (e.g., 2021-22 data released September 2023)
- **Missing data**: Some states/districts fail to report certain variables
- **Free/reduced lunch**: No longer universally collected post-2014 due to Community Eligibility Provision (universal free meals in high-poverty schools), making poverty proxy inconsistent
- **County assignment**: ~5% of schools missing county code; requires geocoding
- **Charter school reporting**: Varies by state (some report charters as separate LEAs, others as schools within districts)

### EDFacts

**Strengths:**
- Accountability and performance data not available in CCD
- Detailed subgroup breakdowns
- Aligned with federal ESSA requirements

**Limitations:**
- **Suppression**: Small cell sizes suppressed to protect student privacy (typically n<10)
- **State variation**: Assessment difficulty varies by state (not comparable across states without linking to NAEP, as SEDA does)
- **Chronic absenteeism**: Definition varies slightly by state
- **Graduation rates**: Cohort tracking methods improved over time; pre-2011 data less reliable

### School District Finance (F-33)

**Strengths:**
- Comprehensive revenue and expenditure detail
- Standardized accounting (NCES Financial Accounting for Local and State School Systems)
- Long time series

**Limitations:**
- **Fiscal autonomy**: Only ~13,000 of 18,000 school districts are fiscally independent (others are components of larger governmental entities)
- **Lag time**: 18-24 months
- **Charter schools**: Financial reporting varies; charters may not be captured consistently
- **Capital spending**: Lumpy across years (large construction projects)

### Private School Universe Survey (PSS)

**Strengths:**
- Only comprehensive source on private schools
- Includes tuition and financial aid

**Limitations:**
- **Response rate**: 80-90% (lower than CCD because private schools are not required to respond)
- **Biennial until 2019**: Now annual, but historical data are every-other-year
- **Limited outcomes data**: No test scores, graduation rates, etc.
- **Financial data**: Less detailed than IPEDS for postsecondary or F-33 for districts

### IPEDS

**Strengths:**
- Mandatory for Title IV institutions (comprehensive coverage)
- Extensive variables across multiple domains
- Includes restricted-access student-level transcript data (but not public)

**Limitations:**
- **Non-Title-IV institutions**: Not included (e.g., some military academies, specialized institutions)
- **Aggregation**: Institution-level only (no student-level microdata in public files)
- **Part-time students**: Completion and retention rates focus on full-time first-time students
- **For-profit sector**: High volatility (many closures post-2010)

### SEDA

**Strengths:**
- Cross-state comparability (linked to NAEP scale)
- Achievement gaps directly calculated
- Linked to sociodemographic covariates
- Growth/learning rates (value-added approach)

**Limitations:**
- **Coverage**: Only districts and schools with state testing data (excludes private, charters in some states)
- **Time period**: 2009-2018 (version 4.1); not updated in real-time
- **State variation**: Some states missing certain grades or years
- **Linking**: NAEP linking assumptions; small errors possible

---

## Data Suppression & Small Numbers

### General Rules:
- **CCD/EDFacts**: Values <10 often suppressed (varies by variable)
- **Assessment data**: Small subgroup counts (n<10 or n<20) suppressed
- **Graduation rates**: Cohorts <20 may be suppressed
- **Strategies**:
  - Aggregate across years (e.g., 3-year or 5-year averages)
  - Aggregate grades (e.g., elementary = 1-5, middle = 6-8)
  - Report as ranges or "flag" low-reliability estimates

---

## Priority Variables for Collection

For a **county-level dataset**, the following are highest-priority education variables:

### Tier 1: Core Enrollment & Demographics (CCD)
1. **Total public school enrollment** (K-12)
2. **Percent economically disadvantaged** (free/reduced lunch or alternative poverty measure)
3. **Racial/ethnic composition** (% White, Black, Hispanic, Asian, other)
4. **Number of public schools**
5. **Number of school districts**
6. **Pupil-teacher ratio** (enrollment-weighted mean)

### Tier 2: Performance & Outcomes (EDFacts, SEDA)
7. **High school graduation rate** (4-year ACGR)
8. **Chronic absenteeism rate**
9. **Mean standardized test scores** (math and reading, if using SEDA)
10. **Achievement gaps** (Black-white, Hispanic-white, economically disadvantaged)

### Tier 3: Finance (F-33)
11. **Per-pupil expenditures** (current spending)
12. **Instruction expenditures per pupil**
13. **Local revenue as % of total** (measure of local tax base/effort)
14. **State revenue as % of total**
15. **Federal revenue as % of total**

### Tier 4: Teachers (CCD, EDFacts)
16. **Teacher FTE per 1,000 students**
17. **Percent of teachers with <3 years experience** (from EDFacts)
18. **Average teacher salary** (if available at district level)

### Tier 5: Special Populations (CCD, EDFacts)
19. **Percent of students with disabilities**
20. **Percent English learners**
21. **Percent homeless students**

### Tier 6: Postsecondary (IPEDS)
22. **Number of colleges/universities**
23. **Total college enrollment** (undergrad + grad)
24. **College completion rate** (150% time)
25. **Percent of adults with bachelor's degree or higher** (from ACS, not NCES)

### Tier 7: Private Schools (PSS)
26. **Number of private schools**
27. **Private school enrollment**

---

## Quick Reference

### Key URLs

| Resource | URL |
|----------|-----|
| **NCES Home** | https://nces.ed.gov |
| **CCD Data** | https://nces.ed.gov/ccd/ |
| **NCES Data Explorer** | https://nces.ed.gov/ccd/elsi/ |
| **CCD Downloads** | https://nces.ed.gov/ccd/files.asp |
| **IPEDS Data Center** | https://nces.ed.gov/ipeds/datacenter/ |
| **EDFacts Data** | https://www2.ed.gov/about/inits/ed/edfacts/data-files/index.html |
| **PSS Data** | https://nces.ed.gov/surveys/pss/ |
| **Urban Inst. API** | https://educationdata.urban.org/documentation/ |
| **SEDA** | https://edopportunity.org |
| **Census Education** | https://www.census.gov/topics/education.html |

### Key R Packages

| Package | Purpose | Installation |
|---------|---------|--------------|
| `educationdata` | Access Urban Institute Education Data API | `install.packages("educationdata")` |
| `tidycensus` | Census ACS education attainment | `install.packages("tidycensus")` |
| `tigris` | County shapefiles for spatial joins | `install.packages("tigris")` |
| `sf` | Spatial data operations | `install.packages("sf")` |

### File Naming Conventions (CCD)

CCD files follow the pattern: `ccd_[type]_[sequence]_[year]_[version]_[date].csv`

- `type`: `sch` (school), `lea` (district)
- `sequence`: 3-digit file type code
  - `029`: School directory
  - `052`: School membership (enrollment)
  - `059`: District directory
  - `033`: District membership
- `year`: School year ending (e.g., `2122` = 2021-22)
- `version`: Revision code
- `date`: Release date

**Example:** `ccd_sch_029_2122_w_0a_091422.csv` = School directory, 2021-22, released Sept 14, 2022

### Contact

**NCES:**
- General inquiries: https://nces.ed.gov/help/
- Data questions: nces.info@ed.gov
- Phone: 1-800-424-1616

---

## Example Complete Workflow: County Education Profile

```r
library(tidyverse)
library(educationdata)
library(tidycensus)
library(sf)
library(tigris)

# Set up
census_api_key("YOUR_KEY")
options(tigris_use_cache = TRUE)

# 1. Get CCD school data for target year
schools_2021 <- get_education_data(
  level = "schools",
  source = "ccd",
  topic = "directory",
  filters = list(year = 2021)
)

enrollment_2021 <- get_education_data(
  level = "schools",
  source = "ccd",
  topic = "enrollment",
  subtopic = list("race", "grade"),
  filters = list(year = 2021)
)

# 2. Aggregate to county
county_schools <- schools_2021 %>%
  filter(school_status == "Open") %>%
  mutate(county_fips = paste0(str_pad(fips, 2, "0"), str_pad(county_code, 3, "0"))) %>%
  group_by(county_fips, state_location) %>%
  summarise(
    schools = n(),
    charter_schools = sum(charter == 1, na.rm = TRUE),
    .groups = "drop"
  )

county_enrollment <- enrollment_2021 %>%
  mutate(county_fips = paste0(str_pad(fips, 2, "0"), str_pad(county_code, 3, "0"))) %>%
  group_by(county_fips) %>%
  summarise(
    total_students = sum(enrollment, na.rm = TRUE),
    .groups = "drop"
  )

# 3. Get district finance data
district_finance_2019 <- get_education_data(
  level = "school-districts",
  source = "ccd",
  topic = "finance",
  filters = list(year = 2019)
)

# Aggregate to county (using district-county crosswalk)
# For simplicity, assign each district to its primary county
county_finance <- district_finance_2019 %>%
  mutate(county_fips = paste0(str_pad(fips, 2, "0"), str_pad(county_code, 3, "0"))) %>%
  group_by(county_fips) %>%
  summarise(
    per_pupil_exp = weighted.mean(exp_per_pupil, w = enroll, na.rm = TRUE),
    mean_local_rev_pct = weighted.mean(tlocrev / totalrev * 100, w = enroll, na.rm = TRUE),
    .groups = "drop"
  )

# 4. Get college data (IPEDS)
colleges_2021 <- get_education_data(
  level = "college-university",
  source = "ipeds",
  topic = "directory",
  filters = list(year = 2021)
)

county_colleges <- colleges_2021 %>%
  filter(inst_status == 1) %>%  # Active
  mutate(county_fips = paste0(str_pad(fips_ipeds, 2, "0"), str_pad(county_code, 3, "0"))) %>%
  group_by(county_fips) %>%
  summarise(
    colleges = n(),
    four_year_colleges = sum(inst_level == 1, na.rm = TRUE),
    .groups = "drop"
  )

# 5. Combine all
county_education_profile <- county_schools %>%
  left_join(county_enrollment, by = "county_fips") %>%
  left_join(county_finance, by = "county_fips") %>%
  left_join(county_colleges, by = "county_fips") %>%
  replace_na(list(colleges = 0, four_year_colleges = 0))

# 6. Add ACS education attainment for adults
acs_education <- get_acs(
  geography = "county",
  variables = c(
    total_pop_25plus = "B15003_001",
    bach_or_higher = "B15003_022"
  ),
  year = 2021,
  survey = "acs5"
) %>%
  select(GEOID, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  mutate(pct_bach_or_higher = bach_or_higher / total_pop_25plus * 100)

# 7. Final join
county_education_final <- county_education_profile %>%
  left_join(acs_education, by = c("county_fips" = "GEOID"))

# 8. Export
write_csv(county_education_final, "county_education_data.csv")
```

---

## Changelog

**Version 1.0 (2025-11-11)**
- Initial comprehensive documentation
- All major NCES data systems documented (CCD, PSS, EDFacts, F-33, IPEDS)
- SEDA included for cross-state comparable achievement data
- County aggregation strategies detailed
- Complete R code examples
- Urban Institute Education Data API documented

---

## Citation

When using NCES data, cite the specific data source:

**Common Core of Data:**
```
U.S. Department of Education, National Center for Education Statistics, Common Core of Data (CCD),
"Public Elementary/Secondary School Universe Survey", 2021-22; "Local Education Agency Universe Survey", 2021-22.
```

**IPEDS:**
```
U.S. Department of Education, National Center for Education Statistics, Integrated Postsecondary Education
Data System (IPEDS), [Survey Component], 2021-22.
```

**SEDA:**
```
Reardon, S. F., Ho, A. D., Shear, B. R., Fahle, E. M., Kalogrides, D., Jang, H., & Chavez, B. (2021).
Stanford Education Data Archive (Version 4.1). http://purl.stanford.edu/db586ns4974
```

---

**Document Status:** ✅ Complete
**Last Updated:** November 11, 2025
**Next Update:** As needed for new NCES releases or methodology changes
