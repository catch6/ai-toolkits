# AI Toolkits

A collection of skills for AI agents. Skills are packaged instructions and scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### git-commit

Create Git commits following the Conventional Commits specification. Makes commits easy to review and safe to ship.

**Install:**
```sh
npx skills add https://github.com/catch6/ai-toolkits --skill git-commit
```

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

## Available Commands

### commit

Create Git commits with Conventional Commits format. This is a command template that pre-fills git status and diff context.

**Use when:**
- Quick commit without full skill workflow
- Agent needs pre-filled git context

## License

MIT
