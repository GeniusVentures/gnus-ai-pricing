# Phase 2: Data & Visual Features - Context

**Gathered:** 2026-05-29
**Status:** Ready for planning

## Phase Boundary

Populate the comparison table with real TFLOPS-per-dollar computed values for GNUS.ai (fixed) and all GPUs (calculated), highlight the GNUS.ai column visually, and fill in the full Assumptions & Methodology section with structured content.

**In scope:** DATA-01–05 (GNUS values, GPU calculations, all GPU specs), FEAT-01 (GNUS column highlighting), FEAT-02 (full methodology content)

**Out of scope (deferred):** Dropdown interactivity (Phase 3), live table updates (Phase 3)

## Implementation Decisions

### GNUS Column Highlighting
- Light green background (`bg-green-50`) on GNUS data cells only (not header)
- GNUS values use green text (`text-green-700`) to reinforce the comparison advantage
- Header row keeps standard `bg-gray-100` — no green on header

### Data Display Format
- Two decimal places for all values, formatted via `toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})`
- US locale with comma thousands separators and decimal point
- Future: locale detection via JavaScript (navigator.language / Intl)
- GPU computed values rounded to 2 decimal places before display
- No "higher is better" indicator — values speak for themselves

### Data Storage
- Inline JavaScript object (`gpuData`) containing per-GPU specs: hourlyPrice, utilization, precision TFLOPS arrays
- GNUS values stored as a separate fixed array
- All 7 GPUs defined: H100, A100, RTX 4090, RTX 3090, RTX 5090 (est.), Blackwell B200, L40S
- Default display GPUs: H100 (GPU 1) and RTX 3090 (GPU 2)

### GPU Specifications
- H100: $2.00/hr, 60% util — FP32:67, FP16:1500, FP8:3200, Adaptive:800, Blended:950
- RTX 3090: $0.25/hr, 60% util — FP32:35.6, FP16:150, FP8:550, Adaptive:750, Blended:380
- RTX 4090: $0.35/hr, 60% util — FP32:82.6, FP16:330, FP8:1320, Adaptive:900, Blended:800
- A100: $1.20/hr, 60% util — FP32:19.5 (TF32), FP16:312, FP8:1248, Adaptive:700, Blended:600
- L40S: $0.80/hr, 60% util — FP32:91.6, FP16:366, FP8:1466, Adaptive:850, Blended:750
- RTX 5090 (est.): $0.60/hr, 60% util — FP32:100, FP16:400, FP8:1600, Adaptive:1000, Blended:900
- Blackwell B200: $3.50/hr, 60% util — FP32:90, FP16:2250, FP8:4500, Adaptive:1200, Blended:1800
- Per-GPU utilization rates: 60% default for H100/RTX 4090/A100/B200/L40S. RTX 3090 uses 60%
- RTX 5090 row label includes "(est.)" suffix; methodology notes B200/L40S based on vendor specs

### Methodology Content
- Structured with subheadings: "Pricing Sources", "GPU Utilization", "Precision Multipliers", "GNUS.ai Pricing Model", "Data Freshness"
- Precision multipliers explained: FP32=native, FP16≈2x, FP8≈4x, adaptive=dynamic bit-width (1.58-4 bit)
- GNUS section: idle consumer devices, token-based dynamic pricing, effective TFLOPS/$1/hr from observed network performance
- Data freshness disclaimer: "Data as of February 2026. GPU rental prices fluctuate; check provider websites for current rates."

### Claude's Discretion
- Exact wording of methodology text (factual, neutral per PAGE-04)
- Code structure for JS data object and rendering function
- Pre-computed or runtime-computed GPU effective TFLOPS values
- Left/center alignment of numeric values in table

## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Requirements
- `.planning/project-request.md` — Original GPU data values and calculation formula
- `.planning/REQUIREMENTS.md` — Formal requirements DATA-01–05, FEAT-01–02

### Design
- `.planning/phases/01-static-page-foundation/01-CONTEXT.md` — Phase 1 decisions (table structure, column order, layout)
- `index.html` — Current HTML with placeholder table to be populated

## Existing Code Insights

### Reusable Assets
- `index.html` — Existing table structure with `&mdash;` placeholders. Replace with computed values.
- Tailwind classes from Phase 1: `table-auto`, `border-collapse`, alternating `bg-gray-50`

### Established Patterns
- Single-file HTML: inline JS objects for data, no external dependencies
- Tailwind CDN for all styling — no custom CSS file

### Integration Points
- Table `<tbody>` rows are the insertion point for computed values
- Methodology `<section>` at page bottom needs content replacement
- GPU selector section (static labels) preserved for Phase 3 replacement

## Specific Ideas

- Values formatted as "1,234.56" style (US locale with comma separators)
- GNUS column values in green (`text-green-700`) on green background (`bg-green-50`)
- Methodology includes calculation formula prominently

## Deferred Ideas

None — discussion stayed within phase scope.

---

*Phase: 2-Data & Visual Features*
*Context gathered: 2026-05-29 via smart discuss*
