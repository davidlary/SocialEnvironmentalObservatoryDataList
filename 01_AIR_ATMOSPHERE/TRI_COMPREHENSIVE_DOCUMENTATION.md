# EPA Toxic Release Inventory (TRI) - Comprehensive Documentation
## Complete Chemical List, Variables, and Data Access Guide

**Last Updated:** November 2025
**Data Coverage:** 1987-2024 (Reporting Year 2024 data due July 1, 2025)
**Current Chemical Count:** 799 individual chemicals + 33 chemical categories = 832 total entries

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Complete TRI Chemical List (799 Chemicals)](#complete-tri-chemical-list)
3. [Chemical Categories (33 Categories)](#chemical-categories-33)
4. [Facility-Level Variables](#facility-level-variables)
5. [Release and Waste Management Variables](#release-and-waste-management-variables)
6. [Data Access Methods](#data-access-methods)
7. [Reporting Requirements and Thresholds](#reporting-requirements-and-thresholds)
8. [County-Level Aggregation Methods](#county-level-aggregation-methods)
9. [Data Quality Considerations](#data-quality-considerations)
10. [Code Examples (R, API)](#code-examples)

---

## Executive Summary

The EPA Toxic Release Inventory (TRI) is the most comprehensive public database of industrial toxic chemical releases and waste management activities in the United States. Established under Section 313 of the Emergency Planning and Community Right-to-Know Act (EPCRA) in 1986, TRI provides annual data from facilities across manufacturing and certain other sectors.

### Key Facts:
- **799 individually listed chemicals** + **33 chemical categories**
- **Historical data:** 1987-present (37+ years)
- **Geographic coverage:** All U.S. states, territories, and tribal lands
- **Facility coverage:** 20,000+ facilities annually
- **Data elements:** 100+ variables per facility-chemical combination
- **Release pathways:** Air, water, land, underground injection, off-site transfers
- **Public access:** Free via multiple platforms (API, bulk downloads, web tools)

---

## Complete TRI Chemical List

### Current Status (2024-2025)
- **799 individual chemicals** listed
- **33 chemical categories** (e.g., "Lead compounds", "Mercury compounds")
- **Administrative stays:** 2 chemicals currently not reportable:
  - Methyl mercaptan
  - 2,2-dibromo-3-nitrilopropionamide

### Chemical Organization

The TRI chemical list is organized by:
1. **Individual chemicals** (with CAS numbers)
2. **Chemical compound categories** (with category codes like N010, N020, etc.)
3. **Special designations:**
   - PBT (Persistent Bioaccumulative Toxic) chemicals - 16 chemicals + 4 categories
   - PFAS (Per- and polyfluoroalkyl substances) - 205 chemicals (as of RY 2025)
   - OSHA carcinogens
   - Chemicals of special concern

### 📋 COMPLETE CHEMICAL CATALOG (TIER 2)

**For the complete alphabetized searchable catalog of all 799 TRI chemicals with CAS numbers, chemical formulas, year added, and reporting thresholds, see:**

**[EPA_TRI_COMPLETE_CHEMICAL_LIST.md](EPA_TRI_COMPLETE_CHEMICAL_LIST.md)**

This companion Tier 2 catalog provides:
- All 799 individual chemicals in alphabetical order
- CAS numbers and chemical formulas for each entry
- Year added to TRI reporting requirements
- PBT and PFAS designations
- Reporting thresholds (standard 25,000 lbs vs. lower 100 lbs for PBTs)
- Special administrative statuses
- Quick reference tables organized by chemical class

**Use this document (Tier 1)** for overview of TRI system, variables, data access, and priority chemicals.
**Use EPA_TRI_COMPLETE_CHEMICAL_LIST.md (Tier 2)** to look up specific chemicals or browse the complete list.

---

## 1. METAL AND METAL COMPOUND CATEGORIES (17 Categories)

### Complete Metal Categories with Codes:

| Code | Category Name | CAS Number Range | Year Added | Notes |
|------|---------------|------------------|------------|-------|
| **N010** | Antimony compounds | Various | 1987 | Includes all antimony compounds |
| **N020** | Arsenic compounds | Various | 1987 | Inorganic and organic arsenic compounds |
| **N040** | Barium compounds | Various | 1987 | Excludes barium sulfate |
| **N050** | Beryllium compounds | Various | 1987 | All beryllium compounds |
| **N078** | Cadmium compounds | Various | 1987 | PBT chemical category |
| **N090** | Chromium compounds | Various | 1987 | Excludes chromite ore from Transvaal Region |
| **N096** | Cobalt compounds | Various | 1987 | All cobalt compounds |
| **N100** | Copper compounds | Various | 1987 | Some pigments delisted 1989 |
| **N420** | Lead compounds | Various | 1987 | PBT chemical category; lower threshold |
| **N450** | Manganese compounds | Various | 1987 | All manganese compounds |
| **N458** | Mercury compounds | Various | 1987 | PBT chemical category; lower threshold |
| **N495** | Nickel compounds | Various | 1987 | All nickel compounds |
| **N725** | Selenium compounds | Various | 1987 | All selenium compounds |
| **N740** | Silver compounds | Various | 1987 | All silver compounds |
| **N760** | Thallium compounds | Various | 1987 | All thallium compounds |
| **N770** | Vanadium compounds | Various | 1987 | All vanadium compounds |
| **N982** | Zinc compounds | Various | 1987 | All zinc compounds |

### Individual Metals Listed (60 total metals and metal compounds):
- Aluminum (CAS 7429-90-5)
- Antimony (CAS 7440-36-0)
- Arsenic (CAS 7440-38-2)
- Barium (CAS 7440-39-3)
- Beryllium (CAS 7440-41-7)
- Cadmium (CAS 7440-43-9)
- Chromium (CAS 7440-47-3)
- Cobalt (CAS 7440-48-4)
- Copper (CAS 7440-50-8)
- Lead (CAS 7439-92-1)
- Lithium carbonate (CAS 554-13-2)
- Manganese (CAS 7439-96-5)
- Mercury (CAS 7439-97-6)
- Molybdenum trioxide (CAS 1313-27-5)
- Nickel (CAS 7440-02-0)
- Osmium tetroxide (CAS 20816-12-0)
- Selenium (CAS 7782-49-2)
- Silver (CAS 7440-22-4)
- Thallium (CAS 7440-28-0)
- Thorium dioxide (CAS 1314-20-1)
- Titanium tetrachloride (CAS 7550-45-0)
- Vanadium (CAS 7440-62-2)
- Zinc (CAS 7440-66-6)
- Plus various tin compounds, metal salts, and fungicides (ferbam, maneb, metiram, zineb)

---

## 2. POLYCYCLIC AROMATIC COMPOUNDS (PACs) - Category N590

**Category Code:** N590
**Number of Compounds:** 25 individual PACs
**Classification:** PBT (Persistent Bioaccumulative Toxic)
**Reporting Threshold:** 100 pounds (lower than standard threshold)

### Complete List of 25 PACs:

| CAS Number | Chemical Name | Year Added |
|------------|---------------|------------|
| 56-55-3 | Benz[a]anthracene | 2000 |
| 205-99-2 | Benzo[b]fluoranthene | 2000 |
| 205-82-3 | Benzo[j]fluoranthene | 2000 |
| 207-08-9 | Benzo[k]fluoranthene | 2000 |
| 206-44-0 | Benzo[j,k]fluorene (Fluoranthene) | 2000 |
| 189-55-9 | Benzo[r,s,t]pentaphene (Dibenzo[a,i]pyrene) | 2000 |
| 218-01-9 | Benzo[a]phenanthrene (Chrysene) | 2000 |
| 50-32-8 | Benzo[a]pyrene | 2000 |
| 226-36-8 | Dibenz[a,h]acridine | 2000 |
| 224-42-0 | Dibenz[a,j]acridine | 2000 |
| 53-70-3 | Dibenzo[a,h]anthracene | 2000 |
| 194-59-2 | 7H-Dibenzo[c,g]carbazole | 2000 |
| 5385-75-1 | Dibenzo[a,e]fluoranthene | 2000 |
| 192-65-4 | Dibenzo[a,e]pyrene | 2000 |
| 189-64-0 | Dibenzo[a,h]pyrene | 2000 |
| 191-30-0 | Dibenzo[a,l]pyrene | 2000 |
| 57-97-6 | 7,12-Dimethylbenz[a]anthracene | 2000 |
| 42397-64-8 | 1,6-Dinitropyrene | 2000 |
| 42397-65-9 | 1,8-Dinitropyrene | 2000 |
| 193-39-5 | Indeno[1,2,3-cd]pyrene | 2000 |
| 56-49-5 | 3-Methylcholanthrene | 2000 |
| 3697-24-3 | 5-Methylchrysene | 2000 |
| 7496-02-8 | 6-Nitrochrysene | 2000 |
| 5522-43-0 | 1-Nitropyrene | 2000 |
| 57835-92-4 | 4-Nitropyrene | 2000 |

---

## 3. DIOXIN AND DIOXIN-LIKE COMPOUNDS - Category N150

**Category Code:** N150
**Number of Compounds:** 17 individual dioxin and dioxin-like compounds
**Classification:** PBT (Persistent Bioaccumulative Toxic)
**Reporting Unit:** GRAMS (all other TRI chemicals reported in pounds)
**Reporting Threshold:** 0.1 grams (extremely low due to high toxicity)
**Toxic Equivalency (TEQ):** EPA calculates TEQ using WHO Toxic Equivalency Factors (TEFs)

### Key Dioxin Compounds:
- 2,3,7,8-Tetrachlorodibenzo-p-dioxin (TCDD) - most toxic
- Polychlorinated dibenzo-p-dioxins (PCDDs)
- Polychlorinated dibenzofurans (PCDFs)
- Certain dioxin-like polychlorinated biphenyls

### TEQ Calculation:
TEQ = Σ(mass of each congener × TEF for that congener)

Example: 10 grams of compound × 0.1 TEF = 1 gram TEQ

EPA provides separate TEQ data files with calculated toxic equivalency values for analysis and comparison.

---

## 4. PFAS CHEMICALS (205 Total for RY 2025)

**Classification:** Chemicals of Special Concern (designated 2023)
**Reporting Threshold:** 100 pounds (lower than standard 25,000/10,000 thresholds)
**Special Rules:**
- NO de minimis exemption (must report regardless of concentration in mixtures)
- NO Form A certification option (must use full Form R)
- Range reporting limitations

### PFAS Added Under 2020 NDAA:
- Initial addition: 172 PFAS (RY 2021)
- Total for RY 2024: 196 PFAS
- Total for RY 2025: 205 PFAS (9 additional added)

### Nine PFAS Added for RY 2025 (reports due July 1, 2026):

| CAS Number | Chemical Name |
|------------|---------------|
| 3108-42-7 | Ammonium perfluorodecanoate (PFDA NH4) |
| 3830-45-3 | Sodium perfluorodecanoate (PFDA-Na) |
| 377-73-1 | Perfluoro-3-methoxypropanoic acid |
| 27619-97-2 | 6:2 Fluorotelomer sulfonate acid |
| 425670-75-3 | 6:2 Fluorotelomer sulfonate anion |
| 59587-38-1 | 6:2 Fluorotelomer sulfonate potassium salt |
| 59587-39-2 | 6:2 Fluorotelomer sulfonate ammonium salt |
| 27619-94-9 | 6:2 Fluorotelomer sulfonate sodium salt |
| 3030471-22-5 | Acetic acid, [(γ-ω-perfluoro-C8-10-alkyl)thio] derivs., Bu esters |

### Seven PFAS Added for RY 2024 (reports due July 1, 2025):

| CAS Number | Chemical Name |
|------------|---------------|
| 307-24-4 | Perfluorohexanoic acid (PFHxA) |
| 422-64-0 | Perfluoropropanoic acid |
| 2923-26-4 | Sodium perfluorohexanoate |
| 21615-47-4 | Ammonium perfluorohexanoate |
| 82113-65-3 | 1,1,1-Trifluoro-N-[(trifluoromethyl)sulfonyl] methanesulfonamide |
| Additional 2 PFAS | (See EPA official list) |

### Key PFAS Already on TRI List (from initial 172):
- Perfluorooctanoic acid (PFOA) - CAS 335-67-1
- Perfluorooctanesulfonic acid (PFOS) - CAS 1763-23-1
- Ammonium perfluorooctanoate - CAS 3825-26-1
- Perfluorodecanoic acid - CAS 335-76-2
- Various fluorotelomer acrylates, sulfonates, alcohols, phosphates, and polymers

**Access:** Complete list of 205 PFAS available at:
- EPA TRI Explorer: https://enviro.epa.gov/triexplorer/tri_text.list_chemical_pfas
- EPA PFAS TRI List PDF: https://www.epa.gov/system/files/documents/2024-01/list-of-pfas-added-to-the-tri-by-the-ndaa.pdf

---

## 5. VOLATILE ORGANIC COMPOUNDS (VOCs)

### Common VOCs on TRI List:

**BTEX Compounds:**
- **Benzene** - CAS 71-43-2 (carcinogen)
- **Toluene** - CAS 108-88-3
- **Ethylbenzene** - CAS 100-41-4
- **Xylene (mixed isomers)** - CAS 1330-20-7
  - o-Xylene - CAS 95-47-6
  - m-Xylene - CAS 108-38-3
  - p-Xylene - CAS 106-42-3

**Other Major VOCs:**
- Styrene - CAS 100-42-5 (OSHA carcinogen)
- Acetaldehyde - CAS 75-07-0 (OSHA carcinogen)
- Formaldehyde - CAS 50-00-0 (OSHA carcinogen, highest air releases)
- Methyl ethyl ketone - CAS 78-93-3
- Methyl isobutyl ketone - CAS 108-10-1
- Acetone - CAS 67-64-1
- Cyclohexane - CAS 110-82-7
- n-Hexane - CAS 110-54-3

---

## 6. CHLORINATED SOLVENTS

### Complete Chlorinated Solvent List:

**Chlorinated Methanes:**
- **Carbon tetrachloride** - CAS 56-23-5 (one of EPA's first 7 for risk evaluation)
- **Methylene chloride** (Dichloromethane) - CAS 75-09-2 (risk evaluation completed)
- Chloroform - CAS 67-66-3
- Methyl chloride - CAS 74-87-3

**Chlorinated Ethanes:**
- **1,1,1-Trichloroethane** (TCA) - CAS 71-55-6
- 1,1,2-Trichloroethane - CAS 79-00-5
- 1,2-Dichloroethane - CAS 107-06-2
- Hexachloroethane - CAS 67-72-1

**Chlorinated Ethenes:**
- **Trichloroethylene** (TCE) - CAS 79-01-6 (major groundwater contaminant, risk evaluation)
- **Tetrachloroethylene** (Perchloroethylene, PCE, PERC) - CAS 127-18-4 (dry cleaning solvent)
- Vinyl chloride - CAS 75-01-4 (carcinogen)
- Vinylidene chloride - CAS 75-35-4

**Other Chlorinated Compounds:**
- 1,4-Dioxane - CAS 123-91-1 (risk evaluation)
- 1-Bromopropane - CAS 106-94-5 (risk evaluation)
- N-methylpyrrolidone - CAS 872-50-4 (risk evaluation)

**Use:** Metal degreasing, dry cleaning, chemical intermediates, paint strippers
**Environmental Concern:** Common groundwater contaminants at 80% of Superfund sites and 3,000+ DoD sites

---

## 7. PESTICIDES AND HERBICIDES

### Pesticides on TRI List:

**YES - On TRI List:**
- **Atrazine** - CAS 1912-24-9 (herbicide, de minimis 1.0%)
- **Paraquat dichloride** - CAS 1910-42-5 (herbicide, de minimis 1.0%)
- **Dicamba** - CAS 1918-00-9 (herbicide)
- **Picloram** - CAS 1918-02-1 (herbicide)
- **Propachlor** - CAS 1918-16-7 (herbicide)
- **Nitrapyrin** - CAS 1929-82-4 (nitrification inhibitor)
- **Methiocarb** - CAS 2032-65-7 (insecticide)
- **Captan** - CAS 133-06-2 (fungicide)
- **Chlorothalonil** - CAS 1897-45-6 (fungicide)
- Various organophosphate pesticides

**NO - NOT on TRI List:**
- **Glyphosate** - NOT required to be reported under EPCRA Section 313
- Most currently used agricultural pesticides (covered under separate FIFRA reporting)

**Note:** Agricultural chemical manufacturers must report if they meet TRI facility criteria, but farms and agricultural operations are generally NOT covered under TRI.

---

## 8. CARCINOGENS

### OSHA Carcinogens on TRI List:

**Top Air Releases (2023 data):**
1. **Styrene** - CAS 100-42-5 (highest quantity)
2. **Acetaldehyde** - CAS 75-07-0
3. **Formaldehyde** - CAS 50-00-0

**EPA Carcinogen Classifications:**
- **Group A:** Human carcinogen (sufficient human evidence)
- **Group B:** Probable human carcinogen (limited human or sufficient animal evidence)
- **Group C:** Possible human carcinogen (limited animal evidence, no human data)

**Known Human Carcinogens (partial list):**
- Benzene - CAS 71-43-2
- Vinyl chloride - CAS 75-01-4
- Arsenic compounds
- Cadmium compounds
- Chromium compounds (hexavalent)
- Nickel compounds
- Asbestos - CAS 1332-21-4
- 2,3,7,8-TCDD (dioxin)

**Trends:** OSHA carcinogen air releases decreased 10% (6.9 million pounds) from 2022-2023.

**Access:** EPA's "Basis of TRI OSHA Carcinogen Designation" document provides complete list with classification basis.

---

## Chemical Categories (33 Total)

### Complete List of 33 Chemical Categories:

| Code | Category Name | Notes |
|------|---------------|-------|
| **N010** | Antimony compounds | Metal compound category |
| **N020** | Arsenic compounds | Metal compound category, carcinogen |
| **N040** | Barium compounds | Excludes barium sulfate |
| **N050** | Beryllium compounds | Metal compound category |
| **N078** | Cadmium compounds | PBT chemical category |
| **N084** | Chlorophenols | Organic category |
| **N090** | Chromium compounds | Excludes chromite ore from Transvaal |
| **N096** | Cobalt compounds | Metal compound category |
| **N100** | Copper compounds | Some pigments delisted 1989 |
| **N106** | Cyanide compounds | Highly toxic category |
| **N120** | Diisocyanates | Organic category, respiratory hazard |
| **N150** | Dioxin and dioxin-like compounds | 17 congeners, PBT, reported in grams |
| **N171** | Ethylenebisdithiocarbamic acid, salts and esters (EBDCs) | Fungicide category |
| **N230** | Certain glycol ethers | Reproductive toxicants |
| **N270** | Hexabromocyclododecane | Flame retardant, added recently |
| **N420** | Lead compounds | PBT, lower threshold |
| **N450** | Manganese compounds | Metal compound category |
| **N458** | Mercury compounds | PBT, lower threshold |
| **N495** | Nickel compounds | Metal compound category |
| **N503** | Nicotine and salts | Pesticide category |
| **N511** | Nitrate compounds | Environmental concern |
| **N530** | Nonylphenol | Endocrine disruptor |
| **N535** | Nonylphenol ethoxylates | Surfactant category |
| **N575** | Polybrominated biphenyls (PBBs) | Flame retardant, banned |
| **N583** | Polychlorinated alkanes | Includes C10-C13 alkanes |
| **N590** | Polycyclic aromatic compounds | 25 PACs, PBT category |
| **N725** | Selenium compounds | Metal compound category |
| **N740** | Silver compounds | Metal compound category |
| **N746** | Strychnine and salts | Highly toxic pesticide |
| **N760** | Thallium compounds | Metal compound category |
| **N770** | Vanadium compounds | Metal compound category (MISSING FROM INITIAL 30) |
| **N982** | Zinc compounds | Metal compound category |
| **DINP** | Diisononyl phthalate | Added July 2023, phthalate category |

**Note:** Three categories may not be fully captured in searches; EPA official documents contain complete enumeration.

---

## Facility-Level Variables

### A. Facility Identification (TRI Basic Data File - 100+ fields)

**Geographic/Location:**
- TRI Facility ID (unique identifier)
- Facility name
- Street address
- City
- State abbreviation
- ZIP code (5-digit)
- ZIP code (4-digit extension)
- County name
- County FIPS code (critical for county-level aggregation)
- Latitude (decimal degrees)
- Longitude (decimal degrees)
- Horizontal coordinate reference system
- Federal facility indicator (Y/N)

**Corporate/Ownership:**
- Parent company name
- Parent company DUNS number
- Facility DUNS number

**Environmental IDs:**
- EPA Registry ID (unique facility identifier across EPA systems)
- NPDES permit ID (if applicable)
- RCRA ID (if applicable)
- Underground Injection Control (UIC) ID

**Industry Classification:**
- Primary NAICS code (6-digit, determines TRI coverage)
- Additional NAICS codes (facilities can have multiple)
- Industry sector description

---

### B. Chemical Identification

**Chemical Information:**
- Chemical name (as listed on TRI)
- CAS number (Chemical Abstracts Service registry number)
- TRI chemical ID
- Chemical category indicator
- Metal indicator (Y/N)
- Carcinogen indicator (Y/N)
- PBT indicator (Y/N)
- PFAS indicator (Y/N - added 2020+)
- Dioxin indicator (Y/N)
- Clean Air Act chemical indicator
- CERCLA/Superfund listed
- Classification (acute toxicity, chronic toxicity, etc.)

---

### C. Production and Activity Information

**Activity Basis:**
- Manufacture the chemical (Y/N)
- Process the chemical (Y/N)
- Otherwise use the chemical (Y/N)
- Produce the chemical (Y/N)
- Import the chemical (Y/N)

**Production Ratios (for dioxin reporting):**
- Production ratio or activity index
- Calculation method

---

## Release and Waste Management Variables

### Section 5 - On-Site Releases

**5.1 Air Emissions:**
- Fugitive air emissions (non-point sources) - pounds
- Stack/point source air emissions - pounds
- Total on-site air emissions - pounds

**5.2 Water Discharges:**
- Surface water discharges (to streams, rivers, lakes, oceans) - pounds
  - Receiving stream/water body name
  - NPDES permit number
- Underground injection Class I wells - pounds
- Underground injection Class II-V wells - pounds

**5.3 On-Site Land Disposal:**
- RCRA Subtitle C landfills - pounds
- Other on-site landfills - pounds
- Land treatment/application farming - pounds
- Surface impoundments - pounds
- Other land disposal - pounds

**5.4 Total On-Site Disposal or Other Releases:**
- Sum of all Section 5.1-5.3 quantities - pounds

**5.5 On-Site Release Basis of Estimate:**
- Code for each release type (M1, M2, C, E1, E2, O)

---

### Section 6 - Off-Site Transfers

**6.1 Transfers for Disposal:**
- To POTWs (Publicly Owned Treatment Works) - pounds
  - POTW name
  - POTW location
- To other off-site locations - pounds by disposal method:
  - Underground injection
  - Landfills
  - Land treatment
  - Surface impoundments
  - Other disposal
- Total transfers for disposal - pounds

**6.2 Transfers for Further Waste Management:**
- Transfers to recycling - pounds
  - Solvent/organic recovery
  - Metals recovery
  - Other reuse/recovery
- Transfers to energy recovery - pounds
  - Fuel blending
  - Energy recovery
- Transfers to treatment - pounds
  - Incineration
  - Stabilization
  - Other treatment
- Transfers as waste - pounds

**6.3 Off-Site Transfer Locations:**
- Receiving facility name
- Street address, city, state, ZIP
- EPA Registry ID (if available)
- RCRA ID (if applicable)

---

### Section 7 - On-Site Waste Treatment

**7A Treatment Efficiency:**
- Type of treatment (incineration, wastewater treatment, etc.)
- Treatment efficiency range (%)
- Treatment method code

**7B On-Site Energy Recovery:**
- Quantity used for energy recovery - pounds

**7C On-Site Recycling:**
- Quantity recycled on-site - pounds

---

### Section 8 - Source Reduction and Waste Management

**8.1-8.7 Quantity Comparisons (Reported for Current Year, Prior Year, and 2 Future Years):**

**8.1 Production-Related Waste:**
- Total quantity of chemical entering waste management system - pounds

**8.2 Methods of Waste Treatment:**
- Energy recovery on-site - pounds
- Energy recovery off-site - pounds
- Recycling on-site - pounds
- Recycling off-site - pounds
- Treatment on-site - pounds
- Treatment off-site - pounds

**8.3 Total Waste Management:**
- Sum of quantities from 8.2

**8.4 One-Time Releases:**
- Quantity and description of unusual events

**8.5 Production/Activity Index:**
- Production ratio (percentage of prior year)
- Activity index

**8.6 Non-Production Related Waste:**
- Catastrophic events
- Remediation activities
- Other one-time events

**8.7 Total Waste Management:**
- Sum of production + non-production waste

**8.8 Source Reduction Activities:**
- Good operating practices
- Inventory control
- Spill and leak prevention
- Raw material modifications
- Product modifications
- Process modifications
- Cleaning and degreasing
- Surface preparation and finishing
- On-site use/reuse

---

### Additional TRI Variables

**Reporting Information:**
- Reporting year
- Submission date
- Revision indicator
- Revision number
- Reason for revision
- Form type (Form R, Form A, or Form A certification)
- Submission method (electronic, paper)
- Report withdrawal code (if applicable)

**Calculation Information:**
- Maximum amount on site at any time - pounds
- Basis of estimate codes for all quantities:
  - **M1** - Continuous monitoring
  - **M2** - Periodic/random monitoring
  - **M** - Monitoring (general, pre-2007)
  - **C** - Mass balance calculations
  - **E1** - Published emission factors (e.g., AP-42)
  - **E2** - Site-specific emission factors
  - **E** - Engineering calculations (general, pre-2007)
  - **O** - Other methods

**Chemical Use Information:**
- Maximum chemical concentration (%)
- De minimis exemption claim (Y/N for non-PFAS)

**Certification:**
- Certifying official name and title
- Certification date
- Technical contact name, email, phone

---

## Data Access Methods

### 1. EPA Envirofacts API (RESTful)

**Base URL:** `https://data.epa.gov/efservice/`

**Structure:** `https://data.epa.gov/efservice/[table]/[column][operator][value]/[joins]/[first]:[last]/[sort]/[format]`

**Output Formats:** JSON (default), CSV, Excel, HTML, JSONP, Parquet, PDF, XML

**Key TRI Tables:**
- `tri.tri_facility` - Facility information
- `tri.tri_reporting_form` - Main reporting data
- `tri.tri_transfer` - Off-site transfers
- `tri.tri_release` - Release quantities

**Operators:**
- equals, notEquals
- lessThan, greaterThan, lessThanEqual, greaterThanEqual
- beginsWith, endsWith, contains, excludes
- like, notLike
- in, notIn
- /and/, /or/ (logical combinators)

**County-Level Query Example:**
```
https://data.epa.gov/efservice/tri.tri_facility/county_code/equals/06001/CSV
```
This returns all TRI facilities in Alameda County, CA (FIPS 06001) in CSV format.

**Pagination:** Use `/[start]:[end]/` to retrieve specific record ranges
```
https://data.epa.gov/efservice/tri.tri_facility/state_abbr/equals/CA/0:100/JSON
```
Returns records 0-100 for California facilities.

**Rate Limits:** 15-minute maximum query execution time

**Documentation:** https://www.epa.gov/enviro/envirofacts-data-service-api

---

### 2. TRI Basic Data Files (Bulk Downloads)

**URL:** https://www.epa.gov/toxics-release-inventory-tri-program/tri-basic-data-files-calendar-years-1987-present

**Format:** CSV (comma-separated values)

**Coverage:** 1987-2023 (complete); 2024 (preliminary)

**Fields:** 100 most-used data fields from Form R and Form A

**Download Structure:**
- **By Year:** Select reporting year (1987-2024)
- **By Geography:**
  - U.S. totals (all facilities)
  - Federal facilities only
  - Tribal lands
  - Individual states (50 states + territories)

**URL Pattern:**
```
https://data.epa.gov/efservice/downloads/tri/mv_tri_basic_download/{YEAR}_{GEOGRAPHY}/csv
```

**Example:**
```
https://data.epa.gov/efservice/downloads/tri/mv_tri_basic_download/2023_US/csv
```

**Documentation:**
- Guide to Using TRI Basic Data Files (PDF) - describes each data element
- TRI Reporting Forms and Instructions - detailed field definitions

**Important Notes:**
- Dioxin quantities in GRAMS, all others in POUNDS
- Revisions reflected in files (facilities can revise prior years)
- Updated regularly when revisions submitted

---

### 3. TRI Basic Plus Data Files

**URL:** https://www.epa.gov/toxics-release-inventory-tri-program/tri-basic-plus-data-files-calendar-years-1987-present

**Enhanced Features:**
- All 100 basic fields PLUS additional detailed variables
- Separate files for different data types:
  - File Type 1a - Reporting form data
  - File Type 1b - Waste transfer data
  - File Type 3a - On-site disposal data
  - File Type 3b - Off-site disposal data
  - File Type 3c - POTW transfer data

**Use Case:** Research requiring complete variable set beyond 100 basic fields

---

### 4. TRI National Analysis Data

**URL:** https://www.epa.gov/trinationalanalysis

**Interactive Tools:**
- TRI Toxics Tracker - dashboard with visualizations
- Interactive maps - state, county, metropolitan, watershed, tribal levels
- Trend analysis - 1987-2023

**Geographic Files:**
- Shapefiles with TRI summary data
- GIS-ready formats
- Aggregated to various geographic levels

**Summary Reports:**
- Annual National Analysis report (published annually)
- PDF reports with key findings
- Chemical profiles
- Industry sector analyses

**Most Recent:** 2023 data released October 2024

---

### 5. TRI Explorer

**URL:** https://enviro.epa.gov/triexplorer/

**Features:**
- Web-based query interface
- Facility searches
- Chemical searches
- Geographic searches (state, county, ZIP)
- Trend reports
- Release reports
- Custom queries

**Query Types:**
- Release trends by facility, chemical, industry, geography
- Facility reports (detailed facility profiles)
- Chemical reports
- Comparison reports

**Export Options:**
- CSV download
- Excel export
- PDF reports
- Data visualizations

---

### 6. TRI Data Exchange (XML)

**URL:** https://www.epa.gov/toxics-release-inventory-tri-program/tri-data-exchange

**Purpose:** XML schema for programmatic data submission and retrieval

**Use Case:** Advanced users, automated systems, bulk data processing

---

### 7. Dioxin TEQ Data Files

**URL:** https://www.epa.gov/toxics-release-inventory-tri-program/tri-dioxin-and-dioxin-compounds-and-teq-data-files-calendar

**Special Files:** Toxic Equivalency (TEQ) calculated values for dioxin congeners

**Coverage:** 2008-present

**Format:** CSV with individual congener masses and calculated TEQ values

---

### 8. RSEI Geographic Microdata

**URL:** https://www.epa.gov/rsei

**RSEI Model:** Risk-Screening Environmental Indicators

**Features:**
- Toxicity-weighted releases
- Exposure estimates
- Population impacts
- Geographic grid cells (810m × 810m)
- Census block group aggregation
- County, ZIP code, tract aggregation

**Metrics:**
- RSEI Score = Toxicity weight × Exposed population × Estimated dose
- RSEI Hazard = Toxicity-weighted pounds
- Toxicity-weighted concentration

**EasyRSEI Dashboard:** https://edap.epa.gov/public/extensions/EasyRSEI/EasyRSEI.html

---

## Reporting Requirements and Thresholds

### Facility Coverage Criteria (All 3 Must Be Met):

**1. Industry Sector (NAICS Code):**
- **Manufacturing:** NAICS 31-33 (all 6-digit codes)
- **Additional Sectors:**
  - Metal mining (NAICS 212)
  - Coal mining (NAICS 2121)
  - Electric utilities (NAICS 221)
  - Chemical wholesalers (NAICS 42469)
  - Petroleum terminals (NAICS 424710)
  - Hazardous waste management (NAICS 562)
  - Solvent recovery (NAICS 562112)
  - Federal facilities (all sectors if meet other criteria)

**Full list:** 40 CFR 372.23

**2. Employee Threshold:**
- 10 or more full-time employee equivalents (FTEs)
- FTE = 20,000 hours or more per year
- Includes all employees (not just those working with TRI chemicals)

**3. Chemical Activity Thresholds:**

**Standard Thresholds (most chemicals):**
- **Manufacture:** 25,000 pounds per year
- **Process:** 25,000 pounds per year
- **Otherwise Use:** 10,000 pounds per year

**Lower Thresholds for PBT Chemicals:**
- **Mercury and mercury compounds:** 10 pounds (manufacture/process/otherwise use)
- **Lead and lead compounds:** 100 pounds (manufacture/process/otherwise use)
- **Dioxin and dioxin-like compounds:** 0.1 grams (all activities)
- **Polycyclic aromatic compounds (PACs):** 100 pounds (all activities)

**PFAS Threshold (205 chemicals):**
- **All PFAS:** 100 pounds (manufacture/process/otherwise use)

---

### De Minimis Exemption

**Standard:** 1.0% concentration for most chemicals
- Facilities can exclude quantities in mixtures/trade name products if:
  - Concentration < 1.0%
  - Activity is "otherwise use" (NOT manufacture or process)

**Lower De Minimis:** 0.1% for some highly toxic chemicals

**NO De Minimis for:**
- PFAS chemicals (as of 2023 rule)
- PBT chemicals (in some circumstances)
- Manufacturing and processing activities

---

### Reporting Timeline

**Reporting Year:** Calendar year (January 1 - December 31)

**Due Date:** July 1 of following year
- RY 2023 data due: July 1, 2024
- RY 2024 data due: July 1, 2025
- RY 2025 data due: July 1, 2026

**Submission Method:**
- TRI-MEweb (online web form)
- CDX TRI Made Easy (desktop software)
- XML submission

**Revisions:** Facilities can revise prior year reports at any time (must state reason)

---

### NAICS Codes Update

**Current System:** 2022 NAICS codes (required as of RY 2022, due July 1, 2023)

**Transition:** EPA periodically adopts updated NAICS codes as published by OMB

**Determination:** Full 6-digit NAICS code determines coverage (not 2-, 3-, 4-, or 5-digit)

---

### Form Types

**Form R (Full Report):**
- Required for most chemicals and activities
- Complete release and waste management data
- All PFAS must use Form R (no Form A option)

**Form A (Certification Statement):**
- Abbreviated form for low releases/transfers
- Eligibility: Annual reportable amount ≤ 500 pounds AND
  - Total releases ≤ 500 pounds, OR
  - All releases ≤ 5,000 pounds AND no off-site disposal >5,000 pounds
- NOT available for PFAS

---

## County-Level Aggregation Methods

### Basic County Aggregation

**Primary Field:** County FIPS code (5-digit)
- First 2 digits: State FIPS
- Last 3 digits: County code

**Aggregation Approach:**
```r
# Sum all facility releases by county
county_totals <- tri_data %>%
  group_by(county_fips, year, chemical_name) %>%
  summarise(
    total_releases = sum(total_on_site_release_total, na.rm = TRUE),
    air_releases = sum(on_site_release_total_air, na.rm = TRUE),
    water_releases = sum(on_site_release_total_water, na.rm = TRUE),
    land_releases = sum(on_site_release_total_land, na.rm = TRUE),
    facility_count = n_distinct(tri_facility_id)
  )
```

---

### Normalization Methods

**1. Per Capita Releases:**
```r
# Join with Census population data
library(tidycensus)

# Get county population
county_pop <- get_estimates(
  geography = "county",
  product = "population",
  year = 2023
)

# Calculate per capita
county_per_capita <- county_totals %>%
  left_join(county_pop, by = c("county_fips" = "GEOID")) %>%
  mutate(releases_per_capita = total_releases / population)
```

**2. Releases per Square Mile:**
```r
# Get county areas
county_area <- tigris::counties(year = 2023) %>%
  mutate(area_sqmi = as.numeric(st_area(geometry)) / 2589988.11) %>%
  st_drop_geometry()

# Calculate density
county_density <- county_totals %>%
  left_join(county_area, by = c("county_fips" = "GEOID")) %>%
  mutate(releases_per_sqmi = total_releases / area_sqmi)
```

**3. Industry-Adjusted Metrics:**
```r
# Compare to economic output
county_industry <- tri_data %>%
  group_by(county_fips, naics_2digit) %>%
  summarise(
    releases = sum(total_on_site_release_total),
    facility_count = n_distinct(tri_facility_id)
  ) %>%
  left_join(county_gdp_data, by = c("county_fips", "naics_2digit"))
```

---

### Temporal Aggregation

**Trend Analysis:**
```r
# Calculate annual changes
county_trends <- tri_data %>%
  group_by(county_fips, year) %>%
  summarise(total_releases = sum(total_on_site_release_total)) %>%
  arrange(county_fips, year) %>%
  group_by(county_fips) %>%
  mutate(
    pct_change = (total_releases - lag(total_releases)) / lag(total_releases) * 100,
    five_year_avg = zoo::rollmean(total_releases, k = 5, fill = NA, align = "right")
  )
```

---

### Chemical-Specific Aggregation

**By Chemical Category:**
```r
# Metal compounds total
metal_releases <- tri_data %>%
  filter(metal == "YES") %>%
  group_by(county_fips, year) %>%
  summarise(total_metal_releases = sum(total_on_site_release_total))

# Carcinogens
carcinogen_releases <- tri_data %>%
  filter(carcinogen == "YES") %>%
  group_by(county_fips, year) %>%
  summarise(total_carcinogen_releases = sum(total_on_site_release_total))
```

---

### Multi-County Facilities

**Challenge:** Some facilities span multiple counties (e.g., refineries, mines)

**Solution 1 - Primary County:**
```r
# Use facility's reported county
facility_county <- tri_data %>%
  distinct(tri_facility_id, county_fips)
```

**Solution 2 - Spatial Allocation:**
```r
# Use spatial analysis to allocate releases proportionally
library(sf)

facility_locations <- tri_data %>%
  distinct(tri_facility_id, latitude, longitude) %>%
  st_as_sf(coords = c("longitude", "latitude"), crs = 4326)

county_boundaries <- tigris::counties()

# Identify overlapping counties and allocate
```

---

### Avoiding Double-Counting

**Off-Site Transfers:**
```r
# "Total disposal or other releases" already removes double-counting
# when facility transfers to another TRI facility

# Use this field for county totals:
county_releases <- tri_data %>%
  group_by(county_fips, year) %>%
  summarise(
    total_disposal_releases = sum(total_disposal_or_other_releases)
  )
```

---

### RSEI-Enhanced County Metrics

**Toxicity-Weighted Releases:**
```r
# Download RSEI county-level data
rsei_county <- read.csv("RSEI_county_data.csv")

# Aggregate RSEI scores
county_risk <- rsei_county %>%
  group_by(county_fips, year) %>%
  summarise(
    total_rsei_score = sum(rsei_score),
    total_rsei_hazard = sum(rsei_hazard),
    max_facility_score = max(rsei_score)
  )
```

---

## Data Quality Considerations

### 1. Estimation Methods and Accuracy

**Basis of Estimate Variability:**
- **M1/M2 (Monitoring):** Highest accuracy, direct measurement
- **C (Mass Balance):** Good accuracy if inputs/outputs well-characterized
- **E1/E2 (Emission Factors):** Moderate accuracy, varies by factor quality
- **O (Other):** Lowest certainty, wide potential error margins

**Analysis Implications:**
- Weight facilities using monitoring more heavily in high-precision studies
- Include basis of estimate as control variable
- Flag estimates with low certainty for sensitivity analysis

---

### 2. Reporting Completeness

**Industry Variation:**
- Manufacturing (NAICS 31-33): Most comprehensive coverage
- Mining: Moderate coverage (only metal and coal mining)
- Agriculture: NOT covered (except chemical manufacturing facilities)
- Services: Minimal coverage (only specific sectors)

**Threshold Effects:**
- Facilities below thresholds not required to report (systematic undercount)
- Small businesses disproportionately excluded
- Lower-volume chemical uses invisible

**Solution:** Note coverage limitations; do not extrapolate to non-covered sectors

---

### 3. Chemical Coverage Limitations

**Not on TRI List:**
- Glyphosate (most widely used herbicide)
- Many current-use pesticides
- Pharmaceuticals
- Cosmetic ingredients
- Food additives
- Nanomaterials (most)
- Microplastics

**Recently Added (Limited Historical Data):**
- PFAS: Only 2020+ data (172 PFAS), 2024+ (196 PFAS), 2025+ (205 PFAS)
- DINP: Only 2024+ data

---

### 4. Geographic Resolution Issues

**Facility-Level Precision:**
- Releases reported at facility point location
- Actual contamination may spread across multiple counties
- Air emissions can travel 100+ miles
- Water discharges flow downstream

**Multi-County Facilities:**
- Some facilities have operations in multiple counties
- County assignment based on primary location
- May misallocate releases to single county

**Solution:**
- Use RSEI model for dispersion-adjusted estimates
- Consider airshed/watershed rather than political boundaries
- Buffer analysis around facilities

---

### 5. Temporal Comparability

**Chemical List Changes:**
- Additions: Create appearance of increased releases (actually better reporting)
- Delistings: Create appearance of decreased releases
- Solution: Consistent chemical set for trend analysis

**NAICS Code Updates:**
- 2017 NAICS update changed some facility classifications
- 2022 NAICS update (most recent)
- May cause discontinuities in industry-specific trends

**Threshold Changes:**
- PBT threshold lowering (2000) increased reporting
- PFAS threshold lowering (2020) increased reporting
- Historical data not comparable without adjustment

**Facility Reporting Changes:**
- New facilities enter dataset
- Facilities close or fall below thresholds
- Improved measurement methods over time

---

### 6. Release vs. Exposure

**TRI Reports Releases, Not Exposures:**
- 100 pounds released to air ≠ 100 pounds of human exposure
- Dispersion, transformation, deposition affect actual exposure
- Population density and proximity matter

**Use RSEI for Exposure Estimates:**
- Accounts for toxicity
- Models atmospheric dispersion
- Incorporates population location
- Provides exposure-adjusted metrics

---

### 7. Missing and Incomplete Data

**Common Issues:**
- Withheld data (CBI - Confidential Business Information)
- Non-response to optional fields
- Incomplete waste transfer information
- Missing basis of estimate codes (older data)

**Handling:**
- Document % missing for each variable
- Multiple imputation for critical analyses
- Sensitivity analysis with/without missing data
- Flag low data quality counties

---

### 8. Off-Site Transfer Complexity

**Tracking Challenges:**
- Transfers reported by sending facility
- Receiving facility also reports (potential double-count)
- EPA provides "total disposal or other releases" to address this
- Some transfers cross state/county lines (geographic allocation issues)

**Solution:** Use EPA's calculated "total disposal" field, not raw transfers

---

### 9. Units and Conversions

**Critical Unit Awareness:**
- **Dioxin:** Grams (all others in pounds)
- **Conversions:**
  - 1 pound = 453.592 grams
  - 1 ton = 2,000 pounds
- **TEQ for dioxin:** Requires conversion using WHO TEF values

**Common Errors:**
- Mixing dioxin (grams) with other chemicals (pounds)
- Forgetting to convert when comparing
- Not applying TEF for dioxin toxicity comparisons

---

### 10. Industry Sector Changes

**NAICS Code Updates:**
- Facilities may change primary NAICS code
- Not necessarily change in operations, just classification
- Creates apparent industry shifts

**Facility Ownership Changes:**
- Parent company changes affect reporting
- Consolidation/deconsolidation of facilities
- May affect facility ID assignment

---

### 11. Revision Tracking

**Data Revisions:**
- Facilities can revise any prior year
- EPA updates files continuously
- Downloaded data may differ from prior downloads

**Best Practice:**
- Document download date
- Note "as of" date for any analysis
- Re-download periodically for long-term projects
- Check revision flags in data

---

### 12. Environmental Justice Considerations

**Disproportionate Impacts:**
- TRI data shows uneven geographic distribution
- Low-income and minority communities often higher exposures
- County-level aggregation may mask within-county disparities

**Enhanced Analysis:**
- Census tract or block group level (via RSEI)
- Overlay demographic data
- EJ Screen tool integration
- Environmental justice indicators

---

## Code Examples

### R: Download TRI Data via API

```r
# Load required libraries
library(httr)
library(jsonlite)
library(dplyr)
library(tidyr)

# Function to query EPA Envirofacts TRI API
get_tri_data <- function(state_abbr, year = NULL) {

  # Base URL
  base_url <- "https://data.epa.gov/efservice"

  # Build query URL
  if (!is.null(year)) {
    url <- paste0(base_url, "/tri.tri_facility",
                  "/state_abbr/equals/", state_abbr,
                  "/year/equals/", year,
                  "/JSON")
  } else {
    url <- paste0(base_url, "/tri.tri_facility",
                  "/state_abbr/equals/", state_abbr,
                  "/JSON")
  }

  # Make API request
  response <- GET(url)

  # Check if request successful
  if (status_code(response) == 200) {
    # Parse JSON
    data <- fromJSON(content(response, "text", encoding = "UTF-8"))
    return(as_tibble(data))
  } else {
    warning(paste("API request failed with status:", status_code(response)))
    return(NULL)
  }
}

# Example: Get California TRI facilities
ca_facilities <- get_tri_data("CA", year = 2023)

# View results
head(ca_facilities)

# Get county FIPS codes
ca_counties <- ca_facilities %>%
  count(county_fips, county_name) %>%
  arrange(desc(n))

print(ca_counties)
```

---

### R: Download TRI Basic Data Files

```r
library(readr)
library(dplyr)

# Function to download TRI Basic Data File
download_tri_basic <- function(year, geography = "US",
                                output_dir = "data/tri") {

  # Create output directory if doesn't exist
  if (!dir.exists(output_dir)) {
    dir.create(output_dir, recursive = TRUE)
  }

  # Build download URL
  url <- paste0("https://data.epa.gov/efservice/downloads/tri/",
                "mv_tri_basic_download/", year, "_", geography, "/csv")

  # Output filename
  filename <- file.path(output_dir,
                        paste0("TRI_", year, "_", geography, ".csv"))

  # Download file
  cat("Downloading TRI data for", year, geography, "...\n")
  download.file(url, filename, mode = "wb")

  # Read the file
  cat("Reading data...\n")
  tri_data <- read_csv(filename,
                       col_types = cols(.default = "c"),
                       na = c("", "NA", "N/A"))

  cat("Downloaded", nrow(tri_data), "records\n")

  return(tri_data)
}

# Example: Download 2023 US data
tri_2023 <- download_tri_basic(2023, "US")

# Example: Download California data for multiple years
ca_data <- map_df(2019:2023, ~download_tri_basic(.x, "CA"))

# Convert numeric columns
numeric_cols <- c("total_releases", "fugitive_air", "stack_air",
                  "water_releases", "underground_injection",
                  "land_releases", "offsite_releases")

tri_clean <- tri_2023 %>%
  mutate(across(all_of(numeric_cols), as.numeric))
```

---

### R: County-Level Aggregation

```r
library(dplyr)
library(tidycensus)
library(tigris)
options(tigris_use_cache = TRUE)

# Aggregate TRI data to county level
aggregate_county_tri <- function(tri_data, year) {

  # Sum releases by county
  county_totals <- tri_data %>%
    filter(year == !!year) %>%
    group_by(county_fips, county_name, state_abbr) %>%
    summarise(
      facility_count = n_distinct(tri_facility_id),
      total_releases = sum(total_releases, na.rm = TRUE),
      air_releases = sum(fugitive_air + stack_air, na.rm = TRUE),
      water_releases = sum(water_releases, na.rm = TRUE),
      land_releases = sum(land_releases, na.rm = TRUE),
      underground_injection = sum(underground_injection, na.rm = TRUE),
      offsite_releases = sum(offsite_releases, na.rm = TRUE),
      .groups = "drop"
    )

  return(county_totals)
}

# Get population data
get_county_population <- function(year) {
  pop <- get_estimates(
    geography = "county",
    product = "population",
    year = year,
    geometry = FALSE
  ) %>%
    filter(variable == "POP") %>%
    select(GEOID, NAME, population = value)

  return(pop)
}

# Calculate per capita releases
calculate_per_capita <- function(county_tri, county_pop) {

  result <- county_tri %>%
    left_join(county_pop, by = c("county_fips" = "GEOID")) %>%
    mutate(
      releases_per_capita = total_releases / population,
      air_per_capita = air_releases / population,
      water_per_capita = water_releases / population,
      land_per_capita = land_releases / population
    )

  return(result)
}

# Get county areas
get_county_areas <- function(year) {
  counties_sf <- counties(year = year, cb = TRUE)

  areas <- counties_sf %>%
    mutate(
      area_sqm = as.numeric(st_area(geometry)),
      area_sqmi = area_sqm / 2589988.11  # Convert to square miles
    ) %>%
    st_drop_geometry() %>%
    select(GEOID, NAME, area_sqmi)

  return(areas)
}

# Calculate density metrics
calculate_density <- function(county_tri, county_areas) {

  result <- county_tri %>%
    left_join(county_areas, by = c("county_fips" = "GEOID")) %>%
    mutate(
      releases_per_sqmi = total_releases / area_sqmi,
      facilities_per_sqmi = facility_count / area_sqmi
    )

  return(result)
}

# Complete workflow example
analyze_county_tri <- function(tri_data, year) {

  # Aggregate to county
  county_totals <- aggregate_county_tri(tri_data, year)

  # Get population
  county_pop <- get_county_population(year)

  # Get areas
  county_areas <- get_county_areas(year)

  # Calculate metrics
  county_analysis <- county_totals %>%
    left_join(county_pop, by = c("county_fips" = "GEOID")) %>%
    left_join(county_areas, by = c("county_fips" = "GEOID")) %>%
    mutate(
      releases_per_capita = total_releases / population,
      releases_per_sqmi = total_releases / area_sqmi,
      facilities_per_100k = (facility_count / population) * 100000
    )

  return(county_analysis)
}

# Run analysis
county_results <- analyze_county_tri(tri_2023, 2023)

# Top 10 counties by total releases
top_releases <- county_results %>%
  arrange(desc(total_releases)) %>%
  select(county_name, state_abbr, total_releases,
         facility_count, releases_per_capita) %>%
  head(10)

print(top_releases)
```

---

### R: Chemical-Specific Analysis

```r
# Analyze specific chemical releases
analyze_chemical <- function(tri_data, chemical_name, year) {

  chem_data <- tri_data %>%
    filter(year == !!year,
           chemical == !!chemical_name) %>%
    group_by(county_fips, county_name, state_abbr) %>%
    summarise(
      facility_count = n_distinct(tri_facility_id),
      total_releases = sum(total_releases, na.rm = TRUE),
      .groups = "drop"
    ) %>%
    arrange(desc(total_releases))

  return(chem_data)
}

# Example: Lead compounds by county
lead_releases <- analyze_chemical(tri_2023, "Lead compounds", 2023)

# Top 10 counties for lead
lead_top10 <- lead_releases %>%
  head(10) %>%
  mutate(releases_pounds = scales::comma(total_releases))

print(lead_top10)

# Analyze chemical category
analyze_category <- function(tri_data, category_type, year) {

  # Define categories
  categories <- list(
    metals = c("Antimony compounds", "Arsenic compounds", "Barium compounds",
               "Beryllium compounds", "Cadmium compounds", "Chromium compounds",
               "Cobalt compounds", "Copper compounds", "Lead compounds",
               "Manganese compounds", "Mercury compounds", "Nickel compounds",
               "Selenium compounds", "Silver compounds", "Thallium compounds",
               "Vanadium compounds", "Zinc compounds"),

    carcinogens = tri_data %>%
      filter(carcinogen == "YES") %>%
      pull(chemical) %>%
      unique(),

    pbts = tri_data %>%
      filter(pbt == "YES") %>%
      pull(chemical) %>%
      unique(),

    pfas = tri_data %>%
      filter(pfas == "YES") %>%
      pull(chemical) %>%
      unique()
  )

  # Filter by category
  cat_data <- tri_data %>%
    filter(year == !!year,
           chemical %in% categories[[category_type]]) %>%
    group_by(county_fips, county_name, state_abbr) %>%
    summarise(
      chemical_count = n_distinct(chemical),
      facility_count = n_distinct(tri_facility_id),
      total_releases = sum(total_releases, na.rm = TRUE),
      .groups = "drop"
    ) %>%
    arrange(desc(total_releases))

  return(cat_data)
}

# Example: Metal compound releases
metal_releases <- analyze_category(tri_2023, "metals", 2023)

# Carcinogen releases
carcinogen_releases <- analyze_category(tri_2023, "carcinogens", 2023)
```

---

### R: Time Series Analysis

```r
library(ggplot2)

# Multi-year trend analysis
analyze_county_trends <- function(tri_data, county_fips_code) {

  trends <- tri_data %>%
    filter(county_fips == county_fips_code) %>%
    group_by(year) %>%
    summarise(
      facility_count = n_distinct(tri_facility_id),
      total_releases = sum(total_releases, na.rm = TRUE),
      air_releases = sum(fugitive_air + stack_air, na.rm = TRUE),
      water_releases = sum(water_releases, na.rm = TRUE),
      land_releases = sum(land_releases, na.rm = TRUE),
      .groups = "drop"
    ) %>%
    arrange(year) %>%
    mutate(
      pct_change = (total_releases - lag(total_releases)) /
                    lag(total_releases) * 100,
      five_year_avg = zoo::rollmean(total_releases, k = 5,
                                     fill = NA, align = "right")
    )

  return(trends)
}

# Visualize trends
plot_county_trends <- function(trends_data, county_name) {

  p <- ggplot(trends_data, aes(x = year, y = total_releases)) +
    geom_line(color = "steelblue", size = 1) +
    geom_point(color = "steelblue", size = 2) +
    geom_line(aes(y = five_year_avg), color = "red",
              linetype = "dashed", size = 0.8) +
    labs(
      title = paste("TRI Total Releases:", county_name),
      subtitle = "Blue = Annual, Red Dashed = 5-Year Moving Average",
      x = "Year",
      y = "Total Releases (pounds)",
      caption = "Source: EPA Toxic Release Inventory"
    ) +
    scale_y_continuous(labels = scales::comma) +
    theme_minimal() +
    theme(
      plot.title = element_text(face = "bold", size = 14),
      axis.text = element_text(size = 10)
    )

  return(p)
}

# Example usage
alameda_trends <- analyze_county_trends(ca_data, "06001")
plot_alameda <- plot_county_trends(alameda_trends, "Alameda County, CA")
print(plot_alameda)
```

---

### R: Access RSEI Data

```r
# Download RSEI Geographic Microdata
download_rsei <- function(year, output_dir = "data/rsei") {

  if (!dir.exists(output_dir)) {
    dir.create(output_dir, recursive = TRUE)
  }

  # RSEI data URL (example - check EPA for current URLs)
  url <- paste0("https://gaftp.epa.gov/RSEI/",
                "RSEIMicrodata_", year, ".zip")

  zip_file <- file.path(output_dir, paste0("RSEI_", year, ".zip"))

  # Download
  download.file(url, zip_file, mode = "wb")

  # Unzip
  unzip(zip_file, exdir = output_dir)

  # Read main file
  rsei_file <- list.files(output_dir, pattern = "\\.csv$",
                          full.names = TRUE)[1]
  rsei_data <- read_csv(rsei_file)

  return(rsei_data)
}

# Aggregate RSEI to county level
aggregate_rsei_county <- function(rsei_data) {

  county_rsei <- rsei_data %>%
    group_by(county_fips, year) %>%
    summarise(
      total_rsei_score = sum(rsei_score, na.rm = TRUE),
      total_rsei_hazard = sum(rsei_hazard, na.rm = TRUE),
      avg_rsei_score = mean(rsei_score, na.rm = TRUE),
      max_rsei_score = max(rsei_score, na.rm = TRUE),
      facility_count = n_distinct(tri_facility_id),
      .groups = "drop"
    )

  return(county_rsei)
}
```

---

### Python: Download TRI Data

```python
import requests
import pandas as pd
import json

def get_tri_facilities(state_abbr, year=None):
    """
    Query EPA Envirofacts TRI API for facility data

    Args:
        state_abbr: Two-letter state abbreviation (e.g., 'CA')
        year: Reporting year (optional)

    Returns:
        DataFrame with facility information
    """

    base_url = "https://data.epa.gov/efservice"

    if year:
        url = f"{base_url}/tri.tri_facility/state_abbr/equals/{state_abbr}/year/equals/{year}/JSON"
    else:
        url = f"{base_url}/tri.tri_facility/state_abbr/equals/{state_abbr}/JSON"

    # Make request
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        df = pd.DataFrame(data)
        return df
    else:
        print(f"Error: API returned status code {response.status_code}")
        return None

# Example usage
ca_facilities = get_tri_facilities('CA', 2023)
print(ca_facilities.head())

# County counts
county_counts = ca_facilities.groupby(['county_fips', 'county_name']).size()
print(county_counts.sort_values(ascending=False))
```

---

### Python: County-Level Aggregation

```python
import pandas as pd
import numpy as np

def aggregate_tri_county(tri_df, release_cols):
    """
    Aggregate TRI data to county level

    Args:
        tri_df: DataFrame with TRI facility data
        release_cols: List of column names with release quantities

    Returns:
        DataFrame with county-level aggregates
    """

    # Convert release columns to numeric
    for col in release_cols:
        tri_df[col] = pd.to_numeric(tri_df[col], errors='coerce')

    # Aggregate
    county_agg = tri_df.groupby(['county_fips', 'county_name',
                                  'state_abbr', 'year']).agg({
        'tri_facility_id': 'nunique',
        **{col: 'sum' for col in release_cols}
    }).reset_index()

    # Rename facility count column
    county_agg.rename(columns={'tri_facility_id': 'facility_count'},
                      inplace=True)

    return county_agg

# Example
release_columns = ['total_releases', 'fugitive_air', 'stack_air',
                   'water_releases', 'land_releases']

county_tri = aggregate_tri_county(ca_facilities, release_columns)
print(county_tri.head())

# Top 10 by total releases
top10 = county_tri.nlargest(10, 'total_releases')
print(top10[['county_name', 'total_releases', 'facility_count']])
```

---

### SQL: Query TRI Database

```sql
-- Example queries for TRI database analysis

-- 1. County-level totals for a specific year
SELECT
    county_fips,
    county_name,
    state_abbr,
    COUNT(DISTINCT tri_facility_id) AS facility_count,
    SUM(total_releases) AS total_releases,
    SUM(fugitive_air + stack_air) AS air_releases,
    SUM(water_releases) AS water_releases,
    SUM(land_releases) AS land_releases
FROM tri_facility_data
WHERE year = 2023
GROUP BY county_fips, county_name, state_abbr
ORDER BY total_releases DESC;

-- 2. Top chemicals by release quantity
SELECT
    chemical_name,
    cas_number,
    SUM(total_releases) AS total_releases,
    COUNT(DISTINCT tri_facility_id) AS facility_count,
    COUNT(DISTINCT county_fips) AS county_count
FROM tri_facility_data
WHERE year = 2023
GROUP BY chemical_name, cas_number
ORDER BY total_releases DESC
LIMIT 20;

-- 3. Trend analysis for specific county
SELECT
    year,
    COUNT(DISTINCT tri_facility_id) AS facility_count,
    SUM(total_releases) AS total_releases,
    SUM(air_releases) AS air_releases,
    SUM(water_releases) AS water_releases,
    LAG(SUM(total_releases), 1) OVER (ORDER BY year) AS prior_year_releases,
    (SUM(total_releases) - LAG(SUM(total_releases), 1) OVER (ORDER BY year)) /
        NULLIF(LAG(SUM(total_releases), 1) OVER (ORDER BY year), 0) * 100
        AS pct_change
FROM tri_facility_data
WHERE county_fips = '06001'  -- Alameda County, CA
GROUP BY year
ORDER BY year;

-- 4. PFAS releases by county
SELECT
    county_fips,
    county_name,
    state_abbr,
    COUNT(DISTINCT chemical_name) AS pfas_chemical_count,
    COUNT(DISTINCT tri_facility_id) AS facility_count,
    SUM(total_releases) AS total_pfas_releases
FROM tri_facility_data
WHERE pfas_indicator = 'YES'
  AND year = 2023
GROUP BY county_fips, county_name, state_abbr
HAVING SUM(total_releases) > 0
ORDER BY total_pfas_releases DESC;

-- 5. Carcinogen releases with population context
SELECT
    t.county_fips,
    t.county_name,
    t.state_abbr,
    COUNT(DISTINCT t.tri_facility_id) AS facility_count,
    SUM(t.total_releases) AS carcinogen_releases,
    c.population,
    (SUM(t.total_releases) / c.population) AS releases_per_capita
FROM tri_facility_data t
JOIN county_population c ON t.county_fips = c.county_fips
WHERE t.carcinogen = 'YES'
  AND t.year = 2023
  AND c.year = 2023
GROUP BY t.county_fips, t.county_name, t.state_abbr, c.population
ORDER BY releases_per_capita DESC;
```

---

## Additional Resources

### Official EPA Resources

**Main TRI Website:**
https://www.epa.gov/toxics-release-inventory-tri-program

**TRI Listed Chemicals:**
https://www.epa.gov/toxics-release-inventory-tri-program/tri-listed-chemicals

**TRI Data Downloads:**
https://www.epa.gov/toxics-release-inventory-tri-program/tri-basic-data-files-calendar-years-1987-present

**TRI National Analysis:**
https://www.epa.gov/trinationalanalysis

**TRI Explorer:**
https://enviro.epa.gov/triexplorer/

**Envirofacts API:**
https://www.epa.gov/enviro/envirofacts-data-service-api

**RSEI Model:**
https://www.epa.gov/rsei

**TRI Reporting Forms and Instructions:**
https://www.epa.gov/toxics-release-inventory-tri-program/reporting-tri-facilities

---

### Key EPA Documents (PDFs)

**Chemical Lists:**
- TRI Chemical List (current year): https://www.epa.gov/system/files/documents/2024-01/ry-2023-tri-chemical-list-01092024.pdf
- All TRI Chemical List Changes: https://www.epa.gov/system/files/documents/2024-01/tri-chemical-list-changes-12-27-2023_0.pdf
- List of PFAS Added by NDAA: https://www.epa.gov/system/files/documents/2024-01/list-of-pfas-added-to-the-tri-by-the-ndaa.pdf

**Data Documentation:**
- TRI Basic Data File Format Documentation: https://www.epa.gov/sites/default/files/2015-03/documents/tri_basic_data_file_format_v13_0.pdf
- TRI Basic Plus Documentation: https://www.epa.gov/system/files/documents/2024-09/file_type_1a_1.pdf
- TRI Reporting Codes: https://guideme.epa.gov/ords/guideme_ext/guideme_ext/guideme/file/tri%20reporting%20codes%20for%20form%20r%20and%20form%20a%20-%20july%202022.pdf

**RSEI Documentation:**
- RSEI Methodology: https://www.epa.gov/system/files/documents/2023-04/rsei-methodology-document-v2311-March2023.pdf

---

### R Packages

**EPA Data Access:**
- `epair` (EPA Air Quality) - https://github.com/ropensci/epair

**Census Data:**
- `tidycensus` - https://walker-data.com/tidycensus/
- `tigris` - Spatial census data

**Data Manipulation:**
- `dplyr`, `tidyr`, `readr` (tidyverse)
- `data.table` (large datasets)

**Spatial Analysis:**
- `sf` - Simple features for spatial data
- `leaflet` - Interactive maps
- `tmap` - Thematic maps

---

### Contact and Support

**TRI Technical Support:**
- Email: tri.support@epa.gov
- Phone: (202) 566-0250

**Envirofacts Support:**
- https://www.epa.gov/enviro/envirofacts-web-services

**RSEI Support:**
- Email: rsei@epa.gov

---

## Document Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | November 2025 | Initial comprehensive documentation created |

---

## Citation

When using TRI data in research or publications:

**Suggested Citation:**
U.S. Environmental Protection Agency (EPA). Toxics Release Inventory (TRI) Program. [Year]. Available at: https://www.epa.gov/toxics-release-inventory-tri-program

**Example:**
U.S. Environmental Protection Agency (EPA). 2024. Toxics Release Inventory (TRI) Basic Data Files. Available at: https://www.epa.gov/toxics-release-inventory-tri-program/tri-basic-data-files-calendar-years-1987-present. Accessed November 11, 2025.

---

**END OF DOCUMENTATION**
