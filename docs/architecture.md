# Architecture

## Three-Layer Model
Decision Gate is built on three layers that separate governance from
diagnosis from proposal. Each layer can be tuned independently.

## Layer 1: Decision Policy (Governance)
The governing layer wraps around the entire system. It overrides, mandates,
or redirects routing regardless of health signals. Two rule categories:
Mandatory Rules (always enforced: destructive ops, irreversible actions,
safety constraints) and Runtime Assessment (context-dependent: user
preferences, deadlines, async/sync mode).

## Layer 2: Health Assessment (Diagnosis)
Three health dimensions organized by concern: Execution Health (is the agent
operating efficiently? Failure rate, time per unit, cost vs estimate, speed),
Requirement Health (is the goal stable? Scope creep, unknown unknowns, manual
judgment creep), Decision Health (are next-step options sound? Multiple paths,
irreversibility, preference ambiguity).

## Layer 3: Trigger Engine (Proposal)
TRIGGER_DECISION = f(Threshold, Confidence, Policy). A health signal
contributes to routing only when threshold is reached AND confidence
is at least MEDIUM. But Policy can override at any point. The Engine
proposes; Policy disposes.

## Why Three Layers?
Flat trigger lists mix concerns, lack overrides, and produce false
positives. Three layers separate governance from diagnosis from proposal.
You can change thresholds without touching policy, or add policy rules
without redesigning health signals.
