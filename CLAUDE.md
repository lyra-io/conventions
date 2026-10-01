# Lyra Conventions Instructions

This public repository maintains shared engineering rules for `lyra-io` projects.

## Required reading

- Read [workflow.md](workflow.md) completely before changing this repository.
- Read each rule file you are changing and preserve unrelated rules.
- `CLAUDE.md` is the single source of this repository's agent instructions; `AGENTS.md` is a tracked relative symlink to it.

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
