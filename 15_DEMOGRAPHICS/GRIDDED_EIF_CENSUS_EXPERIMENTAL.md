# Census Bureau Gridded Environmental Impacts Frame (Gridded EIF)
## Experimental High-Resolution Demographics + Environmental Hazards

**Status:** 🧪 EXPERIMENTAL DATA PRODUCT (New 2025)
**Last Updated:** November 13, 2025
**Geographic Resolution:** 0.01-degree grid (~1.2 sq km)
**Temporal Coverage:** 1999-2024
**Update Frequency:** Annual
**Access:** https://www.census.gov/data/experimental-data-products/gridded-eif.html

---

## 🆕 What's New

The **Gridded Environmental Impacts Frame (Gridded EIF)** is a groundbreaking experimental dataset released by the US Census Bureau in 2025 that combines:

1. **Detailed demographics** (age, sex, race, ethnicity, income) from confidential Census administrative records
2. **Environmental hazard exposure** (air pollution: CO, Ozone) on the same grid
3. **High spatial resolution** (0.01-degree grid ≈ 1.2 square kilometers)
4. **Privacy protection** (aggregated to grid cells, not individual-level)

---

## 📊 Executive Summary

### Why This Dataset is Important

**FIRST-OF-ITS-KIND:** This is the only dataset that links Census Bureau's comprehensive demographic data with environmental hazard exposures at fine spatial resolution nationwide.

**Key Advantages:**
- **Eliminates data linkage challenges:** Demographics and environmental exposures already co-located on same grid
- **High spatial resolution:** 0.01-degree grid captures intra-county variation
- **Privacy-protected:** Derived from confidential EIF microdata but publicly accessible
- **Consistent methodology:** Same grid structure and variables across all years (1999-2024)
- **Open access:** No restricted data use agreement required

**Use Cases:**
- Environmental justice research (income/race disparities in pollution exposure)
- Fine-scale health-environment studies
- County-level aggregation with demographic stratification
- Validation of exposure assessment models

---

## 📋 Variables Available

### Demographics (Grid Cell Level)

#### Race-Age-Sex Dataset
| Variable Category | Details | Years |
|-------------------|---------|-------|
| **Total Population** | Total population count in grid cell | 1999-2024 |
| **Age Groups** | Population by age (specific groups to be documented) | 1999-2024 |
| **Sex** | Male, Female counts | 1999-2024 |
| **Race** | White, Black, Asian, American Indian/Alaska Native, Native Hawaiian/Pacific Islander, Two or More Races | 1999-2024 |
| **Hispanic/Latino Origin** | Hispanic, Non-Hispanic | 1999-2024 |

#### Race-Income Dataset
| Variable Category | Details | Years |
|-------------------|---------|-------|
| **Household Income Decile** | Population by race/ethnicity and household income decile (10 groups) | 1999-2024 |
| **Race/Ethnicity** | Same categories as above | 1999-2024 |

### Environmental Hazards (Grid Cell Level)

| Hazard | Pollutant | Units | Source | Years |
|--------|-----------|-------|--------|-------|
| **Air Pollution** | Carbon Monoxide (CO) | ppb | Kim et al. (2020), CACES | 1999-2022 |
| **Air Pollution** | Ozone (O₃) | ppb | Kim et al. (2020), CACES | 1999-2022 |

**Note:** Air pollution data from Center for Air, Climate, and Energy Solutions (CACES) harmonized estimates.

---

## 🗺️ Geographic Structure

### Grid Specification
- **Grid Type:** Fixed 0.01-degree latitude/longitude grid
- **Approximate Size:** 1.2 square kilometers in North America
- **Coverage:** Contiguous United States (48 states + DC)
- **Grid Points:** Indexed by centroid (latitude/longitude)
- **Coordinate System:** WGS84 (EPSG:4326)

### Aggregation to Counties

Since the data is gridded at fine resolution, it can be aggregated to US counties:

```r
library(sf)
library(dplyr)
library(arrow)

# Read Gridded EIF (example for 2023)
gridded_eif <- read_parquet("gridded_eif_race_age_sex_2023.parquet")

# Load county boundaries
counties <- st_read("tl_2023_us_county.shp") %>%
  st_transform(4326)  # WGS84

# Convert grid centroids to spatial points
grid_sf <- st_as_sf(gridded_eif,
                    coords = c("longitude", "latitude"),
                    crs = 4326)

# Spatial join: Assign each grid cell to a county
grid_with_county <- st_join(grid_sf, counties)

# Aggregate to county level
county_aggregated <- grid_with_county %>%
  st_drop_geometry() %>%
  group_by(GEOID, NAME) %>%
  summarize(
    total_population = sum(total_population, na.rm = TRUE),
    mean_CO_ppb = weighted.mean(CO_ppb, total_population, na.rm = TRUE),
    mean_O3_ppb = weighted.mean(O3_ppb, total_population, na.rm = TRUE),
    # Demographic breakdowns
    population_white = sum(population_white, na.rm = TRUE),
    population_black = sum(population_black, na.rm = TRUE),
    # Income deciles...
    .groups = "drop"
  )
```

---

## 💾 Data Access and Format

### File Format

**Parquet files** are used due to large dataset size (efficient compressed columnar format).

### File Structure

For each year, two datasets are available:

1. **Race-Age-Sex File:** `gridded_eif_race_age_sex_YYYY.parquet`
2. **Race-Income File:** `gridded_eif_race_income_YYYY.parquet`

### Years Available

| Dataset Type | Years | Notes |
|--------------|-------|-------|
| **Demographics (Race-Age-Sex)** | 1999-2024 | 2024 is "real-time" (updated frequently) |
| **Demographics (Race-Income)** | 1999-2024 | 2024 is "real-time" |
| **Air Pollution (CO, O₃)** | 1999-2022 | Harmonized pollution estimates |

### Download Location

**Official Source:** https://www.census.gov/data/experimental-data-products/gridded-eif.html

### File Size

**Warning:** Each annual file is large (multi-gigabyte) due to fine spatial resolution covering entire US.

---

## 🔬 Data Sources and Methodology

### Underlying Data

The public Gridded EIF is derived from the confidential **Environmental Impacts Frame (EIF)** microdata, which combines:

1. **Census Bureau administrative records** (Social Security Administration, IRS, Medicare/Medicaid)
2. **Census Bureau survey data** (Decennial Census, ACS)
3. **High-resolution environmental data** from academic/federal sources

### Privacy Protection Method

**Differential privacy** and aggregation techniques are applied to grid cells to prevent re-identification while preserving statistical accuracy.

### Air Pollution Data Source

**Kim et al. (2020)** harmonized air pollution estimates:
- Combines EPA monitoring data, satellite observations, land use, meteorology
- Machine learning prediction models
- Validated against ground monitors
- Published by Center for Air, Climate, and Energy Solutions (CACES)

**Reference:** Kim, S.Y., Bechle, M., Hankey, S., Sheppard, L., Szpiro, A.A., & Marshall, J.D. (2020). Concentrations of criteria pollutants in the contiguous U.S., 1979 – 2015: Role of prediction model parsimony in integrated empirical geographic regression. *PLOS ONE*, 15(2), e0228535.

---

## 📊 R Code Examples

### Example 1: Load and Explore Gridded EIF

```r
library(arrow)
library(dplyr)
library(ggplot2)

# Read 2023 race-age-sex data
eif_2023 <- read_parquet("gridded_eif_race_age_sex_2023.parquet")

# Examine structure
glimpse(eif_2023)

# Summary statistics
summary(eif_2023)

# Check grid coverage
nrow(eif_2023)  # Number of grid cells

# Visualize total population distribution
ggplot(eif_2023, aes(x = longitude, y = latitude, fill = log10(total_population))) +
  geom_tile() +
  scale_fill_viridis_c() +
  coord_fixed(1.3) +
  labs(title = "Gridded EIF: Log10 Population Density (2023)",
       fill = "Log10(Pop)") +
  theme_minimal()
```

### Example 2: Calculate County-Level Demographics + Air Pollution

```r
library(sf)
library(arrow)
library(dplyr)

# 1. Load Gridded EIF (demographics + pollution)
eif <- read_parquet("gridded_eif_race_age_sex_2020.parquet")

# 2. Load county boundaries (TIGER/Line 2020)
counties <- st_read("https://www2.census.gov/geo/tiger/TIGER2020/COUNTY/tl_2020_us_county.zip") %>%
  st_transform(4326) %>%
  filter(!STATEFP %in% c("02", "15", "60", "66", "69", "72", "78"))  # Contiguous US

# 3. Convert grid points to sf object
eif_sf <- st_as_sf(eif, coords = c("longitude", "latitude"), crs = 4326)

# 4. Spatial join: assign grid cells to counties
eif_counties <- st_join(eif_sf, counties %>% select(GEOID, NAME))

# 5. Aggregate to county level with population-weighted means
county_summary <- eif_counties %>%
  st_drop_geometry() %>%
  group_by(GEOID, NAME) %>%
  summarize(
    # Total population
    total_pop = sum(total_population, na.rm = TRUE),

    # Demographics
    pct_white = sum(pop_white, na.rm = TRUE) / total_pop * 100,
    pct_black = sum(pop_black, na.rm = TRUE) / total_pop * 100,
    pct_hispanic = sum(pop_hispanic, na.rm = TRUE) / total_pop * 100,

    # Air pollution (population-weighted means)
    CO_ppb = weighted.mean(CO_ppb, total_population, na.rm = TRUE),
    O3_ppb = weighted.mean(O3_ppb, total_population, na.rm = TRUE),

    .groups = "drop"
  )

# 6. Save county-level dataset
write.csv(county_summary, "county_demographics_pollution_2020.csv", row.names = FALSE)
```

### Example 3: Environmental Justice Analysis

```r
# Analyze air pollution by income decile

eif_income <- read_parquet("gridded_eif_race_income_2020.parquet")

# Calculate mean pollution exposure by income decile
pollution_by_income <- eif_income %>%
  group_by(income_decile) %>%
  summarize(
    population = sum(total_population, na.rm = TRUE),
    mean_CO = weighted.mean(CO_ppb, total_population, na.rm = TRUE),
    mean_O3 = weighted.mean(O3_ppb, total_population, na.rm = TRUE),
    .groups = "drop"
  )

# Visualize
ggplot(pollution_by_income, aes(x = income_decile, y = mean_CO)) +
  geom_col(fill = "steelblue") +
  labs(title = "Carbon Monoxide Exposure by Income Decile (2020)",
       x = "Income Decile (1=lowest, 10=highest)",
       y = "Mean CO (ppb)") +
  theme_minimal()
```

---

## 🐍 Python Code Examples

### Example 1: Load and Process Gridded EIF

```python
import pandas as pd
import geopandas as gpd
from pyarrow import parquet

# Read Parquet file
eif = pd.read_parquet("gridded_eif_race_age_sex_2023.parquet")

# Examine data
print(eif.head())
print(eif.dtypes)
print(eif.describe())

# Convert to GeoDataFrame
eif_gdf = gpd.GeoDataFrame(
    eif,
    geometry=gpd.points_from_xy(eif.longitude, eif.latitude),
    crs="EPSG:4326"
)
```

### Example 2: Aggregate to Counties

```python
import geopandas as gpd
import pandas as pd

# Load county boundaries
counties = gpd.read_file("https://www2.census.gov/geo/tiger/TIGER2020/COUNTY/tl_2020_us_county.zip")
counties = counties.to_crs("EPSG:4326")
counties = counties[~counties.STATEFP.isin(["02", "15", "60", "66", "69", "72", "78"])]

# Load gridded EIF
eif = pd.read_parquet("gridded_eif_race_age_sex_2020.parquet")
eif_gdf = gpd.GeoDataFrame(
    eif,
    geometry=gpd.points_from_xy(eif.longitude, eif.latitude),
    crs="EPSG:4326"
)

# Spatial join
eif_with_county = gpd.sjoin(eif_gdf, counties[["GEOID", "NAME", "geometry"]],
                             how="left", predicate="within")

# Aggregate to county level
county_data = eif_with_county.groupby("GEOID").apply(
    lambda x: pd.Series({
        "total_pop": x["total_population"].sum(),
        "CO_ppb": (x["CO_ppb"] * x["total_population"]).sum() / x["total_population"].sum(),
        "O3_ppb": (x["O3_ppb"] * x["total_population"]).sum() / x["total_population"].sum(),
        "pct_white": x["pop_white"].sum() / x["total_population"].sum() * 100,
        "pct_black": x["pop_black"].sum() / x["total_population"].sum() * 100
    })
).reset_index()

# Save
county_data.to_csv("county_demographics_pollution_2020.csv", index=False)
```

---

## ⚠️ Data Quality and Limitations

### Strengths

✅ **Comprehensive coverage:** Entire contiguous US at fine resolution
✅ **Consistent methodology:** Same grid structure across all years
✅ **Privacy-protected:** Publicly accessible without restricted data agreement
✅ **High spatial resolution:** 0.01-degree grid captures intra-county variation
✅ **Integrated demographics + environment:** No need for separate linkage

### Limitations

⚠️ **Experimental status:** Dataset may change in future releases
⚠️ **Limited environmental hazards:** Currently only CO and Ozone (1999-2022)
⚠️ **Air pollution lag:** Pollution data ends 2022 (2-3 year lag behind demographics)
⚠️ **Large file sizes:** Parquet files are multi-gigabyte (requires sufficient RAM/storage)
⚠️ **Privacy trade-off:** Aggregation to grid cells prevents very fine-scale analysis
⚠️ **Contiguous US only:** Alaska, Hawaii, territories not currently included
⚠️ **Income deciles not inflation-adjusted:** Decile cutoffs change over time

### Important Notes

1. **Experimental Data Product:** Census Bureau notes this is experimental; methodology may evolve
2. **Citation Required:** Cite as: U.S. Census Bureau, Gridded Environmental Impacts Frame (Gridded EIF), https://www.census.gov/data/experimental-data-products/gridded-eif.html
3. **Not Official Statistics:** This is not an official Census Bureau statistic
4. **Validation Recommended:** Compare aggregated results with official Census county totals

---

## 📚 Related Data Sources

### Census Bureau Data (for comparison/validation)
- **American Community Survey (ACS):** County-level demographics (NHGIS)
- **Decennial Census:** 10-year population counts by county
- **TIGER/Line Shapefiles:** County boundaries for spatial aggregation

### Air Pollution Data (alternative sources)
- **EPA AQS:** Ground monitor measurements (sparse coverage)
- **CACES National Air Pollution Maps:** Original source for Gridded EIF pollution data
- **NASA SEDAC:** Gridded population and air pollution estimates
- **NOAA HYSPLIT:** Atmospheric dispersion models

### Environmental Justice Tools
- **EPA EJScreen:** Combines demographics + environmental indicators by Census tract
- **CDC Environmental Justice Index:** County/census tract environmental burden + social vulnerability

---

## 📖 Documentation and Support

### Official Documentation
- **Main page:** https://www.census.gov/data/experimental-data-products/gridded-eif.html
- **Working paper:** Voorheis, J. (2024). The Privacy-Protected Gridded Environmental Impacts Frame. Census Bureau Working Paper CES-WP-24-74.
  - URL: https://www.census.gov/library/working-papers/2024/adrm/CES-WP-24-74.html
  - PDF: https://www2.census.gov/library/working-papers/2024/adrm/ces/CES-WP-24-74.pdf

### Technical Support
- **Census Bureau contact:** Via main EIF product page
- **GitHub issues:** (If Census creates public repository)

### Related Research
- **Kim et al. (2020):** Air pollution methodology
- **Environmental Inequality Lab:** Research using EIF data (https://www.environmental-inequality-lab.org/)

---

## 🎯 Priority Derived Variables for County-Level Analysis

For environmental health research, aggregate these key metrics to county level:

### Demographics
1. **Total population** by age group, sex, race/ethnicity
2. **Percent by race/ethnicity** (White, Black, Hispanic, Asian, etc.)
3. **Percent by income decile** (lowest 10%, highest 10%, etc.)
4. **Racial/income diversity indices** (e.g., Gini coefficient, entropy)

### Environmental Exposures (Population-Weighted Means)
5. **Mean CO exposure (ppb)** - population-weighted average
6. **Mean O₃ exposure (ppb)** - population-weighted average
7. **Percent exposed above EPA standard** (if thresholds available)
8. **Disparity metrics:** Exposure differences by race/income

### Environmental Justice Metrics
9. **Correlation between race/income and pollution exposure**
10. **Excess pollution burden on minority/low-income populations**

---

## ✅ Recommended Workflow

### Step 1: Download Data
Visit Census Bureau Gridded EIF page and download Parquet files for desired years

### Step 2: Load in R or Python
Use `arrow` (R) or `pandas.read_parquet()` (Python)

### Step 3: Spatial Join to Counties
Use `sf` (R) or `geopandas` (Python) to assign grid cells to counties

### Step 4: Aggregate with Population Weights
Calculate county-level statistics using population-weighted means for exposures

### Step 5: Validate
Compare aggregated demographics to official ACS/Census county totals

### Step 6: Analyze
Perform environmental health or environmental justice analyses

---

**Last Updated:** November 13, 2025
**Version:** 1.0 (Initial documentation)
**Data Product Status:** Experimental (Census Bureau)
