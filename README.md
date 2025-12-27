# Agent Workflows

A collection of optimized Git workflows designed for agent-driven development. These workflows help automate common tasks like pushing changes, managing branches, and keeping your local environment in sync with the remote.

## Available Workflows

| Command | Description |
| :--- | :--- |
| `/amend-push` | Stages all modified files, amends them to the last commit, and force-pushes. |
| `/new-feature` | Fetches the latest code from `origin/main` and creates a fresh feature branch. |
| `/fetch-reset` | Fetches from the remote and hard-resets your local branch to match it (discards local changes). |
| `/rebase-main` | Rebases your current feature branch onto the latest `origin/main`. |
| `/squash-push` | Squashes all commits on your branch into one and force-pushes with a custom message. |
| `/pr-summary` | Generates a concise summary of all changes in your branch compared to `origin/main`. |
| `/undo-last-commit` | Un-commits the last change but keeps your files staged for quick edits. |
| `/cleanup-branches` | Identifies and deletes local branches that have already been merged into `main`. |
| `/sync-global` | Copies all workflows from this repository to your global `~/.gemini/antigravity/global_workflows/` directory. |

## Global Sync

To make these workflows available across all your projects, use the `/sync-global` command. This will copy the `.md` files to:
`~/.gemini/antigravity/global_workflows/`

## Usage

Simply invoke the command by name in your chat (e.g., "/amend-push") or describe the action you want to take. The agent will read the corresponding `.md` file and execute the steps.
