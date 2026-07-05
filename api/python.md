# Python

Native PyO3 bindings over the Rust core. Construct an `Xray` from a JSON spec, then
drive it with `command(json) -> json` — load a dataset, then build a frame.

```bash
pip install wickra-xray
```

```python
import json
from wickra_xray import Xray

spec = json.dumps({
    "dataset_ref": "m",
    "symbol": "BTCUSDT",
    "panels": [{"kind": "footprint", "price_bin": 1.0, "bucket_ms": 60000}],
})

xray = Xray(spec)
xray.command(json.dumps({"cmd": "load", "dataset": dataset}))
frame = json.loads(xray.command(json.dumps({"cmd": "frame"})))
print(len(frame["panels"]), "panels")
```

## More

- [PyPI](https://pypi.org/project/wickra-xray/)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/python)
