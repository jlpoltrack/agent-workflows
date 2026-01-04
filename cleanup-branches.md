---
description: Clean up local branches merged into main
version: 1.2.0
---

// turbo-all

# Cleanup Branches Workflow
**Last Updated: 2025-12-27**

This workflow identifies and deletes local branches that have already been merged into the `main` branch.

## Steps

1. List and delete merged branches
```bash
# Prefer 'JLP' or 'origin' if they exist, otherwise use first remote
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

## Usage

Simply say: "/cleanup-branches"
