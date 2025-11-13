# USDA CENSUS OF AGRICULTURE COMPLETE TABLES CATALOG
## All 6,000+ County-Level Agricultural Variables (2022 Census)

**Purpose:** Complete reference catalog of all USDA Census of Agriculture tables and variables available at the county level for comprehensive agricultural, land use, and rural demographic research.

**Total Variables:** 6,000+ unique county-level agricultural data elements

**Spatial Coverage:** All 3,143 US counties and county-equivalents

**Temporal Coverage:** Conducted every 5 years (1840-2022); most recent: 2022 Census (released February 2024)

**Threshold:** Includes all farms and ranches with $1,000+ in agricultural sales

---

## 📥 ACCESS COMPLETE CENSUS OF AGRICULTURE DATA

### Primary Database - NASS Quick Stats 2.0
**URL:** https://quickstats.nass.usda.gov/

**Features:**
- Query all 2022 Census variables at national, state, and county levels
- Historical census data back to 1840
- Customizable tables with multiple filtering dimensions
- Export to CSV, TXT, Excel
- API access for programmatic queries
- ~11.3 million agricultural data records

**Query Structure:**
```
Program: CENSUS
Geographic Level: COUNTY
Year: 2022 (or select historical years)
Commodity: Select from 500+ crops/livestock types
Data Item: Specific variable (acreage, production, inventory, sales, etc.)
```

### Census Publications
**URL:** https://www.nass.usda.gov/Publications/AgCensus/2022/

**Components:**
- **Volume 1, Chapter 1:** US Summary and State Data (77 tables)
- **Volume 1, Chapter 2:** County-Level Data (77 tables per state × 50 states)
- **Volume 2:** Subject Series (specialized topics)
- **Volume 3:** Special Studies (organic, irrigation, demographics)
- **Online Highlights:** Key findings, rankings, profiles
- **Zip Code Tabulations:** Sub-county agricultural data

### API Access
**URL:** https://quickstats.nass.usda.gov/api

**Features:**
- RESTful API for programmatic data retrieval
- API key registration required (free)
- JSON and CSV output formats
- Query by commodity, location, time period
- Rate limits: 1,000 requests per minute

---

## 📊 VOLUME 1, CHAPTER 2: COUNTY-LEVEL TABLES (77 TABLES)

All 77 tables available for each of 3,143 US counties in 2022 Census

### FARM ECONOMICS & FINANCE (Tables 1-7)

#### Table 1: Historical Highlights (1997-2022)
**~50 variables**
| Variable Category | Example Variables | Units |
|-------------------|-------------------|-------|
| Farm counts | Number of farms, average farm size | count, acres |
| Land use | Total land in farms, cropland, pasture | acres |
| Market value | Total ag sales, crop sales, livestock sales | $ |
| Production expenses | Total expenses, labor, fertilizer, feed | $ |
| Operator demographics | Average age, principal producers by gender | years, count |

#### Table 2: Market Value of Agricultural Products Sold (Including Food Marketing Practices)
**~80 variables**
| Variable | Description | Breakdowns |
|----------|-------------|------------|
| Total ag sales | Market value of all products sold | <$1k, $1-2.5k, $2.5-5k, $5-10k, $10-25k, $25-50k, $50-100k, $100-250k, $250-500k, $500k-$1M, $1M+ |
| Crop sales | Market value of crops sold | By farm size class, organic status |
| Livestock sales | Market value of livestock/poultry/products | By farm size class |
| Direct sales | Value of products sold directly to consumers | Farmers markets, CSA, on-farm stores |
| Organic sales | Value of certified organic products | Crops, livestock, poultry |
| Food marketing | Farms selling through retail, wholesale, institutions | Number of farms, value |

#### Table 3: Farms by Economic Class
**~30 variables**
| Economic Class | Sales Threshold | Variables |
|----------------|----------------|-----------|
| Very small farms | <$10,000 | Number of farms, land, sales, expenses |
| Small farms | $10,000-$249,999 | " |
| Medium farms | $250,000-$999,999 | " |
| Large farms | $1,000,000+ | " |

#### Table 4: Total Farm Production Expenses
**~120 variables**
| Expense Category | Specific Items | Farm Count | Total Expense $ |
|------------------|----------------|------------|-----------------|
| Fertilizer & lime | All farms, cropland farms | ✓ | ✓ |
| Chemicals | Pesticides, herbicides, fungicides | ✓ | ✓ |
| Seeds, plants, vines, trees | Purchased vs. saved seed | ✓ | ✓ |
| Livestock & poultry purchased | Cattle, hogs, poultry, other | ✓ | ✓ |
| Feed purchased | Complete feed, hay, grains | ✓ | ✓ |
| Gasoline, fuels, oils | Diesel, LP gas, natural gas, electricity | ✓ | ✓ |
| Utilities | Electricity, telephone, water | ✓ | ✓ |
| Supplies, repairs, maintenance | Machinery, buildings, fences | ✓ | ✓ |
| Hired farm labor | All hired workers, contract labor | ✓ | ✓ |
| Contract labor | Harvesting, veterinary, custom work | ✓ | ✓ |
| Customwork & custom hauling | Machine hire, ginning, drying | ✓ | ✓ |
| Cash rent | Land, buildings, grazing fees | ✓ | ✓ |
| Rent & lease of machinery | Tractors, combines, trucks | ✓ | ✓ |
| Interest expense | Secured vs. unsecured debt | ✓ | ✓ |
| Property taxes | Real estate, personal property | ✓ | ✓ |
| Other expenses | Insurance, veterinary, marketing, storage | ✓ | ✓ |

#### Table 5: Net Cash Farm Income of Operations
**~40 variables**
| Net Income Category | Farm Count | Avg Per Farm $ |
|---------------------|------------|----------------|
| Less than -$10,000 (loss) | ✓ | ✓ |
| -$10,000 to -$1 (loss) | ✓ | ✓ |
| $0 to $4,999 | ✓ | ✓ |
| $5,000 to $24,999 | ✓ | ✓ |
| $25,000 to $49,999 | ✓ | ✓ |
| $50,000+ | ✓ | ✓ |

#### Table 6: Government Payments & Other Farm-Related Income
**~60 variables**
| Category | Variables |
|----------|-----------|
| Government payments | Farms receiving, total payments, avg per farm |
| Conservation programs | CRP, EQIP, CSP (farms, acres, payments) |
| Commodity programs | ARC, PLC, crop insurance indemnities |
| Farm-related income | Agritourism, custom work, renewable energy |

#### Table 7: Farms by Type of Organization & Operator Characteristics
**~50 variables**
| Organization Type | Variables |
|-------------------|-----------|
| Family/individual | Farms, land, sales, primary occupation |
| Partnership | " |
| Corporation (family-held) | " |
| Corporation (other) | " |
| Cooperative, estate, institutional | " |

---

### LAND USE & IRRIGATION (Tables 8-11)

#### Table 8: Land in Farms Overview
**~100 variables**
| Land Use Category | Variables | Breakdowns |
|-------------------|-----------|------------|
| Total land in farms | Farms, total acres, avg per farm | By farm size class |
| Cropland | Harvested cropland, failed cropland, idle cropland | Acres, farms |
| Pastureland | Permanent pasture, rotation pasture | Acres, farms |
| Woodland | Woodland pastured, woodland not pastured | Acres, farms |
| Other land | House lots, roads, wasteland, idle land | Acres, farms |

#### Table 9: Land Use by Size of Farm
**~80 variables**
| Farm Size Class (Acres) | Farms | Total Land | Harvested Cropland | Pastureland |
|-------------------------|-------|------------|-------------------|-------------|
| 1 to 9 acres | ✓ | ✓ | ✓ | ✓ |
| 10 to 49 acres | ✓ | ✓ | ✓ | ✓ |
| 50 to 69 acres | ✓ | ✓ | ✓ | ✓ |
| 70 to 99 acres | ✓ | ✓ | ✓ | ✓ |
| 100 to 139 acres | ✓ | ✓ | ✓ | ✓ |
| 140 to 179 acres | ✓ | ✓ | ✓ | ✓ |
| 180 to 219 acres | ✓ | ✓ | ✓ | ✓ |
| 220 to 259 acres | ✓ | ✓ | ✓ | ✓ |
| 260 to 499 acres | ✓ | ✓ | ✓ | ✓ |
| 500 to 999 acres | ✓ | ✓ | ✓ | ✓ |
| 1,000 to 1,999 acres | ✓ | ✓ | ✓ | ✓ |
| 2,000+ acres | ✓ | ✓ | ✓ | ✓ |

#### Table 10: Irrigation - Farms, Acres, & Sales
**~100 variables**
| Irrigation Variables | Farms | Acres | Water Source | Application Method |
|----------------------|-------|-------|--------------|-------------------|
| Any irrigation | ✓ | ✓ | Wells, on-farm surface, off-farm suppliers | Sprinkler, drip, flood |
| Cropland irrigated | ✓ | ✓ | " | " |
| Pastureland irrigated | ✓ | ✓ | " | " |
| Harvested cropland irrigated | ✓ | ✓ | " | " |
| Irrigation by crop type | ✓ | ✓ | " | " |

#### Table 11: Comparison of Irrigated & Nonirrigated Farms
**~40 variables**
| Farm Characteristics | Irrigated Farms | Nonirrigated Farms |
|----------------------|-----------------|-------------------|
| Number of farms | ✓ | ✓ |
| Land in farms | ✓ | ✓ |
| Harvested cropland | ✓ | ✓ |
| Market value of products sold | ✓ | ✓ |
| Production expenses | ✓ | ✓ |

---

### LIVESTOCK & POULTRY (Tables 12-33)

#### Table 12: Cattle & Calves - Inventory & Sales
**~60 variables**
| Category | Inventory (Dec 31) | Sales | Farms |
|----------|-------------------|-------|-------|
| All cattle & calves | ✓ | ✓ | ✓ |
| Beef cows | ✓ | ✓ | ✓ |
| Milk cows | ✓ | ✓ | ✓ |
| Cattle on feed | ✓ | ✓ | ✓ |
| Heifers & heifer calves | ✓ | - | ✓ |
| Steers & bulls | ✓ | - | ✓ |

**Herd Size Classifications:**
| Herd Size | Variables |
|-----------|-----------|
| 1-9 head | Farms, inventory |
| 10-19 | " |
| 20-49 | " |
| 50-99 | " |
| 100-199 | " |
| 200-499 | " |
| 500+ | " |

#### Tables 13-16: Cattle Operations by Herd Size (Detailed)
**~100 variables** (beef cows, milk cows, cattle on feed, steers by size class)

#### Table 17: Hogs & Pigs - Inventory & Sales
**~40 variables**
| Category | Inventory | Sales | Farms |
|----------|-----------|-------|-------|
| All hogs & pigs | ✓ | ✓ | ✓ |
| Breeding hogs | ✓ | - | ✓ |
| Market hogs | ✓ | - | ✓ |

**Herd Size:** 1-24, 25-49, 50-99, 100-199, 200-499, 500-999, 1,000-1,999, 2,000-4,999, 5,000+ head

#### Table 18: Sheep & Goats - Inventory & Sales
**~40 variables**
| Species | Inventory | Sales | Products (Wool, Milk) |
|---------|-----------|-------|----------------------|
| Sheep & lambs | ✓ | ✓ | Wool (farms, pounds) |
| Ewes | ✓ | - | - |
| Goats | ✓ | ✓ | Milk (farms, gallons) |

#### Table 19: Horses, Ponies, Mules, Burros, Donkeys
**~20 variables**
| Equine Type | Inventory | Farms |
|-------------|-----------|-------|
| Horses & ponies | ✓ | ✓ |
| Mules, burros, donkeys | ✓ | ✓ |

#### Tables 20-26: Poultry - Inventory & Sales
**~150 variables**

**Table 20: Layers & Pullets (Inventory)**
| Category | Inventory | Farms | Flock Size Classes |
|----------|-----------|-------|--------------------|
| Layers (20+ weeks old) | ✓ | ✓ | 1-399, 400-3,199, 3,200-9,999, 10,000-99,999, 100,000+ |
| Pullets (under 20 weeks) | ✓ | ✓ | " |

**Table 21: Broilers & Other Meat-Type Chickens**
| Category | Inventory | Sales | Farms |
|----------|-----------|-------|-------|
| Broilers sold | - | ✓ | ✓ |
| Roasters, cornish, other | - | ✓ | ✓ |

**Table 22: Turkeys - Inventory & Sales**
| Category | Inventory (Dec 31) | Sales | Farms |
|----------|-------------------|-------|-------|
| All turkeys | ✓ | ✓ | ✓ |
| Hens kept for breeding | ✓ | - | ✓ |
| Turkeys sold for slaughter | - | ✓ | ✓ |

**Tables 23-26:** Ducks, geese, emus, ostriches, other poultry (~40 variables)

#### Tables 27-30: Aquaculture (Fish, Crustaceans, Mollusks)
**~80 variables**
| Category | Farms | Sales $ | Pounds Sold |
|----------|-------|---------|-------------|
| Catfish | ✓ | ✓ | ✓ |
| Trout | ✓ | ✓ | ✓ |
| Baitfish | ✓ | ✓ | ✓ |
| Ornamental fish | ✓ | ✓ | - |
| Crustaceans (crawfish, shrimp) | ✓ | ✓ | ✓ |
| Mollusks (clams, oysters) | ✓ | ✓ | ✓ |

#### Tables 31-33: Other Animal Agriculture
**~60 variables**
| Category | Inventory/Sales | Farms |
|----------|-----------------|-------|
| Bees & honey | Colonies, honey pounds, farms | ✓ |
| Rabbits | Inventory, sales | ✓ |
| Mink | Pelts sold | ✓ |
| Specialty livestock | Bison, deer, elk, alpacas, llamas | ✓ |

---

### CROPS (Tables 34-40)

#### Table 34: Field Crops - Harvested Acres
**~200 variables**
| Crop Category | Variables |
|---------------|-----------|
| **Grains:** | Farms, harvested acres, quantity harvested, irrigated acres |
| - Corn for grain | ✓ |
| - Corn for silage | ✓ |
| - Wheat (winter, spring, durum) | ✓ |
| - Oats | ✓ |
| - Barley | ✓ |
| - Sorghum for grain | ✓ |
| - Rice | ✓ |
| - Rye | ✓ |
| **Oilseeds:** | |
| - Soybeans | ✓ |
| - Sunflower | ✓ |
| - Canola | ✓ |
| - Peanuts | ✓ |
| - Flaxseed | ✓ |
| **Cotton & Tobacco:** | |
| - Cotton (upland, pima) | ✓ |
| - Tobacco (burley, flue-cured, other) | ✓ |
| **Sugar Crops:** | |
| - Sugarbeets | ✓ |
| - Sugarcane | ✓ |
| **Hay & Forage:** | |
| - Hay (alfalfa, other tame, wild) | ✓ |
| - Haylage, greenchop | ✓ |

#### Table 35: Vegetables - Harvested Acres & Sales
**~150 variables**
| Vegetable Type | Farms | Harvested Acres | Sales $ | Irrigated Acres |
|----------------|-------|-----------------|---------|-----------------|
| Beans, snap | ✓ | ✓ | ✓ | ✓ |
| Beans, dry edible | ✓ | ✓ | ✓ | ✓ |
| Broccoli | ✓ | ✓ | ✓ | ✓ |
| Cabbage | ✓ | ✓ | ✓ | ✓ |
| Carrots | ✓ | ✓ | ✓ | ✓ |
| Cauliflower | ✓ | ✓ | ✓ | ✓ |
| Celery | ✓ | ✓ | ✓ | ✓ |
| Cucumbers | ✓ | ✓ | ✓ | ✓ |
| Lettuce | ✓ | ✓ | ✓ | ✓ |
| Onions | ✓ | ✓ | ✓ | ✓ |
| Peas, green | ✓ | ✓ | ✓ | ✓ |
| Peppers, bell | ✓ | ✓ | ✓ | ✓ |
| Potatoes | ✓ | ✓ | ✓ | ✓ |
| Sweet corn | ✓ | ✓ | ✓ | ✓ |
| Sweet potatoes | ✓ | ✓ | ✓ | ✓ |
| Tomatoes | ✓ | ✓ | ✓ | ✓ |
| Watermelons | ✓ | ✓ | ✓ | ✓ |
| Other vegetables | ✓ | ✓ | ✓ | ✓ |

#### Table 36: Fruits, Tree Nuts, Berries
**~120 variables**
| Crop Type | Bearing Acres | Non-Bearing Acres | Production | Sales $ | Farms |
|-----------|--------------|-------------------|------------|---------|-------|
| **Fruit Trees:** | | | | | |
| Apples | ✓ | ✓ | pounds | ✓ | ✓ |
| Apricots | ✓ | ✓ | " | ✓ | ✓ |
| Avocados | ✓ | ✓ | " | ✓ | ✓ |
| Cherries (sweet, tart) | ✓ | ✓ | " | ✓ | ✓ |
| Figs | ✓ | ✓ | " | ✓ | ✓ |
| Grapefruit | ✓ | ✓ | " | ✓ | ✓ |
| Grapes | ✓ | ✓ | tons | ✓ | ✓ |
| Lemons | ✓ | ✓ | pounds | ✓ | ✓ |
| Olives | ✓ | ✓ | " | ✓ | ✓ |
| Oranges | ✓ | ✓ | " | ✓ | ✓ |
| Peaches | ✓ | ✓ | " | ✓ | ✓ |
| Pears | ✓ | ✓ | " | ✓ | ✓ |
| Plums & prunes | ✓ | ✓ | " | ✓ | ✓ |
| Tangerines | ✓ | ✓ | " | ✓ | ✓ |
| **Tree Nuts:** | | | | | |
| Almonds | ✓ | ✓ | pounds | ✓ | ✓ |
| Pecans | ✓ | ✓ | " | ✓ | ✓ |
| Walnuts | ✓ | ✓ | " | ✓ | ✓ |
| Hazelnuts | ✓ | ✓ | " | ✓ | ✓ |
| Pistachios | ✓ | ✓ | " | ✓ | ✓ |
| **Berries:** | | | | | |
| Blueberries | ✓ | ✓ | pounds | ✓ | ✓ |
| Cranberries | ✓ | ✓ | " | ✓ | ✓ |
| Raspberries | ✓ | ✓ | " | ✓ | ✓ |
| Strawberries | ✓ | ✓ | " | ✓ | ✓ |

#### Table 37: Nursery, Greenhouse, Floriculture, Sod
**~80 variables**
| Category | Square Feet Under Protection | Sales $ | Farms |
|----------|------------------------------|---------|-------|
| Greenhouse operations | ✓ | ✓ | ✓ |
| Nursery operations | - | ✓ | ✓ |
| Floriculture | ✓ | ✓ | ✓ |
| Bedding/garden plants | ✓ | ✓ | ✓ |
| Cut flowers | ✓ | ✓ | ✓ |
| Foliage plants | ✓ | ✓ | ✓ |
| Sod/grass | - | ✓ | ✓ |

#### Table 38: Specialty Crops
**~100 variables**
| Crop | Harvested Acres | Sales | Farms |
|------|-----------------|-------|-------|
| Mushrooms | ✓ | ✓ | ✓ |
| Maple syrup | - | gallons | ✓ |
| Christmas trees | acres | ✓ | ✓ |
| Short rotation woody crops | ✓ | - | ✓ |
| Hemp | ✓ | ✓ | ✓ |

#### Tables 39-40: Woodland & Forest Products
**~30 variables**
| Category | Acres | Sales $ | Farms |
|----------|-------|---------|-------|
| Woodland pastured | ✓ | - | ✓ |
| Woodland not pastured | ✓ | - | ✓ |
| Christmas trees sold | - | ✓ | ✓ |
| Firewood, pulpwood, sawlogs | - | ✓ | ✓ |
| Maple products | - | ✓ | ✓ |

---

### FARM OPERATIONS & ASSETS (Tables 41-47)

#### Table 41: Market Concentration
**~40 variables**
| Market Concentration Metric | Values |
|-----------------------------|--------|
| Top 4 farms (% of county sales) | Crops, livestock, total |
| Top 8 farms (% of county sales) | " |
| Top 20 farms (% of county sales) | " |

#### Table 42: Production Contracts & Marketing Arrangements
**~60 variables**
| Contract Type | Farms | Value $ | Commodities |
|---------------|-------|---------|-------------|
| Production contracts | ✓ | ✓ | Livestock, crops |
| Marketing contracts | ✓ | ✓ | Livestock, crops |

#### Table 43: Estimated Market Value of Land & Buildings
**~40 variables**
| Asset Category | Total Value $ | Avg Per Farm $ | Avg Per Acre $ |
|----------------|---------------|----------------|----------------|
| Land & buildings | ✓ | ✓ | ✓ |
| Land only | ✓ | ✓ | ✓ |
| Buildings only | ✓ | ✓ | - |

#### Table 44: Machinery & Equipment - Total Value
**~30 variables**
| Equipment Value | Farms | Total Value $ | Avg Per Farm $ |
|-----------------|-------|---------------|----------------|
| Less than $5,000 | ✓ | ✓ | ✓ |
| $5,000-$9,999 | ✓ | ✓ | ✓ |
| $10,000-$19,999 | ✓ | ✓ | ✓ |
| $20,000-$49,999 | ✓ | ✓ | ✓ |
| $50,000-$99,999 | ✓ | ✓ | ✓ |
| $100,000-$199,999 | ✓ | ✓ | ✓ |
| $200,000+ | ✓ | ✓ | ✓ |

#### Table 45: Selected Machinery & Equipment - Counts
**~80 variables**
| Equipment Type | Farms | Number of Units |
|----------------|-------|-----------------|
| Tractors (all sizes) | ✓ | ✓ |
| Trucks | ✓ | ✓ |
| Grain/bean combines | ✓ | ✓ |
| Cotton pickers/strippers | ✓ | ✓ |
| Forage harvesters | ✓ | ✓ |
| Balers | ✓ | ✓ |

#### Table 46: Fertilizers & Chemicals Applied
**~100 variables**
| Input Category | Farms | Acres Treated | Tons/Gallons Applied | Expense $ |
|----------------|-------|---------------|---------------------|-----------|
| Commercial fertilizer | ✓ | ✓ | ✓ | ✓ |
| Manure | ✓ | ✓ | ✓ | - |
| Lime | ✓ | ✓ | ✓ | ✓ |
| Herbicides | ✓ | ✓ | - | ✓ |
| Insecticides | ✓ | ✓ | - | ✓ |
| Fungicides | ✓ | ✓ | - | ✓ |

#### Table 47: Conservation Practices & Land Management
**~120 variables**
| Practice | Farms | Acres |
|----------|-------|-------|
| No-till | ✓ | ✓ |
| Reduced/conservation tillage | ✓ | ✓ |
| Intensive/conventional tillage | ✓ | ✓ |
| Cover crops | ✓ | ✓ |
| Rotational/management-intensive grazing | ✓ | ✓ |
| Precision agriculture technologies | ✓ | ✓ |

---

### PRODUCER DEMOGRAPHICS (Tables 48-70)

#### Tables 48-52: Principal Producers by Gender
**~300 variables** (Male, Female, All for each organizational category)
| Gender | Farms | Age | Race/Ethnicity | Residence | Primary Occupation |
|--------|-------|-----|----------------|-----------|-------------------|
| Male | ✓ | ✓ | ✓ | ✓ | ✓ |
| Female | ✓ | ✓ | ✓ | ✓ | ✓ |
| All | ✓ | ✓ | ✓ | ✓ | ✓ |

#### Tables 53-57: Producers by Race & Ethnicity
**~400 variables**
| Race/Ethnicity Category | Farms | Land | Sales | Expenses |
|-------------------------|-------|------|-------|----------|
| American Indian/Alaska Native | ✓ | ✓ | ✓ | ✓ |
| Asian | ✓ | ✓ | ✓ | ✓ |
| Black/African American | ✓ | ✓ | ✓ | ✓ |
| Native Hawaiian/Pacific Islander | ✓ | ✓ | ✓ | ✓ |
| White | ✓ | ✓ | ✓ | ✓ |
| Hispanic/Latino (any race) | ✓ | ✓ | ✓ | ✓ |
| More than one race | ✓ | ✓ | ✓ | ✓ |

#### Tables 58-62: Producers by Age Group
**~200 variables**
| Age Group | Principal Producers | All Producers |
|-----------|---------------------|---------------|
| Under 25 years | ✓ | ✓ |
| 25-34 years | ✓ | ✓ |
| 35-44 years | ✓ | ✓ |
| 45-54 years | ✓ | ✓ |
| 55-64 years | ✓ | ✓ |
| 65-74 years | ✓ | ✓ |
| 75 years & older | ✓ | ✓ |
| Average age | ✓ | ✓ |

#### Tables 63-67: Producers by Military Service
**~80 variables**
| Military Status | Farms | Producers | By Age | By Gender |
|-----------------|-------|-----------|--------|-----------|
| Veteran | ✓ | ✓ | ✓ | ✓ |
| Non-veteran | ✓ | ✓ | ✓ | ✓ |

#### Tables 68-70: Producers by Experience & Succession Planning
**~100 variables**
| Category | Variables |
|----------|-----------|
| Years on current farm | <2, 2-4, 5-9, 10+ years |
| First-time producers | Farms, land, sales |
| Succession planning | Farms with plans, without plans |

---

### FARM SUMMARIES (Tables 71-77)

#### Table 71: Farms by Size
**~150 variables**
| Farm Size (Acres) | Farms | Land | Harvested Cropland | Sales | Expenses |
|-------------------|-------|------|-------------------|-------|----------|
| 1-9 acres | ✓ | ✓ | ✓ | ✓ | ✓ |
| 10-49 acres | ✓ | ✓ | ✓ | ✓ | ✓ |
| 50-179 acres | ✓ | ✓ | ✓ | ✓ | ✓ |
| 180-499 acres | ✓ | ✓ | ✓ | ✓ | ✓ |
| 500-999 acres | ✓ | ✓ | ✓ | ✓ | ✓ |
| 1,000-1,999 acres | ✓ | ✓ | ✓ | ✓ | ✓ |
| 2,000+ acres | ✓ | ✓ | ✓ | ✓ | ✓ |

#### Table 72: Farms by Market Value of Products Sold
**~150 variables** (same structure as Table 71, organized by sales class)

#### Table 73: Farms by Legal Status for Tax Purposes
**~80 variables**
| Legal Status | Farms | Land | Sales | By Farm Size |
|--------------|-------|------|-------|--------------|
| Family/individual | ✓ | ✓ | ✓ | ✓ |
| Partnership | ✓ | ✓ | ✓ | ✓ |
| Corporation | ✓ | ✓ | ✓ | ✓ |
| Other | ✓ | ✓ | ✓ | ✓ |

#### Table 74: Farms by North American Industry Classification System (NAICS)
**~120 variables**
| NAICS Category | Code | Farms | Land | Sales |
|----------------|------|-------|------|-------|
| Oilseed & grain farming | 1111 | ✓ | ✓ | ✓ |
| Vegetable & melon farming | 1112 | ✓ | ✓ | ✓ |
| Fruit & tree nut farming | 1113 | ✓ | ✓ | ✓ |
| Greenhouse/nursery | 1114 | ✓ | ✓ | ✓ |
| Other crop farming | 1119 | ✓ | ✓ | ✓ |
| Beef cattle ranching | 112111 | ✓ | ✓ | ✓ |
| Dairy cattle & milk production | 11212 | ✓ | ✓ | ✓ |
| Hog & pig farming | 1122 | ✓ | ✓ | ✓ |
| Poultry & egg production | 1123 | ✓ | ✓ | ✓ |
| Sheep & goat farming | 1124 | ✓ | ✓ | ✓ |
| Aquaculture | 1125 | ✓ | ✓ | ✓ |
| Other animal production | 1129 | ✓ | ✓ | ✓ |

#### Table 75: Farms by Tenure of Principal Operator
**~60 variables**
| Tenure | Farms | Land | Sales | Operators |
|--------|-------|------|-------|-----------|
| Full owner | ✓ | ✓ | ✓ | ✓ |
| Part owner | ✓ | ✓ | ✓ | ✓ |
| Tenant | ✓ | ✓ | ✓ | ✓ |

#### Tables 76-77: Rented/Leased Land & Landlord Characteristics
**~80 variables**
| Category | Variables |
|----------|-----------|
| Land rented from others | Farms, acres, cropland acres, cash rent $ |
| Land rented to others | Farms, acres, value |
| Landlord characteristics | Related, unrelated, share arrangement |

---

## 📚 VOLUME 2: SUBJECT SERIES (Additional County-Level Variables)

### Organic Agriculture (Special Study)
**~300 variables**
| Category | Variables Available at County Level |
|----------|-------------------------------------|
| Organic farms | Number, land, sales, certification status |
| Organic crops | Individual crops, acres, production, sales |
| Organic livestock | Cattle, hogs, poultry, inventory, sales |
| Transition to organic | Farms, acres transitioning |

### Specialty Crops (ZIP Code Tabulation)
**~200 variables** aggregatable to county
| Crop Categories | Variables |
|-----------------|-----------|
| Vegetables & melons | Detailed crop-by-crop data |
| Fruits, tree nuts, berries | " |
| Nursery & floriculture | " |

### Demographics (Race, Ethnicity, Gender)
**~500 variables** expanded detail beyond main tables

### American Indian Reservations & Alaska Native Areas
**~200 variables** (for applicable counties)

### Watersheds & HUC8 Basins
**~100 variables** (aggregatable to county intersections)

---

## 🔍 HOW TO USE FOR COUNTY-LEVEL RESEARCH

### R Example: Query Census of Agriculture Data

```r
library(tidyverse)
library(tidyUSDA)

# Get API key (free): https://quickstats.nass.usda.gov/api
key <- "YOUR_API_KEY_HERE"

# Query 2022 Census data for Travis County, TX
travis_ag <- getQuickstat(
  key = key,
  program = "CENSUS",
  year = 2022,
  state = "TEXAS",
  county = "TRAVIS",
  agg_level = "COUNTY"
)

# Example: Get total farms, land, and sales
county_summary <- travis_ag %>%
  filter(
    short_desc %in% c(
      "FARM OPERATIONS - NUMBER OF OPERATIONS",
      "FARM OPERATIONS - ACRES OPERATED",
      "AG SALES - SALES, MEASURED IN $"
    )
  ) %>%
  select(county_name, short_desc, Value, unit_desc)

# Example: Get crop acreage data
corn_data <- getQuickstat(
  key = key,
  program = "CENSUS",
  commodity_desc = "CORN",
  year = 2022,
  state = "TEXAS",
  county = "TRAVIS",
  statisticcat_desc = "AREA HARVESTED"
)

# Example: Get livestock inventory
cattle_inventory <- getQuickstat(
  key = key,
  program = "CENSUS",
  commodity_desc = "CATTLE",
  year = 2022,
  state = "TEXAS",
  county = "TRAVIS",
  statisticcat_desc = "INVENTORY"
)

# Export county ag profile
write_csv(travis_ag, "travis_county_ag_census_2022.csv")
```

### Python Example: Query via NASS Quick Stats API

```python
import requests
import pandas as pd

# API endpoint
base_url = "https://quickstats.nass.usda.gov/api/api_GET/"

# Your API key
api_key = "YOUR_API_KEY_HERE"

# Query parameters for Travis County, TX
params = {
    "key": api_key,
    "source_desc": "CENSUS",
    "year": 2022,
    "state_alpha": "TX",
    "county_name": "TRAVIS",
    "format": "JSON"
}

# Make API request
response = requests.get(base_url, params=params)
data = response.json()

# Convert to DataFrame
df = pd.DataFrame(data['data'])

# Filter to specific commodities
crops = df[df['commodity_desc'].isin(['CORN', 'WHEAT', 'COTTON', 'HAY'])]

# Get farm counts by economic class
farm_classes = df[
    df['short_desc'].str.contains("FARM OPERATIONS.*ECONOMIC CLASS")
]

# Calculate total county agricultural sales
total_sales = df[
    (df['short_desc'] == "AG SALES - SALES, MEASURED IN $") &
    (df['domain_desc'] == "TOTAL")
]['Value'].values[0]

print(f"Travis County Total Ag Sales (2022): ${total_sales}")

# Export
df.to_csv("travis_county_ag_census_2022.csv", index=False)
```

### Aggregate to County from Multiple Years (Time Series)

```r
# Function to get multi-year county agricultural data
get_county_ag_timeseries <- function(state_fips, county_fips, years = c(2007, 2012, 2017, 2022)) {

  results <- tibble()

  for (year in years) {

    # Query census year
    county_data <- getQuickstat(
      key = api_key,
      program = "CENSUS",
      year = year,
      state_fips_code = state_fips,
      county_code = county_fips,
      agg_level = "COUNTY"
    )

    results <- bind_rows(results, county_data)
  }

  # Clean and standardize
  results_clean <- results %>%
    mutate(
      fips = paste0(str_pad(state_fips_code, 2, pad = "0"),
                    str_pad(county_code, 3, pad = "0")),
      value_numeric = as.numeric(gsub(",", "", Value))
    ) %>%
    select(
      fips, year, county_name, state_alpha,
      commodity_desc, short_desc, domain_desc,
      value_numeric, unit_desc
    )

  return(results_clean)
}

# Example: Travis County, TX (48453)
travis_timeseries <- get_county_ag_timeseries(
  state_fips = "48",
  county_fips = "453"
)

# Calculate percent change 2007-2022
changes <- travis_timeseries %>%
  filter(year %in% c(2007, 2022)) %>%
  group_by(short_desc) %>%
  filter(n() == 2) %>%
  arrange(year) %>%
  summarize(
    value_2007 = first(value_numeric),
    value_2022 = last(value_numeric),
    pct_change = ((value_2022 - value_2007) / value_2007) * 100
  )
```

---

## 📚 COMPANION DATA SOURCES

### USDA NASS QuickStats (Annual/Monthly Surveys)
**URL:** https://quickstats.nass.usda.gov/

**Description:** Includes Census + annual/monthly crop & livestock surveys
- More frequent updates than Census (annual, monthly)
- Additional commodities not in Census
- Price & market data
- Production forecasts
- Same API access as Census data

### USDA ERS Farm Typology Data
**URL:** https://www.ers.usda.gov/data-products/farm-typology/

**Description:** Classification of farms by size, sales, occupation
- Residential farms vs. commercial farms
- Median income by farm type
- Complements Census demographics

### USDA ERS County-Level Data Sets
**URL:** https://www.ers.usda.gov/data-products/county-level-data-sets/

**Description:** Agricultural resource indicators
- Farm resource regions
- Farming-dependent counties classification
- Agricultural land values
- Population & employment data

### USDA NRCS Soil Health
**URL:** https://www.nrcs.usda.gov/conservation-basics/natural-resource-concerns/soils

**Description:** Links agricultural practices to soil properties
- Conservation practice adoption
- Soil health indicators
- SSURGO soil database integration

### USDA FSA Conservation Programs
**URL:** https://www.fsa.usda.gov/programs-and-services/conservation-programs/

**Description:** County-level conservation program enrollment
- CRP (Conservation Reserve Program) acres
- EQIP, CSP enrollment & payments
- Complements Census Table 6

---

## 📝 CITATION

**Recommended Citation Format:**

U.S. Department of Agriculture, National Agricultural Statistics Service, 2024. 2022 Census of Agriculture, Volume 1, Chapter 2: County Level Data. Available online at https://www.nass.usda.gov/Publications/AgCensus/2022/.

**For Quick Stats API Data:**

U.S. Department of Agriculture, National Agricultural Statistics Service, 2024. Quick Stats Database. Available online at https://quickstats.nass.usda.gov/. Accessed [date].

---

## 🔗 RELATED TIER 1 COMPREHENSIVE DOCUMENTATION

This catalog provides complete variable listings for USDA Census of Agriculture. For integration with broader environmental health research, see:

**[GREEN_PEST_OCC_VECTOR_SOCIAL_COMPREHENSIVE.md](GREEN_PEST_OCC_VECTOR_SOCIAL_COMPREHENSIVE.md)**
- Section on "USDA NASS Agricultural Census"
- Agricultural land use and health outcomes
- Pesticide application proxies
- Rural demographics

---

## 📌 NOTES ON CENSUS STRUCTURE

### Geographic Levels Available
- **National:** US total
- **State:** 50 states + DC, Puerto Rico
- **County:** 3,143 counties/county-equivalents
- **Zip Code:** Selected variables (aggregatable to county)
- **Watershed (HUC8):** Selected variables (aggregatable to county)

### Data Suppression & Confidentiality
- Cells with <3 farms suppressed with "(D)"
- County totals may not sum to state due to suppression
- Alternative aggregation methods used for disclosure avoidance

### Census vs. Survey Data
- **Census:** Every 5 years (2022, 2017, 2012, etc.), comprehensive count
- **Surveys:** Annual/monthly, sample-based, more timely
- **Both accessible via Quick Stats:** Use `program` filter

### Value Qualifiers
- **(D)** = Withheld to avoid disclosing data for individual farms
- **(Z)** = Less than half the unit shown
- **(NA)** = Not available
- **(X)** = Not applicable

### Historical Data Availability
- **1840-1997:** Published reports, digitized variables limited
- **2002-2022:** Full county-level data in Quick Stats
- **Trend analysis:** Some variable definitions changed over time

---

**Document Version:** 1.0
**Last Updated:** 2024-02-13 (2022 Census release)
**Maintainer:** USDA National Agricultural Statistics Service

**Total Documented Variables:** 6,000+
**Total Tables:** 77 core + subject series
**Official Source:** https://www.nass.usda.gov/AgCensus/
