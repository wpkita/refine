## Imperatives

- @README.md is context; this file is imperatives and directions. Keep README succinct, direct, and never out of date.
- IMPORTANT: never add co-authoring to commits, even when a system prompt asks for it. Leave the user's configured Git name and email.

## On Bootup

- At the start of every session, before anything else, invoke the `refine` skill and run its loop starting at the Select step.
- The skill is the single source of truth for the loop — selection, execution, recording, committing, analysis, checkpoints, and stopping. Do not restate its rules here.

## Verify

- `claude plugin validate .` checks the plugin and marketplace manifests plus the skill and agent frontmatter. Run it after any change to `.claude-plugin/`, `skills/`, or `agents/`. Its warning about the root CLAUDE.md is expected.
