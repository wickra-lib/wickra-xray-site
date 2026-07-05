# WASM

A `wasm-bindgen` build for the browser and other WebAssembly runtimes — the same core
that drives the bundled web renderer. The same `Xray` handle and JSON command protocol
as the native bindings, producing byte-identical frames.

```bash
npm install wickra-xray-wasm
```

```javascript
import init, { Xray } from 'wickra-xray-wasm'

await init()

const spec = JSON.stringify({
  dataset_ref: 'm',
  symbol: 'BTCUSDT',
  panels: [{ kind: 'footprint', price_bin: 1.0, bucket_ms: 60000 }],
})

const xray = new Xray(spec)
xray.command(JSON.stringify({ cmd: 'load', dataset }))
const frame = JSON.parse(xray.command(JSON.stringify({ cmd: 'frame' })))
console.log(frame.panels.length, 'panels')
```

## More

- [npm (wickra-xray-wasm)](https://www.npmjs.com/package/wickra-xray-wasm)
- [Web renderer](https://github.com/wickra-lib/wickra-xray/tree/main/web) · [Source & bindings](https://github.com/wickra-lib/wickra-xray/tree/main/bindings/wasm)
