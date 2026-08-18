# ENG1 delivery conventions (dev workflows)

These facts apply whenever implementing stories or quick-dev work for projects managed from this BMAD control-plane repo.

## Artifact vs code layout

- This repository (`eng1-bmad`) stores BMAD planning and implementation artifacts under the configured `_bmad-output` paths.
- Application source code lives in a **separate** project directory/repo. Never assume product code is under this BMAD `{project-root}`. Confirm the target code root with the user before editing files.

## Jira (project ENG1, Atlassian MCP)

- Standard subtasks may already exist under the parent ticket — **check before creating**. Reuse existing subtasks when present (match by title); only create ones that are missing.
- Standard subtask set under the story/ticket:
  1. **Development** — catch-all for development work. Set to **In Progress** when work starts; set to **Done** when ready for review.
  2. **Code Review** — developer-centric testing/review procedures (replaces former "Review & Test"). Include detailed instructions aimed at a developer. Leave **To Do** until that review work begins.
  3. **Stakeholder Review** — **decision point**: ask the user whether this is needed. If yes, create or keep it with simple testing instructions for a non-technical user, leave **To Do**. If no, ensure the subtask exists (create if missing), add a comment explaining why Stakeholder Review is not needed, then set it to **Done**.
  4. **Deploy** — issue type **Deploy**. Description text only when manual deploy intervention is needed (new cronjob, log monitoring, manual script run, etc.); otherwise keep the description empty/minimal. Add an appropriate line to the **Release Notes** field. Leave **To Do** when ensured at completion.

## Git branching

- Branch name = Jira ticket key lowercased (e.g. `ENG1-1234` → `eng1-1234`).
- Detect the repo default trunk as `main` or `master` (whichever exists / is the remote HEAD).
- Base branch: trunk (`main`/`master`) if the **previous** story was already merged; otherwise branch from the **previous story’s branch**.

## Pull requests

- After committing and pushing to the new branch, open a pull request.
- Prefer **GitHub MCP**; fall back to **GitHub CLI (`gh`)** if MCP is unavailable.
- PR title **must include the Jira ticket number** (e.g. `ENG1-1234: …`).
