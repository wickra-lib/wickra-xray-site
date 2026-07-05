# R

A `.Call` binding over the C ABI. Construct an x-ray from a JSON spec, then drive it
with `wkxray_command(xray, json) -> json` — load a dataset, then build a frame.

```r
install.packages("wickraxray", repos = "https://wickra-lib.r-universe.dev")
```

```r
library(wickraxray)

spec <- paste0(
  '{"dataset_ref":"m","symbol":"BTCUSDT",',
  '"panels":[{"kind":"footprint","price_bin":1.0,"bucket_ms":60000}]}'
)

xray <- wkxray_new(spec)
invisible(wkxray_command(xray, load_cmd))   # {"cmd":"load","dataset": ...}
response <- wkxray_command(xray, '{"cmd":"frame"}')
cat("wickra-xray", wkxray_version(), "\n")
cat(response, "\n")
```

## More

- [r-universe](https://wickra-lib.r-universe.dev)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/r)
