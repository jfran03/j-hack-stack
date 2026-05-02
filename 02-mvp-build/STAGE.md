# Stage 02 — Minimal Viable Product

> **Role:** Pragmatic engineer. Protect the happy path. Ship something that works over something that's complete.

---

## Your Job Here

Read the project brief. Run V&V before the first line of code. Build inside the project folder. Log progress to the event wiki page. Protect the happy path above all else.

---

## Step 1 — Load Context

1. Read `projects/{event-slug}/CLAUDE.md` — single source of truth for problem, user, wow moment, scope, and stack.
2. Read `shared/wiki/stack-pitfalls.md` — know what has burned the team before. If this page is empty (first event), skip.
3. Read `shared/wiki/events/{event-slug}.md` — this is where build progress gets logged throughout the stage.
4. Check `projects/{event-slug}/{project-name}/` (the project root — **never** a `src/` wrapper):
   - **No code files yet** → proceed to V&V, then build directly here.
   - **Contains a cloned repo** → run **Cloned Repo Intake** before anything else.

---

## Cloned Repo Intake

> Run whenever the user brings in a repo they did not write from scratch.
> Ask every question before reading a single file. Do not guess.

### Questions to ask (in order)

1. **Origin** — Where does this come from? (own prior work / teammate's code / public template / open-source)
2. **State** — How complete is it? Does it run right now?
3. **Role** — Building on top, replacing parts, or referencing for patterns?
4. **Sacred vs. changeable** — What must not be touched? What is fair game?
5. **Stack delta** — Does its stack match the project brief? If not, which takes precedence?
6. **Entry point** — How do you run it locally? Any env vars or setup steps?

### After the user answers

1. Read the README, then the dependency manifest (`package.json`, `requirements.txt`, `go.mod`, etc.).
2. State the gap between what the repo does and what the project brief requires.
3. Create `projects/{event-slug}/repo-context.md` (from `projects/_template/repo-context.md`) and fill it in.
4. If the stack differs from the brief, log the deviation in the brief's Stack table and in `shared/sources/{event-slug}/decisions.md`.

Do not proceed to V&V until `repo-context.md` exists and the user confirms the gap assessment.

---

## Step 2 — V&V Checkpoint

> **Run this before writing a single line of code.**
> Verification and Validation are two separate questions. Both must pass.

### Validation — are we building the right thing?

Re-read the project brief and ask:
- Does the problem statement still hold? Has anything changed since Stage 01 that invalidates it?
- Is the target user still specific and real?
- Is the wow moment still achievable with the time and stack available?

If anything has shifted, surface it now and amend the project brief before proceeding. Log the amendment in `shared/sources/{event-slug}/decisions.md`.

### Verification — are we planning to build it correctly?

Given the brief and the stack, ask:
- Does the proposed approach actually produce the wow moment end-to-end?
- Is there a clear happy path from user action to visible output?
- Are there any gaps between the brief and the implementation plan — features assumed but not scoped, dependencies assumed but not validated?

State the happy path explicitly before building. If the approach has gaps, resolve them now.

**V&V passes when:** both checks are yes and the user confirms. Log the V&V result as the first entry in the Build Log section of `shared/wiki/events/{event-slug}.md`.

---

## Step 3 — Validate the Riskiest Dependency First

Before writing UI or business logic, prove the hardest external thing works:
- API auth and rate limits
- Model call latency and output format
- Data source availability

If it fails, surface it immediately. Log it in the event wiki page. Do not build three layers around an unvalidated assumption.

---

## Project Root Rule — NEVER VIOLATE

`projects/{event-slug}/{project-name}/` is the project root. All code, config, and assets go directly inside it.

**NEVER create a `src/` folder as a wrapper for the entire project.** This produces `src/src/` nesting and breaks all path assumptions.

```
CORRECT:
{project-name}/
├── CLAUDE.md
├── package.json
├── index.html
├── api/
└── src/        ← only if framework-conventional (e.g. Vite) and contains source files only

WRONG:
{project-name}/
├── CLAUDE.md
└── src/        ← ❌ entire project dumped here
    ├── package.json
    ├── index.html
    └── src/    ← ❌ src/src/ nesting
```

---

## Step 4 — Build

### Computational Thinking Applied

- **Decomposition:** Slice into the smallest unit that demos end-to-end. Separate frontend, backend, data, and external APIs.
- **Pattern recognition:** Where has the team moved fast before? Replicate that environment.
- **Abstraction:** Mock or hardcode everything that is not the core interaction.
- **Algorithm:** Validate riskiest dependency → build happy path → freeze features → polish demo.

### Build Log

After each significant decision, blocker resolved, or workstream completed — append a short entry to the Build Log table in `shared/wiki/events/{event-slug}.md`. One line is enough. This is the continuity record if context cuts off mid-stage.

### Ongoing Validation

At every sync checkpoint (default: every 3 hours), ask:
- Is the happy path still intact end-to-end?
- Are we building what the project brief says, or have we drifted?

If scope drift is detected: cut the drift or amend the brief with a logged reason. Never silently expand scope.

---

## Relevant Tools

> Only invoke tools listed here during this stage. Full registry is in `shared/wiki/our-team.md` — do not load it unless looking up a specific tool's details.

| Tool | Use case in this stage |
|---|---|
| GitHub MCP | Clone repos, manage branches, open PRs for demo deployment |
| Code execution skill | Run and verify build steps without leaving the agent context |
| `/simplify` skill | Review changed code for quality after a workstream completes |
| `/security-review` skill | Run before feature freeze if the build handles user data or auth |

Add or remove rows as your MCP setup changes. If a tool isn't listed here, don't use it at this stage.

---

## 60/30/10 at This Stage

- **60% (traditional):** API integrations, file handling, frontend scaffolding, deployment, auth, data persistence
- **30% (rules):** input validation, routing, fallbacks, cached responses, deterministic transformations of model output
- **10% (AI):** the actual LLM calls, embedding lookups, generation steps — bounded, prompted, wrapped in retry logic

---

## Step 5 — Gate

When the happy path works end-to-end:

1. Append the **Build Notes** section of `projects/{event-slug}/CLAUDE.md` — happy path, key decisions, what's mocked or fragile.
2. Update the Outcomes section of `shared/wiki/events/{event-slug}.md`.
3. Log major decisions in `shared/sources/{event-slug}/decisions.md`.
4. Update `shared/status.md` — advance stage to `02-build`.
5. Call feature freeze.

---

## Stage Gate Checklist

- [ ] V&V passed and logged in event wiki page
- [ ] If repo cloned: `repo-context.md` exists and gap confirmed
- [ ] `projects/{event-slug}/{project-name}/` exists and runs without setup steps
- [ ] Happy path walked end-to-end at least once
- [ ] Build Notes written in the project brief
- [ ] Build Log in event wiki page reflects actual progress
- [ ] Feature freeze called
- [ ] `shared/status.md` updated
