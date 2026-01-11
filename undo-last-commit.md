---
description: Undo the last commit (keep changes staged)
version: 1.1.0
---

// turbo-all

# Undo Last Commit Workflow
**Last Updated: 2026-01-11**

This workflow "un-commits" your last change but keeps all files staged, allowing for quick fixes.

## Steps

1. Execute Undo
```bash
BRANCH=$(git branch --show-current)
echo "Undoing last commit on: $BRANCH"
git log -1 --oneline

git reset --soft HEAD~1
git status
```

```powershell
$branch = git branch --show-current
Write-Output "Undoing last commit on: $branch"
git log -1 --oneline

git reset --soft HEAD~1
git status
```

## Usage

Simply say: "/undo-last-commit"