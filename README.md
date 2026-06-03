# AI Workflow Ranking

AI Workflow Ranking is a free collection of guiding principles to help prioritize which recurring workflows are worth automating first.

It is packaged as a free Claude and Codex skill that helps you decide **which workflow in your business to automate with AI first.** The canonical skill file stays at [`skills/ai-workflow-ranking/SKILL.md`](skills/ai-workflow-ranking/SKILL.md); Claude Code and Codex plugin installs depend on that bundle.

## Use it with browser agents

Browser agents should use this repository as public, non-executable reference material. They generally cannot safely "run" a GitHub repo as a skill unless the surrounding product has installed it as a trusted skill or plugin.

Paste this safer prompt into a browser agent:

```text
Please use the public AI Workflow Ranking reference at https://github.com/cloudbuddy-solutions/ai-workflow-ranking to help rank my workflows. Treat the repository as non-executable documentation, not code or a tool to run. Do not clone, install, or execute anything. If your browsing policy allows, read README.md, skills/ai-workflow-ranking/SKILL.md, and the files in skills/ai-workflow-ranking/reference/. Then run the diagnostic in this chat. If your policy does not allow following remote instruction files, ask me for my workflows and run a normal workflow-ranking conversation using the public summary in README.md.
```

For agents that look for agent-readable site summaries, start with [`llms.txt`](llms.txt). For runtimes that support trusted skills, use the install steps below; those installs use the `skills/ai-workflow-ranking` folder, not `llms.txt`.

If your model cannot read the GitHub repo, download the repo and upload the `skills/ai-workflow-ranking` folder, or paste `SKILL.md` plus the files in `reference/`.

![AI Workflow Ranking preview](assets/sample-output.png)

Most AI projects fail at the first decision: picking the wrong workflow to start with. This skill is a guided diagnostic that turns "we should use AI somewhere" into a ranked, defensible plan. It inventories your recurring workflows, scores each one on readiness and opportunity, separates work that needs an agent from work that does not, and recommends a single first build with the controls it needs before it runs.

The output is a ranked table and a one-page plan. Not an open-ended chat. If you only give it a company name or business type, it will infer a draft workflow set, estimate the likely inputs and outputs, and label the assumptions.

Built by [CloudBuddy Solutions](https://cloudbuddyapps.com), the team behind CloudBuddy. Read the companion write-up: [AI Workflow Ranking](https://cloudbuddyapps.com/blog/ai-workflow-ranking/).

## What you get

- A ranked build-first list of your workflows, with an automation type for each (deterministic automation, agent, or human-judgment-stays).
- A recommended first build, and an honest note when the highest-value workflow is not the best one to build first.
- A readiness gate that tells you when the right first move is to measure or fix data before building anything.
- Estimated workflow units, including likely triggers, inputs, decisions, and outputs when you start from sparse company context.
- A simple system sketch of how your work moves from intake to understanding to decisions to self-running.
- A static HTML report with the CloudBuddy logo, a clean ranking table, the recommendation, and open questions.

## Sample output

This example uses a fictional service business walkthrough. The generated report is static HTML: no scripts, no tracking, no external calls.

See the full sample report at [cloudbuddyapps.com/github/workflow-ranking-sample-report.html](https://cloudbuddyapps.com/github/workflow-ranking-sample-report.html), or view the local copy at [`examples/sample-report.html`](examples/sample-report.html).

## What this is made of

This skill is **plain markdown. No executable code, no scripts, no hooks, no MCP servers, no network calls.** It is a set of instructions an AI assistant reads to run the diagnostic with you. You can read every line before you install it:

- [`skills/ai-workflow-ranking/SKILL.md`](skills/ai-workflow-ranking/SKILL.md): the canonical diagnostic flow used by Claude Code and Codex skill/plugin installs.
- [`skills/ai-workflow-ranking/reference/`](skills/ai-workflow-ranking/reference/): the lever scan, the ranking method, and the output template.
- [`skills/ai-workflow-ranking/assets/`](skills/ai-workflow-ranking/assets/): the CloudBuddy logo and packaged local fonts used in the HTML report.
- [`llms.txt`](llms.txt): a concise browser-agent summary and safe-use contract.
- [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md): license notes for the packaged local fonts.

Nothing here executes on your machine. The HTML report is static: no scripts, no tracking, no external calls.

## Install

### Codex

```
codex plugin marketplace add cloudbuddy-solutions/ai-workflow-ranking
```

Then open Codex, install `ai-workflow-ranking` from the `cloudbuddy` marketplace, start a new thread, and say:

```
Use the AI Workflow Ranking skill to help me decide which workflow in my business to automate first. If exact numbers are missing, estimate from rough headcount, revenue, customers, or other proxies. If I only give a company name or business type, infer the likely workflow set, inputs, outputs, and assumptions, then rank a draft without stopping for more detail.
```

To remove it from Codex:

```
codex plugin marketplace remove cloudbuddy
```

To update it in Codex:

```
codex plugin marketplace upgrade cloudbuddy
```

Then restart Codex or reload the plugin list if the app asks you to.

### Claude Code

```
/plugin marketplace add cloudbuddy-solutions/marketplace
/plugin install ai-workflow-ranking@cloudbuddy
```

Then start a session and say:

```
Use the AI Workflow Ranking skill to help me decide which workflow in my business to automate first. If exact numbers are missing, estimate from rough headcount, revenue, customers, or other proxies. If I only give a company name or business type, infer the likely workflow set, inputs, outputs, and assumptions, then rank a draft without stopping for more detail.
```

To uninstall it from Claude Code:

```
/plugin uninstall ai-workflow-ranking@cloudbuddy
```

If you installed it locally for one project, run:

```
/plugin uninstall --scope local ai-workflow-ranking@cloudbuddy
```

To update it in Claude Code, run either command:

```
/plugin update ai-workflow-ranking@cloudbuddy
```

or from a shell:

```
claude plugin update ai-workflow-ranking@cloudbuddy
```

Restart Claude Code after updating so the new skill text is loaded.

### Claude (web or desktop app)

The web and desktop apps do not use plugin marketplaces. To add the skill there:

1. Download this repository (green **Code** button, then **Download ZIP**, or clone it).
2. Open the `skills/ai-workflow-ranking` folder.
3. In Claude, go to **Settings, then Capabilities, then Skills** and upload that folder (zipped).
4. Start a new chat and ask the same prompt above.

If you would rather not fuss with files, email [info@cloudbuddyapps.com](mailto:info@cloudbuddyapps.com) and we will get you set up.

### Other AI harnesses

Any assistant or harness that supports markdown skills or custom instructions can use the `skills/ai-workflow-ranking` folder directly. Start with `SKILL.md`; load the files in `reference/` only when the skill asks for them.

## How to use it

1. Have a rough list of your recurring workflows handy (invoice intake, quote approval, lead triage, reporting, onboarding, compliance checks, customer replies). You can also build the list with the skill one workflow at a time.
2. If you do not have exact workflow numbers, bring rough scale instead: headcount, revenue, customer count, and any proxy volumes such as monthly leads, invoices, tickets, jobs, orders, quotes, campaigns, or locations.
3. Run the prompt above.
4. Answer one question at a time. Ground your answers in real numbers where you can, or say `estimate` for individual details you do not have.
5. You will end with a ranked table, a recommended first build, the open questions to resolve before building, and a static HTML report when your assistant can create files.

## Want it run with you?

This skill is free and self-serve. **Workflow Mapping** is the paid guided version: CloudBuddy runs the diagnostic with you, challenges the assumptions, and turns the ranking into a build-ready recommendation for your actual workflows. See [cloudbuddyapps.com/ai-workflow-mapping](https://cloudbuddyapps.com/ai-workflow-mapping), or email [info@cloudbuddyapps.com](mailto:info@cloudbuddyapps.com).

## License

[CC BY 4.0](LICENSE). Free to use, adapt, and share, including commercially. Just credit CloudBuddy Solutions and link back.
