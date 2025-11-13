# Comprehensive Documentation: Wildfire Smoke, Traffic Exposure, Walkability, and Hazardous Waste Sites
## US County-Level Environmental Exposure Data Sources

**Last Updated:** November 12, 2025
**Status:** NEW - Gap Analysis Phase 2 Complete
**Priority:** HIGH - Critical disease associations (respiratory, cardiovascular, cancer, metabolic)

---

## TABLE OF CONTENTS

1. [Overview](#overview)
2. [NOAA HMS Wildfire Smoke Plumes](#1-noaa-hms-wildfire-smoke-plumes)
3. [EPA Smart Location Database - Walkability Index](#2-epa-smart-location-database-walkability-index)
4. [FHWA HPMS Traffic Volumes](#3-fhwa-hpms-traffic-volumes)
5. [EPA RCRAInfo Hazardous Waste Sites](#4-epa-rcrainfo-hazardous-waste-sites)
6. [EPA LMOP Landfills](#5-epa-lmop-landfills)
7. [Integration & Use Cases](#integration--use-cases)
8. [Priority Variables Summary](#priority-variables-summary)

---

## OVERVIEW

This document provides comprehensive documentation for **5 critical environmental exposure data sources** that fill major gaps in county-level health observatory data:

| Source | Disease Relevance | Coverage | Years | Priority |
|--------|------------------|----------|-------|----------|
| **NOAA HMS Wildfire Smoke** | Respiratory, CVD, all-cause mortality, pregnancy | All counties | 2005-present (daily) | ⭐⭐⭐⭐⭐ |
| **EPA Smart Location Database** | CVD, diabetes, obesity, mental health | All counties | 2019 | ⭐⭐⭐⭐⭐ |
| **FHWA HPMS Traffic Volumes** | Respiratory, CVD, injuries, noise | All counties | 1980s-present | ⭐⭐⭐⭐⭐ |
| **EPA RCRAInfo** | Cancer, birth defects, respiratory | All counties | 1980s-present | ⭐⭐⭐⭐ |
| **EPA LMOP Landfills** | Respiratory, cancer, birth defects | All counties | Current + historical | ⭐⭐⭐⭐ |

**Key Gap Filled:** These sources provide **exposure** data (smoke days, traffic volume, walkability metrics, hazardous waste proximity) that complement existing **emissions** and **health outcomes** data.

**Total New Variables:** ~200 priority variables across 5 sources

---

## 1. NOAA HMS WILDFIRE SMOKE PLUMES

### Overview

**What It Is:** Daily smoke plume polygons from satellite imagery analysis by NOAA analysts
**Disease Relevance:** Respiratory disease (asthma exacerbations, COPD), cardiovascular mortality, all-cause mortality, pregnancy outcomes (preterm birth, low birth weight)
**Evidence Strength:** **VERY STRONG** - Multiple studies link smoke days to hospitalizations, ED visits, mortality

**Critical Gap Filled:** Existing GetData repository has wildfire **emissions** from NEI, but not smoke **exposure** plumes that affect populations hundreds of miles downwind.

### Data Availability

**Coverage:** Continental US (CONUS), all 3,143 counties
**Temporal Coverage:** **2005-present** (20 years daily data)
**Update Frequency:** **Daily** (processed same-day or next-day)
**Spatial Resolution:** Smoke plume polygons (variable size, typically 50-500 km diameter)
**Data Format:** Shapefiles (daily KML, KMZ), Text files (centroids)

### Variables Available

#### Raw Data (Daily):
1. **Smoke plume polygons** - Geographic boundaries of visible smoke
2. **Smoke density** - Qualitative: Light, Medium, Heavy
3. **Satellite source** - GOES-East, GOES-West, Terra, Aqua, Suomi-NPP
4. **Analysis time** - Date/time of smoke observation

#### Derived County-Level Variables (Annual Aggregation):
1. **Smoke days per year** - Count of days with any smoke coverage
2. **Light smoke days** - Days with light density smoke
3. **Medium smoke days** - Days with medium density smoke
4. **Heavy smoke days** - Days with heavy density smoke
5. **Population-weighted smoke days** - Weighted by % county area covered
6. **Smoke season length** - First to last smoke day
7. **Maximum consecutive smoke days** - Longest continuous smoke event
8. **Smoke frequency** - % of year with smoke present
9. **Heavy smoke frequency** - % of year with heavy smoke
10. **Smoke-free days** - Days without any smoke coverage
11. **Summer smoke days** - June-September smoke days (peak wildfire season)
12. **Annual smoke coverage** - Sum of (% county covered × smoke days)

### Access Methods

#### Primary Source:
**Website:** NOAA Office of Satellite and Product Operations (OSPO)
**URL:** https://www.ospo.noaa.gov/products/land/hms.html
**Historical Archive:** https://satepsanone.nesdis.noaa.gov/pub/FIRE/HMS/

#### Data Formats Available:
- **Shapefiles (GIS):** Daily smoke polygons with attributes
- **KML/KMZ:** Google Earth-compatible daily smoke plumes
- **Text files:** Centroids of fire locations (less useful for smoke area)
- **GeoJSON:** Available via NOAA API (experimental)

#### Download Methods:

**Method 1: Manual Daily Downloads**
```bash
# Download daily HMS shapefile (example: November 12, 2024)
wget https://satepsanone.nesdis.noaa.gov/pub/FIRE/HMS/GIS/2024/11/hms_smoke20241112.zip
unzip hms_smoke20241112.zip
```

**Method 2: Bulk Historical Download (Preferred for Research)**
```bash
# Download all 2023 smoke shapefiles
for month in {01..12}; do
  for day in {01..31}; do
    wget -nc https://satepsanone.nesdis.noaa.gov/pub/FIRE/HMS/GIS/2023/${month}/hms_smoke2023${month}${day}.zip
  done
done
```

**Method 3: R Package (Recommended)**
```r
# Install HMS package (if available) or use manual approach
# No official R package exists as of 2024, manual processing required

library(sf)
library(tidyverse)
library(lubridate)

# Read daily HMS smoke shapefile
smoke_20241112 <- st_read("hms_smoke20241112.shp")

# Examine attributes
head(smoke_20241112)
# Typical fields: Density (Light/Medium/Heavy), Start (YYYYMMDDHHMM), End, Satellite

# Read US counties shapefile
counties <- st_read("cb_2020_us_county_500k.shp") # Census Bureau TIGER

# Calculate smoke coverage by county for single day
county_smoke <- st_intersection(counties, smoke_20241112) %>%
  mutate(smoke_area = st_area(.)) %>%
  group_by(GEOID, NAME, Density) %>%
  summarize(
    smoke_area_km2 = sum(as.numeric(smoke_area) / 1e6),
    .groups = "drop"
  )

# Join back to full county list
counties_full <- counties %>%
  st_drop_geometry() %>%
  left_join(county_smoke, by = c("GEOID", "NAME")) %>%
  mutate(
    date = as.Date("2024-11-12"),
    smoke_present = !is.na(smoke_area_km2),
    smoke_density = replace_na(Density, "None")
  )

print(counties_full)
```

**Method 4: Annual County Aggregation Workflow**
```r
library(sf)
library(tidyverse)
library(lubridate)

# Function to process single day
process_hms_day <- function(date, counties_sf) {

  date_str <- format(date, "%Y%m%d")
  url <- sprintf("https://satepsanone.nesdis.noaa.gov/pub/FIRE/HMS/GIS/%s/%s/hms_smoke%s.zip",
                 year(date), sprintf("%02d", month(date)), date_str)

  # Download and unzip
  temp_zip <- tempfile(fileext = ".zip")
  temp_dir <- tempdir()

  tryCatch({
    download.file(url, temp_zip, quiet = TRUE)
    unzip(temp_zip, exdir = temp_dir)

    # Read shapefile
    shp_file <- list.files(temp_dir, pattern = paste0("hms_smoke", date_str, ".shp$"), full.names = TRUE)

    if (length(shp_file) == 0) {
      # No smoke this day
      return(data.frame(
        GEOID = counties_sf$GEOID,
        date = date,
        smoke_present = FALSE,
        density = "None"
      ))
    }

    smoke_sf <- st_read(shp_file, quiet = TRUE)

    # Ensure same CRS
    smoke_sf <- st_transform(smoke_sf, st_crs(counties_sf))

    # Intersect with counties
    county_smoke <- st_intersection(counties_sf, smoke_sf) %>%
      mutate(smoke_area = st_area(.)) %>%
      group_by(GEOID, Density) %>%
      summarize(
        smoke_area_km2 = sum(as.numeric(smoke_area) / 1e6),
        .groups = "drop"
      )

    # Join back
    result <- counties_sf %>%
      st_drop_geometry() %>%
      left_join(county_smoke, by = "GEOID") %>%
      mutate(
        date = date,
        smoke_present = !is.na(smoke_area_km2),
        density = replace_na(Density, "None")
      ) %>%
      select(GEOID, date, smoke_present, density, smoke_area_km2)

    return(result)

  }, error = function(e) {
    # No data for this day
    return(data.frame(
      GEOID = counties_sf$GEOID,
      date = date,
      smoke_present = FALSE,
      density = "None"
    ))
  })
}

# Process entire year
counties <- st_read("cb_2020_us_county_500k.shp")

dates_2023 <- seq(as.Date("2023-01-01"), as.Date("2023-12-31"), by = "day")

smoke_2023_daily <- map_dfr(dates_2023, ~process_hms_day(.x, counties))

# Calculate annual county metrics
smoke_2023_annual <- smoke_2023_daily %>%
  group_by(GEOID) %>%
  summarize(
    smoke_days_total = sum(smoke_present),
    smoke_days_light = sum(density == "Light"),
    smoke_days_medium = sum(density == "Medium"),
    smoke_days_heavy = sum(density == "Heavy"),
    smoke_pct_year = mean(smoke_present) * 100,
    max_consecutive_smoke = max(rle(smoke_present)$lengths[rle(smoke_present)$values]),
    first_smoke_day = min(date[smoke_present], na.rm = TRUE),
    last_smoke_day = max(date[smoke_present], na.rm = TRUE),
    smoke_season_length = as.numeric(last_smoke_day - first_smoke_day),
    .groups = "drop"
  )

write_csv(smoke_2023_annual, "hms_smoke_2023_county_annual.csv")
```

### Data Quality & Limitations

**Strengths:**
- ✅ Daily temporal resolution (20 years of daily data!)
- ✅ Human analyst quality control (not purely automated)
- ✅ Multiple satellite sources (GOES, MODIS, VIIRS)
- ✅ National coverage (all counties)
- ✅ Free and publicly available
- ✅ Near-real-time updates (same-day or next-day)

**Limitations:**
- ⚠️ **Qualitative smoke density** (Light/Medium/Heavy, not quantitative PM2.5)
- ⚠️ **Visible smoke only** (cloud cover may obscure smoke)
- ⚠️ **No vertical resolution** (smoke plume height unknown - may be aloft, not at surface)
- ⚠️ **Subjective density classification** (analyst judgment, some variability)
- ⚠️ **Large plume polygons** (typically 50-500 km, less precise than monitor PM2.5)
- ⚠️ **Processing required** (daily shapefiles must be aggregated to county × year)

**Validation:**
- HMS smoke plumes correlate well with surface PM2.5 monitors (r = 0.6-0.8 in wildfire-affected regions)
- Heavy smoke days typically correspond to PM2.5 >100 μg/m³ (Unhealthy)
- Light smoke days typically correspond to PM2.5 20-55 μg/m³ (Moderate)

**Use with Caution:**
- Smoke density is qualitative, not quantitative PM2.5 concentration
- Some smoke plumes are aloft (not reaching surface) - HMS doesn't distinguish
- For quantitative PM2.5, use EPA AQS monitors or satellite AOD (though fewer locations)

### Disease Associations (Evidence Summary)

**Respiratory Disease:**
- Asthma ED visits: +10% per smoke day (Rappold et al. 2011 EHP)
- COPD hospitalizations: +7% per heavy smoke day (Gan et al. 2020 ATS)
- Respiratory infections: Associated with smoke exposure in children (Haikerwal et al. 2015)

**Cardiovascular Disease:**
- CVD mortality: +5% per 10 μg/m³ PM2.5 from wildfire smoke (Aguilera et al. 2021 JAHA)
- Cardiac arrest: +70% during major smoke events (Jones et al. 2020 Journal of Exposure Science)

**Pregnancy Outcomes:**
- Preterm birth: OR 1.05-1.19 for smoke exposure during pregnancy (Abdo et al. 2019 Environ Res)
- Low birth weight: -7g per 10 μg/m³ PM2.5 wildfire smoke (Heft-Neal et al. 2022 Nature)

**All-Cause Mortality:**
- +1-2% mortality per heavy smoke day (Borchers-Arriagada et al. 2020 IJE)
- 2020 wildfires: Estimated 19,000-52,000 excess deaths in Western US (Aguilera et al. 2021)

### Use Cases for County-Level Analysis

1. **Time-series health impacts:** Correlate smoke days with daily/weekly hospitalizations
2. **Wildfire preparedness:** Identify counties with increasing smoke day trends
3. **Vulnerable populations:** Cross-reference with CDC SVI, age 65+, asthma prevalence
4. **Economic impacts:** Smoke days × lost work days, tourism impacts
5. **Climate change adaptation:** Track smoke season expansion over 2005-2024

### Priority Variables for Collection

**Top 10 HMS variables (county × year):**
1. Total smoke days per year
2. Heavy smoke days per year
3. Light smoke days per year
4. Medium smoke days per year
5. % of year with smoke present
6. Maximum consecutive smoke days
7. Summer smoke days (June-Sept)
8. Smoke season length (days between first and last smoke)
9. Heavy smoke season length
10. Population-weighted smoke exposure days

---

## 2. EPA SMART LOCATION DATABASE - WALKABILITY INDEX

### Overview

**What It Is:** Comprehensive built environment database with 90+ indicators including National Walkability Index
**Disease Relevance:** Cardiovascular disease, diabetes, obesity, mental health, all-cause mortality
**Evidence Strength:** **VERY STRONG** - Hundreds of studies link walkability to physical activity and health outcomes

**Critical Gap Filled:** Existing GetData repository has basic walkability from County Health Rankings. SLD provides comprehensive 90+ indicators of built environment.

### Data Availability

**Coverage:** All census block groups (aggregable to county), all 3,143 counties
**Temporal Coverage:** **Version 3.0 (2019)** - based on 2017-2019 ACS data, released 2021
**Update Frequency:** Periodic (v1.0: 2011; v2.0: 2013; v3.0: 2019; v4.0 expected ~2026)
**Spatial Resolution:** Census block groups (primary), aggregable to tract, county, metro
**Data Format:** File geodatabase (.gdb), CSV, shapefiles

### Variables Available (90+ Total)

The Smart Location Database provides **90+ variables** organized into themes:

#### **National Walkability Index (Primary Composite Measure)**
1. **NatWalkInd** - National Walkability Index (0-20 scale, higher = more walkable)
   - Based on 4 D variables: Density, Diversity, Design, Destination accessibility
   - Population-weighted composite

#### **D1: DENSITY Variables (10 variables)**
2. **D1A** - Gross population density (population per acre)
3. **D1B** - Gross employment density (jobs per acre)
4. **D1C** - Gross activity density (population + jobs per acre)
5. **D1C5_RET** - Retail employment density
6. **D1C5_OFF** - Office employment density
7. **D1C5_IND** - Industrial employment density
8. **D1C5_SVC** - Service employment density
9. **D1C5_ENT** - Entertainment employment density
10. **D1C5_ED** - Education employment density
11. **D1C5_HLTH** - Healthcare employment density

#### **D2: DIVERSITY Variables (15 variables)**
12. **D2A_EPHHM** - Employment and household entropy (0-1, higher = more mixed use)
13. **D2A_JPHH** - Jobs-to-household balance ratio
14. **D2B_E5MIX** - 5-tier employment entropy (retail, office, industrial, service, entertainment)
15. **D2C_TRPMX1** - Jobs within 45-min auto commute mix
16. **D2C_TRPMX2** - Jobs within 45-min transit commute mix
17. **D2A_WRKEMP** - Workers per household (proxy for employment accessibility)
18. **D2R_JOBPOP** - Employment to population ratio
19. **D2R_WRKEMP** - Workers to employment ratio
20. **D2A_EPHHM** - Entropy of employment by sector
21-26. **D2B sector employment %** - % employment in retail, office, industrial, service, entertainment, education

#### **D3: DESIGN Variables (20 variables)**
27. **D3A** - Total road network density (centerline miles/sq mi)
28. **D3AAO** - Auto-oriented road network density
29. **D3AMM** - Pedestrian-oriented road network density
30. **D3B** - Street intersection density (intersections/sq mi)
31. **D3BAO** - Auto-oriented intersection density
32. **D3BMM3** - Pedestrian-oriented 3-way intersection density
33. **D3BMM4** - Pedestrian-oriented 4-way intersection density
34. **D3BPO3** - % 3-way intersections
35. **D3BPO4** - % 4-way intersections (highly walkable)
36-46. **Link-node ratio, cul-de-sacs, grid patterns, block size metrics** (11 variables)

#### **D4: DESTINATION ACCESSIBILITY Variables (25 variables)**
47. **D4A** - Distance from population-weighted centroid to nearest transit stop (meters)
48. **D4B** - Aggregate transit frequency (weekday trips within 0.25 mi)
49. **D4C** - Aggregate transit frequency (weekend trips within 0.25 mi)
50. **D4D** - Aggregate transit frequency (combined weekday + weekend)
51. **D4E** - Density of transit stops within 0.25 mi
52. **D5AR** - Jobs within 45-min auto travel time
53. **D5AE** - Employment within 45-min auto travel time
54. **D5BR** - Jobs within 45-min transit travel time
55. **D5BE** - Employment within 45-min transit travel time
56. **D5CR** - Jobs accessible by low-speed auto (<20mph)
57. **D5CE** - Employment accessible by low-speed auto
58. **D5DR** - Jobs accessible by walk/bike (2 mi)
59. **D5DE** - Employment accessible by walk/bike (2 mi)
60-71. **Distance to major destinations:** Distance to nearest park, school, grocery, pharmacy, hospital, library, etc. (12 variables)

#### **D5: DISTANCE TO TRANSIT Variables (10 variables)**
72. **D5ar_ret** - Retail jobs within 45-min auto
73. **D5ae_ret** - Retail employment within 45-min auto
74. **D5br_ret** - Retail jobs within 45-min transit
75. **D5be_ret** - Retail employment within 45-min transit
76-81. **Distance quantiles** - % population within 0.25 mi, 0.5 mi, 1 mi of transit (6 variables)

#### **DEMOGRAPHICS & CONTEXT Variables (10 variables)**
82. **TotPop** - Total population (2019 ACS)
83. **HH** - Total households
84. **Emptot** - Total employment
85. **CBSA** - Core-Based Statistical Area code
86. **CBSA_Name** - Metro area name
87. **GEOID10** - Census block group FIPS code
88. **GEOID20** - 2020 Census block group (for updates)
89. **AutoOwn0, AutoOwn1, AutoOwn2p** - Households with 0, 1, 2+ vehicles

### Access Methods

#### Primary Source:
**Website:** EPA Smart Growth Program
**URL:** https://www.epa.gov/smartgrowth/smart-location-mapping
**Direct Download:** https://edg.epa.gov/data/Public/OP/SLD/SmartLocationDb.gdb.zip (v3.0, 1.2 GB)

#### Data Formats Available:
- **File Geodatabase (.gdb):** Primary format, all 90+ variables
- **CSV:** Available by request or manual export from geodatabase
- **Shapefiles:** Can be exported from geodatabase
- **ArcGIS Online:** Interactive web map viewer

#### Download & Processing

**Method 1: Direct Download and Load**
```r
library(sf)
library(tidyverse)

# Download SLD v3.0 (1.2 GB file geodatabase)
download.file(
  "https://edg.epa.gov/data/Public/OP/SLD/SmartLocationDb.gdb.zip",
  destfile = "SmartLocationDb.gdb.zip"
)

unzip("SmartLocationDb.gdb.zip")

# Read file geodatabase (requires sf package with GDAL)
sld_bg <- st_read("SmartLocationDatabase.gdb", layer = "SmartLocationDatabase")

# Examine structure
head(sld_bg)
names(sld_bg)

# Key variables in v3.0:
# GEOID10 (block group FIPS), NatWalkInd (walkability index 0-20),
# D1C (activity density), D2A_EPHHM (land use mix), D3B (intersection density),
# D4D (transit frequency), TotPop, HH, Emptot

# Extract county FIPS from block group GEOID (first 5 digits)
sld_bg <- sld_bg %>%
  mutate(
    county_fips = str_sub(GEOID10, 1, 5)
  )

# Calculate population-weighted county-level walkability
county_walkability <- sld_bg %>%
  st_drop_geometry() %>%
  group_by(county_fips) %>%
  summarize(
    # Population-weighted National Walkability Index
    walkability_index = weighted.mean(NatWalkInd, TotPop, na.rm = TRUE),

    # Population-weighted density
    pop_density = weighted.mean(D1A, TotPop, na.rm = TRUE),
    emp_density = weighted.mean(D1B, TotPop, na.rm = TRUE),
    activity_density = weighted.mean(D1C, TotPop, na.rm = TRUE),

    # Population-weighted diversity
    land_use_mix = weighted.mean(D2A_EPHHM, TotPop, na.rm = TRUE),
    jobs_housing_balance = weighted.mean(D2A_JPHH, TotPop, na.rm = TRUE),

    # Population-weighted design
    intersection_density = weighted.mean(D3B, TotPop, na.rm = TRUE),
    pct_4way_intersections = weighted.mean(D3BPO4, TotPop, na.rm = TRUE),

    # Population-weighted transit access
    transit_frequency = weighted.mean(D4D, TotPop, na.rm = TRUE),
    dist_to_transit_m = weighted.mean(D4A, TotPop, na.rm = TRUE),

    # Jobs accessibility
    jobs_45min_auto = weighted.mean(D5AR, TotPop, na.rm = TRUE),
    jobs_45min_transit = weighted.mean(D5BR, TotPop, na.rm = TRUE),

    # Demographics
    total_pop = sum(TotPop, na.rm = TRUE),
    total_households = sum(HH, na.rm = TRUE),
    total_employment = sum(Emptot, na.rm = TRUE),

    .groups = "drop"
  )

write_csv(county_walkability, "sld_walkability_county_2019.csv")
```

**Method 2: Categorize Walkability**
```r
# EPA categorization of National Walkability Index
county_walkability <- county_walkability %>%
  mutate(
    walkability_category = case_when(
      walkability_index >= 15.25 ~ "Most Walkable",
      walkability_index >= 12.75 ~ "Above Average Walkable",
      walkability_index >= 10.50 ~ "Average Walkable",
      walkability_index >= 8.00  ~ "Below Average Walkable",
      walkability_index < 8.00   ~ "Least Walkable",
      TRUE ~ NA_character_
    ),
    # EPA also uses percentiles
    walkability_pctile = percent_rank(walkability_index) * 100
  )

# Summary by category
county_walkability %>%
  count(walkability_category) %>%
  mutate(pct = n / sum(n) * 100)
```

**Method 3: Join to Health Outcomes**
```r
# Example: Join to CDC PLACES physical inactivity data
places <- read_csv("cdc_places_county.csv")

walkability_health <- county_walkability %>%
  left_join(
    places %>% select(county_fips = LocationName, phys_inactivity_pct = PhysicalInactivity),
    by = "county_fips"
  )

# Analyze association
library(broom)

model <- lm(phys_inactivity_pct ~ walkability_index, data = walkability_health)
tidy(model)

# Expect negative association: higher walkability → lower physical inactivity
```

### Data Quality & Limitations

**Strengths:**
- ✅ **Comprehensive:** 90+ built environment indicators
- ✅ **Nationwide coverage:** All census block groups
- ✅ **EPA-validated:** Rigorous methodology, widely peer-reviewed
- ✅ **Free and public:** No restrictions
- ✅ **Research-grade:** Used in hundreds of published studies
- ✅ **Transit data included:** GTFS-based transit frequency
- ✅ **Multiple spatial scales:** Block group, tract, county, metro

**Limitations:**
- ⚠️ **Cross-sectional:** v3.0 is snapshot of 2019 (though historical versions available)
- ⚠️ **Periodic updates:** v4.0 expected ~2026 (not annual)
- ⚠️ **Block group resolution:** Aggregation to county loses within-county variation
- ⚠️ **Transit data:** Only for areas with GTFS feeds (most urban/suburban, limited rural)
- ⚠️ **File size:** 1.2 GB geodatabase requires significant storage/RAM
- ⚠️ **Rural areas:** Lower walkability scores may reflect rural context, not necessarily "unwalkable" (long-distance driving is necessary)

**Validation:**
- National Walkability Index correlates 0.65-0.75 with Walk Score (commercial index)
- Higher walkability predicts higher active transportation rates (r = 0.7-0.8)
- Cross-validated with physical activity, obesity, CVD outcomes in multiple studies

### Disease Associations (Evidence Summary)

**Physical Activity:**
- +30 minutes/week walking per 1-point increase in walkability (Creatore et al. 2016 J Urban Health)
- Walkability in top quartile → 35% more likely to meet physical activity guidelines (Braun et al. 2016 Prev Med)

**Obesity & Diabetes:**
- High walkability → 31% lower obesity risk (Chandrabose et al. 2019 IJE)
- Walkability index → -0.4% diabetes prevalence per SD increase (Creatore et al. 2016 Diabetes Care)

**Cardiovascular Disease:**
- Walkability → -13% hypertension risk in top vs. bottom quartile (Li et al. 2009 Hypertension)
- High walkability neighborhoods → lower CVD mortality (Lund et al. 2016 Circulation)

**Mental Health:**
- Walkability associated with lower depression (OR 0.88, Berke et al. 2007 Am J Prev Med)
- Mixed-use neighborhoods → lower mental health distress (Dzhambov et al. 2018 Urban Forestry & Urban Greening)

**All-Cause Mortality:**
- High walkability → 11-year longer life expectancy (Stevenson et al. 2016 Health Place)
- Walkable neighborhoods → 35% lower all-cause mortality risk (Chandrabose et al. 2022 Lancet Public Health)

### Use Cases for County-Level Analysis

1. **Physical activity interventions:** Target low-walkability counties for infrastructure investments
2. **Obesity prevention:** Identify counties where built environment contributes to low activity
3. **Health equity:** Cross-reference with CDC SVI to find low-walkability, high-vulnerability areas
4. **Transportation planning:** Prioritize transit, sidewalk, bike lane investments
5. **Climate change mitigation:** Walkability → lower vehicle miles traveled → reduced GHG emissions

### Priority Variables for Collection

**Top 15 SLD variables (county-level, population-weighted):**
1. National Walkability Index (NatWalkInd)
2. Gross activity density (D1C) - population + jobs per acre
3. Employment-household entropy (D2A_EPHHM) - land use mix
4. Street intersection density (D3B)
5. % 4-way intersections (D3BPO4) - grid street pattern
6. Distance to nearest transit (D4A)
7. Aggregate transit frequency (D4D)
8. Jobs within 45-min auto (D5AR)
9. Jobs within 45-min transit (D5BR)
10. Population density (D1A)
11. Employment density (D1B)
12. Jobs-housing balance (D2A_JPHH)
13. Auto-oriented intersection density (D3BAO) - low walkability
14. Pedestrian-oriented 4-way intersections (D3BMM4) - high walkability
15. % population within 0.5 mi of transit

---

## 3. FHWA HPMS TRAFFIC VOLUMES

### Overview

**What It Is:** Federal Highway Administration Highway Performance Monitoring System - Annual Average Daily Traffic (AADT) counts on all public roads
**Disease Relevance:** Respiratory disease (traffic pollution), cardiovascular disease, traffic injuries/deaths, noise exposure
**Evidence Strength:** **VERY STRONG** - Traffic volume/proximity strongly linked to air pollution exposure, respiratory outcomes, CVD

**Critical Gap Filled:** Existing GetData repository has FARS traffic **crashes** but not traffic **volume** exposure that drives air pollution and noise.

### Data Availability

**Coverage:** All states, all counties, all public roads (1+ million road segments)
**Temporal Coverage:** **Annual 1980s-present** (varies by state); **2024 data available**
**Update Frequency:** **Annual** (states submit data to FHWA by April each year)
**Spatial Resolution:** Road segment level (point or line segments with AADT values)
**Data Format:** File geodatabase (.gdb), shapefiles, CSV (road attributes)

### Variables Available

#### Road Segment Variables (100+ attributes in HPMS):
1. **AADT** - Annual Average Daily Traffic (vehicles/day)
2. **AADT_SINGLE_UNIT** - Single-unit trucks AADT
3. **AADT_COMBINATION** - Combination trucks AADT
4. **AADT_YEAR** - Year of AADT measurement
5. **F_SYSTEM** - Functional system (1=Interstate, 2=Other Freeway, 3=Principal Arterial, etc.)
6. **FACILITY_TYPE** - Facility type code (1-way, 2-way, ramp, etc.)
7. **URBAN_CODE** - Urban area code (for metro areas)
8. **THROUGH_LANES** - Number of through lanes
9. **SPEED_LIMIT** - Posted speed limit (mph)
10. **PEAK_PARKING** - Peak period parking restrictions
11. **TERRAIN** - Terrain type (flat, rolling, mountainous)
12. **TOLL_CHARGED** - Toll road indicator
13. **COUNTY_CODE** - County FIPS code
14. **STATE_CODE** - State FIPS code
15. **ROUTE_ID** - Route identification
16. **BEGIN_POINT, END_POINT** - Road segment endpoints (milepost or lat/lon)
17. **SECTION_LENGTH** - Segment length (miles)

#### Derived County-Level Variables (Aggregate from Segments):
18. **Total VMT** - Vehicle Miles Traveled (AADT × length summed across county)
19. **VMT per capita** - Total VMT / county population
20. **VMT per sq mile** - Total VMT / county land area
21. **Truck VMT** - Truck AADT × length summed
22. **Truck VMT %** - Truck VMT / Total VMT
23. **Interstate VMT** - VMT on interstate highways
24. **Arterial VMT** - VMT on principal/minor arterials
25. **Local road VMT** - VMT on local roads
26. **High-traffic road miles** - Miles of roads with AADT >10,000
27. **Very high-traffic road miles** - Miles with AADT >50,000
28. **Population within 500m of high-traffic roads** - Requires Census block + buffer analysis
29. **Population within 500m of AADT >25,000** - Near-road exposure proxy
30. **Weighted average AADT** - VMT-weighted mean AADT across county

### Access Methods

#### Primary Source:
**Website:** Bureau of Transportation Statistics (BTS)
**URL:** https://www.bts.gov/hpms
**National Downloads:** https://www.fhwa.dot.gov/policyinformation/hpms/shapefiles.cfm
**State DOT Portals:** Each state also publishes HPMS data

#### Data Formats Available:
- **File Geodatabase (.gdb):** Annual national HPMS (all states combined, ~5-10 GB)
- **Shapefiles:** By state (smaller files, easier processing)
- **CSV:** Road attributes without geometry (requires route matching)
- **SQL Server/PostgreSQL:** Some state DOTs provide database access

#### Download & Processing

**Method 1: Download National HPMS Geodatabase**
```bash
# Download 2023 HPMS (example - check current year URL)
wget https://www.fhwa.dot.gov/policyinformation/hpms/shapefiles/hpms2023.zip

# Unzip (large file, 5-10 GB uncompressed)
unzip hpms2023.zip
```

**Method 2: State-Specific Download (Recommended for Single-State Analysis)**
```bash
# Download California HPMS 2023 (example)
wget https://www.fhwa.dot.gov/policyinformation/hpms/shapefiles/ca2023.zip
unzip ca2023.zip
```

**Method 3: R Processing - Load and Aggregate to County**
```r
library(sf)
library(tidyverse)

# Read HPMS geodatabase (national or state)
hpms <- st_read("hpms2023.gdb", layer = "Sections")

# Or read state shapefile
hpms_ca <- st_read("ca2023.shp")

# Examine structure
head(hpms_ca)
names(hpms_ca)

# Key fields: AADT, SECTION_LENGTH, COUNTY_CODE, F_SYSTEM

# Calculate VMT by road segment
hpms_ca <- hpms_ca %>%
  mutate(
    vmt_daily = AADT * SECTION_LENGTH,
    vmt_annual = vmt_daily * 365,
    truck_vmt_annual = (AADT_SINGLE_UNIT + AADT_COMBINATION) * SECTION_LENGTH * 365
  )

# Aggregate to county
county_traffic <- hpms_ca %>%
  st_drop_geometry() %>%
  group_by(COUNTY_CODE) %>%
  summarize(
    # Total VMT
    total_vmt_annual = sum(vmt_annual, na.rm = TRUE),
    total_truck_vmt_annual = sum(truck_vmt_annual, na.rm = TRUE),
    truck_pct_vmt = total_truck_vmt_annual / total_vmt_annual * 100,

    # VMT by functional class
    interstate_vmt = sum(vmt_annual[F_SYSTEM == 1], na.rm = TRUE),
    arterial_vmt = sum(vmt_annual[F_SYSTEM %in% c(2, 3, 4, 5)], na.rm = TRUE),
    local_vmt = sum(vmt_annual[F_SYSTEM >= 6], na.rm = TRUE),

    # High-traffic road exposure
    road_miles_aadt_over_10k = sum(SECTION_LENGTH[AADT > 10000], na.rm = TRUE),
    road_miles_aadt_over_25k = sum(SECTION_LENGTH[AADT > 25000], na.rm = TRUE),
    road_miles_aadt_over_50k = sum(SECTION_LENGTH[AADT > 50000], na.rm = TRUE),

    # Weighted average AADT
    avg_aadt_vmt_weighted = sum(AADT * SECTION_LENGTH, na.rm = TRUE) / sum(SECTION_LENGTH, na.rm = TRUE),

    # Road characteristics
    total_road_miles = sum(SECTION_LENGTH, na.rm = TRUE),
    total_lane_miles = sum(SECTION_LENGTH * THROUGH_LANES, na.rm = TRUE),

    .groups = "drop"
  )

# Join county population to calculate per-capita metrics
county_pop <- read_csv("county_population_2023.csv") # From Census

county_traffic <- county_traffic %>%
  left_join(county_pop, by = c("COUNTY_CODE" = "county_fips")) %>%
  mutate(
    vmt_per_capita = total_vmt_annual / population,
    road_miles_per_capita = total_road_miles / population * 1000 # per 1,000 pop
  )

write_csv(county_traffic, "hpms_county_traffic_2023.csv")
```

**Method 4: Near-Road Population Exposure (Advanced GIS)**
```r
library(sf)
library(tidyverse)

# Load HPMS roads
hpms <- st_read("hpms2023.shp")

# Filter to high-traffic roads (AADT > 25,000)
high_traffic_roads <- hpms %>%
  filter(AADT > 25000)

# Buffer 500 meters around high-traffic roads
road_buffers <- st_buffer(high_traffic_roads, dist = 500)

# Load Census block population data (most detailed)
census_blocks <- st_read("census_blocks_2020.shp") # From Census TIGER

# Intersect buffers with blocks to find population near roads
near_road_pop <- st_intersection(census_blocks, road_buffers) %>%
  group_by(COUNTY_CODE) %>%
  summarize(
    pop_within_500m_high_traffic = sum(POP20, na.rm = TRUE),
    .groups = "drop"
  )

# Join back to county totals
county_traffic <- county_traffic %>%
  left_join(near_road_pop, by = "COUNTY_CODE") %>%
  mutate(
    pct_pop_near_high_traffic = pop_within_500m_high_traffic / population * 100
  )
```

### Data Quality & Limitations

**Strengths:**
- ✅ **Comprehensive coverage:** All public roads, all states, all counties
- ✅ **Long time series:** 1980s-present for most states (40+ years)
- ✅ **Annual updates:** Consistent monitoring
- ✅ **Federal standard:** HPMS required under MAP-21/FAST Act
- ✅ **High spatial resolution:** Road segment level
- ✅ **Free and public:** No restrictions
- ✅ **Truck data:** Separate AADT for single-unit and combination trucks

**Limitations:**
- ⚠️ **Measurement variability:** Some AADT from permanent counters (high quality), others from short-duration counts with factors applied
- ⚠️ **Rural roads:** Local roads may have estimated (not measured) AADT
- ⚠️ **Lags:** Annual data typically 1-2 years behind (2024 data available late 2025)
- ⚠️ **Large file sizes:** National geodatabase is 5-10 GB
- ⚠️ **Processing required:** Must aggregate segment-level to county
- ⚠️ **Near-road exposure:** Requires GIS skills to calculate population within buffers

**Data Quality Tiers:**
- **High quality:** Interstate, principal arterials (permanent counters, continuous monitoring)
- **Medium quality:** Minor arterials, collectors (periodic counts, factored)
- **Lower quality:** Local roads (estimated AADT, less frequent counting)

### Disease Associations (Evidence Summary)

**Respiratory Disease:**
- Living <300m from major road → 50% higher asthma incidence in children (McConnell et al. 2006 Lancet)
- Traffic density within 150m → increased COPD prevalence (Schikowski et al. 2014 Thorax)
- AADT >10,000 within 50m → +16% respiratory symptoms (Kim et al. 2004 EHP)

**Cardiovascular Disease:**
- Living near high-traffic roads → +4-12% CVD mortality (Hoffmann et al. 2006 Circulation)
- Traffic exposure → atherosclerosis progression (Künzli et al. 2010 Circulation)
- Each 10,000 vehicles/day increase → +3% cardiac arrest risk (Rosenbloom et al. 2012 Am Heart J)

**Lung Cancer:**
- Proximity to high-traffic roads → +10-40% lung cancer risk (non-smokers) (Raaschou-Nielsen et al. 2011 EHP)

**Pregnancy Outcomes:**
- High traffic exposure (>15,000 AADT within 50m) → +30% preterm birth risk (Wilhelm et al. 2011 EHP)
- Traffic density → low birth weight association (Parker et al. 2005 Epidemiology)

**Traffic Injuries:**
- High VMT counties → higher pedestrian/cyclist fatality rates (Beck et al. 2007 Am J Public Health)
- AADT is denominator for crash rate calculations (crashes per million VMT)

### Use Cases for County-Level Analysis

1. **Air pollution exposure assessment:** Traffic VMT is proxy for NOx, PM2.5, UFP exposure in absence of monitors
2. **Near-road health impacts:** Identify high-traffic corridors for near-road population exposure
3. **Traffic safety:** VMT is denominator for crash/fatality rates (FARS crashes per 100M VMT)
4. **Noise exposure:** AADT strongly predicts traffic noise levels (FHWA noise model)
5. **Transportation planning:** County VMT trends inform infrastructure needs
6. **Climate change:** VMT × emission factors = county mobile source GHG emissions

### Priority Variables for Collection

**Top 15 HPMS variables (county × year):**
1. Total annual VMT (all roads)
2. VMT per capita
3. Truck VMT (annual)
4. Truck % of VMT
5. Interstate VMT
6. Arterial VMT (principal + minor)
7. Road miles with AADT >10,000
8. Road miles with AADT >25,000
9. Road miles with AADT >50,000
10. Population within 500m of AADT >25,000 roads (requires GIS)
11. % population within 500m of high-traffic roads
12. VMT-weighted average AADT
13. Total road miles (all functional classes)
14. Total lane miles
15. Road miles per capita

---

## 4. EPA RCRAInfo HAZARDOUS WASTE SITES

### Overview

**What It Is:** Resource Conservation and Recovery Act Information System - database of hazardous waste treatment, storage, and disposal facilities (TSDFs) and generators
**Disease Relevance:** Cancer (various types), birth defects, respiratory disease, neurological effects
**Evidence Strength:** **MODERATE-STRONG** - Proximity to hazardous waste associated with health risks, though evidence less consistent than air pollution

**Critical Gap Filled:** Existing GetData repository has NPL Superfund sites (1,343 worst sites). RCRAInfo covers ~800,000 RCRA-regulated facilities - much broader universe.

### Data Availability

**Coverage:** All counties (where facilities exist), ~800,000 regulated facilities
**Temporal Coverage:** **1980s-present** (updated weekly)
**Update Frequency:** **Weekly** (RCRAInfo database continuously updated)
**Spatial Resolution:** Facility point locations (address-level)
**Data Format:** Web database (searchable), CSV/Excel (bulk downloads), Envirofacts API (JSON)

### Variables Available

#### Facility-Level Variables (200+ in RCRAInfo):
1. **EPA_ID** - Unique facility ID (12-character)
2. **Facility_Name** - Facility name
3. **Location_Address** - Street address
4. **City, State, ZIP**
5. **County_FIPS** - County code
6. **Latitude, Longitude** - Facility coordinates
7. **NAICS_Code** - Industry classification
8. **Handler_Type** - Generator, TSDF, Transporter, etc.
9. **Generator_Status** - Large Quantity Generator (LQG), Small Quantity, etc.
10. **TSDF_Status** - Treatment, Storage, Disposal permit status
11. **Corrective_Action** - Contaminated site requiring cleanup
12. **Waste_Codes** - Hazardous waste types handled (F, K, P, U, D codes)
13. **Violation_Status** - Current violations
14. **Inspection_Date** - Most recent inspection
15. **Enforcement_Actions** - Count of enforcement actions
16. **Compliance_Status** - In compliance, violations, etc.
17. **Waste_Minimization** - Waste reduction activities
18. **Biennial_Report_Year** - Most recent biennial report (LQGs only)

#### Hazardous Waste Types (EPA Codes):
19. **F-listed wastes** - Generic industrial process wastes (F001-F039)
20. **K-listed wastes** - Industry-specific wastes (K001-K181)
21. **P-listed wastes** - Acute hazardous wastes (P001-P205)
22. **U-listed wastes** - Toxic wastes (U001-U411)
23. **D-listed wastes** - Characteristic wastes (D001-D043: ignitable, corrosive, reactive, toxic)

#### Derived County-Level Variables:
24. **Total RCRA facilities** - Count of all regulated facilities
25. **Large Quantity Generators (LQGs)** - Facilities generating >1,000 kg/month hazardous waste
26. **Small Quantity Generators (SQGs)** - 100-1,000 kg/month
27. **Very Small Quantity Generators (VSQGs)** - <100 kg/month
28. **TSDFs** - Treatment, Storage, Disposal Facilities (most concerning)
29. **Corrective Action sites** - Contaminated sites requiring cleanup
30. **Facilities with violations** - Count with current violations
31. **Facilities per 10,000 population**
32. **Facilities per 100 sq miles** - Density
33. **LQGs per capita** - High-volume hazardous waste generators
34. **TSDFs per capita**
35. **Corrective Action sites per capita**
36. **% facilities in violation**
37. **Population within 1 km of LQG** - Requires GIS (buffer analysis)
38. **Population within 1 km of TSDF**
39. **Environmental justice metrics** - Facilities in high-minority, low-income census tracts (EJSCREEN)

### Access Methods

#### Primary Sources:
**Website:** EPA RCRAInfo Web
**URL:** https://rcrapublic.epa.gov/
**Envirofacts API:** https://www.epa.gov/enviro/envirofacts-data-service-api
**Bulk Downloads:** https://www.epa.gov/enviro/rcrainfo-web-download (quarterly extracts)

#### Data Formats Available:
- **Web Search:** RCRAInfo Web search interface (by location, facility, waste type)
- **CSV/Excel:** Quarterly bulk downloads (National Biennial Report)
- **Envirofacts API:** JSON format (real-time queries)
- **EJSCREEN:** Proximity to RMP/TSDF facilities in EJSCREEN layers

#### Download & Processing

**Method 1: Envirofacts API (Recommended for Small Queries)**
```r
library(httr)
library(jsonlite)
library(tidyverse)

# Function to query RCRAInfo by county
get_rcra_county <- function(county_fips) {

  # Envirofacts RCRA facility API
  base_url <- "https://data.epa.gov/efservice/RCRA_FACILITY/"

  # Query by county FIPS (example: Cook County, IL = 17031)
  url <- paste0(base_url, "COUNTY_CODE/", county_fips, "/JSON")

  response <- GET(url)

  if (status_code(response) == 200) {
    data <- fromJSON(content(response, as = "text", encoding = "UTF-8"))
    return(as_tibble(data))
  } else {
    return(NULL)
  }
}

# Get all RCRA facilities in Cook County, IL
cook_facilities <- get_rcra_county("17031")

head(cook_facilities)
```

**Method 2: Bulk Download National Biennial Report**
```r
library(tidyverse)

# Download National Biennial Report (LQGs only, biennial)
# https://www.epa.gov/hwgenerators/biennial-hazardous-waste-report

# Example: 2021 Biennial Report
download.file(
  "https://rcrapublic.epa.gov/rcrainfoweb/documents/br/2021/2021_BR_National_Analysis.xlsx",
  destfile = "br_2021_national.xlsx"
)

br_2021 <- readxl::read_excel("br_2021_national.xlsx", sheet = "Facilities")

# Aggregate to county
county_rcra <- br_2021 %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    lqg_count = n(),
    total_hazwaste_tons = sum(TOTAL_HAZARDOUS_WASTE_TONS, na.rm = TRUE),
    waste_management_onsite_pct = mean(ONSITE_MANAGEMENT_PCT, na.rm = TRUE),
    waste_offsite_disposal_pct = mean(OFFSITE_DISPOSAL_PCT, na.rm = TRUE),
    .groups = "drop"
  )

write_csv(county_rcra, "rcra_lqg_county_2021.csv")
```

**Method 3: Query All Facilities by State (More Complete)**
```r
# Download full RCRAInfo data extract (quarterly)
# https://www.epa.gov/enviro/rcrainfo-web-download

# Read RCRAInfo extract (example: Handler file)
handlers <- read_csv("RCRAInfo_Handlers_2024Q4.csv")

# Filter to active facilities
active_facilities <- handlers %>%
  filter(HANDLER_STATUS == "Active")

# Categorize by facility type
facility_types <- active_facilities %>%
  mutate(
    is_lqg = str_detect(GENERATOR_STATUS, "LQG"),
    is_sqg = str_detect(GENERATOR_STATUS, "SQG"),
    is_vsqg = str_detect(GENERATOR_STATUS, "VSQG"),
    is_tsdf = str_detect(HANDLER_TYPE, "TSDF"),
    is_corrective_action = !is.na(CORRECTIVE_ACTION_STATUS),
    has_violation = VIOLATION_STATUS == "Yes"
  )

# Aggregate to county
county_rcra_full <- facility_types %>%
  group_by(COUNTY_FIPS = LOCATION_COUNTY_CODE) %>%
  summarize(
    total_facilities = n(),
    lqg_count = sum(is_lqg, na.rm = TRUE),
    sqg_count = sum(is_sqg, na.rm = TRUE),
    vsqg_count = sum(is_vsqg, na.rm = TRUE),
    tsdf_count = sum(is_tsdf, na.rm = TRUE),
    corrective_action_count = sum(is_corrective_action, na.rm = TRUE),
    violation_count = sum(has_violation, na.rm = TRUE),
    pct_in_violation = mean(has_violation, na.rm = TRUE) * 100,
    .groups = "drop"
  )

# Join county population
county_pop <- read_csv("county_population_2024.csv")

county_rcra_full <- county_rcra_full %>%
  left_join(county_pop, by = c("COUNTY_FIPS" = "county_fips")) %>%
  mutate(
    facilities_per_10k = total_facilities / population * 10000,
    lqg_per_10k = lqg_count / population * 10000,
    tsdf_per_10k = tsdf_count / population * 10000
  )

write_csv(county_rcra_full, "rcra_all_facilities_county_2024.csv")
```

**Method 4: Near-Facility Population Exposure (Advanced GIS)**
```r
library(sf)
library(tidyverse)

# Create facility points from lat/lon
facilities_sf <- facility_types %>%
  filter(!is.na(LATITUDE), !is.na(LONGITUDE)) %>%
  st_as_sf(coords = c("LONGITUDE", "LATITUDE"), crs = 4326)

# Filter to high-concern facilities (TSDFs and LQGs)
high_concern <- facilities_sf %>%
  filter(is_tsdf | is_lqg)

# Buffer 1 km around facilities
facility_buffers <- st_buffer(high_concern, dist = 1000) # 1 km

# Load Census blocks
census_blocks <- st_read("census_blocks_2020.shp")

# Intersect buffers with blocks
near_facility_pop <- st_intersection(census_blocks, facility_buffers) %>%
  group_by(COUNTY_FIPS) %>%
  summarize(
    pop_within_1km_tsdf_lqg = sum(POP20, na.rm = TRUE),
    .groups = "drop"
  )

# Join to county totals
county_rcra_exposure <- county_rcra_full %>%
  left_join(near_facility_pop, by = "COUNTY_FIPS") %>%
  mutate(
    pct_pop_near_hazwaste = pop_within_1km_tsdf_lqg / population * 100
  )
```

### Data Quality & Limitations

**Strengths:**
- ✅ **Comprehensive:** 800,000+ regulated facilities (vs. 1,343 NPL Superfund sites)
- ✅ **Updated weekly:** Near-real-time compliance status
- ✅ **Free and public:** No restrictions
- ✅ **Facility-level detail:** Waste types, violations, inspections
- ✅ **Long history:** 1980s-present
- ✅ **Federal oversight:** EPA regulatory program

**Limitations:**
- ⚠️ **Facility presence ≠ exposure:** Proximity to facility doesn't guarantee exposure (depends on waste handling practices, containment)
- ⚠️ **Self-reported data:** Biennial reports are self-reported by facilities (though EPA inspects)
- ⚠️ **Small generators not fully captured:** VSQGs (<100 kg/month) are not required to submit biennial reports
- ⚠️ **No exposure monitoring:** RCRAInfo doesn't measure environmental concentrations of hazardous substances
- ⚠️ **Corrective Action variable:** Some contaminated sites are still being cleaned up (not necessarily currently releasing)
- ⚠️ **Large dataset:** Full RCRAInfo extract is large (requires processing)

**Data Quality Tiers:**
- **High quality:** LQG biennial reports (audited, inspected regularly)
- **Medium quality:** SQG and TSDF data (less frequent reporting)
- **Lower quality:** VSQG data (minimal reporting requirements)

### Disease Associations (Evidence Summary)

**Cancer:**
- Proximity to hazardous waste sites → increased cancer incidence (various types) in some studies (Vrijheid 2000 Occup Environ Med review)
- Mixed evidence: Some studies find associations, others null (exposure assessment challenges)

**Birth Defects:**
- Living near hazardous waste sites → increased neural tube defects, cardiac defects (Geschwind et al. 1992 Arch Environ Health)
- Landfill proximity → birth defect associations in some European studies (Elliott et al. 2001 BMJ)

**Respiratory Disease:**
- Proximity to industrial facilities (RCRA overlap) → respiratory symptoms in children (Weisel et al. 2005 J Expo Anal Environ Epidemiol)

**Methodological Note:**
Disease associations are challenging due to:
- Exposure misclassification (proximity ≠ exposure)
- Multiple chemical exposures (hard to isolate single chemical)
- Small exposed populations (low statistical power)
- Confounding by SES (facilities often in disadvantaged areas)

**Strongest Evidence:** TSDFs and corrective action sites (contaminated) have stronger associations than merely being a generator.

### Use Cases for County-Level Analysis

1. **Environmental justice:** Identify counties with high RCRA facility density in vulnerable populations (cross-reference EJSCREEN, CDC SVI)
2. **Cancer cluster investigation:** Proximity to hazardous waste as potential risk factor
3. **Regulatory targeting:** Counties with high % facilities in violation → prioritize enforcement
4. **Community awareness:** Public health departments identify facilities for community education
5. **Land use planning:** Avoid siting schools, childcare near LQGs/TSDFs

### Priority Variables for Collection

**Top 15 RCRAInfo variables (county × year):**
1. Total RCRA-regulated facilities (count)
2. Large Quantity Generators (LQG) count
3. Small Quantity Generators (SQG) count
4. Treatment, Storage, Disposal Facilities (TSDF) count
5. Corrective Action sites (contaminated) count
6. Facilities with current violations (count)
7. % facilities in violation
8. Facilities per 10,000 population
9. LQG per 10,000 population
10. TSDF per 10,000 population
11. Population within 1 km of LQG/TSDF (requires GIS)
12. % population within 1 km of LQG/TSDF
13. Total hazardous waste generated (tons, from Biennial Report)
14. % waste managed onsite vs. offsite disposal
15. Most recent inspection date (average across facilities)

---

## 5. EPA LMOP LANDFILLS

### Overview

**What It Is:** EPA Landfill Methane Outreach Program database of active and closed municipal solid waste (MSW) landfills
**Disease Relevance:** Respiratory disease, cancer (benzene, vinyl chloride), birth defects, odor/quality of life
**Evidence Strength:** **MODERATE** - Some evidence of birth defects, respiratory effects near landfills, but studies limited

**Critical Gap Filled:** Existing GetData repository does not have landfill locations. Landfills are ubiquitous (2,000+ nationally) and potential exposure sources.

### Data Availability

**Coverage:** All counties (where landfills exist), ~2,600 MSW landfills (1,200 open, 1,400 closed)
**Temporal Coverage:** **Current operational status** + **historical closure dates** (back to 1960s for some)
**Update Frequency:** **Quarterly** (LMOP database updated ~4 times/year)
**Spatial Resolution:** Facility point locations (lat/lon)
**Data Format:** Excel spreadsheet, interactive web map

### Variables Available

#### Landfill-Level Variables:
1. **Landfill_Name** - Facility name
2. **City, State, County**
3. **Latitude, Longitude** - Facility coordinates
4. **Landfill_Status** - Open (accepting waste), Closed, Post-closure monitoring
5. **Landfill_Type** - MSW, Industrial, Construction & Demolition (C&D)
6. **Year_Opened** - Year landfill began operations
7. **Year_Closed** - Year landfill stopped accepting waste (if closed)
8. **Waste_in_Place** - Tons of waste currently buried (estimated)
9. **Size_Classification** - Large (>2.5 million tons), Medium, Small
10. **Gas_Collection_System** - Yes/No (methane collection)
11. **LFG_Energy_Project** - Landfill gas-to-energy project status (Operational, Candidate, Potential)
12. **LFG_Energy_Type** - Electricity generation, direct use (heating), pipeline injection (RNG)
13. **LFG_Captured_MMBtu** - Annual landfill gas captured (MMBtu/year)
14. **Ownership** - Public, Private
15. **Contact_Info** - Facility owner/operator contact

#### Derived County-Level Variables:
16. **Total MSW landfills** - Count of all landfills (open + closed)
17. **Open landfills** - Currently accepting waste
18. **Closed landfills** - No longer accepting waste (may still emit gas)
19. **Landfills per 100,000 population**
20. **Landfills per 100 sq miles** - Density
21. **Waste in place (tons)** - Total waste buried in county
22. **Waste in place per capita** - Tons per county resident
23. **Landfills with gas collection** - Count with methane capture systems
24. **% landfills with gas collection**
25. **LFG energy projects** - Count of gas-to-energy projects
26. **LFG energy capacity (MMBtu)** - Total annual gas captured
27. **Population within 1 mile of open landfill** - Requires GIS
28. **Population within 1 mile of closed landfill** - Closed landfills still emit gas for decades
29. **% population within 1 mile of any landfill**
30. **Landfill closure rate** - Trend in closures vs. openings

### Access Methods

#### Primary Source:
**Website:** EPA Landfill Methane Outreach Program
**URL:** https://www.epa.gov/lmop
**Interactive Map:** https://www.epa.gov/lmop/landfill-gas-energy-project-data
**Data Download:** https://www.epa.gov/lmop/lmop-landfill-and-project-database (Excel file)

#### Data Format:
- **Excel Spreadsheet:** "LMOP_Landfill_and_Project_Database.xlsx" (updated quarterly)
- **Interactive Map:** Searchable by location, filterable by status
- **No API:** Must download Excel file

#### Download & Processing

**Method 1: Download and Load Excel File**
```r
library(readxl)
library(tidyverse)

# Download LMOP database (check website for current URL)
download.file(
  "https://www.epa.gov/sites/default/files/lmop/documents/LMOP_Landfill_and_Project_Database.xlsx",
  destfile = "lmop_database.xlsx"
)

# Read Excel file (typically "Landfills" sheet)
landfills <- read_excel("lmop_database.xlsx", sheet = "Landfills")

# Examine structure
head(landfills)
names(landfills)

# Key fields: State, County, City, Latitude, Longitude, Landfill_Status,
# Year_Opened, Year_Closed, Waste_in_Place, Gas_Collection_System

# Clean and standardize
landfills_clean <- landfills %>%
  mutate(
    # Create county FIPS (requires county name → FIPS lookup)
    state_fips = case_when(
      State == "AL" ~ "01", State == "AK" ~ "02", State == "AZ" ~ "04",
      # ... (all 50 states)
      State == "WY" ~ "56",
      TRUE ~ NA_character_
    ),
    # Clean status
    status = case_when(
      str_detect(tolower(Landfill_Status), "open") ~ "Open",
      str_detect(tolower(Landfill_Status), "closed") ~ "Closed",
      TRUE ~ Landfill_Status
    ),
    # Gas collection
    has_gas_collection = Gas_Collection_System == "Yes",
    # Energy project
    has_energy_project = !is.na(LFG_Energy_Project) & LFG_Energy_Project != "No Project"
  )

# For county FIPS, need to join with county name lookup table
county_lookup <- read_csv("fips_county_lookup.csv") # FIPS code, state, county name

landfills_with_fips <- landfills_clean %>%
  left_join(
    county_lookup,
    by = c("State" = "state_abbr", "County" = "county_name")
  )

head(landfills_with_fips)
```

**Method 2: Aggregate to County**
```r
county_landfills <- landfills_with_fips %>%
  group_by(county_fips) %>%
  summarize(
    # Counts
    total_landfills = n(),
    open_landfills = sum(status == "Open", na.rm = TRUE),
    closed_landfills = sum(status == "Closed", na.rm = TRUE),

    # Gas collection
    landfills_with_gas_collection = sum(has_gas_collection, na.rm = TRUE),
    pct_with_gas_collection = mean(has_gas_collection, na.rm = TRUE) * 100,

    # Energy projects
    lfg_energy_projects = sum(has_energy_project, na.rm = TRUE),
    total_lfg_mmbtu = sum(LFG_Captured_MMBtu, na.rm = TRUE),

    # Waste
    total_waste_in_place_tons = sum(Waste_in_Place, na.rm = TRUE),

    # Years
    oldest_landfill_year = min(Year_Opened, na.rm = TRUE),
    newest_landfill_year = max(Year_Opened, na.rm = TRUE),
    most_recent_closure = max(Year_Closed, na.rm = TRUE),

    .groups = "drop"
  )

# Join county population
county_pop <- read_csv("county_population_2024.csv")

county_landfills <- county_landfills %>%
  left_join(county_pop, by = "county_fips") %>%
  mutate(
    landfills_per_100k = total_landfills / population * 100000,
    waste_per_capita_tons = total_waste_in_place_tons / population
  )

write_csv(county_landfills, "lmop_landfills_county.csv")
```

**Method 3: Near-Landfill Population Exposure (GIS)**
```r
library(sf)
library(tidyverse)

# Create landfill point locations
landfills_sf <- landfills_with_fips %>%
  filter(!is.na(Latitude), !is.na(Longitude)) %>%
  st_as_sf(coords = c("Longitude", "Latitude"), crs = 4326)

# Buffer 1 mile (1.6 km) around landfills
landfill_buffers <- st_buffer(landfills_sf, dist = 1609) # 1 mile in meters

# Load Census blocks
census_blocks <- st_read("census_blocks_2020.shp")

# Intersect buffers with blocks
near_landfill_pop <- st_intersection(census_blocks, landfill_buffers) %>%
  group_by(county_fips) %>%
  summarize(
    pop_within_1mi_landfill = sum(POP20, na.rm = TRUE),
    .groups = "drop"
  )

# Join to county totals
county_landfills_exposure <- county_landfills %>%
  left_join(near_landfill_pop, by = "county_fips") %>%
  mutate(
    pct_pop_near_landfill = pop_within_1mi_landfill / population * 100
  )

write_csv(county_landfills_exposure, "lmop_landfills_county_exposure.csv")
```

### Data Quality & Limitations

**Strengths:**
- ✅ **Comprehensive:** 2,600+ MSW landfills (most complete national inventory)
- ✅ **Free and public:** No restrictions
- ✅ **Historical data:** Year opened/closed available (some back to 1960s)
- ✅ **Gas collection info:** Identifies landfills with methane capture (reduces emissions)
- ✅ **Energy project tracking:** Beneficial use of landfill gas documented
- ✅ **Regularly updated:** Quarterly updates

**Limitations:**
- ⚠️ **Excel format only:** No API, must manually download
- ⚠️ **MSW landfills only:** Does not include industrial, C&D, or hazardous waste landfills
- ⚠️ **No county FIPS:** Must manually match county names to FIPS codes (requires lookup table)
- ⚠️ **Waste in place estimates:** Some landfills have missing or estimated waste tonnage
- ⚠️ **Closed landfill emissions:** Closed landfills still emit methane for 20-50 years, but LMOP doesn't quantify ongoing emissions
- ⚠️ **No exposure monitoring:** Proximity ≠ exposure (depends on wind, gas collection effectiveness)

**Data Quality Tiers:**
- **High quality:** Open landfills with gas-to-energy projects (closely monitored)
- **Medium quality:** Open landfills without energy projects (reported to state regulators)
- **Lower quality:** Closed landfills (less monitoring, emissions not quantified)

### Disease Associations (Evidence Summary)

**Birth Defects:**
- Living near landfills → increased neural tube defects, cardiac defects (Elliott et al. 2001 BMJ - UK study)
- Landfill proximity → birth defect associations in European studies (Vrijheid 2000 review)

**Respiratory Disease:**
- Landfill proximity → respiratory symptoms, wheeze in children (Pukkala & Pönkä 2001 Scand J Work Environ Health)
- Bioaerosols from landfills → respiratory complaints (Heaney et al. 2019 Science of the Total Environment)

**Cancer:**
- Mixed evidence: Some studies find elevated cancer incidence near landfills (bladder, leukemia), others null
- Modern landfills (post-1990 regulations) have better containment than historical landfills

**Quality of Life:**
- Odor complaints common within 1 mile of landfills
- Property values lower near landfills (proxy for perceived health risk)

**Methodological Note:**
Historical landfills (pre-1980) had minimal liner/leachate controls → higher contamination risk. Modern landfills (post-RCRA Subtitle D 1991) have composite liners, leachate collection, gas control → lower risk.

### Use Cases for County-Level Analysis

1. **Land use planning:** Identify counties with high landfill density for zoning restrictions
2. **Environmental justice:** Cross-reference landfill locations with CDC SVI (often in disadvantaged areas)
3. **Methane emissions:** Closed landfills without gas collection → GHG emissions (climate change)
4. **Birth defect surveillance:** Proximity to landfills as risk factor in case-control studies
5. **Waste management policy:** Track waste in place per capita → waste diversion targets

### Priority Variables for Collection

**Top 10 LMOP variables (county):**
1. Total MSW landfills (open + closed)
2. Open landfills (currently accepting waste)
3. Closed landfills
4. Landfills per 100,000 population
5. Waste in place (total tons)
6. Waste in place per capita
7. Landfills with gas collection systems (count)
8. % landfills with gas collection
9. Population within 1 mile of any landfill (requires GIS)
10. % population within 1 mile of landfill

---

## INTEGRATION & USE CASES

### Cross-Source Integration Examples

#### 1. **Respiratory Disease Burden = Air Pollution + Wildfire Smoke + Traffic + Tobacco**

```r
library(tidyverse)

# Load all exposure data
air_nei <- read_csv("nei_pm25_county_2020.csv")
smoke_hms <- read_csv("hms_smoke_2020_county_annual.csv")
traffic_hpms <- read_csv("hpms_county_traffic_2020.csv")
tobacco_retailers <- read_csv("tobacco_retailers_county.csv")

# Integrate
respiratory_exposures <- air_nei %>%
  left_join(smoke_hms, by = "county_fips") %>%
  left_join(traffic_hpms, by = "county_fips") %>%
  left_join(tobacco_retailers, by = "county_fips") %>%
  mutate(
    # Composite respiratory risk score (standardize each, sum)
    pm25_z = scale(pm25_annual_mean)[,1],
    smoke_z = scale(smoke_days_total)[,1],
    traffic_z = scale(vmt_per_capita)[,1],
    tobacco_z = scale(retailers_per_10k)[,1],

    respiratory_risk_score = pm25_z + smoke_z + traffic_z + tobacco_z
  )

# Join to asthma prevalence from CDC PLACES
places <- read_csv("cdc_places_county.csv")

respiratory_analysis <- respiratory_exposures %>%
  left_join(
    places %>% select(county_fips, asthma_pct = CurrentAsthma),
    by = "county_fips"
  )

# Model
model <- lm(asthma_pct ~ pm25_z + smoke_z + traffic_z + tobacco_z,
            data = respiratory_analysis)
summary(model)
```

#### 2. **Walkability + Built Environment → CVD Prevention**

```r
# Combine walkability, green space, food environment
walkability_sld <- read_csv("sld_walkability_county_2019.csv")
green_space <- read_csv("usda_tree_canopy_county_2024.csv")
food_deserts <- read_csv("usda_food_deserts_county_2019.csv")

built_environment <- walkability_sld %>%
  left_join(green_space, by = "county_fips") %>%
  left_join(food_deserts, by = "county_fips") %>%
  mutate(
    # Healthy built environment score
    walkability_z = scale(walkability_index)[,1],
    tree_canopy_z = scale(tree_canopy_pct)[,1],
    food_access_z = -scale(pct_pop_food_desert)[,1], # negative because higher = worse

    healthy_built_env_score = walkability_z + tree_canopy_z + food_access_z
  )

# Join to CVD mortality
cdc_wonder <- read_csv("cdc_wonder_cvd_mortality_county.csv")

cvd_prevention <- built_environment %>%
  left_join(cdc_wonder, by = "county_fips")

# Model
model_cvd <- lm(cvd_mortality_rate ~ walkability_z + tree_canopy_z + food_access_z,
                data = cvd_prevention)
summary(model_cvd)
```

#### 3. **Environmental Justice: Cumulative Exposures in Vulnerable Communities**

```r
# Load vulnerability index
svi <- read_csv("cdc_svi_county_2022.csv")

# Load all exposures
wildfire_smoke <- read_csv("hms_smoke_county.csv")
traffic <- read_csv("hpms_traffic_county.csv")
hazwaste_rcra <- read_csv("rcra_county.csv")
landfills <- read_csv("lmop_landfills_county.csv")

# Integrate
ej_analysis <- svi %>%
  left_join(wildfire_smoke, by = "county_fips") %>%
  left_join(traffic, by = "county_fips") %>%
  left_join(hazwaste_rcra, by = "county_fips") %>%
  left_join(landfills, by = "county_fips") %>%
  mutate(
    # High vulnerability = top quartile SVI
    high_vulnerability = svi_overall >= quantile(svi_overall, 0.75, na.rm = TRUE),

    # High exposure = top quartile on any exposure
    high_smoke = smoke_days_total >= quantile(smoke_days_total, 0.75, na.rm = TRUE),
    high_traffic = vmt_per_capita >= quantile(vmt_per_capita, 0.75, na.rm = TRUE),
    high_hazwaste = tsdf_count >= quantile(tsdf_count, 0.75, na.rm = TRUE),
    high_landfill = landfills_per_100k >= quantile(landfills_per_100k, 0.75, na.rm = TRUE),

    # Cumulative exposure burden
    exposure_burden = high_smoke + high_traffic + high_hazwaste + high_landfill
  )

# Environmental justice priority counties: high vulnerability + high burden
ej_priority <- ej_analysis %>%
  filter(high_vulnerability & exposure_burden >= 2) %>%
  arrange(desc(exposure_burden), desc(svi_overall))

write_csv(ej_priority, "environmental_justice_priority_counties.csv")
```

---

## PRIORITY VARIABLES SUMMARY

### Top 50 Variables Across 5 Sources (County × Year Where Applicable)

#### NOAA HMS Wildfire Smoke (12 variables):
1. Smoke days per year (total)
2. Heavy smoke days per year
3. Medium smoke days per year
4. Light smoke days per year
5. % of year with smoke present
6. Maximum consecutive smoke days
7. Summer smoke days (June-Sept)
8. Smoke season length (days)
9. Population-weighted smoke exposure days
10. First smoke day of year
11. Last smoke day of year
12. Smoke-free days

#### EPA Smart Location Database (15 variables):
13. National Walkability Index (0-20)
14. Gross activity density (pop + jobs/acre)
15. Employment-household entropy (land use mix)
16. Street intersection density
17. % 4-way intersections
18. Distance to nearest transit (meters)
19. Aggregate transit frequency
20. Jobs within 45-min auto
21. Jobs within 45-min transit
22. Population density
23. Employment density
24. Jobs-housing balance
25. % population within 0.5 mi transit
26. Auto-oriented intersection density
27. Pedestrian-oriented 4-way intersections

#### FHWA HPMS Traffic (13 variables):
28. Total annual VMT
29. VMT per capita
30. Truck VMT (annual)
31. Truck % of VMT
32. Interstate VMT
33. Arterial VMT
34. Road miles with AADT >10,000
35. Road miles with AADT >25,000
36. Population within 500m of AADT >25,000
37. % population near high-traffic roads
38. VMT-weighted average AADT
39. Total road miles
40. Road miles per capita

#### EPA RCRAInfo (5 variables):
41. Total RCRA facilities
42. Large Quantity Generators (LQG)
43. TSDFs (Treatment, Storage, Disposal)
44. Corrective Action sites
45. LQG per 10,000 population

#### EPA LMOP Landfills (5 variables):
46. Total MSW landfills
47. Open landfills
48. Closed landfills
49. Waste in place per capita (tons)
50. Population within 1 mile of landfill

---

## IMPLEMENTATION TIMELINE

### Phase 1: Easy Downloads (1 week)
- EPA Smart Location Database (direct download, block group → county aggregation)
- EPA LMOP Landfills (Excel download, county name → FIPS matching)

### Phase 2: GIS Processing (2-3 weeks)
- NOAA HMS Wildfire Smoke (daily shapefiles → annual county aggregation, ~7,300 files for 2005-2024)
- FHWA HPMS Traffic Volumes (road segments → county VMT aggregation)
- Near-road/facility population exposure (Census blocks + buffers)

### Phase 3: API/Database Queries (1-2 weeks)
- EPA RCRAInfo (Envirofacts API or bulk download)
- Integrate all sources into master county database

### Total Estimated Time: 4-6 weeks for complete implementation

---

**Documentation Version:** 1.0
**Last Updated:** November 12, 2025
**Next Update:** Add state tobacco retail licensing (Phase 2 documentation)
