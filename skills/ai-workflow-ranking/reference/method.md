# Ranking Method (Phase 4 reference)

Score each candidate workflow 1-5 on four dimensions, then sum. Carry forward the automation type from the lever scan: `deterministic automation`, `agent`, or `human-judgment stays`.

Exact numbers are preferred, but rough estimates are allowed when the user chooses estimate-assisted mode or says `estimate` for a detail. Base estimates on conservative proxies such as headcount, revenue, active customers, monthly leads, tickets, invoices, orders, quotes, jobs, claims, campaigns, locations, or role/team structure. Label estimated inputs in the notes and final artifact.

| Dimension | Question | 1 | 5 |
| --- | --- | --- | --- |
| Time saved | Realistic net human time per cycle freed by automating it | Minutes, rarely | Many hours, constant |
| Effort (ease) | How easy the build is, given data and integration readiness | Big lift, missing data/APIs | Data ready, clear rules, fast |
| Strategic importance | How much it moves what the business cares about | Nice-to-have | Tied to revenue, risk, or a core promise |
| Connectedness | Whether it is a hub others depend on | Isolated | Unlocks several downstream steps |

## Formula

```text
Priority = TimeSaved + Effort(ease) + StrategicImportance + Connectedness
```

Equal weight by default. Only re-weight with a stated reason. Example: a user who needs to show results fast gets Time saved and Effort weighted higher so a quick win surfaces first.

Time saved is net hours freed, not total hours the workflow touches. Subtract work that still remains for review, exception handling, relationship management, or judgment. If a workflow takes 60 hours per week but automation only removes 12 hours of copy/paste and drafting, score the 12 hours.

When estimating time saved:
- Start from volume times human minutes per item, then subtract review and exception time.
- If only headcount is known, estimate the affected team's weekly repetitive admin time conservatively, not the whole team's capacity.
- If only revenue and customers are known, infer likely transaction volume only when the business model makes that reasonable; otherwise ask for a proxy volume.
- Use a range when uncertainty is high and score from the conservative midpoint.

Automation type does not add points. It changes the recommendation:
- `deterministic automation`: recommend an integration, script, workflow automation, or dashboard before calling it an agent.
- `agent`: recommend a model-assisted build when inputs, review path, and controls are clear.
- `human-judgment stays`: recommend decision support, measurement, checklists, or retrieval. Do not frame it as a self-running agent. Do not score or rank these; list them with Priority `n/a` so they appear in the inventory without competing for the first build.

## Gates (override the first-build recommendation)

- If a workflow has no baseline measurement, it can still be #1 by priority, but it cannot be the first production build. First move: capture a baseline.
- An estimated baseline is enough to rank and pick a proof, but it is not the same as a measured baseline. If production ROI or production rollout depends on an estimated baseline, make the first move `foundation` or `shadow pilot` to capture the real baseline.
- If risky or irreversible actions have no human approval or oversight, it can still be #1 by priority, but it cannot be the first production build. First move: add controls, or pilot in shadow mode. A draft-only or review-gated agent that writes nothing to a real system (a person approves every output) clears this gate by design; do not block it for lacking controls.
- If the rules are tribal knowledge no one can write down, cap it; the rules must be made explicit first.
- If the automation type is `human-judgment stays`, do not recommend it as the first automation build. First move: make the judgment visible, measurable, and better supported.

## Tie-breakers

- New or skeptical user: pick the easiest high-value item first to prove the method.
- Save the connected hub workflow for the second build, once trust exists, because it touches more and carries more risk.
- The #1 ranked workflow is the highest overall value by the formula. The recommended first build is the best first proof. If those differ, say so and show the recommended sequence.

## Sequencing into a system

The ranked list is "what first." Show how it connects using the arc:

```text
Intake  →  Understanding  →  Decisions  →  Self-running
```

Place the user's workflows on that arc as they are today, then show where the first build moves the chosen one. The goal over time is a connected system, not a pile of point automations.
