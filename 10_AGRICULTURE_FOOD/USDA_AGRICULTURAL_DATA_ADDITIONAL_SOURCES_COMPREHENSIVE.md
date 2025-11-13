# USDA AGRICULTURAL DATA - ADDITIONAL SOURCES BEYOND CENSUS & QUICK STATS
## Comprehensive County-Level Research Report

**Last Updated**: November 12, 2025
**Research Focus**: County-level agricultural data BEYOND USDA Census of Agriculture and NASS Quick Stats
**Geographic Coverage**: 3,143 US Counties
**Status**: Comprehensive review completed

---

## EXECUTIVE SUMMARY

This report identifies **additional** county-level agricultural data sources beyond the already-documented USDA Census of Agriculture (quinquennial, 6,000+ variables) and USDA NASS Quick Stats (annual/quarterly, 10,000+ variables).

### Key Findings:

**TRUE ADDITIONS (New County-Level Data):**
1. **USDA Risk Management Agency (RMA)** - Crop insurance data by county annually (1948-present)
2. **USDA Farm Service Agency (FSA)** - Conservation Reserve Program enrollment by county
3. **USDA NRCS** - Conservation practices and financial assistance by county (FY 2005-2024)
4. **Bureau of Economic Analysis (BEA)** - Farm income as part of county personal income (annual, 1969-present)
5. **USDA NASS Cash Rents Survey** - County-level farmland rental rates (annual, 2008-present)
6. **USDA Organic Integrity Database** - Certified organic operations by location (searchable)
7. **USGS Water Use Data** - Agricultural water withdrawal by county (quinquennial, 2000-2020)

**ALREADY CAPTURED IN QUICK STATS/CENSUS:**
- Crop Production reports (county data in Quick Stats)
- Livestock inventories (county data in Quick Stats and Census)
- Milk production (state-level only, not county)
- Egg production (Census has county data; monthly surveys are state-level)
- Specialty crops surveys (county data in Quick Stats where available)
- Agricultural prices received (state/national only, not county-level)
- Farm labor (regional/state only, not county-level)

**NOT AVAILABLE AT COUNTY LEVEL:**
- Livestock Slaughter (state-level only)
- ARMS survey data (national/state only, not county)
- Most NASS monthly/quarterly surveys (state-level, with county data only for major commodities in Quick Stats)

---

## TABLE OF CONTENTS

1. [TRUE ADDITIONS - New County Data Sources](#1-true-additions---new-county-data-sources)
2. [ALREADY DOCUMENTED - Census/Quick Stats Coverage](#2-already-documented---censusquick-stats-coverage)
3. [STATE/REGIONAL ONLY - No County Data](#3-stateregional-only---no-county-data)
4. [Detailed Source Documentation](#4-detailed-source-documentation)
5. [Data Access Methods](#5-data-access-methods)
6. [Priority Variables for Collection](#6-priority-variables-for-collection)
7. [Quick Reference](#7-quick-reference)

---

## 1. TRUE ADDITIONS - NEW COUNTY DATA SOURCES

These sources provide county-level agricultural data NOT fully captured in the Census of Agriculture or NASS Quick Stats.

### 1.1 USDA Risk Management Agency (RMA) - Crop Insurance Data

**Source**: Summary of Business Reports
**Agency**: USDA Risk Management Agency
**Status**: ✅ TRUE ADDITION - Annual county insurance data not in Census/Quick Stats

#### Geographic & Temporal Coverage
- **Geography**: All counties with crop insurance activity (~2,900+ counties)
- **Years**: 1948-2024 (historical archive available)
- **Frequency**: Annual crop year summaries; updated continuously during crop year
- **Access**: Free, public download

#### Variables Available (~20+ per county per crop)

**By County and Crop:**
- `POLICIES_SOLD` - Number of crop insurance policies
- `POLICIES_EARNING_PREMIUM` - Policies active during crop year
- `POLICIES_INDEMNIFIED` - Policies with loss payments
- `NET_PLANTED_ACRES` - Insured acres planted
- `NET_ENDORSED_ACRES` - Total insured acres
- `LIABILITY` - Total insured value of crops ($)
- `TOTAL_PREMIUM` - Total insurance premium ($)
- `SUBSIDY` - Federal subsidy portion ($)
- `FARMER_PAID_PREMIUM` - Producer-paid portion ($)
- `INDEMNITY` - Total loss payments made ($)
- `LOSS_RATIO` - Indemnity/Premium ratio (%)
- `NET_FARMER_BENEFIT` - (Indemnity - Farmer Premium)

**Crop Coverage**: 120+ insured commodities including:
- Major field crops (corn, soybeans, wheat, cotton, rice, sorghum, etc.)
- Specialty crops (vegetables, fruits, nuts)
- Forage and grazing land
- Nursery crops
- Organic crops

#### Why This is a TRUE ADDITION
- **Census of Agriculture** includes only whether farm HAS crop insurance (yes/no), total premium paid
- **Quick Stats** does NOT include crop insurance data
- **RMA data** provides detailed annual losses, indemnities, acres insured BY CROP BY COUNTY

#### Access Methods
**URL**: https://www.rma.usda.gov/SummaryOfBusiness/StateCountyCrop
**Format**: ZIP files with pipe-delimited text files
**Update**: Annually, with monthly updates during crop year
**API**: Report Generator available at https://public-rma.fpac.usda.gov/apps/SummaryOfBusiness

#### Data Quality
- **Source**: Administrative records from all crop insurance policies
- **Coverage**: ~89% of major field crop acreage insured (2024)
- **Reliability**: Complete administrative data, no sampling error
- **Suppression**: Some counties suppressed if <3 policies to protect confidentiality

---

### 1.2 USDA Farm Service Agency (FSA) - Conservation Reserve Program (CRP)

**Source**: CRP Statistics
**Agency**: USDA Farm Service Agency
**Status**: ✅ TRUE ADDITION - Detailed CRP enrollment not in Census

#### Geographic & Temporal Coverage
- **Geography**: All counties (physical location of contracted land)
- **Years**: 1986-2024 (CRP program inception to present)
- **Frequency**: Annual; monthly enrollment reports
- **Access**: Free, public download

#### Variables Available (~15 per county)

**CRP Enrollment by County:**
- `CRP_CONTRACTS` - Number of active CRP contracts
- `CRP_FARMS` - Number of farms with CRP contracts
- `CRP_ACRES_ENROLLED` - Total CRP acres under contract
- `GENERAL_CRP_ACRES` - General signup acres
- `CONTINUOUS_CRP_ACRES` - Continuous signup acres
- `GRASSLAND_CRP_ACRES` - Grassland CRP acres
- `CREP_ACRES` - Conservation Reserve Enhancement Program acres
- `AVERAGE_ANNUAL_RENTAL_PAYMENT` - Annual rental rate ($/acre)
- `TOTAL_ANNUAL_RENTAL_PAYMENTS` - Total county rental payments ($)
- `SOIL_RENTAL_RATE` - County average soil rental rate ($/acre)
- `FARMABLE_WETLAND_ACRES` - Wetland restoration acres
- `CP_PRACTICE_CODES` - Specific conservation practices by acres

**CRP Practice Types** (50+ practices tracked):
- Grass planting
- Tree planting
- Wildlife habitat
- Wetland restoration
- Riparian buffers
- Filter strips
- Pollinator habitat
- etc.

#### Why This is a TRUE ADDITION
- **Census of Agriculture** asks only about "enrolled in CRP" (yes/no) and total CRP acres
- **FSA data** provides detailed breakdowns by CRP type, practice, payment amounts, annual tracking

#### Access Methods
**URL**: https://www.fsa.usda.gov/programs-and-services/conservation-programs/reports-and-statistics/conservation-reserve-program-statistics
**Format**: Excel files, county-level tables
**Update**: Monthly summary reports; annual detailed reports
**Contact**: FSA Information Center

#### Data Quality
- **Source**: Administrative records from CRP contracts
- **Coverage**: All enrolled CRP land (24.7M acres nationally as of 2024)
- **Reliability**: Complete enrollment data, no sampling error
- **Suppression**: Minimal; most counties report data

---

### 1.3 USDA Natural Resources Conservation Service (NRCS) - Conservation Practices

**Source**: RCA Data Viewer / Financial Assistance Programs
**Agency**: USDA Natural Resources Conservation Service
**Status**: ✅ TRUE ADDITION - Detailed conservation practice application by county

#### Geographic & Temporal Coverage
- **Geography**: All counties
- **Years**:
  - Practice data: FY 2005-2024
  - Financial assistance: FY 2014-2024
  - Easements: FY 1998-2024
- **Frequency**: Annual (fiscal year)
- **Access**: Free, public download and interactive viewer

#### Variables Available (~100+ conservation practices tracked)

**Financial Assistance by County (FY 2014-2024):**
- `CONTRACTS_SIGNED` - Number of NRCS conservation contracts
- `DOLLARS_OBLIGATED` - Total financial assistance obligated ($)
- `HISTORICALLY_UNDERSERVED_CONTRACTS` - Contracts with underserved farmers
- `EQIP_CONTRACTS` - Environmental Quality Incentives Program contracts
- `CSP_CONTRACTS` - Conservation Stewardship Program contracts
- `ACEP_EASEMENTS` - Agricultural Conservation Easement Program
- `RCPP_PROJECTS` - Regional Conservation Partnership Program

**Conservation Practices Applied (FY 2005-2024):**
- `PRACTICE_CODE` - NRCS practice code (e.g., 328 = Conservation Crop Rotation)
- `PRACTICE_COUNT` - Number of times practice applied in county
- `PRACTICE_ACRES` - Acres treated with practice
- `PRACTICE_LINEAR_FEET` - For linear practices (buffers, terraces)
- `PRACTICE_UNITS` - For counted practices (ponds, wells, etc.)

**Major Practice Categories** (170+ specific practices):
- Crop management (no-till, cover crops, crop rotation)
- Grazing management (prescribed grazing, fencing)
- Soil health (nutrient management, residue management)
- Water management (irrigation efficiency, watering facilities)
- Wildlife habitat (habitat restoration, pollinator habitat)
- Water quality (filter strips, grassed waterways, buffers)
- Energy conservation (renewable energy systems)
- Forestry (tree planting, forest stand improvement)

**Easement Data (FY 1998-2024):**
- `EASEMENTS_CLOSED` - Number of conservation easements
- `EASEMENT_ACRES` - Total acres under easement
- `WETLAND_EASEMENTS` - Wetland Reserve Program easements
- `AGRICULTURAL_LAND_EASEMENTS` - Farmland protection easements

#### Why This is a TRUE ADDITION
- **Census of Agriculture** asks about conservation practices adopted but not detailed practice-by-practice or NRCS program participation levels
- **NRCS data** provides detailed application of specific conservation practices, program enrollment, financial assistance amounts BY FISCAL YEAR

#### Access Methods
**URL**: https://www.nrcs.usda.gov/resources/data-and-reports/rca-data-viewer
**Downloads**: https://www.nrcs.usda.gov/rca-data-downloads
**Format**: Interactive data viewer with download to Excel
**API**: Direct data queries available
**Contact**: RCA@usda.gov

#### Data Quality
- **Source**: Administrative records from NRCS program contracts
- **Coverage**: All NRCS-assisted conservation activities
- **Reliability**: Complete program data
- **Note**: Only captures conservation practices implemented through NRCS programs, not all conservation adoption

---

### 1.4 Bureau of Economic Analysis (BEA) - Farm Income & Earnings

**Source**: Regional Economic Accounts - Personal Income by County
**Agency**: U.S. Department of Commerce, Bureau of Economic Analysis
**Status**: ✅ TRUE ADDITION - Annual time series of farm income by county

#### Geographic & Temporal Coverage
- **Geography**: All 3,143 counties
- **Years**: 1969-2024 (55-year time series)
- **Frequency**: Annual
- **Access**: Free, public download

#### Variables Available (~10 farm-related per county)

**Farm Income Components:**
- `FARM_EARNINGS` - Net earnings from farm proprietors
- `FARM_PROPRIETORS_INCOME` - Net farm proprietor income ($)
- `NONFARM_PROPRIETORS_INCOME` - For comparison
- `TOTAL_PERSONAL_INCOME` - County total (farm is subset)
- `PER_CAPITA_PERSONAL_INCOME` - Including farm income
- `FARM_INCOME_SHARE` - % of county income from farming

**Income Sources:**
- Net earnings by place of work
- Farm proprietors' income (net)
- Contributions for government social insurance
- Residence adjustment

#### Why This is a TRUE ADDITION
- **Census of Agriculture** provides farm income only quinquennially
- **USDA ERS** provides state-level farm income, not county
- **BEA data** provides ANNUAL county-level time series (1969-present) with farm income as component of personal income

#### Comparison to Census/NASS
- Census: Detailed farm sales, expenses, net income (every 5 years)
- BEA: Net farm proprietors' income annually (continuously)
- **BEA fills inter-census years** with annual estimates

#### Access Methods
**URL**: https://www.bea.gov/data/income-saving/personal-income-county-metro-and-other-areas
**Interactive Tool**: https://apps.bea.gov/itable/?ReqID=70&step=1
**Format**: Excel, CSV downloads; API available
**Update**: Annual (released November for prior year)
**API**: BEA API for programmatic access

#### Data Quality
- **Source**: Incorporates USDA farm statistics, tax records, administrative data
- **Method**: Statistical modeling between Census years
- **Reliability**: High for aggregate farm income; less detail than Census
- **Note**: Farm income defined differently than USDA (uses BEA national accounts definitions)

---

### 1.5 USDA NASS - Cash Rents by County

**Source**: Cash Rents Survey
**Agency**: USDA National Agricultural Statistics Service
**Status**: ✅ TRUE ADDITION - Annual county rental rates not in Census

#### Geographic & Temporal Coverage
- **Geography**: All counties with 20,000+ acres cropland + pasture (~2,000+ counties)
- **Years**: 2008-2024 (annual survey established 2008)
- **Frequency**: Annual (released August)
- **Access**: Free via Quick Stats database

#### Variables Available (~6 per county)

**Rental Rates:**
- `RENT_CROPLAND_IRRIGATED` - Cash rent for irrigated cropland ($/acre)
- `RENT_CROPLAND_NONIRRIGATED` - Cash rent for non-irrigated cropland ($/acre)
- `RENT_PASTURE` - Cash rent for pasture land ($/acre)

**For Each Rental Rate:**
- Mean rental rate ($/acre)
- Standard error
- Coefficient of variation

#### Why This is a TRUE ADDITION
- **Census of Agriculture** asks about rented/leased land but not specific rental rates
- **NASS Cash Rents Survey** provides ANNUAL county-specific rental rates for cropland and pasture

#### Access Methods
**URL**: Access via Quick Stats at https://quickstats.nass.usda.gov/
**Query**: Select Program = "Survey", Commodity = "Rent", Geographic Level = "County"
**Format**: CSV download from Quick Stats
**Report**: Annual Land Values and Cash Rents report

#### Data Quality
- **Source**: Annual survey of farm operators
- **Sample**: Representative sample of farms in each county
- **Mandate**: 2008 Farm Bill required county-level rental rate estimates
- **Suppression**: Some counties suppressed if insufficient sample
- **Reliability**: Based on survey methodology, subject to sampling error

---

### 1.6 USDA Organic Integrity Database

**Source**: Organic INTEGRITY Database
**Agency**: USDA Agricultural Marketing Service (AMS)
**Status**: ✅ TRUE ADDITION - Operation-level location data, aggregable to county

#### Geographic & Temporal Coverage
- **Geography**: All organic operations (searchable by location: address, city, county, state, zip)
- **Years**: Current + historical annual snapshots
- **Frequency**: Continuously updated; annual historical snapshots
- **Access**: Free, public searchable database

#### Variables Available (per operation, aggregable to county)

**Operation Information:**
- `OPERATION_NAME` - Certified organic operation name
- `LOCATION` - Address, city, county, state, zip code
- `CERTIFICATION_STATUS` - Certified, suspended, surrendered, revoked
- `CERTIFYING_AGENT` - Certifying organization
- `OPERATION_TYPE` - Crop, livestock, wild crop, handler/processor
- `SCOPE_CATEGORIES` - Specific categories certified for

**Organic Categories:**
- Crops (specific crops listed)
- Livestock (cattle, poultry, hogs, etc.)
- Wild crops
- Handling/processing

**Aggregable to County:**
- Number of certified organic operations
- Operations by type (crop, livestock, handler)
- Operations by certification status

#### Why This is a TRUE ADDITION
- **Census of Agriculture** provides county totals of organic farms, acres, sales
- **Organic Integrity Database** provides CURRENT, continuously updated list of ALL certified operations with exact locations, allowing real-time county aggregation and tracking of entries/exits

#### Access Methods
**URL**: https://organic.ams.usda.gov/integrity/
**Search**: By location, operation name, certifying agent, products
**Download**: Historical annual lists available
**Format**: Searchable web interface; downloadable CSV
**API**: Data available through Ag Data Commons

#### Data Quality
- **Source**: Administrative records from USDA-accredited certifying agents
- **Coverage**: All USDA-certified organic operations (required by law)
- **Reliability**: Complete administrative database
- **Update**: Continuously updated as certifications granted/revoked

---

### 1.7 USGS - Water Use Data (Agricultural/Irrigation)

**Source**: Water Use in the United States
**Agency**: U.S. Geological Survey
**Status**: ✅ TRUE ADDITION - Detailed agricultural water withdrawal data

#### Geographic & Temporal Coverage
- **Geography**: All counties (also available by HUC watershed)
- **Years**: 1950-2020 (quinquennial: 1950, 1955, ..., 2015, 2020)
- **Frequency**: Every 5 years
- **Access**: Free, public download

#### Variables Available (~20 per county for irrigation)

**Irrigation Water Use:**
- `IRRIGATION_TOTAL_WITHDRAWALS` - Total irrigation withdrawals (Mgal/day)
- `IRRIGATION_GROUNDWATER_WITHDRAWALS` - From groundwater (Mgal/day)
- `IRRIGATION_SURFACE_WATER_WITHDRAWALS` - From surface water (Mgal/day)
- `IRRIGATION_ACRES` - Irrigated acres in county
- `IRRIGATION_WATER_USE_PER_ACRE` - Application rate (gallons/day/acre)

**By Irrigation Type (where available):**
- Sprinkler irrigation
- Microirrigation (drip/trickle)
- Surface irrigation (flood, furrow)

**Other Agricultural Water Use:**
- `LIVESTOCK_TOTAL_WITHDRAWALS` - Water for livestock (Mgal/day)
- `AQUACULTURE_TOTAL_WITHDRAWALS` - Water for aquaculture (Mgal/day)

**Advanced Products (2000-2020):**
- Monthly irrigation withdrawals by HUC12 watershed
- Consumptive use estimates
- Evapotranspiration (ET) estimates
- Irrigation efficiency by crop

#### Why This is a TRUE ADDITION
- **Census of Agriculture** includes irrigated acres, irrigation methods, water sources
- **USGS Water Use** provides estimated WATER VOLUMES withdrawn for irrigation by county, plus livestock and aquaculture water use
- Different metrics: Census = infrastructure/practices; USGS = actual water volume consumed

#### Access Methods
**URL**: https://www.usgs.gov/mission-areas/water-resources/science/water-use-united-states
**Data Portal**: https://waterdata.usgs.gov/nwis/wu
**Format**: Downloadable datasets, interactive maps
**Advanced**: HUC12 monthly reanalysis (2000-2020) at ScienceBase

#### Data Quality
- **Source**: State water agencies, USDA data, modeling
- **Method**: Compilation + modeling (not direct measurement for all sites)
- **Reliability**: Best available national estimates; accuracy varies by state
- **Note**: 2020 is most recent; 2025 compilation expected ~2027

---

## 2. ALREADY DOCUMENTED - CENSUS/QUICK STATS COVERAGE

These data are **ALREADY CAPTURED** in the documented USDA Census of Agriculture and/or NASS Quick Stats. They are listed here for reference to confirm they do not need separate documentation.

### 2.1 NASS Crop Production Reports (Monthly/Annual)

**Status**: ❌ ALREADY IN QUICK STATS

**What They Contain:**
- Monthly Crop Production reports for major crops
- Acres planted, harvested
- Yield per acre
- Total production

**Geographic Level:**
- National and state-level in monthly reports
- **County-level data available in Quick Stats database** for major crops
- County estimates reinstated for 2024 crop season (corn, cotton, peanuts, rice, sorghum, soybeans)

**Why Already Documented:**
- Quick Stats database aggregates all NASS survey data including county-level crop production
- Census of Agriculture provides quinquennial county crop production
- **Recommendation**: Access via Quick Stats for annual/inter-census years

---

### 2.2 NASS Livestock Inventories

**Status**: ❌ ALREADY IN QUICK STATS & CENSUS

**What They Contain:**
- Cattle and calves inventory (Jan 1, July 1)
- Hogs and pigs inventory (quarterly)
- Sheep and lambs inventory
- Poultry inventory

**Geographic Level:**
- State-level for most commodities in regular surveys
- **County-level available in Quick Stats** for:
  - All cattle inventory (annual)
  - Beef cows (annual)
  - Milk cows (annual)

**Why Already Documented:**
- Quick Stats includes county-level livestock inventory data
- Census of Agriculture provides comprehensive quinquennial county livestock data
- **Recommendation**: Use Census for comprehensive coverage; Quick Stats for annual major livestock

---

### 2.3 NASS Milk Production

**Status**: ❌ ALREADY IN CENSUS (State-level only for monthly surveys)

**What It Contains:**
- Monthly milk production
- Number of milk cows
- Milk per cow

**Geographic Level:**
- **State-level** for monthly Milk Production reports (24 major states)
- **County-level** in Census of Agriculture (quinquennial)

**Why Already Documented:**
- Census of Agriculture includes county milk production
- Monthly surveys are state-level only, not county
- **No additional county-level data available** beyond Census

---

### 2.4 NASS Egg Production & Poultry

**Status**: ❌ ALREADY IN CENSUS (State-level only for monthly surveys)

**What It Contains:**
- Chickens and Eggs survey (monthly)
- Number of layers, egg production
- Turkey production
- Broiler production

**Geographic Level:**
- **State-level** for monthly surveys
- **County-level** in Census of Agriculture (quinquennial)

**Why Already Documented:**
- Census of Agriculture includes county-level poultry and egg data
- Monthly surveys are state-level only
- **No additional county-level data available** beyond Census

---

### 2.5 NASS Specialty Crops Surveys (Fruits, Vegetables, Nuts)

**Status**: ❌ ALREADY IN QUICK STATS & CENSUS

**What They Contain:**
- Fruit surveys (apples, citrus, grapes, berries, etc.)
- Nut surveys (almonds, walnuts, pecans, etc.)
- Vegetable surveys (potatoes, tomatoes, lettuce, etc.)

**Geographic Level:**
- State-level for most specialty crop surveys
- **County-level available in Quick Stats** for major producing counties
- **County-level in Census** (quinquennial)

**Why Already Documented:**
- Quick Stats database includes county data where available
- Census provides comprehensive quinquennial coverage
- **Recommendation**: Query Quick Stats for specific specialty crop county data

---

### 2.6 NASS Agricultural Prices Received

**Status**: ❌ NOT COUNTY-LEVEL (State/National only)

**What It Contains:**
- Monthly prices received by farmers
- ~65 commodities (livestock, crops, dairy, poultry)
- Prices paid indexes

**Geographic Level:**
- **State and national level ONLY**
- **No county-level prices available**

**Why Not a County Source:**
- NASS does not publish county-level agricultural prices
- State-level is the finest geographic detail available

---

### 2.7 NASS Land Values (State-Level)

**Status**: ⚠️ PARTIALLY IN CENSUS; Cash Rents = TRUE ADDITION (see 1.5)

**What It Contains:**
- Farm real estate values ($/acre)
- Cropland values
- Pasture values
- **Cash rental rates** (county-level via Cash Rents Survey - see Section 1.5)

**Geographic Level:**
- **State-level** for land values
- **County-level** for cash rental rates (2008-present)

**Why Partially Documented:**
- Land values are state-level only
- Cash rental rates by county are a TRUE ADDITION (documented in 1.5)
- Census includes estimated market value of land/buildings by farm, aggregated to county

---

### 2.8 NASS Aquaculture (Census of Aquaculture)

**Status**: ❌ ALREADY IN CENSUS

**What It Contains:**
- 2023 Census of Aquaculture (conducted with 2022 Ag Census)
- Catfish, trout, other aquaculture sales
- Acres/facilities by type

**Geographic Level:**
- **State-level** for regular Catfish Production and Trout Production reports
- **County-level** in Census of Aquaculture (most recent: 2023)

**Why Already Documented:**
- Census of Aquaculture is part of Agricultural Census documentation
- Regular surveys are state-level
- **No additional county data** beyond quinquennial Census

---

### 2.9 NASS Honey Bee Colonies and Honey Production

**Status**: ❌ ALREADY IN CENSUS (State-level for annual surveys)

**What It Contains:**
- Honey bee colonies (annual)
- Honey production (annual)
- Colony losses, stressors

**Geographic Level:**
- **State-level** for annual Honey Bee Colonies report
- **County-level** in Census of Agriculture (quinquennial)

**Why Already Documented:**
- Census includes county-level bee and honey data
- Annual surveys are state-level only

---

### 2.10 NASS Maple Syrup Production

**Status**: ❌ ALREADY IN CENSUS (State-level for annual estimates)

**What It Contains:**
- Maple syrup production
- Number of taps
- Production per tap

**Geographic Level:**
- **State-level** only for annual estimates
- Limited county data (if any)

**Why Already Documented:**
- Census of Agriculture may include county data in forest products
- Annual surveys are state-level

---

### 2.11 NASS Crop Progress & Condition

**Status**: ⚠️ STATE-LEVEL REPORTS; Gridded County Data Available

**What It Contains:**
- Weekly crop progress (planting, development, harvest)
- Crop condition ratings (excellent, good, fair, poor, very poor)

**Geographic Level:**
- **State-level** in weekly reports
- **Agricultural Statistics District** level for some states
- **County-level confidential** - NASS publishes gridded synthetic representations

**Available County Products:**
- Crop Progress Gridded Layers (synthetic county data for corn, soybeans, cotton, winter wheat)
- Accessible via Quick Stats for some geographies

**Why Partially Documented:**
- Quick Stats may include some county-level crop condition data
- Weekly reports are primarily state-level
- Not true county-level public data (gridded representations)

---

### 2.12 NASS Crop Values

**Status**: ❌ ALREADY IN QUICK STATS & CENSUS

**What It Contains:**
- Annual Crop Values report
- Production value by crop
- Calculated as Production × Price

**Geographic Level:**
- **State-level** in Crop Values report
- **County-level derivable** from Quick Stats: County Production × State Price

**Why Already Documented:**
- Quick Stats includes county production data
- Census includes sales by commodity
- State prices can be applied to county production for estimates

---

### 2.13 USDA Food Access Research Atlas

**Status**: ❌ ALREADY DOCUMENTED in NUTRITION_TOBACCO_FOOD_ENVIRONMENT_COMPREHENSIVE.md

**What It Contains:**
- Food deserts (low-income, low-access areas)
- Census tract level, aggregable to county

**Why Already Documented:**
- Documented in your existing food environment file
- Not agricultural production data (food access/retail)

---

### 2.14 SNAP Retailer Locations & Farmers Markets

**Status**: ❌ ALREADY DOCUMENTED in NUTRITION_TOBACCO_FOOD_ENVIRONMENT_COMPREHENSIVE.md

**What They Contain:**
- SNAP-authorized retailers (USDA FNS)
- USDA Farmers Market Directory

**Why Already Documented:**
- Documented in your existing food environment file
- Related to food retail/access, not farm production

---

## 3. STATE/REGIONAL ONLY - NO COUNTY DATA

These sources do **NOT provide county-level data**. They are documented here to clarify that they should NOT be pursued for county-level collection.

### 3.1 USDA ERS Farm Income and Wealth Statistics

**Status**: ❌ STATE-LEVEL ONLY

**Geographic Coverage**: National and state-level ONLY
**Why Not County**: ERS explicitly states "State-level are the most geographically disaggregated estimates produced by USDA, Economic Research Service"
**Alternative**: BEA provides county-level farm income (see Section 1.4)

---

### 3.2 USDA NASS Livestock Slaughter

**Status**: ❌ STATE-LEVEL ONLY

**Geographic Coverage**: State, regional, and national only
**Why Not County**: Livestock slaughter is reported from federally inspected plants, aggregated to state level
**Note**: Census includes livestock sold by county, but not slaughter by county

---

### 3.3 USDA NASS Agricultural Prices Received

**Status**: ❌ STATE/NATIONAL ONLY

**Geographic Coverage**: State and national prices
**Why Not County**: NASS does not publish county-level price data
**Note**: Prices are market-based, not location-of-production specific

---

### 3.4 USDA NASS Farm Labor

**Status**: ❌ REGIONAL/STATE ONLY

**Geographic Coverage**: 15 multi-state labor regions plus CA, FL, HI individually
**Why Not County**: Farm Labor survey provides regional/state estimates only
**H-2A Data**: National and state-level H-2A program statistics (not county)

---

### 3.5 USDA ERS Agricultural Resource Management Survey (ARMS)

**Status**: ❌ NATIONAL/STATE ONLY

**Geographic Coverage**: National; 15 major states individually
**Why Not County**: ARMS is a sample survey designed for national/state estimates, not county
**Note**: Crop Reporting Districts (groups of counties) are sampling units, but data not published at that level

---

### 3.6 USDA AMS Agricultural Marketing Service - Prices

**Status**: ❌ MARKET/REGIONAL, NOT COUNTY

**Geographic Coverage**: Terminal markets, shipping points (not county of origin)
**What Available**: Local food directories (farmers markets, food hubs) - location-based but not county production data
**Why Not County**: Price reporting by market location, not farm/county origin

---

### 3.7 USDA APHIS Veterinary Services - Animal Disease Surveillance

**Status**: ❌ STATE-LEVEL or EVENT-SPECIFIC (Not Routine County Data)

**Geographic Coverage**: State-level surveillance; outbreak-specific county reporting
**Why Not County**: Routine disease surveillance reported at state level
**CEAH Reports**: Epidemiological reports are state/national, not routine county data
**Note**: In disease outbreaks, affected counties may be identified, but this is not regular data collection

---

### 3.8 State Departments of Agriculture - Variable County Data

**Status**: ⚠️ VARIES BY STATE

**Geographic Coverage**: Some states publish county data more detailed than NASS
**Examples**:
- Some states provide county livestock estimates beyond NASS
- Some states provide county crop estimates for additional crops
- Most data eventually flows into NASS Quick Stats through cooperative agreements

**Why Not Systematically Documented**:
- **Highly variable** across states
- Most county data from state ag departments is **cooperative NASS data** already in Quick Stats
- No standardized national state-level county database beyond NASS

**Recommendation**:
- For specific states of interest, check state department of agriculture websites
- Nebraska, Kansas, Iowa, California, Texas have robust state ag statistics programs
- But this is not a separate national county data source

---

## 4. DETAILED SOURCE DOCUMENTATION

This section provides complete documentation for each TRUE ADDITION source.

---

### SOURCE 1: USDA RISK MANAGEMENT AGENCY (RMA) - CROP INSURANCE

**Official Name**: Summary of Business Reports
**Agency**: USDA Risk Management Agency (RMA)
**Program**: Federal Crop Insurance Program

#### 1. Geographic Coverage
- **County-Level**: Yes (all counties with insured crops, ~2,900+ counties)
- **Coverage Years**: 1948-2024 (76 years of historical data)
- **Update Frequency**:
  - Annual summary files (crop year basis)
  - Monthly updates during active crop year
  - Final data typically available 12-18 months after crop year

#### 2. Variables Available

**Total Variables**: ~20 variables × 120+ crops × 2,900+ counties = 6,000,000+ data points annually

**Core Insurance Variables (per county per crop):**

| Variable | Description | Units |
|----------|-------------|-------|
| Policies Sold | Number of policies sold | Count |
| Policies Earning Premium | Policies active during year | Count |
| Policies Indemnified | Policies receiving loss payments | Count |
| Net Planted Acres | Insured acres planted | Acres |
| Net Endorsed Acres | Total insured acres | Acres |
| Liability | Total insured value | Dollars |
| Total Premium | Total insurance premium | Dollars |
| Subsidy | Federal subsidy portion | Dollars |
| Producer Premium | Farmer-paid portion | Dollars |
| Indemnity | Total loss payments | Dollars |
| Loss Ratio | Indemnity ÷ Premium | Percent |
| Net Farmer Benefit | Indemnity - Producer Premium | Dollars |

**Crop Coverage**: 120+ commodities including:
- All major field crops (corn, soybeans, wheat, cotton, rice, sorghum, barley, oats, etc.)
- Specialty crops (vegetables, fruits, nuts, nursery)
- Forage and hay
- Livestock (dairy, beef, swine, poultry)
- Pasture, rangeland, forage (PRF)

#### 3. Frequency of Release
- **Crop Year Basis**: Data released by crop year (e.g., 2024 crop year)
- **Monthly Updates**: Sales and contract data updated monthly during crop year
- **Final Data**: Available 12-18 months post-crop year
- **Historical Archive**: Back to 1948

#### 4. Access Methods

**Website Download**:
- URL: https://www.rma.usda.gov/SummaryOfBusiness/StateCountyCrop
- Format: ZIP files containing pipe-delimited text files (|)
- Files organized by crop year
- State/County/Crop level detail

**Report Generator**:
- URL: https://public-rma.fpac.usda.gov/apps/SummaryOfBusiness
- Interactive query tool
- Custom reports by commodity, state, county, year
- Export to Excel, CSV, PDF

**Bulk Download**:
- Annual state/county/crop files
- National summary files
- Historical archives

**No API**: Direct API not available; bulk file download required

#### 5. Data Format
- **File Type**: Pipe-delimited text files (.txt)
- **Compression**: ZIP archives
- **Size**: ~100-500 MB per crop year (compressed)
- **Structure**: One row per state-county-crop-insurance plan combination

**Example Record Structure**:
```
State Code|State Abbreviation|County Code|County Name|Commodity Code|Commodity Name|Insurance Plan Code|Insurance Plan|Year|Policies Sold|...[additional fields]
```

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: Asks "Do you have crop insurance?" (yes/no) + total premium paid
- RMA: Detailed annual data on acres insured, indemnities, loss ratios BY CROP
- **RMA provides**: Annual time series, crop-specific insurance metrics, loss payments

**vs. Quick Stats**:
- Quick Stats: Does NOT include crop insurance data
- RMA: Only source of county-level crop insurance statistics

**Unique Value**:
- Annual crop risk and loss data by county by crop
- Indemnity payments = proxy for crop losses/weather impacts
- Acres insured = indicator of farming activity and risk management
- Loss ratios = county-level risk assessment

#### 7. Data Quality & Limitations

**Strengths**:
- Administrative data (complete enumeration of all insured acres)
- High accuracy (legal/financial records)
- Long time series (1948-present)
- Detailed crop breakdown

**Limitations**:
- Only covers insured acres (~89% of major crops, lower for specialty crops)
- Suppression rules: <3 policies in county = data suppressed
- Does not include uninsured farming activity
- Crop year basis may not align with calendar year

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Administrative records, complete for insured crops

---

### SOURCE 2: USDA FARM SERVICE AGENCY (FSA) - CONSERVATION RESERVE PROGRAM

**Official Name**: Conservation Reserve Program Statistics
**Agency**: USDA Farm Service Agency (FSA)
**Program**: Conservation Reserve Program (CRP)

#### 1. Geographic Coverage
- **County-Level**: Yes (all counties, based on physical location of contracted land)
- **Coverage Years**: 1986-2024 (program inception to present)
- **Update Frequency**:
  - Monthly summary reports
  - Annual detailed enrollment reports
  - Data as of end of previous month

#### 2. Variables Available

**Total Variables**: ~15-20 core variables per county

**CRP Enrollment Variables:**

| Variable | Description | Units |
|----------|-------------|-------|
| CRP Contracts | Active CRP contracts | Count |
| CRP Farms | Farms with CRP contracts | Count |
| CRP Acres | Total enrolled acres | Acres |
| General CRP Acres | General signup acres | Acres |
| Continuous CRP Acres | Continuous signup acres | Acres |
| Grassland CRP Acres | Grassland CRP acres | Acres |
| CREP Acres | Conservation Reserve Enhancement | Acres |
| Annual Rental Payment | Total annual payment | Dollars |
| Average Rental Rate | Avg payment per acre | $/acre |
| Soil Rental Rate | County soil rental rate | $/acre |

**CRP Practice Breakdowns** (50+ conservation practices):
- CP1: Grass planting
- CP2: Tree planting
- CP3: Tree planting (hardwoods)
- CP4: Wildlife habitat
- CP8: Grass waterways
- CP9: Shallow water areas for wildlife
- CP10: Vegetative cover (existing)
- CP21: Filter strips
- CP22: Riparian buffers
- CP23: Wetland restoration
- CP25: Rare and declining habitat
- CP33: Upland bird habitat buffers
- CP42: Pollinator habitat
- ...and 40+ more

**Payment Information**:
- Annual rental payments by county
- Average payment per acre
- Soil rental rates (for setting payment rates)

#### 3. Frequency of Release
- **Monthly Reports**: Enrollment summary (acres, contracts, farms)
- **Annual Reports**: Detailed by practice type, county
- **Historical Data**: Available back to 1986 (program start)

#### 4. Access Methods

**Website**:
- URL: https://www.fsa.usda.gov/programs-and-services/conservation-programs/reports-and-statistics/conservation-reserve-program-statistics
- Format: Excel files, PDF reports
- County-level enrollment tables

**Monthly Reports**:
- Summary of current enrollment by county
- Released monthly (data through end of previous month)

**Annual Reports**:
- Detailed enrollment by practice
- Enrollment trends
- Payment summaries

**Data Files**:
- Excel spreadsheets with county data
- Multiple tabs for different CRP types
- Practice-level detail

**No Direct API**: Data must be downloaded from website

#### 5. Data Format
- **File Type**: Excel (.xlsx), PDF
- **Structure**: County rows, variable columns
- **Updates**: Monthly enrollment summaries; annual detailed reports

**Example County Record**:
```
County | State | Contracts | Farms | Total Acres | General Acres | Continuous Acres | Grassland Acres | Annual Payment | Avg Rate
Adams | IL | 45 | 42 | 1,250 | 800 | 350 | 100 | $125,000 | $100/acre
```

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: "Enrolled in CRP?" (yes/no) + total CRP acres
- FSA: Detailed enrollment by CRP type (General, Continuous, Grassland, CREP), practice codes, payment amounts
- **FSA provides**: ANNUAL tracking, practice-level detail, payment information

**vs. Quick Stats**:
- Quick Stats: Does NOT include detailed CRP enrollment data
- FSA: Only comprehensive source of county-level CRP statistics

**Unique Value**:
- Conservation land use (land not in production)
- Annual time series of conservation adoption
- Practice-specific conservation activities
- Economic impact (rental payments to farmers)

#### 7. Data Quality & Limitations

**Strengths**:
- Administrative records (all CRP contracts)
- Complete enumeration (not sampled)
- Detailed practice breakdown
- Long time series (1986-present)

**Limitations**:
- Only CRP land (not all conservation practices)
- Some counties may have minimal or no CRP enrollment
- Practice codes may change over time
- Payment rates reflect program rules, not market rates

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Complete administrative records

---

### SOURCE 3: USDA NRCS - CONSERVATION PRACTICES & FINANCIAL ASSISTANCE

**Official Name**: RCA Data Viewer / Resources Conservation Act Data
**Agency**: USDA Natural Resources Conservation Service (NRCS)
**Program**: Multiple conservation programs (EQIP, CSP, ACEP, RCPP, etc.)

#### 1. Geographic Coverage
- **County-Level**: Yes (all counties)
- **Coverage Years**:
  - Conservation practices: FY 2005-2024
  - Financial assistance: FY 2014-2024
  - Easements: FY 1998-2024
- **Update Frequency**: Annual (fiscal year basis)

#### 2. Variables Available

**Financial Assistance Variables (FY 2014-2024):**

| Variable | Description | Units |
|----------|-------------|-------|
| Contracts Signed | NRCS conservation contracts | Count |
| Dollars Obligated | Financial assistance | Dollars |
| Underserved Contracts | Contracts with underserved farmers | Count |
| EQIP Contracts | Environmental Quality Incentives | Count |
| CSP Contracts | Conservation Stewardship Program | Count |
| ACEP Easements | Agricultural Conservation Easements | Count |
| RCPP Projects | Regional Conservation Partnerships | Count |

**Conservation Practice Variables (FY 2005-2024):**

170+ NRCS Conservation Practices tracked, including:

| Practice Code | Practice Name | Units Tracked |
|---------------|---------------|---------------|
| 328 | Conservation Crop Rotation | Acres |
| 340 | Cover Crop | Acres |
| 329 | Residue and Tillage Management, No-Till | Acres |
| 345 | Residue and Tillage Management, Mulch Till | Acres |
| 590 | Nutrient Management | Acres |
| 528 | Prescribed Grazing | Acres |
| 512 | Pasture and Hay Planting | Acres |
| 382 | Fence | Feet |
| 441 | Irrigation System, Microirrigation | Count |
| 430 | Irrigation Pipeline | Feet |
| 443 | Irrigation System, Surface and Subsurface | Count |
| 587 | Structure for Water Control | Count |
| 378 | Pond | Count |
| 595 | Pest Management Conservation System | Acres |
| 449 | Irrigation Water Management | Acres |
| 612 | Tree/Shrub Establishment | Acres |
| 391 | Riparian Forest Buffer | Acres |
| 393 | Filter Strip | Acres |
| 412 | Grassed Waterway | Acres |
| 394 | Firebreak | Feet |
| 342 | Critical Area Planting | Acres |

**For Each Practice:**
- Practice count (number of applications)
- Acres treated (for area practices)
- Linear feet (for linear practices like fence, pipeline)
- Units (for countable practices like ponds, wells)

**Easement Variables (FY 1998-2024):**

| Variable | Description | Units |
|----------|-------------|-------|
| Easements Closed | Conservation easements finalized | Count |
| Easement Acres | Acres under easement | Acres |
| Wetland Easements | Wetland Reserve Program | Count |
| Agricultural Land Easements | Farmland protection | Count |
| Easement Purpose | Conservation purpose category | Category |

#### 3. Frequency of Release
- **Annual Updates**: Data released annually (fiscal year basis)
- **Final Data**: FY 2023 final data available
- **Preliminary Data**: FY 2024-2025 year-to-date data available
- **Historical Archive**: Back to FY 2005 (practices), FY 1998 (easements)

#### 4. Access Methods

**RCA Data Viewer** (Interactive):
- URL: https://www.nrcs.usda.gov/resources/data-and-reports/rca-data-viewer
- Interactive maps, charts, and tables
- Filter by county, state, practice, fiscal year
- Export to Excel, CSV

**RCA Data Downloads** (Bulk):
- URL: https://www.nrcs.usda.gov/rca-data-downloads
- Bulk Excel files
- Machine-readable flat files
- Historical data archives

**Key Dashboards:**
- Financial Assistance Program (contracts, dollars, practices)
- Conservation Practice Application (practice counts, acres)
- Conservation Easements (easements, acres, purpose)

**Contact**: RCA@usda.gov

#### 5. Data Format
- **File Type**: Excel (.xlsx), CSV
- **Interactive Tool**: Web-based data viewer with export
- **Bulk Files**: Downloadable datasets
- **Structure**: County-level records with practice details

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: Asks about conservation practices ADOPTED on farm (not linked to NRCS programs)
- NRCS: Conservation practices APPLIED THROUGH NRCS PROGRAMS with financial assistance
- **NRCS provides**: Program participation, financial assistance amounts, annual tracking

**vs. FSA CRP**:
- FSA: CRP land retirement program (taking land out of production)
- NRCS: Working lands conservation (keeping land in production with conservation practices)
- **Different programs**: Complementary data

**Unique Value**:
- Working lands conservation practices (on productive farmland)
- Financial assistance to farmers for conservation
- Detailed practice-by-practice application data
- Annual program participation trends

#### 7. Data Quality & Limitations

**Strengths**:
- Administrative records (all NRCS contracts)
- Detailed practice breakdown (170+ practices)
- Long time series (FY 2005-present for practices)
- Linked to financial assistance

**Limitations**:
- Only NRCS-assisted conservation (not farmer-initiated practices without NRCS)
- Fiscal year basis (Oct 1 - Sep 30)
- Practice definitions may change over time
- Does not capture conservation impact (only practice application)

**Coverage Note**:
- NRCS works with ~500,000 farmers annually
- Not all conservation activity is NRCS-assisted
- Census captures broader conservation adoption

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Administrative records for NRCS programs

---

### SOURCE 4: BUREAU OF ECONOMIC ANALYSIS (BEA) - FARM INCOME BY COUNTY

**Official Name**: Regional Economic Accounts - Personal Income by County
**Agency**: U.S. Department of Commerce, Bureau of Economic Analysis
**Component**: Farm proprietors' income

#### 1. Geographic Coverage
- **County-Level**: Yes (all 3,143 counties + DC)
- **Coverage Years**: 1969-2024 (55-year time series)
- **Update Frequency**: Annual (released November for prior calendar year)

#### 2. Variables Available

**Farm-Related Income Components:**

| Variable | Description | Units |
|----------|-------------|-------|
| Farm Proprietors' Income | Net farm income | Dollars (thousands) |
| Farm Earnings | Net earnings from farm proprietors | Dollars |
| Total Personal Income | Total county income (for context) | Dollars |
| Per Capita Personal Income | Including farm income | Dollars/person |
| Farm Share of Income | Farm income ÷ Total income | Percent |

**Additional Context Variables:**
- Nonfarm proprietors' income (comparison)
- Wage and salary income
- Transfer payments
- Property income (dividends, interest, rent)

**Farm Income Definition (BEA)**:
- Net income of sole proprietorships and partnerships
- Includes farm operator dwellings (imputed rent)
- Excludes corporate farms (captured in corporate profits nationally)
- Includes income of farm residents from farm production

#### 3. Frequency of Release
- **Annual Release**: November each year (for prior calendar year)
- **Time Series**: 1969-present (continuous 55+ years)
- **Revisions**: Annual updates may revise prior 3 years

#### 4. Access Methods

**Interactive Data Application**:
- URL: https://apps.bea.gov/itable/?ReqID=70&step=1
- Select "Personal Income (state and local)"
- Choose county, years, variables
- Export to Excel, CSV

**Bulk Downloads**:
- URL: https://www.bea.gov/data/income-saving/personal-income-county-metro-and-other-areas
- Downloadable datasets
- All counties, all years
- CSV and Excel formats

**BEA API**:
- URL: https://apps.bea.gov/api/signup/
- RESTful API for programmatic access
- Free API key required
- Query by county FIPS code, year, variable

**Example API Call**:
```
https://apps.bea.gov/api/data/?&UserID=YOUR_API_KEY&method=GetData&datasetname=Regional&TableName=CAINC5N&LineCode=1&GeoFips=17001&Year=2023
```

#### 5. Data Format
- **File Type**: Excel, CSV
- **API**: JSON, XML
- **Structure**: County-year panel data
- **FIPS Codes**: 5-digit county FIPS

**Example Record**:
```
GeoFIPS | GeoName | Year | LineCode | Description | Value
17001 | Adams, IL | 2023 | 1 | Total personal income | 500,000
17001 | Adams, IL | 2023 | 50 | Farm proprietors' income | 45,000
```

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: Detailed farm sales, expenses, net income (every 5 years)
- BEA: Annual farm income estimates (continuous time series)
- **BEA advantage**: ANNUAL data fills inter-census years

**vs. USDA ERS**:
- ERS: State-level farm income (not county)
- BEA: County-level farm income (annual)
- **BEA advantage**: County detail

**Differences in Definition**:
- Census: Farm-level accounting (sales - expenses + government payments)
- BEA: Proprietor income by residence (national accounts definition)
- BEA includes non-cash items (inventory change, operator dwelling value)

**Unique Value**:
- Only source of ANNUAL county-level farm income time series
- Long historical record (1969-present)
- Consistent methodology over time
- Integration with broader county economy measures

#### 7. Data Quality & Limitations

**Methodology**:
- BEA uses USDA farm income statistics as inputs
- Allocates state/national totals to counties using allocation factors
- Factors include: Census of Agriculture, NASS sales, agricultural employment, crop/livestock production

**Strengths**:
- Annual time series (fills inter-census gaps)
- Long historical record (1969-present)
- Consistent with national economic accounts
- Free, easily accessible

**Limitations**:
- Less detailed than Census (net income only, not breakdowns)
- Modeled allocation to counties (not direct survey)
- Revised periodically as new benchmark data available
- Farm income definition differs from USDA

**Reliability**: ⭐⭐⭐⭐ (4/5) - Modeled from USDA sources, but best annual county time series available

**Use Cases**:
- Annual farm income trends by county
- Economic impact of agriculture on county economies
- Long-term time series analysis (1969-present)
- Comparing farm vs. nonfarm income

---

### SOURCE 5: USDA NASS - CASH RENTS BY COUNTY

**Official Name**: Cash Rents Survey / Land Values and Cash Rents Report
**Agency**: USDA National Agricultural Statistics Service (NASS)
**Mandate**: 2008 Farm Bill (county-level rental rates for counties with 20,000+ acres cropland+pasture)

#### 1. Geographic Coverage
- **County-Level**: Yes (~2,000+ counties meeting 20,000 acre threshold)
- **Coverage Years**: 2008-2024 (annual survey established 2008)
- **Update Frequency**: Annual (released August each year)

#### 2. Variables Available

**Rental Rate Variables ($/acre):**

| Variable | Description | Units |
|----------|-------------|-------|
| Cropland, Irrigated - Rent | Cash rent for irrigated cropland | $/acre |
| Cropland, Non-irrigated - Rent | Cash rent for non-irrigated cropland | $/acre |
| Pasture - Rent | Cash rent for pasture | $/acre |

**For Each Rental Rate:**
- Mean (average rental rate)
- Standard error
- Coefficient of variation (reliability measure)

**National & State Context:**
- U.S. average rental rates (for comparison)
- State average rental rates
- Year-over-year change

#### 3. Frequency of Release
- **Annual Survey**: Conducted May-June each year
- **Release**: August (typically first week)
- **Report**: "Land Values and Cash Rents" report includes county data
- **Historical Data**: 2008-present in Quick Stats

#### 4. Access Methods

**Quick Stats Database**:
- URL: https://quickstats.nass.usda.gov/
- Query:
  - Program = "Survey"
  - Commodity = "Rent" or "Rent, Cash"
  - Geographic Level = "County"
  - Year = 2008-2024
- Export: CSV, Excel

**Annual Report**:
- URL: https://www.nass.usda.gov/Publications/Todays_Reports/reports/land0824.pdf (example 2024)
- PDF report includes county tables (in appendix)
- National, state, and county summaries

**Quick Stats API**:
- Programmatic access via NASS API
- Query county rental rates by FIPS code and year

**Example Query (Quick Stats)**:
```
Sector: Economics
Commodity: Rent, Cash, Cropland, Irrigated
Data Item: Rent, Cash, Cropland, Irrigated - Rental Rate, Measured in $ / Acre
Geographic Level: County
State: Iowa
Year: 2024
```

#### 5. Data Format
- **Quick Stats**: CSV export from database
- **Annual Report**: PDF with tables
- **Structure**: County-year records with rental rates by land type

**Example Record**:
```
County | State | Year | Cropland Irrigated Rent ($/acre) | Cropland Nonirrigated Rent ($/acre) | Pasture Rent ($/acre) | CV%
Sioux | IA | 2024 | 320 | 280 | 85 | 5.2
```

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: Asks about rented/leased acres, but not specific rental rates paid
- NASS Cash Rents: Provides county-specific average rental rates
- **Cash Rents advantage**: Annual rates, enables rental market analysis

**vs. NASS Land Values**:
- Land Values: State-level only (average value of farmland $/acre)
- Cash Rents: County-level rental rates
- **Different metrics**: Land value = asset value; cash rent = annual rental income

**Unique Value**:
- Only source of county-specific farmland rental rates
- Annual tracking of land rental markets
- Important for farm business economics (input cost)
- Indicator of land productivity and competition

#### 7. Data Quality & Limitations

**Survey Methodology**:
- **Sample**: Probability sample of farm operators
- **Data Collection**: Mail survey with phone follow-up
- **Respondents**: Farm operators who rent out land or rent in land

**Strengths**:
- Mandated by law (2008 Farm Bill)
- Annual data (tracks rental market trends)
- County-specific rates
- Reliable methodology

**Limitations**:
- Only counties with 20,000+ acres cropland+pasture
- Sampling error (CV% reported with each estimate)
- Cash rent only (not share rent arrangements)
- High CV% counties have less reliable estimates

**Suppression**:
- Counties with insufficient sample or high CV% may be suppressed
- Indicated by "(D)" in tables

**Reliability**: ⭐⭐⭐⭐ (4/5) - Survey-based with sampling error, but best available county rental rate data

**Use Cases**:
- Farm economics (input cost analysis)
- Land rental market trends
- Agricultural land values (complement to ownership values)
- County agricultural competitiveness

---

### SOURCE 6: USDA ORGANIC INTEGRITY DATABASE

**Official Name**: Organic INTEGRITY Database
**Agency**: USDA Agricultural Marketing Service (AMS)
**Program**: National Organic Program (NOP)

#### 1. Geographic Coverage
- **Operation-Level**: All certified organic operations (searchable by location)
- **Aggregable to County**: Yes (via city, county, state, zip code fields)
- **Coverage Years**: Current + historical annual snapshots
- **Update Frequency**: Continuously updated; annual snapshots archived

#### 2. Variables Available

**Per Certified Operation:**

| Variable | Description | Format |
|----------|-------------|--------|
| Operation Name | Legal business name | Text |
| Physical Address | Street address | Text |
| City | City location | Text |
| County | County location | Text |
| State | State | 2-letter code |
| Zip Code | ZIP code | 5-digit |
| Certifying Agent | Name of certifier | Text |
| Certification Status | Certified/Suspended/Revoked | Status |
| Operation Type | Crop/Livestock/Wild/Handler | Category |
| Scope Categories | Certified categories | List |
| Crops | Specific crops certified | List |
| Livestock | Specific livestock types | List |

**Certification Scope Categories:**
- Crops (field crops, vegetables, fruits, etc.)
- Livestock (cattle, poultry, hogs, etc.)
- Wild crops
- Handling/Processing

**Aggregable County Metrics:**
- Count of certified organic operations
- Operations by type (crop, livestock, handler)
- Operations by status (active, suspended)
- Crop diversity (number of different crops)
- Livestock types

#### 3. Frequency of Release
- **Real-Time**: Database updated continuously as certifications granted/revoked
- **Annual Snapshots**: Historical lists archived annually
- **Data History Page**: Annual lists downloadable (2018-present)

#### 4. Access Methods

**Online Searchable Database**:
- URL: https://organic.ams.usda.gov/integrity/
- Search by:
  - Operation name
  - Location (address, city, county, state, zip)
  - Certifying agent
  - Products (crops, livestock)
- Export: Individual operation details

**Historical Annual Lists**:
- URL: https://organic.ams.usda.gov/integrity/DataHistory/DataHistory.aspx
- Annual lists of all certified operations (2018-present)
- Download: CSV files
- Snapshot as of specific date each year

**Ag Data Commons**:
- URL: https://agdatacommons.nal.usda.gov/articles/dataset/The_Organic_INTEGRITY_Database/24661722
- Monthly snapshots
- Full database downloads
- Machine-readable formats

#### 5. Data Format
- **Online**: Web interface, HTML
- **Export**: CSV downloads
- **Structure**: One row per certified operation
- **Updates**: Continuous (online), annual snapshots (archived)

**Example Record**:
```
Operation Name | Address | City | County | State | Zip | Certifying Agent | Status | Type | Scope
ABC Organic Farm | 123 Farm Rd | Ames | Story | IA | 50010 | Iowa Dept Ag | Certified | Crop | Corn, Soybeans, Hay
XYZ Dairy | 456 Dairy Ln | Madison | Dane | WI | 53703 | MOSA | Certified | Livestock | Dairy Cattle
```

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: County totals of organic farms, organic acres, organic sales (quinquennial)
- Organic DB: CURRENT list of every certified operation with location
- **Organic DB advantage**: Real-time, operation-level detail, enables current counts

**vs. Quick Stats**:
- Quick Stats: County organic production data from Census/surveys
- Organic DB: Current certified operation locations
- **Different purposes**: Quick Stats = production data; Organic DB = certification status

**Unique Value**:
- Only real-time list of certified organic operations
- Operation-level location (can map, analyze density)
- Certification status tracking (new certifications, revocations)
- Handler/processor locations (not just farms)

#### 7. Data Quality & Limitations

**Data Source**:
- Administrative records from USDA-accredited certifying agents
- Legal requirement to report all certifications

**Strengths**:
- Complete enumeration (all certified operations)
- Real-time updates
- Detailed operation information
- Historical tracking

**Limitations**:
- Does NOT include acres or production volumes
- Does NOT include non-certified organic (farms transitioning or not certified)
- Operation address = business address (may not be production location)
- Requires geocoding or county field for county aggregation

**Coverage**:
- All operations certified under USDA National Organic Program
- Does NOT include state organic programs (if different from USDA)
- Does NOT include international organic (unless certified to USDA standards)

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Complete administrative database

**Use Cases**:
- Count of certified organic operations by county
- Organic farm density mapping
- Tracking organic sector growth (new certifications over time)
- Local/regional organic supply chain analysis
- Complement to Census organic acreage/sales data

---

### SOURCE 7: USGS - WATER USE DATA (AGRICULTURAL/IRRIGATION)

**Official Name**: Water Use in the United States
**Agency**: U.S. Geological Survey (USGS)
**Program**: National Water Use Science Project

#### 1. Geographic Coverage
- **County-Level**: Yes (all 3,143 counties)
- **Also Available**: HUC watershed boundaries (HUC8, HUC12)
- **Coverage Years**: 1950, 1955, 1960, ..., 2015, 2020 (quinquennial)
- **Update Frequency**: Every 5 years (next: 2025 data expected ~2027-2028)

#### 2. Variables Available

**Irrigation Water Use (per county):**

| Variable | Description | Units |
|----------|-------------|-------|
| Irrigation Total Withdrawals | Total water for irrigation | Mgal/day |
| Irrigation Groundwater Withdrawals | Groundwater for irrigation | Mgal/day |
| Irrigation Surface Water Withdrawals | Surface water for irrigation | Mgal/day |
| Irrigation Acres | Irrigated acres | Acres |
| Irrigation per Acre | Application rate | gal/day/acre |

**Irrigation by Type** (where available):
- Sprinkler irrigation
- Microirrigation (drip, trickle)
- Surface irrigation (flood, furrow)

**Other Agricultural Water Use:**

| Variable | Description | Units |
|----------|-------------|-------|
| Livestock Total Withdrawals | Water for livestock | Mgal/day |
| Livestock Groundwater | Groundwater for livestock | Mgal/day |
| Livestock Surface Water | Surface water for livestock | Mgal/day |
| Aquaculture Total Withdrawals | Water for aquaculture | Mgal/day |
| Aquaculture Groundwater | Groundwater for aquaculture | Mgal/day |
| Aquaculture Surface Water | Surface water for aquaculture | Mgal/day |

**Advanced Datasets (2000-2020):**
- Monthly irrigation withdrawals (by HUC12 watershed)
- Consumptive use (water not returned to system)
- Evapotranspiration estimates
- Reference ET (ETo) and actual ET (ETa)
- Irrigation efficiency by crop

#### 3. Frequency of Release
- **Quinquennial**: Every 5 years (aligned with years ending in 0 and 5)
- **Release Timeline**:
  - 2020 water use data → released 2023-2024
  - 2025 water use data → expected 2027-2028
- **Historical Archive**: 1950-2020 (14 compilations)

#### 4. Access Methods

**National Water Use Data**:
- URL: https://waterdata.usgs.gov/nwis/wu
- County-level summary tables
- Downloadable datasets
- Interactive maps

**Water Use in the United States (main page)**:
- URL: https://www.usgs.gov/mission-areas/water-resources/science/water-use-united-states
- Reports, data files, methodologies

**Advanced Products**:
- **Monthly Irrigation Reanalysis (2000-2020)**: HUC12 watershed level
- URL: https://www.usgs.gov/data/monthly-crop-irrigation-withdrawals-and-efficiencies-huc12-watershed-years-2000-2020-within
- Includes consumptive use, ET, irrigation efficiency

**ScienceBase Catalog**:
- URL: https://www.sciencebase.gov/catalog/
- Search "water use" for detailed datasets
- Download: CSV, geodatabase, shapefiles

#### 5. Data Format
- **File Type**: CSV, Excel, geodatabase
- **Structure**: County-year records with water use by category
- **Advanced**: NetCDF, GeoTIFF for gridded products

**Example County Record (2020)**:
```
County FIPS | County Name | State | Year | Irrigation Total (Mgal/day) | Irrigation GW | Irrigation SW | Irrigated Acres | Livestock Total | Aquaculture Total
19193 | Sioux, Iowa | IA | 2020 | 25.5 | 15.2 | 10.3 | 75,000 | 2.1 | 0
```

#### 6. Comparison to Already Documented Sources

**vs. Census of Agriculture**:
- Census: Irrigated acres, irrigation methods, water sources (farms)
- USGS: Estimated water VOLUMES withdrawn (Mgal/day)
- **Different metrics**: Census = infrastructure; USGS = water quantity

**Comparison of Irrigation Data:**

| Aspect | Census of Agriculture | USGS Water Use |
|--------|----------------------|----------------|
| Irrigated Acres | ✅ Yes | ✅ Yes |
| Irrigation Methods | ✅ Yes (sprinkler, drip, flood) | ⚠️ Limited |
| Water Source | ✅ Yes (on-farm, off-farm, GW) | ✅ Yes (GW, SW) |
| Water Volume | ❌ No | ✅ Yes (Mgal/day) |
| Frequency | Every 5 years | Every 5 years |

**Unique Value of USGS**:
- Water VOLUMES (not just acres irrigated)
- Livestock and aquaculture water use (not in Census)
- Integrated with other water use categories (public supply, industrial, etc.)
- Enables water stress/availability analysis

#### 7. Data Quality & Limitations

**Methodology**:
- **Data Sources**:
  - State water agencies (permits, metered data)
  - USDA Census of Agriculture (irrigated acres)
  - Crop water use coefficients
  - Modeling where direct measurement unavailable

**Estimation Methods**:
- Some states: Direct measurement/reporting
- Other states: Estimated from irrigated acres × crop water coefficients × irrigation efficiency

**Strengths**:
- National consistency
- Long time series (1950-2020)
- Integrated water use picture (ag + other uses)
- County-level detail

**Limitations**:
- Quinquennial only (not annual)
- Estimation methods vary by state (data quality varies)
- Livestock/aquaculture estimates less reliable than irrigation
- Not crop-specific at county level (except in advanced HUC12 datasets)

**Reliability**: ⭐⭐⭐⭐ (4/5) - Best available national county-level water use data, but relies on modeling in some areas

**Use Cases**:
- Agricultural water use intensity (water per acre)
- Groundwater vs. surface water dependence
- Water stress/scarcity analysis
- Livestock and aquaculture water demand
- Complement to Census irrigation infrastructure data

---

## 5. DATA ACCESS METHODS

### 5.1 Download Workflows

**USDA RMA Crop Insurance**:
1. Visit https://www.rma.usda.gov/SummaryOfBusiness/StateCountyCrop
2. Select crop year (2024, 2023, etc.)
3. Download ZIP file for state/county/crop summary
4. Extract pipe-delimited text files
5. Import to R, Python, Excel for analysis

**USDA FSA CRP Statistics**:
1. Visit https://www.fsa.usda.gov/programs-and-services/conservation-programs/reports-and-statistics/conservation-reserve-program-statistics
2. Select "Enrollment by County" report
3. Download Excel file
4. Extract county tables

**USDA NRCS Conservation Practices**:
1. Visit https://www.nrcs.usda.gov/resources/data-and-reports/rca-data-viewer
2. Select "Financial Assistance Program" dashboard
3. Filter by state, county, fiscal year, practice
4. Export to Excel or CSV

**BEA Farm Income**:
1. Visit https://apps.bea.gov/itable/?ReqID=70&step=1
2. Select "Personal Income by County"
3. Choose "Farm proprietors' income" line item
4. Select counties and years
5. Download Excel or CSV

**NASS Cash Rents (via Quick Stats)**:
1. Visit https://quickstats.nass.usda.gov/
2. Select Program = "Survey"
3. Select Commodity = "Rent, Cash"
4. Select Geographic Level = "County"
5. Select years (2008-2024)
6. Download CSV

**USDA Organic Integrity Database**:
1. Visit https://organic.ams.usda.gov/integrity/
2. Search by state/county
3. Export search results (CSV)
4. Or download annual snapshots from Data History page

**USGS Water Use**:
1. Visit https://waterdata.usgs.gov/nwis/wu
2. Select year (2020, 2015, etc.)
3. Select "County data"
4. Download CSV or Excel

### 5.2 R Code Examples

**Example 1: Download RMA Crop Insurance Data**
```r
library(tidyverse)

# RMA data must be downloaded manually and unzipped
# Read pipe-delimited file
rma_data <- read.delim(
  "sob-2024-state-county-crop.txt",
  sep = "|",
  header = TRUE,
  stringsAsFactors = FALSE
)

# Filter for specific commodity and state
iowa_corn <- rma_data %>%
  filter(state_name == "IOWA", commodity_name == "CORN") %>%
  select(county_name, policies_sold, net_planted_acres, indemnity_amount, total_premium)

# Calculate loss ratio
iowa_corn <- iowa_corn %>%
  mutate(loss_ratio = indemnity_amount / total_premium)
```

**Example 2: Access BEA Farm Income via API**
```r
library(httr)
library(jsonlite)

# BEA API key (get free at https://apps.bea.gov/api/signup/)
api_key <- "YOUR_API_KEY"

# Query farm income for Iowa counties, 2023
url <- paste0(
  "https://apps.bea.gov/api/data/",
  "?&UserID=", api_key,
  "&method=GetData",
  "&datasetname=Regional",
  "&TableName=CAINC5N",
  "&LineCode=50",  # Farm proprietors' income
  "&GeoFips=STATE:19",  # Iowa
  "&Year=2023"
)

response <- GET(url)
data <- content(response, as = "text")
farm_income <- fromJSON(data)

# Parse and clean
farm_income_df <- farm_income$BEAAPI$Results$Data %>%
  select(GeoFips, GeoName, TimePeriod, DataValue) %>%
  mutate(DataValue = as.numeric(DataValue))
```

**Example 3: Query NASS Cash Rents from Quick Stats**
```r
library(rnassqs)

# Set NASS API key
nassqs_auth(key = "YOUR_NASS_API_KEY")

# Query county cash rents for Iowa, 2024
cash_rents <- nassqs(
  list(
    source_desc = "SURVEY",
    sector_desc = "ECONOMICS",
    commodity_desc = "RENT",
    statisticcat_desc = "RENTAL RATE",
    agg_level_desc = "COUNTY",
    state_name = "IOWA",
    year = 2024
  )
)

# Clean and reshape
rents_clean <- cash_rents %>%
  select(county_name, short_desc, Value) %>%
  mutate(
    land_type = case_when(
      str_detect(short_desc, "IRRIGATED") ~ "Irrigated",
      str_detect(short_desc, "NON-IRRIGATED") ~ "Non-Irrigated",
      str_detect(short_desc, "PASTURE") ~ "Pasture"
    ),
    rent_per_acre = as.numeric(Value)
  ) %>%
  select(county_name, land_type, rent_per_acre)
```

**Example 4: Access USGS Water Use Data**
```r
library(tidyverse)
library(dataRetrieval)

# USGS water use data is available as bulk download
# Download from https://waterdata.usgs.gov/nwis/wu
# Example: Read 2020 water use data

water_use <- read_csv("usgs_water_use_2020.csv")

# Filter for irrigation data
irrigation <- water_use %>%
  filter(category == "Irrigation") %>%
  select(state_cd, county_cd, county_nm,
         total_withdrawals_mgd, groundwater_mgd, surface_water_mgd,
         irrigation_acres, water_per_acre = gallons_per_day_per_acre)

# Calculate irrigation intensity
irrigation <- irrigation %>%
  mutate(
    groundwater_pct = groundwater_mgd / total_withdrawals_mgd * 100,
    surface_water_pct = surface_water_mgd / total_withdrawals_mgd * 100
  )
```

**Example 5: Access NRCS Conservation Practices (via bulk download)**
```r
library(readxl)
library(tidyverse)

# Download Excel file from NRCS RCA Data Downloads
# https://www.nrcs.usda.gov/rca-data-downloads

# Read financial assistance data
nrcs_financial <- read_excel(
  "NRCS_Financial_Assistance_FY2024.xlsx",
  sheet = "County_Data"
)

# Filter for specific state and practice
iowa_eqip <- nrcs_financial %>%
  filter(State == "Iowa", Program == "EQIP") %>%
  select(County, Contracts_Signed, Dollars_Obligated, Acres_Treated)

# Summary by county
county_summary <- iowa_eqip %>%
  group_by(County) %>%
  summarize(
    total_contracts = sum(Contracts_Signed, na.rm = TRUE),
    total_dollars = sum(Dollars_Obligated, na.rm = TRUE),
    total_acres = sum(Acres_Treated, na.rm = TRUE),
    dollars_per_acre = total_dollars / total_acres
  )
```

### 5.3 Bulk Data Collection Workflow

**Recommended Priority Order**:

1. **Start with Census of Agriculture + Quick Stats**:
   - These are your foundation (already documented)
   - Provides comprehensive baseline

2. **Add Annual Time Series** (HIGH PRIORITY):
   - BEA Farm Income (1969-2024): Fills inter-census years
   - NASS Cash Rents (2008-2024): Annual land rental markets

3. **Add Risk & Conservation** (HIGH PRIORITY):
   - RMA Crop Insurance (1948-2024): Annual crop risk/losses
   - FSA CRP (1986-2024): Conservation land retirement
   - NRCS Practices (FY 2005-2024): Working lands conservation

4. **Add Specialty Sources** (MEDIUM PRIORITY):
   - Organic Integrity Database: Current organic operations
   - USGS Water Use (1950-2020): Quinquennial water volumes

**Storage Recommendations**:
- Use DuckDB or SQLite for local storage
- Separate tables for each source
- County FIPS codes as primary key
- Year as secondary key
- Enable joins across sources by county-year

---

## 6. PRIORITY VARIABLES FOR COLLECTION

### 6.1 Essential New Variables (Beyond Census/Quick Stats)

**Crop Insurance (RMA) - Top 10 Variables**:
1. Total indemnity payments by county ($ loss payments)
2. Acres insured by major crops
3. Loss ratio (indemnity/premium) by crop
4. Number of policies indemnified (farm risk indicator)
5. Total liability (insured value of crops)

**Conservation (FSA CRP) - Top 5 Variables**:
6. CRP acres enrolled (land not in production)
7. CRP annual rental payments (economic impact)
8. General vs. Continuous CRP breakdown

**Conservation (NRCS) - Top 5 Variables**:
9. EQIP/CSP contracts and dollars obligated
10. Conservation practices applied (acres): no-till, cover crops, prescribed grazing

**Farm Income (BEA) - Top 3 Variables**:
11. Annual farm proprietors' income (time series)
12. Farm share of county income (%)

**Land Economics (NASS) - Top 3 Variables**:
13. Cash rent for irrigated cropland ($/acre)
14. Cash rent for non-irrigated cropland ($/acre)

**Water Use (USGS) - Top 3 Variables**:
15. Irrigation water withdrawals (Mgal/day)
16. Groundwater vs. surface water split
17. Livestock water use

**Organic (USDA) - Top 2 Variables**:
18. Count of certified organic operations

### 6.2 Collection Frequency Recommendations

**Annual Collection**:
- RMA Crop Insurance (annual crop year)
- FSA CRP enrollment (annual or monthly)
- NRCS conservation practices (annual fiscal year)
- BEA farm income (annual)
- NASS cash rents (annual)
- Organic Integrity Database (annual snapshot)

**Quinquennial Collection**:
- USGS water use (every 5 years, aligned with Census years)

---

## 7. QUICK REFERENCE

### 7.1 Primary URLs

| Source | Main URL |
|--------|----------|
| RMA Crop Insurance | https://www.rma.usda.gov/SummaryOfBusiness/StateCountyCrop |
| FSA CRP Statistics | https://www.fsa.usda.gov/programs-and-services/conservation-programs/reports-and-statistics/conservation-reserve-program-statistics |
| NRCS RCA Data Viewer | https://www.nrcs.usda.gov/resources/data-and-reports/rca-data-viewer |
| BEA Regional Data | https://apps.bea.gov/itable/?ReqID=70&step=1 |
| NASS Quick Stats | https://quickstats.nass.usda.gov/ |
| Organic Integrity DB | https://organic.ams.usda.gov/integrity/ |
| USGS Water Use | https://waterdata.usgs.gov/nwis/wu |

### 7.2 Data Contact Information

| Agency | Email Contact |
|--------|---------------|
| RMA | Contact via website form |
| FSA | FSA Information Center |
| NRCS | RCA@usda.gov |
| BEA | CustomerService@bea.gov |
| NASS | nass@usda.gov |
| USGS | GS-W-NWISWeb_Data_Inquiries@usgs.gov |

### 7.3 API Keys Required

| Source | API Key Required? | Signup URL |
|--------|-------------------|------------|
| RMA | No | N/A |
| FSA | No | N/A |
| NRCS | No | N/A |
| BEA | Yes (free) | https://apps.bea.gov/api/signup/ |
| NASS Quick Stats | Yes (free) | https://quickstats.nass.usda.gov/api |
| USGS | No | N/A |

---

## APPENDIX A: RESEARCH METHODOLOGY

### Sources Investigated

This research systematically investigated all categories requested:

**USDA Agencies**:
- ✅ USDA NASS (Crop Production, Livestock, Milk, Eggs, Prices, Land Values, Labor)
- ✅ USDA RMA (Crop Insurance)
- ✅ USDA FSA (CRP, ACEP, Emergency Programs)
- ✅ USDA NRCS (Conservation Practices, Easements)
- ✅ USDA ERS (Farm Income, ARMS, Cost of Production)
- ✅ USDA AMS (Organic, Farmers Markets, Local Food, Prices)
- ✅ USDA APHIS (Animal Disease Surveillance)

**Other Federal**:
- ✅ Bureau of Economic Analysis (Farm Income)
- ✅ USGS (Water Use)

**Specialty Topics**:
- ✅ Organic agriculture
- ✅ Aquaculture
- ✅ Specialty crops (fruits, nuts, vegetables)
- ✅ Honey bees, maple syrup
- ✅ Forestry, Christmas trees
- ✅ Agritourism, direct sales
- ✅ Value-added agriculture
- ✅ Farm labor (including H-2A)
- ✅ Agricultural productivity

### Research Methods
- Web searches for each data source (November 2025)
- Website examination for data availability
- Documentation review for geographic coverage
- Comparison to already-documented sources (Census, Quick Stats)

### Verification
- All URLs verified functional as of November 12, 2025
- Data availability confirmed through website/API exploration
- Geographic coverage verified through source documentation

---

## DOCUMENT METADATA

**Document Version**: 1.0
**Last Updated**: November 12, 2025
**Author**: Claude Code (AI Research Assistant)
**Research Date**: November 12, 2025
**Sources Verified**: All URLs and data access methods verified as of November 2025
**Next Review**: Recommended annual update to capture new data releases

---

## SUMMARY TABLE: TRUE ADDITIONS VS ALREADY DOCUMENTED

| Category | Source | County Data? | Status | Notes |
|----------|--------|--------------|--------|-------|
| **TRUE ADDITIONS** |
| Crop Insurance | USDA RMA Summary of Business | ✅ Yes | ✅ NEW | Acres insured, indemnities, loss ratios by crop (annual, 1948-2024) |
| Conservation Reserve | USDA FSA CRP Statistics | ✅ Yes | ✅ NEW | CRP enrollment, practices, payments by county (annual, 1986-2024) |
| Conservation Practices | USDA NRCS RCA Data Viewer | ✅ Yes | ✅ NEW | Practices applied, financial assistance by county (FY 2005-2024) |
| Farm Income | BEA Regional Accounts | ✅ Yes | ✅ NEW | Annual farm proprietors' income (1969-2024) |
| Land Rental Rates | NASS Cash Rents Survey | ✅ Yes | ✅ NEW | Cropland & pasture rental rates ($/acre, annual, 2008-2024) |
| Organic Certification | USDA Organic Integrity DB | ✅ Yes | ✅ NEW | Certified operations by location (current + annual snapshots) |
| Agricultural Water Use | USGS Water Use | ✅ Yes | ✅ NEW | Irrigation, livestock, aquaculture water volumes (quinquennial, 1950-2020) |
| **ALREADY DOCUMENTED** |
| Crop Production | NASS Crop Production Reports | ✅ Yes | ❌ In Quick Stats | County data in Quick Stats for major crops |
| Livestock Inventory | NASS Livestock Reports | ✅ Yes | ❌ In Quick Stats/Census | County cattle, hogs inventories in Quick Stats |
| Specialty Crops | NASS Fruits/Vegetables Surveys | ⚠️ Limited | ❌ In Quick Stats/Census | Major producing counties in Quick Stats |
| Crop Values | NASS Crop Values Report | ⚠️ Derivable | ❌ In Quick Stats | County production × state price |
| Aquaculture | Census of Aquaculture | ✅ Yes | ❌ In Census | Quinquennial Census of Aquaculture (2023) |
| Organic Production | Census & Surveys | ✅ Yes | ❌ In Census/Quick Stats | Acres, sales in Census; Organic Integrity DB adds operation locations |
| Food Access | USDA Food Access Atlas | ✅ Yes | ❌ Already Documented | In your NUTRITION_TOBACCO_FOOD_ENVIRONMENT_COMPREHENSIVE.md |
| Farmers Markets | USDA AMS Directory | ✅ Yes | ❌ Already Documented | In your NUTRITION_TOBACCO_FOOD_ENVIRONMENT_COMPREHENSIVE.md |
| **NOT COUNTY-LEVEL** |
| Farm Income (State) | USDA ERS Farm Income | ❌ No | ❌ State Only | State-level only; use BEA for county |
| Livestock Slaughter | NASS Livestock Slaughter | ❌ No | ❌ State Only | State-level only |
| Agricultural Prices | NASS Prices Received | ❌ No | ❌ State/National Only | State and national prices only |
| Farm Labor | NASS Farm Labor | ❌ No | ❌ Regional Only | Multi-state regions, CA/FL/HI only |
| Cost of Production | USDA ERS ARMS | ❌ No | ❌ National/State Only | Sample survey, not county-level |
| Milk Production (monthly) | NASS Milk Production | ❌ No | ❌ State Only | Monthly state-level; Census has county |
| Egg Production (monthly) | NASS Chickens & Eggs | ❌ No | ❌ State Only | Monthly state-level; Census has county |
| Animal Disease | USDA APHIS Surveillance | ❌ No | ❌ State/Event Only | State-level; outbreak-specific county data |

---

**END OF COMPREHENSIVE RESEARCH REPORT**
