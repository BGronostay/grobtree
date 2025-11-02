# IntelliJ Settings for GrobTree

GrobTree’s behaviour inside IntelliJ IDEA is driven by a single application-level settings group split into a main page (`Settings → Tools → GrobTree`) and an Advanced page (`Settings → Tools → GrobTree Advanced`). This guide explains every option, why it exists, and when you should change it—no source digging required.

## Main Settings: Configuration Source

### Optional JAR File
- **JAR path** – Points to a packaged bundle that contains configuration XML, icons, or extension classes. Use the browse button to avoid typos.
- **Use classes and resources of JAR file** – When enabled, GrobTree adds the selected JAR to its class loader. Keep it checked if your configuration references custom listener classes or icons that live inside the JAR. You can still point to a JAR for configuration-only use; disabling the checkbox falls back to GrobTree’s internal class loader.
- **Name of configuration file** – Only relevant when you later choose “Configuration file inside JAR resources”. Enter the path to the XML inside the archive (defaults to `ConverterConfig.xml`; include folders such as `configs/ConverterConfig.xml` if needed).

> When you select a JAR through the file chooser, the checkbox is automatically enabled to make sure the resources are found.

### Configuration Origin
Pick where GrobTree reads `ConverterConfig.xml` from:

| Option | Description | Typical Use |
| --- | --- | --- |
| **Internal example configuration resource file** | Loads the bundled showcase XML shipped with the plugin. | Quick tours, sanity-checking a new install. |
| **Configuration file inside JAR resources** | Reads `jarConfigurationFileName` from the selected JAR. The default name is `ConverterConfig.xml`. | Shipping a ready-made configuration with your team’s JAR or when you maintain configuration + processors together. |
| **External configuration file** | Points directly to an XML file on disk. | Local development of a custom configuration or ad-hoc experiments. |

If you enter a JAR path but stay on “External configuration file”, GrobTree still uses the JAR for classes and icons as long as the checkbox is ticked.

When “External configuration file” is selected, the browse field underneath the radio buttons must point to the XML on disk. GrobTree persists the absolute path, so remember to update it if you move the file.

### Patch Configuration Support
- **Use patch configuration file** – Enables delta-merging a second XML file on top of the base configuration. GrobTree applies the patch after loading the base file, so you can ship narrow tweaks (e.g., new colours or transformed captions) without forking the main file.
- **Patch configuration path** – Browse to the patch XML. The field is enabled only for XML-backed origins (internal resource, JAR resource, or external file). Disable the checkbox to revert to the untouched base configuration.

### Force Reload Button
`Force Reload` bumps the internal configuration revision so the next apply immediately reparses everything, even if file paths and timestamps have not changed. Use it right after rebuilding a JAR in place or editing an XML that keeps the same name.

## Advanced Settings
Open `Settings → Tools → GrobTree Advanced` for fine-grained behaviour tweaks.

| Setting | Effect                                                                                                                                                                                                          | When to change |
| --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| --- |
| **Override With Config If Available** | If the loaded configuration exposes `pluginName`/`pluginIconPath`, GrobTree renames the tool window stripe and swaps its icon.                                                                                  | Branding the tool window for a specific project or client. |
| **Always reload configuration** | Skips caching and reparses the configuration on every access. Guarantees fresh data but costs extra I/O.                                                                                                        | Editing XML by hand and testing frequently. Turn it off in stable environments to speed up startup. |
| **Always show update tab settings button** | Keeps the “Update and Overwrite with Defaults” toolbar action visible even when nothing changed.                                                                                                                | Training sessions or scripted demos where you need to highlight the button’s purpose. |
| **Hide not enabled buttons** | Suppresses toolbar actions when GrobTree disables them. When unchecked, disabled buttons remain visible but greyed out.                                                                                         | Minimalist UI preferences or shared screenshots where inactive buttons cause confusion. |
| **Default selectable RegEx id** | Preselects a named regular-expression preset when multiple options exist in the configuration. Leave blank to accept whatever the XML marks as default.                                                         | Streamlining onboarding when teams always pick the same splitter. |
| **Default selectable config id** | Preselects a specific evaluation profile among the configuration’s selectable configs.                                                                                                                          | Useful when you add new presets but want a stable default for most users. |
| **Special color** | Overrides the named colour GrobTree uses for emphasis in certain captions. Accepts any JB colour id (e.g., `JB.JBColor.RED` or `FC.DEFAULT_CONSTANT`. Falls back to magenta if the name is unknown. | Harmonising GrobTree’s highlight colour with project branding. |

Changes on the Advanced page are applied immediately after pressing **Apply** and force GrobTree to rebuild its internal configuration cache, so the next log import reflects your new defaults.

## Lifecycle Notes
- Settings are stored per-IDE instance in `GrobTreePlugin.xml`, so the same choices apply across all projects until you change them.
- If a configuration fails to load, GrobTree falls back to a minimal internal preset and surfaces a notification. Check the event log for root causes such as missing files or invalid XML.
- The `Always reload` toggle is handy while iterating, but on large configurations it can add noticeable overhead when combined with frequent log tails.

With these options tuned, GrobTree can load your configuration from any combination of disk and packaged resources, refresh on demand, and present the UI exactly the way your team expects.
