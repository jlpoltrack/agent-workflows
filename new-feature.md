---
description: Create a new branch from origin/main
version: 1.1.0
---

// turbo-all

# New Feature Branch Workflow
**Last Updated: 2025-12-27**

This workflow ensures you start from the latest code by fetching the remote and creating a new branch from upstream `main`.

## Steps

1. Create new feature branch (Agent will prompt for remote and branch name)
```bash
echo "Available remotes:"
git remote -v | awk '{print $1}' | sort -u
echo ""
echo "Enter remote name:"
read -r REMOTE

if ! git remote | grep -q "^$REMOTE$"; then
  echo "!!! Error: Remote '$REMOTE' does not exist"
  exit 1
fi

git fetch $REMOTE

echo ""
echo "Remote: $REMOTE"
echo ""
echo "Enter new branch name:"
read -r BRANCH_NAME

git checkout -b $BRANCH_NAME $REMOTE/main
git branch --set-upstream-to=$REMOTE/main

echo ""
echo Outcome: Created Branch \| Name: $BRANCH_NAME \| Base: $REMOTE/main
```

## Usage

Simply say: "/new-feature"
