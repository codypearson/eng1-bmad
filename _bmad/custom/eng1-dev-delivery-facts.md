# ENG1 delivery conventions (dev workflows)

These facts apply whenever implementing stories or quick-dev work for projects managed from this BMAD control-plane repo.

## Artifact vs code layout

- This repository (`eng1-bmad`) stores BMAD planning and implementation artifacts under the configured `_bmad-output` paths.
- Application source code lives in a **separate** project directory/repo. Never assume product code is under this BMAD `{project-root}`. Confirm the target code root with the user before editing files.

## Jira (project ENG1, Atlassian MCP)

- Represent in-progress work as **Sub-tasks** under the parent story. Move each work subtask to **Done** when that piece of work is complete.
- When story implementation is complete, create two closing subtasks and leave both in **To Do**:
  1. **Review & Test** — detailed, specific instructions for manual and/or automated testing.
  2. **Deploy** — issue type **Deploy**. Description text only when manual deploy intervention is needed (new cronjob, log monitoring, manual script run, etc.); otherwise keep the description empty/minimal. Add an appropriate line to the **Release Notes** field.

## Git branching

- Branch name = Jira ticket key lowercased (e.g. `ENG1-1234` → `eng1-1234`).
- Detect the repo default trunk as `main` or `master` (whichever exists / is the remote HEAD).
- Base branch: trunk (`main`/`master`) if the **previous** story was already merged; otherwise branch from the **previous story’s branch**.

## Pull requests

- After committing and pushing to the new branch, open a pull request.
- Prefer **GitHub MCP**; fall back to **GitHub CLI (`gh`)** if MCP is unavailable.
- PR title **must include the Jira ticket number** (e.g. `ENG1-1234: …`).
