# moyuan-labs GitHub standards

This public repository provides organization-wide GitHub defaults and reusable automation for `moyuan-labs`. The Node workflow has completed a real cross-repository CommerceKernel run; Python and content workflows remain candidates pending real callers.

## What is inherited automatically

- Pull request and issue templates
- Contribution guidance
- Security reporting guidance

Repositories can override these defaults by defining their own files.

## What is injected by repository profile

GitHub does not automatically inherit Dependabot configuration or technology-specific caller workflows. A user requests a repository name, profile, and visibility; the responsible Agent runs the audited repository creator:

```bash
./scripts/create-repository <repository-name> <node|python|docs|assets> [private|public]
```

The user does not need to run Git commands or configure the repository by hand. The creator initializes the repository, opens a governance bootstrap pull request, and enables automatic deletion of merged remote head branches. It never enables auto-merge and never merges the bootstrap pull request.

See [GitHub governance](docs/GITHUB_GOVERNANCE.md) for inheritance, plan limits, ruleset status, and the local branch-cleanup boundary.
