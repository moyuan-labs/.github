# GitHub governance boundary

Snapshot date: 2026-09-01.

## Automatic inheritance

After this repository's bootstrap Pull Request is merged, GitHub automatically supplies its default Pull Request template, Issue templates, `CONTRIBUTING.md`, and `SECURITY.md` to `moyuan-labs` repositories that do not define repository-specific replacements.

## Repository creator injection

GitHub does not automatically inherit `.github/dependabot.yml` or technology-specific caller workflows. `scripts/create-repository` is the single new-repository entry point. It creates a repository, injects the selected `node`, `python`, `docs`, or `assets` profile on `chore/bootstrap-governance`, applies `settings/repository-defaults.json`, and opens a Pull Request. It never auto-merges.

Users do not need to create branches, commit, push, or open and update Pull Requests. The responsible Agent or creator performs those low-risk, traceable actions automatically. Users remain responsible for requirements, Pull Request review, and explicit merge approval or rejection. Merge, force push, history rewrite, repository visibility changes, and deletion of unmerged work remain authorization-gated.

The practical user entry is a request such as: “Create `example-service` as a private `python` repository.” The Agent translates that request into the creator command and returns the bootstrap Pull Request for review.

The default repository setting is `delete_branch_on_merge=true`. GitHub then deletes only the same-repository remote head branch after its Pull Request is merged. It does not delete open, unmerged, default, protected, or cross-repository head branches.

Local branch cleanup remains an Agentic Git Delivery responsibility. Delete a local branch only after confirming the Pull Request is merged, remote default branch is synchronized, the worktree is clean, and the branch has no unmerged commits. Then prune stale remote-tracking references. Otherwise preserve the branch and report the unmet condition.

## Candidate reusable Actions and workflow templates

- `.github/workflows/reusable-node-ci.yml` is the shared npm/lockfile build-and-test implementation.
- `.github/workflows/reusable-python-ci.yml` is the shared uv/lockfile check-and-test implementation.
- `.github/workflows/reusable-content-ci.yml` provides minimal docs/assets integrity checks.
- `workflow-templates/node-ci.yml` is an optional GitHub Actions UI template. It is not automatic provisioning.
- `repository-profiles/*` contains the thin callers and matching Dependabot configuration injected by the repository creator.

Callers currently reference `@main`. Treat the reusable workflows as reviewable organization infrastructure. Do not call them validated from another repository until a real caller Pull Request has completed successfully.

In this bootstrap change, the creator has been syntax-checked and dry-run for all four profiles, and the workflow files have passed `actionlint`. No disposable remote repository was created for an end-to-end provisioner test. The provisioner and workflows remain candidates until their respective real GitHub Pull Requests complete successfully.

## Current plan limitation

The `moyuan-labs` organization is currently on GitHub Free. Organization-wide rulesets for all private repositories and required organization workflows need a higher plan. The current token also lacks `admin:org`.

`rulesets/default-branch-protection.team-plan.json` is therefore a disabled, versioned proposal only. It records the intended default-branch baseline: Pull Requests required, one independent approval, conversation resolution, no deletion, and no force push. Do not describe it as active. After a plan upgrade and explicit settings authorization, an organization owner must review and import or apply it, then verify its repository targeting before enabling enforcement.

Required workflow enforcement is intentionally absent from the draft. Add it only after the plan supports it and each required workflow has been proven against representative repositories.
