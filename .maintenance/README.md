# Repository Maintenance Documentation

This directory contains maintenance prompts and update histories for the Social Environmental Observatory Data List.

---

## 📋 Maintenance Schedule

### Recommended Update Frequency

| Type | Frequency | Time Required | Prompt File |
|------|-----------|---------------|-------------|
| **Quick Check** | Monthly | 30-60 minutes | `QUICK_CHECK_PROMPT.md` |
| **Comprehensive Update** | Quarterly | 2-4 hours | `PERIODIC_UPDATE_PROMPT.md` |
| **Major Revision** | Annually | 1-2 days | Use comprehensive + deep review |

---

## 🔄 How to Use These Prompts

### Method 1: Direct Copy-Paste to Claude Code

1. Open Claude Code (https://claude.com/code)
2. Navigate to repository directory:
   ```
   cd /Users/davidlary/Dropbox/Environments/Code/GetData/SocialEnvironmentalObservatoryDataList
   ```
3. Copy the entire contents of `PERIODIC_UPDATE_PROMPT.md` or `QUICK_CHECK_PROMPT.md`
4. Paste into Claude Code
5. Claude will autonomously execute all phases
6. Review outputs and approve git push

### Method 2: Command File

```bash
# From repository root:
cat .maintenance/PERIODIC_UPDATE_PROMPT.md | pbcopy
# Paste into Claude Code
```

### Method 3: Reference in Conversation

Simply tell Claude Code:
```
Please execute the periodic update prompt located at
.maintenance/PERIODIC_UPDATE_PROMPT.md in this repository
```

---

## 📁 Directory Structure

```
.maintenance/
├── README.md                      # This file
├── PERIODIC_UPDATE_PROMPT.md      # Comprehensive quarterly update
├── QUICK_CHECK_PROMPT.md          # Monthly quick health check
├── changelogs/                    # Update history
│   ├── CHANGELOG_2025-11-13.md   # Initial creation
│   └── CHANGELOG_[YYYY-MM-DD].md # Future updates
└── quick_checks/                  # Monthly check logs
    └── check_[YYYY-MM-DD].txt    # Quick check results
```

---

## 📝 Maintenance History

### Version 4.0 - November 13, 2025 (Initial Creation)
- Created comprehensive data catalog structure
- Documented 43,000+ variables from 200+ sources
- Established 98% completeness of available county-level data
- Key additions: NHGIS priority, asbestos occurrence, beach closures
- Established maintenance framework

### Future Updates
[Document each quarterly update here]

---

## 🎯 Priority Sources to Monitor

### Critical (Check Every Update)
1. **NHGIS** - Pre-harmonized demographic/economic data
2. **CDC WONDER** - Mortality data
3. **EPA SDWIS** - Drinking water violations
4. **EPA AQS** - Air quality monitoring
5. **ERA5** - Climate reanalysis

### High Priority (Check Quarterly)
6. USGS NWIS - Water quality
7. TRI - Toxic releases
8. SEER - Cancer incidence
9. Agricultural Census/NASS
10. CDC PLACES - Health prevalence

### Watch for Major Releases
- Decennial Census (every 10 years)
- Agricultural Census (every 5 years)
- NLCD Land Cover (every 2-3 years)
- New EPA regulations (drinking water MCLs, air quality NAAQS)
- New disease registries

---

## 🔧 Maintenance Best Practices

### Before Starting Update
- [ ] Ensure clean git status (`git status`)
- [ ] Pull latest from remote (`git pull origin main`)
- [ ] Set aside sufficient time (don't rush)
- [ ] Have GitHub credentials ready

### During Update
- [ ] Work systematically through all phases
- [ ] Document all findings (even if "no changes")
- [ ] Test sample links/APIs before updating
- [ ] Keep detailed notes of issues encountered

### After Update
- [ ] Create comprehensive changelog
- [ ] Update version numbers in README and MASTER_INDEX
- [ ] Commit with detailed message
- [ ] Push to remote
- [ ] Verify remote shows updates

### Git Commit Message Template
```
Periodic maintenance update [QUARTER/YEAR]

UPDATES:
- Temporal coverage: [Updated X sources to YYYY]
- New sources: [List or "None added"]
- Variables: [Expanded in X sources, added Y variables]
- Links: [Fixed X broken links]
- Metadata: [FIPS/boundary updates if any]

FINDINGS:
- [Note any significant changes]
- [Deprecated sources]
- [Emerging data gaps]

Version: 4.X
Files modified: X
Lines changed: +XXX/-XXX

🤖 Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>
```

---

## 📊 Update Metrics to Track

For each update, document:
- **Sources checked:** [Count]
- **Sources updated:** [Count]
- **New sources added:** [Count]
- **Variables added:** [Estimate]
- **Links tested:** [Count]
- **Links fixed:** [Count]
- **Time spent:** [Hours]
- **Version increment:** X.X → X.X

---

## 🚨 When to Do Major Revision (Version X.0)

Trigger a major revision when:
- Decennial Census release (major demographic update)
- Significant reorganization needed (>20% files restructured)
- New data collection paradigm (e.g., AI/ML-derived county estimates)
- Breaking changes to multiple major sources
- Adding 10+ new major data sources

Major revisions may require 1-2 days and should involve:
- Complete file structure review
- All links tested
- All code examples tested
- Comprehensive disease-environment literature review
- User feedback integration

---

## 🐛 Common Issues & Solutions

### Issue: Source URL has changed
**Solution:** Search "[source name] site:gov" or use Wayback Machine

### Issue: API endpoint deprecated
**Solution:** Check data provider's API documentation, update code examples

### Issue: New authentication required
**Solution:** Document in file, provide instructions for obtaining API keys

### Issue: Data temporarily unavailable
**Solution:** Note in documentation, set reminder to check again in 1-3 months

### Issue: Source permanently discontinued
**Solution:** Move to "deprecated sources" section, suggest alternatives

### Issue: File size exceeds 100KB
**Solution:** Split into multiple files, move exhaustive lists to Tier 2 catalogs

---

## 📧 Contacts for Questions

- **Repository Maintainer:** David Lary (davidlary@me.com)
- **GitHub Issues:** [Repository URL]/issues
- **Data Source Questions:** Consult individual source documentation

---

## 📚 Additional Resources

### Useful Tools
- **Link Checker:** https://validator.w3.org/checklink
- **API Testing:** Postman, curl, httpie
- **Git GUI:** GitHub Desktop, GitKraken (if preferred over command line)

### Monitoring Services to Consider
- **Uptimerobot:** Monitor critical data source URLs
- **RSS Feeds:** Subscribe to EPA/USGS/CDC data release feeds
- **Google Alerts:** "county level environmental data"

### Reference Documentation
- Git version control: https://git-scm.com/doc
- Markdown syntax: https://www.markdownguide.org/
- GitHub workflow: https://docs.github.com/

---

**Last Updated:** November 13, 2025
**Maintenance Framework Version:** 1.0
