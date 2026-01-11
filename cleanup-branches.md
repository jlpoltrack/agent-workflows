---
description: Clean up local branches merged into main
version: 1.1.0
---

// turbo-all

# Cleanup Branches Workflow
**Last Updated: 2026-01-11**

This workflow identifies and deletes local branches that have already been merged into the `main` branch.

## Steps

1. List and delete merged branches

```bash
# prefer 'JLP' or 'origin' if they exist, otherwise use first remote
if git remote | grep -q "^JLP$"; then
  REMOTE="JLP"
elif git remote | grep -q "^origin$"; then
  REMOTE="origin"
else
  REMOTE=$(git remote | head -n 1)
fi

echo "Branches merged into $REMOTE/main:"
MERGED=$(git branch --merged $REMOTE/main | grep -v "^\*" | grep -v "main")

if [ -z "$MERGED" ]; then
  echo "No merged branches to clean up"
else
  echo "$MERGED"
  echo ""
  echo "Deleting merged branches..."
  echo "$MERGED" | xargs git branch -d
  echo ""
  echo Outcome: Cleaned up merged branches
fi
```

```powershell
# prefer 'JLP' or 'origin' if they exist, otherwise use first remote
$remotes = git remote
if ($remotes -contains "JLP") {
    $remote = "JLP"
} elseif ($remotes -contains "origin") {
    $remote = "origin"
} else {
    $remote = $remotes | Select-Object -First 1
}

Write-Host "Branches merged into $remote/main:"
$merged = git branch --merged "$remote/main" | Where-Object { $_ -notmatch "^\*" -and $_.Trim() -ne "main" } | ForEach-Object { $_.Trim() }

if (-not $merged) {
    Write-Host "No merged branches to clean up"
} else {
    $merged | ForEach-Object { Write-Host $_ }
    Write-Host ""
    Write-Host "Deleting merged branches..."
    $merged | ForEach-Object { git branch -d $_ }
    Write-Host ""
    Write-Host "Outcome: Cleaned up merged branches"
}
```

## Usage

Simply say: "/cleanup-branches"
