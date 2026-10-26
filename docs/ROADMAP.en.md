# After Preview 2

[Home](../README.md) · [繁體中文](ROADMAP.zh-TW.md)

These are priorities for the next round, not capabilities already supplied by this candidate. No dates are committed. Complete package, clean-account and cross-machine acceptance before expanding the scope.

## 1. Make execution nodes easier to install

First complete Gemini CLI, automatic App intake and isolated development for Windows binary deployments, reusing existing authorization, acceptance, sandbox and task flows. Toolchains and helpers must actually work; removing the frozen guard is not a solution. Validate dispatch, editing, tests, cancellation and reporting on a fresh node, then extend packaging and acceptance to macOS.

## 2. Whole-package updates and recovery

Source installations already have signed releases and staged updates; executable installations still update manually. A separate helper should download and verify a release, wait for idle, replace the whole package and check health, restoring the program and compatible data on failure. Also verify recovery after interruption while retaining accounts, settings and work data.

## 3. Make progress easier to follow

Use the same task identifier across the initiating conversation, execution side and Hub. Distinguish intake, execution, approval waits, tests, reporting and reconciliation. Show only observed progress; background CLI work must not be presented as a native App conversation. Acceptance covers success, failure, cancellation, reconnect and privacy masking.

Schedule code signing, macOS notarization, de-identified diagnostics and additional network paths according to trial feedback. Mobile, voice and a larger agent framework are not prerequisites for this round. [Current scope](RELEASE_NOTES.en.md)
