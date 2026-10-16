# Engineering Leadership Playbook

How I hire, onboard, grow and lead engineering teams: rubrics, templates, a blameless post-mortem and an AI-tooling rollout playbook.

This is the working version of how I run a team after 7+ years of engineering management (12+ years in tech), including a peak of 12 direct reports and about 24 people managed over my tenure. Everything here is genericized. There are no names, no client internals and no employer-specific material.

## How I run a team

**1. Clear ownership, written specs, early feedback.**
Every engineer knows what they own and what "done" means. Feedback arrives while it is still cheap to act on, not at review time.

**2. Hire slowly, on written evidence.**
Each hiring decision has a written rationale. See [`hiring/`](hiring/).

**3. Make the first 90 days explicit.**
A new hire should never have to guess what good looks like. See [`onboarding/30-60-90.md`](onboarding/30-60-90.md).

**4. Talk to people regularly, and review them twice a year.**
Monthly 1:1s keep problems small. Twice-yearly reviews tie salary movement to growth in scope, responsibility and impact. See [`one-on-ones.md`](one-on-ones.md) and [`performance-and-promotion.md`](performance-and-promotion.md).

**5. Treat incidents as system failures, not people failures.**
Blameless, written, with actions that have owners. See [`incidents/ddos-postmortem.md`](incidents/ddos-postmortem.md).

**6. Adopt new tooling through the normal process, and measure it.**
Start from everyday tasks, keep the tooling inside the existing development process, and judge it by delivery metrics. See [`ai-adoption/claude-code-rollout.md`](ai-adoption/claude-code-rollout.md).

**7. Stay close enough to the work to be useful.**
I stay hands-on for roughly 10-20% of my time: code review, architecture decisions and incident work.

## Track record behind this playbook

| Area | Result |
|---|---|
| Span of control | Peak 12 direct reports (3 senior engineers, 4 mid engineers, 3 QAs, 2 DevOps); ~24 managed over the tenure |
| Hiring | 9 hires from ~36 candidates and ~45 interview rounds; every offer accepted |
| Growth | 8 promotions across three tracks (mid to senior engineer, QA to automation QA, QA to project management) |
| Reviews | Twice-yearly performance and compensation reviews; 12+ cycles run in my own line |
| Incidents | Service restored within 2 hours of an extortion-driven DDoS; $0 ransom paid |
| AI adoption | Claude Code rolled out across 2 engineering teams: cycle time -22%, PR throughput +40% |

## Contents

| Path | What it is |
|---|---|
| [`hiring/`](hiring/) | Interview loop, scorecard and rubric |
| [`onboarding/30-60-90.md`](onboarding/30-60-90.md) | 30/60/90-day plan template |
| [`one-on-ones.md`](one-on-ones.md) | How I run 1:1s, with a template |
| [`performance-and-promotion.md`](performance-and-promotion.md) | Review cycle, levels and promotion criteria |
| [`incidents/ddos-postmortem.md`](incidents/ddos-postmortem.md) | Blameless post-mortem of a DDoS incident |
| [`ai-adoption/claude-code-rollout.md`](ai-adoption/claude-code-rollout.md) | Rolling out an AI coding agent to engineering teams |

## License

Text is released under [CC BY 4.0](LICENSE). Use it, adapt it, and keep the attribution.
