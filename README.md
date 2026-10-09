# GNUS AI Pricing Comparison

Interactive comparison of AI inference compute cost-performance between GNUS.ai decentralized inference and traditional GPU rental options.

**Live page:** Open `index.html` in any browser — no server required.

## Features

- **Interactive GPU selection** — Choose any two GPUs from 7 options (H100, A100, RTX 4090, RTX 3090, RTX 5090 est., Blackwell B200, L40S)
- **Dual display modes** — TFLOPS per $1/hour and USD per 1,000 effective TFLOPS-hours (cost view)
- **Live recalculation** — Table updates instantly on any selection change
- **5 precision levels** — FP32, FP16, FP8, Adaptive Low-Bit, and Blended Inference
- **GNUS.ai highlighted** — Visual distinction for decentralized inference comparison
- **Methodology documented** — Full assumptions, pricing sources, and precision multiplier explanations

## Tech Stack

Single self-contained HTML file — no build tools, no framework, no server.

- Tailwind CSS (CDN)
- Vanilla JavaScript
- Static deployment

## Data

Hardcoded GPU specifications and prices as of February 2026. **GNUS-side effective TFLOPS-per-dollar values are illustrative inputs from the original project request, not independently observed production-network benchmarks.** They must not be interpreted as an available mainnet compute tariff, an approved API price, or demonstrated savings.

The **rental-GPU columns only** use the following formulas. The GNUS.ai column instead displays five fixed February 2026 scenario ratios (200, 600, 1,400, 3,500, 2,200), and cost mode simply inverts each as `1000 / supplied_GNUS_ratio`. No GNUS peak throughput, hourly rental cost, or measured network price is derived:

```text
effective_TFLOPS_per_$1_hour = peak_TFLOPS_at_precision * utilization / rental_USD_per_hour
USD_per_1000_effective_TFLOPS_hour = 1000 / effective_TFLOPS_per_$1_hour
```

See [GNUS Pricing Methodology and Status](https://docs.gnus.ai/about-gnus.ai/features-and-benefits/pricing-methodology/) for the difference between this throughput model, historical $0.005/node-hour cases, and the **owner-set but not yet implemented $0.0003 per funded ELM-job processing-hour** rate. **Pooled job-hours versus separate per-ELM allocations remain undecided**; never automatically multiply by ELM count. Existing general-processing jobs instead estimate native work using caller-supplied `dimensions.block_len`, interpreted as bytes by the FLOPs-per-byte price formula. That assumption may be wrong when a processor uses patch depth or element count; the quote is not a measure of actual FLOPs or runtime. The estimated USD amount is converted to GNUS at the current token quote for escrow. None of these figures establishes a GCS public API retail tariff.

## License

MIT — see [LICENSE.txt](LICENSE.txt)
