# COMPREHENSIVE DOCUMENTATION: County Business Patterns (CBP) & Quarterly Census of Employment and Wages (QCEW)

**Last Updated:** November 11, 2025
**Data Status:** CBP 2023 (Most Recent), QCEW Q1 2025 (Latest Release)

---

## TABLE OF CONTENTS

1. [PART 1: COUNTY BUSINESS PATTERNS (CBP)](#part-1-county-business-patterns-cbp)
2. [PART 2: QUARTERLY CENSUS OF EMPLOYMENT AND WAGES (QCEW)](#part-2-quarterly-census-of-employment-and-wages-qcew)
3. [NAICS INDUSTRY CLASSIFICATION](#naics-industry-classification)
4. [PRODUCTION-READY CODE EXAMPLES](#production-ready-code-examples)

---

# PART 1: COUNTY BUSINESS PATTERNS (CBP)

## OVERVIEW

County Business Patterns (CBP) is an annual series providing subnational economic data by industry. Published by the U.S. Census Bureau since 1964, CBP provides statistics on business establishments at detailed geographic and industry levels.

**Data Coverage:** 98% of private nonfarm employment
**Geographic Levels:** National, State, County, Metropolitan/Micropolitan Statistical Area, Combined Statistical Area, ZIP Code, Congressional District
**Industry Detail:** 2- through 6-digit NAICS codes

---

## COMPLETE VARIABLE DOCUMENTATION

### Core Variables (Available via API and Downloads)

| Variable Name | Description | Data Type | Units | Years Available |
|--------------|-------------|-----------|-------|-----------------|
| **ESTAB** | Number of establishments | Integer | Count | 1986-2023 |
| **EMP** | Mid-March employment | Integer | Count | 1986-2023 |
| **EMP_N** | Noise range for employment | Integer | Range indicator | 2007-2023 |
| **PAYQTR1** (API: **QP1**) | First quarter payroll | Integer | Thousands of dollars | 1986-2023 |
| **PAYQTR1_N** (API: **PAYQTR1_N**) | Noise range for Q1 payroll | Integer | Range indicator | 2007-2023 |
| **PAYANN** (API: **AP**) | Annual payroll | Integer | Thousands of dollars | 1986-2023 |
| **PAYANN_N** | Noise range for annual payroll | Integer | Range indicator | 2007-2023 |

### Establishment Size Class Variables (Download Files)

**Variable Pattern:** `N{size_class}`

| Variable | Employment Range | Available |
|----------|-----------------|-----------|
| **N1_4** | 1-4 employees | 1986-2023 |
| **N5_9** | 5-9 employees | 1986-2023 |
| **N10_19** | 10-19 employees | 1986-2023 |
| **N20_49** | 20-49 employees | 1986-2023 |
| **N50_99** | 50-99 employees | 1986-2023 |
| **N100_249** | 100-249 employees | 1986-2023 |
| **N250_499** | 250-499 employees | 1986-2023 |
| **N500_999** | 500-999 employees | 1986-2023 |
| **N1000** | 1,000+ employees (total) | 1986-2023 |
| **N1000_1** | 1,000-1,499 employees | 1986-2023 |
| **N1000_2** | 1,500-2,499 employees | 1986-2023 |
| **N1000_3** | 2,500-4,999 employees | 1986-2023 |
| **N1000_4** | 5,000+ employees | 1986-2023 |

### Employment Size Class Code (API)

**Variable:** `EMPSZES` (Employment size of establishments code)

Available in API queries to filter by size class.

### Geographic Variables

| Variable | Description | Format |
|----------|-------------|--------|
| **FIPSTATE** | FIPS State Code | 2-digit string |
| **FIPSCTY** | FIPS County Code | 3-digit string |
| **STATE** | State FIPS (API) | 2-digit |
| **COUNTY** | County FIPS (API) | 3-digit |
| **CBSA** | Metro/Micro Statistical Area | 5-digit |
| **CSA** | Combined Statistical Area | Variable |
| **ZIPCODE** | 5-digit ZIP Code | 5-digit string |
| **CD** | Congressional District | Variable |
| **GEO_ID** | Geographic identifier code | String |
| **NAME** | Geographic name | String |

### Industry Classification Variables

| Variable | Description | Format | Detail Level |
|----------|-------------|--------|--------------|
| **NAICS** (Download) | Industry Code | 6-digit string | 3-6 digits |
| **NAICS2017** (API) | 2017 NAICS code | String | 2-6 digits |
| **NAICS2017_LABEL** (API) | Industry description | String | Text |
| **INDLEVEL** | Industry level code | Integer | 2-6 |
| **SECTOR** | NAICS economic sector | String | 2-digit |
| **SUBSECTOR** | Subsector classification | String | 3-digit |
| **INDGROUP** | Industry group | String | Variable |

**INDLEVEL Codes:**
- `2` = 2-digit NAICS (Sector)
- `3` = 3-digit NAICS (Subsector)
- `4` = 4-digit NAICS (Industry Group)
- `5` = 5-digit NAICS (NAICS Industry)
- `6` = 6-digit NAICS (National Industry)

### Legal Form of Organization (LFO)

**Variable:** `LFO` (Available at U.S. and state level only)

| Code | Description |
|------|-------------|
| **C** | C-Corporations and other corporate legal forms |
| **S** | S-Corporations |
| **P** | Partnerships |
| **N** | Non-profits |
| **I** | Sole Proprietorships |
| **G** | Government |
| **O** | Other |

### Data Quality and Suppression Variables

| Variable | Description | Values |
|----------|-------------|--------|
| **EMPFLAG** | Employment suppression flag | See table below |
| **EMP_NF** | Employment noise flag | G/H/D/S |
| **QP1_NF** | Q1 payroll noise flag | G/H/D/S |
| **AP_NF** | Annual payroll noise flag | G/H/D/S |

**EMPFLAG Values (Employment Size Range when Suppressed):**

| Flag | Employment Range |
|------|-----------------|
| **A** | 0-19 |
| **B** | 20-99 |
| **C** | 100-249 |
| **E** | 250-499 |
| **F** | 500-999 |
| **G** | 1,000-2,499 |
| **H** | 2,500-4,999 |
| **I** | 5,000-9,999 |
| **J** | 10,000-24,999 |
| **K** | 25,000-49,999 |
| **L** | 50,000-99,999 |
| **M** | 100,000+ |

**Noise Flag Values:**

| Flag | Description | Change Amount |
|------|-------------|---------------|
| **G** | Low noise | <2% change |
| **H** | Medium noise | 2-5% change |
| **J** | High noise | ≥5% change |
| **D** | Withheld to avoid disclosure (deprecated after 2017) | N/A |
| **S** | Withheld (publication standards, 2017+) | N/A |

---

## YEARS AVAILABLE

### Historical Coverage

- **1964-1997:** Data tabulated using SIC (Standard Industrial Classification)
- **1998-present:** Data tabulated using NAICS
- **1986-2023:** CSV downloads available
- **Pre-1986:** Available from National Archives

### Most Recent Data (as of November 2025)

- **Latest Available:** 2023 (released in 2024)
- **2024 Data Expected:** Summer 2026
- **2025 Data Expected:** Summer 2027

### Disclosure Avoidance Methodology by Year

- **2007-2021:** Multiplicative noise infusion
- **2022+:** Differential privacy methodology (two-component noise injection)

---

## DATA ACCESS METHODS

### 1. Census API

**Base Endpoint:** `https://api.census.gov/data/{YEAR}/cbp`

**Available Years:** 1986-2023 (via API: recent years only; check availability)

#### API Key Requirements

- **Required if:** >500 queries per day
- **Request Key:** https://api.census.gov/data/key_signup.html
- **Rate Limit:** 500 queries/day without key

#### Basic API Call Structure

```
https://api.census.gov/data/{YEAR}/cbp?get={VARIABLES}&for={GEOGRAPHY}&{FILTERS}
```

**Example - All Counties, Total Establishments:**
```
https://api.census.gov/data/2023/cbp?get=ESTAB,EMP,PAYANN,NAICS2017_LABEL,NAME&for=county:*&NAICS2017=00
```

**Example - Specific County, 6-digit NAICS:**
```
https://api.census.gov/data/2023/cbp?get=ESTAB,EMP,PAYQTR1,PAYANN&for=county:001&in=state:01&NAICS2017=722511
```

**Example - State Level by Size Class:**
```
https://api.census.gov/data/2023/cbp?get=ESTAB,EMP,EMPSZES&for=state:06&NAICS2017=72
```

**Example - Metro Area Data:**
```
https://api.census.gov/data/2023/cbp?get=ESTAB,EMP,PAYANN,NAME&for=metropolitan%20statistical%20area/micropolitan%20statistical%20area:*&NAICS2017=54
```

#### Variables API Documentation

**Endpoint:** `https://api.census.gov/data/{YEAR}/cbp/variables.html`

Example: https://api.census.gov/data/2023/cbp/variables.html

### 2. Direct CSV Downloads

**Location:** https://www.census.gov/programs-surveys/cbp/data/datasets.html

**File Formats:**
- County files: `cbp{YY}co.zip` (e.g., `cbp23co.zip` for 2023)
- State files: `cbp{YY}st.zip`
- National files: `cbp{YY}us.zip`

**Download URL Pattern:**
```
https://www2.census.gov/programs-surveys/cbp/datasets/{YEAR}/cbp{YY}co.zip
```

Example: https://www2.census.gov/programs-surveys/cbp/datasets/2023/cbp23co.zip

**Record Layout Documentation:**
```
https://www2.census.gov/programs-surveys/cbp/technical-documentation/records-layouts/noise-layout/county_layout.txt
```

### 3. Data.census.gov (Interactive Query Tool)

**URL:** https://data.census.gov/

**Navigation:**
1. Select "Economy" → "County Business Patterns"
2. Choose geography (County, State, etc.)
3. Select industry (NAICS codes)
4. Download filtered results

---

## R PACKAGE ACCESS

### Using `censusapi` Package

```r
# Install package
install.packages("censusapi")
library(censusapi)

# Set API key (get from https://api.census.gov/data/key_signup.html)
Sys.setenv(CENSUS_KEY = "your_key_here")

# Example 1: All counties, construction sector (NAICS 23)
cbp_county <- getCensus(
  name = "cbp",
  vintage = 2023,
  vars = c("ESTAB", "EMP", "PAYANN", "NAICS2017_LABEL", "NAME"),
  region = "county:*",
  NAICS2017 = "23"
)

# Example 2: Specific state, all 6-digit NAICS in retail (44-45)
cbp_retail_ca <- getCensus(
  name = "cbp",
  vintage = 2023,
  vars = c("ESTAB", "EMP", "PAYQTR1", "PAYANN", "NAICS2017", "NAICS2017_LABEL"),
  region = "county:*",
  regionin = "state:06",
  NAICS2017 = "44*,45*"  # Wildcard for all retail codes
)

# Example 3: County totals (all industries)
cbp_totals <- getCensus(
  name = "cbp",
  vintage = 2023,
  vars = c("ESTAB", "EMP", "PAYANN", "GEO_ID", "NAME"),
  region = "county:*",
  NAICS2017 = "00"  # 00 = total across all industries
)

# Example 4: Establishments by size class
cbp_size <- getCensus(
  name = "cbp",
  vintage = 2023,
  vars = c("ESTAB", "EMP", "EMPSZES", "NAME"),
  region = "state:*",
  NAICS2017 = "54"  # Professional/technical services
)
```

### Direct API Calls in R

```r
library(httr)
library(jsonlite)

# Function to query CBP API
get_cbp_data <- function(year, variables, geography, filters = NULL, api_key = NULL) {
  base_url <- paste0("https://api.census.gov/data/", year, "/cbp")

  params <- list(
    get = paste(variables, collapse = ","),
    `for` = geography
  )

  if (!is.null(filters)) {
    params <- c(params, filters)
  }

  if (!is.null(api_key)) {
    params$key <- api_key
  }

  response <- GET(base_url, query = params)
  content <- content(response, "text", encoding = "UTF-8")
  data <- fromJSON(content)

  # Convert to data frame
  df <- as.data.frame(data[-1, ], stringsAsFactors = FALSE)
  colnames(df) <- data[1, ]

  return(df)
}

# Example usage
cbp_data <- get_cbp_data(
  year = 2023,
  variables = c("ESTAB", "EMP", "PAYANN", "NAME"),
  geography = "county:*",
  filters = list(NAICS2017 = "00")
)
```

### Processing Downloaded CSV Files

```r
library(readr)
library(dplyr)

# Read county-level CBP file
cbp_county <- read_csv(
  "cbp23co.txt",
  col_types = cols(
    FIPSTATE = col_character(),
    FIPSCTY = col_character(),
    NAICS = col_character(),
    EMPFLAG = col_character(),
    EMP = col_integer(),
    QP1 = col_integer(),
    AP = col_integer(),
    EST = col_integer(),
    N1_4 = col_integer(),
    N5_9 = col_integer(),
    N10_19 = col_integer(),
    N20_49 = col_integer(),
    N50_99 = col_integer(),
    N100_249 = col_integer(),
    N250_499 = col_integer(),
    N500_999 = col_integer(),
    N1000 = col_integer(),
    N1000_1 = col_integer(),
    N1000_2 = col_integer(),
    N1000_3 = col_integer(),
    N1000_4 = col_integer()
  )
)

# Create FIPS code
cbp_county <- cbp_county %>%
  mutate(
    FIPS = paste0(FIPSTATE, FIPSCTY),
    NAICS_2digit = substr(NAICS, 1, 2)
  )

# Filter to county totals (NAICS = "------")
county_totals <- cbp_county %>%
  filter(NAICS == "------") %>%
  select(FIPS, EST, EMP, QP1, AP, N1_4:N1000_4)

# Filter to specific industry
manufacturing <- cbp_county %>%
  filter(substr(NAICS, 1, 2) %in% c("31", "32", "33")) %>%
  group_by(FIPS) %>%
  summarise(
    mfg_establishments = sum(EST, na.rm = TRUE),
    mfg_employment = sum(EMP, na.rm = TRUE),
    mfg_payroll = sum(AP, na.rm = TRUE)
  )
```

---

## DATA QUALITY CONSIDERATIONS

### Suppression Rules

1. **Primary Suppression (Confidentiality):**
   - Fewer than 3 establishments in a cell
   - One establishment accounts for >80% of employment in a cell
   - Data marked with EMPFLAG (A-M ranges)

2. **Noise Infusion (2007-2021):**
   - Multiplicative noise applied to establishment-level data before aggregation
   - Noise flags (G/H/J) indicate magnitude of perturbation
   - Low noise (G): <2% change
   - Medium noise (H): 2-5% change
   - High noise (J): ≥5% change

3. **Differential Privacy (2022+):**
   - Two-component approach:
     - Per-record differential privacy (formal guarantee)
     - Second-stage noise (relative protection for large establishments)
   - Provides mathematically provable privacy guarantees
   - Demonstration tables released April 2023

### Coverage Limitations

- **Excludes:**
  - Self-employed individuals
  - Employees of private households
  - Railroad employees
  - Agricultural production employees
  - Most government employees

- **Includes:**
  - ~98% of private nonfarm employment
  - All establishments with paid employees
  - Business establishments with or without payroll

### Geographic Coverage

- **50 states + DC:** Complete coverage
- **Puerto Rico:** Available
- **Island Areas:** Available
- **County-level:** All 3,000+ counties
- **ZIP Code:** All active ZIP codes
- **Metro Areas:** All CBSAs and CSAs

### NAICS Coverage at County Level

- **Available:** 3-digit through 6-digit NAICS codes
- **Note:** Not all 6-digit codes available in all counties (due to suppression)
- **Total Codes:** ~1,000+ 6-digit NAICS industries

---

# PART 2: QUARTERLY CENSUS OF EMPLOYMENT AND WAGES (QCEW)

## OVERVIEW

The Quarterly Census of Employment and Wages (QCEW) is a comprehensive dataset published by the U.S. Bureau of Labor Statistics (BLS) that provides detailed quarterly and annual employment and wage data for workers covered by state Unemployment Insurance (UI) laws and Unemployment Compensation for Federal Employees (UCFE) program.

**Data Coverage:** 98%+ of all U.S. employment
**Frequency:** Quarterly (Q1-Q4) + Annual Averages
**Geographic Levels:** National, State, County, Metropolitan/Micropolitan Statistical Area
**Industry Detail:** 2- through 6-digit NAICS codes
**Ownership Sectors:** Total, Private, Federal, State, Local Government

---

## COMPLETE VARIABLE DOCUMENTATION

### Quarterly CSV File Fields (47 Total Fields)

#### Core Identification Fields (1-8)

| Field # | Variable Name | Description | Format | Notes |
|---------|--------------|-------------|--------|-------|
| 1 | **area_fips** | Area (county) FIPS code | 5-char string | SS CCC format |
| 2 | **own_code** | Ownership code | 1-char string | 0-5 (see ownership table) |
| 3 | **industry_code** | NAICS industry code | 6-char string | 10 = total, 6-digit NAICS |
| 4 | **agglvl_code** | Aggregation level code | 2-char string | See aggregation table |
| 5 | **size_code** | Establishment size class | 1-char string | 0-9 (see size table) |
| 6 | **year** | Year | 4-char string | YYYY |
| 7 | **qtr** | Quarter | 1-char string | 1-4 |
| 8 | **disclosure_code** | Confidentiality flag | 1-char string | Blank or N (suppressed) |

#### Title/Label Fields (9-13) - Excluded from singlefile downloads

| Field # | Variable Name | Description |
|---------|--------------|-------------|
| 9 | **area_title** | Area name |
| 10 | **own_title** | Ownership sector name |
| 11 | **industry_title** | Industry description |
| 12 | **agglvl_title** | Aggregation level description |
| 13 | **size_title** | Size class description |

#### Primary Quarterly Metrics (14-21)

| Field # | Variable Name | Description | Units | Max Length |
|---------|--------------|-------------|-------|------------|
| 14 | **qtrly_estabs** | Quarterly establishment count | Count | 8 digits |
| 15 | **month1_emplvl** | Employment level, first month | Count | 9 digits |
| 16 | **month2_emplvl** | Employment level, second month | Count | 9 digits |
| 17 | **month3_emplvl** | Employment level, third month | Count | 9 digits |
| 18 | **total_qtrly_wages** | Total quarterly wages | Dollars | 15 digits |
| 19 | **taxable_qtrly_wages** | Taxable quarterly wages | Dollars | 15 digits |
| 20 | **qtrly_contributions** | Quarterly UI contributions | Dollars | 13 digits |
| 21 | **avg_wkly_wage** | Average weekly wage | Dollars | 8 digits |

**Monthly Employment Mapping:**
- **Q1:** month1 = Jan, month2 = Feb, month3 = Mar
- **Q2:** month1 = Apr, month2 = May, month3 = Jun
- **Q3:** month1 = Jul, month2 = Aug, month3 = Sep
- **Q4:** month1 = Oct, month2 = Nov, month3 = Dec

#### Location Quotient Fields (22-30)

Location quotients compare regional data to U.S. benchmarks (rounded to hundredths).

| Field # | Variable Name | Description |
|---------|--------------|-------------|
| 22 | **lq_disclosure_code** | LQ confidentiality flag |
| 23 | **lq_qtrly_estabs** | LQ for establishments |
| 24 | **lq_month1_emplvl** | LQ for month 1 employment |
| 25 | **lq_month2_emplvl** | LQ for month 2 employment |
| 26 | **lq_month3_emplvl** | LQ for month 3 employment |
| 27 | **lq_total_qtrly_wages** | LQ for total wages |
| 28 | **lq_taxable_qtrly_wages** | LQ for taxable wages |
| 29 | **lq_qtrly_contributions** | LQ for contributions |
| 30 | **lq_avg_wkly_wage** | LQ for average weekly wage |

**Location Quotient Interpretation:**
- LQ > 1.0: Higher concentration than national average
- LQ = 1.0: Same as national average
- LQ < 1.0: Lower concentration than national average

#### Over-the-Year (OTY) Change Fields (31-47)

Compares current quarter to same quarter one year prior.

| Field # | Variable Name | Description | Units |
|---------|--------------|-------------|-------|
| 31 | **oty_disclosure_code** | OTY confidentiality flag | Flag |
| 32 | **oty_qtrly_estabs_chg** | Change in establishments | Count |
| 33 | **oty_qtrly_estabs_pct_chg** | Percent change in establishments | Percent |
| 34 | **oty_month1_emplvl_chg** | Change in month 1 employment | Count |
| 35 | **oty_month1_emplvl_pct_chg** | Percent change, month 1 employment | Percent |
| 36 | **oty_month2_emplvl_chg** | Change in month 2 employment | Count |
| 37 | **oty_month2_emplvl_pct_chg** | Percent change, month 2 employment | Percent |
| 38 | **oty_month3_emplvl_chg** | Change in month 3 employment | Count |
| 39 | **oty_month3_emplvl_pct_chg** | Percent change, month 3 employment | Percent |
| 40 | **oty_total_qtrly_wages_chg** | Change in total wages | Dollars |
| 41 | **oty_total_qtrly_wages_pct_chg** | Percent change, total wages | Percent |
| 42 | **oty_taxable_qtrly_wages_chg** | Change in taxable wages | Dollars |
| 43 | **oty_taxable_qtrly_wages_pct_chg** | Percent change, taxable wages | Percent |
| 44 | **oty_qtrly_contributions_chg** | Change in contributions | Dollars |
| 45 | **oty_qtrly_contributions_pct_chg** | Percent change, contributions | Percent |
| 46 | **oty_avg_wkly_wage_chg** | Change in average weekly wage | Dollars |
| 47 | **oty_avg_wkly_wage_pct_chg** | Percent change, avg weekly wage | Percent |

### Annual CSV File Fields (43 Total Fields)

#### Core Identification Fields (1-8)

Same as quarterly, except:
- Field 7: **year** (no quarter field in annual files)

#### Primary Annual Metrics (14-20)

| Field # | Variable Name | Description | Units |
|---------|--------------|-------------|-------|
| 14 | **annual_avg_estabs** | Annual average establishments | Count |
| 15 | **annual_avg_emplvl** | Annual average employment | Count |
| 16 | **total_annual_wages** | Sum of 4 quarters' wages | Dollars |
| 17 | **taxable_annual_wages** | Sum of 4 quarters' taxable wages | Dollars |
| 18 | **annual_contributions** | Sum of 4 quarters' contributions | Dollars |
| 19 | **annual_avg_wkly_wage** | Average weekly wage (annual) | Dollars |
| 20 | **avg_annual_pay** | Average annual pay per employee | Dollars |

**Calculation Notes:**
- `annual_avg_emplvl` = Average of 12 monthly employment levels
- `total_annual_wages` = Sum of 4 quarterly wage totals
- `avg_annual_pay` = total_annual_wages / annual_avg_emplvl

#### Location Quotient Fields (22-28)

| Field # | Variable Name | Description |
|---------|--------------|-------------|
| 22 | **lq_disclosure_code** | LQ confidentiality flag |
| 23 | **lq_annual_avg_estabs** | LQ for establishments |
| 24 | **lq_annual_avg_emplvl** | LQ for employment |
| 25 | **lq_total_annual_wages** | LQ for total wages |
| 26 | **lq_taxable_annual_wages** | LQ for taxable wages |
| 27 | **lq_annual_contributions** | LQ for contributions |
| 28 | **lq_annual_avg_wkly_wage** | LQ for weekly wage |

#### Over-the-Year (OTY) Change Fields (30-43)

| Field # | Variable Name | Description |
|---------|--------------|-------------|
| 30 | **oty_disclosure_code** | OTY confidentiality flag |
| 31 | **oty_annual_avg_estabs_chg** | Change in establishments |
| 32 | **oty_annual_avg_estabs_pct_chg** | Percent change, establishments |
| 33 | **oty_annual_avg_emplvl_chg** | Change in employment |
| 34 | **oty_annual_avg_emplvl_pct_chg** | Percent change, employment |
| 35 | **oty_total_annual_wages_chg** | Change in total wages |
| 36 | **oty_total_annual_wages_pct_chg** | Percent change, total wages |
| 37 | **oty_taxable_annual_wages_chg** | Change in taxable wages |
| 38 | **oty_taxable_annual_wages_pct_chg** | Percent change, taxable wages |
| 39 | **oty_annual_contributions_chg** | Change in contributions |
| 40 | **oty_annual_contributions_pct_chg** | Percent change, contributions |
| 41 | **oty_annual_avg_wkly_wage_chg** | Change in weekly wage |
| 42 | **oty_annual_avg_wkly_wage_pct_chg** | Percent change, weekly wage |
| 43 | **oty_avg_annual_pay_chg** | Change in annual pay |

---

## CODE TABLES

### Ownership Codes (own_code)

| Code | Description | Scope |
|------|-------------|-------|
| **0** | Total, all ownerships | All establishments |
| **1** | Federal government | Federal agencies |
| **2** | State government | State agencies, universities |
| **3** | Local government | Counties, cities, school districts |
| **4** | International government | Discontinued after 1994 |
| **5** | Private sector | All privately owned firms |

**Note:** Code 4 (International government) was discontinued after 1994; these establishments are now included in private sector (code 5) starting in 1995.

### Establishment Size Codes (size_code)

| Code | Employment Range | Notes |
|------|-----------------|-------|
| **0 or blank** | All establishment sizes | Total across all sizes |
| **1** | Fewer than 5 employees | 1-4 employees |
| **2** | 5-9 employees | |
| **3** | 10-19 employees | |
| **4** | 20-49 employees | |
| **5** | 50-99 employees | |
| **6** | 100-249 employees | |
| **7** | 250-499 employees | |
| **8** | 500-999 employees | |
| **9** | 1,000 or more employees | |

**Important:** Size data available only for Q1 (first quarter) of each year. Size class determined by March employment level.

### Aggregation Level Codes (agglvl_code) - County Level

Codes starting with "7" indicate county-level data:

| Code | Description |
|------|-------------|
| **70** | County, Total Covered |
| **71** | County, Total by ownership sector |
| **72** | County, by Domain by ownership sector |
| **73** | County, by Supersector by ownership sector |
| **74** | County, NAICS Sector (2-digit) by ownership |
| **75** | County, NAICS 3-digit by ownership |
| **76** | County, NAICS 4-digit by ownership |
| **77** | County, NAICS 5-digit by ownership |
| **78** | County, NAICS 6-digit by ownership |

**Usage Example:**
- For county totals across all industries: `agglvl_code = 71`
- For county-level 6-digit NAICS detail: `agglvl_code = 78`

### Area Codes (area_fips)

**Format:** 5-character string (SSCCC)
- SS = 2-digit state FIPS code
- CCC = 3-digit county FIPS code

**Examples:**
- `47037` = Davidson County, Tennessee (47 = TN, 037 = Davidson)
- `06037` = Los Angeles County, California (06 = CA, 037 = Los Angeles)
- `01000` = Alabama statewide (000 substitutes for county in statewide records)

**Complete List:** https://www.bls.gov/cew/classifications/areas/qcew-area-titles.htm

**Note:** Connecticut introduced new county geographies based on Planning Regions in 2022, effective with 2024 data.

### Industry Codes (industry_code)

**Special Codes:**
- `10` = Total, all industries
- `1011` = Goods-producing domain
- `1012` = Service-providing domain
- `1013` = Unclassified

**NAICS Codes:**
- 2-digit (sector): `31`, `52`, `72`, etc.
- 3-digit (subsector): `311`, `523`, `722`, etc.
- 4-digit (industry group): `3111`, `5231`, `7223`, etc.
- 5-digit (NAICS industry): `31111`, `52311`, `72231`, etc.
- 6-digit (national industry): `311111`, `523110`, `722310`, etc.

**Complete List:** https://www.bls.gov/cew/classifications/industry/industry-titles.htm

### Disclosure Codes

| Code | Description |
|------|-------------|
| **(blank)** | Data available; no suppression |
| **N** | Data suppressed for confidentiality |

**Suppression Rules:**
1. **Fewer than 3 establishments** in a cell
2. **One establishment accounts for >80%** of employment (80/3 rule)
3. **Secondary suppression** to prevent calculation of primary suppressions
4. **State request** for additional protection

**Extent:** Approximately 60% of most detailed data suppressed for confidentiality.

---

## YEARS AND QUARTERS AVAILABLE

### Historical Coverage

- **1990-present:** Complete NAICS-based data
- **Earlier data:** SIC-based data available back to 1975

### Most Recent Data (as of November 2025)

- **Latest Full Database:** Q3 2024 (through September 2024)
- **Latest County Release:** Q1 2025 (preliminary county-level data)
- **Next Release:** Q2 2025 scheduled for December 3, 2025

### Release Schedule for 2025

| Quarter | Data Period | Release Date |
|---------|-------------|--------------|
| Q4 2024 | Oct-Dec 2024 | June 4, 2025 |
| Q1 2025 | Jan-Mar 2025 | September 3, 2025 |
| Q2 2025 | Apr-Jun 2025 | December 3, 2025 |
| Q3 2025 | Jul-Sep 2025 | March 2026 (est.) |
| Q4 2025 | Oct-Dec 2025 | June 2026 (est.) |

**Important Change (2025):** Beginning with Q4 2024 data (released June 4, 2025), the news release and full data update publish on the same date (previously staggered).

**General Timeline:** Data released approximately 6-7 months after quarter end.

**Release Calendar:** https://www.bls.gov/cew/release-calendar.htm

---

## DATA ACCESS METHODS

### 1. BLS Open Data - CSV Direct Downloads

**Best for:** Bulk county-level data, programmatic access

#### URL Pattern for County Data (Area Slice)

```
https://data.bls.gov/cew/data/api/{YEAR}/{QUARTER}/area/{AREA_CODE}.csv
```

**Parameters:**
- `{YEAR}` = 4-digit year (e.g., 2024)
- `{QUARTER}` = 1, 2, 3, or 4
- `{AREA_CODE}` = 5-digit FIPS code (SSCCC)

**Examples:**

```
# Los Angeles County, CA - Q1 2024
https://data.bls.gov/cew/data/api/2024/1/area/06037.csv

# Davidson County, TN (Nashville) - Q3 2024
https://data.bls.gov/cew/data/api/2024/3/area/47037.csv

# California statewide - Q2 2024
https://data.bls.gov/cew/data/api/2024/2/area/06000.csv

# All U.S. (national) - Q4 2023
https://data.bls.gov/cew/data/api/2023/4/area/US000.csv
```

**Coverage:** Most recent 5 years available via this method.

#### URL Pattern for Industry Slice

```
https://data.bls.gov/cew/data/api/{YEAR}/{QUARTER}/industry/{INDUSTRY_CODE}.csv
```

**Example:**
```
# All areas, construction industry (NAICS 23), Q1 2024
https://data.bls.gov/cew/data/api/2024/1/industry/23.csv
```

#### URL Pattern for Size Class Slice

```
https://data.bls.gov/cew/data/api/{YEAR}/1/size/{SIZE_CODE}.csv
```

**Note:** Size data available only for Q1 each year.

**Example:**
```
# All areas, establishments with 500-999 employees, Q1 2024
https://data.bls.gov/cew/data/api/2024/1/size/8.csv
```

### 2. QCEW Data Files (Bulk Downloads)

**Location:** https://www.bls.gov/cew/downloadable-data-files.htm

**File Types:**

1. **Quarterly CSV Files:**
   - By area: `{YEAR}.q1-q4.by_area.zip`
   - By industry: `{YEAR}.q1-q4.by_industry.zip`
   - By size: `{YEAR}.q1.by_size.zip` (Q1 only)
   - Singlefile: `{YEAR}.q1-q4.singlefile.zip`

2. **Annual CSV Files:**
   - By area: `{YEAR}.annual.by_area.zip`
   - By industry: `{YEAR}.annual.by_industry.zip`
   - Singlefile: `{YEAR}.annual.singlefile.zip`

**Download Example:**
```
https://data.bls.gov/cew/data/files/{YEAR}/csv/{YEAR}_qtrly_by_area.zip
```

### 3. QCEW Data Viewer (Interactive Query Tool)

**URL:** https://data.bls.gov/cew/apps/data_views/data_views.htm

**Features:**
- Point-and-click interface
- Filter by area, industry, ownership, size
- Export to Excel or CSV
- View time series charts

**Best for:** Ad-hoc queries, small datasets, exploration

### 4. BLS Public Data API (Series ID Based)

**Base URL:** `https://api.bls.gov/publicAPI/v2/timeseries/data/`

**Note:** QCEW data accessible through BLS API using series IDs. Series ID construction is complex; see BLS documentation.

**Example Series ID Format:**
```
ENU[AREA][OWNERSHIP][INDUSTRY][DATATYPE]
```

**Registration:** https://data.bls.gov/registrationEngine/ (increases query limits)

---

## R PACKAGE ACCESS

### Using Direct CSV Downloads

```r
library(readr)
library(dplyr)
library(httr)

# Function to download QCEW data for a specific county and quarter
get_qcew_county <- function(year, quarter, county_fips) {
  url <- paste0(
    "https://data.bls.gov/cew/data/api/",
    year, "/", quarter, "/area/", county_fips, ".csv"
  )

  data <- read_csv(url, col_types = cols(.default = "c"))

  # Convert numeric columns
  numeric_cols <- c(
    "qtrly_estabs", "month1_emplvl", "month2_emplvl", "month3_emplvl",
    "total_qtrly_wages", "taxable_qtrly_wages", "qtrly_contributions",
    "avg_wkly_wage", "lq_qtrly_estabs", "lq_month1_emplvl",
    "lq_month2_emplvl", "lq_month3_emplvl", "lq_total_qtrly_wages",
    "lq_taxable_qtrly_wages", "lq_qtrly_contributions", "lq_avg_wkly_wage",
    "oty_qtrly_estabs_chg", "oty_qtrly_estabs_pct_chg",
    "oty_month1_emplvl_chg", "oty_month1_emplvl_pct_chg",
    "oty_month2_emplvl_chg", "oty_month2_emplvl_pct_chg",
    "oty_month3_emplvl_chg", "oty_month3_emplvl_pct_chg",
    "oty_total_qtrly_wages_chg", "oty_total_qtrly_wages_pct_chg",
    "oty_taxable_qtrly_wages_chg", "oty_taxable_qtrly_wages_pct_chg",
    "oty_qtrly_contributions_chg", "oty_qtrly_contributions_pct_chg",
    "oty_avg_wkly_wage_chg", "oty_avg_wkly_wage_pct_chg"
  )

  data <- data %>%
    mutate(across(all_of(numeric_cols), as.numeric))

  return(data)
}

# Example usage
la_county_q1_2024 <- get_qcew_county(2024, 1, "06037")

# Filter to county totals (all industries, private sector)
la_totals <- la_county_q1_2024 %>%
  filter(
    own_code == "5",        # Private sector
    industry_code == "10",  # Total all industries
    agglvl_code == "71"     # County total by ownership
  ) %>%
  select(
    area_fips, year, qtr, qtrly_estabs, month1_emplvl,
    month2_emplvl, month3_emplvl, total_qtrly_wages, avg_wkly_wage
  )

# Filter to specific industry (e.g., professional services, NAICS 54)
la_prof_services <- la_county_q1_2024 %>%
  filter(
    own_code == "5",
    substr(industry_code, 1, 2) == "54",
    agglvl_code %in% c("75", "76", "77", "78")  # 3-6 digit NAICS
  ) %>%
  select(
    industry_code, industry_title, agglvl_code,
    qtrly_estabs, month3_emplvl, avg_wkly_wage
  ) %>%
  arrange(industry_code)
```

### Downloading Multiple Counties/Quarters

```r
# Function to download multiple quarters for a county
get_qcew_county_timeseries <- function(county_fips, start_year, end_year) {

  data_list <- list()

  for (year in start_year:end_year) {
    for (quarter in 1:4) {
      tryCatch({
        cat("Downloading", county_fips, year, "Q", quarter, "\n")

        data <- get_qcew_county(year, quarter, county_fips)
        data_list[[paste0(year, "_Q", quarter)]] <- data

        Sys.sleep(1)  # Be nice to BLS servers

      }, error = function(e) {
        cat("Error downloading", year, "Q", quarter, ":", e$message, "\n")
      })
    }
  }

  combined_data <- bind_rows(data_list)
  return(combined_data)
}

# Example: Get 2020-2024 data for Los Angeles County
la_timeseries <- get_qcew_county_timeseries("06037", 2020, 2024)

# Analyze employment trends in tech sector
la_tech_trends <- la_timeseries %>%
  filter(
    own_code == "5",
    industry_code == "51",  # Information sector
    agglvl_code == "74"     # Sector level
  ) %>%
  select(year, qtr, month3_emplvl, avg_wkly_wage, oty_month3_emplvl_pct_chg) %>%
  arrange(year, qtr)
```

### Using Annual Data

```r
# Function to download annual QCEW data
get_qcew_county_annual <- function(year, county_fips) {
  # Note: For annual data, use annual-specific API or download files
  # Annual CSV files available from:
  # https://data.bls.gov/cew/data/files/{YEAR}/csv/{YEAR}_annual_by_area.zip

  # For demonstration, showing structure
  url <- paste0(
    "https://data.bls.gov/cew/data/files/", year,
    "/csv/", year, "_annual_by_area.zip"
  )

  temp_zip <- tempfile(fileext = ".zip")
  temp_dir <- tempdir()

  download.file(url, temp_zip, mode = "wb")
  unzip(temp_zip, exdir = temp_dir)

  # Find CSV file
  csv_file <- list.files(temp_dir, pattern = "\\.csv$", full.names = TRUE)[1]

  data <- read_csv(csv_file, col_types = cols(.default = "c")) %>%
    filter(area_fips == county_fips)

  # Convert numeric columns
  numeric_cols <- c(
    "annual_avg_estabs", "annual_avg_emplvl", "total_annual_wages",
    "taxable_annual_wages", "annual_contributions", "annual_avg_wkly_wage",
    "avg_annual_pay", starts_with("lq_"), starts_with("oty_")
  )

  data <- data %>%
    mutate(across(matches(paste(numeric_cols, collapse = "|")), as.numeric))

  return(data)
}

# Example usage
la_annual_2023 <- get_qcew_county_annual(2023, "06037")

# County totals with average annual pay
la_annual_summary <- la_annual_2023 %>%
  filter(
    own_code == "5",
    industry_code == "10",
    agglvl_code == "71"
  ) %>%
  select(
    area_fips, year, annual_avg_estabs, annual_avg_emplvl,
    total_annual_wages, avg_annual_pay
  )
```

### Processing All Counties

```r
library(tidyr)

# Get county FIPS codes (simplified example)
county_fips <- c("06037", "36061", "17031", "47037", "48201")  # LA, NY, Cook, Davidson, Harris

# Download Q1 2024 data for multiple counties
county_data_list <- lapply(county_fips, function(fips) {
  cat("Processing", fips, "\n")
  get_qcew_county(2024, 1, fips)
})

all_counties <- bind_rows(county_data_list)

# Create county comparison of total private employment
county_comparison <- all_counties %>%
  filter(
    own_code == "5",
    industry_code == "10",
    agglvl_code == "71"
  ) %>%
  select(
    area_fips, area_title, qtrly_estabs, month3_emplvl,
    total_qtrly_wages, avg_wkly_wage, oty_month3_emplvl_pct_chg
  ) %>%
  mutate(
    avg_qtrly_wage_per_emp = total_qtrly_wages / month3_emplvl
  ) %>%
  arrange(desc(month3_emplvl))
```

### Using `blsAPI` Package (Series ID Method)

```r
# Install if needed
# install.packages("blsAPI")

library(blsAPI)
library(rjson)

# Note: QCEW series IDs are complex
# Format: ENU[AREA][OWNERSHIP][INDUSTRY][DATATYPE]
# Example: ENU0608510010 = CA, Private, Software Publishing, Establishments

# Register for API key at https://data.bls.gov/registrationEngine/
# Increases limit from 25 to 500 queries per day

# Example query (requires valid series ID)
series_id <- "ENU0608510010"
bls_data <- blsAPI(series_id, startyear = 2020, endyear = 2024)
bls_json <- fromJSON(bls_data)

# Convert to data frame (structure varies)
# Note: Direct CSV download method recommended for QCEW over series ID method
```

---

## DATA QUALITY CONSIDERATIONS

### Suppression and Confidentiality

1. **Primary Suppression (80/3 Rule):**
   - Fewer than 3 establishments in a cell
   - One establishment accounts for >80% of employment
   - Marked with `disclosure_code = "N"`

2. **Secondary Suppression:**
   - Additional cells suppressed to prevent calculation of primary suppressions
   - Especially important in MSAs with multiple counties

3. **Extent of Suppression:**
   - Approximately 60% of most detailed level data suppressed
   - More suppression at finer geographic/industry detail
   - Less suppression at aggregate levels

4. **Confidentiality Protection:**
   - Based on Federal CIPSEA (2002) requirements
   - Methodology not disclosed to prevent reverse engineering
   - Data acquired under pledge of confidentiality to employers

### Coverage and Limitations

**Covered:**
- 98%+ of all U.S. employment
- All workers covered by state UI laws
- Federal employees (UCFE program)
- All 50 states + DC + PR + USVI

**Excluded:**
- Self-employed
- Unpaid family workers
- Railroad employees (covered under separate system)
- Some agricultural workers
- Elected officials in most states
- Students employed by schools

### Data Revisions

- **Preliminary Data:** Initial release
- **Revised Data:** First revision approximately 6 months after initial release
- **Final Data:** Typically finalized within 12-18 months
- **Revision Schedule:** Published at https://www.bls.gov/cew/revisions/

### Geographic Coverage

- **National:** Complete
- **State:** All 50 states + DC
- **County:** All 3,000+ counties
- **Metropolitan Areas:** All CBSAs (Core-Based Statistical Areas)
- **Puerto Rico & USVI:** Available

**Note:** Connecticut changed county definitions in 2024 to align with Planning Regions.

### Size Class Data

- **Availability:** First quarter (Q1) only each year
- **Determination:** Based on March employment level
- **Size Classes:** 9 classes from <5 to 1,000+ employees
- **Uses:** Establishment size distribution analysis

---

# NAICS INDUSTRY CLASSIFICATION

## NAICS 2017 Structure

The North American Industry Classification System (NAICS) is a hierarchical system providing 5 levels of detail:

- **2-digit:** Sector (20 sectors)
- **3-digit:** Subsector
- **4-digit:** Industry Group
- **5-digit:** NAICS Industry (comparable US/Canada/Mexico)
- **6-digit:** National (U.S.) Industry (most detailed)

## Complete NAICS 2017 Sector List (2-Digit Codes)

| Code | Sector Name |
|------|-------------|
| **11** | Agriculture, Forestry, Fishing and Hunting |
| **21** | Mining, Quarrying, and Oil and Gas Extraction |
| **22** | Utilities |
| **23** | Construction |
| **31-33** | Manufacturing |
| **42** | Wholesale Trade |
| **44-45** | Retail Trade |
| **48-49** | Transportation and Warehousing |
| **51** | Information |
| **52** | Finance and Insurance |
| **53** | Real Estate and Rental and Leasing |
| **54** | Professional, Scientific, and Technical Services |
| **55** | Management of Companies and Enterprises |
| **56** | Administrative and Support and Waste Management and Remediation Services |
| **61** | Educational Services |
| **62** | Health Care and Social Assistance |
| **71** | Arts, Entertainment, and Recreation |
| **72** | Accommodation and Food Services |
| **81** | Other Services (except Public Administration) |
| **92** | Public Administration |

**Notes:**
- Manufacturing (31-33), Retail Trade (44-45), and Transportation (48-49) use combined 2-digit ranges
- All sectors except 11 and 92 are covered by Economic Census
- NAICS 2017 is current classification (effective 2017)

## Industry Detail Available at County Level

### CBP (County Business Patterns)

- **Available:** 3-digit through 6-digit NAICS
- **Note:** 2-digit (sector) available through aggregation
- **Suppression:** Many 6-digit codes suppressed in small counties

### QCEW (Quarterly Census of Employment and Wages)

- **Available:** All levels (2-digit through 6-digit)
- **Aggregation codes:** 74-78 for county-level industry detail
- **Suppression:** Significant suppression at detailed levels

## High-Level QCEW Industry Aggregations

### Domains (2 categories)

- **1011:** Goods-producing
- **1012:** Service-providing

### Supersectors (10 BLS-defined aggregations)

| Code | Supersector |
|------|-------------|
| **101** | Total, all industries |
| **102** | Goods-producing |
| **103** | Service-providing |
| **1021** | Natural resources and mining |
| **1022** | Construction |
| **1023** | Manufacturing |
| **1024** | Trade, transportation, and utilities |
| **1025** | Information |
| **1026** | Financial activities |
| **1027** | Professional and business services |
| **1028** | Education and health services |
| **1029** | Leisure and hospitality |
| **1030** | Other services |
| **1031** | Public administration |

## Example NAICS Hierarchy: Food Services

```
72 - Accommodation and Food Services (Sector, 2-digit)
  722 - Food Services and Drinking Places (Subsector, 3-digit)
    7225 - Restaurants and Other Eating Places (Industry Group, 4-digit)
      72251 - Restaurants and Other Eating Places (NAICS Industry, 5-digit)
        722511 - Full-Service Restaurants (National Industry, 6-digit)
        722513 - Limited-Service Restaurants (National Industry, 6-digit)
        722514 - Cafeterias, Grill Buffets, and Buffets (National Industry, 6-digit)
        722515 - Snack and Nonalcoholic Beverage Bars (National Industry, 6-digit)
```

## Complete Industry Code Lists

- **NAICS Official:** https://www.census.gov/naics/
- **QCEW Industry Codes:** https://www.bls.gov/cew/classifications/industry/industry-titles.htm
- **Supersector Crosswalk:** https://www.bls.gov/cew/classifications/industry/high-level-industries.htm

---

# PRODUCTION-READY CODE EXAMPLES

## Example 1: Build Complete County × Year × Industry Panel (CBP)

```r
library(censusapi)
library(tidyverse)

# Set Census API key
Sys.setenv(CENSUS_KEY = "your_key_here")

# Function to get CBP data for all counties, specific year
get_cbp_all_counties <- function(year, naics_codes = "00") {

  cat("Downloading CBP", year, "data...\n")

  # Get data from API
  data <- getCensus(
    name = "cbp",
    vintage = year,
    vars = c("ESTAB", "EMP", "PAYQTR1", "PAYANN",
             "NAICS2017", "NAICS2017_LABEL", "GEO_ID", "NAME"),
    region = "county:*",
    NAICS2017 = naics_codes
  )

  # Add year column
  data$year <- year

  # Create FIPS code
  data <- data %>%
    mutate(
      fips = paste0(state, county),
      estab = as.numeric(ESTAB),
      emp = as.numeric(EMP),
      payqtr1 = as.numeric(PAYQTR1),
      payann = as.numeric(PAYANN)
    ) %>%
    select(
      fips, year, naics = NAICS2017, naics_label = NAICS2017_LABEL,
      estab, emp, payqtr1, payann, name = NAME
    )

  return(data)
}

# Download multiple years
years <- 2019:2023
cbp_panel <- map_df(years, ~get_cbp_all_counties(.x, "00"))

# Save to CSV
write_csv(cbp_panel, "cbp_county_totals_2019_2023.csv")

# Get specific industries across years
industries <- c("23", "42", "54", "62", "72")  # Construction, Wholesale, Prof Services, Healthcare, Food Services
industry_names <- c("Construction", "Wholesale", "Professional", "Healthcare", "Food Services")

cbp_industries <- map2_df(
  rep(years, each = length(industries)),
  rep(industries, times = length(years)),
  ~get_cbp_all_counties(.x, .y)
)

# Add industry category
cbp_industries <- cbp_industries %>%
  mutate(
    industry_category = case_when(
      substr(naics, 1, 2) == "23" ~ "Construction",
      substr(naics, 1, 2) == "42" ~ "Wholesale",
      substr(naics, 1, 2) == "54" ~ "Professional",
      substr(naics, 1, 2) == "62" ~ "Healthcare",
      substr(naics, 1, 2) == "72" ~ "Food Services",
      TRUE ~ "Other"
    )
  )

write_csv(cbp_industries, "cbp_county_industries_2019_2023.csv")
```

## Example 2: Calculate Industry Concentration Metrics (CBP)

```r
library(tidyverse)

# Assuming cbp_data loaded with county × industry data

# Calculate location quotients manually
cbp_lq <- cbp_data %>%
  # Get county totals
  left_join(
    cbp_data %>%
      filter(naics == "00") %>%
      select(fips, year, county_total_emp = emp),
    by = c("fips", "year")
  ) %>%
  # Get national industry totals
  left_join(
    cbp_data %>%
      group_by(naics, year) %>%
      summarise(national_industry_emp = sum(emp, na.rm = TRUE), .groups = "drop"),
    by = c("naics", "year")
  ) %>%
  # Get national total
  left_join(
    cbp_data %>%
      filter(naics == "00") %>%
      group_by(year) %>%
      summarise(national_total_emp = sum(emp, na.rm = TRUE), .groups = "drop"),
    by = "year"
  ) %>%
  # Calculate LQ
  mutate(
    lq = (emp / county_total_emp) / (national_industry_emp / national_total_emp)
  ) %>%
  filter(naics != "00")  # Exclude totals

# Find counties with high concentration in tech (NAICS 51)
tech_clusters <- cbp_lq %>%
  filter(substr(naics, 1, 2) == "51", year == 2023) %>%
  arrange(desc(lq)) %>%
  select(fips, name, naics, naics_label, emp, lq) %>%
  head(20)

print(tech_clusters)

# Calculate Herfindahl-Hirschman Index (industry diversity)
hhi <- cbp_data %>%
  filter(naics != "00") %>%
  group_by(fips, year) %>%
  mutate(
    total_emp = sum(emp, na.rm = TRUE),
    emp_share = emp / total_emp,
    emp_share_sq = emp_share^2
  ) %>%
  summarise(
    hhi = sum(emp_share_sq, na.rm = TRUE),
    .groups = "drop"
  ) %>%
  mutate(
    diversity = 1 - hhi  # Higher = more diverse
  )

# Most and least diverse counties
most_diverse <- hhi %>% filter(year == 2023) %>% arrange(desc(diversity)) %>% head(10)
least_diverse <- hhi %>% filter(year == 2023) %>% arrange(diversity) %>% head(10)
```

## Example 3: Build Complete County × Quarter × Industry Panel (QCEW)

```r
library(tidyverse)

# Function to download QCEW for all counties in a state
get_qcew_state_quarter <- function(state_fips, year, quarter) {

  url <- paste0(
    "https://data.bls.gov/cew/data/api/",
    year, "/", quarter, "/area/", state_fips, "000.csv"
  )

  cat("Downloading", state_fips, year, "Q", quarter, "\n")

  tryCatch({
    data <- read_csv(url, col_types = cols(.default = "c"), show_col_types = FALSE)

    # Keep only county-level records
    data <- data %>%
      filter(
        substr(area_fips, 3, 5) != "000",  # Exclude statewide
        agglvl_code == "71",               # County totals by ownership
        own_code == "0"                    # All ownerships
      )

    return(data)

  }, error = function(e) {
    cat("Error:", e$message, "\n")
    return(NULL)
  })
}

# Download all California counties, 2023-2024
ca_counties <- map_df(
  expand.grid(year = 2023:2024, quarter = 1:4),
  ~get_qcew_state_quarter("06", .x$year, .x$quarter)
)

# Convert to numeric
ca_counties <- ca_counties %>%
  mutate(
    year = as.integer(year),
    qtr = as.integer(qtr),
    qtrly_estabs = as.numeric(qtrly_estabs),
    month1_emplvl = as.numeric(month1_emplvl),
    month2_emplvl = as.numeric(month2_emplvl),
    month3_emplvl = as.numeric(month3_emplvl),
    total_qtrly_wages = as.numeric(total_qtrly_wages),
    avg_wkly_wage = as.numeric(avg_wkly_wage)
  )

write_csv(ca_counties, "qcew_california_counties_2023_2024.csv")

# Calculate average quarterly employment
ca_counties <- ca_counties %>%
  mutate(
    avg_qtr_emp = (month1_emplvl + month2_emplvl + month3_emplvl) / 3
  )

# Time series plot for Los Angeles County
la_trend <- ca_counties %>%
  filter(area_fips == "06037") %>%
  arrange(year, qtr) %>%
  mutate(
    quarter_date = as.Date(paste0(year, "-", qtr*3, "-01"))
  )

library(ggplot2)
ggplot(la_trend, aes(x = quarter_date, y = month3_emplvl)) +
  geom_line(size = 1) +
  geom_point(size = 2) +
  labs(
    title = "Los Angeles County Employment Trend",
    x = "Quarter",
    y = "Employment (Month 3)",
    caption = "Source: BLS QCEW"
  ) +
  theme_minimal()
```

## Example 4: Merge CBP and QCEW Data

```r
library(tidyverse)

# CBP: Annual data (mid-March employment, annual payroll)
# QCEW: Quarterly data (monthly employment, quarterly wages)

# Strategy: Use QCEW Q1 (Jan-Mar) to match CBP timing

# Load CBP 2023
cbp_2023 <- read_csv("cbp_county_totals_2023.csv")

# Load QCEW Q1 2023 for all counties (assuming downloaded)
qcew_q1_2023 <- read_csv("qcew_all_counties_2023_q1.csv")

# Filter QCEW to county totals, private sector
qcew_summary <- qcew_q1_2023 %>%
  filter(
    agglvl_code == "71",
    own_code == "5",       # Private sector only (to match CBP coverage)
    industry_code == "10"
  ) %>%
  select(
    fips = area_fips,
    qcew_q1_estabs = qtrly_estabs,
    qcew_jan_emp = month1_emplvl,
    qcew_feb_emp = month2_emplvl,
    qcew_mar_emp = month3_emplvl,
    qcew_q1_wages = total_qtrly_wages,
    qcew_avg_wkly_wage = avg_wkly_wage
  ) %>%
  mutate(
    qcew_q1_avg_emp = (qcew_jan_emp + qcew_feb_emp + qcew_mar_emp) / 3
  )

# Merge CBP and QCEW
merged_data <- cbp_2023 %>%
  left_join(qcew_summary, by = "fips") %>%
  mutate(
    # Compare CBP (mid-March) to QCEW (March)
    emp_diff = emp - qcew_mar_emp,
    emp_diff_pct = (emp - qcew_mar_emp) / qcew_mar_emp * 100,

    # Compare establishment counts
    estab_diff = estab - qcew_q1_estabs,

    # Annualize QCEW wages for comparison
    qcew_annual_wages_est = qcew_q1_wages * 4,
    payroll_diff = payann - qcew_annual_wages_est
  )

# Examine discrepancies
discrepancies <- merged_data %>%
  filter(abs(emp_diff_pct) > 5) %>%  # >5% difference
  select(fips, name, emp, qcew_mar_emp, emp_diff, emp_diff_pct) %>%
  arrange(desc(abs(emp_diff_pct)))

print(discrepancies)

# Note: Some differences expected due to:
# 1. CBP includes some establishments without payroll
# 2. Timing differences (CBP = week of March 12, QCEW = month 3)
# 3. Different imputation methods for missing data
```

## Example 5: Industry Employment Shifts Over Time (QCEW)

```r
library(tidyverse)
library(lubridate)

# Function to get QCEW industry data for a county
get_county_industry_timeseries <- function(county_fips, start_year, end_year) {

  data_list <- list()

  for (year in start_year:end_year) {
    for (quarter in 1:4) {
      url <- paste0(
        "https://data.bls.gov/cew/data/api/",
        year, "/", quarter, "/area/", county_fips, ".csv"
      )

      tryCatch({
        data <- read_csv(url, col_types = cols(.default = "c"), show_col_types = FALSE)

        # Keep sector-level data (2-digit NAICS), private sector
        data <- data %>%
          filter(
            agglvl_code == "74",  # Sector level
            own_code == "5"       # Private sector
          )

        data_list[[paste0(year, "_Q", quarter)]] <- data

        Sys.sleep(0.5)  # Rate limiting

      }, error = function(e) {
        cat("Error:", year, "Q", quarter, "-", e$message, "\n")
      })
    }
  }

  combined <- bind_rows(data_list)
  return(combined)
}

# Get Nashville (Davidson County, TN) data 2019-2024
nashville_industries <- get_county_industry_timeseries("47037", 2019, 2024)

# Convert to numeric and process
nashville_clean <- nashville_industries %>%
  mutate(
    year = as.integer(year),
    qtr = as.integer(qtr),
    industry_code = as.character(industry_code),
    month3_emplvl = as.numeric(month3_emplvl),
    avg_wkly_wage = as.numeric(avg_wkly_wage),
    oty_month3_emplvl_pct_chg = as.numeric(oty_month3_emplvl_pct_chg)
  ) %>%
  mutate(
    quarter_date = ymd(paste0(year, "-", qtr*3, "-01"))
  )

# Calculate employment share by sector
nashville_shares <- nashville_clean %>%
  group_by(year, qtr) %>%
  mutate(
    total_emp = sum(month3_emplvl, na.rm = TRUE),
    emp_share = month3_emplvl / total_emp * 100
  ) %>%
  ungroup()

# Plot employment trends by major sectors
major_sectors <- c("23", "31", "42", "51", "54", "62", "72")
sector_names <- c(
  "23" = "Construction",
  "31" = "Manufacturing",
  "42" = "Wholesale Trade",
  "51" = "Information",
  "54" = "Professional Services",
  "62" = "Healthcare",
  "72" = "Food Services"
)

plot_data <- nashville_shares %>%
  filter(industry_code %in% major_sectors) %>%
  mutate(
    sector_name = recode(industry_code, !!!sector_names)
  )

ggplot(plot_data, aes(x = quarter_date, y = month3_emplvl, color = sector_name)) +
  geom_line(size = 1) +
  labs(
    title = "Nashville Employment by Industry (2019-2024)",
    x = "Quarter",
    y = "Employment",
    color = "Sector"
  ) +
  theme_minimal() +
  theme(legend.position = "bottom")

# Identify fastest growing/declining sectors
sector_growth <- nashville_clean %>%
  filter(year %in% c(2019, 2024), qtr == 2) %>%  # Q2 comparison
  select(industry_code, industry_title, year, month3_emplvl) %>%
  pivot_wider(names_from = year, values_from = month3_emplvl, names_prefix = "emp_") %>%
  mutate(
    employment_change = emp_2024 - emp_2019,
    pct_change = (emp_2024 - emp_2019) / emp_2019 * 100
  ) %>%
  arrange(desc(pct_change))

print(sector_growth)
```

## Example 6: Establishment Size Distribution Analysis (QCEW)

```r
library(tidyverse)

# Download Q1 2024 size data for all areas
# Note: Size data only available in Q1

url_size <- "https://data.bls.gov/cew/data/api/2024/1/size/0.csv"
size_data <- read_csv(url_size, col_types = cols(.default = "c"))

# Filter to county-level, private sector, total industry
county_size <- size_data %>%
  filter(
    substr(area_fips, 3, 5) != "000",  # Counties only
    own_code == "5",                   # Private sector
    industry_code == "10",             # Total all industries
    agglvl_code == "71"                # County level
  ) %>%
  mutate(
    across(c(qtrly_estabs, month1_emplvl, month2_emplvl,
             month3_emplvl, total_qtrly_wages), as.numeric)
  )

# Get size distribution for specific counties
top_counties <- c("06037", "36061", "17031", "48201", "04013")  # LA, NYC, Cook, Harris, Maricopa

county_size_dist <- size_data %>%
  filter(
    area_fips %in% top_counties,
    own_code == "5",
    industry_code == "10",
    agglvl_code == "71",
    size_code != "0"  # Exclude "all sizes"
  ) %>%
  mutate(
    qtrly_estabs = as.numeric(qtrly_estabs),
    month3_emplvl = as.numeric(month3_emplvl)
  ) %>%
  select(area_fips, area_title, size_code, size_title, qtrly_estabs, month3_emplvl)

# Calculate share of establishments and employment by size
size_analysis <- county_size_dist %>%
  group_by(area_fips, area_title) %>%
  mutate(
    estab_share = qtrly_estabs / sum(qtrly_estabs, na.rm = TRUE) * 100,
    emp_share = month3_emplvl / sum(month3_emplvl, na.rm = TRUE) * 100
  ) %>%
  ungroup()

# Visualize size distribution
ggplot(size_analysis, aes(x = size_title, y = estab_share, fill = area_title)) +
  geom_col(position = "dodge") +
  coord_flip() +
  labs(
    title = "Establishment Size Distribution by County (Q1 2024)",
    x = "Size Class",
    y = "Share of Establishments (%)",
    fill = "County"
  ) +
  theme_minimal()

# Compare establishment vs employment shares
size_comparison <- size_analysis %>%
  select(area_title, size_title, estab_share, emp_share) %>%
  pivot_longer(cols = c(estab_share, emp_share),
               names_to = "metric", values_to = "share") %>%
  mutate(
    metric = recode(metric,
                    estab_share = "Establishments",
                    emp_share = "Employment")
  )

ggplot(size_comparison %>% filter(area_title == "Los Angeles County, California"),
       aes(x = size_title, y = share, fill = metric)) +
  geom_col(position = "dodge") +
  coord_flip() +
  labs(
    title = "Los Angeles County: Establishments vs Employment by Size",
    x = "Size Class",
    y = "Share (%)",
    fill = "Metric"
  ) +
  theme_minimal()
```

## Example 7: Calculate County-Level Economic Indicators

```r
library(tidyverse)

# Combine CBP and QCEW to create comprehensive indicators

# Function to calculate economic indicators
calculate_county_indicators <- function(cbp_data, qcew_annual_data) {

  # Merge datasets
  county_econ <- cbp_data %>%
    left_join(
      qcew_annual_data %>%
        filter(
          agglvl_code == "71",
          own_code == "5",
          industry_code == "10"
        ) %>%
        select(
          fips = area_fips,
          year,
          qcew_annual_avg_emp = annual_avg_emplvl,
          qcew_total_annual_wages = total_annual_wages,
          qcew_avg_annual_pay = avg_annual_pay
        ),
      by = c("fips", "year")
    )

  # Calculate indicators
  indicators <- county_econ %>%
    mutate(
      # Establishment size
      avg_emp_per_estab = emp / estab,

      # Wage levels
      avg_annual_pay_cbp = (payann * 1000) / emp,  # CBP in thousands
      avg_quarterly_pay = (payqtr1 * 1000) / emp * 4,

      # Productivity proxy
      wages_per_estab = payann / estab,

      # Employment density (requires area data)
      # estab_per_capita = estab / population  # If population available
    )

  return(indicators)
}

# Load QCEW annual data (2023)
qcew_annual_2023 <- read_csv("qcew_annual_2023.csv")

# Calculate indicators
county_indicators_2023 <- calculate_county_indicators(cbp_2023, qcew_annual_2023)

# Rank counties by various metrics
top_wage_counties <- county_indicators_2023 %>%
  filter(!is.na(qcew_avg_annual_pay)) %>%
  arrange(desc(qcew_avg_annual_pay)) %>%
  select(name, emp, estab, qcew_avg_annual_pay, avg_emp_per_estab) %>%
  head(20)

print(top_wage_counties)

# Industry diversification using CBP industry detail
industry_diversity <- cbp_industries %>%
  filter(year == 2023) %>%
  group_by(fips) %>%
  summarise(
    n_industries = n(),
    total_emp = sum(emp, na.rm = TRUE),
    hhi = sum((emp / total_emp)^2, na.rm = TRUE),
    diversity_index = 1 - hhi,
    .groups = "drop"
  )

# Merge with county indicators
county_indicators_full <- county_indicators_2023 %>%
  left_join(industry_diversity, by = "fips")

# Export
write_csv(county_indicators_full, "county_economic_indicators_2023.csv")
```

---

## ADDITIONAL RESOURCES

### Official Documentation

**CBP:**
- Main Page: https://www.census.gov/programs-surveys/cbp.html
- API Documentation: https://www.census.gov/data/developers/data-sets/cbp-zbp/cbp-api.html
- Methodology: https://www.census.gov/programs-surveys/cbp/technical-documentation/methodology.html
- Glossary: https://www.census.gov/programs-surveys/cbp/about/glossary.html

**QCEW:**
- Main Page: https://www.bls.gov/cew/
- Data Files: https://www.bls.gov/cew/downloadable-data-files.htm
- Open Data Access: https://www.bls.gov/cew/additional-resources/open-data/
- Documentation Guide: https://www.bls.gov/cew/about-data/documentation-guide.htm
- Reporter's Guide: https://www.bls.gov/cew/publications/reporters-guide/

### Code and Reference Tables

**CBP:**
- NAICS 2017 Codes: https://www.census.gov/naics/
- Record Layouts: https://www.census.gov/programs-surveys/cbp/technical-documentation/record-layouts.html

**QCEW:**
- Area Codes: https://www.bls.gov/cew/classifications/areas/qcew-area-titles.htm
- Industry Codes: https://www.bls.gov/cew/classifications/industry/industry-titles.htm
- Ownership Codes: https://www.bls.gov/cew/classifications/ownerships/ownership-titles.htm
- Size Codes: https://www.bls.gov/cew/classifications/size/size-titles.htm
- Aggregation Codes: https://www.bls.gov/cew/classifications/aggregation/agg-level-titles.htm

### R Packages

- **censusapi:** https://cran.r-project.org/package=censusapi
- **blsAPI:** https://cran.r-project.org/package=blsAPI
- **tidyverse:** https://www.tidyverse.org/

### Related Datasets

- **ZIP Code Business Patterns (ZBP):** ZIP code level version of CBP
- **Nonemployer Statistics (NES):** Businesses without paid employees
- **County Employment and Wages (QCEW County News Release):** Subset of QCEW data
- **Business Dynamics Statistics (BDS):** Establishment births, deaths, job creation/destruction

---

## DATA CITATION

**County Business Patterns:**
```
U.S. Census Bureau. (2024). County Business Patterns: 2023 [Data file].
Retrieved from https://www.census.gov/programs-surveys/cbp/data/datasets.html
```

**QCEW:**
```
U.S. Bureau of Labor Statistics. (2025). Quarterly Census of Employment and Wages
[Data file]. Retrieved from https://www.bls.gov/cew/
```

---

## REVISION HISTORY

- **November 11, 2025:** Initial comprehensive documentation created
- Data status: CBP 2023 (latest), QCEW Q1 2025 (latest county release)

---

**END OF DOCUMENTATION**
