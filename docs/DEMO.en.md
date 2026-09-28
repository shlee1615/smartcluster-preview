# Watch the workflow

[Home](../README.md) · [繁體中文](DEMO.zh-TW.md) · [Setup guide](USER_GUIDE.en.md)

[Watch the English-captioned demo](../media/SmartCluster-MSI-demo-v3.en.mp4) · [Subtitles](../media/SmartCluster-MSI-demo-v3.en.srt)

![SmartCluster demonstration](../media/cover.en.png)

In this real recorded workflow, a user asks an agent on Mac mini M4 to send a text review to Claude on MSI. SmartCluster carries the supported task through MCP, the target's official CLI performs the analysis, and the initiating conversation retrieves the result. The Hub provides the task record used to check the execution node and completion.

## Follow the 60-second story

| Time | What you see | Why it matters |
|---|---|---|
| 0–6 s | Hub node graph: five online nodes | Discover the available network. This task involves the Mac and MSI; it does not use all five nodes. |
| 6–10 s | A prior MCP node query in the lead conversation | Ask about available computers from chat. This short query clip precedes the new task. |
| 10–20 s | A request to review the fictional Orbit pitch | Give the target a concrete task and request three recommendations. |
| 20–37 s | MSI desktop and Windows Task Manager | See the target computer during the task. Process names and activity alone do not identify or prove completion of a specific task. |
| 37–45 s | The lead conversation retrieves the review | Bring the result back to the user, without manually copying it from the target. |
| 45–56 s | Hub completion and history | Check the recorded initiator, execution node, outcome, and delivery. |
| 56–60 s | Closing view | Delegate in chat and follow the outcome. |

## Try a comparable workflow

First follow the setup guide, connect MCP to the intended profile, and complete a no-AI diagnostic. Enable and sign in to the intended AI provider on the target. Use your own node name in these requests:

> List this group's nodes and enabled AI providers. Identify Windows Test Node and report its readiness.

> Ask Claude on Windows Test Node to review the following fictional product pitch for clarity and unsupported claims. Return a short review and three recommendations. Do not modify files. Track the task to its final state and include its task ID: [insert sample text].

> Retrieve the final result for that task. If it failed or remains queued, report the actual state instead of assuming success.

The target owner controls provider access and account allowance. A successful diagnostic tests connectivity; it does not establish AI readiness. Tools available to a task depend on its configured execution path and permissions.

## What this film does and does not establish

Both language editions are 60-second, 1080p, 30 fps recordings with edited timing, titles, captions, and original synthesized background music. They have no spoken narration. Some original operating-system labels remain in Chinese. The English edition is an English-captioned edition, not a completely English operating-system session.

The MSI footage shows a process view. It does not show Claude's live chat or terminal output, and no PID-to-task mapping was captured. Task attribution comes from the Hub record. Cuts and accelerated segments are not a performance benchmark or a continuous live session. Orbit is fictional demonstration content.

Visible execution output is planned for the [next phase](ROADMAP.en.md). The film is a demonstration of a development environment; it does not establish public macOS binary availability or release acceptance of every displayed node or network path.
