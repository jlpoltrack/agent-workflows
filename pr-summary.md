---
description: Generate a summary of changes against origin/main
version: 1.1.0
---

// turbo-all

# PR Summary Workflow
**Last Updated: 2026-01-11**

This workflow analyzes the differences between your current branch and the upstream `main` branch to help generate a PR description.

## Steps

1. Show changes summary
```bash
BRANCH=$(git branch --show-current)

# remote detection with fallback: jlp -> origin -> first available
if git remote | grep -qi "^jlp$"; then
  REMOTE="jlp"
elif git remote | grep -qi "^origin$"; then
  REMOTE="origin"
else
  REMOTE=$(git remote | head -n 1)
fi

if [ -z "$REMOTE" ]; then
  REMOTE="origin"
fi

echo "Branch: $BRANCH"
echo "Target: $REMOTE/main"
echo ""
echo "File Statistics:"
git diff --stat $REMOTE/main..$BRANCH
echo ""
echo "Detailed Changes:"
git diff $REMOTE/main..$BRANCH
```

```powershell
$Branch = git branch --show-current
$Remotes = git remote

if ($Remotes -contains "jlp") {
    $Remote = "jlp"
} elseif ($Remotes -contains "origin") {
    $Remote = "origin"
} else {
    $Remote = $Remotes | Select-Object -First 1
}

if (-not $Remote) {
    $Remote = "origin"
}

Write-Host "Branch: $Branch"
Write-Host "Target: $Remote/main"
Write-Host ""
Write-Host "File Statistics:"
git diff --stat $Remote/main..$Branch
Write-Host ""
Write-Host "Detailed Changes:"
git diff $Remote/main..$Branch
```

## Usage

Simply say: "/pr-summary"