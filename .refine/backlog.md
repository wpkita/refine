# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Update the state diagram's checkpoint wording

- **type:** bug
- **impact:** low — the README diagram's "continue (default when unattended)" edge predates the interruption-is-the-checkpoint mechanism; slightly stale, not wrong
- **effort:** small
- **notes:** Reword the Checkpoint→Select edge to reflect that unattended runs never ask and interruption is the checkpoint.
