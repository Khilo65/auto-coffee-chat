---
name: outreach-ledger
description: Set up and run a customizable professional outreach workspace with an evidence-backed contact ledger, message history, follow-up reviews, scheduling, automatic meeting preparation briefs, debriefs and outcome analysis. Use for relationship-led career, research, partnership or business outreach across organizations and sectors.
---

# Outreach Ledger

Build a personal relationship workflow that can be resumed safely in Codex. Adapt it to the current user's identity, goals, voice, accounts and sector. This file is self-contained; no creator's private contacts, paths, accounts, calendar IDs or other skills are required.

Example first request: `Use $outreach-ledger to initialize my outreach workspace and walk me through setup.` Later requests can be `draft outreach`, `check replies`, `book this chat`, `prepare for my meeting`, `debrief this call`, `review results` or `pause monitoring`.

A skill describes how to work. Installing or opening it does not start a daemon, connect accounts, grant sending permission or create scheduled tasks. Only initialize a workspace when requested or first-use intent is clear; ordinary drafting in an existing workspace must not reset setup or trigger another onboarding.

## 1. First-run setup

Read applicable workspace instructions and inspect only the relevant existing outreach files. Reuse a canonical ledger when one exists. Do not overwrite files or create a competing tracker. If an established schema differs, map these requirements to it; propose a migration before changing its structure. Keep research and local scaffolding moving as missing preferences are collected. If no permanent root is chosen, use a clearly labelled temporary staging directory, disclose its location and leave the permanent location pending; do not silently initialize in an unrelated existing project. Ask the three groups progressively when a single response would be unwieldy.

Ask the following in up to three short grouped prompts. Infer answers already given. Record unanswered required choices as pending; a suggested default is not approval.

1. **Purpose and profile:** workspace location, name and preferred sign-off; goals and target organizations/sectors/locations; relevant CV/bio/portfolio and writing examples; audience, application route or commercial purpose; meeting length and information sought. Ask which supplied files may be used and whether any relationship history already exists. Do not infer achievements or import an address book wholesale.
2. **Accounts and wiring:** chosen channels and exact sending identities, regular Chrome profile (or another explicitly chosen supported regular browser), authorized email accounts, calendar account and booking calendar, all calendars to check for conflicts, IANA timezone, meeting platform, reminders and preparation-brief delivery. Ask the user to connect/sign in through supported tools. Never request passwords, tokens or MFA codes in workspace files.
3. **Operating permissions:** draft-only or a defined class of approved sends, target allowlist/campaign scope, review holds and do-not-contact people, daily ceilings, follow-up policy, authority to create events separately from authority to invite/notify guests, flexible versus fixed calendar blocks, monitoring cadence/timezone and notification preference. Ask whether to activate scheduled monitoring after the first manual check. Default external sending and monitoring to disabled until authorized.

Recommended initial defaults, to present as editable choices:

- Draft-only messages, existing-contact monitoring, 15-minute chats, one availability-only follow-up after at least five business days, one-on-one booking calendar, 60- and 5-minute reminders.
- A conservative daily LinkedIn ceiling of 15 outgoing notes/messages/InMail combined, with capacity left for replies. This is a chosen operating ceiling, not a claim about LinkedIn's official limits. Use a lower applicable platform/account restriction.
- Immediate prep brief in Codex after booking; no external delivery of briefs. Email sends, new prospect campaigns and cross-channel follow-ups require their own authorization.
- Independent editorial review before outgoing drafts when a separate agent is available. Ask whether this is mandatory for sending; default to required before an unattended send.
- One daily check at a user-chosen local time; otherwise no schedule. Notify for actual replies needing review, a new or materially changed booking/brief, or a concrete access blocker. Routine no-change checks are silent.

### Wiring checklist and first manual check

Inspect the tools actually available in this environment; read their current instructions and use their supported names and arguments. Do not assume a browser, connector or automation API is installed because a previous installation had it.

| Capability | First-use verification | If unavailable |
| --- | --- | --- |
| Local workspace | Confirm selected directory and read/write access with a harmless local file | Keep setup pending; do not pretend data was saved |
| Browser use | Confirm the chosen supported regular, non-private browser profile and the user's visible LinkedIn identity | Ask the user to enable the supported browser connection and open/sign into the correct regular profile |
| Email, if selected | Verify exact account and a narrowly selected relevant thread, including Sent | Explain connector setup or use an authorized normal UI; do not scan another mailbox |
| Calendar, if selected | Verify account, booking calendar and conflict-calendar IDs with a bounded read | Continue drafting; block bookings until the required calendars can be checked |
| Platform and invitations | Inspect supported conferencing/event tools and verify an actual created join link when booking is authorized | Offer a usable supported alternative; do not promise an unauthenticated host |
| Automations | Inspect supported scheduling tools and existing tasks for this workflow | Keep a manual checklist; no invented cron jobs, hooks or background service |
| Notifications | Confirm the chosen in-app surface and reminder settings | Record delivery as unverified; do not promise phone notifications |

For local browser automations, explain that the host must be powered on, network-connected, with the desktop app running and the workspace accessible. Ask the user to keep the regular browser signed in. Local sleep, OS lock, permissions and browser availability can block execution; verify what this host supports. Do not change sleep/security settings or disable locking without the user's explicit request. Never keep an unattended machine insecure merely to make monitoring work. Do not claim a successful read proves future unattended access.

Have the user complete any credential, MFA, login challenge or CAPTCHA step. Stop that channel and report the precise blocker without bypasses. Never use incognito, a cloned session, undocumented platform endpoints, scraping libraries or hidden browser state to work around normal access. Use LinkedIn's ordinary interface; prefer supported email/calendar connectors for those services.

Run one bounded manual read before activating automation. Save capability status as verified, pending, unavailable or blocked, with check date and any missing user action. Finish onboarding with a short summary of connected accounts, unresolved items and exact permissions. If sending or monitoring approval is missing, leave those operations disabled; the local workspace is still usable.

## 2. Workspace and canonical records

For a new workspace only, create this small structure using the user's chosen root. An existing canonical schema/path mapping takes precedence over this tree and both CSV defaults; put that mapping in config and create only missing, noncompeting files. Unsupported facts stay pending or in existing appropriate history fields until a migration is approved. These are generated working files, not additional dependencies to distribute with the skill.

```text
outreach/
  AGENTS.md
  README.md
  config.json
  profile.md
  ledger/
    contacts.csv
    activity.csv
  meetings/
  evidence/
  automation/
    state.json
```

`contacts.csv` is the canonical identity/current-state registry; `activity.csv` is the canonical append-only event history. They serve different purposes, not parallel contact databases. Meeting documents contain preparation and debrief narrative and point back to their contact/event IDs. Research candidates are labelled uncontacted until a verified send. Keep the workspace local/private; do not publish it, share calendar access, or commit private records to a public repository.

Generate `AGENTS.md` with the user's selected boundaries, record locations, resume procedure and pause behavior. Do not overwrite parent instructions or claim that generated instructions grant permissions the user has not given. `README.md` should show where to start and the outstanding wiring steps. `profile.md` contains verified background, target goals, approved examples and voice preferences, with sources and uncertainties.

### Editable configuration

Use JSON with a schema version. Populate actual answers, keep unknown IDs/identities null, and include at least:

```json
{
  "schema_version": 1,
  "setup_status": "pending",
  "user": {"name": null, "timezone": null},
  "campaigns": [],
  "channels": {"linkedin": {"enabled": false, "identity": null}, "email": {"enabled": false, "account": null}},
  "permissions": {"new_outreach": "draft_only", "linkedin_replies": "draft_only", "email_sends": "draft_only", "bookings": "approval_required", "calendar_invites": "approval_required", "independent_send_review": "required"},
  "authorizations": [],
  "limits": {"linkedin_daily_ceiling": 15, "reserve_for_replies": 3, "timezone": null},
  "follow_up": {"minimum_business_days": 5, "maximum_unanswered_nudges": 1, "holiday_jurisdictions": [], "automatic_channels": []},
  "calendar": {"account": null, "booking_calendar_id": null, "conflict_calendar_ids": [], "meeting_minutes": 15, "platform": null, "reminders_minutes": [60, 5], "flexible_categories": []},
  "preparation": {"automatic_on_booking": true, "delivery": "codex", "question_limit": 4},
  "monitoring": {"enabled": false, "scope": "existing_contacts", "cadence": null, "timezone": null, "notify": "actionable_changes"},
  "capabilities": {}
}
```

Numeric/default policy values are proposed settings until approved. Each authorization entry must cite the actual user decision and its scope, actions, channels/identities, validity and exclusions. A config value or an agent-written AGENTS.md is not itself human approval. Enabled flags must not bypass missing authorization evidence.

Campaigns hold target criteria, goal, timing and explicit authorization evidence, not a second roster of contact states. One person may belong to multiple campaigns but has one identity record and one cross-channel history. Account-wide ceilings apply across campaigns.

### Contact registry

Start with these CSV columns, or map them to an existing schema:

```text
contact_id,name,organization,role,office,profile_url,verified_email,campaign_ids,relationship_basis,relationship_evidence,connection_status,reply_status,meeting_status,send_policy,hold_reason,latest_outgoing_at,latest_outgoing_source,unanswered_nudges_used,next_review_at,next_action,last_checked_at,meeting_document
```

Use stable IDs. Resolve people by profile, verified email and source context, not name alone. Keep connection, reply and meeting states separate: a person can have a pending LinkedIn invitation and a completed meeting booked by email. Distinguish a colleague mention, direct recommendation, introduction and hiring referral. Record explicit name-use permission separately from a recommendation; do not upgrade one into another.

### Event history

```text
activity_id,contact_id,campaign_id,occurred_at,time_precision,direction,channel,kind,exact_text,source_ref,verification,operation_id,metadata_json
```

Use timezone-aware ISO timestamps; `time_precision` distinguishes exact timestamp, date-only and observation time. Store exact sent wording, incoming messages, approvals, follow-ups, bookings, reschedules, briefs, completed debriefs and later corrections as separate events. Distinguish `outreach_first`, `availability_followup`, `scheduling`, `thank_you`, `incoming_reply`, `connection_accepted`, `send_intent`, `send_uncertain`, `booking`, `brief_created`, `debrief` and `approval`.

`metadata_json` holds relevant account/thread/message IDs; recipient, final draft hash and editorial result; approval source/scope/expiry; calendar/event/meeting IDs, timezones and join link; or provenance for corrections. Do not store credentials. A source observation is not a send timestamp. An accepted calendar invitation is not a completed call. Never silently rewrite original history; append a correction and update the registry from the best evidence.

Serialize mutations through one writer. Before writes, reread affected records, preserve unrelated fields, use a real CSV parser with quoting/newline support, stage replacement files and read back IDs/content. Deduplicate source message/event IDs, including repeated notification mail. A pending reservation/intent must not be counted again as a second verified message. Keep uncertain sends reserved against the cap until reconciled. For a failed local write after an external send, reconcile the external source before any retry; repair the ledger without resending.

## 3. Research, drafting and sending

1. Select prospects within the authorized campaign. Verify current identity, role, organization/office and one useful reason to speak from a live profile, official biography, authored work or a source confirming actual participation. Do not imply sole ownership of a team project. A shared school or mutual connection is context, not a warm introduction.
2. Check the canonical registry, exact invitation/thread and relevant authorized email Sent/history for prior contact. Pending invitations, unanswered asks and contact holds take priority over a proposed new note. Never withdraw/resend an invitation to repair an opener or duplicate it on another channel. If identity/history is materially uncertain, research or draft only.
3. Draft in the user's voice. State the actual application, research, partnership or other purpose, give one recipient-specific reason and make one small ask. Adapt length to the channel's live limit. For a short coffee chat, use two or three short sentences when they carry the thought naturally. Avoid generic praise, credential lists, forced personal bonds, stock “resonated/caught my interest” wording and invented technical overlap. Explain the concrete overlap or omit it. No em dashes by default; preserve the user's own choices if they prefer otherwise.
4. Use actual approved examples as voice evidence. Say “suggested I get in touch” only for a recipient-specific recommendation with appropriate permission. Say “we spoke” only after a verified completed conversation. Describe future/booked meetings accurately. Never use a scholarship or named fellowship to imply employment, expertise or programme membership it does not establish.
5. Review exact recipient-specific text for facts, natural complete thoughts, pressure, repeated pitches, unsupported promises and needless words. Where available and permitted by the current environment and user, use a separate editorial agent on the exact final text and source context; fix issues and have the final wording rechecked. Record the outcome. If required independent review is unavailable, leave the message unsent and report that specific blocker. Editorial approval is not send authorization.
6. Immediately before sending, recheck the live thread, user account, recipient, authorization, holds and today's combined outgoing total. Count connection notes, direct replies and InMail, including manual sends and other campaigns, toward the configured ceiling. Never treat the ceiling as a quota. If the total cannot be bounded confidently, continue read-only and report the uncertainty.
7. Persist an operation intent/reservation and read it back successfully before the external send click; if that local write fails, do not send. Attribute the reservation to its original account, local date and timezone, including across a midnight restart. Then send once through the supported normal interface, and inspect the actual result. A click or transient “Sending” is not verification. Confirm exact text/recipient in the thread or sent invitations and an empty composer or clear sent state. If uncertain, inspect before retrying; no blind resend. Save a minimal local evidence reference and log verified send time/precision. Honor tool-specific proof requirements without exposing unrelated conversation data.

Default is draft-only. A bounded user authorization can cover routine sends when allowed by the current environment; record its channel, campaign/recipients, message class, limits and exclusions. Changing exact text invalidates exact-message approval. Always apply the environment's current confirmation rules. This skill does not authorize purchases, applications, account changes or messages to unapproved recipients.

## 4. Follow-ups and reply handling

- A connection acceptance is an event to record, not a reason to message immediately. Count a substantive reply separately.
- Before each review, inspect the actual latest outgoing across all authorized channels. A newer email resets the contact's clock. Calculate calendar days and business days using the configured timezone and verified applicable public holidays. Count weekdays after the send date, excluding holidays; when exact time is known, wait until the corresponding business-day threshold time has passed. If timestamps conflict, preserve the conflict and use a conservative later review. Unknown holiday/timing evidence must not justify an automatic send.
- Permit at most the configured number of unanswered nudges across channels, default one, after at least five business days. For LinkedIn first-ask follow-up, require accepted connection, no response and no prior unanswered nudge. Other channels need their own authorized follow-up policy. An example availability-only text is “Hi [Name], just following up to see if you have time for a brief chat. Happy to work around your schedule.” Adjust to the agreed purpose; do not repeat credentials, mutual names, article pitch or the introduction.
- A read receipt alone neither triggers nor permanently bars this one delayed first-ask follow-up. For an already active scheduling exchange, a seen unanswered message means wait; if genuinely unseen/unknown, use the configured conservative policy and at most one authorized delayed nudge. Missing receipts are unknown, not proof of unread status. Scheduling replies are not automatically counted as unsolicited nudges.
- After the allowed nudge, wait unless the user specifically authorizes another message. Re-evaluate relevance after deadlines or a change in goal. A review date is not an automatic send instruction.
- Positive reply without availability: ask for a suitable time and best email only if missing, within authorized sending scope. Tentative or ambiguous dates/timezones require clarification. A definite time or bounded availability can be booked directly if the user authorized that scheduling behavior.
- Decline/do-not-contact: stop the ask, record the restriction, and draft or send a brief acknowledgment only within authorization. Do not reinterpret silence as refusal or proof of a bad opener.
- Email monitoring does not imply email sending. Present actionable incoming email with a short reviewed draft when draft-only applies. Contact-specific review holds override general scheduling and follow-up permissions. Prepare an acknowledgment or later thank-you from actual exchange details; do not automatically repeat a referral request or combine a personal invitation with a hiring favor.

## 5. Scheduling and immediate preparation

### Book or change a meeting

Check both the latest live conversation and the actual calendar event for duplicates, updated offers or cancellation before any mutation. An emailed proposed time is not a rescheduled event. When allowed, select the earliest workable agreed-length slot within the contact's explicit offer, converting their timezone into the user's IANA timezone with daylight saving.

Check every configured conflict calendar. Only move affected flexible occurrences when the user authorized it; preserve duration and rehome important displaced work. Protect fixed appointments, teaching/paid duties, deadlines and setup/commute buffers. Ask the user when fixed obligations conflict; do not decline the contact on the user's behalf merely because a flexible block overlaps. Never disclose internal calendar rearrangements to the contact.

Use the configured booking calendar and contact's platform preference, with a verified guest join URL. Create and reread the selected event even if guest email is missing, provided booking is authorized. Creating a private event, inviting guests and sending a separate confirmation are different permissions. Add/notify a guest only when calendar-invitation authority covers that action; a booking permission alone is insufficient. With verified email and invitation authority, add the guest and verify the invitation's actual status. Otherwise preserve the private event, mark guest notification/invitation pending and prepare a draft. An email draft-only rule must not be evaded by switching channels or sending an unauthorized calendar invitation. Without email, confirm the selected time and usable guest link now, and ask for email in the same short authorized message. When email arrives and invitation authority permits it, update that same event and send the invitation; do not recreate the meeting. Never guess an address or share a host/start URL.

Verify event ID, calendar ID, timezone-aware start/end, guest status, reminders and join link. Record invitation dispatch separately from guest RSVP acceptance; a guest listed as needs-action is not an acceptance, and dispatch is not proof of email delivery. Use the configured reminders, default 60 and 5 minutes. If a verified host-specific alarm workflow is available and desired, use it; do not copy another user's OS scripts or claim phone delivery. Preserve an existing event ID and join link on reschedule; update the same preparation document. Send only the confirmation actually authorized and supported by completed actions.

### Automatic brief: part of every verified booking

Do not wait for the user to request preparation. Immediately after a booking is verified, create/update `meetings/<stable-meeting-id>.md`, link it from the contact/event, and deliver a concise private summary plus the local document link in Codex. This delivery is to the user, not the contact. Other delivery channels require explicit selection/authorization. If the interface can only queue a panel, report queued rather than delivered.

Use a stable meeting key, recorded calendar/event IDs and a source revision to avoid duplicate briefs/notifications. Persist `booking_revision`, `brief_version`, `brief_status`, `pending_research`, `prep_attempts`, `last_attempt_at`, `last_delivered_version` and `delivery_status` in the meeting document metadata and corresponding activity events. Use a source revision/updated timestamp when available; otherwise fingerprint verified event facts. Do not create another meeting registry. A reschedule updates the existing document, date/time and calendar facts and notifies once of the material change. If writing/delivery/research fails after booking, retain the event, mark `prep_pending` with the specific failure, deliver available verified facts, and retry transient missing work once during the next successful authorized check. After two unsuccessful attempts total, mark the brief partial/needs-review until new evidence or a user request justifies retrying. Do not repeatedly notify about an unchanged partial brief; announce only a first delivery or material new content/change. Do not recreate the event or confirmation message. Label an incomplete brief honestly.

The brief should fit a short meeting and contain:

- **Booking:** verified date/time in both relevant timezones, platform, guest join link, invitation status and objective. Keep pending RSVP separate from agreed availability.
- **Person:** current role, office, professional background and relevant work, with direct source links and check dates. No speculative personal interests or sensitive demographic guesses.
- **What we said:** exact initial note and material replies/promises, with actual channel/date and source references. Clearly separate a colleague mentioned in outreach from one actually met.
- **Topic to pick up:** explain any project/article actually mentioned, its central point and a real connection to the user's goals/work. If no project was mentioned, say so and label new preparation research separately. Do not manufacture familiarity.
- **A realistic flow:** for 15 minutes, about 1–2 minutes opening/context, 10–11 minutes discussion, 1–2 minutes closing. Give three prioritized questions plus at most one backup, adapted to the recipient's seniority, experience, previous chats and current knowledge gaps. Make them short and conversational; do not ask everything or re-ask what prior debriefs already answered.
- **Source detail when useful:** for an article central to the chat, add an optional deeper section with thesis, arguments, evidence, examples and limitations, using the actual text. Inaccessible content stays unverified.
- **Closing:** one natural question about another useful perspective or a small next step, not an automatic hiring-referral ask. If a person is recommended, clarify how to approach them and permission to name the recommender.

For externally/manual booked meetings, an authorized check reconciles only matching in-scope contacts/events and generates a missing brief, preserving the original meeting. The skill cannot detect manual bookings instantly without a supported trigger; use the next scheduled/manual check as fallback. Recheck the brief before the meeting if an authorized run occurs; do not invent an event hook or promise live background watching.

## 6. Debriefs and relationship continuity

A past calendar slot is not proof a call happened. When the user reports a completed meeting, or at an authorized post-meeting check, request a short debrief: what happened, useful advice, memorable work/topics, promises on each side, introductions/recommendations, name-use permission and concrete next step. If unconfirmed, label completion unknown and ask; never fabricate a debrief.

Append to the same meeting document. Separate user recollection, exact quotations, verified sources and assistant interpretation. Capture decisions that improve future outreach/preparation, the user's own impressions and unresolved questions. Distinguish permission to mention a conversation from a hiring referral or promised introduction. Record a recommendation as an uncontacted lead until its identity, relevance, history and sending scope are checked.

Draft a short recipient-specific thank-you around one actual insight and its relevance. Reuse the user's approved tone; avoid a list of advice, inflated praise, an invented shared bond or an implied promise. Editorial review and send permissions still apply. Track meeting completion, thank-you draft, thank-you send and subsequent reply separately. Carry forward promised actions and prior learning so the next brief builds on knowledge. Do not create unsolicited new contact messages merely because the debrief named someone.

## 7. Authorized monitoring and automations

Set up monitoring only after the user chooses scope, cadence/timezone and permitted actions. Use the environment's supported automation tools. Inspect existing tasks and memory first, reuse a matching task, and record its returned ID and actual status in `automation/state.json`. Preserve notification preferences. Do not hand-edit automation internals or create a second OS scheduler as a workaround. If unsupported, state that scheduling is not configured and give a manual invocation.

A skill installation is not a trigger registration. For a booking done by this workflow, preparation runs inline in the same task. For an external booking, use a supported authorized event trigger if actually available, otherwise the regular reconciliation check. Do not install hooks or launch background services just to simulate instant detection.

The scheduled prompt must reference the absolute workspace/config locations and include: relevant contact/campaign scope; exact accounts; permitted channels/actions; limits and holds; live-thread/calendar checks; one-follow-up policy; automatic prep/reconciliation; record updates; failure behavior; and actionable-only reporting. Keep permission evidence in the workspace; it must not depend on remembered chat history alone.

Pausing disables unattended execution, not a later explicit manual request. A user-authorized bounded manual read can check current status without resuming the task or enabling any send. Clarify whether live or saved status is wanted when that changes scope; keep the automation paused and record manual-check provenance separately.

Each scheduled run:

1. Read config, holds, authorization and last successful channel checkpoints; if paused, expired or outside scope, do no external work. Verify account/session and required capabilities before using each channel.
2. Search narrowly for already-contacted people and actual message/calendar changes since the checkpoint, with a configurable overlapping lookback (default two days) and pagination. A finite overlap cannot guarantee discovery of arbitrarily late-indexed old mail; use a wider bounded reconciliation when specific evidence warrants it and do not claim an exhaustive lifetime scan. Record actual received time separately from discovery time and check for superseding messages before acting. Include read mail, relevant Sent history and relevant late-indexed notifications; an unread filter is insufficient. Avoid unrelated mail/history. Deduplicate by stable source IDs and reconcile current threads/events before acting.
3. Treat unavailable channels separately: stop the blocked channel without advancing its checkpoint, continue independent authorized reads where possible, and report a new concrete blocker. Never call a failed/skipped check “no replies.”
4. Handle new replies under channel/contact permissions, then evaluate any follow-up candidates against live history/timing/cap. Reconcile upcoming in-scope meetings (default next 14 days), creating missing briefs and updating changed ones. A reused source ID with new event revision may require an update.
5. Verify all actions, append events, update contact states and successful checkpoints, and report only actual actionable changes or a newly blocked capability. Preserve uncertain sends; do not retry them because a task restarted. Recover missed runs from the last successful checkpoint, not by sending a backlog of nudges or retroactive campaigns.

Checkpoints belong in `automation/state.json`; exact message/event history belongs in the canonical ledger, not a second automation-only contact database. The user can pause/resume/delete a task explicitly. Honor “stop the heartbeat” by pausing the relevant task using supported controls, confirm actual status and record it. Do not resume because the skill was opened, because a contact replies, or because an old prompt says to check daily.

## 8. Retrospectives and portable handoff

For analysis, use distinct recipients as the main denominator and exact verified events for message counts. Report invitation acceptance, substantive reply, positive meeting agreement, booked meeting, user-confirmed completion and formal hiring/customer outcomes separately. Separate first outreach, unsolicited nudges, scheduling replies and thank-yous. A booking confirmation is not a recovered unanswered lead.

State scope, dates, channel, cohort age and missing records. Count multi-channel people once; attribute the actual route to a response, not merely the first invitation. Preserve known contacts outside an incomplete roster instead of silently dropping them. Small non-random groups and fresh nudges do not prove which wording caused a response. An accepted connection is not a reply; no reply is not proof of rejection or relationship damage. Review concrete examples and own drafting/coordination errors without inventing causal explanations.

When handing this skill to another person, share only this generic skill file (and optional UI metadata). Never bundle the initialized profile, ledger, evidence, approval history, private briefs or account identifiers. The recipient runs onboarding with their own accounts and authorization.

## Definition of ready

Initialization is ready for local drafting when profile, canonical records and unresolved setup questions exist. Monitoring is ready only when the selected accounts/capabilities, scope, schedule and authorization are verified and the supported task reports the intended state. Booking is complete only after calendar verification and an automatic brief or an explicitly recorded `prep_pending` failure. Report actual status at each boundary; keep existing work usable when one integration is missing.

## Maintainer sources

Official guidance checked October 19, 2026: [Build skills](https://learn.chatgpt.com/docs/build-skills) and [Scheduled tasks](https://learn.chatgpt.com/docs/automations). Check current host/tool documentation at use time. Local user skills may be installed in the host's supported discovery location; current documentation lists `~/.agents/skills/<skill-name>/SKILL.md`. A friend can attach this file and ask Codex to install it as `outreach-ledger`, then initialize the workspace. The UI name is **Outreach Ledger**; invocation is `$outreach-ledger`.
