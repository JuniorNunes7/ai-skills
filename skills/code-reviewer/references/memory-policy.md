# Memory Policy

## Location
Use only the exact repo memory file. Store memory outside the reviewed repository:

`../code-reviewer-data/memories/<owner>__<repo>.yaml`

The path is relative to the `code-reviewer` skill directory. Use lowercase owner/repo names and replace `/` with `__`.

Before every review, load only this exact file if it exists. Never list, scan, merge, or infer preferences from memory files for other repositories. If the file is missing, proceed without repository memory. This restriction applies to repository memory; the separate exact global profile in `global-memory-policy.md` is allowed.

## Format
Use this compact shape:

```yaml
version: 1
repository: owner/repo
updated_at: YYYY-MM-DD
preferences: []
accepted_exceptions: []
review_output:
  default_mode: ask
  github_comments: inline
```

## Store
Store only durable, confirmed decisions that can guide future reviews beyond the current PR, file, class, method, endpoint, or one-off implementation:

- Preferred output format.
- Review strictness preferences.
- Accepted exceptions to general best practices.
- Repeatedly accepted architectural constraints.

Prefer compact entries:

```yaml
- topic: concise category
  decision: general rule or preference
  source: optional short note such as "user-confirmed"
```

Use one short sentence for `decision`. Write the durable rule, not the triggering occurrence.

## Curation Gate
Propose or save memory only when all checks pass:

- Reusable across future PRs in another file or area.
- Generalized beyond the exact line, file, component, method, issue, or PR.
- Confirmed by the user or clearly accepted.
- Actionable without reading the original PR.
- Safe: no code snippets, secrets, customer data, or transient facts.
- Non-duplicative with existing memory.

If the point is useful but too local, generalize it first. If it cannot be generalized safely, explain briefly and do not save it.

## Propose
After user feedback, always check whether a confirmed preference should become memory. Ask with the exact generalized wording you intend to save:

`Should I save this memory for future reviews: "Controllers should not contain business logic"?`

Architecture answers are memory candidates only when they define reusable conventions. When the user explains why a finding should pass, suggest a compact `accepted_exceptions` entry only if the tradeoff is reusable.

Do not store feedback that:

- Only applies to the current PR.
- Names a specific file, method, component, controller, issue, or diff line instead of a reusable rule.
- Contains code, secrets, or sensitive details.
- Conflicts with current project docs or stronger evidence.
- Is too vague to guide future reviews.

## Never Store

- PR diffs or code snippets.
- Secrets, tokens, credentials, or private customer data.
- Long explanations or temporary PR facts.
- File-, class-, method-, component-, issue-, or PR-specific findings.
- Guesses that the user did not confirm.

## Update
Before updating memory, confirm the exact generalized wording unless the user already provided final text and asked to save it.

Before adding a new `preferences` or `accepted_exceptions` entry, check the existing entries and do not create duplicate or substantially equivalent memories. Update or remove an existing entry only when the confirmed decision changes.

When memory conflicts with current project docs or code, prefer current project evidence and ask whether memory should be updated.

If memory grows noisy, propose summarizing related entries into a few compact preferences or accepted exceptions, then ask before updating the file.
