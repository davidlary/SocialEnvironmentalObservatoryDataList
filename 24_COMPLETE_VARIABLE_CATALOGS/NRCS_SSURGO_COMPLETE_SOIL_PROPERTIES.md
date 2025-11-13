# NRCS SSURGO COMPLETE SOIL PROPERTIES
## All Soil Survey Geographic Database Properties

**Purpose:** Complete reference catalog of all soil physical, chemical, hydraulic, and interpretive properties in NRCS SSURGO

**Last Updated:** November 13, 2025
**SSURGO Version:** 2.3.2 (current)
**Database Structure:** Hierarchical (Mapunit → Component → Horizon)
**Total Properties:** ~150 core properties across 4 major tables + 57 pre-aggregated gSSURGO properties

---

## 📥 ACCESS COMPLETE OFFICIAL DOCUMENTATION

### **Primary Sources:**

1. **SSURGO Main Portal:**
   - Homepage: https://www.nrcs.usda.gov/resources/data-and-reports/soil-survey-geographic-database-ssurgo
   - Interactive portal: https://www.nrcs.usda.gov/resources/data-and-reports/ssurgo-portal

2. **Soil Data Access (SDA) - Query Interface:**
   - API endpoint: https://sdmdataaccess.nrcs.usda.gov/
   - Complete tables/columns documentation: https://sdmdataaccess.nrcs.usda.gov/documents/TablesAndColumnsReport.pdf
   - Table column descriptions: https://www.nrcs.usda.gov/sites/default/files/2022-08/SSURGO-Metadata-Table-Column-Descriptions-Report.pdf

3. **gSSURGO (Gridded SSURGO):**
   - Homepage: https://www.nrcs.usda.gov/resources/data-and-reports/gridded-soil-survey-geographic-gssurgo-database
   - User guide: https://www.nrcs.usda.gov/sites/default/files/2022-08/gSSURGO_UserGuide_July2020.pdf

4. **R Package for Programmatic Access:**
   - soilDB package: https://ncss-tech.github.io/soilDB/
   - CRAN documentation: https://cran.r-project.org/web/packages/soilDB/soilDB.pdf

---

## 🗂️ DATABASE STRUCTURE

SSURGO uses a **hierarchical relational structure** requiring aggregation for county-level analysis:

```
MAPUNIT (polygon-level, spatial)
    ↓ mukey (map unit key)
COMPONENT (unmapped soil types within map units)
    ↓ cokey (component key)
CHORIZON (soil horizon properties by depth)
```

**Aggregation Workflow:**
1. **Horizon → Component:** Depth-weighted averaging (e.g., top 0-100 cm)
2. **Component → Map Unit:** Component-percent weighting
3. **Map Unit → County:** Area-weighted or dominant condition

---

## 🌱 CHORIZON TABLE: HORIZON-LEVEL PROPERTIES (~80 properties)

**Table:** `chorizon`
**Description:** Soil properties measured or estimated for each soil horizon (depth layer)
**Key Field:** `cokey` (component key) + horizon identifiers

### **1. DEPTH & IDENTIFICATION (5 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **hzdept_r** | Horizon depth, top (representative value) | cm |
| **hzdepb_r** | Horizon depth, bottom (representative value) | cm |
| **hzname** | Horizon designation (e.g., A, Bt, C) | text |
| **desgnmaster** | Master horizon designation | text |
| **hzthk_r** | Horizon thickness (calculated) | cm |

### **2. TEXTURE PROPERTIES (15 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **texture** | Soil texture class (text) | text |
| **sandtotal_r** | Total sand (0.05-2.0 mm) | % weight |
| **sandvc_r** | Very coarse sand (1.0-2.0 mm) | % weight |
| **sandco_r** | Coarse sand (0.5-1.0 mm) | % weight |
| **sandmed_r** | Medium sand (0.25-0.5 mm) | % weight |
| **sandfine_r** | Fine sand (0.1-0.25 mm) | % weight |
| **sandvf_r** | Very fine sand (0.05-0.1 mm) | % weight |
| **silttotal_r** | Total silt (0.002-0.05 mm) | % weight |
| **siltco_r** | Coarse silt (0.02-0.05 mm) | % weight |
| **siltfine_r** | Fine silt (0.002-0.02 mm) | % weight |
| **claytotal_r** | Total clay (<0.002 mm) | % weight |
| **claysizedcarb_r** | Clay-sized carbonates | % weight |
| **om_r** | Organic matter | % weight |
| **dbthirdbar_r** | Bulk density at 1/3 bar (field capacity) | g/cm³ |
| **partdensity** | Particle density | g/cm³ |

### **3. CHEMICAL PROPERTIES (20 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **ph1to1h2o_r** | pH 1:1 soil:water | pH units |
| **ph01mcacl2_r** | pH 0.01M CaCl2 | pH units |
| **phoxidized_r** | pH oxidized | pH units |
| **ec_r** | Electrical conductivity (salinity) | dS/m |
| **esp_r** | Exchangeable sodium percentage | % |
| **sar_r** | Sodium adsorption ratio | unitless |
| **cec7_r** | Cation exchange capacity at pH 7 | meq/100g |
| **ecec_r** | Effective cation exchange capacity | meq/100g |
| **sumbases_r** | Sum of bases (Ca, Mg, Na, K) | meq/100g |
| **base_sat_r** | Base saturation | % |
| **caco3_r** | Calcium carbonate equivalent | % weight |
| **gypsum_r** | Gypsum content | % weight |
| **calcium_r** | Extractable calcium | mg/kg |
| **magnesium_r** | Extractable magnesium | mg/kg |
| **sodium_r** | Extractable sodium | mg/kg |
| **potassium_r** | Extractable potassium | mg/kg |
| **carbonates_r** | Carbonates | % weight |
| **bicarbonates_r** | Bicarbonates | mg/L |
| **sulfate_r** | Sulfate | mg/L |
| **nitrate_r** | Nitrate | mg/kg |

### **4. HYDRAULIC PROPERTIES (12 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **awc_r** | Available water capacity (1/3 bar - 15 bar) | cm/cm |
| **wtenthbar_r** | Water content at 1/10 bar | % volume |
| **wthirdbar_r** | Water content at 1/3 bar (field capacity) | % volume |
| **wfifteenbar_r** | Water content at 15 bar (wilting point) | % volume |
| **wsatiated_r** | Water content at satiation (0 bar) | % volume |
| **ksat_r** | Saturated hydraulic conductivity | µm/s |
| **ksat_l** | Saturated hydraulic conductivity (low) | µm/s |
| **ksat_h** | Saturated hydraulic conductivity (high) | µm/s |
| **dbovendry_r** | Bulk density oven-dry | g/cm³ |
| **partdensity** | Particle density | g/cm³ |
| **lep_r** | Linear extensibility percent (shrink-swell) | % |
| **ll_r** | Liquid limit | % weight |

### **5. ROCK FRAGMENTS (8 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **fragvol_r** | Total rock fragment volume | % volume |
| **frag3to10_r** | Rock fragments 3-10 inches | % volume |
| **fraggt10_r** | Rock fragments >10 inches | % volume |
| **gravel_r** | Gravel (2 mm - 7.5 cm) | % volume |
| **cobbles_r** | Cobbles (7.5-25 cm) | % volume |
| **stones_r** | Stones (25-60 cm) | % volume |
| **boulders_r** | Boulders (>60 cm) | % volume |
| **channers_r** | Channers (thin, flat fragments) | % volume |

### **6. ENGINEERING PROPERTIES (10 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **kwfact** | Kw factor (whole soil erodibility) | unitless |
| **kffact** | Kf factor (fine earth erodibility) | unitless |
| **pi_r** | Plasticity index | % weight |
| **ll_r** | Liquid limit | % weight |
| **aashto_r** | AASHTO classification | text |
| **unified_r** | Unified soil classification | text |
| **str_r** | Soil reaction (strength) | tons/sq ft |
| **strdmp_r** | Soil reaction damped | tons/sq ft |
| **atterberg_li** | Atterberg liquid limit | % weight |
| **atterberg_pi** | Atterberg plasticity index | % weight |

### **7. OTHER HORIZON PROPERTIES (10 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **gravel_r** | Gravel content | % volume |
| **stratextsflag** | Stratified textures flag | boolean |
| **rupresblkcem** | Rupture resistance cementation | text |
| **rupresblkdry** | Rupture resistance dry | text |
| **rupresblkmst** | Rupture resistance moist | text |
| **rupresplate** | Rupture resistance platy | text |
| **stickiness** | Stickiness | text |
| **plasticity** | Plasticity | text |
| **manner** | Manner of failure | text |
| **effclass** | Effervescence class | text |

**Note:** Properties with `_r` suffix indicate representative values. Most properties also have `_l` (low) and `_h` (high) values representing range uncertainty.

---

## 🏞️ COMPONENT TABLE: COMPONENT-LEVEL PROPERTIES (~50 properties)

**Table:** `component`
**Description:** Unmapped soil types (components) within map units, with taxonomic and landscape attributes
**Key Field:** `cokey` (component key), links to `mukey` (map unit key)

### **1. IDENTIFICATION & TAXONOMY (12 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **compname** | Component name (soil series or phase) | text |
| **comppct_r** | Component percentage of map unit | % |
| **compkind** | Component kind | Series, Taxadjunct, Variant, Family, etc. |
| **majcompflag** | Major component flag (>15% of map unit) | Yes/No |
| **taxorder** | Soil Taxonomy Order (highest level) | 12 orders (Entisols, Inceptisols, etc.) |
| **taxsuborder** | Soil Taxonomy Suborder | text |
| **taxgrtgroup** | Soil Taxonomy Great Group | text |
| **taxsubgrp** | Soil Taxonomy Subgroup | text |
| **taxpartsize** | Particle size class | Fine, coarse-loamy, sandy, etc. |
| **taxpartsizemod** | Particle size modifier | text |
| **taxceactcl** | CEC activity class | Superactive, active, semiactive, etc. |
| **taxreaction** | Reaction class | Calcareous, acid, etc. |

### **2. SLOPE & LANDFORM (8 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **slope_r** | Slope gradient (representative) | % |
| **slope_l** | Slope gradient (low) | % |
| **slope_h** | Slope gradient (high) | % |
| **slopelenusle_r** | Slope length (USLE) | feet |
| **runoff** | Runoff class | Very low, low, medium, high, very high |
| **tfact** | T factor (tolerable soil loss) | tons/acre/year |
| **elev_r** | Elevation (representative) | meters |
| **aspectrep** | Aspect (representative) | degrees |

### **3. HYDROLOGIC PROPERTIES (5 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **hydgrp** | Hydrologic soil group | A, B, C, D, A/D, B/D, C/D |
| **hydricrating** | Hydric rating | Yes, No, Unranked |
| **drainagecl** | Natural drainage class | Excessively, well, moderately well, somewhat poorly, poorly, very poorly |
| **flodfreqcl** | Flooding frequency class | None, very rare, rare, occasional, frequent, very frequent |
| **pondfreqcl** | Ponding frequency class | None, rare, occasional, frequent |

### **4. AGRICULTURAL INTERPRETATIONS (10 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **nirrcapcl** | Non-irrigated capability class | I-VIII |
| **nirrcapscl** | Non-irrigated capability subclass | e, w, s, c |
| **nirrcapunit** | Non-irrigated capability unit | numeric |
| **irrcapcl** | Irrigated capability class | I-VIII |
| **irrcapscl** | Irrigated capability subclass | e, w, s, c |
| **irrcapunit** | Irrigated capability unit | numeric |
| **foragesuitgrpid** | Forage suitability group ID | text |
| **ecoclassid** | Ecological site ID | text |
| **ecoclasstypename** | Ecological site type | text |
| **yldunits** | Yield units | text |

### **5. PARENT MATERIAL & GEOMORPHOLOGY (8 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **pmgroupname** | Parent material group | text |
| **pmorigin** | Parent material origin | Igneous, sedimentary, metamorphic |
| **pmkind** | Parent material kind | Till, outwash, alluvium, colluvium, loess, etc. |
| **pmtaxpartsize** | Parent material texture | text |
| **geomdesc** | Geomorphic description | text |
| **landform** | Landform | Terrace, floodplain, hillslope, etc. |
| **landscape** | Landscape | text |
| **microfeature** | Microfeature | text |

### **6. OTHER COMPONENT ATTRIBUTES (7 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **localphase** | Local phase | text |
| **otherph** | Other phase | text |
| **interpfocus** | Interpretation focus | text |
| **invsiteind** | Investigate site indicator | Yes/No |
| **rsprod_r** | Range site production | lbs/acre |
| **farmlndcl** | Farmland classification | Prime, important, not classified |
| **frostact** | Frost action | Low, moderate, high |

---

## 🗺️ MAPUNIT TABLE: MAP UNIT PROPERTIES (~25 properties)

**Table:** `mapunit`
**Description:** Polygon-level attributes for soil map units
**Key Field:** `mukey` (map unit key)

### **Key Map Unit Properties**

| Property | Description | Values |
|----------|-------------|--------|
| **muname** | Map unit name | text |
| **mukind** | Map unit kind | Consociation, complex, association, undifferentiated group |
| **muacres** | Map unit area | acres |
| **farmlndcl** | Farmland classification | Prime, important, not classified |
| **brockdepmin** | Minimum bedrock depth | cm |
| **wtdepannmin** | Minimum annual water table depth | cm |
| **wtdepaprjunmin** | Minimum Apr-Jun water table depth | cm |
| **flodfreqdcd** | Flooding frequency dominant condition | None, rare, occasional, frequent |
| **flodfreqmax** | Flooding frequency maximum | text |
| **pondfreqprs** | Ponding frequency present | text |
| **aws025wta** | Available water storage 0-25 cm (weighted avg) | cm |
| **aws050wta** | Available water storage 0-50 cm (weighted avg) | cm |
| **aws0100wta** | Available water storage 0-100 cm (weighted avg) | cm |
| **aws0150wta** | Available water storage 0-150 cm (weighted avg) | cm |
| **drclassdcd** | Drainage class dominant condition | text |
| **hydgrpdcd** | Hydrologic group dominant condition | A, B, C, D |
| **iccdcd** | Irrigated capability class dominant condition | I-VIII |
| **niccdcd** | Non-irrigated capability class dominant condition | I-VIII |
| **engdcd** | Engineering limitations | text |
| **forpehrtdcp** | Potential erosion hazard (forest roads) | text |
| **urbrecptdcd** | Urban recreation development | text |

---

## 📊 gSSURGO VALU1 TABLE: PRE-AGGREGATED PROPERTIES (57 properties)

**Table:** `Valu1`
**Description:** Pre-summarized "ready to map" attributes at map unit level
**Source:** Derived from SSURGO using best-practice aggregation methods

### **Official Documentation:**
- Complete Valu1 field list: Included in gSSURGO download metadata
- User Guide: https://www.nrcs.usda.gov/sites/default/files/2022-08/gSSURGO_UserGuide_July2020.pdf

### **1. CROP PRODUCTIVITY INDICES (6 properties)**

| Property | Description | Range |
|----------|-------------|-------|
| **nccpi2cs** | NCCPI corn and soybeans | 0-1 |
| **nccpi2sg** | NCCPI small grains | 0-1 |
| **nccpi2co** | NCCPI cotton | 0-1 |
| **nccpi2all** | NCCPI all crops | 0-1 |
| **pctearthmc** | Percent earthy map unit (major components) | % |
| **rootznemc** | Root zone depth (earthy, major components) | cm |

### **2. AVAILABLE WATER STORAGE - AWS (12 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **aws025wta** | AWS 0-25 cm (weighted average) | cm |
| **aws050wta** | AWS 0-50 cm (weighted average) | cm |
| **aws0100wta** | AWS 0-100 cm (weighted average) | cm |
| **aws0150wta** | AWS 0-150 cm (weighted average) | cm |
| **aws025wtd** | AWS 0-25 cm (dominant condition) | cm |
| **aws050wtd** | AWS 0-50 cm (dominant condition) | cm |
| **aws0100wtd** | AWS 0-100 cm (dominant condition) | cm |
| **aws0150wtd** | AWS 0-150 cm (dominant condition) | cm |
| **rootznaws** | AWS within crop root zone | cm |
| **droughty** | Drought vulnerable soil landscapes | boolean |
| **pwsl1pomu** | Potential wetland soil landscapes (method 1) | % |
| **mukey** | Map unit key (identifier) | integer |

### **3. HYDROLOGIC PROPERTIES (4 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **hydgrpdcd** | Hydrologic group dominant condition | A, B, C, D, A/D, B/D, C/D |
| **hydclprs** | Hydric classification present | Yes/No |
| **wtdepannmin** | Minimum annual water table depth | cm |
| **wtdepaprjunmin** | Minimum Apr-Jun water table depth | cm |

### **4. CAPABILITY CLASSIFICATION (4 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **niccdcd** | Non-irrigated capability class dominant condition | I-VIII |
| **iccdcd** | Irrigated capability class dominant condition | I-VIII |
| **niccdcdpct** | Percent of map unit in non-irrigated capability class | % |
| **iccdcdpct** | Percent of map unit in irrigated capability class | % |

### **5. FLOODING & PONDING (4 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **flodfreqdcd** | Flooding frequency dominant condition | None, rare, occasional, frequent, very frequent |
| **flodfreqmax** | Flooding frequency maximum | text |
| **pondfreqprs** | Ponding frequency present | Yes/No |
| **slopegradwta** | Slope gradient weighted average | % |

### **6. DEPTH RESTRICTIONS (5 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **brockdepmin** | Minimum depth to bedrock | cm |
| **brockdepmax** | Maximum depth to bedrock | cm |
| **cecsoi_r** | CEC of soil (0-100 cm) | meq/100g |
| **ecec_r** | Effective CEC (0-100 cm) | meq/100g |
| **om_r** | Organic matter (surface horizon) | % weight |

### **7. TEXTURE & STRUCTURE (6 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **sandtotal_r** | Total sand (0-100 cm weighted avg) | % weight |
| **silttotal_r** | Total silt (0-100 cm weighted avg) | % weight |
| **claytotal_r** | Total clay (0-100 cm weighted avg) | % weight |
| **dbthirdbar_r** | Bulk density at 1/3 bar (0-100 cm weighted avg) | g/cm³ |
| **ksat_r** | Saturated hydraulic conductivity (0-100 cm) | µm/s |
| **ph1to1h2o_r** | pH 1:1 water (0-100 cm weighted avg) | pH units |

### **8. INTERPRETATIONS (8 properties)**

| Property | Description | Values |
|----------|-------------|--------|
| **forpehrtdcp** | Potential erosion hazard (forest roads) | Slight, moderate, severe |
| **musumcpct** | Map unit sum of component percentages | % |
| **urbrecptdcd** | Urban recreation development | text |
| **drclassdcd** | Drainage class dominant condition | text |
| **farmlndcl** | Farmland classification | Prime, important, not classified |
| **englndcl** | Engineering limitations | text |
| **tfact** | T factor (tolerable soil loss) | tons/acre/year |
| **erocl** | Erosion class | text |

### **9. OTHER AGGREGATED PROPERTIES (8 properties)**

| Property | Description | Units |
|----------|-------------|-------|
| **rsprod_r** | Range site production (representative) | lbs/acre |
| **taxorder** | Taxonomic order (dominant) | text |
| **taxsuborder** | Taxonomic suborder (dominant) | text |
| **soc_r** | Soil organic carbon (0-100 cm) | % weight |
| **caco3_r** | Calcium carbonate equivalent (0-100 cm) | % weight |
| **gypsum_r** | Gypsum content (0-100 cm) | % weight |
| **sar_r** | Sodium adsorption ratio (0-100 cm) | unitless |
| **ec_r** | Electrical conductivity (0-100 cm) | dS/m |

**Note:** Many Valu1 properties exist in multiple aggregation variants:
- **wta** = weighted average (component-percent weighted)
- **wtd** = dominant condition (most common/abundant)
- **dcd** = dominant condition
- **prs** = present (yes/no)
- **min/max** = minimum/maximum values

---

## 🔧 SOIL INTERPRETATION TABLES (~20 interpretation categories)

**Tables:** `cointerp` (component interpretation), `muinterp` (map unit interpretation)
**Description:** Suitability ratings for various land uses

### **Major Interpretation Categories:**

| Interpretation | Description | Rating Classes |
|----------------|-------------|----------------|
| **Agricultural Interpretations** | Crop suitability, irrigation, drainage | Very limited, somewhat limited, not limited |
| **Building Site Development** | Dwellings, roads, septic systems | Slight, moderate, severe |
| **Sanitary Facilities** | Septic tank absorption fields, sewage lagoons | Slight, moderate, severe |
| **Construction Materials** | Sand, gravel, topsoil, roadfill | Good, fair, poor |
| **Water Management** | Pond reservoir areas, embankments, irrigation | Slight, moderate, severe |
| **Recreational Development** | Camps, picnic areas, playgrounds, paths | Slight, moderate, severe |
| **Wildlife Habitat** | Habitat for various species | Very low, low, moderate, high, very high |
| **Rangeland** | Rangeland productivity, composition | Productivity rating 0-100 |
| **Forestland** | Tree growth, equipment limitations | Site index, productivity class |
| **Engineering** | Corrosion (steel/concrete), excavation difficulty | Low, moderate, high |
| **Erosion Hazard** | Wind, water erosion | Slight, moderate, severe, very severe |
| **Soil Compaction** | Off-road equipment | Slight, moderate, severe |
| **Construction Depth** | Depth to bedrock, water table | Slight, moderate, severe |

**Interpretation Rules:**
- Each interpretation has fuzzy-logic rule set
- Component ratings aggregated to map unit level
- Multiple properties evaluated simultaneously
- Output is typically limiting condition (most restrictive)

---

## 🔍 HOW TO USE SSURGO DATA FOR COUNTY-LEVEL RESEARCH

### **Step 1: Download SSURGO Data**

**Option A: Soil Data Access (SDA) - Programmatic (RECOMMENDED)**

```r
library(soilDB)
library(tidyverse)

# Query SSURGO data for specific county using Soil Data Access
# Example: Travis County, Texas (FIPS 48453)

# Get spatial data for county
travis_ssurgo <- fetchSDA_spatial(
  x = "SELECT * FROM sapolygon WHERE areasymbol = 'TX453'",
  geom.src = 'sapolygon'
)

# Get component data
travis_components <- fetchSDA(
  "SELECT co.mukey, co.cokey, co.compname, co.comppct_r, co.slope_r,
          co.hydgrp, co.drainagecl, co.taxorder
   FROM component AS co
   INNER JOIN mapunit AS mu ON co.mukey = mu.mukey
   WHERE mu.mukey IN
   (SELECT mukey FROM sapolygon WHERE areasymbol = 'TX453')"
)

# Get horizon data
travis_horizons <- fetchSDA(
  "SELECT ch.cokey, ch.hzdept_r, ch.hzdepb_r,
          ch.sandtotal_r, ch.claytotal_r, ch.om_r,
          ch.ph1to1h2o_r, ch.awc_r, ch.ksat_r, ch.dbthirdbar_r
   FROM chorizon AS ch
   WHERE ch.cokey IN
   (SELECT cokey FROM component WHERE mukey IN
    (SELECT mukey FROM sapolygon WHERE areasymbol = 'TX453'))"
)
```

**Option B: gSSURGO - Pre-Aggregated (EASIER)**

```r
library(terra)
library(sf)

# Download gSSURGO for state (available by state)
# gSSURGO includes Valu1 table with 57 pre-aggregated properties
# Download from: https://nrcs.app.box.com/v/soils

# Example: Load gSSURGO raster and Valu1 table
gssurgo_raster <- rast("gSSURGO_TX.tif")
valu1_table <- read_csv("valu1.csv")

# Load county boundary
county_boundary <- st_read("tl_2020_48_county.shp") %>%
  filter(GEOID == "48453") # Travis County

# Extract map unit keys for county
county_mukeys <- extract(gssurgo_raster, vect(county_boundary))

# Join to Valu1 table for soil properties
county_soils <- valu1_table %>%
  filter(mukey %in% unique(county_mukeys$mukey))
```

**Option C: Web Soil Survey - Manual Download**
- Interactive interface: https://websoilsurvey.nrcs.usda.gov/
- Draw AOI (county boundary)
- Download: Spatial + Tabular data
- Join tables: mapunit → component → chorizon

---

### **Step 2: Aggregate Horizon Data to Meaningful Depths**

```r
library(tidyverse)

# Calculate depth-weighted averages for 0-30 cm (surface soil)
surface_soil <- travis_horizons %>%
  # Filter to 0-30 cm depth
  filter(hzdept_r < 30) %>%
  mutate(
    # Calculate overlap of each horizon with 0-30 cm zone
    depth_overlap = pmin(hzdepb_r, 30) - pmax(hzdept_r, 0),
    # Weight = thickness of overlap
    weight = depth_overlap / 30
  ) %>%
  group_by(cokey) %>%
  summarize(
    # Depth-weighted means
    sand_0_30 = sum(sandtotal_r * weight, na.rm = TRUE),
    clay_0_30 = sum(claytotal_r * weight, na.rm = TRUE),
    om_0_30 = sum(om_r * weight, na.rm = TRUE),
    ph_0_30 = sum(ph1to1h2o_r * weight, na.rm = TRUE),
    awc_0_30 = sum(awc_r * depth_overlap, na.rm = TRUE), # sum for AWC
    ksat_0_30 = exp(sum(log(ksat_r + 0.01) * weight, na.rm = TRUE)), # geometric mean
    bd_0_30 = sum(dbthirdbar_r * weight, na.rm = TRUE)
  )
```

---

### **Step 3: Aggregate Component Data to Map Unit Level**

```r
# Component-percent weighted aggregation to map unit
mapunit_soil <- travis_components %>%
  left_join(surface_soil, by = "cokey") %>%
  group_by(mukey) %>%
  summarize(
    # Component-weighted means
    sand = sum(sand_0_30 * comppct_r, na.rm = TRUE) / sum(comppct_r, na.rm = TRUE),
    clay = sum(clay_0_30 * comppct_r, na.rm = TRUE) / sum(comppct_r, na.rm = TRUE),
    om = sum(om_0_30 * comppct_r, na.rm = TRUE) / sum(comppct_r, na.rm = TRUE),
    ph = sum(ph_0_30 * comppct_r, na.rm = TRUE) / sum(comppct_r, na.rm = TRUE),
    awc = sum(awc_0_30 * comppct_r, na.rm = TRUE) / sum(comppct_r, na.rm = TRUE),

    # Dominant condition (most common value weighted by comppct)
    hydgrp_dominant = hydgrp[which.max(comppct_r)],
    drainagecl_dominant = drainagecl[which.max(comppct_r)],

    # Area-weighted slope
    slope_mean = sum(slope_r * comppct_r, na.rm = TRUE) / sum(comppct_r, na.rm = TRUE)
  )
```

---

### **Step 4: Aggregate Map Units to County Level**

```r
# Area-weighted aggregation to county
# Requires spatial data to get map unit areas

library(sf)

# Calculate area of each map unit polygon
travis_ssurgo <- travis_ssurgo %>%
  mutate(area_sqm = as.numeric(st_area(.)))

# Join soil properties
travis_with_props <- travis_ssurgo %>%
  left_join(mapunit_soil, by = "mukey")

# County-level area-weighted means
county_soil_summary <- travis_with_props %>%
  st_drop_geometry() %>%
  summarize(
    fips = "48453",
    county_sand = sum(sand * area_sqm, na.rm = TRUE) / sum(area_sqm, na.rm = TRUE),
    county_clay = sum(clay * area_sqm, na.rm = TRUE) / sum(area_sqm, na.rm = TRUE),
    county_om = sum(om * area_sqm, na.rm = TRUE) / sum(area_sqm, na.rm = TRUE),
    county_ph = sum(ph * area_sqm, na.rm = TRUE) / sum(area_sqm, na.rm = TRUE),
    county_awc = sum(awc * area_sqm, na.rm = TRUE) / sum(area_sqm, na.rm = TRUE),
    county_slope = sum(slope_mean * area_sqm, na.rm = TRUE) / sum(area_sqm, na.rm = TRUE),

    # Dominant hydrologic group (most common by area)
    county_hydgrp = hydgrp_dominant[which.max(area_sqm)],

    # Percent of county in each hydrologic group
    pct_hydgrp_A = sum(area_sqm[hydgrp_dominant == "A"], na.rm = TRUE) / sum(area_sqm) * 100,
    pct_hydgrp_B = sum(area_sqm[hydgrp_dominant == "B"], na.rm = TRUE) / sum(area_sqm) * 100,
    pct_hydgrp_C = sum(area_sqm[hydgrp_dominant == "C"], na.rm = TRUE) / sum(area_sqm) * 100,
    pct_hydgrp_D = sum(area_sqm[hydgrp_dominant == "D"], na.rm = TRUE) / sum(area_sqm) * 100
  )
```

---

### **Step 5: Alternative - Use gSSURGO Pre-Aggregated Data**

```r
# Much faster - uses pre-computed map unit aggregations

# Extract county statistics from gSSURGO Valu1 table
county_gssurgo <- travis_ssurgo %>%
  st_drop_geometry() %>%
  left_join(valu1_table, by = "mukey") %>%
  mutate(area_sqm = area_sqm) %>%
  summarize(
    fips = "48453",
    # Available water storage (already aggregated to map unit)
    aws_0_100cm = sum(aws0100wta * area_sqm, na.rm = TRUE) / sum(area_sqm),

    # NCCPI crop productivity (already aggregated)
    nccpi_all = sum(nccpi2all * area_sqm, na.rm = TRUE) / sum(area_sqm),

    # Hydrologic group (already determined at map unit)
    hydgrp = hydgrpdcd[which.max(area_sqm)],

    # Drainage class
    drainage = drclassdcd[which.max(area_sqm)]
  )
```

---

## 📚 COMPANION DATA SOURCES

### **NRCS Related Datasets:**

**Soil Climate (PRISM-based):**
- 30-year normals: Temperature, precipitation by soil map unit
- Portal: https://www.ncss-tech.net/

**Ecological Site Descriptions:**
- Plant community dynamics by soil component
- Portal: https://edit.jornada.nmsu.edu/

**Soil Health Indicators:**
- Soil organic carbon, aggregate stability, infiltration
- Assessment framework: https://www.nrcs.usda.gov/conservation-basics/natural-resource-concerns/soil/soil-health

---

## 📈 TEMPORAL & SPATIAL COVERAGE

| Attribute | Details |
|-----------|---------|
| **Spatial Coverage** | All U.S. states and territories |
| **Spatial Resolution** | 1:12,000 to 1:24,000 scale (polygon boundaries) |
| **Minimum Mapping Unit** | 1-3 acres (varies by survey) |
| **Temporal Coverage** | Ongoing soil surveys (1900s-present) |
| **Update Frequency** | Continuous (individual survey areas updated 5-15 year cycle) |
| **Most Recent Version** | SSURGO 2.3.2 (October 2022 schema), data updated daily |
| **gSSURGO Release** | Annual (October each year) |

---

## ⚠️ DATA QUALITY & LIMITATIONS

### **Strengths:**
- Most comprehensive soil dataset in U.S.
- Field-verified data by professional soil scientists
- Detailed property information (80+ horizon properties)
- Includes uncertainty estimates (_l, _r, _h values)
- Freely available with complete documentation

### **Limitations:**
- **Scale-dependent:** Designed for 1:12,000-1:24,000 use, not suitable for site-specific (<1 acre) analysis
- **Temporal mismatch:** Survey dates vary widely (1950s-2020s), mix of old and new data
- **Property estimation:** Many properties are estimated via pedotransfer functions, not measured
- **Map unit delineations:** Polygons represent soil associations, not pure soil types
- **Component percentages:** Estimates of soil type composition, not measured
- **No temporal dynamics:** Static properties, does not capture seasonal or annual variability
- **Aggregation complexity:** Requires multi-step aggregation (horizon → component → map unit → county)
- **Missing data:** Some properties may be NULL for certain components/horizons

---

## 📝 CITATION

**When using SSURGO data, cite:**

> Soil Survey Staff. 2023. Gridded Soil Survey Geographic (gSSURGO) Database for the Conterminous United States. United States Department of Agriculture, Natural Resources Conservation Service. Available at: https://nrcs.app.box.com/v/soils

> Soil Survey Staff. 2023. Soil Survey Geographic (SSURGO) Database. United States Department of Agriculture, Natural Resources Conservation Service. Available at: https://sdmdataaccess.nrcs.usda.gov/

**For specific soil surveys:**

> USDA Natural Resources Conservation Service. [Year]. Soil Survey of [County], [State]. Available at: https://websoilsurvey.nrcs.usda.gov/

---

**Last Updated:** November 13, 2025
**Database Version:** SSURGO 2.3.2
**Total Properties Documented:** ~150 core properties + 57 gSSURGO aggregated properties + 20 interpretation categories = **227 total soil attributes**
