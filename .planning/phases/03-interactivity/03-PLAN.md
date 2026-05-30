---
phase: "03"
plan: "01"
wave: 1
depends_on: []
files_modified:
  - index.html
requirements:
  - CTRL-01
  - CTRL-02
  - CTRL-03
  - TABL-03
autonomous: true
must_haves:
  truths:
    - "Two dropdown selectors labeled 'GPU 1' and 'GPU 2' displayed above the table"
    - "GPU 1 defaults to H100, GPU 2 defaults to RTX 3090"
    - "All 7 GPU options available in both dropdowns"
    - "Changing either dropdown instantly recalculates table values"
  artifacts:
    - index.html
  key_links:
    - "Column headers update to show selected GPU name"
    - "renderTable() reused from Phase 2"
    - "DOMContentLoaded sets defaults and renders initial table"
---

# Plan 01: Interactive GPU Selectors

Replace static GPU labels with interactive dropdown `<select>` elements that trigger instant table recalculation via the existing `renderTable()` function.

## Tasks

### Task 1: Replace static labels with dropdown selectors

<action>
In the GPU selector section (`<section>`), replace the two `<span>` elements with:
- `<label for="gpu1-select" class="text-sm text-gray-500">GPU 1</label>`
- `<select id="gpu1-select" class="border border-gray-300 rounded-lg bg-white px-3 py-2 text-gray-700 font-semibold">` with `<option>` elements for all 7 GPUs
- `<label for="gpu2-select" class="text-sm text-gray-500">GPU 2</label>`  
- `<select id="gpu2-select" class="border border-gray-300 rounded-lg bg-white px-3 py-2 text-gray-700 font-semibold">` with same 7 options
- GPU options: H100, A100, RTX 4090, RTX 3090, RTX 5090 (est.), Blackwell B200, L40S
- Option values should match gpuData keys exactly (e.g., "H100", "Blackwell B200", "RTX 5090 (est.)")
- Layout: labels stacked above selects, both selects side by side in `flex flex-wrap gap-4`
- Keep the outer container border, padding, and bg-gray-50
</action>

<read_first>
- index.html (GPU selector section lines 40-46, gpuData keys for exact option value mapping)
- .planning/phases/03-interactivity/03-CONTEXT.md (dropdown design decisions)
</read_first>

<acceptance_criteria>
- GPU selector section contains two `<select>` elements (not `<span>`)
- Each select has `<label>` with "GPU 1" and "GPU 2"
- Each select contains 7 `<option>` elements
- Option values match gpuData keys (H100, A100, RTX 4090, RTX 3090, "RTX 5090 (est.)", "Blackwell B200", L40S)
- RTX 5090 option text includes "(est.)"
- Labels and selects are inside the bordered container with bg-gray-50
</acceptance_criteria>

<verify>
```bash
grep -c '<select' index.html | xargs -I{} sh -c '[ {} -eq 2 ] && echo "PASS: 2 selects" || echo "FAIL: {} selects"'
grep -c '<option' index.html | xargs -I{} sh -c '[ {} -ge 14 ] && echo "PASS: {} options (>=14)" || echo "FAIL: only {} options"'
grep -q 'gpu1-select' index.html && echo "PASS: gpu1 select"
grep -q 'gpu2-select' index.html && echo "PASS: gpu2 select"
grep -q 'RTX 5090 (est.)' index.html && echo "PASS: RTX 5090 option"
grep -q 'Blackwell B200' index.html && echo "PASS: B200 option"
grep -q '<span.*GPU 1' index.html && echo "FAIL: old span still present" || echo "PASS: no old spans"
```
</verify>

### Task 2: Wire up selection handlers and header updates

<action>
Update the DOMContentLoaded handler to:
1. Add change event listeners on both selects calling `renderTable(gpu1Select.value, gpu2Select.value)`
2. Add `id` attributes to the GPU header `<th>` elements: `id="header-gpu1"` and `id="header-gpu2"`
3. In `renderTable()`, after updating data cells, also update:
   - `document.getElementById('header-gpu1').textContent = gpu1Name;`
   - `document.getElementById('header-gpu2').textContent = gpu2Name;`
4. Set the default select values (H100 and RTX 3090) before the initial renderTable call
5. Update the existing "GPU Selection" label to be visually consistent with the new selects
</action>

<read_first>
- index.html (current DOMContentLoaded handler, renderTable function, thead th elements)
- .planning/phases/03-interactivity/03-CONTEXT.md (selection behavior decisions)
</read_first>

<acceptance_criteria>
- Changing GPU 1 dropdown triggers table recalculation
- Changing GPU 2 dropdown triggers table recalculation
- Column header th text updates to show selected GPU name
- Default selections (H100, RTX 3090) render correct values on page load
- No page reload required — instant update on selection change
</acceptance_criteria>

<verify>
```bash
grep -q 'addEventListener.*change' index.html && echo "PASS: change event listeners"
grep -q 'header-gpu1' index.html && echo "PASS: header-gpu1 id"
grep -q 'header-gpu2' index.html && echo "PASS: header-gpu2 id"
grep -q 'header-gpu1.*textContent' index.html && echo "PASS: header update logic"
grep -q 'gpu1Select.value' index.html && echo "PASS: gpu1 value reference"
grep -q 'gpu2Select.value' index.html && echo "PASS: gpu2 value reference"
```
</verify>
