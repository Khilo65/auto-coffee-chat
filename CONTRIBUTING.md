# Contributing

Useful contributions improve a specific decision or workflow in the skill. Explain the problem, the smallest proposed change, and how you checked it.

Areas worth working on include contact prioritization, natural recipient-specific writing, cross-channel duplicate prevention, follow-up timing, booking recovery, automatic meeting preparation, and honest measurement of outcomes.

## Protect private data

Use invented people and synthetic conversations in examples. Do not paste real messages, contact details, profiles, screenshots, meeting links, account identifiers, private file paths, tokens, or exports into this repository, issues, or pull requests. Removing a name from a real conversation may still leave it recognizable.

Run actual outreach in a separate private workspace outside the repository. Contributions never authorize sending messages, inviting people, connecting accounts, or starting monitoring.

The `.gitignore` allowlist admits only the current public distribution files. A new public reference or helper needs a deliberate allowlist change and review. Inspect all staged content and commit author details before pushing; do not force-add private files. If a credential is exposed, revoke or rotate it promptly and handle repository history separately from deleting the current file.

## Review changes

Use the current Codex skill validator when available. For workflow changes, describe a bounded synthetic scenario and the observed result. Check the path for an unknown or failed send, a contact on an approval hold, a rescheduled meeting, and missing account access when relevant.

Keep setup customizable. Preserve the separation between drafts, approved actions, attempted actions, verified sends, bookings, and completed meetings. Do not promise background execution or account access that the host has not verified.

When reporting results, include the denominator, observation window, channel, and definition of success. Count coffee chats separately from hiring interviews. Do not infer causality from a small uncontrolled sample.

## Submit a benchmark

Use the [benchmark guide](benchmarks/README.md) and [result template](benchmarks/result-template.json). Add an anonymized aggregate result under `benchmarks/results/` through a pull request, with the implementation version, observation window and known limitations. Include nonresponders and automation errors. Real outreach results and synthetic workflow checks must be labelled separately. Higher rates across different campaigns do not prove a causal improvement.
