---
description: Rebase current branch on origin/main
version: 1.0.0
---

// turbo-all

# Rebase on Main Workflow
**Last Updated: 2025-12-27**

This workflow keeps your feature branch up-to-date with the project's main branch.

## Steps

1. Echo current context
```bash
echo "Branch: $(git branch --show-current)"
echo "Target: origin/main"
```

2. Fetch latest main
```bash
git fetch origin main
```

3. Rebase onto origin/main
```bash
git rebase origin/main
```

## Usage

Simply say: "/rebase-main"
