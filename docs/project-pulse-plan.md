# Project Pulse Dashboard — Implementation Plan

## Goal

Build Mona's lightweight, contributor-friendly Project Pulse dashboard as a static app using HTML, CSS, and JSON. Do not add a framework or introduce unnecessary dependencies. The dashboard should let contributors scan project ownership, status, recent activity, priority or risk, and a short summary at a glance.

## Repository findings and constraints

- `app/` is currently empty.
- `.vscode/tasks.json` exists and defines the Copilot CLI exercise terminal task.
- `.vscode/launch.json` does not exist; create it for the dashboard launch configuration without changing `tasks.json`.
- The required application files are `app/index.html`, `app/styles.css`, and `app/project-data.json`.
- Serve the dashboard from `app/` and open `index.html` so the UI appears instead of a directory listing. Serving the page also allows it to load the JSON data over HTTP.
- Confirm the launch configuration's compatibility with the Codespace's installed VS Code support. Do not assume a launch type or extension is available before checking.
- Keep the work within the assigned files and avoid adding a framework, build pipeline, or unrelated tooling.

## File ownership

| File | Owner | Responsibility |
| --- | --- | --- |
| `app/index.html` | Coder | Semantic page structure, dashboard container/hooks, and loading/rendering behavior for project data. |
| `app/styles.css` | Designer | Layout, visual styling, responsive behavior, accessibility-oriented presentation, and the `.dashboard` and `.project-card` hooks. |
| `app/project-data.json` | Coder | Static project records using the agreed data shape below. |
| `.vscode/launch.json` | Coder | The named **Run Project Pulse Dashboard** launch configuration, serving from `app/` and opening `index.html`; confirm launch-type compatibility in the Codespace. |

The Designer provides design guidance and reviews the experience; the Designer's file implementation scope is `app/styles.css`. The Coder owns the HTML, JSON, and launch configuration. The Orchestrator coordinates these boundaries and integrates the results.

## Data contract

`app/project-data.json` must have a top-level `projects` array. Each project object must include:

- `name` — project name.
- `owner` — responsible owner.
- `status` — current status, displayed as a clearly labeled status badge.
- `recentActivity` — concise recent activity text.
- `priority` — priority or risk level, shown with readable text rather than color alone.
- `summary` — additional agreed field, providing the brief's contributor-friendly summary.

Keep the JSON valid and use consistent, meaningful values for all records. Treat the required fields as presentational content, not executable markup.

## Phases, dependencies, and coordination

### 1. Orchestrator kickoff and scope

The Orchestrator confirms the brief, repository findings, file ownership, data contract, and validation criteria with the Planner, Designer, and Coder. Keep implementation within the listed files.

### 2. Parallel planning and design

The Designer can work in parallel with the Coder's initial data and launch investigation:

- **Designer:** define information hierarchy and card presentation; plan layout, spacing, typography, status/priority treatment, responsive behavior, and accessibility. Specify how the `.dashboard` and `.project-card` hooks will be used in `app/styles.css`.
- **Coder:** prepare representative records in `app/project-data.json`; inspect the Codespace's installed VS Code support to determine a compatible launch configuration. Do not finalize a guessed launch type.
- **Orchestrator:** clarify cross-file expectations, especially the HTML class hooks and the data fields, and relay them to both agents.

These workstreams can proceed in parallel because the data schema and CSS hooks are agreed in this plan. The launch investigation is independent of the visual design.

### 3. Sequential implementation and integration

1. **Coder** establishes the HTML structure and data-loading/rendering contract in `app/index.html`, using `.dashboard` and `.project-card` hooks agreed with the Designer. Include clear loading, successful content, empty-data, and data-load/parse error behavior.
2. **Designer** implements `app/styles.css` against those agreed hooks and the planned semantic structure. If hook names or markup need to change, coordinate with the Coder before changing the shared contract.
3. **Coder** completes `app/project-data.json` and `.vscode/launch.json`. The launch configuration must be named **Run Project Pulse Dashboard**, serve from `app/`, and open `index.html` rather than a directory listing. Confirm that its selected launch type is supported by the installed Codespace VS Code environment.
4. **Orchestrator** integrates the files, resolves any contract mismatches, and runs the validation checklist. Changes to HTML structure and corresponding CSS are sequentially coordinated to avoid styling against stale markup.

The Designer's CSS work may begin while the Coder implements HTML once the class-hook and structure contract is established. Final integration and end-to-end launch verification must happen after all four assigned files are present.

## Responsibilities

### Designer

- Establish a clear information hierarchy that makes project name, owner, status, recent activity, priority/risk, and summary easy to scan.
- Design a polished card-based layout with readable spacing, legible typography, and a consistent status-badge treatment.
- Implement visual styling and responsive layouts in `app/styles.css`, including the `.dashboard` and `.project-card` hooks.
- Address accessibility: sufficient text contrast, visible focus treatment for any interactive controls, meaningful heading hierarchy support, and no reliance on color alone to convey status or priority.
- Check the layout at narrow and wide viewport sizes and avoid horizontal overflow.

### Coder

- Build semantic page structure and the data-driven rendering behavior in `app/index.html`; load project records from `app/project-data.json` and render the agreed fields.
- Handle loading, empty `projects`, malformed/unavailable JSON, and missing or blank field values without leaving an unexplained blank page.
- Populate `app/project-data.json` with valid JSON, a top-level `projects` array, and all required fields plus `summary` on each record.
- Create `.vscode/launch.json` with the **Run Project Pulse Dashboard** configuration, serving from `app/` and opening `index.html`; verify the configuration is compatible with installed Codespace VS Code support.
- Validate the browser experience and launch behavior after integration.

### Orchestrator

- Delegate work by the file ownership table and preserve the agreed HTML/CSS hooks and JSON contract.
- Coordinate the Designer and Coder at the handoff between structure and styling; surface integration changes before they create rework.
- Ensure the launch choice is based on available VS Code support rather than an unverified assumption.
- Review the integrated result against the brief and validation checklist; request focused fixes where needed.

## Edge cases and implementation constraints

- Empty or missing project data must produce a useful empty state rather than an empty dashboard.
- Failed data loading or invalid JSON must result in a clear, user-facing error state; do not silently fail.
- Guard display of absent or blank fields with readable fallback text so one incomplete record does not break rendering.
- Escape or safely insert data as text; project data should not be interpreted as HTML.
- Status and priority must remain understandable without color, including in high-contrast conditions.
- Narrow screens must retain readable cards and avoid horizontal scrolling.
- Do not rely on opening the HTML as a local `file://` page to load JSON; use the launch configuration's server behavior.
- Preserve `.vscode/tasks.json`; the dashboard's run configuration is a separate addition.

## Validation expectations

The Orchestrator and Coder should confirm:

1. Only the assigned files are created or changed: `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`.
2. `app/project-data.json` parses as JSON, has a top-level `projects` array, and every project contains `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
3. The dashboard loads through the launch configuration and displays the UI from `app/index.html`, not a server directory listing; JSON loads successfully from the served `app/` directory.
4. Project cards display all agreed fields, status and priority remain identifiable without color, and loading/empty/error cases are understandable.
5. The dashboard remains readable at narrow and wide viewport sizes, with no horizontal overflow; semantic structure, text contrast, and keyboard-visible focus are checked.
6. The launch configuration is named **Run Project Pulse Dashboard**, uses `app/` as its serving root, opens `index.html`, and is compatible with the Codespace's installed VS Code support.
7. Existing `.vscode/tasks.json` remains unchanged and no framework or unrelated tooling has been introduced.
