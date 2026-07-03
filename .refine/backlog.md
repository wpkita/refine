# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Fix the install path: the GitHub source URL 404s publicly

- **type:** bug
- **impact:** high — the README install prompt tells a fresh session to copy SKILL.md from https://github.com/wpkita/refine, but that URL returns 404 unauthenticated (repo private or unpublished); the installation story is the doorway to the whole vision and is currently broken for any target session without push-level access
- **effort:** small
- **notes:** Found by the install-prompt validation. The real fix is the user making wpkita/refine public — Refine must not flip repo visibility unilaterally. The executable part: update README's Installation section to state the access requirement honestly (and/or offer a local-clone source as fallback) so the docs don't overpromise, and surface the make-it-public ask to the user at the next checkpoint.

### Update the state diagram's checkpoint wording

- **type:** bug
- **impact:** low — the README diagram's "continue (default when unattended)" edge predates the interruption-is-the-checkpoint mechanism; slightly stale, not wrong
- **effort:** small
- **notes:** Reword the Checkpoint→Select edge to reflect that unattended runs never ask and interruption is the checkpoint.
