---
description: Stage, amend, and force-push changes to the remote
version: 1.2.0
---

// turbo-all

# Amend and Force-Push Workflow
**Last Updated: 2025-12-27**

This workflow stages all modified files, amends them to the last commit, and force-pushes the current branch to its upstream remote repository.

## Steps

1. Execute Amend and Force-Push
```bash
BRANCH=$(git branch --show-current)
REMOTE_COUNT=$(git remote | wc -l | tr -d ' ')

if [ "$REMOTE_COUNT" -eq 1 ]; then
  REMOTE=$(git remote)
else
  REMOTE=$(git remote | grep -i '^jlp$' | head -1)
fi

git add -A
git commit --amend --no-edit --quiet
git push --force-with-lease $REMOTE $BRANCH --quiet

echo Outcome: Amended and Pushed \| Branch: $BRANCH \| Remote: $REMOTE
```

## Usage

Simply say: "/amend-push" or "amend and push"