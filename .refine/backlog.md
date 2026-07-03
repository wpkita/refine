# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Exercise the bundled agents in a real delegated Analyze pass

- **type:** feature
- **impact:** low — the agent definitions exist and follow the standard frontmatter format, but the loop has so far run every lens inline; delegation itself is unexercised
- **effort:** small
- **notes:** On the next Analyze pass, delegate recon/mechanical lenses to `refine-recon`, scoring to `refine-scorer`, and the stopping verdict to `refine-stopper`, and confirm the model mapping actually engages.

### Dry-run the full loop in the scratch install target

- **type:** feature
- **impact:** low — install mechanics are validated; the remaining unknown is skill auto-discovery and first-run Analyze in a fresh session, which can't be confirmed from this session
- **effort:** small
- **notes:** Start a session in a freshly installed target repo and confirm the skill is discovered and the first Analyze pass populates the seeded backlog.
