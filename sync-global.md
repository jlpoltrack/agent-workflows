---
description: Sync all local workflows to the global directory
version: 1.0.0
---

// turbo-all

# Global Sync Workflow
**Last Updated: 2025-12-27**

This workflow copies all `.md` workflow files from the current repository into the global `global_workflows` directory located in your home folder's `.gemini` path.

## Steps

1. Create the destination directory if it doesn't already exist
```bash
mkdir -p ~/.gemini/antigravity/global_workflows
```

2. Copy all Markdown workflow files to the global directory
```bash
cp ./*.md ~/.gemini/antigravity/global_workflows/
```

3. Display the destination content for confirmation
```bash
ls -F ~/.gemini/antigravity/global_workflows/
```

## Usage

Simply say: "/sync-global" or "sync global"
