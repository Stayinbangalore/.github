# Stayin Engineering Workflow

This is the default workflow for repositories in the `Stayinbangalore` organization.

## Where work lives

- **ClickUp** — task ownership, priority, due date, estimate, and time tracking only.
- **GitHub Issue** — requirement, discussion, decisions, acceptance criteria, and QA findings.
- **GitHub PR** — implementation, review, testing, and evidence.

Technical discussion should not live only in ClickUp, Teams, calls, or DMs. Record important decisions in the relevant GitHub Issue or PR.

## Standard flow

`ClickUp Task -> GitHub Issue -> Branch -> Pull Request -> Merge`

The ClickUp task links to the GitHub Issue. The PR links to the Issue.

Use:

- `Closes #123` when the PR completes the Issue.
- `Advances #123` when the PR is only partial work.

## Naming

Issue / PR title:

`type(scope): concise description #<issue-number>`

The Issue title does not need the trailing Issue number.

Common types:

`feat`, `bug`, `fix`, `hotfix`, `refactor`, `chore`, `ui`, `docs`

Branch examples:

- `feat/368-lead-filtering`
- `fix/412-pg-lead-endpoints`
- `hotfix/501-session-loop`

Repository-specific templates may add extra checks where needed.
