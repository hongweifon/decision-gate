# Decision Gate

A Runtime Decision Framework for AI Agents.

## Why
AI agents have one universal failure mode: they do not know when to stop.
Decision Gate answers the question at every checkpoint: should I keep going?

## Architecture
Three layers: Decision Policy (governance), Health Assessment (execution,
requirement, decision health), Trigger Engine (f of Threshold, Confidence,
Policy). Nine outputs in three categories: Execution Actions, Coordination,
Termination. The Engine proposes; Policy disposes.

Full documentation: [English](../)
