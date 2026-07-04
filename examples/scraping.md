# Example: Web Scraping
---
Task: Scrape contact information from 50 university websites.
---
Initial estimate: 2 minutes per site, about 2 hours total.
---
Execution: First 12 sites complete smoothly using template-based extraction.
Remaining 38 sites are found to use custom React SPAs requiring per-site
Playwright scripting. Each now takes 10 to 15 minutes.
---
Health assessment: Execution Health flagged. Time per unit increased from
2 min to 10 to 15 min, exceeding 3x threshold. Confidence HIGH because the
frontend technology change is structural, not incidental.
---
Policy check: No user waiver active. No mandatory gate.
---
Gate route: Coordination, Ask User.
Options presented:
A. Continue all 50 sites: 6 to 10 hours remaining, 100 percent coverage.
B. Prioritize top 20 by ranking: about 2 hours, 80 percent coverage.
C. Deliver the 12 completed now, expand on request: 0 hours, 24 percent.
---
Result without Decision Gate: Agent continues scraping for 6 plus hours
before context exhaustion or user intervention.
Result with Decision Gate: User makes informed decision at the 30 minute
mark. Time and tokens saved: significant.
