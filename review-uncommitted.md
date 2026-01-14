---
description: Review uncommitted changes (staged and unstaged)
version: 1.0.0
---

# Review Uncommitted Changes
**Last Updated: 2026-01-13**

// turbo
1. Show the status of uncommitted changes:
   git status --short

// turbo
2. Show the diff of all uncommitted changes (staged + unstaged):
   git diff HEAD

3. Review the changes for:
   - potential bugs or logic errors
   - code style and consistency
   - missing error handling
   - opportunities for simplification
   - any TODO or FIXME items that should be addressed

4. Provide a summary with actionable feedback.
