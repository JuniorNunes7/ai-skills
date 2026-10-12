# Context Policy

## Collect
- PR title, body, base branch, head branch, commits, changed file names, and patch.
- Existing PR comments, review threads, and requested changes to avoid duplicate feedback.
- Linked task resources in the PR body when present. Attempt to access the relevant task context, including its description, acceptance criteria, and discussion when available.
- Nearby project docs and configs when available.
- Tests or call sites directly affected by the changed files.

## Scope Reconciliation
Treat the PR description and accessible linked task context as scope evidence, not just background.

Before finalizing the review, compare that evidence with the changed behavior and determine whether:

- A documented requirement appears unimplemented or only partially implemented.
- A meaningful behavior change has no documented scope.
- The available description is absent, incomplete, or too ambiguous to support either conclusion.

When the documented scope and implementation agree, continue with the normal review checks; do not create scope commentary merely to restate the PR.

When scope evidence is absent or insufficient, summarize the observed changes directly in the review summary. State the access limitation when a linked task could not be consulted. Do not infer an unstated requirement from a missing or inaccessible task.

When a mismatch remains after available context is checked, report it as a finding or a question according to the evidence and impact. A missing confirmed requirement can be a defect; an unexplained change should be presented as a scope question unless it independently creates a concrete risk.

## Fetch Efficiently
Start from the diff. Fetch more only when it can change the review outcome:

1. Changed file patch.
2. Relevant linked task context, when a link is present.
3. Full changed file only if surrounding context is missing.
4. Neighboring tests or call sites.
5. Project docs/configs.
6. Similar implementations.
7. Base or head branch files when branch comparison is necessary.

Avoid loading large folders or full repositories unless the PR is architectural and the extra context is needed.

## Ask
Ask the user only when the answer can materially change the review. Do not ask everything; first use available docs, memory, PR comments, nearby code, tests, and similar implementations.

Ask for:

- Conflicting project conventions.
- Product/business rules needed to judge correctness.
- Private context missing from the PR, linked task resources, docs, code, or comments.
- High-impact architecture not confirmed by docs/code, such as layer boundaries, business-rule ownership, persistence boundaries, or whether a rule should exist.
- Publishing mode has not been chosen for the current PR.

Do not ask when the uncertainty is low-impact style, can be answered by fetching a small amount of additional context, or can be safely reported as residual risk.

## Architectural Questions
Ask before turning an ambiguous architecture choice into a finding. State:

- The observed PR choice.
- Checked context and missing evidence.
- The review decision depending on the answer.
- 2-3 neutral options plus `Other`.

Use this shape:

```markdown
I noticed that <architectural choice in the PR>, and I did not find docs or similar code that clearly establish this pattern. Which direction should I use for this review?

- <Option A: project accepts this pattern.>
- <Option B: expected alternative boundary or ownership.>
- <Option C: the rule/behavior should not exist.>
- Other: <user can type the intended convention.>
```

After the user answers, apply the answer to the review. If it looks durable and reusable, use `memory-policy.md` to ask whether the generalized rule should be saved.

## Tools
Use GitHub MCP for PR data whenever possible.

When the PR links to a task or another work item, use an available authorized source to inspect it before asking the user for that context. Do not assume a particular task system or request new authorization merely to retry unavailable access; state the limitation and continue with the evidence available.

Use local shell commands only when a checkout is available and they reduce uncertainty, such as targeted `rg`, tests, type checks, or linters. Do not run commands that mutate tracked files during review unless the user explicitly requests it.
