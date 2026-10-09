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

The two displayed formulas are:

```text
effective_TFLOPS_per_$1_hour = peak_TFLOPS_at_precision * utilization / rental_USD_per_hour
USD_per_1000_effective_TFLOPS_hour = 1000 / effective_TFLOPS_per_$1_hour
```

See [GNUS Pricing Methodology and Status](https://docs.gnus.ai/about-gnus.ai/features-and-benefits/pricing-methodology/) for the difference between this throughput model, historical $0.005/node-hour figures, proposed $0.0003/active external ELM-hour cognitive compute assumptions, and native per-FLOP estimators. No GCS API retail price is finalized by this table.

## License

MIT — see [LICENSE.txt](LICENSE.txt)
