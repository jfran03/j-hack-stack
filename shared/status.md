# Workspace Status

> Current state of the workspace. Update this whenever the structure changes significantly or an event completes.

---

## Setup status

- [x] Root CLAUDE.md — system architecture defined
- [x] Stage folders (01, 02, 03) — STAGE.md and input templates created
- [x] `projects/_template/CLAUDE.md` — project brief template created
- [x] `shared/` — three-layer wiki system (sources, wiki, schema) built
- [ ] `shared/wiki/our-team.md` → **Preferred Stack table** — **fill this in before first event**
- [ ] First event run

## Active event

None.

<!-- When Stage 01 finalizes an event, replace this block with:

## Active event

- **Slug:** {event-slug}
- **Status:** {active | paused | abandoned}
- **Stage:** {01-ideation | 02-build | 03-pitch}
- **Project brief:** projects/{event-slug}/CLAUDE.md
- **Event wiki:** shared/wiki/events/{event-slug}.md
- **Started:** {YYYY-MM-DD}
- **Last updated:** {YYYY-MM-DD}

Update Stage and Last updated each time the project advances or a session resumes.
Set Status to paused if work stops mid-event. Set to abandoned if the project is dropped.
-->

## Last significant change

2026-05-01 — Initial workspace build. Key design decisions:
- The project brief (`projects/{event-slug}/CLAUDE.md`) is the single handoff artifact across all three stages. Each stage reads it and appends its section.
- It IS the CLAUDE.md for that project folder — Claude reads it automatically when working inside the folder, no explicit instruction needed.
- `shared/` replaced a flat file structure with a three-layer compiled wiki: sources (immutable), wiki (compiled), schema (governance).
- Stack defaults live in `shared/wiki/our-team.md` (human-maintained, not compile-step) so Stage 01 can pull them into each new project brief without reading scattered files.

## What to do next

1. Fill in `shared/wiki/our-team.md` → Preferred Stack.
2. When ready for an event: go to Stage 01, provide the hackathon brief, and the agent will walk the flow.
