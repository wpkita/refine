# Done

Completed backlog items, most recent first. Moved here from [backlog.md](backlog.md).

### Expand the maturity ladder into an exhaustive checklist and declare it the source of truth

- **type:** feature
- **impact:** high — the ladder drives all backlog prioritization; the user's healthy-repo checklist exposed real gaps (editor config, warnings-as-errors, injection scanning, architecture tests, test-pyramid shape, one-command setup, misspellings, feature-branch history, project website), and nothing stated which document wins when guidance conflicts
- **effort:** medium
- **resolution:** Rewrote `.claude/skills/refine/maturity.md` from 50 to 65 rungs, keeping the tier structure (Tier 0 gates → foundation → enforcement/automation → code health → polish) and the catastrophe > velocity > aesthetics bias. Folded in the user's pillar checklist plus the "code itself" signals from Ben Balter and the five-pillar maintenance breakdown from the GitHub community discussion (both cited in a Provenance section); popularity metrics deliberately excluded — the ladder measures repo content, the causes rather than the outcomes. Added a fourth stance for single-maintainer repos: community rungs rank lower without outside users, never zero, and headcount-dependent rungs adapt rather than fail. Declared the file a living document and the SOURCE OF TRUTH for prioritization in maturity.md itself, SKILL.md (scoring rubric and lens row), all three agent definitions, and README. README de-hardcoded the rung count so it can't go stale as the living document grows. User-directed via prompt.md; executed outside the loop.

### Integrate the ranked repo-maturity indicators into Analyze and scoring

- **type:** feature
- **impact:** high — the lens catalog said what to look for but had no cross-repo notion of what a mature repo *has*; the ladder gives Analyze a ranked checklist and gives scoring a principled impact anchor instead of per-finding intuition
- **effort:** medium
- **resolution:** Added `.claude/skills/refine/maturity.md`: fifty ranked rungs grouped into tiers (Tier 0 gates → foundation → enforcement/automation → code health → polish), ordered by the bias catastrophe > velocity > aesthetics. Wired it in as a new always-on lens (community rungs conditional on outside users), and bound three rules into the scoring rubric for all candidates: failing Tier 0 gates are top-of-backlog bugs nothing outranks; ladder gaps default to impact by tier, adjusted for repo type; enforcement beats documentation. Recon now reports repo shape (library/application/CLI/docs) since rank conditioning depends on it, and runs the machine-checkable rungs as predicates; judgment rungs go to Sonnet with an evidence requirement. Where a rung overlaps an existing lens, the lens stays the check and the ladder only supplies rank — no duplicate findings. The skill outgrowing a single file is acknowledged in README and strengthens the queued plugin-packaging item. User-directed at a checkpoint; executed immediately.

### Scaffold the bundled agent definitions the docs already promised

- **type:** bug
- **impact:** medium — README and SKILL.md both claimed the model mapping "lives in per-agent frontmatter in the agent definitions the skill bundles," but no agent definitions existed; the gap-analysis lens's own stance applied: a stated mechanism with no artifact is a bug in the project
- **effort:** medium
- **resolution:** Created `.claude/agents/refine-recon.md` (Haiku — recon, mechanical lenses, backlog bookkeeping), `refine-scorer.md` (Sonnet — rubric scoring and selection), and `refine-stopper.md` (Opus — stopping-criterion verdicts, returns stop|continue plus the signal). Implementation stays with the orchestrating session at the session default. Updated both Model Selection tables to name the agents, extended the install prompt to copy `.claude/agents/refine-*.md`, and made README's Current State evergreen (pointing at the backlog files instead of restating their contents, which went stale every iteration). Found by this run's first lens-catalog Analyze pass — the catalog caught a gap the old checklist had missed twice; executed immediately, so it never sat in backlog.md.

### Update the state diagram's checkpoint wording

- **type:** bug
- **impact:** low — the README diagram's "continue (default when unattended)" edge predated the interruption-is-the-checkpoint mechanism; slightly stale, not wrong
- **effort:** small
- **resolution:** Reworded the Checkpoint→Select edge to "continue — unattended runs never ask, interruption is the checkpoint," matching SKILL.md step 6 and the Backlog section's prose.

### Fix the install path: the GitHub source URL 404s publicly

- **type:** bug
- **impact:** high — the README install prompt pointed fresh sessions at https://github.com/wpkita/refine, which returns 404 unauthenticated; the installation story was broken for any target session without repo access
- **effort:** small
- **resolution:** Executed the unilateral half: README's Installation section now states the access requirement honestly — the target session needs authenticated access to wpkita/refine, or a local clone to copy from, until the repo is public. The other half is the user's call, not Refine's: making the repo public is an ownership/visibility decision the loop must not take unilaterally, so it is surfaced as an explicit ask in the run summary. Once the repo is public, the caveat sentence should be deleted (doc-drift lens will catch it if forgotten).

### Validate the install prompt end-to-end in a scratch target repo

- **type:** feature
- **impact:** low — the install is a single file copy, so failure risk is small, but it had never actually been exercised
- **effort:** small
- **resolution:** Ran the install in a scratch repo. Mechanics pass: SKILL.md lands at `.claude/skills/refine/SKILL.md` with valid frontmatter (name + description, which is what skill discovery requires), `.refine/backlog.md` and `.refine/done.md` seed cleanly, and the install commit succeeds. The GitHub fetch step fails: https://github.com/wpkita/refine returns 404 unauthenticated, so the prompt as written cannot work from a fresh target session — validated from the local clone instead, and filed the 404 as a high-impact bug at the top of the backlog. The item earned its keep: "never actually exercised" was hiding a real blocker.

### Give Analyze a lens catalog: what to look for, when it applies, and Refine's stance

- **type:** feature
- **impact:** high — the Analysis Phase hardcoded four deterministic checks and two qualitative passes; arbitrary target repos need far more dimensions, and candidate quality bounds everything downstream
- **effort:** medium
- **resolution:** Rewrote SKILL.md's Analysis Phase around a fifteen-lens catalog (tests, TODO markers, doc drift, dead code, coverage gaps, e2e gaps, secrets, vulnerable deps, deprecated calls, naming, misspellings, slow paths, DB indexes, architecture, gap analysis), absorbing the old deterministic/qualitative sections. Each lens carries a check, an "applies when" condition, and a one-line stance — the stances are where the opinionated principle is encoded. A Haiku recon pass identifies what the repo is and selects only applicable lenses; the target's own CLAUDE.md/README serve as repo-specific values, so no Refine config surface exists. Lenses surface, the scoring rubric prices — which is what makes subjective lenses safe. Catalog is a floor, not a ceiling: recon may improvise repo-specific lenses. Rejected: per-repo enabled-checks config (defeats unattended + opinionated), numeric targets (false precision), exhaustive every-pass runs (cost, noise).

### Define the unattended-checkpoint mechanism

- **type:** feature
- **impact:** medium — unattended operation is the primary use case, but the between-item checkpoint had no way to "time out": an interactive question blocks forever
- **effort:** medium
- **resolution:** Interruption is the checkpoint. Interactive sessions ask as before; unattended runs (scheduled/headless, or any session where a checkpoint went unanswered) never ask — the checkpoint is stated in the iteration summary and the loop continues immediately, with any arriving user message counting as the answer. One unanswered checkpoint degrades the session to unattended. Rejected timeout-based asking (no reliable mechanism) and every-N-iterations checkpoints (arbitrary). Encoded in SKILL.md step 6 and README.

### Add a LICENSE

- **type:** feature
- **impact:** medium — the repo is public and the vision is other people importing Refine; no license meant all rights reserved and blocked that reuse
- **effort:** small
- **resolution:** MIT, confirmed by the user at the checkpoint (the one call the loop doesn't make unilaterally — licensing is legal, not technical). Copyright 2026 Will Kita.

### Deduplicate the loop: CLAUDE.md defers to SKILL.md

- **type:** bug
- **impact:** medium — CLAUDE.md's Bootup/Between-Work-Items sections predated the skill and had already diverged from it (no stopping criterion, no resolution requirement, no model mapping); two sources of truth guarantee future drift
- **effort:** small
- **resolution:** CLAUDE.md now keeps only the repo imperatives and a bootup trigger pointing at `.claude/skills/refine/SKILL.md`, which is declared the single source of truth for the loop. Found by this iteration's doc-drift check; executed immediately, so it never sat in backlog.md.

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
