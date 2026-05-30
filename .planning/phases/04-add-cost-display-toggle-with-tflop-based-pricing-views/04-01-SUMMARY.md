# Plan 01: Summary — Cost Display Toggle

**Phase:** 04 — Cost Display Toggle
**Plan:** 01
**Completed:** 2026-05-29
**Status:** Complete

## What Was Built

Added a "Display Mode" dropdown in the GPU selector section with two modes:
- **TFLOPS per $1/hr** (existing behavior) — shows effective TFLOPS per dollar
- **Cost per 1K TFLOP/hr** (new default) — shows dollar cost per 1,000 TFLOPs

The display mode dropdown sits alongside the GPU selects with matching styling. Changing the mode instantly recalculates all table values. Cost mode uses the formula `(price / (peak_tflops * utilization)) * 1000`. GNUS column retains green highlighting in both modes.

## Files Changed

| File | Action |
|------|--------|
| `index.html` | Modified (mode dropdown, calcCost, renderTable mode param) |
