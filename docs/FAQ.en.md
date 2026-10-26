# FAQ and Troubleshooting

[Home](../README.md) · [繁體中文](FAQ.zh-TW.md) · [User guide](USER_GUIDE.en.md)

## Does SmartCluster come with its own AI?

It does not include a model subscription. The diagnostic uses no AI. Real analysis uses a provider installed, signed in and enabled on the target computer, consuming that account's allowance. Codex/Claude CLI and App receivers are separate channels. New Gemini capabilities require a supported execution node; installing this package alone does not make them available.

## Can I operate it entirely from chat?

Once a client that supports local stdio MCP is connected, you can query nodes, dispatch and track work, and operate the supported local service and invitation features. Creating and switching groups still uses the web interface. If the AI only offers advice on what to do, check whether the tools are loaded, whether calls are allowed, and whether there is an actual result.

## SmartScreen says "Windows protected your PC" on first launch?

This build is unsigned, so this prompt is expected. First verify the ZIP against the SHA-256 from your inviter (`Get-FileHash`) and continue only if it matches; if it does not, stop and check with your inviter. On company-managed devices, let IT decide. Do not disable SmartScreen or antivirus; if antivirus quarantines a file, hand the hash and file name to IT or your inviter rather than adding an exclusion yourself.

## Why can't I copy just SmartCluster.exe?

The program needs the `_internal` folder beside it (the Python runtime, libraries, and web assets). Always move the whole `SmartCluster` folder.

## If I close that black window, will the groups stop?

The window that appears when you double-click `SmartCluster.exe` serves the **My groups** management page; closing it makes the management page unavailable, but **the background services of groups that have been started do not stop**. To stop a group, click **Stop service** on the management page. Start automatically at sign-in uses the windowless `SmartCluster-background.exe`, so this window does not appear.

## How do I update? Is it automatic?

The executable build does not update automatically, and the Hub does not push to it (the console shows **Executable install: manual update**). See [section 9 of the user guide](USER_GUIDE.en.md#9-manual-update-this-build-has-no-automatic-update): pause intake, stop the services and AI Apps, back up `.smartcluster-groups`, extract the new version to a new folder, rename so the path stays the same, launch and confirm. Restore the backup before rolling back to an older version.

## Does viewing another group send work to the wrong place?

**View** does not change intake. MCP is bound to a specified local profile and does not change with the UI selection or the intake group. One intake group at a time per registry; this is not a shared lock across all independent installations on the machine. Still verify the group and target on every dispatch.

## Why does an App job stay queued?

First confirm that the receiver is connected and that the sender and project are within the permitted scope, then check intake activity. For manual receivers, say "Please collect SmartCluster jobs" in the original conversation. A configured Gemini sidecar on a supported deployment can notify an open native App, but requires separate installation and setup; this binary does not provide that installation flow. An online Node or successful submission does not prove that the App claimed or completed the job.

## Does joining expose my entire computer?

No. Group pairing, AI sign-in, project permissions, file delivery, and App intake are configured separately. The group owner cannot expand your local permissions just because you joined. mTLS authenticates devices/nodes; it cannot serve as complete person-based role management.

## Where does my data go?

Dispatched content and results are handled by the collaboration path and stored as the feature requires; AI analysis hands the content you submit to the target node and the selected AI service. Full App history stays on its original computer. Share only what the current job needs; when reporting a problem, do not attach raw work data, invitations, or credentials.

## Why introduce Gemini/CTE when my local Node cannot run isolated development?

The introduction covers the SmartCluster collaboration workflow. This trial package provides Windows management/dispatch and supported local Node functions. Its frozen Node does not execute `agent.develop`, nor install Gemini CLI or Gemini App MCP/sidecar integration. Those paths require a configured, accepted and authorized execution node. Choose a capable target; changing a label or removing a guard does not enable a capability. See the [capability matrix](RELEASE_NOTES.en.md).

The CTE-Codex application is not bundled. Bridge development acceptance comes from the existing Primary development deployment. It does not support sub-delegation, Hub model overrides or complete token usage reporting.

## Do Gemini model settings synchronize with the desktop App?

No. The Hub-managed CLI model and Gemini desktop App's native model selector are separate; configure and verify each. A configured provider label also does not establish that the App intake service is running.

## Common problems

| Symptom | What to do |
|---|---|
| Management page stops working or asks you to sign in | Reopen the local entry point from the EXE; do not share URLs that contain sign-in information |
| Service shows intake enabled but nothing runs | Start the service first, then check health status and diagnostic results |
| The AI sees a different group | Check the MCP profiles-dir and profile_id; not the cluster_id |
| The AI says it cannot find the SmartCluster tools | Check the full EXE path and argument order in the MCP configuration (`--profiles-dir … --profile … mcp`), then **quit the App completely and reopen it** |
| Join times out | Check the version, Hub address and actual port, routing, and permitted firewall rules |
| Invitation or certificate mismatch | Re-verify the source, time, and fingerprint with the group owner; do not skip TLS verification |
| Join interrupted | Resume the existing join record first; do not keep creating new identities |
| Switch keeps waiting | Check the original group's unfinished tasks; continue once they finish, or cancel the switch |
| Outcome needs reconciliation | Inspect the actual artifacts and processes; keep the records; do not automatically redo side effects |
| Old group is missing | A new registry does not automatically import an old installation; keep the original data |
| Autostart did not take effect | After moving or replacing the program folder, turn autostart on again; it records an absolute path |
| The EXE is blocked by the system | The candidate is unsigned; verify the source and hash, then hand it to IT or your inviter; do not disable protection |

## Can I deploy it commercially right away?

This is still a trial build; product licensing, support, and service commitments have not been published. Trial terms are in [release status](RELEASE_NOTES.en.md). Third-party AI and VPN services have their own terms; check them for your use case, and do not treat a trial or a third-party free plan as a grant of commercial use. [WAN guide](WAN.en.md)

## Does executable packaging protect the source code?

Not guaranteed. The EXE and `_internal` contain readable HTML/CSS/JavaScript assets identical to the source, plus all product Python bytecode. PyInstaller packaging does not keep program contents confidential: web assets can be extracted, and bytecode may be analyzed or decompiled. The owner has decided to offer the invite-only trial with this limitation disclosed.

## How do I report an issue?

The trial is invite-only; report directly and privately to your inviter. Include the version, operating system, single-machine/LAN/WAN scope, reproduction steps, expected and actual results, and redacted error codes. Remove accounts, IPs, paths, task content, and short-lived sign-in data from screenshots first. There is no automatic redacted export. For sensitive findings, do not publish exploit details or secrets.
