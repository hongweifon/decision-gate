# Decision Policy

## Policy Priority: Always Above Triggers
Decision Policy is the governing layer of Decision Gate. It wraps around
the entire system and can override, mandate, or redirect routing regardless
of what the Health Assessment or Trigger Engine report.
When Policy and the Trigger Engine disagree, Policy wins. No exceptions.
A DROP TABLE command has zero health signals (Threshold 0, Confidence 100
percent). The Engine sees nothing. But Policy: destructive operation ahead
forces Escalate. A user says always retry. The Engine proposes Re-plan
because failure rate is high. Policy: user waiver overrides to Retry.

## Mandatory Rules (Always Enforced)
Destructive operation: force gate regardless of health. Irreversible
action: require explicit confirmation. Critical safety constraint:
abort immediately. These rules fire even with zero health signals.

## Runtime Assessment Rules (Context-Dependent)
User waiver: do everything, do not ask suppresses health signals
unless risk is critical. Deadline awareness: escalate if remaining
time is less than estimated. Async mode: route to safest path, prefer
Execution Actions over Coordination, never Abort silently.

## Policy Override Examples
Scenario: 3 API 404s known outage. Threshold MET, Confidence HIGH,
Policy NEUTRAL. Result: Re-plan. Scenario: DROP TABLE. Threshold
0, Confidence 100 percent, Policy MANDATORY GATE. Result: Escalate.
Scenario: User said always retry. Threshold MET, Confidence HIGH,
Policy USER WAIVER. Result: Retry.

## Design Principle
The Trigger Engine proposes. Decision Policy disposes. This separation
means policy rules can be added or modified without redesigning health
signals or confidence thresholds.
