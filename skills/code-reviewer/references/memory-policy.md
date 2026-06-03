# Memory Policy

## Location

Store memory outside the installed skill directory and never inside the repository being reviewed:

`../code-reviewer-data/memories/<owner>__<repo>.yaml`

The path is relative to the `code-reviewer` skill directory. For example, if the skill is installed at `~/.agents/skills/code-reviewer`, memory lives at `~/.agents/skills/code-reviewer-data/memories/*.yaml`.

Use lowercase owner and repo names. Replace `/` with `__`.

Always check the exact memory file for the repository being reviewed before every review, even when the user does not mention memory. Do not list, scan, merge, or consult memory files for other repositories. If the exact file does not exist, proceed without memory and consider creating it only after the user confirms a durable preference or decision.

## Format

Use this compact shape:

```yaml
version: 1
repository: owner/repo
updated_at: YYYY-MM-DD
preferences: []
project_conventions: []
accepted_exceptions: []
review_output:
  default_mode: ask
  github_comments: inline
```

## What To Store

Store only durable, confirmed decisions:

- Preferred output format.
- Review strictness preferences.
- Project conventions the user confirmed.
- Accepted exceptions to general best practices.
- Repeatedly accepted architectural constraints.

Each entry should be one short sentence or a small object with `topic`, `decision`, and optional `source`.

## Proactive Suggestions

After user feedback, analyze whether anything should become memory. Suggest saving it when it is:

- Durable across future reviews.
- Specific enough to guide behavior.
- Confirmed by the user or clearly accepted.
- Safe to store without code, secrets, or transient PR details.

Do not wait for the user to ask for memory if their feedback reveals a reusable preference.

If the feedback should not be stored, explain why briefly. Common reasons:

- It only applies to the current PR.
- It contains code, secrets, or sensitive details.
- It conflicts with current project docs or stronger evidence.
- It is too vague to guide future reviews.

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
