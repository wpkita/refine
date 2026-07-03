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
5. **Analyze (as needed).** Run deterministic checks (tests, lint, doc drift, TODO scan) and qualitative review of the target repo. Append findings to the backlog as candidate items with `type`, `impact`, `effort`, and `notes`, slotted into priority order by your own judgment.
6. **Checkpoint.** Ask the user: continue to the next item, or add a new item first? If they add one, slot it into priority order yourself — never ask where it goes. If the session is unattended or the user does not respond, continue. The checkpoint must never block the loop.
7. **Stop** when the user says so, or when diminishing returns are detected (successive analysis passes yield only low-impact candidates).

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
