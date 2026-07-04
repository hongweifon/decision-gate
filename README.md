> 🇺🇸 English · 🇨🇳 [简体中文](docs/zh/README.md)

# Decision Gate
A Runtime Decision Framework for AI Agents.
Teach agents not only how to execute — but when to pause, reroute, and ask.
---
Who Should Use This
Long-running coding tasks, research agents, batch data processing, web
scraping at scale, CI/CD debugging workflows, data pipelines, automation.
Not for one-shot tasks or simple Q&A.
---
The Architecture
User Policy -> Decision Policy Layer -> Mandatory Rules / Runtime
Assessment -> Health Assessment (3 dimensions) -> Trigger Engine
f(Threshold, Confidence, Policy) -> Route Decision (9 outputs, 3 categories).
See docs/architecture.md for the full diagram.
---
Quick Example
Task: Scrape 50 university websites. 12 done smooth, 38 use custom SPAs
each 5x slower. Without: agent scrapes 6+ hours until context exhaustion.
With: agent stops at checkpoint. Route: Ask User. Options: Continue all
50 (6-10h), Prioritize top 20 (2h, 80%), Deliver 12 now (0h, 24%).
---
Installation
Codex Reference Implementation: codex skills install decision-gate
As a Framework: Read docs/. Adapt for Claude, Gemini, LangGraph,
AutoGen, or any agent runtime.
---
Benchmarks
Real-world comparisons planned for v0.2. Current examples are
qualitative only. See benchmarks/.
---
Why It Works
Policy overrides everything. Three health dimensions cover Execution,
Requirement, Decision. Threshold x Confidence suppresses false positives.
Three output categories let the agent or human decide. Framework adapts
to any architecture, not just one prompt.
---
Docs
philosophy.md: Why. architecture.md: How. health-model.md: Health
dimensions. decision-policy.md: Policy system. routing.md: Outputs.
examples.md: Scenarios. faq.md: Common questions.
---
Links
SKILL.md: Reference implementation. CHANGELOG.md. CONTRIBUTING.md.
---
MIT License
