# Java

An FFM (Panama) wrapper over the C ABI. Construct an `Xray` from a JSON spec, then
drive it with `command(json) -> json` — load a dataset, then build a frame.

```xml
<!-- Maven Central -->
<dependency>
  <groupId>org.wickra</groupId>
  <artifactId>wickra-xray</artifactId>
  <version>0.1.0</version>
</dependency>
```

```java
import org.wickra.xray.Xray;

public final class Frame {
    private static final String SPEC =
        "{\"dataset_ref\":\"m\",\"symbol\":\"BTCUSDT\","
        + "\"panels\":[{\"kind\":\"footprint\",\"price_bin\":1.0,\"bucket_ms\":60000}]}";

    public static void main(String[] args) {
        try (Xray xray = new Xray(SPEC)) {
            xray.command(LOAD);   // {"cmd":"load","dataset": ...}
            String response = xray.command("{\"cmd\":\"frame\"}");
            System.out.println("wickra-xray " + Xray.version());
            System.out.println(response);
        }
    }
}
```

The binding uses the Java Foreign Function & Memory API, so it needs JDK 22+ and
`--enable-native-access`.

## More

- [Maven Central](https://central.sonatype.com/artifact/org.wickra/wickra-xray)
- [Source & examples](https://github.com/wickra-lib/wickra-xray/tree/main/examples/java)
