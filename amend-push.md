---
description: Stage, amend, and force-push changes to the remote
version: 1.1.1
---

// turbo-all

# Amend and Force-Push Workflow
**Last Updated: 2025-12-27**

This workflow stages all modified files, amends them to the last commit, and force-pushes the current branch to its upstream remote repository.

## Steps

1. Get and display the current branch name
```bash
echo "Branch: $(git branch --show-current)"
```

2. Get and display the upstream remote
```bash
echo "Remote: $(git config --get branch.$(git branch --show-current).remote || echo "origin")"
```

3. Stage all modified files
```bash
git add -A
```

4. Amend to the last commit without editing the message
```bash
git commit --amend --no-edit
```

5. Force-push to the upstream remote (using branch and remote from steps 1 and 2)
```bash
git push --force-with-lease $(git config --get branch.$(git branch --show-current).remote || echo "origin") $(git branch --show-current)
```

## Usage

Simply say: "/amend-push" or "amend and push"