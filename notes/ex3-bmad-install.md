# Exercise 3 — Install BMAD, and know what it costs

Installed with `npx bmad-method install`, interactively, with Claude Code as the only IDE.

## What the manifest says

`_bmad/_config/manifest.yaml`:

- Version: `6.12.4`
- Modules: `core`, `bmm`
- IDEs: `claude-code` (only)

## What it created on disk

| Path | What it is | Size |
|---|---|---|
| `.claude/skills/` | 29 `bmad-*` skills (no other skills) | ~2.1 MB |
| `_bmad/` | `_config`, `core`, `bmm`, `custom`, `render`, `scripts`, `config.toml`, `config.user.toml` | ~159 KB |
| `_bmad-output/` | Empty for now; the planning artifacts land here from exercise 5 | — |

No `.agents/` folder: the first install had `cursor` and `antigravity-cli` checked too, which copied the skills there as well. It was removed and reinstalled with Claude Code only.

## What survives a re-install

- **Survives untouched:** `_bmad/custom/`. The installer never touches it, so overrides belong there.
- **Does not survive:** `_bmad/config.user.toml`. It is regenerated on every install; direct edits are overwritten.
- **Not committed:** `_bmad/custom/*.user.toml` (personal overrides) and everything under `_bmad/render/`.

## What it costs every session

From `/skills`, sorted by tokens (`t`). Only each skill's name and description load at session start; the body loads only when the skill runs.

| Skill | Tokens |
|---|---|
| `bmad-deep-recon` | ~250 |
| `bmad-review` | ~180 |
| `bmad-build` | ~160 |
| `bmad-architecture` | ~130 |
| `bmad-spec` | ~130 |
| `bmad-sprint-planning` | ~130 |
| `bmad-forge-idea` | ~120 |
| `bmad-retrospective` | ~110 |
| `bmad-prfaq` | ~110 |
| `bmad-party-mode` | ~100 |
| `bmad-correct-course` | ~80 |
| `bmad-ux` | ~80 |
| `bmad-advanced-elicitation` | ~80 |
| `bmad-project-context` | ~70 |
| `bmad-walkthrough` | ~70 |
| `bmad-help` | ~70 |
| `bmad-customize` | ~70 |
| `bmad-code-review` | ~60 |
| `bmad-agent-analyst` | ~60 |
| `bmad-qa-generate-e2e-tests` | ~50 |
| `bmad-agent-dev` | ~50 |
| `bmad-brainstorming` | ~50 |
| `bmad-agent-pm` | ~50 |
| `bmad-agent-architect` | ~50 |
| `bmad-create-epics-and-stories` | ~50 |
| `bmad-product-brief` | ~50 |
| `bmad-agent-ux-designer` | ~40 |
| `bmad-prd` | ~40 |
| `bmad-build-auto` | ~30 |
| **Total (29 skills)** | **~2,520** |

About 2.1 MB of skills on disk cost about 2,520 tokens per session, because of progressive disclosure. The `user` and `claude.ai sync` skills load in every project and are not counted here.
