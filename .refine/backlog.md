# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Add a LICENSE

- **type:** feature
- **impact:** medium — the repo is public and the vision is other people importing Refine; no license means all rights reserved and blocks that reuse
- **effort:** small
- **notes:** MIT is the obvious default for a tool meant to be copied into other repos, but license choice is ultimately the user's legal call — confirm at the checkpoint before committing one.

### Define the unattended-checkpoint mechanism

- **type:** feature
- **impact:** medium — unattended operation is the primary use case, but the between-item checkpoint has no way to "time out": an interactive question blocks forever
- **effort:** medium
- **notes:** SKILL.md says an unanswered checkpoint defaults to continuing, but nothing defines how. Options: skip the checkpoint entirely when the session is headless/scheduled (detectable?), checkpoint only every N iterations, or make the checkpoint a non-blocking note in the iteration summary that the user can react to. Pick one mechanism and encode it in SKILL.md.
