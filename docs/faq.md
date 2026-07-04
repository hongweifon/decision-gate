# FAQ

## Will this interrupt me every 5 minutes?
No. Threshold plus Confidence dual-gating suppresses transient noise.
You need sustained deviation before the gate fires. Policy can further
suppress interrupts when you say do everything, do not ask.

## Can I tell the agent to never stop?
Yes. Decision Policy honors user waivers. But Policy still gates on
destructive or irreversible operations. Safety overrides convenience.

## Does this work with any agent architecture?
Yes. Decision Gate is a framework, not a Codex-specific prompt. The
SKILL.md is a reference implementation. Adapt the design for Claude,
Gemini, LangGraph, AutoGen, or any runtime.

## What changed from the original engineering-replanning skill?
Version 1 had one output: Re-plan. Version 2 is a runtime decision
routing system with nine outputs in three categories, a three-layer
model, a Threshold times Confidence scoring system, and a governing
Decision Policy layer.

## Is this a stop system or a routing system?
A routing system. Stop (Abort) is one of nine possible routes.
The gate routes to the best action, not always stop, not always
continue, and not always ask the user.

## How do I tune the sensitivity?
Adjust threshold values in the Health Model. Lower equals more
frequent gating. Higher equals only extreme deviations trigger.
Confidence thresholds can also be tuned. All three layers are
configurable independently.
