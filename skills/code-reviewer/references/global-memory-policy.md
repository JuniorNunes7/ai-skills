# Global Review Preferences

## Purpose and Location
Use one global file for durable preferences about *how* reviews should be performed and written, independent of any repository:

`../code-reviewer-data/global-review-preferences.yaml`

The path is relative to the `code-reviewer` skill directory. This is separate from the per-repository files in `memories/`: project conventions, architectural constraints, and accepted exceptions always belong in `memory-policy.md` instead.

## Precedence
This global profile is the lowest-priority source of review guidance. It may refine tone and depth only after applying the base instructions of `SKILL.md` and the confirmed memory for the repository being reviewed.

Never use a global preference to override a base skill instruction or a repository-specific preference, convention, constraint, or accepted exception. If the global profile conflicts with repository memory, follow the repository memory. If it conflicts with the skill, follow the skill.

## Required Preferences

Before collecting PR or diff evidence, load this exact file if it exists. A valid profile has all of these values filled:

- `tone.style`: a non-empty description of the desired tone. It may combine the suggested styles.
- `depth`: one of `pragmatic`, `balanced`, or `thorough`.

If the file is missing, unreadable, malformed, or any required value is absent, ask the onboarding questions below before reviewing. Do not infer the answers from a repository, previous PR, or the user's writing style. Create or repair the file only from the user's answer.

Use this format:

```yaml
version: 1
updated_at: YYYY-MM-DD
tone:
  style: direct and explanatory
depth: balanced
```

## Onboarding Questions

Ask the required questions together, in the user's language. Present the suggestions as starting points, not a closed list:

```markdown
Before I start reviewing, I need to set up your global review preferences. They apply across repositories and can be changed later.

1. Which tone should the review use?
   - Direct and explanatory (recommended)
   - Explanatory and didactic
   - Friendly and collaborative
   - Lighthearted, with restrained humor when appropriate

2. How deep should the review go?
   - Pragmatic: only merge-impacting findings
   - Balanced: important findings plus useful local improvements (recommended)
   - Thorough: inspect more alternatives and report non-blocking improvements too
```

If the user supplies only some answers, ask only for the missing required preferences. Once all are answered, save the compact normalized values and continue the review.

## Apply the Preferences

`tone.style` changes phrasing, not the evidence standard or the language/tone requirements of a repository's confirmed memory. Keep every finding factual, respectful, concrete, and actionable. Use `lighthearted` sparingly; never make humor at the expense of a person, team, or the seriousness of a defect.

`depth` changes the reporting threshold for non-critical maintainability, documentation, and testing improvements. It does not permit overlooking a blocker or major issue, or relaxing a review requirement established by the skill or repository memory.

## Maintain the Global File

Keep this file limited to review method and communication preferences. Good candidates include review focus, tone, and desired depth. Do not put repository conventions, framework choices, code excerpts, PR facts, secrets, customer data, or one-off exceptions here.

Update it only when the user explicitly changes a preference, asks to save one, or completes required onboarding. Preserve the existing values the user did not change, avoid duplicates, and update `updated_at`. Never propose a global preference merely because of one PR decision; use `memory-policy.md` for durable repository-specific decisions.
