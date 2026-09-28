# SmartCluster User Guide

[Home](../README.md) · [繁體中文](USER_GUIDE.zh-TW.md)

Document revision: September 28, 2026. Applies to the 0.11.0.dev3 development preview candidate. [Support and known issues](RELEASE_NOTES.en.md)

## Choose your first goal

| Goal | Prerequisites | What success looks like |
|---|---|---|
| Try one Windows computer | Trusted candidate package from the maintainer; no AI account needed | Diagnostic completed with the expected result |
| Connect another computer | Compatible builds, reachable Hub IPv4, short-lived invitation | Enrollment followed by a cross-computer diagnostic |
| Work from chat | AI client supporting local stdio MCP | Actual tool calls and a final task result |
| Use a remote AI | Selected provider installed, signed in, and enabled on the target | A completed AI task, not diagnostic.echo |
| Send work to an App conversation | Connected receiver, sender/project permissions, active intake | The App claims the job and reports completion |

A **Hub** hosts a group and stores coordination state. A **Node** participates in work. A **profile** is a computer's local group configuration. `profile_id`, `cluster_id`, and `node_id` are different identifiers.

## 1. Get and launch the candidate

Public downloads are not available yet. If the maintainer has supplied a candidate, verify its source, version, and SHA256SUMS, then extract SmartCluster.exe to a stable folder. The executable packages the product's Python runtime; clean-machine acceptance is still pending.

```powershell
Get-FileHash .\SmartCluster.exe -Algorithm SHA256
```

Double-click the executable to open **My groups** in your browser. Keep the launcher window open; Ctrl+C in that window stops the group management page server. This server and group background services are separate. Closing a browser tab does not stop a group. If system protection blocks the candidate, verify its source with your IT team or the maintainer rather than disabling protection.

## 2. Create your first group

1. Enter an English group name, such as **Work Group**.
2. Leave LAN/VPN IPv4 empty for a local-only trial. To invite other computers, enter this computer's reachable IPv4 address. The preview has no graphical gateway-address editor; retain existing data and create a suitable test group if a different address is needed.
3. Click **Start service**, then **Accept work here**. The intake label does not establish service health or AI readiness.
4. Click **Send diagnostic demo**, then **Open console** to find `SmartCluster connection demo`.
5. Confirm `completed` and the result `Hello from SmartCluster`. This is a **no-AI connectivity diagnostic**.

The web interface supports English and Traditional Chinese. Try **Personal Group** for a second group. Each group has separate state and port settings.

## 3. Invite and join

The host starts its Hub with a LAN/VPN address, then creates a short-lived invitation for the intended computer in the console's onboarding flow. Send `invitation.json` privately. The recipient verifies the group name, Hub URL, and CA fingerprint. Use the actual port in that URL, not a port copied from another group.

On the joining computer, select the join-group form, enter **this computer's name**, such as **Windows Test Node**, and choose the invitation file. After enrollment, start the service, enable intake for that group, and complete a diagnostic. Both sides must support the 0.11 intake protocol. A standalone macOS executable is not currently part of the public deliverable.

Joining does not grant access to projects, files, AI accounts, or App receivers. Each computer's user controls its local permissions. If enrollment is interrupted, resume the existing incomplete enrollment first instead of creating duplicate identities.

dev3 preserves the configured English group name in invitations; this was checked against the rebuilt executable on the build host. Older dev2 binaries may still use the default Chinese label. See [version history](RELEASE_NOTES.en.md). Do not use a display name alone as evidence of trust; verify the host and fingerprint.

## 4. Manage groups

| Action | Effect |
|---|---|
| View | Selects the group shown in the UI; does not reroute tasks or change intake |
| Accept work here | One group per registry accepts new work; switching waits for existing work or reconciliation |
| Pause intake | Stops new intake while leaving the Hub running |
| Stop service | Stops this group's local service; stopping its Hub disconnects other members |

If a switch is waiting, inspect the original work, then continue or cancel the switch. Do not erase journals or blindly resubmit work that may already have run. The one-group intake rule applies within the same registry; existing independent installations are not automatically managed by it.

## 5. Connect MCP

Complete the basic diagnostic first. Find the local profile_id using View or `groups --list`, then configure a local stdio MCP server in your AI client. The following is a common JSON layout; the outer configuration depends on your client. Replace the example paths and profile identifier.

```json
{
  "mcpServers": {
    "smartcluster-work": {
      "command": "C:\\Apps\\SmartCluster\\SmartCluster.exe",
      "args": ["--profiles-dir", "C:\\SmartClusterData", "--profile", "REPLACE_WITH_PROFILE_UUID", "mcp"]
    }
  }
}
```

`C:\SmartClusterData` is only an example. Use the same root used to create or join the group. The default is `.smartcluster-groups` in your user home directory. Reload the tools and ask the AI to call `cluster_service_status` and `cluster_list_nodes` to verify the connection.

MCP stays bound to that profile; changing the UI selection or active intake group does not reroute it. A chat service supporting only remote HTTP MCP cannot use this local stdio entry point directly. Pasting a command into chat does not configure MCP.

## 6. Complete work from a conversation

| Goal | Example request | Evidence to check |
|---|---|---|
| Inspect nodes | List this group's nodes and AI provider status. | Names, online state, and target ID |
| Test connectivity | Send a no-AI diagnostic to Windows Test Node and follow it to completion. | diagnostic.echo completed with matching output |
| Get AI analysis | Ask the enabled Claude CLI on Demo Mac to review this text. | agent.analyze, provider, result, and task ID |
| Send an App job | List connected receivers, then send the work to the project conversation I select. | Actual App intake; track with cluster_app_job |
| Start locally | Check the local SmartCluster service and start the existing service if needed. | cluster_service_status / cluster_service_start |

Use `cluster_get_task` for ordinary tasks. A `cluster_cancel_task` request still requires checking the final state. App jobs have separate tracking/cancellation tools; cancellation does not undo changes already made. Group creation and switching currently use the UI. MCP does not provide unrestricted operating-system control.

## 7. Data and maintenance

Group state defaults to `.smartcluster-groups`. Deleting the EXE does not remove it, and legacy `.state` installations are not automatically imported. Depending on the feature, task inputs, results, events, and metadata are transmitted to targets or stored by the Hub/Node. Full App conversation history stays on its original computer. AI analysis sends submitted content to the selected node and AI service.

Cross-computer traffic uses mTLS for node authentication and transport encryption. This is not disk encryption or protection against executable reverse engineering. Keep invitations, login URLs, private keys, tokens, and state directories private.

Before backup or replacement, pause intake, finish or reconcile work, stop the related services, and back up the entire data root including SQLite sidecar files. Keep the old executable and a consistent backup. There is no automatic update/rollback UI, and downgrade compatibility is not guaranteed. Schedule downtime with members before stopping a Hub. [Troubleshooting](FAQ.en.md) · [WAN](WAN.en.md)
