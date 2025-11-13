# FIPS Codes & Geographic Identifiers
## Essential Reference for US County-Level Data

**Purpose:** This document explains the standard geographic identifiers used across all US county-level datasets.

**Read this FIRST** before collecting any county-level data.

---

## 🔑 FIPS Codes - The Universal County Identifier

### What is a FIPS Code?

**FIPS (Federal Information Processing Standards) codes** are standardized numeric codes used by the US government to uniquely identify geographic areas.

**County FIPS Code Structure:**
```
SSCCC
│ │
│ └─ 3-digit County Code (001-999)
└─ 2-digit State Code (01-56, plus 60, 66, 69, 72, 78)
```

**Example:**
- **48453** = Travis County, Texas
  - **48** = Texas (state code)
  - **453** = Travis County (county code within Texas)

---

## 📊 Complete State FIPS Codes

### States (01-56)

| State Code | State Name | Abbrev | State Code | State Name | Abbrev |
|------------|------------|--------|------------|------------|--------|
| 01 | Alabama | AL | 30 | Montana | MT |
| 02 | Alaska | AK | 31 | Nebraska | NE |
| 04 | Arizona | AZ | 32 | Nevada | NV |
| 05 | Arkansas | AR | 33 | New Hampshire | NH |
| 06 | California | CA | 34 | New Jersey | NJ |
| 08 | Colorado | CO | 35 | New Mexico | NM |
| 09 | Connecticut | CT | 36 | New York | NY |
| 10 | Delaware | DE | 37 | North Carolina | NC |
| 11 | District of Columbia | DC | 38 | North Dakota | ND |
| 12 | Florida | FL | 39 | Ohio | OH |
| 13 | Georgia | GA | 40 | Oklahoma | OK |
| 15 | Hawaii | HI | 41 | Oregon | OR |
| 16 | Idaho | ID | 42 | Pennsylvania | PA |
| 17 | Illinois | IL | 44 | Rhode Island | RI |
| 18 | Indiana | IN | 45 | South Carolina | SC |
| 19 | Iowa | IA | 46 | South Dakota | SD |
| 20 | Kansas | KS | 47 | Tennessee | TN |
| 21 | Kentucky | KY | 48 | Texas | TX |
| 22 | Louisiana | LA | 49 | Utah | UT |
| 23 | Maine | ME | 50 | Vermont | VT |
| 24 | Maryland | MD | 51 | Virginia | VA |
| 25 | Massachusetts | MA | 53 | Washington | WA |
| 26 | Michigan | MI | 54 | West Virginia | WV |
| 27 | Minnesota | MN | 55 | Wisconsin | WI |
| 28 | Mississippi | MS | 56 | Wyoming | WY |
| 29 | Missouri | MO | | | |

**Note:** State code 03 (historical), 07 (historical), 14 (historical), 43 (historical), 52 (historical) were never used or discontinued.

### Territories (60, 66, 69, 72, 78)

| Code | Territory |
|------|-----------|
| 60 | American Samoa |
| 66 | Guam |
| 69 | Commonwealth of the Northern Mariana Islands |
| 72 | Puerto Rico |
| 78 | US Virgin Islands |

---

## 🗺️ County FIPS Codes

### Structure
- County codes range from **001 to 999** within each state
- Codes are assigned in **approximate alphabetical order** by county name
- Codes are **permanent** and not reused when counties merge or dissolve

### Total US Counties

**As of 2024:**
- **3,143 counties and county-equivalent areas**
  - 3,007 counties
  - 16 boroughs (Alaska)
  - 11 census areas (Alaska)
  - 41 independent cities (Virginia: 38, Missouri: 1, Maryland: 1, Nevada: 1)
  - 1 district (District of Columbia)
  - 64 parishes (Louisiana)
  - Plus territories: Puerto Rico (78 municipios), other territories

---

## 🏛️ Special Cases & County-Equivalent Areas

### Independent Cities

**Independent cities are NOT part of any county** and have their own FIPS codes.

#### Virginia (38 Independent Cities)

Virginia has 38 independent cities with FIPS codes in the 5XX range:

| FIPS | City | FIPS | City |
|------|------|------|------|
| 51510 | Alexandria city | 51710 | Norfolk city |
| 51520 | Bristol city | 51730 | Petersburg city |
| 51530 | Buena Vista city | 51735 | Poquoson city |
| 51540 | Charlottesville city | 51740 | Portsmouth city |
| 51550 | Chesapeake city | 51750 | Radford city |
| 51570 | Colonial Heights city | 51760 | Richmond city |
| 51580 | Covington city | 51770 | Roanoke city |
| 51590 | Danville city | 51775 | Salem city |
| 51595 | Emporia city | 51790 | Staunton city |
| 51600 | Fairfax city | 51800 | Suffolk city |
| 51610 | Falls Church city | 51810 | Virginia Beach city |
| 51620 | Franklin city | 51820 | Waynesboro city |
| 51630 | Fredericksburg city | 51830 | Williamsburg city |
| 51640 | Galax city | 51840 | Winchester city |
| 51650 | Hampton city | | |
| 51660 | Harrisonburg city | | |
| 51670 | Hopewell city | | |
| 51678 | Lexington city | | |
| 51680 | Lynchburg city | | |
| 51683 | Manassas city | | |
| 51685 | Manassas Park city | | |
| 51690 | Martinsville city | | |
| 51700 | Newport News city | | |

**Important:** Some Virginia independent cities have MERGED with adjacent counties in recent decades (see COUNTY_BOUNDARIES_REDISTRICTING.md).

#### Other Independent Cities

| State | FIPS | City |
|-------|------|------|
| Missouri | 29510 | St. Louis city |
| Maryland | 24510 | Baltimore city |
| Nevada | 32510 | Carson City |

### Alaska Census Areas

Alaska has **no counties**. Instead, it uses:
- **Boroughs** (organized, similar to counties) - FIPS 013-290
- **Census Areas** (unorganized areas grouped by Census Bureau) - FIPS 013-290

**Examples:**
- 02020 = Anchorage Municipality
- 02090 = Fairbanks North Star Borough
- 02110 = Juneau City and Borough
- 02105 = Hoonah-Angoon Census Area
- 02195 = Petersburg Borough (created 2013)
- 02270 = Wade Hampton Census Area (renamed to Kusilvak Census Area in 2015)

**Note:** Alaska boundary changes and name changes are common (see COUNTY_BOUNDARIES_REDISTRICTING.md).

### Louisiana Parishes

Louisiana uses **parishes** instead of counties, but they function the same way and use standard FIPS codes 001-127.

**Examples:**
- 22071 = Orleans Parish (New Orleans)
- 22033 = East Baton Rouge Parish

### District of Columbia

- **11001** = District of Columbia
- Functions as both a city and county-equivalent for statistical purposes

---

## 🔢 Constructing & Parsing FIPS Codes

### From Components to FIPS

```python
# Python example
state_code = "48"  # Texas
county_code = "453"  # Travis County
fips = state_code + county_code  # "48453"

# Ensure proper zero-padding
state_code = str(state_fips).zfill(2)
county_code = str(county_fips).zfill(3)
fips = state_code + county_code
```

```r
# R example
state_code <- "48"
county_code <- "453"
fips <- paste0(state_code, county_code)  # "48453"

# Ensure proper zero-padding
state_code <- str_pad(state_fips, 2, pad = "0")
county_code <- str_pad(county_fips, 3, pad = "0")
fips <- paste0(state_code, county_code)
```

### Parsing FIPS to Components

```python
# Python example
fips = "48453"
state_code = fips[:2]    # "48"
county_code = fips[2:]   # "453"
```

```r
# R example
fips <- "48453"
state_code <- substr(fips, 1, 2)    # "48"
county_code <- substr(fips, 3, 5)   # "453"
```

---

## 📁 Official FIPS Code Lists

### Census Bureau FIPS Files

**National FIPS Codes File:**
- **URL:** https://www.census.gov/geo/reference/codes/cou.html
- **Format:** Text file, Excel
- **Fields:** State code, county code, county name, FIPS code, ANSI code

**Download:**
```bash
# Download current national county FIPS codes
wget https://www2.census.gov/geo/docs/reference/codes/files/national_county.txt
```

**File Format (national_county.txt):**
```
STATE,STATEFP,COUNTYFP,COUNTYNAME,CLASSFP
AL,01,001,Autauga County,H1
AL,01,003,Baldwin County,H1
TX,48,453,Travis County,H1
```

### ANSI Codes

In addition to FIPS codes, counties also have **ANSI (American National Standards Institute) codes**:
- 8-character alphanumeric code
- Example: Travis County, TX = 01383877
- Less commonly used than FIPS
- Found in Census TIGER/Line files

---

## 🔄 County Name Variations & Changes

### Official vs. Common Names

Most county names include the word "County" or "Parish", but:
- **Louisiana:** Uses "Parish" (e.g., "Orleans Parish")
- **Alaska:** Uses "Borough", "Census Area", "Municipality"
- **Independent Cities:** No suffix (e.g., "Baltimore city")

### Name Changes Over Time

Counties occasionally change names:

| FIPS | Old Name | New Name | Year | State |
|------|----------|----------|------|-------|
| 46102 | Shannon County | Oglala Lakota County | 2015 | SD |
| 02270 | Wade Hampton Census Area | Kusilvak Census Area | 2015 | AK |

**Implication for time series:** Data published before the name change will use the old name, after will use the new name. FIPS code remains the same.

### Spelling Variations

Some datasets use variations:
- "St." vs. "Saint"
- Accented characters: "Doña Ana" vs. "Dona Ana"
- Hyphenation: "De Kalb" vs. "DeKalb"

**Best practice:** Always match on FIPS code, not county name.

---

## 🗃️ Other Geographic Identifiers

### GEOID

**GEOID (Geographic Identifier)** is a generalized identifier used by Census Bureau for ALL geographic levels:

**County GEOID = FIPS Code**
- Counties: 5 digits (SSCCC) - same as FIPS
- Tracts: 11 digits (SSCCCTTTTTT)
- Block Groups: 12 digits
- Blocks: 15 digits

**Example:**
- County: 48453 (Travis County)
- Tract: 48453001100 (Tract 11.00 in Travis County)

### CBSA Codes

**CBSA (Core-Based Statistical Area)** codes identify metropolitan/micropolitan areas:
- 5-digit codes
- Counties are assigned to CBSAs (many-to-one relationship)
- One county can be in one CBSA only

**Example:**
- 12420 = Austin-Round Rock-Georgetown, TX Metro Area
- Includes: Travis County (48453), Williamson County (48491), Hays County (48209), etc.

**File:** https://www.census.gov/geographies/reference-files/time-series/demo/metro-micro/delineation-files.html

### State-County Codes (Alternative Systems)

Some datasets use alternative coding:
- **EPA FIPS:** Same as standard FIPS
- **USDA FIPS:** Same as standard FIPS
- **NCHS codes:** Historical county codes (mostly replaced by FIPS)

---

## 💻 Code Examples: Loading FIPS Codes

### Python

```python
import pandas as pd

# Load official Census FIPS codes
url = "https://www2.census.gov/geo/docs/reference/codes/files/national_county.txt"
fips = pd.read_csv(url, dtype=str)

# Create 5-digit FIPS
fips['FIPS'] = fips['STATEFP'] + fips['COUNTYFP']

# Create clean county name (remove " County", " Parish", " city", etc.)
fips['COUNTYNAME_CLEAN'] = fips['COUNTYNAME'].str.replace(
    r' (County|Parish|city|Borough|Census Area|Municipality)$',
    '',
    regex=True
)

# Display
print(fips.head())
```

### R

```r
library(tidyverse)

# Load official Census FIPS codes
url <- "https://www2.census.gov/geo/docs/reference/codes/files/national_county.txt"
fips <- read_csv(url, col_types = cols(.default = "c"))

# Create 5-digit FIPS
fips <- fips %>%
  mutate(FIPS = paste0(STATEFP, COUNTYFP))

# Create clean county name
fips <- fips %>%
  mutate(
    COUNTYNAME_CLEAN = str_remove(
      COUNTYNAME,
      " (County|Parish|city|Borough|Census Area|Municipality)$"
    )
  )

# Display
print(fips)
```

---

## 🔍 Common Issues & Solutions

### Leading Zeros

**Problem:** FIPS codes must have leading zeros, but Excel/CSV often drops them.
- 01001 (Autauga County, AL) becomes 1001 ❌
- 06037 (Los Angeles County, CA) becomes 6037 ❌

**Solutions:**

**Python:**
```python
# When reading CSV
df = pd.read_csv('data.csv', dtype={'FIPS': str})

# Re-pad if already loaded as integer
df['FIPS'] = df['FIPS'].astype(str).str.zfill(5)
```

**R:**
```r
# When reading CSV
df <- read_csv('data.csv', col_types = cols(FIPS = col_character()))

# Re-pad if already loaded as integer
df$FIPS <- str_pad(df$FIPS, 5, pad = "0")
```

### Numeric vs. String

**Best practice:** Always treat FIPS codes as **strings**, not integers.
- Preserves leading zeros
- Prevents arithmetic operations

### Mismatched County Names

**Problem:** County names spelled differently across datasets.

**Solution:** Always join on FIPS code, not county name:

```python
# Good - join on FIPS
df1.merge(df2, on='FIPS', how='left')

# Bad - join on name (will miss mismatches)
df1.merge(df2, on='COUNTYNAME', how='left')
```

---

## 📚 Additional Resources

### Official Sources

1. **Census Bureau Geography Program**
   - https://www.census.gov/programs-surveys/geography.html

2. **FIPS Codes Documentation**
   - https://www.census.gov/library/reference/code-lists/ansi.html

3. **TIGER/Line Shapefiles** (include FIPS codes)
   - https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

4. **Geographic Names Information System (GNIS)**
   - https://www.usgs.gov/us-board-on-geographic-names

### Tools

- **Census Geocoder:** https://geocoding.geo.census.gov/
- **FIPS Code Lookup:** https://transition.fcc.gov/oet/info/maps/census/fips/fips.txt

---

## ✅ Checklist: FIPS Code Best Practices

Before starting data collection:

- [ ] Load official Census FIPS code list
- [ ] Treat FIPS codes as strings (never integers)
- [ ] Always use 5-digit format with leading zeros
- [ ] Join datasets on FIPS code, not county name
- [ ] Be aware of independent cities (especially Virginia)
- [ ] Check for Alaska Census Area name/boundary changes
- [ ] Note historical county name changes (Shannon→Oglala Lakota)
- [ ] Understand county-equivalent areas (DC, parishes, boroughs)
- [ ] Review COUNTY_BOUNDARIES_REDISTRICTING.md for changes over time

---

**Next:** Read [COUNTY_BOUNDARIES_REDISTRICTING.md](./COUNTY_BOUNDARIES_REDISTRICTING.md) to understand how county boundaries change over time and how to handle these changes in longitudinal datasets.
