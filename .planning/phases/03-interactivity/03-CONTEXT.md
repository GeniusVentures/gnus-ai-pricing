# Phase 3: Interactivity - Context

**Gathered:** 2026-05-29
**Status:** Ready for planning

## Phase Boundary

Replace the static GPU selector labels with interactive dropdown selectors. When the user changes either dropdown, the comparison table recalculates and updates instantly with the selected GPUs' effective TFLOPS values. Column headers update to match the selected GPU names.

**In scope:** CTRL-01–03 (dropdown selectors with defaults and all GPU options), TABL-03 (live table updates on selection change)

**Out of scope (deferred):** URL-based sharing, localStorage persistence of selections, additional GPUs beyond the 7 specified

## Implementation Decisions

### Dropdown Design
- Tailwind-styled `<select>` elements with `border border-gray-300 rounded-lg bg-white px-3 py-2`
- `<label>` above each select for accessibility — "GPU 1" and "GPU 2"
- Side-by-side layout (`flex flex-wrap gap-4`) — stacks on mobile via flex-wrap
- Keep existing bordered container (`border border-gray-200 rounded-lg p-4 bg-gray-50`) from Phase 1
- Replace the static `<span>` elements with `<select>` elements

### Selection Behavior
- Allow duplicate GPU selections (no restriction) — simple, user can compare same GPU
- Default: GPU 1 = H100, GPU 2 = RTX 3090 (CTRL-02)
- Table column headers (`<th>`) update to show the selected GPU name
- No animation/transition on value change — instant recalculation
- All 7 GPU options available: H100, A100, RTX 4090, RTX 3090, RTX 5090 (est.), Blackwell B200, L40S
- RTX 5090 entry shows "(est.)" suffix in the dropdown option text

### JS Implementation
- Reuse existing `renderTable(gpu1Name, gpu2Name)` from Phase 2
- Add `change` event listeners on both `<select>` elements calling `renderTable()`
- On DOMContentLoaded: populate dropdowns, set defaults, render initial table
- Header update: set `textContent` of the GPU column `<th>` elements to the selected name

### Claude's Discretion
- Exact padding/spacing of dropdown elements within the container
- Event handler wiring (inline onchange vs addEventListener)
- How GPU names map between select values and gpuData keys

## Canonical References

### Requirements
- `.planning/REQUIREMENTS.md` — CTRL-01, CTRL-02, CTRL-03, TABL-03

### Design
- `.planning/phases/01-static-page-foundation/01-CONTEXT.md` — Layout decisions (D-08, D-09)
- `.planning/phases/02-data-visual-features/02-CONTEXT.md` — GPU data structure and renderTable API
- `index.html` — Existing GPU selector section and table structure

## Existing Code Insights

### Reusable Assets
- `index.html` — GPU selector section (lines 40-46) with static labels to be replaced
- `renderTable(gpu1Name, gpu2Name)` function — already accepts GPU names, ready for dropdown integration
- `gpuData` object — all 7 GPUs already defined
- `DOMContentLoaded` event listener — already calls renderTable, extend for dropdown setup

### Integration Points
- GPU selector `<section>` is the replacement target — static `<span>` elements become `<select>` elements
- Table `<thead>` th elements need id attributes for header update
- Onchange handlers wire into existing `renderTable()`

## Specific Ideas

- Dropdowns mirror the 7 GPU keys from `gpuData` — exact name matching
- RTX 5090 option text includes "(est.)" as in the data key
- Headers update to show full GPU name including "(est.)" suffix

## Deferred Ideas

None — discussion stayed within phase scope.

---

*Phase: 3-Interactivity*
*Context gathered: 2026-05-29 via smart discuss*
