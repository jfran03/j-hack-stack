# Hackathon Workflow — Architecture Spec

> **What this is:** An Interpretable Context Methodology (ICM) workspace for running hackathons end-to-end. One agent. Three numbered stages. Plain markdown context files. No orchestration framework.
>
> **What this is for:** Claude Code reads this file first to understand the system, then navigates into the appropriate stage folder based on where the user is in the hackathon.

---

## 1. Foundational Principles

This workspace is built on three ideas:

### 1.1 Interpretable Context Methodology (Van Clief & McDermott, 2026)
Folder structure replaces orchestration code. Numbered folders represent stages. Markdown files inside each folder tell the agent what role to play at that stage. Outputs from one stage are plain-text artifacts that become inputs to the next.

**One stage, one job.** A stage that ideates does not also build. A stage that builds does not also pitch. This is Unix philosophy applied to AI workflows.

### 1.2 The 60/30/10 Rule (Van Clief)
Any tool built inside this workspace should follow:
- **60% traditional code** — file I/O, integrations, networking, plumbing
- **30% rule-based logic** — routing, validation, deterministic decisions
- **10% AI processing** — only the parts that genuinely require a language model

If you reach for an LLM call and a regex or a switch statement would do the job, use the regex. The LLM is the smallest layer, not the centerpiece.

### 1.3 The Compiled Wiki (Karpathy)
Knowledge that survives across hackathons should compound, not reset. Karpathy's analogy: source code is compiled once into a binary, not re-executed from raw form on every run. Apply this to hackathon knowledge.

- **Sources** are immutable raw inputs (briefs, post-mortems, judge feedback).
- **The wiki** is a compiled, interlinked artifact that gets updated, not re-derived.
- **The schema** governs how sources flow into wiki pages.

After each hackathon, a compile step ingests the post-mortem, updates affected entity pages (judges, patterns, stack pitfalls, team), strengthens cross-references, and flags contradictions with prior knowledge. The wiki gets denser and smarter every event. You stop solving the same problem twice.

The human's job is to curate sources, ask questions, and make decisions. The agent does the bookkeeping.

---

## 2. The Three Stages

```
hackathon-workflow/
├── CLAUDE.md                  ← you are here (read first, always)
├── 01-ideation-validation/
│   ├── STAGE.md               ← role: critical co-founder
│   ├── inputs/                ← hackathon brief, theme, team info
│   └── outputs/               ← validated problem statement, scope
├── 02-mvp-build/
│   ├── STAGE.md               ← role: pragmatic engineer
│   ├── inputs/                ← (auto-populated from stage 01 outputs)
│   └── outputs/               ← working demo, happy path notes
├── 03-pitch-deck-writeup/
│   ├── STAGE.md               ← role: storyteller and editor
│   ├── inputs/                ← (auto-populated from stage 01 + 02 outputs)
│   └── outputs/               ← deck, demo script, writeup
└── shared/
    ├── purpose.md             ← scope gate: what belongs here, what doesn't
    ├── sources/               ← raw, immutable: briefs, post-mortems, judge feedback
    │   └── {event-slug}/
    ├── wiki/                  ← compiled, compounding: entity pages updated per event
    │   ├── _index.md
    │   ├── judges.md
    │   ├── winning-patterns.md
    │   ├── stack-pitfalls.md
    │   ├── our-team.md
    │   └── archetypes/        ← reusable problem/solution shapes
    └── schema/
        ├── ingest-rules.md    ← how new sources update which wiki pages
        ├── provenance.md      ← who/what authored each change (human vs. agent)
        └── contradictions.md  ← flagged conflicts awaiting resolution
```

**Routing rule for Claude Code:** When the user invokes a stage, read `CLAUDE.md` (this file) → read `shared/*.md` → read the relevant `0N-stage/STAGE.md` → read prior stage outputs if they exist. Do not load context from stages the user is not currently working in.

---

## 3. Stage 01 — Ideation & Validation

**Role:** Skeptical co-founder. Push back on bad ideas. Stress-test the problem before any building begins.

**What gets consolidated here from the broader hackathon framework:**
- Problem selection (real, relatable, demonstrable, time-feasible)
- Target user definition (specific, not "everyone")
- Novelty angle (tech, approach, or combination)
- Initial scope-cutting

### Computational Thinking Applied

- **Decomposition:** Separate problem space from solution space. Validate the problem first. Break the problem into sub-problems and pick the smallest one that still matters.
- **Pattern recognition:** Surface analogous winning hackathon ideas. Spot the patterns: API-powered, visually immediate, emotionally resonant.
- **Abstraction:** Strip edge cases and scale considerations. Focus on the core use case for one specific user on one specific day.
- **Algorithm:** Apply a fixed decision filter — *Is it demoable? Is it buildable in time? Does someone clearly need this?* All three must be yes.

### 60/30/10 Inside This Stage
- **60% (traditional):** templates, decision-log writes, file I/O for capturing ideas
- **30% (rules):** the three-question filter, scope-feasibility checks, time-budget guardrails
- **10% (AI):** generating idea variants, surfacing analogous projects, drafting the problem statement

### Required Outputs (move to `outputs/` before advancing)
1. `problem-statement.md` — one sentence, plain language
2. `target-user.md` — specific persona, specific moment, specific frustration
3. `scope-contract.md` — what's in, what's explicitly out, with a feasibility check
4. `wow-moment.md` — the single thing that will make a judge lean forward

---

## 4. Stage 02 — Minimal Viable Product

**Role:** Pragmatic engineer. Protect the happy path. Ship something that works over something that's complete.

**What gets consolidated here from the broader hackathon framework:**
- Core "wow" feature (the smallest working unit that still impresses)
- Technical stack decisions (use what the team knows, minimize integration risk)
- Team role clarity (parallel workstreams, sync checkpoints)
- Ruthless scope management

### Computational Thinking Applied

- **Decomposition:** Slice the build into the smallest unit that demos end-to-end. Separate frontend, backend, data, and external APIs. Identify what can be parallelized.
- **Pattern recognition:** Recognize where the team has moved fast before and replicate that environment. Spot bottlenecks early (one person blocking everyone) and redistribute.
- **Abstraction:** Mock or hardcode everything that isn't the core interaction. Treat external APIs as black boxes. Each teammate only needs to understand their interface with the rest.
- **Algorithm:** Validate the riskiest dependency *first* before building anything around it. Define exact happy-path steps and protect them. Set fixed sync points (every 3 hours) and a hard feature-freeze time.

### 60/30/10 Inside This Stage
This is where the rule has the most teeth.
- **60% (traditional):** API integrations, file handling, frontend scaffolding, deployment plumbing, auth, data persistence
- **30% (rules):** input validation, routing, fallbacks, cached responses, deterministic transformations of model output
- **10% (AI):** the actual LLM calls, embedding lookups, generation steps — bounded, prompted, and wrapped in retry logic

If a "feature" requires more than 10% AI to work, it's probably trying to do too much in the model. Push logic into the 30% layer.

### Required Outputs (move to `outputs/` before advancing)
1. `working-demo/` — the actual artifact, runnable
2. `happy-path.md` — the exact sequence of steps that must work in the demo
3. `known-limitations.md` — what's mocked, what's fragile, what to avoid touching
4. `risky-dependency-log.md` — every external thing that could fail mid-demo

---

## 5. Stage 03 — Pitch Deck & Writeup

**Role:** Storyteller and editor. The judges see this, not the code. Translate the work into a narrative that lands.

**What gets consolidated here from the broader hackathon framework:**
- Demo / presentation (the highest-emphasis component)
- Hero moment positioning
- Confident, rehearsed delivery
- Writeup for submission portals

### Computational Thinking Applied

- **Decomposition:** Break the pitch into discrete beats — hook, problem, solution, walkthrough, ask. Each beat is a slide or a paragraph.
- **Pattern recognition:** Winning pitches almost always follow before/after structure. Recognize and apply.
- **Abstraction:** Hide implementation complexity. Judges see outcomes, not architecture. Show the user's experience, not the system diagram.
- **Algorithm:** Rehearse a fixed sequence so under pressure you don't improvise and lose the thread. Time every beat. Have a 60-second version and a 3-minute version.

### 60/30/10 Inside This Stage
- **60% (traditional):** slide assembly, asset management, video recording/editing, writeup formatting
- **30% (rules):** slide-count limits, time-per-beat enforcement, required-section checklists for submission
- **10% (AI):** drafting copy variants, tightening language, generating alt-text, brainstorming hooks

### Required Outputs (move to `outputs/` before advancing)
1. `deck.pdf` (or link) — visual slides
2. `demo-script.md` — exactly what the presenter says, beat by beat
3. `writeup.md` — for the submission portal, in their required format
4. `judge-qa-prep.md` — anticipated questions and rehearsed answers

---

## 6. Cross-Stage Rules

### 6.1 Stage Gates
A stage is not complete until all required outputs exist in its `outputs/` folder. Do not advance to the next stage with missing outputs. The next stage's `STAGE.md` will fail-fast if its expected inputs aren't there.

### 6.2 The Compounding Wiki
Every irreversible decision (problem chosen, stack picked, feature cut, name chosen) is captured in `shared/sources/{event-slug}/decisions.md` during the event — that file is immutable raw input.

After the event, run the **compile step**: an agent reads the new sources and updates the relevant wiki pages in `shared/wiki/`. Rules:
- The wiki is the only place where knowledge compounds. Sources never get edited.
- Every wiki edit gets a provenance line in `schema/provenance.md` — was it human-authored or agent-synthesized?
- Contradictions with existing wiki content go to `schema/contradictions.md` for human resolution. Do not silently overwrite.
- New sources outside the scope defined in `purpose.md` are skipped, not ingested.

This is the Karpathy pattern applied to hackathon knowledge. The wiki is the binary. Sources are the source code. You compile after each event.

### 6.3 Time Budget
Hackathons are constraint-driven. A typical 24-hour event allocates roughly:
- Stage 01: 10–15% of total time (2–4 hours)
- Stage 02: 65–70% of total time (16–18 hours)
- Stage 03: 15–20% of total time (4–6 hours)

These percentages are defaults, not laws. Adjust per event in `shared/time-budget.md` if needed.

### 6.4 Context Hygiene
Per ICM: load only what the current stage needs. Do not pull stage 03 context while in stage 01. The folder boundary is the context boundary.

---

## 7. How Claude Code Should Use This Workspace

### Starting a session

1. Read this `CLAUDE.md` in full.
2. Read `shared/status.md`. Three possible states:
   - **No active event** → ask the user what they'd like to do (start a new event, or other).
   - **Active event** → load `projects/{event-slug}/CLAUDE.md` immediately. Do not ask the user to repeat context already in the brief. Confirm which stage to work in.
   - **Active event but status is `paused` or last-updated is more than 24 hours ago** → surface it explicitly: *"There's a project in the pipeline — `{slug}` at stage `{stage}`, last updated `{date}`. Continue, or close it out and save to wiki?"* Wait for the user's decision before loading anything else.
3. Read `shared/wiki/_index.md` — surface compiled prior knowledge. Do not re-derive what the wiki already knows.
4. Determine the current stage from `shared/status.md` or by asking the user.
5. Read the `STAGE.md` for that stage only.

**Closing out an event early (abandoned or paused):**
If the user chooses to close out a project before Stage 03 completes:
1. Fill in the Outcomes section of `shared/wiki/events/{event-slug}.md` with what was reached and why it stopped.
2. Update `shared/status.md` — set status to `abandoned` or `paused` with a date.
3. If the user wants to archive it: copy `projects/{event-slug}/CLAUDE.md` to `shared/sources/{event-slug}/project-brief.md`. The event will feed the compile step whenever a post-mortem is written.
4. If abandoned entirely: clear the active event block in `shared/status.md`.

### The project brief is the handoff artifact

Each hackathon event has one file that carries context across all three stages:

```
projects/{event-slug}/CLAUDE.md
```

- **Stage 01** creates this file (from `projects/_template/CLAUDE.md`) and fills in the problem, user, wow moment, scope, and stack.
- **Stage 02** reads it as the build brief, then appends the Build Notes section at its gate.
- **Stage 03** reads it as the pitch brief, then appends the Pitch Angle section at its gate.

When working inside a project folder, Claude reads the project `CLAUDE.md` automatically. It is the only cross-stage context the agent needs — do not re-read scattered stage output files.

### Context hygiene

Load only what the current stage needs:
- Always: root `CLAUDE.md`, the project brief (if it exists), the current `STAGE.md`
- Stage 01 only: `shared/wiki/winning-patterns.md`, `shared/wiki/our-team.md` (preferred stack + tool registry)
- Stage 02 only: `shared/wiki/stack-pitfalls.md`
- Stage 03 only: `shared/wiki/winning-patterns.md`, submission requirements

Do not load wiki pages or other stage outputs beyond this list.

**MCPs and skills:** each `STAGE.md` has a Relevant Tools section listing which MCPs and skills apply at that stage. Only invoke those. Do not load the full tool registry (`shared/wiki/our-team.md` → Available MCPs & Skills) during stage work — the STAGE.md is the filter. Reference the registry only if you need to look up a specific tool's details.

### On post-event compile

When the user runs the compile step (after the event, once a post-mortem is written):
1. Read the new sources in `shared/sources/{event-slug}/`.
2. Read `shared/schema/ingest-rules.md` to determine which wiki pages each source updates.
3. For each affected wiki page: read it, integrate, strengthen cross-references, flag contradictions to `schema/contradictions.md` — never silently overwrite.
4. Append every edit to `schema/provenance.md` with timestamp and authorship (agent vs. human).
5. Never edit a source. Sources are immutable.

When in doubt, the agent's role is whatever the current stage's `STAGE.md` says it is. This file is the constitution; `STAGE.md` files are the operating instructions; the project brief is the handoff; the wiki is institutional memory.

---

## 8. Extending This Library

This is a base scaffold. As you run more hackathons, the workspace should compound, not accumulate.

**After each event:**
- Drop the post-mortem and any judge feedback into `shared/sources/{event-slug}/`.
- Run the compile step. The wiki absorbs what's new.
- Resolve any flagged contradictions in `schema/contradictions.md` yourself — this is curation work the agent shouldn't do unsupervised.

**Over time:**
- Wiki pages get denser. `winning-patterns.md` starts as empty; after five events, it has earned its weight.
- Add new entity pages when a new dimension emerges (e.g., `wiki/sponsors.md` if sponsor relationships start mattering).
- Add stage-specific templates to each stage's `inputs/` as you spot patterns in your prep work.
- Build small scripts in `shared/scripts/` for the 60% layer (output validation, broken-link detection in the wiki, source ingestion).
- Refine the decision filters in each `STAGE.md` based on what actually predicted success — but record the change and why in `schema/provenance.md`.

**What not to do:**
- Don't edit sources. They are the historical record.
- Don't let the wiki grow without curation. Run periodic linting (broken links, contradictions, scope drift) — this is the 30% layer doing its job.
- Don't pull stage-specific context into wiki pages. The wiki is cross-event institutional knowledge; stage outputs are event-specific.

The folder structure is the architecture. Edit the markdown, and you've edited the system. Compile the sources, and the system gets smarter.