# Rust

The native crate. Fold an `XraySpec` over a `Dataset` with `build_frame` to get an
`XrayFrame` of render data-models.

```bash
cargo add wickra-xray
```

```rust
use xray_core::{build_frame, Dataset, XraySpec};

const SPEC: &str = r#"{
    "dataset_ref": "m",
    "symbol": "BTCUSDT",
    "panels": [{"kind": "footprint", "price_bin": 1.0, "bucket_ms": 60000}]
}"#;

let spec = XraySpec::from_json(SPEC).expect("valid spec");
let mut dataset = Dataset::from_json(DATASET).expect("valid dataset");
dataset.sort();
let cursor = dataset.bounds().map_or(0, |(_, hi, _)| hi);

let frame = build_frame(&dataset, &spec, cursor).expect("build frame");
println!("{} panels", frame.panels.len());
```

## More

- [crates.io/crates/wickra-xray](https://crates.io/crates/wickra-xray) · [docs.rs](https://docs.rs/wickra-xray)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/rust)
- [Panels & spec](https://github.com/wickra-lib/wickra-xray/tree/main/docs)
