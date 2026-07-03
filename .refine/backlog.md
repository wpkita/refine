# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Give Analyze a lens catalog: what to look for, when it applies, and Refine's stance

- **type:** feature
- **impact:** high — the Analysis Phase hardcodes four deterministic checks and two qualitative passes; arbitrary target repos need far more dimensions (coverage, secrets, vulnerable deps, deprecated calls, naming consistency, misspellings, slow paths, missing indexes, e2e gaps), and candidate quality bounds everything downstream
- **effort:** medium
- **notes:** Add a lens catalog to SKILL.md's Analysis Phase. Each lens carries: how to check, an "applies when" condition, and a one-line stance on what "better" means (this is where the opinionated principle gets encoded — never ask the user to configure thresholds). Analyze starts with a cheap Haiku recon pass ("what kind of repo is this?") and selects only the applicable lenses — never runs the whole catalog. Valuation stays with the existing scoring rubric: lenses surface candidates, the rubric prices them, so subjective lenses are fine. The target repo's own CLAUDE.md/README are read as the source of repo-specific values — customization with no new config surface. Rejected: per-repo enabled-checks config, numeric targets (false precision), exhaustive every-pass runs (cost, noise).

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
