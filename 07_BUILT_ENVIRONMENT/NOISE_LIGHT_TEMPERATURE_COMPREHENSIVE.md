# NOISE POLLUTION, LIGHT POLLUTION & TEMPERATURE EXTREMES
## Comprehensive County-Level Environmental Health Data Sources

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Repository:** GetData
**Category:** Environmental Health - Noise Exposure, Light Pollution, Heat/Cold Stress

---

## Executive Summary

This document provides comprehensive coverage of county-level data sources for three emerging environmental health exposures:

1. **Noise Pollution** - Cardiovascular disease, sleep disturbance, cognitive impairment
2. **Light Pollution** - Circadian rhythm disruption, cancer, metabolic disorders
3. **Temperature Extremes** - Heat stroke, cardiovascular stress, cold-related mortality

All data sources provide county-level coverage or are aggregable to county level, with emphasis on longest available time ranges and most authoritative sources.

**Key Statistics:**
- **Noise Data:** 2014-present (BTS Transportation Noise Map)
- **Light Pollution:** 1992-present (33 years DMSP-VIIRS harmonized time series)
- **Heat/Cold Data:** 1895-present (130+ years NOAA climate records)

---

## PART 1: NOISE POLLUTION

### Health Impacts

**Diseases Linked to Chronic Noise Exposure:**

| Health Outcome | Evidence Strength | Key Mechanism | Threshold |
|----------------|-------------------|---------------|-----------|
| **Cardiovascular Disease** | Strong | Chronic stress, cortisol, sympathetic activation | >55 dB DNL |
| **Hypertension** | Strong | Stress hormones, sleep disturbance | >50 dB DNL |
| **Myocardial Infarction** | Moderate | Inflammation, oxidative stress | >60 dB DNL |
| **Stroke** | Moderate | Hypertension pathway | >60 dB DNL |
| **Sleep Disturbance** | Very Strong | Arousal, fragmentation | >40 dB nighttime |
| **Cognitive Impairment (children)** | Strong | Attention, learning, reading comprehension | >55 dB school |
| **Mental Health** | Moderate | Chronic annoyance, stress | >55 dB DNL |
| **Hearing Loss** | Strong (occupational) | Direct damage | >85 dB continuous |

**Key Terms:**
- **DNL (Day-Night Average Sound Level):** 24-hour average sound level with 10 dB penalty for nighttime noise (10 PM - 7 AM)
- **Lden:** Similar to DNL, European standard with evening penalty
- **LAeq:** Equivalent continuous sound level (A-weighted)

**WHO Guidelines (2018):**
- Road traffic: <53 dB Lden (cardiovascular protection)
- Aircraft: <45 dB Lden
- Rail: <54 dB Lden

---

### Source 1: Bureau of Transportation Statistics - National Transportation Noise Map

**Official Name:** BTS National Transportation Noise Map
**Status:** ✅ ONLY COMPREHENSIVE US TRANSPORTATION NOISE DATABASE (2014 baseline, updates underway)

#### Overview

The BTS National Transportation Noise Map models transportation noise exposure (aviation, highway, rail) for the entire United States at high spatial resolution. This is the only national-scale noise assessment combining all major transportation sources.

#### Coverage

- **Geographic:** United States, state and county level
- **Temporal:** 2014 (baseline); periodic updates planned
- **Spatial Resolution:** Census block level (aggregable to county)
- **Sources Covered:** Aviation (airports), highway traffic, railroad
- **Population Exposure:** Estimates for 308+ million US residents

#### Variables Available

| Variable | Description | Units | Source |
|----------|-------------|-------|--------|
| Aviation DNL | Day-Night Average Sound Level from aircraft | dB DNL | FAA Airport Noise Model |
| Highway DNL | Day-Night Average Sound Level from road traffic | dB DNL | FHWA Traffic Noise Model |
| Rail DNL | Day-Night Average Sound Level from trains | dB DNL | FRA Rail Noise Model |
| Combined Transportation DNL | Total noise from all three sources | dB DNL | Energy-summed |
| Population Exposure by Threshold | Population exposed to >45, >55, >65, >75 dB DNL | Count, % | Census block aggregation |

**Noise Level Categories:**
- **<45 dB:** Quiet (rural areas, low traffic)
- **45-55 dB:** Moderate (suburban, light traffic)
- **55-65 dB:** High (urban, moderate traffic) - *WHO threshold for health effects*
- **65-75 dB:** Very High (near highways, airports)
- **>75 dB:** Severe (airport runways, major highways)

#### Data Access

**Interactive Map:**
- **URL:** https://maps.dot.gov/BTS/NationalTransportationNoiseMap/
- **Features:**
  - View noise levels by location
  - Toggle aviation, highway, rail layers
  - Query population exposure statistics
  - Zoom to county, state, national level
- **Output:** On-screen visualization, summary statistics

**Data Download:**
- **URL:** https://data.bts.gov/stories/s/National-Transportation-Noise-Map/ri89-bhxh/
- **BTS Data Inventory:** Search "National Transportation Noise Map"
- **Format:**
  - Census block-level data (CSV)
  - GIS shapefiles (county, state summaries)
  - Summary statistics by jurisdiction
- **Variables Downloadable:**
  - Block ID, State, County FIPS
  - Aviation DNL, Highway DNL, Rail DNL, Combined DNL
  - Population count, land area

**County-Level Aggregation Example:**
```r
library(tidyverse)

# Read census block-level noise data
noise_blocks <- read_csv("BTS_Transportation_Noise_Blocks.csv")

# Aggregate to county level
county_noise <- noise_blocks %>%
  mutate(COUNTY_FIPS = substr(BLOCK_GEOID, 1, 5)) %>%
  group_by(COUNTY_FIPS, STATE_NAME, COUNTY_NAME) %>%
  summarize(
    # Population-weighted average DNL
    mean_combined_dnl = weighted.mean(COMBINED_DNL, POPULATION, na.rm = TRUE),
    mean_aviation_dnl = weighted.mean(AVIATION_DNL, POPULATION, na.rm = TRUE),
    mean_highway_dnl = weighted.mean(HIGHWAY_DNL, POPULATION, na.rm = TRUE),
    mean_rail_dnl = weighted.mean(RAIL_DNL, POPULATION, na.rm = TRUE),

    # Population exposure counts
    pop_above_55db = sum(POPULATION[COMBINED_DNL >= 55], na.rm = TRUE),
    pop_above_65db = sum(POPULATION[COMBINED_DNL >= 65], na.rm = TRUE),
    pop_above_75db = sum(POPULATION[COMBINED_DNL >= 75], na.rm = TRUE),

    # Percentages
    pct_above_55db = pop_above_55db / sum(POPULATION, na.rm = TRUE) * 100,
    pct_above_65db = pop_above_65db / sum(POPULATION, na.rm = TRUE) * 100,

    total_population = sum(POPULATION, na.rm = TRUE),
    .groups = "drop"
  )

write_csv(county_noise, "county_transportation_noise.csv")
```

#### Data Quality

**Strengths:**
- Only national-scale US transportation noise assessment
- Combines all three major transportation sources (aviation, highway, rail)
- Population exposure estimates included
- Validated modeling methodologies (FAA, FHWA, FRA)
- High spatial resolution (census block)

**Limitations:**
- Modeled data, not direct measurements
- 2014 baseline (10+ years old; traffic volumes, aircraft operations have changed)
- Simplified modeling assumptions (uniform terrain, standard meteorology)
- Does not include:
  - Industrial noise (factories, manufacturing)
  - Construction noise
  - Recreational noise (sports stadiums, concerts)
  - Neighborhood noise (lawnmowers, leaf blowers)
  - Wind turbine noise
- Designed for national/regional analysis, less accurate at hyperlocal level

**Validation:** FAA, FHWA, FRA models validated against ground measurements; typical accuracy ±3 dB

#### Comparison with Ground Truth

**FAA Airport Noise Model:** Used for Part 150 noise studies; validated at 98 airports
**FHWA Traffic Noise Model (TNM):** Validated against roadside noise monitors; correlation r=0.85-0.92
**FRA Rail Noise Model:** Validated against FRA noise measurements

#### Use Cases for County-Level Analysis

1. **Cardiovascular Disease Risk:** Identify high-noise counties for CVD studies
2. **Sleep Disturbance Assessment:** Estimate population exposed to nighttime noise >40 dB
3. **Urban vs. Rural:** Compare noise burden in metropolitan vs. rural counties
4. **Transportation Infrastructure Impact:** Link highway density, airport proximity to noise exposure
5. **Health Disparities:** Examine socioeconomic patterns in noise exposure (environmental justice)

**County-Level Metrics:**
- Mean population-weighted DNL (dB)
- % population exposed to >55 dB (WHO threshold)
- % population exposed to >65 dB (high noise)
- Source breakdown (% noise from aviation, highway, rail)

---

### Source 2: University of Washington - National Transportation Noise Exposure Map

**Official Name:** UW DEOHS National Transportation Noise Exposure Map
**Status:** ✅ RESEARCH-GRADE DATA FOR EPIDEMIOLOGICAL STUDIES (Multi-year average)

#### Overview

The University of Washington Department of Environmental & Occupational Health Sciences developed a refined transportation noise exposure map specifically for population health studies. This dataset is tailored for epidemiological research and provides tract-level estimates aggregable to counties.

#### Coverage

- **Geographic:** Contiguous United States (CONUS), census tract level
- **Temporal:** Multi-year average (specific years depend on traffic data vintage)
- **Spatial Resolution:** Census tracts (~2,500-8,000 people) aggregable to counties
- **Sources:** Highway traffic, aviation, railroad

#### Variables Available

| Variable | Description | Units |
|----------|-------------|-------|
| Transportation Noise (A-weighted 24-hour average) | Continuous outdoor noise level | dB LAeq |
| Highway Traffic Noise | Road traffic component | dB LAeq |
| Aviation Noise | Aircraft component | dB LAeq |
| Railroad Noise | Rail traffic component | dB LAeq |

**Note:** Uses LAeq (equivalent continuous sound level) rather than DNL; LAeq ≈ DNL - 3 dB for typical day-night traffic patterns

#### Data Access

**Primary Access:**
- **URL:** https://deohs.washington.edu/national-transportation-noise-exposure-map
- **Format:**
  - R sf (simple features) data object
  - Shapefiles (census tracts with noise values)
- **Access Method:** Download from UW DEOHS website or contact researchers
- **Use Agreement:** Academic research use (cite publication)

**Citation:**
> Bowe, B., Xie, Y., Yan, Y., & Al-Aly, Z. (2019). Burden of Cause-Specific Mortality Associated With PM2.5 Air Pollution in the United States. *JAMA Network Open*, 2(11), e1915834.
>
> Casey, J. A., Morello-Frosch, R., Mennitt, D. J., Fristrup, K., Ogburn, E. L., & James, P. (2017). Race/Ethnicity, Socioeconomic Status, Residential Segregation, and Spatial Variation in Noise Exposure in the Contiguous United States. *Environmental Health Perspectives*, 125(7), 077017.

**R Code Example:**
```r
library(sf)
library(tidyverse)

# Read UW transportation noise shapefile
noise_tracts <- st_read("UW_Transportation_Noise_Tracts.shp")

# Aggregate to county level (population-weighted)
# Requires tract-level population data from Census
census_pop <- read_csv("tract_population.csv")

county_noise <- noise_tracts %>%
  st_drop_geometry() %>%
  left_join(census_pop, by = c("GEOID" = "tract_fips")) %>%
  mutate(COUNTY_FIPS = substr(GEOID, 1, 5)) %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    mean_noise_laeq = weighted.mean(NOISE_LAEQ, POPULATION, na.rm = TRUE),
    mean_highway_laeq = weighted.mean(HIGHWAY_LAEQ, POPULATION, na.rm = TRUE),
    mean_aviation_laeq = weighted.mean(AVIATION_LAEQ, POPULATION, na.rm = TRUE),
    mean_rail_laeq = weighted.mean(RAIL_LAEQ, POPULATION, na.rm = TRUE),
    .groups = "drop"
  )
```

#### Data Quality

**Strengths:**
- Research-grade data validated for epidemiological studies
- Used in peer-reviewed publications (Environmental Health Perspectives, JAMA Network Open)
- Census tract resolution (finer than county, allows within-county analysis)
- Population exposure weighting

**Limitations:**
- Multi-year average (not annual time series)
- Specific vintage may be older than current traffic/aviation patterns
- LAeq vs. DNL: LAeq does not include nighttime penalty (less conservative for sleep/CVD risk)

**Recommended Use:** Health outcome studies requiring validated noise exposure estimates

#### Use Cases

1. **Cardiovascular Cohort Studies:** Link tract-level noise to CVD incidence
2. **Environmental Justice:** Examine noise disparities by race/ethnicity, income (tract-level demographic data)
3. **Within-County Variation:** Assess urban core vs. suburban noise differences
4. **Hypertension Risk:** Estimate population at risk (>50 dB threshold)

---

### Source 3: FAA Airport Noise Exposure Maps

**Official Name:** FAA Part 150 Airport Noise Compatibility Planning
**Status:** ✅ AIRPORT-SPECIFIC NOISE CONTOURS (Site-by-site, not national compilation)

#### Overview

The Federal Aviation Administration requires commercial airports to conduct noise studies under Part 150 regulations. These studies produce detailed DNL contour maps around airports showing noise exposure zones.

#### Coverage

- **Geographic:** Individual airports (350+ US commercial airports)
- **Temporal:** Varies by airport (studies updated every 5-10 years)
- **Spatial Resolution:** Noise contours (65 dB, 70 dB, 75 dB DNL typically)
- **Affected Area:** Typically 10-20 mile radius around airports

#### Variables Available

- **DNL Contours:** Polygons showing 65, 70, 75 dB DNL exposure zones
- **Aircraft Operations:** Annual operations by aircraft type, time of day
- **Flight Tracks:** Arrival and departure corridors
- **Population Exposure:** Residents within each contour
- **Noise-Compatible Land Use:** Residential, schools incompatible with >65 dB

#### Data Access

**Airport-Specific Access:**
- **Method:** Search "[Airport Name] Part 150 Noise Study" or visit airport website
- **Format:** PDF reports with noise contour maps, GIS shapefiles (varies by airport)
- **Example Airports:**
  - Los Angeles International (LAX): https://www.lawa.org/noise-management
  - Chicago O'Hare (ORD): https://www.flychicago.com/community/noise
  - Seattle-Tacoma (SEA): https://www.portseattle.org/page/aircraft-noise

**National Compilation:**
- **Challenge:** No centralized database of all airport noise contours
- **FAA Noise Portal:** https://www.faa.gov/noise
- **Alternative:** Federal Docket Management System (regulations.gov) - search Part 150 studies

**County-Level Aggregation:**
```r
# Read airport noise contour shapefile
airport_noise <- st_read("LAX_Noise_Contours_2023.shp")

# Intersect with county boundaries
counties <- st_read("county_boundaries.shp")

county_airport_noise <- st_intersection(airport_noise, counties) %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    area_above_65db = sum(st_area(geometry)[DNL >= 65]),
    area_above_70db = sum(st_area(geometry)[DNL >= 70]),
    population_65db = sum(POPULATION[DNL >= 65], na.rm = TRUE),
    .groups = "drop"
  )
```

#### Data Quality

**Strengths:**
- Highest quality airport noise data (detailed modeling, validated)
- Includes actual flight operations data
- Population exposure estimates
- Updated regularly (FAA requirement for major airports)

**Limitations:**
- Airport-by-airport (not national database)
- Access varies (some airports provide GIS, others PDF only)
- Does not cover general aviation airports (<50,000 annual operations)
- County aggregation requires manual GIS processing

#### Use Cases

1. **Airport-Proximate Counties:** Assess noise burden in counties with major airports (Los Angeles, Cook County IL, King County WA)
2. **Childhood Development Studies:** Identify schools within 65 dB contours (learning impairment)
3. **Property Value Impact:** Link noise zones to real estate values
4. **Annoyance/Sleep Studies:** Estimate population exposed to nighttime aircraft noise

---

## PART 2: LIGHT POLLUTION

### Health Impacts

**Diseases Linked to Artificial Light at Night (ALAN):**

| Health Outcome | Evidence Strength | Key Mechanism | Exposure Type |
|----------------|-------------------|---------------|---------------|
| **Breast Cancer** | Strong (IARC Group 2A) | Melatonin suppression, hormone disruption | Shift work, outdoor ALAN |
| **Prostate Cancer** | Moderate | Melatonin suppression | Shift work, outdoor ALAN |
| **Colorectal Cancer** | Emerging | Circadian disruption | Shift work, ALAN |
| **Sleep Disorders** | Very Strong | Circadian rhythm disruption, delayed melatonin onset | Outdoor ALAN, indoor light |
| **Obesity** | Moderate | Circadian disruption, altered metabolism | Late-night light exposure |
| **Type 2 Diabetes** | Moderate | Metabolic dysregulation, insulin resistance | Shift work, ALAN |
| **Depression** | Moderate | Circadian disruption, mood regulation | Chronic ALAN exposure |
| **Cardiovascular Disease** | Emerging | Circadian stress, sleep disruption | Shift work, ALAN |

**Key Mechanisms:**
1. **Melatonin Suppression:** Blue light (460-480 nm) suppresses pineal melatonin production (oncostatic hormone)
2. **Circadian Rhythm Disruption:** Shifted or weakened circadian clock gene expression
3. **Sleep Deprivation:** Reduced sleep quality and duration
4. **Metabolic Dysregulation:** Altered glucose metabolism, leptin/ghrelin (appetite hormones)

**WHO/IARC Classification (2019):** Shift work involving circadian disruption classified as "probably carcinogenic (Group 2A)"

---

### Source 4: VIIRS Day/Night Band (DNB) Nighttime Lights - NASA Black Marble

**Official Name:** NASA Black Marble VNP46 Suite - VIIRS Day/Night Band Nighttime Lights
**Status:** ✅ HIGHEST RESOLUTION, RADIOMETRICALLY CALIBRATED (375m/750m, 2012-present)

#### Overview

NASA's Black Marble product suite provides daily, monthly, and annual nighttime light data from the VIIRS (Visible Infrared Imaging Radiometer Suite) instrument aboard Suomi NPP, NOAA-20, and NOAA-21 satellites. This is the highest quality nighttime light dataset for light pollution and human activity monitoring.

#### Coverage

- **Geographic:** Global, including all US counties
- **Temporal:** 2012-present (Suomi NPP launch), daily composites available
- **Spatial Resolution:**
  - 375 meters (2017-present, highest resolution)
  - 750 meters (2012-2016)
- **Temporal Resolution:** Daily, monthly composites, annual composites
- **Update Frequency:** Daily uploads, monthly/annual products released periodically

#### Variables Available

| Product | Description | Temporal Resolution | Units |
|---------|-------------|---------------------|-------|
| **VNP46A1** | Daily nighttime radiance | Daily | nanoWatts/cm²/sr |
| **VNP46A2** | Monthly nighttime radiance | Monthly | nanoWatts/cm²/sr |
| **VNP46A3** | Annual nighttime radiance | Annual | nanoWatts/cm²/sr |
| **VNP46A4** | Nighttime lights change detection | Annual | Change classification |

**Derived Variables:**
- Radiance (nW/cm²/sr): Brightness of artificial light
- Cloud-free observations: Number of clear observations per pixel per month/year
- Temporal trends: Change in radiance 2012-2024
- Seasonal patterns: Summer vs. winter light levels

**Radiance Interpretation:**
- **0-1 nW/cm²/sr:** Very dark (rural, wilderness)
- **1-10 nW/cm²/sr:** Low light (suburban, small towns)
- **10-50 nW/cm²/sr:** Moderate light (urban areas)
- **50-200 nW/cm²/sr:** High light (urban cores, commercial districts)
- **>200 nW/cm²/sr:** Extreme light (city centers, sports stadiums, major highways)

#### Data Access

**NASA Earthdata:**
- **Portal:** https://www.earthdata.nasa.gov/topics/human-dimensions/nighttime-lights
- **Black Marble Product Suite:** https://blackmarble.gsfc.nasa.gov/
- **Download:**
  - NASA Earthdata Search: https://search.earthdata.nasa.gov/ (search "VNP46")
  - LAADS DAAC: https://ladsweb.modaps.eosdis.nasa.gov/
  - **Requires:** Free NASA Earthdata Login (https://urs.earthdata.nasa.gov/)
- **Format:** HDF5, GeoTIFF (grid tiles)

**Google Earth Engine:**
- **Advantage:** Cloud-based processing, no download required
- **Dataset:** `NOAA/VIIRS/DNB/MONTHLY_V1/VCMSLCFG` (monthly composites)
- **Spatial Aggregation:** Compute county means, medians, sums directly in GEE

**GEE Code Example:**
```javascript
// Google Earth Engine: Calculate county-level annual nighttime lights (2023)

// Load county boundaries
var counties = ee.FeatureCollection("TIGER/2018/Counties");

// Load VIIRS DNB monthly composites for 2023
var viirs = ee.ImageCollection("NOAA/VIIRS/DNB/MONTHLY_V1/VCMSLCFG")
  .filterDate('2023-01-01', '2023-12-31')
  .select('avg_rad');  // Average radiance

// Calculate annual mean radiance
var annual_lights_2023 = viirs.mean();

// Aggregate to county level
var county_lights = annual_lights_2023.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),  // Mean radiance per county
  scale: 750  // 750m resolution
});

// Add sum (total light) and percentiles
county_lights = annual_lights_2023.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean()
    .combine(ee.Reducer.median(), '', true)
    .combine(ee.Reducer.sum(), '', true)
    .combine(ee.Reducer.percentile([90, 95]), '', true),
  scale: 750
});

// Export to CSV
Export.table.toDrive({
  collection: county_lights,
  description: 'County_Nighttime_Lights_2023',
  fileFormat: 'CSV'
});
```

**Direct Python Download (earthaccess library):**
```python
import earthaccess
import rasterio
import geopandas as gpd
import numpy as np

# Authenticate with NASA Earthdata
earthaccess.login()

# Search for VNP46A3 annual product for 2023
results = earthaccess.search_data(
    short_name='VNP46A3',
    temporal=('2023-01-01', '2023-12-31'),
    bounding_box=(-125, 24, -66, 50)  # CONUS
)

# Download
files = earthaccess.download(results, "viirs_nightlights")

# Read HDF5 and extract to county polygons
counties = gpd.read_file("county_boundaries.shp")

# Process raster and extract county means
# (Requires raster processing - rasterio, rasterstats)
```

#### Data Quality

**Strengths:**
- Highest spatial resolution nighttime lights data (375m)
- Radiometrically calibrated (absolute radiance values, not relative like DMSP)
- Daily observations allow temporal analysis (seasonal patterns, event detection)
- Cloud masking and atmospheric correction applied
- Long time series (2012-present, 12+ years)
- Validated against ground measurements

**Limitations:**
- Requires GIS processing to aggregate from pixels to counties
- Large data volumes (daily HDF5 files ~500 MB each)
- Radiance measures light emitted upward; not direct measure of ground-level light exposure
- Does not account for indoor vs. outdoor light exposure
- Satellites observe only cloud-free nights (monthly composites average 15-25 clear observations)

**Validation:** Ground-based light measurements (photometers) show correlation r=0.85-0.95 with VIIRS radiance

#### Use Cases for County-Level Analysis

1. **Breast/Prostate Cancer Risk:** Estimate outdoor light pollution exposure (melatonin suppression)
2. **Sleep Disorder Prevalence:** High-light counties may have more sleep complaints
3. **Urbanization Trends:** Track light growth 2012-2024 (urban sprawl)
4. **Circadian Disruption:** Identify extreme light counties (>50 nW/cm²/sr)
5. **Dark Sky Preservation:** Find low-light counties (astronomical research, wildlife conservation)

**County-Level Metrics:**
- Mean nighttime radiance (nW/cm²/sr)
- Median radiance (central tendency, less affected by urban cores)
- 90th/95th percentile radiance (extreme light areas)
- Total radiance sum (overall light emission)
- % county area with radiance >10 nW/cm²/sr (urbanized)
- Trend: Annual change in radiance 2012-2024 (urbanization rate)

---

### Source 5: Harmonized DMSP-VIIRS Nighttime Lights Dataset

**Official Name:** Harmonized Global Nighttime Light Dataset (DMSP-VIIRS, 1992-2024)
**Status:** ✅ LONGEST TIME SERIES (33 years, 1992-2024)

#### Overview

This dataset harmonizes the DMSP-OLS nighttime lights (1992-2013) and VIIRS DNB (2012-present) to create a consistent long-term time series of global nighttime lights at 1km resolution. Critical for studying trends in urbanization, light pollution, and human activity over three decades.

#### Coverage

- **Geographic:** Global, 1km resolution (aggregable to county)
- **Temporal:** 1992-2024 (33-year time series)
- **Spatial Resolution:** 1km x 1km (~30 arc-seconds)
- **Temporal Resolution:** Annual composites
- **Harmonization:** DMSP and VIIRS calibrated to common scale

#### Variables Available

- **Harmonized Radiance:** Consistent radiance values 1992-2024 (calibrated units)
- **Temporal Trends:** Annual change in light intensity
- **Urbanization Proxy:** Light growth indicates urban expansion
- **Population Proxy:** Nighttime lights correlate with population (r=0.7-0.9)

#### Data Access

**Primary Repository: Figshare**
- **URL:** https://figshare.com/articles/dataset/Harmonization_of_DMSP_and_VIIRS_nighttime_light_data_from_1992-2018_at_the_global_scale/9828827
- **Updated Versions:** Check for extensions beyond 2018 (2024 versions likely published)
- **Format:** GeoTIFF (annual rasters, 1992-2024)
- **Size:** ~500 MB per annual raster
- **License:** CC BY 4.0 (open access)

**Google Earth Engine:**
- **Dataset (DMSP-OLS):** `NOAA/DMSP-OLS/NIGHTTIME_LIGHTS`
- **Dataset (Harmonized):** Search GEE Data Catalog for "harmonized nighttime lights"

**Download and County Aggregation Example:**
```r
library(terra)
library(sf)
library(tidyverse)

# Read county boundaries
counties <- st_read("county_boundaries.shp")

# Read harmonized nighttime lights time series (1992-2024)
ntl_files <- list.files("harmonized_ntl", pattern = "*.tif", full.names = TRUE)

# Function to extract county means for one year
extract_county_lights <- function(raster_file, year) {
  ntl_raster <- rast(raster_file)

  county_values <- extract(
    ntl_raster,
    vect(counties),
    fun = mean,
    na.rm = TRUE,
    bind = TRUE
  ) %>%
    st_as_sf() %>%
    st_drop_geometry() %>%
    mutate(year = year)

  return(county_values)
}

# Extract for all years
years <- 1992:2024
county_ntl_timeseries <- map2_dfr(ntl_files, years, extract_county_lights)

# Calculate trends
county_trends <- county_ntl_timeseries %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    mean_radiance_1992_2000 = mean(radiance[year <= 2000], na.rm = TRUE),
    mean_radiance_2015_2024 = mean(radiance[year >= 2015], na.rm = TRUE),
    radiance_change = mean_radiance_2015_2024 - mean_radiance_1992_2000,
    pct_change = (radiance_change / mean_radiance_1992_2000) * 100,
    .groups = "drop"
  )

write_csv(county_trends, "county_nighttime_lights_trends_1992_2024.csv")
```

#### Data Quality

**Strengths:**
- Longest nighttime lights time series available (33 years)
- Harmonized across sensor transition (DMSP → VIIRS)
- Enables trend analysis (urbanization, light pollution growth)
- 1km resolution suitable for county aggregation
- Validated against DMSP and VIIRS original products

**Limitations:**
- DMSP (1992-2013) lower resolution and radiometric quality than VIIRS
- Harmonization introduces some smoothing (reduces extreme values)
- Not suitable for hyperlocal analysis (<1 km scale)

**Validation:** Harmonized dataset correlates r=0.95+ with original DMSP and VIIRS products

#### Use Cases

1. **Long-Term Cancer Trends:** Examine breast/prostate cancer incidence 1992-2024 vs. light pollution growth
2. **Urbanization Impact:** Counties with rapid light increase (1992 → 2024) vs. stable rural counties
3. **Circadian Disruption Over Time:** Assess whether chronic light exposure (decades) predicts disease better than recent exposure
4. **Before-After Studies:** Pre- and post-urbanization light exposure (e.g., 1995 vs. 2020)

**County-Level Metrics:**
- Mean radiance 1992-2000 (baseline)
- Mean radiance 2015-2024 (current)
- Absolute change (nW/cm²/sr or calibrated units)
- Percent change (% increase in light pollution)
- Trend slope (radiance/year, linear regression 1992-2024)

---

## PART 3: TEMPERATURE EXTREMES (HEAT & COLD)

### Health Impacts

**Heat-Related Health Effects:**

| Health Outcome | Mechanism | At-Risk Populations |
|----------------|-----------|---------------------|
| **Heat Stroke** | Thermoregulatory failure | Elderly, children, outdoor workers |
| **Dehydration** | Fluid loss, electrolyte imbalance | Elderly, kidney disease patients |
| **Cardiovascular Events** | Increased cardiac workload, dehydration | Elderly, CVD patients, hypertension |
| **Kidney Disease** | Dehydration, rhabdomyolysis | Agricultural workers, outdoor laborers |
| **Respiratory Exacerbation** | Ozone formation, air stagnation | Asthma, COPD patients |
| **Mental Health Crisis** | Heat stress, sleep deprivation | Psychiatric patients |
| **Preterm Birth** | Maternal heat stress | Pregnant women |
| **All-Cause Mortality** | Multiple pathways | Elderly, low-income (no AC) |

**Cold-Related Health Effects:**

| Health Outcome | Mechanism | At-Risk Populations |
|----------------|-----------|---------------------|
| **Hypothermia** | Core body temperature drop | Homeless, elderly, rural residents |
| **Frostbite** | Tissue freezing | Outdoor workers, homeless |
| **Cardiovascular Events** | Vasoconstriction, blood pressure spike | Elderly, CVD patients |
| **Respiratory Infections** | Cold air damage to airways | Children, elderly, COPD patients |
| **Falls/Injuries** | Ice, snow | Elderly |

**Key Thresholds:**
- **Heat:** >95°F (35°C), heat index >105°F (extreme heat warning)
- **Cold:** <32°F (0°C), wind chill <-20°F (-29°C) (frostbite risk)
- **Relative Thresholds:** Local 95th/99th percentile temperatures (heat waves), 1st/5th percentile (cold waves)

---

### Source 6: NOAA Urban Heat Island Mapping Campaign

**Official Name:** NOAA Climate Program Office - Urban Heat Island Mapping Campaign
**Status:** ✅ HIGH-RESOLUTION GROUND MEASUREMENTS (2017-present, 105+ communities mapped)

#### Overview

NOAA's Urban Heat Island (UHI) mapping campaign recruits community scientists to collect ground-truth temperature and humidity data on the hottest day of summer. Sensors mounted on vehicles traverse urban areas, capturing fine-scale temperature variations (street level). This is the highest quality hyperlocal heat exposure data available.

#### Coverage

- **Geographic:** Selected counties/cities (105+ communities mapped 2017-2024)
- **Temporal:**
  - Campaign years: 2017-present (annual expansion)
  - Measurement day: Hottest day of summer (typically July/August)
  - Time points: Morning (~6 AM), afternoon (~3 PM), evening (~7 PM)
- **Spatial Resolution:** Street-level (sensors every ~1 km along traversed routes)
- **2024 Participating Counties:** Hennepin & Ramsey (MN), Pierce (WA), +11 other communities

**Total Mapped Communities (2017-2024):**
- 2017-2019: 12 communities
- 2020: 18 communities
- 2021: 16 communities
- 2022: 14 communities
- 2023: 22 communities
- 2024: 23 communities
- **Total: 105+ unique communities**

#### Variables Available

| Variable | Description | Units | Collection Times |
|----------|-------------|-------|------------------|
| Air Temperature | Ambient temperature at sensor height (~1.5 m) | °F / °C | Morning, afternoon, evening |
| Relative Humidity | Moisture content of air | % | Morning, afternoon, evening |
| Heat Index | Apparent temperature (temp + humidity) | °F / °C | Calculated |
| Spatial Variation | Within-city temperature range | °F / °C | Max - min observed |
| Latitude/Longitude | Sensor measurement location | Decimal degrees | Per measurement |

**Typical Heat Island Magnitude:**
- 10-20°F difference between hottest and coolest areas within a city
- Urban cores: 95-105°F
- Green/suburban areas: 85-90°F

#### Data Access

**Primary Portal: Heat.gov**
- **URL:** https://www.heat.gov/
- **2024 Launch:** National Integrated Heat Health Information System
- **Features:**
  - Interactive maps of UHI campaign results
  - Download GIS data (points, interpolated surfaces)
  - Summary reports by community

**NOAA Data Portal:**
- **URL:** https://www.noaa.gov/news-release/noaa-seeks-applications-for-2024-urban-heat-island-initiative
- **Campaign Results:** Published on NOAA CPO website after each campaign
- **Format:**
  - GIS shapefiles (measurement points)
  - GeoTIFF (interpolated temperature surfaces)
  - CSV (raw sensor data with lat/lon/temp/humidity/time)

**Download Example:**
```r
library(sf)
library(tidyverse)

# Read UHI campaign data for a city (example: Minneapolis 2024)
uhi_points <- st_read("Minneapolis_UHI_2024_afternoon.shp")

# Summary statistics
uhi_summary <- uhi_points %>%
  st_drop_geometry() %>%
  summarize(
    mean_temp_f = mean(TEMP_F, na.rm = TRUE),
    min_temp_f = min(TEMP_F, na.rm = TRUE),
    max_temp_f = max(TEMP_F, na.rm = TRUE),
    temp_range = max_temp_f - min_temp_f,
    mean_humidity = mean(HUMIDITY_PCT, na.rm = TRUE),
    mean_heat_index = mean(HEAT_INDEX_F, na.rm = TRUE)
  )

# Spatial analysis: overlay with census tracts for demographics
tracts <- st_read("census_tracts_minneapolis.shp")

tract_heat <- st_join(tracts, uhi_points) %>%
  group_by(TRACT_FIPS) %>%
  summarize(
    mean_temp = mean(TEMP_F, na.rm = TRUE),
    measurements = n(),
    .groups = "drop"
  )

# Link to socioeconomic data (environmental justice)
ej_analysis <- tract_heat %>%
  left_join(census_demographics, by = "TRACT_FIPS") %>%
  mutate(
    high_heat = mean_temp > quantile(mean_temp, 0.75, na.rm = TRUE)
  ) %>%
  group_by(high_heat) %>%
  summarize(
    pct_low_income = mean(BELOW_POVERTY_PCT, na.rm = TRUE),
    pct_minority = mean(MINORITY_PCT, na.rm = TRUE)
  )
```

#### Data Quality

**Strengths:**
- Ground-truth measurements (not modeled or satellite-estimated)
- High spatial resolution (street-level, ~100m-1km)
- Captures extreme heat day (most health-relevant)
- Three time points (morning, afternoon, evening) show diurnal variation
- Community engagement (raises awareness, builds local capacity)
- Peer-reviewed methodology (NOAA/CAPA validated protocol)

**Limitations:**
- Single-day snapshot (not annual or seasonal coverage)
- Limited geographic coverage (105 communities out of 3,143 counties)
- Not all counties mapped (focus on cities with 50,000+ population)
- Inter-annual variability (hottest day varies year-to-year)
- Vehicle-based sampling (biased toward roads, undersamples parks, backyards)

**Validation:** Sensors calibrated pre- and post-campaign; accuracy ±0.5°F

#### County-Level Use Cases

1. **Intra-County Heat Disparities:** Identify hottest neighborhoods for targeted cooling interventions
2. **Environmental Justice:** Link high-heat areas to low-income, minority populations (tree canopy deficits, lack of AC)
3. **Heat-Health Surveillance:** Prioritize areas for heat-related illness monitoring
4. **Urban Planning:** Inform tree planting, cool pavement, cooling center placement
5. **Climate Adaptation:** Baseline data for tracking UHI mitigation efforts

**County-Level Metrics (for mapped counties):**
- Mean county temperature (afternoon measurement)
- Temperature range (max - min within county)
- % county area >95°F (extreme heat)
- % county area with heat index >105°F (danger level)

---

### Source 7: CDC/NOAA HeatRisk System (2024 Launch)

**Official Name:** CDC/NOAA HeatRisk System - Heat and Health Index
**Status:** ✅ NEW 2024 SYSTEM (Real-time heat-health forecasts, county level)

#### Overview

Launched in 2024, HeatRisk is a joint CDC-NOAA system that combines meteorological heat forecasts with health outcome data to provide actionable heat risk assessments. Unlike traditional heat index, HeatRisk accounts for local acclimatization, historical heat-health impacts, and vulnerable populations.

#### Coverage

- **Geographic:** United States, county level
- **Temporal:** 2024-present (system launched spring 2024)
- **Forecast Horizon:** Current day + 7-day outlook
- **Update Frequency:** Daily updates (morning)

#### Variables Available

| Variable | Description | Scale | Meaning |
|----------|-------------|-------|---------|
| HeatRisk Level | Overall heat-health risk | 0-4 | 0=Minimal, 1=Minor, 2=Moderate, 3=Major, 4=Extreme |
| National Weather Service Heat Forecast | Temperature, humidity, heat index | °F, % | Standard meteorological forecast |
| Historical Heat-Health Impact | County-specific heat sensitivity | Relative | Based on past ED visits, hospitalizations |
| Vulnerable Population Flag | High-risk groups present | Binary | Elderly, outdoor workers, homeless |

**HeatRisk Level Definitions:**
- **Level 0 (Minimal):** Little to no heat impact on health
- **Level 1 (Minor):** Sensitive individuals (elderly, chronic illness) at risk
- **Level 2 (Moderate):** General population at risk with prolonged exposure
- **Level 3 (Major):** Anyone at risk; widespread heat-related illness expected
- **Level 4 (Extreme):** Rare, dangerous heat; health emergency likely

#### Data Access

**Real-Time Web Interface:**
- **URL:** Integrated into CDC Environmental Public Health Tracking Network (https://ephtracking.cdc.gov/)
- **Heat.gov Dashboard:** https://www.heat.gov/ (2024 launch)
- **Features:**
  - Interactive map (county-level HeatRisk)
  - 7-day forecast
  - Historical risk days
  - Community resources (cooling centers, hydration tips)

**Data Download (Anticipated):**
- **Format:** CSV, JSON API (details TBD as of 2024 launch)
- **Historical Archive:** Expected to accumulate 2024-present

**Future Data Access Example (Anticipated API):**
```r
library(httr)
library(jsonlite)
library(tidyverse)

# Hypothetical CDC HeatRisk API call
heatrisk_url <- "https://ephtracking.cdc.gov/api/heatrisk"

# Get HeatRisk data for all counties, date range
heatrisk_data <- GET(
  heatrisk_url,
  query = list(
    startDate = "2024-06-01",
    endDate = "2024-08-31",
    geography = "county",
    format = "json"
  )
) %>%
  content("parsed") %>%
  map_dfr(as_tibble)

# Summarize by county (summer 2024)
county_heatrisk_summer <- heatrisk_data %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    days_heatrisk_3_or_4 = sum(HeatRisk_Level >= 3, na.rm = TRUE),  # Major/Extreme
    days_heatrisk_2_plus = sum(HeatRisk_Level >= 2, na.rm = TRUE),  # Moderate+
    max_heatrisk = max(HeatRisk_Level, na.rm = TRUE),
    .groups = "drop"
  )
```

#### Data Quality

**Strengths:**
- Combines meteorology and health outcomes (more actionable than heat index alone)
- County-specific calibration (accounts for local acclimatization)
- Real-time forecasts (7-day outlook for public health planning)
- Validated against ED visits, hospitalizations
- Partnership between CDC (health) and NOAA (meteorology)

**Limitations:**
- New system (launched 2024, limited historical data)
- Forecast accuracy decreases beyond 3-day window
- Relies on historical heat-health relationships (may not capture future extreme events)

#### Use Cases

1. **Real-Time Surveillance:** Daily monitoring of heat risk for emergency preparedness
2. **Retrospective Analysis (2024+):** Count high-risk days per county per summer
3. **Vulnerable Population Targeting:** Identify counties with frequent Level 3/4 events
4. **Climate Adaptation Planning:** Track changes in heat risk days over time (2024-2030+)

**County-Level Metrics (Summer Season):**
- Days with HeatRisk ≥3 (Major/Extreme)
- Days with HeatRisk ≥2 (Moderate+)
- Maximum HeatRisk level reached
- % summer days with elevated risk

---

### Source 8: NOAA National Centers for Environmental Information (NCEI) - Climate Data

**Official Name:** NOAA NCEI Climate Data Online (CDO) / nClimDiv County-Level Data
**Status:** ✅ LONGEST CLIMATE RECORD (1895-present, 130+ years!)

#### Overview

NOAA NCEI maintains the longest continuous climate records for the United States, including county-level temperature data through the nClimDiv (Climate Divisional) dataset. This provides monthly temperature normals, extremes, and degree days for all US counties from 1895-present.

#### Coverage

- **Geographic:** United States, climate divisions (5-10 per state) and county estimates
- **Temporal:** 1895-present (130+ years!)
- **Temporal Resolution:** Monthly, seasonal, annual
- **Update Frequency:** Monthly (1-month lag)

#### Variables Available

| Variable | Description | Units | Temporal Aggregation |
|----------|-------------|-------|----------------------|
| Mean Temperature | Monthly mean temp | °F | Monthly, annual |
| Maximum Temperature | Monthly mean of daily highs | °F | Monthly, annual |
| Minimum Temperature | Monthly mean of daily lows | °F | Monthly, annual |
| Heating Degree Days (HDD) | Cumulative heating demand (base 65°F) | Degree-days | Monthly, annual |
| Cooling Degree Days (CDD) | Cumulative cooling demand (base 65°F) | Degree-days | Monthly, annual |

**Derived Extreme Temperature Metrics (from daily data):**
- Days with Tmax >90°F, >95°F, >100°F (extreme heat days)
- Days with Tmin <32°F, <20°F, <0°F (extreme cold days)
- Heat waves: ≥3 consecutive days >95°F (or local 95th percentile)
- Cold waves: ≥3 consecutive days <20°F (or local 5th percentile)

#### Data Access

**Method 1: Climate Data Online (CDO) Web Interface**
- **URL:** https://www.ncdc.noaa.gov/cdo-web/
- **Search:** By location (county, state), date range, dataset
- **Datasets:**
  - **Daily Summaries (GHCND):** Station-level daily Tmax, Tmin, precipitation
  - **Monthly Summaries (GSOM):** Station monthly aggregates
  - **nClimDiv:** County/division monthly climate data
- **Output:** CSV, JSON
- **Limit:** 10,000 records per request

**Method 2: NOAA NCEI API**
- **API Documentation:** https://www.ncdc.noaa.gov/cdo-web/webservices/v2
- **Authentication:** Free API token (https://www.ncdc.noaa.gov/cdo-web/token)
- **Endpoints:**
  - `/datasets`: List available datasets
  - `/locations`: Search counties
  - `/data`: Query temperature data by location, date
- **Format:** JSON

**API Example:**
```r
library(httr)
library(jsonlite)
library(tidyverse)

# NOAA NCEI API token (register at link above)
noaa_token <- "YOUR_API_TOKEN"

# Get temperature data for a county (nClimDiv dataset)
# County FIPS: 06037 (Los Angeles County, CA)
county_fips <- "06037"

# Query nClimDiv monthly temperature for 2023
noaa_url <- "https://www.ncei.noaa.gov/cdo-web/api/v2/data"

temp_data <- GET(
  noaa_url,
  query = list(
    datasetid = "NORMAL_MLY",  # Monthly normals
    locationid = paste0("FIPS:", county_fips),
    startdate = "2023-01-01",
    enddate = "2023-12-31",
    datatypeid = "MLY-TAVG-NORMAL",  # Monthly average temperature
    limit = 1000
  ),
  add_headers(token = noaa_token)
) %>%
  content("parsed")

# Extract and summarize
county_temp <- temp_data$results %>%
  map_dfr(as_tibble) %>%
  mutate(
    temp_f = value / 10,  # NOAA reports in tenths of degrees
    month = lubridate::month(date)
  )

annual_mean <- mean(county_temp$temp_f)
```

**Method 3: nClimDiv Direct Download**
- **URL:** https://www.ncei.noaa.gov/access/metadata/landing-page/bin/iso?id=gov.noaa.ncdc:C00005
- **Download:** Bulk files (all counties, all years)
- **Format:** Fixed-width text, CSV
- **Size:** ~50 MB (all data 1895-present)

**R Code: Calculate Extreme Heat Days from Daily Data**
```r
library(rnoaa)
library(tidyverse)

# Use rnoaa package to access GHCND (daily) data
# Requires NOAA API token
options(noaakey = "YOUR_API_TOKEN")

# Find weather stations in a county
# (Requires county boundary, ~10 km buffer around centroid)
stations <- ghcnd_stations() %>%
  filter(state == "CA") %>%
  # Add county assignment logic (spatial join, or use station metadata)
  filter(county_name == "Los Angeles")

# Get daily temperature data for a station, 2024
station_id <- "USC00045114"  # Example station
daily_temp <- ghcnd_search(
  stationid = station_id,
  var = c("tmax", "tmin"),
  date_min = "2024-01-01",
  date_max = "2024-12-31"
)$tmax  # Access tmax data

# Calculate extreme heat days
extreme_heat_days <- daily_temp %>%
  mutate(
    tmax_f = tmax / 10 * 9/5 + 32,  # Convert tenths of °C to °F
    extreme_heat_95 = tmax_f >= 95,
    extreme_heat_100 = tmax_f >= 100
  ) %>%
  summarize(
    days_above_95f = sum(extreme_heat_95, na.rm = TRUE),
    days_above_100f = sum(extreme_heat_100, na.rm = TRUE)
  )

# Aggregate multiple stations to county level (spatial average)
```

#### Data Quality

**Strengths:**
- Longest continuous climate record in US (1895-present, 130 years!)
- Quality-controlled (NOAA QC procedures)
- Monthly updates (near-real-time)
- nClimDiv provides county estimates (interpolated from stations)
- Heating/cooling degree days useful for heat stress assessment

**Limitations:**
- nClimDiv: Spatial interpolation (not direct county measurements; based on climate divisions)
- Station coverage varies (rural counties may have fewer stations)
- Extreme heat/cold day counts require daily data (station-level, not pre-aggregated to counties)
- Historical data (pre-1950) may have fewer observations

**Recommended Use:**
- **nClimDiv:** County monthly/annual temperature means, degree days
- **GHCND Daily:** Calculate extreme heat/cold days from station data, aggregate to county

#### Use Cases

1. **Long-Term Heat Trends:** Examine county temperature change 1895-2024 (climate warming)
2. **Extreme Heat Frequency:** Count days >95°F per year, track increase over decades
3. **Cardiovascular Disease Risk:** Link cooling degree days (CDD) to CVD hospitalization
4. **Heat Wave Definition:** Calculate local 95th percentile temperature (acclimatization)
5. **Cold Exposure:** Track extreme cold days, link to hypothermia, flu season

**County-Level Metrics:**
- Annual mean temperature (°F)
- Summer mean temperature (June-August)
- Days with Tmax ≥95°F (extreme heat days)
- Days with Tmax ≥100°F (severe heat days)
- Cooling degree days (annual sum)
- Heat waves (≥3 consecutive days ≥95°F or local 95th percentile)
- Temperature trend (°F/decade, 1980-2024)

---

## Data Integration and Analysis Strategies

### Recommended County-Level Variables to Collect

#### Noise Pollution (4 variables)
1. **Mean population-weighted transportation DNL (dB)** - BTS Transportation Noise Map, 2014
2. **% population exposed to >55 dB DNL** - BTS, 2014 (WHO cardiovascular threshold)
3. **% population exposed to >65 dB DNL** - BTS, 2014 (high noise)
4. **Dominant noise source** - BTS, 2014 (aviation/highway/rail)

#### Light Pollution (4 variables)
1. **Mean nighttime radiance (nW/cm²/sr)** - VIIRS DNB, annual 2023 (or most recent)
2. **Median nighttime radiance** - VIIRS DNB, 2023 (less sensitive to urban core outliers)
3. **Light pollution trend (radiance change/year)** - Harmonized DMSP-VIIRS, 1992-2024
4. **% county area with radiance >10 nW/cm²/sr** - VIIRS DNB, 2023 (urbanized areas)

#### Heat Exposure (6 variables)
1. **Annual mean temperature (°F)** - NOAA NCEI nClimDiv, 2024
2. **Days with Tmax ≥95°F (annual)** - NOAA GHCND daily (station → county), 2024
3. **Days with Tmax ≥100°F (annual)** - NOAA GHCND daily, 2024
4. **Cooling degree days (annual)** - NOAA NCEI nClimDiv, 2024
5. **Summer mean temperature (June-Aug)** - NOAA NCEI, 2024
6. **Days with HeatRisk ≥3 (Major/Extreme)** - CDC/NOAA HeatRisk, summer 2024 (future: 2025+)

#### Cold Exposure (3 variables, optional)
1. **Days with Tmin <32°F (annual)** - NOAA GHCND daily, 2024 (freezing days)
2. **Days with Tmin <20°F (annual)** - NOAA GHCND daily, 2024 (extreme cold)
3. **Heating degree days (annual)** - NOAA NCEI nClimDiv, 2024

**Total Priority Variables: 17 (or 20 with cold exposure)**

---

## Data Limitations and Quality Considerations

### Noise Pollution
**Limitation:** BTS map is 2014 data (10 years old); traffic volumes, aircraft operations have changed
**Recommendation:** Use as baseline; note that current noise may be higher in growing urban areas

### Light Pollution
**Limitation:** Satellite radiance measures light emitted upward; does not directly measure ground-level light exposure or indoor light
**Recommendation:** Use as proxy for outdoor artificial light at night (ALAN); combine with urbanicity for indoor light inference

### Heat/Cold Exposure
**Limitation:** Station-based temperature may not capture urban heat island within counties (need UHI campaign data)
**Recommendation:** Use NOAA NCEI for county averages; supplement with UHI campaign data where available (105 communities)

---

## Related Data Sources (Already Documented)

1. **Climate Extremes (Storms, Floods, Tornadoes):** NOAA Storm Events - See NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md
2. **Land Cover (Urban vs. Rural):** NLCD - See NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md

---

## Update Schedule

| Data Source | Update Frequency | Expected Next Update |
|-------------|------------------|----------------------|
| BTS Transportation Noise Map | Periodic | TBD (check BTS website) |
| VIIRS DNB Nighttime Lights | Daily/Monthly/Annual | Ongoing (check NASA) |
| Harmonized DMSP-VIIRS | Annual | 2025 data (late 2025/early 2026) |
| NOAA UHI Campaign | Annual | Summer 2025 campaigns |
| CDC/NOAA HeatRisk | Daily | Ongoing (2024+) |
| NOAA NCEI Climate Data | Monthly | Every month (1-month lag) |

---

## API Keys and Access Requirements

**Required (Free):**
- NOAA NCEI API Token: https://www.ncdc.noaa.gov/cdo-web/token
- NASA Earthdata Login: https://urs.earthdata.nasa.gov/ (for VIIRS DNB direct download)

**No API Key Required:**
- BTS Transportation Noise Map (public web map, data download)
- Google Earth Engine (requires Google account, no NASA key needed for VIIRS in GEE)
- NOAA UHI Campaign data (public download)
- CDC/NOAA HeatRisk (public web interface)

---

## Citation

**Noise:**
> Bureau of Transportation Statistics. (2024). National Transportation Noise Map. Retrieved from https://www.bts.gov/geospatial/national-transportation-noise-map

**Light Pollution:**
> NASA Black Marble. (2024). VIIRS Day/Night Band Nighttime Lights. Retrieved from https://blackmarble.gsfc.nasa.gov/

**Heat/Cold:**
> NOAA National Centers for Environmental Information. (2024). Climate Data Online. Retrieved from https://www.ncdc.noaa.gov/cdo-web/

> CDC/NOAA. (2024). HeatRisk System. Retrieved from https://www.heat.gov/

---

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Status:** Production-ready
**Total Sources Documented:** 8
**Total Variables:** 17-20 priority county-level variables
