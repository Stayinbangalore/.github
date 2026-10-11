# Stayin Engineering Workflow

All repositories in the `Stayinbangalore` organization follow the approved **Workflow, PR & GitHub Issue Standards**.

Read the full standard here: [`docs/ENGINEERING_WORKFLOW.md`](docs/ENGINEERING_WORKFLOW.md).

The required traceability flow is:

`ClickUp Task -> GitHub Issue -> Sub-Branch -> Pull Request`

Key rules:

- GitHub Issues are the source of truth for technical scope, contracts, dependencies, and acceptance criteria.
- PR titles use `type(scope): concise description #Id`.
- Single-issue PRs use the GitHub Issue ID; combined/batch/epic PRs use the parent ClickUp Task ID.
- Main feature branches use `<feature-name>`; sub-branches use `<type>/<task-id>` or `<type>/<task-name>`.
- PR descriptions use the required four-section template: Task ID / Link, Summary of Changes, Why It Was Needed, Testing Steps.
- Use `Closes #...` / `Fixes #...` for complete work and `Advances #...` for partial work.

Repository-specific contribution files may add implementation guidance, but must preserve these organization rules.
