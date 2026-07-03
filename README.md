# Engineering Re-planning

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Codex Skill](https://img.shields.io/badge/Codex-Skill-6e57e0)](https://github.com/openai/codex)

A **meta-cognitive Codex Skill** that teaches AI agents when to **stop, assess, and re-plan** instead of blindly continuing execution that is no longer optimal.

> "Don't continue just because you can. Evaluate whether you still should."

---

## Table of Contents

- [Why This Exists](#why-this-exists)
- [Design Philosophy](#design-philosophy)
- [When It Triggers](#when-it-triggers)
- [When It Stays Silent](#when-it-stays-silent)
- [Quick Example](#quick-example)
- [Installation](#installation)
- [Usage](#usage)
- [FAQ](#faq)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## Why This Exists

AI agents have a well-known failure mode: **runaway execution**.

They will:
- **Retry indefinitely** — hitting the same API error 50 times
- **Browse endlessly** — crawling page after page of a 10,000-item list
- **Edit recursively** — fixing one bug creates two more, which creates four more
- **Debug in circles** — applying patches that don't work, then applying more patches
- **Burn the context window** — continuing until the conversation is truncated and all progress is lost

These aren't bugs in the agent. They're a missing capability: **the ability to recognize when continued execution has become counterproductive, and to ask for re-direction before the damage compounds.**

This skill teaches that capability as a reusable, tool-agnostic module.

### The Cost of Runaway Execution

| Failure Mode | Typical Outcome |
|---|---|
| Infinite retry loops | Token waste, no progress, eventual context exhaustion |
| Unbounded web scraping | Hours of crawling, most data irrelevant |
| Cascading code fixes | More bugs than when you started |
| Scope creep in automation | Original goal forgotten, side quests dominate |
| Debugging without strategy | Same error, different patches, no diagnosis |

**This skill adds a circuit breaker at every checkpoint.**

---

## Design Philosophy

### 1. Thresholds, Not Heuristics

Every trigger has a **quantitative threshold**. Single failures don't fire.
Consecutive failures, escalating costs, and diminishing returns do.

This prevents the most common failure mode of guard skills: **false positives**
that interrupt normal execution every five minutes.

### 2. Options, Not Commands

The skill never says "stop and give up." It says:

> Here's what's been done. Here's what's changed. Here are 2–4 concrete paths
> forward with costs, completeness, and risks. Which one?

### 3. Tool-Agnostic

This skill has zero dependencies. It works with web scraping, file processing,
debugging, CI/CD pipelines, data pipelines — anything that involves repeated
tool calls over time.

### 4. Engineering Judgment as a Skill

Most Codex skills teach *what to do*. This one teaches *when to stop doing it*.
It's a meta-skill — it operates on the agent's own execution loop.

---

## When It Triggers

The skill monitors **7 trigger signals**, each with defined thresholds:

| # | Signal | Threshold |
|---|--------|-----------|
| 1 | **Effort Escalation** | Actual effort > 3× original estimate, or unknown work exceeds known work |
| 2 | **Success Rate Decline** | ≥ 3 consecutive failures, or > 50% failure rate on last 10 ops |
| 3 | **Scope Creep** | ≥ 2 new task categories added, or side quests > 40% of total time |
| 4 | **Diminishing Returns** | Per-item time > 3× initial speed, or < 5% new data per 10 min |
| 5 | **Unresolvable Ambiguity** | ≥ 3 judgment calls made without user input |
| 6 | **Path Dependency Risk** | Irreversible operations attempted without sign-off |
| 7 | **Multiple Viable Paths** | ≥ 2 approaches with different cost/quality tradeoffs, each > 10 min |

See [SKILL.md](SKILL.md) for the full decision tree with Mermaid flowchart.

---

## When It Stays Silent

The skill deliberately **does not trigger** on:

- Single timeouts, 404s, or transient errors
- One bad data item in a large batch
- The first retry of a failed operation
- Tasks marked "complete everything, don't ask"
- Expected repetitive work
- Normal data cleaning

The design goal: **false positives should be rarer than missed signals.**
An overeager guard that interrupts every 3 minutes is worse than no guard at all.

---

## Quick Example

**Task**: Scrape contact info from 50 university websites.

After 12 smooth sites, the remaining 38 use custom React SPAs.
Each now takes 5× longer.

**Without this skill**: The agent spends hours writing per-site Playwright
scripts, burning tokens and time until context exhaustion or user intervention.

**With this skill**:

```
Completed 12/50 universities (~2 min each).
Remaining 38 use diverse frontend stacks — estimated 10–15 min each.
Total projected: 6–10 hours from this point.

Options:
  A. Continue all 50 — 6–10h, 100% coverage
  B. Prioritize top 20 by ranking — ~2h, 80% of target audience
  C. Deliver the 12 completed now, expand on request — 0h, 24% coverage
```

The user can now make an informed decision instead of discovering the problem
hours later.

---

## Installation

### Via Codex Marketplace (Recommended)

```bash
codex skills install engineering-replanning
```

### Manual Installation

```bash
git clone https://github.com/YOUR_USERNAME/engineering-replanning.git
cp -r engineering-replanning ~/.codex/skills/engineering-replanning
```

### Verify Installation

```bash
codex skills list | grep engineering-replanning
```

---

## Usage

This skill activates automatically during long-running tasks. No explicit
invocation needed.

To increase or decrease sensitivity, edit the threshold values in
[SKILL.md](SKILL.md). Lower thresholds = more frequent checkpoints.
Higher thresholds = only the most extreme deviations trigger.

### Recommended Configurations

| Profile | Threshold Multiplier | Use Case |
|---|---|---|
| **Conservative** | 0.5× | Interactive sessions, user available to answer |
| **Default** | 1.0× | General purpose |
| **Aggressive** | 2.0× | Overnight batch jobs, user expecting completion |

---

## FAQ

### Will this interrupt me every 5 minutes?

No. The thresholds are designed so that transient failures do not trigger
re-planning. You need 3+ consecutive failures, 3× effort escalation, or
similar sustained deviation before the skill intervenes.

### Can I tell the agent to never stop?

Yes. If you say "complete everything, don't ask," the skill records the
waiver and continues. But it will still fire if an **irreversible or
destructive** action is about to happen without confirmation.

### Does this work with any Codex-compatible agent?

Yes. The skill is a markdown instruction set with zero dependencies.
Any agent that reads SKILL.md and follows its instructions will benefit.

### What's the difference between this and just writing "ask before continuing" in the prompt?

Prompts don't have thresholds. They either ask every time (annoying) or
never ask (dangerous). This skill provides calibrated intervention —
only when the math says the situation has materially changed.

### Is this a "stop" skill or a "re-plan" skill?

Both. It stops execution, assesses the situation, and then presents
re-planned options. The user always decides the next step.

---

## Roadmap

- **v1.1**: Configurable threshold profiles (conservative/default/aggressive)
- **v1.2**: Token budget awareness — trigger when approaching context limits
- **v1.3**: Historical learning — track which trigger types are most useful
- **v2.0**: Multi-agent coordination — detect when sub-agents are stuck
- **v2.1**: Cost estimation integration — use token pricing for dollar cost projections

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Key areas for contribution:

- **New trigger signals**: Propose additional failure patterns with evidence
- **Threshold tuning**: Share real-world data on false positive / false negative rates
- **Edge cases**: Report scenarios where the skill behaved incorrectly
- **Multi-language translations**: The skill is currently English-only

### Before submitting a PR:

1. Read the [design philosophy](#design-philosophy) — thresholds are non-negotiable
2. Include concrete examples of the problem your change solves
3. Do not add tool-specific dependencies

---

## License

MIT © 2026

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=YOUR_USERNAME/engineering-replanning&type=Date)](https://star-history.com/#YOUR_USERNAME/engineering-replanning&Date)

---

## Acknowledgments

Inspired by real-world observations of AI agent failure modes in production
Codex sessions. The seven trigger signals are derived from patterns that
repeatedly caused wasted computation across hundreds of long-running tasks.
