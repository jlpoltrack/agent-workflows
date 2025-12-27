---
description: Squash all commits on the branch into one and force-push
version: 1.2.0
---

// turbo-all

# Squash and Push Workflow
**Last Updated: 2025-12-27**

This workflow squashes all commits on the current branch (relative to the upstream's main branch) into a single commit and force-pushes it to the remote repository.

## Steps

1. Execute Squash and Push (requires commit message input)
```bash
BRANCH=$(git branch --show-current)
REMOTE_COUNT=$(git remote | wc -l | tr -d ' ')

if [ "$REMOTE_COUNT" -eq 1 ]; then
  REMOTE=$(git remote)
else
  REMOTE=$(git remote | grep -i '^jlp$' | head -1)
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

## Usage

Simply say: "/squash-push" or "squash and push"
