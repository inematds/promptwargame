# The Mass War Game

The war game prompt takes **one** project apart in depth. This mode takes **many at once** and answers the question the other one can't: _I have N stalled projects — which do I build first, which do I simplify, which do I kill?_

Use it when you have many projects, ideas or systems to compare, and you want the expensive model to do only the **thinking** — leaving execution to a cheap model following a plan that has already been chewed through.

The goal here is **not to execute**. It's to understand, compare, anticipate and prioritize.

---

## 1. Folder structure

```
project-analysis/
├── projects/
│   ├── project-01.md
│   ├── project-02.md
│   └── project-03.md
├── results/
├── general-context.md
├── criteria.md
├── ledger.md
├── assumptions.md
└── master-prompt.md
```

| File | Role |
|---|---|
| `projects/` | One file per project. Never merge several into one — it blends context and ruins the comparison. |
| `results/` | Receives the generated analyses. |
| `general-context.md` | What holds for all of them: scenario, resources, constraints. |
| `criteria.md` | The same criteria applied to every project — this is what makes comparison possible. |
| `ledger.md` | Blockers: missing information, pending decisions, access needed. |
| `assumptions.md` | Everything the AI had to assume, with the impact of being wrong. |
| `master-prompt.md` | The command that runs the mass analysis. |

`ledger.md` and `assumptions.md` are what keep the analysis from turning into fiction. Without them the model invents whatever is missing so it can keep going.

---

## 2. Per-project briefing

Minimal version — start here when you know little:

```markdown
# Project — Name

## What is it?
## What do I want to achieve?
## Where does it stand today?
## What problem am I solving?
## What would success look like?
```

Full version — once the project has substance, add:

```markdown
## Who is it for?
Who uses, buys or benefits from it.

## Known problems
The ones you've already noticed.

## Available resources
What already exists: team, code, domain, database, servers, content,
customers, community, budget, AI models, APIs.

## Constraints
What must be respected: budget, deadline, team size, mandatory technology,
privacy, must run locally, avoid expensive services.

## Specific ask
What you want out of this analysis.
```

Leave blank whatever you don't know. The AI logs it as a blocker — don't fill it with a guess.

---

## 3. `general-context.md`

```markdown
# General Context

## Objective
Analyze several projects to identify improvements, risks, priorities and opportunities.

## Current situation
[Describe the landscape: how many projects, at what stages, what already runs in production.]

## Available resources
[Team, AI models, infrastructure, channels, budget.]

## General constraints
- reduce cost
- prefer simple solutions
- reuse what already exists
- avoid dependencies that are hard to maintain
- never invent information: log questions and blockers

## Desired result
An individual analysis per project plus a general comparison that allows deciding
what to execute first, what to simplify, what to automate, what to pause and
what to abandon.
```

---

## 4. `criteria.md`

The same criteria for every project — always.

```markdown
# General Analysis Criteria

## Substance
- Clarity: is the project unambiguously defined?
- Problem: is a real problem being solved?
- Audience: is it clear who it was built for?
- Value: does it create enough value for the user?
- Edge: does it beat the existing alternatives?

## Execution
- Feasibility: can it be built with the resources that exist today?
- Complexity: is it more complex than it needs to be?
- Bottleneck: what is the single factor blocking progress?
- Simplification: what can be removed?
- Automation: which tasks can be automated?

## Risk
- What could stop this from working?
- Security: any data, permission or access risk?
- Maintenance: will it be easy to maintain once shipped?
- Scalability: can it grow without blowing up the cost?

## Return
- Revenue: how does it generate financial return?
- Cost: which costs can be cut?

## Final classification
- impact: high / medium / low
- effort: high / medium / low
- risk: high / medium / low
- priority: do now / do later / study further / pause / abandon
```

---

## 5. `ledger.md` and `assumptions.md`

Seed both like this:

```markdown
# Blocker Ledger

Logs: missing information, pending decisions, access needed,
missing permissions, external dependencies, unresolved risks.

## Blockers found
None logged so far.
```

```markdown
# Assumptions

For each assumption: related project, the assumption, why it was made,
impact if wrong, how to verify.

## Assumptions logged
None logged so far.
```

When information is missing, the AI must write it at the exact point where it would have mattered:

```
[NEEDS_DEFINING: available monthly budget]
```

---

## 6. Master prompt

```markdown
# Master Prompt — Mass Analysis

You are a technical, operational and business strategist.

There are several projects in the /projects folder. Your mission is to analyze
all of them in bulk.

You must NOT execute the projects.
You must NOT alter the original files.
You must NOT code or implement solutions at this stage.

Your job is to analyze, criticize, compare, simulate and prepare improvement plans.

Read: every file in /projects, /general-context.md, /criteria.md,
/ledger.md and /assumptions.md.

For each project, create /results/result-project-NN.md containing:

1. project summary
2. general diagnosis
3. the real problem being solved
4. strengths
5. weaknesses
6. biggest bottleneck
7. invisible or undeclared problems
8. opportunities
9. quick wins
10. structural improvements
11. what can be removed or simplified
12. what can be automated
13. technical, business and operational risks
14. external dependencies
15. missing information
16. phased execution plan
17. execution war game
18. validation checklist
19. final recommendation
20. which AI model should execute it

Classify every recommendation by impact, effort, risk and priority using the
scale in /criteria.md.

## War game format

For each move in the plan:

### Action
What must be done.
### Expected result
What happens if it works.
### Success signal
What evidence confirms it worked.
### Failure signal
What evidence shows it didn't.
### Likely cause
The most likely cause of that failure.
### Counter-action
What to do to fix it.
### Alternative path
Which route to take if the fix doesn't resolve it.
### Stop condition
The situation where execution must halt instead of improvising.

## Order of work

First produce a first pass over ALL projects.
Do NOT polish the first project before analyzing the rest.
Only once every first pass exists, go back and revise each one.

Update /ledger.md whenever you find missing information, a pending decision,
a blocker, needed access or an unresolved risk.

Update /assumptions.md whenever you have to assume something.

Do not invent facts. If something isn't available, log it plainly.
Be critical, direct and specific. No generic recommendations.

## Final comparison

Once the individual analyses are done, create /results/general-summary.md
comparing every project:

1. overall ranking
2. highest potential
3. lowest effort
4. highest risk
5. fastest return
6. most complex / easiest to execute
7. what to do first
8. what to pause
9. what to abandon
10. projects sharing resources
11. possible integrations between projects
12. shared dependencies and bottlenecks
13. recommended 30-day plan
14. recommended 90-day plan
```

---

## 7. Revision prompt (second pass)

The first pass almost always comes out generic. Run this over it:

```markdown
Review every file in /results.

For each report, find and fix:

1. generic recommendations
2. contradictions
3. ignored risks
4. unidentified dependencies
5. steps with no validation
6. actions with no stop condition
7. assumptions used but never logged in /assumptions.md

Deepen the war game. Make the recommendations more practical.
Update the ledger and the assumptions.
Do not remove useful information.
```

A third pass, if any, should look only at the priority projects.

---

## 8. Execution prompt (one project at a time)

Analysis can be done in bulk. **Execution cannot.** Pick one project and hand the executor: the original briefing, the analysis, the war game, the success criteria, the updated ledger.

```markdown
You are the executor of this project.

Read: the original briefing, the analysis, the war game, the success criteria
and the updated ledger.

Follow the war game move by move. Before each step:
1. confirm the prerequisites
2. execute the action
3. verify the expected result
4. look for the success signal
5. look for failure signals

If a failure occurs:
1. identify the likely cause
2. apply the counter-action
3. test again
4. use the alternative path if needed

If you hit a stop condition:
- halt execution
- do NOT invent a solution
- log the blocker
- explain what is needed to continue

When finishing: run the checklist, validate the results, and report what was
completed, what is still pending, and which risks remain.
```

---

## 9. Which model for which stage

| Stage | Model |
|---|---|
| Strategic analysis, risks, invisible problems, war games, comparison, critical review | The most capable |
| Organizing documents, turning analysis into tasks, consistency review | Mid-tier |
| Executing well-defined tasks, editing files, writing docs, tests, following checklists | The cheapest |

The logic: **the advanced model thinks and anticipates, the mid-tier organizes, the cheap one executes.**

This is where the method pays for itself — the expensive model is spent only on the part that requires anticipating what will go wrong.

---

## 10. Mistakes that kill the method

- **All projects in a single file.** Blends context, destroys the comparison.
- **A different prompt per project.** With no shared criteria there is no ranking.
- **Asking for analysis and execution at once.** The AI starts implementing before it understands.
- **Not defining success.** The model can't tell when it's done.
- **Not logging blockers.** It invents the missing information so it can keep going.
- **Polishing project 01 before looking at the rest.** Burns the budget on whatever happened to be first in line.
- **Accepting generic analysis.** Demand classification by impact, effort, risk and priority.
- **Executing everything at once.** Analysis is bulk; execution is prioritized, one at a time.

---

## Full flow

1. **Preparation** — build the structure, one file per project, context, criteria, ledger, assumptions.
2. **Mass analysis** — run the master prompt, generate a first pass over all of them.
3. **Revision** — second pass: hunt the generic, the contradictory, the ignored risk, the action with no stop condition.
4. **Comparison** — ranking, priorities, 30- and 90-day plans.
5. **Execution** — one priority project, move by move, on the cheap model.
6. **Learning** — after executing, update the briefing, analysis, ledger, assumptions and war game.

The principle: **don't use AI just to tell you what to do.** Use it to simulate what will probably happen, how you'll know it worked, what can go wrong, why, how to react, and when to stop.
