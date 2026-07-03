# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Package Refine as a plugin now that it has outgrown a single file

- **type:** feature
- **impact:** medium — README's stated trigger for plugin distribution ("if the skill outgrows a single file") has fired: the bundle is now one skill plus three agents. A plugin gives two-command install (`/plugin marketplace add wpkita/refine`, `/plugin install refine@refine`), versioned updates, and keeps engine files out of target repos — only `.refine/` state travels with the target
- **effort:** medium
- **notes:** Add `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`; move the skill and agents to plugin-layout dirs (`skills/refine/SKILL.md`, `agents/*.md`). Constraints: dogfooding must keep working (this repo loads its own skill — add the marketplace from the local path, or keep `.claude/` copies in sync); ephemeral remote sessions need the marketplace known (target repos can commit plugin config in `.claude/settings.json`); README's Installation section keeps the prompt install as the zero-infra fallback and gains the plugin path. Blocked-ish on the repo being public for the GitHub marketplace-add path, but the packaging work itself isn't blocked.

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
