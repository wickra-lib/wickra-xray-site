# About Wickra X-Ray

Wickra X-Ray is a free explorer that shows, historically, what only Wickra computes —
**footprint**, **order-book heatmap**, **liquidation map** and **funding/OI
divergence**. One data-driven core folds a recorded dataset into render data-models; a
front-end just draws them.

## What makes it different

- **Four microstructure panels.** Footprint (traded volume per price bin, split by
  aggressor side), order-book heatmap (resting liquidity over a time × price grid),
  liquidation map (liquidation events clustered by price bin), and funding/OI
  divergence (funding, open interest and price on one time axis).
- **Frames are data, not commands.** `xray-core` folds an `XraySpec` over a recorded
  dataset — trades, order-book diffs, funding and open interest — into `XrayFrame`
  render data-models, never renderer calls. A front-end simply draws the frame.
- **Deterministic core.** The parallel (rayon) and sequential (WASM fallback) builds
  are byte-for-byte identical, and the frame crosses the C ABI and WASM unchanged.
- **Free to explore.** X-Ray reads recorded datasets and renders them; it never
  trades and needs no key.

## Why it exists

Footprint, book heatmaps and liquidation maps are usually locked behind paid
terminals. Wickra X-Ray computes them from open data and defines the surface once, in
Rust, as a JSON-over-C-ABI data API (`Xray::command`), exposed to Rust, Python,
Node.js, WASM and — over a C ABI — C, C++, C#, Go, Java and R, plus a web front-end
(Vue + Canvas) that renders the frames in the browser.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free for
any use including commercial. Source, issues and releases on
[GitHub](https://github.com/wickra-lib/wickra-xray).

## Disclaimer

Wickra X-Ray is a software library, **not** a trading system, and is provided
**as-is with no warranty**. It renders microstructure; it does not give financial
advice. Use it at your own risk.
