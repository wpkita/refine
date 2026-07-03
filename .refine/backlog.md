# Backlog

Candidate improvements, one per entry. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### 1. Decide model selection per task type

- **type:** feature
- **impact:** high — model choice drives cost and quality of every loop iteration, and unattended loops multiply both
- **effort:** medium
- **notes:** Define which Claude model each of Refine's tasks should use when run via agents and subagents — e.g., exploration/analysis of the target repo, execution of an improvement, backlog processing (appending candidates, scoring, popping the next item), diminishing-returns evaluation. Consider a cheap/fast model (Haiku) for mechanical work like backlog bookkeeping and broad exploration, and a stronger model (Sonnet/Opus) for judgment-heavy work like selecting the biggest bang-for-the-buck improvement and writing code. Output should be an opinionated mapping of task → model, plus where that mapping lives (skill config? per-agent frontmatter?).
