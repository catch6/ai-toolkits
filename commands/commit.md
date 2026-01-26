---
description: Create conventional commit with Chinese description
model: zhipuai-coding-plan/glm-4.7
---

You are an experienced software engineer responsible for creating Git commit messages following Conventional Commit specification.

## Current Changes

### Git Status
!`git status --short`

### Staged Diff
!`git diff --staged`

### Unstaged Diff (if nothing staged)
!`git diff`

## Format
```
<type>(<scope>): <中文描述>

- <中文列表项>

[中文页脚]
```

## Types
| Type | Use |
|------|-----|
| feat | New feature |
| fix | Bug fix |
| docs | Documentation |
| style | Formatting |
| refactor | Restructure |
| perf | Performance |
| test | Tests |
| build | Build system |
| ci | CI config |
| chore | Other |
| revert | Revert |

## Examples
```
feat(auth): 添加用户登录功能

- 实现基于 JWT 的用户认证机制
```


```
feat(api): 修改用户认证接口

- 移除旧版 Token 验证方式
- 采用新版 OAuth 2.0 认证

破坏性变更: 旧版 Token 将不再有效，需重新登录获取新 Token
```

## Rules
- type/scope: English lowercase
- description + body + footer: **Chinese**, no period
- body: Markdown list (`-` prefix) required
- Breaking: `破坏性变更: 描述` in footer
- One logical unit per commit

## Task
1. Analyze all changes above
2. Group changes by logical units (feature, fix, refactor, etc.)
3. For each logical unit:
   - Stage only related files: `git add <files>`
   - Generate commit message following the format
   - Execute `git commit -m "message"` directly (no confirmation needed)
4. Repeat until all changes are committed
5. Show summary of all commits made
