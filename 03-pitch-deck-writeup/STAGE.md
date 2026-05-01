# Stage 03 — Pitch Deck & Writeup

> **Role:** Storyteller and editor. The judges see this, not the code. Translate the work into a narrative that lands.

---

## Your Job Here

Read the project brief. Every word of the pitch should be traceable back to something already decided — the problem, the target user, the wow moment. You are not inventing a new story; you are surfacing the one that's already there.

---

## Step 1 — Load Context

1. Read `projects/{event-slug}/CLAUDE.md` in full — problem, target user, wow moment, scope, happy path, build notes. This is the only source you need.
2. Read `shared/wiki/winning-patterns.md` — apply relevant before/after framing patterns.
3. Read `03-pitch-deck-writeup/inputs/submission-requirements.md` — know the portal's format before drafting anything.

---

## Step 2 — Build the Pitch

### The Fixed Sequence

| Beat | Content | 3-min | 60-sec |
|---|---|---|---|
| Hook | The moment the problem is real | 15 sec | 10 sec |
| Problem | Who has this pain and when | 30 sec | 10 sec |
| Solution | What we built and how it helps | 30 sec | 15 sec |
| Demo walkthrough | Show it working | 75 sec | 20 sec |
| Impact / ask | Why it matters, what's next | 30 sec | 5 sec |

Stick to this order. Under pressure, improvisation loses the thread.

### Computational Thinking Applied

- **Decomposition:** Each beat is one slide or one paragraph. Write them separately, then sequence.
- **Pattern recognition:** Apply before/after structure from `winning-patterns.md`. Before: the user's frustration. After: the user's relief.
- **Abstraction:** Hide implementation complexity. Show the user's experience, not the system diagram. Judges see outcomes.
- **Algorithm:** Draft → time → cut → rehearse → repeat.

---

## Step 3 — Outputs

Create all four inside `projects/{event-slug}/pitch/`:

1. `deck.pdf` (or link) — visual slides
2. `demo-script.md` — exactly what the presenter says, beat by beat, with timings
3. `writeup.md` — submission portal format (see `submission-requirements.md`)
4. `judge-qa-prep.md` — anticipated questions and rehearsed answers

---

## Step 4 — Gate

When outputs are complete:

1. Append the **Pitch Angle** section of `projects/{event-slug}/CLAUDE.md`:
   - Hook
   - Before/after framing
   - 60-second and 3-minute outlines
2. The completed project brief is now the post-event source. Copy `projects/{event-slug}/CLAUDE.md` to `shared/sources/{event-slug}/project-brief.md`.
3. Update `shared/status.md` — advance stage to `03-pitch`, or mark as complete once submitted.

---

## Relevant Tools

> Only invoke tools listed here during this stage. Full registry is in `shared/wiki/our-team.md` — do not load it unless looking up a specific tool's details.

| Tool | Use case in this stage |
|---|---|

Add or remove rows as your MCP setup changes. If a tool isn't listed here, don't use it at this stage.

---

## 60/30/10 at This Stage

- **60% (traditional):** slide assembly, asset management, writeup formatting
- **30% (rules):** slide-count limits, time-per-beat enforcement, submission checklist
- **10% (AI):** drafting copy variants, tightening language, brainstorming hooks

---

## Rehearsal Checklist

- [ ] 3-minute version timed and under
- [ ] 60-second version timed and under
- [ ] Demo walked through live at least twice (not just in your head)
- [ ] Backup plan if demo fails (screenshot, recording, or graceful acknowledgment)

---

## Stage Gate Checklist

- [ ] All four pitch outputs exist in `projects/{event-slug}/pitch/`
- [ ] Pitch Angle section written in the project brief
- [ ] Project brief copied to `shared/sources/{event-slug}/project-brief.md`
- [ ] Submission portal checklist complete
- [ ] Presenter has done at least one timed rehearsal
