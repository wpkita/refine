# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Validate the install prompt end-to-end in a scratch target repo

- **type:** feature
- **impact:** low — the install is a single file copy, so failure risk is small, but it has never actually been exercised
- **effort:** small
- **notes:** Create a throwaway repo, run the README's install prompt, confirm the skill loads and the first Analyze pass populates the seeded backlog.

### Update the state diagram's checkpoint wording

- **type:** bug
- **impact:** low — the README diagram's "continue (default when unattended)" edge predates the interruption-is-the-checkpoint mechanism; slightly stale, not wrong
- **effort:** small
- **notes:** Reword the Checkpoint→Select edge to reflect that unattended runs never ask and interruption is the checkpoint.
