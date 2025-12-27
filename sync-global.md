---
description: Sync workflows and agent rules to global ~/.gemini directory
version: 2.0.0
---

// turbo-all

# Global Sync Workflow
**Last Updated: 2025-12-28**

Syncs all `.md` workflow files and the `GEMINI.md` agent rules file from this repository to the global `~/.gemini` directory structure.

## Steps

1. Create the workflows destination directory if needed
```bash
mkdir -p ~/.gemini/antigravity/global_workflows
```

2. Copy all workflow files to the global directory
```bash
ls *.md | grep -vE "README.md|GEMINI.md" | xargs -I {} cp {} ~/.gemini/antigravity/global_workflows/
```

3. Copy GEMINI.md agent rules to ~/.gemini (overwrites existing)
```bash
cp ./GEMINI.md ~/.gemini/GEMINI.md
```

4. Confirm synced files
```bash
echo "=== Workflows ===" && ls ~/.gemini/antigravity/global_workflows/*.md && echo "" && echo "=== Agent Rules ===" && cat ~/.gemini/GEMINI.md
```

## Usage

Simply say: "/sync-global" or "sync global"
