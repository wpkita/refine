## Imperatives

- NEVER let @README.md become out of date.
- ALWAYS keep @README.md succinct and direct.
- @README.md is context; this file is imperatives and directions.
- NEVER add co-authoring to commits. Leave as the user's configured Git name and email.

## On Bootup

- At the start of every session, before anything else, read `.refine/backlog.md` and select the topmost item — that is the "next" item.
- Execute that item now, in this session: implement the change it describes. Do not merely read, restate, or analyze it.
- Do not append new candidate items during bootup — that happens in the loop's analysis phase, not here.
- When the item is completed:
    - Move it from `.refine/backlog.md` to `.refine/done.md`.
    - Commit the code changes.

## Between Work Items

- After completing an item (moved to done, committed), ask the user whether to (a) continue to the next backlog item or (b) add a new item to the backlog first.
- If the user adds a new item, slot it into the backlog's priority order using your own judgment. It does not automatically go first or last, and NEVER ask the user where it should go.
- If the session is unattended or the user does not respond, continue to the next item — the checkpoint must never block the loop.
