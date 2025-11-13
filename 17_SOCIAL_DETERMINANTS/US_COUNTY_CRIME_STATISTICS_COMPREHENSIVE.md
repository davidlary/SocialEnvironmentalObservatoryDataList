# US County-Level Crime Statistics: Comprehensive Data Source Documentation

**Report Date:** November 11, 2025
**Status:** Production-Ready Research
**Purpose:** Complete documentation of all available US county-level crime data sources, variables, and access methods

---

## TABLE OF CONTENTS

1. [Executive Summary](#executive-summary)
2. [FBI Uniform Crime Reports (UCR) / NIBRS](#1-fbi-uniform-crime-reports-ucr--nibrs)
3. [FBI Hate Crime Statistics](#2-fbi-hate-crime-statistics)
4. [FBI Human Trafficking Data](#3-fbi-human-trafficking-data)
5. [Bureau of Justice Statistics Data](#4-bureau-of-justice-statistics-data)
6. [State Crime Reporting Systems](#5-state-crime-reporting-systems)
7. [Additional Data Sources](#6-additional-data-sources)
8. [R Packages and Tools](#7-r-packages-and-tools)
9. [Important Limitations and Caveats](#8-important-limitations-and-caveats)
10. [Quick Reference: Access Methods](#9-quick-reference-access-methods)

---

## EXECUTIVE SUMMARY

### Critical Finding: County-Level Data Limitations

**⚠️ IMPORTANT:** True county-level aggregated crime data has significant quality issues. Experts recommend against using county-level UCR data due to:
- Poor imputation methods for missing data
- Incorrect distribution of crimes for agencies serving multiple counties
- Data quality issues that can lead to inaccurate research conclusions

### Recommended Approaches:

1. **Agency-Level Data** → Aggregate to counties yourself using proper methodology
2. **NIBRS Incident-Level Data** → Most detailed, incident-by-incident records
3. **State-Specific Portals** → Some states provide better county aggregations
4. **ICPSR Historical Data** → For historical research (with caveats)

### Data Transition (2021+)

The FBI transitioned from Summary Reporting System (SRS) to National Incident-Based Reporting System (NIBRS) as the standard in 2021. This represents a major shift:
- **SRS**: Summary counts of crimes
- **NIBRS**: Detailed incident-level data with demographics, relationships, locations, weapons, etc.
- **Coverage**: 95%+ of US population by 2024

---

## 1. FBI UNIFORM CRIME REPORTS (UCR) / NIBRS

### 1.1 Overview

**Primary Source:** FBI Crime Data Explorer (CDE)
**URL:** https://cde.ucr.cjis.gov/
**Data Collection:** ~18,000+ law enforcement agencies nationwide
**Coverage:** 95.1% of US population (2024)
**Update Frequency:** Quarterly releases on CDE
**Current Status:** Verified November 2025

### 1.2 Data Reporting Systems

#### Summary Reporting System (SRS) - Legacy (Pre-2021)
- Aggregate monthly crime counts
- Part I and Part II offenses
- Limited demographic detail
- Being phased out

#### National Incident-Based Reporting System (NIBRS) - Current Standard (2021+)
- Incident-level reporting
- 52 Group A offenses across 24 categories
- 11 Group B offenses (arrest data only)
- Detailed victim, offender, location, weapon data

### 1.3 PART I INDEX CRIMES (All Available at County Level via Agency Aggregation)

#### 1.3.1 Violent Crimes

##### Murder and Non-Negligent Manslaughter
- **NIBRS Code:** 09A
- **Description:** Willful killing of one human being by another
- **Variables Available:**
  - Count of offenses
  - Clearance status
  - Victim demographics (age, sex, race, ethnicity)
  - Offender demographics (when known)
  - Victim-offender relationship
  - Weapon type
  - Location type
  - Circumstances
- **Units:** Count, rate per 100,000 population
- **Years:** 1960-present (SRS), 2000-present (NIBRS)
- **Geographic Resolution:** Agency-level, aggregable to county

##### Rape
- **NIBRS Code:** 11A (except incest and statutory rape)
- **Legacy Definition (pre-2013):** "The carnal knowledge of a female forcibly and against her will"
- **Revised Definition (2013+):** "Penetration, no matter how slight, of the vagina or anus with any body part or object, or oral penetration by a sex organ of another person, without the consent of the victim"
- **Impact:** ~42.7% increase in reported rapes due to definition change
- **Variables Available:**
  - Count of offenses (legacy vs. revised definition)
  - Victim demographics
  - Offender demographics
  - Victim-offender relationship
  - Location type
  - Force/threat used
- **Units:** Count, rate per 100,000
- **Years:** 1960-present (with definition break in 2013)

##### Additional Sex Offenses (NIBRS Only)
- **09B - Sodomy:** Oral or anal sexual intercourse with another person, forcibly and/or against that person's will
- **11C - Sexual Assault with an Object:** Use of an object or instrument to unlawfully penetrate
- **11D - Criminal Sexual Contact (Fondling):** Touching of private body parts for sexual gratification, forcibly and/or against person's will
- **36A - Incest:** Non-forcible sexual intercourse between persons related within degrees
- **36B - Statutory Rape:** Non-forcible sexual intercourse with person under statutory age

##### Robbery
- **NIBRS Code:** 120
- **Description:** Taking or attempting to take anything of value by force, threat of force, or violence
- **Classification:** Person crime in SRS, Property crime in NIBRS
- **Robbery Types by Location:**
  - Highway/street robbery (34.3% of all robberies)
  - Commercial house robbery (16.7%)
  - Residence robbery (15.8%)
  - Convenience store (6.6%)
  - Gas/service station (3.0%)
  - Bank (1.4%)
  - Miscellaneous (22.2%)
- **Variables Available:**
  - Count by location type
  - Victim demographics
  - Offender demographics
  - Weapon type used
  - Property stolen/recovered
  - Injury to victims
  - Clearance status
- **Years:** 1960-present

##### Aggravated Assault
- **NIBRS Code:** 13A
- **Description:** Unlawful attack for purpose of inflicting severe bodily injury, usually with weapon
- **Weapon Types Tracked:**
  - Firearms (24.2% of aggravated assaults)
  - Knives/cutting instruments (18.1%)
  - Personal weapons - hands, fists, feet (26.3%)
  - Other weapons (31.4%)
- **Variables Available:**
  - Count by weapon type
  - Victim demographics
  - Offender demographics
  - Victim-offender relationship
  - Injury type
  - Location type
  - Clearance status
- **Years:** 1960-present

#### 1.3.2 Property Crimes

##### Burglary
- **NIBRS Code:** 220
- **Description:** Unlawful entry of structure to commit felony or theft
- **Three Subclassifications:**
  - **Forcible Entry:** Force used to gain entry (58.3-61.0%)
  - **Unlawful Entry (No Force):** No force used (32.6-35.2%)
  - **Attempted Forcible Entry:** Attempted but not completed (6.5%)
- **Variables Available:**
  - Count by entry type
  - Residence vs. non-residence
  - Time of day (day vs. night)
  - Property stolen/value
  - Property recovered
  - Location type
  - Clearance status
- **Years:** 1960-present

##### Larceny-Theft
- **NIBRS Code:** 23 (with subcategories)
- **Description:** Unlawful taking of property without force or fraud
- **Detailed Subcategories:**
  - **6Xa - Pocket-picking:** (0.6% of larcenies)
  - **6Xb - Purse-snatching:** (0.4%)
  - **6Xc - Shoplifting:** (22.2%)
  - **6Xd - Theft from motor vehicle:** (27.0%)
  - **6Xe - Theft of motor vehicle parts/accessories:** (6.5%)
  - **6Xf - Theft from coin-operated machine:** (0.2%)
  - **6Xg - Theft from building:** (10.0%)
  - **Bicycle theft:** (3.1%)
  - **6Xi - All other larceny:** Remainder
- **Variables Available:**
  - Count by subcategory
  - Value of property stolen
  - Property type
  - Location type
  - Clearance status
- **Years:** 1960-present

##### Motor Vehicle Theft
- **NIBRS Code:** 240
- **Description:** Theft or attempted theft of motor vehicle
- **Includes:** Automobiles, trucks, buses, motorcycles, motor homes, recreational vehicles
- **Excludes:** Taking for temporary use by persons with lawful access
- **Special Categories:**
  - Carjacking (tracked separately in some jurisdictions)
  - Auto parts theft (tracked under larceny-theft)
- **Variables Available:**
  - Count of thefts
  - Type of vehicle stolen
  - Vehicle recovery status
  - Value of vehicle
  - Location of theft
  - Clearance status
- **Years:** 1960-present
- **Additional Source:** National Insurance Crime Bureau (NICB) provides metropolitan/city-level data

##### Arson
- **NIBRS Code:** 200
- **Description:** Willful or malicious burning of property
- **Types of Property:**
  - Structural (residential, commercial, industrial, public)
  - Mobile (motor vehicles)
  - Other (crops, timber, etc.)
- **Variables Available:**
  - Count by property type
  - Value of property damage
  - Location type
  - Clearance status
  - Multiple factors involvement (tracked in NIBRS)
- **Years:** 1979-present (added to UCR in 1979)
- **Note:** Arson data collection and reporting quality varies significantly

### 1.4 PART II OFFENSES (Arrest Data Only at County Level)

Contributors provide **arrest data only** for Part II offenses. No offense counts are collected.

#### Simple Assault
- **NIBRS Code:** 13B
- **Description:** Unlawful attack where no weapon is used and no serious injury results
- **Data:** Arrest counts by age, sex, race

#### Fraud
- **Description:** Fraudulent conversion and obtaining money/property by false pretense
- **Includes:** Bad checks (except forgery), confidence games, credit card fraud, impersonation, welfare fraud, wire fraud
- **Data:** Arrest counts by demographics

#### Embezzlement
- **Description:** Misappropriation of money/property entrusted to one's care
- **Data:** Arrest counts by demographics

#### Forgery and Counterfeiting
- **NIBRS Code:** 250
- **Description:** Making, altering, uttering, or possessing false documents
- **Data:** Arrest counts by demographics

#### Vandalism
- **NIBRS Code:** 290 (Destruction/Damage/Vandalism of Property - Group A in NIBRS)
- **Description:** Willful destruction, injury, or defacement of property
- **Data:** Arrest counts by demographics
- **Note:** This is a Group A offense in NIBRS, so incident-level data available

#### Weapons Violations
- **Description:** Violations of regulations on manufacture, sale, purchase, transportation, possession, concealment, or use of firearms, cutting instruments, explosives, etc.
- **Data:** Arrest counts by demographics

#### Drug Offenses
- **NIBRS Codes:**
  - **35A - Drug/Narcotic Violations:** Manufacturing, distributing, selling, buying, using, possessing, transporting, or importing controlled substances
  - **35B - Drug Equipment Violations:** Unlawful manufacture, sale, purchase, possession, or transportation of drug equipment/paraphernalia
- **Drug Types Tracked in NIBRS:**
  - Crack Cocaine (A)
  - Cocaine - all forms except Crack (B)
  - Hashish (C)
  - Heroin (D)
  - Marijuana (E)
  - Morphine (F)
  - Opium (G)
  - Other Narcotics
  - Amphetamines/Methamphetamines (L)
  - Other Stimulants
  - Hallucinogens
  - Barbiturates
  - Depressants
- **Data:** Arrest counts by drug type, offense type (possession/sale/manufacture), demographics
- **Years:** 1960-present (arrests), 2000-present (NIBRS incident details)

#### Sex Offenses (Other than Rape)
- **NIBRS Codes:** Various including prostitution, pornography, indecent exposure, peeping tom
- **Description:** Offenses against chastity, common decency, morals
- **Data:** Arrest counts by demographics

#### Gambling
- **Description:** Unlawful betting, promoting/operating games of chance, possessing gambling equipment
- **Types:**
  - Betting/wagering
  - Operating/promoting/assisting gambling
  - Gambling equipment violations
  - Sports tampering
- **Data:** Arrest counts by type and demographics

#### Prostitution and Commercialized Vice
- **Description:** Unlawful promotion or participation in sexual activities for profit
- **NIBRS Enhancement (2013+):** More specific offense codes
  - Prostitution
  - Assisting or promoting prostitution
  - Purchasing prostitution
- **Data:** Arrest counts by demographics

#### Liquor Law Violations
- **Description:** Violations of state/local liquor laws (except DUI and drunkenness)
- **Includes:** Manufacturing, selling, transporting, possessing, furnishing alcohol
- **Data:** Arrest counts by demographics

#### Driving Under the Influence (DUI)
- **Group B Code:** 90D
- **Description:** Driving or operating vehicle while impaired
- **Data:** Arrest counts by demographics

#### Drunkenness
- **Group B Code:** 90E
- **Description:** Public intoxication (except DUI)
- **Data:** Arrest counts by demographics

#### Disorderly Conduct
- **Group B Code:** 90C
- **Description:** Unlawful disruption of peace
- **Data:** Arrest counts by demographics

#### Family Offenses (Non-Violent)
- **Group B Code:** 90F
- **Description:** Unlawful non-violent acts against family members
- **Includes:** Neglect, desertion, abandonment, non-payment of support
- **Data:** Arrest counts by demographics

#### Vagrancy
- **Description:** Begging, loitering (where prohibited by law)
- **Data:** Arrest counts by demographics

#### Curfew/Loitering Violations (Juveniles)
- **Group B Code:** 90B
- **Description:** Violations of curfew ordinances by juveniles
- **Data:** Juvenile arrest counts

#### Runaways (Juveniles)
- **Description:** Juvenile runaways (no longer widely reported)
- **Data:** Juvenile arrest counts

### 1.5 CLEARANCE RATES

**Definition:** A crime is "cleared" when at least one person is arrested, charged, and turned over for prosecution, or by exceptional means (e.g., death of offender, victim refuses to cooperate).

**Variables Available:**
- Clearances by arrest for all Part I offenses
- Clearances by exceptional means
- Clearances involving only juveniles
- Clearances by offense type
- Time from offense to clearance

**Geographic Levels:**
- Agency-level (primary)
- Aggregable to county
- Available through FBI CDE and ICPSR

**Years:** 1960-present

**Data Sources:**
- FBI Crime Data Explorer
- ICPSR: Offenses Known and Clearances by Arrest datasets
- Vera Institute Arrest Trends Tool (county-level visualization)

**Important Limitations:**
- Not designed to assess complete law enforcement effectiveness
- Does not capture all case dispositions
- Varies significantly by crime type and jurisdiction

### 1.6 LAW ENFORCEMENT EMPLOYEE DATA (LEOKA)

**Full Name:** Law Enforcement Officers Killed and Assaulted

**LEOKA Variables Available:**

#### Agency Staffing
- **Officers Employed:**
  - Full-time sworn officers (male/female breakdown)
  - Part-time sworn officers
  - Full-time civilians
  - Part-time civilians
- **Officers per Capita:**
  - National average: 2.4 per 1,000 inhabitants
  - County agencies: 2.8 per 1,000 inhabitants
  - Varies by jurisdiction size

#### Officers Killed
- **Felonious Deaths:**
  - Circumstances of death
  - Weapon used
  - Type of assignment
  - Activity at time of incident
- **Accidental Deaths:**
  - Type of accident
  - Activity at time

#### Officers Assaulted
- **Assault Data:**
  - Number of assaults
  - Type of weapon/force
  - Assignment type
  - Injury status
  - Circumstances

**Geographic Level:** Agency-level with county FIPS codes

**Years:** 1960-2021 (historical data), continuing

**Access:**
- FBI Crime Data Explorer
- ICPSR OpenICPSR: Jacob Kaplan's Concatenated Files (1960-2021)

### 1.7 ARREST DATA BY DEMOGRAPHICS

**Available Through "Arrests by Age, Sex, and Race" (ASR) Dataset**

**⚠️ IMPORTANT:** FBI retired this data series after 2020. Last release was 2021 data.

#### Age Breakdowns
- **Detailed Ages:** 15-24 (yearly)
- **Age Groups:** Under 10, 10-12, 13-14, 25-29, 30-34, 35-39, 40-44, 45-49, 50-54, 55-59, 60-64, 65+
- **Juvenile vs. Adult:** Under 18 vs. 18+

#### Sex
- Male
- Female

#### Race Categories
- American Indian/Alaska Native
- Asian/Pacific Islander
- Black/African American
- White
- Unknown

#### Ethnicity
- Hispanic/Latino
- Non-Hispanic/Latino

**Available For:** All Part I and Part II offenses

**Geographic Level:** Agency-level, aggregable to county

**Years:** 1974-2021 (county-level: 1974-2016)

**Access:**
- ICPSR: Study numbers vary by year
- OpenICPSR: Jacob Kaplan's Concatenated Files (1974-2021)

**Variables Include:**
- Total arrests by offense
- Arrests by offense, age, sex
- Arrests by offense, race, age
- Arrests by offense, ethnicity, age

### 1.8 NIBRS ADDITIONAL VARIABLES (Incident-Level Only)

Beyond basic crime counts, NIBRS provides:

#### Victim Information
- Age, sex, race, ethnicity
- Resident status
- Victim type (individual, business, society, etc.)
- Injury type and severity
- Victim-offender relationship (35+ categories)

#### Offender Information
- Age, sex, race, ethnicity (when known)
- Suspected drug/alcohol use
- Number of offenders involved

#### Incident Characteristics
- Date and time (hour-level precision)
- Multiple offense types per incident
- Location type (46+ categories - see Section 1.9)
- Premises entered (for burglary)
- Method of entry
- Criminal activity type
- Gang-related indicator
- Drug type and quantity (for drug offenses)

#### Property Information
- Property type (68+ categories)
- Value of property
- Stolen/recovered status
- Property description
- Date recovered

#### Arrestee Information
- Arrest date
- Offense arrested for
- Weapon carried during arrest
- Disposition of juvenile arrestees

### 1.9 NIBRS LOCATION TYPES (46+ Categories)

**Code | Location Type**
- 01 | Air/Bus/Train Terminal
- 02 | Bank/Savings and Loan
- 03 | Bar/Night Club
- 04 | Church/Synagogue/Temple
- 05 | Commercial/Office Building
- 06 | Construction Site
- 07 | Convenience Store
- 08 | Department/Discount Store
- 09 | Drug Store/Doctor's Office/Hospital
- 10 | Field/Woods
- 11 | Government/Public Building
- 12 | Grocery/Supermarket
- 13 | Highway/Road/Alley
- 14 | Hotel/Motel
- 15 | Jail/Prison
- 16 | Lake/Waterway
- 17 | Liquor Store
- 18 | Parking Lot/Garage
- 19 | Rental Storage Facility
- 20 | Residence/Home (includes apartments, condos, nursing homes)
- 52 | School - College/University
- 53 | School - Elementary/Secondary
- (And many more...)

**Usage:** Critical for spatial analysis and understanding crime contexts

---

## 2. FBI HATE CRIME STATISTICS

### 2.1 Overview

**Collection:** Part of UCR Program, separate dataset
**Participation:** 16,419 agencies in 2024
**Coverage:** 95.1% of US population
**Latest Data:** 2024 (released 2025)
**Status:** Verified November 2025

### 2.2 Hate Crime Variables

#### Incident Counts
- **2024 Statistics:** 11,679 criminal incidents, 13,683 related offenses
- **Geographic Levels:** Agency, state, judicial district
- **County Data:** Available through agency aggregation

#### Offense Types (All Part I and Part II offenses can be hate crimes)
- Murder and non-negligent manslaughter
- Rape
- Aggravated assault
- Simple assault
- Intimidation
- Robbery
- Burglary
- Larceny-theft
- Motor vehicle theft
- Arson
- Destruction/damage/vandalism of property
- Other offenses

### 2.3 Bias Motivation Categories (6 Major Types)

#### Race/Ethnicity/Ancestry Bias (63.1% of single-bias incidents)
- Anti-Black or African American
- Anti-White
- Anti-Hispanic or Latino
- Anti-Asian
- Anti-American Indian or Alaska Native
- Anti-Arab
- Anti-Native Hawaiian or Other Pacific Islander
- Anti-Multiple Races, Group
- Anti-Other Race/Ethnicity/Ancestry

#### Religious Bias
- Anti-Jewish
- Anti-Islamic (Muslim)
- Anti-Catholic
- Anti-Protestant
- Anti-Other Christian
- Anti-Mormon
- Anti-Jehovah's Witness
- Anti-Eastern Orthodox (Greek, Russian, etc.)
- Anti-Other Religion
- Anti-Buddhist
- Anti-Hindu
- Anti-Sikh
- Anti-Atheism/Agnosticism
- Anti-Multiple Religions, Group

#### Sexual Orientation Bias
- Anti-Gay (Male)
- Anti-Lesbian
- Anti-Lesbian, Gay, Bisexual, or Transgender (Mixed Group)
- Anti-Bisexual
- Anti-Heterosexual

#### Disability Bias
- Anti-Physical Disability
- Anti-Mental Disability

#### Gender Bias
- Anti-Male
- Anti-Female

#### Gender Identity Bias
- Anti-Transgender
- Anti-Gender Non-Conforming

### 2.4 Victim Types
- Individual persons
- Business/financial institution
- Government
- Religious organization
- Society/public
- Other/unknown

### 2.5 Data Access

**Primary:** FBI Crime Data Explorer → Hate Crime Statistics
**Historical:** ICPSR archives hate crime component of UCR
**Years:** 1991-present
**Format:** CSV, JSON via API, Excel downloads

**Variables Include:**
- Incident ID
- Offense type
- Bias motivation(s) (up to 5 per incident)
- Victim type
- Number of victims
- Offender race (if known)
- Location type

---

## 3. FBI HUMAN TRAFFICKING DATA

### 3.1 Overview

**Added to NIBRS:** 2013
**Coverage:** Agencies reporting NIBRS data
**Status:** Verified November 2025

### 3.2 Offense Types

#### 64A - Human Trafficking, Commercial Sex Acts
- **Description:** Inducing person by force, fraud, or coercion to participate in commercial sex acts, or person induced is under 18
- **Variables:**
  - Victim demographics
  - Offender demographics
  - Victim-offender relationship
  - Location
  - Number of victims
  - Method of force/coercion

#### 64B - Human Trafficking, Involuntary Servitude
- **Description:** Labor trafficking through force, fraud, or coercion
- **Variables:** Same as 64A

### 3.3 Geographic Availability

- **Level:** Agency-level NIBRS data
- **County Access:** Aggregate agency data to county
- **Years:** 2013-present (where agencies report NIBRS)

### 3.4 Data Access

**Primary:** FBI Crime Data Explorer → NIBRS data
**API:** crime-data-api.fr.cloud.gov (requires API key)
**Format:** JSON, CSV

---

## 4. BUREAU OF JUSTICE STATISTICS DATA

### 4.1 Overview

**Agency:** Office of Justice Programs, US Department of Justice
**Website:** https://bjs.ojp.gov
**Status:** Federal websites not regularly updated due to government situation (as of Nov 2025)

### 4.2 National Crime Victimization Survey (NCVS)

**⚠️ LIMITATION:** National and limited subnational estimates only - **NO county-level data directly available**

**Geographic Levels:**
- National estimates
- Limited regional estimates
- Some metropolitan area estimates
- **NOT available:** County-level

**What NCVS Provides:**
- Victimization rates (reported and unreported to police)
- Victim characteristics
- Offender characteristics (as perceived by victim)
- Crime circumstances
- Consequences of victimization
- Response to victimization

**Years:** 1973-present

**Access:**
- BJS N-DASH (National Crime Victimization Survey Dashboard)
- ICPSR datasets
- BJS publications

**Use for County Research:** Can be used with NIBRS to adjust for underreporting

### 4.3 Annual Survey of Jails (MAJOR 2025 CHANGE)

**Historical:** Annual Survey of Jails (ASJ) sampled ~950 jails (1982-2023)

**NEW 2025+:** Annual Census of Jails (COJ) - ALL ~2,800 jails

#### Census of Jails (2025+)

**Coverage:**
- All city, county, regional, and private jails
- 12 Federal Bureau of Prisons detention facilities operating as jails
- **Total:** ~2,800 facilities

**Reference Date:** Last Monday of December (2025 reference: December 29, 2025)

**Variables:**
- Number of inmates confined (by sex, race, ethnicity, age)
- Jail capacity (rated capacity)
- Number of admissions
- Number of releases
- Average daily population
- Number of inmates held for other authorities
- Staff counts (correctional officers, other staff)
- Inmate deaths
- Special populations (juveniles, non-citizens)

**Geographic Level:** **TRUE COUNTY-LEVEL DATA** (facility addresses include county)

**Years:**
- ASJ (sampled): 1982-2023 (excluding 1983, 1988, 1993, 1999, 2005, 2019)
- COJ (complete): 2025-present

**Access:**
- BJS publications
- ICPSR datasets (Study 39202 for 2023 ASJ)
- Future COJ data through BJS

**Significance:** This is one of the best true county-level criminal justice datasets available

### 4.4 Survey of Inmates in Local Jails (SILJ)

**Survey:** In-person interviews with jail inmates
**Latest:** 2024-2025 (in progress as of Nov 2025)
**Previous:** 2002
**Geographic Level:** National estimates, not county-specific

**Variables:**
- Current offense and criminal history
- Socioeconomic characteristics
- Family background
- Drug and alcohol use
- Mental and physical health
- Educational programs
- Use of community-based programs

### 4.5 Law Enforcement Management and Administrative Statistics (LEMAS)

**Survey Frequency:** Periodic (most recent: 2020)
**Coverage:** All publicly funded state, county, local, and tribal law enforcement agencies

**Variables:**
- Agency characteristics
- Personnel (number, demographics, salaries)
- Operating expenditures
- Equipment and technology
- Policies and procedures
- Community policing
- Functions (patrol, investigations, etc.)

**Geographic Level:** Agency-level with county identifiers

**Years:** Multiple surveys since 1987 (1987, 1990, 1993, 1997, 1999, 2000, 2003, 2007, 2013, 2016, 2020)

**Access:** ICPSR

### 4.6 Census of State and Local Law Enforcement Agencies (CSLLEA)

**Survey Type:** Complete enumeration of all agencies
**Latest:** 2018
**Previous:** 2008, 2004, 2000, 1996, 1992

**Variables:**
- Number of sworn officers
- Number of civilian employees
- Agency type
- Functions/responsibilities
- Jurisdiction characteristics

**Geographic Level:** Agency-level, aggregable to county

**Access:** ICPSR, BJS publications

### 4.7 Prosecution and Court Statistics (LIMITED COUNTY DATA)

#### State Court Processing Statistics (SCPS)
- **Coverage:** Sample of 300 counties
- **Variables:** Felony defendant processing from arrest through sentencing
- **Available:** Sex, race, age, prior record, pretrial release, adjudication, sentencing
- **Years:** Various (1990, 1992, 1994, 1996, 1998, 2000, 2002, 2004, 2006, 2009)

#### National Judicial Reporting Program (NJRP)
- **Coverage:** 300 counties
- **Variables:** Persons convicted of felonies in state courts
- **Years:** Various (1986, 1988, 1990, 1992, 1994, 1996, 1998, 2000, 2002, 2004, 2006, 2009)

#### PROMIS (Historical - 1970s-1980s)
- **Prosecutor's Management Information System**
- **Jurisdictions:** Washington DC, St. Louis, Portland
- **Variables:** Detailed case processing from arrest through disposition
- **Access:** ICPSR historical studies

**Limitation:** Court/prosecution data typically NOT available for all counties, only samples

### 4.8 NIBRS National Estimates API

**Important BJS Resource:** National-level estimates from NIBRS data

**URL:** https://bjs.ojp.gov/national-incident-based-reporting-system-nibrs-national-estimates-api

**Geographic Levels:**
- National
- State
- City size categories
- **NOT county-level** in public national estimates

**Variables:** All NIBRS offense, victim, offender characteristics

**Use:** For national context, not county research

---

## 5. STATE CRIME REPORTING SYSTEMS

### 5.1 Overview

Law enforcement agencies report to FBI either:
1. **Directly to FBI** (~30% of agencies)
2. **Through State UCR Program** (~70% of agencies) → State program then sends to FBI

**Advantage of State Programs:** Often provide enhanced county-level data and more user-friendly interfaces than FBI

### 5.2 States with Strong County-Level Crime Data Portals

#### California
**Portal:** https://oag.ca.gov/crime
**Operator:** California Department of Justice
**Data Available:**
- Crime data by county
- Arrest data by county
- Hate crime statistics
- Law enforcement disposition data
- Domestic violence data
- Missing persons
- Downloadable datasets (last 10 years)

**Features:**
- Historical publications
- CSV downloads
- Interactive dashboards
- Monthly and annual reports

**Quality:** ⭐⭐⭐⭐⭐ Excellent

#### Pennsylvania
**Portal:** https://www.ucr.pa.gov/PAUCRSPUBLIC/Home/Index
**Name:** Crime in Pennsylvania Dashboard
**Operator:** Pennsylvania State Police
**Data Available:**
- UCR data by county
- Part I and Part II offense data
- Arrest statistics
- Interactive visualizations

**Quality:** ⭐⭐⭐⭐ Very Good

#### Illinois
**Portal:** https://www.isp.state.il.us/crime/ucrhome.cfm
**Name:** Crime in Illinois
**Operator:** Illinois State Police
**Data Available:**
- UCR data by county
- NIBRS resources and documentation
- Annual publications
- Historical data

**Quality:** ⭐⭐⭐⭐ Very Good

#### Texas
**Operator:** Texas Department of Public Safety
**Data Available:**
- UCR data (access methods vary)
- Crime reporting statistics

**Quality:** ⭐⭐⭐ Good (data availability varies)

#### Florida
**⚠️ WARNING:** Data quality issues
**Problem:** In 2022, Florida reported only 7.7% of their crime data. Similar issues may affect 2023-2024 data.
**Recommendation:** Use Florida county data with extreme caution

#### New York
**Operator:** NY Division of Criminal Justice Services
**Portal:** https://www.criminaljustice.ny.gov/crimnet/ojsa/stats.htm
**Data Available:**
- County and agency data
- Arrests, index crimes
- Various reports

**Quality:** ⭐⭐⭐⭐ Very Good

### 5.3 Other State UCR Programs

Most states operate UCR programs. Key resources:

**Iowa:** https://dps.iowa.gov (Public portal available)
**Ohio:** Through state police (specific portal varies)
**Colorado:** https://cbi.colorado.gov (Colorado Bureau of Investigation)
**Kansas:** https://www.kansas.gov/kbi/stats/
**Arkansas:** https://dps.arkansas.gov (Arkansas State Police)
**Missouri:** Through State Highway Patrol
**Indiana:** Indiana State Police
**Michigan:** Michigan State Police

### 5.4 How to Find Your State's UCR Data

1. Search: "[State name] UCR program" or "[State name] crime statistics"
2. Check state police or state bureau of investigation website
3. Look for "crime statistics," "UCR," or "NIBRS" sections
4. Check Data.gov for state datasets: https://catalog.data.gov/dataset?tags=crime
5. Contact state UCR program coordinator (listed in FBI publications)

### 5.5 Enhanced State Data

Some states provide variables beyond FBI requirements:
- **Domestic violence flags** (many states)
- **Gang-related indicators** (California, Illinois, others)
- **Enhanced location data** (specific addresses in some jurisdictions)
- **Victim services information**
- **Additional demographics**

---

## 6. ADDITIONAL DATA SOURCES

### 6.1 DEA Drug Seizure Data (STRIDE)

**Full Name:** System to Retrieve Information from Drug Evidence

**Coverage:** DEA drug buys and seizures sent to DEA laboratories

**Variables:**
- Drug type
- Drug purity
- Drug price
- Seizure date
- Location (state-level primarily)

**⚠️ COUNTY-LEVEL LIMITATION:** Not publicly available at county level

**Access:** Researchers must work directly with DEA. Data is not a random sample and represents only seizures sent to DEA labs.

**Alternative:** Look to state-level drug task force data or health department overdose data

**Status:** Historical STRIDE data available through research requests

### 6.2 ATF Firearms Trace Data

**Operator:** Bureau of Alcohol, Tobacco, Firearms and Explosives
**Data:** National Tracing Center firearms trace data

**Public Data Available:**
- **State-level:** Annual reports by state
- **City-level:** Top 10-15 cities per state (varies by year)
- **NOT County-level**

**Legal Restrictions:** Congress has restricted ATF from publicly releasing most trace information. Tiahrt Amendment limits data sharing.

**What's Tracked:**
- Firearms recovered and traced
- Type of firearm
- Time-to-crime (time from purchase to recovery)
- Source state
- Destination state

**Years:** 2014-2023 (comprehensive state-level)

**Access:**
- ATF website: https://www.atf.gov/resource-center/data-statistics
- The Trace cleaned datasets: https://datahub.thetrace.org/

**For County Research:** Generally not available

### 6.3 National Insurance Crime Bureau (NICB) - Vehicle Theft

**Focus:** Vehicle theft and insurance crime

**Geographic Levels:**
- State
- Metropolitan Statistical Areas (MSAs) / Core-Based Statistical Areas (CBSAs)
- Cities

**⚠️ COUNTY LIMITATION:** Data organized by MSAs, not counties. Some MSAs encompass multiple counties.

**Reports:**
- Hot Spots Reports (geographic analysis)
- Vehicle Theft Trend Reports
- Specific analyses (carjacking trends, etc.)

**Variables:**
- Vehicle thefts by location
- Vehicle make/model rankings
- Theft trends over time
- Carjacking incidents (major metro areas)

**Years:** 2019-present (recent reports)

**Access:** https://www.nicb.org/news/reports-statistics

**Data Source:** National Crime Information Center (NCIC)

### 6.4 Juvenile Justice Data (OJJDP)

**Operator:** Office of Juvenile Justice and Delinquency Prevention
**Website:** https://ojjdp.ojp.gov/statistics

**⚠️ MIXED COUNTY AVAILABILITY:** Some datasets have county data, others do not

#### Easy Access Tools with County Data:

**1. Easy Access to FBI Arrest Statistics (EZAUCR)**
- **County-Level:** YES
- **Variables:** Juvenile arrests for 29 offense categories
- **Geography:** National, state, county
- **URL:** https://www.ojjdp.gov/ojstatbb/ezaucr/

**2. Easy Access to Juvenile Populations (EZAPOP)**
- **County-Level:** YES
- **Variables:** Population by age, sex, race, ethnicity
- **Geography:** National, state, county
- **Years:** 1990-2022
- **Use:** Denominators for calculating juvenile crime rates

**3. Easy Access to State and County Juvenile Court Case Counts**
- **County-Level:** YES
- **Variables:** Juvenile court case processing
- **Geography:** National, state, county
- **Years:** Varies

**4. Easy Access to Juvenile Court Statistics (EZAJCS)**
- **Years:** 1985-2022
- **Variables:** Court case processing, dispositions
- **Geography:** National, state estimates (limited county)

#### Juvenile Residential Facility Census (JRFCDB)
- **Geographic Level:** State, not county
- **Variables:** Youth in residential placement facilities
- **Years:** 1997-present (biennial)

**Access:** All via OJJDP Statistical Briefing Book

### 6.5 National Gang Center Data

**Survey:** National Youth Gang Survey (NYGS)
**Coverage:** Sample of 2,500+ law enforcement agencies
**Response Rate:** ~85%

**Geographic Coverage:**
- All police departments serving cities 50,000+ population (n=624)
- All suburban county police/sheriffs (n=739)
- Random sample of rural county police/sheriffs (n=492)

**County-Level Variables:**
- Gang problem prevalence (yes/no)
- Number of gangs
- Number of gang members
- Gang-related homicides
- Gang-related offenses (violent and property)
- Demographics of gang members

**Years:** 1996-2012 (annual surveys)

**2012 Statistics:**
- 50% of suburban counties reported gang problems
- 16% of rural counties reported gang problems
- 17% of gang homicides in suburban counties
- 75% of rural counties with gangs reported zero gang homicides

**⚠️ IMPORTANT LIMITATIONS:**
- Surveys ended in 2012
- Data quality concerns around gang-crime definitions
- Incomplete and inconsistent gang-crime statistics
- Caution urged when interpreting results

**Access:**
- National Gang Center: https://nationalgangcenter.ojp.gov/survey-analysis
- ICPSR datasets

### 6.6 Domestic Violence / Intimate Partner Violence Data

**Primary Source:** NIBRS incident data

**NIBRS Variables:**
- Victim-offender relationship (includes intimate partner categories)
- Offense types (assault, intimidation, sex offenses, homicide)
- Demographics of victims and offenders
- Location of incident
- Weapons used
- Injuries sustained

**Methodology for County Estimates:**
- Use NIBRS reported incidents
- Adjust for underreporting using NCVS national rates
- Model-based estimation for counties with good NIBRS coverage

**Example:** Las Vegas 2022
- 1,437 aggravated DV incidents in NIBRS
- Adjusted for ~70% reporting rate = ~2,000 estimated actual incidents

**Alternative Sources:**
- State domestic violence coalitions
- County-level protection order data
- Specialized domestic violence reports from states

**BJS Publication:** "Family Violence Statistics" (periodic)

### 6.7 Data.gov Crime Datasets

**Portal:** https://catalog.data.gov/dataset?tags=crime

**County-Level Datasets Available:**
- Some California county crime data
- Various state and local submissions
- Federal crime data
- Specialized datasets (school crime, etc.)

**Search Tips:**
- Filter by geographic coverage
- Check data dictionary for county identifiers
- Download options usually include CSV
- Quality and coverage vary significantly

**Note:** Most Data.gov crime data is city/municipal level, not county

---

## 7. R PACKAGES AND TOOLS

### 7.1 R Package: fbiAPI

**Package Name:** `fbiAPI` (also listed as `fbi` in some repositories)
**Developer:** Jacob Kaplan
**Status:** Available on GitHub

**Installation:**
```r
# Install from GitHub
# devtools::install_github("jacobkap/fbiAPI")
```

**Functionality:**
- Wrapper for FBI Crime Data API
- Access UCR data (Offenses Known, Arrests, LEOKA, NIBRS)
- Returns data as R data frames
- Simplifies API queries

**API Key Required:** YES - obtain from https://api.data.gov/signup/

**Example Use:**
```r
library(fbiAPI)

# Get agency data
agencies <- fbi_api_agencies()

# Get offense data
offenses <- fbi_api_offenses(state = "CA", year = 2020)
```

**Documentation:** https://rdrr.io/github/jacobkap/fbiAPI/

### 7.2 R Package: crimedata (if available)

**Note:** Search did not find a package specifically called "crimedata" in Nov 2025 search. Main package is fbiAPI.

### 7.3 FBI Crime Data API (Direct Access)

**API Base URL:** https://api.usa.gov/crime/fbi/sapi/
**Swagger Documentation:** https://crime-data-api.fr.cloud.gov/swagger-ui/
**GitHub:** https://github.com/fbi-cde/crime-data-api

**Authentication:** API key required (from api.data.gov)

**Key Endpoints:**
- `/agencies` - Agency information
- `/incidents` - NIBRS incident data
- `/incidents/count` - Incident counts
- `/codes/` - Field codes and possible values
- Various offense-specific endpoints

**Return Formats:** JSON, CSV

**Rate Limits:** Standard api.data.gov limits (1,000 requests/hour)

**Important Notes:**
- 2025 API updates changed some endpoint locations
- All datasets remain available with modified paths
- Static swagger.json (not dynamically generated)

### 7.4 Other Tools

#### Python Libraries
- **FBI Crime Data API:** Direct API calls using `requests` library
- **pandas:** For data manipulation
- **geopandas:** For spatial analysis

#### Example Python Code:
```python
import requests
import pandas as pd

api_key = "YOUR_API_KEY"
url = "https://api.usa.gov/crime/fbi/sapi/api/data/nibrs/offense/states/CA"
params = {"api_key": api_key}

response = requests.get(url, params=params)
data = response.json()
df = pd.DataFrame(data['results'])
```

#### GitHub Repository with R Script Example
- **Repository:** SeyvanGit/UCR-Violent-Crime-Data
- **Functionality:** Downloads violent crime statistics for all 50 states from FBI CDE API
- **Output:** Monthly and yearly summary CSVs

### 7.5 ICPSR Data Access

**Institution:** Inter-university Consortium for Political and Social Research
**Affiliation:** University of Michigan
**URL:** https://www.icpsr.umich.edu/web/NACJD/series/57

**Access Levels:**
- **Public Use:** Free, no membership required
- **Restricted Use:** Requires membership/approval

**Download Formats:**
- SPSS
- Stata
- SAS
- R
- CSV
- Excel

**Key Series:**
- UCR Program Data Series (Series 57)
- National Archive of Criminal Justice Data (NACJD)

---

## 8. IMPORTANT LIMITATIONS AND CAVEATS

### 8.1 County-Level UCR Data Quality Issues

**⚠️ CRITICAL WARNING:** Experts strongly recommend against using county-level UCR aggregated files.

**Problems Identified:**

1. **Missing Data Imputation:**
   - Agencies with missing data have values imputed
   - Imputation methods are flawed
   - Creates artificially "complete" data that is actually inaccurate

2. **Multi-County Agencies:**
   - Some agencies serve multiple counties
   - Crime distribution across counties is poorly handled
   - Can double-count or misallocate crimes

3. **Incomplete Reporting:**
   - Not all agencies in a county report
   - Aggregated files handle this inconsistently
   - Can significantly under- or overestimate true county totals

4. **Population Allocation Issues:**
   - Statewide agencies (e.g., highway patrol) allocated by population
   - May not reflect actual geographic distribution of crimes

**Expert Recommendation (Maltz & Targonski):**
"County-level UCR data should not be used for research, especially in policy studies, until improved methods are developed."

**Better Alternatives:**
- Use **agency-level data** and aggregate yourself with documented methodology
- Use **NIBRS incident-level data** with precise location information
- Use **state-provided county data** (some states do better aggregations)

### 8.2 UCR/NIBRS Reporting Limitations

**Voluntary Reporting:**
- No agency is required to report
- Coverage varies by year and state
- Some jurisdictions never report

**Hierarchy Rule (SRS only):**
- Only most serious offense per incident counted in SRS
- NIBRS eliminates this, reports all offenses
- Makes SRS-to-NIBRS comparisons difficult

**Reporting Quality:**
- Varies by agency
- Training and resources affect accuracy
- Some crimes misclassified

**Underreporting by Public:**
- UCR only includes crimes reported to police
- Many crimes (especially sexual assault, domestic violence) underreported
- Use NCVS to estimate true victimization

### 8.3 SRS to NIBRS Transition Issues (2021)

**Major Data Break:**
- 2021: FBI moved to NIBRS-only reporting
- Agencies not NIBRS-ready dropped out
- Significant coverage gaps in 2021 data

**Comparability Issues:**
- SRS summary counts vs. NIBRS incident-level
- Different offense definitions
- Different hierarchy rules
- Trending across 2021 break is problematic

**State-by-State Transition:**
- Some states transitioned early (2000s)
- Some states transitioned late (2020-2021)
- Creates uneven time series

**Florida Example:**
- 2022: Only 7.7% data reported
- Massive data quality problem
- Use Florida data 2021+ with extreme caution

### 8.4 Clearance Rate Limitations

**Not a Complete Measure:**
- Only measures arrests, not convictions
- Does not capture case dispositions
- "Cleared" ≠ "solved" or "prosecuted successfully"

**Gaming Concerns:**
- Agencies may manipulate clearance statistics
- Pressure to show high clearance rates
- Exceptional clearance may be overused

**Variation:**
- Clearance rates vary dramatically by crime type
- Murder: ~60% cleared
- Property crimes: ~15-20% cleared
- Not comparable across crime types

### 8.5 Hate Crime Reporting Issues

**Severe Underreporting:**
- Many agencies report zero hate crimes (implausible)
- Victim underreporting to police
- Police underidentification of bias motivation

**Bias Determination:**
- Subjective judgment required
- Training varies
- Evidence requirements differ

**Coverage Gaps:**
- Not all agencies participate
- Quality varies dramatically

### 8.6 LEOKA Data Limitations

**Limited Scope:**
- Only officers killed/assaulted
- Does not capture all officer safety issues
- Does not include non-assault incidents

**Reporting Variation:**
- Assault definitions vary
- Some minor assaults may not be reported
- Focus on serious incidents

### 8.7 Arrest Data Limitations (Retired 2021)

**⚠️ NO LONGER COLLECTED:** FBI retired Arrests by Age, Sex, and Race after 2020.

**Historical Data Issues:**
- Racial categories limited and problematic
- Ethnicity data often missing
- Does not reflect case outcomes
- Arrest ≠ guilty

### 8.8 NIBRS Data Advantages and Limitations

**Advantages:**
- Incident-level detail
- No hierarchy rule
- Rich contextual information
- Better for research

**Limitations:**
- Complexity (harder to use)
- Large file sizes
- Transition period coverage gaps
- Still voluntary reporting
- Still subject to police reporting practices

### 8.9 Jail Data Limitations

**Historical ASJ (pre-2025):**
- Sample survey, not complete count
- Estimation error for small counties
- Missing data for non-sampled counties

**New COJ (2025+):**
- Complete count (much better!)
- One-day snapshot (not average daily population trend)
- Does not include those in state prison
- Does not include federal facilities (except those operating as jails)

### 8.10 Juvenile Justice Data Limitations

**Coverage:**
- Not all jurisdictions report
- Court data especially limited
- Definitions vary by state

**Confidentiality:**
- Juvenile records often sealed
- Limits data availability
- Aggregate data only

### 8.11 Gang Data Limitations (Survey Ended 2012)

**Major Problem:** NYGS ended in 2012, no recent data

**Definition Issues:**
- No standard gang definition
- Agency definitions vary
- What counts as "gang-related" varies

**Coverage:**
- Sample survey
- Not all counties included
- Small county estimates unreliable

---

## 9. QUICK REFERENCE: ACCESS METHODS

### 9.1 Interactive Web Tools (No Programming Required)

| Tool | URL | Data | County-Level? |
|------|-----|------|---------------|
| FBI Crime Data Explorer | https://cde.ucr.cjis.gov/ | All UCR/NIBRS, Hate Crime, LEOKA | Agency→County |
| California DOJ | https://oag.ca.gov/crime | CA crime data | Yes |
| Pennsylvania UCR | https://www.ucr.pa.gov/PAUCRSPUBLIC/ | PA crime data | Yes |
| Vera Arrest Trends | https://arresttrends.vera.org/clearance-rates | Clearance rates | Yes |
| OJJDP Easy Access | https://ojjdp.ojp.gov/statistical-briefing-book/ | Juvenile arrests, populations | Yes (some) |
| BJS N-DASH | https://bjs.ojp.gov | NCVS victimization | National only |

### 9.2 Bulk Data Downloads

| Source | URL | Format | County-Level? |
|--------|-----|--------|---------------|
| ICPSR UCR Series | https://www.icpsr.umich.edu/web/NACJD/series/57 | SPSS, Stata, R, CSV | Yes (with caveats) |
| OpenICPSR (Kaplan Files) | https://www.openicpsr.org/openicpsr/project/108164 | R, Stata, CSV | Yes (1960-2017) |
| Data.gov Crime | https://catalog.data.gov/dataset?tags=crime | Various | Mixed |
| FBI CDE Downloads | Via CDE website | CSV, Excel | Agency level |

### 9.3 API Access (Programming Required)

| API | URL | Key Required? | County-Level? |
|-----|-----|---------------|---------------|
| FBI Crime Data API | https://api.usa.gov/crime/fbi/sapi/ | Yes (free) | Agency→County |
| BJS NIBRS Estimates | https://bjs.ojp.gov/nibrs-api | Check site | National/State |

**Get API Key:** https://api.data.gov/signup/

### 9.4 R Package Access

```r
# Install fbiAPI package
# devtools::install_github("jacobkap/fbiAPI")

library(fbiAPI)

# Your workflow:
# 1. Get API key from api.data.gov
# 2. Use fbiAPI functions to query FBI data
# 3. Aggregate agency data to county level yourself
```

### 9.5 Decision Tree: Which Source Should I Use?

```
Do you need CURRENT data (2023-2025)?
├─ YES → FBI Crime Data Explorer (agency-level, aggregate to county yourself)
│         OR State crime portals (CA, PA, NY, IL best options)
│
└─ NO (Historical OK)
    │
    Do you need INCIDENT-LEVEL detail (victim, offender, weapon, etc.)?
    ├─ YES → NIBRS data from FBI CDE or ICPSR
    │         (2000-present, agencies transitioned at different times)
    │
    └─ NO (Crime counts sufficient)
        │
        Are you doing POLICY RESEARCH or ACADEMIC PUBLICATION?
        ├─ YES → Use agency-level data, aggregate to county with documented methods
        │         DO NOT use pre-aggregated county files (quality issues)
        │
        └─ NO (Exploratory/descriptive only)
            │
            OK to use county-level files from ICPSR with caveats
            (Jacob Kaplan's files: 1960-2017 crime, 1974-2016 arrests)
```

---

## 10. VARIABLE CROSSWALK: KEY CRIME VARIABLES FOR COUNTY-LEVEL ANALYSIS

### 10.1 Core Crime Count Variables (Part I Offenses)

| Variable Category | UCR/NIBRS Code | Years Available | Source | County-Level Access |
|-------------------|----------------|-----------------|--------|---------------------|
| Murder/Non-Negligent Manslaughter | 09A | 1960-present | FBI CDE, ICPSR | Agency→County |
| Negligent Manslaughter | 09B | NIBRS 2000+ | FBI CDE | Agency→County |
| Rape (Legacy Definition) | 11A | 1960-2012 | ICPSR | Agency→County |
| Rape (Revised Definition) | 11A | 2013-present | FBI CDE, ICPSR | Agency→County |
| Robbery | 120 | 1960-present | FBI CDE, ICPSR | Agency→County |
| Aggravated Assault | 13A | 1960-present | FBI CDE, ICPSR | Agency→County |
| Burglary | 220 | 1960-present | FBI CDE, ICPSR | Agency→County |
| Larceny-Theft | 23A-23H | 1960-present | FBI CDE, ICPSR | Agency→County |
| Motor Vehicle Theft | 240 | 1960-present | FBI CDE, ICPSR | Agency→County |
| Arson | 200 | 1979-present | FBI CDE, ICPSR | Agency→County |

### 10.2 Crime Rate Variables

| Variable | Numerator | Denominator | Source |
|----------|-----------|-------------|--------|
| Violent Crime Rate | Murder+Rape+Robbery+Agg.Assault | County Population | Calculate |
| Property Crime Rate | Burglary+Larceny+MVT+(Arson) | County Population | Calculate |
| Murder Rate | Murder count | County Population | Calculate |
| [Any offense] Rate | Offense count | County Population | Calculate |

**Population Source:**
- Census Bureau Population Estimates
- OJJDP EZAPOP (for age-specific rates)
- Included in most ICPSR UCR files

### 10.3 Clearance Variables

| Variable | Description | Source | Years |
|----------|-------------|--------|-------|
| Clearances by Arrest | Number of offenses cleared by arrest | FBI CDE, ICPSR | 1960-present |
| Clearances by Exception | Number cleared by exceptional means | FBI CDE, ICPSR | 1960-present |
| Clearances - Juvenile Only | Clearances involving only juveniles | FBI CDE, ICPSR | 1960-present |
| Clearance Rate | (Clearances/Offenses)*100 | Calculate | - |

### 10.4 Arrest Variables by Demographics (⚠️ Retired after 2020)

| Variable | Breakdown | Years | Source |
|----------|-----------|-------|--------|
| Total Arrests by Offense | All Part I and Part II offenses | 1974-2021 | ICPSR |
| Arrests by Age | Under 10, 10-12, 13-14, 15-24 (yearly), 25-29, 30-34, 35-39, 40-44, 45-49, 50-54, 55-59, 60-64, 65+ | 1974-2021 | ICPSR |
| Arrests by Sex | Male, Female | 1974-2021 | ICPSR |
| Arrests by Race | White, Black, Am. Indian, Asian/PI | 1974-2021 | ICPSR |
| Arrests by Ethnicity | Hispanic, Non-Hispanic | 1980s-2021 | ICPSR |
| Juvenile Arrests (Under 18) | By offense | 1974-2021 | ICPSR, OJJDP |

### 10.5 Law Enforcement Variables

| Variable | Description | Source | Years |
|----------|-------------|--------|-------|
| Full-Time Sworn Officers | Total number (male/female) | LEOKA, LEMAS | 1960-present |
| Part-Time Sworn Officers | Total number | LEOKA, LEMAS | 1960-present |
| Full-Time Civilians | Total staff | LEOKA, LEMAS | 1960-present |
| Part-Time Civilians | Total staff | LEOKA, LEMAS | 1960-present |
| Officers per 1,000 Population | Rate | Calculate from LEOKA | - |
| Officers Killed (Felonious) | Count | LEOKA | 1960-present |
| Officers Killed (Accidental) | Count | LEOKA | 1960-present |
| Officers Assaulted | Count, by weapon/injury | LEOKA | 1960-present |

### 10.6 Hate Crime Variables

| Variable | Description | Source | Years |
|----------|-------------|--------|-------|
| Hate Crime Incidents | Total count | FBI Hate Crime Stats | 1991-present |
| Hate Crime Offenses | Total count (>incidents) | FBI Hate Crime Stats | 1991-present |
| Bias Motivation | Race, Religion, Sexual Orientation, Disability, Gender, Gender Identity | FBI Hate Crime Stats | 1991-present |
| Hate Crime by Offense Type | Murder, Assault, Vandalism, etc. | FBI Hate Crime Stats | 1991-present |

### 10.7 Jail Variables (TRUE COUNTY-LEVEL)

| Variable | Description | Source | Years |
|----------|-------------|--------|-------|
| Jail Population (one-day count) | Inmates confined on reference date | ASJ/COJ | 1982-present |
| Jail Population by Demographics | Sex, Race, Ethnicity, Age | ASJ/COJ | 1982-present |
| Rated Capacity | Design capacity | ASJ/COJ | 1982-present |
| Percent of Capacity | (Population/Capacity)*100 | ASJ/COJ | 1982-present |
| Admissions | Total annual | ASJ/COJ | 1982-present |
| Releases | Total annual | ASJ/COJ | 1982-present |
| Average Daily Population | Average across year | ASJ/COJ | 1982-present |
| Held for Other Authorities | Federal, State, Other | ASJ/COJ | 1982-present |
| Jail Staff | Correctional officers, other | ASJ/COJ | 1982-present |

### 10.8 Juvenile Justice Variables (COUNTY-LEVEL)

| Variable | Description | Source | Years |
|----------|-------------|--------|-------|
| Juvenile Population | Age 10-17 by demographics | OJJDP EZAPOP | 1990-2022 |
| Juvenile Arrests | By offense, 29 categories | OJJDP EZAUCR | 1980-present |
| Juvenile Court Cases | Delinquency cases | OJJDP Easy Access | 1985-2022 |

### 10.9 NIBRS-Only Enhanced Variables (Incident-Level, Aggregable to County)

| Variable Category | Description | Years |
|-------------------|-------------|-------|
| Victim Demographics | Age, Sex, Race, Ethnicity, Resident Status | 2000-present |
| Offender Demographics | Age, Sex, Race, Ethnicity (when known) | 2000-present |
| Victim-Offender Relationship | 35+ categories (stranger, acquaintance, intimate partner, family, etc.) | 2000-present |
| Incident Date/Time | Precise date, hour of day | 2000-present |
| Location Type | 46+ categories (residence, school, parking lot, etc.) | 2000-present |
| Weapon Type | 15+ categories (firearm types, knife, blunt object, personal, etc.) | 2000-present |
| Injury Type | None, Apparent Minor, Apparent Broken Bones, etc. | 2000-present |
| Drug Type | 12+ drug categories | 2000-present |
| Property Type/Value | 68+ property types, value stolen/recovered | 2000-present |
| Bias Motivation (Hate Crimes) | Up to 5 biases per incident | 2000-present |
| Gang-Related Flag | Indicator | 2000-present |
| Drug/Alcohol Use | Suspected use by offender | 2000-present |

---

## 11. RECOMMENDED WORKFLOW FOR COUNTY-LEVEL CRIME ANALYSIS

### Step 1: Define Your Research Question
- What crimes? (specific offenses or categories)
- What years? (consider data transitions)
- What counties? (all US, specific states, specific counties)
- What detail? (counts only, or victim/offender characteristics?)

### Step 2: Choose Data Source Based on Needs

**For Current Data (2021-2025):**
- Use FBI Crime Data Explorer
- Download agency-level data
- Aggregate to county yourself

**For Historical Data (pre-2021):**
- Use ICPSR/OpenICPSR
- Jacob Kaplan's concatenated files are convenient
- Be aware of data quality issues

**For Incident-Level Detail:**
- Use NIBRS data (2000-present)
- Larger files, more complex
- Best for understanding crime circumstances

**For Specific States with Good Portals:**
- California, Pennsylvania, Illinois, New York: use state portals
- May have better county aggregations than FBI

### Step 3: Acquire Data

**Via API (R):**
```r
library(fbiAPI)
# Get data for your analysis
```

**Via Direct Download:**
- ICPSR: register, download datasets
- FBI CDE: use export functions
- State portals: download CSV/Excel

### Step 4: Data Cleaning and Preparation

**Check for:**
- Missing data (agencies not reporting)
- Multi-county agencies (decide how to allocate)
- Population data for rates
- Consistent offense definitions across years
- SRS vs. NIBRS reporting

**Aggregate Agency to County:**
```r
# Example pseudo-code
county_crime <- agency_crime %>%
  group_by(county_fips, year) %>%
  summarize(total_murders = sum(murders, na.rm=TRUE),
            # ... other crimes
            )
```

### Step 5: Calculate Rates

```r
# Merge with population data
county_crime <- county_crime %>%
  left_join(county_population, by=c("county_fips", "year"))

# Calculate rates per 100,000
county_crime <- county_crime %>%
  mutate(murder_rate = (total_murders / population) * 100000)
```

### Step 6: Document Your Methodology

**Critical for reproducibility:**
- Which agencies included/excluded?
- How did you handle multi-county agencies?
- How did you handle missing data?
- Which years? SRS or NIBRS?
- Population source?
- Any adjustments or imputations?

### Step 7: Validate Results

**Sanity checks:**
- Do rates seem reasonable?
- Compare to published state/national rates
- Check for outliers (data errors?)
- Verify against other sources if possible

### Step 8: Analysis with Appropriate Caveats

**Remember:**
- UCR = crimes reported to and recorded by police
- Underreporting varies by crime type
- Reporting practices vary by jurisdiction
- County-level aggregations have known quality issues
- Always cite limitations

---

## 12. ADDITIONAL RESOURCES AND REFERENCES

### 12.1 Key FBI Resources

- **FBI Crime Data Explorer:** https://cde.ucr.cjis.gov/
- **FBI UCR Program:** https://www.fbi.gov/how-we-can-help-you/more-fbi-services-and-information/ucr
- **FBI Crime Data API GitHub:** https://github.com/fbi-cde/crime-data-api
- **FBI UCR Technical Specifications:** https://le.fbi.gov/informational-tools/ucr/
- **2025.0 NIBRS User Manual:** Available through FBI law enforcement portal

### 12.2 ICPSR Resources

- **National Archive of Criminal Justice Data:** https://www.icpsr.umich.edu/web/NACJD/
- **UCR Data Series:** https://www.icpsr.umich.edu/web/NACJD/series/57
- **UCR Resource Guide:** https://www.icpsr.umich.edu/web/NACJD/cms/4819

### 12.3 Jacob Kaplan's Resources

- **OpenICPSR Concatenated Files:** https://www.openicpsr.org/openicpsr/project/108164
- **Book: "Uniform Crime Reporting (UCR) Program Data: A Practitioner's Guide"**
  - URL: https://ucrbook.com/
  - Excellent free online resource
  - Covers all aspects of UCR data
  - Includes chapter on county-level data limitations

### 12.4 BJS Resources

- **BJS Homepage:** https://bjs.ojp.gov
- **NIBRS National Estimates API:** https://bjs.ojp.gov/national-incident-based-reporting-system-nibrs-national-estimates-api
- **NCVS Dashboard (N-DASH):** Available through BJS site

### 12.5 OJJDP Resources

- **Statistical Briefing Book:** https://ojjdp.ojp.gov/statistical-briefing-book/
- **Easy Access Tools:** https://ojjdp.ojp.gov/statistical-briefing-book/data-analysis-tools
- **National Gang Center:** https://nationalgangcenter.ojp.gov/

### 12.6 State Resources

- **California DOJ:** https://oag.ca.gov/crime
- **Pennsylvania UCR:** https://www.ucr.pa.gov/PAUCRSPUBLIC/
- **Illinois Crime:** https://www.isp.state.il.us/crime/ucrhome.cfm
- **New York CJ Stats:** https://www.criminaljustice.ny.gov/crimnet/ojsa/stats.htm

### 12.7 Other Resources

- **Vera Institute Arrest Trends:** https://arresttrends.vera.org/
- **CSG Justice Center 50-State Crime Data:** https://projects.csgjusticecenter.org/tools-for-states-to-address-crime/50-state-crime-data/
- **Data.gov Crime Datasets:** https://catalog.data.gov/dataset?tags=crime
- **NICB Reports:** https://www.nicb.org/news/reports-statistics

### 12.8 Academic References on Data Quality

**Maltz, M.D., & Targonski, J.** (Multiple papers on county-level UCR data problems)
- Available through ICPSR documentation
- Read before using county-level files!

**FBI Publications:**
- "Effects of NIBRS on Crime Statistics" (BJS)
- Annual UCR methodology documentation

---

## 13. CONCLUSION

This comprehensive documentation provides production-ready information on all available US county-level crime statistics data sources as of November 2025.

**Key Takeaways:**

1. **County-level aggregated UCR data has significant quality issues** - use with extreme caution or avoid for policy research

2. **Best practice:** Use agency-level data from FBI Crime Data Explorer or ICPSR and aggregate to counties yourself with documented methodology

3. **NIBRS transition (2021)** created data breaks - be careful with trend analysis across this period

4. **True county-level data exists for:**
   - Jail statistics (Annual Census of Jails, 2025+)
   - Juvenile populations and some court data (OJJDP)
   - Some state-provided crime data (especially California, Pennsylvania)

5. **Not available at county level:**
   - NCVS victimization (national/regional only)
   - DEA STRIDE drug data (not publicly available by county)
   - ATF firearms trace (MSA/city only, not county)
   - Gang data (NYGS ended 2012, was sample-based)

6. **Data access is improving:**
   - FBI Crime Data Explorer provides quarterly updates
   - API access available (free key required)
   - R packages facilitate programmatic access
   - Some states provide excellent county-level portals

7. **Always document limitations** in any research using these data

**For questions or updated information**, consult the FBI Crime Data Explorer or contact state UCR program coordinators.

---

**Document Version:** 1.0
**Last Updated:** November 11, 2025
**Next Review:** Check for 2026 data releases and methodology updates

