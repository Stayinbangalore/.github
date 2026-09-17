# Workflow, PR & GitHub Issue Standards

This document defines the organization-wide baseline for branch architecture, Pull Request conventions, GitHub Issue standards, traceability, and engineering discussion ownership.

Repository-specific standards may add stricter requirements where the architecture requires them.

## 1. Systems of Record

### ClickUp

ClickUp is used only for project-management metadata:

- Task ownership
- Priority
- Due date
- Estimation
- Time tracking
- Link to the technical GitHub Issue

Do not use ClickUp as the source of truth for requirements, architecture, acceptance criteria, implementation decisions, QA evidence, or code-review discussion.

### GitHub Issues

GitHub Issues are the source of truth for:

- Functional and technical requirements
- Scope and non-goals
- Architecture and implementation approach discussion
- Technical decisions and clarifications
- Acceptance criteria
- Cross-repository/system dependencies
- Requirement-level QA findings
- References to designs/specifications
- Parent ClickUp task link

### GitHub Pull Requests

Pull Requests are the source of truth for:

- Actual implementation
- Code-review discussion
- CI/build/test results
- Screenshots and video evidence
- API/schema/migration evidence
- Deployment/release impact
- Implementation-specific risks and edge cases

If a technical decision happens in Teams, a meeting, call, or DM, record the outcome in the relevant GitHub Issue or PR.

## 2. End-to-End Workflow

`ClickUp Task -> GitHub Issue -> Sub-Branch -> Pull Request -> Merge / Release`

1. Create or identify the ClickUp task for ownership, priority, due date, and time tracking.
2. Create the GitHub Issue before implementation begins and link the ClickUp task in the Issue.
3. Discuss requirements, architecture, dependencies, and acceptance criteria in the Issue.
4. Create a task branch from the correct active feature/release branch.
5. Open a PR linked to the Issue.
6. Use `Closes #<issue>` / `Fixes #<issue>` only when the PR satisfies the Issue completely.
7. Use `Advances #<issue>` for partial work and keep the Issue open.
8. Record review, testing, QA evidence, migration/deployment impact, and implementation-specific decisions in the PR.
9. Merge only after required acceptance criteria and repository-specific gates are satisfied.

## 3. Branching Strategy

### Main Feature Branches

Used for major modules, epics, or release initiatives.

Pattern:

`<feature-name>`

Examples:

- `marketplace`
- `connect`
- `property-management`

### Task / Sub-Branches

Task branches should be cut from the appropriate feature/release branch.

Preferred patterns:

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
- `hotfix/501-session-expiration-loop`

The GitHub Issue number is preferred in branches because the Issue already links to the ClickUp task.

## 4. Issue Naming Convention

Issue titles use:

`type(scope): concise description in imperative mood`

Supported types:

| Type | Purpose |
| --- | --- |
| `feat` | New features or flows |
| `bug` | Unexpected behavior or regressions |
| `fix` | Diagnostic fixes or patches |
| `hotfix` | Critical production blockers |
| `refactor` | Internal code/architecture improvement without intended behavior change |
| `chore` | Dependencies, configuration, maintenance |
| `ui` | Styling, interaction, visual or micro-animation changes |
| `docs` | Documentation |

Examples:

- `feat(properties): harden flat guide handling`
- `fix(migration): correct PG lead endpoint usage`
- `bug(pgforms): resolve deposit validation error`

## 5. Pull Request Naming Convention

PR titles use:

`type(scope): concise description in imperative mood #<issue-number>`

Examples:

- `feat(connect): add lead filtering and search #368`
- `bug(pgforms): resolve deposit field validation #412`
- `hotfix(auth): fix session expiration redirect loop #501`

The PR body must contain the relationship to the Issue:

- `Closes #368` or `Fixes #368` for complete work.
- `Advances #368` for partial work.

Do not use the ClickUp task as the PR's primary technical reference. The ClickUp task belongs in the Issue.

## 6. Issue Standards

Every Issue should establish enough information to implement and verify the requirement without relying on private messages or ClickUp comments.

At minimum, Issues should provide:

- Clear summary/problem statement
- Required behavior or technical scope
- Acceptance criteria
- Dependencies/cross-repo impact when applicable
- QA/reproduction information when applicable
- ClickUp tracking link

### Labeling Model

Repositories should maintain labels in three dimensions where useful:

**Type**

- `bug`
- `feature` / `enhancement`
- `migration`
- `tech-debt`

**Domain**

- `area:properties`
- `area:leads`
- `area:chat`
- `area:auth`

Additional domain labels may be added as the product evolves.

**Platform**

- `frontend`
- `backend`
- `mobile`
- `database`
- `infrastructure`

## 7. Pull Request Requirements

Every PR must describe:

- Related GitHub Issue
- Summary of implementation
- Change type and affected areas
- API/contract impact when applicable
- Database/migration impact when applicable
- Testing actually performed
- UI evidence for visual work
- Cross-repository dependencies
- Deployment/release impact
- Known risks and edge cases

Avoid copying the entire Issue into the PR. The Issue explains **what and why**; the PR explains **how it was implemented and verified**.

## 8. Priority Framework & SLAs

The current organization priority framework is:

| Priority | Timeline | Definition |
| --- | --- | --- |
| `P0` | Within 7 days | Core feature initiatives; end-to-end scoping and release within one sprint week |
| `P1` | Immediate | Critical blockers; resolve and push the same day |
| `P2` | 24–48 hours | High-priority bugs or essential feature updates |
| `P3` | Within 3 days | Standard maintenance, tech debt, and routine sprint tasks |

Operational display hierarchy may use:

- **Urgent** — immediate operational priority
- **High** — next after urgent work
- **Normal** — standard active sprint queue
- **Low** — backlog/non-blocking improvement

Priority and SLA tracking belongs in ClickUp. Technical severity/context still belongs in the corresponding GitHub Issue.

## 9. Cross-Repository Work

When one requirement spans repositories, create an Issue in each repository that owns implementation work and cross-link them.

Example:

```text
STAYIN_CORE_DB #82
       |
       v
STAYIN_BE #811
       |
       +--> CUSTOMER_STAYIN_FE #651
       +--> BUSINESS_STAYIN_FE #403
```

The relevant Issue should identify dependencies explicitly:

```md
## Dependencies

Requires:
- Stayinbangalore/STAYIN_CORE_DB#82

Consumers:
- Stayinbangalore/CUSTOMER_STAYIN_FE#651
- Stayinbangalore/BUSINESS_STAYIN_FE#403
```

The corresponding PR should normally close only its own repository Issue.

## 10. Conversation Ownership

### Use GitHub Issues for

- Requirement clarification
- Product/technical scope changes
- Architecture decisions
- Cross-repo dependencies
- Acceptance criteria changes
- Requirement-level QA findings

### Use Pull Requests for

- Code review
- Implementation discussion
- CI/test failures
- Screenshots/videos
- Migration verification
- Deployment sequencing
- Requested code changes

### Do not

- Duplicate technical requirements into ClickUp
- Approve architecture decisions only in ClickUp
- Leave acceptance criteria only in ClickUp
- Keep implementation decisions only in private DMs/Teams
- Merge while material technical decisions exist only outside GitHub

## 11. Repository-Specific Overrides

Repositories may provide their own Issue/PR templates when additional requirements are necessary. Examples include:

- Frontend: responsive QA, screenshots, generated API types, session/auth behavior, analytics impact
- Backend: endpoint/DTO contracts, authorization, OpenAPI, queue/cron/socket impact, deployment compatibility
- Database: migration safety, backfills, production rehearsal, rollback/reconstruction, generated package release
- Mobile: platform/device testing, permissions, Firebase/service integration
- Infrastructure/auxiliary systems: cloud deployment, payload contracts, rollback and operational verification

Repository-specific standards may be stricter than this document but should preserve the same GitHub-first source-of-truth model.
