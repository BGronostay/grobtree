# GrobTree Toolbar Buttons

GrobTree exposes two stacked toolbars inside the IntelliJ tool window. The **primary toolbar** (top strip) hosts quick-start actions, and the **main toolbar** carries the controls you use while exploring logs. Every button is listed below with its IntelliJ icon (served from [intellij-icons.jetbrains.design](https://intellij-icons.jetbrains.design)) and a short description of what it does.

## Primary Toolbar (No Tab Open)

| Icon | Purpose |
| --- | --- |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/runAll.svg" width="20" alt="RunAll"> | Scan every open project for running configurations, open GrobTree tabs for them, and start evaluating their live output. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/openNewTab.svg" width="20" alt="OpenNewTab"> | Create an empty GrobTree tab so you can import or attach logs manually. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/general/information.svg" width="20" alt="Information"> | Show the “About GrobTree” panel with version details, links, and diagnostics. |

## Main Toolbar (Log Exploration)

| Icon | Purpose |
| --- | --- |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/toolbarDecorator/import.svg" width="20" alt="Import"> | Open the import dialog to load logs from disk, clipboard, or a custom provider. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/toolbarDecorator/import.svg" width="20" alt="Import"> | Re-run the last import with the previously chosen source and options. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/debugger/attachToProcess.svg" width="20" alt="Attach"> | Attach the current tab to a chosen IntelliJ run configuration and stream its output live. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/expui/fileTypes/addAny.svg" width="20" alt="AddAny"> | Tail an external file and push new lines directly into the active GrobTree tab. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/debugger/threadRunning.svg" width="20" alt="ThreadRunning"> | Toggle automatic evaluation for newly started run configurations (live attach on/off). |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/menu-saveall.svg" width="20" alt="MenuSaveAll"> | Persist the buffer of the current tree (including processed entries) to a file. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/general/layoutEditorOnly.svg" width="20" alt="LayoutEditorOnly"> | Open the buffered tree content in a regular editor tab for diffing or inspection. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/refresh.svg" width="20" alt="Refresh"> | Rebuild the tree from a previously saved buffer (useful after reloading a configuration). |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/gc.svg" width="20" alt="GC"> | Split button that exposes clearing commands. Default click clears the active tree. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/expandall.svg" width="20" alt="ExpandAll"> | Expand every node in the current tree. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/collapseall.svg" width="20" alt="CollapseAll"> | Collapse the entire tree to top-level nodes. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/previousOccurence.svg" width="20" alt="Previous"> | Jump to the previous corresponding node (paired requests/responses, etc.). |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/nextOccurence.svg" width="20" alt="Next"> | Jump to the next corresponding node. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/find.svg" width="20" alt="Find"> | Open the search box scoped to the current GrobTree tab. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/selectall.svg" width="20" alt="SelectAll"> | Remove active filters so every processed entry is displayed again. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/general/projectTab.svg" width="20" alt="ProjectTab"> | Split button for opening the raw output tab. Offers XML, JSON, and plain text variants. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/highlighting.svg" width="20" alt="Highlighting"> | Rename the current GrobTree tab. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/openNewTab.svg" width="20" alt="OpenNewTab"> | Quickly create a new tab from the main toolbar. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/expui/general/settings.svg" width="20" alt="Settings"> | Edit tab-specific settings such as regex selection, display options, and listeners. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/general/information.svg" width="20" alt="Information"> | Open the information dialog for the active tab (configuration metadata, diagnostics). |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/ide/notification/ideUpdate.svg" width="20" alt="IdeUpdate"> | Reapply the configuration defaults to the current tab when GrobTree detects changes. |

### Clear Tree Split Button

| Icon | Purpose |
| --- | --- |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/gc.svg" width="20" alt="GC"> | Remove all entries from the active tree while keeping attachments intact. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/debugger/attachToProcess.svg" width="20" alt="AttachToProcess"> | Clear every tree that is currently attached to a running process. |

### Show Output Split Button

| Icon | Purpose |
| --- | --- |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/general/projectTab.svg" width="20" alt="ProjectTab"> | Open the original raw output in a side tab without changing its formatting. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/expui/fileTypes/xml.svg" width="20" alt="XML"> | Render the raw output with XML syntax highlighting. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/expui/fileTypes/json.svg" width="20" alt="JSON"> | Render the raw output with JSON syntax highlighting. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/expui/fileTypes/text.svg" width="20" alt="Text"> | Render the raw output as plain text (no syntax highlighting). |

### Find Toolbar (Inside the Search Strip)

| Icon | Purpose |
| --- | --- |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/search.svg" width="20" alt="Search"> | Focus the search field and apply the query to the current tree. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/matchCase.svg" width="20" alt="MatchCase"> | Toggle case-sensitive search. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/previousOccurence.svg" width="20" alt="PreviousOccurence"> | Move to the previous search match. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/nextOccurence.svg" width="20" alt="NextOccurence"> | Move to the next search match. |

### Tree Context Menu Highlights

These actions live in the tree context menu but are worth knowing when documenting buttons that appear with icons elsewhere.

| Icon | Purpose |
| --- | --- |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/copy.svg" width="20" alt="Copy"> | Copy the selected node’s caption or value to the clipboard. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/menu-saveall.svg" width="20" alt="MenuSaveAll"> | Save the value of the selected node to disk. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/collapseall.svg" width="20" alt="CollapseAll"> | Collapse the selected set of top-level nodes into a synthetic group. |
| <img src="https://intellij-icons.jetbrains.design/icons/AllIcons/actions/diff.svg" width="20" alt="Diff"> | Compare nodes inside the current tab, project, or across projects. |
