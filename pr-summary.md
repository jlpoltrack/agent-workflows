---
description: Generate a summary of changes against origin/main
version: 1.2.0
---

// turbo-all

# PR Summary Workflow
**Last Updated: 2025-12-27**

This workflow analyzes the differences between your current branch and the upstream `main` branch to help generate a PR description.

## Steps

1. Show changes summary
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
echo "File Statistics:"
git diff --stat $REMOTE/main..$BRANCH
echo ""
echo "Detailed Changes:"
git diff $REMOTE/main..$BRANCH
```

## Usage

Simply say: "/pr-summary"
