# Shared Git and Review Workflow

These rules apply to changes in every `lyra-io` repository, including documentation, code, automation, dependencies, and upstream synchronization.

## Branches and pull requests

- All changes to an existing default or protected integration branch must arrive through a pull request. Never push directly to `main`, `master`, or another protected integration branch.
- Work on a topic branch with a conventional prefix such as `feat/`, `fix/`, `docs/`, `test/`, `refactor/`, `chore/`, or `ci/`. Never use a `codex/` prefix.
- Preserve existing user changes. Do not reset, overwrite, publish, or include unrelated work in a commit.
- Use a conventional PR title such as `feat: ...`, `fix: ...`, or `docs: ...`.
- Structure PR descriptions with `## Motivation`, `## Modifications`, and `## Testing`, with blank lines after headings and before lists. Describe exact API/configuration changes and actual verification results.
- Leave PRs unmerged, with auto-merge disabled, unless the user explicitly requests merging.
- When merging is explicitly requested, squash merge only. Do not use merge commits or rebase merges.
- Do not bypass or disable protections. These rules apply to administrators and automation too.

## Repository setup and enforcement

- A new repository may use GitHub's initial seed commit to establish its default branch. Put substantive rules, code, and documentation changes on topic branches for PR review; do not use bootstrap as an exception for later direct pushes.
- Configure squash-only repository merge settings and require pull requests on the default branch, with no bypass actors, where GitHub supports enforcement.
- If the repository's plan or permissions prevent enforcement, report the gap and still follow the PR workflow. Do not change visibility or billing to bypass the limitation.
- Do not create repositories, change their visibility, or add unrelated repositories to a task without authorization. Use the agreed name and visibility.

## Scope and safety

- A proposal is not an implementation approval, and a passing documentation check is not a passing runtime test.
- Do not broaden an approved naming or documentation change into a bulk API refactor without a separate scope decision.
- Never commit credentials, password files, Secret contents, private keys, kubeconfigs, or sensitive runtime artifacts. Public repositories must not receive private project material accidentally.
- State compatibility effects and update callers/tests together when a separately approved change renames an existing API.
- Resolve contradictions between shared rules and component instructions explicitly; do not silently discard either set.
