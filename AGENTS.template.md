# <Project name>

<!-- Template for a repo's AGENTS.md. Fill in the <...> parts, delete what doesn't apply, and keep it to 60 lines or fewer. Delete this comment. -->

<One or two sentences: what this project is and who uses it.>

## Stack

- .NET <version>, Umbraco <version>, GOV.UK Frontend <version>
- <Database, other key packages>

## Commands (PowerShell)

| Task | Command |
|---|---|
| Restore | `dotnet restore` |
| Build | `dotnet build <Solution>.sln` |
| Run locally | `dotnet run --project <path\to\Web.csproj>` |
| Test | `dotnet test <path or solution>` |
| Format | `dotnet format <Solution>.sln` |
| Front-end build | `<npm run build, if any>` |

Run Build and Test before saying a change is done.

## Layout

- `<src\Project.Web>`: <what lives here>
- `<src\Project.Core>`: <what lives here>
- `<tests\...>`: <unit, integration>
- `<uSync\>`: Umbraco schema and content config. Change only when asked.

## Git and branches

- Branch from `<develop or main>`. Name branches `<feature/STORY-123-short-name>`.
- Pull requests target `<develop>` and need a human review.
- Never push, merge or touch `<main>` or the pipelines without asking.

## Environments

- Local: <how to get a local copy, e.g. connection string in user secrets>
- Test environments: only when asked. Production: never.

## Hands off

- `<pipeline files, infrastructure folder>`
- `<appsettings.Production.json, anything with secrets>`
- <Generated or vendored folders>

## Things to know

- <Gotchas: odd build steps, known flaky tests, packages pinned for a reason>
- <Who owns what, if it matters>
