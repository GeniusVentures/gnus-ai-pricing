---
phase: "01"
plan: "01"
wave: 1
depends_on: []
files_modified:
  - index.html
requirements:
  - PAGE-01
  - PAGE-02
  - PAGE-03
  - PAGE-04
  - TABL-01
  - TABL-02
  - FEAT-03
  - FEAT-04
autonomous: true
must_haves:
  truths:
    - "Page title displays 'AI Inference Compute Cost-Performance Comparison (Feb 2026)'"
    - "Description explains TFLOPS-per-dollar comparison and mentions GNUS.ai idle consumer devices"
    - "All text maintains professional, factual, neutral tone"
    - "Page adapts to desktop, tablet, and mobile viewports"
  artifacts:
    - index.html
  key_links:
    - "Comparison table with 4 columns and 5 precision rows visible"
    - "GNUS.ai column between Category and GPU columns"
    - "GPU selector area shows 'GPU 1: H100' and 'GPU 2: RTX 3090'"
    - "Methodology placeholder section at page bottom"
    - "Tailwind CSS CDN loaded and functional"
---

# Plan 01: Static Page Foundation

Create `index.html` — the complete self-contained HTML file with Tailwind CSS, page structure, comparison table, and responsive design.

## Tasks

### Task 1: Scaffold HTML document with Tailwind CSS CDN

<action>
Create `index.html` in the project root with:
- DOCTYPE html
- lang="en" on html element
- UTF-8 charset meta tag
- viewport meta tag for responsive: width=device-width, initial-scale=1.0
- Title tag: "AI Inference Compute Cost-Performance Comparison (Feb 2026)"
- Tailwind CSS CDN: script src="https://cdn.tailwindcss.com"
- Custom Tailwind config for max-w-5xl container
- Empty body with class="bg-white text-gray-900 min-h-screen"
- Applied professional, factual, neutral tone throughout
</action>

<read_first>
- .planning/phases/01-static-page-foundation/01-CONTEXT.md
</read_first>

<acceptance_criteria>
- `index.html` exists in project root
- File contains valid HTML5 doctype
- File contains `<title>AI Inference Compute Cost-Performance Comparison (Feb 2026)</title>`
- File contains `<script src="https://cdn.tailwindcss.com"></script>`
- File contains viewport meta tag with `width=device-width, initial-scale=1.0`
- Page opens in browser without console errors
</acceptance_criteria>

<verify>
```bash
test -f index.html && echo "PASS: index.html exists"
grep -q '<title>AI Inference Compute Cost-Performance Comparison (Feb 2026)</title>' index.html && echo "PASS: title tag"
grep -q 'cdn.tailwindcss.com' index.html && echo "PASS: Tailwind CDN"
grep -q 'width=device-width' index.html && echo "PASS: viewport meta"
```
</verify>

### Task 2: Build page header with title and description

<action>
Inside body, create a centered container (max-w-5xl mx-auto px-4 py-8):
- h1 heading: "AI Inference Compute Cost-Performance Comparison (Feb 2026)" with text-3xl font-bold text-center mb-6
- Description paragraph with text-gray-600 max-w-3xl mx-auto text-center leading-relaxed containing: "This page provides a factual comparison of effective TFLOPS (floating-point operations per second) per $1 per hour for AI inference across decentralized and traditional GPU rental options."
- Second sentence: "GNUS.ai uses idle consumer devices with dynamic token-based pricing, while the GPU values represent typical cloud rental prices as of February 2026."
- Professional, factual, neutral tone — no marketing language, no superlatives, no hype words
</action>

<read_first>
- .planning/REQUIREMENTS.md (PAGE-01 through PAGE-04)
</read_first>

<acceptance_criteria>
- h1 text matches exactly: "AI Inference Compute Cost-Performance Comparison (Feb 2026)"
- Description contains phrase "effective TFLOPS"
- Description contains phrase "idle consumer devices with dynamic token-based pricing"
- Description contains phrase "GPU rental prices"
- No hype words present (no "revolutionary", "unprecedented", "game-changing", "unmatched", "ultimate", "best-in-class", etc.)
- Text uses professional, neutral language
</acceptance_criteria>

<verify>
```bash
grep -q '<h1.*>AI Inference Compute Cost-Performance Comparison (Feb 2026)</h1>' index.html && echo "PASS: h1 title"
grep -q 'effective TFLOPS' index.html && echo "PASS: TFLOPS mention"
grep -q 'idle consumer devices' index.html && echo "PASS: GNUS description"
grep -q 'GPU rental' index.html && echo "PASS: GPU rental mention"
grep -qi 'revolutionary\|unprecedented\|game-changing\|unmatched\|ultimate\|best-in-class' index.html && echo "FAIL: hype word found" || echo "PASS: no hype words"
```
</verify>

### Task 3: Build GPU selector placeholder area

<action>
Below description, add a section with:
- Container with border border-gray-200 rounded-lg p-4 mb-6 bg-gray-50
- Label text-sm text-gray-500 mb-2: "GPU Selection" (or similar)
- Two inline blocks or flex items showing static text: "GPU 1: H100" and "GPU 2: RTX 3090"
- Text styled as text-lg font-semibold text-gray-700
- Structurally separate from table so Phase 3 can replace with dropdowns
- Note: NO interactive dropdown elements — Phase 3 adds those
</action>

<read_first>
- .planning/phases/01-static-page-foundation/01-CONTEXT.md (D-08, D-09)
</read_first>

<acceptance_criteria>
- Page shows "GPU 1: H100" as static text
- Page shows "GPU 2: RTX 3090" as static text
- Area is clearly labeled as GPU selection
- No select/dropdown elements present in HTML
</acceptance_criteria>

<verify>
```bash
grep -q 'GPU 1: H100' index.html && echo "PASS: GPU 1 label"
grep -q 'GPU 2: RTX 3090' index.html && echo "PASS: GPU 2 label"
grep -q '<select' index.html && echo "FAIL: select element found" || echo "PASS: no dropdowns"
```
</verify>

### Task 4: Build comparison table

<action>
Create the main comparison table below the GPU selector area:
- Table element with class="table-auto w-full border-collapse border border-gray-300"
- Wrap table in div with class="overflow-x-auto" for mobile horizontal scroll
- thead with bg-gray-100:
  - tr with th elements: "Category / Precision Level", "GNUS.ai (Decentralized)", "H100", "RTX 3090"
  - th elements styled: border border-gray-300 px-4 py-3 text-left font-semibold text-sm
- tbody with 5 rows:
  - Row 1: td "FP32 Baseline", td "—" (GNUS), td "—" (H100), td "—" (RTX 3090)
  - Row 2: td "FP16 / Mixed-Precision", td "—", td "—", td "—"
  - Row 3: td "FP8 Quantized", td "—", td "—", td "—"
  - Row 4: td "Adaptive Low-Bit (1.58–4 bit dynamic)", td "—", td "—", td "—"
  - Row 5: td "Typical Blended Inference (small/mid-size models)", td "—", td "—", td "—"
- First column td: font-medium text-gray-800
- Data columns td: text-center text-gray-600
- Alternating row backgrounds: even rows bg-gray-50, odd rows bg-white
- td elements: border border-gray-300 px-4 py-2.5
- Placeholder "—" values in data cells (real data comes in Phase 2)
</action>

<read_first>
- .planning/REQUIREMENTS.md (TABL-01, TABL-02)
- .planning/phases/01-static-page-foundation/01-CONTEXT.md (D-03, D-04, D-05)
</read_first>

<acceptance_criteria>
- Table has 4 columns: Category, GNUS.ai (Decentralized), H100, RTX 3090
- Table has 5 data rows with labels exactly matching: "FP32 Baseline", "FP16 / Mixed-Precision", "FP8 Quantized", "Adaptive Low-Bit (1.58–4 bit dynamic)", "Typical Blended Inference (small/mid-size models)"
- All data cells contain "—"
- Even rows have bg-gray-50 background
- Table is wrapped in overflow-x-auto div
- First column cells are left-aligned with font-medium
- Data column cells are center-aligned
</acceptance_criteria>

<verify>
```bash
grep -q 'FP32 Baseline' index.html && echo "PASS: FP32 row"
grep -q 'Adaptive Low-Bit' index.html && echo "PASS: Adaptive row"
grep -q 'Typical Blended Inference' index.html && echo "PASS: Blended row"
grep -q 'GNUS.ai' index.html && echo "PASS: GNUS column"
grep -q 'overflow-x-auto' index.html && echo "PASS: scroll wrapper"
grep -q 'bg-gray-50' index.html && echo "PASS: alternating rows"
ROW_COUNT=$(grep -c '<tr' index.html); [ "$ROW_COUNT" -ge 6 ] && echo "PASS: $ROW_COUNT rows (>=6)" || echo "FAIL: only $ROW_COUNT rows"
```
</verify>

### Task 5: Build methodology section

<action>
Below the table, add a section:
- Container with mt-8 pt-6 border-t border-gray-200
- h2 heading: "Assumptions & Methodology" with text-xl font-semibold mb-3
- Placeholder content: paragraph with text-gray-500 italic: "Calculation methodology and assumptions will be detailed here. Values are computed as Effective TFLOPS per $1/hr = (Peak TFLOPS × Utilization) / Hourly Rental Price."
- Note: Full methodology content populated in Phase 2
</action>

<read_first>
- .planning/REQUIREMENTS.md (FEAT-02)
- .planning/phases/01-static-page-foundation/01-CONTEXT.md (D-01)
</read_first>

<acceptance_criteria>
- Page contains "Assumptions & Methodology" heading
- Section includes the calculation formula text
- Section is visually separated from table by border-t
</acceptance_criteria>

<verify>
```bash
grep -q 'Assumptions & Methodology' index.html && echo "PASS: methodology heading"
grep -q 'Peak TFLOPS' index.html && echo "PASS: formula mention"
grep -q 'border-t' index.html && echo "PASS: separator border"
```
</verify>

### Task 6: Apply responsive design refinements

<action>
Verify and refine responsive behavior:
- Container uses max-w-5xl with responsive padding (px-4 sm:px-6 lg:px-8)
- h1 uses responsive sizing: text-2xl sm:text-3xl
- Description text uses responsive: text-sm sm:text-base
- Table wrapper uses overflow-x-auto with max-w-full
- GPU selector flex items wrap on small screens
- Footer/methodology section responsive padding
- Test that nothing overflows viewport on 375px width
</action>

<read_first>
- index.html (current state for refinement)
- .planning/phases/01-static-page-foundation/01-CONTEXT.md (D-06, D-07)
</read_first>

<acceptance_criteria>
- Page renders without horizontal overflow (except table which has intentional horizontal scroll)
- h1 text does not overflow on 375px screen width
- GPU selector labels wrap or stack on narrow screens
- All content is readable at 375px width
- No fixed pixel widths that would break responsiveness (view in browser at 375px, 768px, 1280px)
</acceptance_criteria>

<verify>
```bash
grep -q 'max-w-5xl' index.html && echo "PASS: max-width container"
grep -q 'sm:px-6' index.html && echo "PASS: responsive padding"
grep -q 'sm:text-3xl' index.html && echo "PASS: responsive typography"
grep -q 'overflow-x-auto' index.html && echo "PASS: scroll wrapper (intentional)"
# Open in browser and verify no overflow at 375px, 768px, 1280px manually
```
</verify>


