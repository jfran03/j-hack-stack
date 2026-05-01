# Shared — Scope Gate

> This file defines what belongs in `shared/` and what doesn't.
> The agent reads this before touching any shared resource.

---

## What belongs here

`shared/` is cross-event institutional knowledge. A file belongs here if it is useful across multiple hackathons, not just one.

| Belongs | Why |
|---|---|
| Judge names, affiliations, known preferences | Accumulates across events |
| Winning patterns observed over time | Cross-event signal |
| Stack pitfalls the team has hit | Don't repeat the same mistake |
| Team strengths, dynamics, known gaps | Cross-event team knowledge |
| Problem/solution archetypes that recur | Reusable shapes |

## What does NOT belong here

| Does not belong | Where it goes instead |
|---|---|
| Event-specific brief, rules, judging criteria | `shared/sources/{event-slug}/` (raw, immutable) |
| Stage-by-stage decisions for a specific event | `01-ideation-validation/`, `02-mvp-build/`, etc. |
| Working demo code | `02-mvp-build/outputs/working-demo/` |
| Pitch deck, demo script | `03-pitch-deck-writeup/outputs/` |

## The compile boundary

- **Sources** (`shared/sources/`) are immutable historical records. Never edit them after ingestion.
- **Wiki** (`shared/wiki/`) is the compiled artifact. It gets updated by the compile step, not directly by stage work.
- **Schema** (`shared/schema/`) governs how the compile step works and tracks its provenance.

If you are unsure whether something belongs in the wiki, ask: "Would a future team member benefit from knowing this at the start of any future hackathon?" If yes — wiki. If it's specific to one event — sources.
