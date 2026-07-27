# eng1-bmad

BMAD control-plane repo for ENG1 projects. Planning and implementation artifacts live here; application source code lives in separate project repositories.

## What is committed vs installed

| Path | In git? | Notes |
|------|---------|--------|
| `_bmad/custom/` | Yes (team) | Team overrides, delivery facts, pinned output paths |
| `_bmad/custom/*.user.toml` | No | Personal overlays (gitignored) |
| `_bmad-output/` | Yes | PRDs, architecture, epics, sprint status, stories |
| `docs/` | Yes | Shared project knowledge |
| `_bmad/` (everything else) | No | Recreated by the installer |
| `.agents/` | No | Skills installed for Cursor |

After cloning, you must run the BMAD installer locally. Team customizations under `_bmad/custom/` survive reinstalls and merge over installer defaults.

## Prerequisites

- [Node.js](https://nodejs.org) **v20.12+**
- [Python](https://www.python.org) **3.10+** (3.11+ recommended for `tomllib`)
- [uv](https://docs.astral.sh/uv/) recommended (BMad scripts increasingly use `uv run`)
- [Cursor](https://cursor.com) (this repo is set up with the `cursor` tool target)
- Network access for `npx` / GitHub as needed by the installer

Optional but expected for ENG1 delivery workflows:

- Atlassian MCP (Jira project **ENG1**)
- GitHub MCP (preferred) or GitHub CLI (`gh`) for pull requests

## Install BMAD into this repo

From the repo root:

```bash
npx bmad-method install
```

Recommended answers for this repo:

1. **Directory** — current directory (this repo)
2. **Modules** — **BMad Method** (`bmm`); core is included automatically
3. **Channel** — stable (default) unless you intentionally want prerelease
4. **Tools / IDEs** — **Cursor**
5. **Config prompts** — accept defaults; team paths are pinned in `_bmad/custom/config.toml`

### Non-interactive (CI / repeatable local setup)

```bash
npx bmad-method install \
  --yes \
  --directory . \
  --modules bmm \
  --tools cursor
```

Prerelease installer (only when you need it):

```bash
npx bmad-method@next install --yes --directory . --modules bmm --tools cursor
```

Official install reference: [How to Install BMad](https://docs.bmad-method.org/how-to/install-bmad/)

## After install

1. Open this folder in Cursor.
2. Confirm skills appear (e.g. `bmad-help`, `bmad-sprint-planning`, `bmad-dev-story`).
3. Ask: `bmad-help what should I do first?`
4. When implementing, point agents at the **application code repo/directory** — not only this control-plane repo.

## Updating BMAD

Re-run the installer in this directory:

```bash
npx bmad-method install
```

Choose **Quick Update** to refresh with existing settings, or **Modify Install** to change modules/tools. Team files under `_bmad/custom/` are not overwritten by the installer.

## Layout

```text
eng1-bmad/
├── README.md
├── .gitignore
├── _bmad/
│   └── custom/                 # committed team customizations
│       ├── config.toml         # pinned output paths for this control plane
│       ├── eng1-dev-delivery-facts.md
│       ├── bmad-sprint-planning.toml
│       ├── bmad-dev-story.toml
│       └── bmad-quick-dev.toml
├── _bmad-output/               # committed BMAD artifacts
│   ├── planning-artifacts/
│   └── implementation-artifacts/
└── docs/                       # shared project knowledge
```

Installer-managed paths (ignored): `.agents/`, `_bmad/config.toml`, `_bmad/scripts/`, `_bmad/core/`, `_bmad/bmm/`, `_bmad/_config/`, etc.

## Customization

ENG1 delivery rules (Jira ENG1, git branch naming, PRs, Review & Test / Deploy subtasks) live under `_bmad/custom/`. Use the `bmad-customize` skill to change them, or edit those files directly. See [How to Customize BMad](https://docs.bmad-method.org/how-to/customize-bmad/).
