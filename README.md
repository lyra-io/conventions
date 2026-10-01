# Lyra Conventions

Shared engineering rules for repositories in `lyra-io`.

- [Workflow](workflow.md): topic branches, pull requests, squash merges, and safe changes.
- [Repository instructions](CLAUDE.md): how to maintain these rules.

The approved rules live on `main`. Pull-request branches are proposals until reviewed and merged. Change shared rules here rather than maintaining separate copies in every project.

Each project's root `CLAUDE.md` should explicitly require reading the applicable shared rules and then add its own build commands, layout, and component-specific constraints. Keep `AGENTS.md` as a tracked relative symlink to that project's `CLAUDE.md`.

A link alone is not a guarantee that an agent has loaded its target. Read the rules from a local checkout of this repository's approved `main`, or fetch their contents from GitHub. Use a single recorded commit for a task; do not silently switch rule revisions midway through it. Report unavailable rules rather than claiming they were read. Repository adoption changes must be reviewed separately; creating this repository does not update other projects automatically.
