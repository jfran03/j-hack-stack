# j-hack-stack
(Because I felt like Garry Tan making gstack)

A structured workspace for running hackathons end-to-end with an AI agent. Three stages. One project brief. A wiki that compounds across every event.

No orchestration framework. No custom tooling. Just markdown files and a folder structure that tells the agent what to do.

---

## The Problem This Solves

Hackathons are won or lost on context management. Teams lose time re-validating ideas that should have been cut in hour one. Developers build the wrong thing because the brief drifted and nobody noticed. The pitch undersells the product because the storytelling happened last-minute with no grounding in what was actually built.

And after the event, all of that hard-won knowledge — which judges care about what, which stack choices burned the team, which problem shapes tend to win — resets to zero.

This workspace fixes both problems: in-event context and across-event memory.

---

## Core Concepts

### Interpretable Context Methodology (ICM)
*Van Clief & McDermott, 2026*

Folder structure replaces orchestration code. Each numbered stage folder contains a `STAGE.md` that defines the agent's role, its inputs, its decision rules, and its required outputs. The agent reads the folder it's in and knows what to do.

```
01-ideation-validation/   ← role: skeptical co-founder
02-mvp-build/             ← role: pragmatic engineer
03-pitch-deck-writeup/    ← role: storyteller and editor
```

**One stage, one job.** A stage that ideates does not also build. A stage that builds does not also pitch. This is Unix philosophy applied to AI workflows — small, composable responsibilities with clean interfaces between them.

The outputs of each stage are plain-text files that become the inputs of the next. No API calls between stages. No state management. If you can read the folder, you understand the system.

### The 60/30/10 Rule
*Van Clief*

Any tool built inside this workspace follows a ratio:

| Layer | What it covers | Target |
|---|---|---|
| Traditional code | File I/O, integrations, networking, plumbing | 60% |
| Rule-based logic | Routing, validation, deterministic decisions | 30% |
| AI processing | Only what genuinely requires a language model | 10% |

If you reach for an LLM call and a regex or a switch statement would do the job, use the regex. The LLM is the smallest layer, not the centerpiece. This prevents the common failure mode where "AI-powered" becomes a way of avoiding the hard engineering work.

### The Compiled Wiki
*Karpathy analogy*

Knowledge that survives across hackathons should compound, not reset.

The analogy: source code is compiled once into a binary. You don't re-execute from raw source on every run — you compile once, then run the binary. Apply this to knowledge:

- **Sources** (`shared/sources/`) are immutable raw inputs — briefs, post-mortems, judge feedback. Never edited after ingestion. These are the source code.
- **The wiki** (`shared/wiki/`) is the compiled artifact — entity pages for judges, winning patterns, stack pitfalls, team dynamics. Updated after each event, not re-derived from scratch.
- **The schema** (`shared/schema/`) governs how sources flow into wiki pages, tracks provenance, and flags contradictions for human resolution.

After each hackathon, a compile step ingests the new sources and updates the relevant wiki pages. The wiki gets denser and more specific every event. You stop solving the same problem twice.

### Computational Thinking

Each stage applies the four pillars of computational thinking as a structured decision framework — not as abstract principles, but as concrete tools for cutting scope, spotting risk, and protecting the demo.

**Decomposition** — break the problem into the smallest sub-problem that still matters. In Stage 01 this means separating problem space from solution space before touching the solution. In Stage 02 it means slicing the build into the smallest unit that demos end-to-end, and identifying what can run in parallel. In Stage 03 it means treating each beat of the pitch as a discrete unit: hook, problem, solution, walkthrough, ask.

**Pattern Recognition** — surface what's been seen before before starting from scratch. The wiki's `winning-patterns.md` and `archetypes/` pages exist specifically for this: has this problem shape won before? Where has the team moved fast? What does a judge leaning forward look like? Recognizing a known pattern is faster and lower-risk than inventing a new one under time pressure.

**Abstraction** — strip everything that isn't the core interaction. In Stage 01 this means ignoring edge cases and scale to focus on one user on one specific day. In Stage 02 it means mocking or hardcoding anything that isn't the happy path. In Stage 03 it means hiding implementation complexity — judges see outcomes, not architecture.

**Algorithm** — apply fixed decision sequences so that under pressure, the team doesn't improvise. The Stage 01 three-question filter is an algorithm: demoable, buildable in time, someone clearly needs it — all three must be yes, in that order. The pitch structure is an algorithm: hook, problem, solution, walkthrough, ask — in that order, timed.

**Verification & Validation (V&V)** sit at the intersection of all four pillars. Borrowed from systems engineering, they are applied as explicit checkpoints before consequential work begins:
- **Validation** (Stage 01): are we solving the *right* problem? The three-question filter is the validator.
- **Verification** (Stage 02): are we planning to build it *correctly*? Before the first line of code, confirm the implementation approach produces the wow moment end-to-end. Surface gaps between the brief and the plan before they become bugs.

### The Project Brief as Handoff Artifact

Each hackathon event gets one file that carries context across all three stages:

```
projects/{event-slug}/CLAUDE.md
```

Stage 01 creates it. Stage 02 reads it and appends build notes. Stage 03 reads it and writes the pitch from it. It is the single source of truth — not a collection of scattered output files.

Because it lives in its own folder and is named `CLAUDE.md`, Claude Code reads it automatically when working inside that folder. No explicit "read this first" instruction needed. The folder structure does the work.

---

## How It Works

```
j-hack-stack/
├── CLAUDE.md                        ← system constitution (read first, always)
├── 01-ideation-validation/
│   ├── STAGE.md                     ← role, decision filter, V&V, gate checklist
│   └── inputs/                      ← brief template, idea dump template
├── 02-mvp-build/
│   ├── STAGE.md                     ← role, cloned repo intake, V&V, build log
│   └── inputs/                      ← stack decision, workstream split templates
├── 03-pitch-deck-writeup/
│   ├── STAGE.md                     ← role, pitch structure, rehearsal checklist
│   └── inputs/                      ← submission requirements template
├── projects/
│   └── _template/
│       ├── CLAUDE.md                ← project brief template
│       └── repo-context.md          ← cloned repo intake template
└── shared/
    ├── status.md                    ← active event tracker (session entry point)
    ├── purpose.md                   ← scope gate for the shared layer
    ├── time-budget.md               ← stage time allocations
    ├── sources/                     ← immutable per-event raw inputs
    ├── wiki/
    │   ├── _index.md
    │   ├── judges.md
    │   ├── winning-patterns.md
    │   ├── stack-pitfalls.md
    │   ├── our-team.md              ← preferred stack + available MCPs & skills (read by Stage 01)
    │   ├── archetypes/              ← reusable problem/solution shapes
    │   └── events/                  ← per-event live records + build logs
    └── schema/
        ├── ingest-rules.md          ← source → wiki mapping
        ├── provenance.md            ← every wiki edit logged (human vs. agent)
        └── contradictions.md        ← conflicts flagged for human resolution
```

### The flow through an event

**Stage 01** receives the brief and an idea. Runs Validation (3-question filter). On confirmation, creates `projects/{event-slug}/CLAUDE.md` (the project brief) and `shared/wiki/events/{event-slug}.md` (the live event record). Updates `shared/status.md` so any future session finds the active event automatically.

**Stage 02** loads the project brief. Runs V&V before the first line of code. Handles cloned repo intake if the team didn't start from scratch — six questions answered before a file is read. Logs build progress to the event wiki page throughout the stage, so if context cuts off mid-build, the next session has a record. Appends build notes to the project brief at the gate.

**Stage 03** reads the completed project brief and generates the pitch from it. Every word of the pitch is grounded in decisions already made — not invented last-minute. Appends the pitch angle to the brief. Copies the completed brief to sources for post-event archiving.

**Post-event compile** ingests sources from the event, updates the relevant wiki pages, logs every change to provenance, and flags contradictions for human review. The wiki absorbs what's new. Over time it earns its weight.

---

## Getting Started

### Prerequisites

- [Claude Code](https://claude.ai/code) — the agent that reads and operates this workspace

### Setup

```bash
git clone https://github.com/jfran03/j-hack-stack.git
cd j-hack-stack
```

Open the folder in Claude Code. It will read `CLAUDE.md` and `shared/status.md` automatically.

**Before your first event**, fill in two sections in `shared/wiki/our-team.md`:

```
→ Preferred Stack table       (Stage 01 pulls this into every new project brief)
→ Available MCPs & Skills     (each STAGE.md filters this to only what's relevant per stage)
```

These are the only human-maintained inputs the system reads before deriving anything else. Everything else is either generated during events or compiled afterward.

### Running an event

Tell Claude Code you're starting Stage 01 and provide the hackathon brief. The agent will walk the rest.

---

## Design Philosophy

This workspace is built for people who want the AI to do the bookkeeping, not the thinking. The human makes every consequential decision — which problem to solve, whether V&V passes, which contradictions to resolve in the wiki. The agent handles context, structure, logging, and synthesis.

The folder structure is the architecture. Edit the markdown, and you've edited the system. No code to change, no config to redeploy.

---

## License

MIT — see `LICENSE`.
