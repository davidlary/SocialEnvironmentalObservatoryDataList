# Hydrology, Wetlands, and Floodplains Data Sources
## Water Systems and Flood Risk Data for US County-Level Health Analysis

**Last Updated:** November 12, 2025
**Status:** NEW - Physical Geography Gap Analysis
**Priority:** HIGHEST - Critical for waterborne disease, flooding disasters, vector habitat

---

## EXECUTIVE SUMMARY

This document catalogs **3 federal data sources** providing comprehensive hydrology, wetlands, and flood hazard data aggregated to US county level. These sources are essential for understanding:

1. **Waterborne disease risk** (surface water networks, contamination pathways)
2. **Vector-borne disease** (wetland mosquito/tick habitat)
3. **Flood disasters** (exposure, injury, PTSD, infrastructure damage)
4. **Water security** (watershed boundaries, water availability)
5. **Environmental quality** (wetland ecosystem services, water purification)

**CRITICAL IMPORTANCE:** Hydrology/wetlands/floodplains affect:
- **Waterborne disease:** ~7.2 million illnesses/year in US from contaminated water
- **Vector-borne disease:** Wetlands = primary mosquito habitat (WNV, EEE, malaria emerging)
- **Flood mortality:** ~90 deaths/year in US from flooding, thousands injured
- **Mental health:** PTSD from flooding affects 25-50% of disaster survivors
- **Healthcare access:** Floods disrupt services, medication access

**ALL SOURCES ARE FREE AND OPEN ACCESS** ✅

---

## TABLE OF CONTENTS

### PART 1: WATERSHEDS & STREAM NETWORKS
1. [USGS Watershed Boundary Dataset (WBD)](#1-usgs-watershed-boundary-dataset)
2. [USGS National Hydrography Dataset (NHD)](#2-usgs-national-hydrography-dataset)

### PART 2: WETLANDS
3. [FWS National Wetlands Inventory (NWI)](#3-fws-national-wetlands-inventory)

### PART 3: FLOODPLAINS
4. [FEMA National Flood Hazard Layer (NFHL)](#4-fema-national-flood-hazard-layer)

### PART 4: DATA COLLECTION WORKFLOWS
5. [County Aggregation Methods](#county-aggregation-methods)
6. [Derived Health Indicators](#derived-health-indicators)

---

## PART 1: WATERSHEDS & STREAM NETWORKS

### 1. USGS WATERSHED BOUNDARY DATASET (WBD) ⭐⭐⭐⭐⭐

**PRIORITY RANK: #1 for Understanding Water Flow Paths**

#### **Overview**

**What:** Hierarchical watershed boundaries defining surface water drainage
**Who:** US Geological Survey (USGS)
**Resolution:** 6 hierarchical levels (HUC2 to HUC12)
**Coverage:** All 50 states + territories
**Temporal:** Static with periodic updates
**Update Frequency:** Continuous refinements

**Why WBD/HUC is Critical:**
- **Waterborne disease** spreads along watersheds (contamination flows downstream)
- **Water security** defined by watershed boundaries (shared water resources)
- **Flood risk** determined by watershed characteristics (size, slope, land cover)
- **Environmental planning** requires watershed-scale analysis

**Hydrologic Unit Codes (HUC) Hierarchy:**
- **HUC2** (21 regions) - Major river basins (e.g., Mississippi, Colorado)
- **HUC4** (222 subregions) - Large river systems
- **HUC6** (378 basins) - River basins
- **HUC8** (2,300 subbasins) - County-size watersheds ⭐ **OPTIMAL FOR COUNTY ANALYSIS**
- **HUC10** (22,000 watersheds) - Township-size
- **HUC12** (104,000 subwatersheds) - Neighborhood-size

#### **Variables Available (15 metrics)**

**Watershed Identification:**
1. **HUC8 code** - 8-digit watershed identifier
2. **HUC8 name** - Watershed name
3. **HUC8 area** - km²
4. **Number of HUC8s per county** - Watershed complexity

**Watershed Characteristics:**
5. **Dominant HUC8** - Largest watershed by area
6. **Percent area in each HUC8** - Spatial allocation
7. **Upstream drainage area** - Total contributing area (km²)
8. **Downstream connectivity** - Which watersheds receive drainage

**Derived Metrics:**
9. **Watershed fragmentation** - Number of HUCs / county area
10. **Cross-county watersheds** - Shared water resources
11. **Headwater vs. downstream** - Position in drainage network
12. **Watershed complexity index** - Number of HUC levels present

**Public Health Relevance:**
13. **Contamination source tracking** - Identify upstream counties
14. **Waterborne disease risk** - Downstream exposure
15. **Water conflict potential** - Shared watershed resources

#### **Data Access**

**Portal:** https://www.usgs.gov/national-hydrography/watershed-boundary-dataset

**Download Options:**

**1. National Map Downloader:**
```r
# Manual download
# URL: https://apps.nationalmap.gov/downloader/
# Select "Watershed Boundary Dataset (WBD)"
# Choose HUC level (HUC8 recommended for counties)
# Download shapefile

library(sf)

# Load HUC8 watersheds
huc8 <- st_read("WBD_HUC8_national.shp")

# Load counties
counties <- st_read("tl_2020_us_county.shp")

# Intersect to find which HUC8s overlap each county
county_huc8 <- st_intersection(huc8, counties) %>%
  mutate(area_m2 = as.numeric(st_area(.))) %>%
  group_by(GEOID, HUC8, NAME) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop") %>%
  group_by(GEOID) %>%
  mutate(pct_area = area_m2 / sum(area_m2) * 100)

# Dominant HUC8 per county
dominant_huc8 <- county_huc8 %>%
  slice_max(pct_area, n = 1, by = GEOID)
```

**2. USGS National Hydrography API:**
```r
library(httr)
library(jsonlite)

# WFS service for WBD
wfs_url <- "https://hydro.nationalmap.gov/arcgis/services/wbd/MapServer/WFSServer"

# Query HUC8 for a bounding box
bbox <- c(-122.5, 37.0, -121.5, 38.0) # West, South, East, North

response <- GET(wfs_url, query = list(
  service = "WFS",
  request = "GetFeature",
  typename = "wbd:HUC8",
  bbox = paste(bbox, collapse = ","),
  outputFormat = "json"
))

huc8_data <- st_read(content(response, "text"))
```

**3. HUC Crosswalk (Pre-calculated County-HUC relationships):**
```r
# USGS provides pre-calculated county-to-HUC crosswalks
# URL: https://www.usgs.gov/national-hydrography/watershed-boundary-dataset

# Example structure:
# COUNTY_FIPS, HUC8, PCT_AREA
county_huc_xwalk <- read_csv("county_huc8_crosswalk.csv") %>%
  mutate(FIPS = str_pad(COUNTY_FIPS, width = 5, side = "left", pad = "0"))
```

#### **County-Level Aggregation**

**Method 1: Dominant Watershed**

```r
# Most common approach: Assign each county to its dominant HUC8

county_watershed <- county_huc8 %>%
  group_by(GEOID) %>%
  slice_max(pct_area, n = 1) %>%
  select(GEOID, HUC8_dominant = HUC8, HUC8_name = NAME, HUC8_pct = pct_area)
```

**Method 2: Multiple Watersheds per County**

```r
# More accurate: Keep all HUC8s that overlap each county
# Use for waterborne disease modeling (all potential source watersheds)

county_watersheds_all <- county_huc8 %>%
  filter(pct_area > 5) %>% # Keep HUC8s covering >5% of county
  arrange(GEOID, desc(pct_area))

# Calculate watershed complexity
county_watershed_complexity <- county_watersheds_all %>%
  group_by(GEOID) %>%
  summarize(
    n_watersheds = n(),
    watershed_complexity_index = n_watersheds / sum(pct_area) * 100
  )
```

**Method 3: Upstream-Downstream Relationships**

```r
# Identify upstream counties (potential contamination sources)

# Load HUC8 with flow direction
huc8_flow <- st_read("WBD_HUC8_with_flowlines.shp")

# For each county, find upstream HUC8s
county_upstream <- county_huc8 %>%
  left_join(huc8_flow %>% select(HUC8, DOWNSTREAM_HUC = TONEXTHUC), by = "HUC8") %>%
  group_by(GEOID) %>%
  summarize(
    upstream_huc8s = list(unique(HUC8)),
    n_upstream = length(unique(HUC8))
  )
```

#### **Derived Health Indicators**

**1. Waterborne Disease Risk (Downstream Position)**

```r
# Downstream counties have higher contamination risk from upstream sources

county_waterborne_watershed <- county_upstream %>%
  left_join(dominant_huc8, by = "GEOID") %>%
  mutate(
    # More upstream sources = higher risk
    upstream_contamination_risk = log(n_upstream + 1),

    # Position in watershed
    headwater_county = n_upstream <= 2,
    downstream_county = n_upstream > 10,

    # High risk if many upstream counties + shared water source
    high_waterborne_risk = (n_upstream > 5) & (HUC8_pct > 50)
  )

# Health associations:
# - Downstream position → cumulative contamination → Cryptosporidium, Giardia, E. coli
# - Agricultural runoff (nitrates, pesticides) accumulates downstream
# - Industrial contamination flows downstream
```

**2. Water Conflict Potential (Shared Watersheds)**

```r
# Counties sharing watersheds compete for water resources

county_water_conflict <- county_huc8 %>%
  group_by(HUC8) %>%
  mutate(n_counties_in_huc = n_distinct(GEOID)) %>%
  ungroup() %>%
  group_by(GEOID) %>%
  summarize(
    shared_watersheds = sum(n_counties_in_huc > 1),
    water_conflict_potential = mean(n_counties_in_huc[n_counties_in_huc > 1])
  )

# Health associations:
# - Water scarcity → food insecurity (agricultural impacts)
# - Water conflict → stress, mental health
# - Competing demands (drinking, agriculture, industry)
```

#### **Data Quality**

**Strengths:**
- ✅ **National standard** (all agencies use HUC codes)
- ✅ **Hierarchical** (flexible scale HUC2-HUC12)
- ✅ **Free and open**
- ✅ **Well-documented** (extensive metadata)

**Limitations:**
- ⚠️ **Static boundaries** (don't capture dynamic flow patterns)
- ⚠️ **County misalignment** (watersheds don't respect political boundaries)

**Priority Variables:**
1. Dominant HUC8 code
2. Dominant HUC8 name
3. Number of HUC8s per county
4. Upstream watershed count
5. Downstream position indicator

---

### 2. USGS NATIONAL HYDROGRAPHY DATASET (NHD) ⭐⭐⭐⭐

**PRIORITY RANK: #2 for Stream Networks**

#### **Overview**

**What:** National surface water network (streams, rivers, lakes, wetlands)
**Who:** US Geological Survey
**Resolution:** 1:24,000 (high resolution) or 1:100,000 (medium resolution)
**Coverage:** All 50 states
**Temporal:** Periodic updates
**Update Frequency:** Continuous improvements

**Why NHD is Important:**
- **Stream density** → waterborne disease transmission routes
- **Surface water proximity** → contamination exposure
- **Water availability** → food security, health
- **Recreation water** → pathogen exposure (swimming, fishing)

#### **Variables Available (20+ metrics)**

**Stream Network:**
1. **Total stream length** - km
2. **Stream density** - km per km²
3. **Perennial streams** - Year-round flow (km)
4. **Intermittent streams** - Seasonal flow (km)
5. **Ephemeral streams** - Flow only after rain (km)

**Water Bodies:**
6. **Lake area** - km²
7. **Reservoir area** - km²
8. **Number of lakes** - count
9. **Number of reservoirs** - count

**Stream Order:**
10. **Strahler stream order** - 1st order (headwater) to 8th order (major rivers)
11. **Length by stream order** - Distribution of stream sizes

**Derived Metrics:**
12. **Stream network complexity** - Ratio of higher-order to lower-order streams
13. **Water availability index** - Perennial stream density
14. **Recreation water area** - Lake + reservoir area

#### **Data Access**

```r
# Download NHD via National Map
# URL: https://apps.nationalmap.gov/downloader/
# Select "National Hydrography Dataset (NHD)"

library(sf)
library(tidyverse)

# Load NHD flowlines (streams)
nhd_streams <- st_read("NHD_Flowline.shp")

# Load counties
counties <- st_read("tl_2020_us_county.shp")

# Intersect streams with counties
county_streams <- st_intersection(nhd_streams, counties) %>%
  mutate(length_m = as.numeric(st_length(.))) %>%
  group_by(GEOID, FCODE) %>% # FCODE = feature type (perennial, intermittent, etc.)
  summarize(length_m = sum(length_m), .groups = "drop")

# Calculate stream density
county_stream_density <- counties %>%
  mutate(area_m2 = as.numeric(st_area(.))) %>%
  left_join(
    county_streams %>%
      group_by(GEOID) %>%
      summarize(total_stream_length_m = sum(length_m)),
    by = "GEOID"
  ) %>%
  mutate(
    stream_density_km_per_km2 = (total_stream_length_m / 1000) / (area_m2 / 1e6)
  )
```

#### **Derived Health Indicators**

```r
# High stream density → more surface water contact → higher waterborne disease risk
county_stream_health <- county_stream_density %>%
  mutate(
    high_stream_density = stream_density_km_per_km2 > 1.0, # >1 km/km²
    water_contact_potential = stream_density_km_per_km2 * 10, # 0-100 scale

    # Recreation water exposure
    recreation_water_risk = (lake_area_km2 + reservoir_area_km2) > 5
  )

# Health associations:
# - Stream contact → Giardia, Cryptosporidium, Leptospirosis
# - Lake swimming → swimmer's itch, harmful algal blooms
```

**Priority Variables:**
1. Stream density (km/km²)
2. Perennial stream length (km)
3. Lake area (km²)
4. Water contact potential score

---

## PART 2: WETLANDS

### 3. FWS NATIONAL WETLANDS INVENTORY (NWI) ⭐⭐⭐⭐⭐

**PRIORITY RANK: #3 for Vector Habitat & Water Quality**

#### **Overview**

**What:** National wetlands mapping with detailed classification
**Who:** US Fish & Wildlife Service (FWS)
**Resolution:** 1:24,000 to 1:12,000 (1-5 acre minimum mapping unit)
**Coverage:** 95%+ of US (remaining areas in progress)
**Temporal:** Aerial photo interpretation (vintage 1970s-2020s, varies by state)
**Update Frequency:** Rolling updates as new imagery available

**Why NWI is Critical:**
- **Vector-borne disease** → Wetlands = PRIMARY mosquito habitat (80%+ of breeding)
- **Water quality** → Wetlands filter contaminants, reduce flooding
- **Waterborne disease** → Wetland buffers reduce pathogen transport
- **Ecosystem services** → Carbon storage, biodiversity

**NWI is MORE DETAILED than NLCD wetlands:** 29 wetland types vs. 2 NLCD classes

#### **Variables Available (29 wetland types + derived metrics)**

**Cowardin Wetland Classification System:**

**Palustrine (Freshwater Non-Tidal):**
1. **Forested wetland (PFO)** - Swamps, bottomland hardwoods
2. **Shrub wetland (PSS)** - Shrub swamps
3. **Emergent wetland (PEM)** - Marshes, wet meadows
4. **Aquatic bed (PAB)** - Submerged vegetation
5. **Unconsolidated shore (PUS)** - Mud flats
6. **Open water (POW)** - Ponds <20 acres

**Lacustrine (Lake):**
7. **Littoral (L1)** - Shallow lake edge
8. **Limnetic (L2)** - Open lake water

**Riverine (River/Stream):**
9. **Tidal (R1)** - Tidal rivers
10. **Upper perennial (R2)** - Perennial streams
11. **Intermittent (R4)** - Seasonal streams
12. **Lower perennial (R3)** - Large rivers

**Estuarine (Coastal):**
13. **Intertidal (E2)** - Salt marshes, mudflats
14. **Subtidal (E1)** - Submerged coastal

**Marine (Ocean):**
15. **Intertidal (M2)** - Rocky shores, beaches
16. **Subtidal (M1)** - Offshore

**Water Regime Modifiers:**
17. **Permanently flooded (H)** - Year-round water
18. **Intermittently flooded (J)** - Seasonal flooding
19. **Temporarily flooded (A)** - Brief spring flooding
20. **Saturated (B)** - Waterlogged soil, no standing water

**Derived County Metrics:**
21. **Total wetland area** - km²
22. **Percent wetland cover** - %
23. **Wetland density** - wetlands per km²
24. **Wetland fragmentation** - Number of discrete wetlands
25. **Dominant wetland type** - Most common class
26. **Mosquito-prone wetlands** - PEM + PSS (emergent + shrub)
27. **Water quality wetlands** - PFO (forested)
28. **Coastal wetlands** - Estuarine + Marine
29. **Wetland loss** - Compare historical to current (if data available)

#### **Data Access**

**Portal:** https://www.fws.gov/program/national-wetlands-inventory

**Download Options:**

**1. FWS Wetlands Mapper (Web Interface):**
```r
# Manual download from web mapper
# URL: https://www.fws.gov/wetlands/data/mapper.html
# Define AOI (county, state)
# Download shapefile

library(sf)
library(tidyverse)

# Load NWI wetlands
nwi <- st_read("NWI_wetlands.shp")

# Load counties
counties <- st_read("tl_2020_us_county.shp")

# Intersect wetlands with counties
county_wetlands <- st_intersection(nwi, counties) %>%
  mutate(area_m2 = as.numeric(st_area(.))) %>%
  group_by(GEOID, WETLAND_TYPE, ATTRIBUTE) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop")

# Calculate wetland statistics
county_wetland_summary <- county_wetlands %>%
  group_by(GEOID) %>%
  summarize(
    total_wetland_area_km2 = sum(area_m2) / 1e6,
    n_wetlands = n(),
    wetland_density = n() / (sum(area_m2) / 1e6),
    .groups = "drop"
  ) %>%
  left_join(
    counties %>% mutate(county_area_km2 = as.numeric(st_area(.)) / 1e6) %>% st_drop_geometry(),
    by = "GEOID"
  ) %>%
  mutate(
    pct_wetland = total_wetland_area_km2 / county_area_km2 * 100
  )
```

**2. NWI WMS/WFS Service (Programmatic Access):**
```r
library(httr)

# WFS endpoint
wfs_url <- "https://www.fws.gov/wetlands/arcgis/services/Wetlands/MapServer/WFSServer"

# Query wetlands for bounding box
bbox <- c(-122.5, 37.0, -121.5, 38.0)

response <- GET(wfs_url, query = list(
  service = "WFS",
  request = "GetFeature",
  typename = "Wetlands:Wetlands",
  bbox = paste(bbox, collapse = ","),
  outputFormat = "json"
))

nwi_wetlands <- st_read(content(response, "text"))
```

**3. FWS Download Repository (State-Level):**
```bash
# Download state wetlands data
# URL: https://www.fws.gov/program/national-wetlands-inventory/download-state-wetlands-data

# Example: California wetlands
wget https://www.fws.gov/wetlands/downloads/CA_geodatabase.zip
unzip CA_geodatabase.zip
```

#### **County-Level Aggregation**

**Method: Classify Wetlands by Health Relevance**

```r
# Classify wetland types into mosquito habitat categories
classify_mosquito_habitat <- function(wetland_type) {
  # HIGH: Emergent and shrub wetlands (standing water + vegetation)
  high_habitat <- c("PEM", "PSS", "PEM1", "PSS1", "E2EM", "E2SS")

  # MODERATE: Forested wetlands, aquatic beds
  mod_habitat <- c("PFO", "PAB", "PFO1", "PAB1")

  # LOW: Open water (fish predation reduces mosquitoes)
  low_habitat <- c("POW", "L1", "L2", "R2", "R3")

  case_when(
    str_detect(wetland_type, paste(high_habitat, collapse = "|")) ~ "High",
    str_detect(wetland_type, paste(mod_habitat, collapse = "|")) ~ "Moderate",
    str_detect(wetland_type, paste(low_habitat, collapse = "|")) ~ "Low",
    TRUE ~ "Unknown"
  )
}

county_mosquito_habitat <- county_wetlands %>%
  mutate(mosquito_habitat_class = classify_mosquito_habitat(WETLAND_TYPE)) %>%
  group_by(GEOID, mosquito_habitat_class) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop") %>%
  pivot_wider(names_from = mosquito_habitat_class, values_from = area_m2, values_fill = 0) %>%
  mutate(
    mosquito_habitat_index = (High * 1.0 + Moderate * 0.5) / 1e6, # km²
    high_mosquito_risk = High / 1e6 > 10 # >10 km² high-risk wetlands
  )
```

#### **Derived Health Indicators from Wetlands**

**1. Vector-Borne Disease Risk (Wetland Type)**

```r
# Emergent marshes = HIGHEST mosquito breeding habitat

county_vector_wetland <- county_mosquito_habitat %>%
  left_join(county_wetland_summary, by = "GEOID") %>%
  mutate(
    # Mosquito habitat suitability
    mosquito_habitat_km2 = mosquito_habitat_index,
    vector_risk_score = mosquito_habitat_index * 10, # 0-100 scale

    # West Nile Virus risk (wetland + climate)
    wnv_risk_wetland = (mosquito_habitat_km2 > 5) & (mean_temp_summer > 25),

    # Eastern Equine Encephalitis (freshwater swamps)
    eee_risk = (High / 1e6 > 20) # >20 km² emergent wetlands
  )

# Health associations:
# - Emergent wetlands → Culex mosquitoes → West Nile Virus (2,000-3,000 cases/year US)
# - Freshwater swamps → Culiseta melanura → Eastern Equine Encephalitis (~10 cases/year, 30% fatality)
# - Coastal marshes → Aedes sollicitans → Dengue, Zika (emerging threats)
# - Wetlands → tick habitat (Ixodes scapularis) → Lyme disease
```

**2. Water Quality Benefits (Forested Wetlands)**

```r
# Forested wetlands filter nutrients, pathogens

county_water_quality_wetland <- county_wetlands %>%
  mutate(is_forested = str_detect(WETLAND_TYPE, "PFO")) %>%
  group_by(GEOID) %>%
  summarize(
    forested_wetland_km2 = sum(area_m2[is_forested]) / 1e6,
    water_quality_benefit_score = forested_wetland_km2 * 2 # Ecosystem service value
  ) %>%
  mutate(
    adequate_wetland_buffer = forested_wetland_km2 > 5, # >5 km² = good
    waterborne_disease_protection = adequate_wetland_buffer
  )

# Health associations:
# - Forested wetlands → filter pathogens → reduce waterborne disease (Crypto, Giardia, E. coli)
# - Wetland buffers → reduce nitrate, phosphorus → prevent harmful algal blooms
# - Wetland loss → increased flood risk, contamination
```

**3. Flood Attenuation (All Wetlands)**

```r
# Wetlands absorb flood waters, reduce peak flows

county_flood_wetland <- county_wetland_summary %>%
  mutate(
    flood_attenuation_capacity = total_wetland_area_km2 * pct_wetland,
    flood_protection_adequate = pct_wetland > 10, # >10% wetland coverage
    flood_risk_from_wetland_loss = pct_wetland < 5 # <5% = high flood risk
  )

# Health associations:
# - Wetland loss → increased flooding → injury, PTSD, infrastructure damage
# - Wetlands reduce flood peaks by 20-80% (varies by wetland type)
```

**4. Recreational Water Exposure (Open Water Wetlands)**

```r
# Open water wetlands attract recreation → pathogen exposure

county_recreation_wetland <- county_wetlands %>%
  mutate(is_open_water = str_detect(WETLAND_TYPE, "POW|L2|PAB")) %>%
  group_by(GEOID) %>%
  summarize(
    recreation_wetland_km2 = sum(area_m2[is_open_water]) / 1e6
  ) %>%
  mutate(
    recreation_exposure_potential = recreation_wetland_km2 > 1, # >1 km² open water
    harmful_algal_bloom_risk = recreation_wetland_km2 > 5 # Larger water bodies
  )

# Health associations:
# - Swimming in wetlands → Giardia, Cryptosporidium, Leptospirosis
# - Harmful algal blooms → microcystin toxicity → liver damage
```

#### **Data Quality**

**Strengths:**
- ✅ **Most detailed wetland classification** (29 types vs. 2 NLCD)
- ✅ **National coverage** (95%+ US)
- ✅ **Health-relevant categories** (mosquito habitat identifiable)
- ✅ **Free and open**

**Limitations:**
- ⚠️ **Variable vintage** (some areas 1970s, others 2020s)
- ⚠️ **Static** (doesn't capture seasonal changes in wetland extent)
- ⚠️ **Aerial photo interpretation** (accuracy varies)

**Validation:**
- Ground-truthing studies show 85-95% accuracy for wetland presence/absence
- Classification accuracy ~70-85% for detailed wetland types

**Priority Variables for Health Observatory:**
1. **Total wetland area (km²)**
2. **Percent wetland cover (%)**
3. **Emergent wetland area (km²)** - Mosquito habitat
4. **Forested wetland area (km²)** - Water quality
5. **Wetland density (wetlands/km²)** - Fragmentation
6. **Mosquito habitat index** - Vector risk
7. **Water quality benefit score** - Ecosystem service
8. **Flood attenuation capacity**

---

## PART 3: FLOODPLAINS

### 4. FEMA NATIONAL FLOOD HAZARD LAYER (NFHL) ⭐⭐⭐⭐⭐

**PRIORITY RANK: #4 for Flood Disaster Risk**

#### **Overview**

**What:** Detailed flood hazard zones for regulatory and insurance purposes
**Who:** Federal Emergency Management Agency (FEMA)
**Resolution:** Property-level (detailed engineering studies)
**Coverage:** ~60% of US (all studied communities, ~22,000 communities)
**Temporal:** Rolling updates as flood studies completed
**Update Frequency:** Continuous community updates

**Why NFHL is Critical:**
- **Flood mortality** → ~90 deaths/year US, thousands injured
- **Flood morbidity** → PTSD (25-50% of survivors), injuries, drowning
- **Healthcare disruption** → Floods damage hospitals, clinics, medication access
- **Chronic disease exacerbation** → Medication interruption, stress
- **Mental health** → Anxiety, depression, PTSD from flooding

**NFHL is MORE DETAILED than NLCD floodplains:** Differentiates 100-year, 500-year, floodways

#### **Variables Available (20 flood zone types + derived metrics)**

**Special Flood Hazard Areas (SFHA) - 100-Year Flood:**
1. **Zone A** - 1% annual chance flood (100-year), no base flood elevation (BFE) determined
2. **Zone AE** - 1% annual chance, BFE determined
3. **Zone AH** - 1% annual chance, ponding (1-3 feet depth)
4. **Zone AO** - 1% annual chance, sheet flow (1-3 feet depth)
5. **Zone A99** - 1% annual chance, protected by levee under construction
6. **Floodway** - HIGHEST RISK - rapidly flowing water during flood

**Moderate Flood Hazard:**
7. **Zone X (shaded)** - 0.2% annual chance (500-year flood)

**Minimal Flood Hazard:**
8. **Zone X (unshaded)** - <0.2% annual chance
9. **Zone C** - Minimal flood hazard (older maps)

**Coastal Flood Hazards:**
10. **Zone V/VE** - Coastal high hazard (wave action + 1% flood)

**Derived County Metrics:**
11. **Percent area in 100-year floodplain** - %
12. **Percent area in 500-year floodplain** - %
13. **Percent area in floodway** - %
14. **Population in floodplain** - Number of people
15. **Housing units in floodplain** - Number of structures
16. **Critical facilities in floodplain** - Hospitals, fire, police
17. **Flood exposure index** - Weighted by flood frequency + depth
18. **Repetitive loss properties** - Structures flooded multiple times
19. **Coastal flood exposure** - Zone V area
20. **Flood insurance take-up rate** - % policies in SFHA

#### **Data Access**

**Portal:** https://www.fema.gov/flood-maps/national-flood-hazard-layer

**Download Options:**

**1. FEMA Map Service Center:**
```r
# Manual download
# URL: https://msc.fema.gov/portal/advanceSearch
# Search by county name/FIPS
# Download "NFHL" data (shapefile or geodatabase)

library(sf)
library(tidyverse)

# Load NFHL flood zones
nfhl <- st_read("NFHL_FloodHazardZones.shp")

# Load counties
counties <- st_read("tl_2020_us_county.shp")

# Intersect flood zones with counties
county_flood <- st_intersection(nfhl, counties) %>%
  mutate(area_m2 = as.numeric(st_area(.))) %>%
  group_by(GEOID, FLD_ZONE) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop")

# Calculate flood statistics
county_flood_summary <- county_flood %>%
  mutate(
    is_100yr = FLD_ZONE %in% c("A", "AE", "AH", "AO", "A99", "V", "VE"),
    is_500yr = FLD_ZONE %in% c("X", "0.2 PCT ANNUAL CHANCE FLOOD HAZARD"),
    is_floodway = FLD_ZONE == "FLOODWAY"
  ) %>%
  group_by(GEOID) %>%
  summarize(
    flood_100yr_km2 = sum(area_m2[is_100yr]) / 1e6,
    flood_500yr_km2 = sum(area_m2[is_500yr]) / 1e6,
    floodway_km2 = sum(area_m2[is_floodway]) / 1e6
  ) %>%
  left_join(
    counties %>% mutate(county_area_km2 = as.numeric(st_area(.)) / 1e6) %>% st_drop_geometry(),
    by = "GEOID"
  ) %>%
  mutate(
    pct_flood_100yr = flood_100yr_km2 / county_area_km2 * 100,
    pct_flood_500yr = flood_500yr_km2 / county_area_km2 * 100
  )
```

**2. FEMA REST API:**
```r
library(httr)
library(jsonlite)

# Query flood hazard for a county
county_fips <- "48201" # Harris County, TX (Houston)

url <- "https://hazards.fema.gov/gis/nfhl/rest/services/public/NFHL/MapServer/28/query"

response <- GET(url, query = list(
  where = paste0("DFIRM_ID LIKE '", county_fips, "%'"),
  outFields = "*",
  f = "json"
))

flood_zones <- fromJSON(content(response, "text"))$features
```

#### **County-Level Aggregation**

**Method: Classify Flood Zones by Risk**

```r
# High, moderate, low flood risk categories

classify_flood_risk <- function(zone) {
  high_risk <- c("A", "AE", "AH", "AO", "V", "VE", "FLOODWAY")
  moderate_risk <- c("X", "0.2 PCT ANNUAL CHANCE FLOOD HAZARD", "A99")

  case_when(
    zone %in% high_risk ~ "High",
    zone %in% moderate_risk ~ "Moderate",
    TRUE ~ "Low"
  )
}

county_flood_risk <- county_flood %>%
  mutate(risk_class = classify_flood_risk(FLD_ZONE)) %>%
  group_by(GEOID, risk_class) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop") %>%
  pivot_wider(names_from = risk_class, values_from = area_m2, values_fill = 0) %>%
  mutate(
    flood_risk_score = (High / 1e6) * 1.0 + (Moderate / 1e6) * 0.2,
    high_flood_risk_county = (High / 1e6) > 50 # >50 km² high-risk
  )
```

#### **Derived Health Indicators from Floodplains**

**1. Flood Mortality/Injury Risk**

```r
# Population in floodplain = exposure

# Load population data (block-level for precision)
pop_blocks <- st_read("tl_2020_tabblock.shp") %>%
  select(GEOID_block = GEOID, POP = POP20)

# Intersect population with flood zones
pop_flood <- st_intersection(pop_blocks, nfhl) %>%
  mutate(
    is_100yr = FLD_ZONE %in% c("A", "AE", "AH", "AO", "V", "VE"),
    pop_at_risk = POP * (as.numeric(st_area(.)) / as.numeric(st_area(geometry)))
  ) %>%
  st_drop_geometry() %>%
  group_by(GEOID, is_100yr) %>%
  summarize(pop_at_risk = sum(pop_at_risk, na.rm = TRUE), .groups = "drop")

# County-level flood exposure
county_flood_exposure <- pop_flood %>%
  filter(is_100yr) %>%
  left_join(
    pop_blocks %>% st_drop_geometry() %>% group_by(GEOID) %>% summarize(total_pop = sum(POP)),
    by = "GEOID"
  ) %>%
  mutate(
    pct_pop_floodplain = pop_at_risk / total_pop * 100,
    flood_mortality_risk = pop_at_risk * 0.0003, # Historical mortality rate ~0.03%
    flood_injury_risk = pop_at_risk * 0.003 # Injury rate ~0.3%
  )

# Health associations:
# - Drowning (leading cause of flood death)
# - Trauma (debris, structural collapse)
# - Electrocution (flooded electrical systems)
# - Carbon monoxide poisoning (generators in enclosed spaces)
```

**2. Flood PTSD Risk**

```r
# Mental health impacts disproportionate to physical injuries

county_flood_mental_health <- county_flood_exposure %>%
  mutate(
    # PTSD affects 25-50% of disaster survivors
    ptsd_cases_potential = pop_at_risk * 0.35, # 35% average

    # Depression, anxiety
    mental_health_burden = ptsd_cases_potential * 5, # Disability-adjusted life years
    high_mental_health_risk = pct_pop_floodplain > 10 # >10% exposed
  )

# Health associations:
# - PTSD: flashbacks, nightmares, hypervigilance
# - Depression: prolonged recovery, displacement
# - Anxiety: future flood worry
# - Substance abuse: coping mechanism
```

**3. Healthcare Infrastructure Flood Risk**

```r
# Critical facilities in floodplains = service disruption

# Load critical facilities (hospitals, clinics)
hospitals <- st_read("hospitals.shp")

# Intersect with flood zones
hospitals_flood <- st_join(hospitals, nfhl) %>%
  mutate(
    in_100yr_floodplain = FLD_ZONE %in% c("A", "AE", "AH", "AO", "V", "VE"),
    in_floodway = FLD_ZONE == "FLOODWAY"
  ) %>%
  st_drop_geometry() %>%
  group_by(GEOID) %>%
  summarize(
    n_hospitals = n(),
    n_hospitals_flood_risk = sum(in_100yr_floodplain, na.rm = TRUE),
    pct_hospitals_at_risk = n_hospitals_flood_risk / n_hospitals * 100
  )

# Health associations:
# - Hospital flooding → service interruption → excess mortality
# - Pharmacy flooding → medication access disruption → chronic disease exacerbation
# - Nursing homes in floodplains → evacuation challenges → mortality
```

**4. Waterborne Disease Post-Flood**

```r
# Flooding mixes sewage, industrial chemicals → contamination

county_post_flood_disease <- county_flood_risk %>%
  mutate(
    sewage_overflow_risk = flood_risk_score * septic_system_pct, # Septic failure
    industrial_contamination_risk = flood_risk_score * n_industrial_facilities,

    # Waterborne disease outbreak potential
    crypto_outbreak_risk = (flood_risk_score > 10) & (pct_flood_100yr > 5),
    hepatitis_a_risk = (flood_risk_score > 15) & (pct_flood_100yr > 10)
  )

# Health associations:
# - Sewage mixing → E. coli, Salmonella, Hepatitis A, Norovirus
# - Chemical contamination → toxic exposure (Superfund sites flooded)
# - Mold growth post-flood → respiratory disease, asthma
```

#### **Data Quality**

**Strengths:**
- ✅ **Engineering quality** (detailed hydraulic/hydrologic studies)
- ✅ **Regulatory standard** (used for insurance, zoning)
- ✅ **Property-level resolution**
- ✅ **Free and open**

**Limitations:**
- ⚠️ **Incomplete coverage** (~60% US, unmapped rural areas)
- ⚠️ **Outdated in some areas** (some maps 1980s, not updated)
- ⚠️ **Climate change** (100-year flood now more frequent)

**Validation:**
- Flood Insurance Rate Maps (FIRMs) validated through post-flood surveys
- Accuracy generally high for mapped areas

**Priority Variables for Health Observatory:**
1. **Percent area in 100-year floodplain (%)**
2. **Population in 100-year floodplain** (number)
3. **Flood risk score** (composite)
4. **Critical facilities in floodplain** (hospitals, nursing homes)
5. **Flood PTSD risk** (potential cases)
6. **Post-flood disease outbreak potential**

---

## SUMMARY: Hydrology/Wetlands/Floodplains Data Hierarchy

**For US County Health Observatory, Prioritize:**

### **WATERSHEDS & STREAMS:**
1. **USGS WBD** (HUC8) → Watershed boundaries, upstream-downstream (15 variables)
2. **USGS NHD** → Stream networks, water availability (20 variables)

### **WETLANDS:**
3. **FWS NWI** → Vector habitat, water quality (29 wetland types, 8 derived metrics)

### **FLOODPLAINS:**
4. **FEMA NFHL** → Flood disaster risk (20 flood zones, 10 derived metrics)

**CRITICAL FINDINGS:**

1. **NWI wetlands are SUPERIOR to NLCD wetlands:**
   - 29 detailed types vs. 2 classes
   - Can identify mosquito habitat (emergent marshes) vs. water quality benefits (forested wetlands)

2. **FEMA NFHL is SUPERIOR to general floodplain data:**
   - Differentiates 100-year vs. 500-year floods
   - Property-level resolution
   - Floodway (highest risk) identified

3. **HUC8 watersheds are OPTIMAL scale for county analysis:**
   - ~2,300 HUC8s nationwide (county-size)
   - Captures upstream-downstream contamination pathways

**IMPLEMENTATION PRIORITY:**
1. **Months 1-2:** FWS NWI wetlands (mosquito habitat, water quality)
2. **Months 3-4:** FEMA NFHL floodplains (disaster risk, population exposure)
3. **Months 5-6:** USGS WBD watersheds (waterborne disease pathways)

**TOTAL NEW VARIABLES: ~65 variables from 4 sources**

---

**Version:** 1.0 (COMPLETE)
**Last Updated:** November 12, 2025
**Sources Documented:** 4 (USGS WBD, USGS NHD, FWS NWI, FEMA NFHL)
**Status:** Ready for data collection