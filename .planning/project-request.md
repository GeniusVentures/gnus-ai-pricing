
**Project Request: Build Interactive AI Compute Performance Comparison Web Page**

Please build a clean, professional, self-contained single HTML file with Tailwind CSS that compares **GNUS.ai decentralized inference** against various GPUs.

### Core Requirements

1. **Page Title**: "AI Inference Compute Cost-Performance Comparison (Feb 2026)"

2. **Description** (above the table):
    - Short paragraph explaining this is a factual comparison of effective TFLOPS per $1 per hour for AI inference.
    - Mention that GNUS.ai uses idle consumer devices with dynamic token-based pricing, while others are GPU rental prices.

3. **Controls** (at the top):
    - Two dropdown selectors labeled **"GPU 1"** and **"GPU 2"**.
    - Default: GPU 1 = H100, GPU 2 = RTX 3090.
    - Options should include: H100, A100, RTX 4090, RTX 3090, RTX 5090 (est.), Blackwell B200, L40S.

4. **Main Interactive Table**
    - Columns:
        - Category / Precision Level
        - GNUS.ai (Decentralized)
        - [GPU 1 Name]
        - [GPU 2 Name]
    - Rows (categories):
        - FP32 Baseline
        - FP16 / Mixed-Precision
        - FP8 Quantized
        - Adaptive Low-Bit (1.58–4 bit dynamic)
        - Typical Blended Inference (small/mid-size models)

5. **Data & Calculation Logic** (very important — implement accurately):

**GNUS.ai (fixed values)**:
- FP32: 200
- FP16: 600
- FP8: 1400
- Adaptive Low-Bit: 3500
- Blended: 2200

**GPU Calculation Formula** (for all rental GPUs):
- Effective TFLOPS per $1/hr = (Peak TFLOPS in that precision × Utilization) / Hourly Rental Price

**Default Values to Use**:
- **H100**: $2.00/hr, Utilization 60%
    - FP32: 67 TFLOPS → ~20
    - FP16: ~1,500 effective → ~450–750 range (use 750)
    - FP8: ~2,500–3,500 effective → 950
    - Adaptive: 800 (limited gain)

- **RTX 3090**: $0.25/hr, Utilization 60%
    - FP32: 35.6 TFLOPS → ~65–85
    - FP16: ~140–180 TFLOPS → ~320–380
    - FP8: ~500–600
    - Adaptive: ~750

- Add similar realistic values for other GPUs (RTX 4090 ~$0.35/hr, B200 higher performance but ~$3.50/hr, etc.)

6. **Features Requested**:
    - Table updates live when dropdowns change.
    - Clean, readable design with Tailwind CSS.
    - Highlight GNUS.ai column (e.g., light green background or bold).
    - Add a small "Assumptions & Methodology" section at the bottom explaining how numbers are calculated (utilization, pricing, low-precision multipliers, etc.).
    - Responsive design.

7. **Tone**: Professional, factual, neutral — no hype language.

Please generate the complete single-file HTML with embedded Tailwind and JavaScript.
