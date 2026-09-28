# FAQ and Troubleshooting

[Home](../README.md) · [繁體中文](FAQ.zh-TW.md) · [User guide](USER_GUIDE.en.md)

## Does SmartCluster include an AI subscription?

No. The diagnostic demo uses no AI. Real analysis runs through an installed, signed-in, enabled official Claude or Codex CLI on the target computer and uses that account's allowance. App receiver jobs are a separate path from CLI analysis.

## Can I operate it entirely from chat?

After configuring a client that supports local stdio MCP, you can query nodes, dispatch and track tasks, and use supported local service/invitation tools. Group creation and switching still use the web interface. If the AI only offers advice, check that the tools are loaded and allowed, and look for actual tool results.

## Does viewing another group reroute my work?

No. View does not change intake. MCP is pinned to an explicit local profile, independently of UI selection or the active intake group. One group per registry accepts new work; this is not a machine-wide lock across independent installations. Verify the group and target before dispatch.

## Why is an App job still queued?

Check the connected receiver, permitted sender and project, and whether the App is polling. An online Node or a successful submission does not establish that the App is awake. The preview does not guarantee automatic wake-up of idle Apps. Existing external schedules are managed separately.

## Does joining grant access to my entire computer?

No. Pairing, AI sign-in, project access, file delivery, and App intake have separate permissions. A host cannot expand local permissions just because you joined. mTLS identifies devices/nodes; it is not a complete person-based role system.

## Where does my data go?

Task inputs and results are processed and stored by the coordination path as required by the feature. AI analysis sends submitted content to the target node and selected AI service. Full App history remains on its original computer. Share only what the task needs, and never attach raw work data, invitations, or credentials to public issues.

## Common problems

| Symptom | What to check |
|---|---|
| Management page expires or requests login | Reopen it from the EXE; do not share authenticated URLs |
| Intake is enabled but nothing runs | Start the service, then check health and diagnostic results |
| Chat queries the wrong group | Check profiles-dir and profile_id; this is not cluster_id |
| Enrollment times out | Check versions, actual Hub address/port, routing, and permitted firewall rules |
| Invitation or certificate mismatch | Verify source, clock, and fingerprint with the host; retain TLS verification |
| Enrollment is interrupted | Resume the existing record before creating another identity |
| Group switch keeps waiting | Reconcile unfinished work, then continue or cancel the switch |
| Outcome needs reconciliation | Inspect artifacts and processes; preserve records and avoid repeating side effects |
| Legacy group is missing | The new registry does not automatically import an old installation |
| System protection blocks the EXE | Candidate is unsigned; verify source/checksum with IT or the maintainer rather than disabling protection |

## Is it ready for commercial deployment?

This is a development candidate. Product licensing, support terms, and service commitments have not been published. AI and VPN providers have separate terms. A preview or a third-party free plan is not a grant of commercial usage rights. [WAN guide](WAN.en.md)

## Does executable-only distribution hide the implementation?

No. Inspection of the current internal dev3 EXE found 29 readable HTML/CSS/JavaScript assets identical to the source files, plus 29 product Python bytecode modules. PyInstaller packaging does not provide source confidentiality: web assets can be extracted, and bytecode may be analyzed or decompiled. The repository does not publish standalone Python source files. The owner has authorized public executable trials with these reverse-engineering limitations disclosed. Minification, obfuscation, or native compilation can raise analysis effort but cannot guarantee secrecy of code shipped to a user's computer.

## How do I report an issue?

Report problems through this repository's Issues page. Include version, operating system, local/LAN/WAN scope, reproduction steps, expected and actual behavior, and redacted error codes. Remove accounts, addresses, paths, task content, and temporary login information from screenshots. Automatic redacted export is not available. For sensitive findings, first ask the maintainer for a private reporting channel; do not post secrets or exploit details publicly.
