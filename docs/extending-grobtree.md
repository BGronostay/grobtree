# Extending GrobTree

GrobTree exposes a stable public API to customise ingestion, processing, and presentation. The artifacts are published to Maven Central:
```xml
<dependency>
    <groupId>net.gronostay.grobtree</groupId>
    <artifactId>grobtree-api</artifactId>
    <version><!-- latest --></version>
</dependency>
```

## Extension Building Blocks
- **Factories (`net.gronostay.grobtree.api.processing.Factory`)** – Resolve named components from your JAR (e.g., processing listeners, node factories).
- **Processing Listeners** – Implement `ProcessingListener` to interpret log entries and populate the `LogTree`.
- **Log Providers** – Implement `LogProviderListener` to transform custom file formats into structured message buffers.
- **Top Node Creators & Statistics** – Create reusable building blocks that add domain-specific visualisations and expose metrics via `StatisticsProvider`.

## Sample Extension
The publicly available [`grobtree-example-extension`](https://github.com/bgronostay/grobtree-example-extension) demonstrates:
- A factory (`SampleExtensionFactory`) that returns components by `factoryUniqueName`.
- A processing listener that groups request/response pairs, attaches icons/colours, and marks corresponding nodes.
- A CSV log provider that injects metadata from custom-delimited logs.
- A ready-made `SampleConverterConfig.xml`, plus demo log files for quick testing.

Build it with Maven, point GrobTree’s settings to the produced JAR, and load the sample logs to see the end-to-end workflow.
