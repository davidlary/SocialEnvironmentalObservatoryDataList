# Geographic Crosswalks
## Linking ZIP Codes, Census Tracts, and Other Geographies to Counties

**Purpose:** Many datasets are NOT published at the county level. This document explains how to aggregate or allocate data from other geographic units to counties.

**Essential for:** ZIP code data, census tract data, city/place data, hospital service areas, school districts, and more.

---

## 🗺️ Overview: Geographic Hierarchies

### Clean Hierarchies (Nested)

Some geographies nest cleanly within counties:

```
Nation
 └─ State
     └─ County
         └─ Census Tract
             └─ Block Group
                 └─ Block
```

**Advantage:** Simple aggregation - just sum up to county level

### Complex Hierarchies (Many-to-Many)

Other geographies do NOT nest cleanly:

```
ZIP Code ←→ County (many-to-many)
Place (City) ←→ County (may span multiple)
School District ←→ County (may span multiple)
Hospital Service Area ←→ County
Congressional District ←→ County
```

**Challenge:** Requires crosswalks with allocation weights

---

## 📬 ZIP Code → County Crosswalks

### The Problem

**ZIP codes do NOT align with county boundaries:**
- ZIP codes are USPS delivery routes, not geographic areas
- A single ZIP code can span multiple counties
- Counties can contain parts of multiple ZIP codes

### Solution: HUD USPS ZIP-County Crosswalk

**Source:** US Department of Housing and Urban Development (HUD)
**URL:** https://www.huduser.gov/portal/datasets/usps_crosswalk.html

**Files:**
- Quarterly updates (Q1, Q2, Q3, Q4 each year)
- ZIP to County crosswalk with **residential ratios**
- ZIP to Tract, ZIP to CBSA also available

**Key Fields:**
- `ZIP`: 5-digit ZIP code
- `COUNTY`: 5-digit FIPS code
- `RES_RATIO`: **Residential address ratio** (0-1)
  - Proportion of residential addresses in this ZIP that are in this county
- `BUS_RATIO`: Business address ratio (0-1)
- `OTH_RATIO`: Other address ratio (0-1)
- `TOT_RATIO`: Total address ratio (0-1)

**Example:**
```
ZIP    COUNTY  RES_RATIO  BUS_RATIO  TOT_RATIO
78705  48453   1.0        1.0        1.0         # Entirely in Travis County, TX
78669  48453   0.42       0.35       0.41        # 42% residential in Travis
78669  48491   0.58       0.65       0.59        # 58% residential in Williamson
```

### How to Use

**Scenario 1: ZIP-level data → County aggregation**

```python
import pandas as pd

# Load HUD crosswalk (Q4 2024 example)
crosswalk = pd.read_excel('ZIP_COUNTY_Q42024.xlsx', dtype={'ZIP': str, 'COUNTY': str})

# Load your ZIP-level data
zip_data = pd.read_csv('zip_data.csv', dtype={'ZIP': str})
# Columns: ZIP, value

# Merge crosswalk
merged = zip_data.merge(crosswalk[['ZIP', 'COUNTY', 'RES_RATIO']], on='ZIP')

# Allocate ZIP values to counties using residential ratio
merged['allocated_value'] = merged['value'] * merged['RES_RATIO']

# Aggregate to county level
county_data = merged.groupby('COUNTY', as_index=False)['allocated_value'].sum()
```

**Scenario 2: County data → ZIP allocation (inverse)**

```python
# Load county-level data
county_data = pd.read_csv('county_data.csv', dtype={'FIPS': str})
# Columns: FIPS, county_value

# Merge with crosswalk
merged = crosswalk.merge(
    county_data,
    left_on='COUNTY',
    right_on='FIPS'
)

# Allocate county value to ZIPs proportionally
# Note: This assumes value distributes by population (residential ratio)
merged['zip_allocated'] = merged['county_value'] * merged['RES_RATIO']

# For ZIPs spanning multiple counties, sum allocations
zip_data = merged.groupby('ZIP', as_index=False)['zip_allocated'].sum()
```

### Alternative: UDS Mapper

**Source:** University of Wisconsin Population Health Institute
**URL:** https://www.udsmapper.org/

**Features:**
- Web interface for ZIP → County lookup
- Downloadable crosswalk files
- Based on ZIP Code Tabulation Areas (ZCTAs) from Census

**Note:** UDS Mapper uses ZCTAs (census geography) while HUD uses USPS ZIPs (delivery routes). HUD is more current and accurate.

---

## 🏘️ Census Tract → County (Simple Aggregation)

### The Solution: Hierarchical Nesting

Census tracts ALWAYS nest within counties (by design).

**Census Tract GEOID Structure:**
```
SSCCCTTTTTT
│ │   │
│ │   └─ 6-digit Tract Code
│ └─ 3-digit County Code
└─ 2-digit State Code
```

**Example:**
- Tract 48453001100
  - State: 48 (Texas)
  - County: 453 (Travis County)
  - Tract: 001100 (Tract 11.00)

**Implication:** Extract county FIPS from first 5 digits of tract GEOID.

### How to Aggregate Tract Data to Counties

```python
import pandas as pd

# Load tract-level data
tract_data = pd.read_csv('tract_data.csv', dtype={'GEOID': str})
# Columns: GEOID (11-digit), value

# Extract county FIPS (first 5 digits)
tract_data['COUNTY_FIPS'] = tract_data['GEOID'].str[:5]

# Aggregate to county
county_data = tract_data.groupby('COUNTY_FIPS', as_index=False)['value'].sum()
```

```r
library(tidyverse)

# Load tract-level data
tract_data <- read_csv('tract_data.csv', col_types = cols(GEOID = col_character()))

# Extract county FIPS
tract_data <- tract_data %>%
  mutate(COUNTY_FIPS = substr(GEOID, 1, 5))

# Aggregate to county
county_data <- tract_data %>%
  group_by(COUNTY_FIPS) %>%
  summarise(value = sum(value, na.rm = TRUE))
```

---

## 🏙️ Place (City/Town) → County

### The Problem

**Places (cities, towns, CDPs) can span multiple counties:**
- New York City spans 5 counties
- Kansas City, MO spans 4 counties
- Many suburban cities span 2+ counties

### Solution: Census Place-County Relationship File

**Source:** Census Bureau
**URL:** https://www.census.gov/geographies/reference-files/time-series/geo/relationship-files.html

**File:** County-Place Relationship File

**Key Fields:**
- `STATEFP`: State FIPS
- `COUNTYFP`: County FIPS
- `PLACEFP`: Place FIPS (5-digit)
- `PLACENAME`: Place name
- `POPPT`: Population of place in this county
- `AREALANDPT`: Land area of place in this county (sq meters)

**Example: Kansas City, MO (Place FIPS 29038000)**
```
STATE  COUNTY  PLACE    PLACENAME      POPPT    AREALANDPT
29     047     038000   Kansas City    21193    19479042
29     095     038000   Kansas City    319294   803427743
29     165     038000   Kansas City    121071   80842599
29     037     038000   Kansas City    27600    11898733
```

### How to Allocate Place Data to Counties

**Option 1: Population-weighted**
```python
# Load place-county relationship file
place_county = pd.read_csv('place_county_2020.txt', sep='|', dtype=str)

# Calculate population proportion
place_county['pop_share'] = (
    place_county.groupby('PLACEFP')['POPPT']
    .transform(lambda x: x / x.sum())
)

# Merge place data
place_data = pd.read_csv('place_data.csv', dtype={'PLACEFP': str})
merged = place_data.merge(place_county, on='PLACEFP')

# Allocate to counties
merged['allocated_value'] = merged['value'] * merged['pop_share']

# Aggregate to county
county_data = merged.groupby(['STATEFP', 'COUNTYFP'], as_index=False)['allocated_value'].sum()
county_data['FIPS'] = county_data['STATEFP'] + county_data['COUNTYFP']
```

**Option 2: Area-weighted** (use `AREALANDPT` instead of `POPPT`)

---

## 🏫 School District → County

### The Problem

School districts frequently span multiple counties, especially in rural areas.

### Solution: NCES School District-County Relationship Files

**Source:** National Center for Education Statistics (NCES)
**URL:** https://nces.ed.gov/programs/edge/Geographic/RelationshipFiles

**File:** School District to County Relationship File

**Key Fields:**
- `LEAID`: Local Education Agency ID (7-digit school district code)
- `COUNTY_FIPS`: 5-digit county FIPS
- `ENROLLMENT`: Enrollment in this county (for this district)

**Example: A district spanning 3 counties**
```
LEAID    COUNTY_FIPS  ENROLLMENT
4800001  48001        450
4800001  48003        1200
4800001  48005        350
```

### How to Allocate

```python
# Load district-county crosswalk
district_county = pd.read_csv('district_county.csv', dtype=str)

# Calculate enrollment share
district_county['enrollment_share'] = (
    district_county.groupby('LEAID')['ENROLLMENT']
    .transform(lambda x: x / x.sum())
)

# Merge district data and allocate
district_data = pd.read_csv('district_data.csv', dtype={'LEAID': str})
merged = district_data.merge(district_county, on='LEAID')
merged['allocated_value'] = merged['value'] * merged['enrollment_share']

# Aggregate to county
county_data = merged.groupby('COUNTY_FIPS', as_index=False)['allocated_value'].sum()
```

---

## 🏥 Hospital Service Area → County

### The Problem

Hospital service areas (HSAs) and Hospital Referral Regions (HRRs) are defined by patient flow patterns and do NOT align with county boundaries.

### Solution: Dartmouth Atlas Crosswalk

**Source:** Dartmouth Atlas of Health Care
**URL:** https://data.dartmouthatlas.org/

**Files:**
- ZIP to HSA crosswalk
- ZIP to HRR crosswalk

**Method:**
1. Use ZIP→HSA crosswalk to get ZIP-level HSA assignments
2. Use ZIP→County crosswalk (HUD) to allocate to counties
3. Two-step process

---

## 🗳️ Congressional District → County

### The Problem

Congressional districts are drawn independently of county boundaries and frequently split counties.

### Solution: Census Congressional District-County Relationship File

**Source:** Census Bureau
**URL:** https://www.census.gov/geographies/reference-files/time-series/geo/relationship-files.html

**File:** Congressional District to County Relationship File

**Key Fields:**
- `STATE`: State FIPS
- `COUNTY`: County FIPS
- `DISTRICT`: Congressional District (01-53, plus 00 for at-large)
- `POPULATION`: Population of county in this district

### How to Use

```python
# Load CD-county relationship
cd_county = pd.read_csv('cd116_county_2020.txt', sep='|', dtype=str)

# Create full CD identifier
cd_county['CD_FIPS'] = cd_county['STATE'] + cd_county['DISTRICT']

# Calculate population share
cd_county['pop_share'] = (
    cd_county.groupby('CD_FIPS')['POPULATION']
    .transform(lambda x: x / x.sum())
)

# Allocate CD data to counties
cd_data = pd.read_csv('cd_data.csv', dtype={'CD_FIPS': str})
merged = cd_data.merge(cd_county, on='CD_FIPS')
merged['allocated'] = merged['value'] * merged['pop_share']

county_data = merged.groupby(['STATE', 'COUNTY'], as_index=False)['allocated'].sum()
county_data['FIPS'] = county_data['STATE'] + county_data['COUNTY']
```

---

## 🌐 CBSA (Metro/Micro Areas) → County

### The Solution: Clean Hierarchy

CBSAs (Core-Based Statistical Areas) are defined as collections of counties.

**One county → One CBSA** (or no CBSA if rural)
**One CBSA → Multiple counties**

### CBSA Delineation File

**Source:** Office of Management and Budget (OMB) via Census
**URL:** https://www.census.gov/geographies/reference-files/time-series/demo/metro-micro/delineation-files.html

**File:** Metropolitan and Micropolitan Statistical Area Delineation

**Key Fields:**
- `CBSA Code`: 5-digit CBSA code
- `CBSA Title`: Metro/Micro area name
- `Metropolitan/Micropolitan Statistical Area`: Type
- `State FIPS`: 2-digit state code
- `County/County Equivalent FIPS`: 3-digit county code
- `County/County Equivalent`: County name
- `Central/Outlying County`: Central vs. outlying designation

**Example: Austin-Round Rock-Georgetown, TX Metro (CBSA 12420)**
```
CBSA   Title                              State  County  Central/Outlying
12420  Austin-Round Rock-Georgetown, TX   48     021     Central        (Bastrop)
12420  Austin-Round Rock-Georgetown, TX   48     053     Outlying       (Burnet)
12420  Austin-Round Rock-Georgetown, TX   48     055     Outlying       (Caldwell)
12420  Austin-Round Rock-Georgetown, TX   48     209     Central        (Hays)
12420  Austin-Round Rock-Georgetown, TX   48     453     Central        (Travis)
12420  Austin-Round Rock-Georgetown, TX   48     491     Central        (Williamson)
```

### How to Use

**Scenario: Aggregate county data to CBSA**
```python
# Load CBSA delineation
cbsa = pd.read_csv('cbsa_delineation_2020.csv', dtype=str)
cbsa['FIPS'] = cbsa['State FIPS'] + cbsa['County FIPS']

# Load county data
county_data = pd.read_csv('county_data.csv', dtype={'FIPS': str})

# Merge and aggregate
merged = county_data.merge(cbsa[['FIPS', 'CBSA Code']], on='FIPS', how='left')
cbsa_data = merged.groupby('CBSA Code', as_index=False)['value'].sum()
```

**Scenario: Allocate CBSA data to counties**
```python
# Equal allocation to all counties in CBSA (simple approach)
cbsa_data = pd.read_csv('cbsa_data.csv', dtype={'CBSA_Code': str})

# Count counties per CBSA
county_count = cbsa.groupby('CBSA Code').size().reset_index(name='n_counties')

# Merge and divide
merged = cbsa_data.merge(county_count, on='CBSA Code')
merged['value_per_county'] = merged['value'] / merged['n_counties']

# Expand to county level
county_allocated = merged.merge(cbsa[['CBSA Code', 'FIPS']], on='CBSA Code')
```

**Note:** Population-weighted or area-weighted allocation is better than equal allocation when possible.

---

## 📍 Latitude/Longitude → County (Point-in-Polygon)

### The Problem

Some data has only coordinates (e.g., monitoring stations, facilities, events).

### Solution: Spatial Join with County Shapefiles

**Method:** Use GIS software or Python/R spatial packages.

#### Python (GeoPandas)

```python
import geopandas as gpd
from shapely.geometry import Point

# Load county boundaries
counties = gpd.read_file('tl_2020_us_county.shp')

# Your point data
points_df = pd.DataFrame({
    'id': [1, 2, 3],
    'longitude': [-97.74, -118.24, -80.19],
    'latitude': [30.27, 34.05, 25.76]
})

# Convert to GeoDataFrame
geometry = [Point(xy) for xy in zip(points_df['longitude'], points_df['latitude'])]
points_gdf = gpd.GeoDataFrame(points_df, geometry=geometry, crs='EPSG:4326')

# Ensure same CRS
counties = counties.to_crs('EPSG:4326')

# Spatial join (point-in-polygon)
points_with_county = gpd.sjoin(
    points_gdf,
    counties[['GEOID', 'NAME', 'geometry']],
    how='left',
    predicate='within'
)

print(points_with_county[['id', 'longitude', 'latitude', 'GEOID', 'NAME']])
```

#### R (sf package)

```r
library(sf)
library(tidyverse)

# Load county boundaries
counties <- st_read('tl_2020_us_county.shp')

# Your point data
points_df <- tibble(
  id = c(1, 2, 3),
  longitude = c(-97.74, -118.24, -80.19),
  latitude = c(30.27, 34.05, 25.76)
)

# Convert to sf object
points_sf <- st_as_sf(points_df, coords = c('longitude', 'latitude'), crs = 4326)

# Ensure same CRS
counties <- st_transform(counties, 4326)

# Spatial join
points_with_county <- st_join(points_sf, counties[c('GEOID', 'NAME')])

print(points_with_county)
```

---

## 🔢 Summary: When to Use Each Crosswalk

| Source Geography | Target Geography | Method | Key Resource |
|------------------|------------------|--------|--------------|
| ZIP Code | County | HUD ZIP-County crosswalk with allocation ratios | https://www.huduser.gov/portal/datasets/usps_crosswalk.html |
| Census Tract | County | Extract first 5 digits of GEOID | Built-in hierarchy |
| Block Group | County | Extract first 5 digits of GEOID | Built-in hierarchy |
| Place (City) | County | Census Place-County relationship file | https://www.census.gov/geographies/reference-files/ |
| School District | County | NCES District-County relationship file | https://nces.ed.gov/programs/edge/ |
| Congressional District | County | Census CD-County relationship file | https://www.census.gov/geographies/reference-files/ |
| CBSA (Metro) | County | OMB/Census CBSA delineation | https://www.census.gov/geographies/reference-files/time-series/demo/metro-micro/ |
| Hospital Service Area | County | Two-step: HSA→ZIP, ZIP→County | Dartmouth Atlas + HUD |
| Coordinates (Lat/Lon) | County | Spatial join (point-in-polygon) | Census TIGER/Line shapefiles |

---

## ✅ Checklist: Using Geographic Crosswalks

Before converting data to county level:

- [ ] Identify source geography
- [ ] Determine if clean hierarchy (tract, block group) or many-to-many (ZIP, place)
- [ ] Download appropriate crosswalk file
- [ ] Choose allocation method (population, area, equal)
- [ ] Validate results (check totals match before aggregation)
- [ ] Document allocation method in analysis
- [ ] Be aware of temporal issues (crosswalks change yearly)
- [ ] Use crosswalk from same year as data when possible

---

## 📚 Additional Resources

1. **Census Geographic Products:**
   - https://www.census.gov/programs-surveys/geography/guidance/geo-products.html

2. **NCES Education Geography:**
   - https://nces.ed.gov/programs/edge/

3. **HUD USPS Crosswalk Files:**
   - https://www.huduser.gov/portal/datasets/usps_crosswalk.html

4. **Dartmouth Atlas:**
   - https://data.dartmouthatlas.org/

5. **MABLE/Geocorr (Missouri Census Data Center):**
   - http://mcdc.missouri.edu/applications/geocorr.html
   - Interactive tool for creating custom crosswalks

---

**Next:** Read [TEMPORAL_COVERAGE_UPDATE_SCHEDULE.md](./TEMPORAL_COVERAGE_UPDATE_SCHEDULE.md) to understand data update frequencies and release schedules for all sources.
