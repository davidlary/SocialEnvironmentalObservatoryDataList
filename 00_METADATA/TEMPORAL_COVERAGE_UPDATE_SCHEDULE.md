# Temporal Coverage & Update Schedule
## Data Release Frequencies and Historical Availability

**Purpose:** Understand when data sources are updated and what historical coverage is available.

**Critical for:**
- Planning data collection schedules
- Understanding data lag times
- Knowing when to check for updates
- Identifying longest available time series

---

## 📅 Update Frequency Categories

### Real-Time / Daily
- Updated continuously or every day
- Typical lag: 0-1 days

### Weekly / Bi-Weekly
- Updated every 1-2 weeks
- Typical lag: 1-14 days

### Monthly
- Updated every month
- Typical lag: 1-3 months

### Quarterly
- Updated every 3 months (Q1, Q2, Q3, Q4)
- Typical lag: 1-6 months

### Annual
- Updated once per year
- Typical lag: 3-24 months

### Biennial / Multi-Year
- Updated every 2-5 years
- Typical lag: Varies

### Decadal
- Updated every 10 years (Census years)
- Typical lag: 1-2 years after Census

---

## 🌍 INTERNATIONAL SOURCES (HIGHEST PRIORITY)

### ECMWF ERA5 Reanalysis ⭐⭐⭐
- **Update Frequency:** Near real-time (3-5 day lag for preliminary, 2-3 month lag for final)
- **Temporal Coverage:** **1940-present** (84 years!)
- **Temporal Resolution:** Hourly
- **Longest climate time series available**
- **Access:** Copernicus Climate Data Store (free)
- **Update Schedule:** Continuous

### ECMWF CAMS Atmospheric Composition ⭐⭐⭐
- **Update Frequency:** Near real-time (1-2 day lag)
- **Temporal Coverage:** 2003-present
- **Temporal Resolution:** Hourly/3-hourly
- **Access:** Copernicus Atmosphere Data Store (free)

### NASA Earth Observations
- **MODIS:** 2000-present, daily
- **VIIRS:** 2012-present, daily
- **OMI/TROPOMI (Sentinel-5P):** 2004-present (OMI), 2018-present (TROPOMI), daily

### NASA SEDAC Gridded Population
- **Update Frequency:** Every 5 years
- **Temporal Coverage:** 2000, 2005, 2010, 2015, 2020, 2025 (projected)
- **Access:** Free download

---

## 🌤️ AIR QUALITY & ATMOSPHERIC

### EPA Air Quality System (AQS) - Criteria Pollutants
- **Update Frequency:** Daily (raw data), annual (validated data)
- **Temporal Coverage:** 1980-present (PM2.5: 1999-present)
- **Data Lag:** ~6-12 months for finalized annual data
- **Access:** EPA AQS API, AirData downloads

### EPA National Emissions Inventory (NEI)
- **Update Frequency:** Triennial (every 3 years: 2017, 2020, 2023...)
- **Temporal Coverage:** 1990-present
- **Data Lag:** ~2-3 years (2020 NEI published in 2023)
- **Access:** EPA NEI website

### EPA Continuous Emissions Monitoring System (CEMS)
- **Update Frequency:** Quarterly
- **Temporal Coverage:** 1995-present
- **Temporal Resolution:** Hourly
- **Access:** EPA CAMD API

### IMPROVE Network (Aerosol Composition)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1988-present
- **Access:** http://vista.cira.colostate.edu/Improve/

### NOAA HMS Wildfire Smoke
- **Update Frequency:** Daily
- **Temporal Coverage:** 2005-present
- **Access:** NOAA HMS archive

---

## 💧 WATER QUALITY

### USGS NWIS (Water Quality)
- **Update Frequency:** Continuous (as samples collected)
- **Temporal Coverage:** 1901-present (varies by site)
- **Typical Lag:** 1-3 months for lab results
- **Access:** USGS NWIS web services API

### EPA SDWIS (Drinking Water Violations)
- **Update Frequency:** Quarterly
- **Temporal Coverage:** 1993-present
- **Data Lag:** ~3-6 months
- **Access:** EPA SDWIS downloads

### EPA UCMR5 (PFAS Monitoring)
- **Update Frequency:** Ongoing (monitoring period 2023-2025)
- **Temporal Coverage:** 2023-2025
- **Data Lag:** ~3-6 months
- **Access:** EPA UCMR website

---

## 🌾 LAND COVER & SOILS

### NLCD (National Land Cover Database)
- **Update Frequency:** Every 2-3 years
- **Temporal Coverage:** 2001, 2004, 2006, 2008, 2011, 2013, 2016, 2019, 2021
- **Data Lag:** ~2-3 years
- **Access:** MRLC.gov

### NRCS SSURGO (Soils)
- **Update Frequency:** Annual updates
- **Temporal Coverage:** Current (not time series)
- **Access:** NRCS Web Soil Survey

### USGS 3DEP (Elevation)
- **Update Frequency:** Ongoing (as new lidar collected)
- **Temporal Coverage:** Current (snapshots)
- **Access:** USGS National Map

---

## ☠️ TOXIC CHEMICALS

### EPA TRI (Toxic Release Inventory)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1988-present
- **Data Lag:** ~18 months (2023 data available mid-2025)
- **Reporting Year:** Calendar year
- **Access:** EPA TRI Explorer, bulk downloads

### USGS Pesticides (PNSP)
- **Update Frequency:** Every 10 years (major reports)
- **Temporal Coverage:** 1992, 2002, 2012, 2022
- **Data Lag:** ~2-3 years
- **Access:** USGS NAWQA reports

---

## ☀️ RADIATION

### EPA Radon
- **Update Frequency:** Static (radon zones)
- **Temporal Coverage:** Current

### NCI/CDC UV Exposure
- **Update Frequency:** Annual
- **Temporal Coverage:** 1961-2024
- **Access:** NCI website

---

## 🌡️ CLIMATE & WEATHER

### PRISM Climate Data
- **Update Frequency:** Monthly (provisional), annual (stable)
- **Temporal Coverage:** 1981-present
- **Temporal Resolution:** Daily, monthly, annual
- **Access:** PRISM Climate Group (Oregon State)

### Daymet
- **Update Frequency:** Annual
- **Temporal Coverage:** 1980-present
- **Access:** ORNL DAAC

### GRIDMET
- **Update Frequency:** Weekly
- **Temporal Coverage:** 1979-present
- **Access:** Climatology Lab (UC Merced)

### NOAA Storm Events Database
- **Update Frequency:** Monthly
- **Temporal Coverage:** 1950-present (tornadoes); 1996-present (all 48 event types)
- **Data Lag:** ~1-3 months
- **Access:** NOAA NCEI Storm Events

### NIDIS Drought Monitor
- **Update Frequency:** Weekly
- **Temporal Coverage:** 2000-present
- **Access:** drought.gov

---

## 🏥 MORTALITY & DISEASE

### CDC WONDER Mortality
- **Update Frequency:** Annual
- **Temporal Coverage:** 1999-present (current ICD-10); 1968-1998 (ICD-9, separate)
- **Data Lag:** ~12-18 months (2023 data available mid-2025)
- **Access:** CDC WONDER online database

### CDC PLACES (Chronic Disease Prevalence)
- **Update Frequency:** Annual
- **Temporal Coverage:** 2019-present
- **Data Lag:** ~12 months
- **Model Year:** Rolling (incorporates 2-3 years BRFSS data)
- **Access:** CDC PLACES website

### SEER Cancer Incidence
- **Update Frequency:** Annual
- **Temporal Coverage:** 1975-present
- **Data Lag:** ~24 months (2022 data available late 2024)
- **Access:** SEER*Stat, SEER API

### USRDS Kidney Disease
- **Update Frequency:** Annual
- **Temporal Coverage:** 1978-present
- **Data Lag:** ~18-24 months
- **Access:** USRDS Annual Data Report

### CDC Natality (Birth Data)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1995-present (revised birth certificate); 1968-2002 (old certificate)
- **Data Lag:** ~12-18 months
- **Access:** CDC WONDER Natality

### CDC ArboNET (Vector-Borne Diseases)
- **Update Frequency:** Annual
- **Temporal Coverage:** West Nile (2003-present), Lyme (1992-present)
- **Data Lag:** ~12 months
- **Access:** CDC ArboNET downloads

---

## 🏥 HEALTHCARE SYSTEM

### HRSA AHRF (Area Health Resources Files)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1946-present (for some variables), most 1980-present
- **Data Lag:** ~12-18 months
- **Access:** HRSA Data Warehouse (free download)

### CMS Medicare Geographic Variation
- **Update Frequency:** Annual
- **Temporal Coverage:** 2007-present (chronic conditions); earlier for utilization
- **Data Lag:** ~18-24 months
- **Access:** CMS website

### CMS Hospital Compare
- **Update Frequency:** Quarterly
- **Temporal Coverage:** 2005-present
- **Access:** data.cms.gov

---

## 👥 DEMOGRAPHICS & POPULATION

### Census Decennial
- **Update Frequency:** Every 10 years (2000, 2010, 2020, 2030...)
- **Temporal Coverage:** 1790-2020
- **Data Lag:** ~1-2 years (2020 data released 2021-2022)
- **Access:** data.census.gov

### Census ACS (American Community Survey)
- **Update Frequency:** Annual (1-year and 5-year estimates)
- **Temporal Coverage:** 2005-present (5-year); 2006-present (1-year for pop >65K)
- **Data Lag:** ~9-12 months (2023 data available late 2024)
- **Access:** data.census.gov

### Census PEP (Population Estimates Program)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1970-present
- **Data Lag:** ~6-9 months
- **Access:** Census website

---

## 💰 ECONOMIC DATA

### BEA County Economic Data (CAINC, CAGDP)
- **Update Frequency:** Annual
- **Temporal Coverage:**
  - Personal income (CAINC): 1969-present
  - GDP (CAGDP): 2001-present
- **Data Lag:** ~9-12 months
- **Access:** BEA API

### BLS LAUS (Unemployment)
- **Update Frequency:** Monthly
- **Temporal Coverage:** 1990-present
- **Data Lag:** ~1-2 months
- **Access:** BLS API

### Census CBP / BLS QCEW (Employment by Industry)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1986-present (CBP), 1975-present (QCEW)
- **Data Lag:** ~12-18 months
- **Access:** Census CBP, BLS QCEW downloads

---

## 🌾 AGRICULTURE

### USDA Census of Agriculture
- **Update Frequency:** Every 5 years (1997, 2002, 2007, 2012, 2017, 2022...)
- **Temporal Coverage:** 1840-present (modern comprehensive: 1997-present)
- **Data Lag:** ~18-24 months (2022 data released 2024)
- **Access:** USDA NASS QuickStats

### USDA NASS Surveys
- **Update Frequency:**
  - Crop surveys: Annual, monthly, weekly (varies by commodity)
  - Livestock surveys: Annual, quarterly
  - Prices: Monthly
- **Temporal Coverage:** Varies by survey (some back to 1866!)
- **Data Lag:** ~1-6 months
- **Access:** USDA NASS QuickStats API

---

## 🏠 HOUSING & SOCIAL

### HUD Fair Market Rents (FMR)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1983-present
- **Data Lag:** Published ~October for following fiscal year
- **Access:** HUD User website

### HUD CHAS (Housing Affordability)
- **Update Frequency:** Annual (based on ACS 5-year estimates)
- **Temporal Coverage:** 2006-present
- **Data Lag:** ~2 years (based on ACS)
- **Access:** HUD User website

### Eviction Lab
- **Update Frequency:** Varies (historical dataset complete; real-time tracker updates weekly)
- **Temporal Coverage:** 2000-2018 (historical); 2020-present (real-time tracker)
- **Access:** evictionlab.org

---

## 🎓 EDUCATION

### NCES Common Core of Data (CCD)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1986-present
- **Data Lag:** ~12-18 months
- **Access:** NCES data portal

### NCES School Finance
- **Update Frequency:** Annual
- **Temporal Coverage:** 1992-present (F-33); earlier data available
- **Data Lag:** ~18-24 months
- **Access:** NCES data portal

### Stanford SEDA
- **Update Frequency:** Updated irregularly (major releases every few years)
- **Temporal Coverage:** 2009-2018 (current version)
- **Access:** edopportunity.org

---

## 🔥 WILDFIRE & HAZARDS

### USFS Wildfire Hazard Potential (WHP)
- **Update Frequency:** Every ~5 years
- **Temporal Coverage:** 2014, 2020 (next: 2025 expected)
- **Access:** USFS website

### SILVIS WUI (Wildland-Urban Interface)
- **Update Frequency:** Decadal (aligned with Census)
- **Temporal Coverage:** 1990, 2000, 2010, 2020
- **Data Lag:** ~2-3 years after Census
- **Access:** silvis.forest.wisc.edu

### MTBS Burned Area
- **Update Frequency:** Annual
- **Temporal Coverage:** 1984-present
- **Data Lag:** ~1-2 years
- **Access:** mtbs.gov

### NOAA Sea Level Rise
- **Update Frequency:** Updated irregularly (every ~5 years)
- **Temporal Coverage:** Current scenarios (0-10 ft)
- **Access:** NOAA Office for Coastal Management

---

## 🏗️ INFRASTRUCTURE

### FHWA National Bridge Inventory (NBI)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1992-present
- **Data Lag:** ~6-12 months
- **Access:** FHWA website

### USACE National Inventory of Dams (NID)
- **Update Frequency:** Quarterly
- **Temporal Coverage:** Current (historical snapshots available)
- **Access:** nid.usace.army.mil

### EIA Form 861 (Electricity Reliability)
- **Update Frequency:** Annual
- **Temporal Coverage:** 1990-present (reliability metrics: 2013-present)
- **Data Lag:** ~12 months
- **Access:** EIA website

### FCC Broadband Data Collection
- **Update Frequency:** Biannual (June, December)
- **Temporal Coverage:** June 2022-present
- **Data Lag:** ~6 months
- **Access:** FCC BDC website

---

## 🔄 Data Release Calendar (Annual Sources)

### January-March
- Census ACS (previous year, released December/January)
- BLS QCEW (annual summary)

### April-June
- CDC WONDER Mortality (preliminary previous year)
- BEA GDP (first estimate previous year)

### July-September
- EPA AQS (validated previous year)
- NCES CCD (previous school year)
- USDA Census of Agriculture (quinquennial)

### October-December
- BEA Personal Income (revised)
- HUD FMR (following fiscal year)
- HRSA AHRF (previous year)

---

## 📊 Longest Time Series Available (by Source)

| Source | Start Year | Years Available | Notes |
|--------|------------|-----------------|-------|
| **ERA5 Climate** | **1940** | **84 years** | Longest environmental time series |
| Census Population | 1790 | 230+ years | Decadal |
| USGS NWIS Water | 1901 | 120+ years | Site-specific, varies |
| NCEI Climate | 1895 | 129 years | Station data |
| USDA NASS | 1866 | 158 years | Select commodities |
| NOAA Storm Events | 1950 | 74 years | Tornadoes; others 1996+ |
| CDC Mortality | 1968 | 56 years | ICD-9: 1968-1998; ICD-10: 1999+ |
| SEER Cancer | 1975 | 49 years | |
| USRDS Kidney | 1978 | 46 years | |
| IMPROVE Aerosols | 1988 | 36 years | |
| EPA TRI | 1988 | 36 years | |
| BLS LAUS | 1990 | 34 years | |
| EPA NEI | 1990 | 34 years | Triennial |

---

## ⏰ Data Lag Summary

| Lag Time | Sources |
|----------|---------|
| **Near Real-Time (0-7 days)** | ERA5, CAMS, NWIS, HMS Smoke, Drought Monitor |
| **1-3 months** | AQS (daily), LAUS, Storm Events, GRIDMET |
| **6-12 months** | ACS, PEP, AQS (annual), County Health Rankings |
| **12-18 months** | Mortality, TRI, AHRF, CBP, Natality, ArboNET |
| **18-24 months** | SEER, USRDS, Medicare, NCES Finance |
| **2-3 years** | NEI, NLCD, Pesticides, SEDA |
| **5-10 years** | Census Ag (5), Decennial Census (10), WUI (10) |

---

## ✅ Planning Your Data Collection

### For Time-Sensitive Research
- Use sources with shortest lag: ERA5, CAMS, NWIS, AQS daily, LAUS
- Accept that most health outcomes have 12-24 month lag

### For Longest Time Series
- Prioritize: ERA5 (1940+), NCEI climate (1895+), NWIS (1901+)
- Mortality: 1999+ (ICD-10 coding change)
- Census: Decadal back to 1790

### For Panel Data (County × Year)
- Ensure all sources align temporally
- Account for different lag times when interpreting results
- Be aware of boundary changes (see COUNTY_BOUNDARIES_REDISTRICTING.md)

---

## 📚 Resources

- **EPA Data Release Calendar:** https://www.epa.gov/airdata/
- **Census Release Schedule:** https://www.census.gov/programs-surveys/acs/news/data-releases.html
- **BEA Release Schedule:** https://www.bea.gov/news/schedule
- **CDC Data Release:** https://www.cdc.gov/nchs/nvss/deaths.htm

---

**Checklist:**

- [ ] Identify required temporal coverage for research question
- [ ] Check data lag times for most recent year needed
- [ ] Plan data collection around release schedules
- [ ] Be aware of provisional vs. final data
- [ ] Document data vintages used in analysis
- [ ] Set up alerts for annual data releases
- [ ] Allow for 12-24 month lag on health outcomes
- [ ] Use ERA5/CAMS for near real-time environmental data

---

**Summary:** You now have complete understanding of FIPS codes, county boundaries, geographic crosswalks, and temporal coverage for all data sources. You're ready to begin collecting county-level data!
