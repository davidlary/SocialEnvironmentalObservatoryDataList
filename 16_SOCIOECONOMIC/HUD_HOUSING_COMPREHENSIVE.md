# HUD Housing Data - Comprehensive County-Level Documentation

## Executive Summary

The **U.S. Department of Housing and Urban Development (HUD)** maintains extensive housing datasets covering affordable housing programs, fair market rents, housing choice vouchers, public housing, homelessness, community development, and housing market conditions. This documentation provides complete access to county-level housing variables critical for understanding housing affordability, access, and market dynamics.

### Key Features

- **🏠 Assisted Housing**: 5+ million households in HUD programs (public housing, vouchers, multifamily)
- **💰 Fair Market Rents**: Annual rent benchmarks for 2,500+ counties/metro areas
- **📊 CHAS**: Comprehensive Housing Affordability Strategy (ACS special tabulations)
- **🏚️ Homelessness**: Point-in-Time counts, Continuum of Care data
- **🏗️ Community Development**: CDBG funding, HOME Investment Partnerships
- **📈 Market Indicators**: House price index, housing permits, foreclosures
- **🔑 Access**: Free, public data; APIs and bulk downloads available
- **🌎 Geography**: County, metro, ZIP code, census tract, project-level

---

## Table of Contents

1. [Data Systems & Sources](#data-systems--sources)
2. [Fair Market Rents (FMR)](#fair-market-rents-fmr)
3. [HUD Assisted Housing](#hud-assisted-housing)
4. [CHAS - Comprehensive Housing Affordability Strategy](#chas---comprehensive-housing-affordability-strategy)
5. [Housing Choice Vouchers (Section 8)](#housing-choice-vouchers-section-8)
6. [Public Housing](#public-housing)
7. [Multifamily Assisted Housing](#multifamily-assisted-housing)
8. [Homelessness Data](#homelessness-data)
9. [Community Development Block Grants (CDBG)](#community-development-block-grants-cdbg)
10. [HOME Investment Partnerships](#home-investment-partnerships)
11. [FHFA House Price Index](#fhfa-house-price-index)
12. [County-Level Aggregation Strategies](#county-level-aggregation-strategies)
13. [Access Methods & APIs](#access-methods--apis)
14. [R Packages & Code Examples](#r-packages--code-examples)
15. [Data Quality & Limitations](#data-quality--limitations)
16. [Priority Variables for Collection](#priority-variables-for-collection)
17. [Quick Reference](#quick-reference)

---

## Data Systems & Sources

### 1. Fair Market Rents (FMR)
**Purpose:** Establish payment standards for Housing Choice Voucher program
**Coverage:** All 3,143 counties (metro and non-metro areas)
**Years:** 1983-present
**Update Frequency:** Annual (released October 1)
**Restriction:** Public use, no restrictions

### 2. HUD Assisted Housing - Picture of Subsidized Households
**Purpose:** Inventory of all HUD-assisted properties and households
**Coverage:** 5+ million households, 50,000+ properties
**Years:** 1997-present
**Update Frequency:** Annual (some datasets quarterly)
**Restriction:** Public use; project-level data may suppress addresses

### 3. CHAS - Comprehensive Housing Affordability Strategy
**Purpose:** Special tabulations of ACS data for HUD planning
**Coverage:** All counties, places, census tracts
**Years:** 2006-2021 (5-year ACS data)
**Update Frequency:** Annual (1-year lag from ACS release)
**Restriction:** Public use, no restrictions

### 4. HUD USPS ZIP Code Crosswalk Files
**Purpose:** Allocate ZIP code data to counties/tracts
**Coverage:** All ZIP codes
**Years:** 2010-present (quarterly updates)
**Update Frequency:** Quarterly
**Restriction:** Public use

### 5. Point-in-Time (PIT) Homeless Counts
**Purpose:** Annual homeless population count
**Coverage:** All Continuums of Care (CoCs), ~400 geographic areas
**Years:** 2007-present
**Update Frequency:** Annual (one night in January)
**Restriction:** Public use

### 6. Community Development Block Grants (CDBG)
**Purpose:** Funding for community development activities
**Coverage:** 1,200+ entitlement jurisdictions + states (for non-entitlement)
**Years:** 1975-present
**Update Frequency:** Annual
**Restriction:** Public use

### 7. FHFA House Price Index
**Purpose:** Track single-family home price changes
**Coverage:** All states, metros, counties with sufficient sales
**Years:** 1975-present (varies by geography)
**Update Frequency:** Quarterly
**Restriction:** Public use

---

## Fair Market Rents (FMR)

Fair Market Rents are used to determine payment standard amounts for HUD programs. FMRs represent the 40th percentile of gross rents for standard quality rental units.

### Geographic Definitions

- **Metropolitan FMR Areas**: Based on OMB Core-Based Statistical Areas (CBSAs)
- **Non-Metropolitan Counties**: Individual county FMRs
- **Small Area FMRs (SAFMRs)**: ZIP code-level FMRs in select metros (2018+)

### FMR Variables (by Bedroom Size)

#### Standard FMRs (~10 variables per county)
- `FMR_0BR` - Fair Market Rent, efficiency/studio apartment
- `FMR_1BR` - Fair Market Rent, 1-bedroom
- `FMR_2BR` - Fair Market Rent, 2-bedroom
- `FMR_3BR` - Fair Market Rent, 3-bedroom
- `FMR_4BR` - Fair Market Rent, 4-bedroom

#### Additional FMR Metrics
- `FMR50_0BR` through `FMR50_4BR` - 50th percentile FMRs (available for some metros)
- `FMR40_0BR` through `FMR40_4BR` - Standard 40th percentile (same as FMR_*)
- `FMR_PERCENTILE` - Percentile used (40 or 50)
- `METRO_CODE` - CBSA code (for metro areas)
- `COUNTY_CODE` - County FIPS code
- `STATE_ALPHA` - State abbreviation
- `AREANAME` - FMR area name
- `POP2020` - Population (2020 Census)

#### Small Area FMRs (ZIP Code Level, 2018+)
- Same bedroom variables as standard FMRs
- Available for ~30 metros initially, expanding annually
- Enables more localized rent benchmarks

### Time Series
- **1983-present**: Complete FMR series
- **Annual**: Released October 1 for upcoming fiscal year
- **Inflation-adjusted**: Use CPI-U for housing to adjust historical FMRs

---

## HUD Assisted Housing

HUD's "Picture of Subsidized Households" provides comprehensive data on all HUD-assisted properties and households.

### Programs Covered

1. **Public Housing** - Owned and operated by Public Housing Authorities (PHAs)
2. **Housing Choice Vouchers (Section 8)** - Tenant-based rental assistance
3. **Multifamily (Project-Based Section 8)** - Owner-administered rental assistance
4. **Moderate Rehabilitation**
5. **Section 202** - Supportive housing for the elderly
6. **Section 811** - Supportive housing for persons with disabilities
7. **HOME** - Rental housing assistance
8. **HOPWA** - Housing for persons with HIV/AIDS

### Household-Level Variables (~100 variables)

#### A. Program & Property Identification
- `CODE` - Property/project code
- `PROPERTY_NAME` - Property name
- `PROPERTY_ADDRESS`, `PROPERTY_CITY`, `PROPERTY_STATE`, `PROPERTY_ZIP`
- `COUNTY_CODE` - County FIPS code
- `PROGRAM_LABEL` - HUD program type
- `PORTFOLIO_LABEL` - Program portfolio
- `YEAR_MONTH` - Reporting period (YYYYMM)

#### B. Household Characteristics
- `NUMBER_REPORTED` - Number of households
- `NUMBER_ASSISTED` - Number of households receiving assistance
- `AVERAGE_MONTHS_SINCE_LAST_RENT` - Months resident
- `PERCENT_MINORITY` - Percent minority households
- `PERCENT_WHITE_NON_HISP` - Percent white non-Hispanic households
- `PERCENT_BLACK_NON_HISP` - Percent Black non-Hispanic households
- `PERCENT_HISPANIC` - Percent Hispanic households
- `PERCENT_ASIAN_PACIFIC_ISL` - Percent Asian/Pacific Islander households
- `PERCENT_NATIVE_AMERICAN` - Percent American Indian/Alaska Native households

#### C. Household Composition
- `PERSON_PER_UNIT` - Average persons per unit
- `PERCENT_FEMALE_HEADED` - Percent female-headed households
- `PERCENT_DISABLED_HH` - Percent of households with disabled member
- `PERCENT_ELDERLY_HH` - Percent elderly households (head/spouse 62+)
- `PERCENT_LT5_PERSON` - Percent households with children under 5
- `PERCENT_5TO17_PERSON` - Percent households with children 5-17
- `PERCENT_ADULTS` - Percent households with only adults (18+)

#### D. Income
- `AVERAGE_HH_INCOME` - Average household annual income
- `PERCENT_LT50_AMI` - Percent extremely low income (<50% Area Median Income)
- `PERCENT_50TO80_AMI` - Percent very low income (50-80% AMI)
- `PERCENT_GT80_AMI` - Percent low income (>80% AMI)
- `MEDIAN_INCOME` - Median household income

#### E. Rent & Housing Costs
- `AVERAGE_MONTHS_WAITING` - Average months on waiting list
- `MONTHS_SINCE_LAST_RENT` - Months since rent adjustment
- `AVERAGE_RENT_PER_MONTH` - Average contract rent
- `PERCENT_UTILITY_ALLOWANCE` - Percent receiving utility allowance
- `TPOVERTY` - Total persons in poverty
- `SPENDING_PER_PERSON` - Spending per person

---

## CHAS - Comprehensive Housing Affordability Strategy

CHAS data are special tabulations of American Community Survey (ACS) data commissioned by HUD. They provide detailed housing affordability and housing problems data not available in standard ACS tables.

### Coverage
- **Geography**: Nation, states, counties, places (50k+ pop), congressional districts, census tracts
- **Years**: 2006-2021 (5-year ACS; e.g., "2017-2021 CHAS" = 2021 release)
- **Tables**: 19 detailed tables

### Key Variables (~200 variables across tables)

#### Table 1: Housing Problems
**Universe**: Occupied units
**Variables**: Count of households by:
- Housing problems:
  - Cost burden >30% (moderate) or >50% (severe)
  - Overcrowding (>1.01 persons per room)
  - Incomplete kitchen facilities
  - Incomplete plumbing facilities
  - Any of the above ("housing problems")
- Household income (8 categories: <30%, 30-50%, 50-80%, 80-100% AMI, 100%+)
- Household type (elderly, small families, large families, all other)
- Tenure (owner vs. renter)

**Key Metrics (derived):**
- `cost_burden_moderate_count` - Households paying 30-50% income for housing
- `cost_burden_severe_count` - Households paying >50% income for housing
- `overcrowded_count` - Households with >1.01 persons per room
- `total_housing_problems` - Any housing problem

#### Table 9: Cost Burden by Race/Ethnicity
**Variables**: Cost burden by:
- Race/ethnicity (8 categories)
- Income level (4 categories)
- Tenure (owner/renter)

#### Table 15: Homeownership Rates
**Variables**:
- Total households
- Owner-occupied households
- Renter-occupied households
By race/ethnicity and income

#### Table 19: Household Type by Income
**Variables**:
- Elderly households
- Small families (2-4 persons)
- Large families (5+ persons)
- All other households
By income category (<30%, 30-50%, 50-80%, 80-100%, 100%+ AMI)

### CHAS Data Dictionary (Sample Variables)

| Variable Code | Description |
|--------------|-------------|
| `T1_EST1` | Households with income ≤30% AMI, renter, cost burden ≤30% |
| `T1_EST2` | Households with income ≤30% AMI, renter, cost burden 30-50% |
| `T1_EST3` | Households with income ≤30% AMI, renter, cost burden >50% |
| `T1_EST4` | Households with income ≤30% AMI, renter, no/negative income |
| `T9_EST1` | White alone households, income ≤30% AMI, cost burden >50% |
| `T9_EST2` | Black/African American alone, income ≤30% AMI, cost burden >50% |
| `T15_EST1` | Total households |
| `T15_EST2` | Owner-occupied |
| `T15_EST3` | Renter-occupied |

**Margin of Error**: All CHAS estimates include MOE (90% confidence interval)

---

## Housing Choice Vouchers (Section 8)

Housing Choice Vouchers (HCV) provide tenant-based rental assistance to low-income families. Voucher holders find their own housing; HUD pays landlords the difference between ~30% of household income and the FMR.

### Picture of Subsidized Households - Vouchers

**Variables** (county-level aggregation of household records):
- `total_vouchers` - Total vouchers in use
- `total_units_available` - Units available (leased + available)
- `utilization_rate` - Vouchers in use / vouchers allocated
- `avg_hh_income` - Average household income
- `pct_extremely_low_income` - Percent with income <30% AMI
- `pct_elderly` - Percent elderly households
- `pct_disabled` - Percent households with disabled member
- `pct_minority` - Percent minority households
- `avg_months_waiting` - Average months on waiting list
- `avg_months_participation` - Average months in program

### Voucher Special Programs
- **Family Unification Program (FUP)** - For families involved in child welfare system
- **Veterans Affairs Supportive Housing (VASH)** - For homeless veterans
- **Mainstream vouchers** - For non-elderly persons with disabilities
- **Project-based vouchers** - Attached to specific units, not portable

---

## Public Housing

Public housing consists of rental units owned and operated by ~3,000 Public Housing Authorities (PHAs).

### Picture of Subsidized Households - Public Housing

**Variables** (county-level aggregation):
- `total_public_housing_units` - Total public housing units
- `occupied_units` - Occupied units
- `occupancy_rate` - Occupied / total
- `avg_hh_income` - Average household income
- `pct_extremely_low_income` - <30% AMI
- `pct_minority` - Percent minority households
- `avg_time_since_admission` - Average months in program
- `pct_over_income_limit` - Households over-income (grandfathered)

### Development-Level Data
Available at project level with:
- `CODE` - Development code
- `DEVELOPMENT_NAME`
- Address and lat/long
- Units by bedroom size (0BR, 1BR, 2BR, 3BR, 4BR, 5+BR)
- Occupied and available units by size
- Development type (family, elderly, mixed)
- ACC units (under Annual Contributions Contract)

---

## Multifamily Assisted Housing

HUD multifamily programs provide project-based rental assistance in privately-owned properties.

### Programs
- **Section 8 Project-Based Rental Assistance**
- **Section 202** - Supportive housing for the elderly
- **Section 811** - Supportive housing for persons with disabilities
- **Section 236** - Interest reduction payments
- **Rent Supplement**
- **Rental Assistance Payment (RAP)**

### Picture of Subsidized Households - Multifamily

**Variables** (property-level, aggregable to county):
- `property_id` - Property ID
- `project_name` - Property name
- `address`, `city`, `state`, `zip`, `county_fips`
- `latitude`, `longitude`
- `program` - Program type
- `total_units` - Total units in property
- `assisted_units` - Units receiving assistance
- `occupancy` - Number of occupied assisted units
- `occupancy_rate` - Percent occupied
- `unit_type` - Elderly, family, disabled, mixed
- `avg_hh_income` - Average household income
- `pct_minority` - Percent minority
- `pct_elderly` - Percent elderly
- `subsidy_start_date` - Date property entered program
- `subsidy_end_date` - Expiration date (if applicable)
- `at_risk` - Property at risk of leaving program (Y/N)

---

## Homelessness Data

### Point-in-Time (PIT) Count

Annual count of sheltered and unsheltered homeless persons on a single night in January.

**Geographic Coverage**: Continuum of Care (CoC) areas (~400 CoCs, which may span multiple counties)

**Variables** (~50 variables per CoC per year):

#### Total Homeless Counts
- `Overall Homeless` - Total homeless persons
- `Sheltered Homeless` - In emergency shelter or transitional housing
- `Unsheltered Homeless` - On streets, cars, abandoned buildings, etc.

#### By Household Type
- `Homeless Individuals` - Adults without children
- `Homeless People in Families` - Adults and children in families
- `Homeless Parenting Youth` - Parents under 25
- `Homeless Parenting Children` - Children of parenting youth

#### By Subpopulation
- `Chronically Homeless Individuals`
- `Chronically Homeless People in Families`
- `Veterans` - Total homeless veterans
- `Unaccompanied Homeless Youth (Under 18)`
- `Unaccompanied Homeless Youth (Age 18-24)`
- `Severely Mentally Ill`
- `Chronic Substance Abuse`
- `Victims of Domestic Violence`
- `HIV/AIDS`

#### By Gender and Ethnicity
- `Male`, `Female`, `Transgender`, `Gender Non-Conforming`
- `Non-Hispanic/Non-Latino`, `Hispanic/Latino`
- `White`, `Black or African-American`, `Asian`, `American Indian/Alaska Native`, `Native Hawaiian/Other Pacific Islander`, `Multiple Races`

### Housing Inventory Count (HIC)

Annual inventory of homeless assistance beds and units.

**Variables**:
- Bed inventory by program type:
  - Emergency Shelter (ES)
  - Transitional Housing (TH)
  - Safe Haven (SH)
  - Permanent Supportive Housing (PSH)
  - Rapid Re-Housing (RRH)
  - Other Permanent Housing (OPH)
- Beds for families vs. individuals
- Year-round vs. seasonal beds
- HMIS participating beds (Homeless Management Information System)

### Continuum of Care (CoC) to County Crosswalk

**Problem**: CoCs do not align with county boundaries

**Solution**: HUD provides CoC-county crosswalk with population allocation
- `CoC_Code` - CoC identifier
- `County_FIPS` - County FIPS code
- `County_Name`
- `Population_Share` - % of CoC population in this county

**Aggregation Strategy**: Allocate CoC homeless counts to counties using population shares.

---

## Community Development Block Grants (CDBG)

CDBG provides funding to localities for community development activities (affordable housing, infrastructure, public services).

### Entitlement Communities (~1,200)
Cities with population >50,000 and urban counties with population >200,000 receive annual formula allocations.

### CDBG Variables (~30 variables per jurisdiction per year)

#### A. Allocation
- `GEOID` - Jurisdiction identifier
- `GRANTEE` - Entitlement jurisdiction name
- `STATE`
- `PROGRAM_YEAR` - Federal fiscal year
- `CDBG_FORMULA_ALLOCATION` - Total CDBG grant amount
- `PROGRAM_INCOME_RECEIVED` - Additional funds from loan repayments, etc.
- `TOTAL_AVAILABLE` - Allocation + program income + prior year balance

#### B. Expenditures by Activity Type
- `ACQUISITION` - Property acquisition
- `ADMIN` - Administration and planning
- `ECONOMIC_DEVELOPMENT` - Job creation, business assistance
- `HOUSING` - Housing rehabilitation, new construction, homebuyer assistance
- `PUBLIC_FACILITIES` - Infrastructure (water/sewer, streets, community centers)
- `PUBLIC_SERVICES` - Services for low/mod income persons (capped at 15% of grant)
- `OTHER`

#### C. National Objectives
All CDBG activities must meet a national objective:
- `LMI_AREA` - Benefit to low/mod income (LMI) area (51%+ LMI residents)
- `LMI_LIMITED_CLIENTELE` - Direct benefit to LMI persons
- `LMI_HOUSING` - Housing for LMI households
- `SLUM_BLIGHT` - Slum/blight elimination
- `URGENT_NEED` - Urgent community need (disasters, etc.)

#### D. Accomplishments
- `HOUSEHOLDS_ASSISTED` - Number of households assisted
- `PERSONS_ASSISTED` - Number of persons assisted
- `JOBS_CREATED` - Jobs created/retained
- `HOUSING_UNITS_REHABBED` - Housing units rehabilitated
- `HOUSING_UNITS_CONSTRUCTED` - New housing units constructed
- `PUBLIC_FACILITY_PERSONS_SERVED` - Persons served by public facilities

### State CDBG (Non-Entitlement)
States administer CDBG for non-entitlement areas (small cities and rural counties). Data are reported at state level, but specific project information may enable county-level allocation.

---

## HOME Investment Partnerships

HOME provides formula grants to states and localities for affordable housing (rental assistance, rehabilitation, new construction, homebuyer assistance).

### HOME Variables (~40 variables per jurisdiction per year)

#### A. Allocation & Budget
- `JURISDICTION` - Participating Jurisdiction (PJ) name
- `STATE`
- `PROGRAM_YEAR`
- `HOME_ALLOCATION` - Annual formula allocation
- `COMMITTED_AMOUNT` - Funds committed to projects
- `DISBURSED_AMOUNT` - Funds disbursed
- `BALANCE` - Unspent funds

#### B. Projects by Activity Type
- `RENTAL_NEW_CONSTRUCTION` - Units of rental housing, new construction
- `RENTAL_REHAB` - Units of rental housing, rehabilitation
- `HOMEBUYER_NEW` - Homebuyer assistance, new construction
- `HOMEBUYER_REHAB` - Homebuyer assistance, rehabilitation
- `HOMEOWNER_REHAB` - Homeowner rehabilitation
- `TBRA` - Tenant-Based Rental Assistance (vouchers)

#### C. Household Income Targeting
HOME requires projects serve households ≤80% AMI, with 90% of renter households ≤60% AMI.
- `HOUSEHOLDS_LT30_AMI` - Households <30% AMI
- `HOUSEHOLDS_30TO50_AMI` - 30-50% AMI
- `HOUSEHOLDS_50TO60_AMI` - 50-60% AMI
- `HOUSEHOLDS_60TO80_AMI` - 60-80% AMI

#### D. Racial/Ethnic Composition
- `WHITE`, `BLACK`, `ASIAN`, `NATIVE_AMERICAN`, `PACIFIC_ISLANDER`, `HISPANIC`

---

## FHFA House Price Index

The Federal Housing Finance Agency (FHFA) produces the most comprehensive house price index (HPI) for the US, based on repeat sales of single-family homes with mortgages sold to or guaranteed by Fannie Mae or Freddie Mac.

### Geographic Coverage
- **National** - US aggregate
- **Census Divisions** - 9 divisions
- **States** - All 50 states + DC
- **Metropolitan Areas** - ~400 metros
- **Counties** - ~3,000 counties (coverage depends on transaction volume)

### HPI Variables

#### A. Index Values
- `HPI` - House Price Index (100 = base period, typically 1980 Q1 or 1991 Q1)
- `HPI_SA` - Seasonally adjusted HPI
- `HPI_NSA` - Not seasonally adjusted HPI

#### B. Growth Rates
- `CHANGE_1YR` - 1-year percent change
- `CHANGE_5YR` - 5-year percent change
- `CHANGE_SINCE_PEAK` - Percent change since pre-recession peak (2007)
- `CHANGE_SINCE_TROUGH` - Percent change since recession trough (varies by area)

#### C. Time Periods
- **Quarterly**: 1975 Q1 - present (for most geographies)
- **Monthly**: 1991 - present (metro and state level)
- **Annual**: 1975 - present

#### D. Additional Metrics (Distressed Sales Index)
FHFA also produces a separate index excluding distressed sales (foreclosures, short sales).

### Expanded-Data HPI
Uses additional data sources beyond Fannie/Freddie (FHA, county recorder offices) for more comprehensive coverage, especially in rural areas.

---

## County-Level Aggregation Strategies

### Strategy 1: Direct County Aggregation (FMR, CHAS, Assisted Housing)
Most HUD datasets are available with county FIPS codes.

**Steps:**
1. Filter to target year
2. Group by county FIPS
3. Aggregate:
   - **Counts**: Sum (e.g., total vouchers)
   - **Rates**: Calculate from numerators and denominators (e.g., cost burden rate = cost burdened HH / total HH)
   - **Averages**: Household-weighted means (e.g., average income)

**Example:**
```r
county_vouchers <- voucher_data %>%
  group_by(county_fips, year) %>%
  summarise(
    total_vouchers = sum(number_assisted, na.rm = TRUE),
    avg_income = weighted.mean(avg_hh_income, w = number_assisted, na.rm = TRUE),
    pct_extremely_low = weighted.mean(pct_lt30_ami, w = number_assisted, na.rm = TRUE)
  )
```

### Strategy 2: CoC to County Allocation (Homelessness)
Continuum of Care areas do not align with counties. Use population allocation crosswalk.

**Steps:**
1. Join PIT data to CoC-county crosswalk
2. Allocate counts: `county_homeless = coc_homeless * population_share`
3. Sum across all CoCs touching the county

**Example:**
```r
coc_county_xwalk <- read_csv("coc_county_crosswalk.csv")

county_homeless <- pit_data %>%
  left_join(coc_county_xwalk, by = "coc_code") %>%
  mutate(
    overall_homeless_allocated = overall_homeless * population_share,
    sheltered_allocated = sheltered_homeless * population_share,
    unsheltered_allocated = unsheltered_homeless * population_share
  ) %>%
  group_by(county_fips, year) %>%
  summarise(
    overall_homeless = sum(overall_homeless_allocated, na.rm = TRUE),
    sheltered_homeless = sum(sheltered_allocated, na.rm = TRUE),
    unsheltered_homeless = sum(unsheltered_allocated, na.rm = TRUE)
  )
```

### Strategy 3: Jurisdiction to County (CDBG, HOME)
CDBG and HOME entitlements are jurisdictions (cities, counties). Some cities do not align with county boundaries (though most do).

**Simple Approach**: Assign each entitlement to its primary county.

**Complex Approach**: Use jurisdiction boundaries to spatially allocate expenditures to counties (requires GIS).

---

## Access Methods & APIs

### 1. HUD User Portal (Primary Data Source)
**URL:** https://www.huduser.gov/portal/datasets/

**Datasets:**
- Fair Market Rents (FMR)
- Income Limits
- CHAS (Comprehensive Housing Affordability Strategy)
- Picture of Subsidized Households
- Longitudinal Tract Database (LTDB)
- USPS ZIP Code Crosswalk Files

**Format:** Excel, CSV, SAS, SPSS
**Access:** Direct download, no registration required

### 2. HUD Data APIs

#### A. HUD User Data API (Limited Endpoints)
**URL:** https://www.huduser.gov/hudapi/public/

**Endpoints:**
- Fair Market Rents: `GET /fmr/data/{state_code}?year={year}`
- Income Limits: `GET /il/data/{state_code}?year={year}`

**Authentication:** No API key required
**Rate Limit:** Not specified (reasonable use)
**Format:** JSON

**Example:**
```
GET https://www.huduser.gov/hudapi/public/fmr/data/CA?year=2024
```

#### B. HUD eGIS Open Data Portal
**URL:** https://hudgis-hud.opendata.arcgis.com/

**Datasets:**
- Assisted housing properties (point locations)
- HUD program boundaries
- Qualified Census Tracts
- Difficult Development Areas
- Public Housing Authorities

**Format:** Shapefile, KML, GeoJSON, CSV
**API:** ArcGIS REST API

**Example Query:**
```
GET https://services.arcgis.com/VTyQ9soqVukalItT/arcgis/rest/services/Assisted_Housing_and_Properties/FeatureServer/0/query?where=STATE='CA'&outFields=*&f=json
```

### 3. CHAS Data Downloads
**URL:** https://www.huduser.gov/portal/datasets/cp.html

**Files:** 19 tables per geography per period
**Format:** CSV with data dictionary
**Years:** 2006-2021 (5-year ACS)

### 4. HUD Exchange (PIT & HIC Data)
**URL:** https://www.hudexchange.info/programs/coc/coc-homeless-populations-and-subpopulations-reports/

**Datasets:**
- Point-in-Time (PIT) counts
- Housing Inventory Count (HIC)
- Continuum of Care boundaries

**Format:** Excel, CSV
**Access:** Direct download

### 5. FHFA House Price Index
**URL:** https://www.fhfa.gov/DataTools/Downloads/Pages/House-Price-Index-Datasets.aspx

**Files:**
- HPI by state (quarterly, annual)
- HPI by metro (quarterly, monthly)
- HPI by county (quarterly, annual)
- Expanded-data HPI

**Format:** CSV, Excel
**API:** Not available (bulk download only)

---

## R Packages & Code Examples

### 1. `tidycensus` Package (for CHAS via ACS)

While CHAS is a special tabulation, many variables are available in standard ACS tables through `tidycensus`.

**Installation:**
```r
install.packages("tidycensus")
library(tidycensus)

# Set API key
census_api_key("YOUR_KEY")
```

**Get housing cost burden (closest ACS equivalent to CHAS):**
```r
# B25070: Gross Rent as Percentage of Household Income
rent_burden <- get_acs(
  geography = "county",
  variables = c(
    total = "B25070_001",
    burden_30to35 = "B25070_007",
    burden_35to40 = "B25070_008",
    burden_40to50 = "B25070_009",
    burden_50plus = "B25070_010"
  ),
  year = 2021,
  survey = "acs5"
) %>%
  select(GEOID, NAME, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  mutate(
    cost_burden_moderate = burden_30to35 + burden_35to40,
    cost_burden_severe = burden_40to50 + burden_50plus,
    pct_cost_burden_severe = cost_burden_severe / total * 100
  )
```

### 2. Direct HUD Data Downloads

**Download Fair Market Rents:**
```r
library(tidyverse)
library(readxl)

# FMR are released annually; URL pattern is consistent
# Example: FY 2024 FMRs
url_fmr <- "https://www.huduser.gov/portal/datasets/fmr/fmr2024/FY2024_4050_RevFinal.xlsx"

# Download to temp file
temp <- tempfile(fileext = ".xlsx")
download.file(url_fmr, temp, mode = "wb")

# Read Excel file (usually "FY 2024 FMRs" sheet or similar)
fmr_2024 <- read_excel(temp, sheet = 1)

# Clean and select key variables
fmr_clean <- fmr_2024 %>%
  select(
    fips = `FIPS Code`,
    state = State,
    county = `Area Name`,
    fmr_0br = `FMR 0BR`,
    fmr_1br = `FMR 1BR`,
    fmr_2br = `FMR 2BR`,
    fmr_3br = `FMR 3BR`,
    fmr_4br = `FMR 4BR`
  ) %>%
  mutate(fips = str_pad(fips, 5, pad = "0"))
```

**Download Picture of Subsidized Households:**
```r
# HUD releases annual CSV files
# Example: 2023 data
url_psh <- "https://www.huduser.gov/portal/datasets/assthsg/2023_all.csv"

subsidized_2023 <- read_csv(url_psh)

# Aggregate to county level
county_subsidized <- subsidized_2023 %>%
  mutate(county_fips = str_pad(code, 5, "0")) %>%
  group_by(county_fips, state) %>%
  summarise(
    total_units = sum(number_reported, na.rm = TRUE),
    total_assisted = sum(number_assisted, na.rm = TRUE),
    avg_hh_income = weighted.mean(average_hh_income, w = number_assisted, na.rm = TRUE),
    pct_extremely_low = weighted.mean(percent_lt_50_ami, w = number_assisted, na.rm = TRUE),
    pct_minority = weighted.mean(percent_minority, w = number_assisted, na.rm = TRUE),
    .groups = "drop"
  )
```

**Download CHAS Data:**
```r
# CHAS files are organized by table number
# Example: Table 9 (cost burden by race/ethnicity)
# 2017-2021 CHAS data

url_chas <- "https://www.huduser.gov/portal/datasets/cp/CHAS/data_2017_2021/Table9.csv"

chas_t9 <- read_csv(url_chas)

# CHAS data have complex structure; consult data dictionary
# Example: Extract county-level cost burden for renters
county_cost_burden <- chas_t9 %>%
  filter(
    sumlevel == 50,  # County level
    tenure == 2      # Renters (1=owner, 2=renter, 3=all)
  ) %>%
  mutate(
    county_fips = paste0(st, cnty),
    cost_burden_severe = T9_est4 + T9_est9 + T9_est14 + T9_est19  # Sum across races
  ) %>%
  select(county_fips, name, cost_burden_severe)
```

### 3. FHFA House Price Index

**Download county HPI:**
```r
# FHFA provides CSV files updated quarterly
url_hpi <- "https://www.fhfa.gov/DataTools/Downloads/Documents/HPI/HPI_AT_BDL_county.csv"

hpi_county <- read_csv(url_hpi)

# Filter to most recent year and calculate changes
hpi_recent <- hpi_county %>%
  filter(yr == 2024, period == 1) %>%  # Q1 2024
  select(
    county_fips = fips,
    state,
    county,
    hpi = index_nsa,
    change_1yr = index_nsa_1yr,
    change_5yr = index_nsa_5yr
  )
```

### 4. Homelessness PIT Data

**Download and process PIT counts:**
```r
# PIT data are released annually via HUD Exchange
# Example: 2023 PIT (released late 2024)
url_pit <- "https://www.hudexchange.info/resource/3031/2023-ahar-part-1-pit-estimates-of-homelessness-in-the-us/"

# HUD provides Excel files; structure varies by year
# Typically: One row per CoC, columns for subpopulations

# Assuming file has been downloaded locally:
pit_2023 <- read_excel("2023_PIT_Counts_by_CoC.xlsx")

# Load CoC-county crosswalk
coc_xwalk <- read_csv("coc_county_population_crosswalk.csv")

# Allocate to counties
county_pit <- pit_2023 %>%
  left_join(coc_xwalk, by = c("CoC Number" = "coc_code")) %>%
  mutate(
    overall_allocated = `Overall Homeless` * population_share,
    sheltered_allocated = `Sheltered Homeless` * population_share,
    unsheltered_allocated = `Unsheltered Homeless` * population_share
  ) %>%
  group_by(county_fips) %>%
  summarise(
    overall_homeless = sum(overall_allocated, na.rm = TRUE),
    sheltered = sum(sheltered_allocated, na.rm = TRUE),
    unsheltered = sum(unsheltered_allocated, na.rm = TRUE)
  )
```

---

## Data Quality & Limitations

### Fair Market Rents

**Strengths:**
- Complete county coverage
- Long time series (1983+)
- Annual updates

**Limitations:**
- FMRs are 40th percentile (not median or mean)
- Based on ACS and recent mover surveys (may lag market changes)
- Metropolitan FMRs apply uniformly to all counties in metro (until SAFMRs implemented)
- Do not reflect actual rents paid, only benchmarks for voucher program

### Assisted Housing

**Strengths:**
- Comprehensive (all HUD-assisted units)
- Property and household detail
- Annual updates

**Limitations:**
- Excludes non-HUD affordable housing (LIHTC-only properties, state/local programs)
- Household characteristics are aggregated (no microdata)
- Some small PHAs may not report consistently
- Project-level addresses may be suppressed for privacy

### CHAS

**Strengths:**
- Special tabulations not available in standard ACS
- Consistent definitions across geographies
- Margin of error provided (important for small counties)

**Limitations:**
- Based on ACS (sample survey, not full count)
- 5-year data (lags current year by 1-2 years)
- Small counties/tracts may have large MOE (combine years or use caution)
- Area Median Income calculated by HUD; varies by metro/county definition

### Homelessness (PIT)

**Strengths:**
- Only comprehensive national homeless count
- Sheltered vs. unsheltered breakdown
- Detailed subpopulations

**Limitations:**
- **Single-night count**: Snapshot, not annual prevalence
- **Undercount likely**: Especially unsheltered (hard-to-reach locations)
- **CoC geography**: Does not align with counties; allocation required
- **Methodology variation**: CoCs use different counting methods (some more rigorous than others)
- **Weather**: January count may miss seasonal homeless (in some climates)

### CDBG/HOME

**Strengths:**
- Detailed activity and accomplishment data
- Long time series

**Limitations:**
- Entitlement-only (excludes state-administered non-entitlement areas in CDBG reporting)
- Multi-year projects (expenditures may not match allocation year)
- Accomplishments self-reported by grantees (vary in quality)

### FHFA HPI

**Strengths:**
- Repeat-sales methodology (controls for quality)
- Long time series
- Consistent methodology

**Limitations:**
- Fannie/Freddie mortgages only (excludes FHA, VA, cash sales in standard HPI)
- Single-family homes only (no condos, multifamily)
- Rural counties with low transaction volume may have gaps or high volatility
- Does not reflect home prices for new buyers (includes refinances)

---

## Priority Variables for Collection

For a **county-level housing dataset**, the following are highest-priority HUD variables:

### Tier 1: Affordability & Cost Burden (CHAS)
1. **Percent households cost burdened (>30% income on housing)**
2. **Percent severely cost burdened (>50% income on housing)**
3. **Median gross rent**
4. **Median home value**
5. **Homeownership rate**

### Tier 2: Assisted Housing (Picture of Subsidized Households)
6. **Total HUD-assisted units** (all programs)
7. **Housing Choice Vouchers** (tenant-based assistance count)
8. **Public housing units**
9. **Utilization rate** (vouchers in use / allocated)
10. **Percent assisted households extremely low income (<30% AMI)**

### Tier 3: Fair Market Rents
11. **FMR 2-bedroom** (most common voucher size)
12. **FMR 1-bedroom**
13. **Ratio of FMR to median renter income** (affordability index)

### Tier 4: Housing Problems (CHAS)
14. **Percent households with any housing problem** (cost burden, overcrowding, or inadequate facilities)
15. **Percent overcrowded (>1.01 persons per room)**
16. **Percent incomplete kitchen or plumbing**

### Tier 5: Homelessness (PIT)
17. **Total homeless persons**
18. **Unsheltered homeless count**
19. **Chronically homeless count**
20. **Homeless veterans**

### Tier 6: House Prices (FHFA HPI)
21. **House Price Index** (current quarter)
22. **1-year HPI change**
23. **5-year HPI change**
24. **Change since peak (2007)**

### Tier 7: Community Development
25. **CDBG allocation** (total dollars)
26. **HOME allocation**
27. **CDBG households assisted**

---

## Quick Reference

### Key URLs

| Resource | URL |
|----------|-----|
| **HUD User Home** | https://www.huduser.gov/ |
| **Fair Market Rents** | https://www.huduser.gov/portal/datasets/fmr.html |
| **CHAS Data** | https://www.huduser.gov/portal/datasets/cp.html |
| **Picture of Subsidized Households** | https://www.huduser.gov/portal/datasets/assthsg.html |
| **PIT & HIC Data** | https://www.hudexchange.info/programs/coc/coc-homeless-populations-and-subpopulations-reports/ |
| **CDBG Data** | https://www.hudexchange.info/programs/cdbg/ |
| **HOME Data** | https://www.hudexchange.info/programs/home/ |
| **HUD eGIS Open Data** | https://hudgis-hud.opendata.arcgis.com/ |
| **FHFA HPI** | https://www.fhfa.gov/DataTools/Downloads/Pages/House-Price-Index-Datasets.aspx |

### Key R Packages

| Package | Purpose | Installation |
|---------|---------|--------------|
| `tidycensus` | Access ACS housing data (closest to CHAS) | `install.packages("tidycensus")` |
| `tigris` | County shapefiles | `install.packages("tigris")` |
| `readxl` | Read HUD Excel files | `install.packages("readxl")` |
| `sf` | Spatial joins for geocoded properties | `install.packages("sf")` |

### Contact

**HUD User:**
- Email: helpdesk@huduser.gov
- Phone: 1-800-245-2691

**HUD Exchange:**
- Email: https://www.hudexchange.info/help-desk/
- Phone: 1-877-935-9270

---

## Example Complete Workflow: County Housing Profile

```r
library(tidyverse)
library(tidycensus)
library(readxl)

# Set Census API key
census_api_key("YOUR_KEY")

# 1. Get Fair Market Rents
url_fmr <- "https://www.huduser.gov/portal/datasets/fmr/fmr2024/FY2024_4050_RevFinal.xlsx"
temp <- tempfile(fileext = ".xlsx")
download.file(url_fmr, temp, mode = "wb")
fmr_2024 <- read_excel(temp, sheet = 1)

county_fmr <- fmr_2024 %>%
  select(
    fips = `FIPS Code`,
    state = State,
    fmr_2br = `FMR 2BR`
  ) %>%
  mutate(fips = str_pad(fips, 5, "0"))

# 2. Get CHAS cost burden data
url_chas_t1 <- "https://www.huduser.gov/portal/datasets/cp/CHAS/data_2017_2021/Table1.csv"
chas_t1 <- read_csv(url_chas_t1)

county_chas <- chas_t1 %>%
  filter(sumlevel == 50) %>%  # County level
  mutate(
    county_fips = paste0(st, cnty),
    # Sum households with cost burden >30%
    cost_burden_total = T1_est2 + T1_est3 + T1_est6 + T1_est7 + T1_est10 + T1_est11,
    # Total households
    total_hh = T1_est1 + T1_est2 + T1_est3 + T1_est4,
    pct_cost_burden = cost_burden_total / total_hh * 100
  ) %>%
  select(county_fips, name, pct_cost_burden)

# 3. Get assisted housing data
url_psh <- "https://www.huduser.gov/portal/datasets/assthsg/2023_all.csv"
psh_2023 <- read_csv(url_psh)

county_assisted <- psh_2023 %>%
  mutate(county_fips = str_pad(code, 5, "0")) %>%
  group_by(county_fips) %>%
  summarise(
    total_assisted_units = sum(number_assisted, na.rm = TRUE),
    avg_hh_income = weighted.mean(average_hh_income, w = number_assisted, na.rm = TRUE)
  )

# 4. Get FHFA House Price Index
url_hpi <- "https://www.fhfa.gov/DataTools/Downloads/Documents/HPI/HPI_AT_BDL_county.csv"
hpi_county <- read_csv(url_hpi)

county_hpi <- hpi_county %>%
  filter(yr == 2024, period == 1) %>%
  select(
    county_fips = fips,
    hpi = index_nsa,
    hpi_1yr_change = index_nsa_1yr
  )

# 5. Get ACS median renter income for affordability calculation
acs_income <- get_acs(
  geography = "county",
  variables = "B25119_003",  # Median household income (renter-occupied)
  year = 2021,
  survey = "acs5"
) %>%
  select(county_fips = GEOID, median_renter_income = estimate)

# 6. Combine all
county_housing_profile <- county_fmr %>%
  left_join(county_chas, by = c("fips" = "county_fips")) %>%
  left_join(county_assisted, by = c("fips" = "county_fips")) %>%
  left_join(county_hpi, by = c("fips" = "county_fips")) %>%
  left_join(acs_income, by = c("fips" = "county_fips")) %>%
  mutate(
    # Affordability: annual FMR as % of median renter income
    fmr_annual = fmr_2br * 12,
    fmr_burden_pct = (fmr_annual / median_renter_income) * 100
  )

# 7. Export
write_csv(county_housing_profile, "county_housing_data.csv")
```

---

## Changelog

**Version 1.0 (2025-11-11)**
- Initial comprehensive documentation
- All major HUD data systems documented (FMR, CHAS, Assisted Housing, PIT, CDBG, HOME)
- FHFA House Price Index included
- County aggregation strategies detailed
- Complete R code examples
- HUD APIs and bulk download methods documented

---

## Citation

When using HUD data, cite the specific source:

**Fair Market Rents:**
```
U.S. Department of Housing and Urban Development, Office of Policy Development and Research.
Fair Market Rents for the Housing Choice Voucher Program, Fiscal Year 2024.
```

**CHAS:**
```
U.S. Department of Housing and Urban Development, Office of Policy Development and Research.
HUD CHAS Data, 2017-2021. Based on American Community Survey 5-year data.
```

**Picture of Subsidized Households:**
```
U.S. Department of Housing and Urban Development, Office of Policy Development and Research.
A Picture of Subsidized Households, 2023.
```

**Point-in-Time Count:**
```
U.S. Department of Housing and Urban Development, Office of Community Planning and Development.
The 2023 Annual Homeless Assessment Report (AHAR) to Congress, Part 1: Point-in-Time Estimates of Homelessness.
```

**FHFA HPI:**
```
Federal Housing Finance Agency. House Price Index, [Geography], [Quarter/Year].
```

---

**Document Status:** ✅ Complete
**Last Updated:** November 11, 2025
**Next Update:** As needed for new HUD data releases
