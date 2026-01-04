---
description: Fetch latest changes and reset local branch to remote
version: 1.2.0
---

// turbo-all

# Fetch and Reset Workflow
**Last Updated: 2025-12-27**

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
fi

git fetch $REMOTE
git reset --hard $REMOTE/$BRANCH

echo Outcome: Fetched and Reset \| Branch: $BRANCH \| Remote: $REMOTE
```

## Usage

Simply say: "/fetch-reset" or "fetch and reset"
