# LLM Cost Carbon Budget

Budgets for token spend, latency, and estimated energy impact.

> Version: 1.0.0 | License: MIT | Status: production-oriented v1 foundation

## Problem

AI systems can silently become expensive and wasteful when every task goes to the largest model with no budget guardrail.

## What this project solves

A budget checker that estimates spend from token counts, tracks latency targets, and records lower-cost routing options.

LLM Cost Carbon Budget ships as a small, dependency-free CLI and library. It validates a domain-specific JSON packet, emits actionable findings, and gives contributors a concrete surface for adding adapters, richer checks, schemas, and integrations.

## Who it is for

Platform engineers, sustainability teams, AI product owners.

## Quick start

```bash
npm test
npm start -- sample
```

Analyze your own packet:

```bash
llm-cost-carbon-budget ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | node src/cli.js
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

```js
const { analyze } = require("./src/index.js");

const report = analyze({
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
});
console.log(report.summary);
```

## v1 behavior

- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Suggests next actions and contributor extension points.
- Runs fully offline with no API keys and no network access.

## Contribution map

Good first contributions:

- Add provider price feeds.
- Add carbon intensity plugins.
- Add routing policies.
- Add FinOps dashboards.

Larger contributions:

- Add a JSON Schema and compatibility tests.
- Build import/export adapters for popular AI frameworks.
- Add real-world fixtures from public, non-sensitive examples.
- Improve scoring with transparent, documented heuristics.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.

## GitHub Pages

The marketing site lives in `site/index.html`. Enable GitHub Pages from the `site` folder or use the included Pages workflow after publishing.

## Security

This project does not process secrets by default. If you build adapters that touch production systems, keep least privilege, explicit consent, and auditable logs in the design.
