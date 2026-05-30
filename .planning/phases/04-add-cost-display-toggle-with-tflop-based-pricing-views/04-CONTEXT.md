# Phase 4: Cost Display Toggle - Context

**Gathered:** 2026-05-29
**Status:** Ready for planning

## Phase Boundary

Add a display mode dropdown that lets users switch between "TFLOPS per $1/hr" (current behavior) and "Cost per 1K TFLOP/hr" (dollar cost view). All table columns recalculate and update instantly when the mode changes.

**In scope:** Display mode dropdown, cost calculation logic, column value formatting for cost mode, unit label updates

**Out of scope (deferred):** Custom TFLOP count input, localStorage persistence, additional display modes beyond the two specified

## Implementation Decisions

### Display Mode Selector
- Placed next to GPU selects in the same bordered container
- Labeled "Display Mode" with label above the select
- Two options: "TFLOPS per $1/hr" (value: "tflops") and "Cost per 1K TFLOP/hr" (value: "cost")
- Same Tailwind styling as existing GPU selects (`border border-gray-300 rounded-lg bg-white px-3 py-2`)
- Default mode: "Cost per 1K TFLOP/hr" (as specified)
- Change event triggers full table recalculation

### Cost Calculation
- Cost per 1K TFLOPs: `(price / (peak_tflops * utilization)) * 1000`
- Equivalent to: `1000 / effective_tflops_per_dollar`
- Unit label: "$/1K TFLOP/hr"
- Lower cost = better value — GNUS column keeps green highlighting (already signals advantage)

### Number Formatting
- Cost mode: 2 decimal places, US locale (same format function as TFLOPS mode)
- GNUS column: same bg-green-50 + text-green-700 + font-semibold in both modes
- Column headers do NOT change between modes (GPU names stay the same)
- No "(lower is better)" indicator — values speak for themselves

### JS Implementation
- Add `displayMode` variable (default: "cost")
- Modify `renderTable()` to accept or read current display mode
- In cost mode: compute `(price / (tflops * util)) * 1000` for GPU columns, `1000 / gnusValue` for GNUS column
- In tflops mode: existing behavior unchanged
- New `renderAll()` function that calls `renderTable()` with current GPU + mode selections
- Wire display mode change event to `renderAll()`

### Claude's Discretion
- Exact variable naming for display mode state
- Whether to add a unit indicator in table header or near the mode selector
- Edge case handling for zero/near-zero values

## Canonical References

### Design
- `.planning/phases/03-interactivity/03-CONTEXT.md` — Dropdown design patterns established in Phase 3
- `index.html` — Current GPU selects and renderTable implementation

## Existing Code Insights

### Reusable Assets
- `renderTable(gpu1Name, gpu2Name)` — extend to accept or read display mode
- GPU select markup pattern — copy for display mode dropdown
- `formatValue()` function — reuse for both modes
- `calcEffective()` function — add inverse calculation for cost mode

### Integration Points
- GPU selector section (lines 127-147) — add third dropdown here
- `DOMContentLoaded` handler — set display mode default + wire change event
- `renderTable()` — branch on display mode for value computation

## Specific Ideas

- Cost mode converts GNUS values too: 1000 / gnusValue (e.g., 1000/200 = $5.00/1K TFLOP/hr)
- GPU cost: (price / (tflops * util)) * 1000 (e.g., H100 FP16: ($2.00 / (1500*0.60)) * 1000 = $2.22/1K TFLOP/hr)

## Deferred Ideas

None — discussion stayed within phase scope.

---

*Phase: 4-Cost Display Toggle*
*Context gathered: 2026-05-29 via smart discuss*
