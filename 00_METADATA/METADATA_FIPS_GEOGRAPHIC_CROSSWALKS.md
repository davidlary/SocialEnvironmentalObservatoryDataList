# Geographic Metadata, FIPS Codes, and Crosswalks
## Essential Reference for US County-Level Data Collection

**Last Updated:** November 12, 2025
**Purpose:** Comprehensive documentation of geographic identifiers, boundary changes, and crosswalks for county-level data integration
**Critical for:** Data collection, temporal analysis across decades, spatial aggregation

---

## TABLE OF CONTENTS

1. [County FIPS Codes Structure](#county-fips-codes-structure)
2. [FIPS Code Changes Over Time](#fips-code-changes-over-time)
3. [Geographic Boundary Files](#geographic-boundary-files)
4. [Redistricting & Boundary Changes](#redistricting--boundary-changes)
5. [Geographic Crosswalks](#geographic-crosswalks)
6. [Population Denominators](#population-denominators)
7. [Special Geographic Cases](#special-geographic-cases)
8. [Data Collection Best Practices](#data-collection-best-practices)

---

## COUNTY FIPS CODES STRUCTURE

### Standard County FIPS Format

**Structure:** 5-digit code = 2-digit state FIPS + 3-digit county FIPS

**Example:**
- **17031** = Illinois (17) + Cook County (031)
- **06037** = California (06) + Los Angeles County (037)
- **48201** = Texas (48) + Harris County (201)

### Complete US County Universe

**Total Counties:** 3,143 county or county-equivalent jurisdictions (as of 2020)

**Breakdown:**
- **3,006** actual counties
- **64** Louisiana parishes
- **19** Alaska boroughs + 11 Census Areas (= 30 total)
- **42** Virginia independent cities (county equivalents)
- **1** Washington DC (11001 = District of Columbia)

**State FIPS Codes (01-56):**
```
01 = Alabama          02 = Alaska           04 = Arizona
05 = Arkansas         06 = California       08 = Colorado
09 = Connecticut      10 = Delaware         11 = DC
12 = Florida          13 = Georgia          15 = Hawaii
16 = Idaho            17 = Illinois         18 = Indiana
19 = Iowa             20 = Kansas           21 = Kentucky
22 = Louisiana        23 = Maine            24 = Maryland
25 = Massachusetts    26 = Michigan         27 = Minnesota
28 = Mississippi      29 = Missouri         30 = Montana
31 = Nebraska         32 = Nevada           33 = New Hampshire
34 = New Jersey       35 = New Mexico       36 = New York
37 = North Carolina   38 = North Dakota     39 = Ohio
40 = Oklahoma         41 = Oregon           42 = Pennsylvania
44 = Rhode Island     45 = South Carolina   46 = South Dakota
47 = Tennessee        48 = Texas            49 = Utah
50 = Vermont          51 = Virginia         53 = Washington
54 = West Virginia    55 = Wisconsin        56 = Wyoming

Note: 03, 07, 14, 43, 52 are not used (historical reasons)
```

### County FIPS Within States

**Format:** 001 to 999 (odd numbers only in some states like New Mexico)

**Examples:**
- California: 001 (Alameda) to 115 (Yuba) - 58 counties
- Texas: 001 (Anderson) to 507 (Zavala) - 254 counties
- Alaska: 013 (Aleutians East) to 290 (Yukon-Koyukuk) - 30 boroughs/census areas

**Special Notes:**
- Not all 3-digit codes from 001-999 are used (gaps exist)
- Some states use only odd numbers (e.g., New Mexico)
- Independent cities (Virginia) have their own FIPS codes separate from surrounding counties

---

## FIPS CODE CHANGES OVER TIME

### Major FIPS Changes Since 1970

**CRITICAL:** FIPS codes can change due to:
1. County mergers/consolidations
2. County splits (rare)
3. County name changes (FIPS may change or stay same)
4. New counties created
5. Alaska Census Area reorganizations

### Notable FIPS Changes (1990-2020)

#### **Alaska (Frequent Changes):**

**2007-2008 Census Area Reorganization:**
- **Wrangell-Petersburg Census Area** (02280) → SPLIT into:
  - Wrangell City and Borough (02275) - NEW
  - Petersburg Census Area (02195) - NEW
- **Skagway-Hoonah-Angoon Census Area** (02232) → SPLIT into:
  - Skagway Municipality (02230) - NEW
  - Hoonah-Angoon Census Area (02105) - NEW

**2013 Census Area Creation:**
- **Kusilvak Census Area** (02158) - NEW (carved from Wade Hampton Census Area)
- **Wade Hampton Census Area** (02270) → RENAMED to **Kusilvak Census Area** (02158) [FIPS changed]

**Impact:** Time-series data 1990-2024 must account for Alaska boundary/FIPS changes

---

#### **Virginia Independent Cities (Consolidations):**

**1995: Clifton Forge City Reverts to Town:**
- **51560 Clifton Forge City** → Merged into Alleghany County (51005)
- Date: July 1, 1995

**2001: South Boston City Reverts:**
- **51780 South Boston City** → Merged into Halifax County (51083)
- Date: July 1, 1995

**2013: Bedford City Reverts:**
- **51515 Bedford City** → Merged into Bedford County (51019)
- Date: July 1, 2013

**Impact:** Historical mortality/health data before merger dates need city + county aggregated for consistent time series

---

#### **Colorado (County Creation):**

**2001: Broomfield County Created:**
- **08014 Broomfield County** - NEW (November 15, 2001)
- Carved from parts of: Adams (08001), Boulder (08013), Jefferson (08059), Weld (08123)

**Impact:** Pre-2001 data for Broomfield must be aggregated from source counties

---

#### **Montana (Name/FIPS Change):**

**1997: Big Horn County FIPS Change:**
- **30009** (old FIPS) → NO CHANGE (false alarm, no actual FIPS change)

---

#### **New Mexico (Cibola County Creation):**

**1981: Cibola County Created:**
- **35006 Cibola County** - NEW (June 19, 1981)
- Carved from Valencia County (35061)

**Impact:** Pre-1981 data for Cibola must be aggregated from Valencia County

---

### **Comprehensive FIPS Change Tracking**

**Official Source:**
- **Census Bureau County Boundary Changes:** https://www.census.gov/geo/reference/county-changes.html
- **FIPS 6-4 Updates:** NIST maintains historical FIPS code changes

**Download:**
```r
# Census Bureau county equivalency file (crosswalk for mergers/splits)
county_equivalents <- read_csv("https://www2.census.gov/geo/docs/reference/county_adjacency.txt")
```

---

## GEOGRAPHIC BOUNDARY FILES

### Official Sources (Census Bureau TIGER/Line)

**TIGER/Line Shapefiles - Annual Release**

**URL:** https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

**Key Files for County-Level Work:**

1. **Counties (National File):**
   - `tl_YYYY_us_county.zip` (e.g., `tl_2020_us_county.zip`)
   - **Contains:** All 3,143 county boundaries (polygons)
   - **Attributes:** STATEFP, COUNTYFP, GEOID (5-digit FIPS), NAME, NAMELSAD, ALAND (land area), AWATER (water area)

2. **States (National File):**
   - `tl_YYYY_us_state.zip`
   - **Contains:** 50 states + DC + territories

3. **Census Tracts (by State):**
   - `tl_YYYY_SS_tract.zip` (SS = 2-digit state FIPS)
   - **Aggregation:** Tracts → Counties (first 5 digits of tract GEOID = county FIPS)

4. **ZIP Code Tabulation Areas (ZCTAs):**
   - `tl_YYYY_us_zcta520.zip`
   - **Note:** ZCTAs ≠ USPS ZIP codes (statistical approximation)
   - **Crosswalk Required:** ZCTA → County (many-to-many relationship)

5. **Places (Cities/Towns):**
   - `tl_YYYY_SS_place.zip`
   - **Crosswalk Required:** Place → County (places can span multiple counties)

### Historical Boundaries (Decennial)

**NHGIS (National Historical Geographic Information System):**
- **URL:** https://www.nhgis.org/
- **Contains:** County boundaries for every decennial census (1790-2020)
- **Use:** Time-consistent boundary definitions for longitudinal analysis

**Download Example:**
```r
library(ipumsr)

# NHGIS county boundaries for 2000, 2010, 2020 (to assess boundary changes)
nhgis_data <- get_ipums_nhgis_data(
  dataset = "2020_county_boundaries",
  download_type = "gis"
)
```

### Coordinate Reference Systems (CRS)

**Standard CRS for US County Work:**

1. **WGS 84 (EPSG:4326)** - Geographic (lat/lon)
   - Use for: Joining with GPS data, international datasets
   - Example: `st_transform(counties, crs = 4326)`

2. **NAD83 (EPSG:4269)** - US Standard Geographic
   - Use for: Census data (TIGER/Line native CRS)

3. **Albers Equal Area (EPSG:5070)** - US Contiguous + Alaska + Hawaii
   - Use for: Area calculations, spatial statistics
   - Example: `st_transform(counties, crs = 5070)`

4. **Web Mercator (EPSG:3857)** - Web Maps
   - Use for: Leaflet, Mapbox, Google Maps overlays

**Recommendation:** Work in Albers Equal Area (EPSG:5070) for US county analysis (preserves area, good for all US states including Alaska/Hawaii)

---

## REDISTRICTING & BOUNDARY CHANGES

### Census Redistricting Cycles

**Major Boundary Updates:** Occur with each decennial census (2000, 2010, 2020)

**Types of Changes:**
1. **County boundaries:** Rare (only with legislative action)
2. **Census tract boundaries:** Common (redrawn every 10 years)
3. **Block group boundaries:** Very common
4. **Block boundaries:** Change significantly

### Handling Decadal Boundary Changes

**Problem:** Environmental exposure data (e.g., EPA monitor locations, TRI facilities) may fall in different tracts/counties across decades due to boundary shifts.

**Solution: Time-Consistent Geographic Units**

#### **Method 1: Use 2020 Boundaries for All Years**
- Spatially join historical point data (1990-2024) to 2020 county boundaries
- **Advantage:** Consistent geographic units
- **Disadvantage:** Doesn't reflect historical boundaries (e.g., Broomfield County didn't exist pre-2001)

#### **Method 2: Use Period-Specific Boundaries**
- 1990 data → 1990 boundaries
- 2000 data → 2000 boundaries
- 2010 data → 2010 boundaries
- 2020 data → 2020 boundaries
- **Advantage:** Historically accurate
- **Disadvantage:** Time series comparisons require boundary crosswalks

#### **Method 3: Longitudinal Tract Database (LTDB) - RECOMMENDED**

**Brown University LTDB:**
- **URL:** https://s4.ad.brown.edu/projects/diversity/Researcher/Bridging.htm
- **Contains:** Census tract-level crosswalks 1970-2020
- **Function:** Normalize all decades to 2010 or 2020 tract boundaries

**Use Case:** Aggregate tract-level data to consistent county boundaries across time

```r
library(tidyverse)

# Download LTDB crosswalk (2000 tracts → 2010 tracts)
ltdb_2000to2010 <- read_csv("https://s4.ad.brown.edu/projects/diversity/Researcher/LTBDDload/crosswalks/ltdb_std_2000_fullcount.csv")

# Aggregate 2000 tract data to 2010 boundaries
data_2000_normalized <- data_2000 %>%
  left_join(ltdb_2000to2010, by = "TRTID00") %>%
  group_by(TRTID10) %>%
  summarize(
    # Weight by population or housing units
    variable_2010boundary = weighted.mean(variable_2000, weight = POP00, na.rm = TRUE)
  )
```

---

## GEOGRAPHIC CROSSWALKS

### ZIP Code → County

**Problem:** ZIP codes (USPS delivery routes) don't align with county boundaries

**Solutions:**

#### **1. HUD-USPS ZIP-County Crosswalk (Quarterly)**

**Source:** HUD
**URL:** https://www.huduser.gov/portal/datasets/usps_crosswalk.html
**Frequency:** Quarterly updates
**Format:** Excel, CSV

**Variables:**
- ZIP code (5-digit)
- County FIPS (5-digit)
- Residential ratio (% of ZIP's residential addresses in county)
- Business ratio
- Other ratio
- Total ratio

**Use Case:** Allocate ZIP-level data to counties based on residential ratio

**Example:**
```r
library(tidyverse)

# Download Q3 2024 ZIP-County crosswalk
zip_county <- read_csv("https://www.huduser.gov/portal/datasets/usps/ZIP_COUNTY_092024.csv")

# Allocate ZIP-level data to counties
data_county <- data_zip %>%
  left_join(zip_county, by = c("zip" = "ZIP")) %>%
  mutate(
    # Allocate ZIP value to county based on residential ratio
    value_allocated = value * RES_RATIO
  ) %>%
  group_by(COUNTY) %>%
  summarize(
    value_county = sum(value_allocated, na.rm = TRUE)
  )
```

#### **2. UDS Mapper ZIP-County Crosswalk**

**Source:** University of Wisconsin Population Health Institute
**URL:** https://www.udsmapper.org/zip-code-to-zcta-crosswalk/
**Contains:** ZIP → ZCTA → County crosswalk

---

### Census Tract → County

**Easy:** First 5 digits of 11-digit tract FIPS = county FIPS

**Example:**
- Tract FIPS: **17031841300**
  - State: **17** (Illinois)
  - County: **031** (Cook County)
  - Tract: **841300**
- County FIPS: **17031**

**R Code:**
```r
tracts <- tracts %>%
  mutate(
    county_fips = str_sub(GEOID, 1, 5)
  )
```

---

### Census Block Group → County

**Easy:** First 5 digits of 12-digit block group FIPS = county FIPS

**Example:**
- Block Group FIPS: **170318413001**
  - State: **17** (Illinois)
  - County: **031** (Cook County)
  - Tract: **841300**
  - Block Group: **1**
- County FIPS: **17031**

---

### Census Block → County

**Easy:** First 5 digits of 15-digit block FIPS = county FIPS

---

### Place (City/Town) → County

**Problem:** Places can span multiple counties (e.g., New York City spans 5 counties)

**Solution: Census Geographic Relationship Files**

**Source:** Census Bureau
**URL:** https://www.census.gov/geographies/reference-files/time-series/geo/relationship-files.html
**File:** `tab20_place20_county20.txt` (2020 example)

**Contains:**
- Place FIPS
- County FIPS
- Population in place-county intersection
- % of place population in county

**Example: Allocate New York City Data to 5 Boroughs:**
```r
# New York City (3651000) spans:
# 36005 (Bronx), 36047 (Kings/Brooklyn), 36061 (New York/Manhattan),
# 36081 (Queens), 36085 (Richmond/Staten Island)

place_county <- read_delim("https://www2.census.gov/geo/docs/maps-data/data/rel2020/place/tab20_place20_county20.txt", delim = "|")

nyc_allocation <- place_county %>%
  filter(PLACE_GEOID == "3651000") %>%
  mutate(
    # Allocate NYC data to 5 counties by population
    allocated_value = nyc_value * (PLACE_POP / sum(PLACE_POP))
  )
```

---

### ZCTA → Tract → County

**For Finer Spatial Join:**

**Census ZCTA-Tract Relationship File:**
- **URL:** https://www.census.gov/geographies/reference-files/time-series/geo/relationship-files.html
- **File:** `zcta_tract_rel_10.txt` (2010 example)

---

## POPULATION DENOMINATORS

### Annual County Population Estimates

**Census Bureau Population Estimates Program (PEP):**

**URL:** https://www.census.gov/programs-surveys/popest.html

**Datasets:**

1. **Vintage 2023 (Most Recent):**
   - **URL:** https://www2.census.gov/programs-surveys/popest/datasets/2020-2023/counties/totals/co-est2023-alldata.csv
   - **Years:** 2020-2023 (annual July 1 estimates)
   - **Variables:** Total population, births, deaths, migration (domestic, international)

2. **Vintage 2020 (Bridged to 2020 Census):**
   - **Years:** 2010-2020
   - **Use:** Consistent denominator for 2010-2020 decade

3. **Vintage 2010 (Bridged to 2010 Census):**
   - **Years:** 2000-2010
   - **Use:** Consistent denominator for 2000-2010 decade

4. **Vintage 2000 (Bridged to 2000 Census):**
   - **Years:** 1990-2000
   - **Use:** Consistent denominator for 1990-2000 decade

**Critical:** Use "vintage" estimates that are bridged to the most recent census for time series consistency.

---

### Population by Age, Race, Sex (Annual)

**Census Bureau PEP - Single Year of Age (SYOA):**

**URL:** https://www2.census.gov/programs-surveys/popest/datasets/2020-2023/counties/asrh/

**File Example:** `cc-est2023-syasex.csv`

**Variables:**
- Population by single year of age (0-85+)
- By sex (male, female)
- By race/ethnicity (total, Hispanic, NH White, NH Black, NH Asian, NH AIAN, NH NHPI)

**Use Case:** Age-standardized mortality rates, age-specific disease rates

---

### Intercensal Population Estimates (Between Censuses)

**NCHS Bridged-Race Population Estimates:**

**URL:** https://www.cdc.gov/nchs/nvss/bridged_race.htm

**Advantage:**
- NCHS-specific population estimates (used for CDC WONDER mortality rates)
- Bridged-race categories (consistent with death certificates)
- Single year of age, county-level, 1990-present

**Critical for Mortality Rates:** Always use NCHS bridged-race population denominators when calculating death rates from CDC WONDER data (ensures consistency with published CDC rates).

**Download:**
```r
# Example: 2020-2023 NCHS bridged-race estimates
nchs_pop <- read.delim("https://www.cdc.gov/nchs/nvss/bridged_race/data_documentation.htm")
```

---

## SPECIAL GEOGRAPHIC CASES

### Alaska Boroughs and Census Areas

**Structure:** Alaska has no counties; instead:
- **19 organized boroughs** (equivalent to counties)
- **11 Census Areas** (unorganized territories, Census-defined)

**FIPS Codes:** 02013 to 02290 (30 total)

**Challenges:**
- Census Area boundaries change between censuses (see FIPS changes section)
- Some areas are extremely large (Yukon-Koyukuk Census Area = 147,842 sq mi, larger than Montana)

**Recommendation:** For Alaska-specific analysis, consider aggregating to **Alaska Native Regional Corporations** or **Public Health Regions** instead of Census Areas.

---

### Virginia Independent Cities

**Structure:** Virginia has **42 independent cities** that are NOT part of any county (unique in US)

**FIPS Codes:** 51510-51840

**Challenges:**
- Independent cities have separate FIPS from surrounding counties
- Some datasets aggregate independent city data into surrounding counties (creates confusion)
- Historical consolidations (see FIPS changes section)

**Examples:**
- **51059** = Fairfax County
- **51600** = Fairfax City (independent, NOT in Fairfax County)
- **51013** = Arlington County
- **51760** = Richmond City (independent)

**Recommendation:** For Virginia analysis:
- Treat independent cities as separate county equivalents (42 + 95 counties = 137 total jurisdictions)
- Check if historical data merged city + county (especially for pre-1995 Clifton Forge, pre-2013 Bedford)

---

### Washington, DC (District of Columbia)

**FIPS Code:** **11001**

**Structure:** DC is both a city and a "county-equivalent" (no counties within DC)

**Census Designation:**
- State FIPS: **11**
- County FIPS: **001**
- Combined: **11001**

---

### Territories (Not in 3,143 Counties)

**Puerto Rico:** 78 municipios (municipalities) - separate FIPS codes (72001-72153)
**US Virgin Islands:** 3 islands - separate FIPS codes (78010, 78020, 78030)
**Guam, American Samoa, Northern Mariana Islands:** Separate FIPS

**Note:** Most federal datasets include territories, but many health datasets (CDC PLACES, County Health Rankings) do NOT. Clarify scope before assuming territory inclusion.

---

## DATA COLLECTION BEST PRACTICES

### 1. Always Use 5-Digit FIPS (Not Names)

**Why:** County names are not unique across states (30 "Washington" counties!)

**Example Ambiguity:**
- **Springfield:** Appears in 33+ states
- **Washington County:** 31 states have one

**Solution:** Always join data on FIPS code, not name.

---

### 2. Pad FIPS with Leading Zeros

**Problem:** Excel/CSV treats FIPS as numbers, drops leading zeros

**Examples:**
- **Alabama - Autauga County:** FIPS = **01001** → Excel converts to **1001** ❌
- **Alaska - Aleutians East:** FIPS = **02013** → Excel converts to **2013** ❌

**Solution:**
```r
# Read FIPS as character (not numeric)
data <- read_csv("file.csv", col_types = cols(FIPS = "c"))

# Or pad with leading zeros after reading
data <- data %>%
  mutate(FIPS = str_pad(FIPS, width = 5, side = "left", pad = "0"))
```

---

### 3. Check for FIPS Changes in Time Series

**Before Merging Multi-Year Data:**
1. Check if any counties merged/split during time period
2. Consult Census County Boundary Changes page
3. Aggregate historical data for merged counties (e.g., Virginia independent cities)

**Example: Broomfield County, CO:**
```r
# For 1990-2000 data, Broomfield (08014) didn't exist
# Allocate 2001+ Broomfield data back to Adams, Boulder, Jefferson, Weld?
# OR exclude Broomfield from 1990-2000 time series?
# OR use only 2001-2024 data?
```

---

### 4. Use Population-Weighted Centroids (Not Geographic Centroids)

**Problem:** Geographic centroid of county may be in unpopulated area (e.g., desert, lake)

**Solution:** Use Census population-weighted centroids

**Source:** Census Bureau TIGER/Line
**File:** `tl_2020_us_county.zip` (includes `INTPTLAT`, `INTPTLON` attributes = population-weighted centroids)

---

### 5. Handle Suppressed Data

**Small Count Suppression:** Many datasets suppress counties with <10 or <20 events (CDC WONDER, BLS, etc.)

**Strategies:**
1. Aggregate multiple years (if annual counts <10, try 3-year or 5-year aggregates)
2. Aggregate to larger geography (multi-county regions)
3. Use Bayesian spatial smoothing (borrow strength from neighbors)
4. Report as "suppressed" (do NOT impute with zero)

---

### 6. Verify Land vs. Total Area

**TIGER/Line Attributes:**
- **ALAND:** Land area (sq meters)
- **AWATER:** Water area (sq meters)

**Use Land Area for Density Calculations:**
```r
counties <- counties %>%
  mutate(
    land_area_sq_km = ALAND / 1e6,
    pop_density = population / land_area_sq_km
  )
```

**Why:** Including water area underestimates population density (e.g., Great Lakes counties)

---

### 7. Document Data Provenance

**For Every Variable, Record:**
- Source (agency, dataset name)
- Vintage (year of data, not download date)
- FIPS code vintage (2010 boundaries? 2020 boundaries?)
- Geographic scope (all 3,143 counties? excludes territories?)
- Suppression rules (suppressed if <10 events? <20?)
- Download date
- Processing steps (aggregation from tracts? allocation from ZIPs?)

---

## SUMMARY CHECKLIST

**Before Collecting County-Level Data:**

- [ ] Confirm data uses 5-digit FIPS codes (not names)
- [ ] Check for leading zero issues in FIPS codes
- [ ] Verify FIPS code vintage (2010? 2020?)
- [ ] Check for county mergers/splits during time period
- [ ] Identify suppression rules (small counts)
- [ ] Download appropriate population denominators (Census PEP vintage)
- [ ] Download county boundary file (TIGER/Line) for spatial joins
- [ ] Use population-weighted centroids (not geographic)
- [ ] Calculate density using land area (not total area)
- [ ] Document data provenance and processing steps

**For Spatial Analysis:**

- [ ] Transform to Albers Equal Area (EPSG:5070) for US analysis
- [ ] Use NHGIS historical boundaries if comparing across decades
- [ ] Use HUD ZIP-County crosswalk for ZIP-level data
- [ ] Use Census relationship files for place-county crosswalks
- [ ] Handle Alaska Census Areas carefully (boundary changes)
- [ ] Treat Virginia independent cities as separate county equivalents

---

**References:**

- Census Bureau Geographic Terms: https://www.census.gov/programs-surveys/geography.html
- FIPS Codes: https://www.census.gov/library/reference/code-lists/ansi.html
- TIGER/Line Shapefiles: https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html
- NHGIS: https://www.nhgis.org/
- HUD ZIP-County Crosswalk: https://www.huduser.gov/portal/datasets/usps_crosswalk.html
- NCHS Bridged-Race Population: https://www.cdc.gov/nchs/nvss/bridged_race.htm

---

**Version:** 1.0
**Last Updated:** November 12, 2025
**Next Update:** Add county name-to-FIPS lookup table