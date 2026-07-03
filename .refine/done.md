# Done

Completed backlog items, most recent first. Moved here from [backlog.md](backlog.md).

### Scaffold the Refine skill (SKILL.md)

- **type:** feature
- **impact:** high — turns the packaging and model-selection decisions into an invocable artifact
- **effort:** medium
- **resolution:** Created `.claude/skills/refine/SKILL.md` encoding the full loop (select → execute → record → commit → analyze → checkpoint → stop), the backlog format (titled headings, file order is priority), the checkpoint rules, and the task→model mapping. Invocable as `/refine` in this repo and copyable into target repos. Produced by this iteration's analysis pass and executed immediately, so it never sat in backlog.md.

### Ask the user between work items whether to continue or add a backlog item

- **type:** feature
- **impact:** medium — gives the user a lightweight steering point between iterations without breaking the loop's one-improvement-per-iteration rhythm
- **effort:** medium
- **resolution:** Added a "Between Work Items" section to CLAUDE.md: after an item is completed and committed, ask the user whether to continue or add a new backlog item first. New items are slotted into priority order by the LLM's own judgment (never automatically first/last, never arbitrated by the user). An unanswered checkpoint defaults to continuing — it never blocks an unattended loop. README's Backlog section documents the behavior.

### Decide model selection per task type

- **type:** feature
- **impact:** high — model choice drives cost and quality of every loop iteration, and unattended loops multiply both
- **effort:** medium
- **resolution:** Cheap models for constant mechanical work, strong models for rare high-stakes judgment. Haiku: backlog bookkeeping, broad repo exploration/analysis. Sonnet: candidate scoring, improvement selection, implementation (session default). Opus: diminishing-returns evaluation — runs at most once per iteration so cost is negligible, but a wrong stop/continue call is the most expensive mistake an unattended loop can make. The mapping lives in per-agent frontmatter (`model:` field) in the agent definitions the skill bundles; the orchestrating loop inherits the session model. See README.md → Model Selection.

### Decide if Claude skill or other

- **type:** feature
- **impact:** high — packaging determines how Refine is imported into target repos and how it runs unattended
- **effort:** medium
- **resolution:** Packaged as a Claude Code skill (`SKILL.md` + the `.refine/` backlog files, both flat files committed to the target repo). Rejected a plugin: it bundles multiple skills/commands/hooks and needs distribution/versioning infra Refine doesn't need for a single self-contained loop. A skill matches the backlog's own flat-file-in-target-repo pattern with no install/build step, and is invocable directly or picked up via this repo's own bootup convention — fits the unattended, phone-driven use case cleanly. See README.md.
