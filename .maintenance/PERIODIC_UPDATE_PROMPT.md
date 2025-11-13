# PERIODIC UPDATE & ENHANCEMENT PROMPT
## Social Environmental Observatory Data List Maintenance

**Last Run:** [DATE]
**Recommended Frequency:** Quarterly or Semi-annually
**Estimated Time:** 2-4 hours with Claude Code

---

## 🎯 COMPREHENSIVE UPDATE INSTRUCTIONS FOR CLAUDE CODE

Please systematically review and update the Social Environmental Observatory Data List repository. Work autonomously through all phases, documenting findings and making all necessary updates.

**Working Directory:** `/Users/davidlary/Dropbox/Environments/Code/GetData/SocialEnvironmentalObservatoryDataList`

---

## PHASE 1: NEW DATA SOURCES (45 minutes)

### Task 1.1: Federal Agency New Releases
Research and identify NEW county-level data sources released since last update:

**EPA (Environmental Protection Agency)**
- Search: "EPA new data releases [current year]" + "county level"
- Check: https://www.epa.gov/data
- Check: EPA Open Data portal additions
- Look for: New monitoring programs, updated datasets, expanded coverage

**USGS (US Geological Survey)**
- Search: "USGS new datasets [current year]" + "county"
- Check: https://www.usgs.gov/products/data
- Check: ScienceBase catalog recent additions
- Look for: New water quality parameters, geologic datasets, land cover products

**CDC (Centers for Disease Control)**
- Search: "CDC new county-level data [current year]"
- Check: https://data.cdc.gov/browse?limitTo=datasets
- Check: CDC WONDER new databases
- Look for: New health outcome registries, expanded disease surveillance

**NOAA (National Oceanic and Atmospheric Administration)**
- Search: "NOAA climate data new [current year]"
- Check: https://www.ncei.noaa.gov/
- Look for: New climate datasets, updated normals, expanded monitoring

**Census Bureau**
- Check: New ACS tables, expanded variables
- Check: Most recent decennial census data availability
- Check: New experimental data products

**USDA (Agriculture, NRCS, ERS)**
- Check: Latest Agricultural Census release
- Check: New NASS QuickStats variables
- Check: Updated SSURGO soil data

**NASA Earth Observations**
- Check: New satellite data products with US county coverage
- Check: Giovanni/SEDAC new datasets

**NIH/NCI/NIA Health Registries**
- Check: New cancer/disease registries
- Check: Expanded geographic coverage

### Task 1.2: State & International Sources
- **State health departments:** New open data portals
- **International reanalysis:** ECMWF ERA6 (if released), new Copernicus services
- **Academic sources:** New openly available county-level datasets from major institutions

### Task 1.3: Scientific Literature Review
Search recent publications (past 6 months) for:
- "environmental health" + "county level" + "new data"
- "disease environment association" + "novel exposure"
- Review top environmental health journals for new exposure-disease pathways

**If NEW sources found:**
- Document source name, URL, variables, coverage, access method
- Assess priority (HIGH/MEDIUM/LOW based on research relevance)
- Add to appropriate directory with comprehensive documentation
- Update MASTER_INDEX and README

---

## PHASE 2: EXISTING SOURCE UPDATES (60 minutes)

### Task 2.1: Temporal Coverage Updates
For each documented data source, verify and update:

**Priority sources to check (do ALL):**
1. **NHGIS:** Latest ACS year available (check https://www.nhgis.org/)
2. **ERA5:** Verify temporal coverage still current
3. **CDC WONDER:** Latest mortality year available
4. **USGS NWIS:** Check data availability dates
5. **EPA AQS:** Latest air quality year
6. **EPA SDWIS:** Latest drinking water violations
7. **TRI:** Latest reporting year
8. **USDA Census of Agriculture:** Latest release year
9. **NLCD:** New land cover epoch released?
10. **SEER Cancer:** Latest diagnosis year
11. **CDC PLACES:** Latest year available
12. **HRSA AHRF:** Latest year available

**For each source:**
- Update "Coverage: YYYY-present" dates in documentation
- Update "Last Updated" dates in file headers
- Note any gaps in data availability
- Update code examples if API endpoints changed

### Task 2.2: New Variables in Existing Sources
Check if existing sources have added new variables:

**High Priority:**
- **NHGIS:** New ACS tables added?
- **USGS NWIS:** New parameter codes?
- **EPA TRI:** New chemicals added to list?
- **NASS QuickStats:** New agricultural variables?
- **CDC WONDER:** New ICD codes available?
- **HRSA AHRF:** New health workforce categories?

**If new variables found:**
- Add to relevant Tier 1 files
- Update Tier 2 complete catalogs if applicable
- Update variable counts in MASTER_INDEX

### Task 2.3: Changed Access Methods
Verify and update:
- API endpoints (test at least 5 major sources)
- Download URLs (check for redirects/broken links)
- Portal interfaces (note UI changes affecting workflows)
- Authentication requirements (new API keys needed?)

---

## PHASE 3: DATA QUALITY & ACCURACY (30 minutes)

### Task 3.1: Link Verification
Test critical links (sample 20-30 URLs):
- Official data source URLs
- API documentation links
- Download portals
- Technical documentation PDFs

**If broken links found:**
- Search for updated URLs
- Update documentation
- Note in commit message

### Task 3.2: Metadata Updates
Review and update:

**FIPS Codes:**
- Any new independent cities (Virginia)?
- Alaska boundary reorganizations?
- County name changes?

**County Boundaries:**
- New boundary changes to document?
- Recent redistricting effects?

**Geographic Crosswalks:**
- HUD ZIP-County crosswalk updated?
- New crosswalk sources available?

### Task 3.3: Code Example Testing
Spot-check code examples (test 3-5):
- R code for API access still works?
- Python code syntax current?
- Package versions need updating?
- Deprecated functions to replace?

---

## PHASE 4: DISEASE-ENVIRONMENT ASSOCIATIONS (30 minutes)

### Task 4.1: Recent Epidemiology Review
Search for NEW environmental risk factors (past 6 months literature):

**Disease classes to check:**
- Cancer (any new site-specific associations?)
- Cardiovascular disease
- Kidney disease
- Neurological disorders
- Reproductive/developmental
- Mental health
- Autoimmune diseases (county data emerging?)

**Emerging contaminants:**
- New PFAS compounds identified?
- Microplastics exposure data?
- New pesticides with health concerns?

**Climate-health associations:**
- New evidence for heat/cold mortality?
- Extreme weather health impacts?
- Climate-sensitive infectious diseases?

**If new associations found:**
- Check if exposure data available at county level
- Add to relevant documentation if data exists
- Note in "Data Limitations" if data gap

### Task 4.2: Regulatory Changes
Check for new EPA/FDA/OSHA regulations affecting:
- Drinking water standards (new MCLs?)
- Air quality standards (NAAQS updates?)
- Chemical restrictions (new monitoring requirements?)

---

## PHASE 5: REPOSITORY OPTIMIZATION (20 minutes)

### Task 5.1: File Size Check
Verify no files exceed 100KB (context efficiency):
```bash
find . -name "*.md" -type f -size +100k
```

**If oversized files found:**
- Consider splitting into multiple files
- Move detailed catalogs to Tier 2 directory
- Maintain cross-references

### Task 5.2: Cross-Reference Verification
Check that related domains properly cross-reference:
- Pesticides ↔ Agriculture ↔ Water quality
- Air quality ↔ Mortality
- Social determinants ↔ Demographics ↔ Health outcomes

### Task 5.3: Completeness Check
Verify each numbered directory (01-25) has appropriate files:
- No empty directories (except intentional)
- All directories have comprehensive documentation
- README in 25_PAID_RESTRICTED_DATA current?

---

## PHASE 6: DOCUMENTATION UPDATES (30 minutes)

### Task 6.1: Update MASTER_INDEX
- Verify file counts accurate
- Update variable counts if sources expanded
- Add any new directories
- Update last modified date

### Task 6.2: Update README
- Update "Last Updated" date to current
- Verify Quick Start guide still accurate
- Check Data Scope section for temporal coverage
- Update "Version" number (increment minor: 4.0 → 4.1)

### Task 6.3: Update Metadata Files
- **TEMPORAL_COVERAGE_UPDATE_SCHEDULE.md:** Update known release schedules
- **NHGIS_COMPREHENSIVE_DOCUMENTATION.md:** Latest NHGIS version/year
- **FIPS_CODES_GEOGRAPHIC_IDENTIFIERS.md:** Any FIPS changes

### Task 6.4: Update Data Limitations
Add newly identified limitations:
- New data sources identified but not yet county-level
- Emerging data gaps
- Sources discontinued
- Temporal lags increased/decreased

---

## PHASE 7: GIT DOCUMENTATION (15 minutes)

### Task 7.1: Create Comprehensive Commit
```bash
git add -A
git commit -m "Periodic maintenance update [QUARTER/YEAR]

[Summarize major updates:]
- Updated temporal coverage: [X sources, new end dates]
- Added new data sources: [List if any]
- Updated variables: [List expanded sources]
- Fixed broken links: [Count]
- Metadata updates: [Describe]
- Version: 4.X

🤖 Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>"

git push origin main
```

### Task 7.2: Create Update Summary
Generate `CHANGELOG_[DATE].md` in `.maintenance/` documenting:
- All sources checked
- Updates made
- New additions
- Deprecated sources (if any)
- Issues found and resolved
- Recommendations for next update

---

## PHASE 8: FINAL VERIFICATION (10 minutes)

### Task 8.1: Consistency Check
- File counts in MASTER_INDEX match reality?
- Variable counts still reasonable estimates?
- All cross-references valid?
- Version numbers updated consistently?

### Task 8.2: Repository Statistics
Document current state:
```bash
# Total files
find . -name "*.md" -type f | grep -E "^./[0-9]" | wc -l

# Repository size
du -sh .

# Line count of documentation
find . -name "*.md" -type f -exec wc -l {} + | tail -1

# Last 10 commits
git log --oneline -10
```

### Task 8.3: Test Data Collection Workflow
Spot-check one complete workflow:
1. Navigate via MASTER_INDEX
2. Read metadata file (NHGIS or FIPS)
3. Access one data source file
4. Verify code example syntax
5. Check download URL works

---

## EXPECTED OUTPUTS

At completion, you should have:

✅ **Updated Documentation Files** (all changes committed)
✅ **MASTER_INDEX.md** (current file counts, variables, dates)
✅ **README.md** (updated version, date, statistics)
✅ **CHANGELOG_[DATE].md** (comprehensive update summary)
✅ **Git Repository** (all changes pushed to remote)
✅ **Verification Report** (documented in commit message)

---

## PRIORITY RANKINGS FOR UPDATES

**CRITICAL (Always Check):**
1. NHGIS temporal coverage
2. CDC WONDER mortality years
3. EPA drinking water/air quality
4. Major federal agency new releases

**HIGH (Check quarterly):**
5. USGS water quality
6. Climate data (PRISM, Daymet, ERA5)
7. TRI, pesticides
8. Cancer registries (SEER)
9. Agricultural census/NASS

**MEDIUM (Check semi-annually):**
10. Infrastructure data
11. Built environment
12. Social determinants
13. International sources

**LOW (Check annually):**
14. Paid/restricted data updates
15. Rare disease registries
16. Specialized monitoring programs

---

## TROUBLESHOOTING

**If you encounter:**
- **Broken links:** Use Wayback Machine or search for "site:gov [dataset name]"
- **API changes:** Check data source's "What's New" or changelog
- **Missing variables:** Contact data provider or check if moved to new product
- **Deprecated sources:** Document in Data Limitations, suggest alternatives

---

## POST-UPDATE CHECKLIST

- [ ] All PHASE 1-8 tasks completed
- [ ] MASTER_INDEX updated
- [ ] README updated
- [ ] CHANGELOG created
- [ ] Git committed with detailed message
- [ ] Git pushed to remote
- [ ] No uncommitted changes (`git status` clean)
- [ ] No broken links found
- [ ] Code examples spot-checked
- [ ] File sizes all <100KB
- [ ] Cross-references validated

---

## NOTES FOR NEXT UPDATE

[Document any issues, pending updates, or recommendations for future maintenance]

**Sources to watch:**
-

**Anticipated new releases:**
-

**Known issues to address:**
-

**Enhancement ideas:**
-

---

## VERSION HISTORY

| Update Date | Version | Major Changes | Updated By |
|-------------|---------|---------------|------------|
| 2025-11-13 | 4.0 | Initial comprehensive structure, NHGIS priority, asbestos, beach closures | Claude + David |
| [NEXT DATE] | 4.1 | [Summary] | [Name] |

---

**END OF PERIODIC UPDATE PROMPT**

Save this file and run it quarterly to maintain world-class data catalog currency!
