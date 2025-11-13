# Infrastructure and Coastal Contaminants - Comprehensive Documentation
## US County-Level Critical Infrastructure and Emerging Contaminant Data Sources

**Coverage:** All 3,143 US Counties
**Last Updated:** November 13, 2025
**Status:** Complete - 10 Data Sources Documented
**Total Variables:** 120+ priority variables

---

## 📋 Overview

This comprehensive documentation covers critical infrastructure proximity, coastal hazards, and emerging contaminants at the US county level. These data sources fill important gaps in environmental health exposure assessment:

- **Infrastructure Proximity:** Dams, nuclear facilities, bridges, wildland-urban interface
- **Coastal Hazards:** Sea level rise, coastal flooding, harmful algal blooms
- **Emerging Contaminants:** PFAS in drinking water
- **Wildfire Risk:** Hazard potential mapping
- **Land Change:** County-level land cover change statistics
- **Population Density:** High-resolution gridded population

All sources provide county-level aggregation or can be spatially aggregated to counties using GIS methods.

---

## 1️⃣ EPA UCMR5 PFAS MONITORING (2023-2025)

### 📊 Overview
The fifth Unregulated Contaminant Monitoring Rule (UCMR5) requires monitoring of 29 PFAS (per- and polyfluoroalkyl substances) and lithium in public water systems. This is the **most comprehensive national PFAS drinking water dataset** available.

**Coverage:**
- 3,000+ public water systems serving >3,300 people
- All 50 states
- 2023-2025 monitoring period
- County-level aggregation possible via PWS service areas

**Key PFAS Monitored:**
- PFOA (perfluorooctanoic acid)
- PFOS (perfluorooctane sulfonic acid)
- PFNA, PFHxS, PFBS, PFHxA, PFDA, PFUnA, PFDoA
- GenX chemicals
- 20 additional PFAS compounds

### 🔢 Variables Available

| Variable Category | Specific Variables | Temporal Coverage |
|------------------|-------------------|-------------------|
| **PFAS Concentrations** | 29 individual PFAS compounds (ng/L) | 2023-2025 |
| **Detection Frequencies** | % samples with detections by compound | 2023-2025 |
| **Maximum Levels** | Highest concentration detected per PWS | 2023-2025 |
| **Population Exposure** | Population served by systems with detections | 2023-2025 |
| **Lithium** | Lithium concentrations in drinking water (μg/L) | 2023-2025 |

**Total Variables:** ~35

### 📡 Data Access

**Official Source:** EPA UCMR Data
**URL:** https://www.epa.gov/dwucmr/fifth-unregulated-contaminant-monitoring-rule
**Format:** Excel spreadsheets, downloadable tables
**Update Frequency:** Quarterly during monitoring period
**Spatial Resolution:** Public water system (PWS) level → aggregate to counties

### 💻 R Code Example

```r
library(tidyverse)
library(readxl)

# Download UCMR5 data from EPA
# https://www.epa.gov/dwucmr/occurrence-data-unregulated-contaminant-monitoring-rule

# Read UCMR5 PFAS data
ucmr5 <- read_excel("UCMR5_All_Results.xlsx")

# Filter for PFAS contaminants
pfas_compounds <- c("PFOA", "PFOS", "PFNA", "PFHxS", "PFBS", "GenX")

pfas_data <- ucmr5 %>%
  filter(ContaminantName %in% pfas_compounds) %>%
  # Remove non-detects for max calculation (or handle as RL/2)
  filter(!is.na(AnalyticalResultValue), AnalyticalResultValue > 0)

# Aggregate to county level
county_pfas <- pfas_data %>%
  group_by(StateCode, CountyName, ContaminantName) %>%
  summarise(
    max_conc_ng_L = max(AnalyticalResultValue, na.rm = TRUE),
    mean_conc_ng_L = mean(AnalyticalResultValue, na.rm = TRUE),
    n_detections = n(),
    n_systems = n_distinct(PWSID),
    .groups = "drop"
  )

# Calculate total PFAS exposure
county_total_pfas <- county_pfas %>%
  group_by(StateCode, CountyName) %>%
  summarise(
    total_pfas_compounds_detected = n_distinct(ContaminantName),
    max_any_pfas_ng_L = max(max_conc_ng_L),
    sum_pfas_ng_L = sum(mean_conc_ng_L),
    .groups = "drop"
  )
```

### 📝 County-Level Metrics

1. **Maximum PFAS Concentration:** Highest level of any PFAS detected in county (ng/L)
2. **Number of PFAS Detected:** Count of distinct PFAS compounds found
3. **Total PFAS:** Sum of mean concentrations across all compounds
4. **Detection Rate:** % of water systems in county with any PFAS detection
5. **Population Exposed:** Population served by systems with PFAS detections

### 🔗 Related Data Sources
- EPA SDWIS (Safe Drinking Water Information System) for PWS locations and service populations
- USGS PFAS monitoring in surface water and groundwater

---

## 2️⃣ USACE NATIONAL INVENTORY OF DAMS (NID)

### 📊 Overview
The US Army Corps of Engineers maintains the National Inventory of Dams, documenting all dams meeting size, storage, or hazard criteria. Dam proximity and failure risk are important environmental health factors.

**Coverage:**
- 91,457 dams (as of 2024)
- All 50 states + territories
- Federal, state, local, and private dams
- County-level counts and characteristics

**Inclusion Criteria:**
- High or significant hazard classification (any size)
- ≥25 feet in height and >15 acre-feet storage, OR
- ≥50 acre-feet storage and >6 feet high

### 🔢 Variables Available

| Variable Category | Specific Variables | Description |
|------------------|-------------------|-------------|
| **Dam Counts** | Total dams per county | All dams meeting NID criteria |
| | High hazard dams | Failure would likely cause loss of life |
| | Significant hazard dams | Failure would cause economic loss, environmental damage |
| | Low hazard dams | Failure unlikely to cause loss of life |
| **Dam Characteristics** | Dam height (feet) | Maximum and mean per county |
| | Storage capacity (acre-feet) | Maximum and total per county |
| | Dam age (years since completion) | Oldest and mean age |
| | Dam condition | Good, fair, poor, unsatisfactory (% by category) |
| **Dam Purposes** | Irrigation, flood control, hydroelectric, water supply, recreation, etc. | Count by primary purpose |
| **Ownership** | Federal, state, local, public utility, private | Count by owner type |
| **Inspection Status** | Date of last inspection | Years since last inspection |
| **Emergency Action Plans** | EAP status | % of high hazard dams with current EAP |

**Total Variables:** ~20

### 📡 Data Access

**Official Source:** USACE National Inventory of Dams
**URL:** https://nid.usace.army.mil/
**Format:** Downloadable CSV, Shapefile, GeoJSON
**Update Frequency:** Quarterly
**Spatial Resolution:** Point locations (lat/lon) → aggregate to counties

### 💻 Python Code Example

```python
import pandas as pd
import geopandas as gpd

# Download NID data from USACE
# https://nid.usace.army.mil/#/downloads

# Read NID shapefile
nid = gpd.read_file("NID_2024.shp")

# Aggregate dam counts by county
county_dams = nid.groupby(['STATE', 'COUNTY']).agg({
    'DAM_NAME': 'count',  # Total dams
    'HAZARD': lambda x: (x == 'H').sum(),  # High hazard count
    'NID_HEIGHT': ['max', 'mean'],
    'NID_STORAGE': ['max', 'sum'],
    'YEAR_COMPLETED': lambda x: (2024 - x).mean(),  # Mean age
    'DAM_CONDITION': lambda x: (x == 'POOR').sum() / len(x)  # % poor condition
}).reset_index()

county_dams.columns = ['state', 'county', 'total_dams', 'high_hazard_dams',
                        'max_height_ft', 'mean_height_ft', 'max_storage_acre_ft',
                        'total_storage_acre_ft', 'mean_age_years', 'pct_poor_condition']

# Calculate dam density
# Merge with county area data
county_area = gpd.read_file("us_counties.shp")
county_dams_density = county_dams.merge(
    county_area[['state', 'county', 'area_sq_mi']],
    on=['state', 'county']
)
county_dams_density['dams_per_100_sq_mi'] = (
    county_dams_density['total_dams'] / county_dams_density['area_sq_mi'] * 100
)
```

### 📝 Priority County-Level Metrics

1. **High Hazard Dam Count:** Number of dams where failure would likely cause fatalities
2. **Dam Density:** Dams per 100 square miles
3. **Poor Condition Rate:** % of dams in poor or unsatisfactory condition
4. **Total Storage Capacity:** Sum of all dam storage in county (acre-feet)
5. **Mean Dam Age:** Average years since completion

---

## 3️⃣ USGS/USFS WILDLAND-URBAN INTERFACE (WUI)

### 📊 Overview
The Wildland-Urban Interface (WUI) represents areas where human development meets wildland vegetation, creating elevated wildfire risk to structures and populations.

**Coverage:**
- All 3,143 US counties
- 1990, 2000, 2010, 2020 (decadal updates)
- Housing units and population in WUI areas
- Interface vs. Intermix classifications

**Definitions:**
- **Interface WUI:** Areas >50% vegetation within 2.4 km, housing density ≥1 unit per 40 acres
- **Intermix WUI:** Areas with vegetation and housing intermixed, >50% vegetation, housing density ≥1 unit per 40 acres

### 🔢 Variables Available

| Variable Category | Specific Variables | Temporal Coverage |
|------------------|-------------------|-------------------|
| **WUI Area** | Total WUI area (sq km) | 1990, 2000, 2010, 2020 |
| | Interface WUI area | 1990, 2000, 2010, 2020 |
| | Intermix WUI area | 1990, 2000, 2010, 2020 |
| **Population** | Population in WUI | 1990, 2000, 2010, 2020 |
| | Population in Interface | 1990, 2000, 2010, 2020 |
| | Population in Intermix | 1990, 2000, 2010, 2020 |
| | % of county population in WUI | 1990, 2000, 2010, 2020 |
| **Housing** | Housing units in WUI | 1990, 2000, 2010, 2020 |
| | Housing units in Interface | 1990, 2000, 2010, 2020 |
| | Housing units in Intermix | 1990, 2000, 2010, 2020 |
| | % of county housing in WUI | 1990, 2000, 2010, 2020 |
| **Change Metrics** | WUI area change 1990-2020 (sq km, %) | Decadal changes |
| | WUI population growth 1990-2020 | Decadal changes |

**Total Variables:** ~15 core (×4 time periods = 60 total variables)

### 📡 Data Access

**Official Source:** USGS and USDA Forest Service
**URL:** https://www.fs.usda.gov/rds/archive/Catalog/RDS-2015-0012-3
**URL (SILVIS Lab):** https://silvis.forest.wisc.edu/data/wui-change/
**Format:** Geodatabase, Shapefiles, CSV summary tables
**Update Frequency:** Decadal (aligned with Census)
**Spatial Resolution:** 30-meter raster → county summaries provided

### 💻 R Code Example

```r
library(tidyverse)
library(sf)

# Download WUI data from SILVIS Lab
# https://silvis.forest.wisc.edu/data/wui-change/

# Read county-level WUI summary statistics
wui_2020 <- read_csv("wui_county_stats_2020.csv")
wui_2010 <- read_csv("wui_county_stats_2010.csv")
wui_2000 <- read_csv("wui_county_stats_2000.csv")
wui_1990 <- read_csv("wui_county_stats_1990.csv")

# Combine all years
wui_panel <- bind_rows(
  wui_1990 %>% mutate(year = 1990),
  wui_2000 %>% mutate(year = 2000),
  wui_2010 %>% mutate(year = 2010),
  wui_2020 %>% mutate(year = 2020)
)

# Calculate key metrics per county
wui_metrics <- wui_panel %>%
  group_by(GEOID, county_name, state) %>%
  arrange(year) %>%
  summarise(
    # Current status (2020)
    wui_area_sq_km_2020 = last(wui_area_sq_km),
    wui_population_2020 = last(wui_population),
    wui_housing_units_2020 = last(wui_housing_units),
    pct_population_in_wui_2020 = last(wui_population / total_population * 100),

    # Change metrics
    wui_area_change_1990_2020_pct =
      (last(wui_area_sq_km) - first(wui_area_sq_km)) / first(wui_area_sq_km) * 100,
    wui_pop_change_1990_2020_pct =
      (last(wui_population) - first(wui_population)) / first(wui_population) * 100,

    .groups = "drop"
  )

# Identify high-risk counties
high_risk_wui <- wui_metrics %>%
  filter(
    pct_population_in_wui_2020 > 50 |  # More than half in WUI
    wui_area_change_1990_2020_pct > 100  # WUI area doubled
  ) %>%
  arrange(desc(pct_population_in_wui_2020))
```

### 📝 Priority County-Level Metrics

1. **WUI Population %:** Percent of county population living in WUI areas (2020)
2. **WUI Area Growth:** Percent change in WUI area 1990-2020
3. **Interface vs. Intermix:** Proportion of WUI in each category
4. **WUI Housing Density:** Housing units per square km in WUI areas
5. **WUI Exposure Trend:** Population growth rate in WUI vs. non-WUI areas

---

## 4️⃣ EPA CYAN + NOAA HABSOS (HARMFUL ALGAL BLOOMS)

### 📊 Overview
Two complementary systems monitor harmful algal blooms (HABs) in US freshwater and coastal waters:

**EPA CyAN (Cyanobacteria Assessment Network):**
- Satellite-based detection of cyanobacterial blooms in freshwater
- 2016-present
- CONUS coverage

**NOAA HABSOS (Harmful Algal BloomS Observing System):**
- Coastal and Great Lakes HAB monitoring
- 2000s-present
- Beach advisories, shellfish closures, fish kills

### 🔢 Variables Available

#### EPA CyAN Variables

| Variable | Description | Temporal Resolution |
|----------|-------------|---------------------|
| **Cyanobacteria Cell Concentration** | Cells/mL estimated from satellite | Daily (cloud-permitting) |
| **Bloom Extent** | Area of waterbody with elevated cyanobacteria | Per event |
| **Bloom Frequency** | Number of days per year with elevated levels | Annual summary |
| **Peak Concentration** | Maximum concentration detected per year | Annual |
| **Alert Days** | Days exceeding WHO recreational thresholds | Annual count |

#### NOAA HABSOS Variables

| Variable | Description | Temporal Resolution |
|----------|-------------|---------------------|
| **HAB Event Count** | Number of reported HAB events | Annual, by county |
| **Event Duration** | Days per event | Per event |
| **Species Detected** | Dominant HAB species (e.g., Karenia brevis) | Per event |
| **Beach Closures** | Number of beaches closed due to HABs | Annual count |
| **Shellfish Harvest Closures** | Area closed to shellfish harvest (acres) | Per event |
| **Fish Kill Events** | Fish mortality events associated with HABs | Annual count |
| **Human Illness Reports** | Reported HAB-related illnesses | Annual count |

**Total Variables:** ~15 (EPA CyAN) + ~10 (NOAA HABSOS) = 25

### 📡 Data Access

**EPA CyAN:**
**URL:** https://www.epa.gov/water-research/cyanobacteria-assessment-network-cyan
**API:** https://qed.epa.gov/cyan/
**Format:** JSON API, GeoTIFF rasters, CSV summaries

**NOAA HABSOS:**
**URL:** https://hab.whoi.edu/
**Format:** Interactive map, downloadable spreadsheets
**Update Frequency:** Real-time (CyAN), weekly (HABSOS)

### 💻 Python Code Example

```python
import requests
import pandas as pd
import geopandas as gpd
from datetime import datetime, timedelta

# EPA CyAN API - Get bloom data for specific waterbodies
def get_cyan_county_data(state, county, year):
    """
    Fetch CyAN bloom data for waterbodies in a county.
    """
    url = "https://qed.epa.gov/cyan/app/api/waterbodies"
    params = {
        "state": state,
        "county": county,
        "year": year
    }
    response = requests.get(url, params=params)
    data = response.json()
    return data

# Example: Travis County, Texas (2023)
travis_cyan_2023 = get_cyan_county_data("TX", "Travis", 2023)

# Process CyAN data to county-level metrics
def summarize_cyan_county(cyan_data):
    """
    Aggregate CyAN waterbody data to county level.
    """
    summary = {
        'n_waterbodies': len(cyan_data['waterbodies']),
        'n_waterbodies_with_blooms': 0,
        'max_concentration_cells_ml': 0,
        'total_bloom_days': 0
    }

    for wb in cyan_data['waterbodies']:
        if wb['bloom_days'] > 0:
            summary['n_waterbodies_with_blooms'] += 1
        summary['max_concentration_cells_ml'] = max(
            summary['max_concentration_cells_ml'],
            wb['max_concentration']
        )
        summary['total_bloom_days'] += wb['bloom_days']

    summary['pct_waterbodies_with_blooms'] = (
        summary['n_waterbodies_with_blooms'] / summary['n_waterbodies'] * 100
        if summary['n_waterbodies'] > 0 else 0
    )

    return summary

# NOAA HABSOS - Coastal counties
# Download event database from https://hab.whoi.edu/
habsos = pd.read_csv("habsos_events_2000_2024.csv")

county_hab_events = habsos.groupby(['state', 'county', 'year']).agg({
    'event_id': 'count',  # Number of events
    'duration_days': 'sum',  # Total days with HABs
    'beach_closures': 'sum',
    'fish_kills': 'sum',
    'human_illness': 'sum'
}).reset_index()

county_hab_events.columns = ['state', 'county', 'year', 'hab_event_count',
                              'total_hab_days', 'beach_closures', 'fish_kills',
                              'illness_reports']
```

### 📝 Priority County-Level Metrics

**Freshwater (EPA CyAN):**
1. **Bloom Days per Year:** Total days with elevated cyanobacteria
2. **Waterbodies Affected:** % of monitored waterbodies with blooms
3. **Peak Concentration:** Maximum cyanobacteria concentration (cells/mL)

**Coastal (NOAA HABSOS):**
4. **HAB Event Frequency:** Number of reported events per year
5. **Beach Closure Days:** Total days beaches closed due to HABs
6. **Fish Kill Events:** Count of HAB-associated fish mortality events

---

## 5️⃣ NRC NUCLEAR POWER PLANT PROXIMITY

### 📊 Overview
The Nuclear Regulatory Commission (NRC) licenses and oversees commercial nuclear power plants. Proximity to nuclear facilities is relevant for radiation exposure risk, emergency preparedness, and environmental monitoring.

**Coverage:**
- 93 operating commercial nuclear power reactors (as of 2024)
- 54 nuclear power plant sites
- 31 states
- Decommissioned plants also tracked

### 🔢 Variables Available

| Variable Category | Specific Variables | Description |
|------------------|-------------------|-------------|
| **Facility Counts** | Operating reactors per county | Reactors within county boundaries |
| | Operating plant sites per county | Distinct sites within county |
| | Reactors within 50-mile radius | Emergency planning zone |
| **Proximity** | Distance to nearest reactor (km) | Euclidean distance from county centroid |
| | Distance to nearest plant site (km) | Site-level distance |
| | Counties in 10-mile EPZ | Emergency Planning Zone |
| | Counties in 50-mile EPZ | Ingestion Pathway Zone |
| **Reactor Characteristics** | Total capacity (MWe) | Sum of reactor capacities |
| | Reactor types | PWR, BWR counts |
| | Reactor age (years) | Oldest and mean |
| | Containment types | Dry, ice condenser, Mark I/II/III |
| **Operational Status** | Operating, suspended, decommissioning | Status of reactors in/near county |
| | License expiration dates | Years until license renewal needed |

**Total Variables:** ~15

### 📡 Data Access

**Official Source:** NRC Operating Reactors List
**URL:** https://www.nrc.gov/reactors/operating/list-power-reactor-units.html
**Format:** HTML table (scrapable), PDF
**Spatial Data:** NRC RASCAL Emergency Planning Zones
**Update Frequency:** Updated as plants begin/cease operations

### 💻 R Code Example

```r
library(tidyverse)
library(sf)
library(rvest)

# Scrape NRC operating reactors list
nrc_url <- "https://www.nrc.gov/reactors/operating/list-power-reactor-units.html"
nrc_page <- read_html(nrc_url)

nrc_reactors <- nrc_page %>%
  html_table(fill = TRUE) %>%
  .[[1]] %>%
  as_tibble() %>%
  clean_names()

# Geocode reactor locations (use known coordinates)
# NRC provides latitude/longitude in facility documents
reactor_locations <- read_csv("nrc_reactor_coordinates.csv")

# Convert to spatial object
reactors_sf <- st_as_sf(reactor_locations,
                        coords = c("longitude", "latitude"),
                        crs = 4326)

# Load county boundaries
counties <- st_read("us_counties.shp")

# Calculate proximity metrics
county_nuclear <- counties %>%
  mutate(
    # Distance to nearest reactor
    dist_to_nearest_reactor_km = st_distance(
      st_centroid(geometry),
      reactors_sf
    ) %>%
      apply(1, min) %>%
      units::set_units("km") %>%
      as.numeric(),

    # Count reactors within 50 miles
    reactors_within_50mi = lengths(st_is_within_distance(
      st_centroid(geometry),
      reactors_sf,
      dist = units::set_units(50, "mi")
    )),

    # In 10-mile EPZ (Emergency Planning Zone)?
    in_10mi_epz = reactors_within_50mi > 0 & dist_to_nearest_reactor_km < 16.09,

    # In 50-mile EPZ (Ingestion Pathway Zone)?
    in_50mi_epz = reactors_within_50mi > 0
  )

# Count reactors physically within county boundaries
reactors_in_county <- st_join(counties, reactors_sf, left = TRUE) %>%
  st_drop_geometry() %>%
  group_by(GEOID, county_name) %>%
  summarise(
    reactors_in_county = sum(!is.na(reactor_name)),
    total_capacity_mwe = sum(capacity_mwe, na.rm = TRUE),
    .groups = "drop"
  )

# Combine proximity and count metrics
county_nuclear_final <- county_nuclear %>%
  left_join(reactors_in_county, by = c("GEOID", "county_name")) %>%
  replace_na(list(reactors_in_county = 0, total_capacity_mwe = 0))
```

### 📝 Priority County-Level Metrics

1. **Distance to Nearest Reactor:** Kilometers from county centroid to nearest operating reactor
2. **Emergency Planning Zone Status:** Binary indicator for 10-mile and 50-mile EPZ
3. **Reactors within 50 Miles:** Count of reactors within ingestion pathway zone
4. **In-County Reactors:** Number of operating reactors within county boundaries
5. **Total Nuclear Capacity:** Sum of megawatt-electric (MWe) capacity for in-county reactors

---

## 6️⃣ FHWA NATIONAL BRIDGE INVENTORY (NBI)

### 📊 Overview
The Federal Highway Administration maintains the National Bridge Inventory, documenting all bridges on public roads over 20 feet in length. Bridge condition and safety are important for transportation infrastructure resilience.

**Coverage:**
- 617,000+ bridges (as of 2024)
- All 50 states + territories
- Federal, state, local bridges
- County-level aggregation

### 🔢 Variables Available

| Variable Category | Specific Variables | Temporal Coverage |
|------------------|-------------------|-------------------|
| **Bridge Counts** | Total bridges per county | 1992-present (annual) |
| | Bridges by material (steel, concrete, wood, other) | Annual |
| | Bridges by structure type (girder, truss, arch, suspension, etc.) | Annual |
| **Bridge Condition** | Structurally deficient bridges (count, %) | Annual |
| | Functionally obsolete bridges (count, %) | Annual |
| | Good condition bridges (rating ≥7) | Annual |
| | Poor condition bridges (rating ≤4) | Annual |
| **Bridge Characteristics** | Mean bridge age (years) | Annual |
| | Total bridge deck area (sq ft) | Annual |
| | Bridges over 100 years old (count) | Annual |
| **Traffic** | Average daily traffic (ADT) per bridge | Annual |
| | Total ADT across all county bridges | Annual |
| | Truck traffic percentage | Annual |
| **Safety** | Bridges with reduced weight limits (count) | Annual |
| | Bridges with posted speed restrictions | Annual |
| | Scour-critical bridges (count) | Annual |
| **Ownership** | Federal, state, county, city, private (counts) | Annual |

**Total Variables:** ~20 core variables × 32 years = 640 variable-years

### 📡 Data Access

**Official Source:** FHWA National Bridge Inventory
**URL:** https://www.fhwa.dot.gov/bridge/nbi.cfm
**Download:** https://www.fhwa.dot.gov/bridge/nbi/ascii.cfm
**Format:** Delimited text files (ASCII), one file per year
**Update Frequency:** Annual
**Spatial Resolution:** Point locations (lat/lon) → aggregate to counties

### 💻 Python Code Example

```python
import pandas as pd
import geopandas as gpd

# Download NBI data (example for 2023)
# Format: Fixed-width ASCII or delimited
nbi_2023 = pd.read_csv(
    "NBI2023.txt",
    dtype=str,  # Read as strings to preserve leading zeros in FIPS codes
    low_memory=False
)

# Key field mappings (simplified - full data dictionary has 100+ fields)
# STATE_CODE_001: State FIPS
# COUNTY_CODE_003: County FIPS
# YEAR_BUILT_027: Year bridge was constructed
# DECK_COND_058: Deck condition rating (0-9, N)
# SUPERSTRUCTURE_COND_059: Superstructure condition (0-9, N)
# SUBSTRUCTURE_COND_060: Substructure condition (0-9, N)
# ADT_029: Average daily traffic
# STRUCTURE_KIND_043A: Structure type code
# STRUCTURE_TYPE_043B: Material type code

# Clean and process
nbi_2023['STATE_FIPS'] = nbi_2023['STATE_CODE_001']
nbi_2023['COUNTY_FIPS'] = nbi_2023['COUNTY_CODE_003']
nbi_2023['GEOID'] = nbi_2023['STATE_FIPS'] + nbi_2023['COUNTY_FIPS']

# Convert condition ratings to numeric
condition_cols = ['DECK_COND_058', 'SUPERSTRUCTURE_COND_059', 'SUBSTRUCTURE_COND_060']
for col in condition_cols:
    nbi_2023[col] = pd.to_numeric(nbi_2023[col], errors='coerce')

# Calculate overall condition (minimum of three ratings)
nbi_2023['min_condition'] = nbi_2023[condition_cols].min(axis=1)

# Bridge age
nbi_2023['YEAR_BUILT_027'] = pd.to_numeric(nbi_2023['YEAR_BUILT_027'], errors='coerce')
nbi_2023['bridge_age'] = 2023 - nbi_2023['YEAR_BUILT_027']

# Structurally deficient: any component rating ≤ 4
nbi_2023['structurally_deficient'] = (nbi_2023['min_condition'] <= 4).astype(int)

# Poor condition: overall rating ≤ 4
nbi_2023['poor_condition'] = (nbi_2023['min_condition'] <= 4).astype(int)

# Aggregate to county level
county_bridges = nbi_2023.groupby('GEOID').agg({
    'STRUCTURE_NUMBER_008': 'count',  # Total bridges
    'structurally_deficient': 'sum',
    'poor_condition': 'sum',
    'bridge_age': 'mean',
    'ADT_029': lambda x: pd.to_numeric(x, errors='coerce').sum(),
    'DECK_AREA_052': lambda x: pd.to_numeric(x, errors='coerce').sum()
}).reset_index()

county_bridges.columns = ['GEOID', 'total_bridges', 'structurally_deficient_bridges',
                           'poor_condition_bridges', 'mean_bridge_age_years',
                           'total_adt', 'total_deck_area_sq_ft']

# Calculate percentages
county_bridges['pct_structurally_deficient'] = (
    county_bridges['structurally_deficient_bridges'] / county_bridges['total_bridges'] * 100
)
county_bridges['pct_poor_condition'] = (
    county_bridges['poor_condition_bridges'] / county_bridges['total_bridges'] * 100
)
```

### 📝 Priority County-Level Metrics

1. **Structurally Deficient Rate:** % of bridges rated structurally deficient
2. **Mean Bridge Age:** Average years since construction
3. **Poor Condition Count:** Number of bridges with condition rating ≤4
4. **Bridge Density:** Bridges per 100 square miles
5. **High-Traffic Deficient Bridges:** Count of structurally deficient bridges with ADT >10,000

---

## 7️⃣ USFS WILDFIRE HAZARD POTENTIAL (WHP)

### 📊 Overview
The USDA Forest Service produces Wildfire Hazard Potential maps showing the relative potential for wildfire on a landscape, considering fuels, topography, and fire behavior.

**Coverage:**
- CONUS (all lower 48 states)
- 2020 (latest comprehensive version)
- 270-meter spatial resolution
- County-level aggregation available

### 🔢 Variables Available

| Variable | Description | Values |
|----------|-------------|--------|
| **Wildfire Hazard Potential** | Continuous index (0-100) | Higher = greater hazard |
| | Classified categories | Very Low, Low, Moderate, High, Very High |
| **County Summaries** | Mean WHP value | County average |
| | % High/Very High WHP | Percent of county area |
| | % Moderate WHP | Percent of county area |
| | % Low/Very Low WHP | Percent of county area |
| **Populated Areas** | Mean WHP in populated areas | WHP where housing density >1 unit/40 acres |
| | % High WHP with housing | Intersection of High WHP + WUI |

**Total Variables:** ~8

### 📡 Data Access

**Official Source:** USDA Forest Service Wildfire Risk to Communities
**URL:** https://wildfirerisk.org/
**Data Download:** https://www.fs.usda.gov/rds/archive/Catalog/RDS-2020-0016
**Format:** GeoTIFF raster (270m), county summary CSV
**Update Frequency:** ~5 years
**Spatial Resolution:** 270 meters → county summaries provided

### 💻 R Code Example

```r
library(terra)
library(sf)
library(tidyverse)

# Download WHP raster from USFS
# https://www.fs.usda.gov/rds/archive/products/RDS-2020-0016/_metadata_RDS-2020-0016.html

# Read WHP raster
whp_raster <- rast("whp2020_conus.tif")

# Read county boundaries
counties <- st_read("us_counties.shp") %>%
  st_transform(crs = crs(whp_raster))

# Extract WHP statistics for each county
county_whp <- exact_extract(
  whp_raster,
  counties,
  fun = c("mean", "median", "min", "max"),
  append_cols = c("GEOID", "NAME")
)

# Calculate percent area in each WHP class
# WHP classes: 0-20 = Very Low, 21-40 = Low, 41-60 = Moderate,
#              61-80 = High, 81-100 = Very High

whp_classes <- exact_extract(
  whp_raster,
  counties,
  function(values, coverage_fractions) {
    data.frame(
      very_low = sum(coverage_fractions[values >= 0 & values <= 20], na.rm = TRUE),
      low = sum(coverage_fractions[values > 20 & values <= 40], na.rm = TRUE),
      moderate = sum(coverage_fractions[values > 40 & values <= 60], na.rm = TRUE),
      high = sum(coverage_fractions[values > 60 & values <= 80], na.rm = TRUE),
      very_high = sum(coverage_fractions[values > 80], na.rm = TRUE),
      total = sum(coverage_fractions, na.rm = TRUE)
    )
  },
  coverage_area = TRUE,
  append_cols = c("GEOID", "NAME")
)

# Calculate percentages
whp_classes_pct <- whp_classes %>%
  mutate(
    pct_very_low = very_low / total * 100,
    pct_low = low / total * 100,
    pct_moderate = moderate / total * 100,
    pct_high = high / total * 100,
    pct_very_high = very_high / total * 100,
    pct_high_or_very_high = (high + very_high) / total * 100
  )

# Combine with mean WHP
county_whp_final <- county_whp %>%
  left_join(whp_classes_pct, by = c("GEOID", "NAME"))
```

### 📝 Priority County-Level Metrics

1. **Mean Wildfire Hazard Potential:** County-wide average WHP score (0-100)
2. **High Hazard Area %:** Percent of county with High or Very High WHP
3. **Populated High Hazard:** WHP in areas with housing (WUI intersection)
4. **WHP Range:** Difference between max and min WHP in county

---

## 8️⃣ NOAA COASTAL INUNDATION / SEA LEVEL RISE

### 📊 Overview
NOAA Office for Coastal Management provides sea level rise inundation mapping and coastal flood exposure data. These datasets project future inundation scenarios and identify vulnerable populations and infrastructure.

**Coverage:**
- US coastal counties (Atlantic, Gulf, Pacific, Great Lakes)
- ~600 coastal counties
- Inundation scenarios: 0-10 feet of sea level rise (1-foot increments)
- Social vulnerability overlays

### 🔢 Variables Available

| Variable Category | Specific Variables | Scenarios |
|------------------|-------------------|-----------|
| **Inundated Area** | Area inundated per scenario (sq km) | 0-10 ft SLR |
| | % of county land area inundated | 0-10 ft SLR |
| **Population Exposure** | Population in inundation zone | 0-10 ft SLR |
| | % of county population exposed | 0-10 ft SLR |
| **Infrastructure** | Road miles in inundation zone | 0-10 ft SLR |
| | Critical facilities exposed (count) | 0-10 ft SLR |
| **Economic Exposure** | Property value at risk ($) | 0-10 ft SLR |
| **Social Vulnerability** | Socially vulnerable population exposed | 0-10 ft SLR |
| | Low-income households in inundation zone | 0-10 ft SLR |

**Total Variables:** ~10 base variables × 11 scenarios = 110 variables

### 📡 Data Access

**Official Source:** NOAA Office for Coastal Management
**URL:** https://coast.noaa.gov/slr/
**Download:** https://coast.noaa.gov/digitalcoast/tools/slr.html
**API:** NOAA Digital Coast Data Access Viewer
**Format:** Shapefiles, GeoTIFF, Web Map Service (WMS)
**Update Frequency:** Periodic (every few years)

### 💻 Python Code Example

```python
import geopandas as gpd
import pandas as pd
from shapely.geometry import Point

# Download NOAA SLR inundation layers
# Available for 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 feet scenarios
# Example: 6-foot sea level rise scenario

slr_6ft = gpd.read_file("noaa_slr_6ft_conus.shp")

# Load coastal counties
coastal_counties = gpd.read_file("us_coastal_counties.shp")

# Calculate inundated area per county
county_inundation = gpd.overlay(
    coastal_counties,
    slr_6ft,
    how='intersection'
)

county_slr_summary = county_inundation.groupby('GEOID').agg({
    'geometry': lambda x: x.unary_union.area / 1e6  # Area in sq km
}).reset_index()

county_slr_summary.columns = ['GEOID', 'inundated_area_sq_km_6ft']

# Merge with total county area
coastal_counties_area = coastal_counties[['GEOID', 'ALAND']].copy()
coastal_counties_area['total_area_sq_km'] = coastal_counties_area['ALAND'] / 1e6

county_slr_summary = county_slr_summary.merge(
    coastal_counties_area[['GEOID', 'total_area_sq_km']],
    on='GEOID',
    how='left'
)

county_slr_summary['pct_area_inundated_6ft'] = (
    county_slr_summary['inundated_area_sq_km_6ft'] /
    county_slr_summary['total_area_sq_km'] * 100
)

# Population exposure (overlay with census blocks)
census_blocks = gpd.read_file("census_blocks_2020.shp")
blocks_in_slr = gpd.sjoin(census_blocks, slr_6ft, how='inner', predicate='intersects')

county_pop_exposure = blocks_in_slr.groupby('GEOID_county').agg({
    'POP20': 'sum'
}).reset_index()

county_pop_exposure.columns = ['GEOID', 'population_in_6ft_slr_zone']

# Combine area and population exposure
county_slr_final = county_slr_summary.merge(
    county_pop_exposure,
    on='GEOID',
    how='left'
).fillna(0)
```

### 📝 Priority County-Level Metrics

1. **Population at Risk (6ft SLR):** Number of people in 6-foot inundation zone
2. **Area Vulnerable (6ft SLR):** % of county land area inundated with 6-foot rise
3. **Critical Infrastructure Exposure:** Count of hospitals, fire stations, power plants in inundation zones
4. **Graduated Exposure Curve:** Population exposure across 1-10 foot scenarios

---

## 9️⃣ MRLC NLCD COUNTY CHANGE STATISTICS

### 📊 Overview
The Multi-Resolution Land Characteristics Consortium (MRLC) provides National Land Cover Database (NLCD) county-level change statistics, documenting land cover transitions between time periods.

**Coverage:**
- All 3,143 US counties
- Time periods: 2001, 2004, 2006, 2008, 2011, 2013, 2016, 2019, 2021
- Change products: 2001-2016, 2016-2019, 2019-2021
- 16 land cover classes

### 🔢 Variables Available

| Variable Category | Specific Variables | Temporal Coverage |
|------------------|-------------------|-------------------|
| **Land Cover Areas** | Area (sq km) for each of 16 NLCD classes | 2001-2021 (9 epochs) |
| | % of county area per class | 2001-2021 |
| **Change Statistics** | Area changed from Class A to Class B (sq km) | Change periods |
| | % of county experiencing change | Change periods |
| | Rate of change per year | Annualized rates |
| **Key Transitions** | Forest to Developed (sq km) | Change periods |
| | Agriculture to Developed | Change periods |
| | Wetland loss | Change periods |
| | Forest loss/gain | Change periods |
| **Impervious Surface** | % impervious surface | 2001-2021 |
| | Change in impervious % | Change periods |

**NLCD Classes:**
- Water (11)
- Developed: Open Space (21), Low Intensity (22), Medium Intensity (23), High Intensity (24)
- Barren (31)
- Forest: Deciduous (41), Evergreen (42), Mixed (43)
- Shrubland (52)
- Herbaceous (71)
- Agriculture: Hay/Pasture (81), Cultivated Crops (82)
- Wetlands: Woody (90), Herbaceous (95)

**Total Variables:** 16 classes × 9 time periods + ~50 change metrics = ~190 variables

### 📡 Data Access

**Official Source:** MRLC/USGS NLCD
**URL:** https://www.mrlc.gov/
**County Statistics:** Not directly provided - must calculate from rasters
**Alternative:** EPA EnviroAtlas has pre-calculated county summaries
**Format:** GeoTIFF (30m resolution), county summaries via processing
**Update Frequency:** Every 2-3 years

### 💻 R Code Example

```r
library(terra)
library(exactextractr)
library(sf)
library(tidyverse)

# Download NLCD rasters
nlcd_2001 <- rast("nlcd_2001_land_cover_l48_20210604.tif")
nlcd_2021 <- rast("nlcd_2021_land_cover_l48_20230630.tif")

# Read county boundaries
counties <- st_read("us_counties.shp") %>%
  st_transform(crs = crs(nlcd_2001))

# Function to calculate NLCD class areas
calculate_nlcd_areas <- function(nlcd_raster, counties_sf) {
  nlcd_freq <- exact_extract(
    nlcd_raster,
    counties_sf,
    function(values, coverage_fractions) {
      # Count pixels in each NLCD class
      pixel_area_sq_m <- 30 * 30  # 30m resolution

      class_areas <- tapply(
        coverage_fractions * pixel_area_sq_m,
        values,
        sum,
        na.rm = TRUE
      )

      # Convert to data frame
      data.frame(
        nlcd_class = as.integer(names(class_areas)),
        area_sq_m = as.numeric(class_areas)
      )
    },
    append_cols = "GEOID"
  )

  # Convert to wide format with one row per county
  nlcd_wide <- nlcd_freq %>%
    mutate(area_sq_km = area_sq_m / 1e6) %>%
    select(-area_sq_m) %>%
    pivot_wider(
      names_from = nlcd_class,
      values_from = area_sq_km,
      values_fill = 0,
      names_prefix = "nlcd_class_"
    )

  return(nlcd_wide)
}

# Calculate for both years
county_nlcd_2001 <- calculate_nlcd_areas(nlcd_2001, counties)
county_nlcd_2021 <- calculate_nlcd_areas(nlcd_2021, counties)

# Calculate change
county_nlcd_change <- county_nlcd_2001 %>%
  left_join(
    county_nlcd_2021,
    by = "GEOID",
    suffix = c("_2001", "_2021")
  ) %>%
  mutate(
    # Key transitions
    developed_gain_sq_km = (
      (nlcd_class_21_2021 + nlcd_class_22_2021 +
       nlcd_class_23_2021 + nlcd_class_24_2021) -
      (nlcd_class_21_2001 + nlcd_class_22_2001 +
       nlcd_class_23_2001 + nlcd_class_24_2001)
    ),

    forest_change_sq_km = (
      (nlcd_class_41_2021 + nlcd_class_42_2021 + nlcd_class_43_2021) -
      (nlcd_class_41_2001 + nlcd_class_42_2001 + nlcd_class_43_2001)
    ),

    agriculture_change_sq_km = (
      (nlcd_class_81_2021 + nlcd_class_82_2021) -
      (nlcd_class_81_2001 + nlcd_class_82_2001)
    ),

    wetland_change_sq_km = (
      (nlcd_class_90_2021 + nlcd_class_95_2021) -
      (nlcd_class_90_2001 + nlcd_class_95_2001)
    )
  )

# Alternative: Use EPA EnviroAtlas county summaries
enviroatlas_url <- "https://enviroatlas.epa.gov/enviroatlas/DataDownloads/"
# Download "Land Cover by County" CSV
county_lc <- read_csv("EnviroAtlas_County_LandCover.csv")
```

### 📝 Priority County-Level Metrics

1. **Developed Land Gain:** Increase in developed land area 2001-2021 (sq km, %)
2. **Forest Loss:** Decrease in forest cover 2001-2021 (sq km, %)
3. **Agricultural Land Change:** Net change in cropland and hay/pasture (sq km)
4. **Wetland Loss/Gain:** Net change in wetland area (sq km)
5. **Impervious Surface Increase:** Change in % impervious surface

---

## 🔟 NASA SEDAC GRIDDED POPULATION OF THE WORLD (GPW)

### 📊 Overview
The NASA Socioeconomic Data and Applications Center (SEDAC) produces the Gridded Population of the World (GPW), providing globally consistent population density grids at high spatial resolution.

**Coverage:**
- Global (including all US counties)
- Time series: 2000, 2005, 2010, 2015, 2020, 2025 (projected)
- Resolution: 30 arc-seconds (~1 km at equator)
- Population density and counts

### 🔢 Variables Available

| Variable | Description | Temporal Coverage |
|----------|-------------|-------------------|
| **Population Count** | Total population per grid cell | 2000-2025 (5-year intervals) |
| **Population Density** | Persons per square kilometer | 2000-2025 |
| **County Summaries** | Total population | 2000-2025 |
| | Mean population density | 2000-2025 |
| | Population-weighted density | 2000-2025 |
| | High-density area (>1000/sq km) | 2000-2025 |
| **Growth Metrics** | Population change 2000-2020 (count, %) | Periods |
| | Density change 2000-2020 | Periods |

**Total Variables:** ~8 base variables × 6 time periods = 48 variables

### 📡 Data Access

**Official Source:** NASA SEDAC
**URL:** https://sedac.ciesin.columbia.edu/data/collection/gpw-v4
**Latest Version:** GPWv4.11 (2018 release), GPWv5 in development
**Format:** GeoTIFF, NetCDF, Gridded ASCII
**Update Frequency:** ~5 years
**County summaries:** Must aggregate from rasters

### 💻 Python Code Example

```python
import rasterio
import geopandas as gpd
import numpy as np
from rasterstats import zonal_stats

# Download GPW population count raster (2020)
gpw_2020_url = "https://sedac.ciesin.columbia.edu/downloads/data/gpw-v4/..."
# Note: Actual download requires registration

# Read population raster
with rasterio.open("gpw_v4_population_count_2020.tif") as src:
    gpw_pop = src.read(1)
    gpw_transform = src.transform
    gpw_crs = src.crs

# Read county boundaries
counties = gpd.read_file("us_counties.shp").to_crs(gpw_crs)

# Calculate zonal statistics for each county
county_pop_stats = zonal_stats(
    counties,
    "gpw_v4_population_count_2020.tif",
    stats=['sum', 'mean', 'max', 'std'],
    geojson_out=True,
    nodata=-9999
)

# Convert to DataFrame
county_gpw = gpd.GeoDataFrame.from_features(county_pop_stats)
county_gpw = county_gpw.rename(columns={
    'sum': 'total_population_gpw_2020',
    'mean': 'mean_population_density_per_cell_2020',
    'max': 'max_population_per_cell_2020',
    'std': 'std_population_density_2020'
})

# Read population density raster
density_stats = zonal_stats(
    counties,
    "gpw_v4_population_density_2020.tif",
    stats=['mean', 'max'],
    geojson_out=False
)

county_gpw['mean_density_persons_sq_km_2020'] = [s['mean'] for s in density_stats]
county_gpw['max_density_persons_sq_km_2020'] = [s['max'] for s in density_stats]

# Calculate population-weighted density
# This requires cell-level calculation:
def population_weighted_density(county_geom, pop_raster, density_raster):
    """
    Calculate population-weighted density for a county.
    """
    # Mask rasters to county
    pop_masked = mask(pop_raster, [county_geom], crop=True)
    dens_masked = mask(density_raster, [county_geom], crop=True)

    # Population-weighted mean density
    pop_array = pop_masked[0]
    dens_array = dens_masked[0]

    # Filter valid cells
    valid = (pop_array > 0) & (dens_array > 0)

    if valid.sum() == 0:
        return np.nan

    pwd = np.average(dens_array[valid], weights=pop_array[valid])
    return pwd

# Apply to all counties (this is slow for large datasets)
# In practice, use parallelization or pre-computed summaries
```

### 📝 Priority County-Level Metrics

1. **Total Population (GPW):** County population from gridded data (comparison with Census)
2. **Mean Population Density:** Persons per square kilometer (county average)
3. **Population-Weighted Density:** Density weighted by population distribution
4. **High-Density Area %:** Percent of county with density >1,000 persons/sq km
5. **Population Growth Rate:** Percent change 2000-2020

**Use Case:** GPW provides consistent global methodology useful for:
- International comparisons
- Fine-scale population distribution (sub-county)
- Historical consistency (different from Census methods)
- Projected populations (2025)

---

## 📊 Summary Table: All Data Sources

| # | Data Source | Variables | Temporal Coverage | Spatial Resolution | Key Use Cases |
|---|-------------|-----------|-------------------|-------------------|---------------|
| 1 | EPA UCMR5 PFAS | 35 | 2023-2025 | PWS → county | Emerging drinking water contaminants |
| 2 | USACE Dam Inventory | 20 | Current + historical | Point → county | Dam failure risk, water infrastructure |
| 3 | WUI | 15 (×4 periods) | 1990, 2000, 2010, 2020 | 30m → county | Wildfire exposure to populations |
| 4 | EPA CyAN + NOAA HABSOS | 25 | 2016-present (CyAN), 2000-present (HAB) | Daily/event | Harmful algal bloom exposure |
| 5 | NRC Nuclear Plants | 15 | Current | Point → distance | Radiation exposure risk proximity |
| 6 | FHWA Bridge Inventory | 20 (×32 years) | 1992-present (annual) | Point → county | Infrastructure condition, safety |
| 7 | USFS Wildfire Hazard | 8 | 2020 | 270m → county | Wildfire risk potential |
| 8 | NOAA Sea Level Rise | 10 (×11 scenarios) | Scenarios 0-10 ft | Varies → county | Coastal flooding, climate adaptation |
| 9 | MRLC NLCD Change | ~190 | 2001-2021 (9 epochs) | 30m → county | Land cover change, urbanization |
| 10 | NASA SEDAC GPW | 8 (×6 periods) | 2000-2025 (5-year) | ~1 km → county | Population density, high-res distribution |

**Total Variables Documented:** 120+ priority variables

---

## 🔗 Integration with Existing GetData Documentation

These 10 data sources complement the existing comprehensive variable catalog:

### Cross-References

**PFAS (UCMR5)** complements:
- USGS_Water_Quality_Parameters_County_Level_COMPREHENSIVE.md
- UV_WATER_SUPERFUND_COMPREHENSIVE.md

**Infrastructure (Dams, Bridges, Nuclear)** complements:
- New infrastructure proximity category

**Wildfire (WUI, Wildfire Hazard)** complements:
- WILDFIRE_TRAFFIC_WALKABILITY_HAZWASTE_COMPREHENSIVE.md
- NOAA_HMS_SMOKE_COMPREHENSIVE.md (if exists)

**Coastal Hazards (HABs, Sea Level Rise)** complements:
- USGS_Water_Quality_Parameters_County_Level_COMPREHENSIVE.md (water quality)
- INTERNATIONAL_CLIMATE_ATMOSPHERIC_SOURCES.md (climate)

**Land Change (NLCD)** complements:
- NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md
- GREEN_PEST_OCC_VECTOR_SOCIAL_COMPREHENSIVE.md (green space)

**Population (GPW)** complements:
- Existing Census demographic data
- Alternative high-resolution population distribution

---

## 💻 County-Level Panel Data Construction

### Recommended Data Structure

For panel data analysis (county × year), prioritize:

**Infrastructure (Static/Slow-Changing):**
- Distance to nearest nuclear plant (static)
- Dam counts and characteristics (updated irregularly)
- Bridge condition (annual 1992-present)

**Exposures (Time-Varying):**
- PFAS detections (2023-2025 monitoring period)
- HAB events (annual counts 2000-present)
- Wildfire hazard (decadal 2020, 2025 expected)
- WUI population (decadal 1990-2020)
- NLCD land cover (9 epochs 2001-2021)

**Coastal Hazards (Scenario-Based):**
- Sea level rise exposure (projections, not time series)
- Use as cross-sectional vulnerability indicator

### Example R Panel Construction

```r
library(tidyverse)

# Start with county-year panel skeleton
county_panel <- expand_grid(
  GEOID = unique_county_fips,
  year = 1990:2024
)

# Add infrastructure (time-invariant or slow-changing)
county_panel <- county_panel %>%
  left_join(nuclear_distance, by = "GEOID") %>%  # Static
  left_join(dam_counts_current, by = "GEOID") %>%  # ~Current
  left_join(bridge_condition_annual, by = c("GEOID", "year"))  # Annual

# Add exposures (time-varying)
county_panel <- county_panel %>%
  left_join(wui_decadal, by = c("GEOID", "year")) %>%  # Carry forward
  left_join(hab_events_annual, by = c("GEOID", "year")) %>%
  left_join(nlcd_change_epochs, by = c("GEOID", "year"))  # Carry forward

# Forward fill decadal variables
county_panel <- county_panel %>%
  group_by(GEOID) %>%
  arrange(year) %>%
  fill(wui_population_pct, wui_area_sq_km, .direction = "down") %>%
  ungroup()
```

---

## 📚 Citation

If using these data sources in research, cite both the original data providers and this documentation:

**Data Sources:** See individual sections for official citations

**This Documentation:**
> GetData Project. (2025). *Infrastructure and Coastal Contaminants - Comprehensive Documentation: US County-Level Critical Infrastructure and Emerging Contaminant Data Sources.* Version 3.8.

---

## 📧 Questions & Updates

For questions about these data sources or to suggest additional infrastructure/coastal data sources, please contact the GetData project maintainers.

**Last Updated:** November 13, 2025
**Version:** 3.8 - Initial Infrastructure and Coastal Contaminants Documentation
