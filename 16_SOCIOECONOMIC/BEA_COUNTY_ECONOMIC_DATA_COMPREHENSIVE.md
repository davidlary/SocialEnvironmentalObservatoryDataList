# Bureau of Economic Analysis (BEA) County-Level Economic Data
## COMPREHENSIVE DOCUMENTATION - ALL AVAILABLE VARIABLES

**Last Updated:** November 11, 2025
**Data Current Through:** 2023 (varies by dataset)
**BEA API Documentation:** https://apps.bea.gov/api/bea_web_service_api_user_guide.htm

---

## EXECUTIVE SUMMARY

The Bureau of Economic Analysis provides comprehensive county-level economic data through three main categories:
1. **GDP by County** (2017-2023, with 2001-2016 to be released)
2. **Personal Income** (1969-2023 with revisions)
3. **Employment** (DISCONTINUED November 14, 2024 due to budget constraints)

**CRITICAL CHANGE (December 3, 2025):** BEA will combine county-level GDP and personal income into one news release. Metropolitan and micropolitan area statistics will be discontinued, though county-level data will continue.

---

## TABLE OF CONTENTS

1. [GDP by County](#1-gdp-by-county)
2. [Personal Income (Complete Component Breakdown)](#2-personal-income-complete-component-breakdown)
3. [Earnings by Industry](#3-earnings-by-industry)
4. [Employment by Industry](#4-employment-by-industry-discontinued)
5. [Regional Price Parities](#5-regional-price-parities-rpp)
6. [Data Access Methods](#6-data-access-methods)
7. [Data Quality and Methodology](#7-data-quality-and-methodology)
8. [Code Examples](#8-code-examples)

---

## 1. GDP BY COUNTY

### Overview
County GDP measures the value of goods and services produced by the county's economy less the value of goods and services used up in production.

### 1.1 Available Tables

#### CAGDP1 - County and MSA GDP Summary
- **Description:** GDP summary statistics by county and metropolitan area
- **Units:** Various (dollars, population, per capita)
- **Years:** 2017-2023 (2001-2016 planned for future release)
- **Geography:** All counties
- **Update:** Annual, December
- **Most Recent:** December 4, 2024 (2023 data)
- **Next Release:** December 3, 2025

**Key Line Codes:**
- Line 1: All industry total GDP
- Line 2: Population (persons)
- Line 3: Per capita real GDP

#### CAGDP2 - GDP in Current Dollars by County and MSA
- **Description:** GDP by county/MSA with industry detail in current dollars
- **Units:** Thousands of dollars
- **Years:** 2017-2023
- **Geography:** All counties (3,113 counties)
- **Industry Detail:** 21 published industries (see Section 1.3)
- **Suppression:** Yes - to protect confidentiality
- **API Dataset:** Regional
- **API TableName:** CAGDP2

**Line Codes by Industry (Current Dollars):**
- Line 1: All industry total
- Line 2: Agriculture, forestry, fishing, and hunting
- Line 3: Mining, quarrying, and oil and gas extraction
- Line 4: Utilities
- Line 5: Construction
- Line 6: Manufacturing
- Line 7: Wholesale trade
- Line 8: Retail trade
- Line 9: Transportation and warehousing
- Line 10: Information
- Line 11: Finance and insurance
- Line 12: Real estate and rental and leasing
- Line 13: Professional, scientific, and technical services
- Line 14: Management of companies and enterprises
- Line 15: Administrative and support and waste management services
- Line 16: Educational services
- Line 17: Health care and social assistance
- Line 18: Arts, entertainment, and recreation
- Line 19: Accommodation and food services
- Line 20: Other services (except public administration)
- Line 21: Government and government enterprises

#### CAGDP8 - Chain-Type Quantity Indexes for Real GDP
- **Description:** Chain-type quantity indexes for real GDP (2017=100.0)
- **Units:** Index (2017=100)
- **Years:** 2017-2023
- **Geography:** All counties
- **Industry Detail:** Same 21 industries as CAGDP2
- **Use:** Measuring real GDP changes over time

#### CAGDP9 - Real GDP in Chained Dollars
- **Description:** Real GDP by county and MSA in chained dollars
- **Units:** Chained 2017 dollars (thousands)
- **Years:** 2017-2023
- **Geography:** All counties
- **Industry Detail:** Same 21 industries as CAGDP2
- **Calculation:** Derived by applying national chain-type price indexes to current dollar values

**Key Line Codes (same structure as CAGDP2):**
- Line codes 1-21 (same industries as CAGDP2)

#### CAGDP10 - Per Capita Real GDP
- **Description:** Per capita real GDP by county and MSA
- **Units:** Chained 2017 dollars per person
- **Years:** 2017-2023
- **Geography:** All counties
- **Calculation:** Real GDP divided by population

#### CAGDP11 - Contributions to Percent Change in Real GDP
- **Description:** Contributions to percent change in real GDP by industry
- **Units:** Percentage points
- **Years:** 2017-2023 (annual percent changes)
- **Geography:** All counties
- **Industry Detail:** Same 21 industries as CAGDP2
- **Use:** Measuring each industry's contribution to overall GDP growth

**Interpretation:** Contributions are additive and sum to the county's overall percent change in real GDP.

### 1.2 Methodology

**Estimation Approach:**
- BEA uses the **income approach** to measure county GDP due to limited geographic detail in final expenditure data
- GDP = Compensation of employees + Taxes on production and imports less subsidies + Gross operating surplus

**Industry Detail:**
- **Published:** 21 distinct industry sectors
- **Estimated:** 65 detailed NAICS-based industries (used in calculation, then aggregated to 21 for publication)

**Data Sources:**
- Quarterly Census of Employment and Wages (QCEW)
- National Establishment Time Series (NETS) sales data
- Economic Census data
- Industry-specific data from various sources
- National chain-type price indexes

**Reference Year:** 2017 for chained-dollar estimates and index numbers

**Methodology Documents:**
- "Local Area Gross Domestic Product Methodology" (Survey of Current Business, March 2020)
- "An Overview of the GDP by County Methodology" (one-page PDF)
- Available at: https://www.bea.gov/data/gdp/gdp-county-metro-and-other-areas

### 1.3 Published Industry Classification (21 Industries)

The 21 published industries for county GDP are aggregations of 65 detailed NAICS-based industries:

1. **Agriculture, forestry, fishing, and hunting** (NAICS 11)
2. **Mining, quarrying, and oil and gas extraction** (NAICS 21)
3. **Utilities** (NAICS 22)
4. **Construction** (NAICS 23)
5. **Manufacturing** (NAICS 31-33)
   - Durable goods manufacturing
   - Nondurable goods manufacturing
6. **Wholesale trade** (NAICS 42)
7. **Retail trade** (NAICS 44-45)
8. **Transportation and warehousing** (NAICS 48-49)
9. **Information** (NAICS 51)
10. **Finance and insurance** (NAICS 52)
11. **Real estate and rental and leasing** (NAICS 53)
12. **Professional, scientific, and technical services** (NAICS 54)
13. **Management of companies and enterprises** (NAICS 55)
14. **Administrative and support and waste management and remediation services** (NAICS 56)
15. **Educational services** (NAICS 61)
16. **Health care and social assistance** (NAICS 62)
17. **Arts, entertainment, and recreation** (NAICS 71)
18. **Accommodation and food services** (NAICS 72)
19. **Other services (except public administration)** (NAICS 81)
20. **Government and government enterprises**
    - Federal civilian
    - Federal military
    - State and local
21. **All industry total**

**Note:** While BEA publishes 21 industries, the underlying calculations use 65 detailed NAICS-based industries. The complete mapping is available in BEA's "Industry Names to NAICS Codes" document (Excel file) at the GDP by County data page.

### 1.4 Years Available

| Data Type | Years Available | Status |
|-----------|----------------|---------|
| Current dollar GDP | 2017-2023 | Available |
| Real GDP (chained 2017 dollars) | 2017-2023 | Available |
| Chain-type quantity indexes | 2017-2023 | Available |
| Contributions to growth | 2018-2023 | Available (percent changes) |
| Historical (2001-2016) | Pending | To be released at later date |

**First Official Release:** December 12, 2019 (prototype estimates)

### 1.5 Geographic Coverage

- **Total Counties:** 3,113 counties (as of 2023)
- **Coverage:** All U.S. counties
- **Suppression:** Data may be suppressed for confidentiality in counties with:
  - Too few employers in an industry
  - Single employer dominance
  - Large state/local government role

---

## 2. PERSONAL INCOME (COMPLETE COMPONENT BREAKDOWN)

### Overview
Personal income is the income received by, or on behalf of, all persons from all sources: from participation in production, from owning a home or business, from ownership of financial assets, and from government and business transfers.

**Historical Coverage:** 1969-2023 (with comprehensive revisions through November 2023)

### 2.1 CAINC1 - Annual Personal Income Summary

**Description:** County and MSA personal income summary with basic statistics

**Years Available:** 1969-2023 (annual)

**Key Line Codes:**
- Line 1: Personal income (thousands of dollars)
- Line 2: Population (persons)
- Line 3: Per capita personal income (dollars)

**Units:**
- Personal income: Thousands of dollars
- Population: Persons
- Per capita: Dollars

**API Parameters:**
- Dataset: Regional
- TableName: CAINC1
- LineCode: 1, 2, or 3
- GeoFips: COUNTY (all counties) or specific FIPS codes
- Year: 1969-2023

### 2.2 CAINC4 - Personal Income and Employment by Major Component

**Description:** Detailed breakdown of personal income components and employment

**Years Available:** 1969-2023 (NAICS basis from 2001; SIC basis 1969-2000)

**Complete Line Codes:**

#### Total Personal Income
- **Line 10:** Total personal income (thousands of dollars)
- **Line 20:** Total population (persons)
- **Line 30:** Per capita personal income (dollars)

#### Employment
- **Line 40:** Total employment (number of jobs)
- **Line 50:** Wage and salary employment
- **Line 60:** Proprietors employment

#### Net Earnings by Place of Residence
- **Line 45:** Net earnings by place of residence
- **Line 50:** Wages and salaries (from all industries)
- **Line 60:** Supplements to wages and salaries
  - Employer contributions for employee pension and insurance funds
  - Employer contributions for government social insurance
- **Line 70:** Proprietors' income
  - Farm proprietors' income
  - Nonfarm proprietors' income
- **Line 80:** Minus: Contributions for government social insurance (employee and self-employed)
- **Line 81:** Plus: Adjustment for residence

#### Dividends, Interest, and Rent
- **Line 46:** Dividends, interest, and rent
- **Line 100:** Dividend income
- **Line 110:** Personal interest income
- **Line 120:** Personal rental income

#### Transfer Receipts
- **Line 47:** Personal current transfer receipts
- Transfer receipts from government
- Transfer receipts from business
- Transfer receipts from persons

**Units:** Thousands of dollars (unless specified)

**API Parameters:**
- Dataset: Regional
- TableName: CAINC4
- LineCode: 10, 20, 30, 40, 45-47, 50, 60, 70, 80, 81, 100, 110, 120
- GeoFips: COUNTY or specific FIPS codes
- Year: 1969-2023

### 2.3 CAINC5N - Personal Income by Major Component and Earnings by NAICS Industry

**Description:** Most detailed personal income table with full industry breakdown of earnings

**Years Available:** 2001-2023 (NAICS basis)

**Related Table:** CAINC5S (SIC basis, 1969-2000)

**Major Components Include:**

#### Personal Income Total and Components
- Total personal income
- Net earnings by place of residence
- Dividends, interest, and rent
- Personal current transfer receipts

#### Earnings by NAICS Industry (Detailed)

**Farm Earnings:**
- Farm earnings
- Farm proprietors' income

**Forestry, Fishing, and Related Activities:**
- Forestry, fishing, and related activities
- Forestry and logging
- Fishing, hunting, and trapping
- Support activities for agriculture and forestry

**Mining, Quarrying, and Oil and Gas Extraction:**
- Mining, quarrying, and oil and gas extraction
- Oil and gas extraction
- Mining (except oil and gas)
- Support activities for mining

**Utilities:**
- Utilities

**Construction:**
- Construction
- Construction of buildings
- Heavy and civil engineering construction
- Specialty trade contractors

**Manufacturing:**
- Manufacturing
- Durable goods manufacturing
  - Wood product manufacturing
  - Nonmetallic mineral product manufacturing
  - Primary metal manufacturing
  - Fabricated metal product manufacturing
  - Machinery manufacturing
  - Computer and electronic product manufacturing
  - Electrical equipment, appliance, and component manufacturing
  - Motor vehicles, bodies and trailers, and parts manufacturing
  - Other transportation equipment manufacturing
  - Furniture and related product manufacturing
  - Miscellaneous manufacturing
- Nondurable goods manufacturing
  - Food and beverage and tobacco product manufacturing
  - Textile mills and textile product mills
  - Apparel manufacturing
  - Leather and allied product manufacturing
  - Paper manufacturing
  - Printing and related support activities
  - Petroleum and coal products manufacturing
  - Chemical manufacturing
  - Plastics and rubber products manufacturing

**Wholesale Trade:**
- Wholesale trade

**Retail Trade:**
- Retail trade
- Motor vehicle and parts dealers
- Food and beverage stores
- General merchandise stores
- Other retail

**Transportation and Warehousing:**
- Transportation and warehousing
- Air transportation
- Rail transportation
- Water transportation
- Truck transportation
- Transit and ground passenger transportation
- Pipeline transportation
- Other transportation and support activities
- Warehousing and storage

**Information:**
- Information
- Publishing industries (except Internet)
- Motion picture and sound recording industries
- Broadcasting and telecommunications
- Data processing, internet publishing, and other information services

**Finance and Insurance:**
- Finance and insurance
- Federal Reserve banks, credit intermediation, and related activities
- Securities, commodity contracts, and investments
- Insurance carriers and related activities
- Funds, trusts, and other financial vehicles

**Real Estate and Rental and Leasing:**
- Real estate and rental and leasing
- Real estate
- Rental and leasing services and lessors of intangible assets

**Professional, Scientific, and Technical Services:**
- Professional, scientific, and technical services
- Legal services
- Computer systems design and related services
- Miscellaneous professional, scientific, and technical services

**Management of Companies and Enterprises:**
- Management of companies and enterprises

**Administrative and Support and Waste Management and Remediation Services:**
- Administrative and support and waste management and remediation services
- Administrative and support services
- Waste management and remediation services

**Educational Services:**
- Educational services

**Health Care and Social Assistance:**
- Health care and social assistance
- Ambulatory health care services
- Hospitals
- Nursing and residential care facilities
- Social assistance

**Arts, Entertainment, and Recreation:**
- Arts, entertainment, and recreation
- Performing arts, spectator sports, museums, and related activities
- Amusements, gambling, and recreation industries

**Accommodation and Food Services:**
- Accommodation and food services
- Accommodation
- Food services and drinking places

**Other Services (except Public Administration):**
- Other services (except public administration)
- Repair and maintenance
- Personal and laundry services
- Religious, grantmaking, civic, professional, and similar organizations

**Government and Government Enterprises:**
- Government and government enterprises
- Federal civilian
- Military
- State and local
  - State government
  - Local government

**API Parameters:**
- Dataset: Regional
- TableName: CAINC5N
- LineCode: Multiple (use GetParameterValuesFiltered to discover all)
- GeoFips: COUNTY or specific FIPS codes
- Year: 2001-2023

**Note:** This is the most comprehensive earnings table available at the county level, with 3-digit NAICS detail in many sectors.

### 2.4 CAINC6N - Compensation of Employees by NAICS Industry

**Description:** Compensation of employees (wages + supplements) by detailed industry

**Years Available:** 2001-2023 (NAICS basis)

**Related Table:** CAINC6S (SIC basis, 1969-2000)

**Coverage:** Same industry detail as CAINC5N, but limited to compensation (excludes proprietors' income)

**Components:**
- Wages and salaries by industry
- Supplements to wages and salaries by industry

**Units:** Thousands of dollars

### 2.5 CAINC30 - Economic Profile by County

**Description:** Comprehensive economic profile with key indicators

**Years Available:** 1969-2023

**Variables Included:**
- Personal income (total and per capita)
- Population
- Employment by major categories
- Earnings by major industry sectors
- Transfer receipts (summary)
- Key demographic and economic indicators

**Important Note:** Lines 240-310 were eliminated in 2024 due to budget constraints.

**API Parameters:**
- Dataset: Regional
- TableName: CAINC30
- GeoFips: COUNTY or specific FIPS codes
- Year: 1969-2023

### 2.6 CAINC35 - Personal Current Transfer Receipts (DISCONTINUED)

**Description:** Detailed breakdown of transfer receipts by type

**Years Available:** 1969-2022

**DISCONTINUED:** November 14, 2024 due to budget constraints

**Line Codes (Historical):**

#### Total Government Transfers
- **Line 1000:** Total government transfers

#### Retirement and Disability
- **Line 2000:** Retirement and disability insurance benefits (total)
- **Line 2100:** Retirement and disability insurance benefits (including Social Security)
- **Line 2110:** Social Security transfers (excluding disability)
- **Line 2120:** Disability insurance benefits

#### Medical Benefits
- **Line 2200:** Medical benefits (total)
  - Medicare transfers
  - **Line 2220:** Medicaid transfers
  - Military medical insurance benefits

#### Income Maintenance
- **Line 2300:** Income maintenance benefits
  - Supplemental Security Income (SSI)
  - Supplemental Nutrition Assistance Program (SNAP)
  - Family assistance
  - Other income maintenance

#### Unemployment Insurance
- **Line 2400:** Unemployment insurance benefits

#### Veterans Benefits
- **Line 2500:** Veterans benefits

#### Education and Training
- **Line 2600:** Education and training assistance

#### Other Transfers
- **Line 3000:** Net current transfer receipts from business
- **Line 4000:** Net current transfer receipts from persons

**Status:** Data through 2022 remains available; no future updates will be published.

### 2.7 CAINC45 - Farm Income and Expenses (DISCONTINUED)

**Description:** Detailed farm income and expenses by county

**Years Available:** 1969-2022

**DISCONTINUED:** November 14, 2024 due to budget constraints

**Components (Historical):**
- Farm income (total)
- Farm cash receipts
- Farm production expenses
- Net farm income
- Farm proprietors' income

**Units:** Thousands of dollars

### 2.8 CAINC91 - Gross Flow of Earnings

**Description:** Earnings by place of work vs. place of residence (commuting flows)

**Years Available:** 2001-2014

**Components:**
- Earnings by place of work
- Earnings by place of residence
- Adjustment for residence (net commuting flows)

**Use:** Analyzing commuting patterns and earnings flows between counties

**Units:** Thousands of dollars

### 2.9 Personal Income Methodology

**Definition:** Personal income is measured before the deduction of personal income taxes and other personal taxes and is reported in current dollars. It does not include realized or unrealized capital gains or losses.

**Key Concepts:**

1. **Place of Residence:** Personal income is attributed to the county where the recipient lives, not where they work.

2. **Per Capita Calculation:** Uses U.S. Census Bureau midyear population estimates as denominator.

3. **Current Dollars:** Not adjusted for inflation (use regional price parities for real comparisons).

4. **Revisions:**
   - Annual revisions covering previous 3-4 years
   - Comprehensive revisions every ~5 years
   - Most recent comprehensive revision: November 2023 (revised 1979-2021)

**Data Sources:**
- IRS tax records
- Social Security Administration
- Bureau of Labor Statistics (QCEW)
- Census Bureau
- Other federal and state sources

**Methodology Document:**
- "Local Area Personal Income and Employment: Concepts and Methods"
- Available at: https://www.bea.gov/resources/methodologies/local-area-personal-income-employment

---

## 3. EARNINGS BY INDUSTRY

### Overview
Earnings represent the sum of wage and salary disbursements, supplements to wages and salaries, and proprietors' income. Earnings by industry are a component of personal income.

### 3.1 Industry Classifications

**NAICS-Based (2001-forward):**
- Most detailed 3-digit NAICS sectors
- Available in CAINC5N, CAINC6N tables
- Consistent with national industry accounts

**SIC-Based (1969-2000):**
- Historical Standard Industrial Classification
- Available in CAINC5S, CAINC6S tables
- Maintains historical continuity

### 3.2 Complete Industry List (NAICS-Based)

See Section 2.3 (CAINC5N) for the complete list of all available NAICS industries.

**Industry Detail Levels:**
- **2-digit NAICS:** Broad sectors (e.g., Manufacturing)
- **3-digit NAICS:** Industry groups (e.g., Food manufacturing)
- **4-digit NAICS:** Limited availability at county level

### 3.3 Suppression and Disclosure

**Confidentiality Protection:**
- Earnings data may be suppressed to prevent disclosure
- Follows BLS nondisclosure rules
- Complementary suppression applied to prevent indirect calculation

**When Suppression Occurs:**
- Small geographic areas (counties)
- Industries with few employers
- Single employer dominance
- Large government role

**Improvement:** BEA switched to new disclosure-avoidance system in 2014, reducing unpublished values by 33%.

### 3.4 Farm vs. Nonfarm Earnings

**Farm Earnings (CAINC5N, CAINC45):**
- Farm proprietors' income
- Wages and salaries of farm workers
- Supplements to wages and salaries

**Nonfarm Earnings (CAINC5N):**
- All other industries
- Detailed NAICS classification
- By place of work

---

## 4. EMPLOYMENT BY INDUSTRY (DISCONTINUED)

### 4.1 CAEMP25N - Total Full-Time and Part-Time Employment (DISCONTINUED)

**Description:** Total employment by NAICS industry

**Years Available:** 2001-2020

**DISCONTINUED:** November 14, 2024 due to budget constraints

**Industry Detail:**
- 2-digit NAICS sector level
- More limited than state-level data (SAEMP25)
- Less detailed than BLS QCEW

**Related Tables:**
- CAEMP25S: SIC-based employment (1969-2000)

**Status:** Historical data remains available; no future updates.

### 4.2 Employment Concepts

**Employment Measures:**
- **Total employment:** Wage and salary + proprietors
- **Wage and salary employment:** Payroll employees only
- **Proprietors employment:** Self-employed workers
- **Full-time equivalent (FTE):** Available in some state tables (not county)

**Limitations at County Level:**
- Most disaggregated level: 2-digit NAICS
- Mining: Only total mining (NAICS 21) available
- Manufacturing: Only total manufacturing (NAICS 31-33) available

**Note:** For more detailed county employment data, use BLS Quarterly Census of Employment and Wages (QCEW).

---

## 5. REGIONAL PRICE PARITIES (RPP)

### 5.1 Official RPP Data

**Geographic Coverage:**
- **Available:** All 50 states, District of Columbia, 384 metropolitan areas
- **NOT Available:** Official county-level RPPs not published by BEA

**What RPPs Measure:**
Differences in price levels across geographic areas for a given year, expressed as a percentage of the overall national price level.

**Components:**
- All items RPP
- Goods RPP
- Services RPP
- Rents RPP

**Base:** U.S. average = 100

**Years Available:** 2008-2023

**Use:** Converting nominal personal income to real income for geographic comparisons

**Data Access:** https://www.bea.gov/data/prices-inflation/regional-price-parities-state-and-metro-area

### 5.2 Experimental County-Level RPPs

**Source:** U.S. Department of Commerce working paper (March 2024)
**Title:** "Estimating County-Level Regional Price Parities from Public Data"

**Methodology:**
- Based on publicly available data
- Uses American Community Survey housing rents data
- County-level calculations aggregated to states and metros

**Status:** Experimental, not official BEA statistics

**Access:** Working paper available from Department of Commerce website

**Note:** BEA internally uses county-level calculations for state/metro RPPs, but does not officially publish county RPPs.

### 5.3 Using RPPs for County Analysis

**Best Practice:**
1. Use metropolitan area RPPs for counties within metros
2. Use state RPPs for nonmetropolitan counties
3. Apply experimental county RPPs with caution (research use)

**Calculation Example:**
```
Real Per Capita Personal Income = (Nominal Per Capita Personal Income / RPP) × 100
```

---

## 6. DATA ACCESS METHODS

### 6.1 BEA API

#### Overview
- **Base URL:** https://apps.bea.gov/api/data
- **Documentation:** https://apps.bea.gov/api/bea_web_service_api_user_guide.htm
- **API Key Required:** Register at https://apps.bea.gov/API/signup/index.cfm

#### Key API Methods

**GetDataSetList**
Returns list of available datasets
```
https://apps.bea.gov/api/data?&UserID=[YOUR_KEY]&method=GetDataSetList&ResultFormat=JSON
```

**GetParameterList**
Returns parameters for a specific dataset
```
https://apps.bea.gov/api/data?&UserID=[YOUR_KEY]&method=GetParameterList&datasetname=Regional&ResultFormat=JSON
```

**GetParameterValues**
Returns valid values for a parameter
```
https://apps.bea.gov/api/data?&UserID=[YOUR_KEY]&method=GetParameterValues&datasetname=Regional&ParameterName=TableName&ResultFormat=JSON
```

**GetParameterValuesFiltered**
Returns values for target parameter based on other parameters
```
https://apps.bea.gov/api/data?&UserID=[YOUR_KEY]&method=GetParameterValuesFiltered&datasetname=Regional&TargetParameter=LineCode&TableName=CAINC1&ResultFormat=JSON
```

**GetData**
Retrieves actual data
```
https://apps.bea.gov/api/data?&UserID=[YOUR_KEY]&method=GetData&datasetname=Regional&TableName=CAINC1&LineCode=3&GeoFips=COUNTY&Year=LAST5&ResultFormat=JSON
```

#### Regional Dataset Parameters

**Required Parameters:**
- `UserID`: Your 36-character API key
- `Method`: GetData
- `datasetname`: Regional
- `TableName`: CAGDP1, CAGDP2, CAINC1, CAINC4, etc.
- `LineCode`: Specific statistic (use GetParameterValuesFiltered to find)
- `GeoFips`: Geographic codes
- `Year`: Year(s) to retrieve

**Optional Parameters:**
- `Frequency`: A (annual) - usually only option for county data
- `ResultFormat`: JSON or XML

**GeoFips Options:**
- `COUNTY`: All counties
- `STATE`: All states
- `01000`: Specific state (Alabama)
- `01001`: Specific county (Autauga County, AL)
- `STATE+01000`: Alabama state total
- Multiple codes: `01001,01003,01005`

**Year Options:**
- `2023`: Single year
- `2020,2021,2022,2023`: Multiple years
- `LAST5`: Last 5 years
- `LAST10`: Last 10 years
- `ALL`: All available years

#### Rate Limits and Throttling

**Limits:**
- Throttling occurs when limits exceeded in previous minute
- HTTP 429 status code indicates throttling
- HTTP RETRY-AFTER header provides timeout period

**Throttle Timeout:** 1 hour (3600 seconds)

**Best Practices:**
1. Use single-threaded requests (wait for result before next request)
2. Monitor request count and data volume
3. Pause when approaching limits
4. Include error handling for HTTP 429
5. Implement exponential backoff on errors

**Recommendations:**
- Batch requests efficiently
- Use LAST5, LAST10 instead of individual years when possible
- Request only needed line codes and geographies
- Cache data locally to minimize repeated requests

#### API Response Format

**JSON Structure:**
```json
{
  "BEAAPI": {
    "Request": {...},
    "Results": {
      "Statistic": "Per capita personal income (dollars)",
      "UnitOfMeasure": "dollars",
      "Data": [
        {
          "GeoFips": "01001",
          "GeoName": "Autauga, AL",
          "TimePeriod": "2023",
          "DataValue": "56789",
          "CL_UNIT": "Dollars",
          "UNIT_MULT": "0"
        },
        ...
      ]
    }
  }
}
```

### 6.2 bea.R Package (R)

#### Installation
```r
install.packages("bea.R")
library(bea.R)
```

#### Setup API Key
```r
beaKey <- 'YOUR-36-CHARACTER-API-KEY'
```

#### Basic Functions

**Search for tables:**
```r
beaSearch(searchTerm = 'personal income', beaKey = beaKey)
```

**Get available parameter values:**
```r
# Get all table names
beaParamValues(beaKey = beaKey,
               datasetName = 'Regional',
               paramName = 'TableName')

# Get line codes for specific table
beaParamValues(beaKey = beaKey,
               datasetName = 'Regional',
               paramName = 'LineCode',
               TableName = 'CAINC1')
```

**Retrieve data:**
```r
# Per capita personal income for all counties, last 5 years
specs <- list(
  'UserID' = beaKey,
  'Method' = 'GetData',
  'datasetname' = 'Regional',
  'TableName' = 'CAINC1',
  'LineCode' = 3,
  'GeoFips' = 'COUNTY',
  'Year' = 'LAST5',
  'ResultFormat' = 'json'
)

countyIncome <- beaGet(specs, asWide = FALSE)
```

#### Advanced Examples

**GDP by industry for specific county:**
```r
# Jefferson County, Alabama (FIPS 01073)
# All industries, last 10 years
specs <- list(
  'UserID' = beaKey,
  'Method' = 'GetData',
  'datasetname' = 'Regional',
  'TableName' = 'CAGDP2',
  'LineCode' = 'ALL',  # All industries
  'GeoFips' = '01073',
  'Year' = 'LAST10',
  'ResultFormat' = 'json'
)

jeffersonGDP <- beaGet(specs, asWide = TRUE)
```

**Personal income components for state:**
```r
# California personal income detail
specs <- list(
  'UserID' = beaKey,
  'Method' = 'GetData',
  'datasetname' = 'Regional',
  'TableName' = 'CAINC4',
  'LineCode' = 'ALL',
  'GeoFips' = 'STATE',
  'Year' = '2023',
  'ResultFormat' = 'json'
)

caIncome <- beaGet(specs, asWide = FALSE)
```

**Multiple counties:**
```r
# Several counties in Texas
specs <- list(
  'UserID' = beaKey,
  'Method' = 'GetData',
  'datasetname' = 'Regional',
  'TableName' = 'CAINC1',
  'LineCode' = 3,
  'GeoFips' = '48201,48113,48029',  # Harris, Dallas, Bexar
  'Year' = 'LAST10',
  'ResultFormat' = 'json'
)

txCounties <- beaGet(specs, asWide = FALSE)
```

### 6.3 Python (beaapi package)

#### Installation
```python
pip install beaapi
```

#### Basic Usage
```python
import beaapi
import pandas as pd

# Set API key
BEA_KEY = 'YOUR-36-CHARACTER-API-KEY'

# Get county personal income data
response = beaapi.data_api(
    UserID=BEA_KEY,
    Method='GetData',
    datasetname='Regional',
    TableName='CAINC1',
    LineCode='3',
    GeoFips='COUNTY',
    Year='LAST5',
    ResultFormat='json'
)

# Convert to DataFrame
data = response['BEAAPI']['Results']['Data']
df = pd.DataFrame(data)
```

#### Advanced Example
```python
import requests
import pandas as pd

BEA_KEY = 'YOUR-API-KEY'
BASE_URL = 'https://apps.bea.gov/api/data'

# Function to get county GDP data
def get_county_gdp(fips_codes, years='LAST5'):
    """
    Retrieve county GDP data from BEA API

    Parameters:
    -----------
    fips_codes : str or list
        County FIPS code(s)
    years : str
        Year specification (e.g., 'LAST5', '2020,2021,2022')

    Returns:
    --------
    pd.DataFrame
    """
    if isinstance(fips_codes, list):
        fips_codes = ','.join(fips_codes)

    params = {
        'UserID': BEA_KEY,
        'method': 'GetData',
        'datasetname': 'Regional',
        'TableName': 'CAGDP2',
        'LineCode': '1',  # All industry total
        'GeoFips': fips_codes,
        'Year': years,
        'ResultFormat': 'JSON'
    }

    response = requests.get(BASE_URL, params=params)
    data = response.json()['BEAAPI']['Results']['Data']

    return pd.DataFrame(data)

# Example usage
counties = ['06037', '06073', '06059']  # LA, SD, Orange counties in CA
gdp_data = get_county_gdp(counties, years='2020,2021,2022,2023')
print(gdp_data)
```

### 6.4 Interactive Data Application

**URL:** https://apps.bea.gov/itable/

**Steps:**
1. Select "Regional Data - GDP and Personal Income"
2. Choose "County" as geographic level
3. Select desired table (CAINC1, CAGDP2, etc.)
4. Choose statistics (line codes)
5. Select years and counties
6. Download as CSV, Excel, or view online

**Features:**
- Interactive maps
- Custom table builder
- Multiple export formats
- Historical data access
- Metropolitan area selections

### 6.5 Bulk CSV Downloads

**URL:** https://apps.bea.gov/regional/downloadzip.htm

**Available Files:**

#### GDP Tables (CAGDP)
- CAGDP1.zip - County and MSA GDP summary
- CAGDP2.zip - GDP in current dollars by industry
- CAGDP8.zip - Chain-type quantity indexes
- CAGDP9.zip - Real GDP in chained dollars
- CAGDP10.zip - Per capita real GDP
- CAGDP11.zip - Contributions to percent change

#### Personal Income Tables (CAINC)
- CAINC1.zip - Annual personal income summary
- CAINC4.zip - Personal income and employment by component
- CAINC5N.zip - Personal income by component and earnings by NAICS industry
- CAINC6N.zip - Compensation of employees by NAICS industry
- CAINC30.zip - Economic profile
- CAINC35.zip - Personal current transfer receipts (through 2022)
- CAINC45.zip - Farm income and expenses (through 2022)
- CAINC91.zip - Gross flow of earnings

#### Employment Tables (CAEMP) - Historical Only
- CAEMP25N.zip - Total employment by NAICS industry (through 2020)

**File Format:**
- CSV (comma-separated values)
- Compressed as ZIP archives
- Includes all years available
- Ready for import into Excel, R, Python, etc.

**Update Schedule:**
- Updated after annual releases (typically December/November)
- Files include all historical revisions

### 6.6 FRED (Federal Reserve Economic Data)

**URL:** https://fred.stlouisfed.org

**BEA County Data Available:**
- County personal income
- County per capita personal income
- County GDP (selected counties/metros)

**Advantages:**
- Simple API
- Time series analysis tools
- Integration with economic indicators
- Graphing capabilities

**Limitations:**
- Not all counties available
- May lag official BEA releases
- Limited to major tables (CAINC1, CAGDP1)

---

## 7. DATA QUALITY AND METHODOLOGY

### 7.1 Disclosure and Suppression Rules

**Confidentiality Requirements:**
- BEA protects confidentiality of source data
- Follows BLS nondisclosure rules for QCEW-based data
- Additional BEA-specific suppressions applied

**Suppression Triggers:**
- Fewer than 3 establishments in an industry-county
- Single employer accounts for >80% of employment
- Potential for indirect disclosure through aggregation
- State/local government dominates employment

**Complementary Suppression:**
- Additional cells suppressed to prevent calculation of suppressed values
- Applied systematically across related geographies
- May suppress data in larger geographies to protect smaller ones

**Disclosure Avoidance Improvements (2014):**
- New system reduced processing time from 5 days to 1 day
- 33% fewer suppressed values
- Better preservation of data utility while protecting confidentiality

### 7.2 Estimation Methods

#### GDP by County

**Income Approach:**
```
GDP = Compensation of Employees
    + Taxes on Production and Imports Less Subsidies
    + Gross Operating Surplus
```

**Components:**
- **Compensation:** QCEW data (wages + supplements)
- **Proprietors' Income:** IRS tax data, distributed to counties
- **Other Income Components (OIC):** Various sources, allocated using NETS sales, QCEW, Economic Census

**Industry Calculation:**
1. Estimate compensation for 65 detailed industries
2. Add proprietors' income (except mining, government)
3. Add OIC (distributed using multiple methods)
4. Aggregate to 21 published industries

**Real GDP:**
- Apply national industry-specific price indexes to current-dollar GDP
- Base year: 2017
- Chain-type quantity indexes account for changing relative prices

#### Personal Income

**Components and Sources:**

1. **Wages and Salaries:** QCEW (Bureau of Labor Statistics)
2. **Supplements:** Calculated from QCEW and other federal sources
3. **Proprietors' Income:** IRS tax records, allocated to counties
4. **Property Income:**
   - Dividends: IRS data
   - Interest: Federal Reserve flow of funds
   - Rent: Various sources including tax data
5. **Transfer Receipts:** Federal program administrative data
   - Social Security Administration
   - Centers for Medicare & Medicaid Services
   - Department of Agriculture (SNAP)
   - State unemployment insurance agencies

**Place of Residence Adjustment:**
- Commuting flows estimated from Census journey-to-work data
- American Community Survey updates
- Adjustment converts place-of-work earnings to place-of-residence

**Population:**
- U.S. Census Bureau midyear estimates
- Includes all residents (civilian, military, institutional)

### 7.3 Revisions

**Annual Updates:**
- Revise previous 3-4 years
- Incorporate newly available source data
- Update seasonal adjustment factors
- Typically released September/December

**Comprehensive Updates:**
- Every ~5 years
- Major methodological improvements
- Updated population estimates
- Revise all available history
- Most recent: November 2023 (revised 1979-2021)

**Types of Revisions:**
1. **Statistical revisions:** Updated source data
2. **Definitional revisions:** Changes in concepts or classifications
3. **Methodological revisions:** Improved estimation techniques

**Revision Schedule:**
- GDP: December annual release revises previous 3 years
- Personal Income: November/December release revises previous 3 years
- Watch BEA website for revision announcements

### 7.4 Data Quality Indicators

**Coverage:**
- **GDP:** All 3,113 counties (some industry detail suppressed)
- **Personal Income:** All 3,113 counties (complete coverage)
- **Suppression Rate:** ~15-20% of industry-county cells for GDP

**Accuracy:**
- Based on administrative records (high quality)
- Annual benchmarking to comprehensive sources
- Consistency with state and national accounts

**Timeliness:**
- Released 12-18 months after reference year
- More timely than Economic Census
- Less timely than monthly indicators (unemployment, etc.)

**Comparability:**
- Consistent methodology across counties
- Integrated with state and national accounts
- NAICS-based (2001-forward) for cross-industry comparison

**Limitations:**
- Suppression reduces geographic detail in some industries
- County boundaries change over time (annexations, etc.)
- Commuting adjustments based on surveys (sampling error)
- Small counties may have larger estimation errors

### 7.5 Known Issues and Considerations

**GDP by County:**
- Only available from 2017 (2001-2016 pending)
- Limited to 21 industries (vs. 65 detailed industries used in calculation)
- Industry suppression more common in small counties
- Does not include unpaid household production

**Personal Income:**
- Does not include capital gains/losses
- Transfer receipts detail discontinued (CAINC35) after 2022
- Farm data discontinued (CAINC45) after 2022
- Place-of-residence adjustment based on periodic survey data

**Employment:**
- County employment by industry discontinued (CAEMP25N) after 2020
- Use BLS QCEW for detailed county employment data
- Proprietors employment has estimation uncertainty

**Cross-County Comparisons:**
- Use Regional Price Parities to adjust for cost-of-living differences
- County size variations enormous (88 residents to 10 million+)
- Metropolitan/nonmetropolitan differences substantial
- Border counties may have large commuting flows

**Time Series:**
- NAICS break in 2001 (SIC before, NAICS after)
- Comprehensive revisions change historical series
- Population estimates revised with each decennial census
- Industry classifications update periodically (NAICS 2002, 2007, 2012, 2017, 2022)

---

## 8. CODE EXAMPLES

### 8.1 R: Complete County Analysis

```r
# Load required packages
library(bea.R)
library(dplyr)
library(tidyr)
library(ggplot2)

# Set API key
beaKey <- 'YOUR-36-CHARACTER-API-KEY'

# Function to get county data
get_county_data <- function(table_name, line_code, years = 'LAST5') {
  specs <- list(
    'UserID' = beaKey,
    'Method' = 'GetData',
    'datasetname' = 'Regional',
    'TableName' = table_name,
    'LineCode' = line_code,
    'GeoFips' = 'COUNTY',
    'Year' = years,
    'ResultFormat' = 'json'
  )

  data <- beaGet(specs, asWide = FALSE)
  return(data)
}

# Get per capita personal income for all counties
income_data <- get_county_data('CAINC1', '3', 'LAST10')

# Clean and process
income_clean <- income_data %>%
  mutate(
    value = as.numeric(DataValue),
    year = as.integer(TimePeriod),
    fips = GeoFips,
    county = GeoName
  ) %>%
  select(fips, county, year, value)

# Calculate growth rates
income_growth <- income_clean %>%
  arrange(fips, year) %>%
  group_by(fips) %>%
  mutate(
    pct_change = (value / lag(value) - 1) * 100,
    cumulative_growth = (value / first(value) - 1) * 100
  ) %>%
  ungroup()

# Top 10 fastest growing counties (cumulative)
top_growth <- income_growth %>%
  filter(year == max(year)) %>%
  arrange(desc(cumulative_growth)) %>%
  head(10)

print(top_growth)

# Get GDP by industry for specific county
# Example: Cook County, Illinois (FIPS 17031)
cook_gdp <- get_county_data('CAGDP2', 'ALL', 'LAST5')

cook_gdp_clean <- cook_gdp %>%
  filter(GeoFips == '17031') %>%
  mutate(
    value = as.numeric(DataValue),
    year = as.integer(TimePeriod),
    industry = Description
  ) %>%
  select(year, industry, value)

# Plot industry composition
library(ggplot2)

cook_gdp_2023 <- cook_gdp_clean %>%
  filter(year == 2023, industry != 'All industry total') %>%
  arrange(desc(value)) %>%
  head(10)

ggplot(cook_gdp_2023, aes(x = reorder(industry, value), y = value)) +
  geom_col(fill = 'steelblue') +
  coord_flip() +
  labs(
    title = 'Cook County, IL - Top 10 Industries by GDP (2023)',
    x = NULL,
    y = 'GDP (thousands of dollars)'
  ) +
  theme_minimal()
```

### 8.2 R: Personal Income Components Analysis

```r
# Detailed personal income components for all US counties
library(bea.R)
library(dplyr)

beaKey <- 'YOUR-36-CHARACTER-API-KEY'

# Get all personal income components (CAINC4)
specs <- list(
  'UserID' = beaKey,
  'Method' = 'GetData',
  'datasetname' = 'Regional',
  'TableName' = 'CAINC4',
  'LineCode' = 'ALL',
  'GeoFips' = 'COUNTY',
  'Year' = '2023',
  'ResultFormat' = 'json'
)

income_components <- beaGet(specs, asWide = FALSE)

# Process data
income_wide <- income_components %>%
  mutate(
    value = as.numeric(DataValue),
    fips = GeoFips,
    county = GeoName,
    component = Description
  ) %>%
  select(fips, county, component, value) %>%
  pivot_wider(
    names_from = component,
    values_from = value
  )

# Calculate shares of total personal income
income_analysis <- income_wide %>%
  mutate(
    wages_share = `Wages and salaries` / `Personal income` * 100,
    transfers_share = `Personal current transfer receipts` / `Personal income` * 100,
    proprietors_share = `Proprietors' income` / `Personal income` * 100,
    property_share = (`Dividends, interest, and rent` / `Personal income`) * 100
  )

# Find counties most dependent on transfer payments
transfer_dependent <- income_analysis %>%
  arrange(desc(transfers_share)) %>%
  select(county, transfers_share, `Personal income`, Population) %>%
  head(20)

print(transfer_dependent)

# Summary statistics
summary(income_analysis$transfers_share)
```

### 8.3 R: Multi-Year GDP Growth Analysis

```r
# Analyze real GDP growth by county
library(bea.R)
library(dplyr)
library(tidyr)

beaKey <- 'YOUR-36-CHARACTER-API-KEY'

# Get real GDP (CAGDP9) for all counties
specs <- list(
  'UserID' = beaKey,
  'Method' = 'GetData',
  'datasetname' = 'Regional',
  'TableName' = 'CAGDP9',
  'LineCode' = '1',  # All industry total
  'GeoFips' = 'COUNTY',
  'Year' = 'ALL',  # All available years
  'ResultFormat' = 'json'
)

real_gdp <- beaGet(specs, asWide = FALSE)

# Calculate compound annual growth rate (CAGR)
gdp_growth <- real_gdp %>%
  mutate(
    value = as.numeric(DataValue),
    year = as.integer(TimePeriod),
    fips = GeoFips,
    county = GeoName
  ) %>%
  select(fips, county, year, value) %>%
  group_by(fips) %>%
  mutate(
    years_elapsed = year - min(year),
    cagr = ifelse(years_elapsed > 0,
                  ((value / first(value)) ^ (1 / years_elapsed) - 1) * 100,
                  NA)
  ) %>%
  ungroup()

# Get most recent CAGR for each county
latest_cagr <- gdp_growth %>%
  filter(year == max(year)) %>%
  select(fips, county, cagr, value) %>%
  arrange(desc(cagr))

# Top 25 fastest growing counties
print(head(latest_cagr, 25))

# Bottom 25 (declining or slowest growth)
print(tail(latest_cagr, 25))

# State-level summary
state_summary <- gdp_growth %>%
  filter(year == max(year)) %>%
  mutate(state = substr(fips, 1, 2)) %>%
  group_by(state) %>%
  summarize(
    n_counties = n(),
    median_cagr = median(cagr, na.rm = TRUE),
    mean_cagr = mean(cagr, na.rm = TRUE),
    total_gdp = sum(value, na.rm = TRUE)
  ) %>%
  arrange(desc(median_cagr))

print(state_summary)
```

### 8.4 Python: Complete Data Retrieval Pipeline

```python
import requests
import pandas as pd
import numpy as np
from typing import List, Dict, Optional

class BEACountyData:
    """
    Class for retrieving and processing BEA county-level economic data
    """

    def __init__(self, api_key: str):
        self.api_key = api_key
        self.base_url = 'https://apps.bea.gov/api/data'

    def get_data(self,
                 table_name: str,
                 line_code: str = '1',
                 geo_fips: str = 'COUNTY',
                 years: str = 'LAST5') -> pd.DataFrame:
        """
        Retrieve data from BEA API

        Parameters:
        -----------
        table_name : str
            BEA table name (e.g., 'CAINC1', 'CAGDP2')
        line_code : str
            Line code or 'ALL' for all line codes
        geo_fips : str
            Geographic FIPS codes or 'COUNTY' for all counties
        years : str
            Years to retrieve (e.g., 'LAST5', '2020,2021,2022')

        Returns:
        --------
        pd.DataFrame
        """
        params = {
            'UserID': self.api_key,
            'method': 'GetData',
            'datasetname': 'Regional',
            'TableName': table_name,
            'LineCode': line_code,
            'GeoFips': geo_fips,
            'Year': years,
            'ResultFormat': 'JSON'
        }

        try:
            response = requests.get(self.base_url, params=params)
            response.raise_for_status()
            data = response.json()['BEAAPI']['Results']['Data']
            df = pd.DataFrame(data)

            # Convert numeric columns
            if 'DataValue' in df.columns:
                df['DataValue'] = pd.to_numeric(df['DataValue'], errors='coerce')
            if 'TimePeriod' in df.columns:
                df['TimePeriod'] = pd.to_numeric(df['TimePeriod'], errors='coerce')

            return df

        except requests.exceptions.RequestException as e:
            print(f"Error fetching data: {e}")
            return pd.DataFrame()

    def get_county_income(self, years: str = 'LAST5') -> pd.DataFrame:
        """Get per capita personal income for all counties"""
        return self.get_data('CAINC1', line_code='3', years=years)

    def get_county_gdp(self, years: str = 'LAST5',
                      industry: str = '1') -> pd.DataFrame:
        """Get county GDP by industry"""
        return self.get_data('CAGDP2', line_code=industry, years=years)

    def get_income_components(self, year: str = '2023') -> pd.DataFrame:
        """Get detailed personal income components"""
        return self.get_data('CAINC4', line_code='ALL', years=year)

    def get_earnings_by_industry(self, year: str = '2023') -> pd.DataFrame:
        """Get earnings by detailed NAICS industry"""
        return self.get_data('CAINC5N', line_code='ALL', years=year)

# Example usage
if __name__ == '__main__':

    # Initialize
    BEA_KEY = 'YOUR-36-CHARACTER-API-KEY'
    bea = BEACountyData(BEA_KEY)

    # Get per capita income for all counties, last 10 years
    print("Fetching county income data...")
    income = bea.get_county_income(years='LAST10')

    # Process and analyze
    income_pivot = income.pivot_table(
        index='GeoFips',
        columns='TimePeriod',
        values='DataValue',
        aggfunc='first'
    )

    # Calculate growth rates
    income_pivot['growth_rate'] = (
        (income_pivot.iloc[:, -1] / income_pivot.iloc[:, 0]) **
        (1 / (len(income_pivot.columns) - 2)) - 1
    ) * 100

    # Top 10 fastest growing
    print("\nTop 10 Fastest Growing Counties (Per Capita Income):")
    print(income_pivot.nlargest(10, 'growth_rate')['growth_rate'])

    # Get GDP by industry for specific counties
    print("\nFetching GDP by industry...")
    target_counties = '06037,48201,17031'  # LA, Harris, Cook
    gdp = bea.get_county_gdp(years='2023')
    gdp_filtered = gdp[gdp['GeoFips'].isin(target_counties.split(','))]

    # Pivot and display
    gdp_pivot = gdp_filtered.pivot_table(
        index='Description',
        columns='GeoName',
        values='DataValue',
        aggfunc='sum'
    )

    print("\nGDP by Industry (2023):")
    print(gdp_pivot.head(10))
```

### 8.5 Python: Bulk Download and Process

```python
import requests
import zipfile
import io
import pandas as pd
from pathlib import Path

def download_bea_bulk_data(table_name: str,
                           output_dir: str = './bea_data') -> pd.DataFrame:
    """
    Download bulk CSV data from BEA and process

    Parameters:
    -----------
    table_name : str
        BEA table name (e.g., 'CAINC1', 'CAGDP2')
    output_dir : str
        Directory to save extracted files

    Returns:
    --------
    pd.DataFrame
    """
    # Create output directory
    Path(output_dir).mkdir(parents=True, exist_ok=True)

    # Download URL
    url = f'https://apps.bea.gov/regional/zip/{table_name}.zip'

    print(f"Downloading {table_name}.zip...")

    try:
        # Download ZIP file
        response = requests.get(url)
        response.raise_for_status()

        # Extract ZIP
        with zipfile.ZipFile(io.BytesIO(response.content)) as zip_file:
            zip_file.extractall(output_dir)

            # Find CSV file
            csv_files = [f for f in zip_file.namelist() if f.endswith('.csv')]

            if csv_files:
                csv_path = Path(output_dir) / csv_files[0]
                print(f"Extracted to {csv_path}")

                # Read CSV
                df = pd.read_csv(csv_path, encoding='latin-1')
                print(f"Loaded {len(df)} rows")

                return df
            else:
                print("No CSV file found in archive")
                return pd.DataFrame()

    except Exception as e:
        print(f"Error: {e}")
        return pd.DataFrame()

# Example: Download and analyze personal income data
if __name__ == '__main__':

    # Download CAINC1 (per capita income)
    cainc1 = download_bea_bulk_data('CAINC1')

    # Filter to per capita income only
    per_capita = cainc1[cainc1['LineCode'] == 3].copy()

    # Convert to numeric
    per_capita.loc[:, 'Value'] = pd.to_numeric(
        per_capita['DataValue'],
        errors='coerce'
    )

    # Get most recent year
    latest_year = per_capita['TimePeriod'].max()

    # Top 25 wealthiest counties
    top_counties = per_capita[
        per_capita['TimePeriod'] == latest_year
    ].nlargest(25, 'Value')

    print(f"\nTop 25 Counties by Per Capita Income ({latest_year}):")
    print(top_counties[['GeoName', 'Value']])

    # Download GDP data
    cagdp2 = download_bea_bulk_data('CAGDP2')

    # Analyze by industry
    latest_gdp = cagdp2[cagdp2['TimePeriod'] == cagdp2['TimePeriod'].max()]

    # Industry totals
    industry_totals = latest_gdp.groupby('Description')['DataValue'].apply(
        lambda x: pd.to_numeric(x, errors='coerce').sum()
    ).sort_values(ascending=False)

    print(f"\nNational Industry Totals (County Sum):")
    print(industry_totals.head(15))
```

### 8.6 R: Comprehensive County Dataset Creation

```r
# Create comprehensive county economic database
library(bea.R)
library(dplyr)
library(tidyr)
library(purrr)

beaKey <- 'YOUR-36-CHARACTER-API-KEY'

# Function to safely get BEA data
safe_bea_get <- function(table_name, line_code, years = 'LAST5') {
  specs <- list(
    'UserID' = beaKey,
    'Method' = 'GetData',
    'datasetname' = 'Regional',
    'TableName' = table_name,
    'LineCode' = line_code,
    'GeoFips' = 'COUNTY',
    'Year' = years,
    'ResultFormat' = 'json'
  )

  tryCatch({
    data <- beaGet(specs, asWide = FALSE)
    return(data)
  }, error = function(e) {
    message(sprintf("Error fetching %s: %s", table_name, e$message))
    return(NULL)
  })
}

# Define all variables to retrieve
variables <- tibble(
  table = c('CAINC1', 'CAINC1', 'CAINC1',
            'CAGDP2', 'CAGDP9',
            'CAINC4', 'CAINC4', 'CAINC4'),
  line_code = c('1', '2', '3',
                '1', '1',
                '45', '46', '47'),
  var_name = c('personal_income', 'population', 'per_capita_income',
               'gdp_current', 'gdp_real',
               'net_earnings', 'dividends_interest_rent', 'transfers')
)

# Retrieve all variables
county_data_list <- variables %>%
  pmap(function(table, line_code, var_name) {
    message(sprintf("Fetching %s...", var_name))
    data <- safe_bea_get(table, line_code, years = '2023')

    if (!is.null(data)) {
      data %>%
        mutate(
          variable = var_name,
          value = as.numeric(DataValue)
        ) %>%
        select(GeoFips, GeoName, TimePeriod, variable, value)
    } else {
      NULL
    }
  })

# Combine all data
county_data <- bind_rows(county_data_list)

# Pivot wider
county_wide <- county_data %>%
  pivot_wider(
    id_cols = c(GeoFips, GeoName, TimePeriod),
    names_from = variable,
    values_from = value
  )

# Calculate additional metrics
county_analysis <- county_wide %>%
  mutate(
    # Shares of personal income
    earnings_share = (net_earnings / personal_income) * 100,
    property_share = (dividends_interest_rent / personal_income) * 100,
    transfers_share = (transfers / personal_income) * 100,

    # GDP per capita
    gdp_per_capita = (gdp_current * 1000) / population,

    # Real GDP per capita
    real_gdp_per_capita = (gdp_real * 1000) / population,

    # Productivity (GDP per worker) - approximate
    # Note: Would need employment data for accurate calculation

    # Extract state FIPS
    state_fips = substr(GeoFips, 1, 2)
  )

# Summary statistics by state
state_summary <- county_analysis %>%
  group_by(state_fips) %>%
  summarize(
    n_counties = n(),
    median_per_capita_income = median(per_capita_income, na.rm = TRUE),
    median_gdp_per_capita = median(gdp_per_capita, na.rm = TRUE),
    median_transfers_share = median(transfers_share, na.rm = TRUE),
    total_population = sum(population, na.rm = TRUE),
    total_gdp = sum(gdp_current, na.rm = TRUE)
  ) %>%
  arrange(desc(median_per_capita_income))

print(state_summary)

# Save to CSV
write.csv(county_analysis,
          'county_economic_data_2023.csv',
          row.names = FALSE)

message("Data saved to county_economic_data_2023.csv")
```

---

## 9. DATA RELEASE CALENDAR

### 9.1 Regular Release Schedule

**County GDP:**
- **Release Date:** Early December (annual)
- **Most Recent:** December 4, 2024 (2023 data)
- **Next Release:** December 3, 2025 (2024 data)
- **Time:** 8:30 AM EST
- **Years Revised:** Previous 3 years

**County Personal Income:**
- **Release Date:** Mid-November (annual)
- **Most Recent:** November 14, 2024 (2023 data)
- **Next Release:** December 3, 2025 (combined with GDP)
- **Time:** 8:30 AM EST
- **Years Revised:** Previous 3-4 years

**IMPORTANT CHANGE (2025):**
Starting December 3, 2025, BEA will combine county-level GDP and personal income into a single annual release.

### 9.2 Comprehensive Updates

**Frequency:** Every ~5 years

**Most Recent:**
- November 2023 comprehensive update
- Revised personal income 1979-2021
- Updated methodology and definitions

**Next Expected:** ~2028

### 9.3 Discontinued Releases

**Employment by Industry (CAEMP25N):**
- Last Release: November 14, 2024
- Final Data Year: 2020
- Reason: Budget constraints

**Transfer Receipts Detail (CAINC35):**
- Last Release: November 14, 2024
- Final Data Year: 2022
- Reason: Budget constraints

**Farm Income (CAINC45):**
- Last Release: November 14, 2024
- Final Data Year: 2022
- Reason: Budget constraints

### 9.4 Monitoring for Updates

**BEA Release Schedule:**
https://www.bea.gov/news/schedule

**Features:**
- Printable calendar
- ICS subscription (add to Outlook/Google Calendar)
- JSON format for programmatic access
- Email notifications available

**Advisory System:**
- BEA sends email advisories before releases
- Subscribe at BEA website
- Includes revision announcements

---

## 10. FREQUENTLY ASKED QUESTIONS

### Q1: What's the difference between GDP and personal income?

**A:** GDP measures production within a county's geographic boundaries. Personal income measures income received by county residents (regardless of where earned). Key differences:

- **GDP:** Place of production, excludes transfer payments
- **Personal Income:** Place of residence, includes transfer payments
- A county with many commuters may have high GDP but lower personal income (or vice versa)

### Q2: Why are some county-industry combinations suppressed?

**A:** To protect confidentiality of individual businesses. Suppression occurs when:
- Fewer than 3 establishments
- One employer dominates (>80% of employment)
- Data could be calculated indirectly

### Q3: Can I get quarterly data for counties?

**A:** No. County-level GDP and personal income are annual only. Quarterly data available for states (SQGDP, SQINC).

### Q4: How do I adjust for inflation and cost of living?

**A:**
- **Inflation:** Use BEA's GDP deflators or chained-dollar estimates (CAGDP9)
- **Cost of Living:** Use Regional Price Parities for metro areas; experimental county RPPs available from Commerce working paper

### Q5: What happened to county employment data?

**A:** BEA discontinued CAEMP25N (county employment by industry) after 2020 due to budget cuts. Use BLS Quarterly Census of Employment and Wages (QCEW) instead.

### Q6: Are metropolitan area data still available?

**A:** Metropolitan area GDP and personal income will be discontinued after 2024. County data will continue.

### Q7: How often is the data revised?

**A:**
- Annual revisions: Previous 3-4 years
- Comprehensive revisions: Every ~5 years (entire history)

### Q8: What's the difference between CAINC5N and CAINC5S?

**A:**
- **CAINC5N:** NAICS industry classification (2001-forward)
- **CAINC5S:** SIC industry classification (1969-2000)

### Q9: Can I get real (inflation-adjusted) personal income?

**A:** BEA doesn't publish real county personal income directly. To calculate:
1. Use state-level implicit price deflators (SAIRPD)
2. Use metro-level Regional Price Parities where available
3. Use GDP deflators as approximation

### Q10: What's the earliest year available for county data?

**A:**
- **Personal Income:** 1969 (with SIC/NAICS break in 2001)
- **GDP:** 2017 (2001-2016 to be released later)

---

## 11. ADDITIONAL RESOURCES

### 11.1 Official BEA Resources

**Main Data Pages:**
- GDP by County: https://www.bea.gov/data/gdp/gdp-county-metro-and-other-areas
- Personal Income by County: https://www.bea.gov/data/income-saving/personal-income-county-metro-and-other-areas
- Regional Accounts Home: https://www.bea.gov/data/economic-accounts/regional

**API and Downloads:**
- API Documentation: https://apps.bea.gov/api/bea_web_service_api_user_guide.htm
- API Key Registration: https://apps.bea.gov/API/signup/index.cfm
- Bulk Downloads: https://apps.bea.gov/regional/downloadzip.htm
- Interactive Tables: https://apps.bea.gov/itable/

**Methodology:**
- GDP by County Methodology: https://www.bea.gov/resources/methodologies/gdp-by-metro
- Personal Income Methodology: https://www.bea.gov/resources/methodologies/local-area-personal-income-employment
- Glossary: https://www.bea.gov/resources/glossary

**News and Updates:**
- Release Schedule: https://www.bea.gov/news/schedule
- BEA Blog: https://www.bea.gov/news/blog
- Regional Accounts Articles: https://www.bea.gov/resources/article-collections/regional

### 11.2 Software Packages

**R:**
- bea.R: https://cran.r-project.org/package=bea.R
- GitHub: https://github.com/us-bea/bea.R
- Guide: https://us-bea.github.io/econ-visual-guide/

**Python:**
- beaapi: https://github.com/us-bea/beaapi
- PyPI: https://pypi.org/project/beaapi/

### 11.3 Related Data Sources

**Bureau of Labor Statistics (BLS):**
- QCEW (employment/wages by county-industry): https://www.bls.gov/cew/
- LAUS (unemployment by county): https://www.bls.gov/lau/

**U.S. Census Bureau:**
- County Business Patterns: https://www.census.gov/programs-surveys/cbp.html
- Economic Census: https://www.census.gov/programs-surveys/economic-census.html
- ACS (demographics): https://www.census.gov/programs-surveys/acs/

**Other Federal Sources:**
- USDA Economic Research Service: https://www.ers.usda.gov/
- HUD (housing data): https://www.hud.gov/program_offices/economic_development
- FRED (Federal Reserve Economic Data): https://fred.stlouisfed.org/

### 11.4 Academic and Research

**Working Papers:**
- County-Level RPPs: "Estimating County-Level Regional Price Parities from Public Data" (March 2024)
- Available from: https://www.commerce.gov/news/blog/2024/03/estimating-county-level-regional-price-parities-public-data

**Survey of Current Business Articles:**
- "Local Area Gross Domestic Product Methodology" (March 2020)
- "GDP and Personal Income by County" (May 2023)
- Available at: https://apps.bea.gov/scb/

**Research Guides:**
- Data Planet LibGuides: https://data-planet.libguides.com/BEALocalAreas

---

## 12. CHANGE LOG AND VERSION HISTORY

### Version 1.0 (November 11, 2025)
- Initial comprehensive documentation
- Documented all available county-level BEA data through 2023
- Included discontinued tables (CAEMP25N, CAINC35, CAINC45)
- Complete API documentation with code examples
- Methodology and quality notes

### Recent BEA Changes (2024-2025)

**November 14, 2024:**
- Discontinued CAEMP25N (county employment by industry)
- Discontinued CAINC35 (transfer receipts detail)
- Discontinued CAINC45 (farm income and expenses)
- Reason: Budget constraints

**December 4, 2024:**
- Released 2023 county GDP data
- Revised 2020-2022 county GDP

**Upcoming December 3, 2025:**
- First combined county GDP and personal income release
- Discontinuation of metropolitan area statistics
- County data will continue

### Comprehensive Update (November 2023)
- Revised personal income 1979-2021
- Updated methodology
- Incorporated 2020 Census population estimates

---

## 13. CONTACT AND SUPPORT

**BEA Customer Service:**
- Email: customerservice@bea.gov
- Phone: (301) 278-9004
- Hours: Monday-Friday, 8:30 AM - 5:00 PM EST

**API Support:**
- Email: APIinfo@bea.gov

**Media Inquiries:**
- Email: news@bea.gov
- Phone: (202) 606-2649

**Mailing Address:**
Bureau of Economic Analysis
U.S. Department of Commerce
4600 Silver Hill Road
Washington, DC 20233

---

## DOCUMENT END

**Document Date:** November 11, 2025
**BEA Data Current Through:** 2023 (varies by table)
**Next Major Update Expected:** December 3, 2025 (combined county GDP/income release)

**Notes:**
- This documentation covers ALL county-level economic variables available from BEA
- Includes both current and discontinued tables
- API rate limits and best practices documented
- Production-ready code examples in R and Python
- Comprehensive methodology and quality notes

**For Updates:**
Monitor BEA release schedule at https://www.bea.gov/news/schedule

---
