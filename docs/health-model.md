# Health Model

## Three Health Dimensions
Health signals are organized into three functional dimensions. Each
dimension maps to a different question about execution.

## Execution Health: Is the agent operating efficiently?
Failure rate rising: more than 50 percent failure over last 10 ops,
HIGH confidence if same error type, LOW if varied. Time per unit
increasing: more than 3x initial speed, HIGH if structural change,
LOW if one slow outlier. Cost exceeding estimate: more than 3x
original, HIGH if data-driven estimate, LOW if guesswork. Speed
degrading: more than 2x slowdown sustained, HIGH if monotonic,
LOW if spike.

## Requirement Health: Is the goal stable?
Scope expanding: 2 or more new task categories, HIGH confidence if
user-initiated, MED if agent-discovered. Unknown unknowns growing:
unknown steps exceed known steps, HIGH if new domain, MED if same
domain deeper. Manual judgment creep: 3 or more judgment calls
without user input, HIGH if domain gap, MED if formatting choice.

## Decision Health: Are the next-step options sound?
Multiple viable paths: 2 or more approaches each exceeding 10 min,
HIGH if tradeoffs clear, MED if one path dominates. Path is
irreversible: destructive or schema-changing operation, HIGH always.
User preference required: time vs quality vs completeness tradeoff,
HIGH if preferences unknown, LOW if implied by task.

## Confidence Assessment
HIGH: pattern is systematic, root cause identifiable, trend monotonic.
MEDIUM: pattern emerging but noisy, root cause plausible but
unconfirmed. LOW: pattern could be noise, root cause speculative,
alternatives exist. All signals require both threshold AND confidence
at MEDIUM or above before contributing to routing.
