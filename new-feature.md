---
description: Create a new branch from origin/main
version: 1.1.0
---

// turbo-all

# New Feature Branch Workflow
**Last Updated: 2026-01-11**

This workflow ensures you start from the latest code by fetching the remote and creating a new branch from upstream `main`.

## Steps

### Bash

1. Create new feature branch (Agent will prompt for remote and branch name)
```bash
# Detect default remote (upstream > origin > first available)
DEFAULT_REMOTE=$(git remote | grep "^upstream$" || git remote | grep "^origin$" || git remote | head -n 1)

echo "Available remotes:"
git remote -v | awk '{print $1}' | sort -u
echo ""
echo "Enter remote name [Default: $DEFAULT_REMOTE]:"
read -r INPUT_REMOTE
REMOTE=${INPUT_REMOTE:-$DEFAULT_REMOTE}

if [ -z "$REMOTE" ]; then
    echo "!!! Error: No remote selected"
    exit 1
fi

if ! git remote | grep -q "^$REMOTE$"; then
  echo "!!! Error: Remote '$REMOTE' does not exist"
  exit 1
fi

git fetch $REMOTE

echo ""
echo "Remote: $REMOTE"
echo ""
echo "Enter new branch name:"
read -r BRANCH_NAME

if [ -z "$BRANCH_NAME" ]; then
    echo "!!! Error: Branch name required"
    exit 1
fi

git checkout -b $BRANCH_NAME $REMOTE/main
git branch --set-upstream-to=$REMOTE/main

echo ""
echo Outcome: Created Branch \| Name: $BRANCH_NAME \| Base: $REMOTE/main
```

### PowerShell

1. Create new feature branch
```powershell
$remotes = git remote
# Detect default remote (upstream > origin > first available)
$defaultRemote = $remotes | Where-Object { $_ -eq "upstream" }
if (-not $defaultRemote) {
    $defaultRemote = $remotes | Where-Object { $_ -eq "origin" }
}
if (-not $defaultRemote) {
    $defaultRemote = $remotes | Select-Object -First 1
}

Write-Host "Available remotes:"
git remote -v | ForEach-Object { ($_ -split '\s+')[0] } | Select-Object -Unique
Write-Host ""

$inputRemote = Read-Host "Enter remote name [Default: $defaultRemote]"
if ([string]::IsNullOrWhiteSpace($inputRemote)) {
    $remote = $defaultRemote
} else {
    $remote = $inputRemote
}

if ([string]::IsNullOrWhiteSpace($remote)) {
    Write-Host "!!! Error: No remote selected" -ForegroundColor Red
    exit 1
}

if (-not ($remotes -contains $remote)) {
    Write-Host "!!! Error: Remote '$remote' does not exist" -ForegroundColor Red
    exit 1
}

git fetch $remote

Write-Host ""
Write-Host "Remote: $remote"
Write-Host ""
$branchName = Read-Host "Enter new branch name"

if ([string]::IsNullOrWhiteSpace($branchName)) {
    Write-Host "!!! Error: Branch name is required" -ForegroundColor Red
    exit 1
}

git checkout -b $branchName "$remote/main"
git branch --set-upstream-to="$remote/main"

Write-Host ""
Write-Host "Outcome: Created Branch | Name: $branchName | Base: $remote/main"
```

## Usage

Simply say: "/new-feature"