# Requirements: GNUS AI Pricing Comparison

**Defined:** 2026-05-29
**Core Value:** Users can interactively compare the cost-performance of GNUS.ai decentralized inference against any two GPUs of their choice, with live-updating data across multiple precision levels.

## v1 Requirements

Requirements for initial release. Each maps to roadmap phases.

### Page Structure

- [ ] **PAGE-01**: Page displays title "AI Inference Compute Cost-Performance Comparison (Feb 2026)"
- [ ] **PAGE-02**: Description paragraph explains factual comparison of effective TFLOPS per $1 per hour for AI inference
- [ ] **PAGE-03**: Description mentions GNUS.ai uses idle consumer devices with dynamic token-based pricing, while others are GPU rental prices
- [ ] **PAGE-04**: Professional, factual, neutral tone throughout — no hype or marketing language

### Controls

- [ ] **CTRL-01**: Two dropdown selectors labeled "GPU 1" and "GPU 2" displayed above the table
- [ ] **CTRL-02**: GPU 1 defaults to H100, GPU 2 defaults to RTX 3090
- [ ] **CTRL-03**: GPU options include H100, A100, RTX 4090, RTX 3090, RTX 5090 (est.), Blackwell B200, and L40S

### Interactive Table

- [ ] **TABL-01**: Table columns: Category/Precision Level, GNUS.ai (Decentralized), [GPU 1 Name], [GPU 2 Name]
- [ ] **TABL-02**: Table rows cover FP32 Baseline, FP16/Mixed-Precision, FP8 Quantized, Adaptive Low-Bit (1.58–4 bit dynamic), and Typical Blended Inference
- [ ] **TABL-03**: Table updates live when GPU dropdown selections change

### Data & Calculations

- [ ] **DATA-01**: GNUS.ai displays fixed values — FP32: 200, FP16: 600, FP8: 1400, Adaptive Low-Bit: 3500, Blended: 2200
- [ ] **DATA-02**: GPU values calculated as Effective TFLOPS per $1/hr = (Peak TFLOPS × Utilization) / Hourly Rental Price
- [ ] **DATA-03**: H100 data configured ($2.00/hr, 60% utilization, precision-specific TFLOPS values)
- [ ] **DATA-04**: RTX 3090 data configured ($0.25/hr, 60% utilization, precision-specific TFLOPS values)
- [ ] **DATA-05**: Realistic values configured for remaining GPUs (RTX 4090, A100, L40S, RTX 5090 est., Blackwell B200)

### Visual & UX Features

- [ ] **FEAT-01**: GNUS.ai column visually highlighted (light green background or bold styling)
- [ ] **FEAT-02**: "Assumptions & Methodology" section at page bottom explaining utilization, pricing, and low-precision multiplier assumptions
- [ ] **FEAT-03**: Clean, readable table design using Tailwind CSS
- [ ] **FEAT-04**: Responsive design that adapts to different screen sizes

## Out of Scope

| Feature | Reason |
|---------|--------|
| Dark mode toggle | Out of scope for v1; can add later |
| Export table to CSV/PDF | Out of scope for v1 |
| Mobile app | Web-only by design |
| Backend API / real-time pricing | Hardcoded reference data only |
| User-submitted GPU benchmarks | Static data, no crowdsourcing |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| PAGE-01 | Phase 1 | Pending |
| PAGE-02 | Phase 1 | Pending |
| PAGE-03 | Phase 1 | Pending |
| PAGE-04 | Phase 1 | Pending |
| CTRL-01 | Phase 1 | Pending |
| CTRL-02 | Phase 1 | Pending |
| CTRL-03 | Phase 1 | Pending |
| TABL-01 | Phase 1 | Pending |
| TABL-02 | Phase 1 | Pending |
| TABL-03 | Phase 1 | Pending |
| DATA-01 | Phase 1 | Pending |
| DATA-02 | Phase 1 | Pending |
| DATA-03 | Phase 1 | Pending |
| DATA-04 | Phase 1 | Pending |
| DATA-05 | Phase 1 | Pending |
| FEAT-01 | Phase 1 | Pending |
| FEAT-02 | Phase 1 | Pending |
| FEAT-03 | Phase 1 | Pending |
| FEAT-04 | Phase 1 | Pending |

**Coverage:**
- v1 requirements: 19 total
- Mapped to phases: 0 (pending roadmap)
- Unmapped: 19 ⚠️

---
*Requirements defined: 2026-05-29*
*Last updated: 2026-05-29 after initial definition*
