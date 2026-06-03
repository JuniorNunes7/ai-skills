# Review Rubric

## Priority Order

1. Correctness: broken logic, regressions, edge cases, race conditions, error handling, invalid assumptions, and data integrity.
2. Security and privacy: authz/authn gaps, secret exposure, injection, unsafe deserialization, dependency risk, and sensitive logging.
3. Contracts: API shape, schema compatibility, migrations, public types, CLI behavior, config, and backwards compatibility.
4. Tests: missing coverage for changed behavior, brittle tests, snapshots hiding behavior, and untested failure modes.
5. Maintainability: human-readable simplicity, unnecessary complexity, weak boundaries, duplication, naming, readability, SOLID, and project convention drift.
6. Documentation: missing or stale docs where the changed behavior affects users, operators, or contributors.

## Severity

- `blocker`: likely production breakage, security issue, data loss, broken public contract, or merge-blocking test failure.
- `major`: meaningful bug, unsupported edge case, migration risk, or design issue likely to cause future defects.
- `minor`: local maintainability, naming, docs, or test improvement that is useful but not merge-blocking.
- `question`: ambiguity that needs project or author intent before a recommendation is defensible.

Prefer fewer, higher-signal findings. Do not pad the review.

## Finding Shape

Each finding should include:

- Severity.
- File and diff line if available.
- What is wrong.
- Why it matters.
- A concrete fix or decision needed.

Keep explanations simple. For complex points, describe the causal chain in plain language instead of listing abstract principles.

## Code Review Discipline

- Do not criticize style when the project already uses that style consistently.
- Do not claim a bug without explaining the failing scenario.
- Do not suggest broad rewrites when a local fix resolves the risk.
- Treat simplification and readability improvements as important when they reduce cognitive load for human readers without changing behavior or fighting project conventions.
- Do not require SOLID terminology in the comment unless it helps the user understand the issue.
- If a finding depends on external library behavior that may have changed, verify it with official docs or ask for context.
- If no important issues are found, say that clearly and mention any residual test or context gaps.
