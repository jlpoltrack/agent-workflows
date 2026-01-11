---
description: Audit files for adherence to GEMINI.md rules and project style
version: 1.0.0
---

// turbo-all

# Project Style Audit Workflow
**Last Updated: 2026-01-11**

This workflow audits one or more files against the project-defined rules in `GEMINI.md`, focusing on lowercase comments, accessibility rules, and formatting.

## Steps

### Bash (macOS/Linux)
```bash
# audit a specific file (replace <file>)
cat <file> | gemini "Audit this file against the rules in GEMINI.md. focus on lowercase comments, date accuracy, and formatting rules. list any violations found."
```

### PowerShell (Windows)
```powershell
# audit a specific file (replace <file>)
Get-Content <file> | gemini "Audit this file against the rules in GEMINI.md. focus on lowercase comments, date accuracy, and formatting rules. list any violations found."
```

## Usage

Simply say: "/style-audit" or "audit style"
