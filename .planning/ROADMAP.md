# Roadmap: GNUS AI Pricing Comparison

**Defined:** 2026-05-29
**Granularity:** Coarse
**Mode:** mvp

## Phases

- [ ] **Phase 1: Static Page Foundation** — Complete HTML page with all content, table structure, and Tailwind styling
- [ ] **Phase 2: Data & Visual Features** — GPU data calculations, GNUS column highlighting, and assumptions documentation
- [ ] **Phase 3: Interactivity** — GPU dropdown selectors and live table updates

## Phase Details

### Phase 1: Static Page Foundation
**Mode:** mvp
**Goal:** Users can view a complete, well-designed comparison page with all content and table structure, using hardcoded default GPUs.
**Depends on:** Nothing
**Requirements:** PAGE-01, PAGE-02, PAGE-03, PAGE-04, TABL-01, TABL-02, FEAT-03, FEAT-04
**Success Criteria** (what must be TRUE):
  1. Page displays the title "AI Inference Compute Cost-Performance Comparison (Feb 2026)"
  2. Description paragraph explains the effective TFLOPS per $1 per hour comparison concept
  3. Description mentions GNUS.ai uses idle consumer devices with dynamic token-based pricing, while others are GPU rental prices
  4. Comparison table is visible with all five precision level rows and column headers for Category/Precision Level, GNUS.ai (Decentralized), and two GPUs
  5. Page uses clean Tailwind CSS styling and adapts layout to different screen sizes (desktop, tablet, mobile)
  6. All text maintains a professional, factual, neutral tone — no marketing language
**Plans:** TBD
**UI hint:** yes

### Phase 2: Data & Visual Features
**Mode:** mvp
**Goal:** Users see accurate TFLOPS-per-dollar values for GNUS.ai and both default GPUs across all precision levels, with methodology explained.
**Depends on:** Phase 1
**Requirements:** DATA-01, DATA-02, DATA-03, DATA-04, DATA-05, FEAT-01, FEAT-02
**Success Criteria** (what must be TRUE):
  1. GNUS.ai column displays the correct fixed values: FP32=200, FP16=600, FP8=1400, Adaptive Low-Bit=3500, Blended=2200
  2. Each GPU column shows values calculated as (Peak TFLOPS × 60% utilization) / hourly rental price, matching the specified data for all seven GPUs
  3. GNUS.ai column is visually distinct from other columns (light green background or bold styling)
  4. "Assumptions & Methodology" section at page bottom explains utilization assumptions, pricing sources, and low-precision multiplier logic
**Plans:** TBD
**UI hint:** yes

### Phase 3: Interactivity
**Mode:** mvp
**Goal:** Users can select any two GPUs from dropdowns and see the comparison table update instantly with recalculated values.
**Depends on:** Phase 2
**Requirements:** CTRL-01, CTRL-02, CTRL-03, TABL-03
**Success Criteria** (what must be TRUE):
  1. Two dropdown selectors labeled "GPU 1" and "GPU 2" are displayed above the comparison table
  2. GPU 1 dropdown defaults to H100 and GPU 2 defaults to RTX 3090
  3. All seven GPU options (H100, A100, RTX 4090, RTX 3090, RTX 5090 est., Blackwell B200, L40S) are available in both dropdowns
  4. Changing either GPU dropdown selection instantly recalculates and updates the corresponding table column with correct effective TFLOPS/$1/hr values
**Plans:** TBD
**UI hint:** yes

## Progress

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Static Page Foundation | 0/0 | Not started | - |
| 2. Data & Visual Features | 0/0 | Not started | - |
| 3. Interactivity | 0/0 | Not started | - |
