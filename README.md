# GNUS AI Pricing Comparison

Interactive comparison of AI inference compute cost-performance between GNUS.ai decentralized inference and traditional GPU rental options.

**Live page:** Open `index.html` in any browser — no server required.

## Features

- **Interactive GPU selection** — Choose any two GPUs from 7 options (H100, A100, RTX 4090, RTX 3090, RTX 5090 est., Blackwell B200, L40S)
- **Dual display modes** — TFLOPS per $1/hr and $/1K TFLOP/hr (cost view)
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

Hardcoded GPU specifications and pricing as of February 2026. See the methodology section in-page for calculation details.

## License

MIT — see [LICENSE.txt](LICENSE.txt)
