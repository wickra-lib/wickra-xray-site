---
layout: home
title: Wickra X-Ray — a free market-microstructure explorer
titleTemplate: false

hero:
  name: "Wickra X-Ray"
  text: "See what only Wickra computes."
  tagline: "A free explorer that shows, historically, footprint, order-book heatmap, liquidation map and funding/OI divergence — one data-driven core folds a recorded dataset into render frames, drawn in the browser."
  image:
    src: /wickra-mark.svg
    alt: Wickra X-Ray
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-xray
    - theme: alt
      text: Panels & spec
      link: https://github.com/wickra-lib/wickra-xray/tree/main/docs
    - theme: alt
      text: API
      link: /api/rust

features:
  - icon: 👣
    title: Footprint
    details: "Traded volume per price bin, split by aggressor side — see where buyers and sellers actually transacted, bar by bar."
  - icon: 🔥
    title: Order-book heatmap
    details: "Resting liquidity over a time × price grid — watch walls build and pull as the book evolves."
  - icon: 💥
    title: Liquidation map
    details: "Liquidation events clustered by price bin — spot the cascades and where forced selling concentrated."
  - icon: 📉
    title: Funding / OI divergence
    details: "Funding, open interest and price on one time axis — see leverage build and unwind against the move."
  - icon: 🧩
    title: Frames are data, not code
    details: "xray-core folds an XraySpec over a recorded dataset into XrayFrame render data-models. Because it is data, the same frame crosses the C ABI and WASM unchanged."
  - icon: 🌐
    title: 10 languages
    details: "The core is a JSON-over-C-ABI data API (Xray::command) in Rust, Python, Node.js, WASM, C, C++, C#, Go, Java and R, plus a web renderer."
---

<script setup>
const installTabs = [
  { label: 'Python', lang: 'bash', code: 'pip install wickra-xray' },
  { label: 'Node',   lang: 'bash', code: 'npm install wickra-xray' },
  { label: 'Rust',   lang: 'bash', code: 'cargo add wickra-xray' },
  { label: 'WASM',   lang: 'bash', code: 'npm install wickra-xray-wasm' },
  { label: 'C',      lang: 'bash', code: '# prebuilt header + library from GitHub releases:\n# github.com/wickra-lib/wickra-xray/releases' },
  { label: 'C#',     lang: 'bash', code: 'dotnet add package WickraXray' },
  { label: 'Go',     lang: 'bash', code: 'go get github.com/wickra-lib/wickra-xray-go' },
  { label: 'Java',   lang: 'xml',  code: '<!-- Maven Central -->\n<dependency>\n  <groupId>org.wickra</groupId>\n  <artifactId>wickra-xray</artifactId>\n  <version>0.1.0</version>\n</dependency>' },
  { label: 'R',      lang: 'r',    code: 'install.packages("wickraxray", repos = "https://wickra-lib.r-universe.dev")' },
]

const pyCode = `import json
from wickra_xray import Xray

spec = json.dumps({
    "dataset_ref": "m",
    "symbol": "BTCUSDT",
    "panels": [{"kind": "footprint", "price_bin": 1.0, "bucket_ms": 60000}],
})

xray = Xray(spec)
xray.command(json.dumps({"cmd": "load", "dataset": dataset}))
frame = json.loads(xray.command(json.dumps({"cmd": "frame"})))
print(len(frame["panels"]), "panels")`

const nodeCode = `import { Xray } from 'wickra-xray'

const spec = JSON.stringify({
  dataset_ref: 'm',
  symbol: 'BTCUSDT',
  panels: [{ kind: 'footprint', price_bin: 1.0, bucket_ms: 60000 }],
})

const xray = new Xray(spec)
xray.command(JSON.stringify({ cmd: 'load', dataset }))
const frame = JSON.parse(xray.command(JSON.stringify({ cmd: 'frame' })))
console.log(frame.panels.length, 'panels')`

const cliCode = `# Build a footprint frame from a recorded dataset (deterministic, offline):
wickra-xray --spec golden/specs/footprint.json --stdin --format json < golden/data.json

# Build all four panels at once:
wickra-xray --spec golden/specs/multi_panel.json --stdin --format json < golden/data.json`

const snippetTabs = [
  { label: 'Python', lang: 'python',     code: pyCode },
  { label: 'Node',   lang: 'javascript', code: nodeCode },
  { label: 'CLI',    lang: 'bash',       code: cliCode },
]
</script>

## The spec is JSON, not code

An `XraySpec` names the `symbol` and the `panels` to build — each with its own binning
(`price_bin`, `bucket_ms`). The core folds the recorded dataset into a frame of render
data-models.

```json
{
  "dataset_ref": "m",
  "symbol": "BTCUSDT",
  "panels": [
    { "kind": "footprint", "price_bin": 1.0, "bucket_ms": 60000 },
    { "kind": "book_heatmap", "price_bin": 1.0, "bucket_ms": 60000 },
    { "kind": "liquidation_map", "price_bin": 1.0, "bucket_ms": 60000 },
    { "kind": "funding_oi_divergence", "bucket_ms": 60000 }
  ]
}
```

Because the spec is data, the same frame crosses the C ABI and WASM unchanged, and
comes back byte-for-byte in every language.

## Install

The same explorer from every language — native Rust, Python, Node.js and WASM, plus a
C ABI for C, C++, C#, Go, Java and R.

<InstallTabs :tabs="installTabs" />

## Load a dataset, build a frame

Build an X-ray from a spec, load a recorded dataset, then pull the frame. The
`command` API returns the same bytes in every binding — the [web renderer](https://github.com/wickra-lib/wickra-xray/tree/main/web)
(Vue + Canvas) is just another consumer of these frames.

<InstallTabs :tabs="snippetTabs" />

## Built on the Wickra core

Wickra X-Ray is part of the [Wickra](https://wickra.org) ecosystem. Its panels are
computed from the same typed microstructure feeds that
[`wickra-core`](https://github.com/wickra-lib/wickra) and
[`wickra-exchange`](https://github.com/wickra-lib/wickra-exchange) produce, so an X-ray
shows exactly the numbers a backtest or a live chart would see.

> Wickra X-Ray is a software library, not a trading system, and gives no financial
> advice — use at your own risk.
