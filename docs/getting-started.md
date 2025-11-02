# Getting Started with GrobTree

## Install the Plugin
1. Download the GrobTree plugin (ZIP) from the releases page.
2. In IntelliJ IDEA, open `Settings → Plugins → ⚙ → Install Plugin from Disk…`.
3. Restart the IDE to load the tool window (`View → Tool Windows → GrobTree`).

> GrobTree requires IntelliJ IDEA 2024.3+ (or any JetBrains IDE with the Platform module).

## Point GrobTree to a Configuration
Open `Settings → Tools → GrobTree` and choose one of the following sources:
- **Internal configuration** – built-in defaults, ideal for a quick tour.
- **External file** – your own `ConverterConfig.xml`.
- **JAR resource** – a packaged extension that bundles converters and icons.

Optional: enable *Override tool window title/icon* to pull branding info from the selected config.

## Import Logs
Inside the GrobTree tool window toolbar you can:
- Import from file (once-off or with follow/tail).
- Paste from the clipboard.
- Attach to a running IntelliJ run configuration (live or historical output).
- Tail an external file path.

Tabs are created on demand; you can rename, duplicate, clear, and persist them.

## Try the Demo Project
The public [`grobtree-testing`](https://github.com/bgronostay/grobtree-testing) repository ships with **cxf-example**, a Spring Boot + Apache CXF application wired for verbose logging:
```bash
git clone https://github.com/bgronostay/grobtree-testing.git
cd grobtree-testing/cxf-example
./mvnw spring-boot:run
```
Attach GrobTree to the run configuration (Main toolbar → “Open tabs for running processes and start evaluating”) and watch live request/response nodes populate in the tree.
