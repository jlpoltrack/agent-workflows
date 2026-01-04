---
description: Stage, amend, and force-push changes to the remote
version: 1.3.0
---

// turbo-all

# Amend and Force-Push Workflow
**Last Updated: 2026-01-09**

This workflow stages all modified files, amends them to the last commit, and force-pushes the current branch to its upstream remote repository. Optimized for PowerShell/Windows.

## Steps

1. Execute Amend and Force-Push
```powershell
$branch = git branch --show-current
$remotes = git remote
$remoteCount = $remotes.Count

if ($remoteCount -eq 1) {
    $remote = $remotes
} else {
    $remote = $remotes | Select-String -Pattern "^jlp$" -CaseInsensitive | Select-Object -First 1
    if (!$remote) {
        $remote = $remotes[0]
    }
}

git add -A
git commit --amend --no-edit --quiet
git push --force-with-lease $remote $branch --quiet

Write-Host "Outcome: Amended and Pushed | Branch: $branch | Remote: $remote"
```

## Usage

Simply say: "/amend-push" or "amend and push"