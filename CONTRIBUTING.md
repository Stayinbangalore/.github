# Contributing to Stayin Engineering

This repository defines the default engineering workflow for repositories in the `Stayinbangalore` organization.

## Source of Truth

Stayin uses the following ownership model:

- **ClickUp** — task ownership, priority, due date, estimation, and time tracking only.
- **GitHub Issues** — requirements, technical scope, architecture discussion, decisions, acceptance criteria, cross-repository dependencies, and requirement-level QA findings.
- **GitHub Pull Requests** — implementation details, code review, CI, test evidence, screenshots, migration/deployment evidence, and implementation-specific discussion.

Do not duplicate technical discussions or acceptance criteria into ClickUp. If a technical decision happens in a meeting, DM, or call, summarize the decision in the relevant GitHub Issue or PR.

## Required Traceability

The expected flow is:

`ClickUp Task -> GitHub Issue -> Branch -> Pull Request -> Merge / Release`

The GitHub Issue is the technical parent of the work. The ClickUp task should link to the Issue. The PR should link to the Issue with `Closes #<issue>` when complete, or `Advances #<issue>` when the PR only completes part of the Issue.

## Issue Titles

Use Conventional Commit-style titles:

`type(scope): concise description in imperative mood`

Examples:

- `feat(properties): add flat guide configuration`
- `bug(pgforms): resolve deposit validation error`
- `fix(leads): correct migrated lead endpoint usage`
- `refactor(chat): simplify socket connection lifecycle`
- `docs(setup): document local environment requirements`

Supported organization types: `feat`, `bug`, `fix`, `hotfix`, `refactor`, `chore`, `ui`, `docs`.

Repository-specific standards may add additional types when needed.

## Branches

Major initiatives may use a feature branch such as:

`marketplace`

Task branches should be cut from the appropriate active feature/release branch and use:

- `feat/<issue-number>-<short-slug>`
- `bug/<issue-number>-<short-slug>`
- `fix/<issue-number>-<short-slug>`
- `hotfix/<issue-number>-<short-slug>`
- `refactor/<issue-number>-<short-slug>`
- `chore/<issue-number>-<short-slug>`
- `ui/<issue-number>-<short-slug>`
- `docs/<issue-number>-<short-slug>`

Examples:

- `feat/368-lead-filtering`
- `fix/412-pg-lead-endpoints`
- `hotfix/501-session-loop`

## Pull Request Titles

Use:

`type(scope): concise description #<issue-number>`

Examples:

- `feat(connect): add lead filtering #368`
- `fix(pgforms): resolve deposit validation #412`

The GitHub Issue number is preferred in PR titles. Keep ClickUp IDs in the parent Issue rather than duplicating them across PR titles and branches.

## Discussion Rules

Use GitHub Issues for requirement and architecture discussion. Use PR review threads for code-level discussion. Resolve review conversations before merging unless a maintainer explicitly records why a thread remains unresolved.

Repository-specific contribution files and templates may add stricter requirements for frontend, backend, database, mobile, infrastructure, or auxiliary systems.

For the complete workflow, see [`docs/ENGINEERING_WORKFLOW.md`](docs/ENGINEERING_WORKFLOW.md).
