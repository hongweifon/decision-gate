# Philosophy

## The Problem: Blind Execution

AI agents are trained to act. Given a task, they execute step after step,
tool call after tool call, until something stops them. Usually that
something is context exhaustion, a hard error, or an impatient user.

This is blind execution: the agent evaluates each step in isolation
(did this API call succeed? can I proceed to the next item?) but never
evaluates the trajectory as a whole.

## The Costs of Blind Execution

- Token waste: Every retry, every unnecessary page, every circular debug
  session burns tokens. Tokens cost money.
- Context decay: Long sessions degrade reasoning quality. Early decisions
  were made with full context; late decisions are made in a fog.
- Opportunity cost: While the agent is grinding through a diminishing-returns
  task, it could be doing something more valuable.
- Trust erosion: When an agent clearly should have stopped but did not,
  users lose confidence in autonomy.

## The Core Insight

An agent that can only *do* but never *decide* is not autonomous. It is
just expensive automation that leaks.

Decision Gate is the *decide* layer. It is what sits between each execution
phase and asks the question that blind execution never asks:

> Given what we know now, is continuing still the best path?

## Why Not Just "Ask Before Continuing"?

Prompts that say "ask before doing anything big" create a different problem:
they ask too often, or never at the right time. They lack:

- Quantitative thresholds: what counts as "big"?
- Confidence assessment: is this a real problem or noise?
- Policy awareness: did the user already pre-authorize this?
- Routing intelligence: stop is not the only option

Decision Gate provides all four.

## The Framework Thesis

Decision Gate is not a Codex-specific prompt. It is a runtime decision
framework spec that can be implemented for any agent architecture:

- Claude: As a system prompt overlay
- Gemini: As a safety-filter extension
- LangGraph: As a conditional edge function
- AutoGen: As a group chat moderator agent
- MCP Agent: As a pre-call interceptor
- Codex: As a Skill (reference implementation)

The design separates mechanism from implementation. The mechanism is
universal: evaluate health, check policy, route appropriately.
