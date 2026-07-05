# Node.js

Native napi-rs bindings over the Rust core. Construct an `Xray` from a JSON spec, then
drive it with `command(json) -> json` — load a dataset, then build a frame.

```bash
npm install wickra-xray
```

```javascript
import { Xray } from 'wickra-xray'

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

- [npm](https://www.npmjs.com/package/wickra-xray)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/node)
