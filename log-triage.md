---
description: Analyze logs to identify unique errors and suggest fixes
version: 1.0.0
---

// turbo-all

# Log Triage Workflow
**Last Updated: 2026-01-11**

This workflow uses the Gemini CLI to process large log files, filtering for unique error signatures and providing troubleshooting advice.

## Steps

### Bash (macOS/Linux)
```bash
# triage a log file (replace <log_file>)
cat <log_file> | gemini "Analyze these logs. filter for unique error messages, identify potential root causes, and suggest specific troubleshooting steps."
```

### PowerShell (Windows)
```powershell
# triage a log file (replace <log_file>)
Get-Content <log_file> | gemini "Analyze these logs. filter for unique error messages, identify potential root causes, and suggest specific troubleshooting steps."
```

## Usage

Simply say: "/log-triage" or "triage logs"
