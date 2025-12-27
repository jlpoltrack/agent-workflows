---
description: Fetch latest changes and reset local branch to remote
version: 1.1.0
---

// turbo-all

# Fetch and Reset Workflow
**Last Updated: 2025-12-27**

This workflow fetches the latest updates from the remote repository and resets the current local branch to match the remote tracking branch exactly. This will discard any local uncommitted changes.

## Steps

1. Get and display the current branch name
```bash
echo "Branch: $(git branch --show-current)"
```

2. Get and display the upstream remote
```bash
echo "Remote: $(git config --get branch.$(git branch --show-current).remote || echo "origin")"
```

3. Fetch from the upstream remote
```bash
git fetch $(git config --get branch.$(git branch --show-current).remote || echo "origin")
```

4. Reset the current branch to match the remote tracking branch
```bash
git reset --hard $(git config --get branch.$(git branch --show-current).remote || echo "origin")/$(git branch --show-current)
```

## Usage

Simply say: "/fetch-reset" or "fetch and reset"
