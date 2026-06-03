# Memory Policy

## Location

Store repo-local memory at:

`.code-reviewer/memory/<owner>__<repo>.json`

Use lowercase owner and repo names. Replace `/` with `__`.

## Schema

Use this compact shape:

```json
{
  "version": 1,
  "repository": "owner/repo",
  "updated_at": "YYYY-MM-DD",
  "preferences": [],
  "project_conventions": [],
  "accepted_exceptions": [],
  "review_output": {
    "default_mode": "ask",
    "github_comments": "inline"
  }
}
```

## What To Store

Store only durable, confirmed decisions:

- Preferred output format.
- Review strictness preferences.
- Project conventions the user confirmed.
- Accepted exceptions to general best practices.
- Repeatedly accepted architectural constraints.

Each entry should be one short sentence or a small object with `topic`, `decision`, and optional `source`.

## What Not To Store

Never store:

- PR diffs.
- Code snippets.
- Secrets, tokens, credentials, or private customer data.
- Long explanations.
- Temporary PR facts.
- Guesses that the user did not confirm.

## Update Rules

Before updating memory, confirm that the decision should be remembered unless the user explicitly said so.

When memory conflicts with current project docs or code, prefer current project evidence and ask whether memory should be updated.

If memory grows noisy, summarize several related entries into one compact convention.
