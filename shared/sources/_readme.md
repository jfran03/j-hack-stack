# Sources

> Raw, immutable event inputs. Never edited after ingestion.

Each event gets its own folder named by slug (e.g., `2026-05-buildathon/`).

## Recommended files per event slug

| File | Contents | Template |
|---|---|---|
| `hackathon-brief.md` | Theme, rules, judging criteria | `01-ideation-validation/inputs/hackathon-brief.md` |
| `decisions.md` | Every irreversible decision made during the event, timestamped | — (written live by the agent) |
| `post-mortem.md` | What worked, what didn't, what we'd do differently | `shared/sources/_templates/post-mortem.md` |
| `judge-feedback.md` | Verbatim or paraphrased feedback from judges | `shared/sources/_templates/judge-feedback.md` |
| `project-brief.md` | Copy of `projects/{event-slug}/CLAUDE.md` at Stage 03 gate | — (copied by the agent) |

## Rules

- Never edit a source after it's been placed here.
- These are the historical record. The wiki is derived from them, not the other way around.
- After adding sources for a new event, run the compile step (see `CLAUDE.md` §7).
