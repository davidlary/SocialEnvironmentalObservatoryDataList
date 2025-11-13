# GREEN SPACE, PESTICIDES, OCCUPATIONAL HAZARDS, VECTORS & SOCIAL ENVIRONMENT
## Comprehensive County-Level Environmental & Social Health Data Sources

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Repository:** GetData
**Category:** Environmental Health - Vegetation, Pesticide Exposure, Workplace Safety, Disease Vectors, Social Environment

---

## Executive Summary

This document provides comprehensive coverage of county-level data sources for five critical environmental and social health exposures:

1. **Green Space & Vegetation** - Mental health, physical activity, cardiovascular health
2. **Pesticide Application** - Parkinson's disease, cancer, neurodevelopmental effects
3. **Occupational Hazards** - Respiratory disease, injuries, cancers
4. **Vector-Borne Disease Risk** - Lyme disease, West Nile virus, emerging infections
5. **Social Environment** - Alcohol outlets, firearms, recreation facilities

All data sources provide county-level coverage or are aggregable to county level, with emphasis on longest available time ranges and most authoritative sources.

**Key Statistics:**
- **Green Space:** 2011-2024 (tree canopy), 2013-present (daily vegetation indices)
- **Pesticides:** 1992-2022 (30-year USGS county estimates, 400+ compounds)
- **Occupational:** 2016-present (OSHA injury data)
- **Vectors:** 1992-present (Lyme disease), 2003-present (West Nile virus)
- **Social:** 1986-present (Census business patterns)

---

## PART 1: GREEN SPACE & VEGETATION

### Health Impacts

**Benefits of Green Space Exposure:**

| Health Outcome | Evidence Strength | Mechanism | Dose-Response |
|----------------|-------------------|-----------|---------------|
| **Cardiovascular Disease** | Strong | Physical activity, stress reduction, air quality | 300m to parks → 20% ↓ CVD risk |
| **Mental Health (Depression)** | Strong | Stress reduction, social interaction, restoration | 300m to green space → 30% ↓ depression |
| **Obesity** | Moderate | Physical activity, recreation | Park access → ↓ BMI |
| **All-Cause Mortality** | Moderate | Multiple pathways | High NDVI → 10-20% ↓ mortality |
| **Respiratory Health** | Moderate | Air quality (trees filter PM2.5), allergen exposure | Tree canopy → ↓ asthma hospitalizations |
| **Cognitive Development (Children)** | Moderate | Attention restoration, stress reduction | School green space → ↑ test scores |
| **Social Cohesion** | Moderate | Public space for interaction | Park access → ↑ community engagement |
| **Heat Mitigation** | Strong | Evapotranspiration, shade | Tree canopy → 2-10°F cooler |

**Mechanisms:**
1. **Physical Activity:** Parks, trails encourage exercise
2. **Psychological Restoration:** Nature reduces stress (cortisol reduction)
3. **Air Quality:** Trees filter PM2.5, VOCs
4. **Social Interaction:** Green spaces facilitate community
5. **Heat Mitigation:** Urban heat island reduction

**Key Metrics:**
- **Tree Canopy Cover:** % land area with tree cover
- **NDVI (Normalized Difference Vegetation Index):** -1 to +1 scale (vegetation density)
- **Park Access:** % population within 10-minute walk (0.5 mile) to park
- **Green Space Area:** Acres per 1,000 residents

---

### Source 1: USDA Forest Service - Tree Canopy Cover (NLCD TCC)

**Official Name:** USDA Forest Service Tree Canopy Cover (part of NLCD Product Suite)
**Status:** ✅ HIGHEST QUALITY US TREE CANOPY DATA (30m resolution, 2011/2016/2021/2024)

#### Overview

The USDA Forest Service produces the National Land Cover Database (NLCD) Tree Canopy Cover product, providing continuous percent tree canopy estimates at 30-meter resolution for the contiguous United States. This is the definitive source for county-level tree canopy assessment.

#### Coverage

- **Geographic:** Contiguous United States (CONUS), all counties
- **Temporal:** 2011, 2016, 2021, **2024 (scheduled release June 2025)**
- **Spatial Resolution:** 30 meters (~0.22 acres per pixel)
- **Update Frequency:** Every 2-3 years (aligned with NLCD updates)

#### Variables Available

| Variable | Description | Units | Format |
|----------|-------------|-------|--------|
| Tree Canopy Cover | Continuous percent tree canopy | 0-100% | GeoTIFF (30m pixels) |
| Tree Canopy Gain | New tree cover since previous epoch | 0-100% | GeoTIFF |
| Tree Canopy Loss | Tree cover lost since previous epoch | 0-100% | GeoTIFF |
| Canopy Density Classes | Categorical: Low (0-20%), Medium (20-60%), High (60-100%) | Categorical | GeoTIFF |

#### Data Access

**Primary Download:**
- **URL:** https://data.fs.usda.gov/geodata/rastergateway/treecanopycover/
- **Format:** GeoTIFF, Cloud-Optimized GeoTIFF (COG)
- **Coverage:** State-by-state tiles or CONUS-wide mosaic
- **Size:** ~50 GB (CONUS), ~500 MB - 5 GB per state

**Alternative: MRLC (Multi-Resolution Land Characteristics Consortium)**
- **URL:** https://www.mrlc.gov/data
- **NLCD Tree Canopy Products:** Download alongside NLCD land cover
- **Same Data:** USDA Forest Service is source; MRLC is distribution portal

**Google Earth Engine:**
- **Dataset:** Search "NLCD Tree Canopy" in GEE Data Catalog
- **Advantage:** No download required; compute county statistics in cloud

**County-Level Aggregation Example (GEE):**
```javascript
// Google Earth Engine: Calculate county-level tree canopy cover

// Load county boundaries
var counties = ee.FeatureCollection("TIGER/2018/Counties");

// Load NLCD Tree Canopy Cover 2021
var treeCanopy = ee.Image("USFS/GTAC/LCMS/v2022-8/TCC/2021")
  .select('TCC');  // Tree Canopy Cover band

// Calculate county-level mean tree canopy cover
var countyTreeCanopy = treeCanopy.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean()
    .combine(ee.Reducer.median(), '', true)
    .combine(ee.Reducer.percentile([25, 75, 90]), '', true),
  scale: 30  // 30-meter resolution
});

// Export to CSV
Export.table.toDrive({
  collection: countyTreeCanopy,
  description: 'County_Tree_Canopy_2021',
  fileFormat: 'CSV'
});
```

**R Example (Local Processing):**
```r
library(terra)
library(sf)
library(tidyverse)
library(exactextractr)

# Read county boundaries
counties <- st_read("county_boundaries.shp")

# Read NLCD Tree Canopy Cover 2021 (GeoTIFF)
tcc_2021 <- rast("NLCD_2021_Tree_Canopy_Cover_CONUS.tif")

# Extract county-level statistics using exact_extract (weighted by pixel coverage)
county_tcc <- exact_extract(
  tcc_2021,
  counties,
  fun = c("mean", "median", "quantile"),
  quantiles = c(0.25, 0.75, 0.90),
  append_cols = c("GEOID", "NAME")
) %>%
  as_tibble() %>%
  rename(
    county_fips = GEOID,
    county_name = NAME,
    mean_tcc_pct = mean,
    median_tcc_pct = median,
    tcc_q25 = q25,
    tcc_q75 = q75,
    tcc_q90 = q90
  ) %>%
  mutate(
    low_canopy = mean_tcc_pct < 20,  # Low canopy flag
    high_canopy = mean_tcc_pct > 60   # High canopy flag
  )

write_csv(county_tcc, "county_tree_canopy_2021.csv")
```

#### Data Quality

**Strengths:**
- Highest spatial resolution for national tree canopy (30m)
- Continuous percent cover (more informative than binary tree/no-tree)
- Multi-epoch data (2011, 2016, 2021, 2024) allows change detection
- Validated against aerial imagery (accuracy ~85%)
- Free, open access

**Limitations:**
- Does not distinguish tree types (deciduous vs. coniferous, native vs. invasive)
- Cannot identify individual trees or tree health
- 30m resolution may miss small urban trees (street trees)
- Shadows, cloud cover can affect accuracy

**Validation:** USDA Forest Service validation: Overall accuracy 85%; user's accuracy (canopy) 89%; producer's accuracy 82%

#### Use Cases for County-Level Analysis

1. **Cardiovascular Disease Risk:** High canopy counties vs. low canopy → CVD rates
2. **Mental Health:** Tree canopy association with depression, anxiety prevalence
3. **Heat Mitigation:** Tree canopy cooling effect (link to extreme heat exposure)
4. **Environmental Justice:** Tree canopy disparities by income/race (tract-level analysis → county aggregation)
5. **Urban Forestry Planning:** Identify low-canopy counties for tree planting initiatives

**County-Level Metrics:**
- Mean tree canopy cover (%)
- Median tree canopy cover (%)
- % county area with >60% canopy (high canopy)
- % county area with <20% canopy (low canopy)
- Tree canopy change 2011-2021 (% gain/loss)

---

### Source 2: NASA Harmonized Landsat Sentinel-2 (HLS) - Vegetation Indices

**Official Name:** NASA Harmonized Landsat Sentinel-2 (HLS) Product Suite with Vegetation Indices
**Status:** ✅ HIGHEST TEMPORAL RESOLUTION (2-5 day, 30m, 2013-present)

#### Overview

The HLS project harmonizes surface reflectance data from Landsat 8/9 and Sentinel-2A/B to create a seamless, high-frequency (every 2-5 days) observation record. Vegetation indices (NDVI, EVI, NDMI) provide dynamic measures of vegetation greenness, health, and moisture.

#### Coverage

- **Geographic:** Global, 30m resolution
- **Temporal:**
  - Landsat 8: 2013-present
  - Sentinel-2A: 2015-present
  - Sentinel-2B: 2017-present
  - Combined: Every 2-5 days (cloud-free)
- **Spatial Resolution:** 30 meters
- **Update Frequency:** Near-real-time (2-3 day latency)

#### Variables Available

| Variable | Description | Range | Health Relevance |
|----------|-------------|-------|------------------|
| **NDVI (Normalized Difference Vegetation Index)** | Vegetation greenness | -1 to +1 (higher = greener) | Green space exposure, vegetation density |
| **EVI (Enhanced Vegetation Index)** | Vegetation greenness (less sensitive to atmosphere) | -1 to +1 | Improved in high-biomass areas |
| **MSAVI (Modified Soil-Adjusted Vegetation Index)** | Vegetation with soil brightness correction | -1 to +1 | Useful in sparse vegetation areas |
| **NDMI (Normalized Difference Moisture Index)** | Vegetation moisture content | -1 to +1 | Drought stress, irrigation |

**NDVI Interpretation:**
- **<0:** Water, clouds, snow
- **0-0.1:** Barren rock, sand
- **0.1-0.2:** Bare soil, sparse vegetation
- **0.2-0.4:** Grassland, shrubland
- **0.4-0.6:** Cropland, moderate vegetation
- **0.6-0.8:** Temperate/tropical forests
- **>0.8:** Dense tropical forests

#### Data Access

**NASA Earthdata:**
- **URL:** https://www.earthdata.nasa.gov/news/harmonized-landsat-sentinel-2-project-releases-vegetation-indices
- **HLSL30:** Landsat 8/9 surface reflectance + vegetation indices
- **HLSS30:** Sentinel-2A/B surface reflectance + vegetation indices
- **Download:** NASA Earthdata Search (https://search.earthdata.nasa.gov/)
- **Requires:** Free NASA Earthdata Login
- **Format:** HDF5, Cloud-Optimized GeoTIFF

**Google Earth Engine (Recommended for County Aggregation):**
- **Dataset:** "NASA/HLS/HLSL30/v002" (Landsat), "NASA/HLS/HLSS30/v002" (Sentinel-2)
- **Variables:** NDVI, EVI, MSAVI bands included
- **Cloud Processing:** No download needed; compute county statistics directly

**GEE Code Example:**
```javascript
// Google Earth Engine: Calculate county-level annual mean NDVI (2023)

// Load county boundaries
var counties = ee.FeatureCollection("TIGER/2018/Counties");

// Load HLS Sentinel-2 data for 2023, growing season (April-October)
var hls_s2 = ee.ImageCollection("NASA/HLS/HLSS30/v002")
  .filterDate('2023-04-01', '2023-10-31')
  .filter(ee.Filter.lt('CLOUD_COVERAGE', 30))  // <30% cloud cover
  .select(['B4', 'B5']);  // Red, NIR bands

// Calculate NDVI for each image
var addNDVI = function(image) {
  var ndvi = image.normalizedDifference(['B5', 'B4']).rename('NDVI');
  return image.addBands(ndvi);
};

var hls_ndvi = hls_s2.map(addNDVI).select('NDVI');

// Calculate growing season mean NDVI
var mean_ndvi_2023 = hls_ndvi.mean();

// Aggregate to county level
var county_ndvi = mean_ndvi_2023.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean()
    .combine(ee.Reducer.median(), '', true)
    .combine(ee.Reducer.stdDev(), '', true)
    .combine(ee.Reducer.percentile([90]), '', true),
  scale: 30,
  tileScale: 4  // Reduce memory usage for large counties
});

// Export
Export.table.toDrive({
  collection: county_ndvi,
  description: 'County_NDVI_Growing_Season_2023',
  fileFormat: 'CSV'
});
```

#### Data Quality

**Strengths:**
- Highest temporal resolution for vegetation monitoring (2-5 day)
- Long time series (2013-present, 11+ years)
- Surface reflectance corrected (atmospherically corrected, cloud-masked)
- Harmonized between Landsat and Sentinel-2 (seamless time series)
- 30m resolution suitable for urban and rural vegetation

**Limitations:**
- Requires cloud-free observations (cloudy days have no data)
- Growing season bias in vegetation indices (winter NDVI low in deciduous forests)
- NDVI saturates in very dense vegetation (use EVI in tropical forests)
- Does not distinguish vegetation types (forest vs. grass vs. crops)

**Validation:** Surface reflectance validated against ground measurements (r²=0.9+); NDVI accuracy depends on cloud masking quality

#### Use Cases

1. **Dynamic Green Space Exposure:** County-level NDVI time series (monthly, seasonal, annual)
2. **Seasonal Vegetation Patterns:** Spring greenup, fall senescence (phenology)
3. **Drought Monitoring:** NDMI (moisture) decline during droughts
4. **Urban Green Space Trends:** NDVI change over time (urbanization vs. greening)
5. **Agricultural Productivity:** Crop NDVI as proxy for yield (rural counties)

**County-Level Metrics:**
- Annual mean NDVI (growing season average)
- Peak NDVI (greenest month, typically July/August)
- NDVI trend (change per year, 2013-2024)
- % county area with NDVI >0.6 (forested)
- % county area with NDVI <0.2 (barren/urban)

---

### Source 3: Trust for Public Land - ParkServe / ParkScore

**Official Name:** Trust for Public Land ParkServe Database / ParkScore Index
**Status:** ✅ COMPREHENSIVE PARK ACCESS DATA (100 largest US cities, 2012-2022)

#### Overview

The Trust for Public Land (TPL) maintains the most comprehensive database of US parks and park access through two initiatives: ParkServe (park locations and access) and ParkScore (annual ranking of park systems in the 100 largest cities).

#### Coverage

- **Geographic:** 100 largest US cities (coverage expanding); some county-level data
- **Temporal:** 2012-2022 (annual ParkScore); ParkServe updated continuously
- **Spatial Resolution:** Park polygons, census block-level access metrics
- **Update Frequency:** ParkScore annual (May); ParkServe continuous updates

#### Variables Available (from README.md documentation)

**ParkScore Metrics (City-Level, Some County-Level):**

| Variable | Description | Units |
|----------|-------------|-------|
| Park Access Percentage | % residents within 10-minute walk (0.5 mile) to park | % |
| Park Acres per 1,000 Residents | Total park acreage / population × 1,000 | Acres/1,000 |
| Park Spending per Capita | City park budget / population | $/resident |
| Playgrounds per 10,000 Residents | Playground count / population × 10,000 | Count/10,000 |
| Median Park Size | Median acreage of parks in city | Acres |
| Parkland as Percentage of City Area | Park acres / total city area × 100 | % |

**ParkServe Database (Park-Level Data):**
- Park name, address, city, county, state, ZIP
- Park boundary (polygon)
- Park size (acres)
- Park type (local, state, national, special use)
- Amenities (playgrounds, sports fields, trails, water features)
- Ownership (city, county, state, federal, private)

#### Data Access

**ParkScore Rankings:**
- **URL:** https://www.tpl.org/parks
- **Annual Report:** PDF and interactive website (100 cities ranked)
- **Format:** Web interface, summary data tables
- **Download:** Limited public data download (contact TPL for research requests)

**ParkServe Database:**
- **URL:** https://www.tpl.org/parkserve
- **Interactive Map:** View park boundaries, 10-minute walk buffers
- **Park Finder:** Search parks by city, ZIP, address
- **Data Access:** Research partnerships (contact TPL); limited public API

**Data Request Example:**
```
Email: parkserve@tpl.org
Subject: Research Data Request - County-Level Park Access

I am requesting county-level park access data for [counties of interest] for health research.
Specifically, I need:
- % population within 10-minute walk to parks
- Park acres per 1,000 residents
- Park counts by type
- Time period: [years]

Purpose: [describe research]
```

#### Data Quality

**Strengths:**
- Most comprehensive US park database (local, state, national parks)
- Validated by city park departments
- 10-minute walk access metric (health-relevant threshold)
- Includes park amenities (playgrounds, trails important for physical activity)
- Annual updates (ParkScore)

**Limitations:**
- ParkScore: Only 100 largest cities (not all counties covered)
- ParkServe: Comprehensive for large cities, less complete for rural counties
- Data access: Not fully open (research requests required)
- Does not measure park quality or usage (only access and size)

**Validation:** TPL works with city park departments to validate park boundaries and amenities

#### Use Cases

1. **Physical Activity & Obesity:** Park access vs. obesity rates in urban counties
2. **Mental Health:** Park access vs. depression prevalence
3. **Environmental Justice:** Compare park access by neighborhood income/race (city analysis)
4. **Urban Planning:** Identify underserved areas (park deserts)
5. **Cardiovascular Disease:** Park density vs. CVD incidence

**County/City-Level Metrics:**
- % population within 10-minute walk to park
- Park acres per 1,000 residents
- Median park size
- Playgrounds per 10,000 children (0-17)
- Park spending per capita (budget indicator)

**Note:** For comprehensive county-level park data beyond 100 largest cities, consider combining:
- Census TIGER/Line Parks boundaries (https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)
- State/county park databases
- Protected Areas Database (PAD-US): https://www.usgs.gov/programs/gap-analysis-project/science/pad-us-data-overview

---

## PART 2: PESTICIDE APPLICATION

### Health Impacts

**Diseases Linked to Pesticide Exposure:**

| Health Outcome | Pesticide Class | Evidence Strength | Population at Risk |
|----------------|-----------------|-------------------|---------------------|
| **Parkinson's Disease** | Organophosphates, organochlorines, paraquat | Very Strong | Agricultural workers, rural residents |
| **Non-Hodgkin Lymphoma** | Glyphosate, 2,4-D, organophosphates | Strong | Farmers, pesticide applicators |
| **Leukemia (childhood)** | Agricultural pesticides (mixed) | Moderate | Children in agricultural areas |
| **Prostate Cancer** | Agricultural pesticides, dichlorvos | Moderate | Farmers, applicators |
| **Lung Cancer** | Arsenic-based pesticides (historical) | Moderate | Agricultural workers |
| **Neurodevelopmental Effects** | Organophosphates, pyrethroids | Strong | Children (prenatal, early childhood) |
| **ADHD, Autism Spectrum Disorder** | Organophosphates, pyrethroids | Emerging | Children in agricultural counties |
| **Reduced IQ** | Organophosphates | Strong | Children with prenatal exposure |
| **Reproductive Effects** | Multiple classes | Moderate | Women of reproductive age, pregnant women |
| **Birth Defects** | 2,4-D, atrazine, others | Moderate | Pregnant women in agricultural areas |
| **Endocrine Disruption** | Atrazine, DDT (historical) | Strong | General population, wildlife |
| **Respiratory Disease (Asthma)** | Multiple classes | Moderate | Agricultural workers, rural children |

**High-Risk Pesticides:**
- **Paraquat:** Parkinson's disease (banned in EU, restricted in US)
- **Glyphosate (Roundup):** Non-Hodgkin lymphoma (IARC Group 2A)
- **Chlorpyrifos:** Neurodevelopmental effects (organophosphate, EPA ban 2021)
- **Atrazine:** Endocrine disruption, birth defects

---

### Source 4: USGS Pesticide National Synthesis Project (PNSP) - County Estimates

**Official Name:** USGS Pesticide National Synthesis Project - Estimated Annual Agricultural Pesticide Use
**Status:** ✅ BEST COUNTY-LEVEL PESTICIDE DATA (1992-2022, 400+ compounds)

### 📋 COMPLETE USGS PESTICIDES CATALOG (TIER 2)

**For the complete catalog of all 650+ pesticide compounds tracked by USGS with CAS numbers, chemical classes, primary uses, environmental fate, and health concerns, see:**

**[USGS_PESTICIDES_COMPLETE_COMPOUND_LIST.md](USGS_PESTICIDES_COMPLETE_COMPOUND_LIST.md)**

This companion Tier 2 catalog provides:
- All 650+ USGS-tracked pesticide compounds organized by class (herbicides, insecticides, fungicides, fumigants)
- CAS numbers and chemical names for each compound
- Primary agricultural uses and target pests/weeds
- Application timing and typical crops
- Environmental fate (persistence, mobility, toxicity)
- Human health concerns and regulatory status
- County-level usage data availability (1992-2022)
- R code examples for pesticide exposure analysis

**Use this document (Tier 1)** for USGS pesticide data overview, top compounds, and data access methods.
**Use USGS_PESTICIDES_COMPLETE_COMPOUND_LIST.md (Tier 2)** to look up specific pesticide compounds or browse the complete 650+ compound catalog.

#### Overview

The USGS PNSP provides the most comprehensive county-level estimates of agricultural pesticide use in the United States. The project combines proprietary farm survey data (crop reporting districts) with USDA harvested crop acres to estimate pesticide application by active ingredient, crop, and county.

#### Coverage

- **Geographic:** All US counties with agricultural activity (~2,900 counties)
- **Temporal:** 1992-2022 (30-year time series!)
  - **Note:** Final estimates for 2018-2022 publishing 2025
- **Compounds:** ~400 pesticide active ingredients
  - Herbicides, insecticides, fungicides, fumigants, growth regulators
- **Crops:** All major US crops (corn, soybeans, wheat, cotton, rice, vegetables, fruits, nuts, pasture, etc.)
- **Update Frequency:** Annual preliminary estimates; revised after Census of Agriculture (every 5 years)

#### Variables Available

| Variable | Description | Units |
|----------|-------------|-------|
| Estimated Pesticide Use by Compound | Total kilograms of active ingredient applied | kg |
| Estimated Application Rate | Application rate per harvested acre | kg/ha (or lbs/acre) |
| Crop-Specific Pesticide Use | Use by crop (corn, soybeans, etc.) | kg |
| High/Low Estimates | Uncertainty range | kg |

**Pesticide Classes Covered:**
- **Herbicides:** Glyphosate, atrazine, 2,4-D, dicamba, metolachlor, acetochlor, pendimethalin, trifluralin, paraquat, imazethapyr
- **Insecticides:** Chlorpyrifos (until 2021), malathion, carbaryl, permethrin, cyfluthrin, lambda-cyhalothrin, imidacloprid, clothianidin
- **Fungicides:** Chlorothalonil, mancozeb, azoxystrobin, propiconazole, tebuconazole
- **Fumigants:** Metam sodium, 1,3-dichloropropene, chloropicrin
- **Total:** ~400 compounds

**Top 10 Agricultural Pesticides (by volume, 2020):**
1. Glyphosate (280 million lbs)
2. Atrazine (70 million lbs)
3. Metolachlor-S (45 million lbs)
4. 2,4-D (40 million lbs)
5. Acetochlor (32 million lbs)
6. Dicamba (25 million lbs)
7. Pendimethalin (18 million lbs)
8. Metam-sodium (17 million lbs)
9. Sulfur (16 million lbs, fungicide)
10. Chlorpyrifos (12 million lbs, banned 2021)

#### Data Access

**Interactive Tool:**
- **URL:** https://www.usgs.gov/tools/estimated-annual-agricultural-pesticide-use
- **Features:**
  - Select pesticide compound, year, crop
  - View county-level map
  - Download county estimates (CSV)
- **Download Format:** CSV with county FIPS, pesticide, year, estimated use (kg)

**Bulk Download:**
- **URL:** https://water.usgs.gov/nawqa/pnsp/usage/maps/
- **State-Level Downloads:** CSV files by state, year, compound
- **National Downloads:** Large CSV files (all counties, all compounds, all years)

**Download Example:**
```r
library(tidyverse)

# Download USGS PNSP data for a specific pesticide (glyphosate) and year (2020)
glyphosate_2020_url <- "https://water.usgs.gov/nawqa/pnsp/usage/maps/county-level/PesticideUseEstimates_GLYPHOSATE_2020.csv"

glyphosate_2020 <- read_csv(glyphosate_2020_url)

# Structure:
# FIPS_CODE, COMPOUND, YEAR, EPEST_LOW_KG, EPEST_HIGH_KG, CROP

# Aggregate all crops to county total
county_glyphosate <- glyphosate_2020 %>%
  group_by(FIPS_CODE, COMPOUND, YEAR) %>%
  summarize(
    total_use_kg = sum((EPEST_LOW_KG + EPEST_HIGH_KG) / 2, na.rm = TRUE),  # Midpoint
    total_use_lbs = total_use_kg * 2.20462,
    .groups = "drop"
  )

# Join with county land area to get kg/km² (exposure intensity)
county_area <- read_csv("county_land_area.csv")  # County FIPS, area_km2

county_glyphosate_intensity <- county_glyphosate %>%
  left_join(county_area, by = c("FIPS_CODE" = "county_fips")) %>%
  mutate(
    use_kg_per_km2 = total_use_kg / area_km2
  )

write_csv(county_glyphosate_intensity, "county_glyphosate_2020.csv")
```

**Multi-Year Time Series Example:**
```r
# Download glyphosate use 1992-2020 (all years)
years <- 1992:2020
glyphosate_urls <- paste0(
  "https://water.usgs.gov/nawqa/pnsp/usage/maps/county-level/PesticideUseEstimates_GLYPHOSATE_",
  years,
  ".csv"
)

glyphosate_timeseries <- map_dfr(glyphosate_urls, read_csv)

# Aggregate to county-year total
county_glyphosate_ts <- glyphosate_timeseries %>%
  group_by(FIPS_CODE, YEAR) %>%
  summarize(
    total_use_kg = sum((EPEST_LOW_KG + EPEST_HIGH_KG) / 2, na.rm = TRUE),
    .groups = "drop"
  )

# Calculate trend: glyphosate increase over time
county_trends <- county_glyphosate_ts %>%
  group_by(FIPS_CODE) %>%
  summarize(
    use_1992_2000 = mean(total_use_kg[YEAR <= 2000], na.rm = TRUE),
    use_2011_2020 = mean(total_use_kg[YEAR >= 2011], na.rm = TRUE),
    pct_change = ((use_2011_2020 - use_1992_2000) / use_1992_2000) * 100,
    .groups = "drop"
  )

# Identify counties with highest glyphosate increase (GMO crop adoption)
top_increase <- county_trends %>%
  filter(!is.na(pct_change) & pct_change > 0) %>%
  arrange(desc(pct_change)) %>%
  head(20)
```

#### Data Quality

**Strengths:**
- **Best available county-level pesticide estimates** (only comprehensive source)
- Long time series (1992-2022, 30 years)
- Covers 400+ compounds (nearly all agricultural pesticides)
- Crop-specific estimates (can link to specific exposures)
- Validated against state-level USDA survey data (R²=0.85-0.95)
- Free, open access

**Limitations:**
- Estimates, not direct measurements (modeled from proprietary surveys + USDA crop data)
- Uncertainty ranges (high/low estimates provided)
- Agricultural pesticides only (does not include residential, golf course, forestry, or structural pesticides)
- County-level aggregation masks within-county variation (some farms use, others don't)
- Suppression: Counties with <3 farms growing a crop may be suppressed
- 2018-2022 final estimates not yet published (as of Nov 2024)

**Methodology:**
1. Proprietary farm survey data at crop reporting district (CRD) level (~10 counties per CRD)
2. USDA NASS harvested crop acres by county
3. Allocation: CRD-level application rates × county harvested acres = county pesticide use

**Validation:** State-level PNSP estimates correlate r²=0.85-0.95 with USDA NASS state-level chemical use surveys (available for select states/years)

**California Exception:** California data uses California Department of Pesticide Regulation (DPR) Pesticide Use Reporting (PUR), which is more detailed (mandatory reporting, section-level).

#### Use Cases for County-Level Analysis

1. **Parkinson's Disease Risk:** High organophosphate/paraquat counties → Parkinson's incidence (strongest environmental link)
2. **Childhood Leukemia:** Agricultural counties with high pesticide use → childhood cancer rates
3. **Neurodevelopmental Outcomes:** Prenatal exposure (maternal residence in high-pesticide counties) → ADHD, ASD, IQ
4. **Non-Hodgkin Lymphoma:** Glyphosate use → NHL incidence (occupational + environmental)
5. **Birth Defects:** Atrazine, 2,4-D, other herbicides → congenital anomalies
6. **Endocrine Disruption:** Atrazine (water contamination) → reproductive outcomes

**County-Level Metrics:**
- Total pesticide use (all compounds, kg/year)
- Glyphosate use (kg/year) - most widely used
- Organophosphate insecticides (kg/year) - neurotoxic
- Atrazine use (kg/year) - endocrine disruptor
- Paraquat use (kg/year) - Parkinson's link
- Pesticide intensity (kg/km² agricultural land)
- Trend: pesticide use change 1992-2022

**High-Priority Pesticides for Health Studies:**
1. **Glyphosate** (herbicide, NHL risk)
2. **Atrazine** (herbicide, endocrine disruption, birth defects)
3. **Chlorpyrifos** (insecticide, neurodevelopmental - banned 2021)
4. **Paraquat** (herbicide, Parkinson's disease)
5. **2,4-D** (herbicide, cancer, birth defects)
6. **Organophosphates** (insecticides, neurotoxicity)

---

## PART 3: OCCUPATIONAL HAZARDS

### Health Impacts

**Work-Related Diseases and Injuries:**

| Health Outcome | Occupational Exposure | High-Risk Industries (NAICS) |
|----------------|----------------------|------------------------------|
| **Respiratory Disease (Silicosis, Asbestosis, COPD)** | Silica dust, asbestos, coal dust, wood dust | Mining (21), Construction (23), Manufacturing (31-33) |
| **Lung Cancer** | Asbestos, diesel exhaust, silica, radon | Mining (21), Construction (23), Transportation (48-49) |
| **Mesothelioma** | Asbestos | Construction (23), Shipbuilding (336611) |
| **Musculoskeletal Disorders** | Repetitive motion, heavy lifting | Manufacturing (31-33), Healthcare (62), Warehousing (493) |
| **Hearing Loss** | Noise (>85 dB) | Manufacturing (31-33), Construction (23), Mining (21) |
| **Traumatic Injuries** | Falls, machinery, struck-by | Construction (23), Agriculture (11), Transportation (48-49) |
| **Cardiovascular Disease** | Shift work, stress, noise | Healthcare (62), Manufacturing (31-33), Transportation (48-49) |
| **Neurological Disorders** | Solvents, heavy metals, pesticides | Manufacturing (31-33), Agriculture (11), Automotive repair (8111) |
| **Dermatological Conditions** | Chemicals, UV exposure | Agriculture (11), Construction (23), Healthcare (62) |
| **Heatstroke/Heat Illness** | Outdoor work, high temps | Agriculture (11), Construction (23), Landscaping (5613) |

**Leading Causes of Work-Related Death (2024):**
1. Transportation incidents (38%)
2. Falls, slips, trips (15%)
3. Violence and other injuries (14%)
4. Contact with objects/equipment (12%)
5. Exposure to harmful substances (9%)

---

### Source 5: OSHA Injury Tracking Application (ITA) Data

**Official Name:** OSHA Injury Tracking Application (ITA) - Establishment-Specific Injury and Illness Data
**Status:** ✅ COMPREHENSIVE WORKPLACE INJURY DATABASE (2016-present, 2024 data published April 2025)

#### Overview

OSHA's Injury Tracking Application (ITA) collects workplace injury and illness data from establishments with 100+ employees (full data) and 20-99 employees (summary data). This is the most comprehensive source of occupational injury data in the United States.

#### Coverage

- **Geographic:** United States, establishment-level (geocoded by address)
- **Temporal:** 2016-present for Form 300A (summary); 2024-present for Forms 300/301 (detailed)
  - **2024 Data:** Published April 2025 (most recent)
- **Establishments:** ~230,000 establishments reporting (varies by year)
- **Workers Covered:** ~33 million employees at reporting establishments
- **Industries:** All NAICS sectors (21-81)

#### Variables Available

**Form 300A (Summary Data, 2016-present):**

| Variable | Description | Units |
|----------|-------------|-------|
| Total Injury and Illness Cases | OSHA-recordable cases | Count |
| Days Away From Work Cases | Injuries requiring ≥1 day away | Count |
| Job Transfer/Restriction Cases | Modified duty cases | Count |
| Other Recordable Cases | First aid beyond treatment | Count |
| Total Deaths | Workplace fatalities | Count |
| Skin Disorders | Work-related skin conditions | Count |
| Respiratory Conditions | Work-related respiratory illness | Count |
| Hearing Loss | Work-related noise-induced hearing loss | Count |
| Poisoning | Chemical poisonings | Count |
| All Other Illnesses | Other occupational diseases | Count |

**Forms 300/301 (Detailed Data, 2024-present):**

| Variable | Description | Details |
|----------|-------------|---------|
| Case Details | Nature of injury/illness | ICD-10 coding, body part, event type |
| Injury/Illness Type | Specific condition | Fracture, laceration, burn, amputation, etc. |
| Event/Exposure | How injury occurred | Fall, struck-by, overexertion, chemical exposure |
| Days Away/Restricted | Duration of impact | Number of days |
| Return to Work | Date returned to work | Date |

**Establishment Information:**
- Establishment name
- NAICS code (6-digit industry classification)
- Address (street, city, state, ZIP)
- County (derivable from ZIP/address)
- Establishment size (employment range)

#### 2024 Data Highlights (Published April 2025)

- **Total Cases:** 527,116 injuries and illnesses
- **Days Away Cases:** 500,572
- **Job Transfer/Restriction:** 410,604
- **Fatalities:** 750 workplace deaths
- **Skin Disorders:** 6,600 cases
- **Respiratory Conditions:** 30,000 cases
- **Hearing Loss:** 10,500 cases

#### Data Access

**OSHA ITA Portal:**
- **URL:** https://www.osha.gov/data
- **Establishment Search:** Search by company name, city, state, industry
- **Data Download:**
  - **By Year:** Download full dataset for 2016-2024 (CSV, Excel)
  - **By Industry:** Filter by NAICS code
  - **By Geography:** Filter by state (county requires geocoding)

**Download Example:**
```r
library(tidyverse)

# Download OSHA ITA 2024 data (Form 300A)
osha_2024_url <- "https://www.osha.gov/Establishment-Specific-Injury-and-Illness-Data-2024.csv"

osha_2024 <- read_csv(osha_2024_url)

# Key columns:
# Establishment_Name, Address, City, State, Zip, NAICS, Industry_Description,
# Total_Cases, Days_Away_Cases, Transfer_Restriction_Cases, Deaths,
# Skin_Disorders, Respiratory_Conditions, Hearing_Loss, Poisoning, Other_Illnesses,
# Total_Hours_Worked, Annual_Average_Employees

# Geocode establishments to county FIPS (requires geocoding service)
# Option 1: Use ZIP code to county crosswalk (approximate)
zip_to_county <- read_csv("HUD_ZIP_COUNTY_CROSSWALK.csv")

osha_county <- osha_2024 %>%
  left_join(zip_to_county, by = c("Zip" = "ZIP")) %>%
  select(Establishment_Name, COUNTY_FIPS, NAICS, Total_Cases, Days_Away_Cases, Deaths, everything())

# Aggregate to county level
county_injuries <- osha_county %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    establishments = n(),
    total_cases = sum(Total_Cases, na.rm = TRUE),
    days_away_cases = sum(Days_Away_Cases, na.rm = TRUE),
    fatalities = sum(Deaths, na.rm = TRUE),
    respiratory = sum(Respiratory_Conditions, na.rm = TRUE),
    hearing_loss = sum(Hearing_Loss, na.rm = TRUE),
    total_workers = sum(Annual_Average_Employees, na.rm = TRUE),
    .groups = "drop"
  ) %>%
  mutate(
    injury_rate = (total_cases / total_workers) * 200000,  # OSHA rate per 100 FTE
    fatality_rate = (fatalities / total_workers) * 200000
  )

write_csv(county_injuries, "county_occupational_injuries_2024.csv")
```

#### Data Quality

**Strengths:**
- Official regulatory data (OSHA-mandated reporting)
- Comprehensive coverage (100+ employee establishments)
- Detailed injury/illness classification (Forms 300/301 starting 2024)
- Annual updates
- Industry-specific data (NAICS codes)

**Limitations:**
- **Underreporting:** Employers may underreport to avoid OSHA scrutiny (estimated 30-50% underreporting)
- **Coverage Gaps:** Small establishments (<20 employees) not required to report; self-employed excluded
- **Geographic Aggregation:** Establishment-level data requires geocoding to aggregate to county level (not provided pre-aggregated)
- **Lag Time:** Current year data released ~April of following year (2024 data in April 2025)
- **Limited Occupational Disease Coverage:** Chronic diseases (cancer, COPD from long-term exposures) underrepresented; focus on acute injuries

**OSHA Calculation:** Injury rate = (Number of cases × 200,000) / Total hours worked by all employees
- 200,000 = 100 full-time employees working 40 hours/week, 50 weeks/year

#### Use Cases for County-Level Analysis

1. **Industry-Specific Hazards:** Counties with high mining (NAICS 21) → silicosis, black lung
2. **Construction Safety:** High construction employment (NAICS 23) → fall injuries, heat illness
3. **Agricultural Injuries:** Farm counties (NAICS 11) → machinery injuries, pesticide exposure
4. **Manufacturing Exposure:** Manufacturing counties (NAICS 31-33) → repetitive strain, chemical exposure, hearing loss
5. **Health Disparities:** Occupational injury rates by county socioeconomic status (low-wage workers higher risk)

**County-Level Metrics:**
- Total OSHA-recordable cases per 100,000 workers
- Days-away-from-work injury rate
- Workplace fatality rate
- Respiratory conditions per 100,000 workers (occupational lung disease proxy)
- Hearing loss cases per 100,000 workers (noise exposure)

**High-Risk Industries to Track (by NAICS):**
- **21 - Mining:** Silica, coal dust, traumatic injuries
- **23 - Construction:** Falls, asbestos, silica, heat illness
- **31-33 - Manufacturing:** Repetitive strain, machinery, chemicals, noise
- **48-49 - Transportation/Warehousing:** Musculoskeletal, vehicle crashes
- **62 - Healthcare:** Musculoskeletal (patient handling), infectious disease, violence

---

### Source 6: Census County Business Patterns - Industry Employment (Proxy)

**Official Name:** Census Bureau County Business Patterns (CBP)
**Status:** ✅ LONGEST INDUSTRY EMPLOYMENT TIME SERIES (1986-2023, 37 years)

**Already Documented:** See CBP_QCEW_COMPREHENSIVE_DOCUMENTATION.md

**Occupational Hazard Use:**
While CBP does not measure exposures directly, industry employment serves as a **proxy for occupational hazard distribution**:

| NAICS | Industry | Occupational Hazard Proxy |
|-------|----------|---------------------------|
| 21 | Mining, Quarrying, Oil & Gas Extraction | Silica dust, diesel exhaust, coal dust exposure |
| 23 | Construction | Asbestos, falls, heat stress, lead |
| 31-33 | Manufacturing | Chemical exposure, noise, repetitive strain |
| 11 | Agriculture, Forestry, Fishing | Pesticides, heat, machinery injuries |
| 48-49 | Transportation & Warehousing | Diesel exhaust, shift work, crashes |

**County-Level Proxy Variables:**
- % workforce in mining (NAICS 21) → silica exposure proxy
- % workforce in construction (NAICS 23) → asbestos exposure proxy
- % workforce in manufacturing (NAICS 31-33) → chemical exposure proxy
- % workforce in agriculture (NAICS 11) → pesticide exposure proxy

**Why Use CBP as Proxy:**
- County-level detail (OSHA ITA requires geocoding)
- Long time series (1986-2023, 37 years) vs. OSHA ITA (2016-present)
- All establishment sizes (OSHA ITA: 20+ employees only)

---

## PART 4: VECTOR-BORNE DISEASE RISK

### Health Impacts

**Vector-Borne Diseases in United States:**

| Disease | Vector | Annual US Cases | Geographic Distribution | Severity |
|---------|--------|-----------------|-------------------------|----------|
| **Lyme Disease** | Blacklegged tick (*Ixodes scapularis*) | ~35,000 reported (est. 476,000 actual) | Northeast, Upper Midwest, Pacific Coast | Arthritis, cardiac, neurological complications if untreated |
| **West Nile Virus** | Mosquitoes (*Culex* species) | ~2,400 cases/year (varies widely) | All 48 states | Neuroinvasive disease (meningitis, encephalitis) 1 in 150 infections |
| **Rocky Mountain Spotted Fever** | Dog tick (*Dermacentor variabilis*) | ~6,200 cases/year | Nationwide, concentrated in South-Central US | 5-10% fatality if untreated |
| **Anaplasmosis** | Blacklegged tick | ~6,000 cases/year | Northeast, Upper Midwest | Flu-like illness, hospitalization common |
| **Babesiosis** | Blacklegged tick | ~2,000 cases/year | Northeast | Malaria-like, severe in immunocompromised |
| **Ehrlichiosis** | Lone star tick (*Amblyomma americanum*) | ~2,000 cases/year | South-Central, Southeast US | Flu-like, can be severe |
| **Dengue** | Aedes mosquitoes | ~1,000 locally-acquired cases/year | Florida, Texas, Hawaii | Hemorrhagic fever, shock syndrome (severe cases) |
| **Chikungunya** | Aedes mosquitoes | <100 locally-acquired | Florida, Texas | Chronic joint pain |
| **Zika Virus** | Aedes mosquitoes | <50 locally-acquired (2016 outbreak past) | Florida, Texas | Microcephaly (birth defect), Guillain-Barre |
| **Powassan Virus** | Blacklegged tick | ~50 cases/year | Northeast, Great Lakes | Encephalitis, 10-15% fatality |

**Climate Change Impact:** Range expansion of ticks and mosquitoes; Lyme disease expanding north and west; mosquito season lengthening

---

### Source 7: CDC ArboNET - Arboviral Disease Surveillance

**Official Name:** CDC ArboNET - National Arboviral Diseases Surveillance System
**Status:** ✅ COMPREHENSIVE MOSQUITO-BORNE DISEASE SURVEILLANCE (2003-present for West Nile)

#### Overview

ArboNET is CDC's national surveillance system for mosquito-borne (arboviral) diseases, including West Nile virus, Zika, Dengue, Chikungunya, and others. Data are reported by state/local health departments to CDC, including **county of residence** for human cases.

#### Coverage

- **Geographic:** United States, county of residence for human cases
- **Temporal:** 2003-present (West Nile comprehensive); varies by disease
  - West Nile: 2003-present (21 years)
  - Zika: 2016-present
  - Dengue: 2010-present (locally-acquired tracking)
  - Chikungunya: 2014-present
- **Update Frequency:** Weekly during mosquito season (May-November), annual summaries
- **2024 Status:** Current season data updated every 1-2 weeks (check CDC website)

#### Variables Available

**Human Disease Cases (County of Residence):**

| Variable | Description | Units |
|----------|-------------|-------|
| West Nile Virus Cases | Total human cases | Count |
| WNV Neuroinvasive Disease | Meningitis, encephalitis | Count |
| WNV Non-Neuroinvasive (Fever) | Milder West Nile fever | Count |
| Zika Cases (Locally-Acquired) | Mosquito transmission in US | Count |
| Dengue Cases (Locally-Acquired) | Mosquito transmission in US | Count |
| Chikungunya Cases (Locally-Acquired) | Mosquito transmission in US | Count |
| St. Louis Encephalitis | Rare arboviral disease | Count |
| Eastern Equine Encephalitis | Rare, severe arboviral disease | Count |
| Powassan Virus | Rare tick-borne virus (also in ArboNET) | Count |

**Mosquito Surveillance Data (Some States):**
- Mosquito infection rate (% pools positive)
- Mosquito species identified
- County-level mosquito activity

**Veterinary Surveillance:**
- Horse cases (sentinel animals for WNV)
- Dead bird reports (crow, jay - WNV indicators)

#### Data Access

**CDC West Nile Virus Website:**
- **URL:** https://www.cdc.gov/westnile/statsmaps/index.html
- **Interactive Maps:** County-level WNV cases, current season and historical
- **Data Downloads:** Historical summary tables (CSV, Excel)
- **Weekly Updates:** May-November (mosquito season)
- **Annual Summaries:** Final data published ~March following year

**CDC WONDER (Historical Data Query):**
- **URL:** https://wonder.cdc.gov/
- **ArboNET Data:** Query by county, year, disease, neuroinvasive vs. non-neuroinvasive
- **Format:** CSV, text table downloads

**State Health Department Portals:**
- Many states publish detailed ArboNET data (mosquito surveillance, case maps)
- **Examples:**
  - California: https://westnile.ca.gov/
  - Texas: https://www.dshs.texas.gov/texas-arbovirus-surveillance
  - New York: https://www.health.ny.gov/diseases/west_nile_virus/

**Download Example (CDC Summary Data):**
```r
library(tidyverse)

# Download CDC West Nile Virus summary data (2023)
wnv_2023 <- read_csv("CDC_WNV_Summary_2023.csv")

# Aggregate to county level (already county-level in CDC data)
# Columns: State, County, Total_Cases, Neuroinvasive, Non_Neuroinvasive, Deaths

# Calculate incidence rates (requires county population)
county_pop <- read_csv("county_population_2023.csv")

wnv_incidence <- wnv_2023 %>%
  left_join(county_pop, by = c("State", "County")) %>%
  mutate(
    incidence_rate = (Total_Cases / Population) * 100000,  # Per 100,000
    neuroinvasive_rate = (Neuroinvasive / Population) * 100000
  )

# Identify high-risk counties (>5 cases per 100,000)
high_risk <- wnv_incidence %>%
  filter(incidence_rate > 5) %>%
  arrange(desc(incidence_rate))

write_csv(wnv_incidence, "county_west_nile_incidence_2023.csv")
```

#### 2023 Data Summary

- **Total Cases:** 2,406 West Nile virus cases
- **Neuroinvasive Cases:** 1,494 (62%)
- **Deaths:** 182 (7.6% case-fatality rate)
- **States Reporting:** 47 jurisdictions
- **High-Incidence States:** Arizona, Nebraska, Colorado, Texas, California

#### Data Quality

**Strengths:**
- Official CDC surveillance data (reportable disease)
- County of residence reported (true geographic distribution)
- Weekly updates during mosquito season (near-real-time)
- Long time series (2003-present for WNV, 21 years)
- Clinical case definitions (laboratory-confirmed)

**Limitations:**
- Passive surveillance (underreporting estimated 30-70× for WNV; many asymptomatic/mild cases)
- Reporting completeness varies by state
- Small counts in low-incidence counties (statistical instability)
- Mosquito surveillance data not systematically compiled at national level (state-by-state)

**Case Definition:** Laboratory-confirmed (IgM antibody, PCR, virus isolation) or probable (clinical + epidemiologic link)

#### Use Cases for County-Level Analysis

1. **West Nile Virus Risk Assessment:** Identify endemic counties (repeated annual cases)
2. **Climate Change & Vector Expansion:** Track county-level WNV emergence over time (2003-2024)
3. **Environmental Risk Factors:** Link WNV incidence to temperature, precipitation, land use, mosquito habitat
4. **Public Health Preparedness:** Prioritize mosquito control, public education in high-risk counties
5. **Emerging Diseases:** Monitor Zika, Dengue locally-acquired cases (Florida, Texas, Hawaii)

**County-Level Metrics:**
- West Nile virus cases (total, neuroinvasive, non-neuroinvasive)
- WNV incidence rate per 100,000 population
- Years with ≥1 case (endemic vs. sporadic)
- Peak year incidence (2012 was historic high: 5,674 cases)
- Trend: increasing, stable, or decreasing (2003-2024)

**High-Risk Regions:**
- **Great Plains:** Nebraska, South Dakota, North Dakota (consistent high incidence)
- **Southwest:** Arizona, Colorado, New Mexico
- **California Central Valley:** Agricultural irrigation creates mosquito habitat
- **Southern US:** Texas, Louisiana, Mississippi

---

### Source 8: CDC Lyme Disease Surveillance

**Official Name:** CDC National Notifiable Diseases Surveillance System (NNDSS) - Lyme Disease
**Status:** ✅ LONGEST TICK-BORNE DISEASE SURVEILLANCE (1992-present county data, 32+ years)

#### Overview

Lyme disease is the most common vector-borne disease in the United States, with ~35,000 reported cases annually (estimated 476,000 actual cases). CDC tracks confirmed and probable cases by county of residence.

#### Coverage

- **Geographic:** United States, county level
- **Temporal:** 1992-present (32+ years of county data)
- **Estimated Cases:** 476,000 annually (vs. ~35,000 reported - significant underreporting)
- **High-Incidence Counties:** Defined as >10 confirmed cases per 100,000 population
- **Update Frequency:** Annual surveillance summaries (released ~November for prior year)

#### Variables Available

| Variable | Description | Units |
|----------|-------------|-------|
| Confirmed Lyme Disease Cases | Laboratory-confirmed, meeting CDC case definition | Count |
| Probable Lyme Disease Cases | Clinical diagnosis, probable exposure | Count |
| Total Cases | Confirmed + probable | Count |
| Incidence Rate | Cases per 100,000 population | Rate |
| High-Incidence County Flag | ≥10 confirmed cases per 100,000 | Binary |
| Erythema Migrans Rash | Classic bull's-eye rash present | Count/% |
| Disseminated Disease | Neurological, cardiac, arthritic complications | Count/% |

**Lyme Disease Stages:**
1. **Early Localized:** Erythema migrans (EM) rash (70-80% of cases)
2. **Early Disseminated:** Multiple EM rashes, facial palsy, meningitis, carditis
3. **Late Disseminated:** Lyme arthritis (knee), neurological complications

#### Data Access

**CDC Lyme Disease Data Portal:**
- **URL:** https://www.cdc.gov/lyme/data-research/facts-stats/index.html
- **Interactive Maps:** County-level incidence rates, high-incidence counties
- **Data Downloads:**
  - Annual surveillance summaries (PDF reports)
  - County-level data tables (Excel, CSV)
  - Historical trends 1992-present

**CDC WONDER:**
- **Query:** Nationally Notifiable Diseases Surveillance System (NNDSS) → Lyme disease
- **Geographic Level:** County
- **Years:** 1992-present
- **Format:** CSV, text table

**Download Example:**
```r
library(tidyverse)

# Download CDC Lyme disease county data (2023)
lyme_2023 <- read_csv("CDC_Lyme_Disease_County_2023.csv")

# Columns: State, County, County_FIPS, Confirmed_Cases, Probable_Cases, Population, Incidence_Rate

# Identify high-incidence counties (≥10 per 100,000)
high_incidence_lyme <- lyme_2023 %>%
  mutate(
    high_incidence = Incidence_Rate >= 10
  ) %>%
  filter(high_incidence)

# Count high-incidence counties by state
state_lyme_summary <- high_incidence_lyme %>%
  group_by(State) %>%
  summarize(
    high_incidence_counties = n(),
    total_cases = sum(Confirmed_Cases + Probable_Cases, na.rm = TRUE),
    .groups = "drop"
  ) %>%
  arrange(desc(high_incidence_counties))

# Top 10 highest-incidence counties
top_lyme_counties <- lyme_2023 %>%
  arrange(desc(Incidence_Rate)) %>%
  head(10) %>%
  select(State, County, Confirmed_Cases, Incidence_Rate)

write_csv(lyme_2023, "county_lyme_disease_2023.csv")
```

#### Geographic Distribution

**High-Incidence Regions:**
- **Northeast:** Connecticut, Massachusetts, Rhode Island, New Jersey, New York, Pennsylvania, Maine, New Hampshire, Vermont
- **Upper Midwest:** Wisconsin, Minnesota, Michigan
- **Mid-Atlantic:** Maryland, Virginia, Delaware
- **Pacific Coast (Expanding):** Northern California, Oregon (less common, different tick species)

**High-Incidence Counties (Examples):**
- Nantucket County, MA: >1,000 cases per 100,000 (highest in US)
- Dutchess County, NY: >200 per 100,000
- Hunterdon County, NJ: >150 per 100,000

**Geographic Expansion:** Lyme disease endemic area expanding north (Canada), west (Midwest), and south (Virginia, North Carolina)

#### Data Quality

**Strengths:**
- Longest tick-borne disease surveillance (1992-present, 32 years)
- County-level data (county of residence)
- Case definition standardized (two-tier antibody testing)
- Annual updates
- High-incidence county classification (public health action threshold)

**Limitations:**
- **Massive Underreporting:** Estimated 10-14× more actual cases than reported (476,000 vs. 35,000)
- Passive surveillance (diagnosis and reporting depend on healthcare access, physician awareness)
- Endemic areas have better surveillance than emerging areas (underdetection in new counties)
- Small counts in low-incidence counties unstable

**Why Underreporting?**
- Many cases treated empirically without laboratory confirmation
- Rash-only cases (early localized) often not tested
- Private lab results not always reported to health departments

#### Use Cases

1. **Lyme Disease Risk Mapping:** Identify endemic counties (>10 per 100,000) for public education
2. **Tick Habitat & Land Use:** Link Lyme incidence to forest cover, land use (CDC uses "forested habitat" as predictor)
3. **Climate Change & Range Expansion:** Track county-level Lyme emergence 1992-2024 (northward, westward spread)
4. **Outdoor Recreation Risk:** Lyme risk for hikers, campers, hunters (link to park, forest access)
5. **Prevention Campaigns:** Target tick bite prevention (permethrin, tick checks) in high-incidence counties

**County-Level Metrics:**
- Confirmed Lyme disease cases
- Lyme incidence rate per 100,000
- High-incidence county flag (≥10 per 100,000)
- Years with ≥1 case (endemic vs. sporadic)
- Trend: increasing, stable, or decreasing (1992-2024)

---

### Source 9: CDC Tickborne Disease Surveillance

**Official Name:** CDC Tickborne Disease Surveillance - NNDSS
**Status:** ✅ COMPREHENSIVE TICKBORNE DISEASE TRACKING (2010-present systematic compilation)

**Additional Tick-Borne Diseases Beyond Lyme:**

| Disease | Data Availability | Geographic Distribution |
|---------|-------------------|-------------------------|
| **Anaplasmosis** | County-level, 2010-present | Northeast, Upper Midwest |
| **Babesiosis** | County-level, 2010-present | Northeast (coastal) |
| **Ehrlichiosis** | County-level, 2010-present | South-Central, Southeast US |
| **Rocky Mountain Spotted Fever** | County-level, 2010-present | Nationwide, concentrated in South-Central |
| **Tularemia** | County-level, 2010-present | South-Central, Western US |
| **Powassan Virus** | County-level, 2010-present | Northeast, Great Lakes |
| **Heartland Virus** | County-level (rare), 2010-present | Midwest, South-Central (emerging) |
| **Bourbon Virus** | County-level (very rare), 2010-present | Midwest (emerging) |

**Data Access:** Same as Lyme disease (CDC website, CDC WONDER)
**Annual Summaries:** https://www.cdc.gov/ticks/data-research/facts-stats/tickborne-disease-surveillance-data-summary.html

---

## PART 5: SOCIAL ENVIRONMENT

### Health Impacts

**Social Environment & Health:**

| Environmental Factor | Health Outcomes | Mechanism |
|---------------------|-----------------|-----------|
| **Alcohol Outlet Density** | Alcohol-related mortality, liver disease, injuries, violence, drunk driving crashes | Increased availability → increased consumption |
| **Firearm Availability** | Firearm homicides, suicides, unintentional injuries | Means availability, impulsivity |
| **Recreation Facility Access** | Obesity ↓, cardiovascular disease ↓, mental health ↑ | Physical activity, social engagement |
| **Fast Food Density** | Obesity, diabetes, cardiovascular disease | Poor diet, high calorie intake |
| **Social Capital** | All-cause mortality ↓, mental health ↑, crime ↓ | Community cohesion, trust, support |

---

### Source 10: Census County Business Patterns - Alcohol Outlets

**Official Name:** Census Bureau County Business Patterns (CBP)
**Status:** ✅ LONGEST BUSINESS ESTABLISHMENT TIME SERIES (1986-2023, 37 years)

**Already Documented:** See CBP_QCEW_COMPREHENSIVE_DOCUMENTATION.md

**Alcohol Outlet Variables (NAICS Codes):**

| NAICS | Business Type | Description |
|-------|---------------|-------------|
| **445310** | Beer, Wine, and Liquor Stores | Off-premise (retail sales for home consumption) |
| **722410** | Drinking Places (Alcoholic Beverages) | On-premise (bars, taverns, nightclubs) |
| **722511** | Full-Service Restaurants | Many serve alcohol on-premise |
| **445110** | Supermarkets and Grocery Stores | Often sell beer, wine |
| **447110** | Gasoline Stations with Convenience Stores | Often sell beer, wine |

**County-Level Metrics:**
- Off-premise alcohol outlets per 10,000 population (NAICS 445310)
- On-premise alcohol outlets per 10,000 population (NAICS 722410)
- Total alcohol outlet density (off + on-premise)
- Ratio on-premise : off-premise (bar culture vs. retail culture)

**Research Use:**
High correlation (r=0.89) between CBP alcohol establishment counts and state/local licensing data (Campbell et al., 2013, *Addiction*)

**Health Associations:**
- 1 additional off-premise outlet per 10,000 → 3.4% increase in alcohol-attributable deaths (Gruenewald et al., 2014)
- High on-premise outlet density → increased assault rates, DUI crashes
- Alcohol outlet density → liver disease mortality (R²=0.65, Siegel et al., 2016)

#### Data Access

**CBP Data:**
- **URL:** https://www.census.gov/programs-surveys/cbp.html
- **Years:** 1986-2023 (2024 data releases summer 2026)
- **Format:** CSV, API
- **Variables:** Establishment count, employment, payroll by NAICS code and county FIPS

**Download Example:**
```r
library(tidyverse)

# Download CBP 2023 county data
cbp_2023 <- read_csv("CBP_2023_County.csv")

# Filter to alcohol-related NAICS codes
alcohol_outlets <- cbp_2023 %>%
  filter(NAICS %in% c("445310", "722410")) %>%
  group_by(FIPS, NAICS) %>%
  summarize(
    establishments = sum(ESTABLISHMENTS, na.rm = TRUE),
    .groups = "drop"
  ) %>%
  pivot_wider(
    names_from = NAICS,
    values_from = establishments,
    names_prefix = "NAICS_",
    values_fill = 0
  )

# Join with county population
county_pop <- read_csv("county_population_2023.csv")

alcohol_density <- alcohol_outlets %>%
  left_join(county_pop, by = "FIPS") %>%
  mutate(
    off_premise_per_10k = (NAICS_445310 / POPULATION) * 10000,
    on_premise_per_10k = (NAICS_722410 / POPULATION) * 10000,
    total_density = off_premise_per_10k + on_premise_per_10k
  )

write_csv(alcohol_density, "county_alcohol_outlet_density_2023.csv")
```

---

### Source 11: ATF Federal Firearms Licensees (FFLs)

**Official Name:** Bureau of Alcohol, Tobacco, Firearms and Explosives - Federal Firearms Licensees
**Status:** ✅ COMPLETE FFL DATABASE (~133,716 licensees as of 2021, monthly updates)

#### Overview

ATF maintains a public database of all Federal Firearms Licensees (FFLs) - businesses and individuals licensed to manufacture, import, or sell firearms. This includes gun stores, pawnbrokers, manufacturers, and collectors.

#### Coverage

- **Geographic:** United States, all FFL holders
- **Temporal:** Current licenses (monthly state-level reports); historical listings available
- **FFL Types:**
  - Type 01: Dealer in firearms (gun stores) - majority
  - Type 02: Pawnbroker
  - Type 07: Manufacturer of firearms
  - Type 08: Importer of firearms
  - Type 09: Dealer in destructive devices
  - Type 10: Manufacturer of destructive devices
  - Type 11: Importer of destructive devices
  - Type 03: Collector of curios and relics
- **2021 Count:** ~133,716 active FFLs

#### Variables Available

| Variable | Description | Available Detail |
|----------|-------------|------------------|
| License Number | FFL identification | FFL number |
| License Type | Dealer, manufacturer, importer, pawnbroker, collector | Type code |
| Business Name | Trade name | Text |
| Address | Street, city, state, ZIP | Text |
| County | County name (derivable from address/ZIP) | Text |

#### Data Access

**ATF FFL Listings:**
- **URL:** https://www.atf.gov/firearms/listing-federal-firearms-licensees
- **Format:**
  - **Complete FFL List:** Downloadable file (text, CSV) with all active FFLs
  - **FFL eZ Check:** https://fflezcheck.atf.gov/ (individual FFL lookup by license number, name, address)
  - **Monthly State Reports:** PDF reports showing FFL counts by state, published monthly

**2024 Updates:**
- **2024 Firearms Commerce Report:** Published with FFL statistics
- **Compliance Inspections:** 9,696 FFL inspections conducted in 2024

**Download Example:**
```r
library(tidyverse)

# Download ATF FFL complete listing (hypothetical URL, check ATF website for current link)
ffl_data <- read_csv("ATF_FFL_Complete_Listing.csv")

# Columns: License_Number, License_Type, Business_Name, Street_Address, City, State, ZIP

# Geocode to county FIPS (requires ZIP to county crosswalk or geocoding service)
zip_to_county <- read_csv("HUD_ZIP_COUNTY_CROSSWALK.csv")

ffl_county <- ffl_data %>%
  left_join(zip_to_county, by = c("ZIP" = "ZIP")) %>%
  select(License_Number, License_Type, Business_Name, COUNTY_FIPS, everything())

# Aggregate to county level
county_ffl <- ffl_county %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    total_ffls = n(),
    dealers_type01 = sum(License_Type == "01", na.rm = TRUE),
    pawnbrokers_type02 = sum(License_Type == "02", na.rm = TRUE),
    manufacturers_type07 = sum(License_Type == "07", na.rm = TRUE),
    collectors_type03 = sum(License_Type == "03", na.rm = TRUE),
    .groups = "drop"
  )

# Join with population for per capita rates
county_pop <- read_csv("county_population_2024.csv")

ffl_density <- county_ffl %>%
  left_join(county_pop, by = "COUNTY_FIPS") %>%
  mutate(
    ffls_per_100k = (total_ffls / POPULATION) * 100000,
    dealers_per_100k = (dealers_type01 / POPULATION) * 100000
  )

write_csv(ffl_density, "county_ffl_density_2024.csv")
```

#### Data Quality

**Strengths:**
- Complete federal database (all licensed firearms dealers)
- Updated monthly (state reports)
- Address-level data (geocodable to county)
- License type classification

**Limitations:**
- Requires geocoding (address → county FIPS not provided)
- Does not capture illegal/unlicensed firearms sales
- FFL count does not equal firearm availability (secondary market, private sales)
- Collectors (Type 03) inflate counts but are not retail dealers

**Research Use:**
- FFL density (per 100,000 population) used as proxy for firearm availability in injury/suicide studies
- Correlation with firearm homicide, suicide rates (r=0.4-0.6, varies by state)

#### Use Cases

1. **Firearm Suicide Risk:** High FFL density counties → higher firearm suicide rates (means availability)
2. **Firearm Homicide:** FFL density vs. firearm homicide rates (weaker correlation than suicide)
3. **Youth Firearm Injury:** FFL proximity to schools, residential areas
4. **Unintentional Firearm Injuries:** Availability indicator
5. **Firearm Policy Analysis:** Track FFL counts before/after state firearm laws

**County-Level Metrics:**
- Total FFLs per 100,000 population
- Firearms dealers (Type 01) per 100,000 population
- Pawnbrokers (Type 02) per 100,000 population
- Ratio dealers : population (urban vs. rural differences)

---

### Source 12: Census County Business Patterns - Recreation Facilities

**Already Documented:** See CBP_QCEW_COMPREHENSIVE_DOCUMENTATION.md

**Recreation Facility Variables (NAICS Codes):**

| NAICS | Business Type | Health Benefit |
|-------|---------------|----------------|
| **713940** | Fitness and Recreational Sports Centers | Gyms, health clubs, yoga studios → physical activity, obesity ↓ |
| **713910** | Golf Courses and Country Clubs | Recreation, social interaction |
| **713950** | Bowling Centers | Social recreation |
| **713920** | Skiing Facilities | Physical activity, outdoor recreation |
| **713990** | All Other Amusement and Recreation Industries | Parks, playgrounds, recreation centers |
| **712190** | Nature Parks and Other Similar Institutions | Nature access, mental health ↑ |

**County-Level Metrics:**
- Fitness centers per 10,000 population (NAICS 713940)
- Total recreation facilities per 10,000 population
- Recreation spending (payroll proxy)

**Health Associations:**
- 1 additional fitness center per 10,000 → 0.2-0.5 BMI unit decrease (Wen & Zhang, 2017)
- Recreation facility access → increased physical activity, cardiovascular health
- County-level recreation density → mental health (social cohesion)

---

## Data Integration and Analysis Strategies

### Recommended County-Level Variables to Collect

#### Green Space & Vegetation (4 variables)
1. **Mean tree canopy cover (%)** - USDA Forest Service Tree Canopy, 2021
2. **Annual mean NDVI (growing season)** - NASA HLS, 2023
3. **Park access (% population within 10-min walk)** - Trust for Public Land ParkServe (100 cities)
4. **Tree canopy change 2011-2021 (%)** - USDA Forest Service

#### Pesticide Application (6 variables)
1. **Total agricultural pesticide use (kg/year)** - USGS PNSP, 2020 (or most recent)
2. **Glyphosate use (kg/year)** - USGS PNSP, 2020 (most widely used)
3. **Organophosphate insecticides (kg/year)** - USGS PNSP, 2020 (neurotoxic, Parkinson's link)
4. **Atrazine use (kg/year)** - USGS PNSP, 2020 (endocrine disruptor)
5. **Paraquat use (kg/year)** - USGS PNSP, 2020 (Parkinson's disease)
6. **Pesticide intensity (kg/km² agricultural land)** - USGS PNSP, 2020

#### Occupational Hazards (5 variables)
1. **Total OSHA-recordable injury rate (per 100,000 workers)** - OSHA ITA, 2024
2. **Days-away-from-work injury rate** - OSHA ITA, 2024
3. **Workplace fatality rate** - OSHA ITA, 2024
4. **% workforce in high-risk industries (mining, construction, manufacturing)** - Census CBP, 2023
5. **Respiratory conditions per 100,000 workers** - OSHA ITA, 2024 (occupational lung disease)

#### Vector-Borne Disease Risk (4 variables)
1. **West Nile virus incidence (per 100,000)** - CDC ArboNET, 2023
2. **Lyme disease incidence (per 100,000)** - CDC Lyme Surveillance, 2023
3. **High Lyme incidence flag (≥10 per 100,000)** - CDC Lyme Surveillance, 2023
4. **Years with ≥1 WNV case (endemic indicator)** - CDC ArboNET, 2003-2023

#### Social Environment (5 variables)
1. **Off-premise alcohol outlets per 10,000 population** - Census CBP, 2023 (NAICS 445310)
2. **On-premise alcohol outlets per 10,000 population** - Census CBP, 2023 (NAICS 722410)
3. **Federal firearms licensees (FFLs) per 100,000 population** - ATF FFL, 2024
4. **Fitness centers per 10,000 population** - Census CBP, 2023 (NAICS 713940)
5. **Total recreation facilities per 10,000 population** - Census CBP, 2023 (multiple NAICS)

**Total Priority Variables: 24**

---

## Update Schedule

| Data Source | Update Frequency | Expected Next Update |
|-------------|------------------|----------------------|
| USDA Tree Canopy Cover | Every 2-3 years | 2024 (June 2025 release) |
| NASA HLS Vegetation Indices | Daily | Ongoing (2-3 day latency) |
| Trust for Public Land ParkScore | Annual | May 2025 |
| USGS PNSP Pesticide Estimates | Annual (revised quinquennially) | 2018-2022 final (2025) |
| OSHA ITA Injury Data | Annual | 2025 data (April 2026) |
| CDC ArboNET (West Nile) | Weekly (season), Annual summary | 2024 final (March 2025) |
| CDC Lyme Disease Surveillance | Annual | 2024 data (November 2025) |
| Census CBP | Annual | 2024 data (Summer 2026) |
| ATF FFL | Monthly state reports | Monthly |

---

## API Keys and Access Requirements

**No API Key Required:**
- USDA Tree Canopy Cover (public download)
- NASA HLS via Google Earth Engine (requires Google account, no NASA key needed)
- Trust for Public Land data (research request)
- USGS PNSP (public download)
- OSHA ITA (public download)
- CDC ArboNET, Lyme Disease (public download)
- Census CBP (public download, API available)
- ATF FFL (public download)

**Optional API Keys (Free):**
- Google Earth Engine (requires Google account for cloud processing)
- Census Bureau API (for CBP data via API): https://api.census.gov/data/key_signup.html

---

## Citation

**Green Space:**
> U.S. Forest Service. (2024). NLCD Tree Canopy Cover. Retrieved from https://data.fs.usda.gov/geodata/rastergateway/treecanopycover/

> NASA. (2024). Harmonized Landsat Sentinel-2 (HLS) Product Suite. Retrieved from https://www.earthdata.nasa.gov/

**Pesticides:**
> U.S. Geological Survey. (2024). Pesticide National Synthesis Project - Estimated Annual Agricultural Pesticide Use. Retrieved from https://water.usgs.gov/nawqa/pnsp/usage/maps/

**Occupational:**
> U.S. Department of Labor, Occupational Safety and Health Administration. (2025). Injury Tracking Application Data. Retrieved from https://www.osha.gov/data

**Vector-Borne Diseases:**
> Centers for Disease Control and Prevention. (2024). ArboNET - National Arboviral Diseases Surveillance. Retrieved from https://www.cdc.gov/westnile/

> Centers for Disease Control and Prevention. (2024). Lyme Disease Surveillance. Retrieved from https://www.cdc.gov/lyme/

**Social Environment:**
> U.S. Census Bureau. (2024). County Business Patterns. Retrieved from https://www.census.gov/programs-surveys/cbp.html

> Bureau of Alcohol, Tobacco, Firearms and Explosives. (2024). Federal Firearms Licensees. Retrieved from https://www.atf.gov/firearms/listing-federal-firearms-licensees

---

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Status:** Production-ready
**Total Sources Documented:** 12
**Total Variables:** 24 priority county-level variables
