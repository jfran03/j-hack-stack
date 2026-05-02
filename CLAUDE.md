# j-hack-stack — Routing

ICM workspace. Three stages. Plain markdown. One agent per stage.

---

## Workspace Map

```
j-hack-stack/
├── CLAUDE.md                        ← you are here (routing only)
├── 01-ideation-validation/STAGE.md  ← role: skeptical co-founder
├── 02-mvp-build/STAGE.md            ← role: pragmatic engineer
├── 03-pitch-deck-writeup/STAGE.md   ← role: storyteller and editor
├── projects/
│   ├── _template/CLAUDE.md          ← copy this to start a new event
│   └── {event-slug}/CLAUDE.md       ← project brief (handoff across stages)
└── shared/
    ├── status.md                    ← active event, current stage, last updated
    ├── time-budget.md               ← per-event time allocations
    ├── purpose.md                   ← scope gate for shared/
    ├── principles.md                ← ICM, 60/30/10, Karpathy compiled wiki
    ├── sources/{event-slug}/        ← raw, immutable event inputs
    ├── wiki/                        ← compiled, compounding cross-event knowledge
    └── schema/                      ← ingest rules, provenance, contradictions
```

---

## Session Start

1. Read `shared/status.md`:
   - **No active event** → ask the user what they'd like to do.
   - **Active event** → load `projects/{event-slug}/CLAUDE.md` immediately. Confirm which stage.
   - **Paused or last-updated >24h** → surface it: *"There's a project in progress — `{slug}` at stage `{stage}`, last updated `{date}`. Continue, or close it out?"* Wait for the user's decision.
2. Read `shared/wiki/_index.md` — surface prior knowledge. Do not re-derive what the wiki already knows.
3. Read `0N-stage/STAGE.md` for the current stage only.

---

## Routing Table

| Task | Go to | Read |
|---|---|---|
| Ideating or validating a problem | `01-ideation-validation/STAGE.md` | project brief + `shared/wiki/winning-patterns.md`, `shared/wiki/our-team.md` |
| Building the MVP | `02-mvp-build/STAGE.md` | project brief + `shared/wiki/stack-pitfalls.md` |
| Writing the pitch or deck | `03-pitch-deck-writeup/STAGE.md` | project brief + `shared/wiki/winning-patterns.md`, `inputs/submission-requirements.md` |
| Post-event compile | `shared/schema/ingest-rules.md` | new sources in `shared/sources/{event-slug}/` |
| Starting a new event (no active event) | `01-ideation-validation/STAGE.md` | `shared/wiki/winning-patterns.md`, `shared/wiki/our-team.md` |

Do not load wiki pages or stage files beyond what this table specifies.

---

## Naming

Event slug format: `YYYY-MM-{short-name}` (e.g. `2026-05-buildathon`)

---

## Closing Out Early

1. Fill Outcomes in `shared/wiki/events/{event-slug}.md`.
2. Update `shared/status.md` → `abandoned` or `paused` with date.
3. Archive: copy `projects/{event-slug}/CLAUDE.md` to `shared/sources/{event-slug}/project-brief.md`.
4. If abandoned: clear the active event block in `shared/status.md`.

---

## Post-Event Compile

1. Read new sources in `shared/sources/{event-slug}/`.
2. Read `shared/schema/ingest-rules.md` → determine which wiki pages to update.
3. For each page: read → integrate → flag contradictions to `shared/schema/contradictions.md`. Never silently overwrite.
4. Log every edit to `shared/schema/provenance.md` with timestamp and authorship.
5. Never edit a source. Sources are immutable.
