---
description: Squash all commits on the branch into one and force-push
version: 1.1.0
---

// turbo-all

# Squash and Push Workflow
**Last Updated: 2026-01-11**

This workflow squashes all commits on the current branch (relative to the upstream's main branch) into a single commit and force-pushes it to the remote repository.

## Steps

1. Execute Squash and Push (requires commit message input)

### Bash
```bash
BRANCH=$(git branch --show-current)
REMOTE_COUNT=$(git remote | wc -l | tr -d ' ')

if [ "$REMOTE_COUNT" -eq 1 ]; then
  REMOTE=$(git remote)
else
  REMOTE=$(git remote | grep -i '^jlp$' | head -1)
  if [ -z "$REMOTE" ]; then
    REMOTE="origin"
  fi
fi

MERGE_BASE=$(git merge-base $REMOTE/main $BRANCH)

echo Current Branch: $BRANCH
echo Remote: $REMOTE
echo ""
echo "Enter commit message for squashed commit:"
read -r COMMIT_MSG

git reset --soft $MERGE_BASE
git commit -m "$COMMIT_MSG"
git push --force-with-lease $REMOTE $BRANCH --quiet

echo ""
echo Outcome: Squashed and Pushed \| Branch: $BRANCH \| Remote: $REMOTE
```

### PowerShell
```powershell
$branch = git branch --show-current
$remotes = git remote
$remoteCount = @($remotes).Count

if ($remoteCount -eq 1) {
    $remote = $remotes
} else {
    $remote = $remotes | Where-Object { $_ -match '^jlp$' } | Select-Object -First 1
    if (-not $remote) {
        $remote = "origin"
    }
}

$mergeBase = git merge-base "$remote/main" $branch

Write-Host "Current Branch: $branch"
Write-Host "Remote: $remote"
Write-Host ""
$commitMsg = Read-Host "Enter commit message for squashed commit"

git reset --soft $mergeBase
git commit -m "$commitMsg"
git push --force-with-lease $remote $branch --quiet

Write-Host ""
Write-Host "Outcome: Squashed and Pushed | Branch: $branch | Remote: $remote"
```

## Usage

Simply say: "/squash-push" or "squash and push"