# Example: Coding
---
Task: Implement a new feature with database migration.
---
Execution: Agent writes migration script. Realizes the schema change
requires updating 3 related models. Updating models requires updating
API handlers. Updating handlers requires updating frontend components.
Each layer reveals more dependencies.
---
Health assessment: Requirement Health flagged. Scope expanded from one
task to five interconnected tasks. Unknown unknowns now exceed known
work. Confidence HIGH because new dependencies are structurally required.
---
Policy check: This is the first gate. The migration has not run yet.
No user waiver active.
---
Gate route: Coordination, Checkpoint and Ask User.
Recommendation: Save current progress. Present expanded scope estimate.
Ask whether to proceed with full chain or split into PRs.
---
Result without Decision Gate: Agent writes everything in one massive,
unreviewable PR that may contain errors from late-stage fatigue.
Result with Decision Gate: Scope is confirmed early. Work is split
into manageable, reviewable units.
