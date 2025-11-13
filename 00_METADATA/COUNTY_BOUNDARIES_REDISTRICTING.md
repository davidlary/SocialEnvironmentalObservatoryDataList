# County Boundaries & Redistricting
## Handling Geographic Changes in Longitudinal Data

**Purpose:** County boundaries change over time through mergers, splits, annexations, and creation of new counties. This document explains how to handle these changes when analyzing time series data.

**Critical for:** Any longitudinal analysis (e.g., 1990-2024 trends)

---

## ⚠️ Why This Matters

### The Problem

When analyzing county-level data over time, you may encounter:

1. **County mergers:** Two counties combine into one (Virginia independent cities ↔ counties)
2. **County splits:** One county divides into two (rare)
3. **New counties created:** County formed from parts of other counties
4. **Boundary annexations:** Cities annex unincorporated county land (common)
5. **Name changes:** County changes name (Shannon → Oglala Lakota, 2015)
6. **Census Area reorganization:** Especially in Alaska

**Example Issue:**
- 2000 data lists Clifton Forge city, VA (FIPS 51560) separately
- 2010 data does NOT include FIPS 51560 (merged into Alleghany County in 2001)
- **Simple time series comparison will MISS this population/data**

### The Solution

**Three approaches:**
1. **Use current boundaries** (backcast historical data to modern boundaries)
2. **Use historical boundaries** (track each boundary configuration separately)
3. **Exclude changed counties** (analyze only stable geographies)

This document provides the information needed for any approach.

---

## 📅 Major County Boundary Changes (1990-Present)

### Virginia Independent City Changes

Virginia has the most frequent county-level changes due to independent cities merging with adjacent counties or transitioning status.

#### Merged/Dissolved Cities

| FIPS | City/County | Action | Year | Merged Into |
|------|-------------|--------|------|-------------|
| 51560 | Clifton Forge city | Merged into county | 2001 | Alleghany County (51005) |
| 51780 | South Boston city | Reverted to town | 1995 | Halifax County (51083) |

**Data Implications:**
- **Before merger:** Data reported separately for city and county
- **After merger:** Data reported only for county (includes former city territory)
- **Solution:** Combine city + county for all pre-merger years to create consistent time series

#### Near-Future Potential Mergers

Several Virginia independent cities have explored merger with adjacent counties:
- Discussions ongoing for economic/efficiency reasons
- Monitor Virginia legislation for updates

### Alaska Census Area Changes

Alaska frequently reorganizes Census Areas as boroughs form or boundaries adjust.

#### Selected Alaska Changes

| FIPS | Area Name | Action | Year | Details |
|------|-----------|--------|------|---------|
| 02280 | Wrangell-Petersburg Census Area | Split | 2008 | → Wrangell City and Borough (02275) + Petersburg Census Area (02195) |
| 02195 | Petersburg Census Area | Borough formation | 2013 | → Petersburg Borough |
| 02270 | Wade Hampton Census Area | Renamed | 2015 | → Kusilvak Census Area |
| 02158 | Kusilvak Census Area | Current name | 2015+ | Same geography as former Wade Hampton |
| 02201 | Prince of Wales-Outer Ketchikan Census Area | Split | 2008 | → Prince of Wales-Hyder Census Area (02198) |
| 02232 | Skagway-Hoonah-Angoon Census Area | Split | 2007 | → Skagway Municipality (02230) + Hoonah-Angoon Census Area (02105) |
| 02261 | Valdez-Cordova Census Area | Split | 2019 | → Chugach Census Area (02063) + Copper River Census Area (02066) |

**Data Implications:**
- **Name changes ONLY:** Same geography, just different name (Wade Hampton → Kusilvak)
  - Solution: FIPS code stays the same; simple name lookup update
- **Splits:** Territory divided into 2+ new FIPS codes
  - Solution: For historical consistency, must COMBINE the new areas when analyzing pre-split years

### South Dakota County Name Change

| FIPS | Old Name | New Name | Year |
|------|----------|----------|------|
| 46102 | Shannon County | Oglala Lakota County | 2015 |

**Data Implications:**
- Same geography and FIPS code
- Only name changed
- Pre-2015 data labeled "Shannon County"
- Post-2015 data labeled "Oglala Lakota County"

**Solution:** FIPS-based matching avoids the issue; name lookups need both names

---

## 🗺️ Independent City Status Changes (Virginia)

### How Independent Cities Work

In Virginia:
- **Independent city** = separate from any county (own FIPS code)
- **Town** = within a county (no separate FIPS code)

**Status transitions:**
- City → Town (becomes part of county) = **merger**
- Town → City (becomes independent) = **split from county**

### Historical Independent City Transitions

#### Cities That Became Towns (1990-Present)

| City | FIPS | Year | Action | Now Part Of |
|------|------|------|--------|-------------|
| South Boston | 51780 | 1995 | City → Town | Halifax County (51083) |
| Clifton Forge | 51560 | 2001 | City → Town | Alleghany County (51005) |

#### Town → City Transitions

| City | FIPS | Year | Action | Split From |
|------|------|------|--------|------------|
| Norton | 51720 | 1954 | Town → City | Wise County (51195) |
| (None since 1990) | | | | |

**Data handling:**
- When city becomes town: Add city data to county for pre-transition years
- When town becomes city: Subtract city data from county for post-transition years

---

## 📏 Boundary Annexations (City Expansion)

### What Are Annexations?

**Annexation:** A city (or independent city) expands its boundaries by incorporating adjacent unincorporated county land.

**Characteristics:**
- Happens continuously (especially in fast-growing areas)
- Does NOT create/destroy FIPS codes
- Transfers population/land from county to city
- More common in the South and West

**Examples:**
- Austin, TX regularly annexes surrounding Travis County land
- Raleigh, NC annexes Wake County land
- Charlotte, NC annexes Mecklenburg County land

### Impact on County-Level Data

**Problem:** Population/area shifts between county and city within same county, but:
- Most county-level datasets report **total county** (including all cities)
- Some datasets report **county unincorporated area only**

**Key Question:** Does the dataset include incorporated cities or not?

**Common patterns:**
- **Census population:** Includes all cities (total county population)
- **County government data:** May exclude independent cities
- **Environmental monitoring:** Station locations may not align with annexation boundaries

**Solution:**
- Use **total county values** (including cities) for consistency
- Be cautious comparing "unincorporated county" over time

---

## 🔄 How to Handle Changes in Longitudinal Analysis

### Approach 1: Current Boundaries (Recommended)

**Use 2024 county boundaries for ALL years.**

**Method:**
- Identify all mergers/splits/creations
- For years BEFORE a change, aggregate the component counties to match current geography
- Creates consistent geographic units over time

**Example: Clifton Forge, VA**
```python
# For years 1990-2000 (before merger)
# Combine FIPS 51560 (Clifton Forge city) + 51005 (Alleghany County)
# Treat as single unit "Alleghany County" with 2001+ definition

combined_2000 = (
    df[df['FIPS'] == '51560']['value'] +  # Clifton Forge
    df[df['FIPS'] == '51005']['value']    # Alleghany
)
```

**Advantages:**
- All years use same geography → simple comparison
- Results interpretable with modern maps

**Disadvantages:**
- Historical data no longer matches historical boundaries exactly
- Requires manual coding of all changes

### Approach 2: Historical Boundaries

**Use the boundaries that existed in each year.**

**Method:**
- Track FIPS codes that existed in each year
- Allow number of counties to vary over time
- For dissolved counties, show as NA after dissolution

**Example: Clifton Forge, VA**
```
Year 2000: 51560 (Clifton Forge) + 51005 (Alleghany) = 2 separate counties
Year 2010: Only 51005 (Alleghany, now includes former Clifton Forge) = 1 county
```

**Advantages:**
- Data matches the actual administrative reality of each year
- No need to combine/split data

**Disadvantages:**
- Panel data has unbalanced geography (counties appear/disappear)
- Difficult to interpret trends when units change
- Mapping requires year-specific boundary files

### Approach 3: Exclude Changed Counties

**Analyze only counties with stable boundaries 1990-present.**

**Method:**
- Create list of all counties that underwent changes
- Exclude them from analysis
- Analyze ~3,100 stable counties

**Example: Exclusion list**
- Virginia: 51560, 51780, 51005, 51083 (changed due to city mergers)
- Alaska: Multiple census areas (splits/reorganizations)
- Total excluded: ~50 counties/areas

**Advantages:**
- Clean, consistent geographic units
- No data manipulation required

**Disadvantages:**
- Loses information from changed counties
- Results not generalizable to all US counties
- Still covers >98% of counties

---

## 📁 Obtaining Historical Boundary Files

### Census TIGER/Line Shapefiles

**Source:** https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

**Available years:**
- Annual files: 2007-present
- Decadal files: 1990, 2000, 2010, 2020

**File types:**
- Counties: `tl_YYYY_us_county`
- Example: `tl_2020_us_county.shp`

**Python example:**
```python
import geopandas as gpd

# Load county boundaries for specific year
counties_2000 = gpd.read_file("tl_2000_us_county.shp")
counties_2020 = gpd.read_file("tl_2020_us_county.shp")

# Compare FIPS codes
fips_2000 = set(counties_2000['GEOID'])
fips_2020 = set(counties_2020['GEOID'])

# Counties that existed in 2000 but not 2020 (dissolved)
dissolved = fips_2000 - fips_2020
print(f"Dissolved: {dissolved}")

# Counties that exist in 2020 but not 2000 (created)
created = fips_2020 - fips_2000
print(f"Created: {created}")
```

### NHGIS (National Historical GIS)

**Source:** https://www.nhgis.org/

**Features:**
- Historical census boundaries back to 1790
- Includes historical county changes
- Provides crosswalks for aggregating historical data to modern boundaries

**Advantage:**
- Pre-built crosswalks save time
- Harmonized boundaries for longitudinal analysis

---

## 📋 Comprehensive List of County Changes (1990-2024)

### By State

#### Alaska
- **Multiple splits and reorganizations** (see table above)
- Most common state for changes

#### Virginia
- **Clifton Forge city** (51560) → Alleghany County (51005), 2001
- **South Boston city** (51780) → Halifax County (51083), 1995

#### South Dakota
- **Shannon County** → **Oglala Lakota County**, 2015 (name only, same FIPS 46102)

#### Other States
- **Montana, New Mexico:** Minor boundary adjustments between counties (land area only, no population impact)
- **Hawaii:** Minor adjustments between Census County Divisions

### Summary Statistics

**1990-2024:**
- **~15-20 significant changes** affecting county FIPS codes
- **~50 minor boundary adjustments** (land area only, minimal population impact)
- **Most common:** Alaska Census Area reorganizations
- **Second most common:** Virginia independent city status changes

**Result:** >99% of US counties have stable boundaries 1990-2024

---

## 💻 Code Examples: Handling Boundary Changes

### Creating Consistent Time Series (Python)

```python
import pandas as pd

# Load county data for multiple years
df = pd.read_csv('county_panel.csv')  # Columns: year, FIPS, value

# Define mergers (component FIPScombine → result FIPS)
mergers = {
    2001: {'51560': '51005', '51005': '51005'},  # Clifton Forge → Alleghany
    1995: {'51780': '51083', '51083': '51083'},  # South Boston → Halifax
}

# Function to aggregate pre-merger years
def harmonize_boundaries(df, mergers):
    df_harmonized = df.copy()

    for merge_year, mapping in mergers.items():
        # For years before merger
        pre_merge = df_harmonized['year'] < merge_year

        # Group dissolved FIPS into receiving FIPS
        for old_fips, new_fips in mapping.items():
            mask = pre_merge & (df_harmonized['FIPS'] == old_fips)
            df_harmonized.loc[mask, 'FIPS'] = new_fips

        # Sum values within each group-year
        df_harmonized = df_harmonized.groupby(
            ['year', 'FIPS'], as_index=False
        )['value'].sum()

    return df_harmonized

# Apply harmonization
df_consistent = harmonize_boundaries(df, mergers)
```

### Creating Exclusion List

```python
# Counties with any boundary change 1990-2024
changed_counties = [
    '51560',  # Clifton Forge city, VA (dissolved 2001)
    '51780',  # South Boston city, VA (dissolved 1995)
    '51005',  # Alleghany County, VA (absorbed Clifton Forge)
    '51083',  # Halifax County, VA (absorbed South Boston)
    '02270',  # Wade Hampton CA, AK (renamed 2015)
    '02158',  # Kusilvak CA, AK (renamed from Wade Hampton)
    '02280',  # Wrangell-Petersburg CA, AK (split 2008)
    '02275',  # Wrangell City and Borough, AK (created 2008)
    '02195',  # Petersburg Borough, AK (created 2013)
    # Add other Alaska changes...
]

# Filter to stable counties only
df_stable = df[~df['FIPS'].isin(changed_counties)]
```

---

## ✅ Checklist: Boundary Change Best Practices

Before longitudinal analysis:

- [ ] Decide on approach: current boundaries, historical boundaries, or exclude changes
- [ ] Identify all boundary changes in your time period
- [ ] Download TIGER/Line shapefiles for relevant years
- [ ] Create crosswalk or exclusion list
- [ ] Document your approach in methods
- [ ] Report number of counties excluded (if applicable)
- [ ] Check for Alaska Census Area changes
- [ ] Check for Virginia independent city changes
- [ ] Verify South Dakota Shannon/Oglala Lakota name consistency

---

## 📚 Additional Resources

1. **Census Boundary Changes:**
   - https://www.census.gov/programs-surveys/geography/technical-documentation/county-changes.html

2. **Virginia Independent Cities:**
   - https://www.census.gov/geographies/reference-files/2010/geo/state-local-geo-guides-2010/virginia.html

3. **Alaska Changes:**
   - https://www.census.gov/geographies/reference-files/2010/geo/state-local-geo-guides-2010/alaska.html

4. **NHGIS Boundary Harmonization:**
   - https://www.nhgis.org/time-series-tables

---

**Next:** Read [GEOGRAPHIC_CROSSWALKS.md](./GEOGRAPHIC_CROSSWALKS.md) to understand how to link ZIP codes, census tracts, and other geographies to counties.
