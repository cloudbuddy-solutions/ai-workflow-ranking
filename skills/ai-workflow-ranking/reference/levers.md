# Lever Scan (Phase 3 reference)

For each workflow, check where each lever is missing or weak. A weak lever is an opportunity. The first five are where AI and agents help directly. Ask plainly; keep it in plain business language.

For any number you need, accept exact numbers, rough ranges, proxy volumes, or `estimate`. Useful proxies include headcount, revenue, active customers, monthly leads, tickets, invoices, orders, quotes, jobs, claims, campaigns, locations, and team structure. If the user gives only proxies, infer conservatively and label the estimate.

Before scoring, classify the workflow by automation type:
- `deterministic automation`: rules, scheduled work, data movement, reconciliation, alerts, reports, or integrations where model judgment is not needed.
- `agent`: repeated judgment, extraction, drafting, classification, triage, routing, summarization, or recommendations where model output can be reviewed.
- `human-judgment stays`: novel, high-risk, relationship-heavy, ethical, legal, strategic, or trust-sensitive decisions where automation should only assist.

Do not force every opportunity into `agent`. Some of the best first builds are deterministic automations or measurement foundations.

## 1. Repeated judgment (the main one)
Look for the same human judgment applied to the same kind of input over and over.
- Is someone reading documents or emails and pulling the same fields each time?
- Is a decision made by applying the same rules to the same inputs?
- Is content drafted from a template plus a few variables?
- Is work triaged or prioritized by hand?
A "yes" here is the strongest agent candidate. Capture the decision being made.

## 2. Data movement between systems
- Do people copy or paste between systems (CRM to spreadsheet to email)?
- Do the tools expose APIs, or only screens a person clicks?
- Is there manual re-keying or reconciliation?
Weak here means an integration step may be needed before the agent works.

## 3. Measurement
- Is there a baseline today (time, cost, cycle time, error rate)?
- Does anyone see this workflow's health in real time, or only when it breaks?
No baseline means one must be captured before a pilot can prove anything. A rough estimate can support ranking, but it is not a measured baseline unless the user says the business tracks it.

## 4. Safe experimentation
- Can a new approach run quietly alongside the current one (shadow mode)?
- Can it be tested on a slice of the work?
Weak here means recommend a shadow-mode pilot, not a production build.

## 5. Human capacity as the bottleneck
- Is this a mostly repetitive full-time job?
- Does work back up when one person is out?
- Are they hiring for work software could absorb?
Strong here means high payoff. Estimate hours freed per cycle.
