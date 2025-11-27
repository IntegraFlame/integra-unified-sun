# Master Blueprint - PowerShell Execution Without Sandboxing

## Overview

This document describes how PowerShell scripts are executed in GitHub Actions workflows without sandboxing restrictions.

## Problem Statement

By default, some execution environments may apply sandboxing restrictions that prevent PowerShell scripts from running with full privileges or accessing external resources. This can block installation scripts like the UV package manager installer.

## Solution

### PowerShell Execution Policy Bypass

The workflow uses `-ExecutionPolicy Bypass` flag at the shell level to disable sandboxing restrictions:

```yaml
shell: pwsh -ExecutionPolicy Bypass -Command {0}
run: |
  irm https://astral.sh/uv/install.ps1 | iex
```

### Key Components

1. **ExecutionPolicy Bypass**: Disables all execution policy restrictions temporarily for the command
2. **Direct Command Execution**: Uses `-Command` (or `-c`) to execute inline scripts
3. **Remote Script Installation**: Downloads and immediately executes the UV installer script

### Workflow Configuration

The `powershell-setup.yml` workflow is configured to:
- Run on Windows runners (where PowerShell is native)
- Execute PowerShell commands without sandboxing
- Install and verify the UV package manager

### Usage

The workflow can be triggered:
- Manually via workflow_dispatch
- Called from other workflows using workflow_call

## Security Considerations

**WARNING**: Bypassing execution policies removes security protections. Only use this approach:
- In trusted CI/CD environments
- When installing software from verified sources
- With proper code review and approval processes

## References

- [UV Package Manager](https://github.com/astral-sh/uv)
- [PowerShell Execution Policies](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies)
