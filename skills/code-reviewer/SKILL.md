---
name: code-reviewer
description: Review GitHub pull requests or raw diffs in any language. Use for critical code-review findings, preferred inline GitHub comments, Markdown review drafts, project-pattern/SOLID/docs/test checks, and confirmed global or repo review preferences.
---

# Code Reviewer

## Defaults
Review PRs/diffs with project context. Help the user understand what changed, what is risky, and what should improve before merge.

Default to Brazilian Portuguese. Keep findings direct, factual, and actionable.

Do not edit PR code or change repository files during review unless the user separately asks for implementation work.

## Instruction Precedence
Apply review guidance in this order when rules overlap:

1. The user's current request and higher-priority platform instructions.
2. This skill's base instructions and its reference policies.
3. Confirmed memory for the repository under review.
4. The global review-preferences profile.

Global preferences tailor tone and depth only. They must never override this skill's base instructions or confirmed preferences, conventions, constraints, and accepted exceptions in the repository's own memory. When repository memory conflicts with global preferences, follow the repository memory and, when needed, explain the practical effect briefly.

## Inputs
Accept either:

- A GitHub PR URL.
- `owner/repo#number`.
- A raw diff or patch when GitHub MCP is unavailable.

If the PR target is missing and cannot be inferred, ask for it before reviewing.

## Required Workflow
1. Check the global review-preferences file using `references/global-memory-policy.md`. If it is missing or has an unfilled required preference, ask the onboarding questions in that reference and save the answers before collecting review evidence.
2. Identify the repo, PR number, title and body, base/head branches, commits, changed files, comments, review threads, and linked task resources when present.
3. Read only the exact repo memory file described in `references/memory-policy.md`, then apply relevant confirmed preferences. Repository memory takes precedence over the global profile; neither can override this skill's base instructions.
4. Gather context with `references/context-policy.md` and reconcile the documented scope with the diff before judging it.
5. Review correctness first: bugs, regressions, security, contracts, data loss, tests, and production risk.
6. Then review design quality: simplicity, maintainability, SOLID where useful, readability, project patterns, docs, and developer experience. Apply the global depth preference when deciding whether to report non-critical improvements.
7. Resolve high-impact ambiguity with a focused question; do not ask about low-impact style or discoverable facts.
8. Choose output with the user: Markdown draft or GitHub review. Prefer inline comments for actionable findings with exact diff lines.
9. Publish to GitHub only after explicit confirmation. Put findings without exact diff lines in the review body.
10. After user feedback or architectural answers, use `references/memory-policy.md` to propose only durable, generalized repository memory. Update global preferences only when the user explicitly changes how they want reviews to be conducted or written.

## Review Standards
Read only the needed reference files:
- `references/review-rubric.md`: priorities, severity, and finding shape.
- `references/context-policy.md`: context budget, tool use, and clarification questions.
- `references/output-policy.md`: Markdown/GitHub formats and publish rules.
- `references/memory-policy.md`: repo memory read/update rules.
- `references/global-memory-policy.md`: global, repository-agnostic review preferences and required onboarding.

## Tools
Use GitHub MCP first for PR data, repository files/search, review threads, and confirmed publishing. If inline review comments are unavailable, offer Markdown instead of top-level issue comments.

Use additional MCPs or skills only when they materially improve confidence, for example:

- Official docs or browsing for current API/framework behavior.
- UI/UX skills for frontend visual or interaction review.
- Project tests, type checks, linters, or static analysis when a checkout is available.

If a tool is unavailable, state the limitation and request the smallest missing context needed.
