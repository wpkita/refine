# Backlog

Candidate improvements, one per entry, ordered by priority (topmost is next). Items are titled, not numbered — order in the file is the priority. The loop's analysis phase appends candidates; the selection phase pops the biggest bang-for-the-buck item. Completed items move to [done.md](done.md).

## Items

### Ask the user between work items whether to continue or add a backlog item

- **type:** feature
- **impact:** medium — gives the user a lightweight steering point between iterations without breaking the loop's one-improvement-per-iteration rhythm
- **effort:** medium
- **notes:** After completing a work item (and its commit), ask the user whether to (a) continue to the next backlog item or (b) add a new item to the backlog first. If the user adds a new item, the LLM makes a judgment call on where to slot it in the priority order — it does not automatically go first or last, and the user is not asked to arbitrate placement. Reconcile with the unattended-operation design principle: when nobody responds (remote/phone-driven sessions), the loop should default to continuing rather than blocking.
