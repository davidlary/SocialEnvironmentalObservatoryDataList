# CHANGELOG - Version 4.2
## November 21, 2025 - Regulatory & Status Updates

**Update Type:** Regulatory changes and data source status updates
**Days Since V4.1:** 8 days
**Time Investment:** 3.5 hours (comprehensive quarterly review)
**Updated By:** Claude Code + David Lary

---

## SUMMARY

Version 4.2 incorporates critical regulatory changes and data source status updates discovered through systematic quarterly maintenance review. While no new data sources were added, several important regulatory and access changes required documentation updates.

---

## CHANGES MADE

### 1. PFAS Drinking Water Standards (CRITICAL UPDATE) ⚠️

**File Updated:** `02_WATER/UV_WATER_SUPERFUND_COMPREHENSIVE.md`

**May 14, 2025 EPA Regulatory Rollback:**
- **RETAINED:** PFOA and PFOS at 4 ppt MCL
- **RESCINDED:** PFHxS, PFNA, GenX (HFPO-DA), PFBS, and Hazard Index
- **Compliance deadline extended:** 2029 → 2031

**Changes:**
- Updated PFAS regulations table with May 2025 status
- Added "Current Regulatory Status" section
- Updated compliance timeline
- Modified implications for SDWIS data (PFOA/PFOS only)
- Updated PFAS violations reference in Priority Variables section

**Impact:** County-level PFAS violation data will only track PFOA and PFOS, not the four rescinded compounds.

---

### 2. Air Quality Standards (NAAQS) Updates

**File Updated:** `01_AIR_ATMOSPHERE/ATMOSPHERIC_EMISSIONS_CHEMISTRY_COMPREHENSIVE.md`

**Regulatory Changes:**
- **SO2 Secondary Standard:** New 10 ppb annual standard (effective January 27, 2025)
- **PM2.5 Primary Standard:** Under reconsideration (2024 rule: 9.0 μg/m³; final decision February 2026)

**Changes:**
- Added "2025 Regulatory Updates" section to file header
- Updated "Last Updated" date to November 21, 2025
- Noted PM2.5 standard uncertainty

**Impact:** PM2.5 NAAQS remains uncertain pending EPA reconsideration.

---

### 3. NASA SEDAC Termination Notice ⚠️

**File Updated:** `23_INTERNATIONAL_SOURCES/INTERNATIONAL_CLIMATE_ATMOSPHERIC_SOURCES.md`

**NASA SEDAC Status:**
- Contract terminated April 30, 2025
- 350+ datasets archived (no longer updated)
- Data accessible via NASA Earthdata Cloud

**Changes:**
- Added termination notes to code examples referencing SEDAC GPW
- Suggested alternatives (LandScan, WorldPop)
- Updated "Last Updated" date to November 21, 2025

**Impact:** SEDAC gridded population data remains available but will not receive updates.

---

### 4. Documentation Updates

**Files Updated:**
- `README.md`
- `MASTER_INDEX.md`

**Changes:**
- **README.md:**
  - Version: 4.1 → 4.2
  - Last Updated: November 13, 2025 → November 21, 2025
  - Added V4.2 to Version History table
  - Updated "Next Update" to 4.3 (Q1 2026)

- **MASTER_INDEX.md:**
  - Version: 4.1 → 4.2
  - File count: 63 → 70 files (correction)
  - Last Updated: November 13, 2025 → November 21, 2025

---

## FILES NOT REQUIRING UPDATES

### NLCD Annual Product
**Status:** Already current with Collection 1.1 (1985-2024)
**File:** `03_LAND_SOIL_GEOLOGY/NLCD_NOAA_STORMS_COMPREHENSIVE_DOCUMENTATION.md`
**Note:** Updated in V4.1 (November 13, 2025)

---

## KEY FINDINGS FROM QUARTERLY REVIEW

### New Research Identified (Not Requiring Repository Changes)

**1. PFAS & County-Level Cancer Study (January 2025)**
- Published: J. Exposure Science & Environmental Epidemiology
- Used SEER county-level cancer data + SDWIS PFAS data
- Found associations with endocrine, digestive, respiratory, oral, skin cancers
- **Validates:** Importance of county-level environmental health data catalogs

**2. Climate Change & Mortality (2025 Lancet Report)**
- 2003 heat wave patterns now would cause 17,800 deaths/week (vs. 9,000 originally)
- Extreme weather deaths vastly undercounted in official statistics

**3. Microplastics & Human Health (2025 Research)**
- Found in brain, heart, placenta, reproductive organs
- 68,000 particles inhaled daily per person
- **Data Gap:** No county-level microplastics monitoring exists yet

### Temporal Coverage Verified (All Current)
- NHGIS: ACS 2024 1-year in processing
- CDC WONDER: 2023 mortality (current)
- SEER Cancer: 2022 diagnoses (current)
- EPA TRI: 2023 (current)
- ERA5: October 2025 (current)
- NLCD: 1985-2024 Annual (current)

### Geographic Metadata Verified (No Changes)
- Virginia independent cities: Stable (38 cities)
- Alaska boroughs: Stable (19 boroughs, 11 census areas)
- US FIPS codes: No county name changes in 2025

---

## REPOSITORY STATISTICS (V4.2)

- **Total Files:** 70 markdown files
- **Repository Size:** 4.8 MB
- **File Size Check:** All files <100KB ✅
- **Directories:** 26 (00-25, all populated)
- **Links Tested:** 5 critical sources (all accessible)

---

## SOURCES CHECKED

**Federal Agencies Reviewed:**
- EPA (Environmental Protection Agency)
- USGS (US Geological Survey)
- CDC (Centers for Disease Control)
- NOAA (National Oceanic and Atmospheric Administration)
- Census Bureau
- USDA (Agriculture, NASS, ERS)
- NASA Earth Observations
- NIH/NCI/NIA Health Registries

**International Sources:**
- ECMWF (ERA5/CAMS)
- NASA SEDAC (terminated)

**Total Web Searches:** 20+
**Total Link Verifications:** 5 critical sources

---

## RECOMMENDATIONS FOR V4.3 (Q1 2026)

### Priority Items to Check (February 2026)
1. Census ACS 2024 1-year data (released December 2025)
2. Census ACS 2020-2024 5-year data (released December 2025)
3. PM2.5 NAAQS final rule (target February 2026)
4. NOAA climate data through 2025
5. Microplastics monitoring program development

### Sources to Watch
- EPA: EJScreen replacement/alternative
- CDC: Modernized WONDER platform
- Census: Experimental data products
- EPA: PFAS monitoring expansion

---

## VERSION CONTROL

- **Previous Version:** 4.1 (November 13, 2025)
- **Current Version:** 4.2 (November 21, 2025)
- **Next Version:** 4.3 (Target: February 2026)

---

## COMMIT MESSAGE

```
Quarterly maintenance update Q4 2025 (Version 4.2)

Regulatory and status updates following comprehensive quarterly review:

- Updated PFAS drinking water standards (May 2025 EPA rollback)
- Updated air quality standards (SO2 Jan 2025, PM2.5 under reconsideration)
- Added NASA SEDAC termination notes (April 2025)
- Updated README and MASTER_INDEX to V4.2
- Created comprehensive quarterly update report

Files modified:
- 02_WATER/UV_WATER_SUPERFUND_COMPREHENSIVE.md (PFAS regulations)
- 01_AIR_ATMOSPHERE/ATMOSPHERIC_EMISSIONS_CHEMISTRY_COMPREHENSIVE.md (NAAQS)
- 23_INTERNATIONAL_SOURCES/INTERNATIONAL_CLIMATE_ATMOSPHERIC_SOURCES.md (SEDAC)
- README.md (version 4.2)
- MASTER_INDEX.md (version 4.2)

New files:
- .maintenance/changelogs/QUARTERLY_UPDATE_REPORT_2025-11-21.md (10,000+ words)
- .maintenance/changelogs/CHANGELOG_2025-11-21_V4.2.md

Version: 4.1 → 4.2
Variables: 43,000+ (unchanged)
Data Sources: 200+ (unchanged)
Files: 70 markdown files

🤖 Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>
```

---

**Changelog Created:** November 21, 2025
**Created By:** Claude Code (Sonnet 4.5)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
