---
name: git-commit
description: 'Use when user asks to commit changes, create a git commit'
---

# Git Commit

## Context

<git-status>
!`git status --porcelain --branch`
</git-status>

<git-diff-stat>
!`git diff --stat HEAD 2>/dev/null || echo "(no commits yet — all files are new)"`
</git-diff-stat>

<git-log>
!`git log --oneline -5 2>/dev/null || echo "(no commits yet)"`
</git-log>


## Diff strategy

Read the **last line** of `<git-diff-stat>` for total insertions/deletions. Then:

| Condition | Action |
|---|---|
| **≤ 800 lines changed** | `git diff HEAD` — read full diff |
| **> 800 lines changed** | Stat + status is enough. Only `git diff HEAD -- <file>` on ambiguous files |
| **No commits yet** (`git-diff-stat` shows "no commits yet") | Treat all files as new; use `git diff --cached --stat` after staging to assess size |
| **All deletions** (status shows only ` D` or `D `) | No diff needed — file names tell the story |
| **Only untracked files** (not in stat) | Only `cat` small/ambiguous ones; clear names need no reading |
| **Binary files** | Skip diff, note in commit message |

When splitting into multiple commits and total > 800 lines, `git diff HEAD -- <group-of-files>` per logical group instead of full diff.

## Stage and commit

1. **Nothing to commit** → inform user, stop
2. **Single logical unit** → one commit
3. **Multiple logical units** → split into multiple commits with semantic grouping
4. **Untracked files** → review names, stage appropriate ones
5. `git add <specific-files>` only (never `git add -A` or `git add .`)

## Commit message

- Conventional Commits: `feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`, etc.
- Type/scope in English, description in Chinese: `feat(auth): 添加用户登录功能`
- 10+ files → add body listing key changes
- Always HEREDOC:
  ```bash
  git commit -m "$(cat <<'EOF'
  type(scope): 描述

  - 变更说明
  EOF
  )"
  ```

## Safety

- **NEVER** force push, skip hooks, run destructive commands, or update git config without explicit request
- Hook failure → fix issue, create **NEW** commit (never amend)
