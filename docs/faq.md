# FAQ & Support

Answers to the questions we hear most often. If something is missing, open an issue or pull request—we love improving the documentation.

## General

**Which IDE versions are supported?**  
GrobTree targets IntelliJ IDEA 2024.3 and newer (or any JetBrains IDE built on that platform release). Older IDEs will refuse to load the plugin.

**Where do I download the plugin?**  
I want to share it at JetBrains Marketplace. Until then, grab the ZIP from the [latest release](https://github.com/bgronostay/grobtree-intellij-idea-plugin/releases/latest). Install via *Settings → Plugins → ⚙ → Install Plugin from Disk…*.

## Using GrobTree

**I installed the plugin but the tool window is empty.**  
GrobTree lazy-loads its UI. Create a new tab or attach to a running configuration and the full toolbar/tree will appear.

**How do I attach to a live process?**  
Open the tool window and use the **Attach** button (plug icon) or click **Open tabs for running processes and start evaluating** to let GrobTree attach automatically to every configuration momentarily running/being debugged.

**Can I tail a log file on disk?**  
Yes. Choose the tail icon (with the “add any” glyph) from the main toolbar, pick the file, and GrobTree will stream new lines into the current tab.

**How do I compare request and response pairs?**  
Converters can mark nodes as “corresponding”. Use the previous/next occurrence buttons to jump through the series; linked nodes render in bold with matching icons.

## Configuration & Extensions

**Where do I start with `ConverterConfig.xml`?**  
Review the bundled configuration (inside the plugin ZIP) plus the [ConverterConfig reference](./converter-config.md). Clone the [example extension](https://github.com/bgronostay/grobtree-example-extension) to see a minimal custom setup.

**Do I need a factory class?**  
Only if you provide multiple custom classes that should be created through shared logic. Otherwise, reference fully qualified class names directly in the configuration.

**Can I ship icons with my configuration?**  
Yes. When loading from a JAR, list icon paths in the `Icons` section. GrobTree adds them to its class loader (if the “Use classes and resources of JAR file” checkbox is enabled).

## Troubleshooting

**Logs import but nothing appears in the tree.**  
Check that your regex splits lines correctly. Enable the raw output tab to confirm GrobTree is reading lines, then tweak the default regex or switch to single-line mode.

**My custom listener fails to load.**  
Look at the IDE Event Log for stack traces. Ensure the class is on the classpath (via configuration JAR or IntelliJ module) and that the fully qualified name is spelled correctly. When using factories, confirm the `factoryUniqueName` matches.

**The tool window title/icon didn’t change.**  
They are only loaded at the start of IntelliJ. If you make changes afterward, you have to restart IntelliJ. Verify that the configuration contains `pluginName` / `pluginIconPath` and that *Override tool window title/icon* is enabled in **Advanced** settings. Reload the configuration afterward.

**I get “Config version mismatch”.**  
Update your `config-version` attribute to the value expected by the plugin. The most recent schema is documented in the [ConverterConfig reference](./converter-config.md); upgrading often just means copying the template header.

## Getting Help

- Search or open issues on the [plugin repository](https://github.com/bgronostay/grobtree/issues).
- Improve the docs directly with a pull request to the `grobtree` repository.
- Reach me on GitHub: [@bgronostay](https://github.com/bgronostay).

Let me know what worked, what didn’t, and which log formats you want GrobTree to understand next.
