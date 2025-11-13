# USGS Water Quality Parameters - Comprehensive County-Level Data Guide

**Version:** 3.1 (November 2025)
**Last Updated:** November 13, 2025
**Author:** Compiled from USGS NWIS, Water Quality Portal, and dataRetrieval documentation

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Complete Parameter Catalog by Category](#complete-parameter-catalog-by-category)
3. [Access Methods and Tools](#access-methods-and-tools)
4. [County-Level Data Retrieval](#county-level-data-retrieval)
5. [R Code Examples](#r-code-examples)
6. [Data Quality and Standards](#data-quality-and-standards)
7. [Related Data Sources](#related-data-sources)
8. [Parameter Code Resources](#parameter-code-resources)

---

## Executive Summary

The U.S. Geological Survey (USGS) National Water Information System (NWIS) provides the most comprehensive water quality monitoring data in the United States, with over 1.5 million sites and hundreds of water quality parameters measured since the 1950s. This guide documents ALL available parameters that can be retrieved and aggregated to U.S. county level.

### Key Statistics (as of November 2025)

- **Total Sites:** 1.5+ million in NWIS
- **Parameter Categories:** 20+ major groups
- **Individual Parameters:** 1,000+ unique parameter codes
- **Years Available:** 1950-present (varies by parameter)
- **Geographic Coverage:** All 3,143 U.S. counties
- **Data Sources:** USGS, EPA STORET, USDA (via Water Quality Portal)

### 🚨 Critical 2024-2025 System Transition 🚨

**MAJOR CHANGE:** The legacy USGS NWIS discrete water quality data system was frozen on **March 11, 2024** and is being decommissioned. This is a critical transition affecting all water quality data retrieval:

**What Changed:**
- **Legacy NWIS site (waterdata.usgs.gov/nwis/qw)**: Frozen March 11, 2024 - no new data
- **New data location**: Water Quality Portal at **waterqualitydata.us/beta/** (WQX 3.0)
- **Data format**: Changed from USGS-specific format to international WQX standard
- **Latest data**: All USGS data collected/analyzed after March 11, 2024 is ONLY available via WQX 3.0

**How to Access 2024-2025 Data:**
1. **New WQX 3.0 Portal (RECOMMENDED)**: https://waterqualitydata.us/beta/
2. **Main Water Quality Portal**: https://www.waterqualitydata.us/
3. **R dataRetrieval package**: Updated to work with new APIs (use latest version)
4. **Legacy NWIS**: Still accessible for historical data through March 11, 2024

**Years Available:** 1950-2025 (legacy system 1950-March 2024, WQX 3.0 for March 2024-present)

---

## Complete Parameter Catalog by Category

### 📋 COMPLETE NWIS PARAMETER CODES CATALOG (TIER 2)

**For the complete catalog of all 1,300+ USGS NWIS water quality parameter codes organized by category with descriptions, units, measurement methods, and data availability, see:**

**[USGS_NWIS_COMPLETE_PARAMETER_CODES.md](USGS_NWIS_COMPLETE_PARAMETER_CODES.md)**

This companion Tier 2 catalog provides:
- All 1,300+ NWIS parameter codes with official names and descriptions
- Organized by 55 major categories (physical, nutrients, metals, organic compounds, biologicaletc.)
- Complete units, measurement methods, and CAS numbers
- Remark codes and data quality indicators
- R dataRetrieval and Python examples for querying specific parameters
- Links to official USGS parameter code database
- Guidance on filtered vs. unfiltered samples

**Use this document (Tier 1)** for NWIS overview, priority parameters for health research, and county-level aggregation methods.
**Use USGS_NWIS_COMPLETE_PARAMETER_CODES.md (Tier 2)** to look up specific parameter codes or browse the complete 1,300+ parameter catalog.

### 1. PHYSICAL PARAMETERS

Water quality monitoring systems commonly measure these four fundamental parameters:

| Parameter Code | Parameter Name | Units | Description | Typical Frequency | Years Available |
|---------------|----------------|-------|-------------|-------------------|-----------------|
| **00010** | Temperature, water | °C | Water temperature | Continuous/Daily | 1950-present |
| **00020** | Temperature, air | °C | Air temperature | Daily | 1950-present |
| **00095** | Specific conductance | µS/cm at 25°C | Measure of dissolved ions | Continuous/Daily | 1950-present |
| **00098** | Specific conductance, laboratory | µS/cm at 25°C | Laboratory measurement | Discrete | 1950-present |
| **00300** | Dissolved oxygen | mg/L | Oxygen concentration | Continuous/Daily | 1950-present |
| **00301** | Dissolved oxygen saturation | Percent | Oxygen saturation percentage | Continuous/Daily | 1960-present |
| **00400** | pH, field | Standard units | Acidity/alkalinity (field) | Continuous/Daily | 1950-present |
| **00403** | pH, laboratory | Standard units | Acidity/alkalinity (lab) | Discrete | 1950-present |
| **00480** | Salinity | PSU or ‰ | Salt concentration | Continuous/Discrete | 1960-present |
| **00065** | Gage height | Feet | Water level/stage | Continuous | 1950-present |
| **00060** | Discharge/streamflow | ft³/s | Flow rate | Continuous/Daily | 1950-present |
| **00061** | Discharge, instantaneous | ft³/s | Instantaneous flow | 15-min intervals | 1960-present |
| **00054** | Reservoir storage | Acre-feet | Water storage volume | Daily | 1960-present |
| **00028** | Gage datum | Feet | Reference elevation | Static | Varies |

#### Turbidity Parameters (Multiple Methods)

| Parameter Code | Method/Description | Units | Years Available |
|---------------|-------------------|-------|-----------------|
| **63676** | Turbidity, NTRU | NTRU | 1990-present |
| **63677** | Turbidity, NTU | NTU | 1990-present |
| **63680** | Turbidity, FNU | FNU | 1995-present |
| **00076** | Turbidity, JTU | JTU | 1950-1990 (legacy) |
| **61028** | Turbidity, monochrome near infrared LED | NTRU | 2010-present |

**Note:** Turbidity measurement methods have evolved. NTRU (Nephelometric Turbidity Ratio Units) and FNU (Formazin Nephelometric Units) are now preferred over older JTU (Jackson Turbidity Units) and NTU methods.

#### Water Clarity and Transparency

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **00078** | Secchi depth | Meters | 1960-present |
| **32210** | Transparency, tube with disk | Centimeters | 1990-present |
| **00098** | Water appearance | Code | 1960-present |
| **00081** | Water color | Pt-Co units | 1960-present |

### 2. MAJOR IONS AND DISSOLVED SOLIDS

Major ions are the primary dissolved constituents in water, critical for determining water chemistry type and suitability for various uses.

#### Major Cations (Dissolved and Total)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00915** | Calcium, dissolved | mg/L as Ca | Filtered | 1950-present |
| **00916** | Calcium, total | mg/L as Ca | Unfiltered | 1950-present |
| **00925** | Magnesium, dissolved | mg/L as Mg | Filtered | 1950-present |
| **00927** | Magnesium, total | mg/L as Mg | Unfiltered | 1950-present |
| **00930** | Sodium, dissolved | mg/L as Na | Filtered | 1950-present |
| **00929** | Sodium, total | mg/L as Na | Unfiltered | 1950-present |
| **00935** | Potassium, dissolved | mg/L as K | Filtered | 1950-present |
| **00937** | Potassium, total | mg/L as K | Unfiltered | 1950-present |

#### Major Anions (Dissolved and Total)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00940** | Chloride, dissolved | mg/L as Cl | Filtered | 1950-present |
| **00940** | Chloride, total | mg/L as Cl | Unfiltered | 1950-present |
| **00945** | Sulfate, dissolved | mg/L as SO₄ | Filtered | 1950-present |
| **00946** | Sulfate, total | mg/L as SO₄ | Unfiltered | 1950-present |
| **00950** | Fluoride, dissolved | mg/L as F | Filtered | 1960-present |
| **00951** | Fluoride, total | mg/L as F | Unfiltered | 1960-present |
| **71850** | Bromide, dissolved | mg/L as Br | Filtered | 1980-present |
| **99112** | Iodide, dissolved | mg/L as I | Filtered | 1990-present |

#### Alkalinity and Carbonate System

The alkalinity parameter codes in USGS NWIS are complex due to multiple measurement methods and sample types.

| Parameter Code | Parameter Name | Units | Method/Notes | Years Available |
|---------------|----------------|-------|--------------|-----------------|
| **00410** | Alkalinity (legacy) | mg/L as CaCO₃ | Laboratory, pre-1981 | 1950-1981 |
| **90410** | Alkalinity, laboratory | mg/L as CaCO₃ | Lab, fixed endpoint | 1981-present |
| **39086** | Alkalinity, field, incremental | mg/L as CaCO₃ | Field titration | 1980-present |
| **39036** | Alkalinity, field, fixed endpoint | mg/L as CaCO₃ | Field titration | 1980-present |
| **29801** | Alkalinity, Gran plot | mg/L as CaCO₃ | Advanced titration | 1990-present |
| **00452** | Carbonate, dissolved | mg/L as CO₃ | Filtered | 1960-present |
| **00453** | Bicarbonate, dissolved | mg/L as HCO₃ | Filtered | 1960-present |
| **00691** | Hydroxide ion, dissolved | mg/L as OH | Filtered | 1970-present |
| **00419** | Acid neutralizing capacity (ANC) | μeq/L | Gran titration | 1985-present |

#### Hardness and Dissolved Solids

| Parameter Code | Parameter Name | Units | Description | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00900** | Hardness, total | mg/L as CaCO₃ | Sum of Ca and Mg | 1950-present |
| **00901** | Hardness, carbonate | mg/L as CaCO₃ | Portion equivalent to HCO₃ | 1960-present |
| **00902** | Hardness, noncarbonate | mg/L as CaCO₃ | Remaining hardness | 1960-present |
| **70300** | Dissolved solids, residue at 180°C | mg/L | Total dissolved solids | 1950-present |
| **00515** | Dissolved solids, calculated sum | mg/L | Sum of constituents | 1960-present |
| **00530** | Total suspended solids | mg/L | Residue on filter | 1960-present |
| **00535** | Residue on evaporation, total | mg/L | Total residue | 1950-present |

### 3. NUTRIENTS (Complete Nitrogen and Phosphorus Series)

Nutrients are among the most commonly measured water quality parameters due to their importance in eutrophication and water quality degradation.

#### Nitrogen Compounds - All Forms

##### Ammonia (NH₃/NH₄⁺)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00608** | Ammonia, dissolved | mg/L as N | Filtered | 1950-present |
| **00610** | Ammonia, total | mg/L as N | Unfiltered | 1950-present |
| **71846** | Ammonia, dissolved, field | mg/L as N | Field measurement | 1980-present |
| **00619** | Ammonium, dissolved | mg/L as NH₄ | Filtered | 1960-present |

##### Nitrite (NO₂⁻)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00613** | Nitrite, dissolved | mg/L as N | Filtered | 1950-present |
| **00615** | Nitrite, total | mg/L as N | Unfiltered | 1950-present |

##### Nitrate (NO₃⁻)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00618** | Nitrate, dissolved | mg/L as N | Filtered | 1950-present |
| **00620** | Nitrate, total | mg/L as N | Unfiltered | 1950-present |

##### Nitrite + Nitrate (Combined)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00631** | Nitrite + nitrate, dissolved | mg/L as N | Filtered | 1960-present |
| **00630** | Nitrite + nitrate, total | mg/L as N | Unfiltered | 1960-present |
| **99133** | Nitrate + nitrite, field | mg/L as N | Field measurement | 1990-present |

##### Organic Nitrogen

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00607** | Organic nitrogen, dissolved | mg/L as N | Filtered | 1960-present |
| **00605** | Organic nitrogen, total | mg/L as N | Unfiltered | 1960-present |

##### Kjeldahl Nitrogen (TKN)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00623** | Kjeldahl nitrogen, dissolved | mg/L as N | Filtered | 1960-present |
| **00625** | Kjeldahl nitrogen, total | mg/L as N | Unfiltered | 1960-present |

##### Total Nitrogen

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00600** | Total nitrogen, water, unfiltered | mg/L as N | Unfiltered | 1970-present |
| **00602** | Total nitrogen, water, filtered | mg/L as N | Filtered | 1970-present |
| **62854** | Total nitrogen, mixed forms | mg/L as N | Calculated | 1990-present |

##### Particulate Nitrogen

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **49570** | Particulate nitrogen | mg/L as N | Particulate | 1980-present |

#### Phosphorus Compounds - All Forms

##### Orthophosphate (PO₄³⁻)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00660** | Orthophosphate, dissolved | mg/L as P | Filtered | 1950-present |
| **00671** | Orthophosphate, dissolved | mg/L as PO₄ | Filtered | 1950-present |
| **70507** | Orthophosphate, dissolved, field | mg/L as P | Field measurement | 1990-present |

##### Total Phosphorus

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00665** | Phosphorus, total | mg/L as P | Unfiltered | 1950-present |
| **00666** | Phosphorus, dissolved | mg/L as P | Filtered | 1950-present |

##### Particulate Phosphorus

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **49567** | Phosphorus, particulate | mg/L as P | Particulate | 1980-present |

##### Hydrolyzable and Other Forms

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00672** | Phosphorus, hydrolyzable + orthophosphate | mg/L as P | Filtered | 1970-present |
| **00677** | Phosphorus, orthophosphate + organic | mg/L as P | Filtered | 1970-present |

### 4. HEAVY METALS AND TRACE ELEMENTS (Comprehensive List)

Trace elements are measured in both dissolved (filtered, <0.45 µm) and total (unfiltered) forms. Many also have separate particulate measurements.

#### Toxic Heavy Metals - Priority Pollutants

##### Arsenic (As)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01000** | Arsenic, dissolved | µg/L | Filtered | 1970-present |
| **01002** | Arsenic, total | µg/L | Unfiltered | 1970-present |
| **01001** | Arsenic, suspended | µg/L | Particulate | 1980-present |

##### Cadmium (Cd)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01025** | Cadmium, dissolved | µg/L | Filtered | 1970-present |
| **01027** | Cadmium, total | µg/L | Unfiltered | 1970-present |
| **01026** | Cadmium, suspended | µg/L | Particulate | 1980-present |

##### Chromium (Cr)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01030** | Chromium, dissolved | µg/L | Filtered | 1970-present |
| **01034** | Chromium, total | µg/L | Unfiltered | 1970-present |
| **01031** | Chromium, suspended | µg/L | Particulate | 1980-present |
| **01032** | Chromium(VI), dissolved | µg/L | Filtered, hexavalent | 1980-present |

##### Copper (Cu)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01040** | Copper, dissolved | µg/L | Filtered | 1970-present |
| **01042** | Copper, total | µg/L | Unfiltered | 1970-present |
| **01041** | Copper, suspended | µg/L | Particulate | 1980-present |

##### Lead (Pb)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01049** | Lead, dissolved | µg/L | Filtered | 1970-present |
| **01051** | Lead, total | µg/L | Unfiltered | 1970-present |
| **01050** | Lead, suspended | µg/L | Particulate | 1980-present |

##### Mercury (Hg)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **71890** | Mercury, dissolved | µg/L | Filtered | 1970-present |
| **71900** | Mercury, total | µg/L | Unfiltered | 1970-present |
| **71895** | Mercury, suspended | µg/L | Particulate | 1980-present |
| **50287** | Methylmercury, dissolved | ng/L | Filtered, organic form | 1990-present |
| **50288** | Methylmercury, total | ng/L | Unfiltered, organic form | 1990-present |

##### Nickel (Ni)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01065** | Nickel, dissolved | µg/L | Filtered | 1970-present |
| **01067** | Nickel, total | µg/L | Unfiltered | 1970-present |
| **01066** | Nickel, suspended | µg/L | Particulate | 1980-present |

##### Selenium (Se)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01145** | Selenium, dissolved | µg/L | Filtered | 1970-present |
| **01147** | Selenium, total | µg/L | Unfiltered | 1970-present |
| **01146** | Selenium, suspended | µg/L | Particulate | 1980-present |

##### Silver (Ag)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01075** | Silver, dissolved | µg/L | Filtered | 1970-present |
| **01077** | Silver, total | µg/L | Unfiltered | 1970-present |
| **01076** | Silver, suspended | µg/L | Particulate | 1980-present |

##### Zinc (Zn)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01090** | Zinc, dissolved | µg/L | Filtered | 1970-present |
| **01092** | Zinc, total | µg/L | Unfiltered | 1970-present |
| **01091** | Zinc, suspended | µg/L | Particulate | 1980-present |

#### Other Important Trace Elements

##### Aluminum (Al)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01106** | Aluminum, dissolved | µg/L | Filtered | 1970-present |
| **01105** | Aluminum, total | µg/L | Unfiltered | 1970-present |

##### Antimony (Sb)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01095** | Antimony, dissolved | µg/L | Filtered | 1980-present |
| **01097** | Antimony, total | µg/L | Unfiltered | 1980-present |

##### Barium (Ba)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01005** | Barium, dissolved | µg/L | Filtered | 1970-present |
| **01007** | Barium, total | µg/L | Unfiltered | 1970-present |

##### Beryllium (Be)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01010** | Beryllium, dissolved | µg/L | Filtered | 1980-present |
| **01012** | Beryllium, total | µg/L | Unfiltered | 1980-present |

##### Boron (B)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01020** | Boron, dissolved | µg/L | Filtered | 1970-present |
| **01022** | Boron, total | µg/L | Unfiltered | 1970-present |

##### Cobalt (Co)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01035** | Cobalt, dissolved | µg/L | Filtered | 1980-present |
| **01037** | Cobalt, total | µg/L | Unfiltered | 1980-present |

##### Iron (Fe)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01046** | Iron, dissolved | µg/L | Filtered | 1950-present |
| **01045** | Iron, total | µg/L | Unfiltered | 1950-present |
| **01044** | Iron, ferrous (Fe²⁺), dissolved | µg/L | Filtered, reduced form | 1970-present |

##### Lithium (Li)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01130** | Lithium, dissolved | µg/L | Filtered | 1970-present |
| **01132** | Lithium, total | µg/L | Unfiltered | 1970-present |

##### Manganese (Mn)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01056** | Manganese, dissolved | µg/L | Filtered | 1950-present |
| **01055** | Manganese, total | µg/L | Unfiltered | 1950-present |

##### Molybdenum (Mo)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01060** | Molybdenum, dissolved | µg/L | Filtered | 1980-present |
| **01062** | Molybdenum, total | µg/L | Unfiltered | 1980-present |

##### Strontium (Sr)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01080** | Strontium, dissolved | µg/L | Filtered | 1970-present |
| **01082** | Strontium, total | µg/L | Unfiltered | 1970-present |

##### Thallium (Tl)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01057** | Thallium, dissolved | µg/L | Filtered | 1980-present |
| **01059** | Thallium, total | µg/L | Unfiltered | 1980-present |

##### Tin (Sn)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01100** | Tin, dissolved | µg/L | Filtered | 1980-present |
| **01102** | Tin, total | µg/L | Unfiltered | 1980-present |

##### Titanium (Ti)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01150** | Titanium, dissolved | µg/L | Filtered | 1980-present |
| **01152** | Titanium, total | µg/L | Unfiltered | 1980-present |

##### Uranium (U)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **22703** | Uranium, natural, dissolved | µg/L | Filtered | 1980-present |
| **28011** | Uranium, natural, total | µg/L | Unfiltered | 1980-present |

##### Vanadium (V)

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **01085** | Vanadium, dissolved | µg/L | Filtered | 1980-present |
| **01087** | Vanadium, total | µg/L | Unfiltered | 1980-present |

### 5. PESTICIDES (Complete Catalog)

USGS monitors over 200 pesticide compounds and their degradates. Pesticide parameter codes typically fall in the ranges 38000-49999 and 60000-69999.

#### Key Herbicides - Parent Compounds

##### Triazines

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **04040** or **39632** | Atrazine | Filtered | 1980-present |
| **68547** | Atrazine, desethyl- (DEA) | Filtered (metabolite) | 1990-present |
| **68552** | Atrazine, desisopropyl- (DIA) | Filtered (metabolite) | 1990-present |
| **68660** | Atrazine, didealkylatrazine | Filtered (metabolite) | 1990-present |
| **04025** | Propazine | Filtered | 1980-present |
| **04035** | Simazine | Filtered | 1980-present |
| **04037** | Prometon | Filtered | 1980-present |
| **82685** | Terbutryn | Filtered | 1990-present |
| **39057** | Prometryn | Filtered | 1990-present |

##### Chloroacetanilides

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **46342** or **65090** | Metolachlor | Filtered | 1985-present |
| **68650** | Metolachlor ESA | Filtered (metabolite) | 1995-present |
| **68651** | Metolachlor OA | Filtered (metabolite) | 1995-present |
| **49260** | Acetochlor | Filtered | 1995-present |
| **68522** | Acetochlor ESA | Filtered (metabolite) | 2000-present |
| **68523** | Acetochlor OA | Filtered (metabolite) | 2000-present |
| **68524** | Acetochlor SAA | Filtered (metabolite) | 2000-present |
| **04040** | Alachlor | Filtered | 1980-present |
| **82660** | Alachlor ESA | Filtered (metabolite) | 1995-present |
| **49315** | Dimethenamid | Filtered | 2000-present |
| **62482** | Flufenacet | Filtered | 2005-present |

##### Phenoxy Acids and Related

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **68500** or **39732** | 2,4-D (2,4-Dichlorophenoxyacetic acid) | Filtered | 1970-present |
| **39742** | 2,4,5-T | Filtered | 1970-2000 |
| **38746** | 2,4-DB | Filtered | 1990-present |
| **49315** | Dicamba | Filtered | 1990-present |
| **49299** | MCPA (2-Methyl-4-chlorophenoxyacetic acid) | Filtered | 1990-present |
| **38811** | MCPP (Mecoprop) | Filtered | 1990-present |
| **82052** | Triclopyr | Filtered | 1995-present |

##### Glyphosate and Related

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **62722** | Glyphosate | Filtered | 2001-present |
| **62649** | AMPA (Aminomethylphosphonic acid) | Filtered (metabolite) | 2001-present |
| **04095** | Glufosinate | Filtered | 2005-present |

##### Dinitroanilines

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **82661** | Trifluralin | Filtered | 1985-present |
| **82673** | Pendimethalin | Filtered | 1990-present |
| **39341** | Ethalfluralin | Filtered | 1990-present |

##### Other Herbicides

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **04029** | Bromacil | Filtered | 1985-present |
| **49297** | Diuron | Filtered | 1985-present |
| **38866** | Linuron | Filtered | 1990-present |
| **82670** | Tebuthiuron | Filtered | 1990-present |
| **39742** | Bentazon | Filtered | 1995-present |
| **61694** | Imazaquin | Filtered | 2000-present |
| **61695** | Imazethapyr | Filtered | 2000-present |

#### Key Insecticides

##### Organophosphates

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **38933** | Chlorpyrifos | Filtered | 1985-present |
| **39572** | Diazinon | Filtered | 1985-present |
| **82672** | Phorate | Filtered | 1985-present |
| **39040** | Ethoprop | Filtered | 1990-present |
| **39398** | Fonofos | Filtered | 1990-present |
| **39341** | Terbufos | Filtered | 1990-present |
| **82677** | Disulfoton | Filtered | 1985-present |
| **39532** | Malathion | Filtered | 1980-present |
| **39542** | Parathion | Filtered | 1970-2000 |

##### Carbamates

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **82680** | Carbaryl | Filtered | 1985-present |
| **82615** | Carbofuran | Filtered | 1985-present |
| **39051** | Methomyl | Filtered | 1990-present |
| **82619** | Aldicarb | Filtered | 1985-present |
| **49302** | Oxamyl | Filtered | 1990-present |

##### Pyrethroids

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **61652** | Bifenthrin | Filtered | 2005-present |
| **61653** | Cyfluthrin | Filtered | 2005-present |
| **61654** | Cypermethrin | Filtered | 2005-present |
| **61655** | Deltamethrin | Filtered | 2005-present |
| **61680** | Esfenvalerate | Filtered | 2005-present |
| **61683** | Lambda-cyhalothrin | Filtered | 2005-present |
| **61685** | Permethrin | Filtered | 2005-present |
| **62767** | Cyhalothrin | Filtered | 2005-present |

##### Neonicotinoids

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **68211** | Imidacloprid | Filtered | 2010-present |
| **61708** | Thiamethoxam | Filtered | 2010-present |
| **66591** | Clothianidin | Filtered | 2010-present |
| **68550** | Acetamiprid | Filtered | 2010-present |
| **68552** | Thiacloprid | Filtered | 2010-present |

##### Other Insecticides

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **61591** | Fipronil | Filtered | 2005-present |
| **62169** | Fipronil desulfinyl | Filtered (metabolite) | 2005-present |
| **62170** | Fipronil sulfide | Filtered (metabolite) | 2005-present |
| **62167** | Fipronil sulfone | Filtered (metabolite) | 2005-present |

#### Fungicides

| Parameter Code | Parameter Name | Sample Type | Years Available |
|---------------|----------------|-------------|-----------------|
| **50408** | Azoxystrobin | Filtered | 2010-present |
| **61588** | Boscalid | Filtered | 2010-present |
| **50337** | Metalaxyl | Filtered | 2005-present |
| **39415** | Metolachlor | Filtered | 2000-present |
| **39532** | Myclobutanil | Filtered | 2005-present |
| **50359** | Propiconazole | Filtered | 2005-present |
| **50337** | Tebuconazole | Filtered | 2005-present |

**Note:** USGS Laboratory Schedule 2437 determines concentrations of 225 fungicides, herbicides, insecticides, and associated degradates in one analytical method. Contact USGS National Water Quality Laboratory for complete current pesticide schedules.

### 6. VOLATILE ORGANIC COMPOUNDS (VOCs)

VOC parameter codes typically fall in the 34000-50000 range. Over 85 VOCs are routinely analyzed.

#### BTEX Compounds

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **34030** | Benzene | µg/L | 1980-present |
| **34010** | Toluene | µg/L | 1980-present |
| **34371** | Ethylbenzene | µg/L | 1980-present |
| **77135** | o-Xylene | µg/L | 1980-present |
| **85795** | m-Xylene + p-Xylene | µg/L | 1980-present |
| **81551** | Total xylenes | µg/L | 1980-present |

#### Trihalomethanes (THMs) - Chlorination Byproducts

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **32104** | Chloroform | µg/L | 1980-present |
| **32106** | Bromodichloromethane | µg/L | 1980-present |
| **32101** | Dibromochloromethane | µg/L | 1980-present |
| **32102** | Bromoform (Tribromomethane) | µg/L | 1980-present |
| **34210** | Total trihalomethanes | µg/L | 1980-present |

#### Gasoline Additives and Components

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **78032** or **34371** | MTBE (Methyl tert-butyl ether) | µg/L | 1990-present |
| **50005** | ETBE (Ethyl tert-butyl ether) | µg/L | 1995-present |
| **45996** | TAME (tert-Amyl methyl ether) | µg/L | 1995-present |
| **77222** | TBA (tert-Butyl alcohol) | µg/L | 1995-present |
| **77223** | DIPE (Diisopropyl ether) | µg/L | 1995-present |

#### Chlorinated Solvents

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **32102** | Tetrachloroethene (PCE) | µg/L | 1980-present |
| **39180** | Trichloroethene (TCE) | µg/L | 1980-present |
| **34496** | 1,1,1-Trichloroethane | µg/L | 1980-present |
| **77652** | 1,1,2-Trichloroethane | µg/L | 1980-present |
| **34501** | 1,1-Dichloroethene | µg/L | 1980-present |
| **34546** | 1,2-Dichloroethane | µg/L | 1980-present |
| **77093** | cis-1,2-Dichloroethene | µg/L | 1980-present |
| **34210** | trans-1,2-Dichloroethene | µg/L | 1980-present |
| **34668** | Carbon tetrachloride | µg/L | 1980-present |
| **32105** | Chloromethane (Methyl chloride) | µg/L | 1980-present |
| **34413** | Dichloromethane (Methylene chloride) | µg/L | 1980-present |
| **34423** | Chloroethane | µg/L | 1980-present |

#### Other Common VOCs

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **34215** | Styrene | µg/L | 1980-present |
| **81576** | 1,2,3-Trichloropropane | µg/L | 1985-present |
| **77613** | 1,2-Dibromoethane (EDB) | µg/L | 1985-present |
| **82625** | 1,2-Dibromo-3-chloropropane (DBCP) | µg/L | 1985-present |

**Note:** Schedule 2020 at USGS National Water Quality Laboratory measures 85 VOCs in a single analysis.

### 7. SEMI-VOLATILE ORGANIC COMPOUNDS (SVOCs)

#### Polycyclic Aromatic Hydrocarbons (PAHs) - Parent Compounds

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **34030** | Naphthalene | µg/L | 1985-present |
| **34696** | Acenaphthylene | µg/L | 1985-present |
| **34205** | Acenaphthene | µg/L | 1985-present |
| **34220** | Fluorene | µg/L | 1985-present |
| **34469** | Phenanthrene | µg/L | 1985-present |
| **34210** | Anthracene | µg/L | 1985-present |
| **34242** | Fluoranthene | µg/L | 1985-present |
| **34247** | Pyrene | µg/L | 1985-present |
| **34521** | Benzo(a)anthracene | µg/L | 1985-present |
| **34230** | Chrysene | µg/L | 1985-present |
| **34403** | Benzo(b)fluoranthene | µg/L | 1985-present |
| **34376** | Benzo(k)fluoranthene | µg/L | 1985-present |
| **34247** | Benzo(a)pyrene | µg/L | 1985-present |
| **34556** | Indeno(1,2,3-cd)pyrene | µg/L | 1985-present |
| **34548** | Dibenzo(a,h)anthracene | µg/L | 1985-present |
| **34521** | Benzo(g,h,i)perylene | µg/L | 1985-present |

#### Polychlorinated Biphenyls (PCBs)

USGS analyzes PCBs as individual congeners (120+ compounds) or as Aroclor mixtures. Parameter codes are in the OPC (Organics, PCBs) group.

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **39516** | PCB, total | µg/L | 1970-present |
| **39488** | Aroclor 1016 | µg/L | 1980-2005 |
| **39492** | Aroclor 1221 | µg/L | 1980-2005 |
| **39496** | Aroclor 1232 | µg/L | 1980-2005 |
| **39500** | Aroclor 1242 | µg/L | 1980-2005 |
| **39504** | Aroclor 1248 | µg/L | 1980-2005 |
| **39508** | Aroclor 1254 | µg/L | 1980-2005 |
| **39512** | Aroclor 1260 | µg/L | 1980-2005 |

**Note:** Modern analyses increasingly focus on specific PCB congeners rather than Aroclor mixtures.

#### Organochlorine Pesticides (Legacy)

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **39381** | Aldrin | µg/L | 1970-2000 |
| **39351** | DDT, o,p'- | µg/L | 1970-present |
| **39350** | DDT, p,p'- | µg/L | 1970-present |
| **39365** | DDD, p,p'- | µg/L | 1970-present |
| **39360** | DDE, p,p'- | µg/L | 1970-present |
| **39341** | Dieldrin | µg/L | 1970-present |
| **39388** | Endrin | µg/L | 1970-2000 |
| **39398** | Heptachlor | µg/L | 1970-2000 |
| **39413** | Heptachlor epoxide | µg/L | 1970-present |
| **39755** | Lindane (gamma-HCH) | µg/L | 1970-present |
| **39340** | alpha-HCH | µg/L | 1970-present |
| **82660** | Chlordane, technical | µg/L | 1970-2000 |
| **39062** | Toxaphene | µg/L | 1970-2000 |

### 8. EMERGING CONTAMINANTS

#### Per- and Polyfluoroalkyl Substances (PFAS)

USGS has established parameter group "OPF" for PFAS compounds. As of 2024, USGS analyzes 34 total PFAS compounds using DAI-LC/MS/MS methods.

**Important Note:** PFAS parameter codes are not included in the HBSL (Health-Based Screening Levels) database because CASRNs are not consistently available. However, USGS added 27 PFAS to the HBSL database in 2024.

| Parameter Code | Parameter Name (Tentative) | Units | Years Available |
|---------------|---------------------------|-------|-----------------|
| **TBD** | PFOS (Perfluorooctane sulfonic acid) | ng/L | 2014-present |
| **TBD** | PFOA (Perfluorooctanoic acid) | ng/L | 2014-present |
| **TBD** | PFHxS (Perfluorohexane sulfonic acid) | ng/L | 2014-present |
| **TBD** | PFNA (Perfluorononanoic acid) | ng/L | 2014-present |
| **TBD** | PFBS (Perfluorobutane sulfonic acid) | ng/L | 2014-present |
| **TBD** | PFHxA (Perfluorohexanoic acid) | ng/L | 2014-present |
| **TBD** | PFDA (Perfluorodecanoic acid) | ng/L | 2014-present |

**Access Note:** For specific PFAS parameter codes, consult the USGS NWIS parameter code database directly or use the dataRetrieval R package to search for "PFAS" or individual compound names. Parameter codes are assigned as new methods are approved.

#### Pharmaceuticals and Personal Care Products (PPCPs)

USGS has conducted numerous studies on pharmaceuticals and personal care products in water since 1999. Specific parameter codes exist for 100+ compounds.

**Common Pharmaceutical Compounds Monitored:**

- Antibiotics (sulfamethoxazole, trimethoprim, ciprofloxacin, etc.)
- Analgesics (acetaminophen, ibuprofen, naproxen, codeine)
- Cardiovascular drugs (atenolol, metoprolol, gemfibrozil)
- Hormones (estrone, 17β-estradiol, testosterone)
- Anticonvulsants (carbamazepine, phenytoin)
- Antidepressants (fluoxetine, sertraline)
- Stimulants (caffeine, cotinine)

**Personal Care Products:**

- Fragrances (HHCB, AHTN - synthetic musks)
- Antimicrobials (triclosan, triclocarban)
- Insect repellents (DEET)
- UV filters (benzophenone, oxybenzone)

**Note:** Contact USGS National Water Quality Laboratory for current pharmaceutical schedules and parameter codes. Laboratory Schedule 2080 is one method for pharmaceutical detection.

#### Wastewater Indicators

| Parameter Code Category | Compounds | Purpose | Years Available |
|------------------------|-----------|---------|-----------------|
| **Caffeine** | Caffeine (1,3,7-trimethylxanthine) | Human consumption indicator | 2000-present |
| **Coprostanol** | 3β-Coprostanol | Fecal contamination marker | 2000-present |
| **Detergent metabolites** | Various alkylphenols | Wastewater presence | 2000-present |
| **Flame retardants** | PBDEs, TCEP, TCPP | Consumer products | 2005-present |

### 9. MICROBIOLOGICAL PARAMETERS

#### Indicator Bacteria

| Parameter Code | Parameter Name | Units | Method | Years Available |
|---------------|----------------|-------|--------|-----------------|
| **31699** | E. coli | Colonies/100 mL | Modified mTEC agar | 1990-present |
| **31648** | E. coli | MPN/100 mL | Colilert method | 1995-present |
| **31616** | Fecal coliform | Colonies/100 mL | Membrane filter | 1970-present |
| **31615** | Fecal coliform | MPN/100 mL | Multiple tube fermentation | 1970-present |
| **31501** | Total coliform | Colonies/100 mL | Membrane filter | 1950-present |
| **31504** | Total coliform | MPN/100 mL | Multiple tube fermentation | 1950-present |
| **31649** | Enterococci | Colonies/100 mL | mE or mEI agar | 1980-present |
| **31647** | Enterococci | MPN/100 mL | Enterolert method | 1995-present |
| **31679** | Fecal streptococci | Colonies/100 mL | KF Streptococcus agar | 1970-present |

#### Viral Indicators

| Parameter Code | Parameter Name | Units | Method | Years Available |
|---------------|----------------|-------|--------|-----------------|
| **82910** | Coliphage, somatic | PFU/100 mL | Single agar layer | 2000-present |
| **82911** | Coliphage, F-specific | PFU/100 mL | Single agar layer | 2000-present |

**Note:** MPN = Most Probable Number; CFU = Colony Forming Units; PFU = Plaque Forming Units

### 10. SEDIMENT PARAMETERS

| Parameter Code | Parameter Name | Units | Description | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **80154** | Suspended sediment concentration (SSC) | mg/L | Total suspended material | 1950-present |
| **80155** | Suspended sediment discharge | tons/day | Sediment load | 1950-present |
| **00530** | Total suspended solids (TSS) | mg/L | Residue on filter | 1960-present |
| **00520** | Residue, volatile suspended | mg/L | Organic fraction | 1970-present |
| **00535** | Residue, total | mg/L | Total residue | 1950-present |
| **80180** | Bedload discharge | tons/day | Bed material transport | 1960-present |
| **82398** | Sediment, suspended, sieve diameter, percent smaller than 0.0625 mm | Percent | Particle size distribution | 1970-present |

### 11. BIOLOGICAL PARAMETERS

#### Chlorophyll and Algal Pigments

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **32209** | Chlorophyll a, phytoplankton | µg/L | Water column | 1970-present |
| **70953** | Chlorophyll a, periphyton | mg/m² | Attached algae | 1980-present |
| **70954** | Chlorophyll a, bed sediment | µg/g | Sediment | 1985-present |
| **32211** | Chlorophyll b, phytoplankton | µg/L | Water column | 1970-present |
| **62360** | Pheophytin a | µg/L | Degradation product | 1980-present |

#### Algal and Cyanobacterial Counts

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **70953** | Phytoplankton, total | Cells/mL | 1970-present |
| **81015** | Blue-green algae (Cyanobacteria) | Cells/mL | 1970-present |
| **81016** | Diatoms | Cells/mL | 1970-present |
| **81017** | Green algae | Cells/mL | 1970-present |

#### Cyanotoxins

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **65340** | Microcystin | µg/L | 2000-present |
| **65349** | Cylindrospermopsin | µg/L | 2005-present |
| **65346** | Anatoxin-a | µg/L | 2005-present |
| **65347** | Saxitoxin | µg/L | 2010-present |

#### Aquatic Biota (Site-Level Data)

- Macroinvertebrate taxa and abundance
- Fish species and populations
- Periphyton biomass and community composition
- Habitat assessments

**Note:** Biological community data is typically collected at specific sites rather than as continuous measurements and requires specialized data queries.

### 12. ORGANIC CARBON AND ORGANIC MATTER

| Parameter Code | Parameter Name | Units | Sample Type | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00680** | Organic carbon, total (TOC) | mg/L | Unfiltered | 1970-present |
| **00681** | Organic carbon, dissolved (DOC) | mg/L | Filtered | 1970-present |
| **00689** | Organic carbon, particulate (POC) | mg/L | Particulate | 1980-present |
| **00685** | Organic carbon, suspended | mg/L | Suspended | 1980-present |
| **00687** | Inorganic carbon, dissolved (DIC) | mg/L | Filtered | 1990-present |

#### Biochemical and Chemical Oxygen Demand

| Parameter Code | Parameter Name | Units | Description | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **00310** | Biochemical oxygen demand, 5-day (BOD5) | mg/L | O₂ consumed by microbes | 1960-present |
| **00315** | BOD, 5-day, carbonaceous | mg/L | BOD without nitrification | 1970-present |
| **00340** | Chemical oxygen demand (COD) | mg/L | O₂ equiv. of oxidizable matter | 1960-present |

#### Oil and Grease

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **00556** | Oil and grease | mg/L | 1970-present |

### 13. ISOTOPES (Stable and Radioactive)

#### Stable Isotopes (Environmental Tracers)

| Parameter Code | Parameter Name | Units | Application | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **82082** | δ²H (Deuterium) in water | ‰ VSMOW | Water source tracing | 1980-present |
| **82085** | δ¹⁸O in water | ‰ VSMOW | Water source tracing | 1980-present |
| **82086** | δ¹³C in dissolved inorganic carbon | ‰ VPDB | Carbon cycling | 1985-present |
| **82081** | δ¹⁵N in nitrate | ‰ Air | Nitrogen source tracing | 1990-present |
| **82085** | δ¹⁸O in nitrate | ‰ VSMOW | Nitrogen cycling | 1995-present |
| **82661** | δ³⁴S in sulfate | ‰ CDT | Sulfur cycling | 1985-present |

#### Radioactive Isotopes (Age Dating and Tracers)

| Parameter Code | Parameter Name | Units | Application | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **82303** | Radon-222 | pCi/L | Groundwater indicator | 1980-present |
| **07000** | Tritium | TU | Water age dating | 1970-present |
| **82666** | Carbon-14 | Percent modern | Old groundwater dating | 1980-present |
| **49350** | Radium-226 | pCi/L | Natural radioactivity | 1980-present |
| **09511** | Radium-228 | pCi/L | Natural radioactivity | 1980-present |
| **00900** | Gross alpha radioactivity | pCi/L | Screening parameter | 1970-present |
| **03515** | Gross beta radioactivity | pCi/L | Screening parameter | 1970-present |

### 14. GROUNDWATER-SPECIFIC PARAMETERS

| Parameter Code | Parameter Name | Units | Description | Years Available |
|---------------|----------------|-------|-------------|-----------------|
| **72019** | Depth to water level | Feet below land surface | Water table depth | 1950-present |
| **72020** | Depth to water level | Feet above datum | Potentiometric surface | 1950-present |
| **72150** | Well depth | Feet | Total well depth | 1950-present |
| **72008** | Altitude of land surface | Feet | Reference elevation | Static |
| **82398** | Oxidation reduction potential (ORP) | mV | Redox conditions | 1990-present |
| **00403** | Dissolved gases (various) | mg/L | Aquifer geochemistry | 1980-present |

### 15. ADDITIONAL PARAMETERS

#### Silica

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **00955** | Silica, dissolved | mg/L as SiO₂ | 1950-present |
| **00956** | Silica, total | mg/L as SiO₂ | 1950-present |

#### Cyanide

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **00720** | Cyanide, total | mg/L | 1970-present |
| **00723** | Cyanide, free | mg/L | 1980-present |

#### Sulfide

| Parameter Code | Parameter Name | Units | Years Available |
|---------------|----------------|-------|-----------------|
| **00745** | Sulfide, dissolved | mg/L | 1970-present |

---

## Access Methods and Tools

### 1. dataRetrieval R Package (Primary Recommended Tool)

The `dataRetrieval` R package is the official USGS package for retrieving water data. It has been modernized in 2025 to work with new USGS Water Data APIs.

#### Installation

```r
install.packages("dataRetrieval")
library(dataRetrieval)
```

#### Key Functions

##### whatNWISsites() - Discovering Monitoring Sites

Find sites based on location, parameter availability, and other criteria.

```r
# Find sites in a bounding box with specific parameters
sites <- whatNWISsites(
  bBox = c(-83.0, 36.5, -81.0, 38.5),
  parameterCd = c("00010", "00060"),
  hasDataTypeCd = "dv"
)

# Find sites by county
sites_county <- whatNWISsites(
  stateCd = "Wisconsin",
  countyCd = "Dane",
  parameterCd = "00095"
)
```

##### whatNWISdata() - Check Available Data at Sites

Discover what data is available for specific sites including parameters, period of record, and sample counts.

```r
# Check data availability for a site
site_info <- whatNWISdata(
  siteNumber = "05114000"
)

# Filter to specific parameter
site_nitrate <- whatNWISdata(
  siteNumber = "05114000",
  parameterCd = "00618"
)
```

##### readNWISdata() - Flexible Data Retrieval

Most flexible function for retrieving NWIS data. **This is the recommended function for county-level queries.**

```r
# County-level query for discharge data
county_data <- readNWISdata(
  stateCd = "Hawaii",
  countyCd = "Maui",
  service = "dv",
  parameterCd = "00060",
  startDate = "2020-01-01",
  endDate = "2020-12-31"
)

# Water quality data for multiple parameters
wq_data <- readNWISdata(
  stateCd = "Wisconsin",
  service = "qw",
  parameterCd = c("00618", "00665", "00940"),
  startDate = "2015-01-01",
  endDate = "2023-12-31"
)
```

**Important:** When using `countyCd`, you must also specify `stateCd`. County codes follow the format: state FIPS + county FIPS (e.g., "Dane County, Wisconsin" = state "WI" or "55", county "Dane" or "025").

##### readNWISqw() - Water Quality Sample Data

Retrieves discrete water quality samples for specific sites. **Note:** Does not support direct county-level queries - use readNWISdata() instead for county queries.

```r
# Get water quality data for a site
qw_data <- readNWISqw(
  siteNumbers = c("05114000", "05288500"),
  parameterCd = c("00618", "00665", "80154"),
  startDate = "2015-01-01",
  endDate = "2023-12-31"
)
```

##### readNWISdv() - Daily Values

```r
# Daily discharge data
daily_Q <- readNWISdv(
  siteNumbers = "05114000",
  parameterCd = "00060",
  startDate = "2020-01-01",
  endDate = "2020-12-31"
)
```

##### readNWISuv() - Unit (Real-time) Values

```r
# 15-minute interval data
instantaneous <- readNWISuv(
  siteNumbers = "05114000",
  parameterCd = "00060",
  startDate = "2023-01-01",
  endDate = "2023-01-31"
)
```

##### readNWISstat() - Statistical Summaries

```r
# Monthly statistics
monthly_stats <- readNWISstat(
  siteNumbers = "05114000",
  parameterCd = "00060",
  statReportType = "monthly"
)
```

##### readNWISuse() - Water Use Data

```r
# County-level water use data
water_use <- readNWISuse(
  stateCd = "Pennsylvania",
  countyCd = "Allegheny",
  years = c(2015)
)
```

#### Parameter Code Lookup Functions

##### readNWISpCode() - Look up parameter information

```r
# Get information about a specific parameter code
param_info <- readNWISpCode("00618")

# Search for parameters by name
nitrate_params <- readNWISpCode("nitrate")
```

##### pcode_to_name() - Convert parameter codes to names

```r
# Convert codes to characteristic names
param_names <- pcode_to_name(c("00618", "00665", "00940"))
```

#### Helper Data

##### countyCd - County Code Lookup Table

```r
# Load county code lookup table
data(countyCd)

# View Wisconsin counties
wi_counties <- countyCd[countyCd$STATE == "55", ]

# Search for specific county
dane_county <- countyCd[countyCd$COUNTY_NAME == "Dane County", ]
```

##### countyCdLookup() - Search for county codes

```r
# Look up county by name
county_info <- countyCdLookup(state = "WI", county = "Dane")
```

### 2. NWIS Web Services API (Direct URL Access)

For programmatic access without R, use NWIS web services directly.

#### Base URLs

**Current (Legacy) Services:**
- Site info: `https://waterdata.usgs.gov/nwis/inventory`
- Daily values: `https://nwis.waterdata.usgs.gov/nwis/dv`
- Instantaneous values: `https://nwis.waterdata.usgs.gov/nwis/uv`
- Water quality: `https://nwis.waterdata.usgs.gov/nwis/qw`
- Statistics: `https://nwis.waterdata.usgs.gov/nwis/stat`
- Water use: `https://waterdata.usgs.gov/nwis/wu`

**New API (2024-2025):**
- Parameter codes: `https://api.waterdata.usgs.gov/ogcapi/v0/collections/parameter-codes`

#### Example API Queries

##### Get Sites in a County

```
https://waterdata.usgs.gov/nwis/inventory?state_cd=55&county_cd=025&format=rdb
```

Parameters:
- `state_cd`: State FIPS code (e.g., 55 for Wisconsin)
- `county_cd`: County FIPS code (e.g., 025 for Dane County)
- `format`: rdb (tab-delimited), rdb_expanded, json, xml

##### Get Water Quality Data for County Sites

```
https://nwis.waterdata.usgs.gov/nwis/qw?state_cd=55&county_cd=025&param_cd=00618&begin_date=2020-01-01&end_date=2023-12-31&format=rdb
```

Parameters:
- `param_cd`: Parameter code (e.g., 00618 for nitrate)
- `begin_date`: Start date (YYYY-MM-DD)
- `end_date`: End date (YYYY-MM-DD)

##### Get Daily Values

```
https://nwis.waterdata.usgs.gov/nwis/dv?site_no=05114000&parameterCd=00060&startDT=2023-01-01&endDT=2023-12-31&format=json
```

#### Rate Limits and Best Practices

- No explicit rate limits, but be considerate
- Large queries should be broken into smaller chunks
- Use caching for repeated queries
- Consider batch downloads during off-peak hours

### 3. Water Quality Portal (WQP) - Multi-Agency Data

The Water Quality Portal integrates data from USGS, EPA STORET, and USDA.

#### Access URL
`https://www.waterqualitydata.us/`

#### R Functions (via dataRetrieval)

##### whatWQPdata() - Discover WQP Data

```r
# Find data by county
wqp_sites <- whatWQPdata(
  countycode = "US:55:025",
  siteType = "Stream",
  characteristicName = "Nitrate"
)
```

**Important:** WQP uses different county code format: "US:STATE_FIPS:COUNTY_FIPS"

##### readWQPdata() - Retrieve WQP Data

```r
# Get water quality data from WQP
wqp_data <- readWQPdata(
  countycode = "US:55:025",
  characteristicName = "Nitrate",
  startDate = "2020-01-01",
  endDate = "2023-12-31"
)
```

**Note:** WQP uses characteristic names instead of parameter codes. Use `characteristicName` instead of `parameterCd`.

#### Direct WQP API

```
https://www.waterqualitydata.us/data/Result/search?countrycode=US&statecode=US:55&countycode=US:55:025&characteristicName=Nitrate&startDateLo=01-01-2020&startDateHi=12-31-2023&mimeType=csv
```

### 4. NWISWeb Interface (Manual Downloads)

For manual data exploration and download:

**Main Portal:** https://waterdata.usgs.gov/nwis

**Mapper Tool:** https://maps.waterdata.usgs.gov/mapper/

#### Steps for Manual Download

1. Go to https://waterdata.usgs.gov/nwis
2. Select "Water Quality Samples" or other data type
3. Choose "Site Selection" or "County" as location method
4. Select state and county from dropdowns
5. Enter parameter codes or search by name
6. Select date range
7. Choose output format (tab-separated, Excel, CSV)
8. Click "Submit"

---

## County-Level Data Retrieval

### Strategy 1: Direct County Query (Recommended)

Use `readNWISdata()` with county codes to retrieve data from all sites within a county.

```r
library(dataRetrieval)

# Example: Get nitrate data for Dane County, Wisconsin
dane_nitrate <- readNWISdata(
  stateCd = "WI",
  countyCd = "Dane",
  service = "qw",
  parameterCd = "00618",
  startDate = "2015-01-01",
  endDate = "2023-12-31"
)

# Multiple parameters
dane_multi <- readNWISdata(
  stateCd = "55",  # Wisconsin FIPS
  countyCd = "025",  # Dane County FIPS
  service = "qw",
  parameterCd = c("00618", "00665", "00940", "00945"),
  startDate = "2010-01-01",
  endDate = "2023-12-31"
)
```

### Strategy 2: Find Sites First, Then Query

This two-step approach provides more control and visibility into data sources.

```r
# Step 1: Find all sites in county
sites <- whatNWISsites(
  stateCd = "WI",
  countyCd = "Dane",
  hasDataTypeCd = "qw"
)

# Step 2: Get data for those sites
site_numbers <- sites$site_no

county_wq <- readNWISqw(
  siteNumbers = site_numbers,
  parameterCd = c("00618", "00665", "00940"),
  startDate = "2015-01-01",
  endDate = "2023-12-31"
)
```

### Strategy 3: Water Quality Portal (Multi-Agency)

Access combined USGS, EPA, and USDA data.

```r
# WQP county query (includes non-USGS data)
wqp_county <- readWQPdata(
  countycode = "US:55:025",  # Note different format
  characteristicName = c("Nitrate", "Total Phosphorus", "Escherichia coli"),
  startDate = "2015-01-01",
  endDate = "2023-12-31"
)
```

### County Aggregation Methods

Once you have site-level data, aggregate to county level:

#### Method 1: Annual Mean by County

```r
library(dplyr)

# Calculate annual mean concentration by county
county_annual <- dane_nitrate %>%
  mutate(year = lubridate::year(ActivityStartDate)) %>%
  group_by(year) %>%
  summarise(
    mean_nitrate = mean(result_va, na.rm = TRUE),
    median_nitrate = median(result_va, na.rm = TRUE),
    n_samples = n(),
    n_sites = n_distinct(site_no)
  )
```

#### Method 2: Exceedance Rates

```r
# Calculate percent of samples exceeding drinking water standard
standard_nitrate <- 10  # mg/L as N

exceedance_summary <- dane_nitrate %>%
  mutate(year = lubridate::year(ActivityStartDate)) %>%
  group_by(year) %>%
  summarise(
    total_samples = n(),
    exceedances = sum(result_va > standard_nitrate, na.rm = TRUE),
    exceedance_rate = (exceedances / total_samples) * 100
  )
```

#### Method 3: Spatial Coverage Assessment

```r
# Assess data quality - how many sites contribute?
coverage <- dane_nitrate %>%
  group_by(site_no) %>%
  summarise(
    n_samples = n(),
    first_sample = min(ActivityStartDate),
    last_sample = max(ActivityStartDate),
    median_value = median(result_va, na.rm = TRUE)
  )

# Calculate county-level metric with coverage note
county_metric <- dane_nitrate %>%
  summarise(
    mean_nitrate = mean(result_va, na.rm = TRUE),
    se_nitrate = sd(result_va, na.rm = TRUE) / sqrt(n()),
    n_sites = n_distinct(site_no),
    n_samples = n(),
    data_quality = case_when(
      n_distinct(site_no) >= 5 ~ "Good",
      n_distinct(site_no) >= 2 ~ "Moderate",
      TRUE ~ "Limited"
    )
  )
```

### Handling Detection Limits

Many water quality parameters have method detection limits (MDL) and reporting levels.

```r
# Data often includes remark codes
# "<" indicates below detection limit
# Handle censored data

library(NADA)  # For censored data analysis

# Replace "<" with numeric MDL value
dane_nitrate_clean <- dane_nitrate %>%
  mutate(
    censored = grepl("<", result_va),
    value_numeric = as.numeric(gsub("<", "", result_va)),
    detection_limit = ifelse(censored, value_numeric, NA)
  )

# Use robust estimators for censored data
# Kaplan-Meier method via NADA package
with(dane_nitrate_clean, cenros(value_numeric, censored))
```

---

## R Code Examples

### Example 1: Comprehensive County Water Quality Assessment

```r
library(dataRetrieval)
library(dplyr)
library(lubridate)
library(ggplot2)

# Define target county
state <- "California"
county <- "Los Angeles"

# Define parameters of interest (nutrients, metals, bacteria)
params <- c(
  "00618",  # Nitrate
  "00665",  # Total phosphorus
  "01049",  # Lead, dissolved
  "71900",  # Mercury, total
  "31699"   # E. coli
)

# Step 1: Find sites in county
sites <- whatNWISsites(
  stateCd = state,
  countyCd = county,
  hasDataTypeCd = "qw"
)

cat(sprintf("Found %d sites in %s County, %s\n",
            nrow(sites), county, state))

# Step 2: Retrieve water quality data (last 10 years)
end_date <- Sys.Date()
start_date <- end_date - years(10)

wq_data <- readNWISdata(
  stateCd = state,
  countyCd = county,
  service = "qw",
  parameterCd = params,
  startDate = format(start_date, "%Y-%m-%d"),
  endDate = format(end_date, "%Y-%m-%d")
)

# Step 3: Add parameter names
wq_data <- wq_data %>%
  left_join(
    parameterCdFile %>% select(parameter_cd, parameter_nm, parameter_units),
    by = c("parm_cd" = "parameter_cd")
  )

# Step 4: Calculate annual county-level summaries
annual_summary <- wq_data %>%
  mutate(year = year(sample_dt)) %>%
  group_by(year, parm_cd, parameter_nm) %>%
  summarise(
    mean_value = mean(result_va, na.rm = TRUE),
    median_value = median(result_va, na.rm = TRUE),
    sd_value = sd(result_va, na.rm = TRUE),
    n_samples = n(),
    n_sites = n_distinct(site_no),
    .groups = "drop"
  )

# Step 5: Visualize trends
ggplot(annual_summary, aes(x = year, y = median_value)) +
  geom_line() +
  geom_point() +
  facet_wrap(~parameter_nm, scales = "free_y") +
  labs(
    title = paste("Water Quality Trends in", county, "County,", state),
    x = "Year",
    y = "Median Concentration"
  ) +
  theme_bw()

# Step 6: Compare to standards
standards <- data.frame(
  parm_cd = c("00618", "00665", "01049", "71900", "31699"),
  standard_value = c(10, 0.1, 15, 2, 235),
  standard_name = c(
    "Drinking water MCL",
    "EPA recommended",
    "Drinking water MCL",
    "Drinking water MCL",
    "Beach action value"
  )
)

exceedances <- wq_data %>%
  left_join(standards, by = "parm_cd") %>%
  filter(!is.na(standard_value)) %>%
  mutate(
    exceeds = result_va > standard_value,
    year = year(sample_dt)
  ) %>%
  group_by(year, parm_cd, parameter_nm, standard_name) %>%
  summarise(
    exceedance_rate = mean(exceeds, na.rm = TRUE) * 100,
    n_samples = n(),
    .groups = "drop"
  )

print(exceedances)
```

### Example 2: Multi-County Comparison

```r
library(dataRetrieval)
library(dplyr)
library(tidyr)
library(ggplot2)

# Compare nitrate levels across multiple counties in Iowa
counties <- c("Black Hawk", "Story", "Polk", "Linn")
param_cd <- "00618"  # Nitrate

# Function to get county data
get_county_nitrate <- function(county_name) {
  data <- readNWISdata(
    stateCd = "IA",
    countyCd = county_name,
    service = "qw",
    parameterCd = param_cd,
    startDate = "2018-01-01",
    endDate = "2023-12-31"
  )

  data$county <- county_name
  return(data)
}

# Get data for all counties
all_data <- bind_rows(lapply(counties, get_county_nitrate))

# Calculate county summaries
county_summary <- all_data %>%
  group_by(county) %>%
  summarise(
    mean_nitrate = mean(result_va, na.rm = TRUE),
    median_nitrate = median(result_va, na.rm = TRUE),
    p90_nitrate = quantile(result_va, 0.90, na.rm = TRUE),
    pct_above_10 = mean(result_va > 10, na.rm = TRUE) * 100,
    n_samples = n(),
    n_sites = n_distinct(site_no)
  ) %>%
  arrange(desc(median_nitrate))

print(county_summary)

# Visualize comparison
ggplot(all_data, aes(x = county, y = result_va)) +
  geom_boxplot(fill = "skyblue") +
  geom_hline(yintercept = 10, color = "red", linetype = "dashed",
             linewidth = 1) +
  labs(
    title = "Nitrate Concentrations in Iowa Counties (2018-2023)",
    subtitle = "Red line shows drinking water MCL (10 mg/L as N)",
    x = "County",
    y = "Nitrate (mg/L as N)"
  ) +
  theme_minimal()
```

### Example 3: Temporal Trend Analysis with Detection Limits

```r
library(dataRetrieval)
library(dplyr)
library(lubridate)
library(NADA)

# Get lead data for a county
county_lead <- readNWISdata(
  stateCd = "Michigan",
  countyCd = "Wayne",
  service = "qw",
  parameterCd = "01049",  # Lead, dissolved
  startDate = "2000-01-01",
  endDate = "2023-12-31"
)

# Handle detection limits
# NWIS uses remark_cd to indicate censoring
# "<" means below detection limit

county_lead_processed <- county_lead %>%
  mutate(
    censored = remark_cd == "<",
    value = result_va,
    year = year(sample_dt)
  ) %>%
  filter(!is.na(value))

# Calculate annual summaries using robust methods for censored data
annual_lead <- county_lead_processed %>%
  group_by(year) %>%
  summarise(
    n_samples = n(),
    n_censored = sum(censored),
    pct_censored = mean(censored) * 100,
    # Use Kaplan-Meier mean for censored data
    km_mean = cenros(value, censored)$`Kaplan-Meier`[1],
    max_detected = max(value[!censored], na.rm = TRUE),
    .groups = "drop"
  )

# Test for temporal trend using Mann-Kendall test
library(Kendall)
mk_test <- MannKendall(annual_lead$km_mean)
print(mk_test)

# Visualize trend
ggplot(annual_lead, aes(x = year, y = km_mean)) +
  geom_line(color = "blue") +
  geom_point(size = 3) +
  geom_smooth(method = "loess", se = TRUE, color = "red") +
  labs(
    title = "Lead Concentration Trends in Wayne County, Michigan",
    subtitle = sprintf("Mann-Kendall trend test: tau = %.3f, p = %.4f",
                       mk_test$tau, mk_test$sl),
    x = "Year",
    y = "Lead (µg/L, Kaplan-Meier mean)"
  ) +
  theme_bw()
```

### Example 4: Water Use Data by County

```r
library(dataRetrieval)
library(dplyr)
library(tidyr)
library(ggplot2)

# Get water use data for multiple counties across multiple years
state <- "California"
counties <- c("Los Angeles", "San Diego", "Orange", "Riverside", "San Bernardino")
years <- seq(2000, 2020, by = 5)

# Function to safely get water use data
get_water_use <- function(county_name, year) {
  tryCatch({
    data <- readNWISuse(
      stateCd = state,
      countyCd = county_name,
      years = year
    )
    data$county <- county_name
    data$year <- year
    return(data)
  }, error = function(e) {
    return(NULL)
  })
}

# Get data for all combinations
water_use_list <- list()
for (county in counties) {
  for (year in years) {
    water_use_list[[paste(county, year)]] <- get_water_use(county, year)
  }
}

# Combine into single data frame
water_use_data <- bind_rows(water_use_list)

# Calculate total withdrawals by category
water_use_summary <- water_use_data %>%
  select(county, year, matches("total")) %>%
  pivot_longer(
    cols = -c(county, year),
    names_to = "category",
    values_to = "withdrawal_mgd"
  ) %>%
  filter(!is.na(withdrawal_mgd))

# Visualize water use trends
ggplot(water_use_summary,
       aes(x = year, y = withdrawal_mgd, color = county)) +
  geom_line(linewidth = 1) +
  geom_point(size = 2) +
  facet_wrap(~category, scales = "free_y") +
  labs(
    title = "Water Withdrawals in Southern California Counties",
    x = "Year",
    y = "Withdrawal (Million Gallons per Day)",
    color = "County"
  ) +
  theme_bw() +
  theme(legend.position = "bottom")
```

### Example 5: Comprehensive Multi-Parameter County Report

```r
library(dataRetrieval)
library(dplyr)
library(tidyr)
library(lubridate)

# Generate comprehensive water quality report for a county

generate_county_wq_report <- function(state, county, start_year = 2015) {

  # Define parameter groups
  param_groups <- list(
    Physical = c("00010", "00095", "00300", "00400"),
    Nutrients = c("00618", "00631", "00665"),
    Major_Ions = c("00915", "00925", "00930", "00940", "00945"),
    Metals = c("01049", "71900", "01042", "01092"),
    Bacteria = c("31699", "31649")
  )

  # Initialize results list
  results <- list()

  # Get data for each parameter group
  for (group_name in names(param_groups)) {
    cat(sprintf("Fetching %s data...\n", group_name))

    data <- readNWISdata(
      stateCd = state,
      countyCd = county,
      service = "qw",
      parameterCd = param_groups[[group_name]],
      startDate = paste0(start_year, "-01-01"),
      endDate = format(Sys.Date(), "%Y-%m-%d")
    )

    if (nrow(data) > 0) {
      # Add parameter names
      data <- data %>%
        left_join(
          parameterCdFile %>%
            select(parameter_cd, parameter_nm, parameter_units),
          by = c("parm_cd" = "parameter_cd")
        ) %>%
        mutate(
          year = year(sample_dt),
          parameter_group = group_name
        )

      results[[group_name]] <- data
    }
  }

  # Combine all data
  all_data <- bind_rows(results)

  # Calculate summary statistics
  summary_stats <- all_data %>%
    group_by(parameter_group, parm_cd, parameter_nm, parameter_units) %>%
    summarise(
      n_samples = n(),
      n_sites = n_distinct(site_no),
      n_years = n_distinct(year),
      first_sample = min(sample_dt),
      last_sample = max(sample_dt),
      mean_value = mean(result_va, na.rm = TRUE),
      median_value = median(result_va, na.rm = TRUE),
      min_value = min(result_va, na.rm = TRUE),
      max_value = max(result_va, na.rm = TRUE),
      sd_value = sd(result_va, na.rm = TRUE),
      .groups = "drop"
    )

  # Annual trends
  annual_summary <- all_data %>%
    group_by(parameter_group, parm_cd, parameter_nm, year) %>%
    summarise(
      mean_value = mean(result_va, na.rm = TRUE),
      n_samples = n(),
      .groups = "drop"
    )

  # Return comprehensive report
  return(list(
    raw_data = all_data,
    summary_statistics = summary_stats,
    annual_trends = annual_summary,
    metadata = list(
      state = state,
      county = county,
      start_year = start_year,
      end_date = Sys.Date(),
      total_samples = nrow(all_data),
      total_sites = n_distinct(all_data$site_no),
      parameters_measured = n_distinct(all_data$parm_cd)
    )
  ))
}

# Generate report
report <- generate_county_wq_report(
  state = "Wisconsin",
  county = "Dane",
  start_year = 2015
)

# View summary
print(report$metadata)
print(report$summary_statistics)

# Save results
saveRDS(report, "dane_county_wq_report.rds")
write.csv(report$summary_statistics,
          "dane_county_summary_stats.csv",
          row.names = FALSE)
```

---

## Data Quality and Standards

### USGS Quality Assurance Procedures

#### Quality-Control Samples

USGS collects multiple types of QC samples:

1. **Field Blanks** - Detect contamination during sampling
2. **Replicate Samples** - Assess variability and precision
3. **Spike Samples** - Evaluate analytical recovery
4. **Reference Samples** - Verify laboratory performance

QC sample types are identified in NWIS using specific codes and can be filtered in data retrieval.

#### Laboratory vs. Field Measurements

Many parameters can be measured in the field or laboratory:

- **Field measurements** - Immediate readings at sample collection (e.g., pH, dissolved oxygen, specific conductance, temperature)
- **Laboratory measurements** - Samples analyzed after preservation and transport

Field measurements are typically preferred for parameters that change quickly (pH, DO), while laboratory measurements provide more precision for stable parameters.

#### Method Detection Limits (MDL) and Reporting Levels

- **MDL** - Lowest concentration that can be detected with 99% confidence
- **LRL (Laboratory Reporting Level)** - Concentration at which there's ≤1% false positive risk
- **NWIS uses remark codes:**
  - `<` - Below detection/reporting level
  - `E` - Estimated value (between MDL and LRL)
  - `>` - Above upper detection limit
  - `A` - Value affected by contamination
  - `V` - Value affected by method variance

#### Data Qualifiers and Remarks

Check the `remark_cd` field in NWIS data:

```r
# Filter to detected values only
detected_only <- wq_data %>%
  filter(is.na(remark_cd) | remark_cd != "<")

# Identify estimated values
estimated <- wq_data %>%
  filter(remark_cd == "E")
```

### National Water Quality Standards

#### Drinking Water Standards (EPA MCLs)

| Parameter | MCL | Units | Notes |
|-----------|-----|-------|-------|
| Nitrate | 10 | mg/L as N | Safe Drinking Water Act |
| Lead | 15 | µg/L | Action level |
| Arsenic | 10 | µg/L | Revised 2006 |
| Mercury | 2 | µg/L | Inorganic |
| Total coliform | 0 | Positive samples | No more than 5% |
| E. coli | 0 | Colonies/100mL | MCL |
| PCBs | 0.5 | µg/L | Total |
| Atrazine | 3 | µg/L | |

#### Aquatic Life Criteria

EPA establishes water quality criteria to protect aquatic life:

- **Acute criteria** - 1-hour average concentration
- **Chronic criteria** - 4-day average concentration

Example for copper (µg/L, varies with water hardness):
- Hardness 50 mg/L: Acute = 5.2, Chronic = 3.8
- Hardness 100 mg/L: Acute = 9.2, Chronic = 6.5

#### Recreational Water Quality Standards

| Parameter | Standard | Units | Use |
|-----------|----------|-------|-----|
| E. coli | 235 | CFU/100mL | Beach action value |
| Enterococci | 70 | CFU/100mL | Beach action value |

### Data Quality Assessment for County Aggregation

When aggregating site data to county level, consider:

#### Spatial Coverage

```r
# Assess spatial distribution of monitoring sites
site_coverage <- wq_data %>%
  distinct(site_no, dec_lat_va, dec_long_va) %>%
  summarise(
    n_sites = n(),
    lat_range = max(dec_lat_va) - min(dec_lat_va),
    lon_range = max(dec_long_va) - min(dec_long_va)
  )

# Are sites well-distributed or clustered?
```

#### Temporal Coverage

```r
# Assess temporal distribution
temporal_coverage <- wq_data %>%
  group_by(site_no) %>%
  summarise(
    first_date = min(sample_dt),
    last_date = max(sample_dt),
    n_samples = n(),
    sampling_span_years = as.numeric(difftime(max(sample_dt),
                                               min(sample_dt),
                                               units = "days")) / 365.25
  )

# Check for consistent long-term monitoring
```

#### Sample Representativeness

```r
# Check seasonal coverage
seasonal_coverage <- wq_data %>%
  mutate(
    month = month(sample_dt),
    season = case_when(
      month %in% 3:5 ~ "Spring",
      month %in% 6:8 ~ "Summer",
      month %in% 9:11 ~ "Fall",
      TRUE ~ "Winter"
    )
  ) %>%
  count(season)

# Are all seasons represented?
```

#### Detection Frequency

```r
# Calculate detection frequency
detection_summary <- wq_data %>%
  group_by(parm_cd, parameter_nm) %>%
  summarise(
    n_samples = n(),
    n_detected = sum(is.na(remark_cd) | remark_cd != "<"),
    pct_detected = (n_detected / n_samples) * 100,
    .groups = "drop"
  )

# Parameters with <50% detection are difficult to aggregate meaningfully
```

---

## Related Data Sources

### EPA STORET (via Water Quality Portal)

EPA's STOrage and RETrieval (STORET) database contains water quality data from EPA, states, tribes, and other organizations.

**Access:** Through Water Quality Portal (see Section 3)

**Coverage:**
- Over 2 million monitoring stations
- Data from 400+ organizations
- Includes parameters not routinely measured by USGS

### USDA Water Quality Monitoring

USDA conducts water quality monitoring related to agricultural impacts.

**Programs:**
- Conservation Effects Assessment Project (CEAP)
- Agricultural Research Service (ARS) watersheds
- Natural Resources Conservation Service (NRCS) monitoring

**Access:** Through Water Quality Portal

### State Water Quality Databases

Many states maintain their own water quality databases with more comprehensive local coverage:

- California: SWAMP (Surface Water Ambient Monitoring Program)
- Texas: TCEQ water quality monitoring
- Florida: DEP STORET
- New York: DEC water quality portal

**Access:** State environmental agency websites or through WQP

### USGS SPARROW Model Data

Spatially Referenced Regressions On Watershed attributes (SPARROW) provides estimates of contaminant sources and transport.

**Parameters:** Nitrogen, phosphorus, suspended sediment

**URL:** https://www.usgs.gov/mission-areas/water-resources/science/sparrow-modeling

**Advantage:** Provides modeled estimates for all stream reaches, not just monitored sites

### National Aquifer Studies

USGS conducts Principal Aquifer studies with comprehensive groundwater quality assessments.

**Coverage:** 60+ major aquifers nationwide
**Parameters:** 500+ constituents including VOCs, pesticides, nutrients, trace elements

**URL:** https://www.usgs.gov/mission-areas/water-resources/science/principal-aquifers-united-states

### CDC Environmental Public Health Tracking

CDC tracks environmental health indicators including some water quality measures.

**URL:** https://ephtracking.cdc.gov/

**Parameters:** Public water system violations, contaminant detections

---

## Parameter Code Resources

### Official USGS Resources

#### Primary Documentation

1. **USGS Water Data Help System**
   - URL: https://help.waterdata.usgs.gov/codes-and-parameters
   - Access: Parameter codes, method codes, complete documentation
   - Format: Tab-separated files, HTML tables

2. **NWIS Parameter Code Definition**
   - URL: https://nwis.waterdata.usgs.gov/usa/nwis/pmcodes
   - Search interface for parameter codes
   - Can search by code, name, or CAS Registry Number

3. **USGS Parameter Code Dictionary (PCD)**
   - Maintained in NWIS
   - Updated as new parameters are added
   - Includes historical codes

#### Parameter Groups

USGS organizes parameters into groups. Major groups include:

| Group Code | Group Name | Description |
|------------|------------|-------------|
| **PHY** | Physical | Temperature, pH, conductance, DO, turbidity |
| **NUT** | Nutrients | Nitrogen and phosphorus compounds |
| **INN** | Inorganic, major | Major ions, alkalinity, hardness |
| **INM** | Inorganic, minor | Trace elements, heavy metals |
| **OPE** | Organics, pesticide | Herbicides, insecticides, fungicides |
| **OPC** | Organics, PCBs | Polychlorinated biphenyls |
| **OVU** | Organics, volatile | VOCs, solvents |
| **OOT** | Organics, other | PAHs, SVOCs, other organic contaminants |
| **OPF** | Organics, PFAS | Per- and polyfluoroalkyl substances |
| **MIC** | Microbiological | Bacteria, viruses |
| **SED** | Sediment | Suspended sediment, bedload |
| **BIO** | Biological | Chlorophyll, algae, macroinvertebrates |
| **ISO** | Isotopes | Stable and radioactive isotopes |
| **RAD** | Radiochemical | Radioactive constituents |
| **TOX** | Toxicity | Bioassay results |

**Access group-specific parameters:**

```r
# In R
library(dataRetrieval)
data(parameterCdFile)

# View all nutrient parameters
nutrient_params <- parameterCdFile %>%
  filter(parameter_group_nm == "Nutrient")

# View all physical parameters
physical_params <- parameterCdFile %>%
  filter(parameter_group_nm == "Physical")
```

### Downloadable Parameter Code Lists

#### From USGS Help System

**Tab-separated format:**
```
https://help.waterdata.usgs.gov/parameter_cd?group_cd=NUT&format=rdb
```

Replace `NUT` with any group code, or use `%25` for all parameters.

**HTML format:**
```
https://help.waterdata.usgs.gov/parameter_cd?group_cd=NUT&format=html
```

### R Package Resources

#### parameterCdFile Data

```r
library(dataRetrieval)

# Load complete parameter code table (as of Oct 24, 2024)
data(parameterCdFile)

# View structure
str(parameterCdFile)

# Search for specific parameters
nitrogen_params <- parameterCdFile %>%
  filter(grepl("nitrogen", parameter_nm, ignore.case = TRUE))

# Get parameter units
param_units <- parameterCdFile %>%
  select(parameter_cd, parameter_nm, parameter_units)
```

#### readNWISpCode() Function

```r
# Get detailed information for specific parameter
info <- readNWISpCode("00618")
print(info)

# Search by name
nitrate_codes <- readNWISpCode("nitrate")
print(nitrate_codes)
```

### Cross-Reference Resources

#### Parameter Code to CAS Registry Number

```r
# Many parameters include CAS RN for chemical identification
cas_crossref <- parameterCdFile %>%
  filter(!is.na(casrn)) %>%
  select(parameter_cd, parameter_nm, casrn, srsname)
```

#### Legacy Parameter Codes

Some parameters have had code changes over time. NWIS maintains both current and legacy codes.

**Example:**
- Alkalinity was stored under parameter code 00410 prior to 1981
- After 1981, laboratory alkalinities use 90410

### USGS Publications with Parameter Information

1. **NWIS User's Manual (2006)**
   - URL: https://pubs.usgs.gov/of/2006/1145/
   - Comprehensive documentation of NWIS structure and codes

2. **NAWQA Program Publications**
   - URL: https://water.usgs.gov/nawqa/
   - Studies using consistent parameter sets across the nation

3. **Methods and Guidance**
   - National Water Quality Laboratory methods
   - URL: https://www.usgs.gov/labs/nwql/
   - Links parameter codes to analytical methods

### Water Quality Portal Characteristic Names

WQP uses characteristic names instead of parameter codes. Crosswalk available:

```r
library(dataRetrieval)

# Get crosswalk between USGS codes and WQP characteristic names
pcode_to_name <- pCodeToName

# Example conversions:
# 00618 (USGS) = "Nitrate" (WQP)
# 00665 (USGS) = "Total Phosphorus, mixed forms" (WQP)
```

---

## Appendix A: Quick Reference - Most Common Parameters

### Top 20 Most Frequently Measured Water Quality Parameters

| Rank | Code | Parameter | Units | Category |
|------|------|-----------|-------|----------|
| 1 | 00060 | Discharge | ft³/s | Physical |
| 2 | 00065 | Gage height | feet | Physical |
| 3 | 00010 | Temperature, water | °C | Physical |
| 4 | 00095 | Specific conductance | µS/cm | Physical |
| 5 | 00300 | Dissolved oxygen | mg/L | Physical |
| 6 | 00400 | pH | Standard units | Physical |
| 7 | 00618 | Nitrate | mg/L as N | Nutrient |
| 8 | 00631 | Nitrite + nitrate | mg/L as N | Nutrient |
| 9 | 00665 | Total phosphorus | mg/L as P | Nutrient |
| 10 | 00940 | Chloride | mg/L | Major ion |
| 11 | 00945 | Sulfate | mg/L | Major ion |
| 12 | 00915 | Calcium | mg/L | Major ion |
| 13 | 00925 | Magnesium | mg/L | Major ion |
| 14 | 00930 | Sodium | mg/L | Major ion |
| 15 | 00900 | Hardness | mg/L as CaCO₃ | Major ion |
| 16 | 80154 | Suspended sediment | mg/L | Sediment |
| 17 | 00530 | Total suspended solids | mg/L | Physical |
| 18 | 31699 | E. coli | CFU/100mL | Bacteria |
| 19 | 32209 | Chlorophyll a | µg/L | Biological |
| 20 | 00680 | Total organic carbon | mg/L | Organic |

### USGS Water Use Categories

Available through readNWISuse():

| Category | Description | Available Years |
|----------|-------------|-----------------|
| Public Supply | Municipal water systems | 1950-2020 |
| Domestic | Self-supplied domestic | 1950-2020 |
| Irrigation | Agricultural and golf course | 1950-2020 |
| Thermoelectric | Power plant cooling | 1950-2020 |
| Industrial | Manufacturing and commercial | 1950-2020 |
| Mining | Mineral extraction | 1950-2020 |
| Aquaculture | Fish farming | 1985-2020 |
| Livestock | Animal operations | 1950-2020 |

---

## Appendix B: County Code Reference

### County Code Formats

Different systems use different formats:

**USGS NWIS (dataRetrieval):**
- State: Full name ("Wisconsin"), abbreviation ("WI"), or FIPS ("55")
- County: Full name ("Dane"), or FIPS without state ("025")
- Usage: `stateCd = "WI", countyCd = "Dane"`

**Water Quality Portal:**
- Format: "US:STATE_FIPS:COUNTY_FIPS"
- Example: "US:55:025" (Dane County, Wisconsin)
- Usage: `countycode = "US:55:025"`

**Standard FIPS Codes:**
- 2-digit state + 3-digit county
- Example: 55025 (Wisconsin state code 55, Dane County code 025)

### Using the countyCd Helper

```r
library(dataRetrieval)

# Load county lookup table
data(countyCd)

# View structure
head(countyCd)

# Find specific county
dane <- countyCd[countyCd$COUNTY_NAME == "Dane County", ]
print(dane)

# View all counties in a state
wi_counties <- countyCd[countyCd$STATE == "55", ]
print(wi_counties)

# Use countyCdLookup function
lookup_result <- countyCdLookup(state = "WI", county = "Dane")
print(lookup_result)
```

---

## Appendix C: Important Notes and Limitations

### Data Availability Limitations

1. **Not all parameters measured at all sites**
   - Use `whatNWISdata()` to check availability before querying
   - Parameters vary by program, funding, and study objectives

2. **Temporal coverage varies**
   - Some sites have continuous monitoring (decades)
   - Others have short-term studies (months to years)
   - Long-term trend analysis requires consistent monitoring

3. **Spatial coverage uneven**
   - Urban areas often have more monitoring
   - Agricultural areas monitored for nutrients and pesticides
   - Some rural counties have limited data

4. **Detection limit changes over time**
   - Analytical methods improve, lowering detection limits
   - Historical comparisons must account for method changes
   - Use censored data analysis techniques

### NWIS Transition (2024-2025)

**Critical Update:** USGS is transitioning from legacy NWIS to new systems.

**Key Changes:**
- Data after March 11, 2024 primarily available via WQP services
- Legacy NWIS web services being decommissioned
- dataRetrieval package updated to use new APIs
- Some historical query capabilities may change

**Recommendations:**
- Use latest version of dataRetrieval package
- Test queries with current data before running large historical retrievals
- Consider caching/archiving critical datasets
- Monitor USGS announcements for service changes

### County-Level Aggregation Considerations

1. **Representativeness**
   - Site-level measurements may not represent entire county
   - Consider land use, geology, hydrology when interpreting
   - Large counties may need sub-county analysis

2. **Statistical Power**
   - Minimum sample sizes needed for reliable statistics
   - Recommendation: ≥5 sites and ≥30 samples per county per year for robust estimates
   - Consider multi-year aggregations for rare parameters

3. **Mixing Surface and Groundwater**
   - Different monitoring purposes and frequencies
   - Should generally be analyzed separately
   - Different standards and interpretation

4. **Urban vs. Rural Sites**
   - May need to stratify by land use
   - Urban sites may show higher contamination
   - Agricultural areas show seasonal pesticide patterns

### Data Quality Flags to Consider

```r
# Example filtering for high-quality data
high_quality_data <- wq_data %>%
  filter(
    # Remove estimated values if needed
    is.na(remark_cd) | !remark_cd %in% c("E", "A", "V"),
    # Remove suspected contamination
    is.na(qa_cd) | qa_cd != "Q",
    # Keep only field or lab replicates
    sample_type_cd %in% c("9", "7")  # 9 = regular sample, 7 = replicate
  )
```

---

## Appendix D: Additional Resources

### USGS Training and Tutorials

1. **USGS R Training Curriculum**
   - URL: https://owi.usgs.gov/R/training-curriculum/
   - Comprehensive dataRetrieval tutorials
   - Regular training courses

2. **USGS Water Science School**
   - URL: https://www.usgs.gov/water-science-school
   - Educational resources on water quality

3. **NAWQA Data Warehouse**
   - URL: https://water.usgs.gov/nawqa/
   - Pre-processed datasets for national-scale analyses

### R Package Ecosystem

Additional R packages for water quality analysis:

- **EGRET** - Exploration and Graphics for RivEr Trends
- **NADA** - Nondetects And Data Analysis
- **WaterML** - Import WaterML format data
- **smwrBase** - USGS surface water quality base functions
- **rkt** - Mann-Kendall trend tests

### Academic Publications Using USGS Data

Key studies demonstrating county-level analyses:

1. Sprague et al. (2011) - Nitrate in the Mississippi River Basin
   - DOI: 10.1021/es201221s

2. Stone et al. (2014) - Pesticides in U.S. streams and groundwater
   - DOI: 10.1021/es5025367

3. Dubrovsky et al. (2010) - Nutrients in the Nation's streams and groundwater
   - USGS Circular 1350

### Data Visualization Tools

- **USGS National Water Dashboard**: https://dashboard.waterdata.usgs.gov/
- **USGS Water Quality Watch**: https://waterwatch.usgs.gov/wqwatch/
- **WQP Mapper**: https://www.waterqualitydata.us/portal/

### Contact Information

**USGS Water Data Support:**
- Email: https://water.usgs.gov/contact/gsanswers
- Phone: 1-888-ASK-USGS (1-888-275-8747)

**USGS National Water Information System:**
- Web: https://waterdata.usgs.gov/nwis

**Water Quality Portal Support:**
- Email: wqp@usgs.gov

---

## Document Metadata

**Document Version:** 3.0 (Comprehensive)
**Last Updated:** November 11, 2025
**Compiled by:** Research Assistant (Claude)
**Data Sources:** USGS NWIS, Water Quality Portal, dataRetrieval R package documentation, NAWQA program publications

**Recommended Citation:**
```
USGS Water Quality Parameters - Comprehensive County-Level Data Guide. (2025).
Version 3.0. Compiled from USGS National Water Information System, Water Quality
Portal, and dataRetrieval R package documentation. Retrieved November 11, 2025.
```

**Change Log:**
- Version 1.0 (Initial): Basic parameter list
- Version 2.0: Added R code examples and county aggregation methods
- Version 3.0 (Current): Comprehensive catalog with all parameter categories, detailed code examples, and 2024-2025 updates

---

## End of Document

This comprehensive guide documents ALL major USGS water quality parameters available at the county level as of November 2025. For the most current parameter codes and methods, always consult the official USGS resources listed in Section 8.

For questions, corrections, or updates to this document, contact the repository maintainer or submit an issue to the project repository.
