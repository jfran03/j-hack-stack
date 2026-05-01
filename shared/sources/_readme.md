# Sources

> Raw, immutable event inputs. Never edited after ingestion.

Each event gets its own folder named by slug (e.g., `2026-05-buildathon/`).

## Recommended files per event slug

| File | Contents |
|---|---|
| `hackathon-brief.md` | Theme, rules, judging criteria (copy from stage 01 inputs) |
| `decisions.md` | Every irreversible decision made during the event, timestamped |
| `post-mortem.md` | What worked, what didn't, what we'd do differently |
| `judge-feedback.md` | Verbatim or paraphrased feedback from judges |
| `happy-path.md` | Copy from stage 02 outputs — what actually ran in the demo |
| `known-limitations.md` | Copy from stage 02 outputs — what was fragile or mocked |

## Rules

- Never edit a source after it's been placed here.
- These are the historical record. The wiki is derived from them, not the other way around.
- After adding sources for a new event, run the compile step (see `CLAUDE.md` §7).
