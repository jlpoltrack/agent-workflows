---
description: Perform a git diff followed by a code review and refactoring suggestions
version: 1.1.0
---

// turbo-all

# Code Review and Refactoring Workflow
**Last Updated: 2026-01-11**

This workflow performs a git diff against the upstream main branch and then provides a detailed code review with refactoring suggestions.

## Steps

1. Get the diff against the target branch

### Bash
```bash
BRANCH=$(git branch --show-current)
REMOTE_COUNT=$(git remote | wc -l | tr -d ' ')

if [ "$REMOTE_COUNT" -eq 1 ]; then
  REMOTE=$(git remote)
else
  REMOTE=$(git remote | grep -i '^jlp$' | head -1)
  if [ -z "$REMOTE" ]; then
    REMOTE=$(git remote | head -1)
  fi
fi

echo "Branch: $BRANCH"
echo "Comparing against: $REMOTE/main"
echo ""

# Get the diff
git diff $REMOTE/main..$BRANCH
```

### PowerShell
```powershell
$branch = git branch --show-current
$remotes = @(git remote)
$remoteCount = $remotes.Count

if ($remoteCount -eq 1) {
    $remote = $remotes[0]
} else {
    $remote = $remotes | Where-Object { $_ -match "^jlp$" } | Select-Object -First 1
    if (-not $remote) {
        $remote = $remotes | Select-Object -First 1
    }
}

Write-Host "Branch: $branch"
Write-Host "Comparing against: $remote/main"
Write-Host ""

# Get the diff
git diff "$remote/main..$branch"
```

2. Review the code changes
Review the output of the previous step. Perform a thorough code review focusing on:
- Potential bugs or logic errors.
- Adherence to best practices and coding standards.
- Opportunities for refactoring to improve readability, maintainability, or performance.
- Documentation or testing needs.

Provide your findings and specific refactoring suggestions in a clear, structured format.

## Usage

Simply say: "/code-review" or "code review"