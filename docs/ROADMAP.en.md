# Next phase

[Home](../README.md) · [繁體中文](ROADMAP.zh-TW.md)

These are planned follow-up improvements, not features promised in the first preview. No delivery date is committed.

## Visible execution on the target

Show a real supported execution interface on the target computer: receipt of a task, available progress or tool output, and the final result. Link the initiating conversation, target view, and Hub record using the same task identifier. A background CLI task does not automatically appear in an existing Claude desktop conversation.

Acceptance should include successful and failed work, cancellation state, disconnect/reconnect behavior, and redaction of private content. Use actual observable output; do not manufacture an agent's internal reasoning or display a simulated transcript as execution evidence. A later demo can show the lead and executing agents side by side with capture timing explained.

## Other follow-up work

- Validate customer-managed enterprise VPN and alternative network paths; current guidance centers on customer-managed Tailscale.
- Improve update, recovery, and redacted diagnostics workflows.
- Evaluate richer group administration and person-based roles separately from current device authentication.

Before public binary distribution, the current candidate still needs completed dependency notices and product terms, signing/distribution decisions, and clean-machine acceptance. See [release status](RELEASE_NOTES.en.md).
