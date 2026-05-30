# GNUS AI Pricing Comparison

## What This Is

A self-contained single HTML page that provides an interactive, factual comparison of AI inference compute cost-performance. It compares GNUS.ai decentralized inference (which uses idle consumer devices with dynamic token-based pricing) against traditional GPU rental options, using effective TFLOPS per $1 per hour as the comparison metric.

## Core Value

Users can interactively compare the cost-performance of GNUS.ai decentralized inference against any two GPUs of their choice, with live-updating data across multiple precision levels.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Interactive comparison table with GNUS.ai and two selectable GPUs
- [ ] Live table updates when GPU dropdown selections change
- [ ] Accurate TFLOPS-per-dollar calculations across five precision levels
- [ ] Assumptions & Methodology section explaining calculation logic
- [ ] Clean, professional, responsive design with Tailwind CSS
- [ ] GNUS.ai column visually highlighted

### Out of Scope

- Backend/server-side data processing — single-file static HTML only
- Real-time pricing data — hardcoded reference values
- Additional benchmark categories beyond the five specified precision levels
- User-submitted data or crowdsourced GPU benchmarks

## Context

- **Current state:** A `.planning/project-request.md` document specifies the exact design, data, and calculation logic.
- **Target deliverable:** A single `index.html` file with embedded Tailwind CSS (via CDN) and vanilla JavaScript.
- **Audience:** Technical users comparing AI inference compute options.
- **Tone:** Professional, factual, neutral — no marketing hype.

## Constraints

- **Tech stack:** Single HTML file, Tailwind CSS (CDN), vanilla JavaScript — no build tools, no frameworks
- **Deployment:** Static file, no server required
- **Data:** Hardcoded GPU specs and pricing values as specified in project-request.md
- **Design:** Clean and readable, responsive, with GNUS.ai column highlighted

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Single-file HTML | Simplest deployment, no build step needed | — Pending |
| Tailwind via CDN | No npm/build tooling required for a single page | — Pending |
| Vanilla JS (no framework) | Overhead of React/Vue unjustified for one interactive table | — Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `/gsd-transition`):
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active
4. Decisions to log? → Add to Key Decisions
5. "What This Is" still accurate? → Update if drifted

**After each milestone** (via `/gsd-complete-milestone`):
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-05-29 after initialization*
