---
description: Clean up local branches merged into main
version: 1.0.0
---

// turbo-all

# Cleanup Branches Workflow
**Last Updated: 2025-12-27**

This workflow identifies and deletes local branches that have already been merged into the `main` branch.

## Steps

1. List branches merged into main (excluding main itself)
```bash
git branch --merged main | grep -v "^\*" | grep -v "main"
```

2. Delete merged branches
```bash
# Example: git branch -d branch-name
# Agent will confirm before deletion
```

## Usage

Simply say: "/cleanup-branches"
