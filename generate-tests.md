---
description: Generate unit tests for a specified file
version: 1.0.0
---

// turbo-all

# Unit Test Generation Workflow
**Last Updated: 2026-01-11**

This workflow delegates the generation of unit tests to the Gemini CLI. It is ideal for creating boilerplate tests for new components or logic.

## Steps

### Bash (macOS/Linux)
```bash
# generate tests for a specific file (replace <file>)
cat <file> | gemini --approval-mode auto_edit "Generate a comprehensive suite of unit tests for this file. use the project's preferred testing framework if detected, otherwise default to a standard one."
```

### PowerShell (Windows)
```powershell
# generate tests for a specific file (replace <file>)
Get-Content <file> | gemini --approval-mode auto_edit "Generate a comprehensive suite of unit tests for this file. use the project's preferred testing framework if detected, otherwise default to a standard one."
```

## Usage

Simply say: "/generate-tests" or "generate tests for [file]"
