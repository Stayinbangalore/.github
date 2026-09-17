# Workflow, PR & GitHub Issue Standards

This document defines the branch architecture, Pull Request (PR) conventions, GitHub Issue standards, templates, and end-to-end task workflows for the engineering organization.

## 1. Branching Strategy

To keep development organized and isolate release cycles, all repositories follow a two-tier branching model:

- **Main Feature Branches**: Used for high-level modules, epics, or major feature initiatives.
  - Pattern: `<feature-name>`
  - Examples: `marketplace`, `connect`, `property-management`
- **Sub-Branches**: Isolated branches cut from the main feature branch for specific tasks, fixes, or components.
  - Pattern: `<type>/<task-id>` or `<type>/<task-name>`
  - Examples:
    - `bug/742v8u`
    - `fix/flat-forms`
    - `feat/lead-filtering`
    - `chore/deps-update`

## 2. Pull Request (PR) Naming Convention

All PR titles must follow Conventional Commits syntax appended with either the **GitHub Issue ID** or the parent **ClickUp Task ID**:

`type(scope): concise description in imperative mood #Id`

### ID Selection Rule

**Single Task / Issue:** Append the GitHub Issue ID (`#<IssueNumber>`).

Examples:

- `feat(properties): harden Flat guide handling and simplify PG guides #378`
- `fix(migration): correct PG lead endpoint usage and typed-lead UI contracts #368`

**Combined / Batch / Epic:** When a single PR addresses multiple issues under an overarching feature or sprint card, append the parent ClickUp Task ID (`#<ClickUpId>`).

Examples:

- `feat(business): full-screen mobile PG form and guide card fixes #86d439d9t`
- `fix(properties): resolve validation errors across Flat and PG flows #86d4316na`

### Supported PR Types

| Type | Description | Example |
| --- | --- | --- |
| `feat` | New features or UI flows | `feat(connect): add lead filtering and search bar #86d4316na` |
| `bug` | Bug fixes or logic errors | `bug(pgforms): resolve deposit field validation error #742v8u` |
| `fix` | Diagnostic fixes or patches | `fix(hookify): load rules from ancestor .claude directories #85716` |
| `hotfix` | Critical production blockers | `hotfix(auth): fix session expiration redirect loop #86746` |
| `refactor` | Code optimization | `refactor(api-client): consolidate axios interceptors #86d4316na` |
| `chore` | Dependencies or configs | `chore(deps): bump tailwindcss to v3.4 #86d4316na` |
| `ui` | Styling and micro-animations | `ui(flat-modal): update confirmation animation #86d4316na` |
| `docs` | Documentation or READMEs | `docs(readme): add environment setup instructions #86d4316na` |

### Difference b/w ClickUp & GitHub Issue – PR Naming Convention

| Type | Scope / Intent | Target Type | Example PR Title |
| --- | --- | --- | --- |
| `feat` | Single Issue | GitHub Issue | `feat(connect): add lead filtering and search bar #412` |
| `feat` | Multi-Issue / Epic | ClickUp Task | `feat(properties): implement PG and Flat guide workflows #86d439d9t` |
| `fix` | Single Issue | GitHub Issue | `fix(migration): correct PG lead endpoint contracts #368` |
| `bug` | Single Defect | GitHub Issue | `bug(pgforms): resolve deposit field validation error #354` |
| `hotfix` | Urgent Blocker | ClickUp / Issue | `hotfix(auth): fix session expiration redirect loop #86746` |
| `refactor` | Code Cleanup | GitHub Issue | `refactor(api-client): consolidate axios interceptors #319` |
| `chore` | Tooling / Deps | ClickUp / Issue | `chore(deps): bump tailwindcss to v3.4 #86d4316na` |

## 3. PR Description Template

Every PR must be opened with a complete, structured description:

### Task ID / Link

Link the GitHub Issue or parent ClickUp task that identifies the work.

### Summary of Changes

- Concise bullet point outlining what was built, updated, or fixed.
- Specific component, API, or logic modification details.

### Why It Was Needed

- Brief context on the issue or requirement being addressed.
- The business or technical motivation for this change.

### Testing Steps

1. Step-by-step instructions to verify the change locally.
2. Expected output or edge cases covered.

## 4. Priority Framework & SLAs

| Priority | Timeline | Definition |
| --- | --- | --- |
| **P0** | Within 7 Days | Core feature initiatives. End-to-end scoping and release within 1 sprint week. |
| **P1** | Immediate | Critical blockers. Must be solved and pushed on the same day. |
| **P2** | 24–48 Hours | High-priority bug fixes or essential feature updates requiring prompt closure. |
| **P3** | Within 3 Days | Standard maintenance, tech debt, and routine sprint tasks. |

### Priority Status Hierarchy

- **Urgent (Deep Red)**: Immediate operational priority over all active work.
- **High (Muted Orange)**: Handled immediately once Urgent items are resolved.
- **Normal (Dusty Yellow)**: Standard active sprint queue.
- **Low (Sage Green)**: Backlog and non-blocking improvements.

## 5. GitHub Issue Standards & Conventions

GitHub Issues serve as the single source of truth for technical scope, domain contracts, cross-repo dependencies, and acceptance criteria before code is written.

### Issue Title Convention

Issue titles strictly follow Conventional Commits syntax using the exact feature scope:

`type(scope): concise description in imperative mood`

Examples:

- `feat(properties): harden Flat guide handling and simplify PG guides`
- `fix(migration): correct PG lead endpoint usage and typed-lead UI contracts`
- `bug(pgforms): resolve deposit field validation error`

### Feature & Type Labeling System

Labeling focuses strictly on work type, domain area, and architecture platform.

**Type Labels**

- `bug`: Unexpected behavior or regressions.
- `feature` / `enhancement`: New capabilities or functional improvements.
- `migration`: Contract breaking changes or schema sync.
- `tech-debt`: Internal cleanup and performance tuning.

**Domain Scope Labels**

- `area:properties`: PG, Flat, and listing management.
- `area:leads`: Inquiries, CRM pipelines, and lead assignments.
- `area:chat`: Business chat and socket connections.
- `area:auth`: Login, session hydration, and privacy screens.

**Platform Labels**

- `frontend`: Web/Client codebase and UI components.
- `backend`: Server API, services, and database migrations.
- `mobile`: Mobile application codebase.

## 6. GitHub Issue Templates

### Template A: Feature / Requirement Issue

#### Summary

Brief 1–2 sentence overview explaining what is being built or changed.

#### Context & Requirements

Functional rules broken down by entity or flow:

- `[Entity / Flow A]`: Specific behavior, access rules, or UI limits.
- `[Entity / Flow B]`: Edge case handling and state requirements.

#### Acceptance Criteria

- [ ] Direct requirement / user action verified.
- [ ] Reload / re-hydration edge case works without stale states.
- [ ] Error states and validation messages display correctly.

#### Tracking & References

- ClickUp Task(s):
- Design / Specs: `[Figma Link / Notion Doc]`
- Related PRs: `[Links to related active work]`

#### QA Verification

Specific steps, accounts, or configurations necessary for QA validation.

### Template B: Bug & Migration Fix Issue

#### Problem Statement

Clear explanation of the error or broken contract. Mention affected code paths:

- Affected File / Flow: `src/features/...`
- Root Cause / Conflict: Why the current behavior fails or violates contracts.

#### Technical Scope & Changes Required

- **Immediate Fix**: Specific adjustments to routes, validation, or component logic.
- **Contract / Model Updates**: Schema fields, DTO updates, or typing changes.
- **UI & Error Handling**: User-facing states, fallbacks, or messaging updates.

#### Cross-Repo / System Dependencies

- Backend PR / Issue: e.g. `STAYIN_BE#769`
- API Spec / Docs: `[Swagger / Postman Collection Link]`
- Parent ClickUp:

#### Acceptance Criteria

- [ ] Incorrect route/state calls eliminated completely.
- [ ] Legacy and migrated fields co-exist without breaking rendering.
- [ ] Correct user-facing error displayed for 4xx/5xx responses.
- [ ] End-to-end create/edit/delete flows tested and verified.

## 7. End-to-End Workflow & Traceability

The engineering pipeline maintains strict traceability across platforms:

**ClickUp Task** → **GitHub Issue** → **Sub-Branch** → **Pull Request**

1. **GitHub Issue Setup**: Link the parent ClickUp task in the issue description. Assign relevant `area:*` and type labels.
2. **Branch Naming**: Cut branches referencing the task or issue.
   - Pattern: `feat/<task-id>` or `fix/gh-<issue-number>-<short-slug>`
   - Example: `fix/gh-368-pg-lead-endpoints`
3. **PR Execution**: Link the GitHub issue in the PR description so merging the PR resolves the issue automatically.
   - Include `Closes #368` or `Fixes #368` in the PR body.
4. **Partial Work Progress**: If a PR addresses part of an issue without fully satisfying all acceptance criteria, reference the issue directly (for example, `Advances #368`) and keep the issue open until all criteria pass.
