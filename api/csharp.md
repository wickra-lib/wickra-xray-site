# C#

Idiomatic .NET over the C ABI. Construct an `Xray` from a JSON spec, then drive it
with `Command(json) -> json` — load a dataset, then build a frame.

```bash
dotnet add package WickraXray
```

```csharp
using Wickra.Xray;

var spec = """
{"dataset_ref":"m","symbol":"BTCUSDT",
 "panels":[{"kind":"footprint","price_bin":1.0,"bucket_ms":60000}]}
""";

using var xray = new Xray(spec);
xray.Command(load);   // {"cmd":"load","dataset": ... }
var response = xray.Command("""{"cmd":"frame"}""");
Console.WriteLine(response);
```

Targets .NET 8.

## More

- [NuGet](https://www.nuget.org/packages/WickraXray)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/csharp)
