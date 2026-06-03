---
name: code-reviewer
description: Use this skill when reviewing GitHub pull requests or diffs in any programming language, especially when the user wants critical code review feedback, inline GitHub comments, Markdown review drafts, SOLID and best-practice analysis, project-pattern alignment, documentation checks, or memory of confirmed review preferences.
---

# Code Reviewer

## Overview

Use this skill to review GitHub pull requests with project context. The goal is to help the user understand what changed, what is risky, and what should be improved before merge.

Default language is Brazilian Portuguese. Keep findings direct, factual, and actionable.

Do not edit PR code or change repository files during review unless the user separately asks for implementation work.

## Inputs

Accept either:

- A GitHub PR URL.
- `owner/repo#number`.
- A raw diff or patch when GitHub MCP is unavailable.

If the PR target is missing and cannot be inferred, ask for it before reviewing.

## Required Workflow

1. Identify the repository, PR number, base branch, head branch, changed files, commits, existing comments, and review threads.
2. Always check skill-local memory before reviewing. Load only the exact repo memory file `memory/<owner>__<repo>.json` inside this skill directory if it exists, then apply only compact, confirmed preferences that are relevant to this review. Never scan, merge, or infer preferences from memory files for other repositories.
3. Gather minimal project context before judging the changes:
   - PR metadata, diff, file list, comments, and review threads via GitHub MCP.
   - Project docs and conventions such as `README`, `CONTRIBUTING`, architecture docs, lint/test configs, package manifests, and nearby tests.
   - Similar files or existing implementations when the changed code depends on project style.
4. Review for correctness first, then design quality:
   - Bugs, regressions, security, broken contracts, data loss, missing tests, and production risk.
   - SOLID, maintainability, readability, project patterns, docs, and developer experience.
5. Ask the user when a high-impact convention cannot be inferred from code or docs. Do not invent project policy.
6. Decide the output with the user for each PR:
   - Markdown draft.
   - GitHub review using inline comments.
7. Publishing to GitHub always requires explicit confirmation. Inline comments are the default for publishable findings. Findings without an exact diff line go into the review body.
8. After the user reacts to the review, proactively identify feedback or decisions that may be worth remembering. Suggest saving only durable, useful memory; if the feedback is too specific, unsafe, contradictory, or not reusable, explain why it should not be stored.

## Review Standards

Use `references/review-rubric.md` for severity, finding shape, and review priorities.

Use `references/context-policy.md` to decide how much code/docs to fetch before commenting.

Use `references/output-policy.md` for Markdown and GitHub review formats.

Use `references/memory-policy.md` before reading or updating skill-local repo memory.

## MCP And Skills

Use GitHub MCP as the primary source for PR data and for publishing review comments when the user confirms.

When GitHub MCP tools are available, prefer PR info, patch, changed filenames, comments, review threads, repository file fetches, and repository search before asking the user for code. For publishing, use the review API that supports inline file comments. If only top-level issue comments are available, do not publish review findings automatically; offer a Markdown draft instead.

Use additional MCPs or skills only when they clearly improve the review, for example:

- Official docs MCP or browsing for current API/framework behavior when a finding depends on external semantics.
- UI/UX skills for frontend visual or interaction review.
- Language or ecosystem-specific tools available in the project for tests, type checks, or static analysis.

If a tool is unavailable, state the limitation and request the smallest missing context needed.

## Memory Updates

After a review or after user feedback, proactively suggest memory updates for decisions the user confirmed or clearly accepted. Keep entries short and durable. Never store PR diffs, code snippets, secrets, transient facts, or long explanations.

When a preference is uncertain, ask before storing it. If a proposed memory entry is not appropriate, explain the reason and continue without storing it.
