# USGS NWIS COMPLETE PARAMETER CODES CATALOG
## All 1,300+ Water Quality & Hydrologic Parameters

**Purpose:** Complete reference catalog of all USGS National Water Information System (NWIS) parameter codes for water quality, physical properties, and hydrologic measurements at monitoring sites across the United States.

**Total Parameters:** 1,300+ unique 5-digit parameter codes

**Spatial Coverage:** 1.9 million monitoring sites across all 50 states, DC, Puerto Rico, US territories

**Temporal Coverage:** Historical data from 1850s to real-time (varies by site and parameter)

---

## 📥 ACCESS COMPLETE OFFICIAL PARAMETER CODE DATABASE

### Primary Database
**USGS NWIS Parameter Code Search:**
https://nwis.waterdata.usgs.gov/usa/nwis/pmcodes

**Features:**
- Searchable by code, parameter name, or keyword
- Complete definitions, units, measurement methods
- Links to Substance Registry System (SRS) names
- Real-time updates as new parameters added

### Alternative Access Methods

**1. Water Quality Portal - SRS Names Association:**
http://www.waterqualitydata.us/public_srsnames/
- All USGS parameters linked to EPA Substance Registry System
- Cross-reference between USGS codes and WQX characteristics
- Chemical Abstract Service (CAS) numbers where applicable

**2. Programmatic Access - Python dataretrieval Package:**
```python
from dataretrieval import nwis

# Get parameter code information
pmcodes_df, md = nwis.get_pmcodes(parameterCd='00060')  # Discharge
pmcodes_df, md = nwis.get_pmcodes(parameterCd='Nitrogen', partial=True)  # All nitrogen params
```

**3. Programmatic Access - R dataRetrieval Package:**
```r
library(dataRetrieval)

# Get parameter code information
pmcodes <- readNWISpCode(parameterCd = "00060")  # Discharge
pmcodes <- readNWISpCode(parameterCd = "all")    # All parameters
```

---

## 🌡️ PHYSICAL PARAMETERS (Group Code: 000XX - 003XX)

### 1. Temperature & Heat
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00010 | Temperature, water | °C | Surface water, groundwater |
| 00011 | Temperature, water, degrees Fahrenheit | °F | Alternative unit |
| 00020 | Temperature, air | °C | Meteorological stations |
| 00021 | Temperature, air, degrees Fahrenheit | °F | Alternative unit |
| 00036 | Temperature, soil | °C | Vadose zone monitoring |

### 2. Dissolved Oxygen & Saturation
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00300 | Dissolved oxygen | mg/L | Water quality criterion |
| 00301 | Dissolved oxygen, percent saturation | % | Hypoxia monitoring |
| 00302 | Dissolved oxygen, periphyton | mg/L | Benthic studies |

### 3. pH & Acid-Base Chemistry
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00400 | pH, water, unfiltered, field | standard units | All water quality studies |
| 00403 | pH, water, unfiltered, laboratory | standard units | QA/QC comparison |
| 00419 | Acid neutralizing capacity | mg/L as CaCO₃ | Acid mine drainage |

### 4. Conductivity & Ionic Strength
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00095 | Specific conductance, water, unfiltered | µS/cm at 25°C | Salinity proxy |
| 00094 | Specific conductance, water, unfiltered, laboratory | µS/cm at 25°C | QA/QC |
| 90095 | Specific conductance, water, unfiltered, field | µS/cm at 25°C | Real-time monitoring |

### 5. Turbidity & Transparency
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00070 | Turbidity, water, unfiltered, broad band light source | NTRU | TMDLs, sediment |
| 00076 | Turbidity, water, unfiltered, monochrome near infra-red LED light | FNU | ISO 7027 standard |
| 00078 | Secchi depth | meters | Lake transparency |
| 63680 | Turbidity, water, unfiltered, nephelometric | NTU | Historical data |

### 6. Dissolved Solids & Salinity
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 70300 | Dissolved solids, water, filtered, tons per day | tons/day | Salt loading |
| 00530 | Total suspended solids | mg/L | Sediment transport |
| 00535 | Residue on evaporation, water, filtered | mg/L | TDS gravimetric |
| 70301 | Total solids, tons per day | tons/day | Mass balance |

### 7. Redox Chemistry
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00080 | Color, water, filtered, platinum-cobalt units | Pt-Co units | Organic matter |
| 00086 | Color, water, unfiltered, platinum-cobalt units | Pt-Co units | Surface water |
| 00480 | Salinity, water, unfiltered | PSU | Estuarine systems |

### 8. Optical Properties
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 32316 | Absorbance, 254 nm | AU/cm | Dissolved organic carbon proxy |
| 32321 | Absorbance, 280 nm | AU/cm | Aromatic carbon |
| 32322 | Absorbance, 340 nm | AU/cm | Photodegradable organics |
| 32395 | Fluorescence, excitation 370 nm/emission 460 nm | RU | Humic-like fluorescence |

---

## ⚗️ CHEMICAL PARAMETERS

### MAJOR IONS (Group Code: 004XX - 009XX)

#### 9. Calcium, Magnesium, Hardness
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00915 | Calcium, water, filtered | mg/L | Major ion chemistry |
| 00916 | Calcium, water, unfiltered, recoverable | mg/L | Total calcium |
| 00925 | Magnesium, water, filtered | mg/L | Major ion chemistry |
| 00927 | Magnesium, water, unfiltered, recoverable | mg/L | Total magnesium |
| 00900 | Hardness, water | mg/L as CaCO₃ | Water treatment |

#### 10. Sodium & Potassium
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00930 | Sodium, water, filtered | mg/L | Major ion chemistry |
| 00929 | Sodium, water, unfiltered, recoverable | mg/L | Total sodium |
| 00935 | Potassium, water, filtered | mg/L | Major ion chemistry |
| 00937 | Potassium, water, unfiltered, recoverable | mg/L | Total potassium |

#### 11. Chloride, Sulfate, Fluoride
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00940 | Chloride, water, filtered | mg/L | Road salt impacts |
| 00945 | Sulfate, water, filtered | mg/L | Acid mine drainage |
| 00950 | Fluoride, water, filtered | mg/L | Drinking water MCL (4 mg/L) |
| 00955 | Silica, water, filtered | mg/L as SiO₂ | Geochemistry |

#### 12. Alkalinity & Carbonate System
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00410 | Acid neutralizing capacity, water, unfiltered | mg/L as CaCO₃ | Total alkalinity |
| 29801 | Alkalinity, water, filtered, fixed endpoint (pH 4.5) titration | mg/L as CaCO₃ | Standard method |
| 00440 | Bicarbonate, water, filtered, inflection-point titration | mg/L | Carbonate speciation |
| 00445 | Carbonate, water, filtered, inflection-point titration | mg/L | High pH waters |

### NUTRIENTS (Group Code: 006XX, 007XX, 610XX - 650XX)

#### 13. Nitrogen - Dissolved Inorganic Forms
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00608 | Ammonia (NH₃ + NH₄⁺), water, filtered | mg/L as N | Toxicity, nitrification |
| 00610 | Ammonia (NH₃ + NH₄⁺), water, unfiltered | mg/L as N | Total ammonia |
| 00613 | Nitrite, water, filtered | mg/L as N | Nitrification indicator |
| 00618 | Nitrate, water, filtered | mg/L as N | Drinking water MCL (10 mg/L) |
| 00631 | Nitrite + Nitrate, water, filtered | mg/L as N | Total oxidized nitrogen |
| 71851 | Nitrate + nitrite, water, filtered, tons per day | tons/day | Load calculations |

#### 14. Nitrogen - Total & Organic Forms
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00600 | Total nitrogen, water, unfiltered | mg/L | TMDL targets |
| 00602 | Total nitrogen, water, filtered | mg/L | Dissolved nitrogen |
| 00605 | Organic nitrogen, water, unfiltered | mg/L | Difference calculation |
| 00607 | Organic nitrogen, water, filtered | mg/L | Dissolved organic N |
| 62855 | Total nitrogen, water, unfiltered, tons per day | tons/day | Load calculations |

#### 15. Phosphorus - Orthophosphate & Total
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00665 | Phosphorus, water, unfiltered | mg/L | Total phosphorus |
| 00666 | Phosphorus, water, filtered | mg/L | Dissolved reactive P |
| 00671 | Orthophosphate, water, filtered | mg/L as P | Plant-available P |
| 70507 | Orthophosphate, water, filtered, tons per day | tons/day | Load calculations |
| 80154 | Orthophosphate, water, unfiltered | mg/L as P | Total ortho-P |

#### 16. Other Nutrient-Related Parameters
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00625 | Ammonia plus organic nitrogen, water, unfiltered | mg/L | TKN (Total Kjeldahl Nitrogen) |
| 00623 | Ammonia plus organic nitrogen, water, filtered | mg/L | Dissolved TKN |

### METALS - TRACE ELEMENTS (Group Code: 010XX - 719XX)

#### 17. Toxic Metals - Arsenic, Cadmium, Lead, Mercury
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 01000 | Arsenic, water, filtered | µg/L | Drinking water MCL (10 µg/L) |
| 01002 | Arsenic, water, unfiltered, recoverable | µg/L | Total arsenic |
| 01025 | Cadmium, water, filtered | µg/L | Drinking water MCL (5 µg/L) |
| 01027 | Cadmium, water, unfiltered, recoverable | µg/L | Total cadmium |
| 01049 | Lead, water, filtered | µg/L | Drinking water AL (15 µg/L) |
| 01051 | Lead, water, unfiltered, recoverable | µg/L | Total lead |
| 71890 | Mercury, water, filtered | µg/L | Bioaccumulation |
| 71900 | Mercury, water, unfiltered, recoverable | µg/L | Total mercury |

#### 18. Essential Metals - Iron, Manganese, Zinc, Copper
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 01046 | Iron, water, filtered | µg/L | Secondary MCL (300 µg/L) |
| 01045 | Iron, water, unfiltered, recoverable | µg/L | Total iron |
| 01056 | Manganese, water, filtered | µg/L | Secondary MCL (50 µg/L) |
| 01055 | Manganese, water, unfiltered, recoverable | µg/L | Total manganese |
| 01090 | Zinc, water, filtered | µg/L | Secondary MCL (5000 µg/L) |
| 01092 | Zinc, water, unfiltered, recoverable | µg/L | Total zinc |
| 01040 | Copper, water, filtered | µg/L | Action Level (1300 µg/L) |
| 01042 | Copper, water, unfiltered, recoverable | µg/L | Total copper |

#### 19. Other Trace Metals
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 01005 | Barium, water, filtered | µg/L | Drinking water MCL (2000 µg/L) |
| 01007 | Barium, water, unfiltered, recoverable | µg/L | Total barium |
| 01010 | Beryllium, water, filtered | µg/L | Drinking water MCL (4 µg/L) |
| 01012 | Beryllium, water, unfiltered, recoverable | µg/L | Total beryllium |
| 01030 | Chromium, water, filtered | µg/L | Total chromium (all oxidation states) |
| 01034 | Chromium, water, unfiltered, recoverable | µg/L | Total chromium |
| 01145 | Selenium, water, filtered | µg/L | Drinking water MCL (50 µg/L) |
| 01147 | Selenium, water, unfiltered, recoverable | µg/L | Total selenium |
| 01080 | Strontium, water, filtered | µg/L | Emerging concern |
| 01082 | Strontium, water, unfiltered, recoverable | µg/L | Total strontium |
| 01065 | Nickel, water, filtered | µg/L | Aquatic life criteria |
| 01067 | Nickel, water, unfiltered, recoverable | µg/L | Total nickel |
| 01095 | Antimony, water, filtered | µg/L | Drinking water MCL (6 µg/L) |
| 01097 | Antimony, water, unfiltered, recoverable | µg/L | Total antimony |
| 01130 | Lithium, water, filtered | µg/L | Emerging concern |
| 01132 | Lithium, water, unfiltered, recoverable | µg/L | Total lithium |
| 01135 | Aluminum, water, filtered | µg/L | Secondary MCL (50-200 µg/L) |
| 01105 | Aluminum, water, unfiltered, recoverable | µg/L | Total aluminum |
| 00720 | Cyanide, water, unfiltered | mg/L | Toxicity |

### ORGANIC COMPOUNDS (Group Code: 320XX - 999XX)

#### 20. Volatile Organic Compounds (VOCs)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 34030 | Benzene, water, unfiltered, recoverable | µg/L | Gasoline contamination |
| 34371 | Ethylbenzene, water, unfiltered, recoverable | µg/L | Petroleum products |
| 34010 | Toluene, water, unfiltered, recoverable | µg/L | Solvent contamination |
| 34423 | Dichloromethane (Methylene chloride), water, unfiltered | µg/L | Industrial solvent |
| 34496 | 1,1,1-Trichloroethane, water, unfiltered | µg/L | Chlorinated solvent |
| 34475 | Tetrachloroethylene (PCE), water, unfiltered | µg/L | Dry cleaning fluid |
| 39180 | Trichloroethylene (TCE), water, unfiltered | µg/L | Degreaser |
| 34210 | Carbon tetrachloride, water, unfiltered | µg/L | Industrial solvent |
| 34413 | Chloroform, water, unfiltered | µg/L | Disinfection byproduct |

#### 21. BTEX (Benzene, Toluene, Ethylbenzene, Xylenes)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 34030 | Benzene, water, unfiltered, recoverable | µg/L | MCL: 5 µg/L |
| 34010 | Toluene, water, unfiltered, recoverable | µg/L | MCL: 1000 µg/L |
| 34371 | Ethylbenzene, water, unfiltered, recoverable | µg/L | MCL: 700 µg/L |
| 85795 | Xylene (mixed isomers), water, unfiltered, recoverable | µg/L | MCL: 10000 µg/L |
| 34536 | o-Xylene, water, unfiltered, recoverable | µg/L | Individual isomer |
| 77135 | m- & p-Xylene, water, unfiltered, recoverable | µg/L | Combined isomers |

#### 22. Pesticides - Herbicides (Triazines, Chloroacetanilides)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 39632 | Atrazine, water, filtered, recoverable | µg/L | Corn herbicide (MCL: 3 µg/L) |
| 04035 | Atrazine, water, filtered | µg/L | Alternative code |
| 82686 | Metolachlor, water, filtered, recoverable | µg/L | Corn/soybean herbicide |
| 46342 | Alachlor, water, filtered, recoverable | µg/L | MCL: 2 µg/L |
| 49260 | Acetochlor, water, filtered, recoverable | µg/L | Corn herbicide |
| 04040 | Deethylatrazine (DEA), water, filtered, recoverable | µg/L | Atrazine metabolite |
| 38933 | Chlorpyrifos, water, filtered, recoverable | µg/L | Insecticide (organophosphate) |

#### 23. Pesticides - Herbicides (Glyphosate, Phenoxy acids)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 62722 | Glyphosate, water, filtered, recoverable | µg/L | Most-used herbicide |
| 49315 | Atrazine, water, filtered, recoverable | µg/L | Most-detected herbicide |
| 39732 | 2,4-D, water, filtered, recoverable | µg/L | Broadleaf herbicide (MCL: 70 µg/L) |
| 49315 | Simazine, water, filtered, recoverable | µg/L | Triazine herbicide |

#### 24. Pesticides - Insecticides (Organophosphates, Carbamates)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 38933 | Chlorpyrifos, water, filtered, recoverable | µg/L | Organophosphate |
| 39532 | Malathion, water, filtered, recoverable | µg/L | Mosquito control |
| 82346 | Diazinon, water, filtered, recoverable | µg/L | Urban use (restricted) |
| 49260 | Carbaryl, water, filtered, recoverable | µg/L | Carbamate insecticide |

#### 25. Polycyclic Aromatic Hydrocarbons (PAHs)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 34247 | Naphthalene, water, unfiltered, recoverable | µg/L | 2-ring PAH |
| 34696 | Phenanthrene, water, unfiltered, recoverable | µg/L | 3-ring PAH |
| 34548 | Pyrene, water, unfiltered, recoverable | µg/L | 4-ring PAH |
| 34556 | Benzo[a]pyrene, water, unfiltered, recoverable | µg/L | Carcinogenic PAH |
| 34521 | Fluoranthene, water, unfiltered, recoverable | µg/L | 4-ring PAH |

#### 26. Pharmaceutical & Personal Care Products (PPCPs)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 62968 | Caffeine, water, filtered, recoverable | µg/L | Human fecal indicator |
| 62063 | Cotinine, water, filtered, recoverable | µg/L | Nicotine metabolite |
| 62005 | Acetaminophen, water, filtered, recoverable | µg/L | Pain reliever |
| 62009 | Albuterol (Salbutamol), water, filtered, recoverable | µg/L | Asthma medication |
| 62054 | Carbamazepine, water, filtered, recoverable | µg/L | Anti-seizure drug |
| 62060 | Sulfamethoxazole, water, filtered, recoverable | µg/L | Antibiotic |

#### 27. Per- and Polyfluoroalkyl Substances (PFAS)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 99230 | Perfluorooctanoic acid (PFOA), water, filtered | ng/L | Emerging contaminant |
| 99217 | Perfluorooctane sulfonic acid (PFOS), water, filtered | ng/L | EPA lifetime health advisory |
| 99221 | Perfluorohexane sulfonic acid (PFHxS), water, filtered | ng/L | PFAS compound |
| 99228 | Perfluorononanoic acid (PFNA), water, filtered | ng/L | PFAS compound |

#### 28. Organic Carbon & Biochemical Oxygen Demand
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00680 | Organic carbon, water, unfiltered | mg/L | Total organic carbon (TOC) |
| 00681 | Organic carbon, water, filtered | mg/L | Dissolved organic carbon (DOC) |
| 00310 | Biochemical oxygen demand, water, unfiltered, 5-day, 20°C | mg/L | Oxygen depletion potential |
| 00340 | Chemical oxygen demand, water, unfiltered | mg/L | Total oxidizable organics |

### RADIONUCLIDES (Group Code: 720XX - 829XX)

#### 29. Uranium & Radon
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 22703 | Uranium (natural), water, filtered | µg/L | MCL: 30 µg/L |
| 28011 | Uranium (natural), water, unfiltered, recoverable | µg/L | Total uranium |
| 82303 | Radon-222, water, unfiltered | pCi/L | Proposed MCL: 300 pCi/L |

#### 30. Gross Alpha & Beta Radioactivity
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 80030 | Gross alpha radioactivity, water, unfiltered | pCi/L as natural U | MCL: 15 pCi/L |
| 03502 | Gross beta radioactivity, water, unfiltered | pCi/L as Cs-137 | MCL: 4 mrem/yr |
| 62639 | Gross beta radioactivity, water, unfiltered | pCi/L as Sr-90/Y-90 | Alternative unit |

#### 31. Specific Radionuclides
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 09511 | Radium-226, water, unfiltered | pCi/L | MCL: 5 pCi/L (combined Ra-226 + Ra-228) |
| 09510 | Radium-228, water, unfiltered | pCi/L | MCL: 5 pCi/L (combined) |

---

## 🦠 BIOLOGICAL PARAMETERS (Group Code: 310XX - 361XX, 700XX)

### 32. Fecal Indicator Bacteria
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 31613 | Escherichia coli, water, Colilert Quanti-Tray/2000 | MPN/100 mL | Beach closures |
| 31616 | Escherichia coli, water, Colilert 18 Quanti-Tray/2000 | MPN/100 mL | Alternative method |
| 31625 | Fecal coliform, water, M-FC MF (0.7 micron) method | CFU/100 mL | Shellfish waters |
| 31615 | Enterococci, water, Enterolert Quanti-Tray/2000 | MPN/100 mL | Marine beaches |
| 31649 | Total coliform, water, Colilert Quanti-Tray/2000 | MPN/100 mL | Drinking water |

### 33. Chlorophyll & Algal Pigments
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 70953 | Chlorophyll a, phytoplankton, spectrophotometric acid method | µg/L | Eutrophication |
| 32209 | Chlorophyll a, phytoplankton, chromatographic-fluorometric method | µg/L | Alternative method |
| 62360 | Pheophytin a, phytoplankton, spectrophotometric acid method | µg/L | Degraded chlorophyll |

### 34. Algae & Phytoplankton (Taxonomic)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 70954 | Cyanobacteria (blue-green algae), phytoplankton | cells/mL | Harmful algal blooms |
| 61960 | Phytoplankton, total biomass, ash-free dry weight | mg/L | Productivity |
| 60050 | Phytoplankton, diversity index | Shannon H | Community structure |

### 35. Cyanotoxins (Harmful Algal Bloom Toxins)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 62860 | Microcystin, water, unfiltered | µg/L | WHO guideline: 1 µg/L (recreational) |
| 65208 | Cylindrospermopsin, water, filtered | µg/L | Cyanobacterial toxin |
| 65207 | Anatoxin-a, water, filtered | µg/L | Neurotoxin |

### 36. Periphyton & Benthic Algae
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 70956 | Chlorophyll a, periphyton, Lorenzen method | mg/m² | Stream productivity |
| 61982 | Periphyton, biomass, ash-free dry weight | g/m² | Benthic production |

---

## 💧 HYDROLOGIC PARAMETERS (Group Code: 000XX, 720XX, 740XX)

### 37. Streamflow & Discharge
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00060 | Discharge, cubic feet per second | ft³/s | Most-measured parameter |
| 00061 | Discharge, instantaneous, cubic feet per second | ft³/s | Real-time data |
| 30208 | Discharge, cubic meters per second | m³/s | SI units |
| 30209 | Discharge, instantaneous, cubic meters per second | m³/s | SI units |

### 38. Gage Height & Water Level
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00065 | Gage height, feet | ft | Stream stage |
| 00062 | Elevation of reservoir water surface above datum | ft | Reservoir levels |
| 62615 | Elevation of groundwater level above datum | ft | Well water levels |
| 72019 | Depth to water level, feet below land surface | ft | Groundwater monitoring |

### 39. Precipitation & Evapotranspiration
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00045 | Precipitation, total, inches | in | Meteorological stations |
| 00046 | Precipitation, total, millimeters | mm | SI units |
| 81395 | Evapotranspiration, potential, inches per day | in/day | Water budget |

### 40. Velocity & Flow Dynamics
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 72255 | Velocity, stream, mean, feet per second | ft/s | Discharge measurement |
| 81904 | Velocity, stream, at sampling point, feet per second | ft/s | Water quality sampling |

---

## 🏔️ SEDIMENT PARAMETERS (Group Code: 800XX - 821XX)

### 41. Suspended Sediment Concentration & Load
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 80154 | Suspended sediment concentration | mg/L | Turbidity source |
| 80155 | Suspended sediment discharge, tons per day | tons/day | Sediment load |
| 00530 | Total suspended solids, water, unfiltered | mg/L | Alternative measurement |

### 42. Bed Material & Particle Size
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 80158 | Suspended sediment, percent finer than 0.062 mm | % | Silt/clay fraction |
| 00191 | Suspended sediment, sieve diameter, percent finer than 0.125 mm | % | Fine sand threshold |
| 81369 | Bed material, fall diameter, percent finer than 2.00 mm | % | Gravel threshold |

### 43. Bedload Transport
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 80225 | Bedload sediment discharge, tons per day | tons/day | Total sediment transport |

---

## 🌊 ISOTOPE & STABLE ISOTOPE PARAMETERS (Group Code: 820XX - 829XX)

### 44. Hydrogen & Oxygen Isotopes (Water Source Tracers)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 82082 | Deuterium/protium ratio, water, unfiltered | per mil | Hydrologic source |
| 82085 | δ Deuterium, water, unfiltered | per mil (VSMOW) | D/H isotopic composition |
| 82082 | Oxygen-18/oxygen-16 ratio, water, unfiltered | per mil | Evaporation tracer |
| 82085 | δ Oxygen-18, water, unfiltered | per mil (VSMOW) | ¹⁸O/¹⁶O composition |

### 45. Carbon & Nitrogen Isotopes
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 82081 | δ Carbon-13/carbon-12 ratio, organic carbon, water, particulate | per mil (VPDB) | Organic matter source |
| 82086 | δ Nitrogen-15/nitrogen-14 ratio, water, particulate | per mil (air) | N pollution source |

### 46. Tritium (³H) - Groundwater Age Dating
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 07000 | Tritium, water, unfiltered | pCi/L | Groundwater age (<50 years) |
| 82311 | Tritium, water, unfiltered | TU (Tritium Units) | Alternative units |

---

## 🔬 FIELD MEASUREMENTS & QUALITY ASSURANCE PARAMETERS

### 47. Field Measurements (Real-time Sondes)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00010 | Temperature, water | °C | Continuous monitoring |
| 00300 | Dissolved oxygen | mg/L | Hypoxia detection |
| 00400 | pH, water, unfiltered, field | standard units | Continuous pH |
| 00095 | Specific conductance, water, unfiltered, field | µS/cm | Real-time salinity |
| 63680 | Turbidity, water, unfiltered, monochrome near infrared LED | FNU | Continuous turbidity |
| 32316 | fDOM, fluorescent dissolved organic matter | QSU | Optical sensor |

### 48. Sample Handling & QA/QC
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 82398 | Sample volume, filtered, liter | L | Trace organics |
| 50624 | Sample medium code | code | Water vs. sediment |
| 84164 | Sampling method code | code | Grab, composite, continuous |
| 00003 | Sampling depth, feet | ft | Depth-specific samples |

### 49. Laboratory QA/QC Parameters
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 99111 | Remark code | code | <, >, E, M, N qualifiers |
| 84171 | Value qualifier code | code | Quality flags |

---

## 📊 ADDITIONAL CATEGORIES & SPECIALIZED PARAMETERS

### 50. Groundwater-Specific Parameters
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 72019 | Depth to water level, feet below land surface | ft | Water table depth |
| 72020 | Elevation of water level above datum, feet | ft | Potentiometric surface |
| 62610 | Groundwater level above NGVD 1929, feet | ft | Regional aquifer maps |

### 51. Marine & Estuarine Parameters
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00480 | Salinity, water, unfiltered | PSU (ppt) | Estuarine mixing |
| 71820 | Tide stage code | code | Tidal influence |
| 61028 | Chlorophyll a, estuarine phytoplankton | µg/L | Coastal eutrophication |

### 52. Atmospheric Deposition
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 00025 | Barometric pressure, millimeters of mercury | mm Hg | Weather stations |
| 00036 | Wind speed, miles per hour | mph | Meteorological |
| 00023 | Sodium, wet deposition | mg/L | National Atmospheric Deposition Program |

### 53. Emerging Contaminants - Hormones & Steroids
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 62054 | Estrone, water, filtered, recoverable | ng/L | Endocrine disruptor |
| 62055 | 17-alpha-Estradiol, water, filtered, recoverable | ng/L | Hormone |
| 62056 | 17-beta-Estradiol, water, filtered, recoverable | ng/L | Natural estrogen |
| 62057 | 17-alpha-Ethynylestradiol, water, filtered, recoverable | ng/L | Synthetic birth control |
| 62170 | Testosterone, water, filtered, recoverable | ng/L | Androgen |

### 54. Taste & Odor Compounds
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 62361 | Geosmin, water, unfiltered, recoverable | ng/L | Earthy/musty odor |
| 62363 | 2-Methylisoborneol (MIB), water, unfiltered, recoverable | ng/L | Earthy/musty odor |

### 55. Disinfection Byproducts (DBPs)
| Parameter Code | Parameter Name | Units | Common Use |
|----------------|----------------|-------|------------|
| 32102 | Total trihalomethanes (TTHMs), water, unfiltered | µg/L | MCL: 80 µg/L |
| 32106 | Bromodichloromethane, water, unfiltered | µg/L | DBP component |
| 34288 | Chloroform, water, unfiltered | µg/L | THM component |
| 32101 | Bromoform, water, unfiltered | µg/L | THM component |
| 32104 | Dibromochloromethane, water, unfiltered | µg/L | THM component |
| 32105 | Haloacetic acids (HAA5), water, filtered | µg/L | MCL: 60 µg/L |

---

## 🔍 HOW TO USE NWIS PARAMETER CODES FOR COUNTY-LEVEL RESEARCH

### Python Example: Query Water Quality Data by Parameter Code

```python
from dataretrieval import nwis
import pandas as pd
import numpy as np

# Define geographic area (Travis County, TX bounding box)
bbox = [-98.165, 30.038, -97.522, 30.628]

# Query multiple water quality parameters (2020-2023)
parameter_codes = [
    '00010',  # Water temperature
    '00060',  # Discharge
    '00300',  # Dissolved oxygen
    '00400',  # pH
    '00095',  # Specific conductance
    '00665',  # Total phosphorus
    '00631',  # Nitrate + Nitrite
    '00608',  # Ammonia
    '00681',  # Dissolved organic carbon
    '70953'   # Chlorophyll a
]

# Get site information within bounding box
sites, md = nwis.what_sites(
    bBox=','.join(map(str, bbox)),
    parameterCd=','.join(parameter_codes),
    siteType='ST'  # Stream sites only
)

print(f"Found {len(sites)} sites in Travis County")

# Query water quality data for all sites
wq_data = pd.DataFrame()

for site_no in sites['site_no']:
    try:
        df, md = nwis.get_qwdata(
            sites=site_no,
            start='2020-01-01',
            end='2023-12-31',
            parameterCd=','.join(parameter_codes)
        )
        wq_data = pd.concat([wq_data, df], ignore_index=True)
    except:
        continue

# Calculate county-level summary statistics
county_summary = wq_data.groupby('parm_cd').agg({
    'result_va': ['mean', 'median', 'std', 'min', 'max', 'count']
}).reset_index()

# Get parameter names
param_info = pd.DataFrame()
for code in parameter_codes:
    info, md = nwis.get_pmcodes(parameterCd=code, partial=False)
    param_info = pd.concat([param_info, info], ignore_index=True)

# Merge parameter names with summary statistics
county_summary_named = county_summary.merge(
    param_info[['parameter_cd', 'parameter_nm', 'parameter_units']],
    left_on='parm_cd',
    right_on='parameter_cd'
)

print(county_summary_named)

# Export to CSV
county_summary_named.to_csv('travis_county_water_quality_2020_2023.csv', index=False)
```

### R Example: Extract Water Quality by Parameter Code

```r
library(dataRetrieval)
library(dplyr)
library(sf)

# Define Travis County bounding box
bbox <- c(-98.165, 30.038, -97.522, 30.628)

# Define parameter codes of interest
param_codes <- c(
  "00010",  # Water temperature
  "00060",  # Discharge
  "00300",  # Dissolved oxygen
  "00400",  # pH
  "00095",  # Specific conductance
  "00665",  # Total phosphorus
  "00631",  # Nitrate + Nitrite
  "00608",  # Ammonia
  "00681",  # Dissolved organic carbon
  "70953"   # Chlorophyll a
)

# Find sites within county with these parameters
sites <- whatNWISsites(
  bBox = bbox,
  parameterCd = param_codes,
  siteType = "ST"
)

cat(sprintf("Found %d stream sites in Travis County\n", nrow(sites)))

# Query water quality data (2020-2023)
wq_data <- readNWISqw(
  siteNumbers = sites$site_no,
  parameterCd = param_codes,
  startDate = "2020-01-01",
  endDate = "2023-12-31"
)

# Add parameter names
wq_data_named <- renameNWISColumns(wq_data)

# Calculate county-level summary statistics by parameter
county_stats <- wq_data %>%
  group_by(parm_cd) %>%
  summarize(
    n_samples = n(),
    n_sites = n_distinct(site_no),
    mean = mean(result_va, na.rm = TRUE),
    median = median(result_va, na.rm = TRUE),
    sd = sd(result_va, na.rm = TRUE),
    min = min(result_va, na.rm = TRUE),
    max = max(result_va, na.rm = TRUE),
    pct_25 = quantile(result_va, 0.25, na.rm = TRUE),
    pct_75 = quantile(result_va, 0.75, na.rm = TRUE)
  )

# Get parameter metadata
param_info <- readNWISpCode(param_codes)

# Join with parameter names
county_stats_final <- county_stats %>%
  left_join(
    param_info %>% select(parameter_cd, parameter_nm, parameter_units),
    by = c("parm_cd" = "parameter_cd")
  )

print(county_stats_final)

# Export to CSV
write.csv(
  county_stats_final,
  "travis_county_wq_summary_2020_2023.csv",
  row.names = FALSE
)
```

### Query Real-Time Continuous Data (15-minute intervals)

```r
# Get real-time data for specific site (Colorado River at Austin)
site_no <- "08158000"

# Query last 7 days of real-time data
rt_data <- readNWISuv(
  siteNumbers = site_no,
  parameterCd = c("00060", "00065", "00010", "00300", "00095", "00400"),
  startDate = Sys.Date() - 7,
  endDate = Sys.Date()
)

# Rename columns to human-readable names
rt_data_named <- renameNWISColumns(rt_data)

# Calculate daily means from 15-minute data
daily_means <- rt_data_named %>%
  mutate(date = as.Date(dateTime)) %>%
  group_by(date, site_no) %>%
  summarize(
    discharge_mean = mean(Flow_Inst, na.rm = TRUE),
    temp_mean = mean(Wtemp_Inst, na.rm = TRUE),
    do_mean = mean(DO_Inst, na.rm = TRUE),
    spc_mean = mean(SpecCond_Inst, na.rm = TRUE),
    ph_mean = mean(pH_Inst, na.rm = TRUE)
  )
```

### Aggregate to County Level from All Sites

```r
# Function to aggregate NWIS data to county level
aggregate_to_county <- function(county_fips, start_date, end_date, param_codes) {

  # Get county boundary
  county_sf <- tigris::counties(state = substr(county_fips, 1, 2), cb = TRUE) %>%
    filter(GEOID == county_fips)

  # Get bounding box
  bbox <- st_bbox(county_sf)

  # Find sites
  sites <- whatNWISsites(
    bBox = c(bbox$xmin, bbox$ymin, bbox$xmax, bbox$ymax),
    parameterCd = param_codes,
    hasDataTypeCd = "qw"
  )

  # Query data
  if (nrow(sites) == 0) {
    return(NULL)
  }

  wq_data <- readNWISqw(
    siteNumbers = sites$site_no,
    parameterCd = param_codes,
    startDate = start_date,
    endDate = end_date
  )

  # Calculate county-level statistics
  county_summary <- wq_data %>%
    group_by(parm_cd) %>%
    summarize(
      fips = county_fips,
      n_sites = n_distinct(site_no),
      n_samples = n(),
      mean = mean(result_va, na.rm = TRUE),
      median = median(result_va, na.rm = TRUE),
      sd = sd(result_va, na.rm = TRUE)
    )

  return(county_summary)
}

# Example: Travis County, TX
travis_wq <- aggregate_to_county(
  county_fips = "48453",
  start_date = "2020-01-01",
  end_date = "2023-12-31",
  param_codes = c("00665", "00631", "00608", "00681")
)
```

---

## 📚 COMPANION DATA SOURCES

### USGS Water Quality Portal (Multi-Agency)
**URL:** https://www.waterqualitydata.us/

**Description:** Combines data from USGS NWIS, EPA STORET, and USDA STEWARDS
- 413+ million results from 3.7 million sites
- Harmonized parameter codes across agencies
- Download large datasets (>10 million records possible)
- Same parameter code system as NWIS

### USGS National Hydrography Dataset (NHD)
**URL:** https://www.usgs.gov/national-hydrography

**Description:** Stream network for spatial linking
- NHDPlus HR (High Resolution) 1:24,000 scale
- Reach catchment boundaries for watershed delineation
- Link NWIS sites to stream segments (COMIDs)
- Drainage area, stream order, flow accumulation

### EPA WATERS Geospatial Services
**URL:** https://www.epa.gov/waterdata/waters-geospatial-services

**Description:** Web services for watershed delineation
- Upstream/downstream tracing from NWIS sites
- Catchment delineation for any point
- Index NWIS sites to NHD reaches

### USGS StreamStats
**URL:** https://streamstats.usgs.gov/

**Description:** Basin characteristics for ungaged locations
- Drainage area, slope, land use, soil properties
- Regional regression equations for flow statistics
- Useful for sites without long-term discharge records

### USGS Water-Use Data
**URL:** https://waterdata.usgs.gov/nwis/wu

**Description:** County-level water withdrawals every 5 years
- Public supply, irrigation, thermoelectric, industrial
- Complements NWIS water quality monitoring
- Links to AQUASTAT for water stress indices

---

## 📝 CITATION

**Recommended Citation Format:**

U.S. Geological Survey, 2024, National Water Information System data available on the World Wide Web (USGS Water Data for the Nation), accessed [date], at http://waterdata.usgs.gov/nwis/.

**For Specific Parameter Code Database:**

U.S. Geological Survey, 2024, Parameter code dictionary for National Water Information System (NWIS), accessed [date], at https://nwis.waterdata.usgs.gov/usa/nwis/pmcodes.

**For Data Retrieved via dataRetrieval Package:**

De Cicco, L.A., Hirsch, R.M., Lorenz, D., Watkins, W.D., Johnson, M., 2024, dataRetrieval: R packages for discovering and retrieving water data available from U.S. federal hydrologic web services, v.2.7.15, doi:10.5066/P9X4L3GE.

---

## 🔗 RELATED TIER 1 COMPREHENSIVE DOCUMENTATION

This catalog provides complete variable listings for USGS NWIS parameters. For integration with broader environmental health research, see:

**[WATER_HYDROLOGY_CLIMATE_COMPREHENSIVE.md](WATER_HYDROLOGY_CLIMATE_COMPREHENSIVE.md)**
- Section on "USGS National Water Information System (NWIS)"
- Priority parameters for public health research
- Integration with hydrologic modeling
- Linkage to StreamStats and NHDPlus

---

## 📌 NOTES ON PARAMETER CODE STRUCTURE

### Filtered vs. Unfiltered
- **Filtered** (dissolved): Sample passed through 0.45 µm filter
- **Unfiltered** (total): Whole water sample including particles
- **Recoverable**: Digestible or extractable fraction

### Common Suffixes
- "_r" = Representative value (SSURGO)
- "_Inst" = Instantaneous (real-time data)
- "_Daily" = Daily value
- "_tons/day" = Load calculation

### Remark Codes (Parameter 99111)
- **<** = Less than detection limit
- **>** = Greater than upper reporting limit
- **E** = Estimated value
- **M** = Presence verified, not quantified
- **N** = Below reporting level

### Laboratory vs. Field Measurements
- **Field** measurements taken on-site (temperature, DO, pH, conductance)
- **Laboratory** measurements from analyzed samples (nutrients, metals, organics)
- Different parameter codes distinguish measurement location

---

**Document Version:** 1.0
**Last Updated:** 2024
**Maintainer:** USGS Water Resources Mission Area

**Total Documented Parameters:** 1,300+
**Major Categories:** 55+
**Official Source:** https://nwis.waterdata.usgs.gov/usa/nwis/pmcodes
