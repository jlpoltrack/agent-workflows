---
description: Fetch latest changes and reset local branch to remote
version: 1.3.0
---

// turbo-all

# Fetch and Reset Workflow
**Last Updated: 2026-01-11**

This workflow fetches the latest updates from the remote repository and resets the current local branch to match the remote tracking branch exactly. This will discard any local uncommitted changes.

## Steps

1. Execute Fetch and Reset
```bash
BRANCH=$(git branch --show-current)
REMOTE_COUNT=$(git remote | wc -l | tr -d ' ')

if [ "$REMOTE_COUNT" -eq 1 ]; then
  REMOTE=$(git remote)
else
  REMOTE=$(git remote | grep -i '^jlp$' | head -1)
  if [ -z "$REMOTE" ]; then
    REMOTE=$(git remote | head -1)
  fi
fi

git fetch $REMOTE
git reset --hard $REMOTE/$BRANCH

echo Outcome: Fetched and Reset \| Branch: $BRANCH \| Remote: $REMOTE
```

```powershell
$branch = git branch --show-current
$remotes = git remote
$remoteCount = @($remotes).Count

if ($remoteCount -eq 1) {
    $remote = $remotes
} else {
    $remote = $remotes | Where-Object { $_ -match "^jlp$" } | Select-Object -First 1
    if (-not $remote) {
        $remote = $remotes | Select-Object -First 1
    }
}

git fetch $remote
git reset --hard "$remote/$branch"

Write-Output "Outcome: Fetched and Reset | Branch: $branch | Remote: $remote"
```

## Usage

Simply say: "/fetch-reset" or "fetch and reset"