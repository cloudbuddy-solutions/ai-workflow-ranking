# Output Template (Phase 5 reference)

Produce a plain chat artifact first, then produce a static HTML report when the environment supports creating files. Keep both plain and direct. No em-dashes, no hype.

## Plain chat artifact

```text
WORKFLOW PRIORITIZATION - [company or user]

Ranked build-first list
| # | Workflow | Type | Time | Effort | Strategic | Connected | Priority | Ready? | First move |
|---|----------|------|------|--------|-----------|-----------|----------|--------|------------|
| 1 | ...      | deterministic automation / agent / human-judgment stays | x/5 | x/5 | x/5 | x/5 | xx | yes / no (reason) | build / shadow pilot / foundation |
| 2 | ...      |      |      |        |           |           |    |        |            |
| 3 | ...      |      |      |        |           |           |    |        |            |
| - | ...      | human-judgment stays | - | - | - | - | n/a | no (human judgment) | decision support only |

Ready? column: write `yes`, or `no (reason)` so the table explains itself. Use a short gate reason: `no (baseline)`, `no (controls)`, `no (rules)`, or `no (human judgment)`. Workflows typed `human-judgment stays` are listed but not scored or ranked: use `-` for the four scores, `n/a` for Priority, and sort them below the ranked rows.

Why each one (automation thesis)
- [workflow]: A [type] could [X] because [lever Y] is missing.
- [workflow]: A [type] could [X] because [lever Y] is missing.
- [workflow]: A [type] could [X] because [lever Y] is missing.

Estimated workflow units
- [workflow]: trigger=[estimated or user-supplied trigger]; inputs=[inputs]; decision/review=[decision or review]; outputs=[outputs].
- [workflow]: trigger=[estimated or user-supplied trigger]; inputs=[inputs]; decision/review=[decision or review]; outputs=[outputs].
- If the user supplied exact units of work, write: Units supplied by user. No inferred units needed.

Rank note
#1 is the highest overall value by the formula. Recommended first build is the best first proof.

Recommended sequence
1. [workflow] - [why this is first]
2. [workflow] - [why this follows]
3. [workflow or foundation step] - [why this waits]

Assumptions and estimates
- [workflow or business proxy]: [estimated input used, why it is reasonable, and confidence: low / medium / high]
- If no estimates were used, write: None. User supplied enough direct evidence.

System sketch
Intake -> Understanding -> Decisions -> Self-running
Today, most of your work sits at: [stage]
The first build moves [workflow] from [stage] to [stage].

Recommendation
Top-ranked workflow: [workflow]
Build first: [workflow]
If different from #1: [explain the gap in one sentence, or write "same as #1"]
Why it won: [best first proof: value, ease, readiness, trust-building, and controls]
First move: [foundation step / shadow-mode pilot / build]
Before anything writes to a real system: [controls needed]
Baseline to capture first: [metric]
Related fit: [none, or note a strong paid-search/ads-optimization fit if one appears]

Open questions a person needs to answer
- [question]
- [question]
```

After the artifact, offer one next step: capture the missing baseline for a blocked top-ranked workflow, or talk through what the recommended first build would look like. Do not oversell. The honest version of this often ends with "map and measure two of these before building anything," and that is a good outcome.

## Static HTML report

When file output is available, create `workflow-ranking-report.html` after the plain chat artifact. If the environment cannot create files, include the full HTML in a fenced `html` block.

Rules:

- Static HTML only. No JavaScript, no tracking, no external CSS, no external fonts.
- Use the packaged logo at `assets/cloudbuddy-logo.png`.
- Use the packaged fonts at `assets/fonts/plus-jakarta-sans-latin-wght-normal.woff2` and `assets/fonts/inter-latin-wght-normal.woff2`.
- Prefer embedding the logo as a data URI if file tools let you read the image. If not, use `src="assets/cloudbuddy-logo.png"` and keep the alt text.
- Prefer embedding the fonts as data URIs if file tools let you read them. If not, use the relative `assets/fonts/...` URLs shown in the template.
- Keep the HTML printable and useful as a leave-behind.
- Escape user-provided text before putting it into HTML.
- Use the same scores, gates, theses, recommendation, and open questions as the plain artifact.
- Include the same workflow units, inputs, decisions, and outputs as the plain artifact when the assistant inferred or collected them.
- Include the same assumptions and estimates as the plain artifact. If none were used, write that no estimates were needed.
- Add the `active` class to the system-sketch stages that describe where the workflow is today and where the first build moves it.
- Keep the ranked table inside `.table-frame`, use the provided `colgroup`, and include `data-label` on every `td` so the table becomes readable cards on mobile.
- For score cells, use `class="score score-1"` through `score-5` and wrap the visible score in `<span class="score-value">x/5</span>`. Use `score-empty` for unscored human-judgment rows.

Use this structure and visual direction:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Workflow Prioritization - [company or user]</title>
  <style>
    @font-face {
      font-family: "Plus Jakarta Sans Variable";
      font-style: normal;
      font-weight: 200 800;
      font-display: swap;
      src: url("assets/fonts/plus-jakarta-sans-latin-wght-normal.woff2") format("woff2-variations");
    }
    @font-face {
      font-family: "Inter Variable";
      font-style: normal;
      font-weight: 100 900;
      font-display: swap;
      src: url("assets/fonts/inter-latin-wght-normal.woff2") format("woff2-variations");
    }
    :root {
      --font-heading: "Plus Jakarta Sans Variable", "Aptos Display", "Segoe UI Variable Display", "Segoe UI", ui-sans-serif, system-ui, sans-serif;
      --font-body: "Inter Variable", Inter, Aptos, "Segoe UI Variable Text", "Segoe UI", ui-sans-serif, system-ui, sans-serif;
      --font-metric: "Inter Variable", Inter, "Aptos", "Segoe UI Variable Text", ui-sans-serif, system-ui, sans-serif;
      --ink: #f4fbf8;
      --muted: #a7b5b2;
      --subtle: #7d8b88;
      --line: rgba(180, 255, 219, 0.18);
      --line-soft: rgba(220, 242, 235, 0.11);
      --green: #39e58f;
      --green-strong: #19c777;
      --green-soft: rgba(57, 229, 143, 0.14);
      --amber: #ffd166;
      --amber-soft: rgba(255, 209, 102, 0.15);
      --red: #ff6b91;
      --red-soft: rgba(255, 107, 145, 0.15);
      --surface: #081012;
      --surface-2: #0d171a;
      --surface-3: #132124;
      --shadow: 0 22px 55px rgba(0, 0, 0, 0.38);
    }
    * { box-sizing: border-box; }
    html { background: #070b0e; }
    body {
      margin: 0;
      background:
        linear-gradient(180deg, rgba(34, 214, 130, 0.13), transparent 330px),
        linear-gradient(135deg, #070b0e 0%, #0d171a 48%, #05080a 100%);
      color: var(--ink);
      font-family: var(--font-body);
      font-size: 15px;
      line-height: 1.55;
      -webkit-font-smoothing: antialiased;
      text-rendering: geometricPrecision;
    }
    .page {
      max-width: 1120px;
      margin: 0 auto;
      padding: 36px 22px 52px;
    }
    .hero {
      position: relative;
      overflow: hidden;
      display: grid;
      grid-template-columns: minmax(0, 1fr) 280px;
      gap: 28px;
      align-items: start;
      padding: 32px;
      background:
        linear-gradient(90deg, rgba(57, 229, 143, 0.12), transparent 44%),
        linear-gradient(135deg, rgba(21, 36, 40, 0.98), rgba(7, 12, 15, 0.98));
      border: 1px solid var(--line);
      border-radius: 8px;
      box-shadow: var(--shadow);
    }
    .hero > * { position: relative; }
    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      color: #91f0bd;
      font-family: var(--font-heading);
      font-size: 12px;
      font-weight: 750;
      letter-spacing: 0;
      text-transform: uppercase;
    }
    .brand img {
      width: 28px;
      height: 28px;
      object-fit: contain;
      filter: drop-shadow(0 0 10px rgba(57, 229, 143, 0.32));
      opacity: 0.92;
    }
    h1 {
      margin: 16px 0 10px;
      color: #f7fffb;
      font-family: var(--font-heading);
      font-size: 54px;
      font-weight: 800;
      line-height: 1;
      letter-spacing: 0;
    }
    .lede {
      max-width: 740px;
      margin: 0;
      color: var(--muted);
      font-size: 18px;
    }
    .summary {
      padding: 18px;
      border: 1px solid var(--line);
      border-radius: 8px;
      background: rgba(7, 12, 15, 0.64);
      box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.05);
    }
    .summary div + div { margin-top: 12px; }
    .summary span {
      display: block;
      color: #86eeb8;
      font-family: var(--font-heading);
      font-size: 12px;
      font-weight: 750;
      text-transform: uppercase;
      letter-spacing: 0;
    }
    .summary strong {
      display: block;
      margin-top: 3px;
      font-family: var(--font-heading);
      font-size: 16px;
      line-height: 1.3;
      color: #ffffff;
    }
    section {
      margin-top: 22px;
      padding: 24px;
      background:
        linear-gradient(180deg, rgba(19, 33, 36, 0.96), rgba(10, 16, 19, 0.96));
      border: 1px solid var(--line);
      border-radius: 8px;
      box-shadow: 0 14px 34px rgba(0, 0, 0, 0.26);
    }
    h2 {
      margin: 0 0 16px;
      color: #f6fffb;
      font-family: var(--font-heading);
      font-size: 21px;
      font-weight: 800;
      line-height: 1.2;
      letter-spacing: 0;
    }
    p { margin: 0 0 12px; }
    p:last-child { margin-bottom: 0; }
    .table-frame {
      max-width: 980px;
      overflow: hidden;
      border: 1px solid var(--line);
      border-radius: 8px;
      background: #081012;
      box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
    }
    .rank-table {
      width: 100%;
      table-layout: fixed;
      border-collapse: separate;
      border-spacing: 0;
      font-size: 14px;
    }
    .rank-col-number { width: 40px; }
    .rank-col-workflow { width: 175px; }
    .rank-col-type { width: 130px; }
    .rank-col-score { width: 76px; }
    .rank-col-priority { width: 72px; }
    .rank-col-ready { width: 145px; }
    .rank-col-move { width: 110px; }
    th, td {
      padding: 14px 12px;
      border-bottom: 1px solid var(--line-soft);
      text-align: left;
      vertical-align: top;
    }
    td {
      overflow-wrap: anywhere;
    }
    th {
      background: rgba(57, 229, 143, 0.08);
      color: #94a9a4;
      font-family: var(--font-heading);
      font-size: 11px;
      line-height: 1.25;
      text-transform: uppercase;
      letter-spacing: 0;
      overflow-wrap: normal;
      word-break: normal;
    }
    tr:last-child td { border-bottom: 0; }
    tbody tr:first-child td {
      background: rgba(57, 229, 143, 0.075);
    }
    tbody tr:first-child td:first-child {
      border-left: 3px solid var(--green);
      color: var(--green);
      font-weight: 800;
    }
    td[data-label="Workflow"] {
      color: #ffffff;
      font-family: var(--font-heading);
      font-weight: 700;
    }
    .rank-number {
      color: var(--subtle);
      font-family: var(--font-metric);
      font-variant-numeric: tabular-nums;
    }
    .score {
      color: #e7f2ef;
      font-family: var(--font-metric);
      font-variant-numeric: tabular-nums;
    }
    .score-value {
      display: inline-block;
      white-space: nowrap;
    }
    .score-value::after {
      content: "";
      display: block;
      width: 48px;
      height: 4px;
      margin-top: 6px;
      border-radius: 999px;
      background:
        linear-gradient(90deg, var(--green) var(--score), rgba(174, 194, 190, 0.18) var(--score));
      box-shadow: 0 0 10px rgba(57, 229, 143, 0.16);
    }
    .score-5 { --score: 100%; }
    .score-4 { --score: 80%; }
    .score-3 { --score: 60%; }
    .score-2 { --score: 40%; }
    .score-1 { --score: 20%; }
    .score-empty .score-value::after { display: none; }
    .priority {
      color: #ffffff;
      font-family: var(--font-metric);
      font-weight: 800;
      font-variant-numeric: tabular-nums;
    }
    .badge {
      display: inline-flex;
      align-items: center;
      max-width: 100%;
      padding: 4px 9px;
      border-radius: 999px;
      font-family: var(--font-heading);
      font-size: 12px;
      font-weight: 800;
      line-height: 1.2;
    }
    .yes { background: var(--green-soft); color: #80f6b6; }
    .no { background: var(--amber-soft); color: var(--amber); }
    .human { background: var(--red-soft); color: var(--red); }
    .grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 28px;
    }
    .callout {
      border-left: 4px solid var(--green);
      padding: 18px;
      background: rgba(57, 229, 143, 0.12);
      border-radius: 8px;
      box-shadow: inset 0 0 0 1px rgba(57, 229, 143, 0.08);
    }
    ol, ul { margin: 0; padding-left: 22px; }
    li + li { margin-top: 10px; }
    .flow {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 10px;
      margin-top: 14px;
    }
    .stage {
      padding: 14px;
      border: 1px solid var(--line);
      border-radius: 8px;
      background: rgba(8, 16, 18, 0.84);
      font-family: var(--font-heading);
      text-align: center;
      font-weight: 800;
    }
    .stage.active {
      border-color: rgba(57, 229, 143, 0.44);
      background: var(--green-soft);
      color: var(--green);
      box-shadow: 0 0 18px rgba(57, 229, 143, 0.10);
    }
    footer {
      margin-top: 22px;
      color: var(--muted);
      font-size: 12px;
      text-align: center;
    }
    @media (max-width: 920px) {
      .page { padding: 18px 14px 36px; }
      .hero {
        grid-template-columns: 1fr;
        gap: 20px;
        padding: 22px;
      }
      h1 { font-size: 36px; }
      .lede { font-size: 16px; }
      section { padding: 18px; }
      .grid, .flow { grid-template-columns: 1fr; }
      .summary {
        display: grid;
        grid-template-columns: 1fr;
        gap: 12px;
      }
      .summary div + div { margin-top: 0; }
      .table-frame {
        max-width: none;
        overflow: visible;
        border: 0;
        background: transparent;
        box-shadow: none;
      }
      .rank-table,
      .rank-table tbody,
      .rank-table tr,
      .rank-table td {
        display: block;
        width: 100%;
      }
      .rank-table colgroup,
      .rank-table thead {
        display: none;
      }
      .rank-table tbody {
        display: grid;
        gap: 12px;
      }
      .rank-table tr {
        padding: 14px;
        border: 1px solid var(--line);
        border-radius: 8px;
        background: rgba(8, 16, 18, 0.86);
      }
      .rank-table td {
        display: grid;
        grid-template-columns: 112px minmax(0, 1fr);
        gap: 12px;
        padding: 7px 0;
        border-bottom: 0;
      }
      .rank-table td::before {
        content: attr(data-label);
        color: var(--muted);
        font-family: var(--font-heading);
        font-size: 12px;
        font-weight: 750;
        line-height: 1.3;
        text-transform: uppercase;
      }
      .rank-table td[data-label="Workflow"] {
        grid-template-columns: 1fr;
        gap: 3px;
        padding-top: 0;
        font-size: 16px;
        font-weight: 800;
      }
      .rank-table td[data-label="Workflow"]::before {
        font-size: 11px;
      }
      .rank-table td:last-child { padding-bottom: 0; }
    }
    @media (max-width: 480px) {
      .page { padding: 12px 10px 28px; }
      .hero, section { padding: 16px; }
      h1 { font-size: 32px; }
      .rank-table td {
        grid-template-columns: 98px minmax(0, 1fr);
      }
    }
    @media print {
      body { background: #fff; }
      .page { max-width: none; padding: 0; }
      .hero, section { box-shadow: none; break-inside: avoid; }
    }
  </style>
</head>
<body>
  <main class="page">
    <header class="hero">
      <div>
        <div class="brand">
          <img src="[logo data URI or assets/cloudbuddy-logo.png]" alt="CloudBuddy">
          <span>CLOUDBUDDY WORKFLOW RANKING</span>
        </div>
        <h1>Workflow Prioritization</h1>
        <p class="lede">A build-first ranking of recurring workflows for [company or user].</p>
      </div>
      <aside class="summary">
        <div><span>Top-ranked workflow</span><strong>[workflow]</strong></div>
        <div><span>Build first</span><strong>[workflow]</strong></div>
        <div><span>First move</span><strong>[foundation / shadow pilot / build]</strong></div>
      </aside>
    </header>

    <section>
      <h2>Ranked Build-First List</h2>
      <div class="table-frame">
        <table class="rank-table">
          <colgroup>
            <col class="rank-col-number">
            <col class="rank-col-workflow">
            <col class="rank-col-type">
            <col class="rank-col-score">
            <col class="rank-col-score">
            <col class="rank-col-score">
            <col class="rank-col-score">
            <col class="rank-col-priority">
            <col class="rank-col-ready">
            <col class="rank-col-move">
          </colgroup>
          <thead>
            <tr>
              <th>#</th>
              <th>Workflow</th>
              <th>Type</th>
              <th>Time</th>
              <th>Effort</th>
              <th>Strategic</th>
              <th>Connected</th>
              <th>Priority</th>
              <th>Ready?</th>
              <th>First move</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td data-label="#" class="rank-number">1</td>
              <td data-label="Workflow">[workflow]</td>
              <td data-label="Type">[type]</td>
              <td data-label="Time" class="score score-5"><span class="score-value">x/5</span></td>
              <td data-label="Effort" class="score score-4"><span class="score-value">x/5</span></td>
              <td data-label="Strategic" class="score score-5"><span class="score-value">x/5</span></td>
              <td data-label="Connected" class="score score-3"><span class="score-value">x/5</span></td>
              <td data-label="Priority" class="priority">xx</td>
              <td data-label="Ready?"><span class="badge yes">yes</span></td>
              <td data-label="First move">[build / shadow pilot / foundation]</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <section class="grid">
      <div>
        <h2>Why Each One</h2>
        <ul>
          <li><strong>[workflow]:</strong> A [type] could [X] because [lever Y] is missing.</li>
        </ul>
      </div>
      <div>
        <h2>Recommended Sequence</h2>
        <ol>
          <li>[workflow] - [why this is first]</li>
          <li>[workflow] - [why this follows]</li>
          <li>[workflow or foundation step] - [why this waits]</li>
        </ol>
      </div>
    </section>

    <section>
      <h2>Workflow Units</h2>
      <ul>
        <li><strong>[workflow]:</strong> trigger=[estimated or user-supplied trigger]; inputs=[inputs]; decision/review=[decision or review]; outputs=[outputs].</li>
        <li><strong>[workflow]:</strong> trigger=[estimated or user-supplied trigger]; inputs=[inputs]; decision/review=[decision or review]; outputs=[outputs].</li>
      </ul>
    </section>

    <section>
      <h2>System Sketch</h2>
      <p>Today, most of your work sits at: <strong>[stage]</strong>. The first build moves <strong>[workflow]</strong> from <strong>[stage]</strong> to <strong>[stage]</strong>.</p>
      <div class="flow">
        <div class="stage active">Intake</div>
        <div class="stage active">Understanding</div>
        <div class="stage">Decisions</div>
        <div class="stage">Self-running</div>
      </div>
    </section>

    <section>
      <h2>Recommendation</h2>
      <div class="callout">
        <p><strong>Build first:</strong> [workflow]</p>
        <p><strong>Why it won:</strong> [best first proof: value, ease, readiness, trust-building, and controls]</p>
        <p><strong>Before anything writes to a real system:</strong> [controls needed]</p>
        <p><strong>Baseline to capture first:</strong> [metric]</p>
      </div>
    </section>

    <section>
      <h2>Assumptions And Estimates</h2>
      <ul>
        <li><strong>[workflow or business proxy]:</strong> [estimated input used, why it is reasonable, and confidence]</li>
      </ul>
    </section>

    <section>
      <h2>Open Questions</h2>
      <ul>
        <li>[question]</li>
        <li>[question]</li>
      </ul>
    </section>

    <footer>
      Prepared with CloudBuddy AI Workflow Ranking. Contact info@cloudbuddyapps.com.
    </footer>
  </main>
</body>
</html>
```
