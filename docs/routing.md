# Routing

## Nine Outputs, Three Categories
When the Decision Gate fires, execution is routed to one of nine outputs
organized into three functional categories.

## Category 1: Execution Actions (Agent-Decided)
These routes can be taken autonomously without user interaction. Continue:
all health dimensions nominal, no policy flags. Retry: transient failure,
high recovery confidence, within retry budget. Fallback: primary approach
blocked, viable degraded path available. Parallelize: independent
sub-tasks identified, concurrency safe.

## Category 2: Coordination (Human-Agent Collaboration)
These routes require human input or approval. Ask User: multiple viable
paths, user preference matters, or ambiguous tradeoff. Checkpoint: progress
should be saved before a risky or irreversible phase. Escalate: problem
exceeds agent capability, requires human domain judgment.

## Category 3: Termination (Stop Current Track)
These routes end the current execution track. Re-plan: strategy is viable
but needs structural adjustment before continuing. Abort: cost exceeds
value, risk unacceptable, or goal unreachable.

## Why Three Categories?
A flat list of nine outputs suggests they are all equivalent. They are
not. Some the agent can decide. Some require human collaboration. Some
mean stopping. This categorization helps models choose the right route
by first asking: Can I decide this, or do I need human input? Should
execution continue, or should it stop?

## Route Selection Heuristic
Ask three questions in order. Does Policy mandate or override? If yes,
follow Policy. Can the agent decide autonomously? If yes, prefer Execution
Actions. Is human input required? If yes, choose the appropriate
Coordination route. Is continuing impossible or unwise? If yes, choose
the appropriate Termination route.
