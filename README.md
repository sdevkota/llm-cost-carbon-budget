# LLM Cost Carbon Budget

Budgets for token spend, latency, and estimated energy impact.

> Version: 2.0.0 | Runtime: Python | License: MIT | Status: production-oriented v2 foundation

## Problem

AI systems can silently become expensive and wasteful when every task goes to the largest model with no budget guardrail.

## What this project solves

A budget checker that estimates spend from token counts, tracks latency targets, and records lower-cost routing options.

LLM Cost Carbon Budget is now Python-first. It ships as a dependency-free Python package and CLI that validates a domain-specific JSON packet, emits actionable findings, and gives contributors a practical foundation for adapters, datasets, evals, and workflow integrations.

## Quick start

```bash
python3 -m unittest discover -s tests
python3 -m llm_cost_carbon_budget.cli sample
```

Analyze your own packet:

```bash
python3 -m llm_cost_carbon_budget.cli ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | python3 -m llm_cost_carbon_budget.cli
```

## Example packet

```json
{
  "workload": {
    "name": "support-summaries",
    "monthlyCalls": 200000
  },
  "tokens": {
    "input": 1200,
    "output": 250
  },
  "budget": {
    "maxUsdMonthly": 500,
    "maxLatencyMs": 2000
  }
}
```

## Library usage

```python
from llm_cost_carbon_budget import analyze

report = analyze({
  "workload": {
    "name": "support-summaries",
    "monthlyCalls": 200000
  },
  "tokens": {
    "input": 1200,
    "output": 250
  },
  "budget": {
    "maxUsdMonthly": 500,
    "maxLatencyMs": 2000
  }
})
print(report["summary"])
```

## v2 behavior

- Python-first CLI and importable library.
- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Runs fully offline with no API keys and no network access.

## Contribution map

- Add provider price feeds.
- Add carbon intensity plugins.
- Add routing policies.
- Add FinOps dashboards.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.
