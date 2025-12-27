---
description: Squash all commits on the branch into one and force-push
version: 1.0.0
---

// turbo-all

# Squash and Push Workflow
**Last Updated: 2025-12-27**

This workflow squashes all commits on the current branch (relative to the upstream's main branch) into a single commit and force-pushes it to the remote repository.

## Steps

1. Get and display the current branch name
```bash
echo "Branch: $(git branch --show-current)"
```

2. Get and display the upstream remote
```bash
echo "Remote: $(git config --get branch.$(git branch --show-current).remote || echo "origin")"
```

3. Prompt the user for a single-line commit message
```bash
# The agent will prompt for this message using notify_user or a direct question
```

4. Determine the merge base with your remote main branch (defaulting to origin/main)
```bash
git merge-base $(git config --get branch.$(git branch --show-current).remote || echo "origin")/main $(git branch --show-current)
```

5. Soft reset to the merge base (leaves files staged)
```bash
git reset --soft $(git merge-base $(git config --get branch.$(git branch --show-current).remote || echo "origin")/main $(git branch --show-current))
```

6. Commit with the provided message
```bash
# Example: git commit -m "Your approved message here"
```

7. Force-push with lease to the upstream remote
```bash
git push --force-with-lease $(git config --get branch.$(git branch --show-current).remote || echo "origin") $(git branch --show-current)
```

## Usage

Simply say: "/squash-push" or "squash and push"
