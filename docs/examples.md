# GrobTree Examples & Sample Logs

GrobTree ships with curated logs so you can tour the plugin, benchmark custom configurations, or demo key features without wiring up your own services. This page explains what each asset contains and how to generate fresh datasets.

## Bundled Logs (`examples/logs/`)

| File | Highlights | Great for |
| --- | --- | --- |
| [`cxf-example.log`](../examples/logs/cxf-example.log) | Full Apache CXF request/response flow with SOAP envelopes, attachments, and GrobTree statistics. | Showcasing deep nesting, correlation pairs, and converter-driven colouring. |
| [`spring-rest-example.log`](../examples/logs/spring-rest-example.log) | JSON-heavy REST API traffic including headers, payloads, KPI calculations, and error handling. | Demonstrating tree navigation with rich payloads plus success/error side-by-side. |

### Using the Logs
1. Install GrobTree and open the tool window.
2. Create a new tab and confirm the default **RFC 3339 timestamp and level** regex is selected.
3. Click **Import logs → Start Import** and pick the desired file.
4. Expand the tree to explore how the converter turns raw text into structured nodes.

> Tip: Save the processed tree to a file using the **Save buffer** action. The exported `.grobtree` file can be shared with teammates who have the plugin installed.

## Generating Fresh Logs (`grobtree-testing`)

The [`grobtree-testing`](https://github.com/bgronostay/grobtree-testing) repository contains runnable services that emit verbose logs tailored for GrobTree demos.

```bash
git clone https://github.com/bgronostay/grobtree-testing.git
cd grobtree-testing/cxf-example
./mvnw spring-boot:run
```

Attach GrobTree to the Spring Boot run configuration (or import the generated log file) to see live updates flow into the tree.

## Curating Your Own Examples
- **Start from the converters** – copy the bundled `ConverterConfig.xml` and tweak the regex or evaluation presets.
- **Capture both happy-path and error scenarios** – GrobTree shines when contrasting nodes sit next to each other.
- **Version your configs** – include the config ID/name in the filename so teammates know which preset to load.
- **Bundle icons and branding** – when distributing a JAR-based config, include custom icons for a polished tree.

Share standout samples via pull requests—fresh logs help the community learn new troubleshooting patterns.
