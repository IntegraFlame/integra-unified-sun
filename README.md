# Integra Unified Sun

This repository contains GitHub Actions workflows and documentation for running PowerShell commands without sandboxing restrictions.

## Workflows

### PowerShell Setup (No Sandbox)
Located in `.github/workflows/powershell-setup.yml`

This workflow allows PowerShell execution with bypassed execution policies, enabling:
- Installation of the UV package manager
- Execution of remote PowerShell scripts
- Running commands without sandboxing restrictions

**Usage:**
```yaml
# Call from another workflow
jobs:
  my-job:
    uses: ./.github/workflows/powershell-setup.yml
```

Or trigger manually via GitHub Actions UI.

### Static Content Deployment
Located in `.github/workflows/static.yml`

Deploys static content to GitHub Pages.

## Documentation

See [docs/architecture/Masterblueprint.md](docs/architecture/Masterblueprint.md) for detailed information about PowerShell execution without sandboxing.

## Security Note

The PowerShell workflows bypass execution policies. Use with caution and only in trusted environments.
