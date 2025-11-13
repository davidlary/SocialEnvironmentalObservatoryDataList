# Comprehensive Guide to US County-Level Traffic Accident/Crash Data Sources

**Last Updated:** November 11, 2025
**Status:** Production-Ready, Exhaustively Researched

---

## Table of Contents

1. [Federal Data Sources](#federal-data-sources)
   - [NHTSA FARS (Fatality Analysis Reporting System)](#1-nhtsa-fars-fatality-analysis-reporting-system)
   - [NHTSA CRSS (Crash Report Sampling System)](#2-nhtsa-crss-crash-report-sampling-system)
   - [CDC WISQARS](#3-cdc-wisqars)
2. [State Data Sources](#state-data-sources)
3. [R Package Tools](#r-package-tools)
4. [Variable Categories Reference](#variable-categories-reference)

---

## FEDERAL DATA SOURCES

### 1. NHTSA FARS (Fatality Analysis Reporting System)

**Overview:**
FARS is a nationwide census providing yearly data regarding fatal injuries suffered in motor vehicle traffic crashes. Operating since 1975, it covers all 50 States, the District of Columbia, and Puerto Rico.

**Geographic Resolution:** County-level (confirmed available)

**Data Coverage:**
- **Years Available:** 1975 to 2023 (2024 data will be released in 2025)
- **Data Updated:** Annually (typically September of following year for final data)
- **Scope:** Fatal crashes only (death within 30 days of crash)
- **Elements Coded:** 170+ data elements, 100+ per crash

**Data Limitations:**
- **ONLY fatal crashes** - does NOT include property damage only (PDO) or non-fatal injury crashes
- Personal identifying information removed for privacy
- Specific crash locations (exact addresses) removed from public files

---

#### FARS API Access

**Base URL:** `https://crashviewer.nhtsa.dot.gov/CrashAPI`

**Available Years:** 2010-2022 (API coverage)

**Authentication:** No API key required (public access)

**Output Formats:** XML, CSV, XLSX, JSON, JSV

#### API Endpoints

##### 1. Get Variables List
```
GET /definitions/GetVariables?dataYear={year}&format=json

Example:
https://crashviewer.nhtsa.dot.gov/CrashAPI/definitions/GetVariables?dataYear=2022&format=json
```

**Returns:** List of all available variables for specified year

##### 2. Get Variable Attributes
```
GET /definitions/GetVariableAttributes?variable={varname}&caseYear={year}&format=json

Example:
https://crashviewer.nhtsa.dot.gov/CrashAPI/definitions/GetVariableAttributes?variable=COUNTY&caseYear=2022&format=json
```

**Returns:** Detailed attributes and valid values for specific variable

##### 3. Query County-Level Crashes
```
Parameters:
- state: State name or FIPS code
- county: County name
- year: Data year (2010-2022)
- format: json, csv, xml

Example URL pattern:
https://crashviewer.nhtsa.dot.gov/CrashAPI/crashes?state=MD&county=Anne%20Arundel%20County&year=2022&format=json
```

**Note:** County selection only available for fatal crashes, not available for Cities and Counties simultaneously due to overlapping boundaries.

---

#### FARS Bulk Data Downloads

##### FTP Site Access
**URL:** `ftp://ftp.nhtsa.dot.gov/FARS/`

**Mirror Site (HTML browsing):** `https://wgetsnaps.github.io/ftp.nhtsa.dot.gov--fars/`

**NBER Mirror:** `http://data.nber.org/fars/ftp.nhtsa.dot.gov/`

**Data.gov Catalog:**
- Main: https://catalog.data.gov/dataset/fatality-analysis-reporting-system-fars
- FTP Raw Data: https://catalog.data.gov/dataset/fatality-analysis-reporting-system-fars-ftp-raw-data

**File Structure:**
```
/FARS/
  ├── 2010/
  │   ├── National/
  │   │   ├── FARS2010NationalCSV.zip
  │   │   ├── FARS2010NationalDBF.zip
  │   │   └── FARS2010NationalSAS.zip
  │   └── Puerto Rico/
  ├── 2011/
  ...
  ├── 2023/ (latest)
  └── FARS-DOC/
      ├── Analytical User Guide/
      │   ├── USERGUIDE-2023.pdf
      │   └── USERGUIDE-{year}.pdf
      └── Coding and Validation Manual/
```

**File Formats Available:**
- **CSV:** Comma-separated values (easiest for R, Python, Excel)
- **DBF:** Database format
- **SAS:** SAS statistical software format

---

#### FARS Query Tools

##### FIRST (Fatality and Injury Reporting System Tool)
**URL:** `https://cdan.dot.gov/query`

**Features:**
- Web-based query builder
- County-level filtering available for fatal crashes
- State/County/City/Region selections
- Cannot select both Cities and Counties simultaneously
- Exports to Excel, CSV
- No registration required for basic queries

**Capabilities:**
- Custom queries with multiple filters
- Demographic breakdowns
- Temporal analysis (time/day/month)
- Geographic mapping

##### STSI (State Traffic Safety Information)
**URL:** `https://cdan.dot.gov/STSI/stsi.htm`

**Features:**
- State and county-specific data for past 10 years
- Pre-built reports and profiles
- Key safety metrics:
  - Belt-use rates
  - Impaired driving statistics
  - Speeding-related crashes
  - Performance measures
- GIS crash location maps
- Alcohol-related crash data
- Economic cost estimates
- Grant funding information

---

#### FARS File Structure and Relationships

FARS data is organized into three interconnected files:

##### 1. ACCIDENT/CRASH File
**Key Variables:**
- `ST_CASE`: Unique crash identifier (primary key)
- `STATE`: State FIPS code
- `COUNTY`: County FIPS code
- `YEAR`: Year of crash
- `DAY`, `MONTH`: Temporal information
- `HOUR`, `MINUTE`: Time of crash
- `DAY_WEEK`: Day of week (1=Sunday, 7=Saturday)

**Geographic Variables:**
- `LATITUDE`, `LONGITUD`: Approximate crash location
- `HARM_EV`: First harmful event
- `MAN_COLL`: Manner of collision
- `REL_ROAD`: Relation to roadway
- `LGT_COND`: Light condition
- `WEATHER`: Weather conditions

**Roadway Variables:**
- `ROUTE`: Route type (Interstate, US Highway, State, County, Local)
- `RUR_URB`: Rural (1) vs Urban (2) designation
- `FUNC_SYS`: Functional system classification
- `RD_OWNER`: Roadway owner

**Crash Characteristics:**
- `CF1`, `CF2`, `CF3`: Crash-related factors
- `FATALS`: Number of fatalities
- `DRUNK_DR`: Number of drunk drivers
- `SP_JUR`: Special jurisdiction (National Park, Indian Reservation, etc.)

##### 2. VEHICLE File
**Key Variables:**
- `ST_CASE`: Crash identifier (links to Accident file)
- `VEH_NO`: Vehicle number within crash
- `NUMOCCS`: Number of occupants
- `MAKE`: Vehicle make (GM, Ford, Toyota, etc.)
- `MODEL`: Vehicle model
- `MAK_MOD`: Combined make/model code
- `BODY_TYP`: Body type (passenger car, SUV, pickup, motorcycle, etc.)
- `MOD_YEAR`: Model year
- `VIN`: Vehicle Identification Number (used for automated coding)
- `VEH_MAN`: Vehicle maneuver
- `TRAV_SP`: Travel speed
- `ROLLOVER`: Rollover occurrence (0=No, 1=Yes)
- `FIRE_EXP`: Fire or explosion (0=No, 1=Yes)
- `IMPACT1`: Initial impact point
- `DEFORMED`: Extent of deformation/damage
- `TOW_VEH`: Vehicle towed indicator
- `UNDERIDE`: Underride (1-5 codes)
- `DR_DRINK`: Driver drinking indicator

**Sequence of Events (up to 4 events):**
- `M_HARM`: Most harmful event
- `SOE1`, `SOE2`, `SOE3`, `SOE4`: Sequence of events

**Safety Equipment:**
- `DR_SF1`, `DR_SF2`, `DR_SF3`, `DR_SF4`: Driver safety equipment factors

##### 3. PERSON File
**Key Variables:**
- `ST_CASE`: Crash identifier
- `VEH_NO`: Vehicle number
- `PER_NO`: Person number
- `PER_TYP`: Person type (1=Driver, 2=Passenger, 5=Pedestrian, 6=Bicyclist, etc.)
- `INJ_SEV`: Injury severity (KABCO scale)
  - 0: No injury
  - 1: No injury (property damage only)
  - 2: Possible injury (C)
  - 3: Suspected minor injury (B)
  - 4: Suspected serious injury (A)
  - 5: Fatal injury (K) - died within 30 days
  - 6: Died prior to crash
  - 9: Unknown

**Demographics:**
- `AGE`: Age in years
- `SEX`: Sex (1=Male, 2=Female)
- `RACE`: Race (FARS revised coding in 2019 to allow multiple races)
- `HISPANIC`: Hispanic origin

**Safety Restraints:**
- `REST_USE`: Restraint system use
- `REST_MIS`: Restraint misuse
- `AIR_BAG`: Air bag deployment
- `EJECTION`: Ejection from vehicle (0=Not ejected, 1=Totally ejected, 2=Partially ejected)
- `EJ_PATH`: Ejection path

**Alcohol/Drugs:**
- `DRINKING`: Police-reported alcohol involvement
- `ALC_RES`: Alcohol test result
- `ALC_STATUS`: Alcohol impairment status
- `DRUGS`: Drug involvement (see limitations below)
- `DRUG_RES`: Drug test results

**Other:**
- `SEAT_POS`: Seating position
- `DEATH_DA`, `DEATH_MO`, `DEATH_YR`: Date of death
- `DEATH_HR`, `DEATH_MN`: Time of death
- `LAG_HRS`, `LAG_MINS`: Lag time between crash and death
- `DOA`: Dead on arrival

---

#### FARS Variable Categories - Complete List

##### CRASH CHARACTERISTICS

**Total Crashes by Severity:**
- Fatal crashes only (by definition of FARS)
- Fatality counts per crash
- Multiple fatality crashes

**Crash Types:**
- Single vehicle vs multi-vehicle (`VE_FORMS`: number of motor vehicles in crash)
- Hit and run (`HIT_RUN`)
- Rollover (`ROLLOVER`)
- Fire/explosion involved (`FIRE_EXP`)
- Work zone (`WRK_ZONE`): Crash in work zone (1995+)
- School zone: Tracked in some states via special jurisdiction
- Railway crossing (`REL_ROAD`)

**Manner of Collision (`MAN_COLL`):**
- Not Collision with Motor Vehicle
- Front-to-Rear
- Front-to-Front
- Angle
- Sideswipe-Same Direction
- Sideswipe-Opposite Direction
- Rear-to-Side
- Rear-to-Rear
- Other

**Sequence of Events:**
- Non-collision events (ran off road, rollover, jackknife)
- Collision with: person, vehicle, fixed object, etc.
- Up to 4 events coded per vehicle
- Most harmful event (`M_HARM`)

##### DEMOGRAPHICS

**Age (`AGE`):**
- Coded in years (0-120+)
- Specific age or age ranges
- Baby boomer generation most represented
- High representation: children <10, adults 65+, ages 35-74

**Sex (`SEX`):**
- 1 = Male
- 2 = Female
- 8 = Not reported
- 9 = Unknown

**Race (`RACE`):**
- Starting 2019: Multiple race coding allowed
- Categories align with NCHS death certificate data
- Data obtained from official death certificates
- Hispanic origin tracked separately (`HISPANIC`)

**Person Type (`PER_TYP`):**
- Driver
- Passenger (by position)
- Pedestrian
- Bicyclist/Pedalcyclist
- Other non-motorist

##### VEHICLE TYPES (`BODY_TYP`)

Categories include:
- Passenger car (compact, sedan, convertible, hatchback)
- Light trucks (pickup, SUV, van, minivan)
- Large trucks (single unit, combination unit)
- Motorcycle (2-wheel, 3-wheel)
- Bus (school, transit, intercity, other)
- Emergency vehicle (fire, ambulance, police)
- Military vehicle
- All-terrain vehicle (ATV)
- Bicycle/pedalcycle
- Other/unknown

##### CONTRIBUTING FACTORS

**Alcohol Involvement:**
- `DRINKING`: Police-reported drinking (1=Yes)
- `ALC_RES`: BAC test result (g/dL × 100)
- `ALC_STATUS`: Impairment determination
  - 0 = Not impaired (BAC < 0.08)
  - 1 = Impaired (BAC ≥ 0.08)
- `DRUNK_DR`: Number of drunk drivers in crash
- **BAC Testing Completeness:** 71% of killed drivers, 28% of surviving drivers (2013 data)
- **Multiple Imputation:** NHTSA uses statistical imputation for missing BAC values

**Drug Involvement:**
- `DRUGS`: Drug involvement indicator
- `DRUG_RES`: Drug test results
- **Data Quality Warning:** NHTSA cautions against use due to inconsistent collection, testing, coding, and reporting across jurisdictions
- **Missingness:** Non-ignorable (missing not-at-random), violates imputation assumptions
- Drug data NOT imputed like alcohol data

**Speed-Related (`SPEEDREL`):**
- 1 = Yes, speeding-related
- 0 = No
- Most common primary factor in distracted driving crashes (26.9%)

**Distracted Driving:**
- Specific distraction codes in driver factors
- 3,275 lives claimed in 2023
- Higher proportion of rear-end collisions
- Peak times: weekday afternoons (3 PM - 7 PM)

**Driver-Related Factors (`DR_CF1` - `DR_CF4`):**
- Failure to yield
- Failure to obey traffic signals
- Following too closely
- Operating vehicle erratically
- Driving wrong way
- Making improper turn
- Driving without headlights
- And 30+ other codes

##### WEATHER CONDITIONS (`WEATHER`)

Codes include:
- Clear
- Rain
- Sleet/Hail
- Snow
- Fog/Smog/Smoke
- Severe crosswinds
- Blowing sand/dirt
- Other
- Unknown

##### ROAD CONDITIONS (`WEATHER1`, `WEATHER2`)

- Dry
- Wet
- Snow/slush
- Ice
- Sand/dirt/gravel
- Water (standing, moving)
- Oil
- Other
- Unknown

**Road Surface Temperature:** Included in snowy/rainy condition analyses

##### LIGHTING CONDITIONS (`LGT_COND`)

- Daylight
- Dark - not lighted
- Dark - lighted
- Dark - unknown lighting
- Dawn
- Dusk
- Unknown

**Lighting Impact:** Studies show potential to reduce fatalities at T-intersections and roadway departures with improved lighting in bad weather

##### VISIBILITY

Affected by:
- Weather phenomena (fog, smoke, snow)
- Time of day
- Roadway lighting presence
- Measured through weather codes and light conditions

##### TIME/TEMPORAL FACTORS

**Time of Day (`HOUR`, `MINUTE`):**
- Coded in military time (0-23:59)
- Peak fatal crash times:
  - Weekdays: 3 PM - 7 PM
  - Weekends: 8 PM - midnight
  - Alcohol-related: midnight - 3 AM

**Day of Week (`DAY_WEEK`):**
- 1 = Sunday through 7 = Saturday
- More fatalities on weekends
- Saturday has highest fatal crash count
- Saturday: 16.41% of pedestrian fatalities (2018)

**Month (`MONTH`):**
- 1 = January through 12 = December
- Summer/fall months: highest crash fatalities
- Spring/summer: peak 8 PM - 11:59 PM
- November-March: peak 4 PM - 7:59 PM

**Holiday Crashes:**
- Special holiday indicators in some analyses
- Elevated fatalities on:
  - Independence Day
  - Memorial Day
  - Labor Day
  - New Year's Day
- Higher proportion alcohol-involved

##### LOCATION FACTORS

**Urban vs Rural (`RUR_URB`):**
- 1 = Rural
- 2 = Urban
- Based on Census designation

**Road Type/Functional Class (`FUNC_SYS`):**
- Interstate
- Principal Arterial (Other Freeways/Expressways, Other)
- Minor Arterial
- Major Collector
- Minor Collector
- Local Road
- Unknown

**Relation to Junction (`REL_ROAD`):**
- Non-Junction
- Intersection
- Intersection-Related
- Driveway Access
- Entrance/Exit Ramp Related
- Railway Grade Crossing
- Crossover-Related
- Shared-Use Path Crossing
- Acceleration/Deceleration Lane
- Through Roadway
- Other

**Type of Intersection (`TYP_INT`):**
- Not at intersection
- Four-way intersection
- T-intersection
- Y-intersection
- Traffic circle
- Roundabout
- Five-point or more
- Other

**Intersection Safety Note:** Approximately half of all U.S. car crashes occur at intersections or are intersection-related (2019)

**Route Type (`ROUTE`):**
- Interstate Highway
- U.S. Highway
- State Highway
- County Road
- Township Road
- Municipal Street
- Indian Reservation Road
- Frontage Road

**Special Jurisdiction (`SP_JUR`):**
- National Park Service
- Military Property
- Indian Reservation
- College/University Campus
- Other Federal Property

##### CRASH OUTCOMES

**Fatalities:**
- Total fatalities (`FATALS`)
- By road user type (driver, passenger, pedestrian, cyclist)
- By vehicle type
- By age group
- By sex
- By race/ethnicity
- Multiple fatality crashes

**Injury Severity (Person-level):**
FARS only includes fatal injury (K), but person file includes all occupants:
- K (5) = Fatal
- A (4) = Suspected serious injury
- B (3) = Suspected minor injury
- C (2) = Possible injury
- O (1,0) = No apparent injury

**Property Damage:**
- Not systematically coded in FARS
- For PDO crashes, see CRSS section below

##### RESTRAINT USE AND SAFETY SYSTEMS

**Restraints (`REST_USE`):**
- None used
- Shoulder belt only
- Lap belt only
- Shoulder and lap belt
- Child safety seat
- Other
- Unknown

**Restraint Misuse (`REST_MIS`):**
- Not misused
- Misused
- Improper use
- Not applicable

**Air Bags (`AIR_BAG`):**
- Not deployed
- Deployed - front
- Deployed - side
- Deployed - curtain
- Deployed - other
- Deployment unknown
- Not applicable

**Ejection (`EJECTION`):**
- Not ejected
- Totally ejected
- Partially ejected
- Unknown
- Not applicable (e.g., motorcycle riders)

**Ejection Path (`EJ_PATH`):**
- Not applicable
- Through windshield
- Through side window
- Through back window/door
- Other path

##### PEDESTRIAN AND CYCLIST SPECIFIC

**Person Type:**
- Pedestrian (`PER_TYP` = 5)
- Bicyclist (`PER_TYP` = 6)
- Other cyclist (`PER_TYP` = 7)

**Age Patterns:**
- Children <10: Highest % pedestrian fatalities
- Children 6-14: Highest % cyclist fatalities
- Adults 65+: High % pedestrian fatalities
- Adults 35-74: Increased cyclist mortality since 1975

**Crash Circumstances:**
- Dart-out crashes: 43% of children 0-9
- Midblock cyclist failed to yield: 26% of cyclists 0-9
- Most pedestrian fatalities: Saturdays (16.41% in 2018)

**Special Manuals:**
- FARS/CRSS Pedestrian Bicyclist Crash Typing Manual available

##### COMMERCIAL VEHICLES

**Vehicle Type Indicators:**
- Body type codes for trucks
- Special study files for medium/heavy trucks
- GVW (Gross Vehicle Weight) ratings
- Carrier identification
- Hazardous materials involvement

**Special Coding Manuals:**
- Medium-Truck Special Study Coding Manual (DOT HS 813 355, Aug 2022)

##### EMERGENCY RESPONSE (Limited in FARS)

**Available:**
- Dead on arrival indicator (`DOA`)
- Time of death
- Lag time between crash and death

**Not Systematically Coded:**
- EMS response time
- Transport time
- Hospital destination
- Treatment details

**Note:** NEMSIS (National EMS Information System) linkages being developed in MMUCC 6th Edition (2024)

---

#### Documentation and Manuals

##### Primary References

**FARS Analytical User's Manual (1975-2023)**
- **Latest:** DOT HS 813 XXX (2024 publication covering 2023 data)
- **Publisher:** NHTSA National Center for Statistics and Analysis
- **Repository:** https://rosap.ntl.bts.gov/view/dot/78035
- **FTP:** ftp://ftp.nhtsa.dot.gov/FARS/FARS-DOC/Analytical User Guide/
- **Content:**
  - Complete data element descriptions
  - File structure documentation
  - Variable definitions
  - Valid codes for all attributes
  - Historical changes by year
  - Appendices with complete variable listings

**FARS/CRSS Coding and Validation Manual (Annual)**
- **Latest:** 2023 Manual (published 2024)
- **Purpose:** Detailed definitions for each data element and attribute
- **Audience:** FARS analysts, researchers needing precise definitions
- **FTP:** ftp://ftp.nhtsa.dot.gov/FARS/FARS-DOC/Coding and Validation Manual/

**MMUCC 6th Edition (2024)**
- **Full Title:** Model Minimum Uniform Crash Criteria Guideline, Sixth Edition
- **Published:** 2024
- **URL:** https://www.nhtsa.gov/traffic-records/model-minimum-uniform-crash-criteria
- **Content:**
  - 105 data elements
  - 1,056 data attributes
  - Standardized definitions aligned with FARS, CRSS, CISS
  - Harmonized with NEMSIS (EMS) data system
  - Previous editions: 1998, 2003, 2008, 2012, 2017

**Data Availability Report**
- **URL:** https://cdan.dot.gov/tsftables/Data%20Availability.pdf
- **Content:** Data completeness by state and year

##### Supplementary Documentation

**FARS/CRSS Pedestrian Bicyclist Crash Typing Manual**
- Specialized coding for non-motorist crashes

**Special Study Manuals**
- Medium-Truck Special Study
- Other vehicle-specific coding guidelines

**Release Notes (Annual)**
- Found in each year's FTP directory
- Documents changes from previous year
- New variables or coding modifications

---

### 2. NHTSA CRSS (Crash Report Sampling System)

**Overview:**
CRSS replaced GES (General Estimates System) in 2016. It is a nationally representative sample of police-reported crashes involving all types of motor vehicles, pedestrians, and cyclists, ranging from property-damage-only crashes to fatalities.

**Important Limitation:** **County-level geographic identifiers are REMOVED** from public CRSS files for privacy protection.

**Geographic Resolution Available:**
- Region (national)
- State (limited)
- Rural/Urban classification
- Police jurisdiction (anonymized)
- Driver ZIP code

**Data Coverage:**
- **Years Available:** 2016 to present
- **Sample Design:** ~60 geographic areas (PSUs - Primary Sampling Units) across U.S.
- **Crash Types:** ALL crashes (PDO, injury, fatal)
- **Updates:** Annual release after quality checks

**Why NOT County-Level:**
Personal information such as names, addresses, license and registration numbers, and **crash locations are not included** in the public CRSS files to protect individual privacy.

**What IS Available:**
- Region
- Urbanicity (rural/urban)
- Police jurisdiction (coded)
- Driver ZIP code
- Representative national and regional estimates

**Access Methods:**

1. **FIRST Query Tool**
   - URL: https://cdan.dot.gov/query
   - Can query CRSS alongside FARS
   - State/County/Region selections NOT available for CRSS (only for FARS fatal crashes)

2. **Data Files**
   - Contact: ncsarequests@dot.gov
   - Phone: 800-934-8517
   - National Center for Statistics and Analysis
   - 1200 New Jersey Avenue SE
   - Washington, DC 20590

3. **Free Access:** After personal identifiers removed, data available to Federal agencies, state/local governments, universities, research institutions, automobile/trucking/insurance industries, and general public

**Use Case:**
- National/regional crash statistics
- Representative sampling of all crash severities
- Injury/PDO crash estimates
- **NOT suitable for county-level analysis**

---

### 3. CDC WISQARS

**Overview:**
Web-based Injury Statistics Query and Reporting System maintained by CDC's National Center for Injury Prevention and Control.

**URL:** https://wisqars.cdc.gov/

**Data Sources:**
- National Vital Statistics System (NVSS)
- Links to FARS data
- All-cause injury mortality and morbidity

**Geographic Resolution:**
- National
- State
- **County-level** (with restrictions)

**Motor Vehicle Crash Variables:**
- Traffic crash fatalities
- Rates per 100,000 population
- Rates per 100 million vehicle miles traveled (VMT)

**Available Breakdowns:**
- Year (2018-2023 by Single Race currently available)
- County
- Age groups
- Sex
- Race/Ethnicity
- Injury intent
- Injury mechanism

**Data Use Restrictions (Important):**
- NCHS implemented **more restrictive rules** for reporting state- and county-level death data (2008+)
- Purpose: Avoid inadvertent disclosure of decedent's identity
- Small count suppression applies
- Some county-level cells may be suppressed for privacy

**Interactive Tools:**
- **WISQARS Explore Fatal and Nonfatal Data:** https://wisqars.cdc.gov/explore/
- **WISQARS Community Health Factors:** https://wisqars.cdc.gov/communityhealthfactors/
  - U.S. map showing rates at county-level
  - Social determinants of health (SDOH) measures
  - Linked to crash fatality data

**Access:**
- Web-based query system (no registration required)
- Results exportable to Excel, CSV
- API access not publicly documented

**Use Case:**
- County-level traffic fatality rates
- Comparison with other injury causes
- Public health perspective on crashes
- Demographic disparities analysis

**Latest Data:** 2018-2023 (as of Nov 2025)

---

## STATE DATA SOURCES

The following states provide county-level crash data through public portals or open records requests. Access methods and variables vary significantly by state.

### States with Robust County-Level Crash Data Systems

#### California

**System:** SWITRS (Statewide Integrated Traffic Records System)
**Status Change:** As of January 8, 2025, SWITRS replaced by **CCRS (California Crash Reporting System)**

**Access Portal:** TIMS (Transportation Injury Mapping System)
**URL:** https://tims.berkeley.edu/

**Features:**
- 7 different crash and geospatial analysis tools
- County-level filtering
- SWITRS Query & Map application
- Custom queries and mapping

**County Data Available:**
- Pedestrian and bicycle crash data by county (2020-2024)
- URL: https://catsip.berkeley.edu/resources/crash-data/pedestrian-and-bicycle-crash-data-county
- Provisional 2024 data updated as of September 23, 2025

**Other Tools:**
- Caltrans SHSP Dashboard: https://shsp.dot.ca.gov/
- 10 years of fatal and serious injury crashes
- Filter by county

**Variables:** See SWITRS codebook at https://tims.berkeley.edu/help/SWITRS.php

**Registration:** Free account required for TIMS

**Note:** Transition to CCRS may affect access methods - check current status

---

#### Texas

**System:** CRIS (Crash Records Information System)
**Maintained by:** TxDOT

**Access Methods:**

1. **CRIS Query Tool**
   - URL: https://cris.dot.state.tx.us/public/Query/app/home
   - Web-based public query
   - County selection available
   - Export to Excel, CSV

2. **Automated Extract Files**
   - Previous 10 years + current year (Jan 1, 2014 to present)
   - CSV format
   - Requires one-time self-registration
   - Two file types:
     - **Public Extract:** Public roads data
     - **Standard Extract:** State highway system + PII (restricted to government agencies)

3. **Bulk Data Request Form**
   - For large requests
   - Submit online form

**Documentation:**
- Automated Interface User Guide V29.0 (June 9, 2025)
- URL: https://www.txdot.gov/content/dam/docs/division/trf/crash-records/cris-guide.pdf
- Purchase User Guide V29.0 (June 23, 2025)

**Data Published:** By June of following year for previous 10 years

**Coverage:** All public roads in Texas

---

#### Florida

**System:** CAR (Crash Analysis Reporting)
**Maintained by:** FDOT Safety Office

**Data Sources:**
- Long-form crash reports from FLHSMV
- Verified by FDOT (fatal and serious injury crashes verified immediately upon receipt)
- Weekly updates from FLHSMV

**Access Portals:**

1. **FDOT Open Data Hub**
   - URL: https://gis-fdot.opendata.arcgis.com/
   - Public crashes on public roads
   - Downloadable spatial data

2. **State Safety Office GIS**
   - URL: https://fdotewp1.dot.state.fl.us/ssogis/home.aspx
   - Monthly data refreshes
   - Filter by year, county, crash type

3. **FLHSMV Traffic Crash Facts**
   - Annual reports with county statistics
   - URL: https://www.flhsmv.gov/traffic-crash-reports/
   - Florida Crash Dashboard: General crash statistics

**Request Process:**
- URL: https://www.fdot.gov/Safety/safetyengineering/crash-data.shtm
- FAQ: https://www.fdot.gov/docs/default-source/safety/11a-safetyengineering/crash-data/frequently-asked-questions.pdf

**2024 County Statistics (Top Counties):**
- Miami-Dade: 59,978 crashes
- Broward: 38,279
- Palm Beach: 26,550
- Hillsborough: 26,265
- Orange: 25,406
- Duval: 23,011

---

#### New York

**System:** ALIS (Accident Location and Information System)
**Maintained by:** NYSDOT

**Access Methods:**

1. **TSSR (Traffic Safety Statistical Repository)**
   - Maintained by ITSMR (Institute for Traffic Safety Management and Research)
   - Crash data by county and municipality
   - URL: https://www.itsmr.org/traffic-safety-statistical-repository/tssr-faq/
   - Preliminary data added monthly
   - Final counts: September of following year

2. **NYSDOT CLEAR Crash Data Viewer**
   - URL: https://clear.dot.ny.gov/clear/cdv/
   - Official visualization tool

3. **NY State Open Data Portal**
   - URL: https://data.ny.gov/
   - Motor Vehicle Crashes datasets
   - Three-year rolling window
   - URL: https://data.ny.gov/Transportation/Motor-Vehicle-Crashes-Case-Information-Three-Year-/e8ky-4vqe

4. **FOIL Request (Freedom of Information Law)**
   - For detailed data
   - Contact DOT FOIL office

**Access Restrictions:**
- NYS government employees: Direct ALIS access
- Others: TSSR or FOIL request

**Data Completeness:**
- Preliminary: Monthly updates
- Final: September following crash year

**Recent Update (2025):** Starting June 2025, reports use "Substance-Related" instead of "Impaired" in crash summaries

**Health Department Data:**
- URL: https://www.health.ny.gov/statistics/prevention/injury_prevention/traffic/county_of_crash.htm
- County of crash statistics

---

#### Illinois

**System:** Illinois Roadway Crash Database
**Maintained by:** IDOT

**URL:** https://idot.illinois.gov/transportation-system/transportation-safety/roadway-safety/illinois-roadway-crash-data.html

**Access Methods:**

1. **IDPH EMS Reporting System - Crash Report Database**
   - URL: https://app.idph.state.il.us/emsrpt/crash.asp
   - Web-based queries

2. **IDOT Safety Office**
   - Direct data requests
   - Custom reports available

**Data Scope:**
- All motor vehicle crashes in Illinois
- Frequency and severity
- Demographic characteristics
- Weather, lighting, road conditions
- Local crash data (IDOT expanded database to include local roads)

**2023 Statistics:**
- Total crashes: 299,000
- Cook County (including Chicago): >50% of all incidents

---

#### Michigan

**System:** Michigan Traffic Crash Facts
**Maintained by:** MSP Traffic Crash Reporting Unit

**Primary Portal:** https://www.michigantrafficcrashfacts.org/

**Features:**
- Interactive mapping
- Charts, tables, lists
- Custom queries
- Police report downloads
- County-level analysis

**Annual Reports:** https://www.michigan.gov/msp/divisions/cjic/traffic-crash-reporting-unit/annual-reports-and-statistics

**Variables:** Comprehensive including demographics, vehicle types, crash circumstances, injury severity

---

#### Pennsylvania

**Data Source:** Pennsylvania Department of Transportation
**Maintained by:** PennDOT

**2023 Statistics:**
- Total crashes: 110,000
- Injury crashes: ~70,000
- Philadelphia + Allegheny County: >33% of total

**Access:** Contact PennDOT for crash data requests

---

#### North Carolina

**System:** North Carolina crash data system
**Maintained by:** NCDOT Traffic Safety Unit

**Access Portals:**

1. **NCDOT Connect**
   - URL: https://connect.ncdot.gov/resources/safety/pages/crash-data.aspx
   - Crash data portal

2. **NC Vision Zero**
   - URL: https://ncvisionzero.org/data-analytics/visualizations/
   - Interactive visualizations
   - County-level statistics
   - City-level data
   - Health outcomes data

3. **County Crash Profile Overview Maps**
   - URL: https://connect.ncdot.gov/resources/State-Mapping/Pages/County-Crash-Profile-Overview-Maps.aspx
   - Vehicle crash profile summaries by county

4. **Statewide Crash Dashboard**
   - URL: https://www.arcgis.com/apps/dashboards/b0bb09fcff824e8da4e8cfe4f79b9b30

**HSIS (Highway Safety Information System):**
- NC participates in federal HSIS program
- Linked crash, roadway, traffic volume data
- Data from 2018 forward
- Guidebook: https://highways.dot.gov/sites/fhwa.dot.gov/files/FHWA-HRT-24-108.pdf (Sept 2024)
- County variable included in Roadway, Traffic Signal, and Crash files

---

#### Massachusetts

**System:** IMPACT (Interactive Mapping Portal for Analysis and Crash Tracking)
**Maintained by:** MassDOT

**Primary URL:** https://apps.crashdata.dot.mass.gov/cdp/home
**Alternate:** https://apps.impact.dot.state.ma.us/cdp/home

**Features:**
- Pre-built reports
- Tabulations
- Custom queries
- Interactive data dashboards
- Municipality/region/mode filtering
- Top crash locations by city/town

**Open Data Hub:** https://massdot-impact-crashes-vhb.opendata.arcgis.com/

**Download Formats:**
- CSV
- KML
- Zip
- GeoJSON
- GeoTIFF
- PNG
- Excel

**Help Documentation:** https://apps.impact.dot.state.ma.us/helpcdp/topics/idh-topic60.htm

---

#### Virginia

**System:** TREDS (Traffic Records Electronic Data System)
**Maintained by:** VDOT, VAHSO, DMV (collaborative)

**Access Methods:**

1. **VDOT Crash Data Portal**
   - URL: https://www.virginiaroads.org/maps/1a96a2f31b4f4d77991471b6cabb38ba
   - Public mapping tool

2. **VDOT Crash Analysis Tool**
   - Power BI dashboard
   - URL: https://app.powerbigov.us/view?r=eyJrIjoiMjhlZjFhZDAtNTljMC00MDA1LWEyOTMtYWYwM2NiMmRiMmRkIiwidCI6IjYyMGFlNWE5LTRlYzEtNGZhMC04NjQxLTVkOWYzODZjNzMwOSJ9

3. **CrashData Basic**
   - URL: https://www.virginiaroads.org/maps/VDOT::crashdata-basic-1

4. **VDOT Open Data (ArcGIS)**
   - URL: https://virginiaroads-vdot.opendata.arcgis.com/

5. **VDOT Dashboard**
   - URL: https://dashboard.virginiadot.org/pages/safety/crashes.aspx

6. **DMV Statewide Crash Data**
   - URL: https://www.dmv.virginia.gov/safety/crash-data

**Data Request Process:**
- LibAnswers FAQ: https://virginiadot.libanswers.com/faq/220306
- FOIL-type requests available

**System:** State-of-the-art automated and centralized system (TREDS)

---

#### Maryland

**System:** ACRS (Automated Crash Reporting System)
**Maintained by:** Maryland State Police

**Crash Data Dashboard:**
- URL: https://zerodeathsmd.gov/resources/crashdata/crashdashboard/
- Zero Deaths Maryland program
- County-level filtering

**Location Data:**
- Approximate locations based on latitude/longitude from officer reports
- Geographic mapping available

---

#### Colorado

**Maintained by:** CDOT (Colorado Department of Transportation)

**Access Methods:**

1. **CDOT Crash Summary Dashboard**
   - URL: https://tableau.state.co.us/t/CDOT/views/CDOTCrashSummaryAVtestver2_0/StatewideSummary
   - Statewide and county-level

2. **Safety Data Archive**
   - URL: https://www.codot.gov/safety/safetydata

3. **CORA Requests (Colorado Open Records Act)**
   - For specific crash data requests
   - Intersection, corridor, city, county
   - Excel format typically
   - Contact CDOT directly for data within jurisdiction

4. **Advancing Transportation Safety Portal**
   - URL: https://transportationsafety.colorado.gov/

**Documentation:**
- Fatal Crash Data: https://www.codot.gov/safety/traffic-safety/data-analysis/fatal-crash-data
- Crash Data: https://www.codot.gov/safety/traffic-safety/data-analysis/crash-data

---

#### Georgia

**Maintained by:** Georgia Department of Transportation

**2022 Statistics:** 387,000 crashes

**Access:** Contact GDOT for county-level crash data

---

#### Washington

**Participation:** NHTSA State Data System (SDS) - one of 34 participating states

**Maintained by:** Washington Traffic Safety Commission

**Data Dashboards:** https://wtsc.wa.gov/dashboards/

**Access:** Contact WTSC or WSDOT for detailed county crash data

---

#### Arizona

**System:** Arizona DOT Crash Database

**2022 Statistics:**
- Total crashes: 121,000
- Maricopa County: >70% of statewide crashes

**Publication:** Annual Motor Vehicle Crash Facts
- URL: https://azdot.gov/sites/default/files/2023-07/2022-Crash-Facts.pdf

**Access:** Contact ADOT for data requests

---

#### Tennessee

**Source:** Tennessee Department of Safety and Homeland Security

**2022 Statistics:**
- Total crashes: 205,000
- Fatal crashes: >1,300

**Access:** Contact TDSH for crash data

---

#### Louisiana

**System:** Louisiana eCrash
**Maintained by:** LSU CARTS (Center for Analytics and Research in Transportation Safety)

**Portals:**

1. **Louisiana State Police - Crash Reports**
   - URL: https://crashreports.dps.la.gov/
   - Purchase individual reports

2. **Louisiana eCrash**
   - URL: https://carts.lsu.edu/ecrash/
   - Official statewide electronic capture platform
   - Used by law enforcement

**Publications:**
- Louisiana Traffic Records Data Report 2023
- URL: https://www.lahighwaysafety.org/media/rrmpm2je/2023-crash-data-report-final.pdf

**Data Scope:**
- Traffic crashes from state, sheriff, local police agencies
- Statistical analysis available
- Wide variety of reporting information

---

#### Minnesota

**System:** MIDAS (Minnesota Injury Data Access System)
**Maintained by:** Minnesota Department of Health

**URL:** https://www.health.state.mn.us/communities/injury/midas/index.html

**Features:**
- Injury, violence, substance use data
- **Linked police crash reports + hospital data + death certificates**
- Filter by county, injury type, sex, timeframe
- Crash outcomes analysis

**Additional:** Minnesota Office of Traffic Safety provides crash data

**Unique Feature:** Data linkage between crash reports, medical records, and death certificates

---

#### Oregon

**System:** TransGIS
**Maintained by:** Oregon DOT

**Features:**
- Interactive map format
- Multi-level views of transportation system
- Complex crash data presentation

**Access:** Contact ODOT for detailed county data

---

#### Indiana

**Source:** Indiana University Public Policy Institute (for ICJI)
**System:** ARIES (Automated Reporting Information Exchange System)

**Publications:**
- Annual crash reports for all 92 counties
- 200+ data items from officer crash reports
- In-depth county characteristics

**Data Request Process:**
- Individual reports: Indiana State Police website
- Research requests: aries.support@lexisnexisrisk.com or 866-495-4206

**Tools:**
- Indianapolis MPO Dashboards: https://www.indympo.org/maps-and-data/dashboards-reports
- CJI Crash Statistics: https://www.in.gov/cji/research/crash-statistics/

---

#### New Jersey

**Source:** New Jersey State Police

**Fatal Crash Statistics (2025 YTD):**
- URL: https://www.nj.gov/njsp/info/fatalacc/index.shtml
- Year-to-date by county
- Click county on map for statistics

**Data Scope:** Minimal public statistics; primarily fatal crashes

---

#### Ohio

**Source:** Ohio Department of Transportation

**Major Crash Corridors:**
- Columbus
- Cleveland
- Cincinnati

**Access:** Contact ODOT for county crash data

---

#### Kentucky

**Status:** Capturing 5 of 23 MMUCC critical crash factors

**Access:** Contact Kentucky Transportation Cabinet for crash data

---

#### Wisconsin

**Status:** 14 of 23 MMUCC critical crash factors captured (leading nation with Kansas)

**Access:** Contact Wisconsin DOT for crash data

---

### Multi-State Resources

#### FMCSA Crash Statistics
**URL:** https://ai.fmcsa.dot.gov/CrashStatistics

**Features:**
- Motor Carrier Management Information System (MCMIS)
- State-level commercial vehicle crash data
- Data snapshot: 9/26/2025
- County-level details available for some states

**Download:** State crash records downloadable from dropdown menu

---

#### Safer Streets Priority Finder - Crash Data Sources
**URL:** https://www.saferstreetspriorityfinder.com/tool/crashdatasources/

**Purpose:** Comprehensive directory of state crash data sources with links

---

## R PACKAGE TOOLS FOR AUTOMATED FARS DATA ACCESS

### 1. rfars Package

**Maintained by:** s87jackson
**CRAN:** https://cran.r-project.org/web/packages/rfars/
**Documentation:** https://cran.r-project.org/web/packages/rfars/readme/README.html
**GitHub:** https://github.com/s87jackson/rfars

**Purpose:** Download and analyze FARS and GES/CRSS data

**Installation:**
```r
install.packages("rfars")
library(rfars)
```

**Key Functions:**

#### get_fars()
Downloads FARS or GES/CRSS data with one line of code

**Parameters:**
- `years`: Vector of years (2011+)
- `states`: State abbreviations or names (FARS)
- `regions`: Region codes (GES/CRSS)

**Examples:**
```r
# Get FARS data for Maryland 2018-2021
crashes_md <- get_fars(years = c(2018, 2019, 2020, 2021), states = "MD")

# Get FARS data for North Carolina, single year
crashes_nc <- get_fars(years = 2021, states = "NC")

# Get GES/CRSS data for region
crashes_ges <- get_fars(years = 2019, regions = 1)
```

**Data Source:** Downloads directly from NHTSA FTP site or uses local cached files

**Codebooks Available:**
```r
# View FARS codebook
View(rfars::fars_codebook)

# View GES/CRSS codebook
View(rfars::gescrss_codebook)
```

---

### 2. crashapi Package

**Maintained by:** Eli Pousson
**GitHub:** https://github.com/elipousson/crashapi
**Documentation:** https://elipousson.github.io/crashapi/

**Purpose:** Access FARS data through NHTSA FARS API (2010-2022)

**Installation:**
```r
# Install from GitHub using pak
pak::pak("elipousson/crashapi")

library(crashapi)
```

**Key Functions:**

#### get_fars()
Downloads fatal crash data with county filtering

**Parameters:**
- `year`: Single year or vector (2010-2022)
- `state`: State name or abbreviation
- `county`: County name
- `details`: TRUE for detailed crash information
- `geometry`: TRUE to return sf spatial object

**County-Level Examples:**

##### Example 1: Get crashes for Anne Arundel County, MD
```r
crashes_detailed <- get_fars(
  year = 2019,
  state = "MD",
  county = "Anne Arundel County",
  details = TRUE
)

# Show 10 random fatal crashes
dplyr::slice_sample(crashes_detailed, n = 10)
```

##### Example 2: Map crashes in Wake County, NC
```r
# Download and convert to spatial data
crashes_sf <- get_fars(
  year = c(2018, 2021),
  state = "NC",
  county = "Wake County",
  geometry = TRUE
)

# Load county boundary
nc <- sf::st_read(system.file("shape/nc.shp", package = "sf"))
wake_co <- sf::st_transform(nc[nc$NAME == "Wake", ], 4326)

# Create map
library(ggplot2)
ggplot() +
  geom_sf(
    data = wake_co,
    fill = NA,
    color = "black"
  ) +
  geom_sf(
    data = sf::st_crop(crashes_sf, wake_co),
    aes(color = TOTALVEHICLES),
    alpha = 0.75
  ) +
  theme_void()
```

##### Example 3: Baltimore City
```r
# Get first 5 crashes from Baltimore city
head(get_fars_crashes(state = "MD", county = "Baltimore city"), 5)
```

**Additional Functions:**

#### get_fars_crash_list()
Returns list of fatal crashes in multiple states

#### get_fars_crash_details()
Returns details of specific fatal crash (requires crash ID)

#### get_fars_crashes()
Returns crashes by location throughout U.S.

**API Endpoints Used:**
- GetCaseList
- GetCrashDetails
- GetCrashes (location-based)

**Output Formats:**
- Data frame (tibble)
- Spatial features (sf object) with `geometry = TRUE`

**API Years:** 2010-2022 currently available

---

### Comparison: rfars vs crashapi

| Feature | rfars | crashapi |
|---------|-------|----------|
| **Data Source** | FTP bulk files | FARS API |
| **Years** | 2011+ (FARS), 2016+ (CRSS) | 2010-2022 |
| **County Filter** | Manual post-download | Built-in parameter |
| **Spatial Output** | No | Yes (sf objects) |
| **CRSS Access** | Yes | No |
| **Speed** | Faster (bulk) | Slower (API) |
| **Best For** | Large downloads, CRSS | County queries, mapping |

---

## VARIABLE CATEGORIES REFERENCE

This section provides a consolidated reference of crash data variables across major data sources.

### Crash-Level Variables

**Identifiers:**
- Crash ID (ST_CASE in FARS)
- State
- County
- Year
- Date (month, day)
- Time (hour, minute)
- Day of week

**Location:**
- Latitude/Longitude
- Route type (Interstate, US Highway, State, Local)
- Road name
- Milepoint
- Rural/Urban
- Functional class
- Relation to junction
- Type of intersection
- Work zone indicator
- School zone indicator (varies by state)

**Environment:**
- Weather conditions
- Road surface conditions
- Light conditions
- Visibility

**Crash Characteristics:**
- Number of vehicles
- Number of persons
- Number of fatalities
- Number injured (by severity)
- Manner of collision
- First harmful event
- Most harmful event

**Contributing Factors:**
- Speeding-related
- Alcohol-involved
- Drug-involved (limited quality)
- Hit and run

---

### Vehicle-Level Variables

**Identifiers:**
- Crash ID
- Vehicle number

**Vehicle Description:**
- Make
- Model
- Body type
- Model year
- VIN

**Vehicle Characteristics:**
- Travel speed
- Initial impact point
- Principal impact point
- Extent of damage
- Towaway indicator

**Events:**
- Rollover
- Fire/explosion
- Sequence of events (up to 4)
- Most harmful event

**Safety Systems:**
- Driver restraint use
- Air bag deployment

**Driver Characteristics:**
- License status
- Speeding
- Distracted driving
- Alcohol/drug involvement

---

### Person-Level Variables

**Identifiers:**
- Crash ID
- Vehicle number
- Person number

**Demographics:**
- Age
- Sex
- Race
- Hispanic origin

**Person Type:**
- Driver
- Passenger (by seating position)
- Pedestrian
- Bicyclist
- Other non-motorist

**Injury:**
- Injury severity (KABCO scale)
- Transported to hospital
- Dead on arrival
- Time of death
- Lag time to death

**Safety Equipment:**
- Restraint use
- Restraint misuse
- Air bag deployment
- Helmet use (motorcyclists, cyclists)

**Ejection:**
- Ejected status
- Ejection path

**Alcohol/Drugs:**
- Police-reported drinking
- BAC test result
- Drug test result
- Impairment determination

---

### Common Data Quality Issues

**FARS:**
- BAC data: 71% of killed drivers, 28% of surviving drivers (2013)
- Drug data: Inconsistent collection across jurisdictions - NHTSA cautions against use
- Exact crash location removed for privacy
- Multiple imputation used for missing BAC

**CRSS:**
- County-level identifiers removed for privacy
- Personal information excluded
- Sampling weights required for national estimates
- Not suitable for local-level analysis

**State Systems:**
- Variable quality and completeness across states
- Different coding systems
- Update frequencies vary
- Some states restrict public access
- Geocoding accuracy varies

**General:**
- Reporting thresholds differ by state
- Officer judgment in coding
- Delayed data entry
- Crashes on private property often not included
- Single-vehicle, non-injury crashes may be underreported

---

## BEST PRACTICES FOR COUNTY-LEVEL ANALYSIS

### Recommended Data Sources by Analysis Type

**Fatal Crashes Only:**
1. FARS (primary federal source)
2. State DOT systems (may have faster updates)
3. CDC WISQARS (for rates/public health perspective)

**All Crash Severities:**
1. State DOT crash databases (primary)
2. Local MPO/COG crash data systems
3. CRSS for national comparison only (not county-level)

**Specific Variables:**
- **Alcohol/Drugs:** FARS (best for alcohol, caution on drugs)
- **Demographics:** FARS, state systems
- **Vehicle Details:** FARS
- **Exact Locations:** State systems (with restrictions)
- **Injury Details:** State systems linked to hospital data (e.g., Minnesota MIDAS)

### Data Access Strategy

**1. Start with FARS for fatal crashes:**
- Use R packages (rfars or crashapi) for automated download
- Or use FIRST query tool for one-time queries
- Or download bulk files from FTP

**2. Supplement with state data for all severities:**
- Check state DOT portal for county
- Register for account if required
- Review data dictionary for variables available
- Note update frequency

**3. Validate and merge:**
- Check for duplicates if merging FARS + state
- Verify county FIPS codes match
- Document data sources and dates
- Note any suppressed cells

### Analysis Considerations

**Population Denominators:**
- Obtain county population from Census Bureau
- Use same year as crash data for rates
- Consider resident vs daytime population for urban areas

**Exposure Measures:**
- Vehicle Miles Traveled (VMT) by county
- Often available from state DOT or FHWA
- More accurate than population for crash rates

**Small Numbers:**
- Aggregate multiple years for small counties
- Use confidence intervals
- Consider suppression rules
- Age-adjustment may not be stable

**Temporal Patterns:**
- Account for day-of-week, time-of-day effects
- Seasonal variation
- COVID-19 impact (2020-2021)
- Holiday periods

---

## APPENDIX: KEY CONTACTS AND RESOURCES

### Federal Agencies

**NHTSA National Center for Statistics and Analysis**
- Address: 1200 New Jersey Avenue SE, Washington, DC 20590
- Phone: 800-934-8517
- Email: ncsarequests@dot.gov
- Website: https://www.nhtsa.gov/data

**CDC National Center for Injury Prevention and Control**
- WISQARS: https://wisqars.cdc.gov/
- Technical questions: Use WISQARS contact form

**FHWA Office of Safety**
- Website: https://highways.dot.gov/safety

### State DOT Contacts

(Refer to individual state sections above for specific URLs and contact methods)

### Professional Organizations

**Governors Highway Safety Association (GHSA)**
- Website: https://www.ghsa.org/

**Transportation Research Board (TRB)**
- Website: https://www.trb.org/

**Association of Transportation Safety Information Professionals (ATSIP)**
- Focus on traffic records professionals

---

## APPENDIX: VARIABLE CROSSWALK

*(To be developed: Mapping of common variables across FARS, MMUCC, and major state systems)*

---

## APPENDIX: COUNTY FIPS CODES

**Source:** U.S. Census Bureau
**URL:** https://www.census.gov/library/reference/code-lists/ansi.html

**Format:** 5-digit codes
- First 2 digits: State FIPS
- Last 3 digits: County FIPS

**Usage:** Required for merging FARS data with other county-level data

**R Package:**
```r
# tidycensus package includes FIPS lookup
library(tidycensus)
fips_codes
```

---

## REVISION HISTORY

| Date | Version | Changes |
|------|---------|---------|
| 2025-11-11 | 1.0 | Initial comprehensive documentation |

---

## NOTES FOR PRODUCTION USE

**Data Currency:**
- FARS: Check annually (September release)
- State systems: Check quarterly or as needed
- API endpoints: Verify before production deployment
- Contact information: Validate annually

**Automation:**
- R packages preferred for reproducibility
- Document package versions
- Error handling for API failures
- Cache data locally with timestamps

**Quality Assurance:**
- Cross-check totals with published reports
- Verify county FIPS codes
- Check for missing data patterns
- Document data cleaning steps

**Legal/Ethical:**
- Respect data use agreements
- Do not attempt to identify individuals
- Follow suppression rules for small counts
- Cite data sources appropriately
- Check license terms for redistribution

---

**END OF DOCUMENT**
