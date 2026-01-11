---
description: Guidance on using the Gemini CLI for automated tasks and code reviews
version: 1.1.0
---

# Gemini CLI Helper Workflow
**Last Updated: 2026-01-11**

This document provides guidance on how to effectively use the `gemini-cli` for automated tasks, when to delegate to it, and how to handle common configuration issues.

## Delegating to Gemini CLI

Delegating tasks to the `gemini-cli` is most effective when:
- **Batch Processing**: you need to apply the same logical change (e.g., refactoring for cross-platform support) across multiple files.
- **Independent Reviews**: you want a "second pair of eyes" to review a git diff or specific file without occupying the main agent's context.
- **Standardization**: you want to enforce project-wide rules or formatting consistently.

### Effort vs. ROI
- **Low Effort**: simple code reviews (`git diff | gemini "review this"`).
- **Medium Effort**: targeted refactoring with file write access (`cat file | gemini --approval-mode auto_edit "refactor this"`).
- **High Effort**: complex multi-file logic. for these, it is often better to use the main agent directly unless modularity is required.

## Context & Quota Management

Using the CLI offloads 'token-heavy' tasks (like reading large logs or diffs), which keeps the main agent's context window lean, improves response speed, and prevents 'forgetting'. It also effectively uses a separate output/usage stream.

## Technical Learnings

### 1. Tool Registry & Approval Modes
The `gemini-cli` restricts available tools based on the active `--approval-mode`. if an expected tool like `run_shell_command` is missing from the registry, it is likely due to the approval level.

- **Default (Read-only)**: only safe tools like `read_file` or `search_file_content` are available.
- **`--approval-mode auto_edit`**: enables file-writing tools (`write_file`, `replace`).
- **`--approval-mode yolo` or `-y`**: enables all tools, including `run_shell_command`.

### 2. Common Errors
- **"Tool not found in registry"**: occurs when the agent tries to use a tool that hasn't been enabled via approval modes or MCP extensions.
- **Non-Interactive Failure**: some tools may fail or be automatically disabled when the CLI is used in a piped/non-interactive context unless `--yolo` is used.

## Efficiency Tips

To get the most out of the subagent:
1. **Pipe for Immediate Context**: instead of asking the subagent to "find file X and review it," use `cat X | gemini "review this"`. this provides the content instantly without the agent needing to search the filesystem.
2. **Use `-y` for Tool Automation**: for any task that requires writing files or running commands in a script, always use `--approval-mode yolo` (or `-y`) to skip confirmation prompts.
3. **Keep Tasks Stateless**: the CLI is best for tasks that can be completed in a single turn without needing deep historical context from your main chat.
4. **Leverage Non-Interactive Mode**: piping to `gemini` is faster for one-shot tasks compared to entering interactive mode.

## Power User Recipes

### 1. Conventional Commit Message
```bash
git diff --staged | gemini "Create a conventional commit message for these changes."
```

### 2. Boilerplate Test Generation
```bash
cat <file> | gemini --approval-mode auto_edit "Generate unit tests for this file using [framework]"
```

### 3. Log & Error Triage
```bash
cat build.log | gemini "Filter these logs for unique errors and suggest fixes."
```

### 4. Rule Audit (Style Police)
```bash
cat <file> | gemini "Audit this file against the rules in GEMINI.md, focusing on lowercase comments and formatting."
```

### 5. Shell Translation
```bash
cat <bash_script> | gemini --approval-mode auto_edit "Translate this to a PowerShell script."
```

## Usage

Simply say: "How do I use gemini-cli?" or "/gemini-cli-helper"
