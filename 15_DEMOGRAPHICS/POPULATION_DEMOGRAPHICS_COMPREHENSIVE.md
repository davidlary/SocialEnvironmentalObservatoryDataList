# Population & Demographics - Comprehensive Documentation
## US County-Level Demographic Data Sources

**Coverage:** All 3,143 US Counties
**Last Updated:** November 13, 2025
**Total Variables:** 300+ demographic variables

---

## 📊 Overview

This comprehensive documentation covers all county-level population and demographic data sources, including:
- Population counts, age, sex, race/ethnicity
- Migration and mobility patterns
- Urban/rural classification
- Population projections
- Historical population trends

---

## 1️⃣ CENSUS DECENNIAL CENSUS

### Overview
Complete population count every 10 years mandated by US Constitution.

**Coverage:**
- All 3,143 US counties
- Decadal: 1790, 1800, ..., 2000, 2010, 2020, 2030 (next)
- 100% count (not sample)

**Key Variables (2020 Census):**
- Total population
- Population by age (18 age groups)
- Population by sex
- Population by race (OMB categories)
- Population by Hispanic/Latino origin
- Voting age population
- Group quarters population
- Housing units (occupied, vacant)

**Total Variables:** ~50 demographic variables

### Data Access

**Source:** Census Bureau
**URL:** https://data.census.gov/
**API:** https://api.census.gov/data.html
**Format:** API, bulk downloads (CSV, databases)

### R Code Example

```r
library(tidycensus)
library(tidyverse)

# Get Decennial Census data (2020)
# Requires Census API key: census_api_key("YOUR_KEY")

# Total population by county
pop_2020 <- get_decennial(
  geography = "county",
  variables = c(
    total_pop = "P1_001N",
    white = "P1_003N",
    black = "P1_004N",
    hispanic = "P2_002N",
    pop_18plus = "P3_001N"
  ),
  year = 2020,
  output = "wide"
)

# Age structure (18 age groups)
age_vars <- paste0("P12_", sprintf("%03d", 3:20), "N")  # Male age groups
pop_age <- get_decennial(
  geography = "county",
  variables = age_vars,
  year = 2020
)
```

---

## 2️⃣ CENSUS AMERICAN COMMUNITY SURVEY (ACS)

### Overview
Annual survey providing detailed demographic, social, economic, and housing estimates.

**Coverage:**
- All 3,143 US counties
- Annual 5-year estimates: 2005-2009, 2006-2010, ..., 2018-2022, 2019-2023
- Annual 1-year estimates: Available for counties with population >65,000

**Key Demographic Variables:**
- Age (single year of age)
- Sex
- Race and ethnicity (detailed categories)
- Household type and size
- Relationship to householder
- Marital status
- Fertility (women 15-50)
- Grandparents as caregivers
- Ancestry
- Place of birth
- Citizenship status
- Language spoken at home
- Migration (moved in past year)

**Total Variables:** ~150 demographic variables

### Data Access

**Source:** Census Bureau ACS
**URL:** https://data.census.gov/
**API:** https://api.census.gov/data/2022/acs/acs5
**Format:** API, bulk downloads
**Update Frequency:** Annual (released December for prior year)

### Python Code Example

```python
import pandas as pd
import requests

# Census API
API_KEY = "YOUR_KEY"
base_url = "https://api.census.gov/data/2022/acs/acs5"

# Get demographic variables for all counties
variables = {
    'B01001_001E': 'total_pop',
    'B01002_001E': 'median_age',
    'B01001_002E': 'male_pop',
    'B01001_026E': 'female_pop',
    'B02001_002E': 'white_alone',
    'B02001_003E': 'black_alone',
    'B03001_003E': 'hispanic'
}

var_list = ','.join(variables.keys())

params = {
    'get': var_list,
    'for': 'county:*',
    'key': API_KEY
}

response = requests.get(base_url, params=params)
data = response.json()

# Convert to DataFrame
df = pd.DataFrame(data[1:], columns=data[0])

# Rename columns
df = df.rename(columns=variables)

# Create FIPS code
df['FIPS'] = df['state'] + df['county']
```

---

## 3️⃣ CENSUS POPULATION ESTIMATES PROGRAM (PEP)

### Overview
Annual population estimates for intercensal years.

**Coverage:**
- All 3,143 US counties
- Annual: 1970-present
- Updated every July
- Bridge between decennial censuses

**Key Variables:**
- Total population
- Population by age (18 age groups)
- Population by sex
- Population by race
- Population by Hispanic origin
- Components of change:
  - Births
  - Deaths
  - Net migration (domestic + international)
  - Natural increase

**Total Variables:** ~30

### Data Access

**Source:** Census Bureau Population Estimates
**URL:** https://www.census.gov/programs-surveys/popest.html
**Format:** CSV downloads, bulk files
**Update Frequency:** Annual (July)

### R Code Example

```r
library(tidyverse)

# Download county population estimates (2020-2023)
url <- "https://www2.census.gov/programs-surveys/popest/datasets/2020-2023/counties/totals/co-est2023-alldata.csv"

pop_est <- read_csv(url) %>%
  mutate(FIPS = paste0(STATE, COUNTY)) %>%
  select(
    FIPS, STNAME, CTYNAME,
    POPESTIMATE2020, POPESTIMATE2021, POPESTIMATE2022, POPESTIMATE2023,
    BIRTHS2023, DEATHS2023,
    DOMESTICMIG2023, INTERNATIONALMIG2023, NETMIG2023
  )

# Calculate population change
pop_est <- pop_est %>%
  mutate(
    pop_change_2020_2023 = POPESTIMATE2023 - POPESTIMATE2020,
    pop_change_pct = (POPESTIMATE2023 - POPESTIMATE2020) / POPESTIMATE2020 * 100
  )
```

---

## 4️⃣ IRS MIGRATION DATA

### Overview
County-to-county migration flows based on address changes on tax returns.

**Coverage:**
- All 3,143 US counties
- Annual: 1990-2022
- Captures migration flows between counties

**Key Variables:**
- Number of returns (households) moved in
- Number of returns moved out
- Number of exemptions (persons) moved in
- Number of exemptions moved out
- Aggregate gross income (AGI) moved in
- Aggregate AGI moved out
- Net migration (in - out)
- Top origin counties for in-migrants
- Top destination counties for out-migrants

**Total Variables:** ~20 per county pair

### Data Access

**Source:** IRS Statistics of Income
**URL:** https://www.irs.gov/statistics/soi-tax-stats-migration-data
**Format:** CSV files by year
**Update Frequency:** Annual (~2-year lag)

### Python Code Example

```python
import pandas as pd

# Download IRS county-to-county migration (2021-2022)
url = "https://www.irs.gov/pub/irs-soi/2122countyinflow.csv"
migration_in = pd.read_csv(url)

# Aggregate to county level
county_inmigration = migration_in.groupby('y2_statefips', 'y2_countyfips').agg({
    'n1': 'sum',  # Number of returns
    'n2': 'sum',  # Number of exemptions (persons)
    'AGI': 'sum'  # Aggregate gross income
}).reset_index()

county_inmigration['FIPS'] = (
    county_inmigration['y2_statefips'].astype(str).str.zfill(2) +
    county_inmigration['y2_countyfips'].astype(str).str.zfill(3)
)

# Calculate migration rate
# (requires merging with population data)
```

---

## 5️⃣ USDA ERS RURAL-URBAN CODES

### Overview
Classification schemes for metropolitan, micropolitan, and rural counties.

**Coverage:** All 3,143 US counties

### Rural-Urban Continuum Codes (RUCC)

**9-level classification:**
- **Metro counties (1-3):**
  1. Counties in metro areas of 1 million+ population
  2. Counties in metro areas of 250,000 to 1 million
  3. Counties in metro areas of <250,000 population
- **Nonmetro counties (4-9):**
  4. Urban population of 20,000+, adjacent to metro area
  5. Urban population of 20,000+, not adjacent to metro area
  6. Urban population of 2,500-19,999, adjacent to metro area
  7. Urban population of 2,500-19,999, not adjacent to metro area
  8. Completely rural or <2,500 urban population, adjacent to metro area
  9. Completely rural or <2,500 urban population, not adjacent to metro area

**Vintages:** 1974, 1983, 1993, 2003, 2013, 2023

### Urban Influence Codes (UIC)

**12-level classification** based on proximity to metro and micro areas

### Data Access

**Source:** USDA Economic Research Service
**URL:** https://www.ers.usda.gov/data-products/rural-urban-continuum-codes/
**Format:** Excel spreadsheets
**Update Frequency:** ~Decadal

---

## 6️⃣ CENSUS POPULATION PROJECTIONS

### Overview
Projected future population by county (where available) or state.

**Note:** Official county-level projections discontinued by Census Bureau. State-level projections available.

**Alternative sources for county projections:**
- University of Virginia Weldon Cooper Center (Virginia only)
- State demographic centers (varies by state)
- Woods & Poole Economics (commercial)

---

## 📋 Summary Table: All Demographic Variables

| Source | Variables | Temporal Coverage | Update Frequency |
|--------|-----------|-------------------|------------------|
| Decennial Census | 50+ | 1790-2020 (decadal) | Every 10 years |
| ACS 5-year | 150+ | 2005-2023 | Annual |
| PEP Estimates | 30 | 1970-present | Annual |
| IRS Migration | 20 | 1990-2022 | Annual |
| Rural-Urban Codes | 3 | 1974-2023 | ~Decadal |

**Total Demographic Variables:** ~300

---

## 💻 Recommended Data Collection Workflow

### For Population Trends
```r
# 1. Get decennial for benchmark years
pop_2020 <- get_decennial(geography = "county", variables = "P1_001N", year = 2020)
pop_2010 <- get_decennial(geography = "county", variables = "P001001", year = 2010)

# 2. Get PEP for annual intercensal estimates
pop_2015 <- get_estimates(geography = "county", product = "population", year = 2015)

# 3. Combine into time series
pop_panel <- bind_rows(
  pop_2010 %>% mutate(year = 2010),
  pop_2015 %>% mutate(year = 2015),
  pop_2020 %>% mutate(year = 2020)
)
```

### For Detailed Demographics
Use ACS 5-year estimates for most stable estimates at county level.

### For Migration Flows
Use IRS county-to-county migration data for origin-destination matrices.

---

## 📚 Additional Resources

- **Census Data Portal:** https://data.census.gov/
- **tidycensus Package (R):** https://walker-data.com/tidycensus/
- **censusdata Package (Python):** https://pypi.org/project/censusdata/
- **IPUMS NHGIS:** https://www.nhgis.org/ (historical harmonized data)

---

**Total Variables Documented:** ~300
**Temporal Range:** 1790-present (varies by source)
**Update Frequency:** Annual (ACS, PEP), Decadal (Census)
