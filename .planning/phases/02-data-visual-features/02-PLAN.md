---
phase: "02"
plan: "01"
wave: 1
depends_on: []
files_modified:
  - index.html
requirements:
  - DATA-01
  - DATA-02
  - DATA-03
  - DATA-04
  - DATA-05
  - FEAT-01
  - FEAT-02
autonomous: true
must_haves:
  truths:
    - "GNUS.ai column displays correct fixed values: FP32=200.00, FP16=600.00, FP8=1,400.00, Adaptive=3,500.00, Blended=2,200.00"
    - "GPU columns show values calculated as (Peak TFLOPS × utilization) / hourly price, rounded to 2 decimal places"
    - "GNUS.ai column visually distinct with bg-green-50 background and text-green-700 text on data cells"
    - "Methodology section explains utilization, pricing sources, and precision multipliers"
    - "All 7 GPUs have complete data specs: H100, A100, RTX 4090, RTX 3090, RTX 5090 (est.), Blackwell B200, L40S"
  artifacts:
    - index.html
  key_links:
    - "Format: toLocaleString('en-US', {minimumFractionDigits:2, maximumFractionDigits:2})"
    - "GPU specs from 02-CONTEXT.md decisions"
    - "GNUS fixed values from project-request.md"
---

# Plan 01: Data & Visual Features

Populate the comparison table with computed TFLOPS-per-dollar values, highlight the GNUS.ai column, and write the full methodology section.

## Tasks

### Task 1: Add GPU data and calculation logic

<action>
In the existing `<script>` block in index.html (after the tailwind.config), add:
- A JS object `gnusData` with fixed GNUS values: FP32: 200, FP16: 600, FP8: 1400, Adaptive: 3500, Blended: 2200
- A JS object `gpuData` keyed by GPU name with each containing `price` (hourly $), `utilization` (0-1), and `tflops` array of [FP32, FP16, FP8, Adaptive, Blended]
- GPU values from CONTEXT.md:
  - H100: price=2.00, util=0.60, tflops=[67, 1500, 3200, 800, 950]
  - A100: price=1.20, util=0.60, tflops=[19.5, 312, 1248, 700, 600]
  - RTX 4090: price=0.35, util=0.60, tflops=[82.6, 330, 1320, 900, 800]
  - RTX 3090: price=0.25, util=0.60, tflops=[35.6, 150, 550, 750, 380]
  - "RTX 5090 (est.)": price=0.60, util=0.60, tflops=[100, 400, 1600, 1000, 900]
  - "Blackwell B200": price=3.50, util=0.60, tflops=[90, 2250, 4500, 1200, 1800]
  - L40S: price=0.80, util=0.60, tflops=[91.6, 366, 1466, 850, 750]
- A function `calcEffective(tflops, util, price)` that returns (tflops * util) / price
- A function `formatValue(val)` that returns val.toLocaleString('en-US', {minimumFractionDigits:2, maximumFractionDigits:2})
- A function `renderTable(gpu1Name, gpu2Name)` that:
  - Looks up gpuData[gpu1Name] and gpuData[gpu2Name]
  - For each precision level index 0-4, computes effective TFLOPS for both GPUs
  - Gets GNUS fixed value from gnusData for the same index
  - Updates the 5 table rows' data cells with formatted values (GNUS column + GPU 1 column + GPU 2 column)
- Call renderTable('H100', 'RTX 3090') on page load
</action>

<read_first>
- index.html (current table structure — locate tbody rows and data cell pattern)
- .planning/phases/02-data-visual-features/02-CONTEXT.md (GPU specifications and format decisions)
- .planning/project-request.md (original data values and formula)
</read_first>

<acceptance_criteria>
- `gnusData` object exists with all 5 precision values
- `gpuData` object exists with all 7 GPUs
- Each GPU entry has price, utilization, and 5-element tflops array
- `calcEffective(67, 0.60, 2.00)` returns 20.1 (H100 FP32)
- `calcEffective(35.6, 0.60, 0.25)` returns 85.44 (RTX 3090 FP32)
- `renderTable('H100', 'RTX 3090')` runs without errors on page load
- Table data cells no longer contain `&mdash;` — replaced with computed numbers
</acceptance_criteria>

<verify>
```bash
grep -q 'gnusData' index.html && echo "PASS: gnusData object"
grep -q 'gpuData' index.html && echo "PASS: gpuData object"
grep -q 'renderTable' index.html && echo "PASS: renderTable function"
grep -q "2.00" index.html && echo "PASS: H100 price"
grep -q "0.25" index.html && echo "PASS: RTX 3090 price"
grep -q "Blackwell B200" index.html && echo "PASS: B200 entry"
grep -q "RTX 5090" index.html && echo "PASS: RTX 5090 entry"
grep -q '&mdash;' index.html && echo "FAIL: placeholder still present" || echo "PASS: no placeholders remain"
```
</verify>

### Task 2: Apply GNUS column highlighting

<action>
In `renderTable()`, after setting numeric values, apply to GNUS data cells (second column of each row):
- Add class `bg-green-50` for light green background
- Add class `text-green-700` for green text
- Add class `font-semibold` for visual weight
- Do NOT modify the header th — header stays bg-gray-100
- Do NOT modify any Category or GPU column cells
- Ensure alternating row backgrounds (bg-white/bg-gray-50) on Category column still work correctly alongside the green GNUS cells
</action>

<read_first>
- index.html (current tbody structure, existing row classes)
- .planning/phases/02-data-visual-features/02-CONTEXT.md (highlighting decisions)
</read_first>

<acceptance_criteria>
- GNUS data cells have `bg-green-50` class
- GNUS data cells have `text-green-700` class
- GNUS data cells have `font-semibold` class
- GNUS header cell does NOT have green background (stays bg-gray-100)
- Category column cells retain alternating bg-white/bg-gray-50
- GPU columns have standard text-gray-900 styling
- Opening index.html in browser shows visually distinct GNUS column
</acceptance_criteria>

<verify>
```bash
grep -c 'bg-green-50' index.html | xargs -I{} sh -c '[ {} -ge 5 ] && echo "PASS: green BG on >=5 cells" || echo "FAIL: only {} green BG cells"'
grep -c 'text-green-700' index.html | xargs -I{} sh -c '[ {} -ge 5 ] && echo "PASS: green text on >=5 cells" || echo "FAIL: only {} green text cells"'
grep -c 'font-semibold' index.html | xargs -I{} sh -c '[ {} -ge 5 ] && echo "PASS: semibold on >=5 cells" || echo "FAIL: only {} semibold cells"'
```
</verify>

### Task 3: Write full methodology section

<action>
Replace the placeholder methodology content with structured sections. Replace the italic placeholder paragraph with:

```
<h3 class="text-lg font-semibold mt-4 mb-2">Pricing Sources</h3>
<p>GPU rental prices are based on typical on-demand cloud pricing from major providers as of February 2026. GNUS.ai pricing reflects the effective cost of decentralized inference using idle consumer devices with dynamic token-based pricing.</p>

<h3 class="text-lg font-semibold mt-4 mb-2">GPU Utilization</h3>
<p>All GPU calculations assume 60% sustained utilization under inference workloads. This reflects typical multi-tenant cloud environments where GPUs are shared across workloads. Actual utilization varies by provider and workload type.</p>

<h3 class="text-lg font-semibold mt-4 mb-2">Precision Multipliers</h3>
<p>Effective TFLOPS vary by numerical precision. FP32 represents native single-precision throughput. FP16/mixed-precision typically yields approximately 2x the throughput of FP32. FP8 quantization further improves throughput by approximately 4x over FP32. Adaptive low-bit inference (1.58–4 bit) dynamically adjusts bit-width per layer, achieving significant throughput gains depending on model architecture. Blended inference values represent typical real-world performance for small to mid-size models (7B–70B parameters) using a mix of precisions.</p>

<h3 class="text-lg font-semibold mt-4 mb-2">GNUS.ai Pricing Model</h3>
<p>GNUS.ai uses idle consumer GPU devices (gaming PCs, workstations) for decentralized AI inference. Pricing is dynamic and token-based, meaning users pay per token processed rather than per GPU-hour. The values shown represent effective TFLOPS per $1 per hour based on observed network performance. This model benefits from zero idle hardware cost — consumer devices that would otherwise be inactive contribute compute capacity.</p>

<h3 class="text-lg font-semibold mt-4 mb-2">Data Freshness</h3>
<p>Data as of February 2026. GPU rental prices fluctuate regularly; check provider websites for current rates. Values marked "(est.)" are based on vendor-published specifications and estimated pricing — independent benchmark data may not yet be available.</p>
```

Keep the existing h2 heading and section structure. Remove the italic styling. Keep `border-t border-gray-200` separator.
</action>

<read_first>
- index.html (current methodology section structure at bottom of page)
- .planning/phases/02-data-visual-features/02-CONTEXT.md (methodology content decisions)
- .planning/REQUIREMENTS.md (FEAT-02 — methodology must explain utilization, pricing, precision multipliers)
</read_first>

<acceptance_criteria>
- Methodology section has 5 subheadings: Pricing Sources, GPU Utilization, Precision Multipliers, GNUS.ai Pricing Model, Data Freshness
- Precision Multipliers section explains FP32, FP16, FP8, and adaptive low-bit
- GNUS section mentions idle consumer devices, token-based pricing, effective TFLOPS/$1/hr
- Data Freshness includes "Data as of February 2026" disclaimer
- Section no longer contains italic placeholder text
- All text is professional, factual, neutral — no marketing language
</acceptance_criteria>

<verify>
```bash
grep -q 'Pricing Sources' index.html && echo "PASS: pricing section"
grep -q 'GPU Utilization' index.html && echo "PASS: utilization section"
grep -q 'Precision Multipliers' index.html && echo "PASS: precision section"
grep -q 'GNUS.ai Pricing Model' index.html && echo "PASS: GNUS pricing section"
grep -q 'Data Freshness' index.html && echo "PASS: freshness section"
grep -q 'token-based' index.html && echo "PASS: GNUS pricing explanation"
grep -q '60% sustained utilization' index.html && echo "PASS: utilization rate explained"
grep -q 'idle consumer' index.html && echo "PASS: GNUS device description"
grep -qi 'revolutionary\|unprecedented\|game-changing\|unmatched\|ultimate\|best-in-class' index.html && echo "FAIL: hype word found" || echo "PASS: no hype words"
```
</verify>
