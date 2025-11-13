# Social Safety Net Programs - Comprehensive County-Level Documentation

## Executive Summary

This documentation provides complete access to county-level data on major US social safety net programs that provide economic assistance, healthcare, and support services to low-income and vulnerable populations. These programs represent critical measures of economic hardship, program participation, and social support infrastructure.

### Key Features

- **🍽️ SNAP (Food Assistance)**: 41+ million participants, monthly county data
- **🏥 Medicaid Enrollment**: 90+ million enrollees, quarterly state data (limited county-level)
- **👶 TANF (Cash Assistance)**: Families receiving temporary assistance, monthly/annual data
- **♿ SSI (Supplemental Security Income)**: Aged, blind, disabled individuals, annual county data
- **📊 SSDI (Social Security Disability Insurance)**: Disabled workers and dependents, annual county data
- **💼 Unemployment Insurance**: Claims, beneficiaries, exhaustions - monthly/quarterly
- **👵 Social Security Retirement**: Beneficiaries and payments, annual county data
- **🔑 Access**: Mix of public datasets, some require agreements, APIs available for some programs
- **🌎 Geography**: Primarily county-level; some programs state-only

---

## Table of Contents

1. [Data Systems & Sources](#data-systems--sources)
2. [SNAP - Supplemental Nutrition Assistance Program](#snap---supplemental-nutrition-assistance-program)
3. [Medicaid & CHIP Enrollment](#medicaid--chip-enrollment)
4. [TANF - Temporary Assistance for Needy Families](#tanf---temporary-assistance-for-needy-families)
5. [SSI - Supplemental Security Income](#ssi---supplemental-security-income)
6. [SSDI - Social Security Disability Insurance](#ssdi---social-security-disability-insurance)
7. [Social Security Retirement & Survivors](#social-security-retirement--survivors)
8. [Unemployment Insurance](#unemployment-insurance)
9. [WIC - Women, Infants, and Children](#wic---women-infants-and-children)
10. [LIHEAP - Energy Assistance](#liheap---energy-assistance)
11. [Free & Reduced-Price School Lunch](#free--reduced-price-school-lunch)
12. [County-Level Aggregation Strategies](#county-level-aggregation-strategies)
13. [Access Methods & APIs](#access-methods--apis)
14. [R Packages & Code Examples](#r-packages--code-examples)
15. [Data Quality & Limitations](#data-quality--limitations)
16. [Priority Variables for Collection](#priority-variables-for-collection)
17. [Quick Reference](#quick-reference)

---

## Data Systems & Sources

### 1. SNAP (Supplemental Nutrition Assistance Program)
**Agency:** USDA Food and Nutrition Service (FNS)
**Coverage:** All 3,143 counties
**Years:** 1969-present (modern SNAP 2008+)
**Update Frequency:** Monthly
**Restriction:** Public use, some county data via FOIA or restricted-use agreements

### 2. Medicaid & CHIP
**Agency:** CMS (Centers for Medicare & Medicaid Services)
**Coverage:** All states; limited county-level public data
**Years:** 1999-present (comprehensive)
**Update Frequency:** Quarterly, monthly
**Restriction:** Public enrollment data at state level; county data restricted (CMS Virtual Research Data Center)

### 3. TANF (Temporary Assistance for Needy Families)
**Agency:** HHS Administration for Children and Families (ACF)
**Coverage:** All states and territories
**Years:** 1996-present (TANF); 1960-1996 (AFDC predecessor)
**Update Frequency:** Monthly, quarterly, annual
**Restriction:** Public use at state level; some states provide county data

### 4. SSI (Supplemental Security Income)
**Agency:** Social Security Administration (SSA)
**Coverage:** All counties
**Years:** 1974-present (SSI program inception)
**Update Frequency:** Annual (December snapshot)
**Restriction:** Public use with statistical safeguards (small cell suppression)

### 5. SSDI (Social Security Disability Insurance)
**Agency:** Social Security Administration (SSA)
**Coverage:** All counties
**Years:** 1957-present (DI program inception)
**Update Frequency:** Annual (December snapshot)
**Restriction:** Public use with statistical safeguards

### 6. Social Security Retirement & Survivors
**Agency:** Social Security Administration (SSA)
**Coverage:** All counties
**Years:** 1940-present
**Update Frequency:** Annual (December snapshot)
**Restriction:** Public use

### 7. Unemployment Insurance
**Agency:** Department of Labor (DOL) Employment & Training Administration (ETA)
**Coverage:** All states; limited county-level
**Years:** 1986-present (comprehensive data); earlier years available
**Update Frequency:** Weekly (initial claims), monthly, quarterly (detailed)
**Restriction:** Public use at state level; county via BLS LAUS or state agencies

### 8. WIC (Women, Infants, and Children)
**Agency:** USDA Food and Nutrition Service (FNS)
**Coverage:** All states
**Years:** 1974-present
**Update Frequency:** Annual
**Restriction:** Public at state level; local agency level sometimes available

---

## SNAP - Supplemental Nutrition Assistance Program

SNAP (formerly Food Stamps) provides nutrition assistance to low-income individuals and families.

### Eligibility
- **Gross income**: ≤130% of federal poverty level (with exceptions)
- **Net income**: ≤100% of poverty level
- **Assets**: ≤$2,750 (or $4,250 if elderly/disabled household)
- **Work requirements**: Able-bodied adults without dependents (ABAWDs) limited to 3 months in 36-month period unless working/training

### County-Level SNAP Variables (~15 variables)

#### A. Participation
- `COUNTY_FIPS` - County FIPS code
- `STATE_ABBR` - State abbreviation
- `COUNTY_NAME` - County name
- `YEAR_MONTH` - Reporting period (YYYYMM)
- `SNAP_HOUSEHOLDS` - Number of households receiving SNAP benefits
- `SNAP_PERSONS` - Number of persons in SNAP households
- `AVG_HOUSEHOLD_SIZE` - Average household size (persons / households)

#### B. Benefits
- `TOTAL_BENEFITS` - Total SNAP benefits issued (dollars)
- `AVG_BENEFIT_PER_HOUSEHOLD` - Average benefit per household (monthly)
- `AVG_BENEFIT_PER_PERSON` - Average benefit per person (monthly)

#### C. Demographics (when available from state agencies or restricted data)
- `SNAP_CHILDREN` - Persons age <18 in SNAP households
- `SNAP_ELDERLY` - Persons age 60+ in SNAP households
- `SNAP_DISABLED` - Persons with disabilities in SNAP households
- `SNAP_WORKING_HH` - Households with earned income

#### D. Participation Rate (derived)
- **Formula**: SNAP persons / persons in poverty (from ACS)
- Indicates program take-up among eligible population
- Typically 60-85% at county level

### Data Sources

#### USDA FNS Data
**URL:** https://www.fns.usda.gov/data-research

**Files:**
- **State-level**: Monthly participation and benefits (public)
- **County-level**: Available through USDA Economic Research Service (ERS) or state agencies

#### USDA ERS SNAP Data
**URL:** https://www.ers.usda.gov/data-products/supplemental-nutrition-assistance-program-snap-data-system/

**SNAP Data System**: Interactive tool with county maps (annual averages)
**Download**: County-level annual average participation and benefits

#### State Agency Reports
Many states publish county-level SNAP data:
- **California**: County Databooks (quarterly)
- **Texas**: County-level statistics
- **New York**: County reports
- **Ohio**: County SNAP participation
- Check state HHS/Social Services websites

### Historical SNAP Data

- **1969-2008**: Food Stamp Program (FSP)
- **2008-present**: Renamed SNAP
- **Data break**: 2008 Farm Bill changed rules (may affect comparability)
- **ARRA (2009-2013)**: Elevated benefits during Great Recession
- **Pandemic (2020-2023)**: Emergency allotments increased benefits

---

## Medicaid & CHIP Enrollment

Medicaid provides health coverage to low-income individuals; CHIP covers children in families with income too high for Medicaid but too low for private insurance.

### Program Structure
- **State-administered**: Each state designs its own program within federal guidelines
- **Expansion states**: 40 states + DC expanded Medicaid under ACA (2014+)
- **Non-expansion states**: 10 states (as of 2025) maintained pre-ACA eligibility

### Eligibility (varies by state)
- **Children**: Up to 200-400% FPL (CHIP)
- **Parents**: Varies widely (31-215% FPL in expansion states; 14-95% in non-expansion)
- **Childless adults**: 138% FPL in expansion states; not eligible in non-expansion
- **Elderly/disabled**: SSI recipients automatically eligible

### Medicaid Variables (Primarily State-Level)

#### A. Enrollment by Eligibility Group (~30 variables)
**Source:** CMS Medicaid & CHIP Enrollment Data

- `TOTAL_ENROLLMENT` - Total Medicaid + CHIP enrollees
- `MEDICAID_TOTAL` - Medicaid only
- `CHIP_TOTAL` - CHIP only
- `DUAL_ELIGIBLE` - Enrolled in both Medicare and Medicaid
- By eligibility group:
  - `AGED` - Age 65+
  - `BLIND_DISABLED` - Blind or disabled
  - `CHILDREN` - Age <19
  - `ADULTS` - Age 19-64, not elderly or disabled
  - `EXPANSION_ADULTS` - Newly eligible under ACA (expansion states only)

#### B. Managed Care Enrollment
- `MANAGED_CARE_TOTAL` - Enrollees in managed care plans
- `FFS_TOTAL` - Fee-for-service enrollees
- `MANAGED_CARE_PCT` - Percent in managed care

#### C. County-Level Medicaid Data (Restricted)

**Access:** CMS Virtual Research Data Center (VRDC) or Research Data Assistance Center (ResDAC)

**Requirements:**
- Institutional affiliation (university, research org)
- IRB approval
- Data Use Agreement (DUA)
- Security plan
- Cost: $5,000-$20,000+ for data preparation

**Variables Available** (in restricted enrollment files):
- County FIPS (beneficiary residence)
- Enrollment months
- Eligibility category
- Demographics (age, sex, race/ethnicity)
- Dual eligibility status
- Managed care vs. FFS

**Public Alternative:** CMS Mapping Medicare Disparities Tool includes some Medicaid dual-eligible data at county level.

---

## TANF - Temporary Assistance for Needy Families

TANF provides cash assistance and work support to low-income families with children. Replaced AFDC (Aid to Families with Dependent Children) in 1996.

### Program Characteristics
- **Block grant**: Fixed federal funding to states
- **Work requirements**: Adults must engage in work activities (30 hrs/week)
- **Time limits**: Federal 60-month lifetime limit; states may impose shorter limits
- **State flexibility**: Wide variation in eligibility, benefit levels, work requirements

### TANF Variables (State-Level, Some County-Level)

#### A. Caseload (~20 variables)
**Source:** HHS Administration for Children and Families (ACF), TANF Caseload Data

- `STATE` - State abbreviation
- `YEAR_MONTH` - Reporting period
- `FAMILIES` - Number of families receiving TANF cash assistance
- `RECIPIENTS` - Number of individuals in TANF families
- `CHILDREN` - Child recipients
- `ADULTS` - Adult recipients
- `AVG_FAMILY_SIZE` - Recipients / families

#### B. Characteristics of Families
**Source:** TANF Active Case Data (quarterly sample data)

- `EMPLOYMENT_STATUS` - Employed (Y/N)
- `TWO_PARENT` - Two-parent families
- `SINGLE_PARENT` - Single-parent families
- `CHILD_ONLY` - Child-only cases (no adult recipient)
- `AGE_YOUNGEST_CHILD` - Distribution by age
- `RACE_ETHNICITY` - Distribution (White, Black, Hispanic, other)
- `EDUCATION` - Adult educational attainment

#### C. Financial Assistance
- `TANF_EXPENDITURES` - Total TANF spending (includes cash + services)
- `CASH_ASSISTANCE` - Cash benefits only
- `AVG_BENEFIT_PER_FAMILY` - Monthly benefit per family (varies by state: $170-$1,000)

#### D. Work Participation
- `FAMILIES_WITH_WORK_ELIGIBLE_ADULT` - Families subject to work requirements
- `FAMILIES_MEETING_WORK_REQ` - Families meeting federal work participation rate
- `WORK_PARTICIPATION_RATE` - Percent meeting requirements

### County-Level TANF Data

**Availability:** Limited; some states publish county data

**States with Known County TANF Data:**
- **California**: CalWORKs county data (quarterly)
- **Ohio**: County caseload reports
- **Pennsylvania**: County assistance office reports
- **Washington**: County caseload data
- Check state HHS/DSHS websites

---

## SSI - Supplemental Security Income

SSI provides cash assistance to aged (65+), blind, and disabled individuals with limited income and resources.

### Eligibility
- **Age**: 65+ OR blind OR disabled
- **Income**: <$943/month individual, $1,415 couple (2024)
- **Resources**: <$2,000 individual, $3,000 couple
- **Citizenship**: US citizen or qualified non-citizen

### SSI County-Level Variables (~40 variables)

**Source:** Social Security Administration (SSA) OASDI and SSI Program Data

#### A. Total SSI Recipients
- `COUNTY_FIPS` - County FIPS code
- `STATE` - State name
- `COUNTY` - County name
- `YEAR` - Calendar year (December data)
- `TOTAL_RECIPIENTS` - Total SSI recipients
- `TOTAL_PAYMENTS` - Total annual payments (thousands of dollars)
- `AVG_MONTHLY_PAYMENT` - Average monthly payment per recipient

#### B. Recipients by Age
- `AGED_RECIPIENTS` - Age 65+
- `AGED_65_74` - Age 65-74
- `AGED_75_PLUS` - Age 75+
- `UNDER_18` - Children under 18
- `AGE_18_64` - Working-age (18-64)

#### C. Recipients by Category
- `BLIND_DISABLED_RECIPIENTS` - Total blind and disabled (all ages)
- `DISABLED_18_64` - Disabled working-age adults
- `DISABLED_CHILDREN` - Disabled children under 18

#### D. Recipients by Sex
- `MALE_RECIPIENTS`
- `FEMALE_RECIPIENTS`

#### E. Recipients by Payment Status
- `FEDERAL_SSI_ONLY` - Receiving federal SSI only
- `FEDERAL_AND_STATE` - Receiving federal SSI plus state supplementation
- `STATE_ONLY` - State supplementation only (rare)

#### F. Concurrent SSI & OASDI
- `CONCURRENT_SSI_OASDI` - Recipients receiving both SSI and Social Security (retirement, disability, or survivors)

#### G. Diagnostic Category (Disabled Adults)
- `INTELLECTUAL_DISABILITY` - Intellectual disability
- `AUTISM` - Autism spectrum disorders
- `SCHIZOPHRENIA` - Schizophrenic and other psychotic disorders
- `MOOD_DISORDERS` - Mood disorders (depression, bipolar)
- `OTHER_MENTAL` - Other mental disorders
- `MUSCULOSKELETAL` - Musculoskeletal system disorders
- `CIRCULATORY` - Circulatory system disorders
- `NEOPLASMS` - Cancer and tumors
- `NERVOUS_SYSTEM` - Nervous system disorders
- `OTHER_PHYSICAL` - Other physical disorders

### Data Suppression
- **Rule**: Cells with 1-9 recipients are suppressed (shown as "*")
- **Common in**: Rural counties, especially for specific subgroups
- **Workaround**: Aggregate across years or combine categories

---

## SSDI - Social Security Disability Insurance

SSDI provides cash benefits and Medicare eligibility to insured workers who become disabled and their dependents.

### Eligibility
- **Work credits**: Must have worked and paid Social Security taxes (typically 5 of last 10 years)
- **Disability**: Unable to engage in substantial gainful activity (SGA) due to medically determinable impairment lasting 12+ months or expected to result in death
- **SGA threshold**: $1,550/month (2024) for non-blind, $2,590 for blind

### SSDI County-Level Variables (~30 variables)

**Source:** Social Security Administration OASDI Program Data

#### A. Total SSDI Beneficiaries
- `COUNTY_FIPS` - County FIPS code
- `STATE`, `COUNTY` - County name
- `YEAR` - Calendar year (December data)
- `DISABLED_WORKERS` - Disabled worker beneficiaries
- `SPOUSES_OF_DISABLED` - Spouse beneficiaries (age 62+ or caring for entitled child)
- `CHILDREN_OF_DISABLED` - Child beneficiaries (under 18, or 18-19 if full-time student, or disabled before age 22)
- `TOTAL_DI_BENEFICIARIES` - Total SSDI (workers + spouses + children)
- `TOTAL_PAYMENTS` - Total annual benefits (thousands of dollars)
- `AVG_MONTHLY_BENEFIT` - Average monthly benefit per disabled worker

#### B. Disabled Workers by Age
- `UNDER_35` - Age under 35
- `AGE_35_49` - Age 35-49
- `AGE_50_54` - Age 50-54
- `AGE_55_59` - Age 55-59
- `AGE_60_FULL_RETIREMENT` - Age 60 to full retirement age
- `FULL_RETIREMENT_PLUS` - Age full retirement age or older (switched to retirement benefits)

#### C. Disabled Workers by Sex
- `MALE_DISABLED_WORKERS`
- `FEMALE_DISABLED_WORKERS`

#### D. Diagnostic Category (same as SSI)
- Categories by primary impairment

#### E. Concurrent Benefits
- `CONCURRENT_DI_OASI` - Workers receiving both disability and retirement (during transition period)
- `CONCURRENT_DI_SSI` - Workers receiving both SSDI and SSI (low earnings history)

---

## Social Security Retirement & Survivors

Social Security Old-Age and Survivors Insurance (OASI) provides retirement and survivors benefits.

### County-Level Variables (~50 variables)

**Source:** Social Security Administration OASDI Program Data

#### A. Total Beneficiaries
- `OASI_TOTAL` - Total Old-Age and Survivors beneficiaries
- `RETIREMENT_TOTAL` - Retired workers
- `SPOUSES_RETIREMENT` - Spouses of retired workers
- `CHILDREN_RETIREMENT` - Children of retired workers
- `SURVIVORS_TOTAL` - Survivor beneficiaries
- `WIDOWS_WIDOWERS` - Widow(er)s
- `CHILDREN_SURVIVORS` - Children of deceased workers
- `PARENTS` - Dependent parents

#### B. Retired Workers by Age
- `AGE_62_64` - Early retirees (age 62-64, reduced benefits)
- `AGE_65_69` - Age 65-69
- `AGE_70_74` - Age 70-74
- `AGE_75_PLUS` - Age 75+

#### C. Benefits
- `TOTAL_ANNUAL_PAYMENTS` - Total OASI payments (thousands)
- `AVG_MONTHLY_BENEFIT_RETIRED_WORKER` - Average monthly benefit per retired worker
- `AVG_MONTHLY_BENEFIT_SURVIVOR` - Average monthly benefit per survivor

---

## Unemployment Insurance

UI provides temporary income support to workers who lose jobs through no fault of their own.

### Program Structure
- **Federal-state partnership**: States administer, federal sets broad guidelines
- **Funding**: Employer payroll taxes (federal and state)
- **Regular benefits**: Typically 26 weeks
- **Extended benefits**: Available during high unemployment (up to 13-20 additional weeks)

### UI Variables (Primarily State-Level)

#### A. Initial Claims (Weekly, State-Level)
**Source:** DOL ETA Weekly Claims Data

- `STATE` - State abbreviation
- `WEEK_ENDING_DATE` - Week ending Saturday
- `INITIAL_CLAIMS` - New UI applications filed
- `CONTINUED_CLAIMS` - Ongoing claims (insured unemployment)

#### B. Insured Unemployment Rate (IUR)
**Source:** DOL ETA, BLS

- **Formula**: Continued claims / covered employment
- **Published**: Weekly (state), monthly (state and some metro areas)

#### C. Beneficiaries & Payments (Quarterly, State-Level)
**Source:** DOL ETA 5159 Report

- `FIRST_PAYMENTS` - Number of first payments made (new claimants receiving benefits)
- `FINAL_PAYMENTS` - Number of final payments (exhausted benefits)
- `WEEKS_COMPENSATED` - Total weeks of benefits paid
- `AVG_WEEKLY_BENEFIT` - Average weekly benefit amount
- `TOTAL_BENEFITS_PAID` - Total dollars paid

#### D. Exhaustion Rate
- **Formula**: Final payments / (first payments + continued claims from prior period)
- Indicates share of claimants who exhaust regular benefits before finding work

### County-Level UI Data

**Primary Source:** BLS Local Area Unemployment Statistics (LAUS)

**Variables** (monthly):
- `COUNTY_FIPS` - County FIPS code
- `LABOR_FORCE` - Civilian labor force
- `EMPLOYED` - Employed persons
- `UNEMPLOYED` - Unemployed persons (not necessarily receiving UI)
- `UNEMPLOYMENT_RATE` - Unemployed / labor force * 100

**Note:** LAUS unemployment counts include all unemployed, not just UI recipients. Actual UI recipients are a subset (typically 30-50% of unemployed receive UI).

**County UI Beneficiaries:** Some states publish county-level UI beneficiary data. Check state workforce/labor department websites.

---

## WIC - Women, Infants, and Children

WIC provides nutrition assistance, breastfeeding support, and health referrals to pregnant women, new mothers, infants, and children up to age 5.

### Eligibility
- **Categorical**: Pregnant, postpartum, breastfeeding women; infants; children under 5
- **Income**: ≤185% federal poverty level
- **Nutritional risk**: Must be at nutritional risk (determined by health professional)

### WIC Variables (State-Level, Some Local Agency Data)

#### A. Participation
**Source:** USDA FNS WIC Program Data

- `STATE` - State
- `YEAR_MONTH` - Reporting period
- `TOTAL_PARTICIPANTS` - Total WIC participants
- `WOMEN` - Women participants (pregnant, postpartum, breastfeeding)
- `INFANTS` - Infant participants (0-12 months)
- `CHILDREN` - Child participants (1-4 years)

#### B. Program Costs
- `TOTAL_FOOD_COSTS` - Food benefits issued
- `AVG_FOOD_COST_PER_PERSON` - Average monthly food cost per participant
- `NUTRITION_SERVICES_COSTS` - Nutrition education and breastfeeding support
- `ADMINISTRATIVE_COSTS` - Program administration

#### C. Local Agency Data (Variable Availability)
Some states publish WIC data by local agency (which may align with counties):
- Participants by local agency
- Local agency locations

**States with Local Agency WIC Data:**
- **California**: Local agency reports
- **Texas**: Local agency data
- Check state health department WIC websites

---

## LIHEAP - Energy Assistance

Low Income Home Energy Assistance Program provides assistance with heating and cooling costs.

### Variables (State-Level, Some Sub-State)

**Source:** HHS Office of Community Services

- `STATE` - State
- `HOUSEHOLDS_ASSISTED` - Number of households receiving assistance
- `HEATING_ASSISTANCE` - Households receiving heating assistance
- `COOLING_ASSISTANCE` - Households receiving cooling assistance
- `CRISIS_ASSISTANCE` - Emergency assistance
- `TOTAL_ASSISTANCE` - Total dollars distributed
- `AVG_ASSISTANCE_PER_HOUSEHOLD` - Average assistance amount

**County-Level:** Limited; some states may provide county breakdowns.

---

## Free & Reduced-Price School Lunch

While not a cash assistance program, free/reduced-price lunch (FRL) eligibility is a widely used poverty indicator and proxy for SNAP eligibility.

### Data Source
National Center for Education Statistics (NCES) Common Core of Data (CCD)

### Variables (School-Level, Aggregable to County)
- `TOTFRL` - Total students eligible for free or reduced-price lunch
- `FRELCH` - Free lunch eligible (≤130% FPL)
- `REDLCH` - Reduced-price lunch eligible (130-185% FPL)
- `MEMBER` - Total students enrolled

**Calculation:**
- `FRL_RATE = TOTFRL / MEMBER * 100`

**Limitation:** As of 2014, Community Eligibility Provision (CEP) allows high-poverty schools to offer universal free meals without collecting individual applications, reducing data quality in recent years for this measure.

---

## County-Level Aggregation Strategies

### Strategy 1: Direct County Data (SSI, SSDI, Social Security)
SSA publishes annual county-level data files.

**Steps:**
1. Download annual county files from SSA website
2. Filter to target year
3. Variables are already county-aggregated

**Example:**
```r
# SSA publishes county files in fixed-width format or Excel
ssi_county <- read_csv("ssi_county_2023.csv")

county_ssi <- ssi_county %>%
  select(
    county_fips = FIPS,
    state, county,
    total_ssi = TOTAL,
    aged_ssi = AGED,
    disabled_ssi = DISABLED,
    avg_payment = AVG_PAYMENT
  )
```

### Strategy 2: State Data with County Estimation (SNAP, TANF, Medicaid)
Many programs publish state-level data only. Estimate county shares using related variables.

**Proxy Method:**
- Use ACS poverty population as proxy for SNAP/TANF eligibility
- Allocate state total to counties proportional to poverty population

**Example:**
```r
# Get county poverty population from ACS
county_poverty <- get_acs(
  geography = "county",
  variables = "B17001_002",  # Population below poverty
  year = 2021
)

# Calculate county share of state poverty population
county_shares <- county_poverty %>%
  mutate(state_fips = substr(GEOID, 1, 2)) %>%
  group_by(state_fips) %>%
  mutate(
    state_poverty_total = sum(estimate),
    county_poverty_share = estimate / state_poverty_total
  ) %>%
  ungroup()

# Apply to state SNAP totals
state_snap <- read_csv("state_snap_2023.csv")  # Hypothetical

county_snap_estimated <- county_shares %>%
  left_join(state_snap, by = c("state_fips" = "state_fips")) %>%
  mutate(
    snap_persons_estimated = state_snap_persons * county_poverty_share,
    snap_benefits_estimated = state_snap_benefits * county_poverty_share
  )
```

**Limitation:** Assumes program participation rates are uniform within state (not true; urban/rural differences exist).

### Strategy 3: Local Agency Aggregation (WIC)
WIC local agencies may serve specific counties. Aggregate local agency data to county.

**Requires:** Crosswalk of local agencies to counties (often available from state WIC office).

---

## Access Methods & APIs

### 1. Social Security Administration (SSA) Data

#### A. OASDI & SSI County Data
**URL:** https://www.ssa.gov/policy/docs/statcomps/oasdi_sc/index.html

**Files:**
- Annual county-level data (Excel, CSV)
- Separate files for OASDI (retirement, survivors, disability) and SSI
- Released annually (typically June for prior December data)

**Access:** Direct download, no registration

#### B. SSA Open Data Platform
**URL:** https://data.ssa.gov/

**Datasets:**
- State and county beneficiary data
- Some interactive visualizations

### 2. USDA Food and Nutrition Service (FNS)

#### A. SNAP State-Level Data
**URL:** https://www.fns.usda.gov/pd/supplemental-nutrition-assistance-program-snap

**Files:**
- Monthly state participation and benefits (Excel, CSV)
- Annual state summaries

#### B. USDA ERS SNAP Data System
**URL:** https://www.ers.usda.gov/data-products/supplemental-nutrition-assistance-program-snap-data-system/

**Features:**
- Interactive maps (county-level annual averages)
- Downloadable county data files

### 3. CMS Medicaid Enrollment Data

#### A. Medicaid & CHIP Enrollment Reports
**URL:** https://www.medicaid.gov/medicaid/program-information/medicaid-and-chip-enrollment-data/index.html

**Files:**
- Monthly and quarterly state enrollment
- Managed care enrollment reports

#### B. T-MSIS (Transformed Medicaid Statistical Information System)
**URL:** https://www.medicaid.gov/medicaid/data-systems/macbis/tmsis/index.html

**Access:** Restricted (ResDAC, VRDC)
**County-Level:** Available in beneficiary files (restricted-use)

### 4. HHS TANF Data

#### A. TANF Caseload Data
**URL:** https://www.acf.hhs.gov/ofa/data/tanf-caseload-data

**Files:**
- Monthly state caseload (families, recipients)
- Quarterly characteristics of families

**Access:** Direct download (Excel)

### 5. Department of Labor UI Data

#### A. Weekly UI Claims (ETA 539)
**URL:** https://oui.doleta.gov/unemploy/claims.asp

**Data:**
- Weekly initial and continued claims by state
- CSV download

#### B. Quarterly UI Data (ETA 5159)
**URL:** https://oui.doleta.gov/unemploy/data_summary/DataSum.asp

**Data:**
- State quarterly first payments, final payments, weeks compensated, benefit amounts

### 6. BLS LAUS (Unemployment by County)

#### A. BLS LAUS Data
**URL:** https://www.bls.gov/lau/

**Files:**
- Monthly county unemployment (CSV, Excel)
- Annual county averages

#### B. BLS API
**URL:** https://www.bls.gov/developers/

**Endpoint Example:**
```
GET https://api.bls.gov/publicAPI/v2/timeseries/data/LAUCN060010000000003
```
(Series ID format: `LAUCN` + county FIPS + `0000000` + data type code)

**Data Type Codes:**
- `03` = Unemployment rate
- `04` = Unemployed persons
- `05` = Employed persons
- `06` = Labor force

**Registration Required:** Free API key (500 requests/day; up to 25 series per query)

---

## R Packages & Code Examples

### 1. `blscrapeR` Package (BLS LAUS Unemployment)

**Installation:**
```r
install.packages("blscrapeR")
library(blscrapeR)
```

**Get county unemployment data:**
```r
# Set BLS API key
set_bls_key("YOUR_API_KEY")

# Get unemployment rate for all counties in Iowa (FIPS 19)
# LAUS series ID format: LAUCN + 5-digit FIPS + 0000000 + 03 (unemployment rate)

# Generate series IDs for all Iowa counties (19001-19197)
iowa_counties <- sprintf("19%03d", seq(1, 197, by = 2))  # Iowa has odd-numbered county codes
series_ids <- paste0("LAUCN", iowa_counties, "0000000003")

# Query BLS API (max 25 series at a time)
iowa_unemployment <- bls_api(series_ids, startyear = 2020, endyear = 2023)

# Clean and format
iowa_unemp_clean <- iowa_unemployment %>%
  mutate(
    county_fips = substr(seriesID, 6, 10),
    year = as.integer(year),
    month = as.integer(period),
    unemployment_rate = as.numeric(value)
  ) %>%
  select(county_fips, year, month, unemployment_rate)
```

### 2. SSA County Data

**Download and process SSI county data:**
```r
library(tidyverse)
library(readxl)

# SSA publishes annual county files
# Example: SSI Recipients by County, December 2023
url_ssi <- "https://www.ssa.gov/policy/docs/statcomps/ssi_sc/2023/ssi_sc23.xlsx"

# Download
temp <- tempfile(fileext = ".xlsx")
download.file(url_ssi, temp, mode = "wb")

# Read (check sheet name; typically "Table 2" for county data)
ssi_county_2023 <- read_excel(temp, sheet = "Table 2", skip = 3)  # Skip header rows

# Clean
ssi_clean <- ssi_county_2023 %>%
  select(
    state = State,
    county = County,
    fips = `FIPS code`,
    total = `Total recipients`,
    aged = `Aged recipients`,
    blind_disabled = `Blind and disabled recipients`,
    under_18 = `Under age 18`,
    age_18_64 = `Age 18-64`,
    age_65_plus = `Age 65 or older`,
    total_payments = `Total annual payments (thousands)`,
    avg_monthly = `Average monthly payment`
  ) %>%
  filter(!is.na(fips), fips != "")  # Remove non-county rows

# Handle suppression (cells with "*")
ssi_clean <- ssi_clean %>%
  mutate(across(total:avg_monthly, ~ifelse(. == "*", NA_real_, as.numeric(.))))
```

### 3. USDA ERS SNAP County Data

**Download SNAP county data:**
```r
# USDA ERS SNAP Data System provides county-level files
# Example URL (check ERS website for current files)
url_snap <- "https://www.ers.usda.gov/webdocs/DataFiles/80611/SNAPCountyData_2022.csv"

snap_county <- read_csv(url_snap)

# Clean
snap_clean <- snap_county %>%
  mutate(
    county_fips = str_pad(FIPS, 5, "0")
  ) %>%
  select(
    county_fips,
    state = State,
    county = County,
    snap_persons = `SNAP_Persons`,
    snap_households = `SNAP_Households`,
    snap_benefits_total = `SNAP_Benefits_Total`,
    avg_benefit_per_person = `Avg_Benefit_Per_Person`
  )
```

### 4. Combine Multiple Safety Net Programs

**Create comprehensive county safety net profile:**
```r
library(tidyverse)
library(tidycensus)

# 1. Get poverty data (denominator for participation rates)
census_api_key("YOUR_KEY")

poverty_data <- get_acs(
  geography = "county",
  variables = c(
    poverty_pop = "B17001_002",
    total_pop = "B01003_001"
  ),
  year = 2021,
  survey = "acs5"
) %>%
  select(GEOID, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  mutate(poverty_rate = poverty_pop / total_pop * 100)

# 2. Load SSI data (from previous example)
# ssi_clean <- ...

# 3. Load SNAP data (from previous example)
# snap_clean <- ...

# 4. Load BLS unemployment data (from previous example)
# Use LAUS annual average
laus_annual <- get_acs(
  geography = "county",
  variables = "S2301_C04_001E",  # Unemployment rate (ACS)
  year = 2021
) %>%
  select(GEOID, unemployment_rate = estimate)

# 5. Combine all
county_safety_net <- poverty_data %>%
  left_join(
    ssi_clean %>% mutate(GEOID = str_pad(fips, 5, "0")),
    by = "GEOID"
  ) %>%
  left_join(
    snap_clean %>% mutate(GEOID = county_fips),
    by = "GEOID"
  ) %>%
  left_join(laus_annual, by = "GEOID") %>%
  mutate(
    # Calculate participation rates
    ssi_per_1000 = total / (total_pop / 1000),
    snap_participation_rate = snap_persons / poverty_pop * 100
  ) %>%
  select(
    GEOID, state, county,
    total_pop, poverty_pop, poverty_rate,
    ssi_recipients = total, ssi_per_1000,
    snap_persons, snap_participation_rate,
    unemployment_rate
  )

# Export
write_csv(county_safety_net, "county_safety_net_2021.csv")
```

---

## Data Quality & Limitations

### SNAP

**Strengths:**
- Universal program (all states participate)
- High participation rate (70-80% of eligible households)
- Monthly data available

**Limitations:**
- **County data availability**: Public access limited; may require FOIA or state-specific sources
- **Eligibility complexity**: Gross/net income tests, asset limits, work requirements vary
- **Policy changes**: Pandemic emergency allotments (2020-2023) inflated participation and benefits; post-pandemic decline
- **Participation rate calculation**: Requires poverty population estimate (ACS has margin of error)

### Medicaid

**Strengths:**
- Large program (90+ million enrollees)
- Comprehensive enrollment data at state level

**Limitations:**
- **County data**: Not publicly available; requires restricted-use data access
- **State variation**: Expansion vs. non-expansion states have fundamentally different eligibility; not comparable
- **Managed care**: Growing share of enrollees in managed care (data quality varies)
- **Churn**: High enrollment/disenrollment rates complicate point-in-time counts

### TANF

**Strengths:**
- Long time series (AFDC 1960-1996, TANF 1996+)
- Monthly caseload data

**Limitations:**
- **Declining caseload**: TANF caseloads have declined 70% since 1996 despite increasing poverty (strict work requirements, time limits, state diversion)
- **State variation**: Enormous variation in eligibility, benefit levels, work requirements
- **County data**: Very limited public access
- **Cash assistance only**: TANF block grant also funds non-cash services (childcare, job training); caseload data exclude these

### SSI & SSDI

**Strengths:**
- Federal program (uniform eligibility rules)
- Comprehensive county-level data
- Annual releases with long time series

**Limitations:**
- **Disability determination**: Lengthy process (6-24 months); backlogs vary by state
- **Suppression**: Small cells (1-9) suppressed in county files
- **Point-in-time**: December snapshot; doesn't capture within-year changes
- **Medicare interaction**: SSDI beneficiaries become Medicare-eligible after 24 months; impacts healthcare data linkage

### Unemployment Insurance

**Strengths:**
- Timely data (weekly initial claims)
- Long time series

**Limitations:**
- **County data**: Limited public access; BLS LAUS provides unemployment counts but not UI recipients
- **Eligibility**: Only ~40% of unemployed workers receive UI (many don't qualify or exhaust benefits)
- **Pandemic anomaly**: Pandemic Unemployment Assistance (PUA) 2020-2021 included gig workers, self-employed (not in regular UI); inflated counts

---

## Priority Variables for Collection

For a **county-level safety net dataset**, the following are highest-priority:

### Tier 1: Core Economic Support Programs
1. **SNAP participants** (persons receiving food assistance)
2. **SNAP participation rate** (SNAP persons / poverty population)
3. **SSI recipients** (aged, blind, disabled with low income)
4. **SSDI beneficiaries** (disabled workers)
5. **Unemployment rate** (BLS LAUS)

### Tier 2: Healthcare Access
6. **Medicaid enrollment** (if county-level accessible; otherwise state-level for context)
7. **Dual-eligible beneficiaries** (Medicare + Medicaid)

### Tier 3: Additional Safety Net
8. **TANF families** (if county-level available; otherwise state-level)
9. **Social Security retirement beneficiaries** (aged 62+)
10. **WIC participants** (if county-level available)

### Tier 4: Rates & Intensity Measures
11. **SSI per 1,000 population** (intensity measure)
12. **SSDI per 1,000 working-age population** (prevalence of disability)
13. **Average SNAP benefit per person** (benefit adequacy)
14. **Average SSI payment** (income support level)

### Tier 5: Subpopulations
15. **SSI disabled children** (child disability prevalence)
16. **SSDI by diagnostic category** (types of disability)
17. **Insured unemployment rate** (UI claims / labor force)

---

## Quick Reference

### Key URLs

| Program | Agency | Data URL |
|---------|--------|----------|
| **SNAP** | USDA FNS | https://www.fns.usda.gov/pd/supplemental-nutrition-assistance-program-snap |
| **SNAP County** | USDA ERS | https://www.ers.usda.gov/data-products/supplemental-nutrition-assistance-program-snap-data-system/ |
| **Medicaid** | CMS | https://www.medicaid.gov/medicaid/program-information/medicaid-and-chip-enrollment-data/index.html |
| **TANF** | HHS ACF | https://www.acf.hhs.gov/ofa/data/tanf-caseload-data |
| **SSI County** | SSA | https://www.ssa.gov/policy/docs/statcomps/ssi_sc/ |
| **SSDI County** | SSA | https://www.ssa.gov/policy/docs/statcomps/oasdi_sc/ |
| **Unemployment** | DOL ETA | https://oui.doleta.gov/unemploy/claims.asp |
| **LAUS County** | BLS | https://www.bls.gov/lau/ |
| **WIC** | USDA FNS | https://www.fns.usda.gov/pd/wic-program |

### Key R Packages

| Package | Purpose | Installation |
|---------|---------|--------------|
| `blscrapeR` | BLS data (unemployment) | `install.packages("blscrapeR")` |
| `tidycensus` | Poverty population (denominators) | `install.packages("tidycensus")` |
| `readxl` | Read SSA Excel files | `install.packages("readxl")` |

### Contact Information

**Social Security Administration:**
- Data inquiries: statistics@ssa.gov
- Publications: https://www.ssa.gov/policy/about/contact-ORES.html

**USDA FNS:**
- SNAP data: FNS-data@usda.gov

**CMS:**
- Medicaid data: MedicaidCHIPDataRequests@cms.hhs.gov

**BLS:**
- LAUS: LAUinfo@bls.gov

---

## Example Complete Workflow: County Safety Net Profile

```r
library(tidyverse)
library(tidycensus)
library(blscrapeR)
library(readxl)

# Set API keys
census_api_key("YOUR_CENSUS_KEY")
set_bls_key("YOUR_BLS_KEY")

# 1. Get poverty population (denominator for participation rates)
poverty <- get_acs(
  geography = "county",
  variables = c(
    poverty_pop = "B17001_002",
    poverty_child = "B17001_004",
    total_pop = "B01003_001"
  ),
  year = 2021,
  survey = "acs5"
) %>%
  select(GEOID, NAME, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  mutate(poverty_rate = poverty_pop / total_pop * 100)

# 2. Download SSI county data
url_ssi <- "https://www.ssa.gov/policy/docs/statcomps/ssi_sc/2023/ssi_sc23.xlsx"
temp_ssi <- tempfile(fileext = ".xlsx")
download.file(url_ssi, temp_ssi, mode = "wb")
ssi_raw <- read_excel(temp_ssi, sheet = "Table 2", skip = 3)

ssi_county <- ssi_raw %>%
  select(
    fips = `FIPS code`,
    ssi_total = `Total recipients`,
    ssi_aged = `Aged recipients`,
    ssi_disabled = `Blind and disabled recipients`,
    ssi_payments = `Total annual payments (thousands)`
  ) %>%
  filter(!is.na(fips), fips != "") %>%
  mutate(
    GEOID = str_pad(fips, 5, "0"),
    across(ssi_total:ssi_payments, ~ifelse(. == "*", NA_real_, as.numeric(.)))
  )

# 3. Download SSDI county data
url_ssdi <- "https://www.ssa.gov/policy/docs/statcomps/oasdi_sc/2023/oasdi_sc23.xlsx"
temp_ssdi <- tempfile(fileext = ".xlsx")
download.file(url_ssdi, temp_ssdi, mode = "wb")
ssdi_raw <- read_excel(temp_ssdi, sheet = "Table 4", skip = 3)

ssdi_county <- ssdi_raw %>%
  select(
    fips = `FIPS code`,
    ssdi_workers = `Disabled workers`,
    ssdi_total = `Total DI beneficiaries`
  ) %>%
  filter(!is.na(fips), fips != "") %>%
  mutate(
    GEOID = str_pad(fips, 5, "0"),
    across(ssdi_workers:ssdi_total, ~ifelse(. == "*", NA_real_, as.numeric(.)))
  )

# 4. Get unemployment rate from BLS LAUS (use tidycensus ACS as simpler alternative)
unemployment <- get_acs(
  geography = "county",
  variables = "S2301_C04_001E",  # Unemployment rate
  year = 2021
) %>%
  select(GEOID, unemployment_rate = estimate)

# 5. Download SNAP county data from USDA ERS
url_snap <- "https://www.ers.usda.gov/webdocs/DataFiles/80611/SNAPCountyData_2021.csv"
snap_county <- read_csv(url_snap) %>%
  mutate(GEOID = str_pad(FIPS, 5, "0")) %>%
  select(
    GEOID,
    snap_persons = SNAP_Persons,
    snap_households = SNAP_Households,
    snap_benefits = SNAP_Benefits_Total
  )

# 6. Combine all
county_safety_net_profile <- poverty %>%
  left_join(ssi_county, by = "GEOID") %>%
  left_join(ssdi_county, by = "GEOID") %>%
  left_join(unemployment, by = "GEOID") %>%
  left_join(snap_county, by = "GEOID") %>%
  mutate(
    # Calculate rates per 1,000 population
    ssi_per_1000 = ssi_total / (total_pop / 1000),
    ssdi_per_1000 = ssdi_workers / (total_pop / 1000),
    # SNAP participation rate (SNAP persons / poverty population)
    snap_participation_rate = snap_persons / poverty_pop * 100
  ) %>%
  select(
    GEOID, NAME,
    total_pop, poverty_pop, poverty_rate,
    ssi_total, ssi_per_1000,
    ssdi_workers, ssdi_per_1000,
    snap_persons, snap_participation_rate,
    unemployment_rate
  )

# 7. Export
write_csv(county_safety_net_profile, "county_safety_net_2021.csv")
```

---

## Changelog

**Version 1.0 (2025-11-11)**
- Initial comprehensive documentation
- All major federal safety net programs documented
- County-level data access methods detailed
- Complete R code examples
- Participation rate calculations provided

---

## Citation

When using safety net data, cite the specific program source:

**SNAP:**
```
U.S. Department of Agriculture, Food and Nutrition Service. Supplemental Nutrition Assistance Program (SNAP) Data System, [Year].
```

**SSI/SSDI:**
```
Social Security Administration. SSI Recipients by State and County, [Year]. Annual Statistical Supplement to the Social Security Bulletin.
```

**Medicaid:**
```
Centers for Medicare & Medicaid Services. Medicaid & CHIP Monthly Application, Eligibility Determinations and Enrollment Reports, [Date].
```

**TANF:**
```
U.S. Department of Health and Human Services, Administration for Children and Families. TANF Caseload Data, [Year].
```

**Unemployment Insurance:**
```
U.S. Department of Labor, Employment and Training Administration. Unemployment Insurance Weekly Claims Data, [Date].
```

---

**Document Status:** ✅ Complete
**Last Updated:** November 11, 2025
**Next Update:** As needed for program policy changes or data availability
