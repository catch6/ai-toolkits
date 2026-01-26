---
name: commit-work
description: Create high-quality git commits. review/stage intended changes, split into logical commits, and write clear commit messages (including Conventional Commits). Use when the user asks to commit, craft a commit message, stage changes, or split work into multiple commits.
---

# Commit Work

## Goal
Make commits that are easy to review and safe to ship:
- only intended changes are included
- commits are logically scoped (split when needed)
- commit messages describe what changed and why

## Inputs to ask for (if missing)
- Single commit or multiple commits? (If unsure: default to multiple small commits when there are unrelated changes.)
- Commit style: Conventional Commits are required.
- Any rules: max subject length, required scopes.

## Workflow (checklist)
1) Inspect the working tree before staging
   - `git status`
   - `git diff` (unstaged)
   - If many changes: `git diff --stat`
2) Decide commit boundaries (split if needed)
   - Split by: feature vs refactor, backend vs frontend, formatting vs logic, tests vs prod code, dependency bumps vs behavior changes.
   - If changes are mixed in one file, plan to use patch staging.
3) Stage only what belongs in the next commit
   - Prefer patch staging for mixed changes: `git add -p`
   - To unstage a hunk/file: `git restore --staged -p` or `git restore --staged <path>`
4) Review what will actually be committed
   - `git diff --cached`
   - Sanity checks:
     - no secrets or tokens
     - no accidental debug logging
     - no unrelated formatting churn
5) Describe the staged change in 1-2 sentences (before writing the message)
   - "What changed?" + "Why?"
   - If you cannot describe it cleanly, the commit is probably too big or mixed; go back to step 2.
6) Write the commit message
   - Use Conventional Commits (required):
     - `type(scope): <Chinese summary>`
     - blank line
     - body (Chinese, describe what/why, markdown list)
     - footer (Chinese, for BREAKING CHANGE) if needed
   - type and scope MUST be English, all other parts MUST be Chinese
   - Prefer an editor for multi-line messages: `git commit -v`
7) Commit directly without user confirmation
   - Execute `git commit` immediately after review, no user confirmation needed
8) Run the smallest relevant verification
   - Run the repo's fastest meaningful check (unit tests, lint, or build) before moving on.
9) Repeat for the next commit until the working tree is clean

## Deliverable
Provide:
- the final commit message(s)
- a short summary per commit (what/why)
- the commands used to stage/review (at minimum: `git diff --cached`, plus any tests run)

## Commit message template (Conventional Commits)

```text
<type>(<scope>): <Chinese summary>

<What changed - Chinese>
<Why it changed - Chinese>

<BREAKING CHANGE: Chinese description (if needed)>
```

Example:
```text
feat(auth): 添加用户登录功能

- 实现基于JWT的用户认证机制
- 支持邮箱和手机号两种登录方式

BREAKING CHANGE: 移除旧版session认证，需要重新登录
```

Notes:
- type/scope MUST be English
- summary/body/footer MUST be Chinese
- Use imperative mood for summary ("添加", "修复", "移除", "重构")
- Body focuses on behavior and intent, not implementation details; use list format with `-` prefix
- For breaking changes: use `!` in header and/or add `BREAKING CHANGE:` footer
