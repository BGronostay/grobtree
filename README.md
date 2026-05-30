<img src="docs/images/tree64.svg" alt="GrobTree Icon" width="180" />

# GrobTree – Structured Log Intelligence for IntelliJ IDEA

**Explore complex logs without leaving your IDE.** GrobTree clusters raw streams into interactive trees so you can spot request/response pairs, runtime metrics, and payload anomalies in seconds.

[Download the latest plugin ZIP →](https://github.com/bgronostay/grobtree/releases/latest) [Open the documentation →](./docs/README.md)

---

## Why GrobTree
- **Shorten log spelunking** – Replace scrolling text panes with a drill-down tree that keeps structure, colours, and icons aligned with your domain.
- **Stay in IntelliJ IDEA** – Attach GrobTree directly to run/debug configurations or tail external files; no extra viewers required.
- **Bring your own semantics** – Customise parsing, captions, icons, and KPIs through `ConverterConfig.xml` and extension APIs.
- **Share live insight** – Export processed trees, capture statistics, and bake presets so every teammate sees the same, reliable view.

---

## Feature Highlights
- **One Log, Many Views** – Split raw logs into individual outputs using regex boundaries or single-line mode. Each output becomes a node with fully customisable captions, colours, icons, and metadata.
- **Live Streaming & Attachments** – Consume logs on-the-fly from IntelliJ run configurations, external processes, and file tails. GrobTree manages one tab per stream and keeps stripes/icons in sync with running state.
- **Rich Tree Navigation** – Expand/collapse top-level entries, inspect nested payloads, open correlated nodes, and jump straight into a common text editor to see the original snippet.
- **Search & Correlation** – Use the integrated find toolbar to highlight matching nodes. Corresponding-node comparers detect request/response pairs so you can traverse related log entries without scanning by hand.
- **Statistics & Metrics** – Capture runtime stats (durations, message counts, custom KPIs) from your top-node creators and visualise them in context.
- **Built-in CXF Support & Extensible Parsing** – Includes Apache CXF advanced logging support and can be tuned for other log styles using the external configuration format.
- **One-Click CXF Request Replay** – Right-click replayable CXF request nodes to generate a `curl` command (clipboard) or open a ready-to-run IntelliJ HTTP request file.

![Full GrobTree View with CXF Demo Output](docs/images/FullScreenCxfExample.png)

---

## 🚀 Quick Start

Get started in just 5 minutes with the **[5-Minute Quick Start Guide](./docs/quick-start.md)**. GrobTree currently requires IntelliJ IDEA 2025.1+ or another compatible JetBrains IDE.

1. **📥 Install** – Download the latest ZIP and install via *Settings → Plugins → ⚙ → Install Plugin from Disk…*
2. **🎯 Open** – Launch GrobTree from *View → Tool Windows → GrobTree*
3. **📁 Import** – Try our sample logs:
   - [`spring-rest-example.log`](./examples/logs/spring-rest-example.log) – REST API with JSON
   - [`cxf-example.log`](./examples/logs/cxf-example.log) – SOAP/REST with CXF
4. **🔍 Explore** – See your logs transformed into an interactive tree!

Prefer live data? Use **Open tabs for running processes and start evaluating** to attach GrobTree to your running applications.

- **[5-Minute Guide](./docs/quick-start.md)** – Step-by-step visual tutorial
- **[Configuration Reference](./docs/converter-config.md)** – Build your own parsing rules
- **[Guided Tour](./docs/quick-start.md#your-first-log-analysis)** – Hands-on exercise

---

## Documentation Map
- [Docs index](./docs/README.md) – One-stop navigation for every guide.
- **Onboarding**
  - [Getting Started Guide](./docs/getting-started.md) – Installation, configuration sources, and demo walkthrough.
- **Daily Usage**
  - [Using GrobTree](./docs/using-grobtree.md) – All tool window controls, live streaming tips, and working with statistics.
  - [Replay Apache CXF Requests](./docs/cxf-request-replay.md) – Generate `curl` and IntelliJ HTTP requests directly from CXF request logs.
  - [IntelliJ Settings](./docs/intellij-settings.md) – Every option inside *Settings → Tools → GrobTree*.
  - [Examples & Sample Logs](./docs/examples.md) – What each curated log showcases and how to generate fresh ones.
- **Reference**
  - [Extending GrobTree](./docs/extending-grobtree.md) – Public APIs and example extension structure.
  - [ConverterConfig.xml Reference](./docs/converter-config.md) – Schema walkthrough for crafting custom parsers.
- **Help**
  - [FAQ & Support](./docs/faq.md) – Troubleshooting, known issues, and how to reach us.

---

## Distribution & Legal
- The GrobTree IntelliJ plugin is distributed under a proprietary EULA and is currently free to use.
- The GrobTree API is published separately under its own open-source license.
- Related example projects may use their own licenses.
- Read the [End User License Agreement](./docs/legal/eula.md) and [Privacy Policy](./docs/legal/privacy.md).

---

## Ecosystem Projects
| Project | Description |
| ------- | ----------- |
| [`grobtree-api`](https://central.sonatype.com/artifact/net.gronostay.grobtree/grobtree-api) | Public Java API for building GrobTree extensions. Available on Maven Central. |
| [`grobtree-testing`](https://github.com/bgronostay/grobtree-testing) | Demo projects (e.g., Apache CXF app) that emit logs suited for GrobTree evaluators. |
| [`grobtree-example-extension`](https://github.com/bgronostay/grobtree-example-extension) | Reference implementation showcasing custom factories, listeners, and log providers. |

---

## Support & Feedback
- Browse the [FAQ](./docs/faq.md) and [Getting Started](./docs/getting-started.md) guides for quick answers.
- Open an issue in the [GrobTree documentation and support repository](https://github.com/bgronostay/grobtree/issues) for bugs or feature requests.
- For docs improvements, file an issue or PR right here in the `grobtree` repository.

### Contact
- Maintainer: **Bernd Gronostay**
- GitHub: [@bgronostay](https://github.com/bgronostay)

GrobTree thrives on real-world feedback—let us know what workflows you want to optimise next.
