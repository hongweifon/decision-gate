# Example: Debugging
---
Task: Fix the CI pipeline that has been failing.
---
Execution: Agent fixes 2 lint errors. Then discovers 14 test failures
across 3 categories: snapshot drift, dependency mismatch, environment
configuration. Fixing dependency mismatch reveals a breaking change in
an upstream library. Fixing that breaks the build script.
---
Health assessment: Execution Health flagged. Multiple new error categories
emerging after each fix attempt, unknown work exceeds known work.
Confidence HIGH because the error cascade is structural.
---
Policy check: No user waiver active. No mandatory gate.
---
Gate route: Coordination, Ask User.
Options presented:
A. Continue fixing all failures in sequence: 1 to 3 hours, high uncertainty.
B. Fix snapshot and config now, open issue for dependency upgrade: 1 hour.
C. Roll back CI to last green commit, apply minimal fixes: 30 minutes.
---
Result without Decision Gate: Agent applies patches in circles, potentially
introducing more breakage than it fixes.
Result with Decision Gate: User chooses B, avoiding dependency rabbit hole.
