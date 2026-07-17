# The War Game Prompt

Plan a full build of [PROJECT], but do it as a war game. Do not assume you can get from A to B on the happy path.

## What we're building

A chat agent that lives on my website with floating quick-action tabs above the widget (for example "Walk me through the website"). Picking a tab starts a guided tour that navigates real pages and subpages, narrates as it goes, and asks the visitor questions to gauge fit. When buying signals appear, it naturally introduces what we offer, my credentials, and our [workshops/services], then captures a lead. It adapts as the conversation goes, nothing cookie-cutter. Brain = [Claude Haiku] called from [Supabase Edge Functions], with every conversation stored in [Supabase Postgres]. The browser never touches the model API directly.

## How to plan it

- Break the build into phases. For each phase give the objective, an optimistic assumption, a pessimistic assumption, the most likely failure modes with fixes, verifiable exit criteria, an alternative path if the main route fails, a stop condition (the situation where execution must halt instead of improvising a way through), and a take budget.
- Add a master table of every failure scenario you can foresee (infra, model API quirks, frontend, conversation quality, security, learning loop) with detection and recovery for each.
- Call out exactly where the [Claude] API differs from [OpenAI] habits so nothing gets ported blindly.
- Design a weekly self-review loop that (1) scans all conversations for prompt injection and (2) adapts the agent's speaking style to its real visitors within hard bounds, so it improves over time without ever losing core professionalism. No change ships without a regression eval and my explicit approval.

## Deliverables

1. A markdown plan written for a cold-start agent with none of this context, including a preamble, the critical path, stack, structure, and methodology.
2. A visual HTML version of the same plan with generated diagrams for the architecture and each phase.

Assume you will hit barriers no matter how intelligent you think you are. Plan for them before writing a single line of code.
