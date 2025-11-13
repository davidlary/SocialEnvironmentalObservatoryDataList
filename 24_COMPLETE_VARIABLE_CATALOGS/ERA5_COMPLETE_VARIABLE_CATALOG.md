# ERA5 COMPLETE VARIABLE CATALOG
## All ECMWF Reanalysis v5 Atmospheric Parameters

**Purpose:** Complete reference catalog of all atmospheric, land, and oceanic variables in ECMWF ERA5 reanalysis

**Last Updated:** November 13, 2025
**ERA5 Version:** ERA5 (5th generation ECMWF reanalysis)
**Temporal Coverage:** January 1940 - present (updated daily within 5 days of real-time)
**Spatial Resolution:** 0.25° × 0.25° (≈31 km) globally
**Vertical Levels:** 137 model levels (surface to 80 km) + 37 pressure levels
**Total Parameters:** 200+ single-level + 16 pressure-level = **~240 total variables**

---

## 📥 ACCESS COMPLETE OFFICIAL PARAMETER DATABASE

### **Primary Sources:**

1. **Climate Data Store (CDS) - Interactive Download:**
   - ERA5 hourly single levels: https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels
   - ERA5 hourly pressure levels: https://cds.climate.copernicus.eu/datasets/reanalysis-era5-pressure-levels
   - Complete ERA5 (all variables): https://cds.climate.copernicus.eu/datasets/reanalysis-era5-complete

2. **ECMWF Official Documentation:**
   - ERA5 data documentation: https://confluence.ecmwf.int/display/CKB/ERA5:+data+documentation
   - Parameter listings (Tables 2-5): https://confluence.ecmwf.int/pages/viewpage.action?pageId=82870405
   - Product User Guide: https://confluence.ecmwf.int/pages/viewpage.action?pageId=505390919

3. **Complete Parameter Database (Excel):**
   - Comprehensive parameter table: https://doi.org/10.5281/zenodo.11119532 (Heil 2024)
   - Contains ALL ERA5 parameters with codes, names, units, descriptions

4. **Programmatic Access (Python):**
   - CDS API: https://cds.climate.copernicus.eu/how-to-api
   - era5cli tool: https://era5cli.readthedocs.io/

---

## 🌍 DATASET CHARACTERISTICS

### **Spatial Coverage:**
- **Global:** All latitudes and longitudes
- **Grid:** Regular lat-lon 0.25° × 0.25° (≈31 km)
- **Native resolution:** Gaussian grid reduced to T1279 spectral truncation

### **Temporal Coverage:**
- **Period:** January 1940 - present
- **Frequency:** Hourly
- **Latency:** ~5 days (preliminary), ~3 months (final quality-assured)
- **Forecast variables:** Available at hours 06:00 and 18:00 UTC (12-hour accumulations)

### **Vertical Structure:**
- **Model levels:** 137 hybrid sigma-pressure levels (surface → 0.01 hPa / 80 km)
- **Pressure levels:** 37 standard isobaric levels (1000 → 1 hPa)
- **Single levels:** Surface and near-surface (2m, 10m, 100m)

---

## 🌡️ SINGLE-LEVEL INSTANTANEOUS PARAMETERS (TABLE 2)

**Description:** Parameters available from **both analyses and forecasts** at specific time points
**Temporal Frequency:** Hourly (00:00, 01:00, ..., 23:00 UTC)

### **1. TEMPERATURE & HEAT PARAMETERS (10 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **2 metre temperature** | 2t | 167 | K | Air temperature at 2m above surface |
| **2 metre dewpoint temperature** | 2d | 168 | K | Dewpoint temperature at 2m |
| **Skin temperature** | skt | 235 | K | Surface skin temperature |
| **Soil temperature level 1** | stl1 | 139 | K | Soil temperature 0-7 cm depth |
| **Soil temperature level 2** | stl2 | 170 | K | Soil temperature 7-28 cm depth |
| **Soil temperature level 3** | stl3 | 183 | K | Soil temperature 28-100 cm depth |
| **Soil temperature level 4** | stl4 | 236 | K | Soil temperature 100-289 cm depth |
| **Sea surface temperature** | sst | 34 | K | SST (open water only) |
| **Ice temperature layer 1** | istl1 | 35 | K | Sea ice temperature (top layer) |
| **Ice temperature layer 4** | istl4 | 38 | K | Sea ice temperature (bottom layer) |

### **2. PRESSURE PARAMETERS (3 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Mean sea level pressure** | msl | 151 | Pa | Pressure reduced to sea level |
| **Surface pressure** | sp | 134 | Pa | Atmospheric pressure at surface |
| **Pressure at sea level** | psl | - | Pa | Alternative MSL pressure |

### **3. WIND PARAMETERS (8 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **10 metre U wind component** | 10u | 165 | m s⁻¹ | Eastward wind at 10m |
| **10 metre V wind component** | 10v | 166 | m s⁻¹ | Northward wind at 10m |
| **100 metre U wind component** | 100u | 228246 | m s⁻¹ | Eastward wind at 100m |
| **100 metre V wind component** | 100v | 228247 | m s⁻¹ | Northward wind at 100m |
| **Eastward turbulent surface stress** | ewss | 180 | N m⁻² s | Accumulated zonal momentum flux |
| **Northward turbulent surface stress** | nsss | 181 | N m⁻² s | Accumulated meridional momentum flux |
| **Vertical integral of divergence of moisture flux** | vidmf | 213 | kg m⁻² | Column-integrated moisture flux divergence |
| **Convective inhibition** | cin | 228001 | J kg⁻¹ | Energy preventing convection |

### **4. CLOUD PARAMETERS (10 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Total cloud cover** | tcc | 164 | 0-1 | Fraction of sky covered by clouds |
| **Low cloud cover** | lcc | 186 | 0-1 | Cloud cover below 2 km |
| **Medium cloud cover** | mcc | 187 | 0-1 | Cloud cover 2-6 km |
| **High cloud cover** | hcc | 188 | 0-1 | Cloud cover above 6 km |
| **Convective available potential energy** | cape | 59 | J kg⁻¹ | Energy available for convection |
| **Total column cloud liquid water** | tclw | 78 | kg m⁻² | Column-integrated liquid water |
| **Total column cloud ice water** | tciw | 79 | kg m⁻² | Column-integrated ice water |
| **Cloud base height** | cbh | 228023 | m | Height of cloud base |
| **Total column rain water** | tcrw | 228089 | kg m⁻² | Column-integrated rain |
| **Total column snow water** | tcsw | 228090 | kg m⁻² | Column-integrated snow |

### **5. SOIL MOISTURE PARAMETERS (7 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Volumetric soil water layer 1** | swvl1 | 39 | m³ m⁻³ | Soil moisture 0-7 cm |
| **Volumetric soil water layer 2** | swvl2 | 40 | m³ m⁻³ | Soil moisture 7-28 cm |
| **Volumetric soil water layer 3** | swvl3 | 41 | m³ m⁻³ | Soil moisture 28-100 cm |
| **Volumetric soil water layer 4** | swvl4 | 42 | m³ m⁻³ | Soil moisture 100-289 cm |
| **Soil type** | slt | 43 | class | FAO soil type classification |
| **Vegetation type** | tvl | 199 | % | Low vegetation cover |
| **Vegetation type** | tvh | 200 | % | High vegetation cover |

### **6. SNOW & ICE PARAMETERS (8 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Snow depth** | sd | 141 | m water equivalent | Depth of snow cover |
| **Snow density** | rsn | 33 | kg m⁻³ | Density of snowpack |
| **Snow albedo** | asn | 32 | 0-1 | Reflectivity of snow surface |
| **Snow evaporation** | es | 44 | m water equivalent | Snow sublimation |
| **Snowmelt** | smlt | 45 | m water equivalent | Melted snow |
| **Sea ice area fraction** | ci | 31 | 0-1 | Fraction of grid cell covered by ice |
| **Lake ice depth** | licd | 228013 | m | Thickness of ice on lakes |
| **Lake ice temperature** | lict | 228014 | K | Temperature of lake ice |

### **7. RADIATION & ALBEDO PARAMETERS (8 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Forecast albedo** | fal | 243 | 0-1 | Surface albedo |
| **UV visible albedo for direct radiation** | aluvp | 15 | 0-1 | UV-visible direct albedo |
| **UV visible albedo for diffuse radiation** | aluvd | 16 | 0-1 | UV-visible diffuse albedo |
| **Near IR albedo for direct radiation** | alnip | 17 | 0-1 | Near-infrared direct albedo |
| **Near IR albedo for diffuse radiation** | alnid | 18 | 0-1 | Near-infrared diffuse albedo |
| **Clear-sky direct solar radiation at surface** | cdir | 228021 | J m⁻² | Direct shortwave flux (clear sky) |
| **Total sky direct solar radiation at surface** | dir | 228022 | J m⁻² | Direct shortwave flux (all sky) |
| **Downward UV radiation at the surface** | uvb | 57 | J m⁻² | UV-B radiation |

### **8. BOUNDARY LAYER & TURBULENCE (7 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Boundary layer height** | blh | 159 | m | Height of planetary boundary layer |
| **Boundary layer dissipation** | bld | 145 | J m⁻² | Turbulent kinetic energy dissipation |
| **Friction velocity** | zust | 228003 | m s⁻¹ | Surface friction velocity |
| **Instantaneous moisture flux** | ie | 229 | kg m⁻² s⁻¹ | Vertical moisture transport |
| **Instantaneous eastward turbulent surface stress** | iews | 230 | N m⁻² | Instantaneous zonal stress |
| **Instantaneous northward turbulent surface stress** | inss | 231 | N m⁻² | Instantaneous meridional stress |
| **Convective available potential energy** | cape | 59 | J kg⁻¹ | CAPE for parcel ascent |

### **9. OCEAN & WAVE PARAMETERS (8 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Significant height of combined wind waves and swell** | swh | 140 | m | Wave height |
| **Mean wave direction** | mwd | 230 | degrees | Direction waves are traveling |
| **Mean wave period** | mwp | 232 | s | Average wave period |
| **Coefficient of drag with waves** | cdww | 148 | dimensionless | Surface drag coefficient |
| **Ocean surface stress equivalent 10m U wind** | ocu | 151162 | m s⁻¹ | U wind from ocean stress |
| **Ocean surface stress equivalent 10m V wind** | ocv | 151163 | m s⁻¹ | V wind from ocean stress |
| **10 metre wind speed** | si10 | 207 | m s⁻¹ | Wind speed magnitude at 10m |
| **Normalized energy flux into ocean** | phioc | 151144 | W m⁻² | Energy transfer to ocean |

### **10. GEOPOTENTIAL & TOPOGRAPHY (4 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Geopotential** | z | 129 | m² s⁻² | Gravitational potential × g |
| **Orography** | oro | 228002 | m | Model surface elevation |
| **Land-sea mask** | lsm | 172 | 0-1 | 1=land, 0=sea/lake |
| **Lake cover** | cl | 26 | 0-1 | Fraction covered by lakes |

### **11. ADDITIONAL INSTANTANEOUS PARAMETERS (10 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Total column water** | tcw | 136 | kg m⁻² | Column-integrated water (vapor+liquid+ice) |
| **Total column water vapour** | tcwv | 137 | kg m⁻² | Column-integrated water vapor |
| **Total column ozone** | tco3 | 206 | kg m⁻² | Column-integrated ozone |
| **Total aerosol optical depth at 550nm** | aod550 | 207 | dimensionless | Aerosol extinction |
| **Vertical integral of mass tendency** | vimass | 214 | kg m⁻² | Column mass change |
| **Mean top net long-wave radiation flux, clear sky** | mtnlwrcs | 212 | W m⁻² | TOA LW clear-sky |
| **Mean top net short-wave radiation flux, clear sky** | mtnswrcs | 213 | W m⁻² | TOA SW clear-sky |
| **Charnock** | chnk | 148 | dimensionless | Sea surface roughness parameter |
| **Total column supercooled liquid water** | tcslw | 228246 | kg m⁻² | Supercooled liquid |
| **Visibility** | vis | 3020 | m | Horizontal visibility distance |

---

## ☔ SINGLE-LEVEL FORECAST PARAMETERS - ACCUMULATED (TABLE 3)

**Description:** Cumulative totals from start of forecast to specified time
**Availability:** Forecast only (hours 06:00, 18:00 UTC)
**Accumulation Period:** Previous 1-hour, 3-hour, 6-hour, or 12-hour depending on forecast step

### **1. PRECIPITATION PARAMETERS (7 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Total precipitation** | tp | 228 | m | Total rain + snow (liquid equivalent) |
| **Large scale precipitation** | lsp | 142 | m | Stratiform precipitation |
| **Convective precipitation** | cp | 143 | m | Convective precipitation |
| **Snowfall** | sf | 144 | m water equivalent | Snow accumulation |
| **Precipitation type** | ptype | 260015 | code | 0=none, 1=rain, 3=freezing rain, 5=snow, 6=wet snow, 7=mixture, 8=ice pellets |
| **Total column rain water** | tcrw | 228089 | kg m⁻² | Instantaneous (not accumulated) |
| **Total column snow water** | tcsw | 228090 | kg m⁻² | Instantaneous (not accumulated) |

### **2. RADIATION PARAMETERS - SURFACE (12 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Surface solar radiation downwards** | ssrd | 169 | J m⁻² | Incoming shortwave at surface |
| **Surface thermal radiation downwards** | strd | 175 | J m⁻² | Incoming longwave at surface |
| **Surface net solar radiation** | ssr | 176 | J m⁻² | Net shortwave at surface |
| **Surface net thermal radiation** | str | 177 | J m⁻² | Net longwave at surface |
| **Surface solar radiation downwards, clear sky** | ssrdc | 228019 | J m⁻² | SW down (no clouds) |
| **Surface thermal radiation downwards, clear sky** | strdc | 228020 | J m⁻² | LW down (no clouds) |
| **Surface net solar radiation, clear sky** | ssrc | 210 | J m⁻² | Net SW (no clouds) |
| **Surface net thermal radiation, clear sky** | strc | 211 | J m⁻² | Net LW (no clouds) |
| **Photosynthetically active radiation at the surface** | par | 58 | J m⁻² | PAR (400-700 nm) |
| **UV visible albedo for direct radiation** | aluvp | 15 | 0-1 | UV direct albedo |
| **UV visible albedo for diffuse radiation** | aluvd | 16 | 0-1 | UV diffuse albedo |
| **Clear-sky direct solar radiation at surface** | cdir | 228021 | J m⁻² | Direct SW (no clouds) |

### **3. RADIATION PARAMETERS - TOP OF ATMOSPHERE (8 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Top net solar radiation** | tsr | 178 | J m⁻² | Net SW at TOA |
| **Top net thermal radiation** | ttr | 179 | J m⁻² | Net LW (OLR) at TOA |
| **TOA incident solar radiation** | tisr | 212 | J m⁻² | Incoming SW at TOA |
| **Top net solar radiation, clear sky** | tsrc | 208 | J m⁻² | Net SW TOA (no clouds) |
| **Top net thermal radiation, clear sky** | ttrc | 209 | J m⁻² | Net LW TOA (no clouds) |
| **Top downward solar radiation** | tdsr | 228022 | J m⁻² | Incoming SW at TOA |
| **Total sky direct solar radiation at surface** | fdir | 228022 | J m⁻² | Direct SW (all sky) |
| **Downward UV radiation at the surface** | uvb | 57 | J m⁻² | UV-B |

### **4. ENERGY FLUX PARAMETERS (8 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Surface sensible heat flux** | sshf | 146 | J m⁻² | Upward sensible heat |
| **Surface latent heat flux** | slhf | 147 | J m⁻² | Upward latent heat (evaporation) |
| **Evaporation** | e | 182 | m water equivalent | Total evapotranspiration |
| **Potential evaporation** | pev | 228251 | m | Potential ET |
| **Surface runoff** | sro | 8 | m | Overland flow |
| **Sub-surface runoff** | ssro | 9 | m | Subsurface drainage |
| **Total column vertically-integrated water vapour flux** | p71.162 | - | kg m⁻¹ s⁻¹ | Horizontal moisture transport |
| **Vertical integral of divergence of cloud water flux** | p84.162 | - | kg m⁻² | Cloud water flux divergence |

### **5. HYDROLOGY PARAMETERS (5 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Runoff** | ro | 205 | m | Total runoff (surface + subsurface) |
| **Snow evaporation** | es | 44 | m water equivalent | Snow sublimation |
| **Snowmelt** | smlt | 45 | m water equivalent | Melted snow |
| **Vertical integral of divergence of moisture flux** | p71.162 | - | kg m⁻² | Column moisture flux divergence |
| **Vertical integral of eastward water vapour flux** | p88.162 | - | kg m⁻¹ s⁻¹ | Zonal moisture transport |

### **6. MOMENTUM & STRESS PARAMETERS (4 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Eastward turbulent surface stress** | ewss | 180 | N m⁻² s | Accumulated zonal momentum flux |
| **Northward turbulent surface stress** | nsss | 181 | N m⁻² s | Accumulated meridional momentum flux |
| **Eastward gravity wave surface stress** | lgws | 195 | N m⁻² s | Gravity wave zonal stress |
| **Northward gravity wave surface stress** | mgws | 196 | N m⁻² s | Gravity wave meridional stress |

### **7. CLOUD & CONVECTION PARAMETERS (6 variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Convective available potential energy** | cape | 59 | J kg⁻¹ | CAPE |
| **Convective inhibition** | cin | 228001 | J kg⁻¹ | CIN |
| **Boundary layer dissipation** | bld | 145 | J m⁻² | Turbulent dissipation |
| **Vertical integral of divergence of cloud water flux** | p84.162 | - | kg m⁻² | Cloud flux divergence |
| **Vertical integral of divergence of geopotential flux** | p73.162 | - | W m⁻² | Geopotential flux divergence |
| **Vertical integral of divergence of thermal flux** | p74.162 | - | W m⁻² | Thermal flux divergence |

---

## ⏱️ SINGLE-LEVEL FORECAST PARAMETERS - MEAN RATES (TABLE 4)

**Description:** Average rates over accumulation period (per second units)
**Availability:** Forecast only
**Units:** Similar to Table 3 but divided by seconds (e.g., m s⁻¹ instead of m)

### **Mean Rate Parameters (30+ variables)**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Mean total precipitation rate** | mtpr | 235055 | kg m⁻² s⁻¹ | Average precipitation rate |
| **Mean convective precipitation rate** | mcpr | 235030 | kg m⁻² s⁻¹ | Average convective precip rate |
| **Mean large-scale precipitation rate** | mlspr | 235029 | kg m⁻² s⁻¹ | Average stratiform precip rate |
| **Mean snowfall rate** | msr | 235020 | kg m⁻² s⁻¹ | Average snowfall rate |
| **Mean surface sensible heat flux** | msshf | 235033 | W m⁻² | Average sensible heat |
| **Mean surface latent heat flux** | mslhf | 235034 | W m⁻² | Average latent heat |
| **Mean evaporation rate** | mer | 235043 | kg m⁻² s⁻¹ | Average evaporation rate |
| **Mean runoff rate** | mror | 235048 | kg m⁻² s⁻¹ | Average runoff rate |
| **Mean surface runoff rate** | msror | 235020 | kg m⁻² s⁻¹ | Average surface runoff |
| **Mean sub-surface runoff rate** | mssror | 235021 | kg m⁻² s⁻¹ | Average subsurface runoff |
| **Mean eastward turbulent surface stress** | metss | 235041 | N m⁻² | Average zonal stress |
| **Mean northward turbulent surface stress** | mntss | 235042 | N m⁻² | Average meridional stress |
| **Mean boundary layer dissipation** | mbld | 235032 | W m⁻² | Average turbulent dissipation |
| **Mean surface downward short-wave radiation flux** | msdwswrf | 235035 | W m⁻² | Average SW down |
| **Mean surface downward long-wave radiation flux** | msdwlwrf | 235036 | W m⁻² | Average LW down |
| **Mean surface net short-wave radiation flux** | msnswrf | 235037 | W m⁻² | Average net SW surface |
| **Mean surface net long-wave radiation flux** | msnlwrf | 235038 | W m⁻² | Average net LW surface |
| **Mean top net short-wave radiation flux** | mtnswrf | 235039 | W m⁻² | Average net SW TOA |
| **Mean top net long-wave radiation flux** | mtnlwrf | 235040 | W m⁻² | Average net LW TOA |

**Note:** Multiply mean rate by 86,400 seconds to get daily total. Example: mtpr × 86400 = daily precipitation in mm.

---

## 📊 SINGLE-LEVEL FORECAST PARAMETERS - MIN/MAX (TABLE 5)

**Description:** Extreme values during accumulation period
**Availability:** Forecast only

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Maximum temperature at 2 metres** | mx2t | 201 | K | Max 2m temp since last post-processing |
| **Minimum temperature at 2 metres** | mn2t | 202 | K | Min 2m temp since last post-processing |
| **10 metre wind gust** | 10fg | 49 | m s⁻¹ | Max wind gust at 10m |
| **Maximum total precipitation rate** | mxtpr | 228226 | kg m⁻² s⁻¹ | Max precipitation rate |
| **Minimum total precipitation rate** | mntpr | 228227 | kg m⁻² s⁻¹ | Min precipitation rate |

---

## 🏔️ PRESSURE-LEVEL PARAMETERS (16 variables × 37 levels)

**Description:** Atmospheric variables on standard isobaric surfaces
**Pressure Levels (37 total):** 1000, 975, 950, 925, 900, 875, 850, 825, 800, 775, 750, 700, 650, 600, 550, 500, 450, 400, 350, 300, 250, 225, 200, 175, 150, 125, 100, 70, 50, 30, 20, 10, 7, 5, 3, 2, 1 hPa

### **Core Pressure-Level Variables**

| Parameter | Short Name | ParamID | Units | Description |
|-----------|------------|---------|-------|-------------|
| **Geopotential** | z | 129 | m² s⁻² | Geopotential height × g (divide by 9.80665 for meters) |
| **Temperature** | t | 130 | K | Air temperature |
| **U component of wind** | u | 131 | m s⁻¹ | Eastward wind |
| **V component of wind** | v | 132 | m s⁻¹ | Northward wind |
| **Vertical velocity** | w | 135 | Pa s⁻¹ | Omega (pressure vertical velocity) |
| **Relative humidity** | r | 157 | % | Relative humidity |
| **Specific humidity** | q | 133 | kg kg⁻¹ | Water vapor mixing ratio |
| **Vorticity (relative)** | vo | 138 | s⁻¹ | Relative vorticity |
| **Divergence** | d | 155 | s⁻¹ | Horizontal divergence |
| **Ozone mass mixing ratio** | o3 | 203 | kg kg⁻¹ | Ozone concentration |
| **Potential vorticity** | pv | 60 | K m² kg⁻¹ s⁻¹ | Ertel's potential vorticity |
| **Specific cloud liquid water content** | clwc | 246 | kg kg⁻¹ | Liquid water in clouds |
| **Specific cloud ice water content** | ciwc | 247 | kg kg⁻¹ | Ice water in clouds |
| **Fraction of cloud cover** | cc | 248 | 0-1 | Cloud fraction |
| **Specific rain water content** | crwc | 75 | kg kg⁻¹ | Rain water |
| **Specific snow water content** | cswc | 76 | kg kg⁻¹ | Snow water |

**Total Pressure-Level Variables:** 16 parameters × 37 levels = **592 pressure-level fields**

---

## 🌱 ERA5-LAND SPECIFIC PARAMETERS (50+ variables)

**Description:** Enhanced land-surface parameters at higher spatial resolution (9 km)
**Dataset:** ERA5-Land hourly data
**Spatial Resolution:** 0.1° × 0.1° (≈9 km)

### **Additional Land Parameters (not in standard ERA5):**

| Parameter | Short Name | Units | Description |
|-----------|------------|-------|-------------|
| **Leaf area index, high vegetation** | lai_hv | m² m⁻² | High vegetation LAI |
| **Leaf area index, low vegetation** | lai_lv | m² m⁻² | Low vegetation LAI |
| **Skin reservoir content** | src | m water equivalent | Water on canopy |
| **Soil heat flux** | - | J m⁻² | Heat flux into soil |
| **Field capacity** | fc | m³ m⁻³ | Soil moisture at field capacity |
| **Wilting point** | wp | m³ m⁻³ | Soil moisture at wilting point |

---

## 🔍 HOW TO USE ERA5 DATA FOR COUNTY-LEVEL RESEARCH

### **Step 1: Register for CDS API Access**

```bash
# Install CDS API client
pip install cdsapi

# Create ~/.cdsapirc with credentials from:
# https://cds.climate.copernicus.eu/how-to-api

# File contents:
# url: https://cds.climate.copernicus.eu/api
# key: YOUR-UID:YOUR-API-KEY
```

---

### **Step 2: Download ERA5 Data for US Counties**

```python
import cdsapi
import pandas as pd
import numpy as np
from datetime import datetime

# Initialize CDS API
c = cdsapi.Client()

# Define US bounding box
us_bbox = {
    'north': 50,    # Canada border
    'west': -125,   # West coast
    'south': 24,    # Southern border
    'east': -66     # East coast
}

# Download ERA5 single-level data for 2020
c.retrieve(
    'reanalysis-era5-single-levels',
    {
        'product_type': 'reanalysis',
        'format': 'netcdf',
        'variable': [
            '2m_temperature',
            'total_precipitation',
            '10m_u_component_of_wind',
            '10m_v_component_of_wind',
            'surface_pressure',
            '2m_dewpoint_temperature',
            'mean_sea_level_pressure'
        ],
        'year': '2020',
        'month': ['01', '02', '03', '04', '05', '06',
                  '07', '08', '09', '10', '11', '12'],
        'day': [f'{d:02d}' for d in range(1, 32)],
        'time': ['00:00', '06:00', '12:00', '18:00'],
        'area': [us_bbox['north'], us_bbox['west'],
                 us_bbox['south'], us_bbox['east']],
    },
    'era5_us_2020.nc'
)
```

---

### **Step 3: Extract County-Level Statistics**

```python
import xarray as xr
import geopandas as gpd
from rasterstats import zonal_stats
import rasterio

# Load ERA5 NetCDF
ds = xr.open_dataset('era5_us_2020.nc')

# Load US county boundaries
counties = gpd.read_file('tl_2020_us_county.shp')

# Convert temperature from Kelvin to Celsius
ds['t2m_celsius'] = ds['t2m'] - 273.15

# Calculate daily means from hourly data
daily_temp = ds['t2m_celsius'].resample(time='1D').mean()

# Calculate annual county averages
for idx, county in counties.iterrows():
    fips = county['GEOID']
    geometry = county['geometry']

    # Extract time series for county polygon
    county_data = daily_temp.rio.clip([geometry], counties.crs)

    # Calculate county-wide spatial mean for each day
    county_ts = county_data.mean(dim=['latitude', 'longitude'])

    # Annual statistics
    counties.loc[idx, 'temp_mean_2020'] = float(county_ts.mean())
    counties.loc[idx, 'temp_min_2020'] = float(county_ts.min())
    counties.loc[idx, 'temp_max_2020'] = float(county_ts.max())
    counties.loc[idx, 'temp_std_2020'] = float(county_ts.std())
```

---

### **Step 4: Calculate Additional Climate Metrics**

```python
# Calculate derived variables

# 1. Precipitation (convert from meters to mm, accumulate)
precip_daily = ds['tp'].resample(time='1D').sum() * 1000  # m → mm
precip_annual = precip_daily.sum(dim='time')

# 2. Wind speed from U and V components
wind_speed = np.sqrt(ds['u10']**2 + ds['v10']**2)
wind_speed_daily = wind_speed.resample(time='1D').mean()

# 3. Relative humidity from temperature and dewpoint
def calculate_rh(temp_k, dewpoint_k):
    """Calculate relative humidity from temperature and dewpoint"""
    e_sat = 611.2 * np.exp(17.67 * (temp_k - 273.15) / (temp_k - 29.65))
    e_actual = 611.2 * np.exp(17.67 * (dewpoint_k - 273.15) / (dewpoint_k - 29.65))
    return 100 * e_actual / e_sat

rh = calculate_rh(ds['t2m'], ds['d2m'])
rh_daily = rh.resample(time='1D').mean()

# 4. Heat index (apparent temperature)
def heat_index(temp_f, rh):
    """Calculate heat index in Fahrenheit"""
    hi = -42.379 + 2.04901523*temp_f + 10.14333127*rh \
         - 0.22475541*temp_f*rh - 6.83783e-3*temp_f**2 \
         - 5.481717e-2*rh**2 + 1.22874e-3*temp_f**2*rh \
         + 8.5282e-4*temp_f*rh**2 - 1.99e-6*temp_f**2*rh**2
    return hi

temp_f = ds['t2m_celsius'] * 9/5 + 32
heat_idx = heat_index(temp_f, rh)

# 5. Growing degree days (base 10°C)
gdd = (daily_temp - 10).where(daily_temp > 10, 0).sum(dim='time')

# 6. Frost days (Tmin < 0°C)
daily_min = ds['t2m_celsius'].resample(time='1D').min()
frost_days = (daily_min < 0).sum(dim='time')

# 7. Extreme heat days (Tmax > 35°C)
daily_max = ds['t2m_celsius'].resample(time='1D').max()
heat_days = (daily_max > 35).sum(dim='time')
```

---

### **Step 5: Aggregate to County Level**

```python
# Create county-level summary dataset
county_climate = []

for idx, county in counties.iterrows():
    fips = county['GEOID']
    geom = [county['geometry']]

    # Spatial statistics for each variable
    stats = {
        'GEOID': fips,
        'year': 2020,

        # Temperature
        'temp_mean': float(zonal_stats(geom, daily_temp.mean('time'), stats='mean')[0]['mean']),
        'temp_min': float(zonal_stats(geom, daily_min.min('time'), stats='min')[0]['min']),
        'temp_max': float(zonal_stats(geom, daily_max.max('time'), stats='max')[0]['max']),

        # Precipitation
        'precip_total_mm': float(zonal_stats(geom, precip_annual, stats='mean')[0]['mean']),
        'precip_days': float(zonal_stats(geom, (precip_daily > 1).sum('time'), stats='mean')[0]['mean']),

        # Wind
        'wind_speed_mean': float(zonal_stats(geom, wind_speed_daily.mean('time'), stats='mean')[0]['mean']),

        # Humidity
        'rh_mean': float(zonal_stats(geom, rh_daily.mean('time'), stats='mean')[0]['mean']),

        # Derived indices
        'gdd_base10': float(zonal_stats(geom, gdd, stats='mean')[0]['mean']),
        'frost_days': float(zonal_stats(geom, frost_days, stats='mean')[0]['mean']),
        'heat_days_35c': float(zonal_stats(geom, heat_days, stats='mean')[0]['mean']),
    }

    county_climate.append(stats)

# Convert to DataFrame
climate_df = pd.DataFrame(county_climate)
climate_df.to_csv('era5_county_climate_2020.csv', index=False)
```

---

### **Step 6: Time Series Analysis**

```python
# Extract daily time series for specific county
travis_county = counties[counties['GEOID'] == '48453']  # Travis County, TX

# Clip ERA5 data to county
county_ts = ds.rio.clip(travis_county.geometry, travis_county.crs)

# Calculate county-mean daily time series
travis_daily = county_ts.mean(dim=['latitude', 'longitude'])

# Convert to pandas DataFrame
travis_df = travis_daily.to_dataframe().reset_index()

# Calculate weekly/monthly aggregations
travis_weekly = travis_df.resample('W', on='time').mean()
travis_monthly = travis_df.resample('ME', on='time').mean()

# Extreme event analysis
heatwave_threshold = travis_df['t2m_celsius'].quantile(0.95)
heatwave_days = (travis_df['t2m_celsius'] > heatwave_threshold).sum()

cold_snap_threshold = travis_df['t2m_celsius'].quantile(0.05)
cold_snap_days = (travis_df['t2m_celsius'] < cold_snap_threshold).sum()
```

---

## 📚 COMPANION REANALYSIS DATASETS

### **ECMWF/Copernicus Family:**

**ERA5-Land:**
- Higher resolution land surface (9 km vs 31 km)
- Enhanced soil, vegetation, hydrological variables
- Portal: https://cds.climate.copernicus.eu/datasets/reanalysis-era5-land

**Copernicus Atmosphere Monitoring Service (CAMS):**
- Atmospheric composition (pollutants, aerosols, greenhouse gases)
- 50+ chemical species
- Portal: https://ads.atmosphere.copernicus.eu/

---

## 📈 TEMPORAL & SPATIAL COVERAGE

| Attribute | Details |
|-----------|---------|
| **Temporal Coverage** | January 1940 - present (daily updates) |
| **Temporal Resolution** | Hourly (00:00 to 23:00 UTC) |
| **Latency** | ~5 days (preliminary), ~3 months (quality-assured) |
| **Spatial Coverage** | Global (90°N to 90°S, 180°W to 180°E) |
| **Spatial Resolution** | 0.25° × 0.25° (≈31 km at equator) |
| **Vertical Levels** | 137 model levels (surface → 80 km) |
| **Pressure Levels** | 37 standard isobaric surfaces (1000 → 1 hPa) |
| **Update Frequency** | Daily (preliminary), monthly (final) |

---

## ⚠️ DATA QUALITY & LIMITATIONS

### **Strengths:**
- Most comprehensive global reanalysis available
- Consistent long-term record (1940-present)
- Hourly temporal resolution
- High spatial resolution (31 km)
- Incorporates observations from millions of sources
- Quality-controlled and bias-corrected

### **Limitations:**
- **Reanalysis, not observations:** Model-generated estimates constrained by observations
- **Forecast parameters:** Accumulated variables (precipitation, radiation) less reliable than analyses
- **Spatial resolution:** 31 km may not capture local topographic effects
- **Observation density:** Fewer observations in early years (pre-1979 satellite era)
- **Precipitation accuracy:** Known biases in complex terrain and tropical regions
- **Derived variables:** Relative humidity, heat index calculated from model output
- **County boundaries:** Aggregation to irregular county shapes requires spatial processing

---

## 📝 CITATION

**When using ERA5 data, cite:**

> Hersbach, H., Bell, B., Berrisford, P., Biavati, G., Horányi, A., Muñoz Sabater, J., Nicolas, J., Peubey, C., Radu, R., Rozum, I., Schepers, D., Simmons, A., Soci, C., Dee, D., Thépaut, J-N. (2023): ERA5 hourly data on single levels from 1940 to present. Copernicus Climate Change Service (C3S) Climate Data Store (CDS). DOI: 10.24381/cds.adbb2d47

> Hersbach, H., Bell, B., Berrisford, P., Hirahara, S., Horányi, A., Muñoz‐Sabater, J., Nicolas, J., Peubey, C., Radu, R., Schepers, D., Simmons, A., Soci, C., Abdalla, S., Abellan, X., Balsamo, G., Bechtold, P., Biavati, G., Bidlot, J., Bonavita, M., De Chiara, G., Dahlgren, P., Dee, D., Diamantakis, M., Dragani, R., Flemming, J., Forbes, R., Fuentes, M., Geer, A., Haimberger, L., Healy, S., Hogan, R.J., Hólm, E., Janisková, M., Keeley, S., Laloyaux, P., Lopez, P., Lupu, C., Radnoti, G., de Rosnay, P., Rozum, I., Vamborg, F., Villaume, S., Thépaut, J.-N. (2020): The ERA5 global reanalysis. Quarterly Journal of the Royal Meteorological Society, 146(730), pp. 1999-2049. DOI: 10.1002/qj.3803

**For ERA5-Land:**

> Muñoz Sabater, J. (2019): ERA5-Land hourly data from 1950 to present. Copernicus Climate Change Service (C3S) Climate Data Store (CDS). DOI: 10.24381/cds.e2161bac

---

**Last Updated:** November 13, 2025
**Dataset Version:** ERA5 (continuous updates)
**Total Parameters:** ~240 variables (70 single-level instantaneous + 60 accumulated/forecast + 20 mean rates + 5 min/max + 16 pressure-level × 37 levels)
