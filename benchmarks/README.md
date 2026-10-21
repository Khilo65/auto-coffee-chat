# Benchmarks

Share aggregate results from your own version of Auto Coffee Chat and compare them using the same definitions. Start with the [historical baseline](results/historical-baseline.json), then copy the [submission template](result-template.json).

The baseline comes from the earlier outreach workflow, which included manual work. It predates the packaged skill and is a descriptive starting point. A higher rate in another campaign does not establish that an automation change caused the difference.

## Historical baseline

| Measure | Numerator / denominator | Rate |
| --- | --- | --- |
| Invitation acceptance | 11 / 48 invitation recipients | 22.9% |
| Substantive LinkedIn replies | 4 / 53 contacted people | 7.5% |
| Substantive replies across approved channels | 5 / 53 contacted people | 9.4% |
| People with a booked coffee chat | 5 / 53 contacted people | 9.4% |
| People with a completed coffee chat | 5 / 53 contacted people | 9.4% |
| Booked meetings completed as of the cutoff | 5 / 5 booked meetings | 100.0% |

The cohort contains 48 connection-note recipients and five InMail recipients. Those groups describe each person's first outreach channel. One response arrived by email after a genuine recommendation, so acceptance and meeting outcomes are not a single nested funnel. No substantive InMail replies were observed among the five InMail recipients.

First-contact ages were approximately 8–19 calendar days at the snapshot, based on recorded dates with some timestamp uncertainty. Recent follow-ups had less time to receive replies. Exact dates, sender details and target organization are withheld. Four additional approaches had incomplete logs or different scope; the wider 5/57 result is documented as a caveat, not mixed into this cohort.

There are three known premature follow-ups that repeated the original pitch. We do not have complete action totals to calculate an overall automation error rate. Formal hiring-interview and job-offer outcomes are unknown. Unknown values are `null`, never invented zeros.

## Submit your results

1. Copy `result-template.json` to `results/<short-neutral-run-id>.json`. Use a new filename for each run or later observation cutoff. Do not put a person, employer, email address or account identifier in the filename.
2. Fill in the fields below from your private ledger. Submit aggregate counts only. Keep `null` for unknown or inapplicable values, and explain important gaps in `notes` or `limitations`. Empty incident lists mean no incidents were listed, not proof that none occurred.
3. Check the arithmetic, cohort membership and private source records locally. Check every public field and Git commit identity for private data before staging. Do not attach your ledger, messages, screenshots, notebook, event links, credentials or private configuration.
4. Open a pull request with the result file, the implementation change you evaluated, and the comparison you think is justified. Fork the repository if you do not have write access. Results are reviewed community reports, not independently verified certifications.

Benchmarking does not authorize new outreach, extra follow-ups or monitoring. Collect results from work you have permission to do; retain the same privacy and sending restrictions.

## Fields to fill in

| Field | What to report |
| --- | --- |
| `schema_version` | Keep `1` for this format. |
| `submission_id` | A short neutral unique ID matching the filename. |
| `result_type` | `observational`, `controlled_experiment`, or `synthetic_workflow`. The supplied baseline uses `historical_observational`. Keep synthetic results separate from real outreach outcomes. |
| `implementation` | Public repository URL and full commit SHA for the version used, a non-sensitive automation revision, what changed, and `manual`, `automated` or `hybrid` execution. Use `null` if a historical version cannot be established. Never include a private automation ID or full account-specific prompt. |
| `cohort` | Purpose, broad target context, inclusion/exclusion rules, and aggregate relationship mix. Count cold, direct recommendation/introduction, and other relationship groups once each at first contact; leave unknown counts `null`. Acceptance alone does not create a warm relationship. |
| `observation` | First-contact date range, snapshot date, IANA timezone and observation method. Use `fixed_window` with a stated number of calendar days after each person's first outreach, or `mixed_age_snapshot` with the cohort age range and caveats. Exact dates can be withheld for privacy if you report enough relative timing to explain maturity; disclose the resulting comparison limit. |
| `policy` | Daily ceiling, minimum business days before a follow-up, maximum unanswered nudges, and any changes or deviations. A chosen daily cap is not a platform allowance. |
| `counts` | Unique people and actual meeting/action totals, using the definitions below. Count both positive and negative substantive replies. |
| `automation_quality` | Audit coverage (`complete`, `sampled` or `partial`), reviewed operation counts, detected errors, checked bookings and complete briefs. A sample applies only to the reviewed operations. Keep total error counts unknown unless the coverage supports them. |
| `evidence` | Evidence level, what was checked locally, and source limitations. `public_raw_data` must stay `false`; this format publishes aggregates only. Do not expose private provenance paths or contact identifiers. |
| `comparison` | Reference submission ID, comparison design and limitations. Explain differences in recipients, relationships, channels, timing and manual assistance. |

The template has the same field structure as the baseline. It is a reporting convention, with no automated validator or leaderboard. Keep counts as nonnegative integers or `null`. Use empty arrays only where a list has no entries; required descriptive fields must be filled in before submission. Additional aggregate metrics need a definition, denominator, observation window and privacy review in the pull request.

## Counting and calculations

Choose the cohort before inspecting outcomes and include nonresponders. Deduplicate people across channels. `initial_channel_people` partitions the cohort by first verified outreach channel; a later email does not create another person. Its known counts must sum to `contacted_people` when that partition is complete. Relationship groups likewise sum to the cohort when fully known.

A substantive reply is a human response that answers the request, supplies useful information, offers availability or declines. Connection acceptance, reactions, read receipts and automated replies do not count. `substantive_linkedin_reply_people` includes replies to either LinkedIn connection notes or InMail; `substantive_reply_people_any_channel` counts each person once across selected channels.

Count a person once in `booked_chat_people` when a meeting is verified booked, and once in `completed_chat_people` when completion is user-confirmed. Multiple meetings with that person increase meeting counts, not person counts. Rescheduling the same meeting does not create another booking. Count all bookings and their completions in the same submitted cohort and observation window; do not remove cancellations or no-shows to improve the rate. A future booking has not completed yet, so disclose meetings still pending before comparing completion rates.

A formal hiring interview is a separate recruitment stage. A coffee chat is not a hiring interview. `outgoing_messages` counts verified individual notes/messages, including scheduling and thank-yous, only when the complete cross-channel history is available.

Calculate rates from the counts, without storing rounded rates as a second source of truth:

- Acceptance = `accepted_invitation_people / invitation_recipients × 100`.
- Reply = `substantive_reply_people_any_channel / contacted_people × 100`.
- Booked-chat conversion = `booked_chat_people / contacted_people × 100`.
- Completed-chat conversion = `completed_chat_people / contacted_people × 100`.
- Meeting completion as of cutoff = `completed_meetings / booked_meetings × 100`.
- Reviewed duplicate-send rate = `duplicate_send_operations / send_operations_reviewed × 100`.
- Reviewed unauthorized-send rate = `unauthorized_send_operations / send_operations_reviewed × 100`. For both error rates, the numerator and denominator must cover exactly the same reviewed operations. Error categories can overlap; do not add their rates.
- Prep coverage = `complete_prep_briefs / bookings_reviewed_for_prep × 100`. A complete brief has verified booking details, sourced background, actual outreach context and tailored questions.

An unknown numerator or a null or zero denominator gives **N/A**, never 0%. Round percentages to one decimal place for display. Overlapping measures cannot be added together. People counts for acceptance and replies cannot exceed their eligible denominator, and completed meeting counts cannot exceed bookings. Compare rates with percentage-point change: `new rate − reference rate`. Report both counts beside the difference. For illustration, an invented 10/100 result compared with 5/53 is approximately +0.6 percentage points; the illustration is not an observed result or evidence of improvement.

## What counts as improvement

For useful comparisons between future versions, use the same outcome definitions and a common observation rule, such as outcomes within 14 calendar days of first outreach. Include only people whose full window has elapsed, apply the same rule to both cohorts, and count outcomes only within that window. State how many people were not yet eligible. Keep target context, initial channel, relationship mix and manual assistance comparable, or report the differences.

Our historical baseline cannot be reconstructed as a uniform 14-day result from the published aggregates. Compare it descriptively. A different sector, more warm introductions or a longer wait can change the result without a better automation.

Measure reliability separately from replies. Better duplicate prevention, fewer unauthorized sends and more complete meeting briefs can improve the workflow even before outreach conversion changes. Count errors against audited operations; missing records do not demonstrate zero errors. Synthetic scenarios can check follow-up timing, uncertain-send recovery, rescheduling and prep creation, but their pass rates are separate from real response rates.

A controlled comparison needs an actual allocation method and comparable observation windows, disclosed before making a causal claim. Do not send duplicate versions to the same person to run a comparison. Every live action still needs the user's authorization. There is no universal score or ranked leaderboard for unlike campaigns.
