# Ingest Rules

> Governs how new sources update which wiki pages during the compile step.
> The agent reads this before touching any wiki page.

---

## Source → Wiki Mapping

| Source file | Updates wiki page(s) | Notes |
|---|---|---|
| `decisions.md` | `our-team.md` (dynamics section), `stack-pitfalls.md` | Stack decisions → pitfalls if they caused issues |
| `post-mortem.md` | `winning-patterns.md`, `stack-pitfalls.md`, `our-team.md` | Primary source for most wiki updates |
| `judge-feedback.md` | `judges.md`, `winning-patterns.md` | Judge identity → judges.md; preference signals → patterns |
| `hackathon-brief.md` | None (source only) | Briefs are historical record; no wiki update |
| `happy-path.md` | `archetypes/` (if pattern is novel) | Only if the solution shape is new and reusable |
| `known-limitations.md` | `stack-pitfalls.md` | Technical fragilities that recurred → pitfall |

---

## Compile Rules

1. **Read before writing.** Always read the current wiki page before updating it. Integrate, don't overwrite.
2. **Strengthen, don't weaken.** If new evidence confirms existing content, add the new event as a supporting citation. Don't delete the prior entry.
3. **Contradict explicitly.** If new evidence contradicts existing content, do not silently update. Flag to `contradictions.md` and leave the original intact until a human resolves it.
4. **Cite sources.** Every new sentence or section added to the wiki must include a source event slug in parentheses or a citation line.
5. **Scope check first.** Before ingesting any source, confirm it falls within the scope defined in `purpose.md`. If it doesn't, skip it and note the skip in `provenance.md`.
6. **Archetypes require two instances.** Do not add a new archetype based on a single event. Flag it as a candidate in `_index.md` and wait for a second occurrence.

---

## Out-of-Scope Sources

If a source file contains content outside the scope defined in `shared/purpose.md` (e.g., personal notes, unrelated project data), skip that content entirely. Record the skip in `provenance.md` with the reason.
