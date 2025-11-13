# COMPREHENSIVE DOCUMENTATION: NLCD & NOAA STORM EVENTS DATA

## PART 1: NATIONAL LAND COVER DATABASE (NLCD)

---

### 1.1 NLCD OVERVIEW

The National Land Cover Database (NLCD) is produced by the Multi-Resolution Land Characteristics (MRLC) Consortium, providing comprehensive land cover information for the United States at 30-meter resolution using Landsat satellite imagery.

**Primary Source:** https://www.mrlc.gov/

**Data Provider:** U.S. Geological Survey (USGS) Earth Resources Observation and Science (EROS) Center

**Spatial Coverage:** Conterminous United States (CONUS), with some products available for Alaska, Hawaii, and Puerto Rico

---

### 1.2 ALL AVAILABLE NLCD YEARS AND RELEASES

#### Legacy NLCD Products (2-3 Year Intervals)

| Product | Release Date | Epochs Included | Notes |
|---------|--------------|-----------------|-------|
| NLCD 1992 | Late 1990s | 1992 | First national land cover dataset |
| NLCD 2001 | Mid-2000s | 2001 | Baseline for modern NLCD series |
| NLCD 2006 | 2011 | 2001, 2006 | First change product |
| NLCD 2011 | 2014 | 2001, 2006, 2008, 2011 | Added intermediate years |
| NLCD 2016 | Early 2019 | 2001, 2004, 2006, 2008, 2011, 2013, 2016 | Expanded temporal coverage |
| NLCD 2019 | June 2021 (ver. 2.0) | 2001, 2004, 2006, 2008, 2011, 2013, 2016, 2019 | 8 epochs total |
| NLCD 2021 | July 20, 2023 | 2001-2021 (9 epochs) | Update-based release |

#### Annual NLCD Products (Annual Time Steps)

| Collection | Release Date | Temporal Coverage | Products Available |
|------------|--------------|-------------------|-------------------|
| Collection 1.0 | October 2024 | 1985-2023 (39 years) | All 6 products |
| Collection 1.1 | June 25, 2025 | 1985-2024 (40 years) | All 6 products |

**Key Innovation:** Annual NLCD provides data at annual time steps (yearly), representing a major improvement over the 2-3 year intervals used in legacy NLCD. Updates are planned every four years going forward.

---

### 1.3 COMPLETE NLCD PRODUCT SUITE

Annual NLCD Collection 1.1 includes **six raster-based land use and land cover science products**:

#### Product 1: Land Cover (LndCov)

**Description:** Depicts the predominant thematic land cover class within the mapping year with respect to broad categories of artificial or natural surface cover.

**16 Land Cover Classes (Modified Anderson Level II):**

| Code | Class Name | Description |
|------|------------|-------------|
| 11 | Open Water | Areas of open water, generally with less than 25% cover of vegetation/land cover |
| 12 | Perennial Ice/Snow | Areas characterized by perennial ice and/or snow |
| 21 | Developed, Open Space | Impervious surfaces account for less than 20% of total cover (lawns, parks, golf courses) |
| 22 | Developed, Low Intensity | Impervious surfaces 20-49% of total cover (single-family housing) |
| 23 | Developed, Medium Intensity | Impervious surfaces 50-79% of total cover (single-family housing) |
| 24 | Developed, High Intensity | Impervious surfaces 80-100% of total cover (apartments, commercial areas) |
| 31 | Barren Land | Rock, sand, clay, or other earthen material with little to no vegetation |
| 41 | Deciduous Forest | Areas dominated by trees where 75%+ of tree species shed foliage simultaneously |
| 42 | Evergreen Forest | Areas dominated by trees where 75%+ maintain leaves all year |
| 43 | Mixed Forest | Areas dominated by trees where neither deciduous nor evergreen species are >75% |
| 51 | Dwarf Scrub | Alaska only - shrubs less than 20 cm height |
| 52 | Shrub/Scrub | Areas dominated by shrubs less than 5 meters tall |
| 71 | Grassland/Herbaceous | Areas dominated by graminoid or herbaceous vegetation |
| 72 | Sedge/Herbaceous | Alaska only - dominated by sedges and forbs |
| 73 | Lichens | Alaska only - dominated by fruticose or foliose lichens |
| 74 | Moss | Alaska only - dominated by mosses |
| 81 | Pasture/Hay | Grasses, legumes, or grass-legume mixtures for livestock grazing or hay |
| 82 | Cultivated Crops | Areas used for production of annual crops (corn, soybeans, vegetables, cotton) |
| 90 | Woody Wetlands | Areas where forest or shrubland vegetation accounts for >20% cover and soil is periodically saturated |
| 95 | Emergent Herbaceous Wetlands | Areas where perennial herbaceous vegetation accounts for >80% cover and soil is periodically saturated |

**Anderson Classification System Connection:** NLCD uses a modified Anderson Level II classification system. The Anderson et al. 1976 classification is hierarchical with four levels (Level I general, Level II descriptive, Level III detailed, Level IV most detailed).

#### Product 2: Land Cover Change (LndChg)

**Description:** Depicts land cover change between one product year and the next, with changes represented in the latter year.

**Format:** Changes are represented using concatenated codes (e.g., 9590 indicates change from Emergent Herbaceous Wetlands [95] to Woody Wetlands [90]), creating an effective from-to transition matrix.

**Use Cases:**
- Urban growth tracking
- Wetland monitoring
- Agricultural expansion/contraction analysis
- Forest loss/gain assessment
- Climate impact assessment

#### Product 3: Land Cover Confidence (LndCnf)

**Description:** Depicts the probability value (0-100%) for the land cover class derived from the classification method.

**Purpose:** Provides users with uncertainty information to assess the reliability of land cover classifications for their specific applications.

#### Product 4: Fractional Impervious Surface (ImpSrf)

**Description:** Depicts the fractional surface area of the map unit (pixel) that is covered with artificial substrate or structures.

**Value Range:** 0-100% impervious cover

**Applications:**
- Urban density analysis
- Stormwater runoff modeling
- Heat island studies
- Urban growth monitoring

#### Product 5: Impervious Descriptor (ImpDsc)

**Description:** Depicts categorical data for developed land cover distinguishing roads from urban non-road and classifying impervious areas.

**12 Categories:**

| Category | Code | Description |
|----------|------|-------------|
| Primary Urban | primary_urban | Interstate and other major roads in urban areas |
| Primary Rural | primary_rural | Interstate and other major roads in rural areas |
| Secondary Urban | secondary_urban | Non-interstate highways in urban areas |
| Secondary Rural | secondary_rural | Non-interstate highways in rural areas |
| Tertiary Urban | tertiary_urban | Any two-lane road in urban areas |
| Tertiary Rural | tertiary_rural | Any two-lane road in rural areas |
| Thinned Urban | thinned_urban | Thinned roads in urban areas |
| Thinned Rural | thinned_rural | Thinned roads in rural areas |
| Nonroad Urban | nonroad_urban | Residential/commercial/industrial, parks, golf courses (urban) |
| Nonroad Rural | nonroad_rural | Developed areas not roads or energy production (rural) |
| Energy Production Urban | energyprod_urban | Energy production sites in urban areas |
| Energy Production Rural | energyprod_rural | Energy production sites in rural areas |

**Purpose:** Allows deeper analysis of developed features by distinguishing transportation infrastructure from other built surfaces.

#### Product 6: Tree Canopy Cover (TreeCnp)

**Description:** Depicts the percentage (0-100%) of tree canopy cover over any land cover class.

**Data Source:** Produced by USDA Forest Service in collaboration with USGS

**Value Range:** 0-100% canopy cover

**Applications:**
- Urban forestry management
- Carbon sequestration studies
- Habitat assessment
- Urban heat mitigation planning

#### Product 7: Spectral Change Day of Year (SpcChg)

**Description:** Depicts the day-of-year (DOY) on which a significant deviation in Landsat surface reflectance was detected within the calendar year.

**Value Range:**
- 0 = No change
- 1-366 = Day of year spectral change occurred

**Purpose:** Identifies timing of significant spectral changes (e.g., wildfires, harvests, floods) beyond seasonal variations, enabling precise temporal change tracking and disturbance detection.

**Use Cases:**
- Wildfire detection and timing
- Forest harvest monitoring
- Drought impact assessment
- Flood extent and timing

---

### 1.4 NLCD RANGELAND AND SHRUBLAND PRODUCTS (Regional)

**Geographic Coverage:** Western United States

**Collaboration:** USGS in partnership with Bureau of Land Management (BLM)

**Products:** RCMAP (Rangeland Condition Monitoring Assessment and Projection)

**Temporal Coverage:** 1985-2021 time series (annual)

**Nine Rangeland Components (30-meter resolution):**

1. Shrub cover (%)
2. Sagebrush cover (%) - *Artemisia* species
3. Big sagebrush cover (%)
4. Non-sagebrush shrub cover (%)
5. Herbaceous cover (%)
6. Annual herbaceous cover (%)
7. Perennial herbaceous cover (%)
8. Litter cover (%)
9. Bare ground cover (%)
10. Shrub height (cm)
11. Sagebrush height (cm)
12. Tree cover (%) - *NEW in latest version*

**Key Finding:** Sagebrush physically covers 86,219 km² (4.4%) but is present in 835,507 km² (42.9%) of the Western U.S. study area.

---

### 1.5 NLCD TECHNICAL SPECIFICATIONS

#### Spatial Resolution
- **30 meters** (consistent across all products, 1985-2024)
- Based on Landsat satellite imagery (Thematic Mapper, ETM+, OLI, OLI-2)
- Note: There is NO 10-meter NLCD product despite some confusion with other datasets

#### Coordinate System
- **Projection:** Albers Conic Equal Area
- **EPSG Code:** 5070 (NAD83 / Conus Albers)
- **Datum:** North American Datum 1983 (NAD83)
- **Standard Parallels:** 29.5° and 45.5°
- **Central Meridian:** -96°
- **Latitude of Origin:** 23°
- **False Easting/Northing:** 0, 0
- **Units:** Meters

#### Updated EPSG Codes:
- **EPSG:6350** - NAD83(2011) / Conus Albers (replaces NAD83(NSRS2007))
- **EPSG:3338** - NAD83 / Alaska Albers
- **EPSG:3310** - NAD83 / California Albers

#### Classification Methods

**Annual NLCD (2024) - Advanced Deep Learning:**
- Ensemble of chained deep learning models
- Harmonic time series analysis
- Leverages methodologies from legacy NLCD and LCMAP (Land Change Monitoring, Assessment, and Projection)
- Modern geospatial deep learning technologies
- Enables validated annual land cover products spanning nearly four decades

**Legacy NLCD (2001-2021):**
- Decision tree classification algorithms
- Multi-temporal Landsat imagery
- Ancillary data integration

#### Accuracy Assessment

**Collection 1.0 Reference Dataset:**
- **Phase 1:** 5,000 randomly distributed plots (30×30 meters each)
- **Phase 2:** Up to 5,000 additional stratified plots capturing changes and rare land cover types
- **Temporal Coverage:** Full 1985-2023 time series
- **Interpretation Sources:** Landsat imagery, high-resolution aerial photography, supporting data
- **Conducted by:** Team of trained image interpreters

**Assessment Approach:**
- Annual land cover classifications for each plot
- Captures rare land cover types
- Identifies temporal changes
- Thematic accuracy evaluation

---

### 1.6 COUNTY-LEVEL NLCD METRICS AND AGGREGATION

#### Key County-Level Metrics Available:

**Land Cover Statistics:**
- Acres or square kilometers by land cover class
- Percentage of county in each of 16 classes
- Developed land percentage (sum of classes 21-24)
- Total forest coverage (sum of classes 41-43)
- Agricultural land (sum of classes 81-82)
- Wetlands (classes 90, 95)

**Impervious Surface Metrics:**
- Average impervious surface percentage
- Total impervious area (acres/sq km)
- Distribution by impervious descriptor categories

**Tree Canopy Metrics:**
- Average tree canopy percentage
- Total tree canopy area (acres/sq km)
- Change in canopy over time

**Change Metrics:**
- Land cover transitions (from-to matrix by class)
- Net change in developed land
- Urban growth rate
- Forest loss/gain
- Agricultural conversion
- Wetland change

---

### 1.7 NLCD DATA ACCESS METHODS

#### Method 1: NLCD EVA Tool (Enhanced Visualization and Analysis) - **EASIEST FOR COUNTIES**

**URL:** https://www.mrlc.gov/eva/

**Features:**
- No GIS software required
- No advanced technical expertise needed
- User-friendly web interface
- Pick any county in the U.S.
- Compare any two NLCD landcover dates
- Instant change analysis (2001-2024)

**Outputs Provided:**
- Interactive graphs and charts
- Statistical breakdowns
- Downloadable spreadsheets (CSV, Excel)
- Acreage statistics by land cover class
- Special sections for:
  - Growth/loss of impervious surfaces
  - Forest change
  - Wetland change

**Partnership:** Developed by MRLC in partnership with NOAA's Office for Coastal Management

**Advantage:** EVA eliminates need for bulky data downloads or multi-layered online maps. Processes NLCD data server-side and delivers distilled county-level information.

#### Method 2: Bulk Raster Download

**URL:** https://www.mrlc.gov/data

**Formats:** GeoTIFF

**Options:**
- State-level tiles
- National mosaics
- Individual products (land cover, impervious, canopy, etc.)
- Individual years

**File Sizes:** Vary by product and geographic extent (national files are multiple GB)

**Use Case:** Best for users who need full raster data for custom analysis, large study areas, or integration with other spatial data.

#### Method 3: Google Earth Engine (GEE)

**Platform:** https://earthengine.google.com/

**Advantages:**
- Cloud-based processing (no downloads needed)
- Computational scalability
- Integration with other GEE datasets
- JavaScript or Python API

**NLCD Collections in GEE:**
- `'USGS/NLCD_RELEASES/2019_REL/NLCD'` - Legacy NLCD 2019
- `'USGS/NLCD_RELEASES/2021_REL/NLCD'` - Legacy NLCD 2021
- Annual NLCD collections (check GEE catalog for latest)

**Example Code - Loading NLCD and County Aggregation:**

```javascript
// Load NLCD dataset
var dataset = ee.ImageCollection('USGS/NLCD_RELEASES/2019_REL/NLCD');
var nlcd2016 = dataset.filter(ee.Filter.eq('system:index', '2016')).first();
var landcover = nlcd2016.select('landcover');

// Load county boundaries
var counties = ee.FeatureCollection('TIGER/2018/Counties');

// Filter to specific state (example: California)
var caCounties = counties.filter(ee.Filter.eq('STATEFP', '06'));

// Calculate zonal statistics
var zonalStats = landcover.reduceRegions({
  collection: caCounties,
  reducer: ee.Reducer.frequencyHistogram(),
  scale: 30
});

// Export results
Export.table.toDrive({
  collection: zonalStats,
  description: 'NLCD_County_Stats',
  fileFormat: 'CSV'
});
```

**Python (geemap) Example:**

```python
import ee
import geemap

# Initialize Earth Engine
ee.Initialize()

# Load NLCD
dataset = ee.Image("USGS/NLCD_RELEASES/2019_REL/NLCD/2019")
landcover = dataset.select("landcover")

# Load counties
states = ee.FeatureCollection("TIGER/2018/States")
counties = ee.FeatureCollection("TIGER/2018/Counties")

# Calculate zonal statistics
output_csv = 'nlcd_county_stats.csv'
geemap.zonal_stats_by_group(
    landcover,
    counties,
    output_csv,
    stat_type="SUM"
)
```

#### Method 4: ArcGIS Living Atlas

**Platform:** ArcGIS Online / ArcGIS Pro

**Services:**
- Web map services (WMS)
- Image services
- Feature services

**REST API Endpoints:** Available through USGS and MRLC

**Tools:**
- Tabulate Area (for county aggregation)
- Zonal Statistics
- Extract by Mask

**Use Case:** Best for users working within Esri ecosystem or needing web services.

#### Method 5: R Packages

##### Package 1: FedData

**Installation:**
```r
install.packages("FedData")
```

**Example - Download NLCD for County:**

```r
library(FedData)
library(tigris)
library(sf)
library(terra)

# Get county boundary
montgomery_county <- tigris::counties(state = "MD", cb = TRUE, year = 2022) %>%
  filter(str_detect(NAME, "Montgomery"))

# Download NLCD data for the county
nlcd_data <- FedData::get_nlcd(
  template = montgomery_county,
  label = "montgomery_county",
  year = 2021,
  dataset = "landcover"  # Options: 'landcover', 'impervious', 'canopy'
)

# Plot results
terra::plot(nlcd_data)
```

**Available Years:** 2001, 2004, 2006, 2008, 2011, 2016, 2019, 2021

**Available Datasets:** 'landcover' (default), 'impervious', 'canopy'

##### Package 2: terra (for raster processing)

**Example - Zonal Statistics by County:**

```r
library(terra)
library(sf)
library(tigris)

# Load NLCD raster
nlcd <- rast("/path/to/nlcd_2021_land_cover.tif")

# Load county boundaries
counties <- vect(tigris::counties(state = "CA", cb = TRUE, year = 2022))

# Crop and mask to counties
nlcd_counties <- crop(nlcd, counties)
nlcd_counties <- mask(nlcd_counties, counties)

# Calculate zonal statistics (frequency of each class)
zonal_stats <- zonal(nlcd_counties, counties, fun = "table")
```

##### Package 3: exactextractr (FASTEST for zonal statistics)

**Installation:**
```r
install.packages("exactextractr")
```

**Example - County Land Cover Statistics:**

```r
library(exactextractr)
library(terra)
library(sf)
library(tigris)
library(dplyr)
library(tidyr)

# Load NLCD
nlcd <- rast("/path/to/nlcd_2021_land_cover.tif")

# Load counties as sf object
counties <- st_as_sf(tigris::counties(cb = TRUE, year = 2022))

# Calculate area by land cover class for each county
county_lc_stats <- exact_extract(nlcd, counties, 'frac') %>%
  bind_cols(counties) %>%
  pivot_longer(
    cols = starts_with("frac_"),
    names_to = "class",
    values_to = "fraction"
  ) %>%
  mutate(
    lc_code = as.integer(str_remove(class, "frac_")),
    area_sqkm = fraction * st_area(geometry) / 1e6
  )

# Convert to acres
county_lc_stats <- county_lc_stats %>%
  mutate(area_acres = area_sqkm * 247.105)
```

**Key Advantage:** exactextractr performs weighted overlay based on fractional intersection of cells with polygons (most accurate for county boundaries).

---

### 1.8 COMPLETE COUNTY AGGREGATION WORKFLOW (R)

```r
library(FedData)
library(terra)
library(sf)
library(tigris)
library(exactextractr)
library(dplyr)
library(tidyr)

# Define NLCD class names
nlcd_classes <- tibble(
  code = c(11, 12, 21, 22, 23, 24, 31, 41, 42, 43, 51, 52,
           71, 72, 73, 74, 81, 82, 90, 95),
  class_name = c(
    "Open Water", "Perennial Ice/Snow", "Developed Open Space",
    "Developed Low Intensity", "Developed Medium Intensity",
    "Developed High Intensity", "Barren Land", "Deciduous Forest",
    "Evergreen Forest", "Mixed Forest", "Dwarf Scrub", "Shrub/Scrub",
    "Grassland/Herbaceous", "Sedge/Herbaceous", "Lichens", "Moss",
    "Pasture/Hay", "Cultivated Crops", "Woody Wetlands",
    "Emergent Herbaceous Wetlands"
  )
)

# Function to get NLCD statistics for a state
get_state_nlcd_stats <- function(state_abbr, year = 2021) {

  # Get all counties for state
  counties <- tigris::counties(state = state_abbr, cb = TRUE, year = 2022) %>%
    st_as_sf()

  # Download state NLCD data
  state_boundary <- tigris::states(cb = TRUE, year = 2022) %>%
    filter(STUSPS == state_abbr)

  nlcd <- FedData::get_nlcd(
    template = state_boundary,
    label = paste0(state_abbr, "_nlcd"),
    year = year,
    dataset = "landcover"
  )

  # Calculate exact zonal statistics
  county_stats <- exact_extract(nlcd, counties, 'frac') %>%
    bind_cols(counties) %>%
    select(GEOID, NAME, starts_with("frac_")) %>%
    pivot_longer(
      cols = starts_with("frac_"),
      names_to = "lc_code",
      values_to = "fraction"
    ) %>%
    mutate(lc_code = as.integer(str_remove(lc_code, "frac_"))) %>%
    filter(fraction > 0) %>%
    left_join(nlcd_classes, by = c("lc_code" = "code"))

  # Calculate areas
  county_stats <- county_stats %>%
    mutate(
      total_area_sqkm = as.numeric(st_area(geometry)) / 1e6,
      class_area_sqkm = fraction * total_area_sqkm,
      class_area_acres = class_area_sqkm * 247.105,
      percentage = fraction * 100
    ) %>%
    st_drop_geometry()

  # Add derived metrics
  summary_stats <- county_stats %>%
    group_by(GEOID, NAME) %>%
    summarize(
      total_developed_pct = sum(percentage[lc_code %in% 21:24]),
      total_forest_pct = sum(percentage[lc_code %in% 41:43]),
      total_agriculture_pct = sum(percentage[lc_code %in% 81:82]),
      total_wetlands_pct = sum(percentage[lc_code %in% c(90, 95)]),
      .groups = "drop"
    )

  # Combine detailed and summary statistics
  result <- list(
    detailed = county_stats,
    summary = summary_stats
  )

  return(result)
}

# Example usage
md_stats <- get_state_nlcd_stats("MD", year = 2021)

# Export results
write.csv(md_stats$detailed, "maryland_nlcd_detailed.csv", row.names = FALSE)
write.csv(md_stats$summary, "maryland_nlcd_summary.csv", row.names = FALSE)
```

---

### 1.9 NLCD DATA QUALITY AND LIMITATIONS

#### Temporal Considerations:
- **1992:** Single snapshot, different methodology than modern NLCD
- **2001-2021 (Legacy):** Consistent methodology, 2-3 year intervals
- **1985-2024 (Annual):** New deep learning methodology, annual time steps

#### Accuracy Notes:
- Overall accuracy varies by land cover class and region
- Higher accuracy for easily distinguishable classes (water, developed)
- Lower accuracy for spectrally similar classes (shrub vs. grassland)
- Change detection accuracy typically lower than single-date classification
- Accuracy assessments provided with each release

#### Known Limitations:
- 30-meter resolution may miss small features
- Mixed pixels at class boundaries
- Temporal mismatch between Landsat acquisition dates and "nominal" year
- Classification challenges in heterogeneous landscapes
- Some Alaska-specific classes not available for CONUS

#### Update Frequency:
- Legacy NLCD: Released every 2-5 years
- Annual NLCD: Annual products, with major collection updates every 4 years

---

## PART 2: NOAA STORM EVENTS DATABASE

---

### 2.1 NOAA STORM EVENTS OVERVIEW

The NOAA Storm Events Database documents storms and significant weather phenomena causing loss of life, injuries, property damage, and/or disruption to commerce.

**Primary Source:** https://www.ncdc.noaa.gov/stormevents/ (or https://www.ncei.noaa.gov/stormevents/)

**Data Provider:** National Weather Service (NWS), National Centers for Environmental Information (NCEI)

**Temporal Coverage:** January 1950 to April 2025 (continuously updated)

**Geographic Coverage:** United States (all 50 states, territories, coastal waters, and marine zones)

---

### 2.2 HISTORICAL DATABASE COVERAGE AND EVOLUTION

#### Period 1: 1950-1954 (5 years)
**Event Types Recorded:** Tornado ONLY

**Rationale:** Limited data collection capabilities, focus on most destructive events

#### Period 2: 1955-1992 (38 years)
**Event Types Recorded:** Tornado, Thunderstorm Wind, Hail

**Data Source:** Keyed from paper publications (Storm Data) into digital data

**Note:** Prior to 1972, tornado data from Storm Data; wind and hail data from U.S. Air Force real-time information

#### Period 3: 1993-1995 (3 years)
**Event Types Recorded:** Tornado, Thunderstorm Wind, Hail

**Data Source:** Extracted from Unformatted Text Files

**Transition Period:** Moving toward comprehensive digital database

#### Period 4: 1996-Present (29+ years)
**Event Types Recorded:** 48 standardized event types (see Section 2.3)

**Standard:** NWS Directive 10-1605

**Data Quality:** Since 1972, concerted effort to maintain agreement with NOAA publication "Storm Data"

**Most Recent Data:** Through April 2025

---

### 2.3 COMPLETE LIST OF 48 STORM EVENT TYPES (1996-Present)

As defined in **NWS Directive 10-1605**, the following 48 event types are recorded:

#### Convective Events (6 types)
1. **Tornado** - Violently rotating column of air in contact with ground
2. **Funnel Cloud** - Rotating column of air not in contact with ground
3. **Waterspout** - Tornado over water
4. **Thunderstorm Wind** - Winds ≥50 knots (58 mph) or causing damage
5. **Hail** - Frozen precipitation ≥1 inch diameter
6. **Lightning** - Lightning strike causing damage, injury, or death

#### Winter Weather Events (9 types)
7. **Winter Storm** - Significant winter precipitation event
8. **Winter Weather** - Winter precipitation not meeting storm criteria
9. **Ice Storm** - Significant ice accumulation
10. **Heavy Snow** - Snowfall meeting or exceeding local warning criteria
11. **Blizzard** - Sustained winds ≥35 mph with considerable falling/blowing snow
12. **Lake-Effect Snow** - Snow showers downwind of Great Lakes
13. **Sleet** - Frozen precipitation (ice pellets)
14. **Freezing Fog** - Fog with temperatures below freezing creating ice
15. **Avalanche** - Snow avalanche

#### Marine Events (11 types)
16. **Marine Thunderstorm Wind** - Thunderstorm winds ≥34 knots over water
17. **Marine Strong Wind** - Sustained winds 25-33 knots over water
18. **Marine High Wind** - Sustained winds ≥34 knots over water
19. **Marine Tropical Storm** - Tropical storm conditions over water
20. **Marine Hurricane/Typhoon** - Hurricane conditions over water
21. **Rip Current** - Strong, localized seaward flowing current
22. **Tsunami** - Sea wave caused by undersea earthquake or landslide
23. **Seiche** - Standing wave in enclosed or partially enclosed body of water
24. **Waterspout** - (Also listed under Convective)
25. **Coastal Flood** - Flooding of coastal areas
26. **Lakeshore Flood** - Flooding along Great Lakes shores
27. **Storm Surge/Tide** - Abnormal rise in water level from storm

#### Flooding Events (4 types)
28. **Flash Flood** - Rapid flooding in low-lying areas, usually within 6 hours
29. **Flood** - General overflowing of water onto normally dry land
30. **Coastal Flood** - (Also listed under Marine)
31. **Lakeshore Flood** - (Also listed under Marine)

#### Tropical Events (3 types)
32. **Tropical Storm** - Organized tropical system, winds 34-63 knots
33. **Tropical Depression** - Organized tropical system, winds <34 knots
34. **Hurricane (Typhoon)** - Intense tropical cyclone, winds ≥64 knots

#### Temperature Events (5 types)
35. **Heat** - Extended period of excessive heat
36. **Excessive Heat** - Extreme heat event meeting warning criteria
37. **Extreme Cold/Wind Chill** - Dangerous cold with wind chill
38. **Cold/Wind Chill** - Cold temperatures below criteria
39. **Frost/Freeze** - Freezing temperatures during growing season

#### Wind Events (3 types)
40. **High Wind** - Sustained winds ≥40 mph or gusts ≥58 mph
41. **Strong Wind** - Sustained winds 20-39 mph
42. **Dust Storm** - Severe dust storm reducing visibility

#### Other Events (7 types)
43. **Dust Devil** - Small, rapidly rotating column of air over land
44. **Wildfire** - Uncontrolled fire in wildland area
45. **Dense Smoke** - Smoke reducing visibility, usually from wildfire
46. **Drought** - Extended period of deficient precipitation
47. **Dense Fog** - Fog reducing visibility to ≤1/4 mile
48. **Debris Flow** - Fast-moving landslide of debris
49. **Volcanic Ashfall** - Volcanic ash falling from eruption
50. **Astronomical Low Tide** - Exceptionally low tide

**Note:** Some events appear in multiple categories due to their characteristics (e.g., Waterspout, Coastal Flood).

---

### 2.4 DATA STRUCTURE AND FILE ORGANIZATION

#### Three Main File Types (Annual)

The NOAA Storm Events database is organized into three separate files per year:

##### File 1: Storm Events Details
**Naming Convention:** `StormEvents_details-ftp_v1.0_dYYYY_cYYYYMMDD.csv.gz`
- **dYYYY** = data year
- **cYYYYMMDD** = file creation date

**Contains:** 51 columns with core event information (see Section 2.5)

**Record Level:** One record per storm event

##### File 2: Storm Events Locations
**Naming Convention:** `StormEvents_locations-ftp_v1.0_dYYYY_cYYYYMMDD.csv.gz`

**Contains:** Geographic location details for events

**Key Fields:**
- event_id (links to details file)
- location_index
- latitude/longitude
- location (city, town, village name)
- azimuth (16-point compass direction from reference point)
- range (distance in miles from reference point)

**Purpose:** Provides precise geographic coordinates and location descriptions, especially for path-based events (tornadoes, flooding)

##### File 3: Storm Events Fatalities
**Naming Convention:** `StormEvents_fatalities-ftp_v1.0_dYYYY_cYYYYMMDD.csv.gz`

**Contains:** Individual fatality records

**Key Fields:**
- fatality_id
- event_id (links to details file)
- fatality_type (direct/indirect)
- fatality_date
- fatality_age
- fatality_sex
- fatality_location

**Purpose:** Detailed information about each death attributed to storm events

---

### 2.5 COMPLETE VARIABLE LIST - STORM EVENTS DETAILS FILE

The **Storm Events Details** file contains **51 columns**. Below is the comprehensive list:

#### Event Identification Variables (8 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **BEGIN_YEARMONTH** | Integer | Four-digit year and spelled-out month when event began |
| **BEGIN_DAY** | Integer | Day of month when event began (1-31) |
| **BEGIN_TIME** | String | Time when event began (format: HHMM, 24-hour) |
| **END_YEARMONTH** | Integer | Year and month when event ended |
| **END_DAY** | Integer | Day of month when event ended |
| **END_TIME** | String | Time when event ended (format: HHMM, 24-hour) |
| **EPISODE_ID** | Integer | ID assigned by NWS to denote the storm episode (can contain multiple events) |
| **EVENT_ID** | Integer | ID assigned by NWS to each individual storm event |

#### Geographic Variables (9 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **STATE** | String | State name (spelled out) |
| **STATE_FIPS** | Integer | State FIPS code (2-digit) |
| **YEAR** | Integer | Four-digit year of event |
| **MONTH_NAME** | String | Name of month (spelled out) |
| **EVENT_TYPE** | String | Type of event (one of 48 types) |
| **CZ_TYPE** | String | County/Zone type: C=County, Z=Forecast Zone, M=Marine |
| **CZ_FIPS** | Integer | FIPS code for county/zone (3-digit for county, varies for zones) |
| **CZ_NAME** | String | County/Parish/Zone/Marine name |
| **WFO** | String | NWS Weather Forecast Office (3-letter identifier) |

#### Time Zone Variable (1 field)

| Variable | Type | Description |
|----------|------|-------------|
| **CZ_TIMEZONE** | String | Time zone (EST, CST, MST, PST, etc.) |

#### Event Characteristic Variables (9 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **INJURIES_DIRECT** | Integer | Number of direct injuries |
| **INJURIES_INDIRECT** | Integer | Number of indirect injuries |
| **DEATHS_DIRECT** | Integer | Number of direct deaths |
| **DEATHS_INDIRECT** | Integer | Number of indirect deaths |
| **DAMAGE_PROPERTY** | String | Property damage estimate (format: value + K/M/B) |
| **DAMAGE_CROPS** | String | Crop damage estimate (format: value + K/M/B) |
| **SOURCE** | String | Source reporting the event |
| **MAGNITUDE** | Float | Magnitude of event (wind speed, hail size, etc.) |
| **MAGNITUDE_TYPE** | String | Type of magnitude (EG, MG, MS, ES, or blank) |

#### Magnitude Type Codes:
- **EG** = Estimated Gust
- **MG** = Measured Gust
- **MS** = Measured Sustained
- **ES** = Estimated Sustained

#### Tornado-Specific Variables (3 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **TOR_F_SCALE** | String | Tornado F-scale rating (F0-F5) or EF-scale (EF0-EF5) |
| **TOR_LENGTH** | Float | Tornado path length in miles (to tenth of mile) |
| **TOR_WIDTH** | Integer | Tornado path width in yards |

**Note:** F-scale used 1950-2006; EF-scale (Enhanced Fujita) operational February 1, 2007-present

**EF Scale:** Uses 28 damage indicators (DI) with varying degrees of damage (DoD); wind estimates based on observed damage to structures and vegetation

#### Hurricane-Specific Variable (1 field)

| Variable | Type | Description |
|----------|------|-------------|
| **HURRICANE_CATEGORY** | Integer | Saffir-Simpson Hurricane Scale rating (1-5) |

**Saffir-Simpson Scale:**
- **Category 1:** 74-95 mph winds
- **Category 2:** 96-110 mph winds
- **Category 3:** 111-129 mph winds (major hurricane)
- **Category 4:** 130-156 mph winds (major hurricane)
- **Category 5:** ≥157 mph winds (major hurricane)

#### Flood-Specific Variable (1 field)

| Variable | Type | Description |
|----------|------|-------------|
| **FLOOD_CAUSE** | String | Reported or estimated cause of flood |

**Common Values:**
- Heavy Rain
- Ice Jam
- Dam/Levee Break
- Heavy Rain/Snow Melt
- Tropical System

#### Location Variables (6 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **BEGIN_RANGE** | Float | Distance in miles from reference point (hundredths) |
| **BEGIN_AZIMUTH** | String | 16-point compass bearing from reference point |
| **BEGIN_LOCATION** | String | Nearest city/town/location where event began |
| **END_RANGE** | Float | Distance in miles from ending reference point |
| **END_AZIMUTH** | String | 16-point compass bearing to ending reference point |
| **END_LOCATION** | String | Nearest city/town/location where event ended |

**16-Point Compass Bearings:** N, NNE, NE, ENE, E, ESE, SE, SSE, S, SSW, SW, WSW, W, WNW, NW, NNW

#### Coordinate Variables (4 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **BEGIN_LAT** | Float | Latitude where event began (decimal degrees) |
| **BEGIN_LON** | Float | Longitude where event began (decimal degrees, negative for W) |
| **END_LAT** | Float | Latitude where event ended (decimal degrees) |
| **END_LON** | Float | Longitude where event ended (decimal degrees) |

**Note:** Coordinates calculated from supplied range and azimuth from reference location

#### Narrative Variables (2 fields)

| Variable | Type | Description |
|----------|------|-------------|
| **EPISODE_NARRATIVE** | Text | Description of entire storm episode (can be lengthy) |
| **EVENT_NARRATIVE** | Text | Description of individual event (detailed text) |

**Purpose:** Provides contextual information, meteorological conditions, impacts, and notable details written by NWS forecasters

#### Data Source Variable (1 field)

| Variable | Type | Description |
|----------|------|-------------|
| **DATA_SOURCE** | String | Source of the storm data entry |

**Common Values:**
- NWS (National Weather Service)
- Emergency Manager
- Law Enforcement
- Public
- Trained Spotter
- Newspaper
- Broadcast Media

---

### 2.6 DAMAGE CODING SYSTEM

#### Property and Crop Damage Codes

Damage values in the database use a **multiplier code system**:

| Code | Multiplier | Example | Numeric Value |
|------|------------|---------|---------------|
| **K** | Thousands | 5.00K | $5,000 |
| **M** | Millions | 2.50M | $2,500,000 |
| **B** | Billions | 1.20B | $1,200,000,000 |

#### Damage Estimate Characteristics:

**Not Inflation-Adjusted:**
- Damage figures represent nominal dollars for the year of the event
- Users must apply Consumer Price Index (CPI) adjustment for temporal comparisons
- NOAA's Billion-Dollar Disaster dataset applies CPI adjustments; Storm Events Database does not

**Estimation Method:**
- Best guess by NWS from available sources at time of publication
- Should be considered broad estimates
- Based on reports from emergency managers, insurance, media, surveys

**Data Quality Notes:**
- Estimates may be incomplete for events still under investigation
- Large events may have multiple damage reports aggregated
- Small events may have approximate or order-of-magnitude estimates
- Crop damage may be preliminary during growing season

#### Converting to Numeric Values (R Example):

```r
# Function to convert damage string to numeric value
convert_damage <- function(damage_str) {
  if (is.na(damage_str) || damage_str == "") return(0)

  # Extract numeric value and multiplier
  value <- as.numeric(str_extract(damage_str, "[0-9\\.]+"))
  multiplier <- str_extract(damage_str, "[KMB]")

  # Apply multiplier
  if (is.na(multiplier)) {
    return(value)
  } else if (multiplier == "K") {
    return(value * 1000)
  } else if (multiplier == "M") {
    return(value * 1000000)
  } else if (multiplier == "B") {
    return(value * 1000000000)
  }
}

# Apply to dataframe
storm_data <- storm_data %>%
  mutate(
    damage_property_num = sapply(DAMAGE_PROPERTY, convert_damage),
    damage_crops_num = sapply(DAMAGE_CROPS, convert_damage),
    total_damage = damage_property_num + damage_crops_num
  )
```

---

### 2.7 DIRECT VS. INDIRECT DEATHS AND INJURIES

#### Direct Deaths/Injuries

**Definition:** Deaths or injuries directly caused by the weather event itself.

**Examples:**
- Person struck by lightning
- Individual hit by tornado debris
- Drowning in flash flood waters
- Death from tree falling during high winds
- Injury from hail impact

#### Indirect Deaths/Injuries

**Definition:** Deaths or injuries indirectly caused by the weather event, occurring before, during, or after the event.

**Examples:**
- Heart attack while shoveling snow after blizzard
- Traffic accident on icy roads following ice storm
- Electrocution from downed power lines after storm
- Carbon monoxide poisoning from generator use during power outage
- Chainsaw injury while clearing fallen trees

#### Recording in Database:

Each event has four separate fields:
- `INJURIES_DIRECT`
- `INJURIES_INDIRECT`
- `DEATHS_DIRECT`
- `DEATHS_INDIRECT`

**Analysis Consideration:** Users should decide whether to include indirect impacts based on their research question. Direct impacts better reflect event intensity; total impacts (direct + indirect) better reflect overall societal burden.

---

### 2.8 COUNTY-LEVEL AGGREGATION METHODS

#### Challenges:

1. **CZ_TYPE Complications:**
   - Events reported by County (C), Forecast Zone (Z), or Marine zone (M)
   - Zone-based events require mapping to counties
   - Some zones span multiple counties

2. **Multi-County Events:**
   - Large events (e.g., winter storms, droughts) may have one record spanning many counties
   - Requires careful aggregation to avoid double-counting

3. **Temporal Aggregation:**
   - Define aggregation period (annual, seasonal, multi-year)
   - Account for events spanning multiple months/years

#### Recommended County-Level Metrics:

##### Event Counts:
- Total events by type
- Total severe weather events (convective only)
- Most common event type
- Diversity of event types (richness)

##### Impact Metrics:
- Total direct deaths
- Total indirect deaths
- Total direct injuries
- Total indirect injuries
- Total property damage (inflation-adjusted)
- Total crop damage (inflation-adjusted)
- Combined economic damage

##### Normalized Metrics (per capita or per area):
- Events per 1000 population
- Deaths per 100,000 population
- Injuries per 100,000 population
- Damage per capita
- Damage per square mile

##### Temporal Metrics:
- Annual event frequency
- Seasonal patterns (by month)
- Trend over time (increasing/decreasing)
- Days with events per year

##### Severity Metrics:
- Average damage per event
- Percentage of events with fatalities
- Percentage of events with injuries
- Maximum tornado rating in county
- Maximum hurricane category

---

### 2.9 NOAA STORM EVENTS DATA ACCESS METHODS

#### Method 1: Interactive Database Search - **EASIEST FOR SMALL QUERIES**

**URL:** https://www.ncdc.noaa.gov/stormevents/

**Features:**
- User-friendly web interface
- Query builder with multiple filters
- Date range selection
- State/County selection
- Event type filtering
- Download results as CSV

**Best For:**
- Individual county queries
- Short time periods
- Specific event types
- Quick exploratory analysis

**Limitations:**
- Query size limits
- Slower for large datasets
- Manual download process

#### Method 2: Bulk FTP/HTTP Download - **BEST FOR LARGE DATASETS**

**FTP URL:** ftp://ftp.ncdc.noaa.gov/pub/data/swdi/stormevents/csvfiles/

**HTTP URL:** https://www1.ncdc.noaa.gov/pub/data/swdi/stormevents/csvfiles/

**File Structure:**
- Annual files (1950-2025)
- Three file types per year:
  - `StormEvents_details-ftp_v1.0_dYYYY_cYYYYMMDD.csv.gz`
  - `StormEvents_locations-ftp_v1.0_dYYYY_cYYYYMMDD.csv.gz`
  - `StormEvents_fatalities-ftp_v1.0_dYYYY_cYYYYMMDD.csv.gz`

**Documentation Available:**
- Storm-Data-Bulk-csv-Format.pdf (field descriptions)

**Download Example (Bash):**
```bash
# Download all details files for 2010-2020
for year in {2010..2020}; do
  wget -r -np -nd -A "*details*d${year}*.csv.gz" \
    https://www1.ncdc.noaa.gov/pub/data/swdi/stormevents/csvfiles/
done
```

**Best For:**
- Multi-year analyses
- All U.S. counties
- Complete dataset
- Reproducible research

#### Method 3: noaastormevents R Package - **BEST FOR R USERS**

**Installation:**
```r
install.packages("noaastormevents")
```

**Key Functions:**

##### find_events()

**Purpose:** Creates dataframe with event listings by county based on user-specified parameters.

**Example 1 - Find Events by Date Range:**
```r
library(noaastormevents)

# Get all events for specific date range
floyd_events <- find_events(
  date_range = c("1999-09-14", "1999-09-18")
)
```

**Example 2 - Find Events by County FIPS:**
```r
# Get events for specific counties
county_events <- find_events(
  date_range = c("2020-01-01", "2020-12-31"),
  county_fips = c("06037", "06073")  # LA and San Diego counties
)
```

**Example 3 - Find Events Near Storm Track:**
```r
# Get events within 300 km of Hurricane Floyd path
floyd_events <- find_events(
  storm = "Floyd-1999",
  dist_limit = 300  # kilometers
)
```

**Example 4 - Filter by Event Type:**
```r
# Get only tornado events
tornado_events <- find_events(
  date_range = c("2010-01-01", "2020-12-31"),
  event_types = c("Tornado", "Funnel Cloud")
)
```

**Output Fields:**
- `fips` - 5-digit county FIPS code
- `begin_date` - Event begin date
- `end_date` - Event end date
- `state` - State name
- `cz_type` - County/Zone type (C/Z/M)
- `cz_name` - County/Zone name
- `event_type` - Type of storm event
- `injuries_direct` - Direct injuries
- `injuries_indirect` - Indirect injuries
- `deaths_direct` - Direct deaths
- `deaths_indirect` - Indirect deaths
- `damage_property` - Property damage
- `damage_crops` - Crop damage

**Zone to County Matching:**
- Package uses regular expressions to match forecast zones to county FIPS codes
- When `cz_type == "Z"`, algorithm attempts to assign correct county FIPS
- May not be perfect for all zones

##### Mapping Functions:

```r
# Map events
map_events(floyd_events)

# Map storm tracks with distance buffer
map_distance(storm = "Floyd-1999", dist_limit = 300)
```

**Best For:**
- R-based analyses
- County-level aggregation
- Storm track analyses
- Integration with other R spatial packages

#### Method 4: NOAA API (If Available)

**Note:** NOAA NCEI provides various APIs, but Storm Events Database access may be limited. Check current API documentation:

**URL:** https://www.ncdc.noaa.gov/cdo-web/webservices/v2

**Requires:** API token (free registration)

---

### 2.10 COMPLETE COUNTY AGGREGATION WORKFLOW (R)

```r
library(noaastormevents)
library(dplyr)
library(tidyr)
library(stringr)
library(tidycensus)  # For population data

# Function to convert damage strings to numeric
convert_damage <- function(damage_str) {
  if (is.na(damage_str) || damage_str == "" || damage_str == "0") return(0)

  value <- as.numeric(str_extract(damage_str, "[0-9\\.]+"))
  multiplier <- str_extract(damage_str, "[KMB]")

  if (is.na(multiplier)) {
    return(value)
  } else if (multiplier == "K") {
    return(value * 1000)
  } else if (multiplier == "M") {
    return(value * 1000000)
  } else if (multiplier == "B") {
    return(value * 1000000000)
  } else {
    return(value)
  }
}

# Function to aggregate storm events by county
aggregate_county_storms <- function(start_year, end_year, state_fips = NULL) {

  # Get all events for time period
  events <- find_events(
    date_range = c(paste0(start_year, "-01-01"),
                   paste0(end_year, "-12-31"))
  )

  # Filter by state if specified
  if (!is.null(state_fips)) {
    events <- events %>%
      filter(substr(fips, 1, 2) == state_fips)
  }

  # Convert damage to numeric
  events <- events %>%
    mutate(
      damage_property_num = sapply(damage_property, convert_damage),
      damage_crops_num = sapply(damage_crops, convert_damage),
      total_damage = damage_property_num + damage_crops_num,
      total_deaths = deaths_direct + deaths_indirect,
      total_injuries = injuries_direct + injuries_indirect
    )

  # Aggregate by county
  county_summary <- events %>%
    group_by(fips, state) %>%
    summarize(
      # Event counts
      total_events = n(),
      unique_event_types = n_distinct(event_type),

      # By event type
      tornado_events = sum(event_type == "Tornado"),
      flood_events = sum(event_type %in% c("Flash Flood", "Flood")),
      wind_events = sum(event_type %in% c("Thunderstorm Wind", "High Wind")),
      winter_events = sum(event_type %in% c("Winter Storm", "Winter Weather",
                                             "Heavy Snow", "Ice Storm")),
      heat_events = sum(event_type %in% c("Heat", "Excessive Heat")),

      # Impacts
      total_deaths = sum(total_deaths, na.rm = TRUE),
      total_injuries = sum(total_injuries, na.rm = TRUE),
      total_property_damage = sum(damage_property_num, na.rm = TRUE),
      total_crop_damage = sum(damage_crops_num, na.rm = TRUE),
      total_economic_damage = sum(total_damage, na.rm = TRUE),

      # Event characteristics
      events_with_deaths = sum(total_deaths > 0),
      events_with_injuries = sum(total_injuries > 0),
      avg_damage_per_event = mean(total_damage, na.rm = TRUE),
      max_damage_event = max(total_damage, na.rm = TRUE),

      # Tornado specifics
      max_tornado_rating = max(as.numeric(str_extract(tor_f_scale, "[0-5]")),
                               na.rm = TRUE),

      # Temporal
      years_covered = end_year - start_year + 1,

      .groups = "drop"
    ) %>%
    mutate(
      # Replace -Inf with NA
      max_tornado_rating = ifelse(is.infinite(max_tornado_rating),
                                  NA, max_tornado_rating),
      max_damage_event = ifelse(is.infinite(max_damage_event),
                                0, max_damage_event),

      # Annual averages
      events_per_year = total_events / years_covered,
      deaths_per_year = total_deaths / years_covered,
      damage_per_year = total_economic_damage / years_covered
    )

  # Get county population for normalization (using 2020 census)
  county_pop <- get_acs(
    geography = "county",
    variables = "B01003_001",  # Total population
    year = 2020,
    geometry = FALSE
  ) %>%
    select(GEOID, population = estimate)

  # Join population and calculate per capita metrics
  county_summary <- county_summary %>%
    left_join(county_pop, by = c("fips" = "GEOID")) %>%
    mutate(
      events_per_100k = (total_events / population) * 100000,
      deaths_per_100k = (total_deaths / population) * 100000,
      injuries_per_100k = (total_injuries / population) * 100000,
      damage_per_capita = total_economic_damage / population
    )

  return(county_summary)
}

# Example usage - Get storm events for Maryland 2010-2020
md_storms <- aggregate_county_storms(
  start_year = 2010,
  end_year = 2020,
  state_fips = "24"  # Maryland
)

# Export results
write.csv(md_storms, "maryland_storm_events_2010_2020.csv", row.names = FALSE)

# Summary statistics
summary_stats <- md_storms %>%
  summarize(
    total_counties = n(),
    total_events = sum(total_events),
    total_deaths = sum(total_deaths),
    total_damage = sum(total_economic_damage),
    avg_events_per_county = mean(total_events),
    counties_with_tornadoes = sum(tornado_events > 0),
    max_county_damage = max(total_economic_damage)
  )

print(summary_stats)
```

---

### 2.11 DATA QUALITY CONSIDERATIONS

#### Reporting Biases:

**Population Bias:**
- Events in densely populated areas more likely to be reported
- Rural areas may have under-reporting
- Improved with technology (Doppler radar, social media)

**Temporal Bias:**
- Reporting became more comprehensive after 1996
- Pre-1996 data only includes tornado, wind, hail
- Technology improvements (Doppler radar 1990s) increased detection

**Event Definition Changes:**
- Criteria for reporting events have evolved
- Warning thresholds have changed over time
- Enhanced Fujita scale implemented 2007 (different from F-scale)

#### Damage Estimation Challenges:

**Not Inflation-Adjusted:**
- Requires user to apply CPI adjustment
- Makes temporal comparisons difficult without adjustment

**Estimation Uncertainty:**
- Damage estimates are broad approximations
- Based on available information at time of publication
- May not capture full economic impact
- Indirect economic impacts not included

**Incomplete Coverage:**
- Small events may go unreported
- Damage to uninsured property may be underestimated
- Crop damage may be preliminary

#### Geographic Complications:

**Zone vs. County Reporting:**
- Large-scale events often reported by forecast zone
- Zones do not perfectly align with county boundaries
- Requires spatial analysis or lookup tables for county attribution

**Marine and Coastal Events:**
- Marine events (CZ_TYPE = "M") don't have county FIPS
- Coastal events may affect multiple jurisdictions
- Requires coastal county assignment

---

### 2.12 INFLATION ADJUSTMENT FOR DAMAGE VALUES

Since damage estimates in the Storm Events Database are in nominal dollars, temporal analyses require inflation adjustment using the Consumer Price Index (CPI).

#### CPI Adjustment Method:

**Formula:**
```
Adjusted_Value = Nominal_Value × (CPI_current / CPI_event_year)
```

#### R Implementation:

```r
library(dplyr)
library(blscrapeR)  # For CPI data from BLS

# Get annual CPI data (using 2024 as base year)
cpi_data <- inflation_adjust(2024)

# Function to adjust damage for inflation
adjust_damage_inflation <- function(damage, year, base_year = 2024) {
  # Get CPI for event year and base year
  cpi_event <- cpi_data %>% filter(year == year) %>% pull(avg_cpi)
  cpi_base <- cpi_data %>% filter(year == base_year) %>% pull(avg_cpi)

  # Calculate adjustment factor
  adjustment_factor <- cpi_base / cpi_event

  # Return adjusted damage
  return(damage * adjustment_factor)
}

# Apply to storm events dataframe
storm_data <- storm_data %>%
  mutate(
    damage_property_adjusted = mapply(
      adjust_damage_inflation,
      damage_property_num,
      year
    ),
    damage_crops_adjusted = mapply(
      adjust_damage_inflation,
      damage_crops_num,
      year
    ),
    total_damage_adjusted = damage_property_adjusted + damage_crops_adjusted
  )
```

**Note:** NOAA's Billion-Dollar Disaster dataset applies CPI adjustment, but the raw Storm Events Database does not.

---

### 2.13 COMMON USE CASES AND ANALYSIS EXAMPLES

#### Use Case 1: County Vulnerability Assessment

Identify counties most vulnerable to storm events based on:
- Historical event frequency
- Deaths and injuries per capita
- Economic damage per capita
- Diversity of event types
- Temporal trends

#### Use Case 2: Urban Planning and Zoning

Use NLCD developed land + storm events to:
- Assess risk to developed areas
- Plan storm infrastructure (stormwater, shelters)
- Identify high-risk development zones
- Model future risk under urban expansion

#### Use Case 3: Climate Change Impact Studies

Temporal analysis of:
- Changes in event frequency over time
- Shifts in event types (e.g., more heat, less cold)
- Changes in event intensity (damage, injuries)
- Spatial shifts in event patterns

#### Use Case 4: Agricultural Risk Assessment

Combine NLCD agricultural land + crop damage:
- Identify counties with high agricultural storm risk
- Assess tornado/hail damage to crops
- Evaluate flood risk to farmland
- Inform crop insurance pricing

#### Use Case 5: Wildfire-Urban Interface

Combine NLCD developed/forest land + wildfire events:
- Map wildfire-urban interface zones
- Assess risk to homes near forests
- Plan evacuation routes
- Inform building codes and defensible space

---

## PART 3: INTEGRATION OF NLCD AND STORM EVENTS DATA

### 3.1 Conceptual Integration

**Common Geographic Unit:** County (5-digit FIPS code)

**Temporal Alignment:**
- NLCD: Annual data (1985-2024)
- Storm Events: Daily event records (1950-2025)

**Integration Opportunities:**

1. **Land Cover as Exposure Variable:**
   - Developed land (NLCD 21-24) as exposure to storm damage
   - Forest cover (NLCD 41-43) as wildfire fuel
   - Agricultural land (NLCD 81-82) as crop damage vulnerability
   - Wetlands (NLCD 90, 95) as flood mitigation capacity

2. **Storm Events as Disturbance:**
   - Wildfires detected in NLCD Spectral Change Day of Year
   - Floods causing land cover change
   - Tornadoes creating forest damage
   - Hurricanes altering coastal land cover

3. **Temporal Analysis:**
   - Correlate urban expansion (NLCD change) with storm damage trends
   - Assess whether developed land increases storm vulnerability
   - Evaluate wetland loss and flood event changes

### 3.2 Integration Workflow (R)

```r
library(dplyr)
library(tidyr)
library(sf)
library(terra)
library(noaastormevents)
library(exactextractr)
library(tigris)

# 1. Get county NLCD statistics (from Section 1.8)
nlcd_stats <- get_state_nlcd_stats("MD", year = 2021)

# 2. Get storm events for same counties (from Section 2.10)
storm_stats <- aggregate_county_storms(
  start_year = 2010,
  end_year = 2020,
  state_fips = "24"
)

# 3. Join datasets
integrated_data <- nlcd_stats$summary %>%
  left_join(storm_stats, by = c("GEOID" = "fips"))

# 4. Calculate composite metrics
integrated_data <- integrated_data %>%
  mutate(
    # Risk metrics
    developed_area_risk = total_developed_pct * events_per_100k,
    flood_wetland_ratio = flood_events / total_wetlands_pct,
    ag_risk = total_agriculture_pct * (total_crop_damage / 1000000),

    # Land cover vulnerability
    impervious_flood_risk = total_developed_pct * flood_events,
    forest_fire_risk = total_forest_pct * sum(event_type == "Wildfire")
  )

# 5. Export integrated dataset
write.csv(integrated_data, "maryland_integrated_nlcd_storms.csv",
          row.names = FALSE)

# 6. Spatial analysis (optional)
counties_sf <- st_as_sf(tigris::counties(state = "24", year = 2022))

integrated_sf <- counties_sf %>%
  left_join(integrated_data, by = "GEOID")

# Map high-risk counties
library(ggplot2)
ggplot(integrated_sf) +
  geom_sf(aes(fill = developed_area_risk)) +
  scale_fill_viridis_c() +
  labs(title = "Developed Area Storm Risk by County",
       fill = "Risk Index") +
  theme_minimal()
```

---

## PART 4: ADDITIONAL RESOURCES AND REFERENCES

### 4.1 Official Documentation

**NLCD:**
- MRLC Consortium: https://www.mrlc.gov/
- USGS NLCD Page: https://www.usgs.gov/centers/eros/science/national-land-cover-database
- EVA Tool: https://www.mrlc.gov/eva/
- Annual NLCD Documentation: https://pubs.usgs.gov/publication/fs20253001

**NOAA Storm Events:**
- Storm Events Database: https://www.ncdc.noaa.gov/stormevents/
- Bulk FTP: https://www1.ncdc.noaa.gov/pub/data/swdi/stormevents/csvfiles/
- Storm Data Format PDF: https://www.ncei.noaa.gov/pub/data/swdi/stormevents/csvfiles/Storm-Data-Bulk-csv-Format.pdf
- NWS Directive 10-1605: https://www.weather.gov/media/directives/010_pdfs/pd01016curr.pdf

### 4.2 Google Earth Engine Resources

**NLCD in GEE:**
- Legacy NLCD 2019: `'USGS/NLCD_RELEASES/2019_REL/NLCD'`
- Legacy NLCD 2021: `'USGS/NLCD_RELEASES/2021_REL/NLCD'`
- GEE Data Catalog: https://developers.google.com/earth-engine/datasets/catalog/USGS_NLCD_RELEASES_2021_REL_NLCD

**GEE Tutorials:**
- Grouped Reductions: https://developers.google.com/earth-engine/guides/reducers_grouping
- Zonal Statistics: https://google-earth-engine.com/Vectors-and-Tables/Zonal-Statistics/

### 4.3 R Package Resources

**NLCD Packages:**
- FedData: https://cran.r-project.org/web/packages/FedData/
- terra: https://cran.r-project.org/web/packages/terra/
- exactextractr: https://cran.r-project.org/web/packages/exactextractr/

**Storm Events Packages:**
- noaastormevents: https://cran.r-project.org/web/packages/noaastormevents/
- GitHub: https://github.com/geanders/noaastormevents
- Vignette: https://cran.r-project.org/web/packages/noaastormevents/vignettes/noaastormevents.html

**Spatial Packages:**
- sf: https://cran.r-project.org/web/packages/sf/
- tigris: https://cran.r-project.org/web/packages/tigris/

### 4.4 Key Scientific References

**NLCD:**
- Jin, S., et al. (2019). Overall methodology design for the United States National Land Cover Database 2016 products. *Remote Sensing*, 11(24), 2971.
- Homer, C., et al. (2020). Conterminous United States land cover change patterns 2001–2016 from the 2016 National Land Cover Database. *ISPRS Journal of Photogrammetry and Remote Sensing*, 162, 184-199.

**Storm Events:**
- Smith, A. B., & Katz, R. W. (2013). US billion-dollar weather and climate disasters: data sources, trends, accuracy and biases. *Natural Hazards*, 67(2), 387-410.
- NOAA NCEI. (2024). Storm Events Database. National Centers for Environmental Information.

**Integration Studies:**
- Ashley, W. S., & Strader, S. M. (2016). Recipe for disaster: How the dynamic ingredients of risk and exposure are changing the tornado disaster landscape. *Bulletin of the American Meteorological Society*, 97(5), 767-786.

### 4.5 Related Datasets

**Complementary Spatial Data:**
- US Census TIGER/Line (county boundaries)
- USGS National Hydrography Dataset (water features)
- USDA CropScape (crop-specific land cover)
- MODIS Land Cover (global, 500m resolution)

**Complementary Hazard Data:**
- NOAA Billion-Dollar Disasters
- FEMA National Risk Index
- SPC Severe Weather Database
- USGS Earthquake Catalog

---

## PART 5: PRODUCTION-READY IMPLEMENTATION CHECKLIST

### 5.1 NLCD Implementation Checklist

- [ ] Determine required years (single year vs. time series)
- [ ] Choose access method (EVA, bulk download, GEE, R packages)
- [ ] Define geographic extent (state, region, or national)
- [ ] Select products needed (land cover, impervious, canopy, change)
- [ ] Set up processing environment (R, Python, GEE, or ArcGIS)
- [ ] Obtain county boundaries (tigris, Census TIGER/Line)
- [ ] Implement zonal statistics workflow
- [ ] Validate sample counties against EVA tool
- [ ] Calculate derived metrics (developed %, forest %, agriculture %)
- [ ] Export results to standardized format (CSV with FIPS code)
- [ ] Document methodology and data sources
- [ ] Archive raw and processed data with metadata

### 5.2 NOAA Storm Events Implementation Checklist

- [ ] Determine temporal extent (start year to end year)
- [ ] Choose access method (web query, FTP bulk, noaastormevents package)
- [ ] Download required files (details, locations, fatalities if needed)
- [ ] Implement damage code conversion (K/M/B to numeric)
- [ ] Handle zone-to-county mapping for CZ_TYPE = "Z"
- [ ] Filter by event types if needed
- [ ] Aggregate to county level with appropriate metrics
- [ ] Calculate per capita and normalized metrics
- [ ] Obtain population data for normalization (tidycensus)
- [ ] Apply inflation adjustment to damage values
- [ ] Handle missing data and edge cases
- [ ] Validate against NOAA Storm Events Database web query
- [ ] Export results with documentation
- [ ] Archive processed dataset with data dictionary

### 5.3 Integration Implementation Checklist

- [ ] Ensure temporal alignment (match NLCD year to storm period)
- [ ] Standardize geographic unit (5-digit county FIPS)
- [ ] Join datasets on FIPS code
- [ ] Handle counties with missing data in either dataset
- [ ] Calculate exposure metrics (developed land × storm frequency)
- [ ] Calculate vulnerability indices (weighted combinations)
- [ ] Create spatial objects for mapping (sf or terra)
- [ ] Generate summary statistics and data quality checks
- [ ] Export integrated dataset with complete documentation
- [ ] Create reproducible workflow (R Markdown, Jupyter Notebook)

---

## DOCUMENT METADATA

**Document Version:** 1.0

**Date Created:** 2025-11-11

**Author:** Claude (Anthropic AI)

**Purpose:** Comprehensive documentation of NLCD and NOAA Storm Events data sources for county-level analysis

**Temporal Coverage of Documentation:**
- NLCD: 1985-2024 (Annual Collection 1.1)
- Storm Events: 1950-April 2025

**Geographic Coverage:** United States (Conterminous U.S., Alaska, Hawaii, territories)

**Last Verified:** November 2025

**Sources:**
- Multi-Resolution Land Characteristics (MRLC) Consortium
- U.S. Geological Survey (USGS)
- NOAA National Centers for Environmental Information (NCEI)
- Multiple peer-reviewed scientific publications
- Official R package documentation

**Note:** Data sources are continuously updated. Check official websites for latest releases and documentation updates.

---

**END OF COMPREHENSIVE DOCUMENTATION**
