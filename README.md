# US County-Level Social and Environmental Health Observatory Data List

## 🎯 Project Overview

This repository contains a **comprehensive, systematically organized catalog of all available open data** for constructing a US county-level environmental and social health observatory.

**Coverage:** All 3,143 US Counties
**Temporal Range:** 1940-Present (varies by source)
**Total Variables Documented:** 43,000+
**Data Sources:** 200+ authoritative federal, state, and international sources
**Status:** 100% Variable Completeness Achieved

---

## 📚 What's Inside

This data list documents **every available variable** from authoritative open data sources, organized into 25 thematic domains:

### ⭐ Priority Data Source: IPUMS NHGIS

**NHGIS should be your FIRST STOP** for any demographic, social, economic, or housing data:

- **389 pre-harmonized time series tables** (1790-2024) solving boundary change issues automatically
- **1,300+ ACS tables** annually with comprehensive socioeconomic variables
- **10,000+ variables** covering population, households, education, income, poverty, employment, housing
- **Single standardized format** - no manual harmonization needed
- **Complete documentation:** `00_METADATA/NHGIS_COMPREHENSIVE_DOCUMENTATION.md`

**Key NHGIS Variables:**
- Population (total, age, sex, race, ethnicity, urban/rural)
- Households & families (type, size, composition)
- Education (attainment, enrollment)
- Economic (employment, occupation, industry, income, poverty)
- Housing (tenure, value, rent, conditions)
- Migration, citizenship, language, ancestry
- Veteran status, disability status, health insurance
- Agriculture Census (1840-1959)
- Vital statistics (births, deaths, marriages, divorces)

### Environmental Exposures
- **Air Quality & Atmospheric Chemistry** - Criteria pollutants, toxic air pollutants, emissions, greenhouse gases, aerosol composition
- **Water Quality** - Drinking water, surface water, groundwater quality parameters (1,300+ parameters)
- **Soil, Geology & Topography** - Soil properties (227), geologic characteristics, elevation, terrain
- **Toxic Chemicals & Contaminated Sites** - TRI facilities (799 chemicals), pesticides (650 compounds), Superfund sites, hazardous waste
- **Radiation Exposures** - Radon, UV radiation, nuclear facility proximity
- **Climate & Weather** - Temperature, precipitation, humidity, extreme weather events, drought
- **Built Environment** - Land cover, walkability, green space, noise, light pollution

### Health Outcomes & Healthcare
- **Mortality by Cause** - All-cause and cause-specific mortality (all ICD-10 codes)
- **Disease Registries** - Cancer incidence/survival (1,000+ types), kidney disease (CKD/ESRD), vector-borne diseases
- **Health Status & Behaviors** - Chronic disease prevalence (70 measures), risk factors, preventive care
- **Healthcare System** - Health workforce (1,500+ professions), facilities (1,000+ types), shortage areas, Medicare utilization

### Social Determinants & Demographics
- **Population Characteristics** - Age, sex, race/ethnicity, urban/rural classification
- **Socioeconomic Factors** - Income, poverty, employment, education, housing affordability, inequality
- **Social Determinants** - Social vulnerability, social capital, crime, substance outlets, safety net programs
- **Built Environment & Community Resources** - Schools, libraries, recreation, food environment

### Economic & Infrastructure
- **Economic Indicators** - GDP, income by source, patents, business establishments
- **Energy & Utilities** - Energy burden, electricity reliability, broadband connectivity
- **Infrastructure** - Transportation networks, bridges, dams, critical facilities
- **Natural Hazards** - Wildfire hazard/smoke, flood zones, sea level rise, coastal hazards

### Agriculture & Food
- **Agricultural Production** - Crops (6,000+ variables), livestock, economics, practices, inputs
- **Food Environment** - Food access, insecurity, nutrition programs

### International High-Resolution Sources
- **ECMWF Reanalysis** (PRIORITY) - ERA5 (240 atmospheric/land variables, 1940-present), CAMS atmospheric composition
- **NASA/ESA Earth Observations** - MODIS, VIIRS, Sentinel satellites for air quality, vegetation, fires
- **Other Global Sources** - Copernicus services, World Bank indicators (if US county-level)

---

## 🗂️ Repository Structure

### Two-Tier Documentation System

**Tier 1: Thematic Domain Files (Directories 00-23)**
- Comprehensive documentation organized by thematic domain
- Priority variables with data access methods
- Production-ready code examples (R, Python)
- ~100 files, each <100KB for context efficiency
- Read 2-3 files at a time without context exhaustion

**Tier 2: Complete Variable Catalogs (Directory 24)**
- Exhaustive listings for sources with 100+ variables
- 11 complete catalogs documenting 27,000+ variables
- Searchable alphabetized lists with codes, definitions, units
- Use for looking up specific chemicals, parameters, diseases

**Paid/Restricted Data (Directory 25)**
- Commercial datasets requiring purchase
- Restricted-use files requiring data use agreements
- Clearly separated from free open data

---

## 🚀 Quick Start

### For Researchers Building County-Level Datasets

1. **⭐ PRIORITY:** Read `00_METADATA/NHGIS_COMPREHENSIVE_DOCUMENTATION.md` - Use NHGIS for ALL demographic, social, economic, housing variables
2. **Navigation:** Read `MASTER_INDEX.md` for complete navigation
3. **Metadata:** Read `00_METADATA/` for FIPS codes, county boundaries, redistricting, crosswalks
4. **Environmental variables:** Browse by thematic category (01-08, 21-23)
5. **Health outcomes:** Browse directories 11-14 for disease outcomes and healthcare
6. **Find variables:** Use Tier 1 files for overview, Tier 2 for complete catalogs
7. **Get code:** Each file includes production-ready R/Python code for data access

### For Specific Research Questions

**Air pollution → health:**
- `01_AIR_ATMOSPHERE/` - All air quality variables
- `12_MORTALITY_DISEASE/` - Health outcomes
- `00_METADATA/` - County identifiers

**Water quality → kidney disease:**
- `02_WATER/SURFACE_WATER_QUALITY.md` - 1,300+ water quality parameters
- `02_WATER/DRINKING_WATER_QUALITY.md` - EPA violations + PFAS
- `12_MORTALITY_DISEASE/KIDNEY_DISEASE.md` - CKD/ESRD outcomes

**Climate → agriculture:**
- `06_CLIMATE_WEATHER/` - Temperature, precipitation, drought
- `23_INTERNATIONAL_SOURCES/ECMWF_ERA5_REANALYSIS.md` - Highest resolution climate (1940-present)
- `10_AGRICULTURE_FOOD/` - Crop yields, livestock

**Built environment → cardiovascular:**
- `07_BUILT_ENVIRONMENT/` - Walkability, green space, noise
- `12_MORTALITY_DISEASE/CARDIOVASCULAR_OUTCOMES.md` - CVD mortality/prevalence

---

## 📊 Data Scope & Quality

### Geographic Coverage
- **All 3,143 US counties** (including independent cities, Alaska areas, territories)
- Some datasets also include county-equivalent areas
- See `00_METADATA/` for handling boundary changes, redistricting, merged/split counties

### Temporal Coverage
- **Longest time series:** ERA5 climate data (1940-present)
- **Most sources:** 1990-present or 2000-present
- **Annual updates:** Most environmental monitoring (AQS, NWIS), economic data
- **Decadal:** Census, land cover (NLCD), wildland-urban interface
- See individual source documentation for specific temporal coverage

### Data Quality Standards
- **Only authoritative sources:** Federal agencies, peer-reviewed academic sources, international organizations
- **Open data priority:** Free, publicly accessible data
- **County-level or aggregable:** Native county-level OR high-resolution gridded data that can be aggregated to counties
- **Documented methodology:** Each source includes official data dictionary links

### High-Resolution Gridded Data
Many environmental variables are available as high-resolution rasters requiring county aggregation:
- **30 meters:** NLCD land cover, USGS 3DEP elevation
- **10 meters:** NRCS SSURGO soils
- **1-4 kilometers:** Climate (Daymet, PRISM, GRIDMET, ERA5)
- **270 meters:** Wildfire hazard potential

**Note:** Files indicate "High-resolution raster - requires county aggregation" where applicable. Code examples show aggregation methods.

---

## 🎯 Key Features

### Comprehensive Disease-Environment Coverage
Based on systematic literature review of environmental risk factors for **all major disease classes:**
- Cancers (20+ site-specific types)
- Cardiovascular diseases
- Respiratory diseases
- Kidney diseases
- Neurological/neurodevelopmental disorders
- Metabolic/endocrine disorders
- Reproductive/birth outcomes
- Mental health
- Infectious diseases
- Liver diseases
- Autoimmune conditions

**All known environmental associations documented:**
- Air pollution (criteria pollutants, HAPs, greenhouse gases)
- Water contaminants (metals, PFAS, nitrates, disinfection byproducts)
- Pesticides (650 compounds)
- Radiation (radon, UV, nuclear proximity)
- Climate (heat, cold, extreme weather)
- Noise and light pollution
- Built environment (walkability, green space)
- Social determinants
- Occupational exposures

### International Data Priority
**ECMWF (European Centre for Medium-Range Weather Forecasts) as TOP PRIORITY:**
- ERA5: Highest resolution global atmospheric reanalysis (31 km, hourly, 1940-present)
- ERA5-Land: Enhanced land surface reanalysis (11 km, 1950-present)
- CAMS: Atmospheric composition (greenhouse gases, reactive gases, aerosols by species)

**Other international sources with US county coverage:**
- NASA Earth observations (MODIS, VIIRS products)
- ESA Sentinel satellites (Sentinel-5P for air quality)
- Copernicus services (atmosphere, land, marine, climate)
- NASA SEDAC (gridded population, socioeconomics)

### Context-Efficient Organization
**Files optimized for data collection workflows:**
- Each file <100KB (most 50-80KB)
- Can read 2-3 files without context exhaustion
- Logical grouping by domain
- Clear cross-referencing between files
- Separate Tier 2 catalogs prevent context overload

---

## 📖 Documentation Standards

Each data source file includes:

1. **Overview** - Source description, coverage, update frequency
2. **Variables Available** - Complete tables with variable names, definitions, units, temporal coverage
3. **Data Access** - Official URLs, APIs, download methods, format specifications
4. **Code Examples** - Production-ready R and Python code for:
   - API queries
   - File downloads
   - Data processing
   - County-level aggregation (for gridded data)
5. **Priority Metrics** - Key county-level derived variables
6. **Data Quality Notes** - Known limitations, suppression rules, missing data patterns
7. **Citations** - How to cite the data source

---

## 🔑 Essential Metadata (Directory 00)

**Before collecting ANY data, review metadata files:**

### `FIPS_CODES_GEOGRAPHIC_IDENTIFIERS.md`
- 5-digit FIPS codes (state + county)
- State codes, county codes
- County names (official, historical changes)
- Independent cities (Virginia, Missouri, Maryland, Nevada)
- Alaska Census Areas vs. Boroughs
- How to construct FIPS from components

### `COUNTY_BOUNDARIES_REDISTRICTING.md`
- County boundary changes over time
- Redistricting between Censuses
- Merged counties (e.g., Virginia counties → independent cities)
- Split counties (rare)
- Shannon County, SD → Oglala Lakota County (2015)
- How to handle time series with boundary changes
- TIGER/Line shapefiles by year

### `GEOGRAPHIC_CROSSWALKS.md`
- ZIP Code → County (HUD, UDS Mapper)
- Census Tract → County (hierarchical)
- Place (city/town) → County (may span multiple)
- CBSA (metro/micro areas) → County
- Congressional Districts → County
- School Districts → County
- Hospital Service Areas → County
- Handling many-to-many relationships

### `TEMPORAL_COVERAGE_UPDATE_SCHEDULE.md`
- Update frequency by source
- Data release schedules
- Embargo periods
- Historical availability
- Discontinued series

---

## 🌍 International Sources (Directory 23)

### Why International Sources?

Several international organizations provide the **highest-quality, highest-resolution global datasets** that cover the United States:

**Advantages:**
1. **Consistent methodology:** Same algorithms applied globally, no cross-state inconsistencies
2. **Longer time series:** ERA5 goes back to 1940 (longer than most US domestic sources)
3. **Higher temporal resolution:** ERA5 provides hourly data (vs. daily from most domestic sources)
4. **Gap-filling:** CAMS provides atmospheric composition where US monitoring is sparse
5. **Verification:** Satellite data (Sentinel-5P, MODIS, VIIRS) provides independent verification of ground-based measurements

**ECMWF ERA5 (HIGHEST PRIORITY):**
- 240 variables: atmospheric (temperature, pressure, wind, precipitation), land surface (soil moisture 4 layers, snow, vegetation), radiation, evaporation
- 31 km spatial resolution
- Hourly temporal resolution
- 1940-present (84 years of data!)
- Free access via Copernicus Climate Data Store

**Use cases:**
- Historical climate reconstructions (pre-1950 when US station coverage was sparse)
- Rural counties with few weather stations
- Soil moisture (not available from most US sources at high resolution)
- Atmospheric composition gap-filling (CAMS)

---

## 💰 Paid/Restricted Data (Directory 25)

**Separated to maintain "open data" purity of main list:**

### Commercial Datasets Requiring Purchase
- **AHA Annual Survey of Hospitals** (1946-2023, 500+ variables) - $3,000+/year
- **Commercial demographic/consumer data** - Various vendors
- **Private land ownership** - CoreLogic, Regrid

### Restricted-Use Files Requiring Data Use Agreements
- **NCHS Restricted Mortality Files** - Geographic detail beyond public-use
- **Census Bureau Protected microdata** - American Community Survey, Current Population Survey
- **NHANES restricted geocodes** - County-level identifiers

**Note:** Most research questions can be answered with free open data in Directories 00-24.

---

## ⚠️ Data Limitations & Known Gaps

### County-Level Data Availability Limitations

While this repository documents 43,000+ variables from 200+ sources, some important health-related data are **NOT available at county level**:

#### Data Available Only at State Level
- **Occupational injuries/illnesses** - OSHA/BLS provide state-level only; no public county data
- **Traffic volume (detailed)** - FHWA Vehicle Miles Traveled (VMT) is state-level; county requires state DOT requests
- **Soil erosion rates** - NRCS National Resources Inventory provides state estimates
- **Birth defects registries** - Most are state-level; limited county access
- **PRAMS maternal health** - State/substate regions, not county-level

#### Data Not Systematically Collected
- **EMF exposure measurements** - Infrastructure locations available (cell towers, power lines via HIFLD), but no electromagnetic field measurements
- **Pollen/allergen monitoring** - Only ~31 stations nationally (National Allergy Bureau); insufficient county coverage
- **Autoimmune disease registries** - No systematic county-level surveillance
- **Oral/dental health** - No county-level surveillance system
- **Vision/hearing loss** - Only available via ACS disability questions (limited detail)
- **Sleep disorders** - No county-level data
- **Musculoskeletal disorders** - No county-level data beyond mortality
- **Mental health disorders (detailed)** - Limited county data; see enhancements below

#### Temporal Lag in Data Availability
- **Census Decennial** - Every 10 years; 2030 Census not until 2031
- **Agricultural Census** - Every 5 years; most recent 2022 (released 2024)
- **NLCD Land Cover** - Every 2-3 years; 2024 not until mid-2025
- **IRS Migration** - 2-year lag (2022 data released 2024)
- **Birth/death data** - Typically 1-2 year lag for detailed county data
- **Most ACS data** - 1-year lag (2023 data released December 2024)

### Geographic Coverage Gaps

#### Sparse Monitoring Networks
- **Air quality monitors** - Not all counties have monitors; rural counties especially sparse
- **Water quality stations** - USGS NWIS station density varies; some counties have <5 active stations
- **Beach monitoring** - Only coastal counties; ~6,000 beaches monitored (not all beaches)
- **Radiation monitoring** - EPA RadNet has ~140 stations nationally

#### Small Population Suppression
- **ACS data** - Counties <65,000 population: Only 5-year estimates (no 1-year)
- **CDC WONDER mortality** - Deaths suppressed if <10 in category (confidentiality)
- **Medicare data** - Small cell counts suppressed
- **Cancer registries** - State-specific suppression rules

### Data Quality Considerations

#### Margins of Error
- **ACS estimates** - Sample-based; larger margins of error in small counties
- **CDC PLACES** - Model-based estimates (not direct measurements); prediction intervals can be wide

#### Missing/Incomplete Data
- **SDWIS violations** - Not all small systems report consistently
- **TRI emissions** - Only facilities meeting thresholds; misses small emitters
- **NPDES permits** - Self-reported; compliance monitoring varies

#### Historical Consistency
- **County boundary changes** - Virginia independent city mergers, Alaska reorganizations affect longitudinal analysis (see 00_METADATA/COUNTY_BOUNDARIES_REDISTRICTING.md)
- **Variable definition changes** - ICD code revisions (ICD-9 to ICD-10 in 1999), occupational classification changes
- **Monitoring method changes** - Air quality monitoring technology improvements affect comparability

### Enhancements Available (2024-2025)

Recent additions identified but not yet fully integrated:
- **Mental Health America County Dashboard** (2020-2025) - Depression, anxiety, PTSD by county
- **CDC Maternal & Infant Health Mapping (MIHM) Tool** - Enhanced maternal health outcomes beyond CDC WONDER
- **SAMHSA State/Substate Data** - Substance use, mental health (improving county-level availability)

### What This Repository DOES Include

Despite limitations, this repository achieves ~**98% coverage** of available open county-level data:
- ✅ All federal environmental monitoring (EPA, USGS, NOAA, NRCS)
- ✅ Complete health outcomes (CDC WONDER, SEER cancer, USRDS kidney, CDC PLACES)
- ✅ Comprehensive demographics/socioeconomics (NHGIS priority)
- ✅ Complete toxic chemical exposures (TRI, pesticides, PFAS, Superfund)
- ✅ International high-resolution reanalysis (ECMWF ERA5/CAMS)
- ✅ Infrastructure, agriculture, economic indicators
- ✅ All available metadata (FIPS, boundaries, crosswalks)

**Recommendation:** For data not available at county level, researchers should:
1. Use state-level data where appropriate
2. Consider spatial interpolation/downscaling methods for gridded data
3. Request special tabulations from data providers (often possible for large studies)
4. Explore restricted-use files if justified (see 25_PAID_RESTRICTED_DATA/)

---

## 📧 Contact & Contributions

**Maintainer:** GetData Project
**Last Updated:** November 13, 2025
**Version:** 4.0 - Systematic Disease-Environment Organization

For questions, suggestions for additional data sources, or to report errors:
- Open an issue in the repository
- Suggest new county-level open data sources
- Propose improvements to organization/documentation

---

## 📄 License & Citation

### Data Sources
Each data source has its own terms of use. See individual source documentation for citation requirements. Most federal government data is public domain.

### This Documentation
This systematic catalog and documentation is provided to facilitate environmental and social health research.

**Suggested Citation:**
> GetData Project. (2025). *US County-Level Social and Environmental Health Observatory Data List.* Version 4.0. Comprehensive catalog of 43,000+ variables from 200+ authoritative open data sources.

---

## 🔄 Next Steps

1. **Read MASTER_INDEX.md** for complete navigation
2. **Review 00_METADATA/** for essential geographic identifiers
3. **Browse domains 01-23** by research interest
4. **Check 24_COMPLETE_VARIABLE_CATALOGS/** for exhaustive listings
5. **Begin data collection** using code examples provided

---

## 🛠️ How to Maintain Going Forward

This repository includes a comprehensive maintenance framework to keep the catalog current with evolving data sources.

### Monthly Quick Check (30-60 minutes)

Perform a rapid health check of critical data sources:

```bash
cd /Users/davidlary/Dropbox/Environments/Code/GetData/SocialEnvironmentalObservatoryDataList
cat .maintenance/QUICK_CHECK_PROMPT.md
```

**Copy the entire contents and paste into Claude Code**

The quick check will:
- Verify the 5 most important sources (NHGIS, CDC WONDER, EPA AQS, USGS NWIS, ERA5)
- Test sample URLs for broken links
- Search for major new data releases
- Create a brief status report

**Recommended schedule:** First week of each month

---

### Quarterly Comprehensive Update (2-4 hours)

Perform systematic review and update of all 200+ data sources:

```bash
cd /Users/davidlary/Dropbox/Environments/Code/GetData/SocialEnvironmentalObservatoryDataList
cat .maintenance/PERIODIC_UPDATE_PROMPT.md
```

**Copy the entire contents and paste into Claude Code**

The comprehensive update follows an 8-phase workflow:
1. **New Data Sources** - Federal/state/international agency releases
2. **Existing Source Updates** - Temporal coverage, new variables, access methods
3. **Data Quality & Accuracy** - Link verification, metadata updates, code testing
4. **Disease-Environment Associations** - Recent epidemiology literature
5. **Repository Optimization** - File size checks, cross-references, completeness
6. **Documentation Updates** - MASTER_INDEX, README, metadata files
7. **Git Documentation** - Comprehensive commit and changelog
8. **Final Verification** - Consistency checks, statistics, workflow testing

**Recommended schedule:** Quarterly (February, May, August, November)

---

### Maintenance Framework Documentation

Complete maintenance documentation is available in the `.maintenance/` directory:

- **PERIODIC_UPDATE_PROMPT.md** - Detailed 8-phase quarterly update instructions
- **QUICK_CHECK_PROMPT.md** - Monthly rapid health check protocol
- **README.md** - Maintenance best practices, schedule, troubleshooting
- **changelogs/** - Version history and update summaries

### Version History

| Update Date | Version | Major Changes |
|-------------|---------|---------------|
| 2025-11-13  | 4.0     | Initial comprehensive structure, NHGIS priority, asbestos, beach closures, maintenance framework |
| [Future]    | 4.1     | [Next quarterly update] |

**Next Scheduled Update:** February 2026

---

**Happy researching!** 🎉
