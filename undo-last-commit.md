---
description: Undo the last commit (keep changes staged)
version: 1.0.0
---

// turbo-all

# Undo Last Commit Workflow
**Last Updated: 2025-12-27**

This workflow "un-commits" your last change but keeps all files staged, allowing for quick fixes.

## Steps

1. Echo current status
```bash
echo "Undoing last commit on: $(git branch --show-current)"
git log -1 --oneline
```

2. Soft reset to previous commit
```bash
git reset --soft HEAD~1
```

3. Confirm state
```bash
git status
```

## Usage

Simply say: "/undo-last-commit"
