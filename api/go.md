# Go

A cgo wrapper over the C ABI. Construct an `Xray` from a JSON spec, then drive it with
`Command(json) -> json` — load a dataset, then build a frame.

```bash
go get github.com/wickra-lib/wickra-xray-go
```

```go
package main

import (
	"fmt"

	wickra "github.com/wickra-lib/wickra-xray-go"
)

const spec = `{"dataset_ref":"m","symbol":"BTCUSDT",` +
	`"panels":[{"kind":"footprint","price_bin":1.0,"bucket_ms":60000}]}`

func main() {
	xray, err := wickra.New(spec)
	if err != nil {
		panic(err)
	}
	defer xray.Close()

	if _, err := xray.Command(load); err != nil { // {"cmd":"load","dataset": ...}
		panic(err)
	}
	frame, err := xray.Command(`{"cmd":"frame"}`)
	if err != nil {
		panic(err)
	}
	fmt.Println("wickra-xray", wickra.Version())
	fmt.Println(frame)
}
```

## More

- [Go module (pkg.go.dev)](https://pkg.go.dev/github.com/wickra-lib/wickra-xray-go)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/go)
