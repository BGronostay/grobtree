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
