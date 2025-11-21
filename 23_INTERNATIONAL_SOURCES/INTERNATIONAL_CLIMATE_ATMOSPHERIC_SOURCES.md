# International Climate & Atmospheric Data Sources
## High-Resolution Global Reanalysis + US-Specific Climate Data for County-Level Analysis

**Last Updated:** November 21, 2025
**Status:** NEW - Gap Analysis identified critical climate/atmospheric data sources
**Priority:** HIGHEST - Superior resolution and temporal coverage vs. NOAA NCEI station data

---

## EXECUTIVE SUMMARY

This document catalogs **international and US-specific high-resolution climate/atmospheric data sources** with US county coverage. These sources provide:

1. **Higher spatial resolution** than interpolated station data
2. **Higher temporal resolution** (hourly vs. daily)
3. **Gap-free coverage** (all counties, all time periods - no missing data from station outages)
4. **Additional variables** not available from US ground stations (soil moisture, solar radiation)

**CRITICAL FINDING:** For US counties, **PRISM/Daymet/GRIDMET are SUPERIOR to ERA5** due to:
- Higher resolution (1-4 km vs. 31 km)
- US-specific calibration with weather stations
- Topographic awareness (mountains, valleys)

**PRIORITY ORDER FOR US COUNTY ANALYSIS:**
1. **PRISM** (4km, 1981-present) - BEST for precipitation
2. **Daymet** (1km, 1980-present) - BEST for temperature (highest resolution)
3. **GRIDMET** (4km, 1979-present) - BEST for wind, humidity, evapotranspiration, fuel moisture
4. **ERA5/ERA5-Land** (31km/11km, 1940-present) - Use for hourly data, soil moisture, pre-1980 climate

**FREE/OPEN ACCESS:** All sources documented below are FREE and open-access ✅

---

## TABLE OF CONTENTS

### PART 1: US-SPECIFIC HIGH-RESOLUTION CLIMATE DATA (PRIORITY)
1. [PRISM Climate Group](#1-prism-climate-group)
2. [Daymet](#2-daymet)
3. [GRIDMET](#3-gridmet)

### PART 2: GLOBAL REANALYSIS (ECMWF)
4. [ERA5 Reanalysis](#4-era5-reanalysis)
5. [ERA5-Land](#5-era5-land)
6. [CAMS Atmospheric Composition](#6-cams-atmospheric-composition)

### PART 3: SATELLITE DATA (NASA/NOAA)
7. [MODIS/VIIRS/Sentinel-5P](#7-satellite-atmospheric-composition)

### PART 4: DATA COLLECTION WORKFLOWS
8. [County Aggregation Methods](#county-aggregation-methods)
9. [Derived Health Indicators](#derived-health-indicators)

---

## PART 1: US-SPECIFIC HIGH-RESOLUTION CLIMATE DATA

### 1. PRISM CLIMATE GROUP ⭐⭐⭐⭐⭐

**PRIORITY RANK: #1 for US County Precipitation**

#### **Overview**

**What:** Parameter-elevation Regressions on Independent Slopes Model
**Who:** Oregon State University PRISM Climate Group
**Resolution:** 4 km (~2.5 miles) OR 800m (high-resolution)
**Coverage:** Contiguous United States
**Temporal:** 1981-present (daily, monthly, 30-year normals)
**Update Frequency:** Daily data updated monthly (~1-2 month lag)

**Why PRISM is Gold Standard for US Precipitation:**
- Topographically-aware (accounts for elevation, rain shadows, orographic effects)
- Calibrates to 10,000+ weather stations + radar
- Widely used in ecology, agriculture, hydrology, health research
- More accurate than station-based interpolation or global reanalysis

#### **Variables Available**

**Core Variables (Daily):**
1. **Precipitation (ppt)** - mm
2. **Maximum temperature (tmax)** - °C
3. **Minimum temperature (tmin)** - °C
4. **Mean temperature (tmean)** - °C
5. **Dewpoint temperature (tdmean)** - °C
6. **Vapor pressure deficit (vpdmin, vpdmax)** - hPa

**Derived Variables:**
7. **Growing degree days (GDD)**
8. **Heating degree days (HDD)**
9. **Cooling degree days (CDD)**

**Monthly/Annual Aggregates:**
- All daily variables aggregated
- 30-year climate normals (1991-2020)

#### **Data Access**

**Portal:** https://prism.oregonstate.edu/

**Download Options:**

**1. Web Interface (Recent Data):**
- URL: https://prism.oregonstate.edu/recent/
- Format: BIL (raster), CSV (time series for point)
- Access: Free (registration required for bulk downloads)

**2. FTP Archive (Historical Data):**
- URL: https://prism.oregonstate.edu/documents/PRISM_downloads_FTP.pdf
- Access: FTP server (ftp://prism.nacse.org/daily/)
- Format: BIL rasters (zipped by year/month)

**3. PRISM Data Explorer (Interactive):**
- URL: https://prism.oregonstate.edu/explorer/
- Use: Download custom time series for point locations or regions

**4. API Access (via Google Earth Engine):**
- Dataset: `OREGONSTATE/PRISM/AN81d` (daily), `OREGONSTATE/PRISM/AN81m` (monthly)
- Access: Free via GEE

**5. R Package:**
```r
# Install prism package
install.packages("prism")
library(prism)

# Set download directory
options(prism.path = "~/prismtmp")

# Download daily data for date range
get_prism_dailys(type = "ppt", minDate = "2020-01-01", maxDate = "2020-12-31", keepZip = FALSE)
get_prism_dailys(type = "tmin", minDate = "2020-01-01", maxDate = "2020-12-31", keepZip = FALSE)
get_prism_dailys(type = "tmax", minDate = "2020-01-01", maxDate = "2020-12-31", keepZip = FALSE)

# Read rasters
ppt_20200101 <- pd_get_name(ls_prism_data()[1, ]) %>% prism_archive_subset()
ppt_raster <- raster(ppt_20200101)

# Extract to points (weather stations, county centroids)
library(sf)
library(terra)

counties <- st_read("cb_2020_us_county_500k.shp")
county_centroids <- st_centroid(counties)

# Extract PRISM values at county centroids
ppt_county <- terra::extract(rast(ppt_raster), vect(county_centroids), fun = mean, ID = FALSE)

counties$ppt_20200101 <- ppt_county
```

**6. Bulk Download (All Years):**
```bash
# Download all daily precipitation for 2020
wget --user=anonymous --password=your@email.com \
  ftp://prism.nacse.org/daily/ppt/2020/PRISM_ppt_stable_4kmD2_20200101_bil.zip

# Loop for entire year
for month in {01..12}; do
  for day in {01..31}; do
    wget --no-clobber ftp://prism.nacse.org/daily/ppt/2020/PRISM_ppt_stable_4kmD2_2020${month}${day}_bil.zip
  done
done
```

#### **County-Level Aggregation Workflow**

**Method 1: Zonal Statistics (Area-Weighted Mean)**

```r
library(sf)
library(terra)
library(tidyverse)
library(exactextractr)

# Load PRISM raster (daily precipitation 2020-01-01)
prism_ppt <- rast("PRISM_ppt_stable_4kmD2_20200101_bil.bil")

# Load county boundaries
counties <- st_read("tl_2020_us_county.shp")

# Project to PRISM CRS (NAD83)
counties_nad83 <- st_transform(counties, crs(prism_ppt))

# Extract mean precipitation for each county (area-weighted)
county_ppt <- exact_extract(prism_ppt, counties_nad83, fun = "mean")

counties$ppt_20200101_mm <- county_ppt

# Convert to imperial (inches) if needed
counties$ppt_20200101_in <- county_ppt / 25.4
```

**Method 2: Population-Weighted Mean (for Temperature)**

```r
# Load population grid (e.g., SEDAC GPW - NOTE: SEDAC terminated April 2025, archive-only)
# Alternative: LandScan or WorldPop for population data
population <- rast("gpw_v4_population_count_rev11_2020_30_sec.tif")

# Resample population to PRISM grid
population_prism <- resample(population, prism_tmax, method = "bilinear")

# Extract population-weighted temperature
county_tmax_popwt <- exact_extract(
  prism_tmax,
  counties_nad83,
  weights = population_prism,
  fun = "weighted_mean"
)

counties$tmax_20200101_popwt <- county_tmax_popwt
```

**Method 3: Process Entire Year → Annual County Statistics**

```r
# Function to process one day
process_prism_day <- function(date, variable = "ppt", counties_sf) {

  # Load raster
  date_str <- format(date, "%Y%m%d")
  file_path <- sprintf("PRISM_%s_stable_4kmD2_%s_bil.bil", variable, date_str)

  if (!file.exists(file_path)) {
    return(NULL)
  }

  prism_raster <- rast(file_path)

  # Extract to counties
  county_values <- exact_extract(prism_raster, counties_sf, fun = "mean")

  data.frame(
    GEOID = counties_sf$GEOID,
    date = date,
    variable = variable,
    value = county_values
  )
}

# Process entire year
dates_2020 <- seq(as.Date("2020-01-01"), as.Date("2020-12-31"), by = "day")

prism_2020_daily <- map_dfr(dates_2020, ~process_prism_day(.x, "ppt", counties_nad83))

# Calculate annual statistics
prism_2020_annual <- prism_2020_daily %>%
  group_by(GEOID) %>%
  summarize(
    # Precipitation
    total_precip_mm = sum(value, na.rm = TRUE),
    mean_daily_precip_mm = mean(value, na.rm = TRUE),
    days_with_precip = sum(value > 1, na.rm = TRUE), # >1mm = rainy day
    max_daily_precip_mm = max(value, na.rm = TRUE),

    # Drought indicators
    consecutive_dry_days_max = max(rle(value < 1)$lengths[rle(value < 1)$values]),

    .groups = "drop"
  )
```

#### **Derived Health Indicators from PRISM**

**Heat Exposure:**
```r
# Calculate heat wave days (tmax > 95°F = 35°C)
prism_tmax_2020 <- map_dfr(dates_2020, ~process_prism_day(.x, "tmax", counties))

heat_exposure <- prism_tmax_2020 %>%
  group_by(GEOID) %>%
  summarize(
    days_over_95F = sum(value > 35, na.rm = TRUE),
    days_over_100F = sum(value > 37.8, na.rm = TRUE),
    days_over_105F = sum(value > 40.6, na.rm = TRUE),

    # Heat wave definition: 3+ consecutive days >95°F
    heat_wave_events = count_heat_waves(value, threshold = 35, duration = 3),

    .groups = "drop"
  )
```

**Cold Exposure:**
```r
# Calculate cold snap days
cold_exposure <- prism_tmin_2020 %>%
  group_by(GEOID) %>%
  summarize(
    days_below_32F = sum(value < 0, na.rm = TRUE),
    days_below_20F = sum(value < -6.7, na.rm = TRUE),
    days_below_0F = sum(value < -17.8, na.rm = TRUE),

    # Cold snap: 3+ consecutive days <32°F
    cold_snap_events = count_cold_snaps(value, threshold = 0, duration = 3),

    .groups = "drop"
  )
```

**Drought Exposure:**
```r
# Standardized Precipitation Index (SPI) - requires multiple years
# Or simple drought metrics
drought <- prism_ppt_2020 %>%
  group_by(GEOID) %>%
  summarize(
    max_consecutive_dry_days = max(rle(value < 1)$lengths[rle(value < 1)$values]),
    pct_days_dry = mean(value < 1) * 100,
    .groups = "drop"
  )
```

#### **Data Quality & Limitations**

**Strengths:**
- ✅ Topographically-aware (accounts for mountains, rain shadows)
- ✅ High resolution (4 km)
- ✅ Daily temporal resolution
- ✅ Calibrated to 10,000+ weather stations
- ✅ Gap-free (no missing data)
- ✅ Long time series (1981-present, 43+ years)
- ✅ FREE for research use

**Limitations:**
- ⚠️ US contiguous only (no Alaska, Hawaii, territories)
- ⚠️ 1-2 month lag for daily data (not near-real-time)
- ⚠️ Fewer variables than ERA5 (no wind, solar radiation, soil moisture)
- ⚠️ Requires spatial processing (not pre-aggregated to counties)

**Validation:**
- PRISM precipitation correlates r > 0.95 with station observations
- Temperature correlates r > 0.98
- Best performance in complex terrain (mountains)

#### **Disease Associations**

**Precipitation → Health:**
- Flooding exposure (extreme precipitation events)
- Waterborne disease outbreaks (heavy rainfall → runoff contamination)
- Vector-borne disease (mosquito breeding habitats)
- Drought → dust exposure (PM10), agricultural stress

**Temperature → Health:**
- Heat waves → cardiovascular mortality, heat stroke, renal disease
- Cold snaps → hypothermia, cardiovascular events
- Diurnal temperature range → cardiovascular stress
- Growing degree days → agricultural productivity, food security

**Priority Variables for Health Observatory:**
1. Annual total precipitation (mm)
2. Days with >95°F maximum temperature
3. Days with <32°F minimum temperature
4. Heat wave events (3+ consecutive days >95°F)
5. Cold snap events (3+ consecutive days <32°F)
6. Maximum consecutive dry days (drought)
7. Days with >2 inches precipitation (flooding risk)
8. Growing degree days (base 50°F)
9. Cooling degree days (base 65°F)
10. Heating degree days (base 65°F)

---

### 2. DAYMET ⭐⭐⭐⭐⭐

**PRIORITY RANK: #2 for US County Temperature (Highest Resolution)**

#### **Overview**

**What:** Daily Surface Weather Data on 1-km Grid for North America
**Who:** NASA ORNL DAAC (Oak Ridge National Laboratory)
**Resolution:** 1 km (~0.6 miles) - HIGHEST RESOLUTION
**Coverage:** North America (US + Canada + Mexico)
**Temporal:** 1980-present (daily)
**Update Frequency:** Annual (typically 6-9 month lag)

**Why Daymet is Best for Temperature:**
- **1 km resolution** (finest for US)
- Alaska + Hawaii + Puerto Rico included (unlike PRISM)
- Elevation-aware
- Widely used in ecological and health research

#### **Variables Available**

**Daily Variables:**
1. **Day length (dayl)** - seconds
2. **Precipitation (prcp)** - mm/day
3. **Shortwave radiation (srad)** - W/m²
4. **Snow water equivalent (swe)** - kg/m²
5. **Maximum temperature (tmax)** - °C
6. **Minimum temperature (tmin)** - °C
7. **Vapor pressure (vp)** - Pa

#### **Data Access**

**Portal:** https://daymet.ornl.gov/

**Download Options:**

**1. Single Pixel Tool (Point Data):**
- URL: https://daymet.ornl.gov/single-pixel/
- Use: Download time series for specific lat/lon (e.g., county centroids)
- Format: CSV

**2. Spatial Data Download:**
- URL: https://daymet.ornl.gov/getdata/
- Format: NetCDF (daily, monthly, annual)
- Access: Free, direct download or via THREDDS

**3. THREDDS Data Server (Programmatic Access):**
- URL: https://thredds.daac.ornl.gov/thredds/catalog/ornldaac/2129/catalog.html
- Protocol: OPeNDAP, HTTPServer
- Use: Download specific spatial/temporal subsets

**4. R Package (daymetr):**
```r
install.packages("daymetr")
library(daymetr)
library(tidyverse)

# Download single pixel (county centroid)
daymet_point <- download_daymet(
  site = "Cook County IL",
  lat = 41.8781,
  lon = -87.6298,
  start = 2020,
  end = 2020,
  internal = TRUE
)

# Download spatial tile (covers multiple counties)
download_daymet_tiles(
  location = c(41, -88), # lat, lon
  start = 2020,
  end = 2020,
  param = c("tmin", "tmax", "prcp"),
  path = "~/daymet/"
)
```

**5. Google Earth Engine:**
```javascript
// Daymet V4 in GEE
var daymet = ee.ImageCollection("NASA/ORNL/DAYMET_V4")
  .filterDate('2020-01-01', '2020-12-31')
  .select(['tmax', 'tmin', 'prcp']);

// Calculate annual mean for counties
var counties = ee.FeatureCollection("TIGER/2020/Counties");

var daymet_annual = daymet.mean();

var county_daymet = daymet_annual.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 1000 // 1 km
});

Export.table.toDrive({
  collection: county_daymet,
  description: 'daymet_county_2020',
  fileFormat: 'CSV'
});
```

#### **County-Level Aggregation**

**Method 1: Extract to County Centroids (Fast)**

```r
library(daymetr)
library(sf)
library(tidyverse)

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>%
  st_transform(4326) # WGS84

# Get centroids
county_centroids <- counties %>%
  st_centroid() %>%
  mutate(
    lon = st_coordinates(.)[,1],
    lat = st_coordinates(.)[,2]
  )

# Download Daymet for all county centroids (2020)
daymet_county <- county_centroids %>%
  st_drop_geometry() %>%
  mutate(
    daymet_data = pmap(list(GEOID, lat, lon), function(id, lat, lon) {
      tryCatch({
        download_daymet(
          site = id,
          lat = lat,
          lon = lon,
          start = 2020,
          end = 2020,
          internal = TRUE,
          silent = TRUE
        )$data
      }, error = function(e) NULL)
    })
  )

# Calculate annual statistics
daymet_annual <- daymet_county %>%
  unnest(daymet_data) %>%
  group_by(GEOID) %>%
  summarize(
    # Temperature
    mean_tmax = mean(tmax..deg.c., na.rm = TRUE),
    mean_tmin = mean(tmin..deg.c., na.rm = TRUE),
    mean_tmean = (mean_tmax + mean_tmin) / 2,

    # Extremes
    max_tmax = max(tmax..deg.c., na.rm = TRUE),
    min_tmin = min(tmin..deg.c., na.rm = TRUE),

    # Heat/cold days
    days_tmax_over_35C = sum(tmax..deg.c. > 35, na.rm = TRUE),
    days_tmin_below_0C = sum(tmin..deg.c. < 0, na.rm = TRUE),

    # Precipitation
    total_prcp_mm = sum(prcp..mm.day., na.rm = TRUE),

    # Radiation/day length
    mean_srad = mean(srad..W.m.2., na.rm = TRUE),
    mean_dayl_hours = mean(dayl..s.) / 3600,

    .groups = "drop"
  )
```

**Method 2: Zonal Statistics from Rasters (More Accurate)**

```r
library(terra)
library(exactextractr)

# Load Daymet NetCDF
daymet_tmax <- rast("daymet_v4_daily_na_tmax_2020.nc")

# Counties
counties <- st_read("tl_2020_us_county.shp") %>%
  st_transform(crs(daymet_tmax))

# Extract mean for each county (area-weighted)
county_tmax_mean <- exact_extract(daymet_tmax, counties, fun = "mean")

# Can also extract:
# - max (county maximum temperature)
# - min (county minimum temperature)
# - quantile(probs = 0.95) (95th percentile - heat exposure)
```

#### **Derived Health Indicators**

**Heat Index (Combination of Temperature + Humidity):**
```r
# Calculate vapor pressure deficit (VPD)
# VPD = saturation vapor pressure - actual vapor pressure
# Daymet provides vapor pressure (vp), can derive VPD

# Heat index requires relative humidity (not directly in Daymet)
# Can approximate with:
# RH ≈ (actual vp / saturation vp) * 100

# Saturation vapor pressure (Tetens equation)
calc_svp <- function(temp_C) {
  0.611 * exp((17.27 * temp_C) / (temp_C + 237.3)) # kPa
}

daymet_heat_index <- daymet_county %>%
  unnest(daymet_data) %>%
  mutate(
    # Convert vapor pressure Pa → kPa
    vp_kPa = vp..Pa. / 1000,

    # Saturation vapor pressure at tmax
    svp_kPa = calc_svp(tmax..deg.c.),

    # Relative humidity (%)
    rh = (vp_kPa / svp_kPa) * 100,
    rh = pmin(rh, 100), # Cap at 100%

    # Heat index (NOAA equation, valid for T>80°F, RH>40%)
    temp_F = tmax..deg.c. * 9/5 + 32,
    heat_index_F = ifelse(
      temp_F > 80 & rh > 40,
      -42.379 + 2.04901523*temp_F + 10.14333127*rh - 0.22475541*temp_F*rh -
        0.00683783*temp_F^2 - 0.05481717*rh^2 + 0.00122874*temp_F^2*rh +
        0.00085282*temp_F*rh^2 - 0.00000199*temp_F^2*rh^2,
      temp_F # No heat index if conditions not met
    ),
    heat_index_C = (heat_index_F - 32) * 5/9
  )

# Heat index >105°F = extreme danger
heat_index_days <- daymet_heat_index %>%
  group_by(GEOID) %>%
  summarize(
    days_heat_index_over_105F = sum(heat_index_F > 105, na.rm = TRUE),
    days_heat_index_over_103F = sum(heat_index_F > 103, na.rm = TRUE),
    .groups = "drop"
  )
```

#### **Data Quality**

**Strengths:**
- ✅ Highest resolution (1 km)
- ✅ Alaska, Hawaii, Puerto Rico included
- ✅ Solar radiation, day length (not in PRISM)
- ✅ Snow water equivalent (winter health impacts)
- ✅ Long time series (1980-present, 44 years)
- ✅ FREE

**Limitations:**
- ⚠️ Fewer variables than ERA5 (no soil moisture, wind)
- ⚠️ 6-9 month lag (2023 data available mid-2024)
- ⚠️ Requires spatial processing

**When to Use Daymet vs. PRISM:**
- **Temperature:** Daymet (1 km > PRISM 4 km)
- **Precipitation:** PRISM (better topographic correction)
- **Alaska/Hawaii:** Daymet ONLY (PRISM doesn't cover)
- **Solar radiation, snow:** Daymet ONLY (not in PRISM)

**Priority Variables:**
1. Mean annual temperature
2. Days with tmax >35°C (95°F)
3. Days with tmin <0°C (32°F)
4. Heat index days >105°F
5. Diurnal temperature range (tmax - tmin)
6. Total precipitation (mm)
7. Annual solar radiation (W/m²)
8. Snow water equivalent peak (kg/m²)
9. Day length variation (seasonal affective disorder proxy)
10. Vapor pressure deficit (drought stress)

---

### 3. GRIDMET ⭐⭐⭐⭐⭐

**PRIORITY RANK: #3 for US County Wind, Humidity, Evapotranspiration**

#### **Overview**

**What:** Gridded Surface Meteorological Dataset
**Who:** University of Idaho
**Resolution:** 4 km (~2.5 miles)
**Coverage:** Contiguous United States
**Temporal:** 1979-present (daily)
**Update Frequency:** Near-real-time (1-2 day lag)

**Why GRIDMET is Critical:**
- **Wind speed/direction** (not in PRISM or Daymet)
- **Reference evapotranspiration (ET0)** - agricultural drought
- **Fuel moisture** - wildfire risk
- **Near-real-time** (fastest updates)
- **Longest time series** (1979-present, 45+ years)

#### **Variables Available**

**Daily Variables (10 total):**
1. **Precipitation (pr)** - mm
2. **Maximum temperature (tmmx)** - K
3. **Minimum temperature (tmmn)** - K
4. **Maximum relative humidity (rmax)** - %
5. **Minimum relative humidity (rmin)** - %
6. **Wind speed at 10m (vs)** - m/s
7. **Wind direction at 10m (th)** - degrees
8. **Shortwave solar radiation (srad)** - W/m²
9. **Specific humidity (sph)** - kg/kg
10. **Reference evapotranspiration (ET0, pet)** - mm (ASCE Penman-Monteith)

**Derived Variables:**
11. **Vapor pressure deficit (vpd)** - kPa
12. **Burning index (bi)** - unitless (wildfire intensity proxy)
13. **Energy release component (erc)** - unitless (wildfire fuel energy)
14. **100-hour dead fuel moisture (fm100)** - %
15. **1000-hour dead fuel moisture (fm1000)** - %

#### **Data Access**

**Portal:** http://www.climatologylab.org/gridmet.html

**Download Options:**

**1. THREDDS Data Server (Direct Download):**
- URL: http://thredds.northwestknowledge.net:8080/thredds/catalog/MET/catalog.html
- Format: NetCDF (by variable, by year)
- Example: `http://thredds.northwestknowledge.net:8080/thredds/fileServer/MET/tmmx/tmmx_2020.nc`

**2. OPeNDAP (Programmatic Subsetting):**
- URL: Same THREDDS server
- Protocol: OPeNDAP
- Use: Download specific spatial/temporal subsets (faster than full NetCDF)

**3. Google Earth Engine:**
```javascript
// GRIDMET in GEE
var gridmet = ee.ImageCollection("IDAHO_EPSCOR/GRIDMET")
  .filterDate('2020-01-01', '2020-12-31');

// Select variables
var tmax = gridmet.select('tmmx'); // K
var wind = gridmet.select('vs'); // m/s
var et0 = gridmet.select('etr'); // mm

// Annual mean for counties
var counties = ee.FeatureCollection("TIGER/2020/Counties");

var gridmet_annual = gridmet.mean();

var county_gridmet = gridmet_annual.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 4000 // 4 km
});

Export.table.toDrive({
  collection: county_gridmet,
  description: 'gridmet_county_2020'
});
```

**4. R Direct Download:**
```r
library(tidyverse)
library(terra)
library(ncdf4)

# Download GRIDMET tmax for 2020
download.file(
  "http://thredds.northwestknowledge.net:8080/thredds/fileServer/MET/tmmx/tmmx_2020.nc",
  destfile = "gridmet_tmmx_2020.nc"
)

# Load raster
gridmet_tmax <- rast("gridmet_tmmx_2020.nc")

# Note: GRIDMET uses EPSG:4326 (WGS84)
# Convert Kelvin to Celsius
gridmet_tmax_C <- gridmet_tmax - 273.15
```

#### **County-Level Aggregation**

**Method 1: Zonal Statistics (Annual Mean)**

```r
library(sf)
library(terra)
library(exactextractr)
library(tidyverse)

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>%
  st_transform(4326) # WGS84

# Load GRIDMET variables for 2020
variables <- c("tmmx", "tmmn", "pr", "vs", "etr", "vpd")

gridmet_county_2020 <- map_dfr(variables, function(var) {

  # Download variable
  url <- sprintf("http://thredds.northwestknowledge.net:8080/thredds/fileServer/MET/%s/%s_2020.nc", var, var)
  nc_file <- sprintf("gridmet_%s_2020.nc", var)

  if (!file.exists(nc_file)) {
    download.file(url, nc_file)
  }

  # Load raster (365 or 366 layers = daily)
  gridmet_raster <- rast(nc_file)

  # Calculate annual mean
  gridmet_annual_mean <- mean(gridmet_raster, na.rm = TRUE)

  # Extract to counties
  county_values <- exact_extract(gridmet_annual_mean, counties, fun = "mean")

  data.frame(
    GEOID = counties$GEOID,
    variable = var,
    value = county_values
  )
})

# Pivot wider
gridmet_county_wide <- gridmet_county_2020 %>%
  pivot_wider(names_from = variable, values_from = value)

# Convert units
gridmet_county_wide <- gridmet_county_wide %>%
  mutate(
    tmax_C = tmmx - 273.15,
    tmin_C = tmmn - 273.15,
    precip_mm = pr,
    wind_ms = vs,
    et0_mm = etr,
    vpd_kPa = vpd / 1000
  ) %>%
  select(-tmmx, -tmmn, -pr, -vs, -etr, -vpd)
```

**Method 2: Daily Statistics → Annual Extremes**

```r
# Function to process daily GRIDMET
process_gridmet_daily <- function(variable, year, counties_sf) {

  # Download
  url <- sprintf("http://thredds.northwestknowledge.net:8080/thredds/fileServer/MET/%s/%s_%d.nc",
                 variable, variable, year)
  nc_file <- sprintf("gridmet_%s_%d.nc", variable, year)

  download.file(url, nc_file)

  # Load raster (daily layers)
  gridmet_daily <- rast(nc_file)

  # Extract to counties (area-weighted mean for each day)
  county_daily <- exact_extract(gridmet_daily, counties_sf, fun = "mean")

  # Convert to data frame
  dates <- seq(as.Date(sprintf("%d-01-01", year)), as.Date(sprintf("%d-12-31", year)), by = "day")

  county_daily_df <- as.data.frame(county_daily) %>%
    mutate(GEOID = counties_sf$GEOID) %>%
    pivot_longer(-GEOID, names_to = "layer", values_to = "value") %>%
    mutate(
      day_of_year = as.numeric(str_extract(layer, "\\d+")),
      date = dates[day_of_year]
    ) %>%
    select(GEOID, date, value)

  return(county_daily_df)
}

# Process tmax daily for 2020
tmax_daily_2020 <- process_gridmet_daily("tmmx", 2020, counties)

# Calculate annual statistics
tmax_annual <- tmax_daily_2020 %>%
  mutate(value_C = value - 273.15) %>%
  group_by(GEOID) %>%
  summarize(
    mean_tmax = mean(value_C, na.rm = TRUE),
    max_tmax = max(value_C, na.rm = TRUE),
    min_tmax = min(value_C, na.rm = TRUE),

    # Heat days
    days_over_35C = sum(value_C > 35, na.rm = TRUE),
    days_over_38C = sum(value_C > 38, na.rm = TRUE),
    days_over_40C = sum(value_C > 40, na.rm = TRUE),

    # Heat waves (3+ consecutive days >35°C)
    heat_wave_events = count_heat_waves(value_C, threshold = 35, duration = 3),

    .groups = "drop"
  )
```

#### **Derived Health Indicators from GRIDMET**

**1. Agricultural Drought (Crop Stress):**
```r
# Reference ET (etr) > Precipitation = water deficit

gridmet_drought <- gridmet_county_2020 %>%
  group_by(GEOID) %>%
  summarize(
    annual_et0_mm = sum(etr, na.rm = TRUE),
    annual_precip_mm = sum(pr, na.rm = TRUE),
    water_deficit_mm = annual_et0_mm - annual_precip_mm,
    aridity_index = annual_et0_mm / annual_precip_mm,
    .groups = "drop"
  )

# Aridity index >1 = water deficit (demand > supply)
# AI >2 = severe drought
```

**2. Wildfire Risk:**
```r
# Download fire weather variables
fire_vars <- c("bi", "erc", "fm100", "fm1000")

gridmet_fire <- map_dfr(fire_vars, function(var) {
  process_gridmet_daily(var, 2020, counties) %>%
    group_by(GEOID) %>%
    summarize(
      "{var}_mean" := mean(value, na.rm = TRUE),
      "{var}_max" := max(value, na.rm = TRUE),
      "{var}_p95" := quantile(value, 0.95, na.rm = TRUE),
      .groups = "drop"
    )
})

# High fire risk days
fire_risk_days <- gridmet_fire %>%
  mutate(
    high_fire_risk_days = erc_p95 > 80, # ERC >80 = high risk
    extreme_fire_risk_days = erc_p95 > 95 # ERC >95 = extreme
  )
```

**3. Wind Exposure (Dust, Pollen Dispersal):**
```r
# Download wind speed
wind_daily <- process_gridmet_daily("vs", 2020, counties)

wind_exposure <- wind_daily %>%
  group_by(GEOID) %>%
  summarize(
    mean_wind_speed_ms = mean(value, na.rm = TRUE),
    max_wind_speed_ms = max(value, na.rm = TRUE),

    # High wind days (>10 m/s = 22 mph)
    days_wind_over_10ms = sum(value > 10, na.rm = TRUE),

    # Dust storm potential (wind >15 m/s = 34 mph)
    days_wind_over_15ms = sum(value > 15, na.rm = TRUE),

    .groups = "drop"
  )
```

#### **Data Quality**

**Strengths:**
- ✅ **Wind speed/direction** - UNIQUE (not in PRISM/Daymet)
- ✅ **Evapotranspiration** - agricultural drought, water stress
- ✅ **Fuel moisture** - wildfire risk
- ✅ **Near-real-time** (1-2 day lag)
- ✅ **Longest time series** (1979-present, 45+ years)
- ✅ FREE

**Limitations:**
- ⚠️ Contiguous US only (no Alaska, Hawaii)
- ⚠️ 4 km resolution (lower than Daymet 1 km)
- ⚠️ No soil moisture (use ERA5-Land for this)

**When to Use GRIDMET:**
- Wind exposure (dust storms, pollen, air pollution dispersion)
- Agricultural drought (ET0, water deficit)
- Wildfire risk (fuel moisture, burning index)
- Rapid temperature changes (cardiovascular triggers)

**Priority Variables:**
1. Mean annual wind speed
2. Days with wind >10 m/s (high wind)
3. Reference evapotranspiration (ET0, mm)
4. Water deficit (ET0 - precipitation)
5. Vapor pressure deficit (plant/human stress)
6. 100-hour fuel moisture (wildfire risk)
7. Energy release component (ERC, fire intensity)
8. Days with high fire risk (ERC >80)
9. Relative humidity minimum (respiratory health)
10. Solar radiation (vitamin D proxy)

---

## SUMMARY: US-SPECIFIC CLIMATE DATA HIERARCHY

**For US County Health Analysis, Use:**

1. **Temperature:**
   - **Daymet** (1 km, highest resolution) for all US states including Alaska/Hawaii
   - OR **PRISM** (4 km) for contiguous US if Daymet unavailable

2. **Precipitation:**
   - **PRISM** (4 km, best topographic correction) for contiguous US
   - **Daymet** (1 km) for Alaska/Hawaii

3. **Wind, Humidity, ET:**
   - **GRIDMET** (4 km, ONLY source) for contiguous US

4. **Solar Radiation:**
   - **Daymet** (1 km) OR **GRIDMET** (4 km)

5. **Snow:**
   - **Daymet** (snow water equivalent)

6. **Hourly Data, Soil Moisture, Pre-1980:**
   - **ERA5/ERA5-Land** (see Part 2 below)

**ALL THREE (PRISM + Daymet + GRIDMET) ARE FREE AND SHOULD BE PRIORITIZED OVER ERA5 FOR US COUNTIES.**

---

## PART 2: GLOBAL REANALYSIS (ECMWF)

### 4. ERA5 REANALYSIS ⭐⭐⭐⭐

**PRIORITY RANK: #4 for US Counties (Use for Hourly Data, Soil Moisture, Pre-1980)**

#### **Overview**

**What:** Fifth generation ECMWF atmospheric reanalysis
**Who:** European Centre for Medium-Range Weather Forecasts (ECMWF)
**Resolution:** 31 km (~0.25° × 0.25° lat/lon)
**Coverage:** Global
**Temporal:** 1940-present (hourly)
**Update Frequency:** Daily (5-day lag for near-real-time)

**Why Use ERA5 for US Counties:**
- **Hourly temporal resolution** (PRISM/Daymet/GRIDMET are daily)
- **Soil moisture** (4 layers, not available in US sources)
- **Pre-1980 climate** (extends back to 1940, GRIDMET starts 1979)
- **100+ variables** (comprehensive atmospheric/land variables)
- **Gap-filling** for non-US territories (Caribbean, Pacific)

**When NOT to Use ERA5:**
- For daily/monthly temperature/precipitation → Use PRISM/Daymet (higher resolution)
- For wind/ET in contiguous US → Use GRIDMET (higher resolution)

#### **Variables Available**

### 📋 COMPLETE ERA5 VARIABLE CATALOG (TIER 2)

**For the complete catalog of all 240 ERA5 atmospheric reanalysis variables organized by category (surface, pressure levels, single-level forecast, etc.) with parameter IDs, units, and descriptions, see:**

**[ERA5_COMPLETE_VARIABLE_CATALOG.md](ERA5_COMPLETE_VARIABLE_CATALOG.md)**

This companion Tier 2 catalog provides:
- All 240 ERA5 variables with official ECMWF parameter names and IDs
- Organized by parameter type (instantaneous, accumulated, pressure-level)
- Complete units and descriptions
- CDS API query examples for county-level data extraction
- Pressure-level variables (16 variables × 37 vertical levels)
- Python/R code for downloading and aggregating to US counties

**Use this document (Tier 1)** for ERA5 overview, priority variables, and when to use ERA5 vs. US-specific sources.
**Use ERA5_COMPLETE_VARIABLE_CATALOG.md (Tier 2)** to look up specific ERA5 parameter codes or browse the complete variable catalog.

**Atmospheric Variables (100+):**

**Surface Temperature & Humidity:**
1. **2m temperature** - K
2. **2m dewpoint temperature** - K
3. **Skin temperature** - K
4. **Surface pressure** - Pa
5. **10m u-component of wind** - m/s
6. **10m v-component of wind** - m/s

**Precipitation & Radiation:**
7. **Total precipitation** - m
8. **Convective precipitation** - m
9. **Surface solar radiation downwards** - J/m²
10. **Surface thermal radiation downwards** - J/m²
11. **Total cloud cover** - fraction

**Soil Variables (UNIQUE - not in PRISM/Daymet/GRIDMET):**
12. **Volumetric soil moisture layer 1** (0-7 cm) - m³/m³
13. **Volumetric soil moisture layer 2** (7-28 cm) - m³/m³
14. **Volumetric soil moisture layer 3** (28-100 cm) - m³/m³
15. **Volumetric soil moisture layer 4** (100-289 cm) - m³/m³
16. **Soil temperature layer 1-4** - K

**Evaporation & Runoff:**
17. **Evaporation** - m
18. **Potential evaporation** - m
19. **Runoff** - m
20. **Surface runoff** - m
21. **Sub-surface runoff** - m

**Snow:**
22. **Snow depth** - m
23. **Snow albedo** - fraction
24. **Snowfall** - m water equivalent
25. **Snowmelt** - m water equivalent

**Pressure Level Variables (37 levels, surface to 1 hPa):**
- Temperature, geopotential, wind components, relative humidity, specific humidity, etc.

**Full Variable List:** https://confluence.ecmwf.int/display/CKB/ERA5%3A+data+documentation

#### **Data Access**

**Portal:** https://cds.climate.copernicus.eu/

**Download Options:**

**1. Copernicus Climate Data Store (CDS):**
- URL: https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels
- Format: NetCDF, GRIB
- Access: FREE (registration required)
- Download limit: ~1000 requests/day

**2. CDS API (Python):**
```python
import cdsapi

c = cdsapi.Client()

# Download ERA5 2m temperature for 2020 (hourly, US bounding box)
c.retrieve(
    'reanalysis-era5-single-levels',
    {
        'product_type': 'reanalysis',
        'variable': ['2m_temperature', '10m_u_component_of_wind', '10m_v_component_of_wind',
                     'total_precipitation', 'volumetric_soil_water_layer_1'],
        'year': '2020',
        'month': ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'],
        'day': ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10',
                '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
                '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31'],
        'time': ['00:00', '01:00', '02:00', '03:00', '04:00', '05:00',
                 '06:00', '07:00', '08:00', '09:00', '10:00', '11:00',
                 '12:00', '13:00', '14:00', '15:00', '16:00', '17:00',
                 '18:00', '19:00', '20:00', '21:00', '22:00', '23:00'],
        'area': [49, -125, 24, -66],  # North, West, South, East (contiguous US)
        'format': 'netcdf',
    },
    'era5_us_2020.nc'
)
```

**3. Google Earth Engine:**
```javascript
// ERA5 Hourly in GEE
var era5 = ee.ImageCollection("ECMWF/ERA5/DAILY")
  .filterDate('2020-01-01', '2020-12-31');

// Select variables
var temp = era5.select('mean_2m_air_temperature'); // K
var precip = era5.select('total_precipitation'); // m

// Annual mean for counties
var counties = ee.FeatureCollection("TIGER/2020/Counties");

var era5_annual = era5.mean();

var county_era5 = era5_annual.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 27830 // ~31 km
});

Export.table.toDrive({
  collection: county_era5,
  description: 'era5_county_2020',
  fileFormat: 'CSV'
});
```

**4. AWS Registry of Open Data:**
- URL: https://registry.opendata.aws/ecmwf-era5/
- Access: S3 bucket `s3://era5-pds/`
- Format: Zarr (cloud-optimized)

**5. R (via ecmwfr package):**
```r
install.packages("ecmwfr")
library(ecmwfr)
library(terra)

# Set CDS credentials
wf_set_key(user = "YOUR_UID", key = "YOUR_API_KEY", service = "cds")

# Define request
request <- list(
  product_type = "reanalysis",
  variable = c("2m_temperature", "total_precipitation", "volumetric_soil_water_layer_1"),
  year = "2020",
  month = sprintf("%02d", 1:12),
  day = sprintf("%02d", 1:31),
  time = sprintf("%02d:00", 0:23),
  area = c(49, -125, 24, -66),  # N, W, S, E
  format = "netcdf",
  dataset_short_name = "reanalysis-era5-single-levels",
  target = "era5_us_2020.nc"
)

# Submit request (will take time to process on CDS servers)
file <- wf_request(user = "YOUR_UID", request = request, transfer = TRUE, path = "~/era5/")
```

#### **County-Level Aggregation**

**Method 1: Extract Hourly → Daily → Annual**

```r
library(terra)
library(exactextractr)
library(tidyverse)
library(sf)

# Load ERA5 NetCDF (hourly 2m temperature for 2020)
era5_t2m <- rast("era5_us_2020_t2m.nc")

# Note: ERA5 has 8,760 layers (365 days × 24 hours) or 8,784 (leap year)

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>%
  st_transform(4326) # ERA5 is in WGS84

# Extract mean for each county (hourly)
county_t2m_hourly <- exact_extract(era5_t2m, counties, fun = "mean")

# Convert to data frame
dates_hours <- seq(as.POSIXct("2020-01-01 00:00:00", tz = "UTC"),
                   as.POSIXct("2020-12-31 23:00:00", tz = "UTC"),
                   by = "hour")

county_t2m_df <- as.data.frame(county_t2m_hourly) %>%
  mutate(GEOID = counties$GEOID) %>%
  pivot_longer(-GEOID, names_to = "layer", values_to = "temp_K") %>%
  mutate(
    hour_index = as.numeric(str_extract(layer, "\\d+")),
    datetime = dates_hours[hour_index],
    temp_C = temp_K - 273.15
  )

# Calculate daily statistics
county_t2m_daily <- county_t2m_df %>%
  mutate(date = as.Date(datetime)) %>%
  group_by(GEOID, date) %>%
  summarize(
    tmax = max(temp_C, na.rm = TRUE),
    tmin = min(temp_C, na.rm = TRUE),
    tmean = mean(temp_C, na.rm = TRUE),
    .groups = "drop"
  )

# Calculate annual statistics
county_t2m_annual <- county_t2m_daily %>%
  group_by(GEOID) %>%
  summarize(
    mean_annual_temp = mean(tmean, na.rm = TRUE),
    days_over_35C = sum(tmax > 35, na.rm = TRUE),
    days_below_0C = sum(tmin < 0, na.rm = TRUE),
    .groups = "drop"
  )
```

**Method 2: Soil Moisture (UNIQUE to ERA5)**

```r
# Load ERA5 volumetric soil moisture layer 1 (0-7 cm)
era5_soil <- rast("era5_us_2020_soil_moisture_layer1.nc")

# Extract to counties (hourly → daily mean → annual statistics)
county_soil_hourly <- exact_extract(era5_soil, counties, fun = "mean")

# Convert to data frame
county_soil_df <- as.data.frame(county_soil_hourly) %>%
  mutate(GEOID = counties$GEOID) %>%
  pivot_longer(-GEOID, names_to = "layer", values_to = "soil_moisture_m3m3") %>%
  mutate(
    hour_index = as.numeric(str_extract(layer, "\\d+")),
    datetime = dates_hours[hour_index],
    date = as.Date(datetime)
  )

# Daily mean soil moisture
county_soil_daily <- county_soil_df %>%
  group_by(GEOID, date) %>%
  summarize(soil_moisture = mean(soil_moisture_m3m3, na.rm = TRUE), .groups = "drop")

# Annual statistics
county_soil_annual <- county_soil_daily %>%
  group_by(GEOID) %>%
  summarize(
    mean_soil_moisture = mean(soil_moisture, na.rm = TRUE),
    min_soil_moisture = min(soil_moisture, na.rm = TRUE),
    days_soil_drought = sum(soil_moisture < 0.15, na.rm = TRUE), # <0.15 = drought
    .groups = "drop"
  )
```

#### **Derived Health Indicators from ERA5**

**1. Hourly Temperature Extremes (Circadian Disruption):**
```r
# Calculate diurnal temperature range at hourly resolution
county_hourly_temp <- county_t2m_df %>%
  mutate(date = as.Date(datetime), hour = hour(datetime)) %>%
  group_by(GEOID, date) %>%
  summarize(
    temp_3am = temp_C[hour == 3],     # Coolest hour
    temp_3pm = temp_C[hour == 15],    # Warmest hour
    diurnal_range = max(temp_C) - min(temp_C),
    .groups = "drop"
  )

# Annual statistics
county_temp_circadian <- county_hourly_temp %>%
  group_by(GEOID) %>%
  summarize(
    mean_diurnal_range = mean(diurnal_range, na.rm = TRUE),
    days_high_diurnal_range = sum(diurnal_range > 20, na.rm = TRUE), # >20°C = high
    .groups = "drop"
  )
```

**2. Soil Moisture Drought (Agricultural Stress, Dust):**
```r
# Soil moisture drought index
county_soil_drought <- county_soil_daily %>%
  group_by(GEOID) %>%
  summarize(
    # Drought severity
    mean_soil_moisture = mean(soil_moisture, na.rm = TRUE),
    days_dry = sum(soil_moisture < 0.15, na.rm = TRUE),
    days_very_dry = sum(soil_moisture < 0.10, na.rm = TRUE),

    # Consecutive dry days
    max_consecutive_dry = max(rle(soil_moisture < 0.15)$lengths[rle(soil_moisture < 0.15)$values]),

    .groups = "drop"
  )

# Health associations:
# - Low soil moisture → dust storms (PM10) → respiratory disease
# - Agricultural drought → crop failure → food insecurity
# - Soil moisture deficit → heat stress amplification
```

**3. Hourly Precipitation (Flash Flooding):**
```r
# Load hourly precipitation
era5_precip <- rast("era5_us_2020_precip.nc")

# Extract to counties
county_precip_hourly <- exact_extract(era5_precip, counties, fun = "mean")

# Convert to data frame (m → mm)
county_precip_df <- as.data.frame(county_precip_hourly) %>%
  mutate(GEOID = counties$GEOID) %>%
  pivot_longer(-GEOID, names_to = "layer", values_to = "precip_m") %>%
  mutate(
    precip_mm = precip_m * 1000,
    datetime = dates_hours[as.numeric(str_extract(layer, "\\d+"))]
  )

# Flash flood risk (>50mm in 3 hours)
county_flash_flood <- county_precip_df %>%
  arrange(GEOID, datetime) %>%
  group_by(GEOID) %>%
  mutate(
    precip_3h = rollsum(precip_mm, k = 3, fill = NA, align = "right")
  ) %>%
  summarize(
    days_flash_flood_risk = sum(precip_3h > 50, na.rm = TRUE) / 24, # Hourly → daily
    max_hourly_precip = max(precip_mm, na.rm = TRUE),
    .groups = "drop"
  )
```

#### **Data Quality**

**Strengths:**
- ✅ **Hourly temporal resolution** (captures diurnal patterns, heat waves, storms)
- ✅ **Soil moisture** (4 layers, unique for US county analysis)
- ✅ **Pre-1980 climate** (1940-present, 84 years)
- ✅ **100+ variables** (comprehensive atmospheric/land surface)
- ✅ **Global coverage** (US territories, international comparisons)
- ✅ FREE

**Limitations:**
- ⚠️ **Lower spatial resolution** (31 km vs 1-4 km for US sources)
- ⚠️ **Model-based** (not directly observed like station data)
- ⚠️ **Large file sizes** (hourly data = 8,760+ layers/year)
- ⚠️ **Download limits** (CDS throttling, slow downloads)

**When to Use ERA5 vs. PRISM/Daymet/GRIDMET:**
- **Hourly data needed:** ERA5 (PRISM/Daymet/GRIDMET are daily)
- **Soil moisture:** ERA5 ONLY (not in US sources)
- **Pre-1980 climate:** ERA5 (GRIDMET starts 1979, PRISM 1981)
- **US territories (Puerto Rico, US Virgin Islands):** ERA5 or Daymet
- **Daily temperature/precipitation:** Use PRISM/Daymet (higher resolution)

**Priority Variables for Health Observatory:**
1. Volumetric soil moisture layer 1 (0-7 cm, m³/m³) - drought, dust
2. Hourly 2m temperature (K) - circadian disruption, heat waves
3. Hourly precipitation (m) - flash flooding
4. 10m wind speed (m/s) - hourly wind exposure
5. Surface solar radiation (J/m²) - UV exposure, vitamin D
6. Snow depth (m) - winter mobility, isolation
7. Soil temperature layer 1 (K) - permafrost, vector-borne disease
8. Evaporation (m) - water availability
9. Total cloud cover (fraction) - seasonal affective disorder
10. Surface runoff (m) - flooding risk

---

### 5. ERA5-LAND ⭐⭐⭐⭐

**PRIORITY RANK: #5 for US Counties (Enhanced Land Surface Variables)**

#### **Overview**

**What:** Enhanced land surface reanalysis based on ERA5
**Who:** ECMWF
**Resolution:** 11 km (~0.1° × 0.1° lat/lon) - **BETTER than ERA5 (31 km)**
**Coverage:** Global land surface (60°S to 60°N)
**Temporal:** 1950-present (hourly)
**Update Frequency:** Monthly (2-3 month lag)

**Why ERA5-Land:**
- **Higher resolution** than ERA5 (11 km vs 31 km)
- **Land-focused** (better soil, vegetation, snow representation)
- **Same hourly temporal resolution** as ERA5
- **Longer time series** than PRISM/Daymet (1950 vs 1980-1981)

**When to Use ERA5-Land vs. ERA5:**
- **Land surface processes:** ERA5-Land (soil, snow, ET, runoff)
- **Atmospheric variables:** ERA5 (pressure levels, clouds, radiation)
- **US counties with daily data:** Still prefer PRISM/Daymet/GRIDMET (higher resolution)

#### **Variables Available (50+ Land Surface)**

**Temperature & Energy:**
1. **2m temperature** - K
2. **2m dewpoint temperature** - K
3. **Skin temperature** - K
4. **Soil temperature layer 1-4** - K

**Soil Moisture (Enhanced vs. ERA5):**
5. **Volumetric soil moisture layer 1** (0-7 cm) - m³/m³
6. **Volumetric soil moisture layer 2** (7-28 cm) - m³/m³
7. **Volumetric soil moisture layer 3** (28-100 cm) - m³/m³
8. **Volumetric soil moisture layer 4** (100-289 cm) - m³/m³

**Precipitation & Water:**
9. **Total precipitation** - m
10. **Evaporation from bare soil** - m
11. **Evaporation from open water** - m
12. **Evaporation from vegetation** - m
13. **Total evaporation** - m
14. **Potential evaporation** - m
15. **Runoff** - m
16. **Surface runoff** - m
17. **Sub-surface runoff** - m

**Snow:**
18. **Snow cover** - %
19. **Snow depth** - m
20. **Snow depth water equivalent** - m
21. **Snowfall** - m water equivalent
22. **Snowmelt** - m water equivalent
23. **Snow albedo** - fraction

**Vegetation:**
24. **Leaf area index (high + low vegetation)** - m²/m²
25. **Skin reservoir content** - m

**Full Variable List:** https://confluence.ecmwf.int/display/CKB/ERA5-Land

#### **Data Access**

**Portal:** https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-land

**Download via CDS API (Python):**
```python
import cdsapi

c = cdsapi.Client()

c.retrieve(
    'reanalysis-era5-land',
    {
        'variable': [
            '2m_temperature', 'total_precipitation',
            'volumetric_soil_water_layer_1', 'volumetric_soil_water_layer_2',
            'surface_runoff', 'total_evaporation'
        ],
        'year': '2020',
        'month': ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'],
        'day': ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10',
                '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
                '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31'],
        'time': ['00:00', '01:00', '02:00', '03:00', '04:00', '05:00',
                 '06:00', '07:00', '08:00', '09:00', '10:00', '11:00',
                 '12:00', '13:00', '14:00', '15:00', '16:00', '17:00',
                 '18:00', '19:00', '20:00', '21:00', '22:00', '23:00'],
        'area': [49, -125, 24, -66],  # N, W, S, E
        'format': 'netcdf',
    },
    'era5_land_us_2020.nc'
)
```

**Google Earth Engine:**
```javascript
// ERA5-Land Monthly in GEE
var era5_land = ee.ImageCollection("ECMWF/ERA5_LAND/MONTHLY")
  .filterDate('2020-01-01', '2020-12-31');

// Select variables
var soil_moisture = era5_land.select('volumetric_soil_water_layer_1_mean');
var temp = era5_land.select('temperature_2m_mean');

// Annual mean for counties
var counties = ee.FeatureCollection("TIGER/2020/Counties");

var era5_land_annual = era5_land.mean();

var county_era5_land = era5_land_annual.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 11132 // ~11 km
});

Export.table.toDrive({
  collection: county_era5_land,
  description: 'era5_land_county_2020'
});
```

#### **County-Level Aggregation**

**Method: Enhanced Soil Moisture + Runoff Analysis**

```r
library(terra)
library(exactextractr)
library(tidyverse)

# Load ERA5-Land soil moisture (4 layers)
era5_land_sm1 <- rast("era5_land_2020_sm_layer1.nc") # 0-7 cm
era5_land_sm2 <- rast("era5_land_2020_sm_layer2.nc") # 7-28 cm
era5_land_sm3 <- rast("era5_land_2020_sm_layer3.nc") # 28-100 cm
era5_land_sm4 <- rast("era5_land_2020_sm_layer4.nc") # 100-289 cm

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>% st_transform(4326)

# Extract mean for each layer (daily)
extract_soil_layer <- function(raster, counties_sf, layer_name) {
  county_values <- exact_extract(raster, counties_sf, fun = "mean")

  as.data.frame(county_values) %>%
    mutate(GEOID = counties_sf$GEOID) %>%
    pivot_longer(-GEOID, names_to = "day", values_to = "soil_moisture") %>%
    mutate(
      layer = layer_name,
      day_of_year = as.numeric(str_extract(day, "\\d+"))
    )
}

soil_all_layers <- bind_rows(
  extract_soil_layer(era5_land_sm1, counties, "layer1_0_7cm"),
  extract_soil_layer(era5_land_sm2, counties, "layer2_7_28cm"),
  extract_soil_layer(era5_land_sm3, counties, "layer3_28_100cm"),
  extract_soil_layer(era5_land_sm4, counties, "layer4_100_289cm")
)

# Calculate annual soil moisture statistics
soil_annual <- soil_all_layers %>%
  group_by(GEOID, layer) %>%
  summarize(
    mean_soil_moisture = mean(soil_moisture, na.rm = TRUE),
    min_soil_moisture = min(soil_moisture, na.rm = TRUE),
    max_soil_moisture = max(soil_moisture, na.rm = TRUE),
    cv_soil_moisture = sd(soil_moisture, na.rm = TRUE) / mean(soil_moisture, na.rm = TRUE),
    days_drought = sum(soil_moisture < 0.15, na.rm = TRUE),
    .groups = "drop"
  ) %>%
  pivot_wider(names_from = layer, values_from = c(mean_soil_moisture, days_drought))
```

#### **Derived Health Indicators**

**1. Agricultural Drought Severity (Multi-Layer Soil Moisture):**
```r
# Root zone soil moisture (weighted average of layers 1-3)
root_zone_drought <- soil_all_layers %>%
  filter(layer %in% c("layer1_0_7cm", "layer2_7_28cm", "layer3_28_100cm")) %>%
  group_by(GEOID, day_of_year) %>%
  summarize(
    root_zone_sm = weighted.mean(soil_moisture, w = c(7, 21, 72)), # Layer depths
    .groups = "drop"
  ) %>%
  group_by(GEOID) %>%
  summarize(
    mean_root_zone_sm = mean(root_zone_sm, na.rm = TRUE),
    agricultural_drought_days = sum(root_zone_sm < 0.20, na.rm = TRUE),
    severe_drought_days = sum(root_zone_sm < 0.15, na.rm = TRUE),
    .groups = "drop"
  )
```

**2. Flooding Risk (Runoff + Precipitation):**
```r
# Load runoff + precipitation
era5_land_runoff <- rast("era5_land_2020_runoff.nc")
era5_land_precip <- rast("era5_land_2020_precip.nc")

# Extract to counties
county_runoff <- exact_extract(era5_land_runoff, counties, fun = "mean")
county_precip <- exact_extract(era5_land_precip, counties, fun = "mean")

# Combine
flood_risk <- data.frame(
  GEOID = counties$GEOID,
  runoff_mean = rowMeans(county_runoff, na.rm = TRUE),
  precip_mean = rowMeans(county_precip, na.rm = TRUE)
) %>%
  mutate(
    runoff_coefficient = runoff_mean / precip_mean, # High = low infiltration
    flood_risk_score = runoff_mean * 1000 # m → mm
  )
```

#### **Data Quality**

**Strengths:**
- ✅ **Higher resolution than ERA5** (11 km vs 31 km)
- ✅ **Enhanced land surface** (better soil, snow, vegetation)
- ✅ **Hourly temporal resolution**
- ✅ **Longer time series** than PRISM/Daymet (1950-present, 74 years)
- ✅ FREE

**Limitations:**
- ⚠️ **Land surface only** (no atmospheric pressure levels)
- ⚠️ **Still lower resolution** than PRISM/Daymet/GRIDMET (11 km vs 1-4 km)
- ⚠️ **2-3 month lag** (slower updates than ERA5)

**Priority Variables:**
1. Volumetric soil moisture layers 1-4 (m³/m³)
2. Surface runoff (m) - flooding
3. Total evaporation (m) - drought severity
4. Snow depth water equivalent (m) - winter water availability
5. Skin temperature (K) - urban heat island

---

### 6. CAMS ATMOSPHERIC COMPOSITION ⭐⭐⭐⭐

**PRIORITY RANK: #6 for US Counties (Gap-Filling for Air Quality)**

#### **Overview**

**What:** Copernicus Atmosphere Monitoring Service - Global atmospheric composition reanalysis
**Who:** ECMWF
**Resolution:** 0.4° × 0.4° (~44 km) OR 0.1° × 0.1° (~11 km, regional)
**Coverage:** Global
**Temporal:** 2003-present (3-hourly analysis, daily forecasts)
**Update Frequency:** Near-real-time (1-2 day lag)

**Why CAMS for US Counties:**
- **Gap-filling** for counties WITHOUT EPA AQS monitors (1,200+ counties have no monitors)
- **Additional pollutants** not measured by EPA (CH4, HCHO, aerosol components)
- **Daily global coverage** (no missing data from station outages)
- **Forecast capability** (5-day air quality forecast)

**When NOT to Use CAMS:**
- For counties WITH EPA AQS monitors → Use EPA AQS (ground-based, more accurate)
- CAMS is MODEL-BASED (less accurate than ground monitors where available)

#### **Variables Available (Atmospheric Composition)**

**Gas Phase Pollutants:**
1. **PM2.5** - µg/m³
2. **PM10** - µg/m³
3. **Ozone (O3)** - µg/m³
4. **Nitrogen dioxide (NO2)** - µg/m³
5. **Sulfur dioxide (SO2)** - µg/m³
6. **Carbon monoxide (CO)** - µg/m³
7. **Ammonia (NH3)** - µg/m³
8. **Nitrogen monoxide (NO)** - µg/m³
9. **Formaldehyde (HCHO)** - µg/m³
10. **Methane (CH4)** - ppb

**Aerosol Components (NOT in EPA AQS):**
11. **Black carbon (BC)** - kg/m³
12. **Organic matter (OM)** - kg/m³
13. **Sulfate aerosol (SO4)** - kg/m³
14. **Nitrate aerosol (NO3)** - kg/m³
15. **Sea salt aerosol** - kg/m³
16. **Dust aerosol** - kg/m³
17. **Ammonium aerosol (NH4)** - kg/m³

**Optical Properties:**
18. **Aerosol optical depth at 550 nm** - unitless
19. **Total column ozone** - DU (Dobson Units)
20. **UV index** - unitless

**Full Variable List:** https://ads.atmosphere.copernicus.eu/cdsapp#!/dataset/cams-global-reanalysis-eac4

#### **Data Access**

**Portal:** https://ads.atmosphere.copernicus.eu/ (Atmosphere Data Store, ADS)

**Download via ADS API (Python):**
```python
import cdsapi

c = cdsapi.Client(url="https://ads.atmosphere.copernicus.eu/api/v2", key="YOUR_KEY")

c.retrieve(
    'cams-global-reanalysis-eac4',
    {
        'variable': [
            'particulate_matter_2.5um', 'particulate_matter_10um',
            'nitrogen_dioxide', 'ozone', 'sulphur_dioxide', 'carbon_monoxide'
        ],
        'date': '2020-01-01/2020-12-31',
        'time': ['00:00', '03:00', '06:00', '09:00', '12:00', '15:00', '18:00', '21:00'],
        'area': [49, -125, 24, -66],  # N, W, S, E
        'format': 'netcdf',
    },
    'cams_us_2020.nc'
)
```

**Sentinel-5P TROPOMI (Satellite, Higher Resolution):**
```javascript
// Sentinel-5P in Google Earth Engine (7km × 3.5km, BETTER than CAMS)
var s5p_no2 = ee.ImageCollection("COPERNICUS/S5P/OFFL/L3_NO2")
  .filterDate('2020-01-01', '2020-12-31')
  .select('tropospheric_NO2_column_number_density');

// Annual mean NO2 for counties
var counties = ee.FeatureCollection("TIGER/2020/Counties");

var no2_annual = s5p_no2.mean();

var county_no2 = no2_annual.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 1113 // Sentinel-5P native resolution
});

Export.table.toDrive({
  collection: county_no2,
  description: 'sentinel5p_no2_county_2020'
});
```

#### **County-Level Aggregation**

**Method: Extract CAMS for Counties WITHOUT EPA Monitors**

```r
library(terra)
library(exactextractr)
library(tidyverse)

# Load CAMS PM2.5 (3-hourly for 2020)
cams_pm25 <- rast("cams_us_2020_pm25.nc")

# Load counties
counties <- st_read("tl_2020_us_county.shp") %>% st_transform(4326)

# Identify counties WITHOUT EPA AQS monitors
epa_monitors <- read_csv("epa_aqs_monitors_2020.csv") # From EPA AQS

counties_with_monitors <- epa_monitors %>%
  distinct(GEOID = State_County_Code)

counties_no_monitors <- counties %>%
  anti_join(counties_with_monitors, by = "GEOID")

# Extract CAMS PM2.5 for counties without monitors
cams_pm25_county <- exact_extract(cams_pm25, counties_no_monitors, fun = "mean")

# Convert to data frame (3-hourly → daily mean → annual mean)
dates_3h <- seq(as.POSIXct("2020-01-01 00:00:00", tz = "UTC"),
                as.POSIXct("2020-12-31 21:00:00", tz = "UTC"),
                by = "3 hours")

cams_pm25_df <- as.data.frame(cams_pm25_county) %>%
  mutate(GEOID = counties_no_monitors$GEOID) %>%
  pivot_longer(-GEOID, names_to = "layer", values_to = "pm25_ugm3") %>%
  mutate(
    datetime = dates_3h[as.numeric(str_extract(layer, "\\d+"))],
    date = as.Date(datetime)
  )

# Daily mean
cams_pm25_daily <- cams_pm25_df %>%
  group_by(GEOID, date) %>%
  summarize(pm25_daily = mean(pm25_ugm3, na.rm = TRUE), .groups = "drop")

# Annual statistics
cams_pm25_annual <- cams_pm25_daily %>%
  group_by(GEOID) %>%
  summarize(
    mean_pm25 = mean(pm25_daily, na.rm = TRUE),
    max_pm25 = max(pm25_daily, na.rm = TRUE),
    days_pm25_unhealthy = sum(pm25_daily > 35.5, na.rm = TRUE), # AQI >100
    days_pm25_very_unhealthy = sum(pm25_daily > 55.5, na.rm = TRUE), # AQI >150
    .groups = "drop"
  )
```

#### **Derived Health Indicators**

**1. Aerosol Component Exposure (UNIQUE - not in EPA AQS):**
```r
# Load CAMS aerosol components
cams_bc <- rast("cams_us_2020_black_carbon.nc")
cams_dust <- rast("cams_us_2020_dust.nc")

# Extract to counties
county_bc <- exact_extract(cams_bc, counties, fun = "mean") %>%
  rowMeans(na.rm = TRUE) # Annual mean

county_dust <- exact_extract(cams_dust, counties, fun = "mean") %>%
  rowMeans(na.rm = TRUE)

# Convert kg/m³ to µg/m³
aerosol_components <- data.frame(
  GEOID = counties$GEOID,
  black_carbon_ugm3 = county_bc * 1e9,
  dust_ugm3 = county_dust * 1e9
)

# Health associations:
# - Black carbon → cardiovascular disease (traffic emissions)
# - Dust → respiratory disease (desert/agricultural regions)
```

**2. Formaldehyde (HCHO) - VOC Exposure Proxy:**
```r
# Load CAMS HCHO
cams_hcho <- rast("cams_us_2020_hcho.nc")

# Extract to counties
county_hcho <- exact_extract(cams_hcho, counties, fun = "mean") %>%
  rowMeans(na.rm = TRUE)

hcho_exposure <- data.frame(
  GEOID = counties$GEOID,
  hcho_ppb = county_hcho * 1e9
)

# Health associations:
# - HCHO → respiratory irritation, cancer risk
# - Proxy for VOC exposure (industrial, wildfire)
```

#### **Data Quality & Validation**

**Strengths:**
- ✅ **Daily global coverage** (no missing data)
- ✅ **Gap-filling** for counties without monitors (1,200+)
- ✅ **Aerosol components** not measured by EPA
- ✅ **Forecast capability** (5-day air quality forecast)
- ✅ FREE

**Limitations:**
- ⚠️ **Model-based** (less accurate than ground monitors)
- ⚠️ **Lower resolution** (44 km vs EPA AQS station data)
- ⚠️ **Validation required** (compare to EPA AQS where available)

**Validation Against EPA AQS:**
- CAMS PM2.5 vs EPA AQS: r ≈ 0.65-0.75 (moderate correlation)
- CAMS NO2 vs EPA AQS: r ≈ 0.50-0.60
- CAMS O3 vs EPA AQS: r ≈ 0.70-0.80

**When to Use CAMS:**
- Counties WITHOUT EPA AQS monitors (1,200+ counties)
- Aerosol composition analysis (BC, dust, OM)
- VOC exposure (HCHO, CH4)
- Air quality forecasting
- International comparisons

**When to Use EPA AQS Instead:**
- Counties WITH EPA AQS monitors (more accurate)
- Regulatory compliance (EPA data preferred)

**Priority Variables:**
1. PM2.5 (µg/m³) - gap-filling for unmonitored counties
2. NO2 (µg/m³) - traffic exposure
3. Black carbon (µg/m³) - traffic, combustion
4. Dust aerosol (µg/m³) - respiratory disease
5. Formaldehyde (ppb) - VOC exposure
6. Ozone (µg/m³) - gap-filling
7. SO2 (µg/m³) - industrial exposure
8. Aerosol optical depth - wildfire smoke
9. UV index - skin cancer, vitamin D
10. Total column ozone - stratospheric ozone

---

## PART 3: SATELLITE ATMOSPHERIC COMPOSITION (VERIFICATION)

### 7. SATELLITE DATA (MODIS/VIIRS/Sentinel-5P) ⭐⭐⭐

**PRIORITY: Verification + Gap-Filling**

#### **Overview**

Satellite remote sensing provides:
- **Higher resolution** than CAMS (Sentinel-5P: 7 km × 3.5 km)
- **Daily global coverage** (cloud-permitting)
- **Independent verification** of ground monitors + models

**Key Satellite Products for US Counties:**

**1. Sentinel-5P TROPOMI (Highest Resolution):**
- **Resolution:** 7 km × 3.5 km
- **Temporal:** 2018-present (daily overpass ~1:30 PM local)
- **Variables:** NO2, O3, SO2, CH4, HCHO, CO, aerosol
- **Access:** Google Earth Engine, Copernicus Data Space
- **Use:** Verify EPA AQS NO2, fill gaps

**2. MODIS Aerosol Optical Depth:**
- **Resolution:** 10 km (Terra), 3 km (MAIAC algorithm)
- **Temporal:** 2000-present (Terra), 2002-present (Aqua)
- **Variables:** AOD 550nm, Ångström exponent
- **Access:** NASA LAADS DAAC, Google Earth Engine
- **Use:** PM2.5 estimation, wildfire smoke

**3. VIIRS Active Fires + Nighttime Lights:**
- **Resolution:** 375 m (active fires), 500 m (nighttime lights)
- **Temporal:** 2012-present (Suomi-NPP), 2017-present (NOAA-20)
- **Variables:** Fire radiative power, nighttime radiance
- **Access:** NASA FIRMS, Google Earth Engine
- **Use:** Wildfire exposure, urban development

**Note:** These satellite products are ALREADY documented in existing files:
- MODIS/VIIRS: Check existing documentation for aerosol/fire products
- This section serves as CROSS-REFERENCE to international sources

---

## PART 4: DATA COLLECTION WORKFLOWS

### COUNTY AGGREGATION METHODS

**General Workflow for Gridded Climate/Atmospheric Data → County Statistics:**

**Step 1: Load County Boundaries**
```r
library(sf)
library(tigris)
options(tigris_use_cache = TRUE)

# Download 2020 US counties (cartographic boundaries)
counties <- counties(year = 2020, cb = TRUE, resolution = "500k")

# Or use TIGER/Line (more detailed)
counties <- counties(year = 2020)

# Filter to contiguous US (if needed)
counties_conus <- counties %>%
  filter(!STATE %in% c("02", "15", "60", "66", "69", "72", "78")) # AK, HI, territories

# Project to appropriate CRS
# - For raster in WGS84 (EPSG:4326): Keep as is or use st_transform(4326)
# - For US analysis: Albers Equal Area (EPSG:5070)
counties_albers <- st_transform(counties, 5070)
```

**Step 2: Load Raster Data (ERA5, PRISM, Daymet, GRIDMET)**
```r
library(terra)

# Load NetCDF or GeoTIFF raster
climate_raster <- rast("climate_data.nc")

# Check CRS
crs(climate_raster)

# If multi-layer (daily/hourly), check number of layers
nlyr(climate_raster) # 365 for daily, 8760 for hourly

# Convert units if needed (e.g., Kelvin to Celsius)
if (units_are_kelvin) {
  climate_raster <- climate_raster - 273.15
}
```

**Step 3: Spatial Extraction (Area-Weighted)**
```r
library(exactextractr)

# Extract mean for each county (area-weighted)
county_values_mean <- exact_extract(climate_raster, counties, fun = "mean")

# Can also extract:
# - max: maximum value within county
# - min: minimum value
# - median: median value
# - stdev: standard deviation
# - quantile: specific percentiles (e.g., 95th percentile heat)
# - weighted_mean: population-weighted (requires population raster)

# For multi-layer rasters (daily data), returns matrix (counties × days)
# Convert to data frame
county_daily_df <- as.data.frame(county_values_mean) %>%
  mutate(GEOID = counties$GEOID) %>%
  pivot_longer(-GEOID, names_to = "day", values_to = "value")
```

**Step 4: Temporal Aggregation (Daily → Annual)**
```r
# Calculate annual statistics
county_annual <- county_daily_df %>%
  group_by(GEOID) %>%
  summarize(
    mean = mean(value, na.rm = TRUE),
    max = max(value, na.rm = TRUE),
    min = min(value, na.rm = TRUE),
    stdev = sd(value, na.rm = TRUE),
    p95 = quantile(value, 0.95, na.rm = TRUE),
    days_above_threshold = sum(value > THRESHOLD, na.rm = TRUE),
    .groups = "drop"
  )

# Join back to county shapefile
counties_with_data <- counties %>%
  left_join(county_annual, by = "GEOID")

# Export
write_csv(st_drop_geometry(counties_with_data), "county_climate_annual.csv")
```

**Step 5: Population-Weighted Aggregation (for Temperature)**
```r
# Load population raster (LandScan, WorldPop, or SEDAC GPW archive)
# NOTE: NASA SEDAC terminated April 2025 - historical data available via NASA Earthdata Cloud
population <- rast("gpw_v4_population_count_2020_30_sec.tif")

# Resample population to match climate raster resolution
population_resampled <- resample(population, climate_raster, method = "bilinear")

# Population-weighted extraction
county_popwt <- exact_extract(
  climate_raster,
  counties,
  weights = population_resampled,
  fun = "weighted_mean"
)

# This gives population-weighted average (people experience this, not land area)
```

---

### DERIVED HEALTH INDICATORS

**Key Health Indicators Derivable from Climate/Atmospheric Data:**

**1. Heat Exposure:**
- Days with tmax >35°C (95°F)
- Days with tmax >38°C (100°F)
- Days with tmax >40°C (105°F)
- Heat wave events (3+ consecutive days >35°C)
- Heat index days >41°C (105°F) - requires temperature + humidity
- Cooling degree days (base 65°F)

**2. Cold Exposure:**
- Days with tmin <0°C (32°F)
- Days with tmin <-18°C (0°F)
- Cold snap events (3+ consecutive days <0°C)
- Heating degree days (base 65°F)

**3. Precipitation Extremes:**
- Days with >50mm (2 inches) precipitation - flooding risk
- Maximum consecutive dry days - drought
- Days with >100mm (4 inches) - flash flood risk
- Total annual precipitation

**4. Drought:**
- Maximum consecutive dry days (>14 days = agricultural stress)
- Standardized Precipitation Index (SPI) - requires multi-year data
- Soil moisture deficit (ERA5/ERA5-Land)
- Water deficit (ET0 - precipitation, from GRIDMET)

**5. Air Quality:**
- Days with PM2.5 >35.5 µg/m³ (AQI >100, unhealthy for sensitive groups)
- Days with PM2.5 >55.5 µg/m³ (AQI >150, unhealthy)
- Annual mean PM2.5 (WHO guideline: 5 µg/m³)
- Days with O3 8-hour max >70 ppb (EPA standard)
- NO2 annual mean (WHO guideline: 10 µg/m³)

**6. Wildfire:**
- Smoke exposure days (NOAA HMS, MODIS AOD)
- High fire risk days (GRIDMET ERC >80)
- Fuel moisture <10% (extreme fire risk)

**7. Wind:**
- Days with wind >10 m/s (22 mph, dust/pollen dispersal)
- Days with wind >15 m/s (34 mph, dust storms)
- Mean wind speed (air pollution dispersion)

**8. Solar/UV:**
- Annual solar radiation (vitamin D, seasonal affective disorder)
- UV index >8 (very high, skin cancer risk)
- Day length variation (seasonal affective disorder)

---

## SUMMARY: INTERNATIONAL CLIMATE & ATMOSPHERIC DATA HIERARCHY

**For US County Health Observatory, Prioritize:**

### **CLIMATE VARIABLES (Temperature, Precipitation, Wind, ET):**
1. **PRISM** (4km, 1981-present) → Precipitation
2. **Daymet** (1km, 1980-present) → Temperature, solar radiation, snow
3. **GRIDMET** (4km, 1979-present) → Wind, humidity, ET, fuel moisture
4. **ERA5** (31km, 1940-present, hourly) → Hourly data, pre-1980 climate
5. **ERA5-Land** (11km, 1950-present, hourly) → Soil moisture, enhanced land surface

### **AIR QUALITY VARIABLES (PM2.5, NO2, O3, Aerosols):**
1. **EPA AQS** (station data) → Where monitors exist (1,900+ counties)
2. **CAMS** (44km, 2003-present) → Gap-filling for unmonitored counties (1,200+)
3. **Sentinel-5P TROPOMI** (7km, 2018-present) → Verify NO2, O3, HCHO
4. **MODIS/VIIRS** (3-10km, 2000-present) → AOD, wildfire smoke

### **PRIORITY VARIABLES FOR HEALTH OBSERVATORY (NEW from International Sources):**

From **ERA5/ERA5-Land:**
1. Volumetric soil moisture layer 1 (0-7 cm) - drought, dust, agricultural stress
2. Hourly temperature (diurnal patterns, circadian disruption)
3. Hourly precipitation (flash flooding)
4. Surface runoff (flooding risk)
5. Snow depth water equivalent (winter isolation, water availability)

From **CAMS:**
6. PM2.5 (gap-filling for 1,200+ unmonitored counties)
7. NO2 (traffic exposure, gap-filling)
8. Black carbon (traffic/combustion exposure)
9. Dust aerosol (respiratory disease)
10. Formaldehyde (VOC exposure proxy)

From **PRISM/Daymet/GRIDMET (US-specific):**
11. Annual precipitation (PRISM, mm)
12. Days tmax >35°C (Daymet, heat exposure)
13. Wind speed >10 m/s days (GRIDMET, dust/pollen)
14. Water deficit (GRIDMET ET0 - precipitation, agricultural drought)
15. Solar radiation (Daymet, vitamin D/SAD)

**TOTAL NEW VARIABLES FROM INTERNATIONAL SOURCES: ~150+**
- ERA5: ~100 variables
- ERA5-Land: ~50 variables (subset of ERA5, enhanced)
- CAMS: ~20 variables
- Minus duplicates (temperature, precipitation overlap): ~150 unique

**IMPLEMENTATION TIMELINE:**
- **Phase 1 (Weeks 1-2):** PRISM/Daymet/GRIDMET - High priority, easy access
- **Phase 2 (Weeks 3-4):** ERA5/ERA5-Land soil moisture - Requires CDS setup
- **Phase 3 (Weeks 5-6):** CAMS air quality - Gap-filling for unmonitored counties
- **Phase 4 (Weeks 7-8):** Sentinel-5P verification - GEE processing

---

**Version:** 2.0 (COMPLETE - Parts 1 + 2)
**Last Updated:** November 12, 2025
**Sources Documented:** 7 (PRISM, Daymet, GRIDMET, ERA5, ERA5-Land, CAMS, Satellite)
**Status:** Ready for data collection