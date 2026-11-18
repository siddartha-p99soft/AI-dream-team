# Project Pulse implementation plan

## Goal

Build a polished, responsive static dashboard that lets contributors scan project ownership, status, recent activity, and priority. The repository has an empty `app/` directory, no app framework or test suite, and an existing `.vscode/tasks.json` for Copilot CLI that must remain unchanged.

## Phases and assignments

| Phase | Assignment | Files and outcome |
| --- | --- | --- |
| 1. Agree on the contract | Orchestrator coordinates; Planner confirms requirements, dependencies, and ownership. Designer defines information hierarchy and responsive/accessibility decisions; Coder agrees on the markup/data contract. | No implementation files. Confirm `.dashboard`, `.project-card`, field names, and status/priority presentation before parallel work. |
| 2. Build independent pieces | Designer implements the visual system and responsive layout. Coder creates representative project data and runnable-app configuration. | Designer: `app/styles.css` (including `.dashboard`, `.project-card`, rounded corners, shadows, and responsive layout). Coder: `app/project-data.json` and `.vscode/launch.json`. These can proceed in parallel after the contract is agreed. |
| 3. Integrate the page | Coder implements the page against the agreed design and data contract; Designer reviews visual/accessibility consistency. | Coder: `app/index.html`, referencing `styles.css` and loading `project-data.json`; render each project as a `.project-card` showing `status`, `recentActivity`, and `priority`. Exact UI title: **Project Pulse**. |
| 4. Validate integration | Coder runs the app checks; Orchestrator verifies requirements and reports results. | Validate all four target files and leave `.vscode/tasks.json` untouched. |

The page depends on the JSON contract (`projects` array; every project has `name`, `owner`, `status`, `recentActivity`, and `priority`) and the Designer's agreed CSS hooks. Thus data/config and CSS can be prepared in parallel after Phase 1; page integration follows those contracts. There is no framework or test suite to extend.

## Launch configuration

Create `.vscode/launch.json` as strict JSON. Add a configuration named **Run Project Pulse Dashboard** with command `python3 -m http.server 5500`, `cwd` `${workspaceFolder}/app`, and a `serverReadyAction` using `uriFormat` `http://localhost:%s/index.html` to open the page. The launch command serves `app/`; the readiness action opens `index.html` rather than the server directory listing. `launch.json` configures this behavior—it is not itself a server. Do not add or modify `tasks.json`.

## Validation

- Parse `project-data.json`; confirm a top-level `projects` array and all five required fields on every entry.
- Confirm `index.html` has the exact title, references the CSS and JSON, and renders `.project-card` elements with status, recent activity, and priority.
- Confirm CSS includes `.dashboard` and `.project-card`, rounded corners, shadows, and a responsive layout.
- Parse `launch.json` as strict JSON and check the exact name, command, working directory, and readiness URL.
- Run `python3 -m http.server 5500` from `app/` and verify the readiness URL serves the dashboard page, not a directory listing. Confirm `.vscode/tasks.json` is unchanged.
