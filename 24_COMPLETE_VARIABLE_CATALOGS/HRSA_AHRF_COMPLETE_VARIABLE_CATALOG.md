# HRSA AREA HEALTH RESOURCES FILES (AHRF) COMPLETE VARIABLE CATALOG
## All 6,000+ County-Level Health System & Population Variables (2023-2024 Release)

**Purpose:** Complete reference catalog of all HRSA Area Health Resources Files (AHRF) variables for comprehensive analysis of healthcare resources, workforce, facilities, and population health at the county level.

**Total Variables:** 6,000+ unique county-level health system data elements

**Spatial Coverage:** All 3,143 US counties and county-equivalents

**Temporal Coverage:** Annual updates; historical data from 1960s to present; most recent: 2023-2024 release

**Data Sources:** 60+ federal and private databases compiled by HRSA

---

## 📥 ACCESS COMPLETE AHRF DATA & DOCUMENTATION

### Primary Download - HRSA Data Warehouse
**URL:** https://data.hrsa.gov/data/download?data=AHRF

**Available Files:**
- **County-level file:** All 6,000+ variables for 3,143 counties
- **State-level file:** Aggregated state data
- **National-level file:** US summary statistics
- **Technical documentation (Excel):** Complete variable catalog with definitions, sources, years
- **SAS, CSV, ASCII formats:** Multiple data formats available

### Interactive Dashboard
**URL:** https://data.hrsa.gov/topics/health-workforce/ahrf

**Features:**
- Filter by health profession, year, location, demographic characteristics
- Visualize clinician supply by specialty and county
- Export custom data subsets
- Compare counties and states

### Contact & Support
- **Email:** data@hrsa.gov
- **Workforce inquiries:** NCHWAinquiries@hrsa.gov
- **Last Updated:** November 2024

---

## 📊 EIGHT MAJOR AHRF VARIABLE CATEGORIES (6,000+ Variables)

### CATEGORY 1: HEALTH CARE PROFESSIONS (~2,000 variables)

Healthcare workforce counts, rates per population, and characteristics by profession and specialty

#### 1.1 PHYSICIANS (MD/DO) - ~800 variables
| Specialty | Variables | Breakdowns |
|-----------|-----------|------------|
| **Primary Care:** | | |
| Family medicine/general practice | Count, rate per 100k pop, per sq mile | Active, total, by gender, by age group |
| Internal medicine | " | " |
| Pediatrics | " | " |
| Obstetrics & gynecology | " | " |
| **Surgical Specialties:** | | |
| General surgery | " | " |
| Orthopedic surgery | " | " |
| Cardiovascular surgery | " | " |
| Neurosurgery | " | " |
| **Medical Specialties:** | | |
| Cardiology | " | " |
| Oncology | " | " |
| Endocrinology | " | " |
| Gastroenterology | " | " |
| Pulmonology | " | " |
| Nephrology | " | " |
| **Mental Health:** | | |
| Psychiatry | " | " |
| Child/adolescent psychiatry | " | " |
| **Other Specialties:** | | |
| Emergency medicine | " | " |
| Radiology | " | " |
| Anesthesiology | " | " |
| Pathology | " | " |
| Dermatology | " | " |
| Ophthalmology | " | " |
| Otolaryngology | " | " |

**Data Sources:** AMA Physician Professional Data, AOA Osteopathic Physicians Data

**Time Series:** Selected years from 1980-2023

#### 1.2 NURSING PROFESSIONALS - ~400 variables
| Profession | Variables | Breakdowns |
|------------|-----------|------------|
| Registered nurses (RN) | Count, rate per 100k, per sq mile | Total, by education level (diploma, associate, bachelor, graduate) |
| Licensed practical nurses (LPN) | " | Total |
| Nurse practitioners (NP) | " | By specialty (family, adult, pediatric, psychiatric) |
| Certified registered nurse anesthetists (CRNA) | " | Total |
| Clinical nurse specialists (CNS) | " | Total |
| Certified nurse midwives (CNM) | " | Total |

**Data Sources:** NSSRN (National Sample Survey of Registered Nurses), state nursing boards

#### 1.3 ALLIED HEALTH PROFESSIONALS - ~400 variables
| Profession | Variables | Breakdowns |
|------------|-----------|------------|
| Physician assistants (PA) | Count, rate per 100k | Total, by specialty |
| Pharmacists | " | Total, retail, hospital |
| Dentists | " | General dentists, specialists (orthodontics, oral surgery, etc.) |
| Dental hygienists | " | Total |
| Optometrists | " | Total |
| Chiropractors | " | Total |
| Podiatrists | " | Total |
| Physical therapists | " | Total |
| Occupational therapists | " | Total |
| Speech-language pathologists | " | Total |
| Audiologists | " | Total |
| Respiratory therapists | " | Total |
| Clinical laboratory personnel | " | Medical technologists, technicians |
| Radiologic technologists | " | Total |

**Data Sources:** Professional association databases, state licensing boards

#### 1.4 MENTAL HEALTH & SUBSTANCE ABUSE PROFESSIONALS - ~200 variables
| Profession | Variables | Breakdowns |
|------------|-----------|------------|
| Psychiatrists | Count, rate per 100k | Adult, child/adolescent |
| Psychologists | " | Clinical, counseling, school |
| Clinical social workers | " | LCSW, MSW |
| Mental health counselors | " | Licensed professional counselors |
| Marriage & family therapists | " | Total |
| Substance abuse counselors | " | Total |

#### 1.5 FEDERALLY QUALIFIED HEALTH CENTER (FQHC) PROVIDERS - ~100 variables
| Category | Variables |
|----------|-----------|
| FQHC clinicians | Total count, by profession (MD, DO, NP, PA, RN) |
| FQHC sites | Number of sites, patients served |
| FQHC funding | Grant amounts, operating costs |

#### 1.6 WORKFORCE SHORTAGE & MALDISTRIBUTION - ~100 variables
| Indicator | Variables |
|-----------|-----------|
| Health Professional Shortage Areas (HPSAs) | Count, type (primary care, dental, mental health), population of need |
| Medically Underserved Areas (MUAs) | Count, MUA score, population |
| Medically Underserved Populations (MUPs) | Count, designation type |
| Primary Care Service Areas (PCSAs) | Designation status |

---

### CATEGORY 2: HEALTH FACILITIES (~1,000 variables)

Counts, characteristics, and capacity of healthcare delivery facilities

#### 2.1 HOSPITALS - ~400 variables
| Hospital Type | Variables | Characteristics |
|---------------|-----------|----------------|
| **All hospitals** | Count, beds, admissions, patient days | By ownership, bed size, teaching status |
| **Community hospitals** | " | Short-term general, non-federal |
| **Critical access hospitals (CAH)** | " | Rural designation, <25 beds |
| **Rural hospitals** | " | All rural designations |
| **Urban hospitals** | " | Metropolitan areas |
| **Teaching hospitals** | " | Medical school affiliation |
| **Public hospitals** | " | Government-owned |
| **Not-for-profit hospitals** | " | Non-profit ownership |
| **For-profit hospitals** | " | Investor-owned |
| **Specialized hospitals:** | | |
| - Psychiatric hospitals | Count, beds | Inpatient mental health |
| - Rehabilitation hospitals | " | Physical rehabilitation |
| - Long-term acute care | " | Extended critical care |
| - Children's hospitals | " | Pediatric specialty |
| - Cancer hospitals | " | Oncology focus |

**Utilization Metrics:** (for most hospital types)
- Total admissions
- Total patient days
- Average length of stay
- Occupancy rate
- Emergency department visits
- Outpatient visits
- Surgeries performed

**Financial:** (selected variables)
- Total expenses
- Payroll expenses
- Medicare/Medicaid utilization

**Data Sources:** AHA Annual Survey, CMS Provider of Services, Medicare Cost Reports

**Time Series:** Annual data 1990-2023

#### 2.2 AMBULATORY CARE FACILITIES - ~200 variables
| Facility Type | Variables |
|---------------|-----------|
| Federally Qualified Health Centers (FQHCs) | Count, sites, patients, visits |
| Rural Health Clinics (RHCs) | Count, Medicare-certified |
| Hospital outpatient departments | Count, visits |
| Ambulatory surgery centers | Count, procedures |
| Urgent care centers | Count (where available) |
| Dialysis facilities | Count, stations, patients |

#### 2.3 LONG-TERM CARE FACILITIES - ~150 variables
| Facility Type | Variables |
|---------------|-----------|
| Nursing homes (skilled nursing facilities) | Count, beds, residents, Medicare/Medicaid certified |
| Residential care facilities | Count, beds |
| Hospice programs | Count, patients served |
| Home health agencies | Count, patients, visits, Medicare-certified |

**Data Sources:** CMS Certification and Survey Provider Enhanced Reports (CASPER), National Post-Acute Care Survey

#### 2.4 MENTAL HEALTH & SUBSTANCE ABUSE FACILITIES - ~100 variables
| Facility Type | Variables |
|---------------|-----------|
| Community mental health centers | Count, services |
| Psychiatric hospitals | Count (see 2.1), beds |
| Residential mental health treatment | Count, beds |
| Substance abuse treatment facilities | Count, outpatient, inpatient, residential |

**Data Sources:** SAMHSA N-SSATS, N-MHSS

#### 2.5 PHARMACY & RETAIL HEALTH - ~50 variables
| Facility Type | Variables |
|---------------|-----------|
| Community pharmacies | Count, chain, independent |
| Hospital pharmacies | Count |
| Retail clinics | Count (where available) |

#### 2.6 SPECIALIZED SERVICES & TECHNOLOGY - ~100 variables
| Service/Technology | Variables |
|-------------------|-----------|
| Trauma centers | Count, by level (I, II, III, IV) |
| Burn care units | Count |
| Neonatal intensive care (NICU) | Count, beds, by level (II, III, IV) |
| Cardiac catheterization | Count of hospitals with service |
| Open heart surgery | " |
| MRI | " |
| CT scanner | " |
| PET scanner | " |
| Mammography | " |

---

### CATEGORY 3: POPULATION CHARACTERISTICS (~1,200 variables)

Demographic composition, size, growth, and structure

#### 3.1 TOTAL POPULATION & COMPONENTS - ~200 variables
| Category | Variables | Breakdowns |
|----------|-----------|------------|
| Total population | Count, annual estimates | Resident population |
| Population change | Numeric change, % change | 1-year, 5-year, 10-year intervals |
| Components of change | Births, deaths, net migration | Annual |
| Population projections | Projected population | 5, 10, 20-year horizons |
| Population density | Persons per square mile | Total, by urban/rural |
| Urban/rural classification | % urban, % rural | Census designation |

**Data Sources:** Census Bureau Population Estimates Program, Decennial Census

**Time Series:** Decennial 1970-2020, annual estimates 1980-2023

#### 3.2 AGE & SEX DISTRIBUTION - ~400 variables
| Age Group | Variables | By Sex |
|-----------|-----------|--------|
| Under 5 years | Count, % of total | Total, male, female |
| 5-17 years | " | " |
| 18-24 years | " | " |
| 25-44 years | " | " |
| 45-64 years | " | " |
| 65-74 years | " | " |
| 75-84 years | " | " |
| 85+ years | " | " |
| 18+ years (adult) | " | " |
| 65+ years (elderly) | " | " |
| Median age | Years | Total, male, female |
| Dependency ratios | Youth, elderly, total | Ratio |

#### 3.3 RACE & ETHNICITY - ~300 variables
| Race/Ethnicity | Variables | Breakdowns |
|----------------|-----------|------------|
| White alone | Count, % of total | Non-Hispanic, Hispanic |
| Black/African American alone | " | " |
| American Indian/Alaska Native alone | " | " |
| Asian alone | " | " |
| Native Hawaiian/Pacific Islander alone | " | " |
| Two or more races | " | " |
| Hispanic/Latino (any race) | " | By subgroup (Mexican, Puerto Rican, Cuban, other) |

**Detailed Asian Subgroups:** (selected variables)
- Asian Indian, Chinese, Filipino, Japanese, Korean, Vietnamese, Other Asian

**Detailed Hispanic Subgroups:**
- Mexican, Puerto Rican, Cuban, Central American, South American, Other Hispanic

#### 3.4 SPECIAL POPULATIONS - ~200 variables
| Population Group | Variables |
|------------------|-----------|
| Veterans | Count, % of adult population, by age, by gender, by era of service |
| Foreign-born | Count, % of population, by region of origin, by citizenship status |
| Language spoken at home | Households, % speaking language other than English, linguistic isolation |
| Disability status | Persons with disabilities, by age group, by type (hearing, vision, cognitive, ambulatory, self-care, independent living) |
| Group quarters population | Count, institutionalized (prisons, nursing homes), non-institutionalized (college dorms, military barracks) |

#### 3.5 HOUSEHOLDS & FAMILIES - ~100 variables
| Category | Variables |
|----------|-----------|
| Total households | Count, average household size |
| Family households | Count, married-couple, single-parent (male, female) |
| Nonfamily households | Count, living alone, 65+ alone |
| Households with children under 18 | Count, % of households |

---

### CATEGORY 4: ECONOMICS (~800 variables)

Income, poverty, employment, and economic characteristics

#### 4.1 INCOME - ~250 variables
| Income Measure | Variables | Breakdowns |
|----------------|-----------|------------|
| Median household income | Dollars | Total, by race/ethnicity |
| Per capita income | " | " |
| Median family income | " | " |
| Mean household income | " | " |
| Income distribution | Households by income bracket | <$10k, $10-15k, $15-25k, $25-35k, $35-50k, $50-75k, $75-100k, $100-150k, $150-200k, $200k+ |
| Income inequality | Gini coefficient, 80/20 ratio | County-level |

**Data Sources:** Census Bureau Small Area Income and Poverty Estimates (SAIPE), ACS

**Time Series:** Annual 1989-2022

#### 4.2 POVERTY - ~200 variables
| Poverty Measure | Variables | Breakdowns |
|-----------------|-----------|------------|
| Persons below poverty | Count, % of population | Total, by age (<18, 18-64, 65+), by race/ethnicity |
| Families below poverty | Count, % of families | Total, with children under 18, female-headed households |
| Children in poverty | Count, % of children <18 | Total, by race/ethnicity |
| Elderly in poverty | Count, % of 65+ | Total, by race/ethnicity |
| Deep poverty | % below 50% poverty threshold | Total |
| Poverty ratio categories | % population by FPL ratio | <50%, 50-99%, 100-124%, 125-149%, 150-199%, 200%+ |

**SNAP (Food Stamps):**
- Households receiving SNAP
- Persons receiving SNAP
- % of population receiving SNAP

#### 4.3 EMPLOYMENT & LABOR FORCE - ~200 variables
| Employment Measure | Variables | Breakdowns |
|--------------------|-----------|------------|
| Civilian labor force | Count, % of population 16+ | Total, by sex |
| Employed persons | Count, employment rate | Total, by sex, by industry, by occupation |
| Unemployed persons | Count, unemployment rate | Total, by sex |
| Not in labor force | Count, % of population 16+ | Total, discouraged workers, retired |

**Employment by Industry:** (NAICS)
- Agriculture, forestry, fishing
- Mining, quarrying, oil & gas
- Construction
- Manufacturing
- Wholesale trade
- Retail trade
- Transportation & warehousing
- Utilities
- Information
- Finance & insurance
- Real estate
- Professional, scientific, technical services
- Management of companies
- Administrative & waste services
- Educational services
- Health care & social assistance
- Arts, entertainment, recreation
- Accommodation & food services
- Public administration

**Employment by Occupation:** (SOC)
- Management
- Business & financial operations
- Computer & mathematical
- Architecture & engineering
- Life, physical, social science
- Community & social service
- Legal
- Education, training, library
- Arts, design, entertainment, sports, media
- Healthcare practitioners
- Healthcare support
- Protective service
- Food preparation & serving
- Building & grounds maintenance
- Personal care & service
- Sales
- Office & administrative support
- Farming, fishing, forestry
- Construction & extraction
- Installation, maintenance, repair
- Production
- Transportation & material moving

**Data Sources:** BLS Local Area Unemployment Statistics (LAUS), Census Bureau County Business Patterns, ACS

#### 4.4 BUSINESS & ECONOMIC ACTIVITY - ~150 variables
| Category | Variables |
|----------|-----------|
| Total establishments | Count, by industry (NAICS) |
| Total employment | Employment count, by industry |
| Total payroll | Annual payroll $, by industry |
| Establishment size | Count by employee size class (1-4, 5-9, 10-19, 20-99, 100-499, 500+) |
| Employer firms | Count, by employee size |
| Nonemployer establishments | Count (self-employed, no employees) |
| Sales/receipts | Total revenue, by industry |

---

### CATEGORY 5: HEALTH PROFESSIONS TRAINING (~300 variables)

Educational programs and training capacity for healthcare workforce

#### 5.1 MEDICAL SCHOOLS & GRADUATES - ~80 variables
| Category | Variables |
|----------|-----------|
| Medical schools (MD-granting) | Count, enrollment, graduates |
| Osteopathic medical schools (DO) | " |
| Medical school faculty | Count, by specialty |
| Medical residents & fellows | Count, by specialty, by program |
| Graduate medical education (GME) programs | Count, by specialty |

**Data Sources:** AAMC, AACOM, ACGME

#### 5.2 NURSING EDUCATION - ~60 variables
| Program Type | Variables |
|--------------|-----------|
| Baccalaureate nursing programs (BSN) | Count, enrollment, graduates |
| Associate degree nursing programs (ADN) | " |
| Diploma nursing programs | " |
| Master's nursing programs (MSN) | " |
| Doctoral nursing programs (PhD, DNP) | " |
| Nurse practitioner programs | Count, graduates, by specialty |

**Data Sources:** AACN, NLN, state boards of nursing

#### 5.3 ALLIED HEALTH EDUCATION - ~100 variables
| Program Type | Variables |
|--------------|-----------|
| Physician assistant programs | Count, enrollment, graduates |
| Pharmacy schools | " |
| Dental schools | " |
| Dental hygiene programs | " |
| Physical therapy programs | " |
| Occupational therapy programs | " |
| Clinical laboratory science programs | " |
| Radiologic technology programs | " |
| Respiratory therapy programs | " |

#### 5.4 TEACHING HOSPITALS & ACADEMIC HEALTH CENTERS - ~60 variables
| Category | Variables |
|----------|-----------|
| Teaching hospitals | Count, beds, medical school affiliation |
| Academic health centers | Count, components (medical school, hospital, research) |
| Residency training capacity | Resident slots, by specialty |
| Fellowship training capacity | Fellow slots, by specialty |

---

### CATEGORY 6: HOSPITAL UTILIZATION (~400 variables)

Inpatient admissions, patient days, procedures, and service use

#### 6.1 INPATIENT UTILIZATION - ~150 variables
| Utilization Measure | Variables | Breakdowns |
|---------------------|-----------|------------|
| Total admissions | Count | All hospitals, community hospitals, by ownership |
| Admissions rate | Per 1,000 population | " |
| Medicare admissions | Count | All hospitals, by diagnosis (AMI, CHF, pneumonia, stroke, etc.) |
| Medicaid admissions | Count | All hospitals |
| Total patient days | Count | All hospitals, community hospitals |
| Average length of stay | Days | All hospitals, by diagnosis |
| Occupancy rate | % beds occupied | All hospitals, community hospitals |

**Admissions by Major Diagnostic Category (MDC):** (selected)
- Circulatory system
- Respiratory system
- Digestive system
- Musculoskeletal system
- Nervous system
- Pregnancy, childbirth, puerperium

#### 6.2 SURGICAL PROCEDURES - ~80 variables
| Procedure Category | Variables |
|--------------------|-----------|
| Total surgical operations | Count, rate per 1,000 pop |
| Inpatient surgeries | Count |
| Outpatient surgeries | Count |

**Specific Procedures:** (selected)
- Cardiac catheterization
- Coronary artery bypass graft (CABG)
- Percutaneous coronary intervention (PCI)
- Hip replacement
- Knee replacement
- Cesarean section
- Hysterectomy
- Appendectomy
- Cholecystectomy

#### 6.3 EMERGENCY DEPARTMENT UTILIZATION - ~60 variables
| Measure | Variables |
|---------|-----------|
| ED visits | Count, rate per 1,000 pop, by hospital |
| ED visits resulting in admission | Count, % of ED visits |
| Ambulatory-sensitive ED visits | Count, % (conditions treatable in primary care) |

#### 6.4 OUTPATIENT SERVICES - ~60 variables
| Service Category | Variables |
|------------------|-----------|
| Outpatient visits | Count, by service type |
| Ambulatory surgery visits | Count |
| Observation stays | Count |
| Diagnostic radiology | Procedures count |
| Laboratory tests | Tests count |

#### 6.5 SPECIALIZED UTILIZATION - ~50 variables
| Service | Variables |
|---------|-----------|
| Intensive care unit (ICU) days | Patient days, by ICU type (medical, surgical, cardiac, neonatal) |
| Mechanical ventilation | Cases, days |
| Dialysis treatments | Count, by modality (hemodialysis, peritoneal) |
| Chemotherapy | Visits, infusions |
| Radiation therapy | Treatments |

**Data Sources:** AHA Annual Survey, Medicare Provider Analysis and Review (MEDPAR), State Inpatient Databases (HCUP SID)

---

### CATEGORY 7: HEALTH STATUS (~600 variables)

Mortality, morbidity, disease prevalence, risk factors, and health outcomes

#### 7.1 MORTALITY - ~250 variables

**All-Cause Mortality:**
| Measure | Variables | Breakdowns |
|---------|-----------|------------|
| Total deaths | Count | By year, by sex, by race/ethnicity, by age group |
| Death rate | Per 100,000 population | Age-adjusted, crude |
| Infant mortality rate | Per 1,000 live births | Total, neonatal, postneonatal |
| Years of potential life lost (YPLL) | Rate per 100,000 pop <75 | Total |

**Cause-Specific Mortality:** (ICD-10 codes)
| Cause of Death | Variables |
|----------------|-----------|
| Diseases of heart | Deaths, age-adjusted rate |
| Malignant neoplasms (cancer) | " |
| - Lung cancer | " |
| - Colorectal cancer | " |
| - Breast cancer | " |
| - Prostate cancer | " |
| Cerebrovascular diseases (stroke) | " |
| Chronic lower respiratory diseases (COPD) | " |
| Accidents (unintentional injuries) | " |
| - Motor vehicle accidents | " |
| - Drug overdose | " |
| - Falls | " |
| Diabetes mellitus | " |
| Alzheimer's disease | " |
| Influenza & pneumonia | " |
| Nephritis, nephrotic syndrome (kidney disease) | " |
| Suicide | " |
| Chronic liver disease & cirrhosis | " |
| Hypertension & hypertensive renal disease | " |
| Parkinson's disease | " |
| Septicemia | " |
| Homicide | " |
| HIV disease | " |

**Maternal & Infant Health:**
- Maternal mortality rate
- Fetal deaths
- Neonatal deaths
- Postneonatal deaths
- Perinatal mortality rate

**Data Sources:** CDC WONDER (National Vital Statistics System), State vital records

**Time Series:** Annual 1980-2022 (most recent year varies by cause)

#### 7.2 NATALITY & REPRODUCTIVE HEALTH - ~100 variables
| Measure | Variables | Breakdowns |
|---------|-----------|------------|
| Total births | Count | By mother's race/ethnicity, age, marital status |
| Birth rate | Per 1,000 population | General fertility rate, age-specific rates |
| Teenage birth rate | Per 1,000 females 15-19 | Total, 15-17, 18-19 |
| Low birthweight | % births <2,500g | Total, very low (<1,500g) |
| Preterm births | % births <37 weeks gestation | Total, very preterm (<32 weeks) |
| Prenatal care | % receiving 1st trimester care | Total, by race/ethnicity |
| Cesarean delivery | % deliveries by C-section | Total, primary, repeat |

**Data Sources:** CDC WONDER (Natality Files), State vital records

#### 7.3 CHRONIC DISEASE PREVALENCE - ~100 variables

**From CDC BRFSS Model-Based Small Area Estimates:**
| Disease/Condition | Variable | Unit |
|-------------------|----------|------|
| Arthritis | % adults | Age-adjusted prevalence |
| Asthma (current) | " | " |
| Coronary heart disease | " | " |
| Stroke | " | " |
| COPD | " | " |
| Diabetes | " | " |
| Chronic kidney disease | " | " |
| Cancer (excluding skin) | " | " |
| High blood pressure | " | " |
| High cholesterol | " | " |

**From CMS Medicare Data:**
| Condition | Variable | Unit |
|-----------|----------|------|
| Alzheimer's/dementia | % Medicare beneficiaries | Prevalence |
| Atrial fibrillation | " | " |
| Chronic kidney disease | " | " |
| COPD | " | " |
| Depression | " | " |
| Diabetes | " | " |
| Heart failure | " | " |
| Hypertension | " | " |
| Ischemic heart disease | " | " |
| Osteoporosis | " | " |
| Rheumatoid arthritis/osteoarthritis | " | " |
| Stroke/TIA | " | " |

#### 7.4 HEALTH RISK FACTORS - ~80 variables

**Behavioral Risk Factors (BRFSS):**
| Risk Factor | Variable | Unit |
|-------------|----------|------|
| Current smoking | % adults | Age-adjusted prevalence |
| Binge drinking | " | " |
| Physical inactivity | " | " |
| Obesity (BMI ≥30) | " | " |
| No leisure-time physical activity | " | " |
| <5 fruits/vegetables per day | " | " |

**Clinical Preventive Services:**
| Service | Variable | Unit |
|---------|----------|------|
| Cholesterol screening | % adults screened | Age-adjusted |
| Colorectal cancer screening | % adults 50-75 screened | " |
| Mammography | % women 50-74 screened | " |
| Flu vaccination | % adults vaccinated | " |
| Dental visit (past year) | % adults | " |
| Health insurance coverage | % adults uninsured | " |

#### 7.5 INFECTIOUS DISEASE - ~40 variables
| Disease | Variables |
|---------|-----------|
| HIV prevalence | Cases, rate per 100,000 |
| AIDS cases | Cumulative, annual |
| Tuberculosis | Cases, rate per 100,000 |
| Sexually transmitted infections | Cases, rates (chlamydia, gonorrhea, syphilis) |
| Hepatitis A, B, C | Cases, rates |
| Lyme disease | Cases, rate per 100,000 |
| West Nile virus | Cases |

**Data Sources:** CDC National Notifiable Diseases Surveillance System (NNDSS), state health departments

#### 7.6 DISABILITY & FUNCTIONAL LIMITATIONS - ~30 variables
| Measure | Variables | Breakdowns |
|---------|-----------|------------|
| Disability prevalence | % population with any disability | By age group, by type |
| Disability types | % with specific disability | Hearing, vision, cognitive, ambulatory, self-care, independent living |
| Functional limitations | % adults | Difficulty walking, climbing stairs, dressing, bathing |

**Data Sources:** ACS, BRFSS

---

### CATEGORY 8: SOCIOECONOMIC & ENVIRONMENTAL CHARACTERISTICS (~700 variables)

Education, housing, crime, environment, and community characteristics

#### 8.1 EDUCATION - ~200 variables
| Educational Attainment | Variables | Breakdowns |
|------------------------|-----------|------------|
| Less than 9th grade | % adults 25+ | By sex, race/ethnicity |
| 9th-12th grade, no diploma | " | " |
| High school graduate | " | " |
| Some college, no degree | " | " |
| Associate degree | " | " |
| Bachelor's degree | " | " |
| Graduate/professional degree | " | " |
| High school graduation rate | % of 9th grade cohort graduating in 4 years | By race/ethnicity |

**School Enrollment:**
- Enrolled in school (by age group)
- Nursery/preschool enrollment
- Elementary/secondary enrollment
- College/graduate school enrollment

**Educational Institutions:**
- Public schools (count)
- Private schools (count)
- Colleges & universities (count)
- Student enrollment (total, by level)

**Data Sources:** ACS, Census Bureau Small Area Estimates, National Center for Education Statistics (NCES) Common Core of Data

#### 8.2 HOUSING - ~180 variables
| Housing Characteristic | Variables | Breakdowns |
|------------------------|-----------|------------|
| Total housing units | Count | Occupied, vacant |
| Occupancy status | Count, % | Owner-occupied, renter-occupied |
| Vacancy status | Count, % | For rent, for sale, seasonal, other vacant |
| Median home value | Dollars | Owner-occupied units |
| Median gross rent | Dollars per month | Renter-occupied units |
| Housing cost burden | % households spending ≥30% income on housing | Owners with mortgage, renters |
| Severe housing cost burden | % spending ≥50% | " |
| Year structure built | Units by decade | Pre-1940, 1940-49, ..., 2010-2019, 2020+ |
| Units in structure | Count | Single-family detached, attached, 2-4 units, 5-9, 10-19, 20-49, 50+, mobile home |
| Rooms per unit | Distribution | 1 room, 2, 3, 4, 5, 6, 7, 8, 9+ rooms |
| Bedrooms | Distribution | No bedroom, 1, 2, 3, 4, 5+ bedrooms |
| Vehicles available | Households by vehicle count | None, 1, 2, 3+ vehicles |
| Lacking complete plumbing | % units | Total |
| Lacking complete kitchen | % units | Total |
| Crowding | % units with >1 person per room | Total, severe (>1.5) |

**Data Sources:** ACS, Decennial Census

#### 8.3 CRIME & SAFETY - ~60 variables

**FBI Uniform Crime Reporting (UCR):**
| Crime Type | Variables |
|------------|-----------|
| Violent crime | Offenses, rate per 100,000 |
| - Murder & nonnegligent manslaughter | " |
| - Rape | " |
| - Robbery | " |
| - Aggravated assault | " |
| Property crime | Offenses, rate per 100,000 |
| - Burglary | " |
| - Larceny-theft | " |
| - Motor vehicle theft | " |
| - Arson | " |

**Law Enforcement:**
- Law enforcement employees (count)
- Law enforcement officers (count)
- Civilian employees (count)

**Data Sources:** FBI UCR Program

#### 8.4 GEOGRAPHY & ENVIRONMENT - ~120 variables
| Category | Variables |
|----------|-----------|
| Land area | Square miles, square kilometers |
| Water area | Square miles, square kilometers |
| Population density | Persons per square mile |
| Geographic classification | Metropolitan/micropolitan, rural, urban |
| CBSA (Core-Based Statistical Area) | Name, code, metro/micro designation |
| USDA Rural-Urban Continuum Code | 1-9 scale (metro size, adjacency, urbanization) |
| USDA Urban Influence Code | 1-12 scale |
| Frontier & Remote Area (FAR) Code | Level 1-4 |
| Census region & division | Northeast, South, Midwest, West; 9 divisions |
| State FIPS code | 2-digit code |
| County FIPS code | 3-digit code |

**Environmental Quality:** (selected variables)
- Air Quality Index (AQI) days
- Water quality violations (SDWA)
- Superfund sites (EPA NPL)
- Brownfield sites

#### 8.5 TRANSPORTATION & COMMUTING - ~80 variables
| Category | Variables |
|----------|-----------|
| Means of transportation to work | % workers | Drive alone, carpool, public transit, walk, other, work from home |
| Travel time to work | % workers by time bracket | <15 min, 15-29, 30-44, 45-59, 60+ min |
| Vehicles available per household | Mean vehicles | By household type |

**Data Sources:** ACS

#### 8.6 INTERNET & TECHNOLOGY ACCESS - ~30 variables
| Category | Variables |
|----------|-----------|
| Computer ownership | % households with computer | Desktop, laptop, smartphone, tablet |
| Internet subscription | % households with internet | Broadband, dial-up, satellite, mobile data plan |
| No internet access | % households | Total |

#### 8.7 SOCIAL ASSOCIATIONS & CIVIC ENGAGEMENT - ~30 variables
| Category | Variables |
|----------|-----------|
| Religious organizations | Count per 10,000 pop |
| Civic organizations | " |
| Business associations | " |
| Political organizations | " |
| Labor organizations | " |
| Social advocacy organizations | " |
| Voter registration | % voting-age population registered |
| Voter turnout | % voting-age population voting | Presidential elections, midterms |

**Data Sources:** County Business Patterns, IRS Business Master File, Election Assistance Commission

---

## 🔍 HOW TO USE AHRF FOR COUNTY-LEVEL RESEARCH

### R Example: Import and Analyze AHRF Data

```r
library(tidyverse)
library(readxl)
library(haven)

# Download AHRF data from https://data.hrsa.gov/data/download?data=AHRF
# Extract ZIP file to working directory

# Option 1: Read SAS file
ahrf_county <- read_sas("AHRF_2023-2024/AHRF_County.sas7bdat")

# Option 2: Read CSV file
ahrf_county <- read_csv("AHRF_2023-2024/AHRF_County.csv")

# Option 3: Read ASCII with SAS import script
# (Use included SAS input script to read fixed-width ASCII file)

# Read technical documentation (Excel file with variable definitions)
ahrf_codebook <- read_excel("AHRF_2023-2024/AHRF_Tech_Doc_2023-2024.xlsx")

# View variable names and descriptions
ahrf_vars <- ahrf_codebook %>%
  select(Variable_Name, Variable_Label, Source, Years_Available) %>%
  arrange(Variable_Name)

# Example: Extract healthcare workforce variables for Travis County, TX
travis_health <- ahrf_county %>%
  filter(
    f12424 == "48",  # Texas state FIPS
    f12430 == "453"  # Travis county FIPS
  ) %>%
  select(
    fips = f12430,
    county_name = f12420,
    state = f12424,

    # Population (2022)
    pop_total_2022 = f04530_22,

    # Primary care physicians (2022)
    pc_phys_2022 = f08860_22,
    pc_phys_rate_2022 = f09920_22,  # Per 100,000 pop

    # Specialists
    specialists_2022 = f08870_22,

    # Nurses
    rn_2022 = f16564_22,
    np_2022 = f16572_22,

    # Dentists
    dentists_2022 = f08815_22,

    # Hospitals
    hospitals_2022 = f08921_22,
    hospital_beds_2022 = f08934_22,

    # Health outcomes
    infant_mort_rate = f11598_22,  # Per 1,000 live births

    # Socioeconomic
    median_hh_income_2022 = f13321_22,
    pct_poverty_2022 = f13836_22,
    pct_uninsured_2022 = f15332_22
  )

print(travis_health)

# Calculate physician-to-population ratios
travis_health <- travis_health %>%
  mutate(
    total_physicians = pc_phys_2022 + specialists_2022,
    physicians_per_100k = (total_physicians / pop_total_2022) * 100000,
    nurses_per_100k = (rn_2022 / pop_total_2022) * 100000,
    beds_per_1k = (hospital_beds_2022 / pop_total_2022) * 1000
  )

# Export
write_csv(travis_health, "travis_county_ahrf_2022.csv")
```

### Python Example: Analyze AHRF Data

```python
import pandas as pd
import numpy as np

# Read AHRF county file (CSV format)
ahrf = pd.read_csv("AHRF_2023-2024/AHRF_County.csv", low_memory=False)

# Read technical documentation
codebook = pd.read_excel("AHRF_2023-2024/AHRF_Tech_Doc_2023-2024.xlsx")

# Create FIPS code
ahrf['fips'] = ahrf['f12424'].astype(str).str.zfill(2) + \
                ahrf['f12430'].astype(str).str.zfill(3)

# Example: Extract primary care physician data for all counties (2022)
pc_phys_data = ahrf[['fips', 'f12420', 'f12424', 'f08860_22', 'f09920_22', 'f04530_22']].copy()
pc_phys_data.columns = ['fips', 'county_name', 'state_fips',
                        'pc_physicians', 'pc_phys_rate', 'population']

# Filter to non-missing data
pc_phys_data = pc_phys_data[pc_phys_data['pc_physicians'].notna()]

# Calculate national percentiles
pc_phys_data['pc_phys_percentile'] = pc_phys_data['pc_phys_rate'].rank(pct=True) * 100

# Identify counties with physician shortages (bottom 25th percentile)
shortage_counties = pc_phys_data[pc_phys_data['pc_phys_percentile'] <= 25]

print(f"Counties with PC physician shortages: {len(shortage_counties)}")
print(f"Mean PC physician rate (shortage counties): {shortage_counties['pc_phys_rate'].mean():.1f}")
print(f"Mean PC physician rate (all counties): {pc_phys_data['pc_phys_rate'].mean():.1f}")

# Export
shortage_counties.to_csv("physician_shortage_counties_2022.csv", index=False)
```

### Multi-Year Trend Analysis

```r
# Extract primary care physician trends over time for all counties
pc_trends <- ahrf_county %>%
  select(
    fips = f12430,
    county = f12420,
    state = f12424,

    # Primary care physicians by year
    pc_2010 = f08860_10,
    pc_2015 = f08860_15,
    pc_2020 = f08860_20,
    pc_2022 = f08860_22,

    # Population by year
    pop_2010 = f04530_10,
    pop_2015 = f04530_15,
    pop_2020 = f04530_20,
    pop_2022 = f04530_22
  ) %>%

  # Calculate rates per 100k
  mutate(
    pc_rate_2010 = (pc_2010 / pop_2010) * 100000,
    pc_rate_2015 = (pc_2015 / pop_2015) * 100000,
    pc_rate_2020 = (pc_2020 / pop_2020) * 100000,
    pc_rate_2022 = (pc_2022 / pop_2022) * 100000,

    # Calculate percent change
    pct_change_2010_2022 = ((pc_rate_2022 - pc_rate_2010) / pc_rate_2010) * 100
  )

# Summarize
summary(pc_trends$pct_change_2010_2022)

# Identify counties with declining physician supply
declining <- pc_trends %>%
  filter(pct_change_2010_2022 < 0) %>%
  arrange(pct_change_2010_2022)

cat(sprintf("%d counties experienced declining PC physician supply 2010-2022\n",
            nrow(declining)))
```

---

## 📚 COMPANION DATA SOURCES

### CMS Geographic Variation Public Use Files
**URL:** https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Geographic-Variation

**Description:** Medicare utilization, spending, quality by county
- Complements AHRF hospital utilization data
- County-level Medicare fee-for-service data
- Per capita spending, utilization rates
- Quality measures

### CDC PLACES (Local Data for Better Health)
**URL:** https://www.cdc.gov/places

**Description:** County-level chronic disease and prevention data
- Model-based small area estimates
- 36 chronic disease measures
- 13 health status measures
- 9 disability measures
- County, place, census tract, ZIP code levels
- Complements AHRF Category 7 (Health Status)

### HRSA Data Warehouse - Additional Datasets
**URL:** https://data.hrsa.gov/data/download

**Description:** Supplementary HRSA data sources
- Health Professional Shortage Areas (HPSA) shapefiles
- Medically Underserved Areas/Populations (MUA/MUP)
- Health Center service delivery sites
- NHSC & Nurse Corps placements
- Ryan White HIV/AIDS program data

### County Health Rankings & Roadmaps
**URL:** https://www.countyhealthrankings.org/

**Description:** County health outcome and factor rankings
- Synthesizes AHRF and other sources
- Composite health rankings by county
- Social determinants of health
- Health behaviors, clinical care, physical environment

### Dartmouth Atlas of Health Care
**URL:** https://www.dartmouthatlas.org/

**Description:** Hospital referral region (HRR) analysis
- Medicare utilization patterns
- End-of-life care intensity
- Surgical procedure rates
- Complements AHRF hospital data with HRR aggregations

---

## 📝 CITATION

**Recommended Citation Format:**

U.S. Department of Health and Human Services, Health Resources and Services Administration, Bureau of Health Workforce, 2024. Area Health Resources Files (AHRF) 2023-2024 Release. Rockville, MD. Available at https://data.hrsa.gov/topics/health-workforce/ahrf.

---

## 🔗 RELATED TIER 1 COMPREHENSIVE DOCUMENTATION

This catalog provides complete variable listings for HRSA AHRF. For integration with broader environmental health research, see:

**[HEALTH_SYSTEMS_OUTCOMES_COMPREHENSIVE.md](HEALTH_SYSTEMS_OUTCOMES_COMPREHENSIVE.md)**
- Section on "Healthcare Access & Utilization (AHRF)"
- Healthcare workforce and facility variables
- Integration with health outcomes
- Environmental health exposure-response analyses

---

## 📌 NOTES ON AHRF STRUCTURE

### Variable Naming Convention
AHRF variables follow a systematic naming pattern:
- **fXXXXX_YY:** Field number (5 digits) + underscore + data year (2 digits)
- Example: `f08860_22` = Field 08860 (Primary care physicians) for year 2022
- Technical documentation Excel file provides crosswalk: Field # → Variable name → Source

### Geographic Identifiers
| Variable | Description |
|----------|-------------|
| f12424 | State FIPS code (2-digit) |
| f12430 | County FIPS code (3-digit, append to state FIPS) |
| f12420 | County name |
| f04437 | CBSA code |
| f00012 | Rural-Urban Continuum Code |
| f00011 | Urban Influence Code |

### Missing Data Codes
- **-9:** Data not available
- **-8:** Data suppressed for confidentiality
- **-1:** Not applicable
- **Blank:** No data reported

### Data Vintages
- Most recent release: 2023-2024 (November 2024)
- Historical files available: 2009-2010 through 2023-2024
- Variables span different years (e.g., 2010, 2015, 2020, 2022, 2023)
- Check technical documentation for specific variable year availability

### File Sizes
- **County file:** 3,143 rows (counties) × 6,000+ columns (variables) = ~50 MB (CSV)
- **State file:** 50 rows × aggregated variables
- **National file:** 1 row × summary statistics
- **Technical documentation:** Excel file with variable catalog (critical reference)

---

**Document Version:** 1.0
**Last Updated:** November 2024 (2023-2024 AHRF Release)
**Maintainer:** HRSA Bureau of Health Workforce

**Total Documented Variables:** 6,000+
**Major Categories:** 8
**Official Source:** https://data.hrsa.gov/topics/health-workforce/ahrf
