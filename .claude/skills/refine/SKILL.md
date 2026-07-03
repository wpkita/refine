---
name: refine
description: Iteratively improve this repository - analyze it, pick the single biggest bang-for-the-buck improvement, apply it, repeat. Use when the user asks to refine the repo, run the improvement loop, or work the .refine/ backlog.
---

# Refine

Improve this repository one focused change at a time, working from the priority-ordered backlog in `.refine/backlog.md`. Unattended operation is the primary use case: never block waiting on the user when a defensible default exists.

## The Loop

1. **Select.** Read `.refine/backlog.md`. The topmost item is next. If the backlog is empty, run an analysis pass first (step 5) to populate it.
2. **Execute.** Implement the item now, in this session. Do not merely read, restate, or analyze it. Exactly one item per iteration — never batch.
3. **Record.** Move the completed item from `.refine/backlog.md` to `.refine/done.md`, appending a `resolution:` line stating what was decided or built and why.
4. **Commit.** One commit per iteration, containing the improvement and every backlog mutation it caused. Never add co-authoring; leave the user's configured Git name and email.
5. **Analyze (as needed).** Run the Analysis Phase (below) and append its candidates to the backlog in priority order.
6. **Checkpoint.** Ask the user: continue to the next item, or add a new item first? If they add one, slot it into priority order yourself — never ask where it goes. If the session is unattended or the user does not respond, continue. The checkpoint must never block the loop.
7. **Stop** when the user says so, or when the Stopping Criterion (below) fires.

## Analysis Phase

Run when the backlog is empty, or when instructed to refresh it.

**Deterministic checks** (delegate to Haiku subagents):

- Run the repo's test suite and linters, if present. Failures become `type: bug` candidates.
- Scan for TODO/FIXME/XXX markers.
- Detect doc drift: docs referencing files, commands, or states that no longer exist.
- Flag dead code and unused dependencies where the repo's tooling supports it.

**Qualitative review** (Sonnet):

- Architecture and readability pass over core or recently-touched files.
- Gap analysis: decisions made but not yet turned into artifacts; stated principles with no mechanism behind them.

**Scoring rubric.** Rate each candidate's `impact` (high/medium/low — user-visible value, or how much it unblocks future iterations) and `effort` (small/medium/large — expected size of the iteration). Qualitative ratings only; numeric scores are false precision. Priority order: impact first, lower effort breaks ties, bugs beat features on equal footing. An item too large for one iteration must be split before it enters the backlog.

**Diminishing-returns hook.** If a full pass yields only low-impact candidates, evaluate the Stopping Criterion rather than silently continuing.

## Stopping Criterion

Diminishing returns means the best available work is no longer worth an iteration. Evaluate after every Analyze pass (delegate the judgment to Opus). Stop when either fires:

- Two consecutive Analyze passes yield only low-impact candidates, or none at all.
- The last three completed iterations were all low-impact.

An empty backlog alone is not a stopping signal — it triggers Analyze. Stopping means reporting, not just halting: summarize the run's completed items, name the signal that fired, and leave remaining low-impact candidates in the backlog for a future run. Bias toward stopping: restarting is cheap; an unattended loop grinding on low-value work is not.

## Backlog Format

Items in `.refine/backlog.md` are titled `###` headings — no numbering; file order is priority order. Each carries `type` (bug | feature), `impact` and `effort` ratings with a one-line justification, and `notes` with enough context to execute the item cold.

## Model Selection

When delegating to subagents, match the model to the work:

| Task | Model |
| --- | --- |
| Backlog bookkeeping (append, move, reformat) | Haiku |
| Broad repo exploration and analysis runs | Haiku |
| Candidate scoring and improvement selection | Sonnet |
| Implementing the improvement | Sonnet (session default) |
| Diminishing-returns evaluation | Opus |
