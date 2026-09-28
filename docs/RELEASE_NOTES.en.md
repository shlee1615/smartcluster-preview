# Release Status and Verification Scope

[Home](../README.md) · [繁體中文](RELEASE_NOTES.zh-TW.md)

Updated September 28, 2026. **0.11.0.dev3 is a development preview candidate, available as an experimental public pre-release.** This is a status document, not a launch announcement.

## New in dev3

The Windows candidate has been rebuilt with the invitation group-name fix. Its executable preserves `Work Group` in invitations. Nine same-host, isolated-process smoke scenarios passed, including fixed-profile MCP, TLS joining/retry, diagnostics, group isolation, intake switching, and the English name. The Hub reports dev3. These checks do not establish independent clean-machine acceptance or mixed-version interoperability. Third-party texts and actual bundle inventory have been collected; the complete dependency review and product terms remain pending. The included film shows an earlier development session.

## Available capabilities

A Windows x64 executable; group creation, enrollment, viewing, and service controls; draining intake switches within one registry; explicitly profile-bound stdio MCP; built-in diagnostics; existing collaboration tasks and App receivers. Cross-computer transport uses implemented mTLS.

## Completed verification

| Scope | Evidence and limits |
|---|---|
| dev3 source regression | 248 Python tests and 33 JavaScript tests passed in the current run; not a clean-machine binary acceptance test |
| dev3 Windows executable | Nine same-host process scenarios passed, including the English invitation name; extracted ZIP launched with project Python environment variables removed |
| Isolated Windows processes | 20 dev2 group/release checks and executable multiprocess smoke checks passed |
| Mac mini M4 + Windows LAN | New Mac test Hub with a Windows dev2 executable member; mTLS, diagnostic round trips, deduplication, stop/restart, and queued-task recovery passed |
| Mac test runtime | Private source deployment; receiver reported 17 profile tests passed, not macOS executable acceptance |
| Previous WAN pilot | Limited Tailscale testing on an older version; not dev2 WAN acceptance |

Counts from different runs or subsets must not be added into a new full-regression total. Private internal evidence files are not included here.

## Known issues

- Historical dev2 issue: invitations could carry a fixed Chinese group label. dev3 includes and tests the fix; existing dev2 artifacts are unchanged. Previous Mac/Windows LAN evidence remains dev2 evidence, not a new dev3 cross-machine test.
- Signing and clean-machine acceptance are pending. No standalone macOS executable is delivered.
- Current-version WAN, extended stability, and complete update/rollback acceptance are pending.
- No ownership transfer, person-based group roles, complete formal leave/dissolve workflow, machine-wide intake coordination across registries, automatic updater, or redacted-export UI.
- Idle App wake-up is not guaranteed. Service health, provider configuration, and App intake require separate checks.

## Public trial download

[Windows x64 ZIP and checksums](https://github.com/shlee1615/smartcluster-preview/releases/tag/v0.11.0.dev3). Extract the entire package and run SmartCluster.exe. The owner has authorized public trial distribution with the current limitations disclosed. This is unsigned and has not passed independent clean-machine acceptance; it is not a production release. Collected dependency notices are preliminary and full dependency review and commercial terms remain unfinished.

The EXE embeds 29 readable web assets and product Python bytecode. Packaging does not prevent extraction or reverse engineering. No standalone Python source, invitations, keys, or private state are attached. GitHub's automatic source archives contain this documentation/media repository, not the private product project.
