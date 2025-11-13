# Topography, Geology, and Soils Data Sources
## High-Resolution Physical Environmental Variables for US County-Level Analysis

**Last Updated:** November 12, 2025
**Status:** NEW - Physical Geography Gap Analysis
**Priority:** HIGHEST - Foundation for environmental health analysis

---

## EXECUTIVE SUMMARY

This document catalogs **7 federal data sources** providing high-resolution physical environmental variables that can be aggregated to US county level. These sources provide foundational data for understanding:

1. **Terrain effects** on exposure (elevation → UV, slope → erosion, aspect → temperature)
2. **Geologic hazards** (landslides, sinkholes, radon source rocks, heavy metal contamination)
3. **Soil properties** affecting water quality, agriculture, vector habitats, contamination pathways
4. **Natural environmental variation** that modulates all other exposures

**CRITICAL IMPORTANCE:** Physical geography variables are **UPSTREAM DETERMINANTS** that affect:
- Air quality (terrain affects pollution dispersion)
- Water quality (geology/soils affect contamination)
- Climate extremes (elevation affects temperature, aspect affects solar exposure)
- Vector-borne disease (soil drainage affects mosquito breeding)
- Agricultural productivity (soils affect food security)
- Natural disasters (terrain/geology affect hazard susceptibility)

**ALL SOURCES ARE FREE AND OPEN ACCESS** ✅

---

## TABLE OF CONTENTS

### PART 1: TOPOGRAPHY & TERRAIN
1. [USGS 3DEP Digital Elevation Models](#1-usgs-3dep-digital-elevation-models)
2. [USDA ERS Terrain Ruggedness](#2-usda-ers-terrain-ruggedness)
3. [NRCS Terrain Derivatives](#3-nrcs-terrain-derivatives)

### PART 2: GEOLOGY
4. [USGS National Geologic Map Database](#4-usgs-national-geologic-map-database)
5. [USGS Karst & Sinkhole Susceptibility](#5-usgs-karst-sinkhole-susceptibility)
6. [USGS Mineral Resources & Mining Districts](#6-usgs-mineral-resources-mining-districts)

### PART 3: SOILS
7. [NRCS SSURGO/gSSURGO Soil Surveys](#7-nrcs-ssurgogssurgo-soil-surveys)

### PART 4: DATA COLLECTION WORKFLOWS
8. [County Aggregation Methods](#county-aggregation-methods)
9. [Derived Environmental Indicators](#derived-environmental-indicators)

---

## PART 1: TOPOGRAPHY & TERRAIN

### 1. USGS 3DEP DIGITAL ELEVATION MODELS ⭐⭐⭐⭐⭐

**PRIORITY RANK: #1 for Terrain Analysis**

#### **Overview**

**What:** 3D Elevation Program - National seamless digital elevation models
**Who:** US Geological Survey (USGS)
**Resolution:** 1 meter (highest quality, limited coverage), 3 meter, 10 meter (national coverage), 30 meter (complete national coverage)
**Coverage:** All 3,143 US counties (50 states + DC + territories)
**Temporal:** Most recent LiDAR acquisitions (rolling updates as new surveys completed)
**Update Frequency:** Continuous updates as new LiDAR collected

**Why 3DEP is Critical:**
- **Elevation** → UV exposure, temperature lapse rate, air pressure (respiratory)
- **Slope** → soil erosion (dust → respiratory disease), runoff (flooding), physical activity barriers
- **Aspect** → solar radiation exposure, temperature variation, vegetation
- **Terrain roughness** → physical activity (obesity, CVD), access to healthcare
- **Topographic position** → cold air pooling (air pollution, temperature extremes)

#### **Variables Available**

**Primary DEM Products:**
1. **Elevation** - meters above sea level (m)
2. **Hillshade** - visualization of terrain relief
3. **Slope** - degrees or percent (°, %)
4. **Aspect** - compass direction of slope face (°, 0-360)
5. **Contours** - elevation isolines (vector)

**Derived Terrain Variables (25+ metrics):**

**Elevation Statistics:**
6. **Mean elevation** - county average (m)
7. **Minimum elevation** - lowest point (m)
8. **Maximum elevation** - highest point (m)
9. **Elevation range** - max - min (m)
10. **Elevation standard deviation** - variability (m)

**Slope Statistics:**
11. **Mean slope** - county average (°)
12. **Percent area steep slopes** - >15° slope (%)
13. **Percent area very steep slopes** - >30° slope (%)
14. **Percent area flat** - <2° slope (%)

**Aspect Statistics:**
15. **Percent north-facing** - 315-45° (%)
16. **Percent south-facing** - 135-225° (%)
17. **Percent east-facing** - 45-135° (%)
18. **Percent west-facing** - 225-315° (%)

**Topographic Indices:**
19. **Terrain Ruggedness Index (TRI)** - mean elevation difference between adjacent cells
20. **Topographic Position Index (TPI)** - elevation relative to surrounding area
21. **Topographic Wetness Index (TWI)** - log(catchment area / slope tangent)
22. **Solar Radiation Index** - potential annual solar radiation (MJ/m²/year)
23. **Heat Load Index** - compound aspect/slope metric for temperature
24. **Relief** - elevation range within moving window (e.g., 1 km radius)
25. **Surface roughness** - standard deviation of slope

#### **Data Access**

**Portal:** https://www.usgs.gov/3d-elevation-program

**Download Options:**

**1. National Map Downloader (Web Interface):**
- URL: https://apps.nationalmap.gov/downloader/
- Format: GeoTIFF, IMG, GridFloat
- Products: 1m, 3m, 10m, 30m DEMs
- Coverage: Select by county, state, or bounding box

**2. The National Map REST API:**
```r
library(httr)
library(jsonlite)

# Query 30m DEM for a county bounding box
bbox <- "-122.5,37.0,-121.5,38.0" # West, South, East, North

url <- "https://tnmaccess.nationalmap.gov/api/v1/products"
params <- list(
  datasets = "National Elevation Dataset (NED) 1/3 arc-second",
  bbox = bbox,
  outputFormat = "JSON"
)

response <- GET(url, query = params)
products <- content(response, as = "parsed")

# Download first product
download_url <- products$items[[1]]$downloadURL
download.file(download_url, "county_dem_30m.tif")
```

**3. AWS Open Data Registry (Cloud-Optimized GeoTIFFs):**
- URL: https://registry.opendata.aws/usgs-3dep/
- Bucket: `s3://prd-tnm/`
- Format: Cloud-Optimized GeoTIFF (COG)
- Access: Direct S3 access (faster for large areas)

**4. Google Earth Engine:**
```javascript
// USGS National Elevation Dataset (NED) in GEE
var ned = ee.Image("USGS/NED");

// Calculate county elevation statistics
var counties = ee.FeatureCollection("TIGER/2020/Counties");

var elevation_stats = ned.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean()
    .combine(ee.Reducer.min(), '', true)
    .combine(ee.Reducer.max(), '', true)
    .combine(ee.Reducer.stdDev(), '', true),
  scale: 30 // 30m resolution
});

Export.table.toDrive({
  collection: elevation_stats,
  description: 'county_elevation_stats',
  fileFormat: 'CSV'
});
```

**5. R Package (elevatr):**
```r
install.packages("elevatr")
library(elevatr)
library(sf)
library(terra)

# Load counties
counties <- st_read("tl_2020_us_county.shp")

# Get elevation data for a single county
county_single <- counties %>% filter(GEOID == "06075") # San Francisco

# Download DEM (z = zoom level, higher = finer resolution)
dem <- get_elev_raster(county_single, z = 10, src = "aws")

# For all counties (process in batches)
dem_30m <- get_elev_raster(counties, z = 9, src = "aws") # z=9 ≈ 30m
```

#### **County-Level Aggregation Workflow**

**Method 1: Elevation Statistics**

```r
library(sf)
library(terra)
library(exactextractr)
library(tidyverse)

# Load DEM (30m resolution)
dem <- rast("ned_30m_conus.tif")

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>%
  st_transform(crs(dem))

# Extract elevation statistics for each county
county_elevation <- counties %>%
  mutate(
    elev_mean_m = exact_extract(dem, ., fun = "mean"),
    elev_min_m = exact_extract(dem, ., fun = "min"),
    elev_max_m = exact_extract(dem, ., fun = "max"),
    elev_range_m = elev_max_m - elev_min_m,
    elev_sd_m = exact_extract(dem, ., fun = "stdev"),
    elev_p25_m = exact_extract(dem, ., fun = "quantile", quantiles = 0.25),
    elev_p75_m = exact_extract(dem, ., fun = "quantile", quantiles = 0.75)
  )

# Population-weighted elevation (where people actually live)
population <- rast("gpw_v4_population_count_2020_30_sec.tif")
population_30m <- resample(population, dem, method = "bilinear")

county_elevation_popwt <- counties %>%
  mutate(
    elev_popwt_mean = exact_extract(dem, ., weights = population_30m, fun = "weighted_mean")
  )
```

**Method 2: Slope & Aspect**

```r
# Calculate slope from DEM (degrees)
slope <- terrain(dem, v = "slope", unit = "degrees")

# Calculate aspect (0-360°)
aspect <- terrain(dem, v = "aspect", unit = "degrees")

# County-level slope statistics
county_slope <- counties %>%
  mutate(
    slope_mean_deg = exact_extract(slope, ., fun = "mean"),
    slope_sd_deg = exact_extract(slope, ., fun = "stdev"),
    pct_flat = exact_extract(slope < 2, ., fun = "mean") * 100,
    pct_steep = exact_extract(slope > 15, ., fun = "mean") * 100,
    pct_very_steep = exact_extract(slope > 30, ., fun = "mean") * 100
  )

# County-level aspect statistics (directional exposure)
# Convert aspect to north/south/east/west categories
aspect_north <- (aspect >= 315 | aspect < 45)
aspect_south <- (aspect >= 135 & aspect < 225)
aspect_east <- (aspect >= 45 & aspect < 135)
aspect_west <- (aspect >= 225 & aspect < 315)

county_aspect <- counties %>%
  mutate(
    pct_north_facing = exact_extract(aspect_north, ., fun = "mean") * 100,
    pct_south_facing = exact_extract(aspect_south, ., fun = "mean") * 100,
    pct_east_facing = exact_extract(aspect_east, ., fun = "mean") * 100,
    pct_west_facing = exact_extract(aspect_west, ., fun = "mean") * 100
  )
```

**Method 3: Topographic Indices**

```r
library(spatialEco) # For TRI, TPI

# Terrain Ruggedness Index (TRI)
tri <- tri(dem)

# Topographic Position Index (TPI)
tpi <- tpi(dem, scale = 10) # 10-cell neighborhood

# Topographic Wetness Index (TWI)
# TWI = ln(catchment area / tan(slope))
# Requires flow accumulation calculation
flow_acc <- flow_accumulation(dem) # From WhiteboxTools or SAGA
twi <- log((flow_acc + 1) / (tan(slope * pi/180) + 0.001))

# County-level topographic indices
county_topo <- counties %>%
  mutate(
    tri_mean = exact_extract(tri, ., fun = "mean"),
    tpi_mean = exact_extract(tpi, ., fun = "mean"),
    twi_mean = exact_extract(twi, ., fun = "mean"),
    twi_high = exact_extract(twi > 10, ., fun = "mean") * 100 # % high wetness
  )
```

**Method 4: Solar Radiation Potential**

```r
# Calculate potential solar radiation (annual)
# Requires: latitude, slope, aspect
# Use insol package

library(insol)

# For each county centroid
county_solar <- counties %>%
  st_centroid() %>%
  mutate(
    lat = st_coordinates(.)[,2],
    lon = st_coordinates(.)[,1]
  ) %>%
  rowwise() %>%
  mutate(
    # Annual solar radiation at horizontal surface (MJ/m²/year)
    solar_annual_flat = daylength(lat, 1:365, 0) %>% sum() * 3.6, # Simplified

    # Adjust for mean slope and aspect (requires county mean slope/aspect)
    solar_annual_adjusted = solar_annual_flat * cos(slope_mean_deg * pi/180)
  )
```

#### **Derived Health Indicators from Terrain**

**1. UV Exposure from Elevation**
```r
# UV increases ~10% per 1000m elevation
# Base UV index at sea level = 5 (moderate)

county_uv <- county_elevation %>%
  mutate(
    uv_elevation_factor = 1 + (elev_mean_m / 1000) * 0.10,
    uv_index_adjusted = 5 * uv_elevation_factor,
    high_uv_area = elev_mean_m > 1500 # >1500m = high UV
  )

# Health associations:
# - High UV → skin cancer (melanoma, non-melanoma)
# - High UV → cataracts, photokeratitis
# - Benefit: Vitamin D production (bone health, immune function)
```

**2. Physical Activity Barriers from Terrain Ruggedness**
```r
# Steep terrain reduces walkability, physical activity

county_walkability_terrain <- county_slope %>%
  mutate(
    terrain_barrier_score = pct_steep + (pct_very_steep * 2), # 0-100 scale
    low_walkability_terrain = terrain_barrier_score > 20 # >20% challenging terrain
  )

# Health associations:
# - Rugged terrain → reduced physical activity → obesity, CVD, diabetes
# - Rugged terrain → reduced healthcare access → delayed care
# - Rugged terrain → isolation → mental health
```

**3. Air Pollution Trapping from Topography**
```r
# Valleys and basins trap air pollution
# TPI < 0 = valley, TPI > 0 = ridge

county_air_trapping <- county_topo %>%
  mutate(
    valley_area_pct = exact_extract(tpi < -0.5, counties, fun = "mean") * 100,
    air_pollution_trap_risk = valley_area_pct > 30 # >30% valley = high risk
  )

# Health associations:
# - Valley topography → air pollution trapping → respiratory disease, CVD
# - Winter inversions → PM2.5 accumulation → mortality spikes
```

**4. Temperature Extremes from Elevation/Aspect**
```r
# Elevation affects temperature (lapse rate ~6.5°C / 1000m)
# South-facing slopes are warmer, north-facing cooler

county_temperature_modulation <- bind_cols(
  county_elevation,
  county_aspect
) %>%
  mutate(
    temp_lapse_adjustment_C = -0.0065 * elev_mean_m, # Cooler at high elevation
    heat_exposure_score = pct_south_facing - pct_north_facing, # -100 to +100
    cold_exposure_score = pct_north_facing - pct_south_facing
  )

# Health associations:
# - High elevation → cooler temperatures → reduced heat mortality
# - High elevation → colder winters → hypothermia, cardiovascular stress
# - South-facing slopes → heat amplification → heat-related illness
```

**5. Soil Erosion & Dust from Slope**
```r
# Steep slopes → erosion → dust → respiratory disease

county_erosion_risk <- county_slope %>%
  mutate(
    erosion_risk_score = pct_steep * 0.5 + pct_very_steep * 1.0, # Weighted
    high_erosion_risk = erosion_risk_score > 15
  )

# Health associations:
# - Soil erosion → PM10 dust → asthma, COPD, respiratory infections
# - Agricultural erosion → pesticide/fertilizer runoff → water contamination
```

#### **Data Quality & Limitations**

**Strengths:**
- ✅ **National coverage** (all 3,143 counties)
- ✅ **High resolution** (1m-30m depending on area)
- ✅ **LiDAR quality** (sub-meter vertical accuracy in many areas)
- ✅ **Free and open** (public domain)
- ✅ **Cloud-optimized** (fast access via AWS)
- ✅ **Continuously updated** (new LiDAR surveys added regularly)

**Limitations:**
- ⚠️ **Variable resolution** (1m LiDAR not available everywhere, 30m in some areas)
- ⚠️ **Vintage variation** (some DEMs from 2000s, others from 2020s)
- ⚠️ **Large file sizes** (30m national DEM = ~50GB compressed)

**Validation:**
- Vertical accuracy: RMSE <1m for LiDAR-derived DEMs
- Horizontal accuracy: Within 1-2 pixels (30-60m for 30m DEMs)

#### **Disease Associations**

**Elevation → Health:**
- **Skin cancer:** UV exposure increases ~10% per 1000m → melanoma, SCC, BCC
- **Respiratory:** Lower oxygen partial pressure at high altitude → chronic mountain sickness
- **Cardiovascular:** Altitude stress → CVD events in susceptible populations
- **Vector-borne disease:** Elevation limits mosquito/tick habitat → reduced Lyme, WNV at >2000m
- **Mental health:** Seasonal Affective Disorder varies with latitude + elevation

**Slope → Health:**
- **Injury:** Steep terrain → falls, agricultural injuries
- **Obesity/CVD:** Reduced walkability → sedentary lifestyle
- **Respiratory:** Soil erosion from slopes → PM10 dust exposure
- **Flooding:** Steep slopes → flash flood risk → injury, PTSD

**Aspect → Health:**
- **Heat exposure:** South-facing slopes amplify heat → heat stroke, CVD mortality
- **Cold exposure:** North-facing slopes remain cooler → hypothermia risk
- **Vitamin D:** Sun exposure varies by aspect → rickets, osteoporosis

**Priority Variables for Health Observatory:**
1. Mean elevation (population-weighted, m)
2. Elevation range (m)
3. Percent area steep slopes (>15°)
4. Mean slope (°)
5. Percent south-facing (%) - heat exposure
6. Terrain Ruggedness Index (TRI)
7. UV elevation factor
8. Valley area percent (air pollution trapping)
9. Temperature lapse adjustment (°C)
10. Erosion risk score

---

### 2. USDA ERS TERRAIN RUGGEDNESS ⭐⭐⭐⭐

**PRIORITY RANK: #2 for Pre-Calculated Terrain Metrics**

#### **Overview**

**What:** Economic Research Service pre-calculated terrain ruggedness metrics for US counties
**Who:** USDA Economic Research Service
**Resolution:** County-level (pre-aggregated from 30m DEMs)
**Coverage:** All 3,143 US counties
**Temporal:** One-time calculation (2004, based on USGS NED)
**Update Frequency:** Static (no updates planned)

**Why ERS Terrain is Useful:**
- **Pre-calculated** county-level metrics (no GIS processing needed)
- **Standardized** definitions across all counties
- **Economic research focus** (rural development, agriculture, healthcare access)
- **Ready to merge** with other county-level data

#### **Variables Available (8 metrics)**

1. **Percent area in 0-3% slope** - Flat terrain (%)
2. **Percent area in 3-8% slope** - Gentle slopes (%)
3. **Percent area in 8-15% slope** - Moderate slopes (%)
4. **Percent area in 15-30% slope** - Steep slopes (%)
5. **Percent area in >30% slope** - Very steep (%)
6. **Topographic diversity index** - Variety of elevation zones
7. **Average relief** - Mean elevation range within 1 km radius (m)
8. **Maximum relief** - Max elevation range within county (m)

#### **Data Access**

**Portal:** https://www.ers.usda.gov/data-products/county-level-data-sets/county-level-data-sets-download-data/

**Direct Download:**
```r
library(tidyverse)

# Download ERS terrain ruggedness data
url <- "https://www.ers.usda.gov/webdocs/DataFiles/48993/Terrain.xls?v=8309.8"
download.file(url, "ERS_Terrain_Ruggedness.xls")

# Read Excel file
library(readxl)
terrain <- read_excel("ERS_Terrain_Ruggedness.xls", sheet = "Terrain")

# Clean FIPS codes (pad with leading zeros)
terrain <- terrain %>%
  mutate(FIPS = str_pad(FIPS, width = 5, side = "left", pad = "0"))
```

#### **County-Level Use (Already Aggregated)**

```r
# Data is already at county level - just merge with other data

# Example: Merge with health outcomes
health_data <- read_csv("county_health_outcomes.csv")

health_terrain <- health_data %>%
  left_join(terrain, by = c("GEOID" = "FIPS"))

# Calculate composite terrain barrier score
health_terrain <- health_terrain %>%
  mutate(
    terrain_barrier_score =
      `PctSlope3to8` * 0.3 +
      `PctSlope8to15` * 0.6 +
      `PctSlope15to30` * 1.0 +
      `PctSlopeOver30` * 2.0,
    rugged_county = terrain_barrier_score > 30 # Threshold for "rugged"
  )
```

#### **Derived Health Indicators**

```r
# Physical activity environment
terrain_walkability <- terrain %>%
  mutate(
    walkable_area_pct = `PctSlope0to3` + `PctSlope3to8`,
    challenging_area_pct = `PctSlope15to30` + `PctSlopeOver30`,
    walkability_score = 100 - challenging_area_pct
  )

# Healthcare access barriers
terrain_access <- terrain %>%
  mutate(
    healthcare_access_barrier = `AvgRelief` > 100 | challenging_area_pct > 20,
    ambulance_response_barrier = `AvgRelief` > 150 # Difficult EMS terrain
  )
```

#### **Data Quality**

**Strengths:**
- ✅ **Pre-calculated** (no GIS processing required)
- ✅ **Standardized** methodology across all counties
- ✅ **Free download** (public domain)
- ✅ **Small file size** (~2 MB Excel file)

**Limitations:**
- ⚠️ **Static** (2004 calculation, no updates)
- ⚠️ **Coarse resolution** source (30m DEM, now superseded by finer DEMs)
- ⚠️ **Limited variables** (8 metrics vs. 25+ from raw DEM processing)

**Priority Variables:**
1. Percent area steep slopes (>15%)
2. Average relief (m)
3. Terrain barrier composite score
4. Walkability score

---

### 3. NRCS TERRAIN DERIVATIVES ⭐⭐⭐

**PRIORITY RANK: #3 for Hydrology-Focused Terrain**

#### **Overview**

**What:** Natural Resources Conservation Service terrain derivatives for hydrologic analysis
**Who:** USDA NRCS (Natural Resources Conservation Service)
**Resolution:** 10m national coverage (some areas 3m)
**Coverage:** All 3,143 US counties
**Temporal:** Derived from USGS 3DEP (updated as new DEMs available)
**Update Frequency:** Rolling updates

**Why NRCS Terrain Derivatives:**
- **Hydrologic focus** (drainage, wetness, flow paths)
- **Agricultural relevance** (soil drainage capacity, flood risk)
- **Vector-borne disease** (wetness index predicts mosquito habitat)

#### **Variables Available (15 metrics)**

**Flow & Drainage:**
1. **Flow direction** - D8 or D-infinity flow routing
2. **Flow accumulation** - Contributing area (cells)
3. **Stream power index** - Erosion potential
4. **Sediment transport index** - Erosion/deposition

**Wetness & Moisture:**
5. **Topographic Wetness Index (TWI)** - log(area / tan(slope))
6. **Compound Topographic Index (CTI)** - Similar to TWI
7. **Potential wetland area** - TWI-based classification

**Curvature:**
8. **Profile curvature** - Slope convexity in flow direction
9. **Plan curvature** - Slope convexity perpendicular to flow
10. **Total curvature** - Combined curvature

**Solar:**
11. **Annual solar radiation** - Potential insolation (kWh/m²/year)
12. **Summer solar radiation** - June-August (kWh/m²)
13. **Winter solar radiation** - December-February (kWh/m²)

**Derived:**
14. **Upslope contributing area** - Watershed area above point (km²)
15. **Stream proximity** - Distance to nearest stream (m)

#### **Data Access**

**Portal:** https://www.nrcs.usda.gov/resources/data-and-reports/

**Access via USDA Geospatial Data Gateway:**
```r
# Manual download:
# 1. Go to https://datagateway.nrcs.usda.gov/
# 2. Select state/county
# 3. Select "Elevation Derivatives" product
# 4. Download GeoTIFF files

# Programmatic access via Web Coverage Service (WCS)
library(sf)
library(terra)

# WCS endpoint for NRCS data
wcs_url <- "https://gis.apfo.usda.gov/arcgis/services/NAIP/USDA_CONUS_PRIME/ImageServer/WCSServer"

# County boundary
county <- st_read("county_boundary.shp")

# Request TWI layer (example - actual layer names vary)
twi <- rast(paste0(wcs_url, "?SERVICE=WCS&VERSION=2.0.1&REQUEST=GetCoverage&COVERAGEID=TWI&SUBSET=x(", bbox$xmin, ",", bbox$xmax, ")&SUBSET=y(", bbox$ymin, ",", bbox$ymax, ")"))
```

#### **County-Level Aggregation**

```r
# Load NRCS TWI raster
twi <- rast("nrcs_twi_10m.tif")

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>%
  st_transform(crs(twi))

# Extract TWI statistics
county_twi <- counties %>%
  mutate(
    twi_mean = exact_extract(twi, ., fun = "mean"),
    twi_sd = exact_extract(twi, ., fun = "stdev"),
    pct_high_wetness = exact_extract(twi > 10, ., fun = "mean") * 100, # >10 = wet
    pct_low_drainage = exact_extract(twi > 12, ., fun = "mean") * 100  # >12 = poor drainage
  )
```

#### **Derived Health Indicators**

**Vector-Borne Disease Risk from Soil Wetness**
```r
# High TWI = poor drainage = mosquito breeding habitat

county_vector_risk <- county_twi %>%
  mutate(
    mosquito_habitat_pct = pct_high_wetness,
    vector_risk_high = mosquito_habitat_pct > 20, # >20% wet areas

    # West Nile Virus risk (combines wetness + temperature)
    wnv_risk_score = mosquito_habitat_pct * temperature_mean / 20
  )

# Health associations:
# - Poor drainage → standing water → mosquito breeding
# - West Nile Virus, Dengue, Zika, Malaria (emerging)
# - Also: tick habitat (moist forest areas)
```

#### **Data Quality**

**Strengths:**
- ✅ **Hydrologic expertise** (NRCS specializes in drainage, soil-water)
- ✅ **Agricultural relevance** (drainage affects crop productivity, food security)
- ✅ **Free access**

**Limitations:**
- ⚠️ **Limited documentation** (not as well-documented as USGS 3DEP)
- ⚠️ **Requires GIS skills** (not pre-aggregated to county level)

**Priority Variables:**
1. Topographic Wetness Index (mean)
2. Percent high wetness area (>10 TWI)
3. Flow accumulation (drainage density)
4. Annual solar radiation potential

---

## PART 2: GEOLOGY

### 4. USGS NATIONAL GEOLOGIC MAP DATABASE ⭐⭐⭐⭐⭐

**PRIORITY RANK: #4 for Bedrock Geology & Geologic Hazards**

#### **Overview**

**What:** National compilation of geologic maps showing bedrock and surficial geology
**Who:** US Geological Survey (USGS)
**Resolution:** 1:500,000 (state-level), 1:100,000 and finer (detailed quadrangles)
**Coverage:** All 50 states (completeness varies)
**Temporal:** Compiled from surveys spanning 1900s-present
**Update Frequency:** Continuous updates as new state maps completed

**Why Geologic Maps are Critical:**
- **Radon source rocks** → lung cancer (granite, black shale, phosphate rocks)
- **Heavy metal contamination** → neurological, renal, cancer (mineralized zones)
- **Karst terrain** → groundwater contamination (limestone, dolomite)
- **Landslide susceptibility** → injury, PTSD (weak/weathered rocks)
- **Soil parent material** → soil chemistry, trace elements (affects agriculture, water)

#### **Variables Available (20+ classifications)**

**Bedrock Lithology (Rock Types):**
1. **Igneous rocks** - Granite, basalt, gabbro, rhyolite
2. **Sedimentary rocks** - Sandstone, shale, limestone, dolomite, conglomerate
3. **Metamorphic rocks** - Schist, gneiss, quartzite, marble
4. **Unconsolidated** - Alluvium, glacial deposits, eolian sand

**Geologic Age:**
5. **Quaternary** (0-2.6 Ma) - Recent deposits
6. **Tertiary** (2.6-66 Ma)
7. **Mesozoic** (66-252 Ma)
8. **Paleozoic** (252-541 Ma)
9. **Precambrian** (>541 Ma) - Oldest rocks

**Surficial Geology:**
10. **Glacial deposits** - Till, outwash, moraines
11. **Alluvial deposits** - Floodplain, terrace, fan
12. **Eolian deposits** - Loess, dune sand
13. **Colluvium** - Slope deposits, landslide debris

**Derived Classifications:**
14. **Radon source potential** - Uranium-bearing rocks (granite, black shale)
15. **Carbonate karst** - Limestone, dolomite (sinkhole/cave terrain)
16. **Heavy metal sources** - Mineralized zones, mining districts
17. **Landslide-prone lithology** - Weak shales, weathered volcanics
18. **Aquifer lithology** - Permeable vs. confining units
19. **Soil parent material** - Determines soil chemistry
20. **Geothermal potential** - Volcanic/high heat flow areas

#### **Data Access**

**Portal:** https://ngmdb.usgs.gov/

**Download Options:**

**1. National Geologic Map Database (Web Map Service):**
```r
library(sf)
library(httr)

# WMS endpoint for US state geology
wms_url <- "https://mrdata.usgs.gov/services/geology"

# Query geologic units for a county
county <- st_read("county_boundary.shp")
bbox <- st_bbox(county)

# Get WMS layers (geology)
geology_wms <- st_read(paste0(
  wms_url, "?SERVICE=WFS&VERSION=2.0.0&REQUEST=GetFeature",
  "&TYPENAME=geology:geology&BBOX=", paste(bbox, collapse = ",")
))

# Extract lithology
county_geology <- geology_wms %>%
  st_intersection(county) %>%
  mutate(area = st_area(.)) %>%
  group_by(LITHOLOGY) %>%
  summarize(area_m2 = sum(area)) %>%
  mutate(pct_area = as.numeric(area_m2 / sum(area_m2) * 100))
```

**2. State Geologic Map Compilation (SGMC):**
- URL: https://mrdata.usgs.gov/geology/state/
- Format: Shapefile, GeoPackage
- Coverage: All 50 states

```bash
# Download California state geology
wget https://mrdata.usgs.gov/geology/state/sgmc-ca.zip
unzip sgmc-ca.zip
```

**3. Geologic Map Schema (GeoSciML):**
```r
# Read state geology shapefile
ca_geology <- st_read("sgmc-ca.shp")

# Key fields:
# - ROCKTYPE1: Primary lithology (e.g., "Granite", "Sandstone")
# - ROCKTYPE2: Secondary lithology
# - MIN_AGE, MAX_AGE: Geologic age (Ma)
# - UNITDESC: Detailed unit description

# Aggregate to county level
counties_ca <- st_read("tl_2020_06_county.shp")

county_geology <- st_intersection(ca_geology, counties_ca) %>%
  mutate(area_m2 = as.numeric(st_area(.))) %>%
  group_by(GEOID, ROCKTYPE1) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop") %>%
  group_by(GEOID) %>%
  mutate(pct_area = area_m2 / sum(area_m2) * 100) %>%
  arrange(GEOID, desc(pct_area))

# Dominant lithology per county
dominant_geology <- county_geology %>%
  slice_max(pct_area, n = 1, by = GEOID)
```

#### **County-Level Aggregation**

**Method: Classify Geologic Units into Health-Relevant Categories**

```r
# Classify lithology into radon source potential
classify_radon_source <- function(rocktype) {
  high_radon <- c("Granite", "Granodiorite", "Tonalite", "Black shale",
                  "Phosphate rock", "Gneiss", "Schist (graphitic)")
  moderate_radon <- c("Sandstone", "Conglomerate", "Volcanic")
  low_radon <- c("Limestone", "Dolomite", "Basalt", "Alluvium")

  case_when(
    rocktype %in% high_radon ~ "High",
    rocktype %in% moderate_radon ~ "Moderate",
    rocktype %in% low_radon ~ "Low",
    TRUE ~ "Unknown"
  )
}

county_radon_geology <- county_geology %>%
  mutate(radon_potential = classify_radon_source(ROCKTYPE1)) %>%
  group_by(GEOID, radon_potential) %>%
  summarize(pct_area = sum(pct_area), .groups = "drop") %>%
  pivot_wider(names_from = radon_potential, values_from = pct_area,
              values_fill = 0, names_prefix = "radon_")

# Classify karst terrain (carbonate rocks)
county_karst <- county_geology %>%
  mutate(is_karst = ROCKTYPE1 %in% c("Limestone", "Dolomite", "Marble")) %>%
  group_by(GEOID) %>%
  summarize(karst_area_pct = sum(pct_area[is_karst]))

# Classify heavy metal source rocks
county_metals <- county_geology %>%
  mutate(
    is_metal_source = ROCKTYPE1 %in% c("Mineralized", "Sulfide-bearing",
                                        "Metal-enriched", "Mining district")
  ) %>%
  group_by(GEOID) %>%
  summarize(metal_source_pct = sum(pct_area[is_metal_source]))
```

#### **Derived Health Indicators**

**1. Radon Exposure from Source Rocks**
```r
# Radon risk from bedrock geology

county_radon_risk <- county_radon_geology %>%
  mutate(
    radon_risk_score = radon_High * 1.0 + radon_Moderate * 0.5,
    high_radon_risk = radon_risk_score > 50 # >50% high/moderate radon source
  )

# Health associations:
# - Radon exposure → lung cancer (2nd leading cause after smoking)
# - Synergistic with smoking (20x risk for smokers in high radon areas)
# - WHO estimates 3-14% of lung cancer attributable to radon
```

**2. Groundwater Contamination from Karst**
```r
# Karst terrain → rapid groundwater contamination

county_karst_risk <- county_karst %>%
  mutate(
    groundwater_vulnerability = karst_area_pct > 25, # >25% karst
    waterborne_disease_risk = karst_area_pct * 0.02 # Proportional risk
  )

# Health associations:
# - Karst → rapid contaminant transport → waterborne disease
# - Cryptosporidium, Giardia, E. coli outbreaks
# - Nitrate contamination (agricultural runoff)
# - PFAS, pesticides reach groundwater quickly
```

**3. Heavy Metal Exposure from Geology**
```r
# Mineralized zones, mining districts → heavy metal contamination

county_metal_risk <- county_metals %>%
  mutate(
    heavy_metal_risk = metal_source_pct > 10, # >10% mineralized
    arsenic_risk = ROCKTYPE1 == "Arsenic-bearing",
    lead_risk = ROCKTYPE1 == "Lead-bearing"
  )

# Health associations:
# - Arsenic (groundwater, soil) → cancer (lung, bladder, skin), CVD
# - Lead → neurodevelopmental effects (IQ loss), CVD
# - Mercury → neurological effects (Minamata disease)
# - Cadmium → renal disease, bone disease (Itai-itai)
```

**4. Landslide Susceptibility from Lithology**
```r
# Weak/weathered rocks → landslide risk

classify_landslide_lithology <- function(rocktype) {
  high_susceptible <- c("Shale", "Claystone", "Serpentinite", "Weathered volcanic")
  moderate_susceptible <- c("Sandstone", "Siltstone", "Schist")
  low_susceptible <- c("Granite", "Basalt", "Limestone", "Quartzite")

  case_when(
    rocktype %in% high_susceptible ~ "High",
    rocktype %in% moderate_susceptible ~ "Moderate",
    TRUE ~ "Low"
  )
}

county_landslide_lithology <- county_geology %>%
  mutate(landslide_suscept = classify_landslide_lithology(ROCKTYPE1)) %>%
  group_by(GEOID) %>%
  summarize(
    pct_high_suscept = sum(pct_area[landslide_suscept == "High"])
  ) %>%
  mutate(landslide_risk = pct_high_suscept > 20)

# Health associations:
# - Landslides → injury, death (1000+ deaths/year globally, US ~25/year)
# - Landslides → PTSD, anxiety, depression
# - Infrastructure damage → healthcare access barriers
```

#### **Data Quality**

**Strengths:**
- ✅ **National coverage** (all 50 states)
- ✅ **Geologic expertise** (century+ of USGS mapping)
- ✅ **Free and open**
- ✅ **Health-relevant classifications** (radon, karst well-documented)

**Limitations:**
- ⚠️ **Variable detail** (some states 1:500,000, others 1:24,000)
- ⚠️ **Complex classification** (thousands of geologic units, requires reclassification)
- ⚠️ **Requires GIS skills** (not pre-aggregated to counties)

**Priority Variables:**
1. Percent area high radon source rocks (%)
2. Percent area karst terrain (%)
3. Dominant bedrock lithology (category)
4. Percent area mineralized/metal-bearing (%)
5. Landslide-susceptible lithology (%)

---

### 5. USGS KARST & SINKHOLE SUSCEPTIBILITY ⭐⭐⭐⭐

**PRIORITY RANK: #5 for Groundwater Vulnerability**

#### **Overview**

**What:** National karst map showing sinkhole and cave terrain
**Who:** US Geological Survey
**Resolution:** 1:250,000 (state-level compilations)
**Coverage:** ~20% of US land area (where karst exists)
**Temporal:** Static compilation
**Update Frequency:** Infrequent updates

**Why Karst Matters:**
- **Rapid groundwater contamination** (no soil filtration)
- **Waterborne disease outbreaks** disproportionately in karst regions
- **Infrastructure hazards** (sinkhole collapse)
- **Flood risk** (rapid surface-to-groundwater connection)

#### **Variables Available (12 metrics)**

**Karst Classification:**
1. **Carbonate karst** - Limestone/dolomite dissolution
2. **Evaporite karst** - Gypsum/salt dissolution
3. **Pseudokarst** - Lava tubes, piping
4. **Covered karst** - Karst beneath unconsolidated cover

**Karst Features:**
5. **Sinkholes (count)** - Depression features
6. **Springs (count)** - Karst groundwater discharge
7. **Caves (count)** - Known cave systems

**Derived Metrics:**
8. **Sinkhole density** - Features per km²
9. **Groundwater vulnerability index** - Contamination susceptibility
10. **Aquifer connectivity** - Surface-groundwater connection
11. **Flood sinkhole potential** - Rapid drainage capacity
12. **Infrastructure risk** - Collapse/subsidence potential

#### **Data Access**

**Portal:** https://www.usgs.gov/centers/kars-karst-science

**Download Options:**

```r
# USGS National Karst Map
url <- "https://www.usgs.gov/media/files/national-karst-map-shapefile"
download.file(url, "national_karst.zip")
unzip("national_karst.zip")

karst <- st_read("national_karst.shp")

# Intersect with counties
counties <- st_read("tl_2020_us_county.shp")

county_karst <- st_intersection(karst, counties) %>%
  mutate(area_m2 = as.numeric(st_area(.))) %>%
  group_by(GEOID, KARST_TYPE) %>%
  summarize(area_m2 = sum(area_m2), .groups = "drop") %>%
  group_by(GEOID) %>%
  mutate(pct_area = area_m2 / sum(area_m2) * 100)

# County-level karst presence
county_karst_summary <- county_karst %>%
  group_by(GEOID) %>%
  summarize(
    karst_present = TRUE,
    karst_area_pct = sum(pct_area),
    dominant_karst_type = KARST_TYPE[which.max(pct_area)]
  )
```

#### **Derived Health Indicators**

**Waterborne Disease Risk**
```r
county_waterborne_risk <- county_karst_summary %>%
  mutate(
    high_contamination_risk = karst_area_pct > 50,
    groundwater_vulnerability_score = karst_area_pct * 2, # 0-200 scale

    # Waterborne disease susceptibility
    crypto_risk_high = karst_present & karst_area_pct > 25,
    ecoli_risk_high = karst_present & dominant_karst_type == "Carbonate"
  )

# Health associations:
# - Karst → Cryptosporidium outbreaks (Milwaukee 1993: 400k ill, 100 deaths)
# - Giardia, E. coli, Campylobacter
# - Nitrate contamination → methemoglobinemia (blue baby syndrome)
```

**Data Quality:**
- ✅ **Expert compilation** (karst hydrogeologists)
- ✅ **Free and open**
- ⚠️ **Incomplete coverage** (~20% US, only where karst exists)

**Priority Variables:**
1. Karst presence (yes/no)
2. Karst area percent (%)
3. Groundwater vulnerability score
4. Sinkhole density (per km²)

---

### 6. USGS MINERAL RESOURCES & MINING DISTRICTS ⭐⭐⭐⭐

**PRIORITY RANK: #6 for Heavy Metal Contamination Sources**

#### **Overview**

**What:** National mineral resources database and mining districts
**Who:** US Geological Survey
**Resolution:** Point locations (mines) + polygons (districts)
**Coverage:** ~10,000 documented mines, hundreds of mining districts
**Temporal:** Historical (1800s-present)
**Update Frequency:** Continuous updates

**Why Mining Matters:**
- **Heavy metal contamination** (Pb, As, Cd, Hg, Cr)
- **Acid mine drainage** (AMD) → stream acidification
- **Dust exposure** (PM10, silica)
- **Legacy contamination** (Superfund sites at ~30% of mining locations)

#### **Variables Available (12 metrics)**

**Commodity Types:**
1. **Metal mines** - Gold, silver, copper, lead, zinc, iron
2. **Industrial minerals** - Limestone, sand/gravel, phosphate
3. **Coal mines** - Surface and underground
4. **Uranium mines** - Radon source, radioactive waste

**Mine Status:**
5. **Active mines** - Currently operating
6. **Inactive/abandoned** - Closed, no reclamation
7. **Superfund sites** - NPL-listed mining contamination

**Derived:**
8. **Mining density** - Mines per km²
9. **Heavy metal source score** - Based on commodity
10. **Acid mine drainage potential** - Sulfide minerals
11. **Distance to nearest mine** - Exposure gradient (km)
12. **Cumulative mining impact** - Historical production volume

#### **Data Access**

```r
# USGS Mineral Resources Data System (MRDS)
library(httr)
library(jsonlite)

# API endpoint
url <- "https://mrdata.usgs.gov/mrds/api/records"

# Query mines in a state
response <- GET(url, query = list(state = "CA", format = "json"))
mines <- fromJSON(content(response, "text"))

# Convert to spatial
mines_sf <- st_as_sf(mines, coords = c("longitude", "latitude"), crs = 4326)

# Aggregate to county level
counties <- st_read("tl_2020_06_county.shp")

county_mines <- st_join(counties, mines_sf) %>%
  group_by(GEOID) %>%
  summarize(
    mine_count = n(),
    metal_mines = sum(commodity_type == "Metal"),
    abandoned_mines = sum(status == "Inactive")
  ) %>%
  mutate(
    mining_density = mine_count / as.numeric(st_area(.) / 1e6) # per km²
  )
```

#### **Derived Health Indicators**

```r
# Heavy metal exposure from mining
county_mining_health <- county_mines %>%
  mutate(
    heavy_metal_risk_score = metal_mines * 2 + abandoned_mines * 3,
    high_contamination_risk = heavy_metal_risk_score > 10,

    # Specific metals
    lead_risk = commodity == "Lead",
    arsenic_risk = commodity == "Gold" | commodity == "Copper",
    uranium_risk = commodity == "Uranium"
  )

# Health associations:
# - Lead → neurodevelopmental effects, CVD
# - Arsenic → cancer (lung, bladder, skin), CVD
# - Cadmium → renal disease
# - Silica dust → silicosis, lung cancer
```

**Priority Variables:**
1. Mine count
2. Metal mine count
3. Abandoned mine count
4. Heavy metal risk score

---

## PART 3: SOILS

### 7. NRCS SSURGO/gSSURGO SOIL SURVEYS ⭐⭐⭐⭐⭐

**PRIORITY RANK: #1 for Soil Properties (MOST COMPREHENSIVE)**

#### **Overview**

**What:** Soil Survey Geographic Database - Most detailed soil maps in the world
**Who:** USDA Natural Resources Conservation Service
**Resolution:** 1:12,000 to 1:24,000 (field-scale detail)
**Coverage:** 95%+ of US (remaining areas in progress)
**Temporal:** Continuously updated
**Update Frequency:** Annual releases (Oct 1st federal fiscal year)

**Why SSURGO is Essential:**
- **40+ health-relevant soil properties** from single source
- **Vector-borne disease** (soil drainage → mosquito habitat)
- **Waterborne disease** (soil permeability → contamination transport)
- **Heavy metal exposure** (soil pH, CEC affect bioavailability)
- **Agricultural productivity** (food security)
- **Dust exposure** (soil texture, erosion)

#### **Variables Available (100+ properties, 40 priority for health)**

### 📋 COMPLETE SSURGO SOIL PROPERTIES CATALOG (TIER 2)

**For the complete catalog of all 227 SSURGO soil properties organized by table (CHORIZON, COMPONENT, MAPUNIT, etc.) with descriptions, units, and calculation methods, see:**

**[NRCS_SSURGO_COMPLETE_SOIL_PROPERTIES.md](NRCS_SSURGO_COMPLETE_SOIL_PROPERTIES.md)**

This companion Tier 2 catalog provides:
- All 227 SSURGO properties with field names, descriptions, and units
- Organized by database table (CHORIZON, COMPONENT, MAPUNIT, MUAGGATT)
- Depth-specific properties (0-5cm, 0-20cm, 0-30cm, 0-100cm, 0-150cm, 0-200cm)
- Aggregation methods for county-level analysis
- R code examples for extracting and computing soil properties
- Links to official SSURGO metadata and technical documentation

**Use this document (Tier 1)** for SSURGO overview, priority health-relevant properties, and data access.
**Use NRCS_SSURGO_COMPLETE_SOIL_PROPERTIES.md (Tier 2)** to look up specific soil property codes or browse the complete database schema.

**Physical Properties:**
1. **Texture class** - Sand, loam, clay, silt (USDA classification)
2. **Sand content** (%)
3. **Silt content** (%)
4. **Clay content** (%)
5. **Rock fragment volume** (%)
6. **Bulk density** (g/cm³)
7. **Particle density** (g/cm³)

**Hydrologic Properties:**
8. **Drainage class** - Excessively drained to very poorly drained (7 classes)
9. **Hydrologic soil group** - A, B, C, D (runoff potential)
10. **Saturated hydraulic conductivity (Ksat)** - μm/s
11. **Available water capacity (AWC)** - cm/cm
12. **Depth to water table** - cm
13. **Flooding frequency** - None, rare, occasional, frequent
14. **Ponding frequency** - None, rare, occasional, frequent

**Chemical Properties:**
15. **pH** - 0-14 scale (1:1 water)
16. **Organic matter content** (%)
17. **Cation exchange capacity (CEC)** - meq/100g
18. **Calcium carbonate equivalent** (%)
19. **Gypsum content** (%)
20. **Electrical conductivity (EC)** - mmhos/cm (salinity)
21. **Sodium adsorption ratio (SAR)** - unitless

**Contaminant Capacity:**
22. **Nitrate leaching potential** - Very low to very high
23. **Pesticide leaching potential** - Low, moderate, high
24. **Phosphorus runoff potential** - Low to very high
25. **Heavy metal retention capacity** - Based on CEC, pH, OM

**Agricultural:**
26. **Farmland classification** - Prime, important, not prime
27. **Crop productivity index** - 0-100 scale
28. **Erosion factor (K)** - Soil erodibility (RUSLE)
29. **Wind erosion group** - 1-8 (1=most susceptible)

**Engineering:**
30. **Corrosion potential** - Steel, concrete
31. **Shrink-swell potential** - Low, moderate, high
32. **Compaction potential** - Road/building suitability
33. **Septic system suitability** - Limitations rating

**Derived Health Indicators:**
34. **Vector habitat suitability** - Poor drainage + warm climate
35. **Groundwater vulnerability** - Permeability + depth to water table
36. **Erosion dust potential** - Wind erosion + fine texture
37. **Heavy metal bioavailability** - pH + CEC combination
38. **Nutrient leaching risk** - Permeability + low OM
39. **Arsenic mobilization potential** - pH + redox conditions
40. **Lead absorption capacity** - Clay + pH + OM

#### **Data Access**

**Portal:** https://websoilsurvey.nrcs.usda.gov/

**Download Options:**

**1. Web Soil Survey (Interactive):**
- URL: https://websoilsurvey.nrcs.usda.gov/app/
- Define AOI (county, custom polygon)
- Download: Spatial (shapefile), Tabular (Access DB, CSV)

**2. gSSURGO (Gridded SSURGO, easier for national analysis):**
```r
# Download gSSURGO from NRCS
# URL: https://nrcs.app.box.com/v/soils (annual releases)
# File: gSSURGO_CONUS_[year].zip (~12 GB compressed)

library(terra)
library(sf)

# Load gSSURGO raster (10m resolution)
gssurgo <- rast("gSSURGO_CONUS.tif")

# Load attribute table
mukey_table <- read.csv("gSSURGO_CONUS_attributes.csv")

# Example: Extract drainage class
# 1. Get MUKEY (Map Unit Key) for each county
# 2. Join to attribute table to get properties

counties <- st_read("tl_2020_us_county.shp")

# Extract dominant soil map unit per county
county_mukey <- exact_extract(gssurgo, counties, fun = "mode") # Most common MUKEY

# Join to soil properties
county_soils <- counties %>%
  mutate(MUKEY = county_mukey) %>%
  left_join(mukey_table, by = "MUKEY")
```

**3. SSURGO via SDA (Soil Data Access API):**
```r
library(soilDB)

# Query SSURGO data for a county
county_fips <- "06075" # San Francisco

# Get soil properties
sda_query <- paste0("
  SELECT
    co.cokey, co.compname, co.comppct_r,
    ch.chkey, ch.hzdept_r, ch.hzdepb_r,
    ch.sandtotal_r, ch.silttotal_r, ch.claytotal_r,
    ch.ph1to1h2o_r, ch.om_r, ch.cec7_r, ch.ksat_r,
    co.drainagecl, co.hydgrp
  FROM component AS co
  JOIN chorizon AS ch ON co.cokey = ch.cokey
  JOIN mapunit AS mu ON co.mukey = mu.mukey
  JOIN legend AS l ON mu.lkey = l.lkey
  WHERE l.areasymbol LIKE 'CA%'
    AND l.areaname LIKE '%San Francisco%'
")

soil_data <- SDA_query(sda_query)
```

#### **County-Level Aggregation**

**Method: Weighted Average by Area**

```r
library(sf)
library(terra)
library(tidyverse)

# Load SSURGO spatial (soil polygons)
ssurgo <- st_read("SSURGO_county.shp")

# Load SSURGO tabular (soil properties)
soil_props <- read.csv("SSURGO_properties.csv")

# Join spatial to tabular
ssurgo_full <- ssurgo %>%
  left_join(soil_props, by = "MUKEY")

# Load county
county <- st_read("county_boundary.shp")

# Intersect soils with county
county_soils <- st_intersection(ssurgo_full, county) %>%
  mutate(area_m2 = as.numeric(st_area(.)))

# Calculate area-weighted average for each property
county_soil_summary <- county_soils %>%
  st_drop_geometry() %>%
  summarize(
    # Physical (weighted by area)
    sand_pct = weighted.mean(sandtotal_r, area_m2, na.rm = TRUE),
    clay_pct = weighted.mean(claytotal_r, area_m2, na.rm = TRUE),
    silt_pct = weighted.mean(silttotal_r, area_m2, na.rm = TRUE),

    # Chemical
    ph = weighted.mean(ph1to1h2o_r, area_m2, na.rm = TRUE),
    om_pct = weighted.mean(om_r, area_m2, na.rm = TRUE),
    cec = weighted.mean(cec7_r, area_m2, na.rm = TRUE),

    # Hydrologic
    ksat_ums = weighted.mean(ksat_r, area_m2, na.rm = TRUE),
    awc = weighted.mean(awc_r, area_m2, na.rm = TRUE),

    # Categorical (percent area in each class)
    pct_poorly_drained = sum(area_m2[drainagecl %in% c("Poorly drained", "Very poorly drained")]) / sum(area_m2) * 100,
    pct_well_drained = sum(area_m2[drainagecl %in% c("Well drained", "Excessively drained")]) / sum(area_m2) * 100,
    pct_hydgrp_A = sum(area_m2[hydgrp == "A"]) / sum(area_m2) * 100,
    pct_hydgrp_D = sum(area_m2[hydgrp == "D"]) / sum(area_m2) * 100
  )
```

#### **Derived Health Indicators from Soils**

**1. Vector-Borne Disease Risk (Poor Drainage)**
```r
# Poorly drained soils → standing water → mosquito breeding

county_vector_soil <- county_soil_summary %>%
  mutate(
    mosquito_habitat_soil = pct_poorly_drained > 20, # >20% poor drainage
    vector_risk_score = pct_poorly_drained * 0.5,

    # West Nile Virus risk (soil + climate)
    wnv_risk = (pct_poorly_drained > 15) & (mean_temp_summer > 25)
  )

# Health associations:
# - Poor drainage → standing water → Culex mosquitoes → West Nile Virus
# - Also: Eastern Equine Encephalitis, St. Louis Encephalitis
# - US: 2,000-3,000 WNV cases/year, ~100 deaths
```

**2. Waterborne Disease (High Permeability)**
```r
# High permeability → rapid contamination transport

county_waterborne_soil <- county_soil_summary %>%
  mutate(
    high_permeability = ksat_ums > 100, # >100 μm/s = rapid
    groundwater_vulnerability = (pct_hydgrp_A > 50) | high_permeability,

    # Nitrate leaching to groundwater
    nitrate_leaching_risk = high_permeability & (om_pct < 2),

    # Septic system contamination risk
    septic_contamination_risk = high_permeability & (depth_to_water < 100)
  )

# Health associations:
# - Rapid permeability → untreated sewage to groundwater → E. coli, Campylobacter
# - Nitrate → methemoglobinemia (blue baby syndrome)
# - PFAS, pesticides reach drinking water aquifers
```

**3. Heavy Metal Bioavailability (pH + CEC)**
```r
# Soil chemistry affects heavy metal absorption, plant uptake, human exposure

county_metal_bioavail <- county_soil_summary %>%
  mutate(
    # Lead bioavailability (low pH + low CEC = high risk)
    lead_bioavail_high = (ph < 6.5) & (cec < 10),

    # Arsenic mobilization (pH extremes)
    arsenic_mobile_high = (ph < 5.5) | (ph > 8.5),

    # Cadmium uptake by plants (low pH + low OM)
    cadmium_uptake_high = (ph < 6.0) & (om_pct < 2),

    # Heavy metal retention capacity (higher = safer)
    metal_retention_capacity = cec * om_pct * (7 - abs(ph - 7))
  )

# Health associations:
# - Lead bioavailability → childhood IQ loss, ADHD, CVD
# - Arsenic → cancer (lung, bladder, skin), CVD
# - Cadmium → renal disease (Itai-itai disease)
```

**4. Dust/Erosion Respiratory Risk**
```r
# Fine-textured, low OM soils → dust generation → respiratory disease

county_dust_risk <- county_soil_summary %>%
  mutate(
    # PM10 dust potential
    dust_suscept_score = (sand_pct + silt_pct) * (1 / (om_pct + 1)),
    high_dust_risk = (wind_erod_group <= 3) & (om_pct < 2),

    # Agricultural dust (combines wind erosion + cultivation)
    ag_dust_risk = high_dust_risk & (pct_cropland > 30)
  )

# Health associations:
# - PM10 dust → asthma exacerbation, COPD, CVD mortality
# - Silica dust (from soil) → silicosis (occupational)
# - Valley Fever (Coccidioidomycosis) in SW US dusty soils
```

**5. Food Security (Soil Productivity)**
```r
# Soil quality affects crop yields → food security → nutrition

county_food_security_soil <- county_soil_summary %>%
  mutate(
    prime_farmland_pct = sum(area_m2[farmland_class == "Prime"]) / sum(area_m2) * 100,
    soil_productivity_index = awc * om_pct * cec / (1 + (abs(ph - 6.5))),

    # Low productivity → food insecurity risk
    low_productivity = prime_farmland_pct < 10 & soil_productivity_index < 50
  )

# Health associations:
# - Poor soils → low crop yields → food insecurity → malnutrition
# - Food deserts in rural areas with poor soils
```

#### **Data Quality**

**Strengths:**
- ✅ **Most comprehensive soil database in world** (100+ properties)
- ✅ **National coverage** (95%+ US)
- ✅ **High resolution** (1:24,000, field-scale)
- ✅ **Continuously updated** (annual releases)
- ✅ **FREE and open**
- ✅ **Extensive documentation** (soil survey manuals)

**Limitations:**
- ⚠️ **Complex structure** (requires soilDB package or SQL skills)
- ⚠️ **Large file sizes** (national SSURGO = 50+ GB)
- ⚠️ **Property uncertainty** (lab-measured vs. estimated)

**Validation:**
- Soil properties validated through lab analysis at ~500,000 sample locations
- Regular correlation to National Cooperative Soil Survey standards

**Priority Variables for Health Observatory (Top 20):**
1. **Drainage class (categorical)** - Vector-borne disease
2. **Percent poorly drained area (%)** - Mosquito habitat
3. **Hydrologic soil group (categorical)** - Runoff/flooding
4. **Saturated hydraulic conductivity (μm/s)** - Contamination transport
5. **pH (unitless)** - Heavy metal bioavailability
6. **Organic matter (%)** - Soil health, carbon storage
7. **Cation exchange capacity (meq/100g)** - Metal retention
8. **Sand content (%)** - Texture, dust potential
9. **Clay content (%)** - Texture, metal absorption
10. **Available water capacity (cm/cm)** - Agricultural productivity
11. **Wind erosion group** - Dust generation
12. **Depth to water table (cm)** - Groundwater vulnerability
13. **Flooding frequency (categorical)** - Disaster risk
14. **Prime farmland percent (%)** - Food security
15. **Erosion factor K** - Soil loss, dust
16. **Salinity (EC, mmhos/cm)** - Agricultural stress
17. **Heavy metal retention capacity (derived)** - Contamination buffering
18. **Nitrate leaching potential (categorical)** - Water quality
19. **Shrink-swell potential** - Infrastructure/housing
20. **Septic system suitability (categorical)** - Wastewater treatment

---

## SUMMARY: Physical Geography Data Hierarchy

**For US County Health Observatory, Prioritize:**

### **TOPOGRAPHY (Elevation, Slope, Aspect):**
1. **USGS 3DEP** (10-30m) → Complete terrain analysis (25 variables)
2. **USDA ERS** (county pre-calc) → Quick access, standardized (8 variables)
3. **NRCS Derivatives** (10m) → Hydrologic focus (15 variables)

### **GEOLOGY (Bedrock, Karst, Mining):**
4. **USGS Geologic Maps** (state compilations) → Radon, lithology (20 variables)
5. **USGS Karst Maps** (regional) → Groundwater vulnerability (12 variables)
6. **USGS Mineral Resources** (point data) → Heavy metal sources (12 variables)

### **SOILS (Most Comprehensive):**
7. **NRCS SSURGO/gSSURGO** (1:24,000) → THE ESSENTIAL SOURCE (100+ variables, 40 priority)

### **CRITICAL FINDING:**
**SSURGO is the SINGLE MOST IMPORTANT physical geography source** due to:
- Comprehensive property coverage (100+)
- Direct health relevance (drainage, pH, contamination)
- National coverage with high resolution
- Free and continuously updated

**IMPLEMENTATION PRIORITY:**
1. **Months 1-2:** SSURGO soil properties (40 priority variables)
2. **Months 3-4:** USGS 3DEP terrain (25 variables)
3. **Months 5-6:** USGS Geologic maps + Karst (32 variables)

**TOTAL NEW VARIABLES: ~100 priority variables from 7 sources**

---

**Version:** 1.0 (COMPLETE)
**Last Updated:** November 12, 2025
**Sources Documented:** 7 (USGS 3DEP, USDA ERS Terrain, NRCS Terrain Derivatives, USGS Geologic Maps, USGS Karst, USGS Minerals, NRCS SSURGO)
**Status:** Ready for data collection
