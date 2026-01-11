---
description: Stage, amend, and force-push changes to the remote
version: 1.4.0
---

// turbo-all

# Amend and Force-Push Workflow
**Last Updated: 2026-01-11**

This workflow stages all modified files, amends them to the last commit, and force-pushes the current branch to its upstream remote repository. Supports Bash (macOS/Linux) and PowerShell (Windows).

## Steps

### Bash (macOS/Linux)
```bash
branch=$(git branch --show-current)
remotes=$(git remote)
remote_count=$(echo "$remotes" | grep -c '^')

if [ "$remote_count" -eq 1 ]; then
    remote=$(echo "$remotes" | head -n 1)
else
    remote=$(echo "$remotes" | grep -i "^jlp$" | head -n 1)
    if [ -z "$remote" ]; then
        remote=$(echo "$remotes" | head -n 1)
    fi
fi

git add -A
git commit --amend --no-edit --quiet
git push --force-with-lease "$remote" "$branch" --quiet

echo "Outcome: Amended and Pushed | Branch: $branch | Remote: $remote"
```

### PowerShell (Windows)
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