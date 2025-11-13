# Nutrition, Tobacco, and Food Environment - Comprehensive County-Level Documentation

## Executive Summary

This documentation covers **additional** county-level data on tobacco use, nutrition behaviors, and food environment infrastructure that complement existing CDC PLACES documentation. These sources provide historical trends, food insecurity subpopulation data, food access infrastructure, and specialty measures not available in other datasets.

### Key Features

- **📊 Food Insecurity**: County estimates by age, race, income (Feeding America)
- **🚬 Historical Smoking**: 1997-2023 trends (NCI Small Area Estimates)
- **🏪 Food Retail Infrastructure**: 250,000+ SNAP retailers, 8,000+ farmers markets (USDA)
- **🍼 Breastfeeding**: County-level initiation rates (birth certificates)
- **🏚️ Food Deserts**: Census tract low-access areas aggregable to county (USDA)
- **🔑 Access**: Free, public data; bulk downloads and APIs available
- **🌎 Geography**: All 3,143 US counties

**Note**: This file complements **CDC_PLACES_COMPREHENSIVE.md** which already documents current smoking, e-cigarette use, fruit/vegetable consumption, physical activity, and obesity at the county level (2019-2024).

---

## Table of Contents

1. [Data Systems & Sources](#data-systems--sources)
2. [NCI Small Area Estimates - Smoking & Physical Activity](#nci-small-area-estimates---smoking--physical-activity)
3. [Feeding America Map the Meal Gap](#feeding-america-map-the-meal-gap)
4. [USDA Food Access Research Atlas](#usda-food-access-research-atlas)
5. [SNAP Retailer Locations](#snap-retailer-locations)
6. [USDA Farmers Market Directory](#usda-farmers-market-directory)
7. [Breastfeeding Initiation Rates](#breastfeeding-initiation-rates)
8. [BRFSS SMART - Selected Counties](#brfss-smart---selected-counties)
9. [County Business Patterns - Restaurant Density](#county-business-patterns---restaurant-density)
10. [State Tobacco Retailer Licensing](#state-tobacco-retailer-licensing)
11. [County-Level Aggregation Strategies](#county-level-aggregation-strategies)
12. [Access Methods & APIs](#access-methods--apis)
13. [R Packages & Code Examples](#r-packages--code-examples)
14. [Data Quality & Limitations](#data-quality--limitations)
15. [Priority Variables for Collection](#priority-variables-for-collection)
16. [Quick Reference](#quick-reference)

---

## Data Systems & Sources

### 1. NCI Small Area Estimates for Smoking & Physical Activity
**Agency:** National Cancer Institute (NIH)
**Coverage:** All 3,143 US counties
**Years:** 1997-2023 (rolling multi-year estimates)
**Update Frequency:** Every 2-3 years
**Restriction:** Public use, no restrictions

### 2. Feeding America Map the Meal Gap
**Agency:** Feeding America (national food bank network)
**Coverage:** All 3,143 US counties + congressional districts
**Years:** 2001-present
**Update Frequency:** Annual (May release with prior year data)
**Restriction:** Public use, free with registration/request

### 3. USDA Food Access Research Atlas
**Agency:** USDA Economic Research Service
**Coverage:** All US census tracts (~73,000 tracts)
**Years:** 2010, 2015, 2019
**Update Frequency:** Every 5 years approximately
**Restriction:** Public use, no restrictions

### 4. SNAP Retailer Locator
**Agency:** USDA Food and Nutrition Service
**Coverage:** All SNAP-authorized retailers (~250,000 locations)
**Years:** 2018-present (snapshots)
**Update Frequency:** Continuously updated
**Restriction:** Public use, no restrictions

### 5. USDA Farmers Market Directory
**Agency:** USDA Agricultural Marketing Service
**Coverage:** All US farmers markets (~8,000 markets)
**Years:** Current + historical
**Update Frequency:** Continuously updated
**Restriction:** Public use, no restrictions

### 6. Birth Certificate Breastfeeding Data
**Agency:** CDC National Vital Statistics System
**Coverage:** All counties (varies by state adoption)
**Years:** 2016-present
**Update Frequency:** Annual
**Restriction:** Public use, suppression for <10 births

### 7. BRFSS SMART
**Agency:** CDC Behavioral Risk Factor Surveillance System
**Coverage:** Selected metropolitan/micropolitan areas (~500 MMSAs)
**Years:** 2003-present
**Update Frequency:** Annual
**Restriction:** Public use, no restrictions

---

## NCI Small Area Estimates - Smoking & Physical Activity

NCI produces model-based county-level estimates for smoking and cancer screening behaviors using multilevel regression and poststratification (MRP) combining NHIS and BRFSS data.

### Geographic & Temporal Coverage

- **Geography:** All 3,143 US counties
- **Years:** Multiple time periods from 1997-2023
  - 1997-1999
  - 2000-2003
  - 2004-2007
  - 2008-2010
  - 2011-2013
  - 2014-2016
  - 2017-2019
  - 2021-2023
- **Estimate Type:** Multi-year rolling averages (increases reliability for small counties)

### Variables Available (~11 outcomes)

#### A. Tobacco Use
- `CURRENT_SMOKER_ALL` - Current smokers, all adults (age-adjusted %)
- `CURRENT_SMOKER_MALE` - Current smokers, males (age-adjusted %)
- `CURRENT_SMOKER_FEMALE` - Current smokers, females (age-adjusted %)
- `EVER_SMOKER_ALL` - Ever smokers, all adults (age-adjusted %)

#### B. Physical Activity
- `PHYSICAL_INACTIVITY_ALL` - No leisure-time physical activity, all adults (age-adjusted %)

#### C. Cancer Screening (also included)
- Mammography (women 50-74)
- Pap test (women 21-65)
- Colorectal cancer screening (adults 50-75)
- HPV vaccination (adolescents)

**Note:** Full list of 11 outcomes available at source website.

### Age Adjustment

All prevalence estimates are **age-adjusted to the 2000 US standard population** to enable valid geographic and temporal comparisons.

### Statistical Methods

- **Model:** Multilevel regression with random effects for counties
- **Data Sources:** National Health Interview Survey (NHIS) + Behavioral Risk Factor Surveillance System (BRFSS)
- **Poststratification:** Adjusts for county-level demographics from Census/ACS
- **Confidence Intervals:** 90% CI provided for all estimates
- **Reliability:** More reliable than direct BRFSS county estimates (which are often unavailable for small counties)

### Key Advantages Over CDC PLACES

1. **Historical time series** - Back to 1997 (CDC PLACES starts 2019)
2. **Sex-specific estimates** - Separate male/female smoking prevalence
3. **Ever smoker** - Not just current, but lifetime smoking exposure
4. **Trend analysis** - 26 years of data enable long-term trend studies

### Data Format

CSV files with county-level estimates:

**Columns:**
- `STATE_FIPS` - State FIPS code (2-digit)
- `COUNTY_FIPS` - County FIPS code (3-digit, state-specific)
- `GEOID` - 5-digit combined FIPS (state + county)
- `COUNTY_NAME` - County name
- `STATE_ABBR` - State abbreviation
- `ESTIMATE` - Prevalence estimate (%)
- `LOWER_CI` - Lower bound 90% confidence interval
- `UPPER_CI` - Upper bound 90% confidence interval
- `TIME_PERIOD` - Multi-year period (e.g., "2017-2019")

---

## Feeding America Map the Meal Gap

**Map the Meal Gap** is the only source providing **county-level food insecurity estimates for subpopulations** (children, seniors, race/ethnicity, income levels).

### Food Insecurity Definition

**Food insecurity** means lack of consistent access to enough food for an active, healthy life. USDA defines three levels:
- **High food security:** No problems or anxiety about food
- **Marginal food security:** Anxiety about food, but little/no change in diet
- **Low food security:** Reduced quality/variety of diet
- **Very low food security:** Disrupted eating patterns, reduced intake

**Map the Meal Gap** measures households classified as low or very low food security.

### County-Level Variables (~20 variables)

#### A. Overall Food Insecurity
- `FOOD_INSECURITY_RATE` - Overall food insecurity rate (%)
- `FOOD_INSECURE_PERSONS` - Number of food insecure individuals
- `FOOD_INSECURE_HOUSEHOLDS` - Number of food insecure households

#### B. Child Food Insecurity
- `CHILD_FOOD_INSECURITY_RATE` - Child (0-17) food insecurity rate (%)
- `FOOD_INSECURE_CHILDREN` - Number of food insecure children

#### C. Senior Food Insecurity
- `SENIOR_FOOD_INSECURITY_RATE` - Senior (60+) food insecurity rate (%)
- `FOOD_INSECURE_SENIORS` - Number of food insecure seniors (60+)

#### D. Food Insecurity by Income Level
- `FI_BELOW_130_FPL_RATE` - Food insecurity rate, households <130% FPL (%)
- `FI_130_TO_185_FPL_RATE` - Food insecurity rate, households 130-185% FPL (%)
- `FI_ABOVE_185_FPL_RATE` - Food insecurity rate, households >185% FPL (%)

#### E. Food Insecurity by Race/Ethnicity
- `FI_WHITE_NON_HISP_RATE` - Food insecurity rate, White non-Hispanic (%)
- `FI_BLACK_NON_HISP_RATE` - Food insecurity rate, Black non-Hispanic (%)
- `FI_HISPANIC_RATE` - Food insecurity rate, Hispanic (%)
- `FI_OTHER_RATE` - Food insecurity rate, other races (%)

#### F. Food Budget Shortfall
- `WEIGHTED_ANNUAL_FOOD_BUDGET_SHORTFALL` - Average annual $ needed per food insecure person to afford adequate food
- `TOTAL_FOOD_BUDGET_SHORTFALL` - Total county food budget shortfall ($)

#### G. Meal Gap
- `MEAL_GAP` - Total meals needed to close food insecurity gap (county total)
- `COST_PER_MEAL` - Average cost per meal in county ($)

#### H. Economic Context
- `MEDIAN_HOUSEHOLD_INCOME` - Median household income ($)
- `UNEMPLOYMENT_RATE` - Unemployment rate (%)
- `POVERTY_RATE` - Poverty rate (%)

### Methodology

**Statistical Model:**
- Proprietary model developed by Feeding America
- Inputs:
  - Current Population Survey Food Security Supplement (CPS-FSS) - national food insecurity data
  - ACS demographic and economic data (county-level)
  - BLS unemployment data (county-level)
  - Housing cost data
  - Food price data (regional)
- Output: County-level food insecurity rates by subpopulation

**Model Validation:**
- Correlated with SNAP participation rates
- Validated against state-level BRFSS food insecurity data where available

### Time Series

- **2001-present:** Annual county estimates
- **Released:** May each year with prior year data (e.g., May 2025 release = 2023 data)
- **Pandemic note:** 2020-2021 estimates show elevated food insecurity; 2022-2023 returning to pre-pandemic trends

### Data Availability

**Access Methods:**
1. **Interactive Map:** https://map.feedingamerica.org/
   - View county-level data visually
   - Export individual county profiles (PDF)

2. **Data Request:** https://www.feedingamerica.org/research/map-the-meal-gap/by-county
   - Excel files available by request (email Feeding America research team)
   - Congressional district data also available

3. **Tableau Public:** Some visualizations published
   - Limited variables, not full dataset

**Request Process:**
- Email: research@feedingamerica.org
- Typically fulfilled within 1-2 business days
- Free for research/educational use
- Attribution required in publications

---

## USDA Food Access Research Atlas

The **Food Access Research Atlas** maps census tracts with low income AND low access to healthy food (commonly called "food deserts").

### Geographic Coverage

- **Unit:** Census tract (~73,000 tracts nationwide)
- **Aggregation:** Can sum/aggregate to county level
- **Years:** 2010, 2015, 2019 (intermittent updates)

### Food Desert Definition

**Low-income tract:**
- Poverty rate ≥20%, OR
- Median family income ≤80% of state/metro area median

**Low-access tract (multiple thresholds):**
- **Urban:** At least 500 people or 33% of population is >0.5 mile OR >1 mile from nearest supermarket/large grocery
- **Rural:** At least 500 people or 33% of population is >10 miles OR >20 miles from nearest supermarket/large grocery

**Supermarket definition:** Store with ≥$2 million in annual sales

### Variables Available (~30 variables per census tract)

#### A. Low-Access Flags
- `LowAccessTract_0.5mile` - Urban tract, low access at 0.5 mile
- `LowAccessTract_1mile` - Urban tract, low access at 1 mile
- `LowAccessTract_10miles` - Rural tract, low access at 10 miles
- `LowAccessTract_20miles` - Rural tract, low access at 20 miles

#### B. Population Counts in Low-Access Areas
- `LALOWI0.5` - Low-income population living >0.5 mile from supermarket
- `LALOWI1` - Low-income population living >1 mile from supermarket
- `LALOWI10` - Low-income population living >10 miles from supermarket
- `LALOWI20` - Low-income population living >20 miles from supermarket

#### C. Subpopulation Counts in Low-Access Areas
- `LATracts_child` - Children in low-access tracts
- `LATracts_senior` - Seniors (65+) in low-access tracts
- `LATracts_SNAP` - SNAP recipients in low-access tracts
- `LATracts_vehicle` - Households without vehicle in low-access tracts

#### D. Vehicle Access
- `TractSNAP` - SNAP households in tract
- `TractWhite` - White population in tract
- `TractBlack` - Black population in tract
- `TractHispanic` - Hispanic population in tract
- `TractAsian` - Asian population in tract
- `TractNativeAm` - Native American population in tract
- `TractMultiracial` - Multiracial population in tract

#### E. Tract Characteristics
- `PovertyRate` - Tract poverty rate (%)
- `MedianFamilyIncome` - Median family income ($)
- `NUMGQTRS` - Number of grocery stores/supermarkets in tract
- `NUMSNAP` - Number of SNAP-authorized stores in tract

### County-Level Aggregation

**Strategy 1: Percent of County Population in Food Deserts**
```
County Food Desert % = (Sum of population in low-access tracts) / (Total county population) * 100
```

**Strategy 2: Absolute Counts**
```
County Food Desert Population = Sum of LALOWI1 across all tracts in county
```

**Strategy 3: Subpopulation Prevalence**
```
Children in Food Deserts = Sum of LATracts_child / Total child population in county
```

---

## SNAP Retailer Locations

USDA authorizes ~250,000 retailers to accept SNAP benefits. Point locations enable calculation of SNAP retailer density and food access metrics.

### Retailer Types (USDA Classification)

- **Supermarket** - Annual sales ≥$2 million with minimum variety (meat, dairy, produce, bread)
- **Supercenter** - Large store with general merchandise + groceries (e.g., Walmart Supercenter, Target Supercenter)
- **Large Grocery Store** - Annual sales $1-2 million
- **Small Grocery Store** - Annual sales $500k-$1 million
- **Medium Grocery Store** - Annual sales $1-2 million
- **Convenience Store** - Annual sales <$500k (limited variety)
- **Combination Grocery/Other** - Mixed-use stores
- **Specialty Food Store** - Bakery, butcher, seafood, produce stand, etc.
- **Farmers Market** - SNAP-authorized farmers markets

### Variables Per Retailer (~15 variables)

- `STORE_NAME` - Retailer name
- `ADDRESS` - Street address
- `ADDRESS2` - Apartment/suite
- `CITY` - City
- `STATE` - State (2-letter abbreviation)
- `ZIP` - ZIP code (5-digit)
- `ZIP4` - ZIP+4
- `LATITUDE` - Latitude (decimal degrees)
- `LONGITUDE` - Longitude (decimal degrees)
- `STORE_TYPE` - Store type classification (see above)
- `AUTHORIZATION_DATE` - Date authorized to accept SNAP
- `WIC_VENDOR` - Also authorized for WIC (Y/N)
- `COUNTY` - County name (if provided)

### County-Level Metrics (Derived)

**Density Measures:**
- SNAP retailers per 1,000 population
- SNAP retailers per square mile
- Supermarkets per 1,000 population
- Convenience stores per 1,000 population

**Food Environment Quality:**
- Ratio of supermarkets to convenience stores (higher = better access to healthy food)
- Percent of SNAP retailers that are supermarkets/large groceries

**Examples:**
- **Healthy food access:** County with 5 supermarkets per 10,000 population
- **Food swamp:** County with 1 supermarket, 20 convenience stores per 10,000 population

---

## USDA Farmers Market Directory

USDA maintains a comprehensive directory of farmers markets with location and operating details.

### Variables Per Market (~25 variables)

#### A. Identification & Location
- `FMID` - Farmers market ID (unique)
- `MARKET_NAME` - Market name
- `WEBSITE` - Website URL
- `FACEBOOK` - Facebook page
- `TWITTER` - Twitter handle
- `YOUTUBE` - YouTube channel
- `OTHERMEDIA` - Other social media

#### B. Address & Coordinates
- `STREET` - Street address
- `CITY` - City
- `COUNTY` - County name
- `STATE` - State
- `ZIP` - ZIP code
- `X` - Longitude
- `Y` - Latitude

#### C. Operating Schedule
- `SEASON1DATE` - Season 1 start/end dates (e.g., "04/01/2024 to 11/30/2024")
- `SEASON1TIME` - Season 1 days/hours (e.g., "Sat: 8:00 AM-12:00 PM")
- `SEASON2DATE` - Season 2 (if year-round or split season)
- `SEASON2TIME` - Season 2 hours

#### D. Products Offered (Binary Flags)
- `ORGANIC` - Organic products available (Y/N)
- `BAKEDGOODS` - Baked goods (Y/N)
- `CHEESE` - Cheese and/or dairy (Y/N)
- `CRAFTS` - Crafts (Y/N)
- `FLOWERS` - Flowers (Y/N)
- `EGGS` - Eggs (Y/N)
- `SEAFOOD` - Seafood (Y/N)
- `HERBS` - Herbs (Y/N)
- `VEGETABLES` - Vegetables (Y/N)
- `HONEY` - Honey (Y/N)
- `JAMS` - Jams/jellies (Y/N)
- `MAPLE` - Maple syrup (Y/N)
- `MEAT` - Meat (Y/N)
- `NURSERY` - Plants/nursery products (Y/N)
- `NUTS` - Nuts (Y/N)
- `PLANTS` - Bedding plants (Y/N)
- `POULTRY` - Poultry (Y/N)
- `PREPARED` - Prepared foods (Y/N)
- `SOAP` - Soap (Y/N)
- `TREES` - Trees (Y/N)
- `WINE` - Wine (Y/N)
- `COFFEE` - Coffee (Y/N)
- `BEANS` - Beans (Y/N)
- `FRUITS` - Fruits (Y/N)
- `GRAINS` - Grains (Y/N)
- `JUICES` - Juices (Y/N)
- `MUSHROOMS` - Mushrooms (Y/N)
- `PETFOOD` - Pet food (Y/N)
- `TOFU` - Tofu (Y/N)
- `WILDHARVESTED` - Wild harvested products (Y/N)

#### E. Payment Methods
- `CREDIT` - Credit cards accepted (Y/N)
- `WIC` - WIC accepted (Y/N)
- `WICCASH` - WIC cash accepted (Y/N)
- `SFMNP` - Senior Farmers Market Nutrition Program coupons accepted (Y/N)
- `SNAP` - SNAP/EBT accepted (Y/N)

### County-Level Metrics (Derived)

- Farmers markets per 10,000 population
- Farmers markets per 100 square miles
- SNAP-accepting farmers markets per 10,000 SNAP recipients
- Farmers markets accepting WIC/SFMNP (senior access)

---

## Breastfeeding Initiation Rates

CDC collects breastfeeding initiation data from birth certificates (revised 2003 standard birth certificate form).

### Coverage & Limitations

**State Adoption of Revised Certificate:**
- **2016:** All 50 states + DC adopted revised certificate with breastfeeding question
- **Earlier years:** Partial adoption (33 states by 2010)

**Question Asked:**
"Is the infant being breastfed?" (checkbox on birth certificate)
- Answered at hospital discharge (typically 1-3 days after birth)

**What Is NOT Captured:**
- **Duration:** How long breastfeeding continues (no follow-up)
- **Exclusivity:** Exclusive breastfeeding vs. mixed feeding
- **Post-discharge:** Breastfeeding initiated after hospital discharge

### County-Level Variable

- `BREASTFEEDING_INITIATION_RATE` - Percent of infants breastfed at all after birth, even briefly (%)

**Numerator:** Births with "breastfeeding" checkbox marked
**Denominator:** All live births

### Data Source

**CDC WONDER Natality Database:**
- URL: https://wonder.cdc.gov/natality.html
- Query system for birth certificate data
- County-level data available

**Suppression:**
- Counties with <10 births with breastfeeding = suppressed
- Very small counties may have missing data

### State & National Benchmarks

**National Rate (2022):** 84.1% initiation
**State Range:** 67% (Louisiana) to 93% (Vermont)

**Healthy People 2030 Target:** 84.6% (national goal)

### Duration & Exclusivity Data (State-Level Only)

**National Immunization Survey-Child (NIS-Child):**
- Provides breastfeeding duration and exclusivity
- **State-level estimates only, NOT county-level**
- Measures:
  - Initiated breastfeeding (ever breastfed)
  - Breastfeeding at 6 months
  - Breastfeeding at 12 months
  - Exclusive breastfeeding through 6 months
- URL: https://www.cdc.gov/breastfeeding-data/survey/results.html

---

## BRFSS SMART - Selected Counties

**BRFSS SMART** (Selected Metropolitan/Micropolitan Area Risk Trends) provides **direct survey estimates** for larger metropolitan and micropolitan statistical areas.

### Geographic Coverage

- **NOT all counties** - Only MMSAs with sufficient sample size
- **Approximately 500 MMSAs** covered (varies by year)
- **Primarily urban/suburban** - Rural counties underrepresented
- **Multi-county MSAs:** Data for MSA as a whole, not individual counties within

### Variables Available (~20+ tobacco/nutrition measures)

**BRFSS SMART includes more detailed measures than CDC PLACES for covered areas.**

#### Tobacco
- Current smoking (every day, some days)
- Smokeless tobacco use
- E-cigarette use (2016+)
- Former smoker status
- Number of cigarettes per day
- Quit attempts in past year
- Smoke-free home policy
- Smoke-free workplace policy

#### Nutrition
- Fruit consumption frequency (times per day)
- Vegetable consumption frequency (times per day)
- Sugar-sweetened beverage consumption (selected years)
- 100% fruit juice consumption

#### Physical Activity
- Minutes of physical activity per week
- Aerobic activity meeting guidelines
- Muscle-strengthening activity

#### Weight
- BMI (calculated)
- Overweight (BMI 25-29.9)
- Obesity (BMI ≥30)
- Severe obesity (BMI ≥40)

### Key Advantage: Direct Survey Estimates

- CDC PLACES uses **model-based estimates** (MRP from BRFSS + ACS)
- BRFSS SMART uses **direct survey responses** from MMSA residents
- Generally more precise for covered areas (lower confidence intervals)

### Limitation: Incomplete Coverage

- **~500 MMSAs covered** out of 3,143 counties
- Small metros and rural counties NOT included
- For comprehensive county coverage, CDC PLACES is better

---

## County Business Patterns - Restaurant Density

**Note:** CBP is already comprehensively documented in **CBP_QCEW_COMPREHENSIVE_DOCUMENTATION.md**. This section focuses specifically on restaurant/food service applications.

### Restaurant NAICS Codes

**Full-Service Restaurants (NAICS 722511):**
- Table service, waitstaff
- Examples: Applebee's, Olive Garden, independent restaurants

**Limited-Service Restaurants (NAICS 722513):**
- Fast food, counter service, no table service
- Examples: McDonald's, Subway, Chipotle

**Cafeterias, Grill Buffets, Buffets (NAICS 722514):**
- Self-service, buffet-style
- Examples: Golden Corral, cafeterias

**Snack and Nonalcoholic Beverage Bars (NAICS 722515):**
- Coffee shops, ice cream parlors, juice bars
- Examples: Starbucks, Dunkin', smoothie bars

### County-Level Variables

**From CBP (annual, 2023 most recent):**
- Number of establishments by NAICS code
- Employment by NAICS code
- Annual payroll by NAICS code
- Establishment size class distribution

**Derived Metrics:**
- Fast food density (722513 establishments per 10,000 population)
- Full-service restaurant density (722511 per 10,000 population)
- Fast food to full-service ratio (food swamp indicator)
- Restaurant employment per capita

**Food Swamp Definition (Research):**
- High ratio of fast food/convenience stores to supermarkets/full-service restaurants
- No official federal designation; research-defined
- Example threshold: >5:1 ratio of unhealthy to healthy food outlets

---

## State Tobacco Retailer Licensing

**Important Note:** There is **NO centralized federal database** of tobacco retailers. Data must be obtained from individual state licensing agencies.

### State Variability

**States with Strong Licensing:**
- California: Retailers of Tobacco Products (RTP) database, publicly accessible
- New York: ~19,420 tobacco retailers licensed, public dataset
- Virginia, Ohio, Massachusetts: County-level data published in research

**States with Weak/No Licensing:**
- Some states do not require state-level tobacco retail licenses
- Others require licenses but do not publish retailer lists

### Example: California RTP Database

**Variables per Retailer:**
- Business name
- DBA (doing business as) name
- Address (street, city, ZIP)
- County
- License number
- License type (Cigarette/Tobacco Products Retailer, Wholesaler)
- License status (Active, Expired, Revoked)
- Effective date

**County-Level Aggregation:**
- Count active licenses by county
- Calculate retailer density (per 10,000 population, per square mile)
- Map clustering of tobacco retailers near schools (research application)

### Research Applications

**Stanford Research Into the Impact of Tobacco Advertising (RITA):**
- Multi-state database of ~300,000 tobacco retailers
- Research access only (not public bulk download)
- Used for studying tobacco retailer density and health outcomes

**Tobacco Control Journal Publications:**
- Many studies have acquired state data via FOIA and published county-level analyses
- Example: "Tobacco retail density and smoking prevalence in US counties" studies

---

## County-Level Aggregation Strategies

### Strategy 1: Tract-Level to County (Food Access Atlas)

**Steps:**
1. Download census tract data from USDA Food Access Research Atlas
2. Load county-tract crosswalk (FIPS code first 5 digits = county)
3. Aggregate population counts to county:
   - Sum low-access population across all tracts in county
   - Calculate % of county population in low-access tracts

**Example:**
```r
# Load Food Access Atlas tract data
food_access <- read_csv("food_access_research_atlas.csv")

# Calculate county aggregates
county_food_access <- food_access %>%
  mutate(county_fips = substr(CensusTract, 1, 5)) %>%
  group_by(county_fips, State) %>%
  summarise(
    total_pop = sum(POP2010),
    low_access_pop_1mile = sum(LALOWI1, na.rm = TRUE),
    low_access_pop_10miles = sum(LALOWI10, na.rm = TRUE),
    pct_low_access_1mile = (low_access_pop_1mile / total_pop) * 100,
    pct_low_access_10miles = (low_access_pop_10miles / total_pop) * 100
  )
```

---

### Strategy 2: Point Locations to County (SNAP Retailers, Farmers Markets)

**Steps:**
1. Download point location data (lat/lon)
2. Spatial join to county boundaries OR use provided county field
3. Count locations per county
4. Calculate density (locations per population or per area)

**Example:**
```r
library(sf)
library(tigris)

# Load SNAP retailer data
snap_retailers <- read_csv("snap_retailer_locations.csv")

# Convert to spatial object
snap_sf <- st_as_sf(snap_retailers,
                    coords = c("LONGITUDE", "LATITUDE"),
                    crs = 4326)

# Load county boundaries
counties <- counties(cb = TRUE, year = 2023)

# Spatial join
retailers_by_county <- snap_sf %>%
  st_join(counties) %>%
  st_drop_geometry() %>%
  count(GEOID, STORE_TYPE, name = "count")

# Pivot to wide format
retailers_wide <- retailers_by_county %>%
  pivot_wider(names_from = STORE_TYPE, values_from = count, values_fill = 0) %>%
  rename_with(~paste0("snap_", tolower(gsub(" ", "_", .x))), -GEOID)

# Calculate density
library(tidycensus)
pop <- get_acs(geography = "county", variables = "B01003_001", year = 2023) %>%
  select(GEOID, population = estimate)

retailers_density <- retailers_wide %>%
  left_join(pop, by = "GEOID") %>%
  mutate(
    supermarkets_per_10k = (snap_supermarket / population) * 10000,
    convenience_per_10k = (snap_convenience_store / population) * 10000,
    supermarket_ratio = snap_supermarket / (snap_supermarket + snap_convenience_store)
  )
```

---

### Strategy 3: Multi-Year Averaging (Small Counties)

For counties with small populations, single-year estimates may be unstable. Average across multiple years.

**Example: Breastfeeding Initiation**
```r
# Load 5 years of birth data
births_2018_2022 <- bind_rows(
  read_csv("births_2018.csv"),
  read_csv("births_2019.csv"),
  read_csv("births_2020.csv"),
  read_csv("births_2021.csv"),
  read_csv("births_2022.csv")
)

# Calculate 5-year average
bf_5year <- births_2018_2022 %>%
  group_by(county_fips) %>%
  summarise(
    total_births = sum(total_births),
    breastfeeding_births = sum(breastfeeding_births),
    bf_initiation_rate_5yr = (breastfeeding_births / total_births) * 100
  ) %>%
  filter(total_births >= 50)  # Reliability threshold
```

---

## Access Methods & APIs

### 1. NCI Small Area Estimates

**Website:** https://sae.cancer.gov/nhis-brfss/estimates/

**Access:**
- Direct download: CSV files by time period
- No API
- No registration required

**File Structure:**
- Separate files for each outcome (current smoking, physical inactivity, etc.)
- Each file contains all counties, all time periods

**Example Download:**
```r
# Current smoking estimates
url <- "https://sae.cancer.gov/nhis-brfss/estimates/current-smoking/allcounties_smoking.csv"
smoking_county <- read_csv(url)
```

---

### 2. Feeding America Map the Meal Gap

**Website:** https://www.feedingamerica.org/research/map-the-meal-gap/by-county

**Access:**
- Email request: research@feedingamerica.org
- Specify year(s) needed
- Provide brief description of research/project
- Free for research/educational use

**Turnaround:** 1-2 business days

**Format:** Excel files with county-level data

---

### 3. USDA Food Access Research Atlas

**Website:** https://www.ers.usda.gov/data-products/food-access-research-atlas/

**Access:**
- Interactive map: https://www.ers.usda.gov/data-products/food-access-research-atlas/go-to-the-atlas
- Bulk download: https://www.ers.usda.gov/data-products/food-access-research-atlas/download-the-data
- CSV files, Excel files
- No API

**Files:**
- Census tract-level data (1 row per tract)
- Data dictionary included

---

### 4. SNAP Retailer Locator

**Website:** https://www.fns.usda.gov/snap/retailer-locator

**Access Methods:**

**A. Interactive Locator:**
- Search by address, city, ZIP
- Returns nearest retailers

**B. Bulk Download:**
- Data.gov catalog: https://catalog.data.gov/dataset/snap-retail-locator
- CSV file: ~250,000 rows
- Updated quarterly

**C. API:**
- ArcGIS REST API
- Base URL: `https://services.arcgis.com/VTyQ9soqVukalItT/arcgis/rest/services/`
- Endpoint: `SNAP_Store_Locations/FeatureServer/0/query`
- No API key required

**Example API Query:**
```
GET https://services.arcgis.com/VTyQ9soqVukalItT/arcgis/rest/services/SNAP_Store_Locations/FeatureServer/0/query?where=STATE='CA'&outFields=*&f=json
```

---

### 5. USDA Farmers Market Directory

**Website:** https://www.ams.usda.gov/local-food-directories/farmersmarkets

**Access:**

**A. Interactive Directory:**
- Search by ZIP, city, state
- Filter by products, payment methods

**B. Bulk Download:**
- Data.gov: https://catalog.data.gov/dataset/farmers-markets-directory-and-geographic-data
- CSV export available
- ~8,000 markets

**C. API:**
- USDA AMS Local Food Directories API
- Documentation: https://www.ams.usda.gov/about-ams/programs-offices/public-affairs/internet/open-data
- RESTful API

---

### 6. Birth Certificate Breastfeeding Data

**Website:** https://wonder.cdc.gov/natality.html

**Access:**
- CDC WONDER Natality query system
- Web interface only (no bulk download, no API)
- Query builder allows selection of:
  - Years
  - Geography (states, counties)
  - Demographics (maternal age, race, education, etc.)
  - Breastfeeding (checkbox)

**Query Steps:**
1. Select "Natality for 2016-2023" (latest years with breastfeeding data)
2. Group results by: County
3. Select measures: Births
4. Additional measures: Breastfeeding
5. Run query
6. Export results (text, CSV, PDF)

**Suppression:** Cells with <10 births suppressed

---

### 7. BRFSS SMART

**Website:** https://www.cdc.gov/brfss/brfssprevalence/index.html

**Access:**
- Interactive query system
- Select year, MMSA, variable
- Download results as CSV
- No bulk API

**Data Files:**
- Annual BRFSS datasets include MMSA identifiers
- Can analyze raw data for SMART areas
- URL: https://www.cdc.gov/brfss/annual_data/annual_data.htm

---

## R Packages & Code Examples

### 1. Load NCI Small Area Estimates

```r
library(tidyverse)

# Download current smoking estimates (2021-2023)
url_smoking <- "https://sae.cancer.gov/nhis-brfss/estimates/current-smoking/allcounties_smoking_2021_2023.csv"
smoking <- read_csv(url_smoking)

# Clean
smoking_clean <- smoking %>%
  mutate(
    county_fips = paste0(str_pad(state_fips, 2, "0"), str_pad(county_fips, 3, "0"))
  ) %>%
  select(
    county_fips, state_abbr, county_name,
    smoking_rate = estimate,
    smoking_lower_ci = lower_ci,
    smoking_upper_ci = upper_ci,
    time_period
  )

# Compare to earlier period for trends
url_smoking_2017 <- "https://sae.cancer.gov/nhis-brfss/estimates/current-smoking/allcounties_smoking_2017_2019.csv"
smoking_2017 <- read_csv(url_smoking_2017)

# Calculate change
smoking_trend <- smoking_clean %>%
  left_join(
    smoking_2017 %>%
      mutate(county_fips = paste0(str_pad(state_fips, 2, "0"), str_pad(county_fips, 3, "0"))) %>%
      select(county_fips, smoking_rate_2017 = estimate),
    by = "county_fips"
  ) %>%
  mutate(
    smoking_change = smoking_rate - smoking_rate_2017,
    pct_change = ((smoking_rate - smoking_rate_2017) / smoking_rate_2017) * 100
  )
```

---

### 2. Process Feeding America Data

```r
# Assume Excel file received from Feeding America
library(readxl)

# Load Map the Meal Gap data
mmg_2023 <- read_excel("Map_the_Meal_Gap_2023.xlsx", sheet = "County")

# Clean and standardize
food_insecurity <- mmg_2023 %>%
  mutate(
    county_fips = str_pad(`FIPS Code`, 5, "0")
  ) %>%
  select(
    county_fips,
    state = State,
    county = County,
    overall_fi_rate = `Overall Food Insecurity Rate (%)`,
    child_fi_rate = `Child Food Insecurity Rate (%)`,
    senior_fi_rate = `Senior Food Insecurity Rate (%)`,
    food_insecure_persons = `Food Insecure Persons`,
    cost_per_meal = `Cost per Meal ($)`,
    food_budget_shortfall = `Weighted Annual Food Budget Shortfall ($)`
  ) %>%
  mutate(across(overall_fi_rate:food_budget_shortfall, as.numeric))

# Calculate food insecurity prevalence relative to poverty
poverty <- get_acs(geography = "county", variables = "B17001_002", year = 2023) %>%
  select(county_fips = GEOID, poverty_pop = estimate)

fi_with_context <- food_insecurity %>%
  left_join(poverty, by = "county_fips") %>%
  mutate(
    fi_rate_poverty_ratio = overall_fi_rate / (poverty_pop / total_pop * 100)
  )
```

---

### 3. Aggregate Food Access Atlas to County

```r
# Load USDA Food Access Research Atlas (2019)
food_access_tracts <- read_csv("FoodAccessResearchAtlasData2019.csv")

# Aggregate to county
county_food_access <- food_access_tracts %>%
  mutate(county_fips = substr(CensusTract, 1, 5)) %>%
  group_by(county_fips, State) %>%
  summarise(
    total_pop = sum(POP2010),
    # Urban low access (>1 mile from supermarket)
    urban_low_access_pop = sum(LALOWI1, na.rm = TRUE),
    urban_low_access_pct = (urban_low_access_pop / total_pop) * 100,
    # Rural low access (>10 miles)
    rural_low_access_pop = sum(LALOWI10, na.rm = TRUE),
    rural_low_access_pct = (rural_low_access_pop / total_pop) * 100,
    # No vehicle households in low access
    no_vehicle_low_access = sum(LATracts_vehicle, na.rm = TRUE),
    # SNAP recipients in low access
    snap_low_access = sum(LATracts_SNAP, na.rm = TRUE),
    # Children in low access
    children_low_access = sum(LATracts_child, na.rm = TRUE),
    # Seniors in low access
    seniors_low_access = sum(LATracts_senior, na.rm = TRUE),
    .groups = "drop"
  )
```

---

### 4. SNAP Retailer Density

```r
library(sf)
library(tigris)
library(tidycensus)

# Download SNAP retailer data
snap_url <- "https://usda-fns.opendata.arcgis.com/datasets/snap-retailer-locator/FeatureServer/0/query?outFields=*&where=1%3D1&f=geojson"
snap_retailers <- st_read(snap_url)

# Load county boundaries
counties <- counties(cb = TRUE, year = 2023)

# Spatial join
snap_by_county <- snap_retailers %>%
  st_join(counties) %>%
  st_drop_geometry() %>%
  count(GEOID, STORE_TYPE, name = "count")

# Pivot wider
snap_wide <- snap_by_county %>%
  pivot_wider(names_from = STORE_TYPE, values_from = count, values_fill = 0,
              names_prefix = "snap_")

# Get population
pop <- get_acs(geography = "county", variables = "B01003_001", year = 2023) %>%
  select(GEOID, population = estimate)

# Calculate density and ratios
snap_density <- snap_wide %>%
  left_join(pop, by = "GEOID") %>%
  mutate(
    supermarket_per_10k = (snap_Supermarket / population) * 10000,
    convenience_per_10k = (`snap_Convenience Store` / population) * 10000,
    total_retailers_per_10k = (rowSums(select(., starts_with("snap_"))) / population) * 10000,
    healthy_ratio = snap_Supermarket / (snap_Supermarket + `snap_Convenience Store`)
  )
```

---

### 5. Farmers Market Density

```r
# Download farmers market data
fm_url <- "https://www.ams.usda.gov/sites/default/files/media/National%20Farmers%20Market%20Directory.csv"
farmers_markets <- read_csv(fm_url)

# Clean and aggregate to county
fm_by_county <- farmers_markets %>%
  filter(!is.na(x), !is.na(y)) %>%  # Remove missing coordinates
  # Create spatial object
  st_as_sf(coords = c("x", "y"), crs = 4326) %>%
  # Spatial join to counties
  st_join(counties) %>%
  st_drop_geometry() %>%
  # Count by county
  group_by(GEOID, NAME) %>%
  summarise(
    farmers_markets = n(),
    snap_accepting = sum(SNAP == "Y", na.rm = TRUE),
    wic_accepting = sum(WIC == "Y", na.rm = TRUE),
    organic_available = sum(Organic == "Y", na.rm = TRUE),
    .groups = "drop"
  )

# Calculate density
fm_density <- fm_by_county %>%
  left_join(pop, by = "GEOID") %>%
  mutate(
    fm_per_10k = (farmers_markets / population) * 10000,
    snap_fm_per_10k = (snap_accepting / population) * 10000
  )
```

---

### 6. Breastfeeding Data from CDC WONDER

**Note:** CDC WONDER does not have an API. Must use web interface and manual download.

**Steps:**
1. Go to https://wonder.cdc.gov/natality.html
2. Select "Natality for 2016-2023"
3. Group Results By: County
4. Select measures: Births, Breastfeeding
5. Run Query
6. Export as text file

**Process Exported Data:**
```r
# Read CDC WONDER export (tab-delimited)
bf_data <- read_tsv("wonder_breastfeeding_export.txt", skip = 1) %>%
  filter(Notes == "Total")  # Remove suppressed/unreliable

# Clean
breastfeeding <- bf_data %>%
  select(
    county = County,
    county_code = `County Code`,
    births = Births,
    breastfeeding_births = `Breastfeeding`
  ) %>%
  mutate(
    county_fips = str_pad(county_code, 5, "0"),
    bf_initiation_rate = (breastfeeding_births / births) * 100
  ) %>%
  filter(!is.na(bf_initiation_rate))
```

---

## Data Quality & Limitations

### NCI Small Area Estimates

**Strengths:**
- Model-based estimates more stable than direct BRFSS county estimates
- Historical time series (1997-2023)
- All counties covered

**Limitations:**
- Multi-year rolling averages (not single-year)
- Model assumptions may not hold for all counties
- Confidence intervals wide for very small counties
- Age-adjusted estimates (not crude prevalence)

---

### Feeding America Map the Meal Gap

**Strengths:**
- Only source for county food insecurity by subpopulation
- Annual updates
- Validated against SNAP participation and BRFSS state data

**Limitations:**
- **Proprietary model** (methodology not fully transparent)
- Model-based estimates, not direct measurement
- Subpopulation estimates have larger uncertainty than overall estimates
- Does not directly measure food access, only economic food insecurity

---

### USDA Food Access Research Atlas

**Strengths:**
- Based on actual distance calculations to supermarkets
- Multiple distance thresholds (0.5, 1, 10, 20 miles)
- Census tract detail allows flexible aggregation

**Limitations:**
- **Infrequent updates** (2010, 2015, 2019; no 2024 update yet)
- Supermarket locations from 2019 may be outdated (store closures/openings)
- Distance measure only (does not account for transportation barriers, store quality, prices)
- "Supermarket" definition excludes some ethnic groceries, small healthy food stores

---

### SNAP Retailer Locator

**Strengths:**
- Comprehensive (all authorized retailers)
- Point locations allow flexible analysis
- Updated continuously

**Limitations:**
- **Authorized to accept SNAP ≠ actually accepts SNAP** (some small retailers rarely process SNAP)
- Store type classification may be inconsistent (e.g., small grocery vs. convenience)
- Does not indicate product availability or quality
- Large retailers (Walmart) may be classified as "Supercenter" even if limited grocery selection

---

### Farmers Market Directory

**Strengths:**
- Most comprehensive farmers market listing
- Operating schedule and product detail
- SNAP/WIC acceptance flags

**Limitations:**
- **Self-reported data** by market managers (may be outdated)
- Seasonal operation (not year-round food access)
- Does not indicate market size, vendor count, or product volume
- Geographic coordinates may be approximate

---

### Birth Certificate Breastfeeding

**Strengths:**
- Population-based (all births)
- County-level available
- Consistent data collection (revised certificate standard)

**Limitations:**
- **Initiation ONLY** (no duration, exclusivity)
- Hospital discharge data (does not capture post-discharge initiation)
- Subject to recall bias
- Suppression for small counties (<10 births)
- Does not capture breastfeeding support, maternal intention, or barriers

---

### BRFSS SMART

**Strengths:**
- Direct survey estimates (not modeled)
- More detailed questions than CDC PLACES
- Larger sample sizes for covered areas

**Limitations:**
- **Incomplete geographic coverage** (~500 MMSAs, not all 3,143 counties)
- Rural areas underrepresented
- Self-reported data (social desirability bias)
- Response rates declining over time (50-60% in recent years)

---

## Priority Variables for Collection

### Tier 1: High Priority - Unique County-Level Data

1. **Food insecurity by subpopulation** (Feeding America)
   - Overall food insecurity rate
   - Child food insecurity rate
   - Senior food insecurity rate
   - Food insecurity by race/ethnicity

2. **Historical smoking trends** (NCI Small Area Estimates)
   - Current smoking 1997-2023
   - Male/female smoking prevalence
   - Ever smoker prevalence

3. **SNAP retailer density** (USDA SNAP Locator)
   - Supermarkets per 10,000 population
   - Convenience stores per 10,000 population
   - Supermarket to convenience store ratio

4. **Breastfeeding initiation** (birth certificates)
   - % infants breastfed at birth

### Tier 2: Medium Priority - Complements Existing Data

5. **Food desert population** (Food Access Atlas)
   - % population in low-access tracts
   - Children in low-access areas
   - SNAP recipients in low-access areas

6. **Farmers market density** (USDA AMS)
   - Farmers markets per 10,000 population
   - SNAP-accepting farmers markets

7. **Restaurant density by type** (CBP - already documented)
   - Fast food restaurants per capita
   - Full-service restaurants per capita

### Tier 3: Lower Priority - Limited Coverage or Redundant

8. **BRFSS SMART** (selected MMSAs only)
   - Detailed tobacco/nutrition for ~500 areas
   - Redundant with CDC PLACES for most variables

9. **Tobacco retailer density** (state-specific)
   - Only available for select states
   - No federal database

---

## Quick Reference

### Key URLs

| Source | URL |
|--------|-----|
| **NCI Small Area Estimates** | https://sae.cancer.gov/nhis-brfss/estimates/ |
| **Feeding America Map the Meal Gap** | https://www.feedingamerica.org/research/map-the-meal-gap/by-county |
| **USDA Food Access Atlas** | https://www.ers.usda.gov/data-products/food-access-research-atlas/ |
| **SNAP Retailer Locator** | https://www.fns.usda.gov/snap/retailer-locator |
| **Farmers Market Directory** | https://www.ams.usda.gov/local-food-directories/farmersmarkets |
| **CDC WONDER Natality** | https://wonder.cdc.gov/natality.html |
| **BRFSS SMART** | https://www.cdc.gov/brfss/brfssprevalence/index.html |
| **County Business Patterns** | https://www.census.gov/programs-surveys/cbp.html |

### Key R Packages

| Package | Purpose |
|---------|---------|
| `tidyverse` | Data manipulation |
| `sf` | Spatial operations |
| `tigris` | County shapefiles |
| `tidycensus` | Population data |
| `readxl` | Read Feeding America Excel files |

### Contact Information

**NCI Small Area Estimates:**
- Email: NCISAEHelp@mail.nih.gov

**Feeding America:**
- Email: research@feedingamerica.org

**USDA ERS (Food Access Atlas):**
- Email: ers@usda.gov

**USDA FNS (SNAP Retailers):**
- Website: https://www.fns.usda.gov/contacts

---

## Changelog

**Version 1.0 (2025-11-12)**
- Initial comprehensive documentation
- Focus on NEW sources not covered in CDC_PLACES_COMPREHENSIVE.md
- Feeding America Map the Meal Gap documented (20 variables)
- NCI Small Area Estimates documented (11 outcomes, 1997-2023)
- SNAP Retailer Locator documented (point data)
- Farmers Market Directory documented (8,000+ markets)
- Birth certificate breastfeeding documented (initiation only)
- USDA Food Access Research Atlas documented (30+ tract-level variables)
- BRFSS SMART documented (selected MMSAs)

---

## Citation

When using these data sources, cite appropriately:

**NCI Small Area Estimates:**
```
Dwyer-Lindgren L, et al. Cigarette smoking prevalence in US counties: 1996–2012.
Population Health Metrics. 2014; 12:5. DOI: 10.1186/1478-7954-12-5

National Cancer Institute. Small Area Estimates for Cancer Risk Factors & Screening Behaviors.
https://sae.cancer.gov/nhis-brfss/
```

**Feeding America:**
```
Feeding America. Map the Meal Gap [Year]: County-level Food Insecurity Estimates.
https://www.feedingamerica.org/research/map-the-meal-gap
```

**USDA Food Access Research Atlas:**
```
U.S. Department of Agriculture, Economic Research Service. Food Access Research Atlas, [Year].
https://www.ers.usda.gov/data-products/food-access-research-atlas/
```

**SNAP Retailer Locator:**
```
U.S. Department of Agriculture, Food and Nutrition Service. SNAP Retailer Locator, [accessed date].
https://www.fns.usda.gov/snap/retailer-locator
```

**Birth Certificate Breastfeeding:**
```
Centers for Disease Control and Prevention, National Center for Health Statistics.
Natality public-use data [Year]. CDC WONDER. https://wonder.cdc.gov/natality.html
```

---

**Document Status:** ✅ Complete
**Last Updated:** November 12, 2025
**Complements:** CDC_PLACES_COMPREHENSIVE.md (for current smoking, e-cigarettes, fruit/vegetable consumption, physical activity)
**Next Update:** As new data sources or major revisions occur
