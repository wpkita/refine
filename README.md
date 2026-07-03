# Refine

Refine is a tool/skill/methodology for iteratively improving a repository. For now, this will focus on code, but the idea is you use Refine on a repository you own and leave it to improve it automatically and agentically in an opinionated way.

Refine gets imported into a target repository (possibly packaged as a Claude Code skill — packaging is undecided) and autonomously improves that repository in a loop, in the spirit of [karpathy/autoresearch](https://github.com/karpathy/autoresearch). Refine is also used to refine itself — this repository is its own first target.

## The Core Loop

1. Run deterministic and non-deterministic, quantitative and qualitative analyses on the target repository.
2. Choose the single biggest bang-for-the-buck improvement.
3. Apply that one improvement.
4. Repeat until diminishing returns are detected or the user stops it.

## Design Principles

- **One improvement per iteration.** Each loop cycle produces exactly one focused change, not a batch.
- **Opinionated.** Refine decides what "better" means; it does not ask the user to arbitrate every choice.
- **Unattended operation is the primary use case.** The user installs Refine into a personal repo, starts a remote session (e.g., from a phone), and walks away while the agent loops. Anything requiring the user to sit at a computer defeats the purpose.
- **Knows when to stop.** Diminishing returns are a first-class stopping criterion, not an afterthought.

## The Backlog

Refine maintains its backlog as flat files committed to the target repo: `.refine/backlog.md` holds candidate improvements (bugs and features compete in one queue), and `.refine/done.md` holds completed items. Git history is the audit trail — every backlog mutation lands in the same commit as the improvement that consumed it, and the files survive ephemeral remote sessions because they travel with the clone.

## Documentation Convention

This README is context. [CLAUDE.md](CLAUDE.md) is imperatives and directions.

## Current State

No code yet — this README, CLAUDE.md, and the `.refine/` backlog files. Refine is dogfooding: this repository is its own first target.
