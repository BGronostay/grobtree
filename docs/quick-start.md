# GrobTree 5-Minute Quick Start

This short tour uses the sample logs in this repository and the built-in GrobTree configuration.

## Prerequisites

- IntelliJ IDEA 2025.1 or newer, or a compatible JetBrains IDE.
- The GrobTree plugin ZIP from the [latest public release](https://github.com/bgronostay/grobtree/releases/latest).

## Install

1. Download the GrobTree plugin ZIP from the [latest public release](https://github.com/bgronostay/grobtree/releases/latest).
2. In IntelliJ IDEA, open `Settings > Plugins`.
3. Click the gear icon and choose `Install Plugin from Disk...`.
4. Select the ZIP file and restart the IDE when prompted.

## Open GrobTree

1. Open a project in IntelliJ IDEA.
2. Choose `View > Tool Windows > GrobTree`.
3. Create a new GrobTree tab if the tool window is empty.

## Your First Log Analysis

1. Click the import action in the GrobTree toolbar.
2. Select one of the bundled sample logs:
   - `examples/logs/cxf-example.log`
   - `examples/logs/spring-rest-example.log`
3. Keep the built-in configuration selected.
4. Start the import and expand the generated tree.

The CXF sample is the best first tour because it shows request/response correlation and the replay actions.

## Try Request Replay

1. Import `examples/logs/cxf-example.log`.
2. Select a replayable Apache CXF request node.
3. Open the context menu.
4. Use `Create CURL Command` or `Replay In HTTP Client`.

## Next Steps

- Read [Using GrobTree](./using-grobtree.md) for the full tool window workflow.
- Read [Replay Apache CXF Requests](./cxf-request-replay.md) for replay-specific behavior.
- Read [ConverterConfig.xml Reference](./converter-config.md) when you want to tune parsing rules.
