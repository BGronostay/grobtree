# Replay Apache CXF Requests

GrobTree can turn Apache CXF request log entries into runnable HTTP requests directly from the tree context menu.

## What You Get

- **Create CURL Command**: builds a `curl` command from the selected CXF request and copies it to your clipboard.
- **Replay In HTTP Client**: opens an IntelliJ HTTP Client request file (`GrobTree-Replay.http`) from the selected CXF request.

Both actions are available from the right-click menu in the log tree.

## When These Actions Appear

The actions are shown only when the selected top-level node is:

- produced by the built-in Apache CXF processing listener, and
- a replayable request entry (not every node is replayable).

If GrobTree cannot extract a valid request from the selected entry, it shows:
`No replayable request found in current selection.`

## 60-Second Walkthrough (Using Sample Logs)

1. Import [`cxf-example.log`](../examples/logs/cxf-example.log) into a new GrobTree tab.
2. Select a CXF request node in the tree.
3. Right-click and choose **Create CURL Command**.
4. Paste into a terminal to run or adjust the generated command.
5. Right-click the same node and choose **Replay In HTTP Client**.
6. IntelliJ opens `GrobTree-Replay.http`; run it in the built-in HTTP Client.

## Why This Is Useful

- Reproduce customer issues without manually rebuilding requests.
- Share deterministic request repro steps with teammates.
- Iterate quickly by editing headers/payloads in the generated `.http` file.

## Troubleshooting

**I do not see the actions**
- Select a CXF request top node (not an arbitrary child node).
- Ensure the active evaluation config uses the Apache CXF listener.
- Test first with the bundled `cxf-example.log` to confirm setup.

**The action is visible but replay fails**
- Check whether the log entry contains a usable address/method.
- Inspect or edit headers/body before replaying (especially auth headers).
