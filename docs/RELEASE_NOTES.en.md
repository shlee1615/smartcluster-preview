# Preview 2: release status and verification scope

[Home](../README.md) · [繁體中文](RELEASE_NOTES.zh-TW.md)

Updated October 26, 2026. **The Preview 2 introduction website is public; the 0.14.0.dev5 Windows x64 program remains an invite-only candidate, not a public binary release.** Build and acceptance evidence must identify the same version, commit and package hash.

## Public website update · October 26

- [Live English website](https://smartcluster.pages.dev/preview2/?lang=en) · [繁體中文](https://smartcluster.pages.dev/preview2/?lang=zh-TW).
- Adds the 120-second English native App case with English/Chinese narration and captions, 36 seconds of captured Hub views, and an enlarged Hub gallery. Retains the separate 60-second animation.
- The public repository contains introduction pages, documentation and edited media only. This update publishes no new program binary, product source, credentials or conversation history. Existing historical release assets are unchanged.

## dev5 refresh

- Adds three quick-start goals: local trial, joining a group and configuring Gemini/CTE. These are reading guides, not connection or authorization changes.
- Adds pausable task-motion graphics and honors reduced-motion preferences. Six video chapter buttons seek without starting audio.
- Refreshes both films with livelier scenes, natural narration, synchronized captions and an original quiet soundtrack that ducks under speech.
- Removes the obsolete 0.11 sidebar label; the header identifies 0.14.0.dev5. Core agent behavior and deployment capabilities remain those of dev4.

## Highlights

- Use one Hub to query, dispatch to and retrieve results from authorized Codex, Claude, Gemini and custom-agent bridge deployments.
- Gemini analysis, persistent conversations, bounded delegation, model selection and automatic desktop App intake have been accepted on a supported development deployment.
- CTE-Codex bridge editing, tests and reporting have been accepted in isolated worktrees on a supported development deployment. Changes remain for review; they are not automatically merged.
- New offline bilingual introduction and videos. Interactive flows and motion graphics are illustrative; live acceptance evidence is identified separately.
- Retains Windows onedir packaging, background sign-in startup, multiple groups and manual updates. Product source code is not distributed.

## Package and execution-node capabilities

| Capability | This Windows binary | Existing configured development deployment |
|---|---|---|
| Groups, Hub management, MCP, diagnostics and supported task dispatch | Included; candidate acceptance is recorded separately | Existing acceptance evidence |
| Codex/Claude CLI | Separate installation, sign-in and local authorization required; AI clients are not bundled | Existing evidence; capability varies by node |
| Gemini CLI and Gemini App MCP/sidecar installation | Unsupported on this frozen Node | Accepted on Primary; requires the native App to be open and project authorization |
| Isolated worktree editing/tests | Not executed by this frozen Node | A capable Node can accept Hub dispatch, subject to current acceptance and local authorization |
| CTE-Codex bridge | CTE application, accounts and configuration are not bundled | Fixed bridge accepted; no sub-delegation, Hub model override or complete usage reporting |

A Hub can dispatch to a capable execution node without its own binary Node gaining that capability. Source installations for configured execution nodes are not included in this trial; they are managed by the deployer. Installation forms can have different capabilities. Mixed **version** compatibility still requires explicit verification.

## Acceptance record

| Scope | Status and boundary |
|---|---|
| Preview 2 full regression | Fresh full run passed on October 26: Python 691 tests (8 skipped), JavaScript 74 passed. Evidence: `outputs/preview2-refresh-full-tests.log` |
| Preview 2 package completeness and source exclusion | Build passed: 115 program files and 160 audited package members. Path, linked-file and public-text checks passed. Final commit and archive hash are recorded in build evidence and the external `SHA256SUMS.txt` |
| Preview 2 same-machine isolated multi-group/mTLS smoke | Nine executable checks passed: paused intake, two-group isolation, viewing without intake switch, drain/switch, previous Hub stays online, fixed-group MCP, English invitation name, mTLS join/retry identity and member diagnostic roundtrip. Not equivalent to a clean account or two physical machines |
| Preview 2 GUI, no-Python standard account and cross-machine acceptance | Incomplete; update only from actual results |
| Primary development deployment, October 26 | Gemini `gemini-4-argon-medium` three-turn new/resumed conversation acceptance; Gemini desktop intake, file editing, five unittest cases and reporting; CTE bridge isolated edit, unittest exit 0 and Hub completed with the original project unchanged |
| Earlier SmartCluster source regression | Evidence for HEAD `517ecf9`: Python 677 tests including 8 skipped, JavaScript 74 passed; not a new regression of this candidate |
| CTE repackaging, October 26 | `0.9.9l-bridge-20261026` full `npm run check` passed; the earlier two failures were fixed. Settings, existing projects and conversations were preserved. This is separate CTE package acceptance |
| Historical 0.13.0.dev7 binary | Build audit and same-machine isolated smoke passed; GUI/clean-account acceptance was incomplete and does not count as Preview 2 acceptance |
| October 5 source-install cluster | MSI one-click dev5→dev6; both Macs updated manually. This does not establish binary updating |

Do not combine test counts across runs, subsets or products. Service availability, provider configuration, automatic App intake and completed work are separate states.

## Known limits

- Unsigned; verify the ZIP hash without disabling SmartScreen or antivirus.
- Executable updates and rollback are manual. Data upgrades and rollback require backups and version-specific acceptance.
- No macOS executable; existing macOS deployments are assessed separately.
- Arbitrary idle Apps are not guaranteed to wake. Gemini notification applies only to its configured native App/sidecar; other receivers use their actual intake mode.
- Gemini App models use the native selector. Hub CLI model settings do not override the App model.
- Native Windows Computer Use still has a browser URL-identification limitation. Passing Chrome extension Browser Use does not establish that native path as fixed.
- Full WAN development delivery, long-running stability, other VPNs and the new cross-machine deployment still require acceptance.
- No complete people-level role management, group-owner transfer, formal leave/dissolve flow or automatic redacted export.

## Contents and trial terms

The package contains `SmartCluster/`, `README.md`, `guide/` (including `preview2/index.html` and media), `notices/`, and `SHA256SUMS.txt`. It excludes product Python/TypeScript sources, development tools, invitations, credentials and private databases. Normal HTML/CSS/JavaScript and Python bytecode remain readable or analyzable; packaging is not reverse-engineering protection.

For evaluation by invited testers only; do not redistribute. Provided as is; do not use production data or unbacked-up environments. The inviter supplies the trial period and other terms. Third-party license texts are in `notices/`.
