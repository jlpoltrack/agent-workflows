---
description: Sync workflows and agent rules to global ~/.gemini directory
version: 2.1.0
---

// turbo-all

# Global Sync Workflow
**Last Updated: 2026-01-09**

Syncs all `.md` workflow files and the `GEMINI.md` agent rules file from this repository to the global `.gemini` directory structure. Optimized for PowerShell/Windows.

## Steps

1. Create the workflows destination directory if needed
```powershell
if (!(Test-Path "$HOME\.gemini\antigravity\global_workflows")) { New-Item -ItemType Directory -Path "$HOME\.gemini\antigravity\global_workflows" -Force }
```

2. Copy all workflow files to the global directory
```powershell
Get-ChildItem -Path *.md -Exclude "README.md", "GEMINI.md" | Copy-Item -Destination "$HOME\.gemini\antigravity\global_workflows\" -Force
```

3. Copy GEMINI.md agent rules to ~/.gemini (overwrites existing)
```powershell
Copy-Item -Path ".\GEMINI.md" -Destination "$HOME\.gemini\GEMINI.md" -Force
```

4. Confirm synced files
```powershell
Write-Host "=== Workflows ==="; Get-ChildItem "$HOME\.gemini\antigravity\global_workflows\*.md" | Select-Object Name; Write-Host "`n=== Agent Rules ==="; Get-Content "$HOME\.gemini\GEMINI.md"
```

## Usage

Simply say: "/sync-global" or "sync global"
