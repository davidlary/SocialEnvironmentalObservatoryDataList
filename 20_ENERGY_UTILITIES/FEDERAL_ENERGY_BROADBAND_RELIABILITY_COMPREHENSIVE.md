# COMPREHENSIVE TECHNICAL DOCUMENTATION: FEDERAL ENERGY, BROADBAND, AND ELECTRICITY RELIABILITY DATA FOR US COUNTY-LEVEL HEALTH OBSERVATORY

**Document Version:** 1.0
**Last Updated:** 2025-11-12
**Author:** Research Investigation for County-Level Environmental and Social Health Observatory
**Purpose:** Technical reference for accessing and processing three federal data sources for health outcomes research

---

## TABLE OF CONTENTS

1. [SOURCE 1: DOE LEAD Tool (Low-Income Energy Affordability Data)](#source-1-doe-lead-tool)
2. [SOURCE 2: FCC Broadband Data Collection (BDC)](#source-2-fcc-broadband-data-collection)
3. [SOURCE 3: EIA Form 861 - Electricity Reliability](#source-3-eia-form-861-electricity-reliability)
4. [Appendix A: Cross-Source Integration Strategies](#appendix-a-cross-source-integration)
5. [Appendix B: Health Relevance Summary](#appendix-b-health-relevance-summary)
6. [References](#references)

---

## SOURCE 1: DOE LEAD TOOL (Low-Income Energy Affordability Data)

### 1.1 OVERVIEW

The Low-Income Energy Affordability Data (LEAD) Tool was created by the U.S. Department of Energy's Better Buildings Clean Energy for Low Income Communities Accelerator (CELICA) to provide comprehensive housing and energy characteristics data for low- and moderate-income (LMI) communities across the United States.

### 1.2 EXACT DATA PORTAL URLs

**Primary Data Downloads:**
- **2022 Update (Most Recent):** https://data.openei.org/submissions/6219
- **2018 Update:** https://data.openei.org/submissions/573
- **Interactive Web Tool:** https://lead.openei.org/
- **Data.gov Portal:** https://catalog.data.gov/dataset/low-income-energy-affordability-data-lead-tool-2022-update
- **Methodology Documentation:** https://www.energy.gov/sites/default/files/2024-12/lead-methodology_122024.pdf

### 1.3 COUNTY-LEVEL VARIABLES AVAILABLE

The LEAD Tool provides county-level data with the following variable categories:

#### 1.3.1 Energy Burden Metrics
- **Energy Burden Percentage:** Percentage of gross household income spent on energy costs
  - Variable naming pattern: Energy burden by income level (AMI, FPL categories)
  - High energy burden threshold: 6% or greater
  - National average for low-income households: 6% (3x higher than non-low-income at 2%)

#### 1.3.2 Income Categories
- **AMI (Area Median Income):** Categories include 0-30%, 30-50%, 50-80%, 80-100%, 100-150%, 150%+
- **SMI (State Median Income):** Same categorical breakdowns as AMI
- **FPL (Federal Poverty Level):** Categories include 0-100%, 100-138%, 138-200%, 200-400%, 400%+
- **LLSI (Lower Living Standard Income):** Additional income benchmark

#### 1.3.3 Energy Expenditure Variables
- Annual energy costs (dollars)
- Monthly energy expenditures
- Electricity costs (mean, median)
- Natural gas costs (mean, median)
- Other fuel costs (heating oil, propane, wood, etc.)

#### 1.3.4 Housing Characteristics
- Building age categories
- Building type (single-family, multi-family, mobile home)
- Owner vs. renter status
- Housing costs (total)
- Number of households by income level

#### 1.3.5 Demographic Variables
- Population counts by income level
- Educational attainment levels
- Number of homeowners vs. renters

**Note:** The complete list of exact variable field names is documented in the "02. Data Dictionary 2022.xlsx" file included in the 2022 data download. This data dictionary contains detailed descriptions of abbreviations and units used in the LEAD Tool data.

### 1.4 TEMPORAL COVERAGE

- **2022 Update:**
  - Based on: 2018-2022 U.S. Census American Community Survey 5-Year Public Use Microdata Samples
  - Calibrated to: 2022 U.S. Energy Information Administration data
    - Electric utility: Survey Form EIA-861
    - Natural gas utility: Survey Form EIA-176
  - Published: August 2024

- **2018 Update:**
  - Based on: 2014-2018 ACS 5-Year PUMS
  - Published: July 2020

- **Update Frequency:** Approximately every 4 years (not on a fixed schedule)

### 1.5 SPATIAL RESOLUTION

The LEAD Tool provides data at multiple geographic levels:
- **National:** United States total
- **State:** 50 states + District of Columbia + Puerto Rico (52 geographies)
- **County:** All U.S. counties
- **City:** Incorporated cities
- **Census Tract:** Sub-county level
- **Tribal Areas:** Federally recognized tribal lands
- **Disadvantaged Communities:** As defined by federal criteria

**Geographic Overlap Files:**
- Cities-to-Tracts mapping
- Tribal Areas-to-Tracts mapping

### 1.6 FILE FORMATS

- **Excel (.xlsx):** Data dictionary and reference lists
- **ZIP Archives:** State-level data files (one ZIP per state)
- **CSV (within ZIP files):** Actual data tables
- **PDF:** Methodology documentation
- **Web Interface:** Interactive queries via lead.openei.org

**Total Dataset Size (2022):** 7.31 GB (60 files for bulk download)

### 1.7 DATA ACCESS METHODS

#### Method 1: Bulk Download (Recommended for Research)
```
1. Navigate to: https://data.openei.org/submissions/6219
2. Click "Download All Resources" button
3. Downloads: All 60 files (7.31 GB) as a single batch
4. Extract ZIP files by state
5. Read CSV files for county-level data
```

#### Method 2: Individual State Downloads
```
1. Navigate to: https://data.openei.org/submissions/6219
2. Scroll to "Files" section
3. Download individual state ZIP files as needed
4. Each state ZIP contains county, city, and tract data for that state
```

#### Method 3: Interactive Web Tool
```
1. Navigate to: https://lead.openei.org/
2. Select geography (state, county, city)
3. Select income levels and housing types
4. Generate custom heat maps and charts
5. Export customized data as CSV or Excel
```

**No formal API:** The LEAD Tool does not currently offer a programmatic API for automated data access. All downloads are file-based.

### 1.8 VARIABLE DEFINITIONS AND UNITS

| Variable Category | Definition | Units | Notes |
|------------------|------------|-------|-------|
| Energy Burden | (Average Annual Energy Cost / Average Annual Household Income) × 100 | Percent (%) | Values >6% considered high burden |
| Energy Cost | Total annual household energy expenditure | US Dollars ($) | Sum of electricity, gas, and other fuels |
| Electricity Cost | Annual electricity expenditure | US Dollars ($) | Calibrated to EIA-861 utility data |
| Natural Gas Cost | Annual natural gas expenditure | US Dollars ($) | Calibrated to EIA-176 utility data |
| Other Fuel Cost | Annual expenditure on heating oil, propane, wood, etc. | US Dollars ($) | Varies by region |
| Household Income | Annual gross household income | US Dollars ($) | From ACS 5-year estimates |
| Number of Households | Count of households in geography/income category | Count | Weighted from ACS PUMS |
| AMI | Area Median Income (HUD definition) | Percent (%) | 0-80% AMI = low-income |
| FPL | Federal Poverty Level | Percent (%) | <100% = in poverty |
| SMI | State Median Income | Percent (%) | State-specific benchmark |

### 1.9 HEALTH RELEVANCE

#### 1.9.1 Heat and Cold Mortality Risk

**Mechanism:** High energy burden forces households to choose between paying energy bills and other necessities (food, medicine), leading to:
- **Cold stress in winter:** Inability to afford adequate heating increases risk of hypothermia, cardiovascular events, and respiratory illness, particularly among elderly populations
- **Heat stress in summer:** Inability to afford air conditioning during heat waves increases risk of heat stroke, dehydration, and death

**Evidence:**
- Study by Hernández et al. (2021) in *International Journal of Environmental Research and Public Health* found that county-level energy burden from LEAD Tool data had significant effects on premature mortality, self-reported health, and life expectancy across U.S. counties
- During heat waves, elderly and poor populations are more likely to experience adverse health outcomes or death because they cannot keep homes adequately cool
- Older adults spend more of their incomes on energy than younger age groups and tend to live in older, less energy-efficient homes

**Key Vulnerable Populations:**
- Elderly adults (especially those 65+)
- Infants and young children
- Individuals with chronic illnesses (cardiovascular disease, respiratory conditions, diabetes)
- Disabled individuals
- Low-income households (<80% AMI or <200% FPL)

#### 1.9.2 Energy Insecurity and Health Outcomes

**Mechanism:** Energy insecurity encompasses:
- Inability to pay energy bills
- Keeping home at unsafe/unhealthy temperatures
- Cutting back on basic necessities (medicine, food) to pay energy bills

**Evidence:**
- Health Affairs (2024) study found energy insecurity indicators associated with increased odds of respiratory conditions, mental health problems, and cardiovascular conditions
- In 2023, nearly 1 in 3 older adults (14.8 million people) were energy insecure in the United States
- Physical and psychological disturbances from inhospitable indoor temperatures
- Anxiety and stress associated with energy debt and economic trade-offs

**Specific Health Outcomes:**
- Respiratory illness (exacerbation of asthma, COPD)
- Cardiovascular events (cold stress increases blood pressure, cardiac strain)
- Mental health (depression, anxiety from economic stress)
- Excess winter mortality (thermal stress on cardio-respiratory system)

#### 1.9.3 Refrigerated Medications

**Mechanism:** Households with high energy burden may:
- Experience utility shutoffs due to non-payment
- Reduce refrigerator/freezer use to lower bills
- Risk medication spoilage for critical refrigerated drugs

**Critical Medications Affected:**
- Insulin (for diabetes management)
- Certain antibiotics
- Biologics for autoimmune conditions
- Some cardiac medications
- Vaccines

### 1.10 DATA SOURCES FEEDING LEAD TOOL

1. **U.S. Census Bureau American Community Survey (ACS)**
   - 5-Year Public Use Microdata Samples (PUMS)
   - Variables: Income, housing characteristics, household demographics, educational attainment

2. **U.S. Energy Information Administration (EIA)**
   - Form EIA-861: Electric utility data (sales, revenue, customers by sector)
   - Form EIA-176: Natural gas utility data (deliveries, revenue, customers by sector)
   - Used to calibrate modeled energy costs to actual utility-level averages

3. **U.S. Department of Housing and Urban Development (HUD)**
   - Area Median Income (AMI) definitions by geography

4. **U.S. Department of Health and Human Services**
   - Federal Poverty Level (FPL) thresholds

**Modeling Approach:** The LEAD Tool uses a statistical model that:
- Takes ACS household-level microdata (housing type, age, size, income, location)
- Estimates energy consumption based on housing characteristics
- Applies local utility rates from EIA data
- Calculates energy burden at household level
- Aggregates to geographic levels (county, city, tract, state)

### 1.11 R CODE EXAMPLES

#### Example 1: Download and Process Single State (County Level)

```r
library(tidyverse)
library(httr)

# Function to download LEAD Tool data for a specific state
download_lead_data <- function(state_name, year = "2022", output_dir = "data/lead") {

  # Create output directory
  dir.create(output_dir, recursive = TRUE, showWarnings = FALSE)

  # Base URL for LEAD Tool 2022 data on OpenEI
  # Note: Actual file URLs must be obtained from https://data.openei.org/submissions/6219
  # The direct download links are provided on the OpenEI page for each state

  base_url <- "https://data.openei.org/files/6219/"

  # Construct filename (example pattern - verify exact naming from OpenEI)
  zip_filename <- paste0("LEAD_Tool_2022_", state_name, ".zip")
  file_url <- paste0(base_url, zip_filename)

  # Download ZIP file
  download_path <- file.path(output_dir, zip_filename)

  cat("Downloading LEAD data for", state_name, "...\n")
  GET(file_url, write_disk(download_path, overwrite = TRUE))

  # Unzip
  cat("Extracting files...\n")
  unzip(download_path, exdir = output_dir)

  # Read county-level data
  # Note: CSV filename pattern must be verified from actual ZIP contents
  county_file <- file.path(output_dir, paste0(state_name, "_County.csv"))

  if (file.exists(county_file)) {
    county_data <- read_csv(county_file, show_col_types = FALSE)
    cat("Successfully loaded", nrow(county_data), "county records for", state_name, "\n")
    return(county_data)
  } else {
    cat("County file not found. Check ZIP contents for correct filename.\n")
    return(NULL)
  }
}

# Example usage
# alabama_counties <- download_lead_data("Alabama")
```

#### Example 2: Bulk Download All States and Combine County Data

```r
library(tidyverse)
library(httr)

# Function to download and process all LEAD Tool state data
download_all_lead_counties <- function(year = "2022", output_dir = "data/lead") {

  # List of all states (50 states + DC + PR)
  states <- c(state.name, "District of Columbia", "Puerto Rico")

  # Initialize list to store county data
  all_counties <- list()

  # Loop through states
  for (state in states) {
    cat("\n========================================\n")
    cat("Processing:", state, "\n")
    cat("========================================\n")

    # Download and read county data
    tryCatch({
      county_data <- download_lead_data(state, year, output_dir)

      if (!is.null(county_data)) {
        # Add state identifier if not already in data
        if (!"state" %in% names(county_data)) {
          county_data <- county_data %>% mutate(state = state)
        }
        all_counties[[state]] <- county_data
      }

      # Polite delay between downloads
      Sys.sleep(2)

    }, error = function(e) {
      cat("Error processing", state, ":", e$message, "\n")
    })
  }

  # Combine all county data
  cat("\n========================================\n")
  cat("Combining all county data...\n")
  cat("========================================\n")

  national_counties <- bind_rows(all_counties)

  cat("Total counties:", nrow(national_counties), "\n")

  # Save combined dataset
  output_file <- file.path(output_dir, "LEAD_Tool_2022_All_Counties_National.csv")
  write_csv(national_counties, output_file)
  cat("Saved national county dataset to:", output_file, "\n")

  return(national_counties)
}

# Example usage
# lead_counties <- download_all_lead_counties()
```

#### Example 3: Extract Specific Energy Burden Variables

```r
library(tidyverse)

# Function to extract key energy burden variables for health analysis
extract_energy_burden_health_vars <- function(lead_data) {

  # Select variables relevant for health outcomes research
  # Note: Exact column names must be verified from Data Dictionary 2022.xlsx

  health_vars <- lead_data %>%
    select(
      # Geographic identifiers
      state,
      county_name = contains("county"),  # adjust to actual column name
      county_fips = contains("fips"),    # adjust to actual column name

      # Energy burden by income level
      matches("energy_burden.*AMI"),     # Energy burden for AMI categories
      matches("energy_burden.*FPL"),     # Energy burden for FPL categories

      # Energy costs
      matches("electricity.*cost"),      # Electricity costs
      matches("gas.*cost"),              # Natural gas costs
      matches("fuel.*cost"),             # Other fuel costs
      matches("total.*energy.*cost"),    # Total energy costs

      # Household counts by income
      matches("households.*AMI"),        # Number of households by AMI
      matches("households.*FPL"),        # Number of households by FPL

      # Income statistics
      matches("median.*income"),         # Median income measures
      matches("mean.*income"),           # Mean income measures

      # Housing characteristics
      matches("owner.*renter"),          # Ownership status
      matches("building.*age"),          # Housing age
      matches("building.*type")          # Housing type
    )

  return(health_vars)
}

# Example usage
# lead_health <- extract_energy_burden_health_vars(lead_counties)
```

#### Example 4: Calculate High Energy Burden Prevalence by County

```r
library(tidyverse)

# Function to calculate percentage of households with high energy burden (>6%)
calculate_high_burden_prevalence <- function(lead_data) {

  # This example assumes specific column structure
  # Column names must be adjusted based on actual LEAD Tool data dictionary

  prevalence <- lead_data %>%
    # Calculate weighted average energy burden
    mutate(
      # Total households in county
      total_households = rowSums(select(., matches("^households_AMI")), na.rm = TRUE),

      # Weighted sum of energy burden
      # (assuming columns like: energy_burden_AMI_0_30, households_AMI_0_30, etc.)
      weighted_burden = (
        energy_burden_AMI_0_30 * households_AMI_0_30 +
        energy_burden_AMI_30_50 * households_AMI_30_50 +
        energy_burden_AMI_50_80 * households_AMI_50_80 +
        energy_burden_AMI_80_100 * households_AMI_80_100 +
        energy_burden_AMI_100_150 * households_AMI_100_150 +
        energy_burden_AMI_150_plus * households_AMI_150_plus
      ) / total_households,

      # High burden flag (>6%)
      high_burden_flag = if_else(weighted_burden > 6, 1, 0),

      # Calculate % households with >6% burden
      pct_high_burden = (
        households_AMI_0_30 * (energy_burden_AMI_0_30 > 6) +
        households_AMI_30_50 * (energy_burden_AMI_30_50 > 6) +
        households_AMI_50_80 * (energy_burden_AMI_50_80 > 6)
      ) / total_households * 100
    ) %>%
    select(
      county_fips,
      county_name,
      state,
      total_households,
      weighted_burden,
      high_burden_flag,
      pct_high_burden
    )

  return(prevalence)
}

# Example usage
# high_burden <- calculate_high_burden_prevalence(lead_counties)
#
# # Summary statistics
# summary(high_burden$pct_high_burden)
#
# # Counties with highest energy burden
# high_burden %>%
#   arrange(desc(pct_high_burden)) %>%
#   head(20)
```

---

## SOURCE 2: FCC BROADBAND DATA COLLECTION (BDC)

### 2.1 OVERVIEW

The Federal Communications Commission's Broadband Data Collection (BDC) program collects and publishes broadband availability data reported by internet service providers (ISPs) across the United States. The BDC replaced the older Form 477 system and provides location-level broadband availability data at census block resolution and finer (using the Broadband Serviceable Location Fabric).

### 2.2 EXACT DATA PORTAL URLs

**Primary Data Access:**
- **National Broadband Map Data Downloads:** https://broadbandmap.fcc.gov/data-download
- **FCC BDC Main Page:** https://www.fcc.gov/BroadbandData
- **BDC Resources Page:** https://www.fcc.gov/BroadbandData/resources
- **BDC Help Center:** https://help.bdc.fcc.gov/hc/en-us
- **ArcGIS Living Atlas (June 2024):** https://www.arcgis.com/home/item.html?id=22ca3a8bb2ff46c1983fb45414157b08
- **FCC BDC System (for filers):** https://bdc.fcc.gov/

**API Endpoints:**
- **Census Block Conversions API:** https://www.fcc.gov/general/census-block-conversions-api-v100
- **FCC Area API:** https://geo.fcc.gov/api/census/
- **BDC Filer API (GitHub):** https://github.com/FCC/bdcapi

**Data Specifications:**
- **BDC Availability Data Specifications (PDF):** https://www.fcc.gov/sites/default/files/bdc-availability-data-specifications-03042022.pdf

### 2.3 CENSUS BLOCK LEVEL VARIABLES AVAILABLE

The FCC BDC provides data at the Broadband Serviceable Location (BSL) level and census block level. Variables can be aggregated to county level.

#### 2.3.1 Geographic Identifiers

| Field Name | Description | Format | Example |
|------------|-------------|--------|---------|
| location_id | Unique identifier for BSL in FCC Fabric | String | Location ID from Fabric |
| block_geoid | 15-digit Census Block GEOID (2020 Census) | String | SSCCCTTTTTTBBBB |
| state_fips | 2-digit state FIPS code | String | "01" = Alabama |
| county_fips | 5-digit county FIPS code (state + county) | String | "01001" = Autauga County, AL |
| tract_geoid | 11-digit Census Tract GEOID | String | State + County + Tract |
| block_group_geoid | 12-digit Block Group GEOID | String | State + County + Tract + BG |

**GEOID Structure (15 digits):**
- Positions 1-2: State FIPS (SS)
- Positions 3-5: County FIPS (CCC)
- Positions 6-11: Tract code (TTTTTT)
- Positions 12-15: Block code (BBBB)

#### 2.3.2 Broadband Availability Variables

| Field Name | Description | Values | Notes |
|------------|-------------|--------|-------|
| technology | Broadband technology type | Integer codes | See technology codes table below |
| max_advertised_download_speed | Maximum advertised download speed | Integer (Mbps) | Downstream speed in megabits per second |
| max_advertised_upload_speed | Maximum advertised upload speed | Integer (Mbps) | Upstream speed in megabits per second |
| low_latency | Low latency service indicator | Boolean (0/1) | 1 = latency ≤100 ms |
| business_residential_code | Service type | String | "R" = Residential, "B" = Business, "X" = Both |

**Technology Codes:**

| Code | Technology Type | Description |
|------|----------------|-------------|
| 10 | Copper Wire (DSL) | Digital Subscriber Line over copper telephone lines |
| 40 | Coaxial Cable (Cable Modem) | Cable internet service over coaxial cable |
| 50 | Fiber to the Premises (FTTP) | Fiber optic cable directly to location |
| 60 | Satellite | Satellite internet (including LEO satellites like Starlink) |
| 70 | Fixed Wireless | Terrestrial fixed wireless service |
| 0 | Other | Other technologies not elsewhere classified |

#### 2.3.3 Provider Information

| Field Name | Description | Format |
|------------|-------------|--------|
| provider_id | FCC Registration Number (FRN) of provider | Integer |
| brand_name | Consumer-facing brand name | String |
| holding_company_name | Parent company name | String |

#### 2.3.4 Speed Tier Definitions (for Aggregation)

The FCC uses several key speed tiers for broadband classification:

| Tier Name | Download Speed | Upload Speed | Classification |
|-----------|---------------|--------------|----------------|
| Basic Broadband | ≥25 Mbps | ≥3 Mbps | FCC 2015 definition |
| Advanced Broadband | ≥100 Mbps | ≥20 Mbps | FCC 2024 benchmark |
| Gigabit Broadband | ≥1000 Mbps | ≥100 Mbps | High-performance |

**Served/Underserved/Unserved Classification:**
- **Served:** Access to ≥100/20 Mbps
- **Underserved:** Access to ≥25/3 Mbps but <100/20 Mbps
- **Unserved:** No access to ≥25/3 Mbps

### 2.4 TEMPORAL COVERAGE

- **BDC Launch:** June 30, 2022 (first data collection)
- **Update Frequency:** Twice per year (biannual)
- **Data Collection Windows:** December 31 and June 30 of each year
- **Lag Time:** Approximately 6 months from collection to publication

**Available Data Releases:**
1. December 31, 2022 (published mid-2023)
2. June 30, 2023 (published late 2023/early 2024)
3. December 31, 2023 (published June 2024)
4. June 30, 2024 (published November 15, 2024) - **Fifth Version, most recent**

**Historical Data (Legacy Form 477):**
- Fixed broadband deployment data available 1999-2021
- Methodology differs from BDC (census block vs. BSL)
- Available at: https://www.fcc.gov/general/broadband-deployment-data-fcc-form-477

### 2.5 SPATIAL RESOLUTION

The BDC provides data at multiple geographic resolutions:

1. **Broadband Serviceable Location (BSL):** Individual addresses/structures (finest resolution)
2. **Census Block (2020):** ~11 million blocks nationally
3. **Census Block Group:** ~242,000 block groups
4. **Census Tract:** ~85,000 tracts
5. **County:** ~3,100 counties
6. **State:** 50 states + DC + territories
7. **H3 Hexagon Resolution 8:** Uber H3 hexagonal grid cells

**For County-Level Analysis:** Aggregate census block data to county level using 5-digit county FIPS code (first 5 characters of block_geoid).

### 2.6 FILE FORMATS

- **CSV (Comma Separated Values):** Fixed broadband availability data
- **Shapefile:** Mobile broadband coverage maps (GIS format)
- **GeoPackage:** Alternative GIS format
- **Parquet:** Not currently offered (CSV only for fixed broadband)

**File Size Considerations:**
- Nationwide data files are very large (multiple gigabytes)
- State-level files are more manageable (varies by state)
- Cannot be opened in Excel due to size; use R, Python, or database software

### 2.7 DATA ACCESS METHODS

#### Method 1: Direct Download from National Broadband Map (Recommended)

```
1. Navigate to: https://broadbandmap.fcc.gov/data-download
2. Select "Fixed Broadband" for wired/wireless terrestrial service
3. Choose download scope:
   a. Nationwide data (all states combined)
   b. By State (select individual states)
   c. By Provider (filter by specific ISP)
4. Select data version (e.g., "June 2024" - most recent)
5. Download CSV file(s)
6. Extract and process in R or database system
```

#### Method 2: FCC Area API (Geocoding)

```
API Endpoint: https://geo.fcc.gov/api/census/

Query Parameters:
- lat: Latitude (decimal degrees)
- lon: Longitude (decimal degrees)
- censusYear: 2020 (for current census)
- format: json

Returns:
- Census block GEOID (15-digit)
- County name and FIPS
- State name and FIPS
- Block population

Example R code:
library(httr)
library(jsonlite)

get_census_block <- function(lat, lon) {
  url <- "https://geo.fcc.gov/api/census/block/find"
  response <- GET(url, query = list(
    latitude = lat,
    longitude = lon,
    censusYear = 2020,
    format = "json"
  ))
  return(content(response, as = "parsed"))
}
```

#### Method 3: BDC Filer API (for bulk submissions)

- **GitHub Repository:** https://github.com/FCC/bdcapi
- **Purpose:** Designed for ISPs filing bulk challenges and responses
- **Not recommended for research data downloads:** Use Method 1 instead

### 2.8 VARIABLE DEFINITIONS AND UNITS

| Variable | Definition | Unit | Range |
|----------|-----------|------|-------|
| max_advertised_download_speed | Maximum downstream speed advertised by provider | Megabits per second (Mbps) | 0.2 - 10,000+ |
| max_advertised_upload_speed | Maximum upstream speed advertised by provider | Megabits per second (Mbps) | 0.2 - 10,000+ |
| low_latency | Round-trip latency ≤100 milliseconds | Boolean | 0 = No, 1 = Yes |
| technology | Type of transmission technology | Categorical code | 10, 40, 50, 60, 70, 0 |
| location_id | Broadband Serviceable Location identifier | String | Unique per location |
| block_geoid | 2020 Census Block identifier | String (15 digits) | SSCCCTTTTTTBBBB |

**Important Notes:**
- Speeds are **advertised maximum**, not measured actual speeds
- Availability means provider **can** offer service, not that service is subscribed
- Data is self-reported by ISPs; FCC conducts verification and challenge process

### 2.9 HEALTH RELEVANCE

#### 2.9.1 Telehealth Access

**Mechanism:** Broadband internet is essential infrastructure for telehealth services, enabling:
- Video consultations with healthcare providers
- Remote patient monitoring
- Digital health record access
- Prescription refills and medication management
- Mental health counseling

**Evidence:**
- Medicare Fee-for-Service study (2020): Counties with greatest broadband availability had **47% higher telehealth utilization** compared to counties with least broadband availability (study covered 3,107 counties)
- COVID-19 pandemic research: For every additional 1% of residents in counties with internet access, between **2.4 and 6 deaths per 100,000 residents were preventable**
- Telehealth expansion alone unlikely to improve health outcomes unless paired with parallel investments in broadband infrastructure

**Key Vulnerable Populations:**
- Rural residents (limited provider access)
- Elderly adults (higher healthcare needs)
- Individuals with mobility limitations
- Patients with chronic conditions requiring frequent monitoring
- Mental health patients (counseling via telehealth)

#### 2.9.2 Health Information Access

**Mechanism:** Internet access enables:
- Searching for health information and symptoms
- Finding healthcare providers and facilities
- Accessing patient portals for test results
- Health insurance enrollment and management
- Public health information during emergencies

**Evidence:**
- "Double-burdened counties" in Appalachia: >70% of counties with highest lung cancer incidence/mortality have rural broadband access <50%
- Digital exclusion (lack of computer/mobile device access) significantly associated with higher coronary heart disease (CHD) prevalence and mortality in Deep South counties

#### 2.9.3 Social Isolation and Mental Health

**Mechanism:** Lack of broadband access contributes to:
- Social isolation, especially among elderly
- Reduced connection with family and friends
- Limited participation in online communities
- Barriers to mental health resources
- Economic isolation (difficulty with employment, education)

**Evidence:**
- Rural broadband disparities associated with worse mental health outcomes
- Social isolation increases mortality risk comparable to smoking
- COVID-19 pandemic highlighted role of internet in maintaining social connections

#### 2.9.4 Digital Determinants of Health

**Broader Framework:**
Broadband access is increasingly recognized as a social determinant of health alongside housing, education, and food security. The Federal Communications Commission's mapping helps identify geographic disparities that align with health inequities.

**Speed Requirements for Health Applications:**
- **Video telehealth:** Minimum 25/3 Mbps (HD quality), recommended 100/20 Mbps
- **Remote patient monitoring:** 10/1 Mbps
- **Health information browsing:** 5/1 Mbps
- **Multiple simultaneous users:** Higher speeds needed

### 2.10 DATA SOURCES FEEDING FCC BDC

#### 2.10.1 Broadband Serviceable Location (BSL) Fabric

- **Created by:** CostQuest Associates under contract to FCC
- **Purpose:** Master dataset of all locations where broadband can be installed
- **Data Sources:**
  - Address data from state, local, and tribal governments
  - Commercially available property data
  - Utility infrastructure data
  - Tax assessor records
  - Field validation

#### 2.10.2 Internet Service Provider (ISP) Submissions

- **Filers:** All facilities-based broadband providers in the U.S.
- **Submission Frequency:** Biannual (June 30, December 31)
- **Required Information:**
  - List of BSL IDs where service available
  - Technology type for each location
  - Maximum advertised speeds (download/upload)
  - Latency category

#### 2.10.3 Challenge Process

- **State, Local, and Tribal Governments:** Can challenge provider submissions
- **Consumers:** Can report inaccurate availability data
- **Verification:** FCC conducts on-the-ground testing and validation

### 2.11 R CODE EXAMPLES

#### Example 1: Download FCC BDC Data for Single State

```r
library(tidyverse)
library(httr)
library(data.table)

# Function to download FCC BDC fixed broadband data for a state
download_fcc_bdc_state <- function(state_abbr,
                                    data_version = "dec2023",
                                    output_dir = "data/fcc_bdc") {

  # Create output directory
  dir.create(output_dir, recursive = TRUE, showWarnings = FALSE)

  # Base URL for FCC National Broadband Map data downloads
  # Note: Actual URLs are provided on https://broadbandmap.fcc.gov/data-download
  # File naming conventions may vary by data release

  base_url <- "https://broadbandmap.fcc.gov/data-download/nationwide-data"

  # Construct state filename
  # Example format: fixed_broadband_deployment_STATE_YYYYMMDD.csv
  # Verify exact naming convention from FCC download page

  csv_filename <- paste0("fixed_broadband_", state_abbr, "_", data_version, ".csv")
  file_url <- paste0(base_url, "/", csv_filename)

  download_path <- file.path(output_dir, csv_filename)

  cat("Downloading FCC BDC data for", state_abbr, "...\n")

  tryCatch({
    GET(file_url, write_disk(download_path, overwrite = TRUE), progress())

    # Read with data.table (faster for large files)
    cat("Reading CSV file...\n")
    bdc_data <- fread(download_path)

    cat("Loaded", nrow(bdc_data), "records for", state_abbr, "\n")
    return(bdc_data)

  }, error = function(e) {
    cat("Error downloading data:", e$message, "\n")
    cat("Verify URL and filename at: https://broadbandmap.fcc.gov/data-download\n")
    return(NULL)
  })
}

# Example usage
# alabama_bdc <- download_fcc_bdc_state("AL", "dec2023")
```

#### Example 2: Aggregate Census Block Data to County Level

```r
library(tidyverse)
library(data.table)

# Function to aggregate FCC BDC block-level data to counties
aggregate_bdc_to_counties <- function(bdc_block_data) {

  # Extract county FIPS from 15-digit block GEOID
  # GEOID structure: SSCCCTTTTTTBBBB
  # Positions 1-5 = state (2) + county (3) = county FIPS

  county_summary <- bdc_block_data %>%
    mutate(
      county_fips = substr(block_geoid, 1, 5),
      state_fips = substr(block_geoid, 1, 2)
    ) %>%

    # Create speed tier flags
    mutate(
      served = (max_advertised_download_speed >= 100 &
                max_advertised_upload_speed >= 20),
      underserved = (max_advertised_download_speed >= 25 &
                     max_advertised_upload_speed >= 3 &
                     !served),
      unserved = (max_advertised_download_speed < 25 |
                  max_advertised_upload_speed < 3)
    ) %>%

    # Group by county and technology
    group_by(county_fips, technology) %>%
    summarise(
      # Count of unique locations (BSLs)
      n_locations = n_distinct(location_id),

      # Count of unique providers
      n_providers = n_distinct(provider_id),

      # Locations by service tier
      n_served = sum(served, na.rm = TRUE),
      n_underserved = sum(underserved, na.rm = TRUE),
      n_unserved = sum(unserved, na.rm = TRUE),

      # Speed statistics
      median_download_speed = median(max_advertised_download_speed, na.rm = TRUE),
      median_upload_speed = median(max_advertised_upload_speed, na.rm = TRUE),
      max_download_speed = max(max_advertised_download_speed, na.rm = TRUE),
      max_upload_speed = max(max_advertised_upload_speed, na.rm = TRUE),

      # Percentage with low latency
      pct_low_latency = mean(low_latency, na.rm = TRUE) * 100,

      .groups = "drop"
    )

  return(county_summary)
}

# Example usage with speed tier summary
# county_broadband <- aggregate_bdc_to_counties(alabama_bdc)
```

#### Example 3: Calculate County-Level Broadband Availability Metrics

```r
library(tidyverse)

# Function to calculate comprehensive county-level broadband metrics
calculate_county_broadband_metrics <- function(county_summary) {

  # Aggregate across all technologies to get county-level totals
  county_metrics <- county_summary %>%
    group_by(county_fips) %>%
    summarise(
      # Overall availability
      total_locations = sum(n_locations, na.rm = TRUE),
      total_providers = n_distinct(provider_id),

      # Service quality
      pct_served = sum(n_served, na.rm = TRUE) / total_locations * 100,
      pct_underserved = sum(n_underserved, na.rm = TRUE) / total_locations * 100,
      pct_unserved = sum(n_unserved, na.rm = TRUE) / total_locations * 100,

      # Best available speeds
      best_download_speed = max(max_download_speed, na.rm = TRUE),
      best_upload_speed = max(max_upload_speed, na.rm = TRUE),

      # Technology diversity
      n_technologies = n_distinct(technology),

      # Fiber availability
      has_fiber = any(technology == 50),
      pct_fiber_locations = sum(n_locations[technology == 50], na.rm = TRUE) /
                            total_locations * 100,

      # Cable availability
      has_cable = any(technology == 40),

      # DSL availability
      has_dsl = any(technology == 10),

      # Satellite availability (often last resort)
      has_satellite = any(technology == 60),

      # Fixed wireless availability
      has_fixed_wireless = any(technology == 70),

      .groups = "drop"
    ) %>%

    # Create composite broadband access score
    mutate(
      # Telehealth readiness: % locations with ≥25/3 Mbps
      telehealth_ready = pct_served + pct_underserved,

      # Advanced broadband: % locations with ≥100/20 Mbps
      advanced_broadband = pct_served,

      # Provider competition (more providers = better)
      competition_level = case_when(
        total_providers >= 4 ~ "High",
        total_providers >= 2 ~ "Moderate",
        TRUE ~ "Low"
      ),

      # Technology diversity score (more options = better)
      tech_diversity_score = n_technologies / 5 * 100  # Max 5 tech types
    )

  return(county_metrics)
}

# Example usage
# county_metrics <- calculate_county_broadband_metrics(county_broadband)
#
# # Summary statistics
# summary(county_metrics$telehealth_ready)
#
# # Counties with lowest broadband access
# county_metrics %>%
#   arrange(telehealth_ready) %>%
#   head(20)
```

#### Example 4: Use FCC Area API to Geocode Locations and Get County FIPS

```r
library(httr)
library(jsonlite)
library(tidyverse)

# Function to get county FIPS from latitude/longitude using FCC API
get_county_from_coordinates <- function(lat, lon) {

  # FCC Area API endpoint
  url <- "https://geo.fcc.gov/api/census/block/find"

  # API query
  response <- GET(url, query = list(
    latitude = lat,
    longitude = lon,
    censusYear = 2020,
    format = "json"
  ))

  # Parse response
  if (status_code(response) == 200) {
    data <- content(response, as = "parsed")

    # Extract FIPS codes
    result <- tibble(
      lat = lat,
      lon = lon,
      state_fips = data$State$FIPS,
      state_name = data$State$name,
      county_fips = data$County$FIPS,
      county_name = data$County$name,
      block_geoid = data$Block$FIPS,
      block_pop = as.numeric(data$Block$`2020pop`)
    )

    return(result)

  } else {
    warning("API request failed for (", lat, ", ", lon, ")")
    return(NULL)
  }
}

# Function to batch geocode multiple locations
batch_geocode_to_county <- function(lat_lon_df) {

  # lat_lon_df must have columns: lat, lon

  results <- list()

  for (i in 1:nrow(lat_lon_df)) {
    cat("Geocoding location", i, "of", nrow(lat_lon_df), "\r")

    result <- get_county_from_coordinates(
      lat = lat_lon_df$lat[i],
      lon = lat_lon_df$lon[i]
    )

    if (!is.null(result)) {
      results[[i]] <- result
    }

    # Rate limiting: FCC API has usage limits
    Sys.sleep(0.5)  # 2 requests per second max
  }

  # Combine results
  geocoded_df <- bind_rows(results)

  return(geocoded_df)
}

# Example usage
# locations <- tibble(
#   lat = c(32.3792, 33.5186, 30.6954),
#   lon = c(-86.3077, -86.8104, -88.0399)
# )
#
# geocoded <- batch_geocode_to_county(locations)
```

---

## SOURCE 3: EIA FORM 861 - ELECTRICITY RELIABILITY

### 3.1 OVERVIEW

The U.S. Energy Information Administration (EIA) Form 861, "Annual Electric Power Industry Report," is a mandatory annual survey that collects data from all electric utilities operating in the United States. The survey includes comprehensive information on utility operations, including electricity reliability metrics (SAIFI and SAIDI) that measure the frequency and duration of power outages.

**Critical Limitation:** Reliability data is reported at the **utility level**, not at the county level. However, service territory files can be used to link utilities to the counties they serve, enabling county-level analysis through spatial aggregation.

### 3.2 EXACT DATA PORTAL URLs

**Primary Data Access:**
- **EIA Form 861 Main Page:** https://www.eia.gov/electricity/data/eia861/
- **Direct Download (Select Year):** https://www.eia.gov/electricity/data/eia861/ (scroll to year-specific ZIP files)

**Documentation:**
- **Form Instructions (2023):** https://www.reginfo.gov/public/do/DownloadDocument?objectID=126696901
- **EIA FAQs:** https://www.eia.gov/tools/faqs/faq.php?id=1194&t=1

**Processed/Cleaned Data:**
- **PUDL (Public Utility Data Liberation):** https://catalystcoop-pudl.readthedocs.io/en/latest/data_sources/eia861.html
- **PUDL GitHub:** https://github.com/catalyst-cooperative/pudl

**Related Tools:**
- **EPA EmPOWER Map (uses EIA-861 service territory):** https://empowermap.hhs.gov/
- **Electricity Entity Boundaries (GitHub):** https://github.com/IMMM-SFA/electricity_entity_boundaries

### 3.3 UTILITY-LEVEL RELIABILITY VARIABLES

#### 3.3.1 Core Reliability Metrics

| Variable Name | Full Name | Definition | Units |
|---------------|-----------|------------|-------|
| SAIFI | System Average Interruption Frequency Index | Average number of sustained interruptions (>5 minutes) per customer per year | Interruptions per customer |
| SAIDI | System Average Interruption Duration Index | Average total minutes of interruption per customer per year | Minutes per customer |
| CAIDI | Customer Average Interruption Duration Index | Average duration of each interruption | Minutes per interruption |

**Formula Definitions:**

**SAIFI:**
```
SAIFI = (Total Number of Customer Interruptions) / (Total Number of Customers Served)
```

**SAIDI:**
```
SAIDI = (Sum of All Customer Interruption Durations in Minutes) / (Total Number of Customers Served)
```

**CAIDI:**
```
CAIDI = SAIDI / SAIFI
```

#### 3.3.2 Reliability Data File Structure (from ZIP)

When you download an EIA-861 annual ZIP file (e.g., `f8612023.zip`), it contains multiple CSV files. The reliability data is in a file typically named:

**File:** `Reliability_YYYY.csv` (where YYYY = year, e.g., `Reliability_2023.csv`)

**Key Fields in Reliability File:**

| Field Name | Description | Data Type | Example Values |
|------------|-------------|-----------|----------------|
| Utility_Number | EIA utility identification number | Integer | 195, 819, 1738 |
| Utility_Name | Name of electric utility | String | "Alabama Power Co", "Pacific Gas & Electric Co" |
| State | State where utility operates | String (2-letter) | "AL", "CA", "TX" |
| Report_Year | Year of data | Integer | 2023 |
| SAIFI | System Average Interruption Frequency Index | Decimal | 0.85, 1.42, 2.11 |
| SAIDI | System Average Interruption Duration Index | Decimal | 112.5, 203.7, 441.2 |
| SAIFI_With_MED | SAIFI including Major Event Days | Decimal | 1.05 |
| SAIDI_With_MED | SAIDI including Major Event Days | Decimal | 250.3 |
| SAIFI_Without_MED | SAIFI excluding Major Event Days | Decimal | 0.82 |
| SAIDI_Without_MED | SAIDI excluding Major Event Days | Decimal | 98.7 |
| IEEE_Standard_Used | Whether utility uses IEEE 1366 standard | String | "Yes", "No" |
| Exclusions | Types of interruptions excluded | String | "Major Events", "Planned Outages" |

**Major Event Days (MED):** IEEE 1366 standard allows utilities to exclude "major events" (e.g., hurricanes, ice storms) from reliability calculations. Both "with MED" and "without MED" metrics are reported.

#### 3.3.3 Service Territory File Structure

To link utilities to counties, use the **Service Territory** file from the EIA-861 ZIP.

**File:** `Service_Territory_YYYY.csv`

**Key Fields:**

| Field Name | Description | Data Type | Example Values |
|------------|-------------|-----------|----------------|
| Utility_Number | EIA utility identification number | Integer | 195 |
| Utility_Name | Name of electric utility | String | "Alabama Power Co" |
| State | State code | String (2-letter) | "AL" |
| County | County name | String | "Autauga County", "Baldwin County" |
| Short_Form | Whether utility filed short form | String | "N", "Y" |

**Usage:** Each row represents one utility-county relationship. A utility operating in multiple counties will have multiple rows.

**County Standardization Challenge:** County names in EIA-861 are text strings and may not match standardized formats. To get FIPS codes, use a county name-to-FIPS lookup (e.g., `tigris` package in R or Census Bureau crosswalk files).

#### 3.3.4 Utility Data File (Additional Context)

**File:** `Utility_Data_YYYY.csv`

Provides additional utility characteristics:

| Field Name | Description | Example Values |
|------------|-------------|----------------|
| Utility_Number | EIA utility ID | 195 |
| Utility_Name | Utility name | "Alabama Power Co" |
| NERC_Region | North American Electric Reliability Corporation region | "SERC", "WECC", "MRO" |
| Balancing_Authority_Code | BA code | "SOCO", "CISO", "PJM" |
| ISO_RTO_Code | Independent System Operator / Regional Transmission Organization | "MISO", "NYISO", "SPP" |

### 3.4 TEMPORAL COVERAGE

- **Reliability Data Available:** 2013 - 2024 (final)
- **Historical Data (1990-2012):** Available but less comprehensive (limited reliability metrics)
- **Service Territory Data:** 2001 - 2024
- **Update Frequency:** Annual
- **Release Schedule:**
  - Early release: Summer (July-August) of year following data year
  - Final release: Fall (October-November) of year following data year
  - Example: 2023 data released October 7, 2025 (final)

**Coverage of US Utilities:**
- Form EIA-861 is a **census** of all U.S. electric utilities
- Reliability reporting: ~94% of U.S. electric customers (2017 data)
- Coverage varies by state (72% in ND/SD to 99% in CA)
- Not all utilities report reliability metrics (smaller utilities may be exempt)

### 3.5 SPATIAL RESOLUTION

**Native Geographic Level:** Utility service territory (not county)

**Geographic Aggregation Challenge:**
- Utilities serve multiple counties (e.g., Duke Energy operates in NC, SC, FL, IN, OH, KY)
- Counties are served by multiple utilities (e.g., rural areas may have cooperative + investor-owned utility)
- No standardized county-level reliability data provided by EIA

**Strategies for County-Level Analysis:**

1. **Population-Weighted Assignment:** Assign utility SAIFI/SAIDI to all counties in service territory, weight by county population served

2. **Utility Service Area Mapping:** Use GIS tools to map utility territories to counties based on census block-level assignments (see PUDL project)

3. **EPA EmPOWER Approach:** EPA's EmPOWER Map uses Medicare claims data + utility service territories to estimate electricity-dependent populations at ZIP code level

4. **Major Utility Dominance:** In counties served by single large utility, use that utility's metrics as county proxy

### 3.6 FILE FORMATS

- **ZIP Archive:** Each year's data in compressed format (e.g., `f8612023.zip`)
- **CSV (within ZIP):** Individual data tables (20+ CSV files per year)
- **Excel (.xls, .xlsx):** Older years (1990-2011) in Excel format
- **DBF (dBASE):** Very old years (1990-1998) in database format

**Download Size:**
- Annual ZIP file: 10-50 MB (varies by year)
- Uncompressed: 100-300 MB total

### 3.7 DATA ACCESS METHODS

#### Method 1: Direct Download from EIA Website (Recommended)

```
1. Navigate to: https://www.eia.gov/electricity/data/eia861/
2. Scroll to "Annual Electric Power Industry Report" section
3. Find table with years (1990 - 2024)
4. Click "Original" column link for desired year (e.g., "f8612023.zip")
5. Download ZIP file to local directory
6. Unzip to extract CSV files
7. Read Reliability_YYYY.csv and Service_Territory_YYYY.csv in R
```

#### Method 2: EIA API (Limited)

The EIA offers an API, but Form 861 data is **not fully available** via API. Bulk file download is required.

**EIA API Information:**
- **API Documentation:** https://www.eia.gov/opendata/
- **Register for API Key:** https://www.eia.gov/opendata/register.php
- **R Package (eia):** https://cran.r-project.org/package=eia
- **R Package (EIAapi):** https://cran.r-project.org/package=EIAapi

**Note:** These APIs primarily serve time-series energy data, not the detailed Form 861 reliability tables.

#### Method 3: PUDL (Public Utility Data Liberation) - Processed Data

**Overview:** Catalyst Cooperative's PUDL project cleans and standardizes EIA-861 data, adding county FIPS codes to service territory data.

**Advantages:**
- County FIPS codes added to service territory table
- Consistent data structure across years
- Python and SQL access
- Well-documented

**Access:**
- **Documentation:** https://catalystcoop-pudl.readthedocs.io/en/latest/
- **Data Downloads:** Via Zenodo (archived versions)
- **Code:** https://github.com/catalyst-cooperative/pudl

**PUDL Tables (EIA-861):**
- `core_eia861__yearly_reliability`: SAIFI, SAIDI, CAIDI metrics
- `core_eia861__yearly_service_territory`: Utility-county linkages with FIPS codes
- `core_eia861__yearly_utility_data_misc`: Utility characteristics

**Years Available in PUDL:** 2001-2024

### 3.8 VARIABLE DEFINITIONS AND UNITS

| Variable | Definition | Unit | Typical Range | Notes |
|----------|-----------|------|---------------|-------|
| SAIFI | Number of sustained interruptions per customer per year | Interruptions/customer/year | 0.5 - 3.0 | Higher = more frequent outages |
| SAIDI | Total minutes of interruption per customer per year | Minutes/customer/year | 50 - 500 | Higher = longer outages |
| CAIDI | Average duration of each interruption event | Minutes/interruption | 50 - 200 | SAIDI / SAIFI |

**Interruption Definitions (IEEE 1366):**
- **Sustained Interruption:** Loss of power for >5 minutes
- **Momentary Interruption:** Loss of power for ≤5 minutes (not included in SAIFI/SAIDI)
- **Planned Outage:** Scheduled maintenance (often excluded from metrics)
- **Unplanned Outage:** Unexpected events (storms, equipment failure, accidents)

**Exclusions (utility-reported):**
Utilities may exclude certain events from SAIFI/SAIDI calculations:
- Major Event Days (extreme weather)
- Planned maintenance outages
- Transmission system failures (not distribution system)
- Customer-owned equipment failures

**Important Caveats:**
- Reporting standards vary by utility and state
- Not all utilities report reliability data
- IEEE 1366 standard is optional (some utilities use different methods)
- "With MED" vs "Without MED" metrics provide different pictures of reliability

### 3.9 HEALTH RELEVANCE

#### 3.9.1 Medical Device Dependence

**Mechanism:** Over 685,000 electricity-dependent medical device users reside at home in the United States (2020 estimate). Power outages directly threaten life-sustaining medical equipment:

**Critical Devices:**
1. **Oxygen Concentrators:** Battery life 2-4 hours (up to 12 hours with external packs at lowest settings)
2. **Ventilators:** Essential for breathing support
3. **CPAP/BiPAP machines:** Sleep apnea treatment
4. **Home Dialysis Equipment:** Kidney disease treatment
5. **Suction Devices:** Airway clearance
6. **Feeding Pumps:** Enteral nutrition
7. **Nebulizers:** Respiratory medication delivery
8. **Wheelchair/Mobility Device Chargers:** Essential for mobility

**Evidence:**
- For medically fragile individuals, power outage can cause acute decompensation that becomes life-threatening within hours
- Power outages can be the difference between life and death for patient on oxygen concentrator
- Major power outages increased 10-fold between 1984-2012
- Average U.S. household experienced 470 minutes (7.8 hours) without power in 2017

**SAIFI and SAIDI Implications:**
- **High SAIFI:** Frequent outages require repeated device restarts, battery cycling, patient stress
- **High SAIDI:** Long outages exceed battery backup capacity, forcing evacuation or emergency intervention
- **Combined High SAIFI + SAIDI:** Worst case for medical device users (frequent AND long outages)

#### 3.9.2 Refrigerated Medications

**Mechanism:** Power outages compromise medication efficacy for refrigerated drugs (2-8°C storage required):

**Critical Medications:**
1. **Insulin:** Type 1 and Type 2 diabetes management
2. **Biologics:** Rheumatoid arthritis, Crohn's disease, psoriasis (e.g., Humira, Enbrel)
3. **Vaccines:** Childhood immunizations, flu shots
4. **Certain Antibiotics:** Reconstituted formulations
5. **Growth Hormone:** Pediatric treatment
6. **Epinephrine Auto-injectors:** Severe allergy management (after first use)

**Temperature Excursion Impacts:**
- Insulin loses potency after >24 hours at room temperature
- Biologics may denature and become ineffective (or dangerous)
- Vaccines lose effectiveness permanently

**Cost Implications:**
- Replacement cost for insulin: $300-500/month
- Biologics: $3,000-$6,000/month
- Creates medication rationing in low-income populations

#### 3.9.3 Heat and Cold Vulnerability During Outages

**Mechanism:** HVAC systems require electricity; outages during temperature extremes increase mortality risk.

**Heat-Related Mortality:**
- **At-risk populations:** Elderly, young children, individuals with cardiovascular/respiratory disease
- **Mechanism:** Loss of air conditioning → hyperthermia, dehydration, heat stroke, cardiovascular stress
- **Climate change:** Increasing frequency/intensity of heat waves compounds risk
- **Energy insecurity intersection:** Low-income households already struggle to afford AC; outages eliminate even minimal cooling

**Evidence:**
- During heat waves, elderly and poor more likely to experience adverse outcomes or death
- Climate change drives up temperatures; elderly and those with underlying conditions at increased risk of dying at home

**Cold-Related Mortality:**
- **At-risk populations:** Elderly, individuals with cardiovascular disease, homeless
- **Mechanism:** Loss of heating → hypothermia, cardiovascular strain (cold increases blood pressure)
- **Cold stress:** Exacerbates respiratory illness (flu, pneumonia, COPD)

**Evidence:**
- Fuel poverty disproportionately affects elderly, infants, and individuals with disability/long-term illness
- Plausible mechanisms linking poor quality housing to excess winter mortality include strain of thermal stress on cardio-respiratory system

**SAIFI and SAIDI Implications:**
- **Winter outages:** High SAIDI during winter storms (ice, snow) creates cold exposure risk
- **Summer outages:** High SAIDI during heat waves creates heat exposure risk
- **Rural vs. Urban:** Rural areas often have higher SAIFI/SAIDI due to longer distribution lines, fewer redundant circuits

#### 3.9.4 Cascading Health System Impacts

**Mechanism:** Power outages affect healthcare delivery infrastructure:

**Healthcare Facilities:**
- Hospitals have backup generators, but extended outages strain fuel supplies
- Rural clinics may lack adequate backup power
- Nursing homes and assisted living facilities vulnerable to extended outages
- Dialysis centers unable to treat patients during outages

**Healthcare Access:**
- Traffic signals out → emergency vehicle delays
- Medical records systems offline
- Telehealth services unavailable
- Oxygen supply company deliveries delayed

#### 3.9.5 Mental Health and Stress

**Mechanism:**
- Anxiety about power reliability for device-dependent individuals
- Economic stress from spoiled food, medication replacement
- Disrupted sleep patterns during outages
- Social isolation (no communication devices)

**Evidence:**
- Energy insecurity-mental health association explained by physical/psychological disturbances from inhospitable temperatures and anxiety/stress from economic trade-offs

### 3.10 DATA SOURCES FEEDING EIA FORM 861

#### 3.10.1 Survey Respondents

**Required Filers (Census of all U.S. electric utilities):**
1. **Electric Utilities:**
   - Investor-owned utilities (IOUs): e.g., Duke Energy, Pacific Gas & Electric, Southern Company
   - Publicly-owned utilities: Municipal utilities, public power districts
   - Rural electric cooperatives: Member-owned non-profits serving rural areas

2. **Power Marketers:** Wholesale electricity traders

3. **Energy Service Providers:** Retail electricity providers in deregulated markets

4. **Transmission Owners/Operators**

5. **Third-Party Owners:** Solar PV and other distributed generation owners

**Total Respondents:** ~3,000+ entities annually

#### 3.10.2 Data Collection Method

- **Electronic Filing:** Filers submit via EIA's secure e-file system
- **Annual Submission:** Data due ~5 months after end of calendar year
- **Verification:** EIA conducts data quality checks, contacts utilities for clarifications

#### 3.10.3 Reliability Data Sources (Utility-Level)

Utilities derive SAIFI/SAIDI metrics from:
- **Outage Management Systems (OMS):** Real-time tracking of interruptions
- **SCADA Systems:** Supervisory Control and Data Acquisition systems monitor grid
- **Customer Information Systems (CIS):** Customer account data for denominators
- **Manual Logs:** Smaller utilities may use paper/spreadsheet records

**IEEE 1366 Standard:** Many (but not all) utilities follow IEEE Standard 1366 for calculating reliability indices. This standard defines:
- Interruption duration thresholds (5 minutes)
- Exclusion criteria for major events
- Calculation methodologies

### 3.11 R CODE EXAMPLES

#### Example 1: Download and Extract EIA-861 Data

```r
library(tidyverse)
library(httr)

# Function to download EIA-861 data for a specific year
download_eia861 <- function(year, output_dir = "data/eia861") {

  # Create output directory
  dir.create(output_dir, recursive = TRUE, showWarnings = FALSE)

  # EIA-861 ZIP file URL
  base_url <- "https://www.eia.gov/electricity/data/eia861/archive/zip"
  zip_filename <- paste0("f861", year, ".zip")
  file_url <- paste0(base_url, "/", zip_filename)

  # Download path
  download_path <- file.path(output_dir, zip_filename)

  cat("Downloading EIA-861 data for year", year, "...\n")
  cat("URL:", file_url, "\n")

  # Download ZIP file (use mode='wb' for binary)
  tryCatch({
    download.file(file_url, destfile = download_path, mode = "wb")
    cat("Download complete.\n")
  }, error = function(e) {
    cat("Error downloading file:", e$message, "\n")
    return(NULL)
  })

  # Unzip
  cat("Extracting ZIP archive...\n")
  unzip(download_path, exdir = file.path(output_dir, paste0("eia861_", year)))

  cat("Files extracted to:", file.path(output_dir, paste0("eia861_", year)), "\n")

  return(file.path(output_dir, paste0("eia861_", year)))
}

# Example usage
# eia861_2023_dir <- download_eia861(2023)
```

#### Example 2: Read Reliability and Service Territory Data

```r
library(tidyverse)

# Function to read EIA-861 reliability data
read_eia861_reliability <- function(year, data_dir) {

  # Construct file path
  reliability_file <- file.path(
    data_dir,
    paste0("eia861_", year),
    paste0("Reliability_", year, ".csv")
  )

  # Check if file exists
  if (!file.exists(reliability_file)) {
    # Try alternative naming conventions
    possible_names <- c(
      paste0("reliability", year, ".csv"),
      "Reliability.csv",
      paste0("Rel_", year, ".csv")
    )

    for (name in possible_names) {
      test_path <- file.path(data_dir, paste0("eia861_", year), name)
      if (file.exists(test_path)) {
        reliability_file <- test_path
        break
      }
    }
  }

  cat("Reading reliability data from:", reliability_file, "\n")

  # Read CSV
  reliability_data <- read_csv(
    reliability_file,
    col_types = cols(.default = "c"),  # Read all as character initially
    show_col_types = FALSE
  ) %>%
    # Standardize column names (case-insensitive)
    rename_with(tolower) %>%

    # Convert numeric fields
    mutate(
      utility_number = as.integer(utility_number),
      report_year = as.integer(report_year),
      saifi = as.numeric(saifi),
      saidi = as.numeric(saidi),
      saifi_with_med = as.numeric(saifi_with_med),
      saidi_with_med = as.numeric(saidi_with_med),
      saifi_without_med = as.numeric(saifi_without_med),
      saidi_without_med = as.numeric(saidi_without_med)
    )

  cat("Loaded", nrow(reliability_data), "utility reliability records.\n")

  return(reliability_data)
}

# Function to read service territory data
read_eia861_service_territory <- function(year, data_dir) {

  # Construct file path
  territory_file <- file.path(
    data_dir,
    paste0("eia861_", year),
    paste0("Service_Territory_", year, ".csv")
  )

  # Check alternative naming
  if (!file.exists(territory_file)) {
    possible_names <- c(
      paste0("service_territory", year, ".csv"),
      "Service_Territory.csv",
      paste0("Serv_Terr_", year, ".csv")
    )

    for (name in possible_names) {
      test_path <- file.path(data_dir, paste0("eia861_", year), name)
      if (file.exists(test_path)) {
        territory_file <- test_path
        break
      }
    }
  }

  cat("Reading service territory data from:", territory_file, "\n")

  # Read CSV
  territory_data <- read_csv(
    territory_file,
    col_types = cols(.default = "c"),
    show_col_types = FALSE
  ) %>%
    rename_with(tolower) %>%
    mutate(
      utility_number = as.integer(utility_number),
      state = str_to_upper(state),
      county = str_trim(county)
    )

  cat("Loaded", nrow(territory_data), "utility-county records.\n")

  return(territory_data)
}

# Example usage
# reliability_2023 <- read_eia861_reliability(2023, "data/eia861")
# territory_2023 <- read_eia861_service_territory(2023, "data/eia861")
```

#### Example 3: Link Utilities to Counties and Create County-Level Reliability Estimates

```r
library(tidyverse)

# Function to add county FIPS codes using tigris package
add_county_fips <- function(territory_data) {

  library(tigris)

  # Get county FIPS crosswalk from Census
  # tigris provides county geometries with FIPS codes
  counties <- counties(cb = TRUE, year = 2020) %>%
    st_drop_geometry() %>%
    select(
      state_abbr = STUSPS,
      county_name = NAME,
      county_fips = GEOID
    ) %>%
    mutate(
      county_name = str_to_upper(county_name),
      county_name = str_remove(county_name, " COUNTY")
    )

  # Clean EIA-861 county names for matching
  territory_with_fips <- territory_data %>%
    mutate(
      county_clean = str_to_upper(county),
      county_clean = str_remove(county_clean, " COUNTY"),
      county_clean = str_remove(county_clean, " PARISH"),  # Louisiana
      county_clean = str_trim(county_clean)
    ) %>%

    # Join with FIPS codes
    left_join(
      counties,
      by = c("state" = "state_abbr", "county_clean" = "county_name")
    )

  # Check match rate
  match_rate <- mean(!is.na(territory_with_fips$county_fips)) * 100
  cat("County FIPS match rate:", round(match_rate, 1), "%\n")

  if (match_rate < 95) {
    warning("Low match rate. Check county name standardization.")
  }

  return(territory_with_fips)
}

# Function to create county-level reliability estimates
create_county_reliability <- function(reliability_data, territory_data) {

  # Add FIPS codes to territory data
  territory_fips <- add_county_fips(territory_data)

  # Join reliability metrics to service territory
  utility_county_reliability <- territory_fips %>%
    inner_join(
      reliability_data %>%
        select(
          utility_number,
          saifi,
          saidi,
          saifi_without_med,
          saidi_without_med,
          ieee_standard_used
        ),
      by = "utility_number"
    )

  # Strategy 1: Simple average (unweighted)
  # Assumes equal importance of all utilities in county
  county_reliability_simple <- utility_county_reliability %>%
    group_by(county_fips, state) %>%
    summarise(
      n_utilities = n_distinct(utility_number),

      # Average across utilities serving the county
      saifi_mean = mean(saifi, na.rm = TRUE),
      saidi_mean = mean(saidi, na.rm = TRUE),
      saifi_without_med_mean = mean(saifi_without_med, na.rm = TRUE),
      saidi_without_med_mean = mean(saidi_without_med, na.rm = TRUE),

      # Min and max (best and worst utility)
      saifi_min = min(saifi, na.rm = TRUE),
      saifi_max = max(saifi, na.rm = TRUE),
      saidi_min = min(saidi, na.rm = TRUE),
      saidi_max = max(saidi, na.rm = TRUE),

      # IEEE standard usage
      pct_ieee_utilities = mean(ieee_standard_used == "Yes", na.rm = TRUE) * 100,

      .groups = "drop"
    )

  return(county_reliability_simple)
}

# Example usage
# county_reliability <- create_county_reliability(
#   reliability_2023,
#   territory_2023
# )
#
# # Summary statistics
# summary(county_reliability$saidi_mean)
#
# # Counties with worst reliability
# county_reliability %>%
#   arrange(desc(saidi_mean)) %>%
#   head(20)
```

#### Example 4: Calculate Health Vulnerability Scores Based on Electricity Reliability

```r
library(tidyverse)

# Function to create electricity reliability health vulnerability index
calculate_reliability_health_risk <- function(county_reliability) {

  # Define thresholds based on national averages
  # National median SAIFI: ~1.2 interruptions/customer/year
  # National median SAIDI: ~120 minutes/customer/year

  health_risk <- county_reliability %>%
    mutate(
      # Frequency risk (more frequent outages = higher risk)
      saifi_risk_score = case_when(
        saifi_mean < 1.0 ~ 1,  # Low risk
        saifi_mean < 1.5 ~ 2,  # Moderate risk
        saifi_mean < 2.0 ~ 3,  # High risk
        saifi_mean >= 2.0 ~ 4, # Very high risk
        TRUE ~ NA_real_
      ),

      # Duration risk (longer outages = higher risk)
      saidi_risk_score = case_when(
        saidi_mean < 100 ~ 1,   # Low risk
        saidi_mean < 150 ~ 2,   # Moderate risk
        saidi_mean < 250 ~ 3,   # High risk
        saidi_mean >= 250 ~ 4,  # Very high risk
        TRUE ~ NA_real_
      ),

      # Combined reliability risk (average of frequency + duration)
      combined_reliability_risk = (saifi_risk_score + saidi_risk_score) / 2,

      # Risk categories
      risk_category = case_when(
        combined_reliability_risk < 1.5 ~ "Low",
        combined_reliability_risk < 2.5 ~ "Moderate",
        combined_reliability_risk < 3.5 ~ "High",
        combined_reliability_risk >= 3.5 ~ "Very High",
        TRUE ~ "Unknown"
      ),

      # Medical device dependent population at risk flag
      # High SAIDI (>120 min) exceeds typical battery backup for oxygen concentrators
      medical_device_risk_flag = if_else(saidi_mean > 120, 1, 0),

      # Heat/cold vulnerability flag
      # High SAIFI + high SAIDI = frequent AND long outages
      hvac_vulnerability_flag = if_else(
        saifi_mean > 1.5 & saidi_mean > 150,
        1,
        0
      )
    )

  return(health_risk)
}

# Function to merge with population data for impact estimates
estimate_population_at_risk <- function(health_risk, population_data) {

  # population_data should have: county_fips, total_pop, elderly_pop,
  # poverty_pop, medical_device_users

  risk_population <- health_risk %>%
    left_join(population_data, by = "county_fips") %>%
    mutate(
      # Estimate population affected by unreliable power
      # Assume high-risk counties affect elderly + poverty populations more
      elderly_at_risk = if_else(
        risk_category %in% c("High", "Very High"),
        elderly_pop,
        0
      ),

      # Medical device users at extreme risk in high SAIDI counties
      medical_device_extreme_risk = if_else(
        medical_device_risk_flag == 1,
        medical_device_users,
        0
      ),

      # Total vulnerable population estimate
      total_vulnerable = elderly_at_risk + medical_device_extreme_risk
    )

  return(risk_population)
}

# Example usage
# health_risk <- calculate_reliability_health_risk(county_reliability)
#
# # Summary of risk distribution
# health_risk %>%
#   count(risk_category) %>%
#   mutate(pct = n / sum(n) * 100)
#
# # Top 20 highest risk counties
# health_risk %>%
#   arrange(desc(combined_reliability_risk)) %>%
#   select(county_fips, state, n_utilities, saifi_mean, saidi_mean,
#          combined_reliability_risk, risk_category) %>%
#   head(20)
```

---

## APPENDIX A: CROSS-SOURCE INTEGRATION STRATEGIES {#appendix-a-cross-source-integration}

### A.1 Creating Unified County-Level Dataset

To integrate all three data sources into a comprehensive county-level health observatory dataset:

```r
library(tidyverse)

# Function to merge LEAD, FCC BDC, and EIA-861 data at county level
integrate_county_data <- function(lead_counties,
                                   fcc_counties,
                                   eia_counties) {

  # Ensure all have standardized county FIPS (5-digit string)
  lead_std <- lead_counties %>%
    mutate(county_fips = str_pad(county_fips, 5, "left", "0"))

  fcc_std <- fcc_counties %>%
    mutate(county_fips = str_pad(county_fips, 5, "left", "0"))

  eia_std <- eia_counties %>%
    mutate(county_fips = str_pad(county_fips, 5, "left", "0"))

  # Full join to retain all counties
  integrated <- lead_std %>%
    full_join(fcc_std, by = "county_fips", suffix = c("_lead", "_fcc")) %>%
    full_join(eia_std, by = "county_fips")

  # Add composite vulnerability scores
  integrated <- integrated %>%
    mutate(
      # Energy + broadband + reliability composite
      infrastructure_vulnerability_index = (
        scale(pct_high_burden)[,1] +          # Energy burden (from LEAD)
        scale(100 - telehealth_ready)[,1] +   # Broadband gap (from FCC)
        scale(combined_reliability_risk)[,1]  # Power reliability (from EIA)
      ) / 3
    )

  return(integrated)
}
```

### A.2 Recommended Analysis Workflow

1. **Download all three datasets** (LEAD 2022, FCC BDC June 2024, EIA-861 2023)
2. **Process to county level** using code examples above
3. **Standardize county FIPS codes** (5-digit strings with leading zeros)
4. **Merge datasets** using county FIPS as key
5. **Add health outcomes data** (CDC mortality, hospitalization rates, etc.)
6. **Conduct spatial analysis** (mapping, clustering, regression models)

### A.3 Key Variables for Health Outcomes Research

**From LEAD Tool:**
- `pct_households_high_burden`: % households with energy burden >6%
- `mean_energy_cost_low_income`: Average annual energy cost for <80% AMI households
- `pct_owner_occupied`: Ownership rate (renters more vulnerable)

**From FCC BDC:**
- `telehealth_ready`: % locations with ≥25/3 Mbps
- `advanced_broadband`: % locations with ≥100/20 Mbps
- `n_providers`: Provider competition (more = better)
- `pct_fiber`: Fiber availability (most reliable technology)

**From EIA-861:**
- `saidi_mean`: Average minutes of outages per year
- `saifi_mean`: Average number of outages per year
- `medical_device_risk_flag`: SAIDI >120 minutes (exceeds battery backup)

---

## APPENDIX B: HEALTH RELEVANCE SUMMARY {#appendix-b-health-relevance-summary}

### B.1 Conceptual Model: Infrastructure and Health

```
Energy Burden (LEAD) ──┐
                       ├──> Heat/Cold Stress ──┐
Electricity Reliability ┘                      │
(EIA-861)                                      ├──> Mortality
                                               │    Morbidity
Broadband Access (FCC) ────> Telehealth Access ┘    Health Disparities
                              Health Information
                              Social Isolation
```

### B.2 Priority Vulnerable Populations

1. **Elderly (65+)**
   - High energy burden (fixed incomes, older homes)
   - Heat/cold vulnerability (impaired thermoregulation)
   - Medical device dependence (oxygen, CPAP)
   - Digital divide (lower broadband adoption)

2. **Low-Income Households (<200% FPL)**
   - Energy insecurity (choice between heat and food)
   - Limited broadband access (affordability)
   - Refrigerated medication access (insulin rationing)
   - Residential instability

3. **Rural Residents**
   - Lower broadband availability and speeds
   - Higher electricity reliability issues (longer distribution lines)
   - Greater distance to healthcare facilities (telehealth critical)
   - Higher energy costs (propane, heating oil)

4. **Individuals with Chronic Illnesses**
   - Medical device dependence (dialysis, oxygen, ventilators)
   - Refrigerated medication needs (biologics, insulin)
   - Frequent healthcare visits (telehealth beneficial)
   - Heat/cold sensitivity (cardiovascular, respiratory disease)

### B.3 Hypotheses for Testing

1. **H1:** Counties with high energy burden (>25% households with >6% burden) have higher age-adjusted cardiovascular mortality rates

2. **H2:** Counties with low broadband access (<50% locations with ≥25/3 Mbps) have lower telehealth utilization and worse diabetes management outcomes

3. **H3:** Counties with high electricity unreliability (SAIDI >200 minutes/year) have higher emergency department visits for heat-related illness during summer months

4. **H4:** The combination of high energy burden + low broadband access + high electricity unreliability creates a "triple burden" associated with excess all-cause mortality

5. **H5:** Rural counties experience compounding effects of all three infrastructure vulnerabilities compared to urban counties

---

## REFERENCES

### LEAD Tool

1. U.S. Department of Energy. (2024). *Low-Income Energy Affordability Data (LEAD) Tool Methodology*. Retrieved from https://www.energy.gov/sites/default/files/2024-12/lead-methodology_122024.pdf

2. OEDI: Open Energy Data Initiative. (2024). *Low-Income Energy Affordability Data - LEAD Tool - 2022 Update*. Retrieved from https://data.openei.org/submissions/6219

3. Hernández, D., Jiang, Y., Carrión, D., Phillips, D., & Aratani, Y. (2021). Exploring the Nexus of Energy Burden, Social Capital, and Environmental Quality in Shaping Health in US Counties. *International Journal of Environmental Research and Public Health*, 18(2), 620. https://doi.org/10.3390/ijerph18020620

4. Hernández, D. (2016). Understanding 'energy insecurity' and why it matters to health. *Social Science & Medicine*, 167, 1-10. https://doi.org/10.1016/j.socscimed.2016.08.029

### FCC Broadband Data Collection

5. Federal Communications Commission. (2024). *Broadband Data Collection*. Retrieved from https://www.fcc.gov/BroadbandData

6. Federal Communications Commission. (2024). *FCC Broadband Data Collection – June 2024 Update*. ArcGIS Living Atlas. Retrieved from https://www.arcgis.com/home/item.html?id=22ca3a8bb2ff46c1983fb45414157b08

7. Nouri, S., Khoong, E. C., Lyles, C. R., & Karliner, L. (2020). Addressing Equity in Telemedicine for Chronic Disease Management During the Covid-19 Pandemic. *NEJM Catalyst Innovations in Care Delivery*, 1(3). https://doi.org/10.1056/CAT.20.0123

8. Benda, N. C., Veinot, T. C., Sieck, C. J., & Ancker, J. S. (2020). Broadband Internet Access Is a Social Determinant of Health! *American Journal of Public Health*, 110(8), 1123-1125. https://doi.org/10.2105/AJPH.2020.305784

### EIA Form 861 Electricity Reliability

9. U.S. Energy Information Administration. (2024). *Annual Electric Power Industry Report, Form EIA-861 detailed data files*. Retrieved from https://www.eia.gov/electricity/data/eia861/

10. U.S. Energy Information Administration. (2018). Average U.S. electricity customer interruptions totaled nearly 8 hours in 2017. *Today in Energy*. Retrieved from https://www.eia.gov/todayinenergy/detail.php?id=37652

11. Casey, J. A., Fukurai, M., Hernández, D., Balsari, S., & Kiang, M. V. (2020). Power Outages and Community Health: a Narrative Review. *Current Environmental Health Reports*, 7, 371-383. https://doi.org/10.1007/s40572-020-00295-0

12. Martínez, P. A., Garcia Lorenzo, B., & Comfort, C. (2021). Keeping the power on to home medical devices. *Journal of Clinical and Translational Research*, 7(3), 387-392. PMCID: PMC7347141

13. Kaye, L., Zhou, Z., Dugan, A., Allen, J. G., & Spengler, J. D. (2021). Who's at Risk When the Power Goes Out? The At-home Electricity-Dependent Population in the United States, 2012. *Journal of Public Health Management and Practice*, 27(Suppl 6), S82-S90. https://doi.org/10.1097/PHH.0000000000001382

### Cross-Cutting Health and Infrastructure

14. Health Affairs. (2024). Energy Insecurity Indicators Associated With Increased Odds Of Respiratory, Mental Health, And Cardiovascular Conditions. *Health Affairs*, 43(4). https://doi.org/10.1377/hlthaff.2023.01052

15. Hernández, D., & Siegel, E. (2019). Energy Insecurity and Its Ill Health Effects: A Community Perspective on the Energy-Health Nexus in New York City. *Energy Research & Social Science*, 47, 78-83. https://doi.org/10.1016/j.erss.2018.08.011

16. Liddell, C., & Morris, C. (2010). Fuel poverty and human health: A review of recent evidence. *Energy Policy*, 38(6), 2987-2997. https://doi.org/10.1016/j.enpol.2010.01.037

### Data Processing and Methods

17. Catalyst Cooperative. (2024). *PUDL: The Public Utility Data Liberation Project*. Retrieved from https://catalyst.coop/pudl/

18. Walker, K. (2024). *Analyzing US Census Data: Methods, Maps, and Models in R*. CRC Press. https://walker-data.com/census-r/

19. IMMM-SFA. (2020). *Electricity Entity Boundaries: Nested boundaries for electricity entities using the EIA-861 dataset*. GitHub repository. https://github.com/IMMM-SFA/electricity_entity_boundaries

---

**END OF COMPREHENSIVE TECHNICAL DOCUMENTATION**

**Document Maintenance:**
- This documentation should be updated when new data releases occur (LEAD Tool every ~4 years, FCC BDC biannually, EIA-861 annually)
- Code examples should be tested with each new data release to verify file structures and field names remain consistent
- Health relevance sections should be updated as new research evidence emerges

**Contact for Questions:**
- LEAD Tool: LEAD.Tool@hq.doe.gov
- FCC BDC: BDC Help Center (https://help.bdc.fcc.gov/hc/en-us)
- EIA-861: EIA Information Center (infoctr@eia.gov)
