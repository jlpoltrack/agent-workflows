---
description: Rebase current branch on origin/main
version: 1.2.0
---

// turbo-all

# Rebase on Main Workflow
**Last Updated: 2025-12-27**

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
fi

echo Branch: $BRANCH
echo Target: $REMOTE/main
echo ""

git fetch $REMOTE main
git rebase $REMOTE/main

echo ""
echo Outcome: Rebased \| Branch: $BRANCH \| Base: $REMOTE/main
```

## Usage

Simply say: "/rebase-main"
