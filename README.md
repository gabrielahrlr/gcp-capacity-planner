# Vertex AI Capacity Planner

A single-file, browser-based calculator for estimating capacity and cost of
Google's Generative AI models on Vertex AI. Compare PayGo tiers against
Provisioned Throughput (PT) commitments and explore hybrid scenarios.

## Usage

Open `capacity_planner.html` in any modern browser — no server, no build step.

```sh
open capacity_planner.html
```

## What it does

- **Configuration & Inputs** — pick a model (Gemini 3.x, Gemini 2.5 family, Veo)
  and define your workload: input/output modalities per query, average / peak /
  low QPS, peak and low traffic hours.
- **Predefined Scenarios** — generates eight strategy comparisons (A–H) mixing
  PT baselines with PayGo Standard / Priority spillage.
- **Custom Explorer** — sliders for a custom PT baseline (in GSUs) and a
  Priority/Standard mix for spillage above that baseline.
- **Readme & Guide** — in-app notes and limitations.

## Estimation modes

- **Normal workload definition** — units/query × QPS across Average / Peak / Low.
- **Tokens per second** — locks QPS to 1, treating inputs as raw units/second.
- **Quick ballpark** — simplified four-row comparison (Full PayGo Std,
  Full PayGo Prio, Full PT) for fast sizing.

## Pricing notes

- The 1-week commit price in `MODEL_SPECS` is the **weekly** rate; the column
  header reads "1 Week Commit (monthly price)" and the displayed value is
  multiplied by `WEEKS_PER_MONTH` (= 4) to express it as monthly cost.
- PayGo cost assumes steady-state traffic for the configured peak/low hours
  with `DAYS_PER_MONTH = 30`.
- Gemini 3.x models are in Preview; pricing and availability are subject
  to change. Verify against the official Vertex AI pricing page before
  committing.

## Tech

Plain HTML + CSS + vanilla JavaScript. All model specs, burndown rates, and
prices live in the `MODEL_SPECS` object inside `capacity_planner.html`, for simplicity and lightweight hosting.

## License

See `LICENSE`.
