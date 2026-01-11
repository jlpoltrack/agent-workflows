---
description: Rebase current branch on origin/main
version: 1.1.0
---

// turbo-all

# Rebase on Main Workflow
**Last Updated: 2026-01-11**

This workflow keeps your feature branch up-to-date with the project's main branch.

## Steps

1. Fetch and rebase on origin/main
```bash
BRANCH=$(git branch --show-current)
REMOTE_COUNT=$(git remote | wc -l | tr -d ' ')

if [ "$REMOTE_COUNT" -eq 1 ]; then
  REMOTE=$(git remote)
else
  REMOTE=$(git remote | grep -i '^jlp$' | head -1)
  if [ -z "$REMOTE" ]; then
    REMOTE=$(git remote | grep -i '^origin$' | head -1)
  fi
  if [ -z "$REMOTE" ]; then
    REMOTE=$(git remote | head -1)
  fi
fi

echo Branch: $BRANCH
echo Target: $REMOTE/main
echo ""

git fetch $REMOTE main
git rebase $REMOTE/main

echo ""
echo Outcome: Rebased \| Branch: $BRANCH \| Base: $REMOTE/main
```

```powershell
$branch = git branch --show-current
$remotes = @(git remote)

if ($remotes.Count -eq 1) {
    $remote = $remotes[0]
} else {
    $remote = $remotes | Where-Object { $_ -eq 'jlp' } | Select-Object -First 1
    if (-not $remote) {
        $remote = $remotes | Where-Object { $_ -eq 'origin' } | Select-Object -First 1
    }
    if (-not $remote) {
        $remote = $remotes | Select-Object -First 1
    }
}

Write-Host "Branch: $branch"
Write-Host "Target: $remote/main"
Write-Host ""

git fetch $remote main
git rebase "$remote/main"

Write-Host ""
Write-Host "Outcome: Rebased | Branch: $branch | Base: $remote/main"
```

## Usage

Simply say: "/rebase-main"