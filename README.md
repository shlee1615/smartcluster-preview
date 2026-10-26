# SmartCluster · Preview 2

### Bring your distributed AI agents into one development workflow.

[繁體中文](README.zh-TW.md) · **English** · [Visit the live website](https://smartcluster.pages.dev/preview2/?lang=en)

**Preview 2 website is live:** [English](https://smartcluster.pages.dev/preview2/?lang=en) · [繁體中文](https://smartcluster.pages.dev/preview2/?lang=zh-TW). Watch the English demo with either English narration or Traditional Chinese explanation.

Choose an authorized computer and agent from your AI conversation. Follow the task through dispatch, execution and reporting, then inspect the result. SmartCluster keeps the task's status visible so that “submitted” and “completed” remain distinct.

- **Choose the right executor.** Connect configured Codex, Claude and Gemini environments, or connect your own agent through a bridge.
- **Coordinate across computers.** The Hub manages tasks; each Node executes within local permissions. Joining a group does not share AI accounts or expose the entire computer.
- **Finish with evidence.** Supported development channels return file changes, test exit codes and reports while preserving the native App's approval process.

## See the workflow

[Watch the 120-second native App demo](https://smartcluster.pages.dev/preview2/?lang=en#native-film) · [English video](preview2/media/smartcluster-native-demo.en.mp4) · [繁體中文 video](preview2/media/smartcluster-native-demo.zh-TW.mp4) · [Demo notes](docs/DEMO.en.md)

The English checkout case follows Gemini in Antigravity as it fixes one formula and passes five tests, then shows the official Claude CLI review and the returned results. The film combines native App footage with user-provided Hub screenshots and clearly labeled editorial summaries; it is not an uninterrupted recording or a Claude desktop recording. Both languages use the same English example. See the [demo notes](docs/DEMO.en.md) for evidence and scope.

The separate [60-second explanatory animation](https://smartcluster.pages.dev/preview2/?lang=en#film) uses motion graphics, not a product screen recording. The interactive workflow submits no real task. An earlier [cross-computer recording](media/SmartCluster-MSI-demo-v3.en.mp4) remains available as a historical demonstration. For offline viewing, open [the local introduction](preview2/index.html?lang=en).

## What is in this trial?

**Preview 2 candidate 0.14.0.dev5 is a Windows x64, invite-only evaluation build; it has not been publicly released.** It provides Hub/Node management, groups, MCP, diagnostics and supported dispatch entry points without a separate Python installation. AI clients and CLIs require their own installation, sign-in and permissions.

| Use | Scope |
|---|---|
| Manage and dispatch with this package | Manage groups, query nodes, submit supported tasks and retrieve results; executable updates are manual |
| Use a configured execution node | Gemini CLI, automatic desktop intake and isolated development require a capable, accepted and locally authorized node |
| Run isolated file editing/tests directly on this binary Node | Unsupported in this build; the Hub's ability to dispatch does not grant execution capability to its local Node |

The full Gemini and CTE-Codex development workflows have been accepted on the Primary development deployment, not on every fresh binary installation. Gemini App and CLI models are configured separately. The CTE bridge does not yet support sub-delegation, Hub model overrides or complete usage reporting.

## Start a trial

1. Obtain the ZIP and SHA-256 from your inviter, then verify and extract the entire package using the [user guide](docs/USER_GUIDE.en.md).
2. Create a test group and complete the no-AI connectivity diagnostic first.
3. Connect local MCP, dispatch to a configured target, and verify the final status and task ID.

[Release and acceptance status](docs/RELEASE_NOTES.en.md) · [FAQ](docs/FAQ.en.md) · [WAN guide](docs/WAN.en.md) · [Next steps](docs/ROADMAP.en.md)

The trial excludes product Python/TypeScript sources, the development repository and private state. Normal web assets and Python bytecode remain readable or analyzable; packaging does not guarantee protection from reverse engineering. This build is unsigned. Consult the release record for clean-account and cross-machine acceptance of this version.
