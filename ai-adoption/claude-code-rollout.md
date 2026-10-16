# Rolling out an AI coding agent (Claude Code)

A playbook for introducing an AI coding agent to engineering teams. It comes from rolling out Claude Code workflows across 2 engineering teams, from 2025 to early 2026, reinforced with 2 internal tech talks for ~50 engineers.

## Results

| Metric | Change |
|---|---|
| Cycle time | **-22%** |
| PR throughput | **+40%** |
| Adoption | Agents became part of daily development in both teams |

Cycle time is measured from ticket start to done.

## Principles

1. **Start from everyday tasks, not from the tool.** Look at what each team does every week (tests, refactors, migrations, bug triage, documentation) and show the agent doing that.
2. **Keep it inside the normal process.** Agent-written code goes through the same review, tests and CI as everyone else's. No special lane.
3. **Measure delivery, not enthusiasm.** Judge by cycle time, throughput and quality, not by usage counts.
4. **Raise the bar on review.** Faster code generation moves the bottleneck to review. Plan for that load.
5. **Treat security and quality as first-class.** Faster generation brings more risk, not less.
6. **Teach context engineering.** Results depend far more on the context you give the agent than on the model.

## Phases

### Phase 0: Baseline (1-2 weeks)

- Pick the metrics: cycle time, PR throughput, change failure rate, review time.
- Record the baseline before anyone changes how they work.
- Survey the team: current tool use, concerns, enthusiasm.
- Agree the guardrails with security (what data can be sent, which repos, which accounts).

### Phase 1: Pilot (3-4 weeks)

- Choose 3-5 engineers from one team, including a skeptic.
- Pick bounded, real tasks: test writing, small features, bug fixes, migrations.
- Hold a weekly 30-minute retro: what worked, what failed, what to put in the shared instructions.
- Create the first project-level instruction file for the agent (`CLAUDE.md`-style): build commands, conventions, boundaries.

### Phase 2: Enable the team

- Run a **hands-on session** on the team's own codebase, not a slide deck.
- Publish a short guide: prompts that worked, anti-patterns, review checklist for agent-written code.
- Set up shared building blocks: project instructions, commonly used skills and tool integrations (MCP), permission settings.
- Name a **champion** per team who answers questions.

### Phase 3: Scale

- Roll out to the second team using the first team's playbook and champion.
- Hold two internal talks to reach the wider engineering group (~50 engineers):
  1. *Prompt engineering: getting reliable results from LLMs.*
  2. *Claude Code in practice: context engineering, MCP and skills.*
- Collect shared instructions and skills into a repository that anyone can contribute to.

### Phase 4: Make it normal

- Review the metrics monthly against the baseline.
- Update the review checklist as new failure patterns appear.
- Fold agent usage into onboarding ([`../onboarding/30-60-90.md`](../onboarding/30-60-90.md)).
- Retire practices that no longer pay for themselves.

## Guardrails

| Risk | Control |
|---|---|
| Sensitive data sent to a vendor | Written policy on what may be shared; enterprise or zero-retention terms; no secrets in prompts |
| Secrets committed | Secret scanning in CI; pre-commit hooks |
| Subtly wrong code | Tests required; the author is responsible for every line, whoever or whatever wrote it |
| Review overload | Smaller PRs; reviewer checklist; budget review time as part of capacity planning |
| Dependency and licence issues | Same dependency review as any other change |
| Skill atrophy | Keep pairing and design discussions; juniors explain their changes |
| Over-trust | Read the diff; run the tests; do not approve what you do not understand |

## Review checklist for agent-written code

- [ ] Do I understand what this change does and why?
- [ ] Is the scope right, with no unrelated edits?
- [ ] Are there tests, and do they test behavior rather than the implementation?
- [ ] Are errors, edge cases and security inputs handled?
- [ ] Does it follow the existing conventions, or does it invent its own?
- [ ] Does it add dependencies, and are they justified?

## Handling resistance

- **"It writes bad code."** Show the pull requests from the pilot. Ask which part is bad, then fix the instructions.
- **"I'll be replaced."** Be honest: expectations of what a team can ship are rising, and engineers who use the tools well are more valuable. Invest in their growth.
- **"I'm faster without it."** Maybe, for that task. Ask them to try it on tests, migrations or documentation first.
- **"It's a security risk."** It can be. That is why the guardrails come first.

## What I would do differently

- **Start measuring earlier.** Capture a clean cycle-time and throughput baseline before the pilot starts, so the effect of the agent can be separated from other changes.

## Metrics dashboard (suggested)

| Metric | Why |
|---|---|
| Cycle time (ticket start to done) | Headline measure of flow |
| PR throughput per engineer per week | Output, read together with quality |
| Review time and queue length | Where the bottleneck moves |
| Change failure rate / reverts | Quality guard |
| Team sentiment (short survey) | Adoption health |
