# Foundational Principles

> Background reading. Not routing. Claude does not need to load this during stage work.

---

## Interpretable Context Methodology (Van Clief & McDermott, 2026)

Folder structure replaces orchestration code. Numbered folders represent stages. Markdown files tell the agent what role to play at each stage. Outputs from one stage are plain-text inputs to the next.

**One stage, one job.** A stage that ideates does not also build. A stage that builds does not also pitch.

---

## The 60/30/10 Rule (Van Clief)

Any tool built in this workspace should follow:

- **60% traditional code** — file I/O, integrations, networking, plumbing
- **30% rule-based logic** — routing, validation, deterministic decisions
- **10% AI processing** — only the parts that genuinely require a language model

If a regex or a switch statement would do the job, use it. The LLM is the smallest layer, not the centerpiece.

---

## The Compiled Wiki (Karpathy)

Knowledge that survives across hackathons should compound, not reset.

- **Sources** (`shared/sources/`) are immutable raw inputs. Never edited after ingestion.
- **The wiki** (`shared/wiki/`) is a compiled artifact. Updated by the compile step, not directly.
- **The schema** (`shared/schema/`) governs how sources flow into wiki pages.

The wiki is the binary. Sources are the source code. You compile after each event.

---

## Extending This Workspace

**After each event:**
- Drop the post-mortem and judge feedback into `shared/sources/{event-slug}/`.
- Run the compile step. Resolve contradictions in `shared/schema/contradictions.md` yourself — this is curation the agent shouldn't do unsupervised.

**Over time:**
- Add new wiki entity pages when a new dimension emerges (e.g. `wiki/sponsors.md`).
- Add stage-specific templates to each stage's `inputs/` as patterns emerge.
- Build small scripts in `shared/scripts/` for the 60% layer (output validation, broken-link detection, source ingestion).
- Refine decision filters in each `STAGE.md` based on what predicted success — record changes and reasoning in `shared/schema/provenance.md`.

**What not to do:**
- Don't edit sources. They are the historical record.
- Don't let the wiki grow without curation.
- Don't pull stage-specific context into wiki pages.
