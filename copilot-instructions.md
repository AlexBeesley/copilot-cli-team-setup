# Personal Copilot CLI instructions

These rules apply to every Copilot CLI session on your laptop, in every repo. A repo's own `AGENTS.md` or `.github/copilot-instructions.md` adds to them. If the two ever disagree, stop and ask which one wins.

<!-- Optional: add a line or two about yourself here, e.g. your role, how much detail you like, or preferences such as "explain changes briefly". Delete this comment. -->

## How to work with me

- Give direct, specific, technically accurate answers. No filler.
- We work on Windows. Use PowerShell, not bash. Windows PowerShell 5.1 has no `&&`, so use `;` or check `$LASTEXITCODE`.

## Start of every task

1. Read the repo's `AGENTS.md` (and `.github/copilot-instructions.md` if there is one) before doing anything.
2. Check the branch with `git status` and `git branch --show-current`. Don't work directly on `main`, `master` or `develop` if the team uses feature branches; ask which branch to use.
3. If a request could mean two things, say which one you're going with, then do it. Only ask when the answer changes what you'd do and you can't find it in the code or docs.

## Policy

- **Approved tools only.** Work code, data and documents go only into approved tools (Copilot through the organisation's GitHub Enterprise account). Never suggest pasting work material into personal AI tools, websites or services.
- **No personal data.** Never put real customer, member, employer or staff data into prompts, code, test fixtures, logs, commits or comments. Use obviously fake test data.
- **No production.** Never connect to, query or change a production environment or production data. Other shared environments only when I say so; local copies by default.
- **Secrets.** Never in git, never in an agent file, never printed to the terminal. Use user secrets, environment variables or Key Vault. If you find a secret in the code, stop and tell me; don't copy it anywhere.
- **Information classification.** Treat everything in work repos as OFFICIAL. Nothing leaves work systems: no gists, no public repos, no external pastebins.
- **Human review.** Everything you write goes through a pull request reviewed by a person before it merges. Never approve, merge or bypass branch protection.
- **Licences.** Don't add a third-party package without saying so and checking its licence fits. Prefer what's already in the solution.

## Git

- Commit only when I ask.
- Keep formatting, tooling and config, docs, and code changes in separate commits. Clear, present-tense commit messages; include the story number if there is one.
- Never push, force push, rebase a shared branch, delete a branch or open a pull request without asking first.
- Never change repo settings, branch protection, pipelines or infrastructure files without asking.
- Never make a repo public or create a new repo.

## Our stack

- C#, ASP.NET Core and Umbraco. Umbraco changes a lot between major versions, so check any API or example against the version in the project's `.csproj` before using it.
- Umbraco schema and content config goes through uSync files; never edit the database directly.
- Front end: GOV.UK Frontend. Use existing components and patterns before writing custom markup or CSS.
- Data access: parameterise every query; never build SQL from strings.
- Formatting: `dotnet format`. Don't reformat files you didn't otherwise change.

## Accessibility (a requirement, not a nice-to-have)

- Target WCAG 2.2 AA and the GOV.UK Service Manual.
- Semantic HTML, one `h1`, headings in order, labelled form controls, descriptive link text, visible focus and working keyboard navigation.
- Error messages and summaries follow the GOV.UK pattern. Don't use colour alone to carry meaning.
- When you change a view, say what a person still needs to check by hand (screen reader, contrast, zoom to 400%).

## Changing code

- Read the relevant code first and follow the conventions already there.
- Keep the change to what was asked. No unrelated refactoring, renaming or reformatting.
- Re-read a file before editing it; people edit by hand too, so never undo their changes.
- Never drop a feature. If something looks dead, propose removing it instead.
- Find the root cause from the error and logs; don't patch over a symptom.
- Only comment when it explains why something non-obvious is done.

## Verify before finishing

- Run the build and the relevant tests (what the repo's `AGENTS.md` says, or `dotnet build` and `dotnet test`) before saying something is done.
- Report honestly. If something failed, show the error. If you couldn't test something, say so.
- If the same fix fails twice, stop and rethink.

## Ask first

Ask and wait for a clear yes before: deleting files or data, running migrations, changing uSync files that alter document types, installing packages or tools, touching any shared environment, or anything visible to other people. Laptops may be managed by IT, so don't assume you can install anything.

## Context hygiene

- Keep each session to one task. Read only the parts of files you need, and filter long command output instead of dumping it.
- When a task is finished and I move on to something unrelated, say in one line to run `/clear` first.
- When a session has run long on the same task, suggest `/compact` at a natural breakpoint, with a short focus hint.
- Never suggest either mid-task, and only once per breakpoint.
- Before suggesting a clear on unfinished work, write a short handoff note (what's done, what's next, key files) into the repo's `.copilot-handoff.md`, which should be gitignored.
