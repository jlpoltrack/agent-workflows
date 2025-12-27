---
description: Generate a summary of changes against origin/main
version: 1.0.0
---

// turbo-all

# PR Summary Workflow
**Last Updated: 2025-12-27**

This workflow analyzes the differences between your current branch and `origin/main` to help generate a PR description.

## Steps

1. Echo current context
```bash
echo "Branch: $(git branch --show-current)"
```

2. Show file breakdown (insertions/deletions)
```bash
git diff --stat origin/main..$(git branch --show-current)
```

3. Show high-level diff of changes
```bash
git diff origin/main..$(git branch --show-current)
```

4. Summarize
```bash
# Agent will now analyze the diff above and provide a concise summary.
```

## Usage

Simply say: "/pr-summary"
