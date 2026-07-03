# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Define the analysis phase concretely

- **type:** feature
- **impact:** high — the loop's step 1 is currently hand-wavy; candidate quality bounds everything downstream
- **effort:** medium
- **notes:** Specify which deterministic analyses run (tests, lint, dead code, TODO scan, doc drift) and which qualitative ones (architecture review, readability pass), plus the scoring rubric that turns findings into backlog entries with impact/effort ratings. Should map to the Haiku-for-exploration model decision.

### Define the diminishing-returns stopping criterion

- **type:** feature
- **impact:** high — "knows when to stop" is a design principle with no mechanism behind it
- **effort:** medium
- **notes:** Define concrete signals: e.g., analysis passes yielding only low-impact candidates for N consecutive iterations, or the backlog's best item falling below an impact threshold. This is the Opus-evaluated judgment per the model-selection decision.

### Define the installation story

- **type:** feature
- **impact:** medium — packaging is decided (skill) but there is no documented way to get Refine into a target repo
- **effort:** small
- **notes:** How does a user import Refine? Options: copy `.claude/skills/refine/` and `.refine/` seed files manually, a bootstrap script, or plugin-marketplace distribution later. Pick the simplest thing that works from a phone-started remote session.
