# Done

Completed backlog items, most recent first. Moved here from [backlog.md](backlog.md).

### Decide if Claude skill or other

- **type:** feature
- **impact:** high — packaging determines how Refine is imported into target repos and how it runs unattended
- **effort:** medium
- **resolution:** Packaged as a Claude Code skill (`SKILL.md` + the `.refine/` backlog files, both flat files committed to the target repo). Rejected a plugin: it bundles multiple skills/commands/hooks and needs distribution/versioning infra Refine doesn't need for a single self-contained loop. A skill matches the backlog's own flat-file-in-target-repo pattern with no install/build step, and is invocable directly or picked up via this repo's own bootup convention — fits the unattended, phone-driven use case cleanly. See README.md.
