# JorahOne Plugins

A Claude Code plugin marketplace that packages the agent skills used across
OneByJorah repositories, so collaborators can install the same set with one
command instead of copying skill folders around.

74 skills, grouped into 11 plugins.

## Install

Published as `OneByJorah/jorahone-plugins` (or whatever repo you push this
directory to):

```bash
claude plugin marketplace add OneByJorah/jorahone-plugins
claude plugin install agent-workflow@jorahone-plugins
```

Inside a session, the same thing:

```
/plugin marketplace add OneByJorah/jorahone-plugins
/plugin install agent-workflow@jorahone-plugins
```

Testing locally before you push:

```bash
claude plugin marketplace add ./jorahone-plugins
claude plugin install python-flask@jorahone-plugins
claude plugin list
claude plugin details python-flask
```

Installed skills are namespaced under the plugin name, so `code-review` from
`agent-workflow` runs as `/agent-workflow:code-review`.

## Plugins

| Plugin | Skills | Use it for |
|---|---|---|
| `agent-workflow` | 28 | Specs, planning, TDD, code review, debugging, git workflow, CI/CD, observability, shipping, security hardening |
| `ponytail` | 6 | Lazy senior dev mode: smallest change that works, repo audit, debt ledger, review, help |
| `python-flask` | 3 | Flask app/API patterns and pytest strategy |
| `docker-selfhosted` | 2 | Compose conventions and multi-stage Dockerfiles |
| `shell-scripting` | 3 | Defensive bash, ShellCheck config, Bats tests |
| `frontend` | 2 | React/Next performance rules, web interface guidelines |
| `design` | 20 | Interface critique and polish, design taste, motion and animation, Apple/mobile design, UI library picks |
| `windows-admin` | 2 | PowerShell, Windows Server, IIS, Active Directory |
| `security-audit` | 1 | Cloudflare security audit workflow |
| `research-focus` | 2 | Deep research with verified citations, ADHD-shaped output |
| `rea` | 5 | Reverse-engineering investigation toolkit |

## Layout

```
.claude-plugin/marketplace.json   # the catalog
plugins/<name>/
  .claude-plugin/plugin.json      # plugin manifest
  skills/<skill>/SKILL.md         # one folder per skill
```

Relative `source` paths in `marketplace.json` are resolved from this directory
(the one containing `.claude-plugin/`). Keep each entry name identical to the
`name` in that plugin's `plugin.json`.

## Updating

Edit or add skills under `plugins/<name>/skills/`, then bump `version` in both
`plugin.json` and the marketplace entry. Users receive it with:

```
/plugin marketplace update jorahone-plugins
```

Removing a marketplace also uninstalls its plugins:

```bash
claude plugin marketplace remove jorahone-plugins
```

## Sources and licensing

Every skill here is copied unmodified from an upstream repository. Credit and
license terms belong to the original authors; each skill keeps its original
`SKILL.md`, and the upstream license governs that skill.

| Skills | Upstream |
|---|---|
| agent-workflow (25 core skills) | `addyosmani/agent-skills` (via `OneByJorah/agent-skills`) |
| `code-review`, `git-guardrails-claude-code` | `mattpocock/skills` |
| `requesting-code-review` | `obra/superpowers` |
| ponytail (6) | `DietrichGebert/ponytail` |
| `flask-python` | `mindrally/skills` |
| `flask-api-development` | `aj-geddes/useful-ai-prompts` |
| `python-testing-patterns`, `bash-defensive-patterns`, `shellcheck-configuration`, `bats-testing-patterns` | `wshobson/agents` |
| `docker-patterns` | `affaan-m/ecc` |
| `multi-stage-dockerfile` | `github/awesome-copilot` |
| `vercel-react-best-practices`, `web-design-guidelines` | `vercel-labs/agent-skills` |
| `powershell-master` | `josiahsiegel/claude-plugin-marketplace` |
| `windows-server` | `bagelhole/devops-security-agent-skills` |
| `security-audit` | `cloudflare/security-audit-skill` |
| `deep-research` | `jordan-gibbs/hyperresearch` |
| design: `impeccable` | `pbakaus/impeccable` |
| design: `frontend-design` | `anthropics/skills` |
| design: `design-taste-frontend` | `leonxlnx/taste-skill` |

| design: `design-mobile-apps` | `designed-by-ai/skills` |
| design: `ui-ux-pro-max` | `nextlevelbuilder/ui-ux-pro-max-skill` |
| design: 15 motion/UI skills (`animate`, `apple-design`, `review-animations`, `write-swift`, ...) | `emilkowalski/skills` |
| `i-have-adhd` | `OneByJorah/i-have-adhd` |
| `rea` (5) | local REA skills |

Community skills run with the full permissions of the agent that loads them.
Review a plugin before installing it into an environment with production
credentials.
