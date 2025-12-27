---
description: Fetch latest changes and reset local branch to remote
version: 1.2.0
---

// turbo-all

# Fetch and Reset Workflow
**Last Updated: 2025-12-31**

This workflow fetches the latest updates from the remote repository and resets the current local branch to match the remote tracking branch exactly. This will discard any local uncommitted changes.

## Steps

1. Execute Fetch and Reset
```bash
BRANCH=$(git branch --show-current)
if [ -z "$BRANCH" ]; then
  echo "Error: Could not determine current branch"
  exit 1
fi

# priority: jlp remote, then fallback to first available
REMOTE=$(git remote | grep -ix 'jlp' | head -1)
if [ -z "$REMOTE" ]; then
  REMOTE=$(git remote | head -1)
fi

if [ -z "$REMOTE" ] || [ -z "$BRANCH" ]; then
  echo "Error: Missing Remote ($REMOTE) or Branch ($BRANCH)"
  exit 1
fi

git fetch "$REMOTE"
git reset --hard "$REMOTE/$BRANCH"

echo SUCCESS: Branch $BRANCH reset to $REMOTE/$BRANCH

```

## Usage

Simply say: "/fetch-reset" or "fetch and reset"
