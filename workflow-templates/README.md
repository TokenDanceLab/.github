# Workflow templates

Skeletons for new repos. Prefer **callable** workflows under `.github/workflows/`:

```yaml
jobs:
  ci:
    uses: TokenDanceLab/.github/.github/workflows/ci-go-service.yml@main
    with:
      go_version: "1.25"
```

Policy: `server/docs/architecture/github-actions-ci-cd-policy.md`.
