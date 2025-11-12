# ConverterConfig.xml Overview

`ConverterConfig.xml` is the central definition that tells GrobTree how to interpret raw log streams, which UI presets to expose, and how the IntelliJ tool window should present information. Every configuration you load—internal sample, external file, or JAR resource—follows the same structure. This guide explains each major section so you can design or review a configuration without inspecting the schema in detail.

---

## Root Metadata
- **config-version** keeps the file aligned with the parser version GrobTree expects. Use the newest templates for ConverterConfig, which demand the current value.
- **api-version** records which public GrobTree API level your custom extensions target. Also be sure to use the latest version of GrobTree API.
- **name** and **version** appear in the UI, letting users choose between multiple configurations or see which revision is active.
- **description** gives context to reviewers (for example, which service the configuration is tuned for).
- **pluginName** and **pluginIconPath** allow branding the IntelliJ tool window. They only take effect when “Override with config if available” is enabled in the advanced settings dialog.

---

## LogProviders
Log providers describe how GrobTree can obtain log lines. You may only use the provided ways of getting logs (importing log-files, Configuration logging, file tailing), but you have the ability to write your own. When a user opens the import dialog, these options populate the list. Behind every provider you reference a `LogProviderListener` implementation that performs the actual reading.

---

## Transformations
Transformations are lightweight preprocessing rules. They run on every line before parsing and are ideal for normalising whitespace, truncating verbose prefixes, or masking sensitive fragments. Think of them as sequential “find and replace” steps with independent toggles for imported logs versus live processing. Keep them focused and fast—the goal is to clean up data, not reimplement parsing logic.

---

## Factory (Optional)
Some configurations share infrastructure objects—custom processing listeners, icon resolvers, or statistics collectors. Declaring a factory lets GrobTree ask a single class to construct these objects on demand. Use it when you have more than one custom component and want to centralise creation logic (including dependency injection, configuration parsing, or caching). If you only load a couple of standalone classes, skip the factory and reference them directly.

---

## RegEx Definitions
Regular expressions determine how GrobTree segments the log stream and which fields become parameters. Think of each entry in the `RegExs` section as a named parsing preset:
- Give the regex a human-friendly name and an optional ID so other parts of the configuration can refer to it.
- Define how timestamps should be produced—either by parsing a single named group or by assembling multiple components such as year, month, and offset.
- List the groups you want to use as parameters.

Keep regexes narrowly focused on structure. Presentation and highlighting happen later in the evaluation configuration.

---

## RunConfigs
Run configuration bindings bridge IntelliJ run/debug configurations with GrobTree presets. When a developer launches a specific run configuration, GrobTree can preselect an evaluation profile and regex, sparing them from manual adjustments. Use this for projects with multiple services or environments where each run has a known log format.

---

## EvaluationConfigs
Evaluation configurations are the heart of the file. Each one represents a selectable way to render the parsed logs. Users switch between them via the dropdown in the tool window. An evaluation configuration answers several questions:
- Which regex (or single-line mode) should be active by default?
- Which captured parameters should appear in captions, live progress, or statistics?
- How should the caption be composed when no custom logic overrides it?
- Which processing listeners should run, in what order, and with which settings?
- What supplementary nodes, icons, or colour rules should be applied to emphasise important values?

### ConfigurableProcessingListener (detailed guide)
`ConfigurableProcessingListener` is the built-in way to convert parsed log entries into tree nodes without writing Java. It lives inside `<ProcessingListeners>` and can appear alongside other listener types. The listener consumes incoming log entries one by one and decides, based solely on the XML you provide, whether to create top-level nodes, which caption to show, which icon to use, and which sub nodes to attach.

#### High-level flow
1. Each listener instance declares global attributes plus one or more `<ConfigurableEntry>` blocks.
2. For every log line, the listener evaluates the entries in document order. The first entry whose pattern and conditions match controls what happens next.
3. When an entry matches, the listener renders a caption from its `ExString`, creates a top-level node with that caption, records the original log text as the node’s value, applies optional icons or correspondences, and finally builds any declared sub nodes.
4. Depending on `returnTrueIfFound` (listener level) and `always` (entry level), processing either stops immediately or continues with later entries and/or other listeners.

#### Listener-level attributes
- `enabled`: Determines whether the listener is available when the configuration loads. Users can toggle it in the UI, but your XML sets the default state.
- `name` and `description`: Human-readable labels shown in configuration dialogs. Use them to describe what the listener extracts (“HTTP requests”, “Payment pipeline”, etc.).
- `returnTrueIfFound` (default `true`): Controls whether the overall processing chain stops once this listener creates at least one node for the current log line. Keep it `true` when the listener “owns” a given log format; set it to `false` if subsequent listeners should also see the entry even after this one has produced nodes.

#### ConfigurableEntry structure
Each `<ConfigurableEntry>` represents one rule. You can add as many as needed; they are checked in order.

- **Pattern** (optional):
  - Holds a Java-style regular expression. Use named capture groups (`(?<GroupName>...)`) to extract values. Any value captured here can be referenced later via `{GroupName}` placeholders.
  - The `flags` attribute accepts the numeric bitmask defined by the regular-expression engine (for example, decimal `2` for case-insensitive matching). Omit it or set it to `0` for plain matching.
  - `useStartPos` (default `true`) determines where matching begins. When `true`, the search starts immediately after GrobTree’s primary regex finished parsing the entry (so timestamps or log prefixes are skipped). Set it to `false` to evaluate the entire raw log line from the very first character.
  - Patterns are optional. If you only need to display already-parsed parameters, omit `<Pattern>` and rely on `ExString` placeholders.

- **Execution control**:
  - `always` (default `false`) decides whether this entry runs even if a previous entry already matched. Leave it `false` for mutually exclusive patterns; set it to `true` for supplemental actions such as “also attach payload details when the header matched earlier”.
  - Entries inherit the listener’s `returnTrueIfFound` behaviour, so if that flag short-circuits the chain you may need to rearrange entries or duplicate the listener when different outcomes are required.

- **Caption templating (`ExString`)**:
  - `ExString` is required for node creation. It functions as a template: literal characters are printed as-is, and `{Placeholder}` segments are replaced with values.
  - Placeholders resolve against a merged value map containing (a) all named groups captured by the entry’s pattern and (b) every parameter produced by the evaluation’s active regex (for example, `Level`, `Thread`, `Timestamp`). If multiple values share the same name, the entry-specific group wins.
  - `ExString` supports multiple segments. Use several `ExString` child nodes to produce differently styled chunks (icons, colors) if desired.

- **Icons and node correlation**:
  - The optional `icon` attribute points to any icon declared under `<Icons>` or to IntelliJ’s built-in icon IDs. When set, the resulting top node shows that icon in the tree.
  - `<EqualityStringCorrespondingNodeComparer>` lets GrobTree find related nodes (for instance, pairing “request” and “response” entries). Fill in:
    - `UniqueId`: A stable identifier shared by all nodes that should participate in the same comparison pool.
    - `ItemId`: A per-node identifier (such as a correlation ID) used to find matches.
    - `ShowOnlyNextNodes`: Keep `true` to search forward only, or `false` to allow backward matches.
    - `MightHaveBeforeNode` / `MightHaveAfterNode`: Set these according to whether predecessors/successors are expected. They guide the UI to highlight missing partners politely.

- **Sub nodes**:
  - `<SubNodes>` can contain one or more `<KeyValueSubNode>` or other supported node definitions. Each sub node reads from the same merged value map as the caption, so both evaluation-level parameters and entry-specific named groups are available.
  - Sub nodes execute immediately after the top node is created. They are ideal for showing headers, payload fields, or metadata that does not belong in the caption itself.

#### Value resolution and placeholder strategy
- The listener always starts with the parameters extracted by the active `RegEx` definition (fields like `Level`, `Thread`, `Payload`, etc.). Think of this as the “base map”.
- When an entry’s pattern matches, any named groups you defined there are layered on top of that base map. The newer values override keys with the same name.
- `ExString` placeholders read from this merged map. If a placeholder is referenced but no value exists, it simply vanishes from the caption, so design your templates accordingly.
- Sub nodes consume the same merged value map, so any placeholder-friendly name you introduce in a pattern is automatically available for child nodes as well.

#### Putting it into practice
1. **Start specific, end generic**: Order entries roughly from most targeted to most permissive. That way, only one entry typically fires and the `always` attribute can be reserved for special cases.
2. **Treat `returnTrueIfFound` as a boundary**: Use `true` when the listener represents a final decision about the log entry. Switch to `false` when this listener is merely annotating the entry and other listeners should still run.
3. **Leverage named groups generously**: Every value you want to reuse in captions should have a meaningful name. Avoid capturing data you do not intend to display—it slows down matching and clutter placeholders.
4. **Use icons and comparers for orientation**: Consistent icons help readers skim the tree. Corresponding node comparers prevent “orphan” response nodes by automatically highlighting unmatched items.

Following these guidelines, `ConfigurableProcessingListener` can express most node-creation logic directly in XML, keeping your configuration self-contained and understandable even for teammates who only interact with the configuration file.

---

## Parameters
Parameters are scoped to evaluation configurations (either the selectable entry itself or the `CommonConfig` that feeds into each one). Use them to tune how GrobTree presents nodes for a specific preset: whether the preferred sub-node is shown automatically, if duplicate lines should be suppressed, how styling behaves, and whether live input remains buffered for rebuilds. Each evaluation can inherit the shared values from `CommonConfig` and override only the items that need special treatment.

---

## Variables and Icons
Variables are named string constants. They simplify maintenance by letting you define a value once (such as a reusable icon path or caption fragment) and reference it throughout the file with `{VariableName}` placeholders.

Icons enumerate the custom artwork packaged with the configuration. When you load from a JAR, point each icon to the resource path inside the archive. Once declared, icon names can be used anywhere the schema accepts an icon reference—log providers, display rules, processing listeners, and so on.

---

## Custom Class Instantiation
Many sections allow you to plug in Java classes—log provider listeners, processing listeners, post-creation hooks. GrobTree offers two strategies:
- **Factory-based** creation, where you mark `useFactory` and supply a unique identifier. The factory decides how to construct and cache the instance.
- **Direct** creation, where you provide a fully qualified class name, optional singleton behaviour, and optional constructor parameters (a string value and/or the current local context).

Choose the approach that fits your packaging model. Factory-based creation is convenient when the same configuration deploys multiple custom pieces that share resources.

---

## Putting It Together
When authoring a configuration, work from parsing to presentation:
1. Define the log providers and transformations so GrobTree can ingest clean data.
2. Add regex definitions that capture every field you care about, including timestamps.
3. Create evaluation configurations that turn those fields into captions, child nodes, colours, and statistics, wiring in processing listeners where custom logic is required.
4. Bind run configurations for fast project-specific onboarding.
5. Finish with global parameters, variables, and icons to polish the user experience.

The IntelliJ settings dialog (main and advanced tabs) controls which configuration is loaded and how aggressively GrobTree refreshes it. Use the “Force Reload” button after editing the XML to verify changes immediately. With a well-structured `ConverterConfig.xml`, teams can tailor GrobTree to any log format while keeping the UI predictable and informative.
