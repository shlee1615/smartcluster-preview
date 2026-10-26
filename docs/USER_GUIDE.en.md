# SmartCluster User Guide

[Home](../README.md) · [繁體中文](USER_GUIDE.zh-TW.md)

Document revision: 2026-10-26. Applies to the 0.14.0.dev5 Windows x64 invite-only trial. [Support and known issues](RELEASE_NOTES.en.md)


## Preview 2 capability boundary

This package provides management/dispatch and supported local Node functions. It does not include AI clients or model subscriptions. Gemini CLI, Gemini App MCP/sidecar installation and isolated development currently require a configured development deployment; this frozen Node does not execute isolated file editing/tests. The Hub can dispatch to capable, accepted and authorized execution nodes, but that does not make those capabilities local to this package. The CTE-Codex application and configuration are deployed separately and are not in this ZIP.

This is an invite-only candidate. Check the [acceptance record](RELEASE_NOTES.en.md); earlier smoke tests do not replace clean-account or new cross-machine acceptance. Open `guide/preview2/index.html` for the offline introduction. Its interactive workflow submits no real task.

## Choose your goal first

| Goal | What you need | What success looks like |
|---|---|---|
| Try one Windows computer | The trial ZIP and its SHA-256 from your inviter; no AI account needed | Diagnostic task completed with the matching result |
| Invite another computer | Same version, a reachable Hub IPv4, a short-lived invitation | The member joins and completes a cross-computer diagnostic |
| Dispatch work from chat | An AI client that supports local stdio MCP (Codex App/CLI, Claude Desktop/Code) | You see actual tool calls and the final task result |
| Use a remote AI | The selected provider installed, signed in, and enabled on the target computer | A real AI task completes; not diagnostic.echo |
| Send work to a specific App conversation | A connected receiver, sender and project permissions, intake activity | The App actually claims the job and reports completion |

A **Hub** hosts a group and stores collaboration state; a **Node** is a computer that participates in work; a **profile** is the group configuration stored on this computer. `profile_id`, `cluster_id`, and `node_id` are different identifiers.

## 1. Obtain, verify, and install

1. Obtain `SmartCluster-0.14.0.dev5-windows-x64-preview.zip` and its SHA-256 from your inviter.
2. Verify it:

   ```powershell
   Get-FileHash .\SmartCluster-0.14.0.dev5-windows-x64-preview.zip -Algorithm SHA256
   ```

   If the hash does not match, do not extract; check with your inviter.
3. Extract the **entire ZIP** to a fixed folder, such as `C:\Apps\SmartCluster-0.14.0.dev5`. After extraction you should have `SmartCluster\SmartCluster.exe`, `SmartCluster\SmartCluster-background.exe`, `SmartCluster\_internal\`, `README.md`, `guide\`, `notices\`, and `SHA256SUMS.txt`. `SHA256SUMS.txt` lists the hash of every file in the package; use it to check that the extraction is complete.
4. **Do not** copy `SmartCluster.exe` on its own to another location: it needs the `_internal` folder beside it. If you move it later, move the whole `SmartCluster` folder and set up autostart and MCP again (see sections 8 and 9).

This build is **unsigned**. Windows may show a SmartScreen prompt on first launch; continue only after the hash has matched. On company-managed devices, let IT decide; do not disable antivirus or SmartScreen. See the [FAQ](FAQ.en.md).

## 2. Launch

Double-click `SmartCluster\SmartCluster.exe`. A console window appears and your browser opens **My groups**. **Keep this window open**: it serves the group management page; to shut down the management page server, press Ctrl+C in that window. Each group's background service is separate from it: closing the browser tab or the management page does not stop a group that has been started.

`SmartCluster-background.exe` is a windowless variant of the same program, used only for start automatically at sign-in; double-clicking it does nothing.

The web interface can be switched between Traditional Chinese and English.

## 3. Create your first group

1. Under **Create group**, enter an English name, such as **Work Group**.
2. For a local-only trial, leave LAN/VPN IPv4 empty. To invite other computers, enter this computer's actually reachable IPv4. There is currently no graphical interface for editing the gateway address afterwards; if you need a different address, keep the original group and create a suitable new group.
3. Click **Start service**, then **Accept work here**. The intake label does not establish service health or AI availability.
4. Click **Send diagnostic demo**, then open the console to find `SmartCluster connection demo`.
5. Confirm that the status is `completed` and the result is `Hello from SmartCluster`. This is a **no-AI connectivity diagnostic**.

Each group has its own data and port settings; use **Personal Group** to create another group.

## 4. Invite and join

The group owner first starts a Hub configured with a LAN/VPN address, then creates a short-lived invitation for a specific computer in the console's join wizard. The generated archive contains `invitation.json` and `READ-ME.txt`. Deliver it privately to the member, who verifies the group name, Hub URL, and CA fingerprint. The actual port is the one in the invitation URL.

The member opens **Join another group**, enters **this computer's name**, such as **Windows Test Node**, selects `invitation.json`, and joins. Then start the service, set it as the intake group, and complete a diagnostic. Both sides should run the **same version**; a macOS computer cannot join with this executable build (macOS is currently deployed from source; ask your inviter for the steps).

Joining does not automatically grant project, file, AI account, or App intake permissions. Each computer's user still controls local permissions. If joining is interrupted, use **Resume incomplete enrollment** first to avoid creating duplicate identities. Do not judge trust by name alone; still verify the group owner and certificate fingerprint.

## 5. Manage multiple groups

| Action | What it actually does |
|---|---|
| View | Changes the on-screen selection; does not change the dispatch destination or the intake group |
| Accept work here | Within one group registry directory, one group at a time takes new work; switching waits for the original work to finish or be reconciled |
| Pause intake | Stops accepting new work; the Hub keeps running |
| Stop service | Stops that group's local service; if this computer hosts the Hub, other members are disconnected |

While a switch is waiting, reconcile the original work; you can then **Continue switch** or cancel the switch. Do not delete journals or blindly resubmit work that may already have run. This rule applies within the same registry; existing independent installations are not automatically brought under its management.

## 6. Connect MCP

Complete the basic diagnostic first. Find this computer's `profile_id` under **View** or with `SmartCluster.exe groups --list`. The MCP command is always the **full path to the EXE**, with the arguments in this order: `--profiles-dir`, the data root, `--profile`, the profile_id, `mcp`. The default data root is `%USERPROFILE%\.smartcluster-groups`; the examples below use `C:\Users\you\.smartcluster-groups`; replace it with the real path and ID.

**Codex (App or CLI)**: add the following to the project's `.codex\config.toml` (or `%USERPROFILE%\.codex\config.toml`):

```toml
[mcp_servers.smartcluster]
command = "C:\\Apps\\SmartCluster-0.14.0.dev5\\SmartCluster\\SmartCluster.exe"
args = ["--profiles-dir", "C:\\Users\\you\\.smartcluster-groups", "--profile", "REPLACE_WITH_PROFILE_UUID", "mcp"]
```

When the join wizard finishes under **Join another group**, it can write this Codex configuration for that project on your behalf.

**Claude Desktop**: add the following under `mcpServers` in `%APPDATA%\Claude\claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "smartcluster-work": {
      "command": "C:\\Apps\\SmartCluster-0.14.0.dev5\\SmartCluster\\SmartCluster.exe",
      "args": ["--profiles-dir", "C:\\Users\\you\\.smartcluster-groups", "--profile", "REPLACE_WITH_PROFILE_UUID", "mcp"]
    }
  }
}
```

After changing the configuration, **quit the App completely and reopen it** (opening a new conversation alone does not load the new tools). After it reloads, first ask the AI to verify the connection with `cluster_service_status` and `cluster_list_nodes`.

MCP is bound to a fixed profile and does not follow the web **View** selection or intake-group switches. A chat service that supports only remote HTTP MCP cannot use this local stdio entry point directly. Pasting the command into a conversation does not configure MCP.

## 7. Complete work from a conversation

| Goal | Example request | How to verify |
|---|---|---|
| Inspect nodes | List the current group's nodes and AI provider status. | Check names, online state, and target ID |
| Connectivity diagnostic | Send a no-AI diagnostic to Windows Test Node and follow it to completion. | diagnostic.echo completed with the matching result |
| AI analysis | Ask the enabled Codex CLI on Demo Mac to review this text. | agent.analyze, provider, final result, and task ID |
| App job | List connected receivers, then send the work to the project conversation I specify. | Actual App intake; track with cluster_app_job |
| Start locally | Check the local SmartCluster service; start the existing service if it is not running. | cluster_service_status / cluster_service_start |

`cluster_get_task` tracks ordinary tasks; after requesting cancellation with `cluster_cancel_task`, still check the final state. App jobs are cancelled with their own tool; changes already made are not rolled back. Creating and switching groups still uses the UI, and MCP is not an entry point for arbitrary control of the operating system.

## 8. Start automatically at sign-in

Turn on **Start automatically at sign-in** on the group's settings page, or run:

```powershell
C:\Apps\SmartCluster-0.14.0.dev5\SmartCluster\SmartCluster.exe --profiles-dir "C:\Users\you\.smartcluster-groups" --profile REPLACE_WITH_PROFILE_UUID service autostart enable
```

This writes the **absolute path** of `SmartCluster-background.exe` to the current user's sign-in startup entries; after sign-in, the group starts in the background with no window. After moving the program folder or switching to a new version, turn it on again from the new location. Change `enable` to `disable` to turn it off.

## 9. Manual update (this build has no automatic update)

Under **Settings › Versions & updates** on the Hub, a node installed from the executable is shown as **Executable install: manual update**, and nothing is pushed to it. To update:

1. In the console, **Pause intake** for this computer's group and wait for work in progress to finish.
2. Quit any AI App that uses SmartCluster MCP, stop the services of all groups on this computer, and close the `SmartCluster.exe` window.
3. Back up `%USERPROFILE%\.smartcluster-groups` (the whole folder, including the SQLite files).
4. Verify the new ZIP's hash, then extract it to a **new** folder, such as `C:\Apps\SmartCluster-0.14.0.dev5`.
5. If you want to leave the paths in the MCP configuration and autostart unchanged: rename the old program folder (for example, append `-old`), then rename the new folder to the original name. Otherwise, update the path in the MCP configuration and turn autostart on again.
6. Launch from the new version, confirm the version shown in **My groups** and that your groups and node identities are still there, then resume intake.
7. Delete the old program folder only after everything checks out. To roll back to the old version: stop the services, rename the folders back, and start again; **the new version may have upgraded the database format, so restore the backup from step 3 before rolling back**.

The Hub and members should run the same version; mixed versions have not been verified.

## 10. Removal

1. Pause intake and wait for work to finish; stop the services of all groups on this computer; close the `SmartCluster.exe` window.
2. Turn off autostart (`service autostart disable`, or on the settings page).
3. Remove the SmartCluster entry from your AI App's MCP configuration.
4. If this computer is a member, ask the group owner to revoke this node in the Hub console.
5. Delete the program folder. The group data in `%USERPROFILE%\.smartcluster-groups` is kept; delete it manually only once you are sure you no longer need it.

## 11. Data and routine maintenance

Group state is stored in `.smartcluster-groups` by default. It is not removed when the EXE is deleted, and legacy `.state` data or data from other installations is not imported automatically. Depending on the feature, task inputs, results, events, and metadata are transmitted to targets or stored by the Hub/Node; full App conversation history stays on its original computer. AI analysis sends submitted content to the selected node and AI service.

Cross-computer traffic uses mTLS to authenticate node identity and encrypt transport; this is not disk encryption or protection against reverse engineering of the program. Never publish invitations, login URLs, private keys, tokens, or an entire data directory. [Troubleshooting FAQ](FAQ.en.md) · [WAN](WAN.en.md)
