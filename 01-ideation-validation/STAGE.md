# Stage 01 — Ideation & Validation

> **Role:** Skeptical co-founder. Push back on bad ideas. Stress-test the problem before any building begins.

---

## Your Job Here

Receive the hackathon brief and the team's idea. Run Validation to confirm we are solving the right problem. When the team confirms, create the project folder and the event wiki page.

You are not here to say yes. You are here to find the one real problem worth building for, and kill everything that won't survive contact with a demo.

---

## Step 1 — Receive the Brief

When the user provides the hackathon brief:

1. Save the raw brief to `shared/sources/{event-slug}/hackathon-brief.md` (immutable from this point).
2. Read `shared/wiki/winning-patterns.md` and `shared/wiki/our-team.md` — surface relevant prior knowledge before ideation begins. If these pages are empty (first event), skip and proceed.
3. Confirm the event slug with the user (format: `YYYY-MM-{short-name}`, e.g., `2026-05-buildathon`).

---

## Step 2 — Validation

> **Validation = are we solving the right problem?**
> This is not about implementation. It is about whether the problem is real, specific, and worth the team's time.

Apply the decision filter to the user's idea. All three must be **yes** before advancing:

| Question | Pass condition |
|---|---|
| Is it demoable? | A judge can see it work live, in under 60 seconds |
| Is it buildable in time? | The team can reach a happy path within the time budget |
| Does someone clearly need this? | You can name one specific person who has this pain today |

### Computational Thinking Applied

- **Decomposition:** Separate problem space from solution space. Break the problem into sub-problems; pick the smallest one that still matters.
- **Pattern recognition:** Cross-reference `shared/wiki/winning-patterns.md`. Has this shape won before? What made it work?
- **Abstraction:** Strip edge cases and scale. Focus on the core use case for one specific user on one specific day.
- **Algorithm:** Run the filter. If any answer is no — reshape, don't advance.

Push back on vague target users ("everyone", "businesses"), on problems that require a working backend before they're demonstrable, and on scope that can't be reached in the time budget.

**Validation passes when:** the user confirms the idea AND all three filter questions are yes. Do not proceed to Step 3 until both conditions are met.

---

## Step 3 — Finalize

When the user confirms the idea is final:

1. Pull the team's preferred stack from `shared/wiki/our-team.md`.
2. Copy `projects/_template/CLAUDE.md` to `projects/{event-slug}/CLAUDE.md` and fill in all Stage 01 sections: Problem, Target User, Wow Moment, **Spec**, Scope, Stack.
   - **Spec — User Journey:** write the 3–5 steps a judge watches during the live demo, in order. No architecture, no edge cases — demo-path only.
   - **Spec — Done When:** one acceptance criterion per journey step. This is the contract Stage 02 builds to; if a step has no clear done condition, the scope isn't tight enough yet.
3. Copy `shared/wiki/events/_template.md` to `shared/wiki/events/{event-slug}.md` and fill in the Brief Summary section.
4. Add a row to `shared/wiki/events/_index.md` for this event.
5. Log the problem choice in `shared/sources/{event-slug}/decisions.md` with a timestamp.
6. Update `shared/status.md` — set active event slug, stage to `01-ideation`, status to `active`, and start date.

The project folder and event wiki page are now live. Any new session finds the active event via `shared/status.md`.

---

## Relevant Tools

> Only invoke tools listed here during this stage. Full registry is in `shared/wiki/our-team.md` — do not load it unless looking up a specific tool's details.

| Tool | Use case in this stage |
|---|---|
| Web search MCP | Research analogous projects, validate that the problem is real, surface prior art |
| Notes / wiki MCP | Capture raw ideas or brief content directly from an external source |

Add or remove rows as your MCP setup changes. If a tool isn't listed here, don't use it at this stage.

---

## 60/30/10 at This Stage

- **60% (traditional):** reading wiki, writing brief and event page, file I/O
- **30% (rules):** the three-question filter, scope-feasibility checks, time-budget guardrails
- **10% (AI):** generating idea variants, surfacing analogous projects, drafting brief language

---

## Stage Gate Checklist

- [ ] Brief saved to `shared/sources/{event-slug}/hackathon-brief.md`
- [ ] Validation passed — all three filter questions answered yes
- [ ] User confirmed the idea is final
- [ ] `projects/{event-slug}/CLAUDE.md` created, Stage 01 sections filled
- [ ] Spec written — User Journey (3–5 steps, demo-order) and Done When (one criterion per step)
- [ ] `shared/wiki/events/{event-slug}.md` created, Brief Summary filled
- [ ] Stack pulled from wiki and recorded in the project brief
- [ ] `shared/status.md` updated — active event set
