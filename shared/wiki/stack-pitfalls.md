# Stack Pitfalls

> Technical choices that have burned the team or saved it — compiled from post-mortems.
> Empty until first event compile. Priors listed below based on common patterns.

---

## Pitfall Format

```
### [Technology / Pattern]
- **What happened:**
- **Why it hurt (or helped):**
- **What to do instead:**
- **Source event:** {slug}
```

---

## Standing Priors (not yet event-sourced)

These are general-knowledge priors. Update or contradict them as our own evidence accumulates.

### Unvalidated External APIs
Integrating an API you haven't tested before the hackathon starts is the highest-risk dependency. Validate auth and rate limits in the first hour.

### OAuth Mid-Demo
OAuth flows that require a browser redirect can break during a live demo (popup blockers, localhost vs. deployed URL mismatch). Use a pre-authenticated token for demo day.

### LLM Latency on the Happy Path
If the model call is in the critical demo path and takes 5+ seconds, the judge's attention drifts. Cache outputs for demo-day inputs you know you'll use.

### Over-Engineering the AI Layer
Trying to do complex reasoning in a single prompt instead of decomposing into smaller, deterministic steps. Keep the 10% layer thin.

---

<!-- Compiled pitfalls added below after each event. -->
