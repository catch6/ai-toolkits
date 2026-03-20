---
name: git-commit
description: 'Use when user asks to commit changes, create a git commit'
---

# Git Commit

## Context

### Current git status (includes branch and untracked files)
<git-status>
!`git status`
</git-status>

### Staged and unstaged changes
<git-diff>
!`git diff HEAD`
</git-diff>

## Your task

Analyze the diff and git status, then stage and commit changes directly — no confirmation, no extra text output.

1. **Nothing to commit** → inform user, stop
2. **Secrets detected** (.env, credentials.json, private keys) → skip those files, warn user
3. **Single logical unit** → one commit
4. **Multiple logical units** → autonomously split into multiple commits with semantic grouping
5. **Untracked files** (in status but not in diff) → review filenames, stage appropriate ones
6. Stage with `git add <specific-files>` (never `git add -A` or `git add .`)

## Commit message format

- **Convention**: Conventional Commits — `feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`, etc.
- **Language**: Type prefix and scope in English, description in Chinese (e.g. `feat(auth): 添加用户登录功能`)
- **HEREDOC**: Always use HEREDOC for correct multi-line handling:
  ```bash
  git commit -m "$(cat <<'EOF'
  feat(scope): 描述
  EOF
  )"
  ```

## Git safety

- **NEVER** force push to main/master
- **NEVER** skip hooks (--no-verify) unless user explicitly asks
- **NEVER** run destructive commands (--force, reset --hard) without explicit request
- **NEVER** update git config
- Hook failure → fix the issue, then create a **NEW** commit (never amend)
