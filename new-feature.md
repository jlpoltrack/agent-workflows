---
description: Create a new branch from origin/main
version: 1.0.0
---

// turbo-all

# New Feature Branch Workflow
**Last Updated: 2025-12-27**

This workflow ensures you start from the latest code by fetching the remote and creating a new branch from `origin/main`.

## Steps

1. Fetch the latest changes from origin
```bash
git fetch origin
```

2. Prompt for branch name
```bash
# Agent will prompt for: "Enter new branch name: "
```

3. Create and switch to the new branch from origin/main
```bash
# Example: git checkout -b feature/name origin/main
```

## Usage

Simply say: "/new-feature"
