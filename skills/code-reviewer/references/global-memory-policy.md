# Global Review Preferences

## Purpose and Location
Use one global file for durable preferences about *how* reviews should be performed and written, independent of any repository:

`../code-reviewer-data/global-review-preferences.yaml`

The path is relative to the `code-reviewer` skill directory. This is separate from the per-repository files in `memories/`: project conventions, architectural constraints, and accepted exceptions always belong in `memory-policy.md` instead.

## Required Preferences

Before collecting PR or diff evidence, load this exact file if it exists. A valid profile has all of these values filled:

- `review_focus`: a non-empty list.
- `tone.style`: a non-empty description of the desired tone. It may combine the suggested styles.
- `depth`: one of `pragmatic`, `balanced`, or `thorough`.

If the file is missing, unreadable, malformed, or any required value is absent, ask the onboarding questions below before reviewing. Do not infer the answers from a repository, previous PR, or the user's writing style. Create or repair the file only from the user's answer.

Use this format:

```yaml
version: 1
updated_at: YYYY-MM-DD
review_focus:
  - readable code that tells the business story
  - behavior, contracts, and meaningful tests
tone:
  style: direct and explanatory
depth: balanced
```

## Onboarding Questions

Ask the required questions together, in the user's language. Present the suggestions as starting points, not a closed list:

```markdown
Before I start reviewing, I need to set up your global review preferences. They apply across repositories and can be changed later.

1. What should receive extra attention, beyond the non-negotiable checks for correctness, security, and contracts?
   - Readable code that tells the business story (recommended)
   - Behavior, contracts, and meaningful tests
   - Clear architectural boundaries and project conventions
   - Documentation, scope, and developer experience
   You can choose more than one or describe your own focus.

2. Which tone should the review use?
   - Direct and explanatory (recommended)
   - Explanatory and didactic
   - Friendly and collaborative
   - Lighthearted, with restrained humor when appropriate

3. How deep should the review go?
   - Pragmatic: only merge-impacting findings
   - Balanced: important findings plus useful local improvements (recommended)
   - Thorough: inspect more alternatives and report non-blocking improvements too
```

If the user supplies only some answers, ask only for the missing required preferences. Once all are answered, save the compact normalized values and continue the review.

## Apply the Preferences

`review_focus` changes emphasis and context-gathering effort; it never suppresses correctness, security, privacy, contracts, data integrity, or material regression checks.

`tone.style` changes phrasing, not the evidence standard. Keep every finding factual, respectful, concrete, and actionable. Use `lighthearted` sparingly; never make humor at the expense of a person, team, or the seriousness of a defect.

`depth` changes the reporting threshold for non-critical maintainability, documentation, and testing improvements. It does not permit overlooking a blocker or major issue.

## Maintain the Global File

Keep this file limited to review method and communication preferences. Good candidates include review focus, tone, and desired depth. Do not put repository conventions, framework choices, code excerpts, PR facts, secrets, customer data, or one-off exceptions here.

Update it only when the user explicitly changes a preference, asks to save one, or completes required onboarding. Preserve the existing values the user did not change, avoid duplicates, and update `updated_at`. Never propose a global preference merely because of one PR decision; use `memory-policy.md` for durable repository-specific decisions.
