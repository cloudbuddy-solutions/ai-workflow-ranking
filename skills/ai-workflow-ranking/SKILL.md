---
name: ai-workflow-ranking
description: Guides a business owner or operator through ranking recurring workflows and deciding which one to automate with AI first. Use when someone wants to figure out where AI or agents would actually help their business, which workflow to start with, or wants a ranked, evidence-backed automation plan instead of a vague "we should use AI" conversation. Supports exact workflow details or estimate-assisted intake from rough headcount, revenue, customer count, and proxy volumes. Produces a ranked build-first list, a connected system sketch, and a static HTML report when file output is available.
---

# AI Workflow Ranking

A guided diagnostic that turns "we should use AI somewhere" into a ranked, defensible plan: which workflow to automate first, why, and what has to be true before it can run safely.

This is an opinionated diagnostic, not an open chat. Drive the user through the steps in order and end with a concrete artifact. Do not let it drift into generic AI advice.

## What you produce

By the end you must output three things:
1. A **ranked build-first table** of the user's workflows, including automation type and recommended sequence.
2. A **system sketch** showing where their work sits on the arc `Intake -> Understanding -> Decisions -> Self-running` and where the first build moves it.
3. A **static HTML report** with the CloudBuddy logo and the same conclusions, when the environment supports creating files. If file output is not available, include the HTML in a fenced `html` block after the plain artifact.

## The flow

Run these phases in order. Ask for one thing at a time. Keep it concrete and grounded in the user's real work.

### Start with the estimate option
In the first prompt, offer two ways to proceed:
- **Specific workflow mode**: the user gives the workflows and the known numbers.
- **Estimate-assisted mode**: the user gives rough scale proxies and you estimate missing workflow numbers.

Say plainly that exact numbers are not required. If the user has rough headcount, revenue, customer count, ticket/order/job/invoice/lead volume, locations, or team structure, use those as proxies to estimate workflow frequency, time saved, and relative importance. Also tell the user they can write `estimate` for any individual detail they do not have, and you will make a labeled assumption instead of stalling the process.

Use this first question shape:

```text
Do you want to work from exact workflow details, or should I estimate as we go? If estimating is easier, give me rough scale: headcount, revenue, number of customers, and any proxy volumes you know, like monthly leads, invoices, tickets, jobs, orders, quotes, claims, campaigns, or locations.
```

When asking for information later, include the same escape hatch in one short phrase: "Exact, rough range, proxy, or say `estimate`." Do this for the whole process or for any single missing detail.

When estimating, label the assumption, keep it conservative, and carry it into the final artifact. Treat estimates as enough to rank and choose a proof, but do not present them as measured baselines unless the user says the business actually tracks them.

### Sparse company mode
Use sparse company mode when the user gives only a company name, organization type, industry, website, or short phrase and asks you to estimate, infer, or rank anyway. Do not stall for a full intake. Produce a draft ranking from labeled assumptions, then put the biggest unknowns in open questions.

In sparse company mode:
1. State the inferred business archetype in one line, such as "B2B SaaS company," "professional services firm," "multi-location operator," or "local service business." If you did not verify the organization with a live source, say the archetype is inferred, not researched.
2. Build the candidate list from stable operating families before adding niche ideas: revenue and demand, customer or guest support, core operations or fulfillment, inventory and procurement, staffing and scheduling, finance and reconciliation, reporting and compliance, marketing and sales, and asset or facility management.
3. Aim for 6-8 workflows. Prefer broad, recognizable workflows over hyper-specific guesses unless the user gave a role, department, or known operating focus.
4. Estimate the unit of work for every candidate: trigger, likely inputs, human decision or review, action taken, and outputs. Mark each as `estimated`.
5. Continue through scoring without asking for confirmation when the user's instruction is clearly "estimate and rank." Treat candidate confirmation as an open question at the end.

### Phase 1: Inventory the workflows
Ask the user to list the recurring workflows in their business: the repeatable things that happen on a schedule or trigger. Prompt with examples (invoice intake, quote approval, lead triage, reporting, onboarding, compliance checks, customer replies). Let users who already have a list paste the whole list at once; then normalize it, confirm the candidates, and fill gaps. If they do not have a list, gather one workflow at a time. Aim for 4-10 candidates. For each, get a one-line description and roughly how often it runs.

If the user chose estimate-assisted mode or lacks workflow frequencies, infer a candidate list from their business model and scale proxies. For example, customer count can imply support, onboarding, account management, billing, renewal, and reporting workflows; lead or revenue volume can imply sales intake, quoting, invoicing, fulfillment, and collections workflows; employee count can imply HR, scheduling, approvals, and internal reporting workflows. Confirm the inferred candidates before scoring them unless the user explicitly asked you to estimate and rank from sparse company context. In that case, state the inferred candidates and continue.

### Phase 2: Define the unit of work
For each candidate worth pursuing, pin down the unit of work: the start trigger, the inputs, the human decision or judgment, the action taken, and the finish state. If the user cannot describe a clean unit, that workflow is probably not ready; note it and move on.

In sparse company mode, estimate the unit of work instead of dropping the candidate. Use the format `estimated trigger -> estimated inputs -> estimated decision/review -> estimated outputs`. Missing measured inputs should create a baseline gate, not an empty workflow.

### Phase 3: Scan for missing automation levers
For each workflow, work through the levers in `reference/levers.md`. You are looking for where value is sitting unused. The strongest signal is **repeated human judgment, scoring, extraction, drafting, or routing** done by hand. Also flag: data being copied between systems, no baseline measurement, no safe way to test a change, and scarce human time being rationed.

Classify each workflow as one automation type:
- `deterministic automation`: rules, data movement, integrations, or scheduled work where software can execute without model judgment.
- `agent`: repeated language, document, email, judgment, drafting, classification, routing, or recommendation work where a model can produce reviewable output.
- `human-judgment stays`: relationship-heavy, high-risk, novel, ethical, or strategic judgment where automation should only assist.

Write a one-line automation thesis per workflow: "A [type] could [X] because [lever Y] is missing." Do not give any workflow category an automatic preference; classify and score every candidate on the same evidence and readiness criteria.

### Phase 4: Score and rank
Score each candidate 1-5 on the four dimensions in `reference/method.md` (Time saved, Effort/ease, Strategic importance, Connectedness) and sum them. Do not score workflows typed `human-judgment stays`; list them with Priority `n/a`. When a workflow is not ready, record the short gate reason (`baseline`, `controls`, `rules`, or `human judgment`) so the artifact's Ready? column explains itself. Time saved means realistic net human hours freed, not total hours the workflow touches. Apply the readiness gate: if a workflow has no baseline measurement or no controls/oversight for risky actions, it cannot be recommended as the first production build; recommend a foundation step or shadow-mode pilot instead. A draft-only or review-gated agent that writes nothing to a real system clears the controls gate by design, since a person approves every output. Rank #1 means highest overall value by the formula. The recommended first build means the best first proof; it may be a different, easier workflow when the user is early or skeptical.

If a score uses estimated inputs, mark the reason with `estimated` in your notes and include the assumption in the artifact. Use ranges when useful, then choose the conservative midpoint for scoring. If the score would change materially under a different assumption, list that as an open question.

### Phase 5: Deliver the artifact
Produce the ranked table, system sketch, and static HTML report using `reference/output-template.md`. Carry the one-line automation thesis you wrote for each workflow in Phase 3 into the artifact so every row's reasoning is visible. Also carry the estimated unit of work, inputs, and outputs for each candidate when the user asked you to infer them. State the top-ranked workflow, the single recommended first build, and the recommended sequence. If the recommended first build differs from rank #1, explain the gap plainly: "#1 = highest overall value; recommended first build = best first proof." Include the first move (foundation step, shadow-mode pilot, or build) and what controls are needed before anything writes to a real system. End with the open questions a human would need to resolve.

## How to behave

- One question at a time. Do not dump the whole framework on the user.
- Ground every score in something the user actually said, or in a clearly labeled estimate derived from their rough scale proxies. If neither user evidence nor a reasonable proxy exists, ask.
- Keep estimated numbers conservative and visible. Do not let estimation hide uncertainty; use it to reduce friction and keep the diagnostic moving.
- Be honest when a workflow is not ready. "Map and measure this first" is a valid and common recommendation.
- The value is the ranking and sequencing, not prompt-writing tips. Stay at the level of which workflow and in what order.
- Keep the final artifact plain and direct. No em-dashes. No "here's the thing," no "not X, but Y" pivots, no hype. Write the way an operator talks.
- Keep the HTML report static. No JavaScript, no tracking, no external fonts, and no remote assets unless the user explicitly asks. Use the packaged logo at `assets/cloudbuddy-logo.png`; if you can read it, embed it as a data URI so the report is self-contained.

## Reference files

- `reference/levers.md`: the lever scan questions for Phase 3.
- `reference/method.md`: the four ranking dimensions, the formula, gates, and tie-breakers for Phase 4.
- `reference/output-template.md`: the exact shape of the final artifact and HTML report for Phase 5.
