# Post-mortem: extortion-driven DDoS outage

**Format:** blameless. This document is about how the system and the process behaved, not about who is at fault. Names, clients and internal details are omitted.

**Status:** generic summary of a real incident. Items marked `TODO(me)` are details I still need to add or confirm before publishing.

## Summary

A production platform came under an extortion-driven DDoS attack, with a demand for payment to stop. The service went down. We refused the ransom, mitigated at the edge with rate-limiting and web-application-firewall rules, restored service within 2 hours, and kept it stable through the remainder of an attack that lasted around 24 hours. No ransom was paid.

## Impact

| Item | Detail |
|---|---|
| Duration of full outage | Restored within 2 hours |
| Duration of attack | ~24 hours |
| Malicious requests blocked by WAF rules | 20M+ |
| Ransom paid | $0 |
| Data loss or breach | `TODO(me)`: confirm "none" |
| Customer-facing impact | `TODO(me)`: describe in generic terms |

## Timeline

Times are relative to the first alert (T+0). `TODO(me)`: fill in the actual sequence from your notes; the structure is here.

| Time | Event |
|---|---|
| T+0 | Monitoring shows a traffic spike and failing health checks; first alert |
| T+? | Extortion message received; the decision on the ransom is taken (see below) |
| T+? | Incident channel opened; roles assigned |
| T+? | Edge rules added: rate-limits, geo and signature-based WAF rules |
| T+<2h | Service restored |
| T+~24h | Attack ends |
| T+? | Hardening and follow-up work begins |

## What went well

- **Clear decision on the ransom, early.** We decided not to pay in the first hour, and it did not come back as a question. Paying marks you as a target.
- **Roles were explicit.** One person ran the incident, one made the technical changes, and one handled communication. The incident lead did not debug.
- **WAF rules worked.** Managed and custom rules blocked 20M+ malicious requests while legitimate traffic still got through.
- **Communication was honest and regular.** Short updates at a fixed interval, even when the update was "no change".
- **We kept making changes small and reversible.**

`TODO(me)`: confirm each bullet matches what actually happened; delete any that do not.

## What went badly

- **Mitigation was not ready.** The edge protection that stopped the attack was configured during the incident, not before it.
- **Detection was by symptom.** We noticed because the site was failing, not because an alert on abnormal traffic had fired.
- **The runbook did not exist.** Decisions that should have been a checklist were improvised.
- `TODO(me)`: add anything else that was honestly bad, and confirm the three above.

## Contributing factors

Blameless post-mortems look for conditions, not culprits:

1. The platform had a public origin that could be reached directly, so edge protection could be bypassed.
2. No baseline of normal traffic meant no meaningful anomaly alert.
3. Ownership of DDoS response was not written down anywhere.
4. A single on-call person carried the whole response in the first hour.

`TODO(me)`: confirm these against what happened.

## Decisions

| Decision | Reasoning |
|---|---|
| Refuse the ransom | Payment does not end an extortion attempt and rewards it. Our mitigation options were credible. |
| Mitigate at the edge, not at the application | The application cannot absorb volumetric traffic. Block before it arrives. |
| Prefer reversible changes | Wrong rules blocking real users is also an outage. |
| Keep a written log during the incident | It makes the timeline in this document possible, and it protects against fatigue. |

## Action items

| # | Action | Owner | Due | Status |
|---|---|---|---|---|
| 1 | Lock down the origin so only the edge network can reach it | Infra | `TODO` | `TODO` |
| 2 | Keep baseline WAF and rate-limit rules deployed permanently, not only in an incident | Infra | `TODO` | `TODO` |
| 3 | Alert on abnormal traffic volume and error rate, not only on downtime | Infra | `TODO` | `TODO` |
| 4 | Write and rehearse a DDoS runbook, including the ransom decision | Engineering manager | `TODO` | `TODO` |
| 5 | Add a second trained responder to the on-call rota | Engineering manager | `TODO` | `TODO` |
| 6 | Agree a customer-communication template | Engineering manager | `TODO` | `TODO` |

## Lessons

1. **Decide the ransom policy before the incident.** A decision made calmly is better than one made at 3 a.m.
2. **Protect the origin.** Edge mitigation only works if there is no way around it.
3. **Separate the roles.** The person managing the incident should not be the person typing commands.
4. **Prepare for the dull parts.** Updates, logs and handovers decide whether the second night goes better than the first.
5. **Look after the people.** After a 24-hour event, give time off and say thanks.

## Blameless review process

How I run these:

1. Hold the review within a week, while memory is fresh.
2. Everyone involved attends; the facilitator is not the incident lead.
3. Build the timeline first, from logs and chat, before discussing causes.
4. Ask "how did it make sense to do that at the time?", never "why did you do that?"
5. Every action item has one owner and a date, and is tracked until it is closed.
6. Publish the post-mortem to the whole engineering team.

## Template for future incidents

```
Title:
Date / duration:
Severity:
Summary (3 sentences):
Impact:
Timeline:
What went well:
What went badly:
Contributing factors:
Decisions and reasoning:
Action items (owner, date):
Lessons:
```
