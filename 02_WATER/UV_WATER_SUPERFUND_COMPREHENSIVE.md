# UV RADIATION, DRINKING WATER QUALITY & SUPERFUND SITES
## Comprehensive County-Level Environmental Health Data Sources

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Repository:** GetData
**Category:** Environmental Health - UV Exposure, Drinking Water Contaminants, Hazardous Waste Sites

---

## Executive Summary

This document provides comprehensive coverage of county-level data sources for three critical environmental health exposures:

1. **UV Radiation & Solar Exposure** - Primary risk factor for skin cancer (melanoma, non-melanoma), cataracts
2. **Drinking Water Quality & Violations** - PFAS, lead, arsenic, nitrates linked to cancer, kidney disease, developmental issues
3. **Superfund & Contaminated Sites** - Mixed chemical exposures associated with multiple cancers, neurological effects

All data sources provide county-level coverage or are aggregable to county level, with emphasis on longest available time ranges and most authoritative sources.

**Key Statistics:**
- **UV Data:** 1961-present (63+ years of county estimates)
- **Drinking Water:** 1993-present (31+ years of SDWIS violations)
- **Superfund:** 1,343 NPL sites (1980-present)

---

## PART 1: UV RADIATION & SOLAR EXPOSURE

### Health Impacts

**Diseases Linked to UV Exposure:**
- **Skin Cancer:** Melanoma (deadliest), basal cell carcinoma, squamous cell carcinoma
- **Cataracts:** Age-related lens opacity (leading cause of blindness)
- **Immune Suppression:** Reduced immune function
- **Photoaging:** Premature skin aging, wrinkles
- **Actinic Keratosis:** Precancerous skin lesions

**Dose-Response:** Risk increases with cumulative UV exposure; childhood exposure particularly important for melanoma

**Geographic Patterns:** Higher UV exposure at lower latitudes, higher altitudes; varies by season, cloud cover, ozone levels

---

### Source 1: NCI/CDC County-Level UV Exposure Data

**Official Name:** National Cancer Institute UV Exposure Database / CDC Environmental Public Health Tracking Network
**Status:** ✅ LONGEST COUNTY-LEVEL UV TIME SERIES (1961-2024, 63+ YEARS)

#### Overview

The NCI UV exposure database provides modeled estimates of average daily UV radiation for all US counties based on NASA satellite data, NOAA ground station measurements, and atmospheric modeling.

#### Coverage

- **Geographic:** Continental United States, all counties (3,143 counties)
- **Temporal:** 1961-1990 baseline, 5-year rolling averages through 2024
- **Spatial Resolution:** County-level aggregates from 1km gridded data
- **Update Frequency:** 5-year intervals (1997-1999, 2000-2004, 2005-2009, etc.)

#### Variables Available

| Variable | Description | Units | Temporal Coverage |
|----------|-------------|-------|-------------------|
| Average Daily Global Solar Radiation | Total solar energy reaching earth's surface | Wh/m² | 1961-2024 |
| UV Index Estimates | Erythemal UV dose (sunburn-weighted) | 0-15+ scale | 1997-2024 |
| Seasonal Variations | Summer, winter, spring, fall averages | Wh/m² | 1961-2024 |
| Annual Mean UV Exposure | Yearly average | Wh/m² | 1961-2024 |
| UV Trend | Change over time | Wh/m²/decade | 1961-2024 |

#### Data Access

**Primary Access:**
- **URL:** https://gis.cancer.gov/tools/uv-exposure/
- **Interactive Tool:** NCI Cancer Atlas UV Exposure Tool
- **Download:** Shapefile, GeoJSON, CSV by county FIPS
- **API:** RESTful API available

**Access Method:**
```r
# Example: Download NCI UV data for all counties
library(tidyverse)
library(httr)

# NCI UV Exposure API endpoint
api_url <- "https://gis.cancer.gov/api/uv-exposure"

# Get county-level UV data for 2010-2014 period
uv_data <- GET(
  api_url,
  query = list(
    period = "2010-2014",
    geography = "county",
    format = "csv"
  )
)

# Parse response
county_uv <- content(uv_data, "parsed")

# Structure:
# FIPS, State, County, AvgDailyUV_Wh_m2, UVIndex_Mean,
# Summer_UV, Winter_UV, Latitude, Altitude
```

**Alternative Access via CDC:**
- **URL:** https://ephtracking.cdc.gov/DataExplorer/
- **Path:** Environmental Health Tracking → Environmental Hazards → UV Radiation
- **Interactive Query:** County selection, time period, download CSV/Excel

#### Data Quality

**Strengths:**
- Longest available county-level UV time series (1961-2024)
- Validated against ground station measurements
- Accounts for cloud cover, atmospheric ozone, elevation, season
- Consistent methodology over time

**Limitations:**
- Modeled estimates (not direct measurements at every county)
- Does not account for individual behaviors (sun exposure time, sunscreen use, clothing)
- County aggregates mask within-county variation (urban vs. rural, valleys vs. mountains)

**Validation:** Ground station comparisons show correlation r=0.92-0.95 with direct measurements

#### Use Cases for County-Level Analysis

1. **Cancer Risk Assessment:** Melanoma incidence correlates with cumulative UV exposure
2. **Time-Trend Analysis:** Examine changes in UV exposure 1961-2024 (ozone depletion, recovery)
3. **Climate Change Impacts:** UV patterns changing with climate
4. **Prevention Planning:** Identify high-UV counties for targeted skin cancer screening, education
5. **Epidemiological Studies:** Control variable for skin cancer, cataract studies

---

### Source 2: NASA/CDC UV Irradiance Dataset

**Official Name:** NASA Applied Sciences Program UV Irradiance / CDC Environmental Public Health Tracking Network
**Status:** ✅ HIGH SPATIAL RESOLUTION (4km gridded, aggregable to county)

#### Overview

This dataset provides daily UV irradiance estimates from NASA Earth Observing System satellites (Aura OMI, TOMS) processed for public health applications through the CDC Tracking Network.

#### Coverage

- **Geographic:** Contiguous United States (CONUS)
- **Temporal:** 2005-2015 (first comprehensive release); periodic updates
- **Spatial Resolution:** 4km x 4km grid (aggregable to county via zonal statistics)
- **Temporal Resolution:** Daily estimates, available as monthly and annual aggregates

#### Variables Available

| Variable | Description | Units | Notes |
|----------|-------------|-------|-------|
| Daily UV Irradiance | Total UV reaching surface | mW/m² | Cloud-adjusted |
| Erythemal UV | Sunburn-weighted UV | mW/m² | Most relevant for health |
| Annual Average UV Exposure | Yearly mean | mW/m² | County aggregate |
| Monthly UV Patterns | Seasonal variation | mW/m² | 12 monthly averages |
| Clear-Sky UV | Potential UV without clouds | mW/m² | Maximum exposure scenario |

#### Data Access

**Primary Access:**
- **Portal:** CDC Environmental Public Health Tracking Network Data Explorer
- **URL:** https://ephtracking.cdc.gov/DataExplorer/
- **Format:** Raster (GeoTIFF) for gridded data; CSV for county aggregates
- **Aggregation:** Pre-computed county averages available

**NASA Data Source:**
- **URL:** https://disc.gsfc.nasa.gov/ (NASA GES DISC - Goddard Earth Sciences Data and Information Services Center)
- **Product:** OMI/Aura Surface UVB Irradiance and Erythemal Dose Daily L3 Global Gridded 1.0 degree x 1.0 degree
- **Format:** HDF5, NetCDF

**R Example:**
```r
library(terra)
library(sf)
library(tidyverse)

# Read county boundaries
counties <- st_read("path/to/county_boundaries.shp")

# Read UV raster (GeoTIFF from CDC or NASA)
uv_raster <- rast("UV_irradiance_annual_2015.tif")

# Extract county-level averages using zonal statistics
county_uv <- extract(
  uv_raster,
  vect(counties),
  fun = mean,
  na.rm = TRUE,
  bind = TRUE
)

# Result: County FIPS with mean UV irradiance
```

#### Data Quality

**Strengths:**
- Satellite-based daily observations (high temporal resolution)
- Cloud-adjusted (accounts for actual sky conditions)
- Validated against ground UV monitors (USDA UV-B network)
- Only publicly-available, spatially-resolved, long-term UV dataset for CONUS

**Limitations:**
- Requires GIS processing to aggregate from 4km grid to counties
- Not available for all years (2005-2015 comprehensive; check CDC for updates)
- Does not account for surface albedo (snow reflection can increase UV)

**Validation:** EPA/USDA UV-B monitoring network comparison shows mean absolute error <10%

#### Use Cases

1. **High-Resolution Exposure Assessment:** 4km grid allows within-county variation analysis
2. **Cloud-Adjusted Estimates:** More accurate than clear-sky models for actual UV exposure
3. **Daily UV Patterns:** Study short-term acute exposures (e.g., heat waves with high UV)
4. **Urban-Rural Gradients:** Examine UV differences within counties

---

### Source 3: NREL National Solar Radiation Database (NSRDB)

**Official Name:** National Renewable Energy Laboratory National Solar Radiation Database
**Status:** ✅ HIGHEST TEMPORAL RESOLUTION (Hourly/Half-Hourly, 1998-present)

#### Overview

The NSRDB is a comprehensive solar resource database developed by NREL for renewable energy applications but highly valuable for UV exposure assessment due to its high temporal resolution and long time series.

#### Coverage

- **Geographic:** United States (4km x 4km resolution, aggregable to county)
- **Temporal:** 1998-present, updated annually
- **Spatial Resolution:** 4km x 4km grid
- **Temporal Resolution:** Hourly (1998-2017), half-hourly (2018-present)

#### Variables Available

| Variable | Description | Units | Health Relevance |
|----------|-------------|-------|------------------|
| Global Horizontal Irradiance (GHI) | Total solar radiation on horizontal surface | W/m² | Total solar exposure |
| Direct Normal Irradiance (DNI) | Direct beam solar radiation | W/m² | Direct UV component |
| Diffuse Horizontal Irradiance (DHI) | Scattered solar radiation | W/m² | Scattered UV |
| Surface Albedo | Ground reflectance | Unitless (0-1) | Snow/ice UV reflection |
| Cloud Properties | Cloud type, optical depth | Various | UV attenuation |
| Aerosol Optical Depth | Atmospheric aerosol load | Unitless | UV attenuation |

#### Data Access

**Primary Access:**
- **URL:** https://nsrdb.nrel.gov/
- **Data Viewer:** Interactive map for point selection
- **Bulk Download:** Available via NREL API or Amazon Web Services (AWS) Open Data
- **Format:** HDF5, CSV (time series for specific locations)

**NREL API Access:**
```python
import requests
import pandas as pd

# NREL API endpoint for NSRDB
api_key = "YOUR_API_KEY"  # Register at https://developer.nrel.gov/signup/
api_url = "https://developer.nrel.gov/api/nsrdb/v2/solar/psm3-download.csv"

# Request data for a specific location (lat/lon) and year
params = {
    "api_key": api_key,
    "wkt": "POINT(-105.18 39.74)",  # Longitude, Latitude (Denver)
    "names": "2020",
    "attributes": "ghi,dni,dhi,surface_albedo",
    "interval": "60",  # 60-minute data
    "utc": "false",
    "email": "your_email@example.com"
}

response = requests.get(api_url, params=params)

# Parse CSV response
solar_data = pd.read_csv(io.StringIO(response.text), skiprows=2)

# For county-level: request data for multiple points or download raster products
```

**County-Level Aggregation:**
- NSRDB provides gridded data; county averages require spatial processing
- Alternative: Download point data for county centroids, interpolate

#### Data Quality

**Strengths:**
- Highest temporal resolution (hourly/half-hourly) allows detailed exposure assessment
- Validated against ground stations (98 SURFRAD, SOLRAD, ISIS stations)
- Serially complete (no missing data)
- Long time series (1998-present, 26+ years)
- Includes atmospheric properties (aerosols, clouds) affecting UV

**Limitations:**
- Designed for solar energy, not UV health applications (GHI is total solar, not UV-specific)
- County aggregation requires GIS processing
- Does not directly provide UV Index (requires conversion from GHI)

**Conversion to UV:** UV comprises ~5% of total solar radiation; UV-B (sunburn) ~1% of GHI. NREL provides PSM (Physical Solar Model) that can estimate UV from GHI.

#### Use Cases

1. **Hourly UV Exposure Patterns:** Analyze time-of-day UV exposure
2. **Cloud/Weather Effects:** Understand real-time UV attenuation
3. **Snow/Ice Reflection:** Surface albedo data captures UV enhancement from snow
4. **Long-Term Trends:** 1998-present allows climate change impact analysis
5. **Extreme UV Events:** Identify days with exceptionally high UV

---

## PART 2: DRINKING WATER QUALITY & VIOLATIONS

### Health Impacts

**Contaminants and Associated Diseases:**

| Contaminant | Health Impacts | Cancer Risk | Other Chronic Disease Risk |
|-------------|----------------|-------------|----------------------------|
| **PFAS (Per- and Polyfluoroalkyl Substances)** | Liver damage, thyroid disease, immune effects | Kidney, testicular cancer | Reproductive issues, developmental delays |
| **Lead** | Neurodevelopmental damage (IQ loss), cognitive impairment | None established | Cardiovascular disease, kidney disease, hypertension |
| **Arsenic** | Skin lesions, peripheral neuropathy | Bladder, lung, skin cancer (strong evidence) | Cardiovascular disease, diabetes |
| **Nitrates** | Methemoglobinemia (blue baby syndrome), thyroid effects | Possible bladder, colorectal cancer | None established |
| **Copper** | Gastrointestinal distress | None established | Liver, kidney damage (high doses) |
| **Disinfection Byproducts (DBPs)** | Reproductive effects | Bladder cancer | None established |
| **Bacteria (E. coli, Legionella)** | Acute gastrointestinal illness, Legionnaires' disease | None | Chronic kidney disease (repeated infections) |

**At-Risk Populations:**
- Infants (nitrates, lead)
- Pregnant women (lead, nitrates, PFAS)
- Elderly (Legionella, lead)
- Immunocompromised (bacteria, parasites)
- Children (lead, PFAS)

---

### Source 4: EPA Safe Drinking Water Information System (SDWIS)

**Official Name:** EPA Safe Drinking Water Information System - Federal Reporting Services
**Status:** ✅ LONGEST COMPREHENSIVE VIOLATIONS DATABASE (1993-present, 31+ years)

#### Overview

SDWIS is the official EPA database tracking compliance with the Safe Drinking Water Act for all public water systems serving 25+ people in the United States. It contains violation data, water quality measurements, and system characteristics.

#### Coverage

- **Geographic:** All public water systems, United States (~148,000 active systems)
- **Temporal:** 1993-present for violations; treatment data varies
- **System Types:** Community water systems (CWS), non-transient non-community (schools, workplaces), transient non-community (rest stops, campgrounds)
- **Update Frequency:** Quarterly (states report → EPA compiles)

#### Variables Available

**Water System Characteristics:**
- System ID (PWSID), system name
- County FIPS code(s) served
- Population served
- Water source type (groundwater, surface water, purchased)
- Number of service connections
- Treatment type

**Violation Data (100+ variables):**

| Violation Category | Variables | Health Significance |
|--------------------|-----------|---------------------|
| **Health-Based Violations** | MCL/MRDL exceedances for specific contaminants | Actual water quality failures |
| **Lead and Copper Rule** | Action Level Exceedances (>0.015 mg/L lead, >1.3 mg/L copper), 90th percentile values, number of samples | Lead neurotoxicity, cardiovascular |
| **Disinfection Byproducts** | Total trihalomethanes (TTHM), haloacetic acids (HAA5) | Cancer risk (bladder) |
| **Inorganic Contaminants** | Arsenic (>0.010 mg/L), nitrate (>10 mg/L), fluoride, selenium, mercury | Cancer, methemoglobinemia |
| **Organic Contaminants** | Pesticides, herbicides, solvents (benzene, vinyl chloride, TCE) | Cancer, liver/kidney damage |
| **Radionuclides** | Uranium, radium, gross alpha | Cancer (lung, bone) |
| **PFAS (2024+)** | PFOA, PFOS, PFHxS, PFNA, GenX (HFPO-DA), PFBS; Hazard Index | Cancer, developmental effects |
| **Microbiological** | Total coliform, E. coli presence | Acute GI illness, sepsis |
| **Monitoring/Reporting Violations** | Failure to test or report results | Unknown water quality |
| **Public Notification Violations** | Failure to notify consumers of violations | Information access |

**Key Health-Based Violation Types:**
1. **Maximum Contaminant Level (MCL) Violation:** Measured concentration exceeds federal limit
2. **Maximum Residual Disinfectant Level (MRDL):** Chlorine, chloramine too high
3. **Treatment Technique (TT) Violation:** Failure to use required treatment (e.g., lead/copper corrosion control)
4. **Action Level Exceedance:** Lead or copper above action levels (not MCLs, but trigger requirements)

#### Data Access

**Method 1: ECHO (Enforcement and Compliance History Online)**
- **URL:** https://echo.epa.gov/tools/data-downloads/sdwa-download-summary
- **Format:** CSV, Excel
- **Update:** Quarterly
- **Files Available:**
  - SDWA Violations: All violations by PWSID, date, contaminant
  - SDWA Systems: Water system characteristics
  - SDWA Enforcement Actions: EPA/state actions taken
  - SDWA Public Water Systems: Current active systems
  - SDWA Lead and Copper Rule: Detailed LCR sampling results

**Download Example:**
```r
library(tidyverse)

# Download SDWA violations data from ECHO
violations_url <- "https://echo.epa.gov/files/echodownloads/SDWA_VIOLATIONS.zip"

# Download and unzip
temp <- tempfile()
download.file(violations_url, temp)
unzip(temp, exdir = "sdwa_data")

# Read violations
violations <- read_csv("sdwa_data/SDWA_VIOLATIONS.csv")

# Filter to health-based violations
health_violations <- violations %>%
  filter(VIOLATION_CATEGORY_CODE == "Health Based")

# Aggregate to county level
county_violations <- health_violations %>%
  group_by(PRIMACY_AGENCY_CODE, COUNTY_SERVED) %>%
  summarize(
    total_violations = n(),
    systems_with_violations = n_distinct(PWSID),
    population_affected = sum(POPULATION_SERVED_COUNT, na.rm = TRUE),
    contaminants = paste(unique(CONTAMINANT_CODE), collapse = ", "),
    .groups = "drop"
  )
```

**Method 2: SDWIS Federal Reports Advanced Search**
- **URL:** https://sdwis.epa.gov/ords/sfdw_pub/r/sfdw/sdwis_fed_reports_public/
- **Interface:** Web-based query tool
- **Capabilities:** Custom queries by state, county, contaminant, date range
- **Export:** CSV, Excel

**Method 3: EPA Envirofacts API**
- **URL:** https://enviro.epa.gov/enviro/sdw_query.html
- **RESTful API:** Query by PWSID, ZIP code, city
- **Format:** JSON, XML, CSV

#### PFAS Regulations (2024)

**Historic Change:** On April 10, 2024, EPA finalized the first-ever national drinking water standards for PFAS:

| PFAS Compound | Maximum Contaminant Level (MCL) |
|---------------|--------------------------------|
| PFOA (perfluorooctanoic acid) | 4 parts per trillion (ppt) |
| PFOS (perfluorooctanesulfonic acid) | 4 ppt |
| PFHxS (perfluorohexanesulfonic acid) | \* |
| PFNA (perfluorononanoic acid) | \* |
| HFPO-DA (GenX) | \* |
| PFBS (perfluorobutanesulfonic acid) | \* |

\* Regulated as a mixture using Hazard Index ≤1

**Compliance Timeline:**
- **2027-2029:** Public water systems must complete initial monitoring
- **2029:** Systems must notify the public of PFAS levels
- **2031:** Systems must comply with PFAS MCLs

**Implication:** PFAS violations data will begin appearing in SDWIS 2027-2031

#### Data Quality

**Strengths:**
- Official regulatory compliance data
- Verified by states and EPA
- Comprehensive coverage (all public water systems ≥25 people)
- Long time series (1993-present, 31+ years)
- Includes population served (can weight by exposure)

**Limitations:**
- Only public water systems (does not cover private wells ~15% of US population)
- Reporting compliance varies by state
- Small systems (<500 people) monitored less frequently (every 3-9 years for some contaminants)
- Violations indicate non-compliance, not actual exposure levels
- Suppression: Systems with monitoring/reporting violations may have unknown water quality

**Known Issues:**
- Lead and Copper Rule: 90th percentile reported; individual tap results not public
- Transient systems (rest stops, campgrounds) less comprehensive monitoring
- Tribal water systems: Some exempt from federal reporting

#### Use Cases for County-Level Analysis

1. **Drinking Water Safety Assessment:** Identify counties with frequent violations
2. **Contaminant-Specific Analysis:** Map lead, arsenic, nitrate, PFAS violations by county
3. **Population Exposure:** Weight violations by population served
4. **Health Outcome Studies:** Link violations to cancer, cardiovascular disease, kidney disease incidence
5. **Environmental Justice:** Examine socioeconomic disparities in water quality violations
6. **Time Trends:** Track improvements or worsening 1993-2025

**County Aggregation Strategy:**
- Sum violations by county FIPS (systems can serve multiple counties; use COUNTY_SERVED field)
- Population-weighted metrics: (Σ population served by violating systems) / (total county population)
- Contaminant-specific rates: (systems with lead violations) / (total systems in county)

---

### Source 5: USGS Groundwater Quality Data

**Official Name:** USGS National Water Quality Assessment (NAWQA) / National Water Quality Network (NWQN)
**Status:** ✅ COMPREHENSIVE GROUNDWATER MONITORING (1990s-present)

#### Overview

USGS collects groundwater quality data from thousands of monitoring wells across the United States as part of the NAWQA and NWQN programs. This data complements EPA SDWIS by providing actual measured concentrations (not just violations) and covers private wells.

#### Coverage

- **Geographic:** ~2,100+ monitoring sites across United States
- **Temporal:** Varies by site; many sites 1990-present
- **Well Types:** Public supply wells, private domestic wells, monitoring wells
- **Update Frequency:** Continuous (varies by site; quarterly to annual sampling)

#### Variables Available (Groundwater Quality)

**Major Ions and Physical Properties:**
- pH, specific conductance, temperature
- Calcium, magnesium, sodium, potassium (water hardness components)
- Chloride, sulfate, bicarbonate

**Nutrients:**
- Nitrate (NO3), nitrite (NO2), ammonia
- Total nitrogen, total phosphorus

**Trace Elements (Heavy Metals):**
- Arsenic, lead, mercury, cadmium, chromium, manganese, selenium
- Uranium, strontium

**Organic Contaminants:**
- Volatile Organic Compounds (VOCs): 85+ compounds (benzene, trichloroethylene, MTBE, chloroform)
- Pesticides: 200+ compounds (atrazine, glyphosate, metolachlor, 2,4-D)
- PFAS: 24 compounds monitored (as of 2024)

**Pharmaceuticals and Personal Care Products:**
- 100+ compounds (antibiotics, hormones, caffeine, DEET)

**PFAS (2024 Update):**

USGS published groundwater PFAS data and predictive models in 2024:
- **Publication:** "PFAS in Groundwater Used for Drinking Water Supply" (USGS, 2024)
- **Findings:** 71-95 million people (45% of tap water samples) may rely on groundwater with detectable PFAS
- **Compounds Measured:** 32 PFAS compounds (including PFOA, PFOS, PFHxS, PFNA, GenX)
- **Detection Frequency:** Higher in urban areas, near industrial/military sites, airports (AFFF firefighting foam)

#### Data Access

**Primary Portal: USGS Water Quality Portal**
- **URL:** https://www.waterqualitydata.us/
- **Coverage:** USGS + EPA + state/tribal data (>400 million records)
- **Search:** By location (state, county, lat/lon box), date, parameter
- **Format:** CSV, TSV, XML, GeoJSON

**Example Query:**
```r
library(dataRetrieval)
library(tidyverse)

# Download PFAS data for a specific state (California) from groundwater wells
ca_pfas <- readWQPdata(
  statecode = "CA",
  siteType = "Well",
  characteristicName = c("Perfluorooctanoic acid", "Perfluorooctane sulfonic acid"),
  startDateLo = "2020-01-01",
  startDateHi = "2024-12-31"
)

# Download nitrate data for all wells in a county
fips_code <- "06037"  # Los Angeles County
county_nitrate <- readWQPdata(
  countycode = fips_code,
  siteType = "Well",
  characteristicName = "Nitrate",
  startDateLo = "2010-01-01"
)

# Summarize by county
county_summary <- county_nitrate %>%
  filter(ResultMeasureValue != "") %>%
  mutate(Nitrate_mg_L = as.numeric(ResultMeasureValue)) %>%
  group_by(CountyCode) %>%
  summarize(
    n_samples = n(),
    mean_nitrate = mean(Nitrate_mg_L, na.rm = TRUE),
    max_nitrate = max(Nitrate_mg_L, na.rm = TRUE),
    pct_above_MCL = mean(Nitrate_mg_L > 10, na.rm = TRUE) * 100  # MCL = 10 mg/L
  )
```

**Alternative: USGS National Water Information System (NWIS)**
- **URL:** https://waterdata.usgs.gov/nwis/qw
- **Web Interface:** Site-by-site query
- **Bulk Download:** Available for specific monitoring networks

#### PFAS Occurrence Data (2024)

**USGS Report:** "Predicted Probability of Detecting PFAS in Groundwater Used for Drinking Water Supply in the Contiguous United States"

- **Model:** Random forest model predicts PFAS detection probability using:
  - Land use (urban, agricultural)
  - Proximity to airports, military bases, industrial sites
  - Wastewater treatment plants
  - Population density
  - Geology
- **Resolution:** 1km x 1km grid (aggregable to county)
- **Output:** Probability of detecting ≥1 PFAS compound at ≥4 ppt (new EPA MCL)
- **Access:** USGS ScienceBase data repository

#### Data Quality

**Strengths:**
- Actual measured concentrations (not just exceedances)
- Covers private wells (not in SDWIS)
- High-quality analytical methods (USGS National Water Quality Laboratory)
- Long time series at some sites (trend analysis possible)
- Includes unregulated contaminants (PFAS, pharmaceuticals)

**Limitations:**
- Point measurements (not comprehensive county coverage)
- Not all counties have USGS monitoring wells
- Sampling frequency varies (some sites annual, others one-time)
- Private well sampling often one-time studies (not continuous monitoring)

**County-Level Aggregation:**
- Wells geocoded with lat/lon → assign to county FIPS
- Calculate county statistics: mean, median, max, % samples exceeding MCL
- Small-number suppression: <5 wells may not be representative

#### Use Cases

1. **Nitrate in Agricultural Counties:** High nitrate in Iowa, Nebraska, California Central Valley (fertilizer runoff)
2. **Arsenic in Western US:** Naturally occurring arsenic in arid West groundwater
3. **PFAS Hotspots:** Identify counties near airports, military bases with elevated PFAS
4. **Private Well Risk:** Estimate contamination in areas relying on private wells (not covered by SDWIS)
5. **Health Studies:** Link measured contaminant levels to cancer, kidney disease rates

**Example County-Level Metrics:**
- Mean arsenic concentration (µg/L)
- % wells exceeding arsenic MCL (10 µg/L)
- Nitrate trend (mg/L/year) over time
- PFAS detection frequency (% wells with detectable PFAS)

---

## PART 3: SUPERFUND & CONTAMINATED SITES

### Health Impacts

**Mixed Exposure at Hazardous Waste Sites:**

Superfund and contaminated sites typically have multiple chemicals present, making exposure assessment complex. Common contaminants and health effects:

| Contaminant Class | Example Chemicals | Health Impacts |
|-------------------|-------------------|----------------|
| **Heavy Metals** | Lead, arsenic, cadmium, chromium, mercury | Cancer (lung, bladder, kidney), neurological effects, kidney disease |
| **Volatile Organic Compounds** | Benzene, trichloroethylene (TCE), vinyl chloride, PERC | Cancer (leukemia, liver, kidney), liver toxicity, neurological effects |
| **Polycyclic Aromatic Hydrocarbons (PAHs)** | Benzo[a]pyrene, naphthalene | Cancer (lung, skin, bladder) |
| **Polychlorinated Biphenyls (PCBs)** | Aroclors | Cancer (liver, biliary tract), immune suppression, endocrine disruption |
| **Pesticides** | DDT, chlordane, dieldrin | Cancer (breast, liver), neurological effects, reproductive effects |
| **Dioxins/Furans** | TCDD (2,3,7,8-tetrachlorodibenzo-p-dioxin) | Cancer (multiple types), immune suppression, reproductive effects |
| **Radioactive Materials** | Uranium, radium, thorium | Cancer (lung, bone, kidney) |

**Exposure Pathways:**
- **Groundwater contamination → drinking water** (most common)
- **Soil contamination → ingestion (children), dermal contact, dust inhalation**
- **Air emissions → inhalation** (volatile chemicals)
- **Surface water contamination → recreational exposure, fish consumption**

**At-Risk Populations:**
- Children (hand-to-mouth behavior, developing organs)
- Pregnant women (developmental effects)
- Residents within 1-mile radius of site
- Subsistence fishers/gardeners (local food consumption)

---

### Source 6: EPA National Priorities List (NPL) Superfund Sites

**Official Name:** EPA National Priorities List (NPL) under Comprehensive Environmental Response, Compensation, and Liability Act (CERCLA)
**Status:** ✅ COMPREHENSIVE SITE INVENTORY (1,343 sites as of 2024)

#### Overview

The NPL is EPA's list of the most serious uncontrolled or abandoned hazardous waste sites in the United States eligible for long-term remedial cleanup under the Superfund program. Sites are prioritized using the Hazard Ranking System (HRS) based on contamination, exposure, and risk.

#### Coverage

- **Geographic:** United States, all states and territories
- **Site Count:** 1,343 final NPL sites (as of 2024)
  - 1,335 non-federal sites
  - 8 federal facility sites
  - 45 sites deleted from NPL (cleanup complete)
- **Temporal:** 1980-present (CERCLA established December 1980)
- **Update Frequency:** Ongoing (sites added/deleted based on cleanup progress)

#### Variables Available

**Site Identification:**
- Site ID (EPA ID number)
- Site name
- Address, city, county, state, ZIP
- Latitude/longitude (geocoded)
- Congressional district

**Site Status:**
- NPL status: Proposed, Final, Deleted
- NPL listing date
- Proposed date, final date
- Deletion date (if cleanup complete)

**Site Characteristics:**
- Contaminants present (200+ possible chemicals)
- Source of contamination (industrial facility, landfill, mining, etc.)
- Size (acres)
- Media affected (groundwater, soil, surface water, air)

**Cleanup Status:**
- Construction completion date
- Remedy selected
- Record of Decision (ROD) date
- Five-year review status

**Population Metrics:**
- Population within 1 mile
- Population within 4 miles
- Population using affected aquifer (for groundwater contamination)

#### Data Access

**Method 1: EPA NPL Sites by State**
- **URL:** https://www.epa.gov/superfund/national-priorities-list-npl-sites-state
- **Format:** HTML tables (state pages), PDF site fact sheets
- **Access:** Browse by state, view individual site profiles

**Method 2: EPA Superfund Site Search**
- **URL:** https://www.epa.gov/superfund/search-superfund-sites-where-you-live
- **Search:** By address, ZIP code, city, county, site name, EPA ID
- **Output:** Site profiles with contamination, cleanup status, documents

**Method 3: EPA Superfund Data Download (FOIA 15 Dataset)**
- **Description:** Comprehensive Superfund data extract
- **Access:** FOIA request or EPA FTP site (if available)
- **Format:** Excel, CSV, Access database
- **Contents:** All NPL sites with full details (contaminants, RODs, cleanup milestones, population data)

**Method 4: EPA Envirofacts CERCLIS Database**
- **URL:** https://enviro.epa.gov/enviro/ef_metadata_html.cerclis_query
- **API:** RESTful queries
- **Format:** JSON, XML, CSV

**Method 5: EPA Superfund Interactive Map**
- **URL:** https://epa.maps.arcgis.com/apps/webappviewer/index.html?id=33cebcdfdd1b4c3a8b51d416956c41f1
- **Features:** Interactive map of all NPL sites, filter by status, state
- **Export:** GIS layers (Shapefile, KML, GeoJSON)

**Download Example (Shapefile):**
```r
library(sf)
library(tidyverse)

# Download NPL sites shapefile from EPA ArcGIS
npl_url <- "https://services.arcgis.com/cJ9YHowT8TU7DUyn/arcgis/rest/services/Superfund_NPL_Sites/FeatureServer/0/query?where=1%3D1&outFields=*&outSR=4326&f=geojson"

# Read NPL sites
npl_sites <- st_read(npl_url)

# Aggregate to county level
county_npl <- npl_sites %>%
  st_drop_geometry() %>%
  group_by(STATE, COUNTY) %>%
  summarize(
    npl_sites_count = n(),
    final_sites = sum(STATUS == "Final NPL", na.rm = TRUE),
    deleted_sites = sum(STATUS == "Deleted", na.rm = TRUE),
    construction_complete = sum(CONSTRUCTION_COMPLETION_DATE != "", na.rm = TRUE),
    population_1mi = sum(POPULATION_1MI, na.rm = TRUE),
    .groups = "drop"
  )

# Merge with county FIPS codes
# (Requires county name to FIPS crosswalk)
```

#### Key Contaminants at NPL Sites (Most Common)

| Contaminant | % of Sites | Primary Health Concern |
|-------------|-----------|------------------------|
| Lead | 44% | Neurotoxicity, developmental delays |
| Trichloroethylene (TCE) | 42% | Cancer (kidney, liver), neurological |
| Benzene | 39% | Leukemia |
| Arsenic | 37% | Cancer (lung, bladder, skin) |
| Cadmium | 32% | Kidney damage, cancer |
| Chromium (VI) | 31% | Lung cancer |
| Polychlorinated biphenyls (PCBs) | 30% | Cancer, immune suppression |
| Chloroform | 26% | Liver toxicity, cancer |
| Vinyl chloride | 20% | Liver cancer (angiosarcoma) |

**Source:** EPA NPL site data analysis

#### Data Quality

**Strengths:**
- Official federal contamination database
- Comprehensive site characterization (years of investigation)
- Long time series (1980-present, 44 years)
- Population exposure estimates included
- Cleanup status tracking

**Limitations:**
- Only most serious sites (HRS score ≥28.5) listed on NPL; thousands of other contaminated sites not included
- Site boundaries may extend beyond reported location
- Contaminant data: Not all contaminants may be identified at time of listing
- Exposure: Proximity-based (1-mile, 4-mile) is crude; actual exposure depends on groundwater flow, air dispersion

**Note:** NPL sites are a subset of all hazardous waste sites. EPA's CERCLIS database (~40,000 sites) includes assessed sites not on NPL. Most states have additional state Superfund programs.

#### Use Cases for County-Level Analysis

1. **Cancer Cluster Investigation:** Identify counties with multiple NPL sites for elevated cancer incidence studies
2. **Environmental Justice:** Examine racial/socioeconomic disparities in NPL site proximity
3. **Exposure Assessment:** Estimate population exposed (sum population_1mi for all sites in county)
4. **Cleanup Progress Tracking:** Monitor construction completion over time
5. **Groundwater Risk:** Identify counties with groundwater-contaminated sites (drinking water risk)

**County-Level Metrics:**
- Number of NPL sites per county
- Number of final vs. proposed vs. deleted sites
- Total population within 1 mile of all sites in county
- Contaminant diversity (number of unique chemicals across county sites)
- Cleanup completion rate (% sites with construction complete)

---

### Source 7: EPA ACRES Brownfields Properties

**Official Name:** EPA Assessment, Cleanup and Redevelopment Exchange System (ACRES) Brownfields Database
**Status:** ✅ COMPREHENSIVE BROWNFIELDS INVENTORY (Program start ~1995-present)

#### Overview

ACRES tracks properties enrolled in EPA's Brownfields Program, which focuses on cleaning up and redeveloping contaminated properties (typically lower-risk than Superfund sites). Brownfields are abandoned or underused commercial/industrial properties where environmental contamination is suspected or confirmed.

#### Coverage

- **Geographic:** United States, county-level
- **Property Count:** 50,000+ properties tracked (cumulative since program start)
- **Temporal:** Program established 1995; ACRES data ~2002-present
- **Property Types:** Former industrial facilities, gas stations, dry cleaners, manufacturing plants, rail yards

#### Variables Available

**Property Information:**
- Property ID (EPA Brownfields ID)
- Property name
- Address, city, county, state, ZIP code
- Latitude/longitude
- Property size (acres)

**Grant Information:**
- Grant type (Assessment, Cleanup, Revolving Loan Fund, Multipurpose)
- Grant recipient (municipality, tribe, nonprofit, state)
- Grant amount ($)
- Grant year

**Contamination Type:**
- Suspected contaminants (petroleum, heavy metals, solvents, etc.)
- Environmental media affected (soil, groundwater)

**Site Status:**
- Assessment status (Phase I, Phase II complete)
- Cleanup status (cleanup plan, cleanup complete, no further action)
- Redevelopment plans (residential, commercial, industrial, green space)

**Cleanup Progress:**
- Cleanup start date, completion date
- Institutional controls (land use restrictions)

#### Data Access

**Method 1: Data.gov - ACRES Brownfields Properties**
- **URL:** https://catalog.data.gov/dataset/acres-brownfields-properties
- **Format:** CSV, Shapefile, Web services
- **Update Frequency:** Quarterly

**Download Example:**
```r
library(tidyverse)

# Download ACRES Brownfields data from Data.gov
acres_url <- "https://edg.epa.gov/metadata/rest/document?id=%7B6DBDF07C-58F4-4C24-949D-E166E0795CAB%7D"

# Alternative: Use EPA Envirofacts API
library(httr)

acres_api <- "https://data.epa.gov/efservice/ACRES/..."  # API endpoint

# Parse and aggregate to county level
brownfields_data <- read_csv("acres_brownfields.csv")

county_brownfields <- brownfields_data %>%
  group_by(STATE, COUNTY) %>%
  summarize(
    total_properties = n(),
    assessment_grants = sum(GRANT_TYPE == "Assessment", na.rm = TRUE),
    cleanup_grants = sum(GRANT_TYPE == "Cleanup", na.rm = TRUE),
    total_grant_amount = sum(GRANT_AMOUNT, na.rm = TRUE),
    cleanup_complete = sum(STATUS == "Cleanup Complete", na.rm = TRUE),
    total_acres = sum(PROPERTY_ACRES, na.rm = TRUE),
    .groups = "drop"
  )
```

**Method 2: EPA Cleanups in My Community**
- **URL:** https://www.epa.gov/cleanups/cleanups-my-community
- **Search:** By address, ZIP, city, county
- **Output:** Interactive map, site profiles
- **Includes:** Brownfields + Superfund + RCRA facilities

**Method 3: State Brownfields Databases**
- Many states maintain their own brownfields inventories with more detail
- Examples:
  - **Michigan:** Part 201/213 sites
  - **New York:** Environmental Restoration Program sites
  - **California:** Land Reuse and Revitalization Act sites
- Access: State environmental agency websites

#### Data Quality

**Strengths:**
- Comprehensive tracking of EPA Brownfields grants
- Grant funding data (economic impact)
- Redevelopment outcomes (community benefit)
- Updates reflect ongoing cleanup progress

**Limitations:**
- Only properties receiving EPA grants (state/private cleanups not included)
- Contaminant data less detailed than Superfund (lower priority sites)
- "Suspected" contamination vs. confirmed (some sites may be clean)
- Voluntary program (not regulatory like Superfund)

**Coverage Gap:** ACRES only includes properties in EPA Brownfields Program. Estimated 450,000-1,000,000 brownfield sites exist in US; ACRES covers ~10% with EPA involvement.

#### Use Cases for County-Level Analysis

1. **Economic Revitalization:** Track brownfields redevelopment (job creation, tax base)
2. **Community Health:** Assess contamination burden in urban areas (brownfields concentrated in cities)
3. **Environmental Justice:** Examine distribution of brownfields in low-income, minority neighborhoods
4. **Land Use Transition:** Identify counties transforming industrial areas to housing, parks, commercial
5. **Grant Funding Patterns:** Analyze federal investment in cleanup by county

**County-Level Metrics:**
- Number of brownfield properties per 10,000 residents
- Total acres of brownfields in county
- EPA grant funding received per capita
- % brownfields with cleanup complete
- Redevelopment type distribution (residential, commercial, green space)

---

### Source 8: EPA EJSCREEN Proximity to NPL Sites

**Official Name:** EPA EJSCREEN Environmental Justice Screening and Mapping Tool (Version 2.3, 2024)
**Status:** ✅ INCLUDES SUPERFUND PROXIMITY INDICATOR (Updated annually)

#### Overview

EJSCREEN is EPA's environmental justice screening tool that combines environmental indicators with demographic and socioeconomic data to identify communities with disproportionate environmental burdens. One indicator is proximity to NPL Superfund sites.

#### Coverage

- **Geographic:** United States, census block group level (aggregable to county)
- **Temporal:** 2016-2024 (Version 2.3 released 2024)
- **Granularity:** 242,335 census block groups (~1,000-3,000 people per block group)
- **Update Frequency:** Annual

#### Variables Available

**Superfund Proximity Indicator:**
- **Count of NPL sites within 5km:** Number of Superfund sites within 5-kilometer radius
- **Proximity index:** Distance-weighted count (closer sites weighted more heavily)
- **Nearest NPL site distance:** Distance in kilometers to closest site

**Combined with Demographics:**
- % low-income, % minority
- Educational attainment, linguistic isolation
- Unemployment rate
- EJSCREEN index: Environmental indicator × demographic index

#### Data Access

**Interactive Tool:**
- **URL:** https://ejscreen.epa.gov/mapper/
- **Features:** Map block groups, filter by indicator, demographics
- **Output:** PDF reports, CSV data export for selected area

**Bulk Download:**
- **URL:** https://www.epa.gov/ejscreen/download-ejscreen-data
- **Format:** Geodatabase (ESRI FileGDB), CSV
- **Size:** ~3 GB (all 242,335 block groups, 200+ variables)

**Download Example:**
```r
library(sf)
library(tidyverse)

# Download EJSCREEN geodatabase (large file)
ejscreen_url <- "https://gaftp.epa.gov/EJSCREEN/2024/EJSCREEN_2024_StatePctile_with_AS_CNMI_GU_VI.gdb.zip"

temp <- tempfile()
download.file(ejscreen_url, temp)
unzip(temp, exdir = "ejscreen_data")

# Read geodatabase
ejscreen <- st_read("ejscreen_data/EJSCREEN_2024_StatePctile.gdb", layer = "Block_Groups")

# Extract Superfund proximity data
superfund_prox <- ejscreen %>%
  st_drop_geometry() %>%
  select(
    GEOID = ID,  # Census block group ID
    STATE_NAME,
    CNTY_NAME,
    NPL_COUNT_5KM = D_NPL_5KM,  # Count of NPL sites within 5km
    NPL_PROX_INDEX = D_NPL_PROX,  # Proximity index
    PCT_LOW_INCOME = LOWINCPCT,
    PCT_MINORITY = MINORPCT
  )

# Aggregate to county level
# (Block group GEOID first 5 digits = county FIPS)
county_superfund <- superfund_prox %>%
  mutate(COUNTY_FIPS = substr(GEOID, 1, 5)) %>%
  group_by(COUNTY_FIPS, STATE_NAME, CNTY_NAME) %>%
  summarize(
    mean_npl_count_5km = mean(NPL_COUNT_5KM, na.rm = TRUE),
    max_npl_count_5km = max(NPL_COUNT_5KM, na.rm = TRUE),
    mean_prox_index = mean(NPL_PROX_INDEX, na.rm = TRUE),
    .groups = "drop"
  )
```

#### Data Quality

**Strengths:**
- High spatial resolution (block group)
- Combines environmental and demographic data (environmental justice analysis)
- Annual updates
- Easy aggregation to county (block group GEOID prefix)

**Limitations:**
- Proximity-based indicator (does not measure actual contamination or exposure)
- 5km radius may be too broad (groundwater contamination can travel farther; air emissions usually more localized)
- Does not account for site characteristics (size, contaminants, cleanup status)

#### Use Cases

1. **Environmental Justice Analysis:** Identify counties where low-income/minority populations disproportionately live near Superfund sites
2. **Exposure Screening:** Prioritize counties for health studies based on Superfund proximity burden
3. **Within-County Disparities:** Examine block group-level variation in Superfund exposure
4. **Trend Analysis:** Track changes in proximity burden 2016-2024 (new sites listed, old sites deleted)

---

## Data Integration and Analysis Strategies

### Multi-Source Integration for Comprehensive Environmental Health Assessment

**Recommended County-Level Variables to Collect:**

#### UV Radiation (3 variables)
1. **Annual average UV irradiance (Wh/m²)** - NCI/CDC County UV, most recent 5-year period
2. **UV Index mean** - NCI/CDC, summer months (highest exposure)
3. **UV trend (Wh/m²/decade)** - NCI/CDC, 1961-2024 time series

#### Drinking Water Quality (10 variables)
1. **Count of health-based MCL violations** - EPA SDWIS, annual
2. **Population served by systems with violations** - EPA SDWIS, annual
3. **Lead action level exceedances** - EPA SDWIS, most recent 3-year period (90th percentile)
4. **Arsenic MCL violations (% systems)** - EPA SDWIS, annual
5. **Nitrate MCL violations (% systems)** - EPA SDWIS, annual
6. **Mean arsenic concentration (µg/L)** - USGS groundwater, most recent 10 years
7. **Mean nitrate concentration (mg/L)** - USGS groundwater, most recent 10 years
8. **% groundwater wells with detectable PFAS** - USGS 2024 model predictions
9. **PFAS MCL violations (count)** - EPA SDWIS, 2027+ (future)
10. **Total coliform/E. coli violations** - EPA SDWIS, annual

#### Superfund & Contaminated Sites (5 variables)
1. **Count of final NPL Superfund sites** - EPA NPL, current
2. **Population within 1 mile of all NPL sites (sum)** - EPA NPL, current
3. **Count of NPL sites with groundwater contamination** - EPA NPL, current
4. **Count of EPA Brownfields properties** - EPA ACRES, cumulative
5. **Mean NPL site count within 5km (block group average)** - EPA EJSCREEN, annual

**Total Priority Variables: 18**

---

### R Code Example: Comprehensive County-Level Data Collection

```r
library(tidyverse)
library(sf)
library(httr)
library(dataRetrieval)

# Function to collect all environmental health data for a county
collect_county_env_health <- function(county_fips) {

  ## 1. UV RADIATION DATA (NCI/CDC)
  uv_api <- "https://gis.cancer.gov/api/uv-exposure"

  uv_data <- GET(
    uv_api,
    query = list(
      fips = county_fips,
      period = "2015-2019",  # Most recent 5-year
      format = "json"
    )
  ) %>%
    content("parsed") %>%
    as_tibble()

  ## 2. DRINKING WATER VIOLATIONS (EPA SDWIS via ECHO)
  # Download SDWIS violations CSV (quarterly file)
  sdwa_violations <- read_csv("SDWA_VIOLATIONS.csv") %>%
    filter(COUNTY_SERVED == county_fips) %>%
    filter(VIOLATION_CATEGORY_CODE == "Health Based") %>%
    filter(year(COMPLIANCE_BEGIN_DATE) == 2024)

  # Summarize
  water_quality <- sdwa_violations %>%
    summarize(
      health_violations = n(),
      population_affected = sum(POPULATION_SERVED_COUNT, na.rm = TRUE),
      lead_violations = sum(CONTAMINANT_CODE == "1030", na.rm = TRUE),  # Lead code
      arsenic_violations = sum(CONTAMINANT_CODE == "1005", na.rm = TRUE),
      nitrate_violations = sum(CONTAMINANT_CODE == "1040", na.rm = TRUE)
    )

  ## 3. USGS GROUNDWATER QUALITY
  # Get county lat/lon bounding box (requires county shapefile)
  county_bbox <- ... # Extract bounding box for county

  # Download nitrate data
  groundwater_nitrate <- readWQPdata(
    countycode = county_fips,
    siteType = "Well",
    characteristicName = "Nitrate",
    startDateLo = "2014-01-01",
    startDateHi = "2024-12-31"
  ) %>%
    filter(ResultMeasureValue != "") %>%
    summarize(
      n_samples = n(),
      mean_nitrate = mean(as.numeric(ResultMeasureValue), na.rm = TRUE)
    )

  # Download arsenic data
  groundwater_arsenic <- readWQPdata(
    countycode = county_fips,
    siteType = "Well",
    characteristicName = "Arsenic",
    startDateLo = "2014-01-01"
  ) %>%
    filter(ResultMeasureValue != "") %>%
    summarize(
      mean_arsenic = mean(as.numeric(ResultMeasureValue), na.rm = TRUE)
    )

  ## 4. NPL SUPERFUND SITES
  npl_sites <- st_read("NPL_Sites.shp") %>%
    st_drop_geometry() %>%
    filter(COUNTY_FIPS == county_fips) %>%
    summarize(
      npl_count = n(),
      population_1mi = sum(POPULATION_1MI, na.rm = TRUE),
      groundwater_sites = sum(str_detect(MEDIA_AFFECTED, "Groundwater"), na.rm = TRUE)
    )

  ## 5. BROWNFIELDS
  brownfields <- read_csv("ACRES_Brownfields.csv") %>%
    filter(COUNTY_FIPS == county_fips) %>%
    summarize(
      brownfield_count = n()
    )

  ## 6. EJSCREEN SUPERFUND PROXIMITY
  ejscreen <- st_read("EJSCREEN_2024.gdb", layer = "Block_Groups") %>%
    st_drop_geometry() %>%
    filter(substr(ID, 1, 5) == county_fips) %>%
    summarize(
      mean_npl_5km = mean(D_NPL_5KM, na.rm = TRUE)
    )

  ## COMBINE ALL DATA
  county_env_health <- tibble(
    county_fips = county_fips,
    # UV
    uv_annual_mean = uv_data$AvgDailyUV,
    # Water
    water_violations = water_quality$health_violations,
    water_pop_affected = water_quality$population_affected,
    lead_violations = water_quality$lead_violations,
    arsenic_violations = water_quality$arsenic_violations,
    nitrate_violations = water_quality$nitrate_violations,
    mean_groundwater_nitrate = groundwater_nitrate$mean_nitrate,
    mean_groundwater_arsenic = groundwater_arsenic$mean_arsenic,
    # Superfund
    npl_sites = npl_sites$npl_count,
    npl_population_1mi = npl_sites$population_1mi,
    npl_groundwater_sites = npl_sites$groundwater_sites,
    brownfield_count = brownfields$brownfield_count,
    mean_npl_prox_5km = ejscreen$mean_npl_5km
  )

  return(county_env_health)
}

# Run for all counties
all_counties <- c("01001", "01003", ...)  # All county FIPS codes
county_data <- map_dfr(all_counties, collect_county_env_health)

# Save
write_csv(county_data, "county_environmental_health_data.csv")
```

---

## Data Limitations and Quality Considerations

### UV Radiation Data
**Limitation:** Modeled estimates do not capture within-county variation (mountains, valleys) or individual behavior (time outdoors, sunscreen use)
**Recommendation:** Use as county-level average; acknowledge individual exposure variation in analysis

### Drinking Water Violations Data
**Limitation:** Only covers public water systems (85% of population); does not include private wells (43 million Americans)
**Recommendation:** Supplement with USGS groundwater quality data for areas with high private well use

### NPL Superfund Sites
**Limitation:** Proximity does not equal exposure; groundwater flow direction, air dispersion, and site characteristics matter
**Recommendation:** Use proximity as screening tool; combine with EJSCREEN exposure indicators

### PFAS Data
**Limitation:** PFAS regulations are new (2024); historical exposure data limited; full compliance monitoring won't start until 2027
**Recommendation:** Use USGS PFAS occurrence predictions (2024 model) for historical estimates

---

## Related Data Sources (Already Documented in SDOH Dataset)

The following environmental health data sources are already documented in other comprehensive files:

1. **Air Pollution:** EPA AQS, EPA NEI, IMPROVE, CSN, CASTNET - See ATMOSPHERIC_EMISSIONS_CHEMISTRY_COMPREHENSIVE.md
2. **Radon Exposure:** EPA Radon Zones, CDC Radon Testing - See RADON_OIL_GAS_ENERGY_COMPREHENSIVE.md
3. **Toxic Chemical Releases:** EPA TRI - See TRI_COMPREHENSIVE_DOCUMENTATION.md
4. **Stream Water Quality:** USGS NWIS - See USGS_Water_Quality_Parameters_County_Level_COMPREHENSIVE.md
5. **Land Cover:** NLCD - See NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md
6. **Climate Extremes:** NOAA Storm Events - See NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md

---

## Update Schedule

| Data Source | Update Frequency | Expected Next Update |
|-------------|------------------|----------------------|
| NCI/CDC UV Exposure | 5-year intervals | 2025 (2020-2024 period) |
| NASA/CDC UV Irradiance | Periodic | Check CDC Tracking Network |
| NREL NSRDB | Annual | 2025 data (late 2026) |
| EPA SDWIS Violations | Quarterly | Every 3 months |
| USGS Groundwater Quality | Continuous | Ongoing (check Water Quality Portal) |
| EPA NPL Sites | Ongoing | Check EPA Superfund site for new listings |
| EPA ACRES Brownfields | Quarterly | Every 3 months |
| EPA EJSCREEN | Annual | Version 2.4 (late 2025) |

---

## API Keys and Access Requirements

**No API Keys Required:**
- NCI/CDC UV Exposure Tool (public)
- NASA GES DISC (requires free Earthdata login)
- NREL NSRDB (requires free API key: https://developer.nrel.gov/signup/)
- EPA SDWIS/ECHO (public)
- USGS Water Quality Portal (public)
- EPA NPL/ACRES/EJSCREEN (public)

**Free Registration:**
- NREL API Key: https://developer.nrel.gov/signup/
- NASA Earthdata Login: https://urs.earthdata.nasa.gov/

---

## Citation

When using these data sources, cite appropriately:

**UV Exposure:**
> National Cancer Institute. (2024). UV Exposure Database. Retrieved from https://gis.cancer.gov/tools/uv-exposure/

**Drinking Water:**
> U.S. Environmental Protection Agency. (2024). Safe Drinking Water Information System (SDWIS). Retrieved from https://www.epa.gov/ground-water-and-drinking-water/safe-drinking-water-information-system-sdwis-federal-reporting

> U.S. Geological Survey. (2024). National Water Quality Assessment Project. Retrieved from https://www.usgs.gov/mission-areas/water-resources/science/national-water-quality-assessment-project

**Superfund:**
> U.S. Environmental Protection Agency. (2024). National Priorities List (NPL). Retrieved from https://www.epa.gov/superfund/superfund-national-priorities-list-npl

---

**Document Version:** 1.0
**Last Updated:** November 12, 2025
**Status:** Production-ready
**Total Sources Documented:** 8
**Total Variables:** 18 priority county-level variables
