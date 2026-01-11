---
description: Generate a conventional commit message from staged changes
version: 1.0.0
---

// turbo-all

# Conventional Commit Message Workflow
**Last Updated: 2026-01-11**

This workflow pipes the output of `git diff --staged` to the Gemini CLI to generate a high-quality, conventional commit message.

## Steps

### Bash (macOS/Linux)
```bash
git diff --staged | gemini "Create a conventional commit message for these changes. output only the commit message text."
```

### PowerShell (Windows)
```powershell
git diff --staged | gemini "Create a conventional commit message for these changes. output only the commit message text."
```

## Usage

Simply say: "/commit-msg" or "generate commit message"
