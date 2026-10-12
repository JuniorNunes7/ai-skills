---
name: code-reviewer
description: Review GitHub pull requests or raw diffs in any language. Use for critical code-review findings, preferred inline GitHub comments, Markdown review drafts, project-pattern/SOLID/docs/test checks, and confirmed repo review-memory preferences.
---

# Code Reviewer

## Defaults
Review PRs/diffs with project context. Help the user understand what changed, what is risky, and what should improve before merge.

Default to Brazilian Portuguese. Keep findings direct, factual, and actionable.

Do not edit PR code or change repository files during review unless the user separately asks for implementation work.

## Inputs
Accept either:

- A GitHub PR URL.
- `owner/repo#number`.
- A raw diff or patch when GitHub MCP is unavailable.

If the PR target is missing and cannot be inferred, ask for it before reviewing.

## Required Workflow
1. Identify the repo, PR number, title and body, base/head branches, commits, changed files, comments, review threads, and linked task resources when present.
2. Read only the exact repo memory file described in `references/memory-policy.md`, then apply relevant confirmed preferences.
3. Gather context with `references/context-policy.md` and reconcile the documented scope with the diff before judging it.
4. Review correctness first: bugs, regressions, security, contracts, data loss, tests, and production risk.
5. Then review design quality: simplicity, maintainability, SOLID where useful, readability, project patterns, docs, and developer experience.
6. Resolve high-impact ambiguity with a focused question; do not ask about low-impact style or discoverable facts.
7. Choose output with the user: Markdown draft or GitHub review. Prefer inline comments for actionable findings with exact diff lines.
8. Publish to GitHub only after explicit confirmation. Put findings without exact diff lines in the review body.
9. After user feedback or architectural answers, use `references/memory-policy.md` to propose only durable, generalized memory.

## Review Standards
Read only the needed reference files:
- `references/review-rubric.md`: priorities, severity, and finding shape.
- `references/context-policy.md`: context budget, tool use, and clarification questions.
- `references/output-policy.md`: Markdown/GitHub formats and publish rules.
- `references/memory-policy.md`: repo memory read/update rules.

## Tools
Use GitHub MCP first for PR data, repository files/search, review threads, and confirmed publishing. If inline review comments are unavailable, offer Markdown instead of top-level issue comments.

Use additional MCPs or skills only when they materially improve confidence, for example:

- Official docs or browsing for current API/framework behavior.
- UI/UX skills for frontend visual or interaction review.
- Project tests, type checks, linters, or static analysis when a checkout is available.

If a tool is unavailable, state the limitation and request the smallest missing context needed.
