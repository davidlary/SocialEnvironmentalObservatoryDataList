# USDA NASS QUICKSTATS COMPLETE VARIABLE CATALOG
## All 10,000+ County-Level Agricultural Variables (Census + Surveys + Prices)

**Purpose:** Complete reference catalog of all USDA National Agricultural Statistics Service (NASS) QuickStats database variables, including Census of Agriculture, annual/monthly surveys, prices, organic certification, and specialty programs.

**Total Variables:** 10,000+ unique county-level agricultural data combinations

**Spatial Coverage:** National, state, and county levels (county availability varies by commodity)

**Temporal Coverage:** Historical data from 1840 (Census); annual surveys from 1960s; monthly data from 1990s to present

**Update Frequency:**
- Census: Every 5 years (most recent: 2022)
- Annual surveys: Yearly
- Monthly surveys: Monthly
- Prices: Weekly, monthly, annual

---

## 📥 ACCESS COMPLETE QUICKSTATS DATA

### Primary Database - NASS QuickStats 2.0
**URL:** https://quickstats.nass.usda.gov/

**Database Size:**
- 11.3 million+ agricultural data records
- 500+ commodities
- 200+ data items per commodity (typical)
- 6 geographic levels
- Multiple years and periods

### Query Structure - 6 Key Dimensions

QuickStats organizes data through hierarchical filtering:

**1. PROGRAM:**
- CENSUS: Census of Agriculture (every 5 years)
- SURVEY: Annual and monthly surveys
- ORGANIC: Organic certification data

**2. SECTOR:**
- ANIMALS & PRODUCTS
- CROPS
- DEMOGRAPHICS
- ECONOMICS
- ENVIRONMENTAL

**3. GROUP:**
- Field Crops
- Fruit & Tree Nuts
- Horticulture
- Vegetables
- Livestock
- Poultry
- Dairy
- Specialty

**4. COMMODITY:**
- 500+ specific commodities (corn, wheat, cattle, milk, etc.)
- Aggregations (e.g., "AG LAND", "FARM OPERATIONS")

**5. DATA ITEM:**
- AREA HARVESTED (acres)
- AREA PLANTED (acres)
- PRODUCTION (bushels, tons, pounds, head, etc.)
- YIELD (per acre)
- PRICE RECEIVED ($ per unit)
- VALUE OF PRODUCTION ($)
- INVENTORY (head, colonies, etc.)
- SALES (head, pounds, $)
- And 200+ other data items...

**6. DOMAIN:**
- TOTAL (all farms)
- ECONOMIC CLASS
- ORGANIC STATUS
- IRRIGATION STATUS
- AREA OPERATED
- And 50+ other domains for subsetting data

### API Access
**URL:** https://quickstats.nass.usda.gov/api

**API Key:** Free registration required

**Features:**
- RESTful API
- JSON and CSV output
- Programmatic queries
- Rate limit: 1,000 requests per minute

---

## 📊 QUICKSTATS VARIABLE STRUCTURE

### Understanding QuickStats "Variables"

QuickStats uses a combinatorial structure where a "variable" is defined by the intersection of:
- **Commodity** (e.g., CORN)
- **Data Item** (e.g., AREA HARVESTED)
- **Domain** (e.g., TOTAL, IRRIGATED, ORGANIC)
- **Year** (e.g., 2022)
- **Period** (e.g., YEAR, marketing year, month)
- **Geographic Level** (e.g., COUNTY)

**Example Variables:**
1. "CORN - ACRES HARVESTED" (Total, 2022, County)
2. "CORN - ACRES HARVESTED, IRRIGATED" (Irrigated subset, 2022, County)
3. "CORN, GRAIN - PRODUCTION, MEASURED IN BU" (Total, 2022, County)
4. "CORN, GRAIN - YIELD, MEASURED IN BU / ACRE" (Total, 2022, County)

This combinatorial system creates **10,000+ unique county-level variable combinations** across all programs.

---

## 🌾 PROGRAM 1: CENSUS OF AGRICULTURE (~6,000 variables)

Comprehensive count every 5 years (2022, 2017, 2012, 2007, 2002, etc.)

**Coverage:** All farms with ≥$1,000 in agricultural sales

**County Availability:** All 3,143 US counties

**Variable Categories:**
1. Farm counts & characteristics
2. Land use
3. Crop acreage & production
4. Livestock inventory & sales
5. Economics & income
6. Production expenses
7. Operator demographics
8. Conservation practices
9. Marketing & sales channels
10. Organic certification

**Detailed Catalog:** See companion file **USDA_AG_CENSUS_COMPLETE_TABLES.md** for complete 77-table structure and 6,000+ Census variables.

**Example Census Variables:**
- "FARM OPERATIONS - NUMBER OF OPERATIONS"
- "FARM OPERATIONS - ACRES OPERATED"
- "AG SALES - SALES, MEASURED IN $"
- "CORN, GRAIN - ACRES HARVESTED"
- "CATTLE, INCL CALVES - INVENTORY"
- "PRODUCERS, PRINCIPAL - AGE, AVG, MEASURED IN YEARS"

---

## 🌽 PROGRAM 2: SURVEY - ANNUAL CROP SURVEYS (~2,500 variables)

Annual production estimates for major field crops, fruits, vegetables, and specialty crops

### 2.1 FIELD CROPS - Annual Surveys

#### CORN (~80 county-level variables)
| Data Item | Units | Domain Options | County Coverage |
|-----------|-------|----------------|-----------------|
| Area planted | acres | Total, irrigated, non-irrigated | ~2,800 counties |
| Area harvested for grain | acres | " | " |
| Area harvested for silage | acres | " | ~1,500 counties |
| Production, grain | bushels | " | ~2,800 counties |
| Production, silage | tons | " | ~1,500 counties |
| Yield, grain | bu/acre | " | ~2,800 counties |
| Yield, silage | tons/acre | " | ~1,500 counties |
| Price received | $/bushel | Total | State-level primarily |
| Value of production | $ | Total | State-level primarily |

**Data Sources:** June Area Survey, August Production Forecast, annual summary

**Time Series:** Annual from 1960s to present

#### SOYBEANS (~60 county-level variables)
| Data Item | Units | Domain Options |
|-----------|-------|----------------|
| Area planted | acres | Total, irrigated, non-irrigated |
| Area harvested | acres | " |
| Production | bushels | " |
| Yield | bu/acre | " |
| Price received | $/bushel | Total |
| Value of production | $ | Total |

**County Coverage:** ~2,200 soybean-producing counties

#### WHEAT (~90 county-level variables by class)
**Wheat Classes:** Winter wheat, spring wheat, durum wheat

| Data Item | Units | Domain Options |
|-----------|-------|----------------|
| Area planted | acres | Total, by class, irrigated |
| Area harvested | acres | " |
| Production | bushels | " |
| Yield | bu/acre | " |
| Price received | $/bushel | By class |

**County Coverage:** ~1,800 wheat-producing counties

#### OTHER MAJOR FIELD CROPS (Annual County-Level Data Available)
| Crop | Typical Variables | County Coverage |
|------|-------------------|-----------------|
| **Cotton** (upland, pima) | Planted, harvested, production (bales), yield (lbs/acre), price | ~800 counties |
| **Rice** | Planted, harvested, production (cwt), yield, price | ~250 counties |
| **Sorghum, grain** | Planted, harvested, production (bu), yield | ~500 counties |
| **Barley** | Planted, harvested, production (bu), yield | ~400 counties |
| **Oats** | Planted, harvested, production (bu), yield | ~600 counties |
| **Peanuts** | Planted, harvested, production (lbs), yield | ~150 counties |
| **Sunflower** (oil, non-oil) | Planted, harvested, production (lbs), yield | ~200 counties |
| **Canola** | Planted, harvested, production (lbs), yield | ~100 counties |
| **Tobacco** (burley, flue-cured) | Harvested, production (lbs), yield | ~200 counties |
| **Sugarbeets** | Harvested, production (tons), yield | ~200 counties |
| **Sugarcane** (sugar, seed) | Harvested, production (tons), yield | ~50 counties |
| **Dry edible beans** | Harvested, production (cwt), yield | ~200 counties |
| **Dry edible peas** | Harvested, production (cwt), yield | ~100 counties |
| **Lentils** | Harvested, production (cwt), yield | ~50 counties |
| **Chickpeas** | Harvested, production (lbs), yield | ~30 counties |
| **Potatoes** (fall, spring, winter) | Planted, harvested, production (cwt), yield | ~300 counties |
| **Sweet potatoes** | Harvested, production (cwt), yield | ~150 counties |

**Total Field Crop Variables (Annual):** ~1,500 unique county-level data combinations

### 2.2 HAY & FORAGE CROPS (~150 variables)

| Crop Type | Data Items | County Coverage |
|-----------|------------|-----------------|
| **Hay, alfalfa** | Harvested, production (tons), yield, price | ~2,500 counties |
| **Hay, other tame** | " | ~2,500 counties |
| **Hay, total** | " | ~2,500 counties |
| **Haylage** | Harvested, production (tons) | State-level |

**Cuttings:** 1st cutting, 2nd cutting, 3rd+ cutting data for some states

### 2.3 VEGETABLES - Annual Surveys (~400 variables)

County-level data availability varies significantly by crop and state

**Major Vegetables with County Data:** (selected)
| Vegetable | Data Items | Typical County Coverage |
|-----------|------------|------------------------|
| **Tomatoes** (fresh, processing) | Area harvested, production (cwt, tons), value ($) | ~100 counties (CA, FL, major states) |
| **Onions** (dry, green) | Area harvested, production (cwt), value | ~80 counties |
| **Lettuce** (head, leaf, romaine) | Area harvested, production (cwt), value | ~50 counties (CA, AZ) |
| **Cabbage** (fresh, processing) | Area harvested, production (tons), value | ~60 counties |
| **Carrots** | Area harvested, production (cwt), value | ~40 counties |
| **Celery** | Area harvested, production (cwt), value | ~20 counties |
| **Cucumbers** (fresh, processing) | Area harvested, production (cwt), value | ~80 counties |
| **Bell peppers** | Area harvested, production (cwt), value | ~60 counties |
| **Sweet corn** (fresh, processing) | Area harvested, production (tons, cwt), value | ~200 counties |
| **Green peas** (fresh, processing) | Area harvested, production (tons, cwt), value | ~50 counties |
| **Snap beans** (fresh, processing) | Area harvested, production (cwt, tons), value | ~80 counties |
| **Watermelons** | Area harvested, production (cwt), value | ~150 counties |

**Note:** Most vegetable data is state-level; county-level limited to major producing areas

### 2.4 FRUITS & TREE NUTS - Annual Surveys (~500 variables)

#### Fruit Trees
| Fruit | Data Items | County Coverage |
|-------|------------|-----------------|
| **Apples** | Bearing/non-bearing acres, production (lbs), utilized production, price, value | ~400 counties |
| **Cherries** (sweet, tart) | Bearing/non-bearing acres, production (lbs, tons), price, value | ~200 counties |
| **Peaches** | Bearing/non-bearing acres, production (lbs), utilized production, value | ~250 counties |
| **Pears** | Bearing/non-bearing acres, production (lbs), value | ~150 counties |
| **Grapes** (all purposes, wine, table, raisin) | Bearing/non-bearing acres, production (tons), price, value | ~400 counties (CA primarily) |
| **Citrus** (oranges, grapefruit, lemons, tangerines) | Bearing/non-bearing acres, production (boxes, lbs), value | ~150 counties (CA, FL, TX, AZ) |

#### Tree Nuts
| Nut | Data Items | County Coverage |
|-----|------------|-----------------|
| **Almonds** | Bearing/non-bearing acres, production (lbs, shelled basis), price, value | ~50 counties (CA) |
| **Walnuts** (English) | Bearing/non-bearing acres, production (lbs, in-shell), value | ~40 counties (CA) |
| **Pecans** (improved, native/seedling) | Bearing/non-bearing acres, production (lbs, in-shell), value | ~300 counties (GA, TX, NM, others) |
| **Pistachios** | Bearing/non-bearing acres, production (lbs), value | ~20 counties (CA) |
| **Hazelnuts** | Bearing/non-bearing acres, production (lbs, in-shell), value | ~10 counties (OR) |

#### Berries
| Berry | Data Items | County Coverage |
|-------|------------|-----------------|
| **Strawberries** | Harvested acres, production (lbs), price, value | ~200 counties |
| **Blueberries** (cultivated, wild) | Bearing/non-bearing acres, production (lbs), value | ~200 counties |
| **Cranberries** | Bearing/non-bearing acres, production (barrels, lbs), value | ~20 counties (WI, MA, NJ, OR, WA) |
| **Raspberries** | Bearing/non-bearing acres, production (lbs), value | ~100 counties |

---

## 🐄 PROGRAM 3: SURVEY - ANNUAL LIVESTOCK SURVEYS (~1,500 variables)

### 3.1 CATTLE & CALVES (~300 county-level variables)

**Annual Inventory (January 1):**
| Category | Data Items | County Coverage |
|----------|------------|-----------------|
| All cattle & calves | Inventory (head) | ~2,800 counties |
| Beef cows | Inventory (head) | ~2,800 counties |
| Milk cows | Inventory (head) | ~2,000 counties |
| Cattle on feed | Inventory (head) | ~400 counties (major feeding areas) |
| Heifers 500+ lbs | Inventory (head) | State-level primarily |
| Steers 500+ lbs | Inventory (head) | State-level primarily |
| Bulls | Inventory (head) | State-level primarily |
| Calves under 500 lbs | Inventory (head) | State-level primarily |

**Annual Production:**
- Calf crop (head)
- Cattle on feed placements (head, quarterly)
- Cattle on feed marketings (head, quarterly)

**Price Received:**
- Cattle, price received ($/cwt) - monthly, state-level
- Calves, price received ($/cwt) - monthly, state-level

**Data Sources:** Cattle Inventory (January), Cattle on Feed (monthly), monthly prices

### 3.2 HOGS & PIGS (~150 county-level variables)

**Quarterly Inventory:**
| Category | Data Items | County Coverage |
|----------|------------|-----------------|
| All hogs & pigs | Inventory (head) | ~1,500 counties |
| Breeding hogs | Inventory (head) | ~1,500 counties |
| Market hogs | Inventory (head) | ~1,500 counties |

**Quarterly Production:**
- Pigs per litter
- Litters farrowed

**Price Received:**
- Hogs, price received ($/cwt) - monthly, state-level

**Data Sources:** Quarterly Hogs & Pigs Report

### 3.3 SHEEP & LAMBS (~80 county-level variables)

**Annual Inventory (January 1):**
| Category | Data Items | County Coverage |
|----------|------------|-----------------|
| All sheep & lambs | Inventory (head) | ~1,200 counties |
| Breeding ewes | Inventory (head) | ~1,200 counties |
| Market sheep | Inventory (head) | State-level primarily |

**Production:**
- Lamb crop (head)
- Wool production (lbs)

**Price Received:**
- Sheep, price received ($/cwt)
- Lambs, price received ($/cwt)
- Wool, price received ($/lb)

### 3.4 GOATS (~40 county-level variables)

**Annual Inventory (January 1):**
- All goats (head)
- Meat & other goats (head)
- Milk goats (head)
- Angora goats (head)

**Production:**
- Mohair production (lbs) - TX primarily

**Data Sources:** Sheep & Goats Report

### 3.5 POULTRY - Annual Surveys (~200 variables)

#### Chickens - Layers
| Category | Data Items | Geographic Level |
|----------|------------|------------------|
| Layers 20+ weeks old | Inventory (head) | State-level |
| Pullets 13-19 weeks | Inventory (head) | State-level |
| Egg production | Dozens, cases | State-level |
| Eggs per layer | Rate | State-level |

#### Chickens - Broilers
| Category | Data Items | Geographic Level |
|----------|------------|------------------|
| Broilers produced | Head | County-level: ~400 counties (major states: AR, GA, AL, NC, MS, etc.) |
| Broilers, value of production | $ | County-level in major states |

#### Turkeys
| Category | Data Items | Geographic Level |
|----------|------------|------------------|
| Turkeys raised | Head | State-level primarily; county in major states |
| Turkeys, value of production | $ | State-level |

**Data Sources:** Chickens & Eggs Report, Poultry - Production & Value

### 3.6 DAIRY - Monthly & Annual Surveys (~250 variables)

**Monthly Production:**
| Data Item | Geographic Level |
|-----------|------------------|
| Milk production | State-level (lbs, all cows) |
| Milk per cow | State-level (lbs) |
| Number of milk cows | State-level (head) |

**Annual Summary:**
- County-level milk production (lbs) - available for ~1,000 dairy counties
- County-level milk cow inventory (head)

**Price Received:**
- All milk, price received ($/cwt) - monthly, state-level
- Milk eligible for fluid market ($/cwt)

**Data Sources:** Milk Production (monthly), Dairy Products (monthly)

### 3.7 HONEY & BEES (~60 variables)

**Annual Inventory & Production:**
| Data Item | Geographic Level |
|-----------|------------------|
| Honey bee colonies | State-level (count) |
| Honey production | State-level (lbs) |
| Yield per colony | State-level (lbs) |
| Value of production | State-level ($) |
| Price per lb | State-level ($/lb) |

**Census:** County-level bee colonies and honey production available in Census of Agriculture years

### 3.8 AQUACULTURE (~40 variables)

**Annual Sales:**
- Catfish sales (lbs, $) - state-level; county-level in major states (MS, AL, AR)
- Trout sales (lbs, $) - state-level
- Other aquaculture ($/sales) - state-level

**Data Sources:** Catfish Production, Trout Production, Aquaculture (Census)

---

## 📅 PROGRAM 4: SURVEY - MONTHLY CROP REPORTS (~800 variables)

### 4.1 CROP PROGRESS & CONDITION

**State-level weekly/monthly reports:**
- Crop progress (% planted, emerged, bloomed, mature, harvested) by week
- Crop condition (% excellent, good, fair, poor, very poor) by week
- Soil moisture (% very short, short, adequate, surplus)

**Crops Covered:**
- Corn, soybeans, wheat, cotton, sorghum, barley, oats, rice, peanuts, sunflower, canola, sugarbeets, potatoes, tobacco

**Data Items per Crop:**
- Planted: % complete by week
- Emerged: % complete
- Progress to key stages (silking, blooming, boll opening, etc.)
- Condition ratings (5 categories) by week
- Harvested: % complete by week

**Time Series:** Weekly during growing season (typically May-October)

**Total Variables:** ~500 state-level weekly data points × crops

### 4.2 MONTHLY PRODUCTION FORECASTS

**Crop Production Report (monthly):**
- Planted acreage forecasts (June)
- Harvested acreage forecasts (August, September, October)
- Production forecasts (August through January)
- Yield forecasts (August through January)

**Updated Monthly** for major crops from August harvest through final January estimates

### 4.3 MONTHLY LIVESTOCK PRODUCTION

**Cattle on Feed:**
- On feed inventory (head) - monthly, state-level (major states only)
- Placements (head) - monthly
- Marketings (head) - monthly

**Milk Production:**
- Monthly milk production (lbs) - state-level
- Number of cows - monthly, state-level
- Production per cow - monthly, state-level

**Chickens & Eggs:**
- Monthly egg production (dozens) - state-level
- Layers inventory - monthly, state-level

**Turkeys:**
- Poults placed for market - monthly, state-level
- Number raised - monthly, state-level

**Total Monthly Livestock Variables:** ~300 state-level time series

---

## 💰 PROGRAM 5: PRICES RECEIVED & PAID (~1,200 variables)

### 5.1 PRICES RECEIVED BY FARMERS

**Monthly Price Surveys:**

#### Crop Prices (Monthly, State-Level)
| Crop | Price Unit | States Reporting |
|------|------------|------------------|
| Corn, grain | $/bushel | ~40 states |
| Soybeans | $/bushel | ~30 states |
| Wheat, all | $/bushel | ~40 states |
| Cotton, upland | cents/lb | ~15 states |
| Rice | $/cwt | ~6 states |
| Sorghum, grain | $/cwt | ~10 states |
| Barley | $/bushel | ~15 states |
| Oats | $/bushel | ~20 states |
| Hay, alfalfa | $/ton | ~40 states |
| Peanuts | cents/lb | ~10 states |
| Potatoes | $/cwt | ~15 states |
| Apples | cents/lb | ~10 states |

#### Livestock & Poultry Prices (Monthly, State-Level)
| Product | Price Unit | States Reporting |
|---------|------------|------------------|
| Cattle | $/cwt | ~40 states |
| Calves | $/cwt | ~40 states |
| Hogs | $/cwt | ~20 states |
| Sheep | $/cwt | ~20 states |
| Lambs | $/cwt | ~20 states |
| Milk, all | $/cwt | ~23 states |
| Eggs, market | cents/dozen | ~15 states |
| Broilers | cents/lb | ~10 states |
| Turkeys | cents/lb | ~8 states |
| Wool | cents/lb | ~10 states |

**Total Price Received Variables:** ~600 monthly state-level time series

### 5.2 PRICES PAID BY FARMERS (Indices)

**Monthly Price Indices (National):**
- Prices Paid Index (all items, 2011=100)
- Feed index
- Fertilizer index
- Fuels index
- Chemicals index
- Seeds index
- Livestock & poultry purchases index
- Machinery index
- Building materials index
- Interest index
- Wage rate index

**Total Prices Paid Variables:** ~50 national monthly indices

### 5.3 PARITY RATIOS

**Monthly National Ratios:**
- Parity ratio (prices received / prices paid)
- By commodity group

---

## 🌱 PROGRAM 6: ORGANIC SURVEY (~400 variables)

**Organic Certification Data (Annual):**

### 6.1 Organic Farms & Acreage
| Data Item | Geographic Level |
|-----------|------------------|
| Organic farms | State-level, county-level (major states) |
| Certified organic acres | State-level, county-level |
| Transitioning acres | State-level, county-level |
| Total organic & transitioning acres | State-level, county-level |

### 6.2 Organic Crop Production
**Major Crops with Organic Data:**
- Corn (grain, silage)
- Soybeans
- Wheat
- Oats
- Hay (alfalfa, other)
- Vegetables (carrots, lettuce, tomatoes, etc.)
- Fruits (apples, berries, grapes)
- Specialty crops

**Data Items per Crop:**
- Farms with organic production
- Organic acres harvested
- Organic production (bushels, tons, lbs)
- Value of organic sales ($)

### 6.3 Organic Livestock & Poultry
| Commodity | Data Items |
|-----------|------------|
| Organic milk cows | Inventory (head), milk production (lbs), farms |
| Organic beef cows | Inventory (head), farms |
| Organic hogs | Inventory (head), farms |
| Organic layers | Inventory (head), egg production, farms |
| Organic broilers | Production (head), farms |

**Geographic Level:** Primarily state-level; county-level in Census years

**Data Source:** Certified Organic Survey (annual since 2008)

---

## 🌿 PROGRAM 7: ENVIRONMENTAL & SPECIALTY SURVEYS (~300 variables)

### 7.1 Chemical Use Surveys

**Periodic Surveys (every 3-5 years):**
| Crop | Data Items |
|------|------------|
| Corn | Acres treated with specific pesticides (herbicides, insecticides, fungicides), application rates, timing |
| Soybeans | " |
| Wheat | " |
| Cotton | " |
| Potatoes | " |
| Apples | " |

**Data Reported:**
- % acres treated
- Lbs active ingredient applied
- Applications per acre
- Application timing

**Geographic Level:** State-level; national estimates

**Note:** See companion catalog **USGS_PESTICIDES_COMPLETE_COMPOUND_LIST.md** for county-level pesticide use estimates (EPest)

### 7.2 Farm Labor

**Quarterly Farm Labor Survey:**
| Data Item | Geographic Level |
|-----------|------------------|
| Hired workers (number) | State-level, regional |
| Wage rates ($/hour) | State-level, regional |
| Hours worked | State-level, regional |

**Worker Types:**
- Field workers
- Livestock workers
- All hired workers

### 7.3 Agricultural Land Values

**Annual Land Value Survey:**
| Data Item | Geographic Level |
|-----------|------------------|
| Cropland value | $/acre, state-level |
| Pasture value | $/acre, state-level |
| Farm real estate value | $/acre, state-level |

**Cash Rents:**
- Cropland cash rent ($/acre)
- Pasture cash rent ($/acre)

---

## 🔍 HOW TO USE QUICKSTATS FOR COUNTY-LEVEL RESEARCH

### R Example: Query QuickStats API

```r
library(tidyverse)
library(tidyUSDA)
library(httr)
library(jsonlite)

# Get API key: https://quickstats.nass.usda.gov/api
api_key <- "YOUR_API_KEY_HERE"

# Example 1: Get corn harvested acres for all counties (2022)
corn_acres <- getQuickstat(
  key = api_key,
  program = "SURVEY",
  commodity_desc = "CORN",
  short_desc = "CORN, GRAIN - ACRES HARVESTED",
  year = 2022,
  agg_level = "COUNTY"
)

# Clean and format
corn_acres_clean <- corn_acres %>%
  mutate(
    fips = paste0(str_pad(state_fips_code, 2, pad = "0"),
                  str_pad(county_code, 3, pad = "0")),
    acres = as.numeric(gsub(",", "", Value))
  ) %>%
  filter(!is.na(acres)) %>%
  select(fips, state_name, county_name, acres, year)

# Example 2: Get cattle inventory for Travis County, TX (time series)
travis_cattle <- getQuickstat(
  key = api_key,
  program = "SURVEY",
  commodity_desc = "CATTLE",
  short_desc = "CATTLE, INCL CALVES - INVENTORY",
  year = 2010:2023,
  state_alpha = "TX",
  county_name = "TRAVIS"
)

# Example 3: Get multiple crops for a county
travis_crops <- getQuickstat(
  key = api_key,
  program = "SURVEY",
  commodity_desc = c("CORN", "WHEAT", "SORGHUM", "HAY"),
  statisticcat_desc = "AREA HARVESTED",
  year = 2022,
  state_alpha = "TX",
  county_name = "TRAVIS",
  agg_level = "COUNTY"
)

# Example 4: Get Census + Survey data combined
ag_data_combined <- getQuickstat(
  key = api_key,
  program = c("CENSUS", "SURVEY"),
  year = c(2022),
  state_alpha = "TX",
  county_name = "TRAVIS",
  agg_level = "COUNTY"
)

# Export
write_csv(corn_acres_clean, "us_county_corn_acres_2022.csv")
```

### Python Example: Query QuickStats API

```python
import requests
import pandas as pd
import numpy as np

# API configuration
api_key = "YOUR_API_KEY_HERE"
base_url = "https://quickstats.nass.usda.gov/api/api_GET/"

# Example 1: Get soybean production for all counties (2022)
params = {
    "key": api_key,
    "commodity_desc": "SOYBEANS",
    "short_desc": "SOYBEANS - PRODUCTION, MEASURED IN BU",
    "year": 2022,
    "agg_level_desc": "COUNTY",
    "format": "JSON"
}

response = requests.get(base_url, params=params)
data = response.json()
df_soybeans = pd.DataFrame(data['data'])

# Create FIPS code
df_soybeans['fips'] = (
    df_soybeans['state_fips_code'].astype(str).str.zfill(2) +
    df_soybeans['county_code'].astype(str).str.zfill(3)
)

# Clean value column
df_soybeans['production_bu'] = (
    df_soybeans['Value']
    .str.replace(',', '')
    .replace('(D)', np.nan)  # Suppressed data
    .astype(float)
)

# Example 2: Get livestock inventory for multiple commodities
livestock_params = {
    "key": api_key,
    "source_desc": "SURVEY",
    "commodity_desc": "CATTLE",
    "statisticcat_desc": "INVENTORY",
    "year": 2023,
    "state_alpha": "TX",
    "county_name": "TRAVIS",
    "format": "JSON"
}

livestock_response = requests.get(base_url, params=livestock_params)
livestock_data = pd.DataFrame(livestock_response.json()['data'])

# Example 3: Time series for county
def get_county_timeseries(api_key, state, county, commodity, data_item, years):
    """Get time series data for a specific county."""

    params = {
        "key": api_key,
        "source_desc": "SURVEY",
        "commodity_desc": commodity,
        "short_desc": data_item,
        "year": ",".join(map(str, years)),
        "state_alpha": state,
        "county_name": county,
        "agg_level_desc": "COUNTY",
        "format": "JSON"
    }

    response = requests.get(base_url, params=params)

    if response.status_code == 200:
        data = response.json()
        if 'data' in data:
            df = pd.DataFrame(data['data'])
            return df[['year', 'Value', 'short_desc', 'county_name']]
    return pd.DataFrame()

# Get corn acres for Travis County 2010-2023
travis_corn = get_county_timeseries(
    api_key=api_key,
    state="TX",
    county="TRAVIS",
    commodity="CORN",
    data_item="CORN, GRAIN - ACRES HARVESTED",
    years=range(2010, 2024)
)

# Export
df_soybeans.to_csv("us_county_soybean_production_2022.csv", index=False)
travis_corn.to_csv("travis_county_corn_acres_timeseries.csv", index=False)
```

### Advanced Query: Aggregate to County from Multiple Data Items

```r
# Function to get comprehensive county agricultural profile
get_county_ag_profile <- function(state_fips, county_fips, year = 2022) {

  # Construct county filter
  state_name <- tigris::fips_codes %>%
    filter(state_code == state_fips) %>%
    pull(state_name) %>%
    unique()

  county_name_lookup <- tigris::fips_codes %>%
    filter(state_code == state_fips, county_code == county_fips) %>%
    pull(county)

  # Query multiple commodity groups
  crops <- getQuickstat(
    key = api_key,
    program = "SURVEY",
    sector_desc = "CROPS",
    statisticcat_desc = "AREA HARVESTED",
    year = year,
    state_alpha = state_name,
    county_name = county_name_lookup,
    agg_level = "COUNTY"
  )

  livestock <- getQuickstat(
    key = api_key,
    program = "SURVEY",
    sector_desc = "ANIMALS & PRODUCTS",
    statisticcat_desc = "INVENTORY",
    year = year,
    state_alpha = state_name,
    county_name = county_name_lookup,
    agg_level = "COUNTY"
  )

  # Combine and summarize
  profile <- bind_rows(
    crops %>% mutate(category = "Crops"),
    livestock %>% mutate(category = "Livestock")
  ) %>%
    mutate(
      fips = paste0(str_pad(state_fips_code, 2, pad = "0"),
                    str_pad(county_code, 3, pad = "0")),
      value_numeric = as.numeric(gsub(",", "", Value))
    ) %>%
    select(fips, county_name, category, commodity_desc,
           short_desc, value_numeric, unit_desc)

  return(profile)
}

# Example usage
travis_profile <- get_county_ag_profile(state_fips = "48", county_fips = "453")
```

---

## 📚 COMPANION DATA SOURCES

### USDA ERS County-Level Data Sets
**URL:** https://www.ers.usda.gov/data-products/county-level-data-sets/

**Description:** Economic Research Service county-level datasets
- Farm income & wealth
- Farm structure & organization
- Agricultural resource management
- Complements NASS production & price data

### USDA RMA Crop Insurance Data
**URL:** https://www.rma.usda.gov/SummaryOfBusiness

**Description:** Federal crop insurance statistics
- Insured acres by crop & county
- Indemnities paid
- Loss ratios
- Premium rates
- Complements NASS crop production data

### USGS EPest Pesticide Use Estimates
**URL:** https://water.usgs.gov/nawqa/pnsp/usage/maps/

**Description:** County-level pesticide use estimates
- Derived from NASS Agricultural Resource Management Survey (ARMS)
- 650+ pesticide compounds
- Annual county estimates (kg applied)
- See **USGS_PESTICIDES_COMPLETE_COMPOUND_LIST.md**

### USDA FSA Conservation Programs
**URL:** https://www.fsa.usda.gov/programs-and-services/conservation-programs/

**Description:** Conservation program enrollment & payments
- Conservation Reserve Program (CRP) acres & payments
- Environmental Quality Incentives Program (EQIP)
- County-level enrollment

---

## 📝 CITATION

**Recommended Citation Format:**

U.S. Department of Agriculture, National Agricultural Statistics Service, 2024. Quick Stats Database. Available online at https://quickstats.nass.usda.gov/. Accessed [date].

**For Specific Surveys:**

U.S. Department of Agriculture, National Agricultural Statistics Service, [Year]. [Survey Name] (e.g., "Crop Production"). Available online at https://www.nass.usda.gov/Publications/. Accessed [date].

---

## 🔗 RELATED TIER 1 & TIER 2 DOCUMENTATION

### Tier 2 Complete Catalogs:
**[USDA_AG_CENSUS_COMPLETE_TABLES.md](USDA_AG_CENSUS_COMPLETE_TABLES.md)**
- Complete 77-table structure for Census of Agriculture
- ~6,000 Census variables detailed

### Tier 1 Comprehensive Documentation:
**[GREEN_PEST_OCC_VECTOR_SOCIAL_COMPREHENSIVE.md](GREEN_PEST_OCC_VECTOR_SOCIAL_COMPREHENSIVE.md)**
- Section on "USDA NASS Agricultural Data"
- Integration with environmental health research
- Agricultural exposures and health outcomes

---

## 📌 NOTES ON QUICKSTATS STRUCTURE

### Data Item Suffixes
Common patterns in `short_desc`:
- **"- ACRES PLANTED":** Total acres planted
- **"- ACRES HARVESTED":** Acres actually harvested
- **"- PRODUCTION, MEASURED IN [UNIT]":** Total production
- **"- YIELD, MEASURED IN [UNIT] / ACRE":** Yield per acre
- **"- INVENTORY":** Livestock head count on specific date
- **"- SALES, MEASURED IN $":** Market value of sales
- **"- PRICE RECEIVED, MEASURED IN $ / [UNIT]":** Price per unit

### Domain Categories
Common domains for subsetting data:
- **TOTAL:** All farms/operations
- **IRRIGATED:** Irrigated subset only
- **NON-IRRIGATED:** Non-irrigated subset
- **ORGANIC STATUS: (CERTIFIED ORGANIC):** Certified organic operations
- **ECONOMIC CLASS:** By farm sales class
- **AREA OPERATED:** By farm size (acres)
- **NAICS CLASSIFICATION:** By industry classification

### Geographic Levels
| Agg Level | Description | Typical Use |
|-----------|-------------|-------------|
| NATIONAL | US total | Overall production, prices |
| REGION | Multi-state regions | Regional comparisons |
| STATE | Individual states | State production, prices |
| AG DISTRICT | State agricultural districts | Sub-state analysis |
| COUNTY | Individual counties | Local production, research |
| ZIP CODE | ZIP code areas | Specialty crops, Census variables |

### Missing Data Codes
- **(D):** Withheld to avoid disclosing data for individual operations
- **(Z):** Less than half the unit shown
- **(NA):** Not available
- **Blank:** Data not collected for this combination

### County Data Availability
**High Coverage (>2,000 counties):**
- Census variables (all counties)
- Corn, soybeans, wheat, hay (major crops)
- Cattle, beef cows, milk cows (livestock)

**Moderate Coverage (500-2,000 counties):**
- Cotton, sorghum, barley, oats, peanuts
- Hogs, broilers (in major producing states)
- Fruits, vegetables (major producing regions)

**Limited Coverage (<500 counties):**
- Specialty crops (citrus, tree nuts, specific vegetables)
- Organic production (primarily state-level)
- Prices (primarily state-level)

### Query Optimization Tips
1. **Start broad, filter narrow:** Query by commodity first, then add filters
2. **Use `short_desc` for precision:** More specific than separate commodity + data item
3. **Check `statisticcat_desc`:** Groups data items (AREA, PRODUCTION, INVENTORY, YIELD, etc.)
4. **Mind the rate limit:** 1,000 API calls per minute
5. **Cache results:** QuickStats data changes infrequently (annual updates)

---

**Document Version:** 1.0
**Last Updated:** 2024
**Maintainer:** USDA National Agricultural Statistics Service

**Total Documented Variables:** 10,000+
**Programs:** 7 (Census, Survey-Crops, Survey-Livestock, Monthly, Prices, Organic, Environmental)
**Official Source:** https://quickstats.nass.usda.gov/
