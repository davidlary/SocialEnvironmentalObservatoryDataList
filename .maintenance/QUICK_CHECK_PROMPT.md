# QUICK CHECK PROMPT (30-60 minutes)
## Rapid Repository Health Check

Use this for **monthly** quick checks between comprehensive quarterly updates.

---

## 🚀 QUICK HEALTH CHECK FOR CLAUDE CODE

**Working Directory:** `/Users/davidlary/Dropbox/Environments/Code/GetData/SocialEnvironmentalObservatoryDataList`

---

## TASK 1: Critical Source Updates (15 min)

Check the 5 most important sources for new data:

1. **NHGIS** (https://www.nhgis.org/)
   - Latest ACS year available?
   - Any new time series tables?

2. **CDC WONDER Mortality** (https://wonder.cdc.gov/)
   - Latest year available?
   - Any new underlying cause codes?

3. **EPA AQS Air Quality** (https://www.epa.gov/outdoor-air-quality-data)
   - Latest year available?
   - Any monitoring network changes?

4. **USGS NWIS Water** (https://waterdata.usgs.gov/nwis)
   - Still operational?
   - Any service disruptions?

5. **ERA5 Climate** (https://cds.climate.copernicus.eu/)
   - Latest month available?
   - Any access changes?

**Action:** Update temporal coverage in documentation if changed.

---

## TASK 2: Link Verification (10 min)

Test 10 random URLs from documentation:
```bash
# Pick 10 random files
find . -name "*.md" -type f | grep -E "^./[0-9]" | shuf -n 10
```

For each file, test 1-2 main URLs.

**Action:** Fix any broken links found.

---

## TASK 3: Recent Data Releases (15 min)

Quick search for major announcements:
- Google: "EPA new dataset [current month]"
- Google: "USGS new data release [current month]"
- Google: "CDC new county data [current month]"
- Check: https://catalog.data.gov/dataset?q=county&sort=metadata_modified+desc

**Action:** Note any major new sources for next comprehensive update.

---

## TASK 4: Repository Check (10 min)

```bash
# Verify no uncommitted changes
git status

# Check recent commits
git log --oneline -5

# Verify synced with remote
git fetch origin
git status

# Count files
find . -name "*.md" -type f | grep -E "^./[0-9]" | wc -l
```

**Action:** Commit and push if any updates made.

---

## TASK 5: User Issues (5 min)

If GitHub issues exist:
- Review any reported broken links
- Note feature requests
- Respond to questions

---

## QUICK UPDATE COMMIT

```bash
git add -A
git commit -m "Quick check update [DATE]

- Verified critical sources current
- Tested sample URLs
- [Note any updates made]

🤖 Claude Code quick check"

git push origin main
```

---

## OUTPUT

Create brief note in `.maintenance/quick_checks/`:

**File:** `check_[YYYY-MM-DD].txt`

```
QUICK CHECK - [DATE]

CRITICAL SOURCES:
✓ NHGIS: [Status]
✓ CDC WONDER: [Status]
✓ EPA AQS: [Status]
✓ USGS NWIS: [Status]
✓ ERA5: [Status]

LINKS TESTED: [Count] - [X broken, X fixed]

NEW SOURCES IDENTIFIED: [List or "None"]

ISSUES: [List or "None"]

NEXT COMPREHENSIVE UPDATE DUE: [Date]
```

---

**Use this monthly to catch issues early before quarterly comprehensive updates!**
