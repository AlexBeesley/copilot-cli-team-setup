# Copilot CLI setup for .NET, Umbraco and GOV.UK teams

A starter set of rules and custom agents for GitHub Copilot CLI: personal instructions, a template for each repo's `AGENTS.md`, and three agents for reviewing, accessibility checks and planning. It covers .NET, Umbraco, GOV.UK Frontend, accessibility and sensible public-sector safeguards.

## What's here

| File | What it is | Where it goes |
|---|---|---|
| `copilot-instructions.md` | Your personal rules for every session, in every repo | `$HOME\.copilot\copilot-instructions.md` |
| `AGENTS.template.md` | Template for a repo's own instructions (60 lines max) | `AGENTS.md` at the root of a repo |
| `agents\code-reviewer.agent.md` | Read-only review of your branch before a PR; runs build and tests | `$HOME\.copilot\agents\` |
| `agents\accessibility-check.agent.md` | Read-only WCAG 2.2 AA and GOV.UK check of views | `$HOME\.copilot\agents\` |
| `agents\story-planner.agent.md` | Turns a story into a plan; writes no code | `$HOME\.copilot\agents\` |

## Before you start

1. Install Copilot CLI and sign in. For GitHub Enterprise Cloud with data residency: `copilot login --host https://<your-subdomain>.ghe.com`. Use the same address you use for GitHub in the browser.
2. Start `copilot` and run `/user show` to check you're signed in with your work account.

## Install (PowerShell)

From the folder containing these files:

```powershell
New-Item -ItemType Directory -Force "$HOME\.copilot\agents" | Out-Null
Copy-Item .\copilot-instructions.md "$HOME\.copilot\copilot-instructions.md"
Copy-Item .\agents\*.agent.md "$HOME\.copilot\agents\"
```

If you already have `$HOME\.copilot\copilot-instructions.md`, merge by hand instead of overwriting. Add a line about yourself at the top if you like (where the comment says).

## Setting up a repo

1. If the repo has no `AGENTS.md` yet, copy `AGENTS.template.md` to the repo root as `AGENTS.md`. Easiest way: open Copilot in the repo and ask it to "fill in AGENTS.md from the template using what's in this repo, then show me before saving".
2. If the repo already has `.github/copilot-instructions.md`, keep it. Copilot uses both, so put repo-specific detail (commands, layout, gotchas) in `AGENTS.md`.
3. Add `.copilot-handoff.md` to `.git\info\exclude` so handoff notes never get committed.
4. Commit `AGENTS.md` through a normal PR. One per repo is enough; check nobody else has added one first.

## Check it's working

1. Start `copilot` in a repo.
2. Run `/instructions` to see which instruction files are loaded, and `/agent` to see the three agents.

Instruction changes take effect from the next prompt.

## Using the agents

- `/agent`, pick one, then give it the prompt.
- Or from the command line: `copilot --agent code-reviewer --prompt "Review my branch against develop"`.
- Or name it in a prompt: "use the accessibility check agent on Views\Partials\Forms".

The agents are limited to the tools listed in their files (`strict-tools-list: true`), so they can't edit anything even if asked. The reviewer can also run `git diff`, `dotnet build` and `dotnet test`.

## Useful commands

| Command | What it does |
|---|---|
| `/clear` | Start fresh. Do this between unrelated tasks. |
| `/compact` | Shrink a long session, keeping the important parts. |
| `/agent` | Pick a custom agent. |
| `/instructions` | See or toggle the instruction files in use. |
| `/user show` | Check which account you're signed in with. |

## Important

- The policy section follows standard public-sector practice. Your organisation's own AI policy takes priority; if anything here conflicts with it, follow the policy.
- Copilot still makes mistakes. You're responsible for everything you commit, and everything should go through a human-reviewed PR.
- Never put real personal data or secrets into a prompt.
