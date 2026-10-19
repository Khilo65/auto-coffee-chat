# Auto Coffee Chat

A customizable **Outreach Ledger** skill for Codex. It helps you research professional contacts, keep an accurate history of conversations, draft outreach, review follow-ups, coordinate meetings, and prepare for the people you meet.

Use it for career networking, research, partnerships, or another clearly defined outreach goal. The first run adapts the workspace to your sector, accounts, calendar, and preferred level of automation.

## Get started

1. Download or clone this repository.
2. Give Codex [the skill file](outreach-ledger/SKILL.md) and ask it to install **Outreach Ledger** using the skill location supported by your installation. The `outreach-ledger` folder contains the skill and its optional UI metadata; preserve an existing installation before replacing it.
3. Open a **separate private workspace outside this repository** for your contacts and meeting notes.
4. Invoke `$outreach-ledger` with the prompt below.

> Set up my outreach workspace. Walk me through my goals, profile, browser, email and calendar connections, approval preferences, follow-up rules and automation schedule. Start with drafts only. Keep all personal records in this private workspace.

## What setup covers

- Your target organizations, sector, purpose, background, and writing style.
- A contact ledger and exact message history, with evidence for replies, sends, permissions, and outcomes.
- Your regular authenticated browser session, selected mail accounts, and relevant calendars. Login or verification steps that need you are surfaced directly.
- A configurable daily message cap, follow-up delay, contact-specific restrictions, and permitted actions. The example cap is a personal limit, not a platform allowance.
- The host conditions needed for scheduled work, including power, network access, an available desktop session, and connected accounts. Check current Codex scheduling support during setup.

**Installing a skill enables instructions for Codex.** It does not install a background service or connect accounts. Sending, calendar invitations, and monitoring require the permissions agreed during setup and tools that actually work in your environment. Monitoring starts disabled.

## From booking to debrief

A verified booking triggers creation or updating of a private meeting brief during the booking workflow. It includes sourced background, exactly what was said in outreach, a topic to pick up, three priority questions and a backup, and a short conversation plan. Codex surfaces the brief to you in the chat. Delivery by email or another channel needs separate authorization.

An authorized monitor can reconcile meetings booked elsewhere at its next check. Immediate detection of external bookings depends on an available event trigger. After the meeting, your debrief captures what you learned, commitments, and any specific recommendations, with a thank-you drafted separately.

Follow-ups use the latest conversation across approved channels. The skill checks prior nudges, elapsed business days, permission holds, and the shared daily cap before a send; an uncertain send is inspected before any retry.

## Results and improvements

The earlier workflow produced **five completed networking conversations from 53 fully tracked contacts (9.4%)**. See [the note for a friend](NOTE_FOR_A_FRIEND.md) for denominators, limits, and ideas to improve it. Historical use included manual steps; these figures are not a benchmark of the newly packaged skill.

Contributions are welcome. Start with [CONTRIBUTING.md](CONTRIBUTING.md), especially its rules for keeping personal data out of issues, examples, and commits.

## Public files and private records

This repository contains generic instructions and aggregate results. Keep real profiles, ledgers, messages, debriefs, screenshots, account configuration, credentials, and automation state in your separate private workspace. Never publish an initialized outreach workspace.

The repository uses a file allowlist in `.gitignore`. That reduces accidental additions; review the staged content and commit metadata before every push. GitHub account ownership and public commit metadata are visible to everyone.
