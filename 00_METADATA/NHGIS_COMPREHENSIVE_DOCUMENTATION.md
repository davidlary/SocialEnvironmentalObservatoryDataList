# IPUMS NHGIS - Comprehensive Documentation
## National Historical Geographic Information System

**⭐ PRIORITY DATA SOURCE ⭐**

NHGIS is **THE PREMIER SOURCE** for county-level demographic, social, economic, housing, and agricultural data. It provides **pre-harmonized, preprocessed data** that solves boundary change issues, making it the first choice for longitudinal county-level analysis.

**Coverage:** All 3,143 US Counties
**Temporal Range:** 1790-2024 (ACS 2024 1-year in processing, 2019-2023 5-year available)
**Total Time Series Tables:** 389
**Total ACS Tables:** 1,300-1,400+ per year
**Last Updated:** November 13, 2025

---

## 🎯 Why NHGIS is Critical

### 1. Pre-Harmonized Time Series
- **389 time series tables** with data already standardized across decades
- Handles county boundary changes automatically
- Consistent variable definitions across years
- No need for manual harmonization

### 2. Comprehensive Coverage
- **Longest time series:** Total Population (1790-2020, 230 years!)
- **100%-count data:** 1790-2020 Decennial Census
- **Sample-based data:** 1970-2000 Long Form + 2005-2023 ACS (2024 1-year in processing)
- **5-year ACS:** 2019-2023 available (provides estimates for all counties)
- **All geographic levels:** Nation → State → County → Tract → Block

### 3. Complete Variable Coverage
- **1,300+ ACS tables** annually (2005-2023, 2024 in processing)
- **ACS 5-year estimates:** 2019-2023 available for all counties
- **Decennial Census:** All summary files (SF1-SF4)
- **Agriculture Census:** 1840-1959
- **Vital Statistics:** Births/deaths 1915-2007, marriages/divorces 1867-2010
- **County Business Patterns:** 1970-2003
- **Religious Census:** 1850-1952

### 4. Production-Ready Data
- Clean, documented, standardized format
- FIPS codes consistent across years
- Codebooks and metadata included
- R and Python API access available

---

## 📊 Data Products Overview

### 1️⃣ Time Series Tables (PRIMARY RESOURCE)

**Total Tables:** 389 time series tables
**Two Types:**
1. **Nominally Integrated:** Link counties by name/code (boundaries may change)
2. **Geographically Standardized:** Normalize to 2010 boundaries (1990-2020)

**Coverage by Topic:**

#### Population & Demographics (100+ tables)
- **Total Population:** 1790-2020 (Table A00: longest time series!)
- **Sex:** 1820-2020 (male, female counts)
- **Age:** 1850-2020 (18+ age groups, median age)
- **Race:** 1790-2020 (OMB categories, detailed race groups)
- **Hispanic/Latino Origin:** 1970-2020
- **Urban/Rural:** 1840-2020
- **Place of Birth:** 1850-2020 (native, foreign-born by region)
- **Citizenship:** 1890-2020
- **Language:** 1890-2020 (spoken at home)
- **Ancestry:** 1980-2020
- **Migration:** 1940-2020 (moved in past year/5 years)

#### Household & Family (50+ tables)
- **Household Type:** 1940-2020 (family, nonfamily, group quarters)
- **Household Size:** 1850-2020
- **Family Type:** 1950-2020 (married couple, male/female householder)
- **Relationship to Householder:** 1940-2020
- **Marital Status:** 1880-2020
- **Fertility:** 1940-2020 (children ever born, births past year)
- **Grandparents as Caregivers:** 1990-2020

#### Education (30+ tables)
- **Educational Attainment:** 1940-2020 (highest degree, years completed)
- **School Enrollment:** 1850-2020 (by age, level)
- **College Enrollment:** 1990-2020 (graduate/professional school)

#### Economic Characteristics (80+ tables)
- **Employment Status:** 1940-2020 (labor force, employed, unemployed)
- **Occupation:** 1850-2020 (detailed occupational categories)
- **Industry:** 1940-2020 (NAICS codes)
- **Class of Worker:** 1940-2020 (private, government, self-employed)
- **Work Status:** 1970-2020 (full-time, part-time, weeks worked)
- **Income:** 1950-2020 (household, family, per capita, median, mean)
- **Poverty Status:** 1970-2020 (persons, families below poverty)
- **Journey to Work:** 1960-2020 (commute time, transportation mode)
- **Work From Home:** 1980-2020

#### Housing Characteristics (50+ tables)
- **Housing Units:** 1940-2020 (total, occupied, vacant)
- **Tenure:** 1890-2020 (owner, renter)
- **Occupancy:** 1940-2020 (occupied, vacant for rent/sale)
- **Value:** 1940-2020 (median, aggregate home value)
- **Gross Rent:** 1940-2020 (median, aggregate)
- **Rooms:** 1940-2020 (number of rooms, bedrooms)
- **Year Built:** 1940-2020
- **Utilities:** 1940-2020 (plumbing, heating, kitchen facilities)
- **Vehicles Available:** 1960-2020
- **Rent as % of Income:** 1990-2020
- **Mortgage Status:** 1990-2020

#### Veteran Status (10+ tables)
- **Veterans:** 1980-2020 (by age, sex, period of service)
- **Veteran Poverty:** 1990-2020

#### Disability Status (10+ tables)
- **Disability:** 1970-2020 (by type, age group)

#### Health Insurance (5+ tables)
- **Insurance Coverage:** 2009-2020 (type of coverage)

---

### 2️⃣ American Community Survey (ACS) Tables

**Availability:**
- **5-year estimates:** 2005-2009 through 2019-2023 (ALL counties)
- **1-year estimates:** 2005-2023 (counties >65,000 population only)

**Total Tables per Year:** 1,300-1,400+ tables

**Subject Areas (Detailed Breakdown):**

#### People
- **Age and Sex:** 100+ tables (single year of age, age groups by sex)
- **Race:** 200+ tables (detailed race categories, combinations)
- **Hispanic Origin:** 150+ tables (detailed origin categories)
- **Ancestry:** 50+ tables (detailed ancestry groups)
- **Place of Birth:** 50+ tables (state, country, region)
- **Citizenship:** 30+ tables
- **Language:** 40+ tables (language spoken at home, English proficiency)
- **Migration/Residence:** 40+ tables (mobility, year moved, place lived 1 year ago)
- **Educational Attainment:** 100+ tables (by age, sex, race, field of degree)
- **School Enrollment:** 50+ tables (by age, level, type)
- **Veteran Status:** 40+ tables (by period of service, age, sex, disability)
- **Disability Status:** 60+ tables (by type, age, employment, poverty)
- **Marital Status:** 40+ tables (by age, sex, race)
- **Fertility:** 30+ tables (women 15-50, birth past year, children ever born)
- **Grandparents:** 20+ tables (living with grandchildren, responsibility)
- **Health Insurance:** 50+ tables (by type, age, employment)

#### Households & Families
- **Household Type:** 80+ tables (family, nonfamily, size)
- **Relationship:** 40+ tables (relationship to householder)
- **Household Size:** 30+ tables
- **Family Type:** 60+ tables (married, male/female householder)

#### Economic
- **Employment Status:** 100+ tables (labor force, employed, unemployed by demographics)
- **Occupation:** 100+ tables (detailed SOC codes)
- **Industry:** 100+ tables (detailed NAICS codes)
- **Class of Worker:** 40+ tables
- **Income:** 150+ tables (household, family, nonfamily, per capita by demographics)
- **Earnings:** 80+ tables (by sex, occupation, education)
- **Poverty:** 100+ tables (by age, sex, race, family type)
- **Food Stamps/SNAP:** 30+ tables
- **Ratio of Income to Poverty:** 40+ tables
- **Work Status:** 50+ tables (full-time, weeks worked)
- **Journey to Work:** 60+ tables (commute time, mode, departure time, vehicles)

#### Housing
- **Units in Structure:** 40+ tables
- **Year Built:** 40+ tables
- **Rooms:** 30+ tables
- **Bedrooms:** 30+ tables
- **Housing Tenure:** 80+ tables (owner, renter)
- **Occupancy Status:** 40+ tables
- **Vacancy Status:** 30+ tables
- **Home Value:** 50+ tables (median, distribution)
- **Gross Rent:** 50+ tables (median, distribution)
- **Gross Rent as % Income:** 40+ tables
- **Mortgage Status:** 50+ tables (with/without mortgage, costs)
- **Selected Housing Costs:** 60+ tables
- **Utilities:** 30+ tables (costs, type)
- **Plumbing/Kitchen Facilities:** 20+ tables
- **Telephone Service:** 20+ tables
- **Vehicles Available:** 30+ tables
- **Heating Fuel:** 20+ tables
- **Occupants per Room:** 20+ tables

---

### 3️⃣ Decennial Census Summary Files

**Years Available:** 1790, 1800, 1810, ..., 2010, 2020

**Geographic Levels:**
- **1790-1970:** State, county (limited tract data)
- **1970-2020:** All levels down to census block

**1790-1950 Census:**
- Total population
- Population by sex (1820+)
- Population by age (1850+)
- Population by race (1790+)
- Housing units (1940+)
- Urban/rural (1840+)

**1960-2000 Census:**
- **100%-count data:** SF1 (short form)
- **Sample data:** SF3 (long form, 1-in-6 sample)
- Both SF1 and SF3 have hundreds of detailed tables

**2010 Census:**
- SF1: 100%-count demographic and housing data
- SF2: Additional detail for specific population groups

**2020 Census:**
- P.L. 94-171 Redistricting File
- Demographic and Housing Characteristics File (DHC)

**Total Tables:** Varies by year (2000 Census has 1,000+ tables in SF3)

---

### 4️⃣ Agricultural Census

**Years Available:** 1840-1959 (county level)

**Variables (varies by year):**
- Number of farms
- Farm acreage (total, improved, unimproved)
- Farm values (land, buildings, implements)
- Crop production (bushels/pounds by crop type)
- Livestock (cattle, horses, sheep, swine, poultry)
- Farm products (wool, butter, cheese, hay, cotton, etc.)

**Note:** More recent Agricultural Census data (1964-2022) available from USDA directly (see 10_AGRICULTURE_FOOD directory)

---

### 5️⃣ County Business Patterns (CBP)

**Years Available:** 1970-2003 (county and ZIP code level)

**Variables:**
- Number of establishments by industry
- Employment (March 12 payroll)
- Payroll (first quarter, annual)
- Industry classifications (SIC 1967, 1972, 1987; NAICS 1997)

**Note:** More recent CBP data (2004-2022) available from Census Bureau directly (see 09_OCCUPATIONAL and 19_ECONOMIC_INDICATORS directories)

---

### 6️⃣ Vital Statistics

#### Natality (Births)
**Years:** 1915-1972, 1969-2007 (county level)

**Variables:**
- Total births
- Births by race
- Births by age of mother
- Birth rates

#### Mortality (Deaths)
**Years:** 1915-1972, 1969-2007 (county level)

**Variables:**
- Total deaths
- Deaths by age
- Deaths by sex
- Deaths by race
- Death rates
- Infant deaths

#### Marriages
**Years:** 1867-2010 (county level, sporadic coverage)

**Variables:**
- Number of marriages

#### Divorces
**Years:** 1867-2010 (county level, sporadic coverage)

**Variables:**
- Number of divorces

**Note:** More recent vital statistics available from CDC WONDER (see 12_MORTALITY_DISEASE directory)

---

### 7️⃣ Religious Census

**Years Available:** 1850, 1860, 1870, 1890, 1906, 1916, 1926, 1936, 1952 (county level)

**Variables:**
- Number of churches/organizations
- Number of members
- Number of Sunday schools
- Church seating capacity
- Value of church property
- Breakdowns by denomination

---

### 8️⃣ GIS Boundary Files

**Years:** 1790-2020 (varies by geography)

**Geographic Levels:**
- States: 1790-2020
- Counties: 1790-2020
- Census tracts: 1910-2020
- Block groups: 1990-2020
- Blocks: 1990-2020
- Places: 1790-2020
- Congressional districts: 1789-2020

**Formats:** Shapefiles (.shp), geodatabase

**Key Feature:** Boundaries match the exact vintage used for each census year

---

## 💻 Data Access Methods

### Method 1: NHGIS Data Finder (Web Interface)

**URL:** https://data2.nhgis.org/

**Steps:**
1. Click "Select Data"
2. Apply filters:
   - **Geographic Levels:** County
   - **Years:** Select years needed
   - **Topics:** Choose subject areas (Total Population, Race, Income, etc.)
   - **Datasets:** Select Census/ACS/Time Series
3. Add tables to cart
4. Submit extract request
5. Download CSV files + codebooks

**Output:** CSV files with FIPS codes, variable values, codebooks

---

### Method 2: R Package (ipumsr)

**Installation:**
```r
install.packages("ipumsr")
library(ipumsr)
```

**Authentication:**
```r
# Set API key (get from https://account.ipums.org/)
set_ipums_api_key("YOUR_API_KEY_HERE")
```

**Example 1: Download Time Series Table**
```r
library(ipumsr)
library(tidyverse)

# Define extract for total population time series (Table A00)
# County level, all available years (1790-2020)

# Note: Must create extract request via web interface first
# or use API to submit extract request

# Download previously submitted extract
extract_info <- get_last_extract_info("nhgis")
data <- read_nhgis(extract_info)

# Process data
pop_timeseries <- data %>%
  filter(geographic_level == "county") %>%
  select(year, state, county, fips = GISJOIN, total_pop = A00AA) %>%
  arrange(fips, year)
```

**Example 2: Get Recent ACS Data (2019-2023)**
```r
# Define extract for ACS 5-year (2019-2023) county data

# Must submit extract request first (via web or API)
# Then download:

nhgis_extract <- read_nhgis("nhgis0001_csv.zip")

# Extract has codebook and data files
# Variable names correspond to ACS table codes (e.g., B01001 = Sex by Age)

acs_data <- nhgis_extract %>%
  select(
    state = STATE,
    county = COUNTY,
    fips = paste0(STATE, COUNTY),
    total_pop = ALUCE001,      # ACS Table B01003: Total Population
    median_age = ALUKE001,      # ACS Table B01002: Median Age
    median_income = AM7YE001    # ACS Table B19013: Median Household Income
  )
```

**Example 3: Get Multiple Census Years**
```r
# Compare 1990, 2000, 2010, 2020 Census
# Using Time Series Table for consistency

# After submitting extract request and downloading:

census_comparison <- read_nhgis("nhgis0002_csv.zip") %>%
  filter(year %in% c(1990, 2000, 2010, 2020)) %>%
  select(
    year,
    fips = GISJOIN,
    state_name = STATE,
    county_name = COUNTY,
    total_pop = A00AA,
    white = CL8AA,
    black = CL8AB,
    asian = CL8AD,
    hispanic = CL9AA
  ) %>%
  pivot_wider(
    id_cols = c(fips, state_name, county_name),
    names_from = year,
    values_from = c(total_pop, white, black, asian, hispanic)
  )
```

---

### Method 3: Python Package (ipumspy)

**Installation:**
```python
pip install ipumspy
```

**Authentication:**
```python
from ipumspy import IpumsApiClient, NhgisExtract

# Set API key
api_key = "YOUR_API_KEY_HERE"
ipums = IpumsApiClient(api_key)
```

**Example: Download ACS Data**
```python
import pandas as pd
from ipumspy import IpumsApiClient, NhgisExtract

# Initialize client
ipums = IpumsApiClient("YOUR_API_KEY")

# Define extract (example: 2019-2023 ACS county data)
extract = NhgisExtract(
    datasets={
        "2019_2023_ACS5a": {
            "geog_levels": ["county"],
            "data_tables": [
                "B01003",  # Total Population
                "B01002",  # Median Age
                "B19013",  # Median Household Income
                "B25077",  # Median Home Value
                "B17001"   # Poverty Status
            ]
        }
    }
)

# Submit extract
ipums.submit_extract(extract)

# Wait for completion and download
# (Check status via web interface or API)

# Load data
data = pd.read_csv("nhgis_extract.csv")

# Create FIPS code
data['FIPS'] = data['STATE'].astype(str).str.zfill(2) + \
               data['COUNTY'].astype(str).str.zfill(3)

# Extract variables (adjust column names based on codebook)
county_data = data[['FIPS', 'STATEA', 'COUNTYA',
                     'ALUCE001',  # Total pop
                     'ALUKE001',  # Median age
                     'AM7YE001',  # Median income
                     'ALUAE001',  # Median home value
                     'ALWWE001'   # Total for poverty determination
                    ]]
```

---

### Method 4: Direct API Access

**Base URL:** `https://api.ipums.org/`

**Endpoints:**
- List time series tables: `GET /metadata/nhgis/time_series_tables`
- List datasets: `GET /metadata/nhgis/datasets`
- Submit extract: `POST /extracts/nhgis`
- Check extract status: `GET /extracts/nhgis/{extract_id}`
- Download extract: `GET /extracts/nhgis/{extract_id}/download`

**Authentication:** Include API key in header: `Authorization: Bearer YOUR_API_KEY`

**Example (curl):**
```bash
# List all time series tables
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.ipums.org/metadata/nhgis/time_series_tables

# Get specific time series table details
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.ipums.org/metadata/nhgis/time_series_tables/A00
```

---

## 🔧 Data Processing Tips

### 1. Understanding GISJOIN Codes
NHGIS uses GISJOIN instead of FIPS for geographic identifiers in some extracts.

**GISJOIN Format:** `G{state}{county}0{tract}{block}`
- Example: `G0100010` = State 01, County 001

**Convert GISJOIN to FIPS:**
```r
# R
library(stringr)

data <- data %>%
  mutate(
    state_fips = str_sub(GISJOIN, 2, 3),
    county_fips = str_sub(GISJOIN, 4, 6),
    FIPS = paste0(state_fips, county_fips)
  )
```

```python
# Python
data['state_fips'] = data['GISJOIN'].str[1:3]
data['county_fips'] = data['GISJOIN'].str[3:6]
data['FIPS'] = data['state_fips'] + data['county_fips']
```

### 2. Handling Missing Data
NHGIS uses specific codes for missing/suppressed data:
- **Blank/NA:** Data not available
- **-1:** Data suppressed for confidentiality
- Check codebook for dataset-specific codes

### 3. Margins of Error (ACS Data)
ACS estimates include margins of error (MOE) at 90% confidence level.

**Calculate standard error:**
```r
SE = MOE / 1.645
```

**Aggregate MOEs:**
```r
# For sums
MOE_sum = sqrt(sum(MOE^2))

# For proportions (requires more complex formulas)
# See Census Bureau ACS documentation
```

### 4. Working with Time Series Tables

**Benefits:**
- Pre-harmonized across boundary changes
- Consistent variable definitions
- Ready for longitudinal analysis

**Example workflow:**
```r
library(tidyverse)

# Load time series data
ts_data <- read_nhgis("nhgis_ts.csv")

# Calculate population change
pop_change <- ts_data %>%
  filter(year %in% c(1990, 2000, 2010, 2020)) %>%
  group_by(fips) %>%
  mutate(
    pop_change = total_pop - lag(total_pop),
    pop_change_pct = (total_pop - lag(total_pop)) / lag(total_pop) * 100
  ) %>%
  ungroup()
```

---

## 📋 Complete Time Series Tables List (By Topic)

**Note:** NHGIS provides **389 time series tables**. Below are major categories. For complete list, download spreadsheet: https://www.nhgis.org/time-series-tables

### Population Tables (100+ tables)
**Total Population:**
- A00: Persons: Total (1790-2020) ⭐ LONGEST TIME SERIES
- AV0: Persons: Total (1970-2020, standardized to 2010)
- B78: Persons: Total (1990-2020, standardized to 2010)
- CL8: Persons: Total (1970-2020)

**Sex:**
- A08: Persons by Sex (1820-2020)
- AV1: Persons by Sex (1970-2020, standardized to 2010)
- CM0: Persons by Sex (1970-2020)

**Age:**
- A09-A14: Persons by Age Groups (1850-2020)
- B18-B24: Median Age by Sex (1970-2020)
- CM1-CM8: Detailed Age Categories (1970-2020)

**Race:**
- A15-A20: Persons by Race (1790-2020)
- B69-B77: Detailed Race Categories (1970-2020)
- CL8: Persons by Detailed Race (1970-2020)

**Hispanic Origin:**
- CL9-CM9: Hispanic/Latino Origin (1970-2020)
- CM9-CN0: Hispanic by Race (1980-2020)

**Urban/Rural:**
- A57: Urban/Rural Status (1840-2020)
- A59: Urban/Rural Persons (1910-2020)
- CL9: Urban/Rural by Race (1970-2020)

**Foreign Born:**
- A21-A25: Place of Birth (1850-2020)
- B49-B53: Foreign Born by Region (1970-2020)

**Citizenship:**
- B54-B56: Citizenship Status (1890-2020)

**Language:**
- B57-B60: Language Spoken at Home (1890-2020)

**Migration:**
- B61-B68: Residence 1/5 Years Ago (1940-2020)

### Household & Family Tables (50+ tables)
**Household Type:**
- A26-A32: Households by Type (1940-2020)
- B93-B98: Family Type (1950-2020)

**Household Size:**
- A33-A35: Persons per Household (1850-2020)
- B99-B101: Household Size Distribution (1940-2020)

**Marital Status:**
- A36-A39: Marital Status by Sex (1880-2020)
- B89-B92: Detailed Marital Status (1970-2020)

**Fertility:**
- B102-B106: Women by Children Ever Born (1940-2020)
- B107-B109: Births in Past Year (1970-2020)

**Grandparents:**
- B110-B112: Grandparents as Caregivers (1990-2020)

### Education Tables (30+ tables)
**Educational Attainment:**
- B39-B47: Years of School Completed (1940-2020)
- B113-B120: Highest Degree (1990-2020)

**School Enrollment:**
- A40-A43: Persons Enrolled by Level (1850-2020)
- B121-B125: Enrollment by Age (1970-2020)

### Economic Tables (80+ tables)
**Employment Status:**
- A44-A48: Labor Force Status (1940-2020)
- B126-B135: Detailed Employment Status (1970-2020)

**Occupation:**
- A49-A52: Persons by Occupation (1850-2020)
- B136-B145: Detailed Occupational Categories (1970-2020)

**Industry:**
- B146-B155: Industry of Employment (1940-2020)

**Class of Worker:**
- B156-B160: Private/Government/Self-Employed (1940-2020)

**Income:**
- A53-A56: Median Income (1950-2020)
- B161-B180: Household/Family Income Distribution (1950-2020)
- B181-B190: Per Capita Income (1970-2020)

**Poverty:**
- B191-B210: Persons/Families Below Poverty (1970-2020)

**Journey to Work:**
- B211-B225: Commute Time, Transportation Mode (1960-2020)

### Housing Tables (50+ tables)
**Housing Units:**
- A58-A61: Total Housing Units (1940-2020)
- B226-B230: Occupied/Vacant Units (1940-2020)

**Tenure:**
- A62-A65: Owner/Renter Occupied (1890-2020)
- B231-B235: Tenure by Race (1970-2020)

**Home Value:**
- A66-A70: Median Home Value (1940-2020)
- B236-B245: Value Distribution (1940-2020)

**Gross Rent:**
- A71-A75: Median Gross Rent (1940-2020)
- B246-B255: Rent Distribution (1940-2020)

**Rooms:**
- B256-B265: Number of Rooms (1940-2020)

**Year Built:**
- B266-B275: Year Structure Built (1940-2020)

**Utilities:**
- B276-B290: Plumbing, Heating, Kitchen (1940-2020)

**Vehicles:**
- B291-B295: Vehicles Available (1960-2020)

### Veteran Tables (10+ tables)
- B296-B305: Veterans by Age, Sex, Period (1980-2020)

### Disability Tables (10+ tables)
- B306-B315: Disability Status by Type (1970-2020)

### Health Insurance Tables (5+ tables)
- B316-B320: Insurance Coverage by Type (2009-2020)

---

## 📚 Key Resources

### Official Documentation
- **NHGIS Website:** https://www.nhgis.org/
- **Data Finder:** https://data2.nhgis.org/
- **User Guide:** https://www.nhgis.org/user-guide
- **Time Series Tables:** https://www.nhgis.org/time-series-tables
- **API Documentation:** https://developer.ipums.org/

### R Resources
- **ipumsr Package:** https://cran.r-project.org/package=ipumsr
- **ipumsr Documentation:** https://tech.popdata.org/ipumsr/
- **Vignettes:** https://tech.popdata.org/ipumsr/articles/

### Python Resources
- **ipumspy Package:** https://pypi.org/project/ipumspy/
- **GitHub:** https://github.com/ipums/ipumspy

### Support
- **Email:** nhgis@umn.edu
- **User Forum:** https://forum.ipums.org/
- **FAQ:** https://www.nhgis.org/frequently-asked-questions-faq

### Citation
When using NHGIS data, cite as:

> Steven Manson, Jonathan Schroeder, David Van Riper, Katherine Knowles, Tracy Kugler, Finn Roberts, and Steven Ruggles. IPUMS National Historical Geographic Information System: Version 18.0 [dataset]. Minneapolis, MN: IPUMS. 2023. https://doi.org/10.18128/D050.V18.0

---

## ⚠️ Important Notes

### 1. County Boundary Changes
- **Nominally integrated tables:** Counties linked by name/code, boundaries may shift
- **Geographically standardized tables:** Normalize to 2010 boundaries (limited years)
- **Recommendation:** Use time series tables to handle boundary changes automatically
- **Manual harmonization:** See `00_METADATA/COUNTY_BOUNDARIES_REDISTRICTING.md` if needed

### 2. Suppressed Data
ACS data may be suppressed for:
- Small populations
- Confidentiality concerns
- Data quality issues

Check for missing values and MOE before analysis.

### 3. Decennial vs. ACS
- **Decennial Census (1790-2020):**
  - 100%-count (not sample)
  - Every 10 years
  - More limited variables (especially 2010, 2020)
  - Higher accuracy for small areas

- **ACS (2005-2023):**
  - Sample-based (margins of error)
  - Annual updates (5-year rolling estimates)
  - 1,300+ detailed variables
  - Use 5-year estimates for counties

### 4. Year Naming Conventions
- **Decennial:** Single year (e.g., 2020)
- **ACS 5-year:** Year range (e.g., 2019-2023 = data collected 2019-2023, released 2024)
- **Time Series:** May show "1990, 2000, 2010" but use specific datasets internally

---

## 🎯 Recommended Workflows

### For Population Demographics
1. **Use NHGIS Time Series Tables** (NOT raw Census files)
2. Select Table A00 for total population (1790-2020)
3. Add age/sex/race tables as needed
4. Download via Data Finder → one CSV with all years
5. FIPS codes consistent across years

### For Detailed Demographics (Recent)
1. **Use ACS 5-year estimates** (NOT 1-year)
2. Select 2019-2023 (most recent as of 2024)
3. Choose specific ACS tables (B01001 for age/sex, etc.)
4. Download via Data Finder
5. Include MOE columns for uncertainty

### For Economic Data
1. **Use NHGIS ACS tables** for income, poverty, employment
2. Select B19013 (median income), B17001 (poverty), B23025 (employment)
3. Or use time series tables for trends (1950-2020)

### For Housing Data
1. **Use NHGIS ACS tables** for recent data
2. Select B25077 (median value), B25064 (median rent), B25001 (housing units)
3. Or use time series tables for historical trends

### For Agriculture
1. **Use NHGIS for historical** (1840-1959)
2. **Use USDA directly for recent** (1964-2022)
3. See `10_AGRICULTURE_FOOD/` directory for USDA sources

---

**Total Variables via NHGIS:** 10,000+ unique variables across all time series and ACS tables

**Temporal Coverage:** 1790-2024 (234 years!)

**Geographic Coverage:** All 3,143 US counties (with historical counties for early years)

**Update Frequency:**
- ACS: Annual (released December)
- Decennial: Every 10 years
- Time Series Tables: Updated after each new Census/ACS release

---

**NHGIS is THE PRIORITY DATA SOURCE for county-level demographic, social, economic, and housing data. Use it FIRST before seeking individual Census Bureau data sources.**
