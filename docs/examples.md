# Examples

Real-world scenarios showing how Decision Gate routes execution.

## Scraping: Execution Health Failure
Task: Scrape 50 university websites. Progress: 12 done at 2 min each.
Remaining 38 use React SPAs at 10-15 min each. Health: Execution Health
flagged, time per unit exceeding 3x, confidence HIGH. Policy: no override
active. Route: Coordination, Ask User. Options: Continue all 50 at 6-10h
100 percent coverage. Prioritize top 20 at 2h 80 percent coverage.
Deliver 12 now at 0h 24 percent coverage.

## Debugging: Decision Health Failure
Task: Fix the CI pipeline. Progress: lint fixed. Tests reveal 14 failures
across 3 categories. Health: Decision Health flagged, multiple paths,
confidence HIGH. Route: Coordination, Ask User. Options: Fix all at 1-3h
high uncertainty. Fix snapshot and config at 1h. Roll back to green at
30 min.

## Database: Policy Override
Task: Clean up database. Progress: agent identifies DROP TABLE command.
Health: zero signals, Threshold 0, Confidence 100 percent. Policy:
mandatory gate for destructive operations. Route: Coordination, Escalate.
Require explicit user confirmation.

## Research: Multiple Source Ambiguity
Task: Research a topic for a report. Progress: found 5 conflicting
authoritative sources. Health: Requirement Health flagged, 3 judgment
calls without user input, confidence HIGH. Route: Coordination, Ask User.
Options: Include all sources with analysis. Prioritize most recent. Use
most cited source as primary.
