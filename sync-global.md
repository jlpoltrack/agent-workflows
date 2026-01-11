---
description: Sync workflows and agent rules to global ~/.gemini directory
version: 2.2.0
---

// turbo-all

# Global Sync Workflow
**Last Updated: 2026-01-11**

Syncs all `.md` workflow files and the `GEMINI.md` agent rules file from this repository to the global `.gemini` directory structure. Supports Windows (PowerShell) and macOS/Linux (Bash).

## Steps

### Windows (PowerShell)

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

### macOS / Linux (Bash)

1. Create the workflows destination directory if needed
```bash
mkdir -p "$HOME/.gemini/antigravity/global_workflows"
```

2. Copy all workflow files to the global directory
```bash
find . -maxdepth 1 -name "*.md" ! -name "README.md" ! -name "GEMINI.md" -exec cp {} "$HOME/.gemini/antigravity/global_workflows/" \;
```

3. Copy GEMINI.md agent rules to ~/.gemini (overwrites existing)
```bash
cp GEMINI.md "$HOME/.gemini/GEMINI.md"
```

4. Confirm synced files
```bash
echo "=== Workflows ===" && ls "$HOME/.gemini/antigravity/global_workflows/"*.md && echo -e "\n=== Agent Rules ===" && cat "$HOME/.gemini/GEMINI.md"
```

## Usage

Simply say: "/sync-global" or "sync global"
