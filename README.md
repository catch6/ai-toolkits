# AI Toolkits

A collection of skills for AI agents. Skills are packaged instructions and scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### git-commit

Create Git commits following the Conventional Commits specification. Makes commits easy to review and safe to ship.

**Use when:**
- "Commit my changes"
- "Craft a commit message"
- "Stage changes"
- "Split work into multiple commits"

**Features:**
- Inspects working tree before staging (`git status`, `git diff`)
- Splits commits by logical boundaries (feature/refactor, backend/frontend, tests/prod)
- Supports patch staging for mixed changes (`git add -p`)
- Enforces Conventional Commits format with Chinese descriptions
- Sanity checks for secrets, debug logging, and formatting churn

**Commit message format:**
```
<type>(<scope>): <中文摘要>

- <变更内容>
- <变更原因>

BREAKING CHANGE: <如有破坏性变更>
```

**Example:**
```
feat(auth): 添加用户登录功能

- 实现基于JWT的用户认证机制
- 支持邮箱和手机号两种登录方式

BREAKING CHANGE: 移除旧版session认证，需要重新登录
```

## Available Commands

### commit

Create Git commits with Conventional Commits format. This is a command template that pre-fills git status and diff context.

**Use when:**
- Quick commit without full skill workflow
- Agent needs pre-filled git context

**Model:** `zhipuai-coding-plan/glm-4.7`

## Installation

```bash
npx add-skill catch6/ai-toolkits
```

## Usage

Skills are automatically available once installed. The agent will use them when relevant tasks are detected.

**Examples:**
```
Commit my changes
```
```
Help me split these changes into logical commits
```
```
Write a commit message for these changes
```

## Skill Structure

Each skill contains:
- `SKILL.md` - Instructions for the agent
- `scripts/` - Helper scripts for automation (optional)
- `references/` - Supporting documentation (optional)

## License

MIT
