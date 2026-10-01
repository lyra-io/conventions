# Lyra Conventions Instructions

This public repository maintains shared engineering rules for `lyra-io` projects.

`CLAUDE.md` is the entry point; do not add a separate README.

## Required reading

- Read [workflow.md](workflow.md) completely before changing this repository.
- Read each rule file you are changing and preserve unrelated rules.
- `CLAUDE.md` is the single source of this repository's agent instructions; `AGENTS.md` is a tracked relative symlink to it.

## Adoption by other projects

- The approved shared rules live on `main`; pull-request branches remain proposals until reviewed and merged. Change shared rules here rather than maintaining separate copies in every project.
- Each project's root `CLAUDE.md` must explicitly require reading the applicable shared rules, then add its own build commands, layout, and component-specific constraints. Keep `AGENTS.md` as a tracked relative symlink to that project's `CLAUDE.md`.
- A link alone is not a guarantee that an agent has loaded its target. Read the rules from a local checkout of this repository's approved `main`, or fetch their contents from GitHub. Use one recorded commit for a task; do not silently switch rule revisions midway through it.
- Report unavailable rules rather than claiming they were read. Repository adoption changes must be reviewed separately; creating this repository does not update other projects automatically.

## Scope

- Keep rules concise, actionable, and language-specific where appropriate.
- Distinguish Lyra policy from upstream language/library conventions.
- Preserve upstream APIs, external trait signatures, generated code, and established non-Rust language conventions unless a separately reviewed change requires otherwise.
- Keep component details in the component repository. Do not publish private proposal content, credentials, logs, or infrastructure data here.
- A rule change does not authorize a bulk code rename or deployment change.

## Verification

- Run `git diff --check` and review the complete staged diff.
- Check Markdown code fences, table structure, and local links.
- Verify `AGENTS.md` is a Git symlink targeting `CLAUDE.md`, not a duplicated file.
- For code examples, run the relevant formatter or syntax check and state whether the example was actually compiled or executed.
- Put actual checks and any untested behavior in the PR's Testing section. This repository has no application runtime test suite.
