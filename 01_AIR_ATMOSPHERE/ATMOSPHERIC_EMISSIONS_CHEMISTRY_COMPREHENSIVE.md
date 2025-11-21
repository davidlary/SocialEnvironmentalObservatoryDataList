# ATMOSPHERIC EMISSIONS, CHEMISTRY, GREENHOUSE GASES & AEROSOLS
## Comprehensive County-Level Data Sources

**Last Updated**: November 21, 2025
**Research Focus**: County-level chemical emissions, atmospheric chemistry, greenhouse gases, and aerosol composition data
**Geographic Coverage**: 3,143 US Counties
**Status**: Comprehensive research completed

**2025 Regulatory Updates:**
- SO2 secondary NAAQS: New 10 ppb annual standard (effective Jan 27, 2025)
- PM2.5 primary NAAQS: Under reconsideration (2024 rule set 9.0 μg/m³; decision Feb 2026)

---

## TABLE OF CONTENTS

1. [Executive Summary](#executive-summary)
2. [EPA National Emissions Inventory (NEI)](#epa-national-emissions-inventory-nei)
3. [Continuous Emissions Monitoring System (CEMS)](#continuous-emissions-monitoring-system-cems)
4. [Aerosol Composition & Particulate Matter](#aerosol-composition--particulate-matter)
5. [Mobile Source Emissions](#mobile-source-emissions)
6. [Agricultural Emissions](#agricultural-emissions)
7. [Biogenic & Natural Emissions](#biogenic--natural-emissions)
8. [Satellite-Based Atmospheric Data](#satellite-based-atmospheric-data)
9. [Already Documented Sources](#already-documented-sources)
10. [Not Available at County Level](#not-available-at-county-level)
11. [Detailed Source Documentation](#detailed-source-documentation)
12. [Data Access Methods](#data-access-methods)
13. [Priority Variables for Collection](#priority-variables-for-collection)
14. [Quick Reference](#quick-reference)

---

## EXECUTIVE SUMMARY

This report catalogs county-level data sources for atmospheric emissions, chemical composition, greenhouse gases, and aerosols in the United States. The focus is on the most respected sources with the longest time ranges.

### Key Findings:

**CRITERIA AIR POLLUTANTS (1 primary source):**
- **EPA National Emissions Inventory (NEI)** - THE definitive source
  - Coverage: All 3,143 counties
  - Years: 1990, 1996, 1999, 2002, 2005, 2008, 2011, 2014, 2017, 2020 (triennial)
  - Variables: PM2.5, PM10, SO2, NOx, VOCs, CO, NH3, lead (100+ subcategories)
  - Sources: Point, area, mobile (on-road, non-road), fires, biogenic, dust
  - Access: Free bulk download, web query tool
  - **Most comprehensive emissions database**

**GREENHOUSE GASES (4 sources beyond GHGRP):**
- EPA GHGRP (already documented) - Facility-level, 2010-present
- **VULCAN Fossil Fuel CO2 Emissions** - High-resolution 2002-2019
- **EPA Power Sector CEMS** - Hourly CO2/CH4 from power plants, 1995-present
- Agricultural GHG (livestock CH4, soil N2O) - Modeled county estimates
- Landfill CH4 - GHGRP + EPA LMOP

**CONTINUOUS EMISSIONS MONITORING (1 source):**
- **EPA CEMS/AMPD** - Hourly data from power plants
  - Coverage: ~1,700 power plants (aggregable to county)
  - Years: 1995-present (30-year time series!)
  - Variables: SO2, NOx, CO2, heat input, gross load
  - Frequency: Hourly measurements
  - **Longest high-frequency emissions time series available**

**AEROSOLS & PM COMPOSITION (3 networks):**
- **IMPROVE Network** (1988-present) - Black carbon, organic carbon, sulfates, nitrates, crustal elements
- **CSN (Chemical Speciation Network)** (2000-present) - Urban PM2.5 speciation
- **CASTNET** (1987-present) - Rural atmospheric deposition chemistry

**MOBILE SOURCE EMISSIONS (1 source):**
- **EPA MOVES Model** - County-level on-road emissions
  - Years: 1990-2060 (historical + projections)
  - Variables: PM2.5, PM10, SO2, NOx, VOCs, CO, NH3, air toxics
  - By vehicle type, road type, fuel type

**BIOGENIC & WILDFIRE (2 sources):**
- **NEI Biogenic Emissions** - Isoprene, monoterpenes from vegetation
- **NEI Wildfire Emissions** - PM2.5, CO, NOx, VOCs by fire event
- **NIFC Fire Data** - Wildfire perimeters and locations

**AGRICULTURAL EMISSIONS (2 sources):**
- **NEI Agricultural Sector** - NH3, PM2.5, NOx from farming
- **EPA Agricultural CH4/N2O** - Livestock and soil emissions (modeled)

**SATELLITE DATA (4 instruments - gridded, aggregable to county):**
- **OMI (2004-present)** - NO2, SO2, HCHO columns
- **TROPOMI (2018-present)** - NO2, SO2, CH4, CO, HCHO columns (high resolution)
- **MOPITT (2000-present)** - CO columns
- **MODIS AOD (2000-present)** - Aerosol optical depth

### Data Quality Assessment:

- ✅ **Excellent (longest time series, most respected):**
  - EPA National Emissions Inventory (1990-present)
  - EPA CEMS/AMPD (1995-present, hourly)
  - IMPROVE Network (1988-present)
  - CASTNET (1987-present)

- ⚠️ **Good but shorter time range:**
  - CSN (2000-present)
  - TROPOMI (2018-present, highest spatial resolution)
  - VULCAN (2002-2019)

- ⚠️ **Model-based:**
  - EPA MOVES (uses activity data + emission factors)
  - Agricultural GHG (uses livestock populations + emission factors)
  - Biogenic VOCs (MEGAN model)

---

## EPA NATIONAL EMISSIONS INVENTORY (NEI)

### Source 1: EPA National Emissions Inventory

**Official Name**: National Emissions Inventory (NEI)
**Agency**: U.S. Environmental Protection Agency (EPA), Office of Air Quality Planning and Standards
**Status**: ✅ PRIMARY COMPREHENSIVE SOURCE FOR CRITERIA & HAP EMISSIONS

#### Geographic & Temporal Coverage

- **Geographic**: All 3,143 US counties + territories
- **Years**: 1990 (baseline), then 1996, 1999, 2002, 2005, 2008, 2011, 2014, 2017, 2020
- **Frequency**: Triennial (every 3 years)
- **Next Release**: NEI 2023 expected 2025-2026
- **Update Schedule**: Released ~2 years after inventory year

#### Pollutants Covered (100+ variables)

**Criteria Air Pollutants (7):**
1. **PM2.5** (Fine Particulate Matter, ≤2.5 micrometers)
2. **PM10** (Particulate Matter, ≤10 micrometers)
3. **SO2** (Sulfur Dioxide)
4. **NOx** (Nitrogen Oxides)
5. **VOC** (Volatile Organic Compounds)
6. **CO** (Carbon Monoxide)
7. **NH3** (Ammonia)
8. **Lead** (Pb)

**Hazardous Air Pollutants (HAPs) - 187 pollutants including:**
- Benzene, toluene, xylene
- Formaldehyde, acetaldehyde
- 1,3-butadiene
- Polycyclic aromatic hydrocarbons (PAHs)
- Heavy metals (mercury, arsenic, chromium, nickel, etc.)
- Chlorinated solvents
- Diesel particulate matter

**PM2.5 Species (detailed composition):**
- Primary PM2.5 (directly emitted)
- SO4 (sulfate) - precursor for secondary PM2.5
- NOx - precursor for secondary PM2.5
- NH3 - precursor for secondary PM2.5
- VOC - precursor for secondary organic aerosols

### 📋 COMPLETE NEI POLLUTANT CATALOG (TIER 2)

**For the complete catalog of all 200+ NEI pollutant codes including criteria pollutants, hazardous air pollutants (HAPs), PM2.5 species, and greenhouse gases, see:**

**[EPA_NEI_COMPLETE_POLLUTANT_CODES.md](EPA_NEI_COMPLETE_POLLUTANT_CODES.md)**

This companion Tier 2 catalog provides:
- All 200+ NEI pollutant codes with descriptions and units
- Organized by category (criteria, HAPs, PM species, GHGs)
- CAS numbers for chemical pollutants
- Source sector applicability
- Reporting requirements and methodologies
- SCC (Source Classification Code) linkages

**Use this document (Tier 1)** for NEI system overview, data access, and priority pollutants.
**Use EPA_NEI_COMPLETE_POLLUTANT_CODES.md (Tier 2)** to look up specific pollutant codes or browse the complete list.

#### Source Categories

**Point Sources:**
- Large industrial facilities (power plants, refineries, chemical plants, etc.)
- ~26,000 point sources nationally
- Facility-level emissions with lat/lon

**Area Sources:**
- Smaller distributed sources aggregated to county
- Examples: residential wood combustion, commercial cooking, gas stations, dry cleaners, architectural coatings
- ~100 area source categories

**On-Road Mobile Sources:**
- Cars, trucks, motorcycles
- By vehicle type, fuel type, road type
- County-level vehicle miles traveled (VMT) based

**Non-Road Mobile Sources:**
- Construction equipment
- Agricultural equipment
- Lawn & garden equipment
- Locomotives
- Commercial marine vessels
- Aircraft (ground support operations)
- Recreational vehicles (ATVs, snowmobiles, etc.)

**Fires:**
- Wildland fires (wildfires)
- Prescribed burns
- Agricultural fires
- Event-specific emissions by fire location

**Biogenic Sources:**
- VOC emissions from vegetation (isoprene, monoterpenes)
- Soil NOx emissions
- Modeled using BEIS (Biogenic Emission Inventory System)

**Fugitive Dust:**
- Paved road dust
- Unpaved road dust
- Construction dust
- Agricultural tilling dust
- Wind erosion

#### Variables Available (per county per pollutant)

| Variable | Description | Units |
|----------|-------------|-------|
| Total Emissions | County total across all sources | Tons/year |
| Point Source Emissions | From large facilities | Tons/year |
| Area Source Emissions | From distributed sources | Tons/year |
| On-Road Mobile | From cars, trucks | Tons/year |
| Non-Road Mobile | From equipment, etc. | Tons/year |
| Fires | From wildfires, prescribed burns | Tons/year |
| Biogenic | From vegetation, soils | Tons/year |
| Fugitive Dust | From roads, construction, wind | Tons/year |

**Plus detailed subcategories:**
- Point sources: Emissions by SCC (Source Classification Code) - facility-level
- Area sources: Emissions by SCC - county-level
- Mobile sources: Emissions by vehicle type, fuel type, road type
- Fires: Emissions by fire event

#### Access Methods

**NEI Data Retrieval Tool (Web Interface):**
- URL: https://www.epa.gov/air-emissions-inventories/national-emissions-inventory-nei-data
- Interactive query by county, pollutant, year, source category
- Export to Excel, CSV

**Bulk Download:**
- URL: https://gaftp.epa.gov/Air/emissions/
- FTP server with complete NEI datasets
- Format: Large CSV files, SQLite databases
- Files organized by year (e.g., 2020v1/)

**Files Available:**
- `county_emissions_<year>.csv` - County totals by pollutant
- `point_sources_<year>.csv` - Facility-level point source emissions
- `area_sources_<year>.csv` - County-level area source emissions
- `mobile_sources_<year>.csv` - County-level mobile emissions
- `fires_<year>.csv` - Fire event emissions
- Supporting documentation PDFs

**API Access:**
- No official API currently
- Data can be loaded into databases for custom queries

#### Data Format

**County-Level Summary File Structure:**
```
state_code, county_code, state_name, county_name, pollutant_code, pollutant_desc,
year, total_emissions_tons, point_tons, area_tons, onroad_tons, nonroad_tons,
fires_tons, biogenic_tons
```

**Point Source File Structure:**
```
facility_id, facility_name, latitude, longitude, state_code, county_code,
SCC, SCC_description, pollutant_code, emissions_tons_per_year, emission_type,
unit_id, process_id, ...
```

#### Data Quality & Methodology

**Data Sources:**
- State/Local/Tribal air agency reports (primary)
- EPA models (mobile sources, biogenic)
- CEMS for power plants (SO2, NOx from continuous monitors)
- Facility-specific reports
- TRI for certain HAPs
- Activity data (VMT, fuel sales, population, agricultural statistics)

**Quality Assurance:**
- EPA reviews and validates state submissions
- Comparisons to ambient monitoring data
- Trend analysis for reasonableness
- Peer review for major methodological changes

**Uncertainty:**
- Point sources: Low uncertainty (reported data)
- Mobile sources: Moderate uncertainty (model-based)
- Area sources: Higher uncertainty (surrogate-based estimates)
- Fires: Moderate uncertainty (satellite detection + emission factors)
- Biogenic: Moderate uncertainty (model-based)

#### Comparison to Other Sources

**vs. TRI (Toxic Release Inventory):**
- TRI: ~800 chemicals, facility-level, 1987-present
- NEI: Includes TRI air releases PLUS criteria pollutants and many more sources
- NEI has broader coverage (mobile, area, fires)

**vs. GHGRP (Greenhouse Gas Reporting Program):**
- GHGRP: CO2, CH4, N2O, fluorinated gases from large facilities
- NEI: Criteria pollutants and HAPs (not comprehensive GHGs)
- Some overlap in facilities; NEI focuses on air quality pollutants

**Unique Value of NEI:**
- Only comprehensive county-level emissions inventory for criteria pollutants
- Includes ALL source sectors (not just facilities)
- Long time series (1990-present)
- Standardized methodology across states
- Basis for air quality modeling and policy analysis

#### Limitations

- **Triennial**: Not annual (except for certain sectors)
- **2-year lag**: Data released ~2 years after inventory year
- **Model-based estimates**: Mobile, biogenic, some area sources
- **No direct CO2**: Focus on air quality pollutants, not climate pollutants (see CEMS for CO2)
- **County aggregation**: Some sources averaged/apportioned to county from larger geographic areas

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Gold standard for US emissions inventory, most respected source

---

## CONTINUOUS EMISSIONS MONITORING SYSTEM (CEMS)

### Source 2: EPA Clean Air Markets Program Data (CEMS/AMPD)

**Official Name**: Air Markets Program Data (AMPD) / Continuous Emissions Monitoring System (CEMS)
**Agency**: U.S. Environmental Protection Agency (EPA), Clean Air Markets Division
**Status**: ✅ LONGEST HIGH-FREQUENCY EMISSIONS TIME SERIES (1995-PRESENT, HOURLY!)

#### Geographic & Temporal Coverage

- **Geographic**: ~1,700 power plants (~5,000 individual units) across US
- **Facilities**: Coal, natural gas, oil-fired electricity generating units (EGUs)
- **Years**: 1995-present (30-year continuous time series!)
- **Frequency**: **HOURLY** measurements (8,760 hours/year per unit)
- **Update**: Data uploaded monthly (current year preliminary, finalized annually)
- **Aggregation**: Facility locations → county-level aggregation

#### Variables Available

**Emissions (hourly):**

| Variable | Description | Units |
|----------|-------------|-------|
| SO2 | Sulfur Dioxide | Pounds/hour, tons/year |
| NOx | Nitrogen Oxides | Pounds/hour, tons/year |
| CO2 | Carbon Dioxide | Short tons/hour, metric tons/year |
| Heat Input | Fuel energy consumed | MMBtu/hour |
| Gross Load | Electricity generated | MWh |

**Additional Variables:**
- Operating time (hours)
- Unit type (boiler, combustion turbine, combined cycle)
- Fuel type (coal, natural gas, oil, other)
- SO2 controls (scrubbers)
- NOx controls (SCR, SNCR, low-NOx burners)
- Program participation (Acid Rain Program, CSAPR, RGGI, etc.)

**Derived Variables (calculable):**
- Emission rates (lbs/MMBtu, tons/MWh)
- Capacity factors
- Fuel efficiency
- Annual facility-level and county-level totals

#### Access Methods

**AMPD Custom Data Download:**
- URL: https://campd.epa.gov/
- Interactive query tool
- Select: facilities, time period, pollutants
- Export: CSV, Excel (limit ~1 million rows per query)

**Bulk Data Download:**
- URL: https://www.epa.gov/airmarkets/clean-air-markets-program-data-and-maps
- Bulk data files by year
- Format: Zipped CSV files
- Hourly data files: Large (gigabytes)
- Annual summary files: Manageable

**API Access:**
- CAMPD API (beta): https://api.epa.gov/easey/
- RESTful API
- Query by facility, date range, pollutant
- Free, no API key required
- JSON output

**Example API Query:**
```
https://api.epa.gov/easey/emissions-mgmt/apportioned/hourly?
beginDate=2023-01-01&endDate=2023-12-31&stateCode=OH&unitType=Boiler
```

#### Data Format

**Hourly Emissions File Structure:**
```
state, facility_name, facility_id, unit_id, date, hour,
operating_time, gross_load_mw, heat_input_mmbtu,
so2_mass_lbs, so2_rate_lbs_mmbtu,
nox_mass_lbs, nox_rate_lbs_mmbtu,
co2_mass_tons, co2_rate_tons_mmbtu
```

**Annual Summary (by facility):**
```
facility_id, facility_name, state, county, latitude, longitude,
year, operating_time_hours,
so2_tons, nox_tons, co2_short_tons, co2_metric_tonnes,
heat_input_mmbtu, gross_load_mwh
```

#### County-Level Aggregation

**Method:**
1. Download facility-level data with lat/lon or state/county
2. Assign facilities to county FIPS codes
3. Sum emissions across all facilities in each county
4. Calculate county totals by year, month, or hour

**R Code Example:**
```r
library(tidyverse)

# Read facility locations
facilities <- read_csv("facility_locations.csv") %>%
  select(facility_id, county_fips, state, county_name)

# Read annual emissions
emissions <- read_csv("ampd_annual_2023.csv") %>%
  select(facility_id, year, so2_tons, nox_tons, co2_metric_tonnes)

# Aggregate to county level
county_emissions <- emissions %>%
  left_join(facilities, by = "facility_id") %>%
  group_by(county_fips, state, county_name, year) %>%
  summarize(
    so2_tons = sum(so2_tons, na.rm = TRUE),
    nox_tons = sum(nox_tons, na.rm = TRUE),
    co2_metric_tonnes = sum(co2_metric_tonnes, na.rm = TRUE),
    facilities = n_distinct(facility_id),
    .groups = "drop"
  )
```

#### Data Quality

**Measurement Method:**
- Continuous Emissions Monitoring Systems (CEMS) installed at facilities
- Part 75 monitoring requirements (40 CFR Part 75)
- Quality-assured instrumental measurements
- Hourly averages of continuous readings
- Audited and certified quarterly

**Quality Assurance:**
- Relative Accuracy Test Audits (RATAs)
- Linearity checks
- Calibration error tests
- Data validation and quality flags
- Missing data substitution procedures (documented)

**Coverage:**
- Captures ~100% of emissions from EGUs (coal, gas, oil power plants)
- Does NOT include:
  - Industrial boilers (unless subject to programs)
  - Small generators
  - Mobile sources
  - Non-combustion sources

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Highest quality emissions data available; continuous instrumental measurement

#### Use Cases

**Air Quality Research:**
- SO2 and NOx trends over time (dramatic decreases due to Clean Air Act)
- Power plant contributions to PM2.5 formation (SO2 → sulfates, NOx → nitrates)
- Emission rate analysis

**Climate Analysis:**
- Power sector CO2 emissions by county
- Annual and hourly trends
- Fuel switching analysis (coal to gas)

**Environmental Justice:**
- Proximity of power plants to communities
- Emissions exposure by demographics

**Energy Policy:**
- Impacts of renewable energy growth on fossil emissions
- Evaluation of emission trading programs (Acid Rain Program, CSAPR)

#### Limitations

- **Power sector only**: Does not include transportation, industry (non-EGUs), agriculture
- **Large sources only**: EGUs >25 MW typically
- **Preliminary data**: Current year data is preliminary until finalized
- **No CH4**: Limited methane monitoring (some gas plants report, but not comprehensive)
- **Not all pollutants**: No PM2.5, VOCs, HAPs, NH3

#### Comparison to NEI

**CEMS Advantages:**
- Hourly resolution (vs. annual)
- 30-year time series (vs. triennial)
- Measured data (vs. modeled for some sources)
- Current data (vs. 2-year lag)

**NEI Advantages:**
- All pollutants (vs. SO2, NOx, CO2 only)
- All source sectors (vs. power plants only)
- Complete county coverage (vs. only counties with power plants)

**Complementary Use:**
- CEMS for high-resolution power sector analysis
- NEI for comprehensive multi-pollutant, multi-sector analysis
- CEMS data feeds into NEI point source estimates for EGUs

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Instrumental continuous monitoring, highest quality

---

## AEROSOL COMPOSITION & PARTICULATE MATTER

### Source 3: IMPROVE Network (Interagency Monitoring of Protected Visual Environments)

**Official Name**: IMPROVE (Interagency Monitoring of Protected Visual Environments) Network
**Agency**: Multiple agencies (EPA, NPS, FWS, FS, BLM, state agencies)
**Coordination**: UC Davis / Colorado State University
**Status**: ✅ LONGEST PM COMPOSITION MONITORING (1988-PRESENT)

#### Geographic & Temporal Coverage

- **Sites**: ~170 monitoring sites (primarily at national parks and wilderness areas)
- **Geographic**: Not all counties; rural/remote sites
- **Aggregation to County**: Sites can be assigned to county of location
- **Years**: 1988-present (37-year record!)
- **Frequency**: 24-hour samples every third day
- **Update**: Data released ~1 year after collection

#### Variables Measured (Aerosol Composition)

**PM2.5 and PM10 Mass:**
- Total PM2.5 (μg/m³)
- Total PM10 (μg/m³)

**PM2.5 Chemical Species (μg/m³):**

| Species | Description | Climate/Health Relevance |
|---------|-------------|-------------------------|
| **Elemental Carbon (EC)** | Black carbon, light-absorbing | Climate warming, respiratory |
| **Organic Carbon (OC)** | Carbonaceous aerosols | SOA, visibility, respiratory |
| **Sulfate (SO4)** | Ammonium sulfate | Secondary PM2.5 from SO2 |
| **Nitrate (NO3)** | Ammonium nitrate | Secondary PM2.5 from NOx |
| **Ammonium (NH4)** | Ammonium ion | Associated with SO4 and NO3 |
| **Soil (Crustal)** | Al, Si, Ca, Fe, Ti | Dust |
| **Sea Salt** | Na, Cl | Marine aerosols |
| **Trace Elements** | As, Br, Cd, Cr, Cu, Mn, Ni, Pb, V, Zn | Industrial, combustion |

**Coarse Mass (PM10-2.5) Species:**
- Soil/dust components
- Sea salt
- Large organic particles

#### Access Methods

**IMPROVE Data Portal:**
- URL: http://views.cira.colostate.edu/fed/QueryWizard/
- Interactive query wizard
- Select: sites, dates, species
- Export: CSV, Excel

**Data Guide:**
- URL: http://vista.cira.colostate.edu/Improve/improve-data/
- Comprehensive documentation
- Data quality flags explained

**FTP Download:**
- Bulk data files by year
- Site metadata with lat/lon and county information

#### Data Format

**Site Data File:**
```
site_code, site_name, latitude, longitude, state, county, elevation,
date, PM25_mass, EC, OC, SO4, NO3, NH4, soil, sea_salt,
Al, Si, Ca, Fe, Ti, Mn, [trace elements],
data_quality_flags
```

#### Data Quality

**Measurement Methods:**
- Gravimetric mass (filter weighing)
- Ion chromatography (SO4, NO3, Cl)
- Thermal-optical reflectance (EC, OC)
- X-ray fluorescence (elements)

**Quality Assurance:**
- Collocated samplers (precision checks)
- Performance audits
- Inter-laboratory comparisons
- Stringent QA/QC protocols

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Gold standard for PM composition, longest record

#### Limitations

- **Sparse Spatial Coverage**: ~170 sites, not all counties
- **Rural Focus**: Sites primarily at national parks/wilderness (not urban)
- **Every-third-day**: Not daily continuous (but long-term trends are robust)
- **1-year lag**: Data not real-time

#### Use Cases

- Long-term trends in black carbon, organic carbon, sulfates
- Source apportionment of PM2.5
- Visibility trends in national parks
- Climate-relevant aerosol species

---

### Source 4: Chemical Speciation Network (CSN)

**Official Name**: EPA Chemical Speciation Network (CSN)
**Agency**: U.S. Environmental Protection Agency
**Status**: ✅ URBAN PM2.5 COMPOSITION (2000-PRESENT)

#### Geographic & Temporal Coverage

- **Sites**: ~180 urban sites nationally
- **Geographic**: Major urban areas (aggregable to county)
- **Years**: 2000-present (24-year record)
- **Frequency**: 24-hour samples, 1-in-3 days or 1-in-6 days
- **Update**: Annual data releases

#### Variables Measured

**PM2.5 Chemical Composition (μg/m³):**
- PM2.5 mass (gravimetric)
- Elemental carbon (EC)
- Organic carbon (OC)
- Sulfate (SO4)
- Nitrate (NO3)
- Ammonium (NH4)
- Elements (by XRF)
- Ions (by ion chromatography)

**Similar to IMPROVE but:**
- Urban focus (IMPROVE = rural)
- Shorter record (2000 vs 1988)
- More frequent sampling at some sites

#### Access Methods

**EPA AQS (Air Quality System):**
- URL: https://www.epa.gov/aqs
- Air Quality System contains CSN data
- Query by site, pollutant, date
- API available

**EPA Pre-Generated Data Files:**
- URL: https://www.epa.gov/amtic/chemical-speciation-network-csn
- Annual data files
- CSV format

#### Data Quality

**Measurement Methods:**
- Multiple analysis methods (gravimetric, IC, thermal-optical, XRF)
- Collocated samplers
- National Performance Audits

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - High-quality urban PM2.5 composition data

---

### Source 5: CASTNET (Clean Air Status and Trends Network)

**Official Name**: Clean Air Status and Trends Network
**Agency**: EPA, managed by EPA Office of Atmospheric Programs
**Status**: ✅ LONGEST DEPOSITION CHEMISTRY RECORD (1987-PRESENT)

#### Geographic & Temporal Coverage

- **Sites**: ~90 rural sites
- **Years**: 1987-present (38-year record!)
- **Frequency**: Weekly samples
- **Focus**: Atmospheric deposition chemistry (wet and dry)

#### Variables Measured

**Ambient Air Concentrations:**
- Ozone (O3) - continuous
- Sulfate (SO4) - filter-based
- Nitrate (NO3) - filter-based
- Ammonium (NH4) - filter-based
- Sulfur dioxide (SO2) - continuous
- Nitric acid (HNO3) - denuder

**Wet Deposition (from National Atmospheric Deposition Program):**
- pH
- SO4, NO3, Cl, NH4 in precipitation

**Dry Deposition (estimated):**
- Inferred from air concentrations + deposition velocities

#### Access Methods

- URL: https://www.epa.gov/castnet
- Data portal with query tools
- CSV downloads

#### Unique Value

- Longest atmospheric chemistry monitoring in US
- Rural sites complement urban networks
- Critical for acid rain trends analysis
- Sulfate and nitrate trends (dramatic decreases)

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Longest atmospheric chemistry record in US

---

### Source 6: NADP (National Atmospheric Deposition Program)

**Official Name**: National Atmospheric Deposition Program (NADP)
**Agency**: Multi-agency program coordinated by University of Illinois
**Status**: ✅ LONGEST WET DEPOSITION RECORD (1978-PRESENT, 46+ YEARS!)

#### Overview

NADP operates the longest-running wet deposition monitoring network in North America. It includes multiple sub-networks measuring different aspects of atmospheric deposition.

#### Sub-Networks

**1. NTN (National Trends Network) - 1978-present:**
- **Years**: 1978-present (46-year record! LONGEST)
- **Sites**: ~250 active sites
- **Frequency**: Weekly precipitation samples
- **Variables**: pH, sulfate, nitrate, ammonium, chloride, calcium, magnesium, potassium, sodium, conductivity
- **Focus**: Wet deposition chemistry (acid rain)

**2. MDN (Mercury Deposition Network) - 1996-present:**
- **Years**: 1996-present (28-year record)
- **Sites**: ~100 sites
- **Frequency**: Weekly precipitation samples
- **Variables**: Total mercury in precipitation, mercury deposition (ng/m²)
- **Focus**: Mercury wet deposition

**3. AMoN (Ammonia Monitoring Network) - 2007-present:**
- **Years**: 2007-present (17-year record)
- **Sites**: ~100 sites
- **Frequency**: Bi-weekly passive samplers
- **Variables**: Ambient ammonia (NH3) concentration (μg/m³)
- **Focus**: Ammonia gas monitoring (complements NTN ammonium in precipitation)

**4. AIRMoN (Atmospheric Integrated Research Monitoring Network):**
- High-frequency precipitation chemistry (event-based sampling)
- Subset of sites for research

#### Geographic & Temporal Coverage

- **Geographic**: All 50 states + territories, ~250-300 total sites across networks
- **Site Assignment**: Sites assignable to county by location
- **Years**: 1978-present for NTN (LONGEST wet deposition record)
- **Update**: Data released annually, available within 1-2 years

#### Variables Available

**NTN Chemistry (per site, aggregable to county):**

| Variable | Description | Units |
|----------|-------------|-------|
| pH | Precipitation acidity | pH units |
| Sulfate (SO4) | Wet deposition | mg/L, kg/ha |
| Nitrate (NO3) | Wet deposition | mg/L, kg/ha |
| Ammonium (NH4) | Wet deposition | mg/L, kg/ha |
| Chloride (Cl) | Wet deposition | mg/L, kg/ha |
| Calcium (Ca) | Wet deposition | mg/L, kg/ha |
| Magnesium (Mg) | Wet deposition | mg/L, kg/ha |
| Potassium (K) | Wet deposition | mg/L, kg/ha |
| Sodium (Na) | Wet deposition | mg/L, kg/ha |
| Precipitation Amount | Weekly total | cm |
| Conductivity | Ionic strength | μS/cm |

**MDN Mercury:**
- Total mercury concentration (ng/L)
- Mercury deposition flux (ng/m²)

**AMoN Ammonia:**
- Ambient NH3 concentration (μg/m³)

#### Access Methods

**NADP Data Portal:**
- URL: https://nadp.slh.wisc.edu/data/
- Interactive maps and data query tools
- Select network (NTN, MDN, AMoN), sites, date range
- Export: CSV, Excel

**Bulk Data Downloads:**
- Annual data files by network
- Site metadata with lat/lon, county
- Format: CSV

**Visualizations:**
- NADP produces annual maps and trend reports
- Isopleth maps of deposition
- Time series plots

#### Data Format

**NTN Weekly Data:**
```
site_id, site_name, latitude, longitude, state, county,
date_on, date_off, precipitation_cm, pH,
sulfate_mg_per_L, nitrate_mg_per_L, ammonium_mg_per_L,
chloride, calcium, magnesium, potassium, sodium,
lab_conductivity, field_conductivity,
sulfate_deposition_kg_per_ha, nitrate_deposition_kg_per_ha, ammonium_deposition_kg_per_ha
```

#### Data Quality

**Sample Collection:**
- Automated wet-only collectors (open only during precipitation)
- Weekly sample retrieval
- Samples shipped to Central Analytical Laboratory (CAL)

**Quality Assurance:**
- Laboratory QA/QC
- Blind audits
- Collocated samplers
- Inter-laboratory comparisons

**Data Completeness:**
- Quality flags for samples
- Completeness criteria for annual summaries

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Longest wet deposition record in North America; critical for acid rain trends

#### Use Cases

**Acid Rain Trends:**
- pH increases (less acidic) since 1980s due to Clean Air Act
- Sulfate deposition decreases (dramatic)
- Nitrate deposition decreases (moderate)

**Nitrogen Deposition:**
- Nutrient enrichment of ecosystems
- Ammonium + nitrate = total inorganic nitrogen deposition

**Mercury Deposition:**
- Toxic metal monitoring
- Source apportionment (power plants, incinerators)

**Ammonia Monitoring:**
- Agricultural emissions tracking
- Ammonia-to-ammonium conversion in atmosphere

#### Comparison to Other Networks

**vs. CASTNET:**
- NADP: Wet deposition (what's in rain/snow)
- CASTNET: Ambient air concentrations + dry deposition estimates
- **Complementary**: Together provide total deposition

**vs. IMPROVE/CSN:**
- NADP: Wet deposition chemistry
- IMPROVE/CSN: Ambient PM composition
- **Different matrices**: Precipitation vs air

**Unique Value:**
- LONGEST wet deposition record (1978+)
- Only comprehensive mercury deposition network (MDN)
- Only dedicated ammonia gas monitoring network (AMoN)
- Critical for tracking Clean Air Act impacts on acid rain

---

### Source 7: EPA AQS (Air Quality System) - Ambient Concentrations

**Official Name**: Air Quality System (AQS)
**Agency**: U.S. Environmental Protection Agency
**Status**: ✅ COMPREHENSIVE AMBIENT AIR QUALITY DATABASE (1980-PRESENT)

#### Overview

AQS is EPA's repository for ambient air quality data from thousands of monitoring stations across the US. It contains measured concentrations of criteria pollutants and many air toxics.

#### Geographic & Temporal Coverage

- **Geographic**: ~4,000 monitoring sites nationally
- **Sites Assignable**: Sites have county FIPS codes
- **Years**: Data from 1980-present (45 years for some pollutants)
- **Frequency**: Varies by pollutant (continuous, hourly, daily, every-third-day)
- **Update**: Near-real-time for current data; validated data released annually

#### Pollutants Monitored

**Criteria Pollutants:**
1. **Ozone (O3)** - 8-hour, 1-hour averages; continuous monitoring
2. **PM2.5** - 24-hour, annual averages; daily or every-third-day sampling
3. **PM10** - 24-hour averages; daily or every-sixth-day sampling
4. **SO2** - 1-hour, 3-hour, 24-hour, annual; continuous monitoring
5. **NO2** - 1-hour, annual; continuous monitoring
6. **CO** - 1-hour, 8-hour; continuous monitoring
7. **Lead** - 3-month rolling average; monthly or quarterly sampling

**Air Toxics (NATTS/UATMP):**
- 187 HAPs including VOCs, carbonyls, metals
- Subset of sites with toxic monitoring

**PM2.5 Speciation:**
- CSN data flows into AQS (documented above)
- EC, OC, sulfate, nitrate, elements

#### Variables Available (per site per pollutant)

| Variable | Description | Format |
|----------|-------------|--------|
| Site Code | Unique site identifier | Code |
| Site Name | Monitoring site name | Text |
| Latitude, Longitude | Site location | Coordinates |
| County FIPS | 5-digit county code | Code |
| Date/Time | Measurement timestamp | DateTime |
| Pollutant Concentration | Measured value | Various units (ppb, ppm, μg/m³) |
| Units | Concentration units | Text |
| Sample Duration | Averaging time | Hours/days |
| Data Quality Flags | Validity flags | Codes |

#### Access Methods

**AQS Data Mart:**
- URL: https://www.epa.gov/outdoor-air-quality-data
- Interactive query tool
- Query by: location, pollutant, date range, site type
- Export: CSV, Excel

**AQS API:**
- URL: https://aqs.epa.gov/aqsweb/documents/data_api.html
- RESTful API
- Free, requires email signup for API key
- Query: sites, monitors, sample data, summary data
- Format: JSON

**Pre-Generated Data Files:**
- URL: https://aqs.epa.gov/aqsweb/airdata/download_files.html
- Annual files by pollutant
- Daily, hourly, 8-hour averages
- Format: ZIP files containing CSV

**Example API Query:**
```
https://aqs.epa.gov/data/api/sampleData/byCounty?
email=myemail@example.com&key=mykey&param=44201&
bdate=20230101&edate=20231231&state=06&county=037
```
(param=44201 is Ozone)

#### Data Format

**Sample Data:**
```
state_code, county_code, site_number, parameter_code,
poc, latitude, longitude, datum, parameter_name,
date_local, time_local, date_gmt, time_gmt,
sample_measurement, units_of_measure, mdl, uncertainty,
qualifier, method_type, method_code, method_name,
state_name, county_name, date_of_last_change
```

#### County-Level Aggregation

**Methods:**
1. **Site-specific**: Use county FIPS from site metadata
2. **County averages**: Average across all sites in a county
3. **Maximum**: County maximum concentration (e.g., design values for NAAQS)
4. **Population-weighted**: Weight by proximity to population centers

**Example R Code:**
```r
library(RAQSAPI)
library(tidyverse)

# Set API credentials
aqs_credentials(username = "myemail@example.com", key = "mykey")

# Get ozone data for all California counties, 2023
ca_counties <- unique(fips_codes$county_code[fips_codes$state_code == "06"])

ozone_data <- map_dfr(ca_counties, function(county) {
  aqs_sampledata_bycounty(
    parameter = "44201",  # Ozone
    bdate = as.Date("2023-01-01"),
    edate = as.Date("2023-12-31"),
    stateFIPS = "06",
    countycode = county
  )
})

# Calculate county annual means
county_ozone <- ozone_data %>%
  group_by(county_code, county) %>%
  summarize(
    annual_mean_ozone = mean(sample_measurement, na.rm = TRUE),
    days_measured = n(),
    sites = n_distinct(site_number),
    .groups = "drop"
  )
```

#### Data Quality

**Measurement Methods:**
- Federal Reference Methods (FRM) or Federal Equivalent Methods (FEM)
- Continuous analyzers for gases (O3, SO2, NO2, CO)
- Filter-based for particulates (PM2.5, PM10, Lead)
- Quality assurance per 40 CFR Part 58

**Quality Flags:**
- Validated data (certified by state/local agencies)
- Flagged for instrument failures, calibration errors, unusual events

**Completeness:**
- Data completeness requirements for regulatory use (typically 75% or higher)

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Regulatory-grade monitoring data; basis for NAAQS compliance

#### Use Cases

**Regulatory:**
- National Ambient Air Quality Standards (NAAQS) attainment/nonattainment determinations
- Design values for criteria pollutants

**Health Research:**
- Exposure assessment
- Epidemiological studies (air pollution and health outcomes)

**Trend Analysis:**
- Long-term air quality improvement tracking
- Impact of regulations (Clean Air Act)

**County-Level Analysis:**
- County air quality rankings
- Environmental justice (disproportionate exposures)

#### Comparison to Other Sources

**AQS vs NEI:**
- AQS: Ambient concentrations (what people breathe)
- NEI: Emissions (what's released)
- **Relationship**: NEI emissions → atmospheric transport/chemistry → AQS concentrations

**AQS vs IMPROVE/CSN:**
- IMPROVE/CSN: Subset of AQS PM2.5 speciation network sites
- AQS: Broader database including all criteria pollutants

**AQS vs CEMS:**
- CEMS: Emissions from power plant stacks
- AQS: Ambient concentrations in community air

**Unique Value:**
- Most comprehensive ambient air quality database for US
- Long-term records (1980+ for many pollutants)
- Regulatory-grade quality assurance
- API access for automated data retrieval

---

### Source 8: PAMS (Photochemical Assessment Monitoring Stations)

**Official Name**: Photochemical Assessment Monitoring Stations
**Agency**: U.S. Environmental Protection Agency
**Status**: ✅ VOC SPECIATION & OZONE PRECURSOR MONITORING (1990s-PRESENT)

#### Overview

PAMS sites provide detailed VOC speciation and ozone precursor monitoring to understand ozone formation chemistry. These sites measure individual VOC species, not just total VOCs.

#### Geographic & Temporal Coverage

- **Geographic**: ~75 PAMS sites in ozone nonattainment or near-nonattainment areas
- **Sites**: Urban areas with ozone issues
- **Years**: 1993-present (varies by site, network redesigned in 2017-2019)
- **Frequency**: Sampling during ozone season (typically May-September)
- **Update**: Data flows into AQS

#### Variables Measured

**VOC Speciation (60+ compounds):**

**Alkanes:**
- Ethane, propane, butane, pentane, hexane, heptane, octane
- Branched alkanes (isobutane, isopentane, 2-methylpentane, 3-methylpentane, etc.)

**Alkenes:**
- Ethylene, propylene, 1-butene, isobutene
- 1,3-butadiene

**Aromatics:**
- Benzene, toluene, ethylbenzene
- Xylenes (m+p-xylene, o-xylene)
- Trimethylbenzenes
- Styrene

**Oxygenated VOCs:**
- Formaldehyde, acetaldehyde
- Acetone, methyl ethyl ketone (MEK)

**Carbonyl Compounds:**
- Using DNPH (2,4-dinitrophenylhydrazine) cartridges
- Formaldehyde, acetaldehyde, acrolein, propionaldehyde, crotonaldehyde, benzaldehyde, etc.

**Other Ozone Precursors:**
- NOx (NO, NO2) - continuous
- CO - continuous
- Meteorology (temperature, wind speed/direction, solar radiation)

#### Sampling Methods

**Canister Sampling:**
- Whole air samples collected in canisters
- Lab analysis by GC-MS or GC-FID
- Typically every 3rd or 6th day during ozone season
- Morning samples (6-9 AM) to capture early precursors

**Carbonyl Sampling:**
- DNPH-coated cartridges
- Lab analysis by HPLC
- Same schedule as canisters

**Continuous Measurements:**
- Automated GC for real-time VOC measurements (some sites)
- Continuous NOx, O3, CO

#### Access Methods

**AQS Database:**
- PAMS data flows into EPA AQS
- URL: https://www.epa.gov/aqs
- Query by site, VOC parameter codes
- API access available

**Pre-Generated Files:**
- Available through AQS annual files
- Filter for PAMS sites

**Parameter Codes:**
- Each VOC has unique parameter code in AQS
- Example: Benzene = 45201, Toluene = 45202

#### Data Format

Same as AQS (described above), with:
- VOC concentrations typically in ppbC (parts per billion carbon) or ppbv
- Carbonyl concentrations in μg/m³

#### Use Cases

**Ozone Formation Analysis:**
- Identify dominant VOC precursors
- Calculate ozone formation potential (reactivity-weighted VOC)
- NOx-limited vs VOC-limited regimes

**Source Apportionment:**
- VOC ratios identify sources (e.g., toluene/benzene ratio for gasoline vs industrial)
- Fingerprinting of emission sources

**Air Quality Modeling:**
- VOC speciation profiles for model inputs
- Validate model VOC predictions

**Trend Analysis:**
- Decreases in VOC concentrations due to mobile source controls
- Benzene trends (Mobile Source Air Toxics rule)

**Reliability**: ⭐⭐⭐⭐ (4/5) - High-quality VOC speciation; limited spatial coverage (urban ozone problem areas)

---

### Source 9: NCore (National Core) Multi-Pollutant Monitoring

**Official Name**: National Core (NCore) Multi-Pollutant Monitoring Network
**Agency**: U.S. Environmental Protection Agency
**Status**: ✅ INTEGRATED MULTI-POLLUTANT SITES (2009-PRESENT)

#### Overview

NCore sites are "super sites" that measure a comprehensive suite of pollutants at a single location. Designed to provide integrated multi-pollutant data for trends, health research, and model evaluation.

#### Geographic & Temporal Coverage

- **Geographic**: ~75 NCore sites (originally ~80), at least one per state
- **Site Selection**: Representative of urban, suburban, and rural areas
- **Years**: 2009-present (15-year record)
- **Frequency**: Varies by pollutant (continuous, daily)

#### Pollutants Measured (Comprehensive Suite)

**Gases (Continuous):**
- Ozone (O3)
- SO2
- NO2, NOy (total reactive nitrogen)
- CO

**Particulate Matter:**
- PM2.5 mass (continuous and 24-hour filter-based)
- PM10 mass
- PM2.5 speciation (same as CSN):
  - EC, OC
  - Sulfate, nitrate, ammonium
  - Elements (XRF)
  - Ions (IC)

**PM10-2.5 (Coarse Fraction):**
- Coarse mass
- Coarse speciation

**Meteorology:**
- Temperature, relative humidity
- Wind speed and direction
- Solar radiation
- Precipitation

**Special Measurements (subset of sites):**
- Black carbon (aethalometer)
- Particle size distribution
- VOCs (at some sites)

#### Unique Features

**Integrated Measurements:**
- All pollutants measured at same location → study interactions
- Continuous and filter-based measurements side-by-side

**PM2.5 Continuous:**
- Real-time PM2.5 (FEM continuous monitors)
- Captures episodic events (wildfires, dust storms)

**Collocated Measurements:**
- Quality assurance through collocated samplers

#### Access Methods

**AQS:**
- NCore data flows into EPA AQS
- Query by NCore site codes
- All parameters available through AQS API

**NCore Site List:**
- EPA provides list of NCore sites
- Site metadata with coordinates, county FIPS

#### Data Format

Same as AQS, with additional metadata indicating NCore site status.

#### Use Cases

**Multi-Pollutant Research:**
- Study pollutant correlations (e.g., PM2.5 and ozone)
- PM2.5 continuous data for health studies (hourly exposures)

**Model Evaluation:**
- Comprehensive dataset for validating air quality models (CMAQ, WRF-Chem)
- Multiple species at same location

**Trends Analysis:**
- Long-term trends (2009-present) for multiple pollutants
- Integrated assessment of air quality improvements

**Reliability**: ⭐⭐⭐⭐⭐ (5/5) - Comprehensive multi-pollutant data; high QA/QC standards

---

## MOBILE SOURCE EMISSIONS

### Source 6: EPA MOVES Model (Motor Vehicle Emission Simulator)

**Official Name**: MOVES (Motor Vehicle Emission Simulator)
**Agency**: U.S. Environmental Protection Agency, Office of Transportation and Air Quality
**Status**: ✅ OFFICIAL MODEL FOR ON-ROAD MOBILE SOURCE EMISSIONS

#### Geographic & Temporal Coverage

- **Geographic**: All 3,143 counties
- **Years**: 1990-2060 (historical + projections)
- **Model Versions**: MOVES4 (current), MOVES3, MOVES2014, MOVES2010, etc.
- **Update**: New model versions released every few years

#### Outputs Available

**Pollutants Modeled:**
- PM2.5, PM10
- SO2
- NOx
- VOCs (total and speciated)
- CO
- NH3
- Benzene, 1,3-butadiene, formaldehyde, acetaldehyde, acrolein, diesel PM (mobile source air toxics)
- GHGs: CO2, CH4, N2O (in recent versions)

**By Source Category:**
- Light-duty vehicles (cars, light trucks)
- Heavy-duty vehicles (trucks, buses)
- Motorcycles
- By fuel type (gasoline, diesel, CNG, electric)
- By road type (urban restricted, urban unrestricted, rural)

**By Process:**
- Running exhaust
- Start exhaust (cold start, hot start)
- Crankcase running
- Evaporative (diurnal, hot soak, permeation, refueling)
- Brake wear
- Tire wear
- Extended idle

#### Inputs Required

To run MOVES for a county, need:
- Vehicle population (by age, type)
- Vehicle Miles Traveled (VMT) by vehicle type and road type
- Speed distribution
- Temperature and humidity
- Fuel properties (sulfur content, RVP)
- Inspection & Maintenance programs

**Default Databases:**
- EPA provides national defaults
- State/local agencies can use local data

#### Access Methods

**MOVES Model Software:**
- URL: https://www.epa.gov/moves
- Free download (Windows only)
- Requires MySQL database
- GUI and command-line batch mode

**Pre-Run County Estimates:**
- NEI includes county mobile source emissions run with MOVES
- Can extract from NEI rather than running MOVES yourself

**MOVES Lookup Tables:**
- Emission rates by vehicle type, speed, temperature
- Can apply to local VMT data

#### Data Format

**MOVES Output Database:**
- MySQL database with multiple tables
- Key output table: `movesoutput`
- Contains: county, year, pollutant, source type, process, emissions (grams or tons)

**Aggregated Output:**
```
county_fips, year, pollutant, source_type, process_type,
emissions_tons_per_year, emissions_grams_per_mile
```

#### Use Cases

- County-level on-road emissions inventory (feeds into NEI)
- Transportation conformity analysis
- Impact of fleet turnover, electrification
- Impact of fuel standards
- Air quality modeling inputs

#### Limitations

- **Model-based**: Not measured emissions; uses activity data + emission factors
- **Complex**: Requires expertise to run
- **Data intensive**: Needs local VMT, fleet data for best accuracy
- **Computational**: Large model runs can take hours/days
- **No non-road**: MOVES is on-road only; non-road uses NONROAD model (now deprecated, functionality in MOVES)

**Reliability**: ⭐⭐⭐⭐ (4/5) - Best available on-road mobile source model; EPA's official tool

---

## AGRICULTURAL EMISSIONS

### Source 7: EPA Agricultural Emissions (NEI Agricultural Sector)

**Covered in NEI Section Above**

**Key Agricultural Emissions Sources:**

**Livestock Operations:**
- NH3 from manure management
- PM2.5 from animal housing, feedlots
- CH4 from enteric fermentation (cattle, sheep)
- N2O from manure management

**Crop Production:**
- NH3 from fertilizer application
- PM10 from tilling, harvesting
- N2O from fertilized soils
- Pesticide drift (VOCs, HAPs)

**Agricultural Burning:**
- PM2.5, CO, NOx, VOCs from crop residue burning
- Prescribed agricultural fires

**County-Level Data:**
- NEI area source category includes agricultural emissions by county
- Based on livestock populations (USDA Census of Agriculture)
- Fertilizer sales by county
- Crop acreage by county
- Emission factors applied

**Access:**
- Through NEI (see Source 1)
- Agricultural sector emissions downloadable separately

**Additional Source:**
- **EPA Inventory of U.S. Greenhouse Gas Emissions and Sinks**
  - National-level annual report
  - Agricultural CH4 and N2O estimates
  - County-level not publicly available (state-level disaggregation possible with USDA data)

---

## BIOGENIC & NATURAL EMISSIONS

### Source 8: NEI Biogenic Emissions

**Included in NEI (Source 1)**

**Biogenic VOC Emissions:**
- Isoprene from broadleaf trees
- Monoterpenes (alpha-pinene, beta-pinene, limonene, etc.) from conifers
- Other biogenic VOCs

**Model Used:**
- BEIS (Biogenic Emission Inventory System)
- Or MEGAN (Model of Emissions of Gases and Aerosols from Nature)

**Inputs:**
- Land cover (forest type, vegetation)
- Temperature
- Solar radiation
- Leaf area index

**County-Level:**
- NEI provides county-level biogenic VOC emissions
- Important for ozone formation (VOCs + NOx + sunlight → O3)
- Important for secondary organic aerosol (SOA) formation

**Access:**
- Through NEI downloads

---

### Source 9: NEI Wildfire Emissions

**Included in NEI (Source 1)**

**Wildfire Emissions Data:**
- Event-specific emissions by fire
- PM2.5, PM10, CO, NOx, VOCs, NH3
- Based on fire perimeters, fuel loading, emission factors

**Fire Detection:**
- Satellite-based (MODIS, VIIRS)
- HMS smoke plumes
- Ground reports

**County Assignment:**
- Fires assigned to counties based on fire perimeter location
- Can have multi-county fires

**Years:**
- Varies by fire season
- Major fire years have large emissions
- 2020 Western wildfires were record-breaking

**Access:**
- NEI fire emissions downloadable
- Fire-specific data: https://www.epa.gov/air-emissions-inventories/wildland-fire-emissions-inventory-system

**Additional Fire Data Source:**
- **NIFC (National Interagency Fire Center)**: Fire perimeters, acres burned by county
  - URL: https://data-nifc.opendata.arcgis.com/

---

## SATELLITE-BASED ATMOSPHERIC DATA

### Source 10: Satellite Atmospheric Composition Data

**Multiple satellite instruments provide atmospheric column measurements aggregable to county level**

#### OMI (Ozone Monitoring Instrument) - 2004-present

**Instrument**: OMI on NASA Aura satellite
**Launch**: 2004
**Status**: Operating (degraded since 2008 row anomaly, but still valuable)

**Variables:**
- NO2 (nitrogen dioxide) tropospheric column
- SO2 (sulfur dioxide) column
- HCHO (formaldehyde) column
- Ozone column
- Aerosol optical depth

**Spatial Resolution:**
- 13 km × 24 km at nadir
- Aggregable to county level

**Temporal Coverage:**
- Daily global coverage
- 2004-present

**Access:**
- NASA GES DISC (Goddard Earth Sciences Data and Information Services Center)
- URL: https://disc.gsfc.nasa.gov/
- Format: HDF5, NetCDF
- Requires processing (Level 2 → Level 3 gridded)

**Use Case:**
- Long-term NO2 trends (traffic, power plants)
- SO2 hotspots (volcanoes, power plants, smelters)
- HCHO as VOC proxy

---

#### TROPOMI (2018-present)

**Instrument**: TROPOMI on ESA Sentinel-5P satellite
**Launch**: 2017, data from 2018
**Status**: Operating

**Variables:**
- NO2 tropospheric column (high resolution!)
- SO2 column
- HCHO column
- CO column
- CH4 column
- O3 column
- Aerosol optical depth

**Spatial Resolution:**
- 3.5 km × 5.5 km (previously 7km × 3.5km)
- **Highest resolution atmospheric composition from space**
- Excellent for county-level analysis

**Temporal Coverage:**
- Daily global coverage
- 2018-present

**Access:**
- ESA Sentinel Data Hub: https://dataspace.copernicus.eu/
- NASA GES DISC (for some products)
- Google Earth Engine (processed products)

**Use Case:**
- Highest spatial resolution for county-level pollution mapping
- CH4 emissions from oil & gas, landfills
- CO from fires, traffic

---

#### MOPITT (CO) - 2000-present

**Instrument**: MOPITT (Measurements of Pollution in the Troposphere) on NASA Terra
**Launch**: 1999, data from 2000
**Status**: Operating (24 years!)

**Variable:**
- CO (carbon monoxide) column and profile

**Spatial Resolution:**
- 22 km × 22 km

**Temporal Coverage:**
- 2000-present (24-year record)

**Access:**
- NASA Atmospheric Science Data Center
- URL: https://eosweb.larc.nasa.gov/project/mopitt/mopitt_table

**Use Case:**
- CO trends (combustion tracer)
- Fire emissions tracking
- Urban pollution

---

#### MODIS AOD (Aerosol Optical Depth) - 2000-present

**Instruments**: MODIS on Terra (2000) and Aqua (2002)
**Status**: Operating

**Variable:**
- Aerosol Optical Depth (AOD) at 550 nm
- Angstrom exponent (aerosol size)
- Fine mode fraction

**Spatial Resolution:**
- 10 km × 10 km (Level 3 product)
- 3 km × 3 km available

**Temporal Coverage:**
- Daily, 2000-present
- Terra: 2000-present
- Aqua: 2002-present

**Access:**
- NASA LAADS DAAC: https://ladsweb.modaps.eosdis.nasa.gov/
- Google Earth Engine

**Use Case:**
- PM2.5 estimation (AOD correlates with surface PM2.5)
- Aerosol trends
- Wildfire smoke tracking

**County-Level Aggregation:**
- Extract satellite pixels overlapping county boundaries
- Average or sum to get county-level values
- Tools: Google Earth Engine, Python (rasterio, geopandas), R (sf, terra)

**Reliability**: ⭐⭐⭐⭐ (4/5) - Satellite data are indirect (column measurements, not surface), but valuable for spatial coverage

---

## ALREADY DOCUMENTED SOURCES

The following sources are already documented in other comprehensive files and will not be duplicated here:

### EPA Toxic Release Inventory (TRI)

**Documented in**: TRI_COMPREHENSIVE_DOCUMENTATION.md

**What It Covers:**
- ~800 toxic chemicals
- Facility-level releases to air, water, land
- 1987-present (38-year record)
- Includes many HAPs also in NEI

**Air Emissions Overlap with This File:**
- TRI has stack emissions, fugitive emissions to air
- NEI incorporates TRI data for certain HAPs
- TRI has facility-level detail
- TRI limited to facilities meeting reporting thresholds

**When to Use TRI:**
- Facility-specific toxic chemical releases
- Long time series (1987 vs NEI 1990)
- Detailed chemical-specific data (e.g., specific PAHs, specific metals)

**When to Use NEI:**
- Comprehensive county-level totals including non-TRI sources
- Criteria pollutants (PM2.5, NOx, etc.)
- Mobile and area sources not in TRI

---

### EPA Greenhouse Gas Reporting Program (GHGRP)

**Documented in**: RADON_OIL_GAS_ENERGY_COMPREHENSIVE.md

**What It Covers:**
- Facility-level GHG emissions
- CO2, CH4, N2O, fluorinated gases
- 2010-present
- Facilities emitting ≥25,000 metric tons CO2e annually

**Overlap with This File:**
- GHGRP has GHGs (CO2, CH4, N2O)
- NEI/CEMS have some CO2 (power plants)
- GHGRP more comprehensive for GHGs from industrial sources

**When to Use GHGRP:**
- Facility-level GHG emissions
- CH4 from landfills, oil & gas, coal mines
- Fluorinated gases (HFCs, PFCs, SF6)

**When to Use NEI/CEMS:**
- Criteria pollutants and HAPs
- All source sectors (not just large facilities)
- Mobile, area, biogenic, fire sources

---

## NOT AVAILABLE AT COUNTY LEVEL

The following sources do NOT provide county-level data:

### EPA National Emissions Trends (NET)

- **What**: Historical emissions trends for US
- **Geographic Level**: National and state-level only
- **Years**: 1970-present
- **Why Not County**: Aggregated for national/state trends reporting
- **Alternative**: Use NEI for county-level

---

### State/Regional Haze SIPs (State Implementation Plans)

- **What**: State-level emissions inventories for regional haze
- **Geographic Level**: State and sometimes multi-state regions
- **Why Not County**: SIPs report state totals
- **Alternative**: Use NEI

---

### Aircraft Emissions

- **What**: Emissions from commercial aircraft
- **Geographic Level**: Airport-specific, not county-aggregated in public data
- **Source**: FAA AEDT (Aviation Environmental Design Tool)
- **Why Not County**: Aircraft emissions occur at altitude and in flight paths, not easily assigned to counties
- **Note**: NEI has some airport ground support equipment (GSE) by county

---

### Marine Vessel Emissions (beyond ports)

- **What**: Emissions from ships in territorial waters
- **Geographic Level**: Shipping lanes, not county-specific
- **Why Not County**: Ships operate in coastal waters and international waters
- **Note**: NEI has commercial marine vessels (CMV) emissions estimated by port county

---

### Upper Atmosphere / Stratospheric Data

- **What**: Ozone depletion, stratospheric chemistry
- **Geographic Level**: Global, zonal
- **Why Not County**: Stratospheric processes are not county-specific

---

## DETAILED SOURCE DOCUMENTATION

(Expanded details for key sources - included in sections above)

---

## DATA ACCESS METHODS

### R Code Example: NEI County Emissions

```r
library(tidyverse)

# Download NEI county summary file
# https://gaftp.epa.gov/Air/emissions/
# Example: 2020v1/county_summaries_2020.csv

nei_county <- read_csv("county_summaries_2020.csv")

# Filter for specific pollutant and county
pm25_data <- nei_county %>%
  filter(pollutant_code == "PM25-PRI") %>%
  select(state_code, county_code, state_name, county_name,
         total_emissions_tons, point_tons, area_tons, onroad_tons,
         nonroad_tons, fires_tons) %>%
  mutate(county_fips = paste0(state_code, county_code))

# Summary by state
state_summary <- pm25_data %>%
  group_by(state_name) %>%
  summarize(
    total_pm25 = sum(total_emissions_tons),
    counties = n()
  ) %>%
  arrange(desc(total_pm25))
```

### Python Code Example: CEMS API

```python
import requests
import pandas as pd

# Query CEMS data via API
base_url = "https://api.epa.gov/easey/emissions-mgmt/apportioned/hourly"
params = {
    "beginDate": "2023-01-01",
    "endDate": "2023-12-31",
    "stateCode": "OH"
}

response = requests.get(base_url, params=params)
data = response.json()

# Convert to DataFrame
df = pd.DataFrame(data)

# Aggregate to facility-year
facility_annual = df.groupby(['facilityId', 'facilityName', 'stateCode']).agg({
    'so2Mass': 'sum',
    'noxMass': 'sum',
    'co2Mass': 'sum'
}).reset_index()

# Convert to tons
facility_annual['so2_tons'] = facility_annual['so2Mass'] / 2000  # lbs to tons
facility_annual['nox_tons'] = facility_annual['noxMass'] / 2000
```

### Google Earth Engine Example: TROPOMI NO2

```javascript
// Load TROPOMI NO2 data
var tropomi = ee.ImageCollection('COPERNICUS/S5P/OFFL/L3_NO2')
  .select('tropospheric_NO2_column_number_density')
  .filterDate('2023-01-01', '2023-12-31');

// Average over year
var no2_annual = tropomi.mean();

// Load US counties
var counties = ee.FeatureCollection('TIGER/2020/COUNTIES');

// Aggregate to counties
var county_no2 = no2_annual.reduceRegions({
  collection: counties,
  reducer: ee.Reducer.mean(),
  scale: 1000
});

// Export
Export.table.toDrive({
  collection: county_no2,
  description: 'county_tropomi_no2_2023',
  fileFormat: 'CSV'
});
```

---

## PRIORITY VARIABLES FOR COLLECTION

### Criteria Air Pollutants (NEI) - Top 10

1. **PM2.5 Total Emissions** (tons/year) - All sources combined
2. **PM10 Total Emissions** (tons/year)
3. **SO2 Total Emissions** (tons/year) - Precursor to sulfate PM2.5
4. **NOx Total Emissions** (tons/year) - Precursor to nitrate PM2.5 and ozone
5. **VOC Total Emissions** (tons/year) - Precursor to ozone and SOA
6. **CO Total Emissions** (tons/year)
7. **NH3 Total Emissions** (tons/year) - Precursor to ammonium PM2.5
8. **PM2.5 by Source Sector** (point, area, mobile, fires)
9. **NOx by Source Sector** (point, mobile, area)
10. **VOC by Source Sector** (mobile, area, biogenic)

### Power Plant Emissions (CEMS) - Top 5

1. **Annual SO2 Emissions** (tons/year) - By county from power plants
2. **Annual NOx Emissions** (tons/year) - By county from power plants
3. **Annual CO2 Emissions** (metric tonnes/year) - By county from power plants
4. **Number of Operating Power Plants** - By county
5. **Gross Electricity Generation** (MWh/year) - By county

### Aerosol Composition - Top 10

1. **Elemental Carbon (EC/Black Carbon)** (μg/m³) - IMPROVE/CSN sites
2. **Organic Carbon (OC)** (μg/m³) - IMPROVE/CSN sites
3. **Sulfate (SO4)** (μg/m³) - IMPROVE/CSN/CASTNET sites
4. **Nitrate (NO3)** (μg/m³) - IMPROVE/CSN/CASTNET sites
5. **Ammonium (NH4)** (μg/m³) - IMPROVE/CSN/CASTNET sites
6. **Soil/Crustal Elements** (μg/m³) - Al, Si, Ca, Fe
7. **Sea Salt** (μg/m³) - Na, Cl
8. **Trace Metals** (ng/m³) - As, Pb, Mn, Ni, V, Zn
9. **PM2.5 Total Mass** (μg/m³) - From composition networks
10. **OC/EC Ratio** - Indicator of primary vs secondary organic aerosols

### Mobile Sources (MOVES/NEI) - Top 5

1. **On-Road NOx Emissions** (tons/year) - By county
2. **On-Road PM2.5 Emissions** (tons/year) - By county
3. **On-Road VOC Emissions** (tons/year) - By county
4. **Non-Road Equipment NOx** (tons/year) - By county
5. **Non-Road Equipment PM2.5** (tons/year) - By county

### Agricultural Emissions - Top 5

1. **Agricultural NH3 Emissions** (tons/year) - From livestock and fertilizer
2. **Agricultural PM10 Emissions** (tons/year) - From tilling, harvesting
3. **Livestock CH4 Emissions** (metric tonnes CO2e/year) - Enteric fermentation
4. **Livestock N2O Emissions** (metric tonnes CO2e/year) - Manure management
5. **Fertilizer N2O Emissions** (metric tonnes CO2e/year) - Soil emissions

### Biogenic & Natural - Top 5

1. **Biogenic Isoprene Emissions** (tons/year) - Vegetation VOCs
2. **Biogenic Monoterpene Emissions** (tons/year) - Vegetation VOCs
3. **Wildfire PM2.5 Emissions** (tons/year) - By fire event and county
4. **Wildfire CO Emissions** (tons/year) - Tracer of biomass burning
5. **Acres Burned by Wildfire** - By county

### Satellite Data (if aggregating to county) - Top 5

1. **TROPOMI NO2 Column** (molec/cm²) - Annual mean by county
2. **TROPOMI CH4 Column** (ppb) - Annual mean by county
3. **OMI SO2 Column** (DU) - Annual mean by county
4. **MODIS AOD** (unitless) - Annual mean by county
5. **MOPITT CO Column** (ppb) - Annual mean by county

---

## QUICK REFERENCE

### Primary Data URLs

| Source | URL |
|--------|-----|
| EPA NEI Data | https://www.epa.gov/air-emissions-inventories/national-emissions-inventory-nei-data |
| EPA NEI FTP | https://gaftp.epa.gov/Air/emissions/ |
| EPA CEMS/AMPD | https://campd.epa.gov/ |
| CEMS API | https://api.epa.gov/easey/ |
| IMPROVE Network | http://views.cira.colostate.edu/fed/ |
| EPA CSN Data | https://www.epa.gov/amtic/chemical-speciation-network-csn |
| EPA CASTNET | https://www.epa.gov/castnet |
| **NADP (National Atmospheric Deposition Program)** | **https://nadp.slh.wisc.edu/data/** |
| **EPA AQS (Air Quality System)** | **https://www.epa.gov/outdoor-air-quality-data** |
| **AQS API** | **https://aqs.epa.gov/aqsweb/documents/data_api.html** |
| **AQS Pre-Generated Files** | **https://aqs.epa.gov/aqsweb/airdata/download_files.html** |
| EPA MOVES | https://www.epa.gov/moves |
| TROPOMI Data | https://dataspace.copernicus.eu/ |
| OMI Data | https://disc.gsfc.nasa.gov/ |
| MODIS AOD | https://ladsweb.modaps.eosdis.nasa.gov/ |

### API Keys Required

| Source | API Key? | Signup URL |
|--------|----------|------------|
| EPA NEI | No | N/A |
| EPA CEMS | No | N/A |
| **EPA AQS API** | **Yes (free, email-based)** | **https://aqs.epa.gov/aqsweb/documents/data_api.html#signup** |
| NASA GES DISC | Yes (free) | https://urs.earthdata.nasa.gov/ |
| Google Earth Engine | Yes (free) | https://code.earthengine.google.com/ |

### Contact Information

| Agency | Email/Contact |
|--------|---------------|
| EPA NEI | State of the Air Report team |
| EPA CEMS | CAMPD@epa.gov |
| IMPROVE | IMPROVE Program Coordinator |
| NASA Satellite Data | GES DISC Help Desk |

---

## DOCUMENT METADATA

**Document Version**: 1.1 (Enhanced with NADP, AQS, PAMS, NCore)
**Last Updated**: November 12, 2025
**Author**: Comprehensive research compilation
**Sources Documented**: 13+ major sources (NEI, CEMS, IMPROVE, CSN, CASTNET, NADP, AQS, PAMS, NCore, MOVES, satellites, agricultural, wildfire, biogenic)
**Sources Verified**: All URLs verified as of November 2025
**Next Review**: Annual update recommended

### Version History
- **v1.0 (November 12, 2025)**: Initial comprehensive documentation of 10 sources
- **v1.1 (November 12, 2025)**: Added NADP (1978+ longest wet deposition), EPA AQS (1980+ ambient concentrations), PAMS (VOC speciation), NCore (multi-pollutant sites)

---

**END OF COMPREHENSIVE DOCUMENTATION**
