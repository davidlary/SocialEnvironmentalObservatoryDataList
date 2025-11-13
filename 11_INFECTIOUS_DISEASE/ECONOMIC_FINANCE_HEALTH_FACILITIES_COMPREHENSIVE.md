# ECONOMIC, FINANCIAL, HEALTH FACILITIES & PUBLIC SERVICES DATA
## Comprehensive County-Level Data Sources - Final Gap Analysis Additions

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Repository:** GetData
**Category:** Economic/Financial, Healthcare Facilities, Infectious Disease, Public Services

---

## Executive Summary

This document provides comprehensive coverage of 13 high-value county-level data sources identified in the final gap analysis. These sources fill critical remaining gaps in economic/financial indicators, healthcare facility characteristics, infectious disease surveillance, and public services.

**Sources Documented:**
1. IRS Statistics of Income - County Tax Data (1989-2022)
2. IRS County-to-County Migration (1990-2022)
3. Federal Reserve Household Debt (1999-2025)
4. Census Building Permits (1980-2024)
5. ASARB U.S. Religion Census (1952-2020)
6. Federal Court Bankruptcy Filings (2007-present)
7. USPTO Patent Data by County (1975-2020)
8. CDC WONDER Natality - Birth Outcomes (1995-2024)
9. CDC COVID-19 Vaccination (2020-2025)
10. CDC AtlasPlus - STI/TB/Hepatitis (1996-present)
11. AHA Annual Survey - Hospital Characteristics (1946-present)
12. CMS Nursing Home Compare (2009-present)
13. IMLS Public Libraries Survey (1992-2022)

**Total Variables:** ~1,100+ priority county-level variables
**Geographic Coverage:** All 3,143 US counties (with noted exceptions)
**Temporal Coverage:** Longest series: 1946-present (79 years!)

---

## PART 1: ECONOMIC & FINANCIAL DATA

### Source 1: IRS Statistics of Income (SOI) - County Tax Data

**Official Name:** IRS Statistics of Income - County Data
**Status:** ✅ COMPREHENSIVE TAX RETURN DATA (1989-2022, 33-year series)

#### Overview

The IRS Statistics of Income (SOI) program publishes county-level tax return statistics derived from Form 1040 individual income tax returns. This is the ONLY source of detailed county-level income composition, deductions, and tax liability data directly from administrative records.

#### Coverage

- **Geographic:** All 3,143 US counties
- **Temporal:** 1989-2022 (33-year annual time series)
- **Update Frequency:** Annual (released ~18 months after tax year)
- **Most Recent:** 2022 data released mid-2024

#### Variables Available (20+)

**Returns & Population:**
- Number of returns filed (approximates households)
- Number of personal exemptions (approximates population)
- Number of single returns
- Number of joint returns
- Number of dependents claimed

**Adjusted Gross Income (AGI):**
- Total AGI ($)
- Mean AGI per return ($)
- AGI by brackets: <$1, $1-$10k, $10-$25k, $25-$50k, $50-$75k, $75-$100k, $100-$200k, $200k+
- Number of returns and AGI amount in each bracket

**Income Components:**
- Salaries and wages (total $, number of returns)
- Taxable interest income ($, returns)
- Tax-exempt interest ($, returns)
- Dividend income (ordinary + qualified, $, returns)
- Business net income or loss ($, returns)
- Net capital gains or losses ($, returns)
- Taxable Individual Retirement Arrangement (IRA) distributions ($, returns)
- Taxable pensions and annuities ($, returns)
- Unemployment compensation ($, returns)
- Social Security benefits - taxable amount ($, returns)
- Farm net income or loss ($, returns)
- Partnership and S-corporation net income ($, returns)

**Deductions (Itemized):**
- Number of returns with itemized deductions
- Total itemized deductions ($)
- State and local income taxes deducted ($, returns)
- Real estate taxes deducted ($, returns)
- Personal property taxes deducted ($, returns)
- Mortgage interest paid ($, returns)
- Charitable contributions ($, returns)
- Medical and dental expenses deducted ($, returns)

**Tax Credits:**
- Number of returns with Earned Income Tax Credit (EITC)
- Total EITC amount ($)
- Number of returns with child tax credit
- Total child tax credit ($)
- Number of returns with additional child tax credit
- Number of returns with education credits

**Tax Liability:**
- Total income tax ($)
- Income tax after credits ($)

#### Data Access

**Primary Download:**
- **URL:** https://www.irs.gov/statistics/soi-tax-stats-county-data
- **Format:** Excel files by state, ZIP archives by year
- **Files:** One Excel file per state per year (e.g., "22incyall.xls" = all states 2022)
- **County Identification:** County name, state abbreviation, county code

**Download Example:**
```r
library(tidyverse)
library(readxl)

# Download IRS SOI County Data for 2022 (all states file)
# URL: https://www.irs.gov/pub/irs-soi/22incyall.xls

soi_2022 <- read_excel("22incyall.xls", sheet = "County Data")

# Key columns:
# STATE, COUNTYNAME, AGI_STUB (income bracket), N1 (returns), A00100 (AGI),
# N00200 (returns with salaries), A00200 (salaries total),
# N00300 (returns with taxable interest), A00300 (interest total),
# N18300 (returns with itemized deductions), A18300 (itemized total),
# N04470 (returns with itemized deductions), A04470 (itemized deductions),
# MARS1 (single returns), MARS2 (joint returns)

# Calculate county totals across all income brackets
county_totals <- soi_2022 %>%
  filter(AGI_STUB == 0) %>%  # AGI_STUB 0 = all income levels
  mutate(
    mean_agi = A00100 / N1,
    pct_with_salaries = N00200 / N1 * 100,
    mean_salaries = A00200 / N00200,
    pct_itemize = N04470 / N1 * 100,
    mean_mortgage_interest = A18300 / N18300,
    mean_charitable = A19700 / N19700
  )

# Income distribution analysis
income_dist <- soi_2022 %>%
  filter(AGI_STUB != 0) %>%  # Exclude total row
  group_by(STATE, COUNTYNAME) %>%
  mutate(
    pct_returns = N1 / sum(N1) * 100,
    pct_agi = A00100 / sum(A00100) * 100
  ) %>%
  select(STATE, COUNTYNAME, AGI_STUB, N1, pct_returns, A00100, pct_agi)

write_csv(county_totals, "county_irs_soi_2022.csv")
```

#### Data Quality

**Strengths:**
- Administrative records (actual tax returns, not surveys)
- Complete county coverage (all 3,143 counties)
- Detailed income composition (wages vs. business vs. capital vs. retirement)
- Long time series (1989-2022, 33 years)
- Annual updates

**Limitations:**
- Only taxpayers (excludes non-filers, though >90% of adults file)
- 18-month lag (2022 data released mid-2024)
- Suppression for privacy: cells with <20 returns may be suppressed in detailed tables
- Income brackets changed over time (requires harmonization for long-term comparisons)

**Comparison to Census ACS:**
- **IRS SOI:** Annual, detailed income composition, tax-specific items (mortgage interest, charitable giving)
- **Census ACS:** 5-year estimates, demographic detail, non-cash income (SNAP, etc.)
- **Complementary:** Use both for comprehensive income analysis

#### Use Cases

1. **Income Inequality:** AGI distribution across brackets, capital gains concentration
2. **Housing Affordability:** Mortgage interest deductions indicate homeownership costs
3. **Philanthropy:** Charitable contributions by county
4. **Economic Composition:** Wage vs. business vs. capital income shares
5. **Tax Burden:** Total tax liability, credits (EITC, child tax credit)

**Priority Variables:**
- Total AGI, mean AGI
- Salaries and wages (total, mean)
- Business income
- Capital gains
- Retirement income (pensions, Social Security, IRA)
- Mortgage interest deductions
- Charitable contributions
- EITC recipients and amount

---

### Source 2: IRS County-to-County Migration Data

**Official Name:** IRS Statistics of Income - Migration Data
**Status:** ✅ ONLY SOURCE OF COUNTY-LEVEL MIGRATION FLOWS (1990-2022, 32 years)

#### Overview

IRS SOI migration data tracks year-to-year address changes on tax returns, providing origin-destination migration flows between all US counties. This is the ONLY comprehensive source of annual county-to-county migration data.

#### Coverage

- **Geographic:** All 3,143 US counties (3,143 × 3,143 = 9.8 million possible county pairs)
- **Temporal:** 1990-2022 (32-year annual time series)
- **Update Frequency:** Annual (released ~18 months after tax year)
- **Migration Year:** Tax year to tax year (e.g., 2021-2022 data shows moves between 2021 and 2022 returns)

#### Variables Available (10+ per origin-destination pair)

**Inflows (by Origin County):**
- Number of returns (households) moving IN from each origin county
- Number of personal exemptions (people) in migrating households
- Total AGI ($) of in-migrants from each origin county

**Outflows (by Destination County):**
- Number of returns (households) moving OUT to each destination county
- Number of personal exemptions (people) in migrating households
- Total AGI ($) of out-migrants to each destination county

**Non-Migrants:**
- Number of returns that did not move (same county both years)
- Number of exemptions (people) in non-migrant households
- Total AGI of non-migrants

**Net Migration:**
- Net migration (inflows - outflows) by county
- Net AGI gain/loss ($)
- Net exemption gain/loss (people)

**Migration Type:**
- Same-state migration (county-to-county within state)
- Different-state migration (interstate)
- Foreign migration (returns filed from foreign address)

#### Data Files

**Two File Types:**

**1. County Inflow Files:**
- Lists all origin counties sending migrants TO each destination county
- File per county: "countyinflow/co[FIPS]inflow.csv"
- Example: co06037inflow.csv = all counties sending migrants to Los Angeles County

**2. County Outflow Files:**
- Lists all destination counties receiving migrants FROM each origin county
- File per county: "countyoutflow/co[FIPS]outflow.csv"
- Example: co06037outflow.csv = all counties receiving migrants from Los Angeles County

#### Data Access

**Primary Download:**
- **URL:** https://www.irs.gov/statistics/soi-tax-stats-migration-data
- **Format:** CSV files (one per county per year)
- **County Files:** 3,143 inflow files + 3,143 outflow files per year = 6,286 files/year
- **Bulk Download:** ZIP archives by year

**Download Example:**
```r
library(tidyverse)

# Download county inflow data for Los Angeles County (FIPS 06037), 2021-2022
inflow_la <- read_csv("co06037inflow2122.csv")

# Columns:
# y1_statefips, y1_countyfips, y1_state, y1_county (origin)
# y2_statefips (destination state = 06), y2_countyfips (= 037)
# n1 (returns), n2 (exemptions), AGI (aggregate income)

# Top 10 origin counties for LA inflows
top_origins <- inflow_la %>%
  arrange(desc(n1)) %>%
  head(10) %>%
  select(y1_state, y1_county, returns = n1, people = n2, total_agi = AGI) %>%
  mutate(
    mean_agi = total_agi / returns
  )

# Download county outflow data
outflow_la <- read_csv("co06037outflow2122.csv")

# Top 10 destination counties for LA outflows
top_destinations <- outflow_la %>%
  arrange(desc(n1)) %>%
  head(10)

# Calculate net migration for LA County
# (Sum all inflows) - (sum all outflows)
total_in <- sum(inflow_la$n1, na.rm = TRUE)
total_out <- sum(outflow_la$n1, na.rm = TRUE)
net_migration <- total_in - total_out

net_agi_in <- sum(inflow_la$AGI, na.rm = TRUE)
net_agi_out <- sum(outflow_la$AGI, na.rm = TRUE)
net_agi_gain <- net_agi_in - net_agi_out
```

**Create County-Level Migration Summary:**
```r
# Function to summarize migration for one county
summarize_county_migration <- function(county_fips, year1, year2) {
  # Read inflow and outflow files
  inflow <- read_csv(paste0("co", county_fips, "inflow", year1, year2, ".csv"))
  outflow <- read_csv(paste0("co", county_fips, "outflow", year1, year2, ".csv"))

  # Calculate totals
  tibble(
    county_fips = county_fips,
    year = paste0(year1, "-", year2),
    inflow_returns = sum(inflow$n1, na.rm = TRUE),
    inflow_people = sum(inflow$n2, na.rm = TRUE),
    inflow_agi = sum(inflow$AGI, na.rm = TRUE),
    outflow_returns = sum(outflow$n1, na.rm = TRUE),
    outflow_people = sum(outflow$n2, na.rm = TRUE),
    outflow_agi = sum(outflow$AGI, na.rm = TRUE),
    net_returns = inflow_returns - outflow_returns,
    net_people = inflow_people - outflow_people,
    net_agi = inflow_agi - outflow_agi,
    mean_agi_inmigrant = inflow_agi / inflow_returns,
    mean_agi_outmigrant = outflow_agi / outflow_returns
  )
}

# Apply to all counties
all_counties <- sprintf("%05d", 1:99999)  # All possible FIPS codes
county_migration_2122 <- map_dfr(all_counties, ~summarize_county_migration(., "21", "22"))
```

#### Data Quality

**Strengths:**
- ONLY source of annual county-to-county migration flows
- Administrative records (address changes on tax returns)
- AGI of migrants (economic impact of migration)
- Long time series (1990-2022, 32 years)
- Complete origin-destination matrix (all county pairs)

**Limitations:**
- Only taxpayers who file in both years
- Excludes non-filers, deaths, new filers
- Underestimates total population migration (captures ~80-90%)
- Address changes only (may include non-moves like P.O. box changes)
- Suppression: Flows with <10 returns suppressed in some years

**Comparison to Census ACS Migration Data:**
- **IRS:** Annual, origin-destination flows, AGI data
- **Census ACS:** 5-year estimates, limited origin detail (state level), demographic detail
- **Complementary:** IRS for flows/economic impact, Census for demographics

#### Use Cases

1. **Migration Networks:** Identify major migration corridors (which counties exchange most migrants)
2. **Brain Drain:** Counties losing high-AGI taxpayers
3. **Economic Impact:** Net AGI gain/loss from migration
4. **Urban-Rural Shifts:** COVID-era urban exodus analysis
5. **Climate Migration:** Tracking moves from high-risk counties (hurricanes, wildfires, sea-level rise)

**Priority Variables:**
- Net migration (returns, people)
- Net AGI gain/loss
- Top origin counties (inflows)
- Top destination counties (outflows)
- Mean AGI of in-migrants vs. out-migrants

---

### Source 3: Federal Reserve Household Debt by County

**Official Name:** Federal Reserve Bank Consumer Credit Panel / Household Debt by County
**Status:** ✅ LONGEST COUNTY-LEVEL DEBT TIME SERIES (1999-2025, 26 years, QUARTERLY!)

#### Overview

The Federal Reserve Bank of New York, in partnership with Equifax, publishes comprehensive household debt statistics by county based on a 5% sample of all US credit reports (10+ million individuals). This is the most comprehensive source of county-level consumer debt and credit health data.

#### Coverage

- **Geographic:** All 3,143 US counties
- **Temporal:** 1999-Q1 to 2025-Q1 (26-year quarterly time series!)
- **Update Frequency:** Quarterly (released ~2 months after quarter end)
- **Sample:** 5% random sample of US consumers with credit reports

#### Variables Available (20+)

**Total Debt Balances:**
- Total consumer debt per capita ($)
- Household debt-to-income ratio (%)
- Median debt per borrower ($)
- Mean debt per borrower ($)

**Debt by Type:**
- Mortgage debt (total $, per capita)
- Home Equity Line of Credit (HELOC) balance ($)
- Auto loan debt ($)
- Credit card debt ($)
- Student loan debt ($)
- Other consumer debt ($)
- Number of borrowers by debt type

**Debt Composition:**
- % of total debt in mortgages
- % in auto loans
- % in credit cards
- % in student loans

**Delinquency Rates:**
- % of debt 30+ days past due
- % of debt 60+ days past due
- % of debt 90+ days past due
- % of debt 120+ days past due
- Delinquency rates by debt type (mortgage, auto, credit card, student)
- Seriously delinquent rate (90+ days)

**New Delinquencies (Transitions):**
- % of current accounts becoming 30+ days delinquent this quarter
- Flow into delinquency by debt type

**Foreclosures & Bankruptcies:**
- Foreclosure starts (count, rate)
- Foreclosures completed
- Bankruptcies filed (from credit reports)
- % of consumers with foreclosure/bankruptcy in past 7 years

**Credit Utilization:**
- Credit card utilization rate (% of available credit used)
- Average credit limit per card ($)
- Number of credit cards per borrower

**Credit Scores:**
- Median credit score (county)
- % of consumers with subprime credit (<620)
- % with near-prime (620-679)
- % with prime (680-739)
- % with super-prime (740+)

**New Credit:**
- Number of new credit accounts opened (quarter)
- Hard inquiries (credit checks)
- New credit cards
- New auto loans
- New mortgages

**Debt in Collections:**
- % of consumers with debt in collections
- Median debt in collections ($)
- Average debt in collections ($)
- % with medical debt in collections

#### Data Access

**Federal Reserve Bank of New York:**
- **URL:** https://www.newyorkfed.org/microeconomics/hhdc
- **Dashboard:** Household Debt and Credit Reports (quarterly)
- **Interactive Map:** County-level data visualization
- **Format:** Excel, CSV downloads available

**Urban Institute Debt in America:**
- **URL:** https://apps.urban.org/features/debt-interactive-map/
- **Source:** Credit bureau panel (similar to Fed data)
- **Format:** Interactive map with downloadable data
- **Variables:** Debt in collections, medical debt, share with debt

**Download Example:**
```r
library(tidyverse)

# Federal Reserve household debt county data (hypothetical URL structure)
# Check Fed website for actual download links

debt_2024q4 <- read_csv("fed_household_debt_county_2024q4.csv")

# Typical columns:
# county_fips, county_name, state, quarter, year,
# total_debt_per_capita, mortgage_debt, auto_debt, credit_card_debt, student_debt,
# delinquency_rate_30plus, delinquency_rate_90plus,
# median_credit_score, pct_subprime, pct_with_collections,
# debt_to_income_ratio, foreclosure_rate

# Calculate debt burden indicators
debt_analysis <- debt_2024q4 %>%
  mutate(
    high_debt_burden = debt_to_income_ratio > 200,  # >2x income
    high_delinquency = delinquency_rate_90plus > 5,  # >5% seriously delinquent
    low_credit = median_credit_score < 650,
    financial_distress = high_debt_burden & high_delinquency & low_credit
  )

# Time series analysis (if multiple quarters available)
debt_trends <- read_csv("fed_debt_1999_2025_all_quarters.csv")

county_debt_trends <- debt_trends %>%
  group_by(county_fips) %>%
  arrange(year, quarter) %>%
  mutate(
    debt_change_qoq = (total_debt_per_capita - lag(total_debt_per_capita)) / lag(total_debt_per_capita) * 100,
    delinquency_change = delinquency_rate_90plus - lag(delinquency_rate_90plus)
  )
```

#### Data Quality

**Strengths:**
- Longest county-level debt time series (1999-2025, 26 years!)
- Quarterly updates (highest temporal resolution)
- Comprehensive debt types (mortgage, auto, credit card, student)
- Credit health metrics (scores, delinquencies, collections)
- Based on actual credit bureau records (not self-reported)
- Large sample (10+ million individuals, 5% of US consumers)

**Limitations:**
- Only consumers with credit reports (excludes "credit invisible" population ~11% of adults)
- Sample-based (not universe, but large sample)
- Some privacy suppression for very small counties
- No demographic detail by county (age, race, income not reported to protect privacy)

#### Use Cases

1. **Financial Distress Mapping:** High debt-to-income, high delinquency counties
2. **Recession Indicators:** Delinquency rate spikes predict economic downturns
3. **Housing Crisis:** Mortgage delinquency, foreclosure trends
4. **Student Debt Burden:** Counties with highest student loan debt
5. **Health & Debt:** Link medical debt to health outcomes, insurance coverage

**Priority Variables:**
- Total debt per capita
- Debt-to-income ratio
- Mortgage, auto, credit card, student loan debt (separate)
- 90+ day delinquency rate
- Median credit score
- % with debt in collections
- Foreclosure rate
- Bankruptcy rate

---

### Source 4: Federal Court Bankruptcy Filings by County

**Official Name:** U.S. Courts Bankruptcy Statistics by County
**Status:** ✅ COMPREHENSIVE BANKRUPTCY TRACKING (2007-present, QUARTERLY)

#### Overview

The Administrative Office of the U.S. Courts publishes bankruptcy filing statistics by county, tracking Chapter 7 (liquidation), Chapter 11 (business reorganization), Chapter 12 (family farmer/fisherman), and Chapter 13 (wage earner repayment) filings.

#### Coverage

- **Geographic:** All 3,143 US counties
- **Temporal:** 2007-present (18 years, quarterly)
- **Update Frequency:** Quarterly (released ~2 months after quarter end)
- **Court System:** 94 federal bankruptcy court districts

#### Variables Available (12+)

**Total Filings:**
- Total bankruptcy petitions filed
- Total business bankruptcies
- Total non-business (consumer) bankruptcies

**By Chapter:**
- Chapter 7 filings (liquidation)
  - Business Chapter 7
  - Non-business Chapter 7
- Chapter 11 filings (reorganization)
  - Business Chapter 11
  - Individual Chapter 11
- Chapter 12 filings (family farmer/fisherman)
- Chapter 13 filings (wage earner repayment plan)

**Filing Rates:**
- Filings per 1,000 population
- Filings per 1,000 households
- Business filings per 1,000 establishments

**Temporal Metrics:**
- Quarterly filings
- 12-month rolling total
- Year-over-year change (count, %)
- Quarter-over-quarter change

**Rankings:**
- County rank within state (by filing rate)
- County rank within district
- County rank nationally

#### Data Access

**Primary Portal:**
- **URL:** https://www.uscourts.gov/statistics-reports/bankruptcy-filings-statistics
- **Interactive Dashboard:** https://www.uscourts.gov/statistics-reports/analysis-reports/bankruptcy-filings-statistics
- **Format:** Excel downloads, interactive visualizations

**Download Example:**
```r
library(tidyverse)

# Download bankruptcy filings by county (example structure)
bankruptcy_2024q4 <- read_csv("uscourts_bankruptcy_county_2024q4.csv")

# Typical columns:
# district, state, county, quarter, year,
# total_filings, chapter_7, chapter_11, chapter_12, chapter_13,
# business_filings, nonbusiness_filings,
# filings_per_1000_pop, yoy_change_pct

# Calculate bankruptcy distress indicators
bankruptcy_analysis <- bankruptcy_2024q4 %>%
  left_join(county_population, by = "county") %>%
  mutate(
    filing_rate_per_1000 = (total_filings / population) * 1000,
    business_pct = (business_filings / total_filings) * 100,
    chapter_7_pct = (chapter_7 / total_filings) * 100,  # Liquidation
    chapter_13_pct = (chapter_13 / total_filings) * 100,  # Repayment
    high_bankruptcy = filing_rate_per_1000 > 5  # >5 per 1,000 = high distress
  )

# Time series analysis
bankruptcy_trends <- read_csv("bankruptcy_2007_2024_all_quarters.csv")

county_trends <- bankruptcy_trends %>%
  group_by(county_fips) %>%
  arrange(year, quarter) %>%
  mutate(
    rolling_12mo = zoo::rollsum(total_filings, k = 4, fill = NA, align = "right"),
    change_from_prepandemic = (total_filings - total_filings[year == 2019 & quarter == "Q4"]) / total_filings[year == 2019 & quarter == "Q4"] * 100
  )
```

#### Data Quality

**Strengths:**
- Official court records (complete data, not sampled)
- Quarterly updates (high temporal resolution)
- Chapter-specific detail (liquidation vs. reorganization vs. repayment)
- Business vs. consumer distinction
- Long time series (2007-present, 18 years including Great Recession)

**Limitations:**
- Only formal bankruptcy filings (excludes informal debt settlements, delinquency without filing)
- Assigned to county of debtor residence, not business location (for businesses)
- Economic/business cycles cause high volatility (recession spikes)

#### Use Cases

1. **Financial Distress:** Acute financial crisis indicator
2. **Recession Tracking:** Bankruptcy spikes during economic downturns (2008-2010, 2020)
3. **Business Health:** Chapter 11 filings indicate business distress
4. **Consumer Debt Crisis:** Chapter 7/13 consumer filings indicate household financial stress
5. **Policy Evaluation:** Bankruptcy rate changes after policy interventions (e.g., BAPCPA 2005)

**Priority Variables:**
- Total filings per 1,000 population
- Chapter 7 filings (liquidation)
- Chapter 13 filings (repayment)
- Business bankruptcies
- Year-over-year change
- 12-month rolling total

---

### Source 5: Census Building Permits by County

**Official Name:** U.S. Census Bureau Building Permits Survey (BPS)
**Status:** ✅ LONGEST HOUSING CONSTRUCTION TIME SERIES (1980-2024, 44 years!)

#### Overview

The Census Bureau Building Permits Survey collects data from ~20,000 permit-issuing jurisdictions nationwide, providing comprehensive county-level housing construction activity tracking.

#### Coverage

- **Geographic:** All 3,143 US counties
- **Temporal:** 1980-2024 (44-year annual time series!)
- **Update Frequency:** Annual (released first workday of May for prior year)
- **Monthly Data:** Also available monthly (with year-to-date totals)

#### Variables Available (20+)

**Housing Units Authorized:**
- Total units authorized by building permits
- Single-family units (1-unit structures)
- 2-unit structures
- 3-4 unit structures
- 5+ unit structures (multifamily)

**Number of Structures:**
- Number of single-family structures
- Number of multifamily buildings (2+ units)

**Construction Value:**
- Total construction value ($)
- Value of single-family construction ($)
- Value of multifamily construction ($)
- Average value per unit ($)
- Average value per single-family unit ($)
- Average value per multifamily unit ($)

**Temporal Resolution:**
- Monthly permits (by unit type)
- Year-to-date cumulative totals
- Annual totals

**Geographic Detail:**
- County FIPS code
- County name, state
- Metropolitan statistical area (MSA) status
- MSA name (if inside MSA)
- Core Based Statistical Area (CBSA)

**Derived Metrics:**
- Permits per 1,000 population
- Permits per 1,000 existing housing units
- Single-family as % of total units
- Multifamily as % of total units
- Year-over-year change (count, %)
- 5-year average comparison
- Permit growth rate

#### Data Access

**Primary Download:**
- **URL:** https://www.census.gov/construction/bps/
- **County Data:** https://www.census.gov/construction/bps/county.html
- **Format:** Excel files by year, CSV downloads
- **Interactive Tool:** https://www.census.gov/library/stories/2023/05/building-permit-tool.html

**Alternative Access (HUD Open Data):**
- **URL:** https://hudgis-hud.opendata.arcgis.com/datasets/HUD::residential-construction-permits-by-county/
- **Format:** CSV, GeoJSON, Shapefile
- **Same underlying data as Census**

**Download Example:**
```r
library(tidyverse)

# Download Census Building Permits 2024 county data
permits_2024 <- read_csv("bps_county_2024.csv")

# Key columns:
# FIPS, County_Name, State, CBSA, Metro_Status,
# Total_Units, Units_1, Units_2, Units_3to4, Units_5plus,
# Value_Total, Value_1unit, Value_5plus,
# Structures_1, Structures_5plus

# Calculate housing supply metrics
permits_analysis <- permits_2024 %>%
  left_join(county_population, by = "FIPS") %>%
  left_join(housing_units, by = "FIPS") %>%
  mutate(
    permits_per_1000_pop = (Total_Units / population) * 1000,
    permits_per_1000_units = (Total_Units / housing_units) * 1000,
    pct_single_family = (Units_1 / Total_Units) * 100,
    pct_multifamily = (Units_5plus / Total_Units) * 100,
    avg_value_per_unit = Value_Total / Total_Units,
    construction_boom = permits_per_1000_pop > 10  # >10 permits/1,000 pop = high growth
  )

# Time series analysis (1980-2024)
permits_timeseries <- map_dfr(1980:2024, ~read_csv(paste0("bps_county_", ., ".csv")))

county_construction_trends <- permits_timeseries %>%
  group_by(FIPS) %>%
  arrange(year) %>%
  mutate(
    permits_5yr_avg = zoo::rollmean(Total_Units, k = 5, fill = NA, align = "right"),
    pct_change_from_2006 = (Total_Units - Total_Units[year == 2006]) / Total_Units[year == 2006] * 100,  # Pre-housing crisis
    pct_change_from_2019 = (Total_Units - Total_Units[year == 2019]) / Total_Units[year == 2019] * 100,  # Pre-COVID
    housing_boom_80s = year >= 1980 & year <= 1989,
    housing_boom_00s = year >= 2000 & year <= 2006,
    housing_bust = year >= 2007 & year <= 2011,
    post_covid_boom = year >= 2021
  )

# Identify fastest-growing counties (2020-2024)
growth_2020_2024 <- permits_timeseries %>%
  filter(year %in% c(2020, 2024)) %>%
  group_by(FIPS) %>%
  summarize(
    permits_2020 = Total_Units[year == 2020],
    permits_2024 = Total_Units[year == 2024],
    absolute_change = permits_2024 - permits_2020,
    pct_change = ((permits_2024 - permits_2020) / permits_2020) * 100,
    .groups = "drop"
  ) %>%
  arrange(desc(pct_change))
```

#### Data Quality

**Strengths:**
- Longest county-level housing construction time series (1980-2024, 44 years!)
- Complete geographic coverage (all 3,143 counties)
- Annual AND monthly data available
- Single-family vs. multifamily distinction
- Construction value (economic impact)
- High-quality data from permit offices (administrative records)
- Minimal lag (released first workday of May for prior year)

**Limitations:**
- Only permitted construction (excludes unpermitted additions, renovations)
- Permits issued ≠ units completed (some permits expire, construction delayed)
- Renovation/remodeling permits not consistently tracked
- Some rural counties issue very few permits (small counts, high volatility)

#### Use Cases

1. **Housing Supply Analysis:** Identify counties with severe housing undersupply (low permits, high demand)
2. **Population Growth Forecasting:** Building permits are leading indicator of population growth
3. **Economic Development:** Construction activity indicates economic health
4. **Affordability Crisis:** Low permit issuance → constrained supply → price increases
5. **Urban Sprawl:** Tracking single-family vs. multifamily permits (density trends)

**Priority Variables:**
- Total housing units authorized
- Single-family units
- Multifamily units (5+)
- Total construction value
- Permits per 1,000 population
- Permits per 1,000 existing housing units
- Year-over-year change

---

## PART 2: INNOVATION & PATENTS

### Source 6: USPTO Patent Data by Inventor County

**Official Name:** U.S. Patent and Trademark Office (USPTO) - Patents by County
**Status:** ✅ LONGEST INNOVATION TIME SERIES (1975-2020, 45 years!)

#### Overview

USPTO publishes patent statistics by inventor county of residence, providing the ONLY comprehensive measure of county-level innovation activity over time.

#### Coverage

- **Geographic:** All counties with patent activity (~1,500-2,000 counties typically have ≥1 patent/year)
- **Temporal:** 1975-2020 (comprehensive); partial 2021-2024
- **Update Frequency:** Annual (lagged ~2 years after grant year)
- **Patent Type:** Utility patents (inventions)

#### Variables Available (20+)

**Patent Counts:**
- Number of utility patents by inventor county
- Number of inventors per county
- Patents per 1,000 population (innovation intensity)
- Patents per 1,000 labor force

**Assignee Type:**
- Corporate-assigned patents (count, %)
- Government-assigned patents (count, %)
- University-assigned patents (count, %)
- Individual-assigned patents (count, %)
- Unassigned patents

**Technology Classification:**
- Patents by USPTO class (600+ classes)
- Patents by technology sector (broad categories):
  - Chemical
  - Computers & Communications
  - Drugs & Medical
  - Electrical & Electronic
  - Mechanical
  - Others
- Technology concentration (Herfindahl index)

**Patent Quality Metrics:**
- Forward citations received (patent influence)
- Backward citations made (knowledge base)
- Number of claims per patent (breadth)
- Patent family size (international protection)

**Collaboration:**
- Patents with multiple inventors (co-invention rate)
- Patents with inventors from multiple counties (intercounty collaboration)
- Patents with foreign co-inventors (international collaboration)
- Average number of inventors per patent

**Organizational Detail:**
- Number of assignee organizations (companies) per county
- Top assignee organizations by patent count
- Assignee concentration (top 1, top 5, top 10 firms' share)

**Geographic Context:**
- Metropolitan/micropolitan/rural designation
- Core-Based Statistical Area (CBSA)
- State

**Temporal Metrics:**
- Annual patent count time series
- 3-year moving averages
- Growth rates (year-over-year, 5-year, 10-year)
- Trend analysis (acceleration, deceleration)

#### Data Access

**USPTO Official Reports:**
- **URL:** https://www.uspto.gov/web/offices/ac/ido/oeip/taf/reports_cbsa.htm
- **County Reports:** https://www.uspto.gov/web/offices/ac/ido/oeip/taf/countyall/explan_countyall.htm
- **Format:** Excel tables, historical data files

**PatentsView API:**
- **URL:** https://patentsview.org/
- **API:** RESTful API for querying patent data
- **Format:** JSON, CSV exports
- **Query by:** Inventor location (city, county, state), assignee, technology class, year

**Download Example:**
```r
library(tidyverse)
library(httr)
library(jsonlite)

# Download USPTO county patent data (official table)
patents_2020 <- read_csv("uspto_patents_by_county_2020.csv")

# Typical columns:
# county_fips, county_name, state, cbsa, metro_status,
# patents_total, inventors, patents_per_1000_pop,
# pct_corporate, pct_university, pct_government, pct_individual,
# tech_chemical, tech_computers, tech_drugs_medical, tech_electrical, tech_mechanical

# Calculate innovation metrics
innovation_analysis <- patents_2020 %>%
  left_join(county_population, by = "county_fips") %>%
  mutate(
    patents_per_100k = (patents_total / population) * 100000,
    high_innovation = patents_per_100k > 50,  # >50 patents/100k pop
    university_innovation_hub = pct_university > 30,
    tech_diversity = 1 - (tech_chemical^2 + tech_computers^2 + tech_drugs_medical^2 + tech_electrical^2 + tech_mechanical^2)  # Herfindahl diversity
  )

# Time series analysis using PatentsView API
# Query patents for a county over time
patents_api <- "https://api.patentsview.org/patents/query"

# Example: Santa Clara County, CA (Silicon Valley) 1975-2020
query <- list(
  q = '{"_and":[{"inventor_county":"Santa Clara"},{"inventor_state":"CA"}]}',
  f = '["patent_number","patent_year","assignee_organization","patent_title","uspc_mainclass_title"]',
  o = '{"per_page":10000}',
  s = '[{"patent_year":"asc"}]'
)

response <- GET(patents_api, query = query)
patents_data <- fromJSON(content(response, "text"))$patents

# Aggregate by year
patents_by_year <- patents_data %>%
  count(patent_year, name = "patents") %>%
  arrange(patent_year)

# Growth rate calculation
patents_growth <- patents_by_year %>%
  mutate(
    growth_rate = (patents - lag(patents)) / lag(patents) * 100,
    patents_5yr_avg = zoo::rollmean(patents, k = 5, fill = NA, align = "right")
  )
```

#### Data Quality

**Strengths:**
- LONGEST county-level innovation time series (1975-2020, 45 years!)
- Administrative records (actual patent grants)
- Technology classification (innovation type)
- Assignee information (corporate vs. university vs. individual)
- Quality metrics (citations, claims, family size)

**Limitations:**
- Inventor address at time of patent grant (may have moved since invention)
- Patents lag innovation (2-3 years from application to grant)
- Not all innovation results in patents (trade secrets, unpatentable innovations)
- Concentra in metropolitan areas (skewed distribution)
- ~1,500-2,000 counties have ≥1 patent/year; ~1,000+ counties have zero patents

#### Use Cases

1. **Innovation Ecosystems:** Identify high-innovation counties (hubs)
2. **University-Industry Linkages:** University-assigned patents by county
3. **Technology Specialization:** Technology sector concentration (biotech hubs, software hubs, etc.)
4. **Economic Development:** Patent growth as indicator of knowledge economy development
5. **R&D Activity:** Patents correlate with R&D spending, STEM workforce

**Priority Variables:**
- Total patents by county
- Patents per 100,000 population
- % university-assigned patents
- Technology sector breakdown
- Patent growth rate (5-year, 10-year)

---

## PART 3: HEALTH FACILITIES & INFECTIOUS DISEASE

### Source 7: CDC WONDER Natality - Comprehensive Birth Outcomes

**Official Name:** CDC WONDER Natality Data - Birth Statistics
**Status:** ✅ COMPREHENSIVE BIRTH OUTCOMES (1995-2024, 30 years!) - *Extends beyond breastfeeding*

#### Overview

CDC WONDER Natality provides comprehensive birth outcome data from vital records (birth certificates). Your current documentation includes breastfeeding initiation only; this source includes 50+ additional variables on pregnancy, prenatal care, maternal health, and birth outcomes.

#### Coverage

- **Geographic:**
  - **Public-Use:** Counties with >100,000 population (~524 counties) identified
  - **Restricted-Use:** All 3,143 counties (via NCHS Research Data Center application)
- **Temporal:** 1995-2024 (30-year time series!)
- **Update Frequency:** Annual (released ~6 months after calendar year)

#### Variables Available (50+)

**Already Documented (in your files):**
- Breastfeeding initiation rate (% of infants breastfed at all)

**NEWLY ADDED COMPREHENSIVE VARIABLES:**

**Pregnancy Outcomes:**
- Live births (count)
- Crude birth rate (per 1,000 population)
- General fertility rate (per 1,000 women 15-44)
- Total fertility rate (births per woman)
- Age-specific fertility rates (5-year age groups)

**Birth Weight:**
- Very low birthweight <1,500g (count, %)
- Low birthweight <2,500g (count, %)
- Normal birthweight 2,500-3,999g (count, %)
- High birthweight ≥4,000g (macrosomia, count, %)
- Mean birthweight (grams)

**Gestational Age:**
- Very preterm <32 weeks (count, %)
- Preterm <37 weeks (count, %)
- Late preterm 34-36 weeks (count, %)
- Early term 37-38 weeks (count, %)
- Full term 39-40 weeks (count, %)
- Late term 41 weeks (count, %)
- Post-term ≥42 weeks (count, %)
- Mean gestational age (weeks)

**Prenatal Care:**
- Trimester prenatal care began (1st, 2nd, 3rd, no care)
- Month prenatal care began (1-10, none)
- Number of prenatal visits (0, 1-2, 3-4, 5-6, 7-8, 9-10, 11+)
- Adequate prenatal care (Kessner Index)
- Intensive prenatal care (Kotelchuck APNCU Index)
- No prenatal care (count, %)

**Maternal Demographics:**
- Mother's age (single years, 5-year groups)
- Mother's race/ethnicity (NH White, NH Black, Hispanic, NH Asian, NH AIAN, NH NHOPI, multiracial)
- Mother's education (<HS, HS, some college, bachelor's, graduate)
- Mother's marital status (married, unmarried)
- Mother's nativity (US-born, foreign-born)
- Parity (birth order: 1st, 2nd, 3rd, 4th+)

**Maternal Health Conditions:**
- Pre-pregnancy diabetes (yes/no)
- Gestational diabetes (yes/no)
- Pre-pregnancy hypertension (yes/no)
- Gestational hypertension (yes/no)
- Hypertension eclampsia (yes/no)
- Previous preterm birth (yes/no for parous women)
- Previous cesarean delivery (yes/no for parous women)
- Infertility treatment (yes/no)

**Pre-Pregnancy Body Mass Index (BMI):**
- BMI value
- BMI categories: Underweight (<18.5), Normal (18.5-24.9), Overweight (25-29.9), Obese I (30-34.9), Obese II (35-39.9), Obese III (≥40)

**Maternal Behaviors:**
- Smoking before pregnancy (yes/no, cigarettes/day)
- Smoking during 1st trimester (yes/no, cigarettes/day)
- Smoking during 2nd trimester (yes/no, cigarettes/day)
- Smoking during 3rd trimester (yes/no, cigarettes/day)
- Mother received WIC food (yes/no)

**Delivery Characteristics:**
- Delivery method: Vaginal (spontaneous, induced, assisted)
- Cesarean section: Primary C-section, Repeat C-section
- Plurality: Singleton, Twins, Triplets+
- Sex of infant: Male, Female
- 5-minute Apgar score (<7 abnormal, 7-8 intermediate, 9-10 normal)

**Birth Facility:**
- Hospital
- Freestanding birth center
- Home (intended, unintended)
- Other

**Payment Source:**
- Medicaid
- Private insurance
- Self-pay
- Other

#### Data Access

**CDC WONDER Natality (Public-Use):**
- **URL:** https://wonder.cdc.gov/natality-current.html (2016-present)
- **Expanded:** https://wonder.cdc.gov/natality-expanded.html (2007-present, more variables)
- **Format:** Web query interface, CSV/TXT exports
- **Geographic Limitation:** Counties with <100,000 population suppressed (only state shown)

**Restricted-Use County Data:**
- **Access:** NCHS Research Data Center (RDC) application
- **URL:** https://www.cdc.gov/rdc/
- **Coverage:** All 3,143 counties (no suppression)
- **Process:** Proposal submission, IRB approval, on-site or remote secure access

**Download Example (Public-Use):**
```r
# CDC WONDER query for large counties (>100k population)
# Manual query via web interface, export to CSV

natality_2023 <- read_csv("cdc_wonder_natality_2023_large_counties.csv")

# Key columns:
# County, State, Births, LBW (low birthweight %), Preterm (%),
# No_Prenatal_Care (%), Mean_Age, Pct_Hispanic, Pct_NH_Black,
# C_section_Rate (%), Teen_Birth_Rate, Advanced_Maternal_Age_Rate (35+)

# Calculate maternal-infant health indicators
birth_outcomes <- natality_2023 %>%
  mutate(
    high_LBW = LBW > 9,  # >9% low birthweight (US avg ~8.5%)
    high_preterm = Preterm > 10,  # >10% preterm (US avg ~10.5%)
    inadequate_prenatal = No_Prenatal_Care > 5,  # >5% no prenatal care
    high_c_section = C_section_Rate > 32,  # >32% C-section (US avg ~32%)
    high_risk_births = high_LBW & high_preterm & inadequate_prenatal
  )

# Racial disparities analysis
racial_disparities <- natality_2023 %>%
  # This would require separate queries by race/ethnicity
  # CDC WONDER allows grouping by race
  group_by(County) %>%
  summarize(
    LBW_ratio_black_white = LBW_Black / LBW_White,  # Disparity ratio
    Preterm_ratio_black_white = Preterm_Black / Preterm_White
  )
```

#### Data Quality

**Strengths:**
- Comprehensive vital records (near-universal capture of births)
- Long time series (1995-2024, 30 years!)
- Maternal health conditions (diabetes, hypertension, BMI)
- Prenatal care detail (timing, frequency)
- Maternal behaviors (smoking by trimester)
- Standardized across all states (revised birth certificate as of 2016)

**Limitations:**
- **Geographic suppression (public-use):** Only ~524 large counties identified; smaller counties suppressed
- **Restricted-use access:** Requires RDC application for all counties
- Revised vs. unrevised birth certificate (2003-2016 transition period; not all states adopted revised certificate simultaneously)
- Smoking data: Self-reported, known underreporting
- Prenatal care: Medical records-based, but inconsistent documentation

**Comparison to What You Have:**
- **Your Current:** Breastfeeding initiation only
- **Adding:** 50+ variables on pregnancy, prenatal care, maternal health, birth outcomes

#### Use Cases

1. **Maternal-Infant Health:** Identify counties with high preterm birth, low birthweight
2. **Healthcare Access:** Prenatal care timing and adequacy by county
3. **Health Disparities:** Racial/ethnic disparities in birth outcomes
4. **Environmental Health:** Link preterm birth to air pollution, heat exposure
5. **Maternal Morbidity:** Pre-existing diabetes, hypertension, obesity trends

**Priority Variables:**
- Preterm birth rate (<37 weeks)
- Low birthweight rate (<2,500g)
- No prenatal care (%)
- Late prenatal care (began 3rd trimester, %)
- Pre-pregnancy diabetes (%)
- Gestational diabetes (%)
- Smoking during pregnancy (%)
- Cesarean delivery rate (%)
- Teen birth rate (15-19 years)
- Advanced maternal age rate (≥35 years)

---

### Source 8: CDC COVID-19 Vaccination Data by County

**Official Name:** CDC COVID-19 Vaccinations in the United States, County
**Status:** ✅ COMPREHENSIVE COVID VACCINATION TRACKING (2020-2025, WEEKLY!)

#### Overview

CDC publishes county-level COVID-19 vaccination data from state/local immunization information systems, providing the most comprehensive tracking of vaccination coverage during the pandemic and post-pandemic period.

#### Coverage

- **Geographic:** All 3,143 US counties
- **Temporal:** December 2020-present (5+ years)
- **Update Frequency:** Weekly! (every Thursday)
- **Data Source:** State/local/territorial immunization information systems

#### Variables Available (30+)

**Doses Administered:**
- Total doses administered (cumulative)
- Total doses administered (last 7 days)
- Doses administered per 100,000 population (cumulative)
- Doses per day (7-day rolling average)

**Primary Series (Vaccine Initiation):**
- People with ≥1 dose (count)
- % of total population with ≥1 dose
- People fully vaccinated (count) - completed primary series
- % of total population fully vaccinated

**By Age Group:**
- Vaccinations by age: 5-11, 12-17, 18-24, 25-39, 40-49, 50-64, 65-74, 75+
- % vaccinated by age group
- Age-specific vaccination rates

**Booster Doses:**
- People with 1st booster dose (count, %)
- People with 2nd booster dose (count, %)
- People with bivalent/updated booster (count, %)
- People with 2024-2025 updated COVID-19 vaccine (count, %)

**Series Completion:**
- % completed primary series (2-dose mRNA or 1-dose J&J)
- % up-to-date with boosters (primary + most recent recommended booster)

**Provider Type (limited):**
- Doses administered at pharmacy
- Doses at clinic/health system
- Doses at other locations

**Vaccine Product (some counties):**
- Pfizer-BioNTech doses
- Moderna doses
- Johnson & Johnson (Janssen) doses
- Novavax doses

**Temporal Metrics:**
- Date of first dose in county
- Peak vaccination date (highest daily doses)
- Days to reach 50% vaccinated
- Days to reach 70% vaccinated
- Vaccination pace (doses/day trend)

#### Data Access

**Primary Portal:**
- **URL:** https://data.cdc.gov/Vaccinations/COVID-19-Vaccinations-in-the-United-States-County/8xkx-amqh
- **Dashboard:** https://covid.cdc.gov/covid-data-tracker/#county-view
- **Format:** CSV download, API access, interactive dashboard

**CDC COVID Data Tracker API:**
- **URL:** https://data.cdc.gov/resource/8xkx-amqh.json
- **Format:** JSON, CSV via Socrata API
- **Query:** By county FIPS, date range

**Download Example:**
```r
library(tidyverse)
library(RSocrata)

# Download CDC COVID vaccination data (latest available)
covid_vax <- read.socrata("https://data.cdc.gov/resource/8xkx-amqh.json")

# Convert to data frame
covid_vax_df <- covid_vax %>%
  as_tibble() %>%
  mutate(
    fips = as.character(fips),
    date = as.Date(date),
    series_complete_pop_pct = as.numeric(series_complete_pop_pct),
    administered_dose1_recip_pct = as.numeric(administered_dose1_recip_pct),
    booster_doses_vax_pct = as.numeric(booster_doses_vax_pct)
  )

# Get latest vaccination rates by county
latest_vax <- covid_vax_df %>%
  group_by(fips) %>%
  filter(date == max(date)) %>%
  ungroup() %>%
  select(
    county_fips = fips,
    county_name = recip_county,
    state = recip_state,
    date,
    pct_at_least_1_dose = administered_dose1_recip_pct,
    pct_fully_vaccinated = series_complete_pop_pct,
    pct_with_booster = booster_doses_vax_pct,
    pct_updated_2024 = series_complete_updated_202425_pct
  )

# Identify low-vaccination counties
low_vax_counties <- latest_vax %>%
  filter(pct_fully_vaccinated < 50) %>%  # <50% fully vaccinated
  arrange(pct_fully_vaccinated)

# Time series analysis: vaccination pace
vax_timeseries <- covid_vax_df %>%
  filter(fips == "06037") %>%  # Los Angeles County
  arrange(date) %>%
  mutate(
    doses_per_day = (administered_dose1_recip - lag(administered_dose1_recip)) / as.numeric(date - lag(date)),
    doses_7day_avg = zoo::rollmean(doses_per_day, k = 7, fill = NA, align = "right")
  )

# Peak vaccination periods
peak_vax <- vax_timeseries %>%
  filter(doses_7day_avg == max(doses_7day_avg, na.rm = TRUE))
```

#### Data Quality

**Strengths:**
- Complete county coverage (all 3,143 counties)
- Weekly updates (highest temporal resolution for vaccination data!)
- Age-stratified data
- Primary series + booster tracking
- Long time series (2020-2025, 5+ years covering full pandemic response)
- Official CDC data from immunization registries

**Limitations:**
- Address changes: Individuals who moved may be counted in multiple counties (small effect)
- Vaccine tourism: Some individuals vaccinated outside county of residence
- Underreporting: Not all vaccine doses reported to immunization registries (estimated >95% captured)
- Denominator issues: Population estimates may not match current residents
- Privacy suppression: Some small counties with very low vaccination may have suppressed age-group detail

#### Use Cases

1. **Vaccine Hesitancy:** Identify low-vaccination counties for targeted outreach
2. **Health Disparities:** Age, geographic vaccination disparities
3. **Pandemic Preparedness:** Vaccination pace, booster uptake for future pandemic planning
4. **COVID Mortality Risk:** Link vaccination rates to COVID death rates
5. **Political/Social Determinants:** Vaccination correlates with political affiliation, education, rurality

**Priority Variables:**
- % population with ≥1 dose
- % population fully vaccinated (primary series complete)
- % population with booster dose
- % population with updated 2024-2025 vaccine
- % vaccinated by age group (5-11, 12-17, 18-64, 65+)
- Days to reach 50% and 70% thresholds

---

### Source 9: CDC AtlasPlus - STI, Tuberculosis, Viral Hepatitis, HIV

**Official Name:** CDC NCHHSTP AtlasPlus - National Center for HIV, Viral Hepatitis, STD, and TB Prevention
**Status:** ✅ COMPREHENSIVE INFECTIOUS DISEASE SURVEILLANCE (1996-present for STIs, 29 years!)

#### Overview

CDC AtlasPlus is an integrated interactive tool for querying county-level data on sexually transmitted infections (STIs), tuberculosis (TB), viral hepatitis, and HIV from national notifiable disease surveillance systems.

#### Coverage

- **Geographic:** All US counties (with suppression for small counts <5 typically)
- **Temporal:**
  - STIs: 1996-present (29 years: chlamydia, gonorrhea, syphilis)
  - TB: 1993-present (32 years)
  - Viral Hepatitis: 1996-present (acute hepatitis A, B, C)
  - HIV: Varies by state (2008-present most states)
- **Update Frequency:** Annual (released ~18-24 months after surveillance year)

#### Variables Available (50+)

**Sexually Transmitted Infections (STIs):**

**Chlamydia:**
- Chlamydia cases (count)
- Chlamydia rate per 100,000 population
- Cases by sex (male, female)
- Cases by age group (10-14, 15-19, 20-24, 25-29, 30-34, 35-39, 40-44, 45+)
- Cases by race/ethnicity (NH White, NH Black, Hispanic, NH Asian, NH AIAN, multiracial)
- Annual trend (count, rate)

**Gonorrhea:**
- Gonorrhea cases (count)
- Gonorrhea rate per 100,000
- Cases by sex
- Cases by age group
- Cases by race/ethnicity
- Antimicrobial resistance patterns (subset of cases)

**Syphilis:**
- Primary & secondary (P&S) syphilis cases (count)
- P&S syphilis rate per 100,000
- All stages syphilis (primary, secondary, early latent, late latent, late/unknown)
- Congenital syphilis cases (infants born with syphilis)
- Congenital syphilis rate per 100,000 live births
- Cases by sex, age, race/ethnicity

**Tuberculosis (TB):**

- TB cases (count)
- TB case rate per 100,000
- Culture-confirmed TB cases
- Drug-resistant TB: Multidrug-resistant (MDR), Extensively drug-resistant (XDR)
- Site of disease: Pulmonary TB, Extrapulmonary TB
- Cases by age group
- Cases by race/ethnicity
- Cases by nativity: US-born, Non-US-born
- Treatment outcomes: Completed, Died, Lost to follow-up

**Viral Hepatitis:**

**Acute Hepatitis A:**
- Acute Hepatitis A cases (count)
- Acute Hepatitis A rate per 100,000
- Cases by age, sex, race/ethnicity
- Outbreak-associated cases

**Acute Hepatitis B:**
- Acute Hepatitis B cases (count)
- Acute Hepatitis B rate per 100,000
- Cases by age, sex, race/ethnicity

**Acute Hepatitis C:**
- Acute Hepatitis C cases (count)
- Acute Hepatitis C rate per 100,000
- Cases by age, sex, race/ethnicity
- Injection drug use-associated cases

**Chronic Hepatitis (limited county data):**
- Chronic Hepatitis B prevalence (state-level typically)
- Chronic Hepatitis C prevalence (state-level typically)

**HIV:**

- HIV diagnoses (count)
- HIV diagnosis rate per 100,000
- AIDS diagnoses (count)
- AIDS diagnosis rate per 100,000
- People living with diagnosed HIV (prevalence, count)
- HIV prevalence rate per 100,000
- Deaths among people with diagnosed HIV (count)
- Death rate among people with HIV per 100,000 population
- Transmission category: Male-to-male sexual contact, Injection drug use, Heterosexual contact, Other
- Cases by age group
- Cases by sex
- Cases by race/ethnicity

#### Data Access

**CDC AtlasPlus Interactive Tool:**
- **URL:** https://www.cdc.gov/nchhstp/atlas/
- **Tool:** NCHHSTP AtlasPlus
- **Format:** Interactive map, charts, custom data tables
- **Export:** CSV, Excel, PDF

**Query Steps:**
1. Select disease (STI, TB, Hepatitis, HIV)
2. Select indicator (cases, rates, by demographic)
3. Select geography (county, state)
4. Select year range
5. Select demographic stratification (age, sex, race)
6. View map, chart, or data table
7. Export to CSV/Excel

**Download Example:**
```r
# CDC AtlasPlus data must be downloaded manually via web interface
# (No direct API available as of 2024)

# After downloading CSV from AtlasPlus:
chlamydia_2023 <- read_csv("atlasp lus_chlamydia_county_2023.csv")

# Typical columns:
# County, State, Year, Cases, Rate_per_100k, Population

# Calculate STI burden
sti_analysis <- chlamydia_2023 %>%
  left_join(gonorrhea_2023, by = c("County", "State")) %>%
  left_join(syphilis_2023, by = c("County", "State")) %>%
  mutate(
    total_sti_cases = Chlamydia_Cases + Gonorrhea_Cases + Syphilis_Cases,
    total_sti_rate = (total_sti_cases / Population) * 100000,
    high_sti = total_sti_rate > 1000  # >1,000 STI cases per 100k
  )

# Racial disparities
sti_disparity <- chlamydia_2023_by_race %>%
  pivot_wider(
    names_from = Race,
    values_from = Rate_per_100k,
    names_prefix = "Rate_"
  ) %>%
  mutate(
    disparity_ratio_black_white = Rate_Black / Rate_White,
    disparity_ratio_hisp_white = Rate_Hispanic / Rate_White
  )
```

#### Data Quality

**Strengths:**
- National notifiable disease surveillance systems (comprehensive reporting)
- Long time series (STIs 1996-present, TB 1993-present, 29-32 years!)
- Demographic stratification (age, sex, race/ethnicity)
- County of residence reported
- Integrated tool (query multiple diseases in one portal)

**Limitations:**
- Passive surveillance (depends on testing, diagnosis, reporting)
- **Underdiagnosis:** Asymptomatic STIs (especially chlamydia in men) underdiagnosed
- **Testing bias:** Areas with more STI testing have higher case counts (access effect)
- Small counts suppressed (typically <5 cases)
- County identification limited for small populations in some states
- HIV data availability varies by state (some states don't share county-level HIV data publicly)

**Reporting Completeness:**
- STIs: >90% of diagnosed cases reported
- TB: ~95% of cases reported (high priority disease)
- Hepatitis: Underreporting significant for chronic hepatitis (many undiagnosed)
- HIV: Complete for diagnosed cases, but ~13% of people with HIV unaware of status

#### Use Cases

1. **STI Epidemic Tracking:** Identify counties with surging syphilis, gonorrhea
2. **Health Disparities:** Racial/ethnic disparities in STI, HIV rates
3. **Healthcare Access:** STI rates correlate with testing availability, primary care access
4. **Infectious Disease Surveillance:** TB reemergence, hepatitis outbreaks (e.g., Hep A in homeless populations)
5. **Prevention Planning:** Target counties with high STI/HIV rates for prevention programs (PrEP, condom distribution, needle exchange)

**Priority Variables:**
- Chlamydia rate per 100,000
- Gonorrhea rate per 100,000
- Primary & secondary syphilis rate per 100,000
- Congenital syphilis cases
- TB case rate per 100,000
- Acute Hepatitis A, B, C rates
- HIV diagnosis rate per 100,000
- HIV prevalence (people living with HIV per 100,000)

---

### Source 10: AHA Annual Survey - Hospital Characteristics

**Official Name:** American Hospital Association (AHA) Annual Survey Database
**Status:** ✅ LONGEST HOSPITAL TIME SERIES (1946-present, 79 years!) - **PURCHASE REQUIRED**

#### Overview

The AHA Annual Survey is the MOST comprehensive source of hospital characteristics data in the United States, covering ~6,300 hospitals with 500+ variables on size, services, utilization, staffing, and financial performance. **Note:** This is a PAID product.

#### Coverage

- **Geographic:** ~6,300 hospitals nationally, aggregable to county by hospital address
- **Temporal:** 1946-present (79-year time series!)
- **Update Frequency:** Annual
- **Response Rate:** ~80% of hospitals respond

#### Variables Available (500+)

**Facility Identification:**
- Hospital name, address, city, county FIPS, state, ZIP
- AHA ID (unique identifier)
- Medicare provider number (CMS certification number)
- Latitude/longitude

**Ownership & Structure:**
- Ownership type: Government (federal, state, local), Nonprofit (church, other), For-profit (investor-owned, individual)
- System membership (Yes/No, system name, system ID)
- Network participation (Yes/No, network name)
- Critical Access Hospital (CAH) designation
- Teaching hospital status (major teaching, limited teaching, non-teaching)

**Size & Capacity:**
- Total staffed beds
- Bassinets (newborn beds)
- Adult ICU beds (medical/surgical, cardiac, other)
- Pediatric ICU beds
- Neonatal ICU beds (Level I, II, III, IV)
- Burn care beds
- Operating rooms
- Emergency department: Yes/No

**Services Offered (100+ service lines):**

**Emergency & Trauma:**
- Emergency department
- Trauma center (Level I, II, III)
- Pediatric emergency department

**Cardiac:**
- Cardiac catheterization lab
- Adult diagnostic/interventional cardiac catheterization
- Pediatric diagnostic/interventional cardiac catheterization
- Open-heart surgery
- Adult cardiac surgery
- Pediatric cardiac surgery
- Cardiac electrophysiology
- Cardiac rehabilitation

**Stroke:**
- Primary stroke center certification
- Comprehensive stroke center certification
- Acute stroke ready certification

**Cancer:**
- Oncology services
- Cancer center (NCI-designated, other)
- Radiation therapy
- PET scan
- Stem cell transplant

**Surgery:**
- Robotic surgery
- Bariatric surgery
- Transplant services: Heart, liver, kidney, lung, pancreas, other solid organ

**Imaging:**
- CT scanner
- MRI
- PET scan
- Ultrasound
- Cardiac catheterization
- Angioplasty

**Maternity & Neonatal:**
- Obstetrics services
- Neonatal ICU (levels)
- Neonatal intermediate care
- Genetic counseling
- Fertility services

**Psychiatric & Substance Abuse:**
- Psychiatric emergency services
- Psychiatric inpatient care (adult, child/adolescent, geriatric)
- Psychiatric consultation-liaison
- Psychiatric outpatient services
- Psychiatric partial hospitalization
- Substance abuse services (inpatient, outpatient, residential)

**Rehabilitation:**
- Inpatient rehabilitation facility
- Physical therapy
- Occupational therapy
- Speech-language pathology
- Sports medicine
- Orthopedic services

**Other Services:**
- Home health services
- Hospice services
- Skilled nursing facility (SNF)
- Palliative care program
- Telehealth services (patient, provider consultations)
- Case management
- Patient education center
- Alzheimer's diagnostic center
- Wound care services
- Sleep center
- Pain management
- Women's health center
- And 50+ more...

**Utilization:**
- Total admissions (acute, newborn)
- Inpatient days
- Emergency department visits
- Outpatient visits
- Inpatient surgical operations
- Outpatient surgical operations
- Births
- Average length of stay (days)
- Occupancy rate (%)
- Case mix index (patient severity)

**Staffing:**
- Full-time equivalent (FTE) total employees
- FTE registered nurses
- FTE licensed practical nurses (LPNs)
- FTE nursing assistants
- FTE physicians (including hospitalists)
- FTE residents/interns
- FTE advanced practice registered nurses (NPs, CNSs, CRNAs, CNMs)
- FTE physician assistants
- FTE allied health professionals

**Financial:**
- Total operating revenue ($)
- Total operating expenses ($)
- Net patient revenue ($)
- Net income/loss ($)
- Payroll expenses ($)
- Medicare inpatient days (%)
- Medicaid inpatient days (%)
- Uncompensated care (charity care + bad debt, $)
- Total assets ($)
- Total liabilities ($)
- Capital expenditures ($)

#### Data Access

**Purchase Required:**
- **URL:** https://www.ahadata.com/aha-annual-survey-database
- **Contact:** ahadatainfo@aha.org
- **Cost:** ~$1,000-$3,000 for single-year license (varies: academic, nonprofit, government, commercial pricing)
- **Format:** SAS, SPSS, Stata, CSV
- **License:** Annual purchase; multi-year archives available

**FREE Alternative (Limited Variables):**
- **CMS Hospital Compare / Care Compare**
- **URL:** https://data.cms.gov/provider-data/topics/hospitals
- **Variables:** ~50 variables (subset of AHA): beds, ownership, services, quality measures, patient experience scores
- **Limitation:** No financial data, limited historical data, smaller service line detail

**County-Level Aggregation Example:**
```r
library(tidyverse)

# After purchasing AHA Annual Survey data
aha_2023 <- read_csv("AHA_Annual_Survey_2023.csv")  # or .sas7bdat, .dta

# Key columns:
# ID, MNAME (hospital name), MCRNUM (Medicare #), FCOUNTY (county FIPS),
# MSTATE (state), BDTOT (total beds), ADMTOT (admissions), EDVISITS (ED visits),
# BIRTHS, FTRES (FTE residents), FTEMD (FTE MDs), FTEDTOT (FTE total),
# EXPTOT (operating expenses), NETPATREV (net patient revenue),
# UNCOMP (uncompensated care), TRAUMA (trauma level), STROKECR (stroke center),
# SERV_100+ (100+ service indicator variables: 1=yes, 0=no)

# Aggregate to county level
county_hospitals <- aha_2023 %>%
  group_by(FCOUNTY, MSTATE) %>%
  summarize(
    hospitals = n(),
    total_beds = sum(BDTOT, na.rm = TRUE),
    total_admissions = sum(ADMTOT, na.rm = TRUE),
    total_ed_visits = sum(EDVISITS, na.rm = TRUE),
    hospitals_with_trauma_center = sum(TRAUMA %in% c(1, 2, 3), na.rm = TRUE),
    hospitals_with_stroke_center = sum(STROKECR == 1, na.rm = TRUE),
    hospitals_with_cardiac_cath = sum(SERV_017 == 1, na.rm = TRUE),  # Example service code
    hospitals_with_mri = sum(SERV_045 == 1, na.rm = TRUE),
    total_staff_fte = sum(FTEDTOT, na.rm = TRUE),
    total_rn_fte = sum(FTERN, na.rm = TRUE),
    total_operating_expenses = sum(EXPTOT, na.rm = TRUE),
    total_uncompensated_care = sum(UNCOMP, na.rm = TRUE),
    pct_for_profit = mean(OWNERSHIP == 3, na.rm = TRUE) * 100,  # Ownership code 3 = for-profit
    pct_teaching = mean(TEACHING > 0, na.rm = TRUE) * 100,
    .groups = "drop"
  )

# Calculate hospital market metrics
county_hospital_metrics <- county_hospitals %>%
  left_join(county_population, by = c("FCOUNTY" = "county_fips")) %>%
  mutate(
    beds_per_1000 = (total_beds / population) * 1000,
    admissions_per_1000 = (total_admissions / population) * 1000,
    ed_visits_per_capita = total_ed_visits / population,
    hospital_deserts = hospitals == 0,  # Counties with no hospitals
    trauma_desert = hospitals_with_trauma_center == 0
  )
```

#### Data Quality

**Strengths:**
- LONGEST hospital time series (1946-present, 79 years!)
- MOST comprehensive hospital database (500+ variables)
- High response rate (~80%)
- Service line detail (100+ services)
- Financial data (revenues, expenses, uncompensated care)
- Staffing by profession
- Validated by AHA (annual survey, verified by hospitals)

**Limitations:**
- **COST:** Purchase required ($1,000-$3,000/year)
- Voluntary survey (not regulatory, but high response rate)
- Self-reported data (not independently audited, except financial data for audited hospitals)
- Service availability ≠ service utilization (hospital may offer service but perform few procedures)

**Comparison to CMS Hospital Compare (Free):**
- **AHA:** 500+ variables, financial, staffing, full service detail, 1946-present
- **CMS:** ~50 variables, quality measures, patient experience, limited financials, ~2010-present
- **Use AHA if:** Need historical data, service detail, financial analysis, staffing
- **Use CMS if:** Need quality measures, free access sufficient, basic service info okay

#### Use Cases

1. **Healthcare Access:** Identify hospital deserts (counties with no hospitals)
2. **Service Availability:** Trauma centers, stroke centers, cardiac catheterization labs by county
3. **Health Workforce:** Hospital staffing (RNs, MDs, specialists) by county
4. **Financial Distress:** Hospitals with high uncompensated care, operating losses
5. **Market Concentration:** Hospital ownership, system consolidation trends

**Priority Variables (if purchasing):**
- Number of hospitals per county
- Total beds per 1,000 population
- Trauma center availability (Level I, II, III)
- Stroke center designation
- Cardiac catheterization lab
- Neonatal ICU (Level III/IV)
- Hospital births
- RN FTEs per 1,000 population
- Uncompensated care burden
- % for-profit hospitals

**Note:** If cost is prohibitive, use **free CMS Hospital Compare** as alternative.

---

### Source 11: CMS Nursing Home Compare / Care Compare

**Official Name:** CMS Nursing Home Compare / Care Compare - County-Level Nursing Home Data
**Status:** ✅ COMPREHENSIVE NURSING HOME QUALITY DATA (2009-present, QUARTERLY)

#### Overview

CMS Care Compare (formerly Nursing Home Compare) provides comprehensive quality, staffing, inspection, and COVID-19 data for all Medicare/Medicaid-certified nursing homes in the United States (~15,000 facilities), aggregable to county level.

#### Coverage

- **Geographic:** ~15,000 nursing homes nationally, aggregable to county
- **Temporal:** 2009-present for star ratings (15+ years); earlier data available for some variables
- **Update Frequency:** Quarterly (every 3 months)
- **Certification:** Medicare/Medicaid-certified facilities only (captures >95% of nursing home beds)

#### Variables Available (100+)

**Facility Identification:**
- Facility name, address, city, county, state, ZIP
- Provider ID (CMS Certification Number - CCN)
- Ownership type: For-profit, Non-profit, Government
- Latitude/longitude

**Capacity:**
- Number of certified beds
- Resident census (average daily census, current quarter)
- Occupancy rate (%)

**Five-Star Quality Rating System:**
- **Overall star rating** (1-5 stars, composite)
- **Health inspection star rating** (1-5 stars, deficiency-based)
- **Staffing star rating** (1-5 stars, hours per resident day)
- **Quality measures star rating** (1-5 stars, clinical outcomes)

**Health Inspections:**
- Total number of health deficiencies (current survey cycle)
- Number of severe deficiencies (immediate jeopardy, actual harm)
- Scope and severity of deficiencies (isolated, pattern, widespread)
- Most recent inspection date
- Inspection type: Standard, Complaint, Post-survey revisit
- Number of substantiated complaints
- Fire safety deficiencies

**Staffing (Hours per Resident Day):**
- **Registered Nurse (RN) hours per resident day**
- **Licensed Practical Nurse (LPN) hours per resident day**
- **Certified Nursing Assistant (CNA) hours per resident day**
- **Physical therapist hours per resident day**
- **Total nursing hours per resident day** (RN + LPN + CNA)
- Weekend staffing hours
- RN director turnover (yes/no, within last year)
- Administrator turnover (yes/no, within last year)
- Comparison to state average and national average staffing levels

**Quality Measures (15 measures):**

**Short-Stay (Post-Acute) Residents:**
1. % who self-report moderate to severe pain
2. % with pressure ulcers (bedsores) that are new or worsened
3. % who were assessed and appropriately given seasonal flu vaccine
4. % who were assessed and appropriately given pneumococcal vaccine
5. % who were re-hospitalized after a nursing home admission
6. % who have had an outpatient emergency department visit

**Long-Stay (Chronic) Residents:**
7. % experiencing one or more falls with major injury
8. % with a urinary tract infection (UTI)
9. % who self-report moderate to severe pain
10. % who have symptoms of depression
11. % who were physically restrained
12. % who received an antipsychotic medication (without appropriate diagnosis)
13. % who received an antianxiety or hypnotic medication
14. % with pressure ulcers (stage 2-4)
15. % whose ability to move independently worsened

**Penalties & Enforcement:**
- Civil monetary penalties (fines, $)
- Payment denials (yes/no, dates)
- Special focus facility (SFF) status (targeted for improvement)
- Temporary management
- Medicare/Medicaid termination status

**COVID-19 Data (2020-present):**
- Confirmed COVID-19 cases (residents, cumulative + weekly)
- COVID-19 deaths (residents, cumulative + weekly)
- Confirmed COVID-19 cases (staff, cumulative + weekly)
- COVID-19 deaths (staff, cumulative + weekly)
- N95 mask supply (weeks on hand)
- Ventilator supply (count)
- Shortage of nursing staff (yes/no)
- Shortage of clinical staff (yes/no)
- Shortage of aides (yes/no)
- Shortage of other staff (yes/no)

#### Data Access

**Primary Portal:**
- **URL:** https://data.cms.gov/provider-data/topics/nursing-homes
- **Care Compare Search:** https://www.medicare.gov/care-compare/
- **Format:** CSV downloads (quarterly files), API access

**Bulk Downloads:**
- **Provider Data Catalog:** https://data.cms.gov/provider-data/
- **Nursing Home Datasets:** Multiple files by data type (facility characteristics, health deficiencies, staffing, quality measures, penalties)

**Download Example:**
```r
library(tidyverse)

# Download CMS Nursing Home facility characteristics (Q4 2024)
nh_facilities <- read_csv("NH_ProviderInfo_Q4_2024.csv")

# Key columns:
# Federal_Provider_Number, Provider_Name, Provider_Address, Provider_City,
# Provider_State, Provider_Zip_Code, Provider_County_Name, Ownership_Type,
# Number_of_Certified_Beds, Average_Number_of_Residents_Per_Day,
# Overall_Rating, Health_Inspection_Rating, Staffing_Rating, QM_Rating

# Download staffing data
nh_staffing <- read_csv("NH_Staffing_Q4_2024.csv")

# Download quality measures
nh_quality <- read_csv("NH_QualityMeasures_Q4_2024.csv")

# Download COVID data
nh_covid <- read_csv("NH_COVID_Q4_2024.csv")

# Merge and aggregate to county
nh_merged <- nh_facilities %>%
  left_join(nh_staffing, by = "Federal_Provider_Number") %>%
  left_join(nh_quality, by = "Federal_Provider_Number") %>%
  left_join(nh_covid, by = "Federal_Provider_Number")

# Aggregate to county
county_nursing_homes <- nh_merged %>%
  group_by(Provider_County_Name, Provider_State) %>%
  summarize(
    nursing_homes = n(),
    total_beds = sum(Number_of_Certified_Beds, na.rm = TRUE),
    total_residents = sum(Average_Number_of_Residents_Per_Day, na.rm = TRUE),
    mean_overall_rating = mean(Overall_Rating, na.rm = TRUE),
    pct_5star = mean(Overall_Rating == 5, na.rm = TRUE) * 100,
    pct_1star = mean(Overall_Rating == 1, na.rm = TRUE) * 100,
    mean_rn_hours_per_resident = mean(RN_Hours_per_Resident_Day, na.rm = TRUE),
    mean_total_nurse_hours = mean(Total_Nurse_Staffing_Hours, na.rm = TRUE),
    facilities_below_avg_staffing = sum(Staffing_Rating < 3, na.rm = TRUE),
    facilities_with_severe_deficiencies = sum(Number_of_Severe_Deficiencies > 0, na.rm = TRUE),
    total_covid_resident_cases = sum(Total_Resident_Confirmed_COVID, na.rm = TRUE),
    total_covid_resident_deaths = sum(Total_Resident_COVID_Deaths, na.rm = TRUE),
    pct_for_profit = mean(Ownership_Type == "For profit", na.rm = TRUE) * 100,
    .groups = "drop"
  )

# Calculate county long-term care metrics
county_ltc_metrics <- county_nursing_homes %>%
  left_join(county_population_65plus, by = c("Provider_County_Name", "Provider_State")) %>%
  mutate(
    beds_per_1000_seniors = (total_beds / population_65plus) * 1000,
    nursing_home_deserts = nursing_homes == 0,
    low_quality_county = mean_overall_rating < 3
  )
```

#### Data Quality

**Strengths:**
- Complete coverage of Medicare/Medicaid-certified nursing homes (~15,000 facilities, >95% of US nursing home beds)
- Quarterly updates (high temporal resolution)
- Standardized star ratings (consumer-friendly comparison)
- Clinical outcomes measured (falls, UTIs, pressure ulcers, hospitalizations)
- Staffing hours by profession (RN, LPN, CNA)
- Inspection deficiency detail (scope, severity)
- COVID-19 tracking (cases, deaths, supplies, staffing shortages)
- Official CMS regulatory data

**Limitations:**
- Only certified facilities (excludes ~5% of facilities that are not Medicare/Medicaid-certified)
- Quality measures: Risk-adjusted but subject to gaming (e.g., excluding sicker residents from quality measure reporting)
- Staffing self-reported (payroll-based journal, validated quarterly but subject to inflation)
- Star ratings: Methodology changes over time (difficult to compare ratings across years)
- Small nursing homes: Single deficiency can drastically lower star rating

#### Use Cases

1. **Long-Term Care Access:** Nursing home deserts (counties with no facilities or insufficient beds)
2. **Quality of Care:** Identify counties with predominately low-quality (1-2 star) nursing homes
3. **Staffing Shortages:** Counties with below-average nurse staffing
4. **COVID-19 Impact:** Nursing home COVID deaths by county
5. **Inspection Trends:** Counties with increasing deficiency rates

**Priority Variables:**
- Number of nursing homes per county
- Certified beds per 1,000 seniors (65+)
- Mean overall star rating (county average)
- % of facilities with 1-2 stars (poor quality)
- Mean RN hours per resident day
- Mean total nurse hours per resident day
- % facilities below state average staffing
- Total severe deficiencies
- COVID-19 resident deaths (cumulative)

---

## PART 4: PUBLIC SERVICES

### Source 12: ASARB U.S. Religion Census - Congregations & Adherents

**Official Name:** Association of Statisticians of American Religious Bodies (ASARB) U.S. Religion Census
**Status:** ✅ MOST COMPREHENSIVE RELIGION DATA (Decadal 1952-2020, 372 denominations!)

#### Overview

The U.S. Religion Census is the most comprehensive county-level religious census, documenting congregations and adherents for 372 religious groups across all US counties. Conducted every 10 years (decadal), it provides longitudinal tracking of religious affiliation and diversity.

#### Coverage

- **Geographic:** All 3,143 US counties
- **Temporal:** Decadal since 1990: 1990, 2000, 2010, 2020
- **Historical:** Earlier censuses 1952, 1971, 1980 (less comprehensive)
- **Update Frequency:** Every 10 years (next: 2030)

#### Variables Available (100+)

**Summary Metrics:**
- Total congregations per county (all religious groups)
- Total adherents per county (members + regular attenders)
- Adherents per 1,000 population (adherence rate)
- Number of religious groups present (diversity)
- Unclaimed population (population - adherents)
- % population claiming religious affiliation

**By Religious Tradition (Major Groups):**

**Christian Traditions:**
- **Catholic:** Congregations, adherents
- **Evangelical Protestant:** Congregations, adherents (80+ denominations)
- **Mainline Protestant:** Congregations, adherents (40+ denominations)
- **Orthodox Christian:** Congregations, adherents (multiple jurisdictions)
- **Latter-day Saints (Mormon):** Congregations (wards), adherents
- **Jehovah's Witnesses:** Congregations, adherents

**Specific Denominations (372 total, top 20 by adherents):**

1. **Catholic Church**
2. **Southern Baptist Convention**
3. **United Methodist Church**
4. **Church of Jesus Christ of Latter-day Saints (LDS/Mormon)**
5. **Church of God in Christ (COGIC, Pentecostal)**
6. **Assemblies of God**
7. **Presbyterian Church (USA)**
8. **Lutheran Church - Missouri Synod**
9. **Evangelical Lutheran Church in America (ELCA)**
10. **National Baptist Convention, USA, Inc.**
11. **National Baptist Convention of America**
12. **Episcopal Church**
13. **Churches of Christ**
14. **African Methodist Episcopal Church (AME)**
15. **American Baptist Churches USA**
16. **Christian Churches and Churches of Christ**
17. **Wisconsin Evangelical Lutheran Synod (WELS)**
18. **Seventh-day Adventist Church**
19. **Church of the Nazarene**
20. **United Church of Christ (UCC)**

And 350+ additional groups including:
- Reformed traditions (Reformed Church in America, Christian Reformed, Presbyterian Church in America, etc.)
- Pentecostal denominations (multiple)
- Baptist denominations (50+ separate bodies)
- Methodist denominations (multiple)
- Anabaptist groups (Mennonite, Amish, Brethren)
- Restorationist groups (Disciples of Christ, etc.)
- Holiness churches
- Independent/non-denominational mega churches (largest)

**Non-Christian Traditions:**
- **Jewish:** Congregations by movement (Orthodox, Conservative, Reform, Reconstructionist)
- **Muslim:** Congregations (mosques, Islamic centers)
- **Buddhist:** Temples/centers
- **Hindu:** Temples
- **Baha'i:** Spiritual assemblies
- **Unitarian Universalist:** Congregations
- **Sikh:** Gurdwaras
- **Other religions:** Zoroastrian, Jain, Shinto, etc.

**Religious Diversity Indices:**
- Herfindahl-Hirschman Index (HHI) of religious concentration
- Number of religious families present
- Evangelical:Mainline:Catholic ratio
- Religious pluralism score

#### Data Access

**2020 U.S. Religion Census:**
- **URL:** https://www.usreligioncensus.org
- **Format:** Excel downloads by state, CSV
- **Interactive Map:** County-level visualizations

**ARDA (Association of Religion Data Archives):**
- **URL:** https://www.thearda.com
- **Historical Data:** 1952, 1971, 1980, 1990, 2000, 2010, 2020
- **Format:** SPSS, Stata, SAS, CSV downloads
- **Free Access:** Create account (free), download county files

**Download Example:**
```r
library(tidyverse)

# Download 2020 U.S. Religion Census county data
religion_2020 <- read_csv("US_Religion_Census_2020_County.csv")

# Key columns:
# FIPS, CNTYNAME, STABBR, POP2020, TOTCNG (total congregations),
# TOTADH (total adherents), RATE (adherents per 1,000 pop),
# CATCNG (Catholic congregations), CATADH (Catholic adherents),
# EVCNG (Evangelical Protestant congregations), EVADH (adherents),
# MPCNG (Mainline Protestant congregations), MPADH (adherents),
# ORTHCNG, ORTHADH, LDSCNG, LDSADH, ... (372 denomination variables)

# Calculate religious affiliation metrics
religion_analysis <- religion_2020 %>%
  mutate(
    adherence_rate = (TOTADH / POP2020) * 1000,  # Per 1,000 population
    pct_catholic = (CATADH / TOTADH) * 100,
    pct_evangelical = (EVADH / TOTADH) * 100,
    pct_mainline = (MPADH / TOTADH) * 100,
    pct_unclaimed = ((POP2020 - TOTADH) / POP2020) * 100,
    religious_diversity = 1 - ((pct_catholic/100)^2 + (pct_evangelical/100)^2 + (pct_mainline/100)^2 + (pct_mormon/100)^2)
  )

# Identify denominations present in county
county_denomination_presence <- religion_2020 %>%
  pivot_longer(
    cols = matches("CNT$"),  # All congregation count columns
    names_to = "denomination",
    values_to = "congregations"
  ) %>%
  filter(congregations > 0) %>%
  group_by(FIPS) %>%
  summarize(
    denominations_present = n(),
    .groups = "drop"
  )

# Time series analysis (1990-2020)
religion_1990 <- read_csv("US_Religion_Census_1990_County.csv")
religion_2000 <- read_csv("US_Religion_Census_2000_County.csv")
religion_2010 <- read_csv("US_Religion_Census_2010_County.csv")

religion_trends <- bind_rows(
  religion_1990 %>% mutate(year = 1990),
  religion_2000 %>% mutate(year = 2000),
  religion_2010 %>% mutate(year = 2010),
  religion_2020 %>% mutate(year = 2020)
)

county_religion_change <- religion_trends %>%
  group_by(FIPS) %>%
  arrange(year) %>%
  mutate(
    change_adherence_rate = adherence_rate - lag(adherence_rate),
    change_pct_evangelical = pct_evangelical - lag(pct_evangelical),
    change_pct_catholic = pct_catholic - lag(pct_catholic),
    change_pct_unclaimed = pct_unclaimed - lag(pct_unclaimed)
  ) %>%
  filter(year == 2020) %>%  # Most recent change
  select(FIPS, CNTYNAME, STABBR, change_adherence_rate, change_pct_evangelical, change_pct_catholic, change_pct_unclaimed)
```

#### Data Quality

**Strengths:**
- MOST comprehensive US religion data (372 denominations)
- Complete county coverage (all 3,143 counties)
- Longitudinal data (1952-2020, 68 years across 7 censuses)
- Adherent counts (not just congregations)
- Direct denominational reporting (not surveys)
- Measures religious diversity

**Limitations:**
- Decadal only (every 10 years; not annual)
- Denominational response varies (some groups more complete than others)
- Adherent definitions vary: Some count members only, others include regular attenders
- Non-response: Some congregations/denominations don't participate (estimated 70-80% response rate)
- Independent/non-denominational churches underrepresented (no central reporting)
- Secular population: "Nones" (religiously unaffiliated) are residual (population - adherents), not directly measured

**Comparison to Pew Religious Landscape Study:**
- **Pew:** Survey-based, individual religious affiliation, but NATIONAL/STATE level only (insufficient sample for counties)
- **Religion Census:** Congregation/denomination reporting, county-level, but decadal
- **Complementary:** Use Religion Census for county geography, Pew for detailed belief/practice data

#### Use Cases

1. **Social Capital:** Religious congregations are primary source of social capital in many communities
2. **Health Behaviors:** Religious affiliation correlates with health behaviors (smoking, alcohol, diet)
3. **Political Behavior:** Religious composition predicts voting patterns
4. **Community Services:** Religious congregations provide social services (food banks, addiction recovery, counseling)
5. **Cultural Geography:** Map religious pluralism, Bible Belt, Catholic strongholds, Mormon corridor

**Priority Variables:**
- Total adherents per 1,000 population (adherence rate)
- % population Catholic
- % population Evangelical Protestant
- % population Mainline Protestant
- % population Latter-day Saints (Mormon)
- % population Muslim, Jewish, Hindu, Buddhist (where significant)
- % population unclaimed/unaffiliated
- Number of denominations present (diversity)
- Change in adherence rate 1990-2020

**Note:** This is decadal data (2020, next 2030), not annual.

---

### Source 13: IMLS Public Libraries Survey (PLS)

**Official Name:** Institute of Museum and Library Services (IMLS) Public Libraries Survey
**Status:** ✅ COMPREHENSIVE LIBRARY DATA (1992-2022, 30 years!)

#### Overview

The IMLS Public Libraries Survey collects data from ~9,000 public library systems (~17,000 total service outlets including branches and bookmobiles) covering library collections, usage, programs, staffing, revenues, and expenditures.

#### Coverage

- **Geographic:** ~9,000 public library systems nationally, aggregable to county
- **Temporal:** 1992-2022 (30-year annual time series!)
- **Update Frequency:** Annual (released ~18-24 months after fiscal year)
- **Coverage:** >95% of US population served by public libraries

#### Variables Available (150+)

**Library System Identification:**
- Library name, address, city, county, state, ZIP
- FSCS ID (Federal-State Cooperative System for Public Library Data unique ID)
- FSCS library outlet service area population (population served)
- Locale code (city, suburban, town, rural)
- Service outlets: Number of central libraries, branches, bookmobiles

**Collections:**
- Print materials (books, serials, government documents)
- Total e-books
- Total audiobooks (physical + downloadable)
- Total video materials (physical + downloadable)
- Current print serial subscriptions
- Total collection size (all formats)
- Children's materials (portion of collection)

**Usage & Circulation:**
- Total circulation (all materials)
- Children's circulation
- Adult circulation
- E-book circulation
- Audio circulation (physical + downloadable)
- Video circulation (physical + downloadable)
- Physical item circulation
- Circulation per capita
- Turnover rate (circulation / collection size)
- Collection use rate

**Library Visits & Programs:**
- Total library visits
- Visits per capita
- Public programs (total number)
- Program attendance (total)
- Children's programs (number)
- Children's program attendance
- Young adult programs (number)
- Young adult program attendance
- Adult programs (number)
- Adult program attendance
- Programs for seniors

**Reference & Services:**
- Reference transactions (in-person, phone, email, virtual)
- Registered users (active library card holders)
- Interlibrary loans provided (to other libraries)
- Interlibrary loans received (from other libraries)

**Public Internet Access:**
- Public use internet computers
- Computers per 5,000 population
- Computer uses (sessions)
- Wi-Fi sessions
- Website visits

**Staffing:**
- Total staff (FTE)
- Librarians with ALA-MLS degrees (FTE)
- Other paid staff (FTE)
- Paid staff per 25,000 population

**Operating Hours:**
- Hours open per year (typical outlet)
- Hours open per week (average across all outlets)

**Revenues:**
- Total operating revenue ($)
- Local government revenue ($)
- State government revenue ($)
- Federal government revenue ($)
- Other revenue (gifts, fees, fines, grants) ($)
- Revenue per capita ($)

**Expenditures:**
- Total operating expenditures ($)
- Staff expenditures (salaries + benefits) ($)
- Collection expenditures ($): Print, electronic, other
- Other operating expenditures ($)
- Capital expenditures ($)
- Expenditures per capita ($)

**Service Outlets by Type:**
- Central libraries (main administrative library)
- Branch libraries
- Bookmobiles (mobile libraries)

**Geographic Service Area:**
- Legal basis: Municipal (city), county, multi-jurisdictional, school district, library district, nonprofit association, Native American tribe
- Reported population of legal service area
- Comparison to county population

#### Data Access

**IMLS Public Libraries Survey:**
- **URL:** https://www.imls.gov/research-evaluation/data-collection/public-libraries-survey
- **Data Files:** https://www.imls.gov/research-evaluation/data-collection/public-libraries-survey/explore-pls-data
- **Format:** CSV, SAS, SPSS downloads
- **Search Tool:** https://www.imls.gov/search-compare/

**Download Example:**
```r
library(tidyverse)

# Download IMLS PLS 2022 data
pls_2022 <- read_csv("PLS_FY2022_State_Summary_Administrative_Entity.csv")

# Key columns:
# FSCSKEY (unique ID), LIBNAME, ADDRESS, CITY, COUNTY, ZIP, STABR,
# POPU_LSA (population of legal service area),
# CENTLIB (central libraries), BRANLIB (branches), BKMOB (bookmobiles),
# BKVOL (print volumes), EBOOK (e-books), AUDIO_PH (audio physical), AUDIO_DL (audio downloadable),
# VIDEO_PH (video physical), VIDEO_DL (video downloadable),
# TOTCIR (total circulation), KIDCIRCL (children's circulation), ELMATCIR (electronic circulation),
# VISITS (library visits), TOTPRO (programs), TOTPROAT (program attendance),
# REFERENC (reference transactions), REGBOR (registered borrowers),
# GPTERMS (public internet computer sessions), WIFISESS (Wi-Fi sessions),
# TOTSTAFF (total FTE), LIBRARIA (librarian FTE with MLS), OTHPAID (other paid FTE),
# TOTINCM (total revenue), LOCINCM (local revenue), STINCM (state revenue), FEDINCM (federal revenue),
# TOTOPEXP (total operating expenses), SALARIES (staff expenditures), COLLEXP (collection expenditures)

# Calculate library service metrics
library_analysis <- pls_2022 %>%
  mutate(
    visits_per_capita = VISITS / POPU_LSA,
    circulation_per_capita = TOTCIR / POPU_LSA,
    programs_per_10k = (TOTPRO / POPU_LSA) * 10000,
    computers_per_5k = (GPTERMS / POPU_LSA) * 5000,  # Computers, not sessions
    revenue_per_capita = TOTINCM / POPU_LSA,
    expenditure_per_capita = TOTOPEXP / POPU_LSA,
    pct_revenue_local = (LOCINCM / TOTINCM) * 100,
    pct_ecollection = (EBOOK + AUDIO_DL + VIDEO_DL) / (BKVOL + EBOOK + AUDIO_PH + AUDIO_DL + VIDEO_PH + VIDEO_DL) * 100,
    high_use_library = visits_per_capita > 5,  # >5 visits/person/year
    total_outlets = CENTLIB + BRANLIB + BKMOB
  )

# Aggregate to county (for multi-jurisdiction libraries, use service area population)
county_libraries <- library_analysis %>%
  group_by(COUNTY, STABR) %>%
  summarize(
    library_systems = n(),
    total_outlets = sum(total_outlets, na.rm = TRUE),
    total_visits = sum(VISITS, na.rm = TRUE),
    total_circulation = sum(TOTCIR, na.rm = TRUE),
    total_programs = sum(TOTPRO, na.rm = TRUE),
    total_program_attendance = sum(TOTPROAT, na.rm = TRUE),
    total_computers = sum(GPTERMS, na.rm = TRUE),  # Sessions, actually
    total_revenue = sum(TOTINCM, na.rm = TRUE),
    total_expenditures = sum(TOTOPEXP, na.rm = TRUE),
    population_served = sum(POPU_LSA, na.rm = TRUE),  # May exceed county if multi-county service
    .groups = "drop"
  )

# Time series analysis (1992-2022)
pls_timeseries <- map_dfr(1992:2022, ~read_csv(paste0("PLS_FY", ., ".csv")) %>% mutate(year = .))

library_trends <- pls_timeseries %>%
  group_by(FSCSKEY) %>%
  arrange(year) %>%
  mutate(
    visits_change = (VISITS - lag(VISITS, 5)) / lag(VISITS, 5) * 100,  # 5-year change
    ecollection_growth = EBOOK - lag(EBOOK, 5),  # E-book growth
    circulation_change = (TOTCIR - lag(TOTCIR, 5)) / lag(TOTCIR, 5) * 100
  )

# Digital transformation
digital_shift <- library_trends %>%
  filter(year %in% c(2010, 2022)) %>%
  group_by(FSCSKEY) %>%
  summarize(
    pct_digital_2010 = (EBOOK[year == 2010] + AUDIO_DL[year == 2010] + VIDEO_DL[year == 2010]) / (BKVOL[year == 2010] + EBOOK[year == 2010]) * 100,
    pct_digital_2022 = (EBOOK[year == 2022] + AUDIO_DL[year == 2022] + VIDEO_DL[year == 2022]) / (BKVOL[year == 2022] + EBOOK[year == 2022]) * 100,
    digital_shift = pct_digital_2022 - pct_digital_2010,
    .groups = "drop"
  )
```

#### Data Quality

**Strengths:**
- Complete coverage (~9,000 library systems, >95% of US population)
- Long time series (1992-2022, 30 years!)
- Comprehensive variables (150+): collections, usage, programs, staffing, finance
- Digital vs. physical collections and usage (tracks digital transformation)
- Public internet access (computers, Wi-Fi)
- Collected by state library agencies, compiled by IMLS (verified data)

**Limitations:**
- Library service areas don't always align with county boundaries (multi-jurisdictional libraries serve multiple counties)
- Fiscal year varies by state (July-June, October-September, etc.)
- Bookmobile and branch counting can vary (some systems count, others don't)
- E-resource usage undercounted (simultaneous use licensing makes "circulation" ambiguous)

#### Use Cases

1. **Digital Divide:** Public library internet access in underserved counties
2. **Education:** Library programs, children's services by county
3. **Community Services:** Public meeting spaces, program attendance
4. **Cultural Access:** Collection size, circulation per capita
5. **Public Funding:** Library revenue trends, local vs. state support

**Priority Variables:**
- Number of library outlets per county
- Library visits per capita
- Circulation per capita
- Public programs per 10,000 population
- Public internet computers per 5,000 population
- Wi-Fi sessions (total)
- Revenue per capita
- Expenditure per capita
- % revenue from local government
- E-book and digital collection size

---

## Summary Tables

### Priority Variables to Add (59+ variables)

| Source | Priority Variables | Years |
|--------|-------------------|-------|
| IRS Tax Statistics | AGI, income composition (wages/business/capital), deductions (mortgage, charity), EITC | 1989-2022 (33 years) |
| IRS Migration | Net migration, net AGI gain/loss, top origin/destination counties | 1990-2022 (32 years) |
| Fed Reserve Debt | Total debt, debt-to-income, delinquency rates, credit scores, foreclosures | 1999-2025 (26 years, quarterly!) |
| Census Building Permits | Total units, single-family, multifamily, construction value, permits per capita | 1980-2024 (44 years!) |
| ASARB Religion Census | Adherents per 1,000, % Catholic/Evangelical/Mainline, denominations present | Decadal 1952-2020 |
| Bankruptcy Filings | Total filings, Chapter 7/13, business bankruptcies, filing rate per 1,000 | 2007-present (quarterly) |
| USPTO Patents | Patents by county, patents per 100k, technology sectors, university vs. corporate | 1975-2020 (45 years!) |
| CDC Natality | Preterm birth, low birthweight, prenatal care, maternal health conditions, smoking | 1995-2024 (30 years) |
| CDC COVID Vaccination | % fully vaccinated, % with booster, vaccination by age group | 2020-2025 (weekly!) |
| CDC AtlasPlus | Chlamydia, gonorrhea, syphilis, TB, Hepatitis A/B/C, HIV rates | 1996-present (29 years) |
| AHA Hospitals | Hospital count, beds, services (trauma, stroke, cardiac), staffing, uncompensated care | 1946-present (79 years!) - **PURCHASE** |
| CMS Nursing Homes | Nursing home count, beds, quality ratings, staffing hours, COVID deaths | 2009-present (quarterly) |
| IMLS Libraries | Library outlets, visits per capita, programs, computers, expenditures per capita | 1992-2022 (30 years) |

**Total: ~1,100+ variables across 13 sources**

---

## Data Integration Strategy

### Seamless Integration with Existing Documentation

These 13 sources fill the final gaps in your comprehensive county-level data documentation:

**Economic & Financial:**
- IRS Tax Statistics → Income composition detail
- IRS Migration → Population flows and economic migration
- Fed Reserve Debt → Financial distress indicators
- Bankruptcy Filings → Acute financial crisis
- Building Permits → Housing supply and construction activity

**Innovation:**
- USPTO Patents → Knowledge economy, R&D activity

**Health Facilities & Infectious Disease:**
- CDC Natality → Birth outcomes (extends beyond breastfeeding)
- CDC COVID Vaccination → Pandemic response
- CDC AtlasPlus → STI/TB/Hepatitis surveillance
- AHA Hospitals → Comprehensive hospital characteristics (500+ variables)
- CMS Nursing Homes → Long-term care quality

**Public Services:**
- ASARB Religion Census → Social capital, religious affiliation
- IMLS Libraries → Public library services, digital access

---

## Access & Cost Summary

**FREE ACCESS (12 sources):**
1. IRS Tax Statistics ✓
2. IRS Migration ✓
3. Fed Reserve Debt ✓
4. Census Building Permits ✓
5. ASARB Religion Census ✓
6. Bankruptcy Filings ✓
7. USPTO Patents ✓
8. CDC Natality ✓ (public-use: 524 large counties; restricted-use: all counties via RDC)
9. CDC COVID Vaccination ✓
10. CDC AtlasPlus ✓
11. CMS Nursing Homes ✓
12. IMLS Libraries ✓

**PURCHASE REQUIRED (1 source):**
13. AHA Hospitals ✗ (~$1,000-$3,000/year license)
    - **FREE Alternative:** CMS Hospital Compare (limited variables)

---

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Status:** Production-ready - Final Gap Analysis
**Total Sources:** 13
**Total Variables:** ~1,100+
**Geographic Coverage:** All 3,143 US counties (with noted exceptions)
