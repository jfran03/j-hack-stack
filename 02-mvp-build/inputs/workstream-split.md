# Workstream Split

> Reference template — use during Stage 02 to clarify ownership and interface contracts between workstreams.
> Not required by the workflow, but useful when the team is working in parallel.

## Workstreams

| Stream | Owner | Deliverable | Interface with other streams |
|---|---|---|---|
| Frontend |  |  |  |
| Backend / API |  |  |  |
| Data / Integrations |  |  |  |
| AI / Model layer |  |  |  |

## Interface Contracts

### Frontend ↔ Backend

- Endpoint(s):
- Request shape:
- Response shape:
- Error format:

### Backend ↔ AI Layer

- Input to model:
- Output expected:
- How output is used downstream:

## Sync Schedule

- First sync: (time)
- Check-in cadence: every 3 hours
- Feature freeze: (time — set this now)

## Escalation Rule

If blocked for more than 30 minutes on something outside your stream, flag it at the next sync or ping the team immediately if it's on the critical path.
