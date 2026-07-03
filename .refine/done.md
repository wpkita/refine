# Done

Completed backlog items, most recent first. Moved here from [backlog.md](backlog.md).

### Define the installation story

- **type:** feature
- **impact:** medium — packaging is decided (skill) but there was no documented way to get Refine into a target repo
- **effort:** small
- **resolution:** Installation is a prompt, not a script — the simplest thing that works from a phone-started remote session. The user tells Claude Code in the target repo to copy `.claude/skills/refine/SKILL.md` from this repo, seed empty `.refine/backlog.md` and `.refine/done.md`, and commit; the skill's Analyze phase populates the backlog on first run. Rejected a bootstrap script (nothing to script beyond a copy) and marketplace distribution (deferred until the skill outgrows a single file). Documented in README → Installation.

### Define the diminishing-returns stopping criterion

- **type:** feature
- **impact:** high — "knows when to stop" is a design principle with no mechanism behind it
- **effort:** medium
- **resolution:** Added a "Stopping Criterion" section to SKILL.md. Diminishing returns = the best available work is no longer worth an iteration; evaluated by Opus after every Analyze pass. Fires when two consecutive Analyze passes yield only low-impact candidates (or none), or when the last three completed iterations were all low-impact. An empty backlog is not a stopping signal (it triggers Analyze). Stopping reports rather than halts: summarize completed items, name the fired signal, leave low-impact candidates in the backlog. Bias toward stopping — restarting is cheap, unattended low-value looping is not.

### Define the analysis phase concretely

- **type:** feature
- **impact:** high — the loop's step 1 is currently hand-wavy; candidate quality bounds everything downstream
- **effort:** medium
- **resolution:** Added an "Analysis Phase" section to SKILL.md. Deterministic checks (Haiku): test suite and linters (failures become bugs), TODO/FIXME scan, doc drift, dead code/unused deps. Qualitative review (Sonnet): architecture/readability pass, gap analysis of decisions without artifacts and principles without mechanisms. Scoring stays qualitative (high/medium/low impact, small/medium/large effort — numeric scores are false precision); priority is impact first, lower effort breaks ties, bugs beat features on equal footing; oversized items must be split before entering the backlog. A pass yielding only low-impact candidates raises the stopping question (criterion still a backlog item).

### Document the loop as a state machine, including the empty-backlog branch

- **type:** feature
- **impact:** medium — makes the loop's control flow unambiguous, especially the backlog-empty → analyze transition and the never-block checkpoint defaults, which prose lists blur
- **effort:** small
- **resolution:** Added a Mermaid state diagram to README's Core Loop section (states: Select, Analyze, Execute, Record, Checkpoint; terminals: diminishing returns, user stop). Added the empty-backlog imperative to CLAUDE.md's bootup section; SKILL.md already carried the transition in its step 1. User-added at a checkpoint and slotted first by judgment: small effort, formalizes just-exercised behavior, and downstream backlog items can reference named states.

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
