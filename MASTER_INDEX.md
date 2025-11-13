# MASTER INDEX - Complete Navigation Guide
## US County-Level Social and Environmental Health Observatory Data List

**Total Variables:** 43,000+
**Data Sources:** 200+ authoritative sources
**Files:** ~120 organized documentation files
**Version:** 4.0 (November 13, 2025)

---

## 📋 Quick Navigation

| Directory | Files | Variables | Description |
|-----------|-------|-----------|-------------|
| [00_METADATA](#00-metadata) | 6 | Essential | **⭐ NHGIS (priority)**, FIPS codes, boundaries, crosswalks, schedules |
| [01_AIR_ATMOSPHERE](#01-air--atmosphere) | 2 | 3,000+ | Criteria pollutants, HAPs, emissions, GHGs, aerosols |
| [02_WATER](#02-water) | 2 | 1,600+ | Water quality (1,300+ params), drinking water, **beach closures**, Superfund, UV |
| [03_LAND_SOIL_GEOLOGY](#03-land-soil--geology) | 3 | 600+ | Land cover, soils (227), topography, geology, **asbestos (876 sites)**, hydrology |
| [04_TOXIC_CHEMICALS](#04-toxic-chemicals) | 6 | 2,000+ | TRI (799), pesticides (650), Superfund, PFAS, lead |
| [05_RADIATION](#05-radiation) | 3 | 50+ | Radon, UV, nuclear facility proximity |
| [06_CLIMATE_WEATHER](#06-climate--weather) | 6 | 800+ | Temperature, precipitation, extremes, drought |
| [07_BUILT_ENVIRONMENT](#07-built-environment) | 6 | 200+ | Walkability, green space, housing, noise, light |
| [08_INFRASTRUCTURE](#08-infrastructure) | 5 | 150+ | Transportation, energy, dams, bridges, facilities |
| [09_OCCUPATIONAL](#09-occupational--industry) | 3 | 300+ | Employment by industry, injuries, composition |
| [10_AGRICULTURE_FOOD](#10-agriculture--food) | 6 | 18,000+ | Ag Census (6K), NASS (10K), food environment |
| [11_INFECTIOUS_DISEASE](#11-infectious-disease--vectors) | 3 | 100+ | Vector-borne, waterborne, STI/TB/hepatitis |
| [12_MORTALITY_DISEASE](#12-mortality--disease-outcomes) | 11 | 2,500+ | All-cause mortality, cancer, CVD, kidney, etc. |
| [13_HEALTH_STATUS](#13-health-status--behaviors) | 4 | 150+ | Chronic disease, risk factors, prevention |
| [14_HEALTHCARE_SYSTEM](#14-healthcare-system) | 6 | 9,000+ | HRSA AHRF (7K), Medicare (500+), hospitals |
| [15_DEMOGRAPHICS](#15-demographics--population) | 4 | 300+ | Age, sex, race, migration, urban/rural |
| [16_SOCIOECONOMIC](#16-socioeconomic) | 6 | 500+ | Income, employment, education, housing, inequality |
| [17_SOCIAL_DETERMINANTS](#17-social-determinants) | 6 | 300+ | Vulnerability, social capital, crime, safety net |
| [18_EDUCATION](#18-education--childcare) | 5 | 400+ | Schools (150+), districts (200+), outcomes |
| [19_ECONOMIC_INDICATORS](#19-economic-indicators) | 5 | 600+ | GDP, income sources, patents, businesses |
| [20_ENERGY_UTILITIES](#20-energy--utilities) | 5 | 100+ | Energy burden, reliability, renewables, broadband |
| [21_WILDFIRE_HAZARDS](#21-wildfire-hazards) | 4 | 80+ | Hazard potential, WUI, smoke, fire history |
| [22_FLOOD_HAZARDS](#22-flood-hazards) | 4 | 100+ | Coastal flooding, sea level rise, inland floods |
| [23_INTERNATIONAL_SOURCES](#23-international-sources-priority) | 8 | 500+ | ERA5 (240), CAMS, Copernicus, NASA, ESA |
| [24_COMPLETE_VARIABLE_CATALOGS](#24-complete-variable-catalogs-tier-2) | 11 | 27,000 | Exhaustive catalogs for sources >100 variables |
| [25_PAID_RESTRICTED_DATA](#25-paid--restricted-data) | 3 | 1,000+ | Commercial datasets, restricted-use files |

**TOTAL:** 62 comprehensive files documenting 43,000+ variables from 200+ sources

---

## 00_METADATA

**Essential reading BEFORE collecting any data**

| File | Purpose |
|------|---------|
| **⭐ NHGIS_COMPREHENSIVE_DOCUMENTATION.md** | **PRIORITY:** Pre-harmonized demographic, social, economic, housing data (1790-2024). 389 time series tables + 1,300+ ACS tables. Use FIRST for ANY demographic/socioeconomic data! |
| **FIPS_CODES_GEOGRAPHIC_IDENTIFIERS.md** | 5-digit FIPS codes, state/county codes, county names, independent cities, Alaska areas |
| **COUNTY_BOUNDARIES_REDISTRICTING.md** | Boundary changes, redistricting, merged/split counties, time series handling |
| **GEOGRAPHIC_CROSSWALKS.md** | ZIP→County, Tract→County, Place→County, CBSA, Congressional Districts, many-to-many relationships |
| **METADATA_FIPS_GEOGRAPHIC_CROSSWALKS.md** | Additional crosswalk reference and geographic identifier details |
| **TEMPORAL_COVERAGE_UPDATE_SCHEDULE.md** | Update frequency, release schedules, historical availability by source |

---

## 01_AIR & ATMOSPHERE

**3,000+ variables** | Criteria pollutants, toxic air, emissions, GHGs, aerosol composition

**Note:** These 2 comprehensive files consolidate all air quality data sources

| File | Variables | Key Sources Documented |
|------|-----------|------------------------|
| **TRI_COMPREHENSIVE_DOCUMENTATION.md** | 1,000+ | EPA TRI 799 chemicals, facility releases by medium (air/water/land), 1988-present |
| **ATMOSPHERIC_EMISSIONS_CHEMISTRY_COMPREHENSIVE.md** | 2,000+ | EPA AQS (PM2.5, PM10, O3, NO2, SO2, CO, HAPs), EPA NEI (200+ pollutants), CEMS hourly, IMPROVE aerosols, GHGs, wildfire smoke (NOAA HMS), NADP deposition |

---

## 02_WATER

**1,600+ variables** | Drinking, surface, groundwater quality; **beach closures**; hydrology

**Note:** These 2 comprehensive files consolidate all water quality data sources

| File | Variables | Key Sources Documented |
|------|-----------|------------------------|
| **USGS_Water_Quality_Parameters_County_Level_COMPREHENSIVE.md** | 1,300+ | USGS NWIS 1,300+ parameters (physical, chemical, biological), surface/groundwater, streamflow (1901+), HABs, watersheds, infrastructure |
| **UV_WATER_SUPERFUND_COMPREHENSIVE.md** | 300+ | EPA SDWIS drinking water (lead, arsenic, PFAS, nitrates), **EPA BEACON beach closures (6,000+ beaches, 2000-2024)**, EPA Superfund/NPL sites (1,343), NCI UV radiation (1961-2024) |

---

## 03_LAND, SOIL & GEOLOGY

**600+ variables** | High-resolution rasters require county aggregation; **asbestos occurrence**

**Note:** These 3 comprehensive files consolidate all land/soil/geology data sources

| File | Variables | Key Sources Documented |
|------|-----------|------------------------|
| **TOPOGRAPHY_GEOLOGY_SOILS_COMPREHENSIVE.md** | 350+ | USGS 3DEP 30m* DEM (elevation, slope, aspect, 25 derived metrics), NRCS SSURGO 10m* (227 soil properties), USGS geologic maps, **USGS Asbestos Occurrence (876 sites: 142 mines, 222 prospects, 512 natural)**, USGS Mineral Resources, USGS Karst mapping |
| **NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md** | 150+ | NLCD 30m* land cover (16 classes, 2001-2021), tree canopy, impervious surface, NOAA Storm Events (48 types, 1950+) |
| **HYDROLOGY_WETLANDS_FLOODPLAINS_COMPREHENSIVE.md** | 100+ | USGS HUC watersheds, USFWS National Wetlands Inventory, FEMA flood zones, stream networks, hydrologic characteristics |

*High-resolution raster - requires county aggregation (code examples provided)

---

## 04_TOXIC_CHEMICALS

**2,000+ variables** | TRI, pesticides, contaminated sites, emerging contaminants

| File | Variables | Key Sources |
|------|-----------|-------------|
| **TOXIC_RELEASE_INVENTORY.md** | 1,000+ | EPA TRI 799 chemicals, facilities, releases by medium (air/water/land), 1988-present |
| **PESTICIDES.md** | 700+ | USGS PNSP 650 compounds (insecticides, herbicides, fungicides, degradates), county-level 1992-2022 |
| **SUPERFUND_CONTAMINATED_SITES.md** | 50+ | EPA NPL sites (1,343), Brownfields, CERCLIS, site characteristics, contaminants |
| **HAZARDOUS_WASTE.md** | 100+ | EPA RCRAInfo facilities (800K+), waste types, violations, TSDFs |
| **PFAS_EMERGING_CONTAMINANTS.md** | 40+ | EPA UCMR5 29 PFAS (2023-2025), USGS PFAS monitoring, lithium |
| **LEAD_EXPOSURE.md** | 30+ | EPA lead paint pre-1978 housing, SDWIS lead violations, CDC childhood lead (state/county where available) |

---

## 05_RADIATION

**50+ variables** | Radon, UV, nuclear proximity

| File | Variables | Key Sources |
|------|-----------|-------------|
| **RADON.md** | 15+ | EPA radon zones, CDC radon testing rates, USGS geologic radon potential |
| **UV_RADIATION.md** | 20+ | NCI/CDC UV exposure 1961-2024, NASA OMI, NREL solar radiation |
| **NUCLEAR_FACILITIES.md** | 15+ | NRC operating reactors (93), proximity, emergency planning zones, capacity |

---

## 06_CLIMATE & WEATHER

**800+ variables** | Temperature, precipitation, extremes, drought

| File | Variables | Key Sources |
|------|-----------|-------------|
| **TEMPERATURE_PRECIPITATION.md** | 200+ | PRISM 4km* (1981+), Daymet 1km* (1980+), NCEI climate normals, station data (1895+) |
| **EXTREME_WEATHER_EVENTS.md** | 50+ | NOAA Storm Events 48 event types (1950-present): tornadoes, hail, flooding, etc. |
| **HEAT_COLD_EXPOSURE.md** | 100+ | CDC/NOAA HeatRisk (2024), NOAA UHI campaigns, temperature extremes, heating/cooling degree days |
| **DROUGHT_INDICES.md** | 30+ | NIDIS Drought Monitor, Palmer Drought Index, SPEI, SPI, soil moisture percentiles |
| **GRIDMET_METEOROLOGY.md** | 20+ | GRIDMET 4km* (1979+): wind, humidity, evapotranspiration, solar radiation, vapor pressure deficit |
| **CLIMATE_PROJECTIONS.md** | 400+ | LOCA downscaled CMIP models, future scenarios (RCP 4.5, 8.5), CONUS-wide county summaries |

*High-resolution grid - county aggregation required

---

## 07_BUILT_ENVIRONMENT

**200+ variables** | Walkability, green space, housing, noise, light

| File | Variables | Key Sources |
|------|-----------|-------------|
| **LAND_DEVELOPMENT_URBANIZATION.md** | 30+ | NLCD developed land classes (21-24), impervious surface change, urban growth |
| **WALKABILITY_TRANSPORTATION_ACCESS.md** | 100+ | EPA Smart Location Database 90+ indicators (2019): walkability, transit, employment access |
| **GREEN_SPACE_PARKS.md** | 30+ | USDA tree canopy (2011/2016/2021/2024), NASA NDVI (HLS daily 2013+), park access |
| **HOUSING_CHARACTERISTICS.md** | 40+ | HUD data, Census housing stock, building permits (1980-2024), age, quality |
| **NOISE_POLLUTION.md** | 20+ | BTS National Transportation Noise Map (2014): aviation DNL, highway, rail |
| **LIGHT_POLLUTION.md** | 15+ | VIIRS nighttime lights (2012-present monthly), DMSP harmonized (1992-2024 33-year series) |

---

## 08_INFRASTRUCTURE

**150+ variables** | Transportation, energy, dams, bridges, critical facilities

| File | Variables | Key Sources |
|------|-----------|-------------|
| **TRANSPORTATION_INFRASTRUCTURE.md** | 40+ | FHWA HPMS traffic (AADT, VMT 1980s-present), National Bridge Inventory (617K+ bridges), road networks |
| **ENERGY_INFRASTRUCTURE.md** | 50+ | eGRID power plants, EIA-860 generators, pipelines, transmission lines, USGS wind turbines (74K+) |
| **DAMS_WATER_INFRASTRUCTURE.md** | 30+ | USACE NID 91,457 dams (hazard, condition, age, storage), wastewater treatment plants |
| **WASTE_FACILITIES.md** | 20+ | EPA LMOP landfills (2,600 MSW), RCRA hazardous waste facilities |
| **CRITICAL_FACILITIES.md** | 20+ | HIFLD: hospitals, fire stations, police, schools, emergency shelters |

---

## 09_OCCUPATIONAL & INDUSTRY

**300+ variables** | Employment by industry, injuries, composition

| File | Variables | Key Sources |
|------|-----------|-------------|
| **EMPLOYMENT_BY_INDUSTRY.md** | 200+ | CBP/QCEW by NAICS (establishments, employment, payroll), 1990-present |
| **OCCUPATIONAL_INJURIES.md** | 50+ | OSHA injuries/illnesses (2016-present), BLS fatal injuries, workers' compensation |
| **INDUSTRY_COMPOSITION.md** | 100+ | Manufacturing, agriculture, mining, construction, services - economic structure |

---

## 10_AGRICULTURE & FOOD

**18,000+ variables** | Comprehensive agricultural production + food environment

| File | Variables | Key Sources |
|------|-----------|-------------|
| **AGRICULTURAL_PRODUCTION_CROPS.md** | 3,000+ | Census of Agriculture (77 tables), NASS crop surveys (area, production, value) |
| **AGRICULTURAL_PRODUCTION_LIVESTOCK.md** | 2,000+ | Census + NASS livestock surveys (inventory, sales, products) |
| **AGRICULTURAL_ECONOMICS_PRACTICES.md** | 1,500+ | Farm economics, expenses, income, conservation, organic, demographics |
| **AGRICULTURAL_INPUTS.md** | 500+ | Fertilizer, pesticides (application), irrigation, energy use |
| **FOOD_ENVIRONMENT_ACCESS.md** | 50+ | USDA Food Atlas, SNAP retailers, farmers markets, food deserts |
| **FOOD_INSECURITY_NUTRITION.md** | 30+ | Feeding America (2001-present by subpopulation), WIC, school meals |

---

## 11_INFECTIOUS_DISEASE & VECTORS

**100+ variables** | Vector-borne, waterborne, STI/TB/viral hepatitis

| File | Variables | Key Sources |
|------|-----------|-------------|
| **VECTOR_BORNE_DISEASES.md** | 50+ | CDC ArboNET: West Nile (2003+), Lyme (1992+), dengue, Zika, ehrlichiosis, anaplasmosis |
| **WATERBORNE_DISEASE_RISK.md** | 20+ | Cryptosporidiosis, giardiasis, legionellosis outbreaks, recreational water illness |
| **STI_TB_VIRAL_HEPATITIS.md** | 40+ | CDC AtlasPlus: syphilis, gonorrhea, chlamydia, HIV/AIDS, TB, hepatitis A/B/C (1996-present) |

---

## 12_MORTALITY & DISEASE OUTCOMES

**2,500+ variables** | All-cause and disease-specific mortality, registries

| File | Variables | Key Sources |
|------|-----------|-------------|
| **MORTALITY_ALL_CAUSES.md** | 1,000+ | CDC WONDER all ICD-10 codes (1999-present), age/sex/race stratified, 113 selected causes detailed |
| **CANCER_INCIDENCE_SURVIVAL.md** | 1,000+ | SEER 1,000+ site/histology types (1975-present), incidence, survival, stage, grade |
| **CARDIOVASCULAR_OUTCOMES.md** | 150+ | Mortality (ICD-10), Medicare prevalence (IHD, HF, stroke, hypertension, AFib) |
| **RESPIRATORY_DISEASE.md** | 100+ | COPD, asthma prevalence (CDC PLACES), mortality, pneumonia, interstitial lung disease |
| **KIDNEY_DISEASE.md** | 500+ | USRDS: CKD stages 1-5, ESRD incidence/prevalence (1978-present), dialysis, transplant, outcomes |
| **DIABETES_METABOLIC.md** | 80+ | CDC PLACES diabetes prevalence, mortality, obesity, metabolic syndrome |
| **NEUROLOGICAL_DEMENTIA.md** | 50+ | Alzheimer's/dementia mortality, Parkinson's mortality, ALS (limited county data) |
| **MENTAL_HEALTH_SUICIDE.md** | 60+ | Suicide mortality (method, intent), CDC PLACES depression, Medicare mental health prevalence |
| **LIVER_DISEASE.md** | 30+ | Cirrhosis mortality, chronic liver disease, hepatocellular carcinoma, hepatitis-related |
| **BIRTH_OUTCOMES.md** | 50+ | CDC Natality (1995-2024): births, preterm, low birth weight, breastfeeding, maternal characteristics |
| **BIRTH_DEFECTS_DEVELOPMENTAL.md** | 30+ | State birth defects registries (county-level where available), neural tube, cardiac, etc. |

---

## 13_HEALTH_STATUS & BEHAVIORS

**150+ variables** | Chronic disease prevalence, risk factors, prevention

| File | Variables | Key Sources |
|------|-----------|-------------|
| **CHRONIC_DISEASE_PREVALENCE.md** | 70 | CDC PLACES (2019-present): 36 chronic conditions, 13 prevention, 9 behaviors, 4 status, 8 disability |
| **HEALTH_BEHAVIORS_RISK_FACTORS.md** | 50+ | NCI smoking (1997-2023), physical activity, diet quality, obesity, binge drinking |
| **PREVENTIVE_CARE.md** | 30+ | Cancer screenings, immunizations, routine checkups, dental visits |
| **DISABILITY_FUNCTIONAL_STATUS.md** | 20+ | Hearing, vision, cognition, ambulatory, self-care, independent living difficulty |

---

## 14_HEALTHCARE_SYSTEM

**9,000+ variables** | Workforce, facilities, shortage areas, utilization

| File | Variables | Key Sources |
|------|-----------|-------------|
| **HEALTH_WORKFORCE.md** | 1,500+ | HRSA AHRF: physicians by specialty, nurses, dentists, allied health professions (1946-present for some) |
| **HEALTH_FACILITIES.md** | 1,000+ | HRSA AHRF: hospitals, clinics, FQHCs, nursing homes, dialysis centers, mental health facilities |
| **HEALTH_PROFESSIONAL_SHORTAGE_AREAS.md** | 200+ | HRSA HPSA designations (primary care, dental, mental health), MUA/MUP, scores |
| **MEDICARE_UTILIZATION_SPENDING.md** | 500+ | CMS 67 chronic conditions, spending, hospitalizations, readmissions, quality measures |
| **HOSPITAL_CHARACTERISTICS_QUALITY.md** | 200+ | CMS Hospital Compare, bed counts, services, quality ratings, safety scores |
| **NURSING_HOMES.md** | 100+ | CMS Nursing Home Compare (2009+): quality ratings, staffing, deficiencies, resident characteristics |

---

## 15_DEMOGRAPHICS & POPULATION

**300+ variables** | Age, sex, race, migration, urban/rural

| File | Variables | Key Sources |
|------|-----------|-------------|
| **POPULATION_AGE_SEX_RACE.md** | 150+ | Census Decennial + ACS + PEP: total population, age groups, sex, race/ethnicity, households |
| **MIGRATION_MOBILITY.md** | 80+ | IRS county-to-county migration flows (1990-2022), ACS geographic mobility, net migration |
| **URBAN_RURAL.md** | 30+ | USDA ERS Rural-Urban Continuum Codes, Urban Influence Codes, RUCA codes, Census urban/rural |
| **POPULATION_PROJECTIONS.md** | 50+ | Census population projections, cohort-component methods, fertility/mortality assumptions |

---

## 16_SOCIOECONOMIC

**500+ variables** | Income, employment, education, housing, inequality

| File | Variables | Key Sources |
|------|-----------|-------------|
| **INCOME_POVERTY.md** | 150+ | ACS median income, per capita income, poverty by age, SAIPE, BEA personal income |
| **EMPLOYMENT_UNEMPLOYMENT.md** | 100+ | BLS LAUS monthly unemployment (1990-present), labor force, employment/population ratio |
| **EDUCATION_ATTAINMENT.md** | 80+ | ACS educational attainment (less than HS through graduate degree), enrollment |
| **HOUSING_AFFORDABILITY.md** | 100+ | HUD CHAS cost burden, HUD FMR by bedroom (1983-present), evictions (Eviction Lab), FHFA HPI |
| **INEQUALITY_MOBILITY.md** | 40+ | Gini index, income quintiles, Opportunity Insights economic mobility, absolute mobility |
| **WEALTH_DEBT.md** | 50+ | Federal Reserve household debt (1999-2025 quarterly), IRS tax data (AGI, deductions 1989-2022) |

---

## 17_SOCIAL_DETERMINANTS

**300+ variables** | Vulnerability, social capital, crime, safety net

| File | Variables | Key Sources |
|------|-----------|-------------|
| **SOCIAL_VULNERABILITY.md** | 20+ | CDC SVI 15 variables across 4 themes (2000-2020 decadal), overall vulnerability ranking |
| **SOCIAL_CAPITAL.md** | 30+ | Penn State Social Capital Index, religious congregations (ASARB 372 denominations), civic organizations |
| **CRIME_SAFETY.md** | 100+ | FBI UCR/NIBRS: violent crime, property crime, hate crimes by bias motivation, arrests |
| **SUBSTANCE_OUTLETS.md** | 40+ | Alcohol outlets, tobacco retailers, firearms dealers (FFLs), cannabis dispensaries |
| **SAFETY_NET_PROGRAMS.md** | 80+ | SNAP (participants, stores), Medicaid enrollment, TANF, SSI, SSDI, Social Security, UI, WIC |
| **COMMUNITY_RESOURCES.md** | 40+ | IMLS libraries (1992-2022), recreation facilities, community centers, parks, museums |

---

## 18_EDUCATION & CHILDCARE

**400+ variables** | Schools, districts, outcomes, higher education

| File | Variables | Key Sources |
|------|-----------|-------------|
| **SCHOOLS_DISTRICTS.md** | 150+ | NCES CCD: enrollment by grade/race, teachers, student/teacher ratio, Title I, magnet/charter (1986+) |
| **SCHOOL_FINANCE.md** | 200+ | NCES F-33 school district finance: revenue by source, expenditures by function, per-pupil spending |
| **EDUCATIONAL_OUTCOMES.md** | 50+ | Stanford SEDA achievement (2009-2018), graduation rates, test scores, learning rates, achievement gaps |
| **COLLEGES_UNIVERSITIES.md** | 100+ | NCES IPEDS: enrollment, completion, faculty, finance, Carnegie classification |
| **CHILDCARE_AVAILABILITY.md** | 20+ | State childcare licensing databases (county-level where available), capacity, quality ratings |

---

## 19_ECONOMIC_INDICATORS

**600+ variables** | GDP, income sources, patents, businesses

| File | Variables | Key Sources |
|------|-----------|-------------|
| **GDP_ECONOMIC_OUTPUT.md** | 100+ | BEA CAGDP: real/nominal GDP, GDP by industry (NAICS), growth rates (2001-present) |
| **INCOME_BY_SOURCE.md** | 200+ | BEA CAINC tables: wages/salaries, dividends/interest/rent, transfer payments, farm income, contributions |
| **PATENTS_INNOVATION.md** | 50+ | USPTO patents by inventor location (1975-2020), utility/design/plant patents, technology classes |
| **BUSINESS_ESTABLISHMENTS.md** | 200+ | CBP/QCEW: establishments by size class, industry, business dynamics (births/deaths), Kauffman Index |
| **BANKRUPTCY_DEBT.md** | 50+ | Federal bankruptcy filings by district/county (2007+), Chapter 7/11/13, business/consumer |

---

## 20_ENERGY & UTILITIES

**100+ variables** | Energy burden, reliability, renewables, broadband

| File | Variables | Key Sources |
|------|-----------|-------------|
| **ENERGY_CONSUMPTION.md** | 30+ | EIA SEDS state-level (allocate to counties via methods), residential/commercial/industrial/transportation |
| **ENERGY_BURDEN_AFFORDABILITY.md** | 20+ | DOE LEAD Tool (2022): energy costs by fuel, burden by income (AMI/FPL/SMI), housing characteristics |
| **ELECTRICITY_RELIABILITY.md** | 15+ | EIA Form 861 (2013-present): SAIFI/SAIDI/CAIDI outage metrics by utility, map to counties |
| **RENEWABLE_ENERGY.md** | 30+ | USGS wind turbines 74K+ locations, NREL solar installations, EIA renewable generation |
| **BROADBAND_CONNECTIVITY.md** | 20+ | FCC Broadband Data Collection (June 2024): availability by technology/speed, census block aggregation |

---

## 21_WILDFIRE_HAZARDS

**80+ variables** | Hazard potential, WUI, smoke, fire history

| File | Variables | Key Sources |
|------|-----------|-------------|
| **WILDFIRE_HAZARD_POTENTIAL.md** | 10+ | USFS WHP 270m (2020): continuous index, 5 classes, mean/max by county |
| **WILDLAND_URBAN_INTERFACE.md** | 40+ | SILVIS WUI (1990, 2000, 2010, 2020): population/housing in WUI, interface vs. intermix, change |
| **WILDFIRE_SMOKE.md** | 20+ | NOAA HMS smoke plumes (2005-present daily): smoke days, density, PM2.5 attribution |
| **FIRE_HISTORY.md** | 20+ | MTBS burned area (1984-present), fire perimeters, severity, FIRED daily burned area |

---

## 22_FLOOD_HAZARDS

**100+ variables** | Coastal flooding, sea level rise, inland floods

| File | Variables | Key Sources |
|------|-----------|-------------|
| **COASTAL_FLOODING_SEA_LEVEL_RISE.md** | 50+ | NOAA SLR scenarios 0-10 ft (1-ft increments): inundation area, population exposure, infrastructure |
| **INLAND_FLOODING.md** | 30+ | FEMA NFHL flood zones (100/500-year), floodplain area, FEMA claims history, flood risk |
| **STORM_SURGE.md** | 10+ | NOAA SLOSH models, hurricane storm surge risk, coastal vulnerability |
| **COASTAL_EROSION.md** | 15+ | USGS coastal change, shoreline erosion rates, barrier island dynamics |

---

## 23_INTERNATIONAL_SOURCES (PRIORITY)

**500+ variables** | ECMWF, Copernicus, NASA, ESA - highest resolution global data

| File | Variables | Key Sources |
|------|-----------|-------------|
| **ECMWF_ERA5_REANALYSIS.md** ⭐⭐⭐ | 240 | **HIGHEST PRIORITY:** Atmospheric (temp, pressure, wind, precip), land surface (soil moisture 4 layers, snow, vegetation), radiation, evaporation - 31km hourly 1940-present |
| **ECMWF_ERA5_LAND.md** | 50+ | Enhanced land surface reanalysis 11km (1950-present): soil temp/moisture, snow, runoff, ET |
| **CAMS_ATMOSPHERIC_COMPOSITION.md** ⭐⭐⭐ | 100+ | **HIGHEST PRIORITY:** GHGs (CO2, CH4, N2O), reactive gases (O3, NO2, SO2, CO, HCHO), aerosols by species (sulfate, nitrate, BC, OC, dust, sea salt) - 44km 2003-present |
| **COPERNICUS_SERVICES.md** | 80+ | Atmosphere Monitoring, Land Monitoring, Marine, Climate Change services |
| **NASA_EARTH_OBSERVATIONS.md** | 100+ | MODIS (vegetation, fire, aerosols), VIIRS (nighttime lights, fire), OMI/TROPOMI (air quality) |
| **ESA_SENTINEL_SATELLITES.md** | 50+ | Sentinel-5P TROPOMI air quality (NO2, SO2, CO, HCHO, aerosols), Sentinel-2 land cover |
| **NASA_SEDAC_GRIDDED_POPULATION.md** | 40+ | GPW ~1km population density (2000-2025 5-year), urban extents, poverty mapping |
| **OTHER_INTERNATIONAL_SOURCES.md** | 50+ | World Bank indicators, OECD regional statistics, WHO (if US county-level coverage exists) |

**Why International Sources?**
- Longer time series (ERA5: 1940-present vs. most US sources 1980+)
- Higher temporal resolution (ERA5: hourly vs. daily)
- Consistent global methodology (no state boundaries)
- Gap-filling where US monitoring sparse (CAMS)
- Independent verification (satellite data)

---

## 24_COMPLETE_VARIABLE_CATALOGS (Tier 2)

**27,000 variables** | Exhaustive searchable catalogs for sources >100 variables

| File | Variables | Description |
|------|-----------|-------------|
| **EPA_TRI_COMPLETE_CHEMICAL_LIST.md** | 799 | All TRI-reportable chemicals: CAS numbers, formulas, year added, thresholds (alphabetized) |
| **EPA_NEI_COMPLETE_POLLUTANT_CODES.md** | 200+ | All NEI pollutant codes + SCC source categories |
| **NRCS_SSURGO_COMPLETE_SOIL_PROPERTIES.md** | 227 | All SSURGO properties: physical, chemical, water, interpretations |
| **ERA5_COMPLETE_VARIABLE_CATALOG.md** | 240 | All ERA5 atmospheric + land + ocean variables with codes, units, levels |
| **USGS_PESTICIDES_COMPLETE_COMPOUND_LIST.md** | 650 | All pesticides: insecticides, herbicides, fungicides, degradates, CAS, classes |
| **USRDS_KIDNEY_COMPLETE_VARIABLE_CATALOG.md** | 500+ | All kidney disease variables: incidence, prevalence, treatment, outcomes by year |
| **SEER_CANCER_COMPLETE_SITE_HISTOLOGY_CATALOG.md** | 1,000+ | All cancer site/histology ICD-O-3 codes: primary site, histology, behavior, grade, stage |
| **USGS_NWIS_COMPLETE_PARAMETER_CODES.md** | 1,300+ | All NWIS parameter codes: physical, chemical, biological, field measurements with units |
| **USDA_AG_CENSUS_COMPLETE_TABLES.md** | 6,000+ | All 77 Census of Agriculture tables with every variable documented |
| **HRSA_AHRF_COMPLETE_VARIABLE_CATALOG.md** | 6,000+ | All AHRF variables: professions, facilities, HPSAs, health status, socioeconomics |
| **USDA_NASS_QUICKSTATS_COMPLETE_VARIABLE_CATALOG.md** | 10,000+ | All NASS QuickStats: Census, surveys, prices - complete query structure |

---

## 25_PAID & RESTRICTED DATA

**1,000+ variables** | Commercial datasets, restricted-use files

| File | Variables | Description |
|------|-----------|-------------|
| **COMMERCIAL_DATASETS.md** | 500+ | AHA Annual Survey of Hospitals (1946-2023, $3K+/year), CoreLogic land ownership, Regrid parcels |
| **RESTRICTED_USE_FILES.md** | 300+ | NCHS restricted mortality, Census protected microdata, NHANES county identifiers |
| **PROPRIETARY_HEALTH_DATA.md** | 300+ | Commercial insurance claims, electronic health records (aggregated), pharmacy data |

---

## 🔍 How to Use This Index

### For Comprehensive Data Collection
1. Start with **00_METADATA** to understand FIPS codes and county boundaries
2. Review all directories 01-23 for relevant domains
3. Use Tier 2 catalogs (24) for exhaustive variable lists
4. Check 25 if research requires paid data

### For Specific Research Questions
1. Use table above to identify relevant directories
2. Read 2-3 files at a time (context-efficient)
3. Follow code examples in each file
4. Cross-reference related domains

### For International/High-Resolution Data
1. **Priority:** 23_INTERNATIONAL_SOURCES for ERA5/CAMS
2. Files marked with * = high-resolution rasters requiring county aggregation
3. Code examples show aggregation methods

---

## 📊 Variable Count by Theme

| Theme | Variables | Top Sources |
|-------|-----------|-------------|
| **Agriculture** | 18,000+ | NASS QuickStats (10K), Ag Census (6K) |
| **Healthcare System** | 9,000+ | HRSA AHRF (7K), CMS Medicare (500+) |
| **Air Quality** | 3,000+ | EPA AQS, NEI, CEMS, IMPROVE |
| **Mortality/Disease** | 2,500+ | CDC WONDER (all ICD-10), SEER (1K), USRDS (500) |
| **Toxic Chemicals** | 2,000+ | EPA TRI (799), USGS Pesticides (650) |
| **Water Quality** | 1,500+ | USGS NWIS (1,300+), EPA SDWIS |
| **Climate/Weather** | 800+ | ERA5 (240), PRISM, Daymet, GRIDMET, NCEI |
| **Economic** | 600+ | BEA (GDP, income), CBP/QCEW, USPTO |
| **International** | 500+ | ERA5, CAMS, Copernicus, NASA, ESA |
| **Land/Soil/Geology** | 500+ | NLCD, SSURGO (227), 3DEP, USGS geology |
| **Socioeconomic** | 500+ | Census, ACS, BLS, IRS, HUD |
| **Education** | 400+ | NCES CCD, finance, SEDA, IPEDS |
| **Demographics** | 300+ | Census, PEP, IRS migration |
| **Social Determinants** | 300+ | CDC SVI, social capital, crime, safety net |
| **Occupational** | 300+ | CBP/QCEW NAICS, OSHA injuries |
| **Infrastructure** | 150+ | NBI bridges, NID dams, HIFLD, eGRID |
| **Health Status** | 150+ | CDC PLACES (70), NCI smoking, behaviors |
| **Built Environment** | 200+ | Smart Location DB (90+), green space, noise, light |
| **Infectious Disease** | 100+ | Vector-borne, waterborne, STI/TB/hepatitis |
| **Energy/Utilities** | 100+ | DOE LEAD, EIA reliability, FCC broadband |
| **Flood Hazards** | 100+ | NOAA SLR, FEMA NFHL, storm surge |
| **Wildfire** | 80+ | WHP, WUI, HMS smoke, MTBS |
| **Radiation** | 50+ | Radon, UV, nuclear |

**TOTAL: 43,000+ variables**

---

## 📧 Questions & Updates

For questions about specific data sources, navigation, or to suggest additions:
- Review individual domain files for detailed documentation
- Check Tier 2 catalogs for exhaustive variable lists
- Consult metadata files for geographic identifiers and boundaries

**Last Updated:** November 13, 2025
**Version:** 4.0 - Systematic Disease-Environment Organization
