# Context Policy

## Minimum Context

Before reviewing, collect:

- PR title, body, base branch, head branch, commits, changed file names, and patch.
- Existing PR comments, review threads, and requested changes to avoid duplicate feedback.
- Nearby project docs and configs when available.
- Tests or call sites directly affected by the changed files.

## Efficient Fetching

Start from the diff. Fetch more only when it can change the review outcome.

Use this order:

1. Changed file patch.
2. Full changed file only if surrounding context is missing.
3. Neighboring tests or call sites.
4. Project docs/configs.
5. Similar implementations.
6. Base or head branch files when branch comparison is necessary.

Avoid loading large folders or full repositories unless the PR is architectural and the extra context is needed.

## When To Ask

Ask the user when:

- Multiple project conventions conflict and the PR depends on choosing one.
- A product requirement or business rule is necessary to judge correctness.
- The PR references private context that is not in docs, code, or comments.
- Publishing mode has not been chosen for the current PR.

Ask concrete questions and explain what decision they affect.

## When To Use Tools

Use GitHub MCP for PR data whenever possible.

Use local shell commands only when a checkout is available and they reduce uncertainty, such as targeted `rg`, tests, type checks, or linters. Do not run commands that mutate tracked files during review unless the user explicitly requests it.
